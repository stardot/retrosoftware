_[Sample Code Library](SampleCodeLibrary "wikilink") &gt; Fast multiplication routines_

# Fast multiplication routines in 6502

This is a copy of an article I posted to the Beeb mailing list yonks ago - perhaps it's useful to someone...?

## Multiplication by iteration and shifting

Normally, multiplication of two 8-bit numbers can be achieved with a little routine such as this:

<tt>

`.multiply`

`\ Multiplies A*X, and stores result in product/product+1`

`CPX #0:BEQ zero`

`DEX:STX product+1`

`LSR A:STA product`

`LDA #0`

`BCC s1:ADC product+1:.s1 ROR A:ROR product`

`BCC s2:ADC product+1:.s2 ROR A:ROR product`

`BCC s3:ADC product+1:.s3 ROR A:ROR product`

`BCC s4:ADC product+1:.s4 ROR A:ROR product`

`BCC s5:ADC product+1:.s5 ROR A:ROR product`

`BCC s6:ADC product+1:.s6 ROR A:ROR product`

`BCC s7:ADC product+1:.s7 ROR A:ROR product`

`BCC s8:ADC product+1:.s8 ROR A:ROR product`

`STA product+1`

`RTS`

`.zero`

`STX product:STX product+1`

`RTS`

</tt>

This completes in an average of 113 cycles (excluding the multiply by zero special case) - not bad, but it's possible to do better, provided you're happy to set aside some space for some tables...

## Faster multiplication by table lookup

There is a method which yields the product of two values from the difference between two squares.

Mathematically:

<tt>

` (a+b)^2 = a^2 + b^2 + 2ab     --> (I)`

` (a-b)^2 = a^2 + b^2 - 2ab     --> (II)`

</tt>

(I) minus (II) gives:

<tt>

` (a+b)^2 - (a-b)^2 = 4ab`

</tt>

or, in other words:

<tt>

`       (a+b)^2     (a-b)^2`

` ab =  -------  -  -------`

`          4           4`

</tt>

So this means we can store a table of f(n) = n^2 / 4 for n = 0..510, and then can achieve multiplication via a single 16-bit subtract! In reality, we use 4 lookup tables; 2 for the LSB/MSBs of the 16-bit value when n is less than 256, and a further 2 for when n is 256 or greater.

We can divide by 4 without worrying about truncation, because we know that (a+b)^2 - (a-b)^2 will always be a multiple of 4, therefore we lose no information or accuracy by discarding the lower 2 bits in the table itself.

Here's some code:

<tt>

` 10 sqrlo256%=&900`

` 20 sqrlo512%=&A00`

` 30 sqrhi256%=&B00`

` 40 sqrhi512%=&C00`

` 50 :`

` 60 FOR N%=0 TO 255`

` 70 s256%=(N%*N%) DIV 4`

` 80 s512%=((N%+256)*(N%+256)) DIV 4`

` 90 N%?sqrlo256%=s256% AND 255`

`100 N%?sqrhi256%=s256% DIV 256`

`110 N%?sqrlo512%=s512% AND 255`

`120 N%?sqrhi512%=s512% DIV 256`

`130 NEXT`

`140 :`

`150 num1=&70:num2=&71:result=&72`

`160 FOR N%=0 TO 2 STEP 2:P%=&700:[OPT N%`

`170 .mult`

`180 SEC:LDA num1:SBC num2:BCS positive`

`190 EOR #255:ADC #1:.positive TAY`

`200 CLC:LDA num1:ADC num2:TAX`

`210 BCS morethan256:SEC`

`220 LDA sqrlo256%,X:SBC sqrlo256%,Y:STA result`

`230 LDA sqrhi256%,X:SBC sqrhi256%,Y:STA result+1`

`240 RTS`

`250 .morethan256`

`260 LDA sqrlo512%,X:SBC sqrlo256%,Y:STA result`

`270 LDA sqrhi512%,X:SBC sqrhi256%,Y:STA result+1`

`280 RTS`

`290 ]:NEXT`

`300 :`

`310 !result=0`

`320 REPEAT`

`330 ?num1=RND(256)-1:?num2=RND(256)-1:CALL mult`

`340 PRINT;?num1;"*";?num2;"=";!result;" (";?num1*?num2;")"`

`350 IF ?num1*?num2<>!result:END`

`360 UNTIL FALSE`

</tt>

So there's a routine which achieves an 8 bit \* 8 bit multiplication in just 55 cycles - over twice the speed of the original routine. The only problem with this is the amount of table space required - 1k.

It turns out that we can reduce the table space by 256 bytes by unifying sqrlo256 and sqrlo512. They are virtually the same, apart from that sqrlo512(n) = sqrlo256(n) EOR &80 when n is odd.

Which leads us to the following space optimisation:

<tt>

` 10 sqrlo%=&900`

` 20 sqrhi256%=&A00`

` 30 sqrhi512%=&B00`

` 40 :`

` 50 FOR N%=0 TO 255`

` 60 s256%=(N%*N%) DIV 4`

` 70 s512%=((N%+256)*(N%+256)) DIV 4`

` 80 N%?sqrlo%=s256% AND 255`

` 90 N%?sqrhi256%=s256% DIV 256`

`100 N%?sqrhi512%=s512% DIV 256`

`110 NEXT`

`120 :`

`130 num1=&70:num2=&71:result=&72`

`140 FOR N%=0 TO 2 STEP 2:P%=&700:[OPT N%`

`150 .mult`

`160 SEC:LDA num1:SBC num2:BCS positive`

`170 EOR #255:ADC #1:.positive TAY`

`180 CLC:LDA num1:ADC num2:TAX`

`190 BCS morethan256`

`200 LDA sqrhi256%,X:STA result+1`

`210 LDA sqrlo%,X:SEC:BCS lessthan256`

`220 .morethan256`

`230 LDA sqrhi512%,X:STA result+1`

`240 TXA:AND #1:BEQ skip:LDA #&80:.skip`

`250 EOR sqrlo%,X:.lessthan256`

`260 SBC sqrlo%,Y:STA result`

`270 LDA result+1:SBC sqrhi256%,Y:STA result+1`

`280 RTS`

`290 ]:NEXT`

`300 :`

`310 !result=0`

`320 REPEAT`

`330 ?num1=RND(256)-1:?num2=RND(256)-1:CALL mult`

`340 PRINT;?num1;"*";?num2;"=";!result;" (";?num1*?num2;")"`

`350 IF ?num1*?num2<>!result:END`

`360 UNTIL FALSE`

</tt>

...which is an average of about 67 cycles, i.e. still substantially better than the original routine.

I wish I'd thought of this trick when I was writing multiplication-intensive demos years ago...

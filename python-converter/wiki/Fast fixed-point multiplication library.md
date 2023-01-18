_[Sample Code Library](SampleCodeLibrary "wikilink") &gt; Fast fixed-point multiplication library_

# Fast fixed-point multiplication library in 6502, using base 127 fixed-point values

Beebs don't multiply numbers very well. Even with the kind of routine I demonstrated [here](Fast_multiplication_routines "wikilink"), we're still limited to multiplying unsigned numbers and getting an unsigned result.

Now, there are many occasions (e.g. in a 3D game) where you want to be able to do the equivalent of:

<tt>

`x = r * SIN(angle)`

</tt>

Obviously, SIN(angle) is a fractional value between -1.0 and 1.0, and one thing the Beeb definitely _does not_ excel in is floating point! Other relatively modern platforms which don't have floating point hardware either (e.g. the Nintendo DS) get around this limitation by storing the sine value multiplied by a constant, fetching this when required, multiplying the two values, and then dividing afterwards by the same constant:

<tt>

`x = r * (SIN(angle) * 256) / 256`

</tt>

If the constant is a nice round power of two, this is a cheap operation. This representation of a fractional value multiplied by a constant is called 'fixed point'.

Well, we know all that anyway. Wouldn't it be nice if we could do this on a Beeb? Here I present one possible way of achieving this in 6502, which maximises precision whilst requiring only 8-bit values.

## Possible fixed-point representations

Let's suppose we only need to be able to represent values between -1.0 and 1.0. This is often all we need as it encompasses all the values of a sine/cosine table, a reciprocal table (for doing quick divisions), and even allows quick interpolation between two values, e.g. `x` `=` `start` `*` `t` `+` `end` `*` `(1-t)`. As long as we can quickly multiply by any value between -1.0 and 1.0 with reasonable precision, we fulfil our remit! If we could find a way to store this fixed point value in 8 bits, it would be great, as we already have a super-fast table based multiplication algorithm (as discussed on the other wiki page) which multiplies 8-bit values.

### Fixed-point with 8 fractional bits

How about the approach mentioned above? Multiplying all the fractional values by 256, so that 1.0 is represented by 256, 0.5 by 128, -1.0 by -256, and so on. This would be an efficient representation because in order to multiply an 8-bit value by one of these fixed-point values, we just do a regular 8-bit \* 8-bit multiply, and then throw away the bottom 8 bits of the result. The top 8 bits are the answer!

Seems simple - apart from that there's a small problem: values between -256 and 256 don't fit into 8 bits. In fact, we need 10 bits in order to represent this entire range, and there's a lot of redundancy there, because in fact with 10 bits we can represent values between -512 and 511.

I'm not going to explore this approach in this article, because, while providing reasonably good precision, it won't work in a straightforward way with our existing multiply routine, and the aim here is to produce a very fast fixed-point multiplication routine, hopefully requiring only 8-bit values.

### Fixed-point with 7 fractional bits

So how about multiplying by 128 instead? Like this, -1.0 is represented by -128 and 1.0 is represented by 128. The problem here is to do with the asymmetry of the two's complement representation - in 8 bits, we can only store values from -128 to +127, which means that if we use 128 as our fixed point constant, we can happily store -1.0, but we can't reach 1.0. This is going to be a problem, so let's throw this idea away straight away.

### Fixed-point with 6 fractional bits

So, finally, how about multiplying by 64? Then, values between -64 and +64 represent our required range of -1.0 to +1.0, and this fits easily into a byte. So then, when we want to get the result, it's simply a case of calculating `a*b` `/` `64`, where of course the division can be performed by a few simple shifts. This approach would work fine, but this is starting to become very imprecise - the fractional part is only represented to the nearest 1/64th - and, what's more, there are a lot of wasted values which we will probably not use (-128 to -65, and 65 to 127 - all representing values less than -1.0 and greater than 1.0 respectively).

At this point, I realised that, thinking outside the box a bit, we didn't need to limit our fixed-point constant to a power of two value. In fact, we could choose anything we wanted, because we already perform our multiplication with lookup tables.

## Base 127 fixed-point representation

It sounds complicated, but the premise is actually very simple: use 127 as our fixed-point constant. Thus -1.0 is represented by -127, and +1.0 is represented by +127. When we want to calculate a \* b (where b is a fixed-point value), we just calculate:

<tt>

`result = a * b / 127`

</tt>

Division by 127? Yuk! But never fear: we won't actually have to divide by 127 by hand. In fact we will build lookup tables which are predivided by 127.

Recall how the multiplication routine works:

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

` ab = f(a+b) - f(a-b)`

</tt>

where: <tt>

`         (a+b)^2`

` f(x) =  -------`

`            4`

</tt>

So, we build a lookup table of f(x) for x=0..255, and that's all there is to it!

Now, imagine if we were to divide the values in this lookup table by a further 127 - that way, we would get this division thrown in for free:

<tt>

` ab / 127 = f(a+b) - f(a-b)`

</tt>

where: <tt>

`         (a+b)^2`

` f(x) =  -------`

`          127*4`

</tt>

The next thing we need to do is make sure it works with signed inputs. The mjultiply method we're going to use will only work with unsigned inputs, so we have to do some other stuff in order that it works well.

The naïve solution is to write code like this:

- Remember sign of (val1 EOR val2)

- If sign of val1 is negative, negate val1.

- If sign of val2 is negative, negate val2.

- Multiply val1 \* val2.

- If the sign we remembered was negative, negate the result.

However, this costs cycles, and also means that the case where any of the inputs is negative is slower than the case where both inputs are positive.

A better solution is to do the table lookup and subtract in different ways, depending on the two signs of the inputs (4 different possibilities).

For example, in the cases where the result needs to be negated, we do the table lookup with positive indices as required, but then reverse the order of the subtraction, like this:

<tt>

` a*b = f(a-b')-f(a+b')  where b' is -b`

</tt>

## Extending the algorithm to multiply bigger values by a fixed-point number

Will write this up sometime.

## Sample code

Here is the source code for all the multiplication routines so far (BeebAsm format):

<tt>

    \\  *******************************************************************************************

    \\  *

    \\  *  Fixed-point multiplication

    \\  *

    \\  *  Essentially this is a library of routines which multiply a signed 8- or 15-bit value

    \\  *  by a further signed 8-bit number, and divides the result by 127.

    \\  *

    \\  *  This means we can represent fractional values from -1.0 to 1.0 using the range -127 to

    \\  *  +127, with no loss of magnitude.

    \\  *

    \\  *  The multiplication technique used is the old favourite:

    \\  *

    \\  *      a*b = f(a+b) - f(|a-b|), where f(x) = a^2 / 4, with x = 0..255

    \\  *

    \\  *******************************************************************************************



    mulval1 = &70

    mulval2 = &71

    mulresult = &72





    ORG &4000



    .Start





    \\---------------------------------------------------------------------------------------------

    \\  Multiply X * cos(Y)

    \\

    \\  X is in the range -127..127, and can be thought of as a fixed-point number if you wish,

    \\      where 127 represents 1.0.

    \\  Y is an angle between 0..255, such that 360 degrees is represented by 256.

    \\

    \\  Result returned in A

    \\---------------------------------------------------------------------------------------------



    .S8_x_Cosine

        LDA CosineTable,Y

        TAY

        JMP S8_x_Fixed







    \\---------------------------------------------------------------------------------------------

    \\  Multiply X * sin(Y)

    \\

    \\  X is in the range -127..127, and can be thought of as a fixed-point number if you wish,

    \\      where 127 represents 1.0.

    \\  Y is an angle between 0..255, such that 360 degrees is represented by 256.

    \\

    \\  Result returned in A

    \\---------------------------------------------------------------------------------------------



    .S8_x_Sine

        LDA SineTable,Y

        TAY

        ; fall through







    \\---------------------------------------------------------------------------------------------

    \\  Multiply X * Y

    \\

    \\  Both X and Y are signed numbers in the range -127..127.

    \\  One or both of them is considered as a fixed-point number, where 127 represents 1.0.

    \\

    \\  Result returned in A

    \\

    \\  This routine takes an average of 58 cycles to execute (including the overhead of the

    \\  subroutine call).

    \\

    \\  The result is an approximation due to various rounding errors, but tests show that:

    \\      75% of the results are accurate to within +/-0.5

    \\      99% of the results are accurate to within +/-1.0

    \\

    \\  This should be ok for now!

    \\---------------------------------------------------------------------------------------------



    .S8_x_Fixed

    {

        STX mulval1                            ; store these two values, we will need to do

        STY mulval2                            ; arithmetic with them later

        CLC                                    ; clear C in anticipation



        TYA:BMI val2neg                        ; handle cases where val2 is negative



        \\ If we get here, val2 is positive



        TXA:BMI val1neg_val2pos



        \\ If we get here, val1 is positive and val2 positive.

        \\ This is the straightforward f(val1+val2) - f(|val1-val2|)



        ; On entry, A contains val1, C is clear

        .val1pos_val2pos

        ADC mulval2

        TAX                                    ; X = val1+val2 (in range 0..254)



        SEC

        LDA mulval1

        SBC mulval2                            ; val1-val2 (in range -127..127)

        BCS skipnegate                         ; see if val1-val2 was negative

        EOR #255                               ; if so negate it to yield a positive value

        ADC #1

        SEC                                    ; set C flag in anticipation

        .skipnegate

        TAY                                    ; Y = |val1-val2| (in range 0..127)



        LDA MultTableHigh,X                    ; C guaranteed to be set here

        SBC MultTableHigh,Y

        RTS



        \\ If we get here, val1 is negative and val2 is positive.

        \\ The method being used requires unsigned numbers, so we do the table lookup with -val1.

        \\ We would then need to negate the result at the end, but in order to save this,

        \\ we just reverse the subtraction of the two table lookups, i.e.

        \\     f(|val1-val2|) - f(val1+val2)

        \\ However, as we just said, we use -val1, so what we now get is:

        \\     f(|-(val1+val2)|) - f(val2-val1)

        \\   = f(|val1+val2|) - f(val2-val1)



        ; On entry, A contains val1, C is clear

        .val1neg_val2pos

        ADC mulval2                            ; val1+val2 (in range -127..127)

        BCS skipnegate2                        ; see if val1+val2 was negative

        EOR #255                               ; if so negate it to yield a positive value

        ADC #1

        SEC                                    ; set C flag in anticipation

        .skipnegate2

        TAX                                    ; X = |val1+val2| (in range 0..127)



        LDA mulval2                            ; C guaranteed to be set here

        SBC mulval1

        TAY                                    ; Y = val2-val1 (in range 0..254)



        SEC

        LDA MultTableHigh,X

        SBC MultTableHigh,Y

        RTS



        \\ If we get here, val2 is negative



        .val2neg

        TXA:BMI val1neg_val2neg



        \\ If we get here, val1 is positive and val2 is negative

        \\ This is similar to the last case; we need to negate the result, and do the table

        \\ lookup with -val2, so we end up with:

        \\     f(|val1+val2|) - f(val1-val2)



        ; On entry, A contains val1, C is clear

        .val1pos_val2neg

        ADC mulval2                            ; val1+val2 (in range -127..127)

        BCS skipnegate3                        ; see if val1+val2 was negative

        EOR #255                               ; if so negate it to yield a positive value

        ADC #1

        SEC                                    ; set C flag in anticipation

        .skipnegate3

        TAX                                    ; X = |val1+val2| (in range 0..127)



        LDA mulval1                            ; C guaranteed to be set here

        SBC mulval2

        TAY                                    ; Y = val1-val2 (in range 0..254)



        SEC

        LDA MultTableHigh,X

        SBC MultTableHigh,Y

        RTS



        \\ If we get here, val1 is negative and val2 is negative

        \\ As well as negating the result, we have to do the table lookup with -val1 and -val2.

        \\ So, this leaves us with:

        \\    f(-(val1+val2)) - f(|val2-val1|)



        ; On entry, A contains val1, C is clear

        .val1neg_val2neg

        ADC mulval2                            ; val1+val2 (in range -254..0)

        EOR #255

        ADC #0

        TAX                                    ; X = -(val1+val2) (in range 0..254)



        SEC

        LDA mulval2

        SBC mulval1                            ; val2-val1 (in range -127..127)

        BCS skipnegate4                        ; see if it was negative

        EOR #255                               ; negate it again if so

        ADC #1

        SEC                                    ; set C flag in anticipation

        .skipnegate4

        TAY                                    ; Y = |val2-val1| (in range 0..127)



        LDA MultTableHigh,X                    ; C guaranteed to be set here

        SBC MultTableHigh,Y

        RTS

    }

    .S8_x_Fixed_END







    \\---------------------------------------------------------------------------------------------

    \\  Multiply XA * cos(Y)

    \\

    \\  XA is a 15-bit signed number (in the range -16384..16383), A=lsb, X=msb

    \\  Y is an angle between 0..255, such that 360 degrees is represented by 256.

    \\

    \\  Result returned in XA (A=lsb, X=msb)

    \\---------------------------------------------------------------------------------------------



    .S15_x_Cosine

    {

        STA preserve+1

        LDA CosineTable,Y

        TAY

        .preserve LDA #0

        JMP S15_x_Fixed

    }







    \\---------------------------------------------------------------------------------------------

    \\  Multiply X * sin(Y)

    \\

    \\  XA is a 15-bit signed number (in the range -16384..16383), A=lsb, X=msb

    \\  Y is an angle between 0..255, such that 360 degrees is represented by 256.

    \\

    \\  Result returned in XA (A=lsb, X=msb)

    \\---------------------------------------------------------------------------------------------



    .S15_x_Sine

    {

        STA preserve+1

        LDA SineTable,Y

        TAY

        .preserve LDA #0

        ; fall through

    }







    \\---------------------------------------------------------------------------------------------

    \\  Multiply XA * Y

    \\

    \\  XA is a 15-bit signed number (in the range -16384..16383), A=lsb, X=msb

    \\  Y is a fixed-point number in the range -127..127 (representing -1.0..1.0)

    \\

    \\  Result returned in XA (A=lsb, X=msb)

    \\

    \\  This routine takes on average about 170 cycles to execute (including the overhead of the

    \\  subroutine call).

    \\---------------------------------------------------------------------------------------------



    .S15_x_Fixed

    {

        ; get high 8 bits (signed)

        STA loadval+1                          ; remember the lsb of val1 for later

        ASL A

        TXA

        ROL A                                  ; get bits 7-14 in A



        ; store the two multiplicands

        STA mulval1

        STY mulval2

        CLC                                    ; clear C in anticipation



        \\ Now we perform a similar version of the multiplication, but getting a

        \\ 16-bit result



        TYA:BMI val2neg                        ; handle cases where val2 is negative



        \\ If we get here, val2 is positive



        LDA mulval1:BMI val1neg_val2pos



        \\ If we get here, val1 is positive and val2 positive.



        ; On entry, A contains val1, C is clear

        .val1pos_val2pos

        ADC mulval2

        TAX                                    ; X = val1+val2 (in range 0..254)



        SEC

        LDA mulval1

        SBC mulval2                            ; val1-val2 (in range -127..127)

        BCS skipnegate                         ; see if val1-val2 was negative

        EOR #255                               ; if so negate it to yield a positive value

        ADC #1

        SEC                                    ; set C flag in anticipation

        .skipnegate

        TAY                                    ; Y = |val1-val2| (in range 0..127)

        BCS dohighmult



        \\ If we get here, val1 is negative and val2 is positive.



        ; On entry, A contains val1, C is clear

        .val1neg_val2pos

        ADC mulval2                            ; val1+val2 (in range -127..127)

        BCS skipnegate2                        ; see if val1+val2 was negative

        EOR #255                               ; if so negate it to yield a positive value

        ADC #1

        SEC                                    ; set C flag in anticipation

        .skipnegate2

        TAX                                    ; X = |val1+val2| (in range 0..127)



        LDA mulval2                            ; C guaranteed to be set here

        SBC mulval1

        TAY                                    ; Y = val2-val1 (in range 0..254)

        SEC

        BCS dohighmult



        \\ If we get here, val2 is negative



        .val2neg

        LDA mulval1:BMI val1neg_val2neg



        \\ If we get here, val1 is positive and val2 is negative



        ; On entry, A contains val1, C is clear

        .val1pos_val2neg

        ADC mulval2                            ; val1+val2 (in range -127..127)

        BCS skipnegate3                        ; see if val1+val2 was negative

        EOR #255                               ; if so negate it to yield a positive value

        ADC #1

        SEC                                    ; set C flag in anticipation

        .skipnegate3

        TAX                                    ; X = |val1+val2| (in range 0..127)



        LDA mulval1                            ; C guaranteed to be set here

        SBC mulval2

        TAY                                    ; Y = val1-val2 (in range 0..254)

        SEC

        BCS dohighmult



        \\ If we get here, val1 is negative and val2 is negative



        ; On entry, A contains val1, C is clear

        .val1neg_val2neg

        ADC mulval2                            ; val1+val2 (in range -254..0)

        EOR #255

        ADC #0

        TAX                                    ; X = -(val1+val2) (in range 0..254)



        SEC

        LDA mulval2

        SBC mulval1                            ; val2-val1 (in range -127..127)

        BCS skipnegate4                        ; see if it was negative

        EOR #255                               ; negate it again if so

        ADC #1

        SEC                                    ; set C flag in anticipation

        .skipnegate4

        TAY                                    ; Y = |val2-val1| (in range 0..127)



        \\ This calculates the result of (high 8 bits of val1) * val2

        \\ This is a 15-bit result



        .dohighmult

        LDA MultTableLow,X

        SBC MultTableLow,Y

        STA mulresult

        LDA MultTableHigh,X

        SBC MultTableHigh,Y

        CMP #128                               ; sign extend

        ROR A                                  ; shift the result down one bit, because

        STA mulresult+1                        ; it represents bits 7-14 of the result

        ROR mulresult                          ; plus a fractional amount



        \\ Get the bottom 7 bits - this is always an unsigned quantity.

        \\ We could just call the S8_x_Fixed multiply routine, but as an optimisation (to avoid

        \\ the JSR and to skip all the redundant checks for val1 being negative), we inline it,

        \\ which means we also skip all the setup stuff.

        \\ This routine will be used to perform perspective divides (as a reciprocal multiply),

        \\ and so called once per vertex - therefore any optimisation is good!



        .loadval LDA #0                        ; self-modified

        AND #127

        STA mulval1

        BIT mulval2

        CLC

        BMI val2neg2



        \\ This is the case where val1 is positive and val2 is positive



        ADC mulval2

        TAX                                    ; X = val1+val2 (in range 0..254)



        SEC

        LDA mulval1

        SBC mulval2                            ; val1-val2 (in range -127..127)

        BCS skipnegate5                        ; see if val1-val2 was negative

        EOR #255                               ; if so negate it to yield a positive value

        ADC #1

        SEC                                    ; set C flag in anticipation

        .skipnegate5

        TAY                                    ; Y = |val1-val2| (in range 0..127)

        JMP dolowmult



        \\ This is the case where val1 is positive and val2 is negative



        .val2neg2

        ADC mulval2                            ; val1+val2 (in range -127..127)

        BCS skipnegate6                        ; see if val1+val2 was negative

        EOR #255                               ; if so negate it to yield a positive value

        ADC #1

        SEC                                    ; set C flag in anticipation

        .skipnegate6

        TAX                                    ; X = |val1+val2| (in range 0..127)



        LDA mulval1                            ; C guaranteed to be set here

        SBC mulval2

        TAY                                    ; Y = val1-val2 (in range 0..254)

        SEC



        \\ This calculates the result of (low 7 bits of val1) * val2



        .dolowmult

        LDA MultTableHigh,X                    ; C guaranteed to be set here

        SBC MultTableHigh,Y

        TAX                                    ; put low 8 bits of the result into X

        LDA #0

        SBC #0

        TAY                                    ; put sign extended high bits into Y



        CLC                                    ; add this portion to the partial result

        TXA

        ADC mulresult

        STA mulresult

        TYA

        ADC mulresult+1

        TAX                                    ; return MSB in X

        LDA mulresult                          ; return LSB in A

        RTS

    }

    .S15_x_Fixed_END









    \\---------------------------------------------------------------------------------------------

    \\ Here are the multiplication tables, align them to a page boundary

    \\ 512 bytes in total... not so bad, really.



    ALIGN 256



    \\ Table used by the multiplication routine to perform (a*b)/127



    .MultTableHigh

    FOR n, 0, 255

        EQUB ((n*n / 4) * 256 / 127 + 0.5) DIV 256

    NEXT



    .MultTableLow

    FOR n, 0, 255

        EQUB ((n*n / 4) * 256 / 127 + 0.5) MOD 256

    NEXT



    \\ Sine/cosine table, values multiplied by 127

    \\ This is 320 bytes long.  It could be reduced if we did the cos lookup in a

    \\ slightly slower way.



    .SineTable

    CosineTable = SineTable + 64

    FOR n, 0, 255 + 64

        a = SIN(n/128*PI) * 127

        IF a >= 0

            EQUB INT(a + 0.5)

        ELSE

            EQUB INT(a - 0.5)

        ENDIF

    NEXT





    \\---------------------------------------------------------------------------------------------

    .End



    SAVE "Code", Start, End

</tt>

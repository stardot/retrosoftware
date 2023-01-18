## Denormalising a number

BBC BASIC stores reals (non-integers) in five-byte floating point format. The following code will convert a real to it's integer version, a process known as denormalisation.

<tt>

`   int=&70:exp=int+4                     :REM Returned integer`
`   real=exp+1                            :REM Pointer to real`
`   :`
`   \ Denormalise - Denormalise a number (convert real to integer)`
`   \ ============================================================`
`   \ On entry,  (real) => 5-byte floating point number`
`   \                   => exponent, mantissa hi, mid, mid, lo`
`   \ On exit,   (int)  =  denormalised integer version of real`
`   \            CC     =  conversion valid, no under/overflow`
`   \            CS     =  conversion invalid, under/overflow`
`   .Denormalise`
`   LDY #0                                :\ (real),Y => exp, man`
`   LDX #4                                :\ Five bytes to reorder and copy`
`   .DenormLp1`
`   LDA (real),Y:STA int,X:INY            :\ Copy and reverse into store`
`   DEX:BPL DenormLp1`
`   LDA exp:BEQ DenormOK                  :\ exp=00, real was zero`
`   LDA int+3:PHP:ORA #&80:STA int+3      :\ Save sign and put top bit in`
`   .DenormLp2`
`   LDA exp:CMP #&A0:BCS Denormalised     :\ Loop until denormalised`
`   ROR int+3:ROR int+2:ROR int+1:ROR int :\ Multiply mantissa by two`
`   BCS DenormOverflow                    :\ Drop out if run out of bits`
`   INC exp:BNE DenormLp2`
`   .Denormalised`
`   PLP:BPL DenormOK                      :\ Positive, return integer`
`   LDX #&FC                              :\ Negate for negative number`
`   .DenormNegate`
`   LDA #0:SBC int-&FC,X:STA int-&FC,X`
`   INX:BMI DenormNegate`
`   .DenormOK`
`   CLC:RTS                               :\ CLC = conversion valid`
`   .DenormOverflow`
`   PLP:SEC:RTS                           :\ SEC = conversion invalid`

</tt>

## Explanation

BBC BASIC stores real (non-integer) numbers in five bytes in a format known as "five-byte floating point". This splits the number into two components - a one-byte exponent and a four-byte mantissa.

All numbers, other than zero, can be expressed as m\*10^e. You may be familiar with this form known as exponential format. For example:

`   100 is 1*10^2`
`   5000 is 5*10^3`
`   0.5 is 5*10^-1.`

Exactly the same can be done using base 2, expressing numbers as m\*2^e, for example:

`   4 is 1*2^2`
`   -8 is -1*2^3`
`   12 is 1.5*2^3`
`   -0.5 is -1*2^-1`

In five-byte floating point format, the manitissa is multiplied or divided by 2, and the exponent reduced or increased, until the mantissa m is in the range 0.5 to 1, excluding 1, for example:

`   4 is 0.5*2^3`
`   -8 is -0.5*2^4`
`   12 is 0.75*2^4`
`   -0.5 is -0.5*2^0`

This means that the first bit of the mantissa is always 1. That means it can be used to hold the sign bit. To allow negative exponents, &80 is added to the exponent. BASIC stores the number in five bytes with the exponent first, followed by the mantissa, high byte to low byte. For example:

`   4 is exponent &83, mantissa &00, &00, &00, &00`
`   -8 is exponent &84, mantissa &80, &00, &00, &00`
`   12 is exponent &84, mantissa &C0, &00, &00, &00`
`   -0.5 is exponent &80, mantissa &00, &00, &00, &00`

Note that the mantissa is stored the opposite way round to an integer.

Zero is a special case and is stored as five zero bytes. Some versions of BBC BASIC extend this and use a zero exponent to indicate that the real actually holds an integer value. For example,

`   &00, &80, &00, &00, &00 is 128 (&80)`
`   &00, &FE, &FF, &FF, &FF is -2 (&FFFFFFFE)    `

To convert a real to an integer the mantissa must be multiplied by two until the exponent is zero (ie &80). For example, converting 0.5\*2^3 back to 4\*2^0.

You can only convert a real to an integer if the the real actually represents an integer. If the real is a non-integer, the code returns Carry set to indicate the real could not be converted.

See <http://mdfs.net/Info/Comp/6502/ProgTips>

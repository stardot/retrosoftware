# BIN/HEX to BCD (to Decimal)

Fast conversion of 16 bit numbers to BCD Binary Coded Decimal, that is 42 = &2A or 42 = &42 in BCD

Having written this code this morning and had a closer look at what is available, this is similar to an unwinding of Print decimal by J.G.Harston.

This code does as far as I can see (having just written it ;-) a very fast conversion from HEX/Binary to BCD - now I am wondering why you would want it!

You could just use BCD mode to keep scores and Print decimal for debugging, but maybe someone will find it interesting and it was a nice little project while I was waiting for the plumber!

The code works by having three tables for what the bits 15..12, 11..8 and 7..3 are as BCD, leaving bits 2..0 which are the same in hex as decimal (0..7)

The code copies the most significant values and then adds the other three (two from tables and the LSB & 7) - Job Done.

The code is wrapped in a SEI/CLI as this means that interrupts don't need to worry about the DECimal flag - something that all interrupts should do, but some code doesn't since it isn't part of the guarantees made on the Beeb (from what I can remember).

When I originally thought of this this morning, I did think of looping like Print decimal, but as this is supposed to be <i>game ready</i>, I didn't like the idea of worst case 64999 being converted and having to loop through subtractions nearly 40 times; so paid the old price of time vs memory and added the small (?) tables.

Here is the BeebAsm code, I will port it over to the Beeb, add some test code and post the code and an .ssd to the forums [1](http://www.retrosoftware.co.uk/forum/viewtopic.php?f=73&t=639).

<tt>

        \\ unless documented, AXY and CNVZ are undefined on exit, BID are unchanged (B=B I=I D=D)



        GUARD &5800

        ORG   &1400



    .BEGIN



    .MAIN

    {

    }



    bin_as_bcd = &70



    .bin_to_bcd \\ &yyxx to bin_to_bcd X=X \\ 99 bytes (+21 if bin_as_bcd not ZP)

    {

        sei \\ disable interrupts to avoid issues when using bcd

        sed

        tya

        pha

        lsr a : lsr a : lsr a : lsr a

        tay

        lda bits1512_b0,y

        sta bin_as_bcd+0

        lda bits1512_b1,y

        sta bin_as_bcd+1

        lda bits1512_b2,y

        sta bin_as_bcd+2

        pla

        and #&f

        tay

        clc

        lda bits118_b0,y

        adc bin_as_bcd+0

        sta bin_as_bcd+0

        lda bits118_b1,y

        adc bin_as_bcd+1

        sta bin_as_bcd+1

        lda #0

        adc bin_as_bcd+2

        sta bin_as_bcd+2

        txa

        lsr a : lsr a : lsr a

        tay

        clc

        lda bits73_b0,y

        adc bin_as_bcd+0

        sta bin_as_bcd+0

        lda bits73_b1,y

        adc bin_as_bcd+1

        sta bin_as_bcd+1

        lda #0

        adc bin_as_bcd+2

        sta bin_as_bcd+2

        txa

        and #7

        adc bin_as_bcd+0

        sta bin_as_bcd+0

        lda #0

        adc bin_as_bcd+1

        sta bin_as_bcd+1

        lda #0

        adc bin_as_bcd+2

        sta bin_as_bcd+2

        cld

        cli

        rts



    .bits1512_b2

        FOR n,0,&f000,&1000

        EQUB n DIV 10000

        NEXT

    .bits1512_b1

        FOR n,0,&f000,&1000

        EQUB (((n DIV 1000) MOD10) * 16) + ((n DIV 100) MOD 10)

        NEXT

    .bits1512_b0

        FOR n,0,&f000,&1000

        EQUB (((n DIV 10) MOD 10) * 16) + (n MOD 10)

        NEXT

    .bits118_b1

        FOR n,0,&f00,&100

        EQUB (((n DIV 1000) MOD10) * 16) + ((n DIV 100) MOD 10)

        NEXT

    .bits118_b0

        FOR n,0,&f00,&100

        EQUB (((n DIV 10) MOD 10) * 16) + (n MOD 10)

        NEXT

    .bits73_b1

        FOR n,0,&f8,&08

        EQUB ((n DIV 100) MOD 10)

        NEXT

    .bits73_b0

        FOR n,0,&f8,&08

        EQUB (((n DIV 10) MOD 10) * 16) + (n MOD 10)

        NEXT

    }



    .END



        PRINT "GAME",~BEGIN, ~END, ~MAIN

        SAVE "GAME", BEGIN, END, MAIN

</tt>

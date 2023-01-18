# Random number generator (very fast - very basic)

I saw a nice 6502 random number generator this morning, but at thousands of cycles per call, I thought a faster one might be useful here.

This is about the fastest random number generator you can get although it is really just a sequence of 256 numbers using 14 bytes (code and data if seed is in ZP).

Each call of rand will return A with the next of a 256 number long sequence of _random_ numbers.

You can change the multiplier (5) and the addition (&45) to many different pairs and get different sequences.

One drawback of this method is that the lsb toggels each call - to avoid this, you could use a 16 bit number and take a selection of bits from the middle.

<tt>

    .rand

    LDA seed

    ASL A

    ASL A

    CLC

    ADC seed

    CLC

    ADC #&45

    STA seed

    RTS

</tt>

See the forums [1](http://www.retrosoftware.co.uk/forum/viewtopic.php?f=73&t=640) for a BBC sample program, .ssd and discussion.

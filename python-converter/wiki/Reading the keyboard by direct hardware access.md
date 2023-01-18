_[Sample Code Library](SampleCodeLibrary "wikilink") &gt; Reading the keyboard by direct hardware access_

# Reading the keyboard by direct hardware access

This is a topic which is barely, if at all, explained in the AUG, and indeed it was an area which caused some of the biggest problems in the first BBC emulators, mostly because it seemed no-one could find any good documentation on it!

But it turns out that, with some initial setup, reading whether a key is pressed or not by accessing the keyboard hardware directly is extremely trivial on the Beeb.

## Introduction

The type of keyboard input we're interested in for games is the one of the INKEY(-keycode) variety, i.e. the one which detects multiple depressed keys at once.

I can't imagine the number of times I wrote code like:

<tt>

`dx%=INKEY(-98)-INKEY(-67)`

`dy%=INKEY(-73)-INKEY(-105)`

`jump%=INKEY(-74)`

</tt>

So often did I check for these keys being pressed that their internal codes are forever etched in my brain, just underneath the opcode for NOP, and the address of OSWRCH.

Did you ever wonder what on earth the significance of these strange key codes were? They weren't related to ASCII in any way, and they seemed to be more-or-less randomly chosen. Well, in fact, they were bringing us closer to the hardware than you might have guessed.

## Doing it 'legally'

Here's the way the AUG _wants_ us to do it. Well, actually, there are two ways. The first one is the call used by INKEY in Basic - OSBYTE &81. Simply put the negative keycode into X and Y, and call OSBYTE with A=&81. When it returns, X and Y are both 0 (key not pressed) or both &FF (key pressed).

For example, to check whether the Space bar is pressed (INKEY(-99)):

<tt>

`LDA #&81`

`LDX #(-99 AND &FF)`

`LDY #(-99 AND &FF00) DIV 256`

`JSR &FFF4`

`CPX #&FF`

`BEQ keypressed`

`.keynotpressed`

</tt>

The second way is to use OSBYTE &79. This is slightly different in that it takes _internal key numbers_ which are positive values, and as well as being able to read whether a particular key is pressed, it can also do a scan from the internal code specified, and return the first pressed key it finds.

What are the internal key numbers? Well, they are the lowest-level identifiers for the keys on the keyboard in the hardware. Internally, the keyboard is a 2d matrix which is arranged similarly to the physical layout of the keyboard. If we think of the internal key number as an 8 bit value, we can think of the top 4 bits as the row, and the bottom 4 bits as the column. This is why some keys have adjacent key numbers, for example 'Z' and 'Space' (which are physically close on the keyboard) are adjacent in the hardware keyboard matrix. Similarly, '\*' and 'Return'.

If we look at an internal keycode table, we see that the internal key code for the Space bar is 98. See how this relates to its negative INKEY number, -99. In order to convert INKEY code to internal code, we just make the value positive and subtract one.

Probably the negative INKEY codes were invented just to shoehorn some extra functionality to Basic's INKEY command, without needing to create a different keyword to read keys by internal key number. Hopefully, you can already see that using OSBYTE &81 is going to be more time-consuming that necessary, as:

- first, it needs to decode the OSBYTE number and reach the appropriate routine which handles OSBYTE &81

- next, it needs to deduce that we are trying to do a negative INKEY read, transform the INKEY code into an internal keycode, and branch to a further routine which does an internal key read

- then, it needs to configure the hardware to do a keyboard read, and actually read the key

- last, it needs to set up the registers' return values, as per the INKEY specification, and also update various internal OS variables, like the 'last key pressed' variable.

Likewise, OSBYTE &79 comes with a little extra fluff, namely:

- the same OSBYTE number decoding as before, and branching to the right place in the OS to perform an OSBYTE &79

- determining whether we want to read a particular key or do a keyboard scan

- setting up the keyboard hardware and reading the key status

There's got to be a better way...

## Doing it the dirty way

The keyboard is mapped to System VIA port A (accessed through &FE41 or &FE4F for "no handshake", whatever the hell that means...). The bottom 7 bits are used to specify which key you wish to poll, and the top bit returns whether the key is pressed or not.

So, first we need to set the Data Direction Register A to specify that the bottom 7 bits are outputs, and the top bit is an input. Hence:

<tt>

`LDA #&7F:STA &FE43`

</tt>

Now, System VIA port A is also shared by the sound chip and the speech chip, so before we can access the keyboard, we need to enable it over the other two possibilities. This is done via the "addressable latch" in System VIA port B.

The addressable latch controls a miscellany of "stuff" (AUG page 419) - there's a further layer of indirection here: we have to set up the bottom 4 bits of System VIA port B as outputs, and then we write the "bit number" of the addressable latch bit we wish to write in bits 0-2, and the value to write in bit 3.

To enable keyboard we have to pull bit 3 of the addressable latch low, so here's how we do this:

<tt>

`LDA #&0F:STA &FE42   \ allow write to addressable latch`

`LDA #&03:STA &FE40   \ set bit 3 to 0`

</tt>

So, that's all the initialisation we need to do. You could probably choose this to be your default hardware state, so that the following key reads will always work with no further hardware configuration to do. Or it may be more useful to have the hardware configured for sound generation - but whatever you choose, the beauty of accessing the hardware directly is that this initialisation can be done once per main loop, then all the keys you're interested in read at once. Using the OS, this hardware initialisation would probably be performed for each and every key read.

Now, reading a key is simplicity itself! We need the internal key number of the key - either consult the table on AUG page 142, or take the negative INKEY code of the key, make it positive, and subtract 1. (e.g. space (-99) becomes 98).

Then, write to System VIA port A, and read it back. The top bit will tell you whether the key is pressed or not (set=pressed):

<tt>

`LDA #97:STA &FE4F:LDA &FE4F  \ N flag = whether 'Z' pressed`

</tt>

All of this has to be done either with interrupts disabled, or a custom IRQ handler in place which doesn't let the OS in, otherwise all of the setup will be undone by OS code (because these values are changed to play sounds, for example).

And that's it! How to read a key in 14(ish) clock cycles.

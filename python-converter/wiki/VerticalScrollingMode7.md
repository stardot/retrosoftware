I read on one of the posts today that someone was looking for a mode 7 scrolling game and that started me thinking - how hard would a vertically scrolling mode 7 routine be and would anyone want it anyway ;-)

This code <i>should</i> show four things:

1. How to set the gfx chip up for mode 7

2. How to set up a v-sync interrupt for flicker free scrolling

3. How to set the mode 7 screen up for <i>pixel</i> graphics

4. How to scroll the mode 7 screen vertically

So, what does it show?

1. I didn't write, just run with the demo in a non-scrolled mode 7 screen.

2. \[Edit\] Works correctly now, updated .ssd on forums

3 Works, by setting the first character of each row to a gfx excape character - see the BBC User Guide for details

4 Works, but I haven't optimised it.

The code is reasonably fast, but you could save a few cycles by copy-n-pasting the decode bit (lda (&80),y..sta (&70),y) three times to remove two thirds of the bpl next, saving 26 bpl \* 3 cycles \* 40 lines which if anyone was going to use the code, I would recommend. You need to unroll the bpl next loop in threes to make sure that the last one is still the 39th, so the next unroll would be 13 and that would be too big IMO.

The data is stored in a similar way to the original mode 7 gfx characters, but uses the full 8 bits for 8 <i>pixels</i>

`[__1][__2]`

`[__4][__8]`

`[_16][_32]`

`[_64][128]`

The row consists of 39 bytes - giving a 78x4 pixel block.

The four decode sections are for the four alignments of a 78x4 block with the 78x3 screen row. top0 uses the first (lowest) 6 bits of each byte in the bits_to_gfx look-up, top1 - the last and the other two or two data lines to get the index for the look-up.

With some small changes, you could leave gaps at the top and bottom for scores and gauges (and not scribble on the first few bytes of ROM). but there is still quite a bit of work to do and so, other than a straight racer, you would need to run at 25fps.

If you wanted to do a game with horizontal scrolling, I would suggest having two copies of the data offset by a pixel and then just copy alternately.

I have posted the source and a sample .ssd on the forums here: [1](http://www.retrosoftware.co.uk/forum/viewtopic.php?f=73&t=635)

\[Edit\] This doesn't actually hardware scroll the screen, it redraws the whole screen every frame, that is why some can be left unscrolled and why it takes nearly 1/50th of a second to run. If you watch for a while, you will see some parts of the screen have bits that change as they scroll down, this is where the values being read by the program change each frame, either because the OS is changing them or because they are being read from HW that has different values each frame (eg timers).

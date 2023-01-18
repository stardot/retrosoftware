*[Sample Code Library](SampleCodeLibrary "wikilink") &gt; Line by line vertical scrolling on the Beeb*

# Line by line vertical scrolling on the Beeb

I thought I'd write up a little bit about the technique I use to get the line-by-line vertical scrolling out of the Beeb, drawing from articles I'd previously written to the Beeb mailing list. Hopefully, it will be useful to anyone else wanting similar features in their games.

There are two aspects to this technique: so-called "vertical rupture" and manipulating the "total vertical adjust" register to actually move the screen by scanline amounts. I'll cover them one at a time.

## Vertical rupture

"Vertical rupture" is the name someone in the Amstrad CPC scene coined for the technique whereby one TV frame contains more than 1 CRTC cycle, allowing us to "split" the screen into separate blocks. Each block can have its start address set independently of the others, meaning that, if we wish, we can hardware scroll parts of the screen whilst leaving other parts stationary.

In order to achieve the smooth scrolling effect, we will need to use this vertical rupture technique. However, let's not run before we can walk! First of all, let's try and set up a simple "ruptured" screen to demonstrate this effect in action. Later, I'll show how we can add in the smooth scrolling.

Suppose we want to set up a simple screen rupture - MODE 2, top 16 lines hardware scrolled, bottom 16 lines stationary. Because the top part of the screen is scrolling, we need to make this use the bottom range of screen addresses (i.e. &5800..&7FFF), as we need to benefit from the hardware screen wrap-around at &8000. Note that it will be necessary to prod the addressable latch at &FE40 to specify a 10k screen.

The bottom half of the screen is stationary, so we use the rupture technique and set up the bottom half's start address to be &3000. So effectively, the two halves of the screen are mapped the other way round, but the truth is that we could split the screen any number of times in a frame, and set each block's address to be whatever we wanted - linear address space? PAH!

##### '''NOTE: ''' You can download (liberally) commented BeebASM source code **[here](./images/Vrupt.zip "wikilink")** to accompany the explanation below...

Here's how we would do this:

-   First note that there are 39 character rows in a PAL screen.

<!-- -->

-   Next note that in normal MODE 2, we have VSync set to occur at line 34 (value in R7)

<!-- -->

-   This means that from the point of VSync we have 5 character rows left of the CRTC cycle - **remember this!** It is important later on....

Then, we would implement rupture as follows:

-   Wait for VSync interrupt!

<!-- -->

-   As we know, this happens towards the end of the CRTC cycle. TV flyback will have started, and the TV is ready to start the new physical frame shortly. So the beginning of the next CRTC cycle represents the top of the new frame.

<!-- -->

-   Immediately set up R12/R13 with the hardware scroll start address for the "top" screen. This is cached by the CRTC and will be used when it starts its new cycle.

<!-- -->

-   Now we must wait until the new CRTC cycle has started. We already know this to take 5 character rows (remember?!).

> 5 character rows
> = 40 (5\*8) scanlines
> = 2560 (40\*64) 1MHz clock ticks

-   So we wait for AT LEAST 2560 clock ticks... to cater for differing tolerances in clock speeds and CRTCs, we wait for a while longer than this, as we only care that we are rastering somewhere within the new CRTC cycle. As I've mentioned in the past, the timing required is not actually all that delicate.

<!-- -->

-   We are now into a new CRTC cycle. The CRTC has taken its internal address pointer from R12/R13 and is currently refreshing the screen from somewhere between &5800 and &8000 (whatever we specified - we are choosing this address for our scrolling after all!)

Next we do a few cunning things:

-   We set R4 to 15, specifying a total CRTC cycle length of 16 rows.

<!-- -->

-   We set R7 to anything greater than 15. This ensures that VSync will NEVER be generated during this cycle. This is what we want, as we know from the PAL standard that we must have 39 rows in a refresh, and generating VSync every 16 rows will clearly cause the TV to barf! Let's set R7 to 255 just to make a point :)

<!-- -->

-   We set R6 to 16: this ensures that we see all the rows of this CRTC cycle; this is what we want - they are all valid after all. Of course we could equally set R6 to anything higher than 16; it won't display any more because there are only 16 rows in the whole CRTC cycle!

Note that setting R4, R6 and R7 *during* the cycle they are controlling works OK, as the CRTC doesn't pre-cache them (as it does with R12/R13); they are simply read each time round its internal loop as it needs them.

Now here's the more cunning bit:

-   We set R12/R13 to look at &3000. As we know, the CRTC has already cached its internal address pointer from R12/R13 this update and changing them mid-update won't affect its screen address pointer. However, as we know, this update is only going to last 16 rows, at which point its cycle will start all over again, and its screen address pointer will be re-cached, this time using the NEW values in R12/R13, i.e. &3000!

<!-- -->

-   Now we need to wait for the new CRTC cycle to begin - this will of course be in 16 character rows time from the last cycle:

![Output from this [disc image](Media:Rupture1.zip "wikilink"). Download commented sourcecode [here](./images/Vrupt.zip "wikilink") ](Rupture1.png "Output from this disc image. Download commented sourcecode here ")

> 16 character rows
> = 128 (16\*8) scanlines
> = 8192 (128\*64) 1MHz clock ticks

-   At this point, the TV will be starting to rasterise the physical bottom half of the screen, and the CRTC will be sending screen data from addresses &3000 onwards to the TV.

The trick now is to restore normal conditions again. We have 23 more rows left in the PAL refresh to make up. So:

-   We set R4 to 22 to give us 23 rows.

<!-- -->

-   We set R6 to 16 to ensure that we only plot 16 rows.

<!-- -->

-   We set R7 such that VSync is generated at the *same point relative to the end of the CRTC cycle as a normal MODE 2 refresh*. As we remembered earlier (you remember?), we had 5 rows left following a VSync. So, if we set R7 to (23-5)=18, we get the VSync in the same place.

And that's pretty much it! The VSync generated then takes us back to the beginning of this loop, upon which we do the same thing all over again.

## Using vertical rupture to produce smooth scrolling

The crux of the idea is that we can use CRTC R5 to introduce additional lines into the PAL frame. The extra R5 lines are added at the end of the CRTC update, after VSync has occurred, which will normally be when the TV is rasterising the top border. Hence we can use R5 to add extra scanlines to the top border, which will essentially move the 'proper' screen down by scanline amounts.

Now we don't want to see the top boundary of the screen moving as we alter R5, because that's ugly and unconvincing. It would be better if we could turn the screen off until the raster beam has reached a particular point on the screen, and then turn it on again, to give a rock-steady top boundary. We know that VSync happens at the same point every TV frame (it has to or the picture rolls). Therefore, we can set a timer at VSync, which will always trigger at the same place on the TV screen.

But there are 312 lines in a PAL frame. Usually these are defined by:

> (R4+1)\*(R9+1)+R5
> = (vertical total rows) \* (number of scanlines per row) + (scanline adjust)
> = (38+1)\*(7+1)+0
> = 312

If we put R5&gt;0 we'll get 313 lines, 314, 315, etc etc. How can we use R5 to offset the top of the screen whilst still maintaining 312 PAL lines?

The trick is of course to use vertical rupture. We split the screen refresh into 2 CRTC cycles. In one, set R5=n, and in the other set R5=(8-n). This way we can ensure that the total number of lines adds up to 312, whilst still adding in extra scanlines following the VSync. Another advantage of this technique is that 2 CRTC cycles means 2 separate screen areas - so we can put a stationary window underneath the scrolling window, for displaying game status and suchlike.

Let's think about the interface we need to present: just as in the last demo, we need a way of setting the start-of-screen address for the scrolled window of the screen, but in addition, we also need a way to define which scanline of the character row should be the first visible one on the screen, i.e. the line after the raster interrupt has turned the screen on again. We'll call this start scanline simply 'line' - its range will be 0...7.

-   When line=0, R5=8. The first visible line is defined to be the one after the 8 extra scanlines introduced to the top border by R5, i.e. scanline 0 of the new character block.

<!-- -->

-   When line=1, R5=7. Now see that the same point on the physical screen corresponds to scanline 1 of this same character block

<!-- -->

-   When line=7, R5=1. We have introduced just one extra line of border, so when we make the screen visible, we are now at scanline 7.

*to do: replace this awful ASCII diagram with something a bit clearer - I don't think this is what you had in mind*
`....             ___                                        n`
`R5=1             ___                                  e  e        ___`
`R5=2             ___                            c  r        ___  |___`
`R5=3             ___                         s        ___  |___  |___`
`R5=4             ___                    f       ___  |___  |___  |___`
`R5=5             ___           p     o    ___  |___  |___  |___  |___`
`R5=6             ___      t  o      ___  |___  |___  |___  |___  |___`
`R5=7             ___          ___  |___  |___  |___  |___  |___  |___`
`R5=8             ___    ___  |_  _ |_  _ |_  _ |_  _ |_  _ |_  _ |_  _  _  _  _ screen enabled here`
`1st visible line ___   |line0| 1   | 2   | 3   | 4   | 5   | 6   | 7`

So we introduce '8 minus line' extra scanlines to the top border. Therefore we set R5 to '8 minus line' during the CRTC cycle which enables VSync.

It then figures that in the other CRTC cycle (the one that contains the scrolled playing area), we set R5=line in order to make up the total number of R5 scanlines to a multiple of 8. This means we'll arrive at the full 312 lines.

![Output from this [disc image](./images/smoothscroll.zip "wikilink").
Use \* and / to scroll up and down, and hold Shift to scroll line-by-line.](./images/smoothscroll.png "fig:Output from this disc image. Use * and / to scroll up and down, and hold Shift to scroll line-by-line.") Let's suppose we want a 24 line scrollable area. What do we do? The disc image on the right contains a demo which creates exactly this screen layout. In the description which follows, the line numbers reference this Basic listing.

Let's start at VSync:

-   At VSync we are already in a CRTC cycle. We know we need to set R5=8-line. What should we set R4 to? Well, in the other CRTC cycle, we need 24 rows + 'line' scanlines. Therefore in this cycle, we need 39-24-1 rows. The additional -1 is from the two settings of R5 in each cycle, which add up to a whole row.

So: *(line 700)*

-   Set up the timer to enable the screen at the beginning of the next TV frame. We need to wait for as much time as it would take to complete this frame if we had set R5 to 8 (biggest top border possible). Hence when R5 is 8, we do not hide any of the following frame. If R5 is 7, then the screen remains off for one further scanline, meaning that the first visible scanline of the following frame is the second scanline, etc etc. This calculation is complicated by the fact that the VSync interrupt doesn't arrive at the moment of VSync, but actually after the VSync pulse width period (by default, 2 scanlines).

<!-- -->

-   *(line 750)* set R5 to '8 minus line'

<!-- -->

-   *(line 760)* set the number of displayed rows for the next cycle to be 24+1 (total screen rows + 1 to account for the fractional row which comes from R5)

<!-- -->

-   *(line 770)* we have just had VSync for this CRTC cycle. We don't want it in the next cycle, so turn it off by setting it to an out-of-range value.

<!-- -->

-   *(line 780)* turn off the screen now. It will be turned on again by the interrupt we just set.

<!-- -->

-   *(line 790)* fetch the start-of-screen address we want for the scrollable area. This is of course variable.

....time passes... the TV raster beam is at the top. The top border gets '8 minus line' extra scanlines added to it. Then the new CRTC cycle begins. 'line' scanlines later, we get our interrupt: *(line 510)*

-   *(line 510)* enable the screen!

<!-- -->

-   *(line 530)* set a timer to interrupt us more-or-less as soon as this CRTC cycle has finished and the new one has begun. We know this will be in 24\*8 scanline times from now.

<!-- -->

-   *(line 560)* define the length of this CRTC cycle - it's 24 lines, plus *(line 570)* the extra residual scanlines which would bring our TV frame back to a multiple of 8 scanlines again.

<!-- -->

-   *(line 590)* prepare the bottom screen window start screen address. This is the constant 'status' area which is the visible part of the other CRTC cycle.

....more time passes... we reach the other CRTC cycle, the one with the VSync in it. Then the interrupt gets called *(line 390)*:

-   *(line 390)* we set the number of rows of this CRTC cycle to be the residual amount we calculated somewhere up there: 39-24-1 rows (remember R4 takes 'number of rows minus 1').

<!-- -->

-   *(line 400)* it's a 1 row high status area, so set R6 to display just one row. This also demonstrates the importance of this lower status window. Without it, we could just set R6=0 as soon as we got here, but we'd have to ensure that our timing was perfect, so that the CRTC didn't get a chance to send anything to the TV for rasterisation this cycle, otherwise we'd get little flickers of the screen appearing. By having a visible part of the screen, we can interrupt anywhere within this character row and it will still work well.

<!-- -->

-   *(line 420)* here's the last bit - setting the VSync position. This determines where the entire screen will be positioned on the TV. It also affects the amount of time we have to wait in line 700 (described above).

------------------------------------------------------------------------

[Richtw](User%3ARichtw "wikilink") 14:00, 11 July 2008 (BST)

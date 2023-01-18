## 31st October 2010

Tricky, tricky Hallowe'en. Later I'm going to play piano dressed as a zombie, but until then - *Onslaught*!

Today it's time to get the code editable (or at least readable) natively on a PC - how did I ever do anything on a Beeb? No copy and paste, search and replace, proper line editing... the horror! My trick here is somewhat lo-tech, but it works for me. *Onslaught* disc in drive 0 in B-Em, blank disc in drive 1. Then, for each source code file:

<tt>

`>LOAD "S.Part1"`
`> *SPOOL :1.Part1`
`> LIST`
`     ....`
`     ....`
`> *SPOOL`

</tt>

Then I just load the entire disc image into a text editor, trim the junk from the top, and between files, delete the first 5 columns of characters (to remove the line numbers), and it's *almost* ready for BeebAsm to assemble exactly as it is! Well, it needs a little tidying up, the Basic build system removing and translating into BeebAsm equivalents, and spaces need to be inserted after each 6502 mnemonic (not because BeebAsm won't assemble it, but because the syntax highlighting on my text editor won't work... oh lah-de-dah, such luxury!). Now I'll be able to look at it properly, and get a feeling for how it all works again, while reformatting the code and adding some useful comments.

But I'm not going to just take the code as-is - it needs a few 21st century improvements, as there are tricks I've learnt since then which need to find their place in Onslaught v2.0. The core engine of the code is going to be rewritten (e.g. things like the sprite routine as mentioned above), and a few bugs fixed (like problems with the sprite clipping and dot movement and the wrap-around point of the level). The aim is to end up with a really polished product - here's what I hope to be able to implement:

-   Nice title screen, with title tune (may have to call for some help on that when it's closer to completion)
-   Around 40-50 levels
-   At least 8 different types of monsters, hopefully more, all with their own behaviour.
-   More varied scenery and colour schemes
-   Bonus system / collectables
-   Perhaps a little sub-game with slightly different mechanics
-   Big emphasis on in-game music and sound, complete with 'hurry up!' frantic bit when time is low
-   Interesting 'home' screen, with high score and demo mode

![Look at all that space wasted on the right!](./images/Onslaught-scr.gif "fig:Look at all that space wasted on the right!") It's quite a big wish-list, but so far it all seems feasible in terms of CPU time. The only doubt is how much memory I have for everything. Here's the first problem - take a look again at the original version and the space on the right, currently unfilled. Obviously the original aim was that this was going to be filled with interesting graphics and useful data - number of lives, level number, score, etc. But it just pains me, because it feels like a big waste of memory, no matter how pretty it could be. That area is 7 characters wide by 24 characters down - this multiplied by 2 (for the two screen buffers), and we have 2688 bytes being used for a big black space. Aaargh!

The other problem with putting any status on the right as that we can't use a colour interrupt to increase the number of on-screen colours (as this is Mode 5). So I'm going to add a few more screen lines at the bottom, which can have their own colour scheme (to keep it interesting), and which will certainly provide more than enough space for all the other stuff we have to show. The other advantage of this is we can use a screen-split (the 'vertical rupture' technique) so that we only need double-buffer the playing area, whilst the status bit remains just a single instance. Oh yeah! It will save about 1k, plus we don't have to update two buffers when we write to the status area, *and* it can have its own colours. What's not to like!

The dimensions of the playing area are slightly unusual - being 31 characters by 21 - plus a character wide frame around the outside. I'm going to keep the frame, as I think it looks nice visually and it's a little bit "different", but what it means is we have a 33 character wide version of Mode 5 (&108 bytes per row). It's a bit odd, but I'm going to keep it that way as it works really well in the original (the dimensions need to be odd numbers as the character is 3x3 and it's the only way to ensure he's well centred).

![Split screen, with double-buffered playing area, and single-buffered status area with different colours](./images/Onslaught-rupture.png "fig:Split screen, with double-buffered playing area, and single-buffered status area with different colours") So I've decided that my strategy is to be that I start off with the engine from scratch, and I'll then bring over routines one-by-one from the original code, making improvements as I go. Here's a picture of the code running my split-screen routine - not much to look at admittedly, but the beautiful thing is, using this foundation, I could already almost blindly port the entire Onslaught code base over to this, and it would run fine! The difference is, using this engine code, it's already much more efficient - no time is wasted idling unnecessarily. When the playing area has been rasterised, and the back buffer is already primed to be displayed next frame, the currently displayed playing area is already being cleared - which it can do with no visible artifacts. Overlapping the game stages like this will win us even more time to do lots of nice stuff each update.

The key to this is the interrupt routine which manages everything. At the beginning of the game I synchronise a free-run timer with VSync, in the way I described [here](http://www.retrosoftware.co.uk/forum/viewtopic.php?p=4093#p4093). This is designed to interrupt just after the playing window has been rasterised, during the bottom frame edge (which is in fact a part of the single buffered bottom screen, rather than the playing window, which saves another 256 bytes!). This interrupt replaces the VSync entirely - we don't need it any more - and apart from settings the bottom screen colours and dimensions, it's also responsible for handling the sound and keyboard reading. It also sets the screen address for the top screen. It maintains a frame count, so that it can be locked to a chosen frame rate, and will automatically do a screen swap if client code sets a zero page variable to 1. When it is done, it will reset this variable again, and client code can poll for this moment, and which point it will have just rasterised the playing area. This interrupt routine then sets a second timer off, which is responsible for managing the top screen dimensions and colours.

In addition there is a third timer used (another free run timer) whose job will be to synthesise the low-frequency notes for the in-game tune (using the technique that Tom Walker invented to play bassier notes than those permitted by the Beeb sound chip). This isn't written yet, but I'll come to it soon, as I want the in-game sound to be a very integral part of the whole game. Unfortunately this means either you'll have to play it on a real Beeb, or on B-Em (pretty much as close to a real Beeb as you can get!). I don't think BeebEm is able to deal with this kind of sound code yet.

Also, I implemented my zero-page sprite routine, with automatic transparency, which leaves me &7E bytes of zero page to use for whatever I want. Should be enough.

Tune in next time to see what happens next - porting the main routines I think...

*[&lt;&lt; Previous entry](OnslaughtDiary20101030 "wikilink") --- [Next entry &gt;&gt;](OnslaughtDiary20101102 "wikilink")*

*[Home](OnslaughtDiary "wikilink")*

------------------------------------------------------------------------

### Comments

-   (Example comment to demonstrate markup).
    -   [Richtw](User%3ARichtw "wikilink") 08:33, 26 November 2010 (GMT)


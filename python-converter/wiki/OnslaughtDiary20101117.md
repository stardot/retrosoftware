## 17th November 2010

It's been quite a busy weekend - but unfortunately, not with Onslaught. But still, I've managed to get a little bit done. Mostly I've been bringing over all the map code from the old codebase - that is, the code which builds levels from their definitions, renders the map in the playing window, and deals with reading whether a particular (x,y) coordinate of the map is solid, or whether it contains something deadly or collectable.

To expand on this, I'll explain how the original codebase works - each level is stored as a number of objects: platforms, vertical strips and generators. These are well compressed, which allows me to potentially store loads of levels. When the level is started, a 24x24 image of the map is built, for quick access by the map renderer, and the routine which tests solidity. In addition to this, a 48x48 image is stored which contains the index of any monster at that position (as a 3x3 block), and the position of the player - this makes collision detection extremely quick, and it's one of the ways that Onslaught manages to run so fast. The player simply has to check whether any position underneath him contains a monster index (before writing his own details). Bullets and tokens just check whether there is something significant underneath them, and do the appropriate thing.

So far I've ported the code 'as is', but there are some improvements I'd like to make. The first is that I want to have 'scenery' tiles in the map, which the player and monsters can walk on top of - essentially they're just intended to make the levels look more interesting, but this means I need to change the way I handle solidity. My aim is to combine it with the 48x48 map, which also means I could have map tiles which are partially solid. Maybe I'll implement sloped surfaces which you automatically walk up.

Then I need to decide if I can justify a separate 24x24 map just for rendering purposes, or whether this can be efficiently combined with the 48x48 map, to free up 576 valuable bytes.

![Go on, you know you wanna...](./images/Texttest.png "fig:Go on, you know you wanna...") Anyway, this evening I decided to take a break from all this and write something new - the text system. Obviously I'm going to need text in the game, and I was determined not to use the standard system font, because - particularly in MODE 5, or any 'chunky pixel' mode - it looks ugly and gives rather an unpolished feel. In the demo version, I had the word 'SCORE' written in an unusual-looking font, and I decided to see if I could create a whole alphabet in this style. After a bit of playing around, I arrived at something which looked consistent across all the characters - the only difficult thing was the size of a character - 5x8 (or actually 4x7 with a blank column to the right and a blank row underneath).

I decided to store these characters on their side, meaning that each one only uses 4 bytes - like this:

<tt>

`EQUB %11111100     ; A`

`EQUB %00100110`

`EQUB %00100010`

`EQUB %11111110`

</tt>

Then they are plotted column-by-column, using a pixel plotter to write a single pixel on 7 lines of a character block. It works really well, and means I can get a drop-shadow type effect by plotting first in black, and then on top in a different colour, offset by a pixel in x and y - and it's _reasonably_ fast. I wouldn't want to be plotting text every frame by any means, but at the start/end of a game, and on the title screen, it'll be fine. And more importantly, the font hardly takes up any memory - only 156 bytes for the whole thing.

I'm quite happy with this little diversion - it adds a little bit more identity to the game, and at least it's not the standard Beeb font, or the ubiquitous 4x8 one found in Repton and all the rest.

_[&lt;&lt; Previous entry](OnslaughtDiary20101112 "wikilink") --- [Next entry &gt;&gt;](OnslaughtDiary20101128 "wikilink")_

_[Home](OnslaughtDiary "wikilink")_

---

### Comments

- (Example comment to demonstrate markup).

  - [Richtw](User%3ARichtw "wikilink") 08:33, 26 November 2010 (GMT)

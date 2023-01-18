# JBiplane Development Diary

![](./images/Jbipwipscreenshot180.png "Jbipwipscreenshot180.png")

## December 2013

Where did I start? I was thinking of games I used to like playing when I was in my teens. One of them was on a friend’s Amiga – a two player (and later modified for 1 player) dogfight game nicknamed [Bip](http://www.youtube.com/watch?v=VOfG04NFt0E) . This was given away on Amiga magazine cover disks. We used to play it for hours. Hunting through the software archive, it looks like only a couple of Beeb games of this type were ever produced. Neither game feels satisfying to play, mostly due to being a bit slow in comparison to BIP on the Amiga. So I thought I’d have a go at a Beeb interpretation. I knew this would stretch me as at this point I’d only chalked up one completed machine code game – and a fairly simple one at that ( [JSnake](http://www.retrosoftware.co.uk/Jsnake) )

## Smooth operator (not really)

I remember thinking “I’d like smooth animation”. My immediate decision at this point was to use Mode 1. My rationale was that Mode 1 = smaller pixels (than Mode 2 or 5) and thus per pixel movement would produce the desired result. So I merrily went ahead and created 8 mode 1 sprites in the excellent [Beebspriter](http://www.retrosoftware.co.uk/beebspriter). My initial effort was disappointing. I started by adapting routines from JSnake to plot the plane sprite to the screen. The plane moved very quickly, and very coarsely across the screen. Why? Because I hadn’t fully appreciated how Mode 1 worked. Once again, the (IMHO) perverse screen addressing layout of the Beeb became the bane of my life for a while :/

| |

|------------------------------------------------------------------|

| ![](./images/EarlyattemptPlaneSprites.png "EarlyattemptPlaneSprites.png") |

| **Early sprite attempts in Mode 1.** |

## Head scratching

Once I’d scratched my head a bit and scribbled a few notes, I worked out that if I wanted to move a sprite in 1 pixel increments horizontally, I’d need to keep 4 copies of each sprite, offset by one pixel to the left or right. This is because in Mode 1, each byte of screen memory represents 4 pixels, each of which can be one of 4 colours. Til now my move-sprite routine was moving the sprite by 1 byte.. and so the sprite was moving along the screen at 4 pixels per frame horizontally – hence the fast yet unpleasant coarse animation.

So.. I needed a fair number of sprite+ offsets. A plane can move in 8 directions.. and I wanted 2 planes on screen. So that will be (8\*4)\*2 = 64 sprites, and that’s before any other graphics such as bullets and scenery. By this time I’d decided that I’d like the sprites to be a little bit bigger than my initial efforts. Hmm.. lots of sprites and bigger: not a good combination for a Mode 1 game. Mode 1 uses 20k of precious RAM. .and storing all these sprites would use lots more, not leaving much for actual game code. I did a little more head scratching.

## To the forums

I redrew all my sprites and changed from Mode 1 to Mode 5. This was reasonbly straightforward and gave me much more RAM as Mode 5 only uses up 10k. I then did a bit more testing and then slowly realised – with a few hints from Tricky on the forums – that my sprite plotting routines were very inefficient indeed. In the top 10ish rows of the screen, I was encountering the dreaded sprite tearing, with just 1 sprite on the screen! As I planned on having 2 planes and a few bullets on screen at once, something needed to be done to fix this.

| |

|--------------------------------------------------------|

| ![](./images/Planesprite.png "Planesprite.png") |

| **Mode 5 sprites - 1 + 3 offsets for each direction.** |

The main inefficiency was needless XY ord calculations. In my previous game, I didn’t actually have any sprites. I was just drawing a line (the snake) .. a couple of pixels appended to the head of the snake. I was (ab)using a very handy example routine [example routine](http://www.retrosoftware.co.uk/wiki/index.php/Calculate_Screen_Address). The routine gave me the X Y coordinate of a byte’s worth of pixels. While using the same routine in my new game, I was calling it for every byte I was plotting or erasing. This used A LOT of CPU cycles. This is BAD for plotting sprites on old and comparatively slow computers. To get flicker free sprites, you need to have erased and plotted a sprite before the monitor/TV scanline passes where the sprite is on screen. The screen is redrawn 50 times a second.. and there aren’t many CPU cycles between refreshes of the screen (at least by modern computing standards).

## Dim bulb

![](./images/Dimbulbpic.png "Dimbulbpic.png ")

Christmas 2013 was approaching. I scratched my head even more (I was probably wearing out a patch of hair on my head at this point!)

On Christmas Eve I [posted](http://www.retrosoftware.co.uk/forum/viewtopic.php?f=73&t=881) a message saying I was still having problems improving efficiency. Tricky gave me some more hints and mentioned creating an 8k screen mode – on Christmas Day!!! I was very grateful; I was round at my in laws and this revelation gave me a much needed distraction. A dim light bulb sputtered in to life in my brain. An 8k screen would make the maths of plotting very easy – and quick. Why? Because then everything fits neatly into 8 bits – very handy for an 8 bit processor. In an 8k version of Mode 5, the screen size = 128x256. This results in 1 char row being 256 bytes in length, with 32 character rows on the screen.

[ JBiplane Dev Diary Continued ---&gt; ](JBiplane_Dev_Diary_Continued "wikilink")

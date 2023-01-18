## Mixed Grill March BBC Micro Development Diary

**_by Jools Henn_**

#### March 2010

_28th March_

Started work on this project. Did some work up to 19th May, then left it for the summer until releasing the first preview.

#### October 2010

_27th October_

First preview released.

Current TODO list:

- Make the levels get harder after you get past the first one

- Randomize backgrounds (anyone got a good random number routine? currently I'm generating pseudorandom numbers by reading bytes from the ROM :))

- Some kind of sound effect when you die

- Some kind of indication that you've completed a level (rather than just an extra flag)

- Game Over screen

- High Score table (or at least some record of high score)

#### January 2011

_22nd January_

\* All of the stuff above is now done (except for the randomize backgrounds, but I'm not too worried about that)

- Random function is now more random

- Used relocation code, giving me more space. I've got 3,573 bytes remaining to use up. There's not much extra code to do, so most of that can go on graphics.

- I had a go at running it in an Electron emulator - I was expecting it to run really slowly, but strangely it crashed just after trying to start the game. Odd, I didn't think I was doing anything BBC-specific... I might investigate further (although it would probably need a few changes to run at a good speed on the Electron anyway).

_23rd January_

\* Recently, I added some animation to the row of houses in the hammer the keys section. This is in the background, so should be animated slowly. I made a routine that copies one fifth of the character row across per frame, just copying it a byte at a time (one byte = two pixels wide). For the first segment, I also store the bytes for the first column before copying over them, and on the last segment paste these values back in on the right hand side after the move (so the houses just loop round).

This worked, but animated them a bit too fast, and also a bit jerky. So I decided to try a single-pixel scroll - this meant using some nasty ROR/ROL and bitmasking, and the routine is considerably slower than the old one (11 instructions per pixel, ouch) - but it looks a lot nicer :)

- After this, I was curious how much CPU time I had left per frame. I need to keep everything running in one frame, otherwise it will all fall to bits (including the music slowing down!). I added in some temporary code to change the background colour when the game code was finished, and changed it back after the VBL. This showed the amount of CPU time I had left varies, but at worst it's about 1/6 of the total. That's not too bad, it'll give me a bit of scope for animating some more small objects. I'd better keep an eye on this, though.

#### February 2011

_10th February_

\* Used up a little bit of my spare CPU time to draw some scrolling flags on the catch-up section. The flag sprite is duplicated and offset by one pixel, so it can be single-pixel-scrolled. I might add some more of these...

_22nd February_

\* There are now three scrolling rows of flags. Maybe they can get replaced with some better graphics sometime, but they'll do for now.

#### March 2011

_20th March_

\* Added "fallen over" graphic, which is shown when you crash into the wall, catch the guide / thief person, or fall too far behind on the catch-up section.

- Added a bonus system, where the faster you catch the person, the more points you get :)

#### June 2011

_19th June_

\* High-score entry bug fixed (pressing escape no longer means you are unable to enter any more highscores)

- You can now press escape in mid-game to instantly end the game.

#### November 2011

_13th November_

Finally got round to spending a bit of time on this, after having a break over the summer. Now, what shall I do with all this lovely memory I have left? ;)

- Added graphics for another person... RV Markie in Ming costume. Well, as near as I could get with Beeb graphics and my lack of drawing ability.

- Drew a whole font in the style of the scoreboard, so I can give the player instructions as they are playing (or taunt them :D). Not used it yet, but watch this space...

_14th November_

\* I'm now using the font I designed yesterday for the level number, game over, and winning screens. That's got rid of all of the ugly mode 2 beeb font from the game :)

- Added some in-game instructions on the bottom of the screen, telling you to match the pose, or waggle your arms.

- Added "amusing" level subtitles and endgame rankings (hey, got to use all this spare memory up somehow :))

- Game size now stands at 7791 bytes. 913 bytes left to use on something...

_15th November_

\* Added "Retro Software" freeware loader.

#### March 2012

_1st March_

\* Tweaked the title screen, it now contains a plot that makes a bit more sense. We're on the home stretch now...

_7th March_

\* Tweaked the player graphics. Previously (although it wasn't that clear), you just saw the backs of the heads of the characters. I could have the characters facing forwards, but then that would mean your left hand controls the right hand of the player, and that seemed wrong. Plus, it looked odd that the legs were going sideways while you're looking at the back of the player's head. In the end I've gone for a compromise - you now see the characters facing at an angle somewhere between "away from you" and "to the right", so you can just about see the players' eyes, noses, and mouths. I also gave "Mixed grill man" more hair, and we can now see him carrying a plate (containing the mixed grill). You can also see more of Markie's green head. Much better.

- Had a bit of a tweak of the music - it always sounded a bit lame before. I changed some of the notes around. Also, now the arpeggios and the tune play at the same time after the first run-through. Hey, we've got polyphony, we may as well use it :)

I do believe we're pretty much done :)

#### April 2012

_17th April_

\* Added a "ping" sound when you successfully go through the wall.

#### May 2012

_5th May_

I took the game along to Retrovision 2012, as a sort-of release - forum thread on this to follow. Calling this version v1.00 - I was intending this to be the final release version of the game, but it turned out some small final tweaks were needed.

_7th May_

\* I'd just noticed before I went to RV that the Retro Software loader disabled the escape key. A little bit of a pain, as you can't press Escape to quit a game any more. I've now removed this line from the loader...

- Reduced the delay slightly on the disc version of the loader.

- Another thing I noticed is some occasional flicker on the character on the right. I'm sure it didn't do that so much before. I finally worked out that it was flickering at a certain point in the music, when it's trying to play the arpeggios. As a workaround to this, I tweaked the music so the arpeggios are played one frame later. It's a barely noticeable difference, but it seemed to stop the flicker again. At least for the most part - if you hold down the keys, you still get flicker, and you still get the occasional flicker sometimes anyway. It's a lot better than it was, though.

OK. I'm drawing a line in the sand here, and declaring the game "DONE!". It's been over two years, it'll never get released otherwise.

- Transferred the game over to the Beeb, and recorded it back in to my sound card. Then I reduced the inter-block gaps manually in an audio editor from the standard 0.8 seconds (approx) to 0.4 seconds (a really tedious job - especially as this was the second time I did it, as I did the same for the version I took to RetroVision and loaded off my mobile phone). 0.4 seconds should be OK, my Beeb is just about happy with 0.2 seconds, so 0.4 leaves a bit of a margin of error. Makes the game load a lot faster (about 1 minute and 45 seconds). I'll be releasing this audio file too for those of you who like to load in from real tape :)

- Final size of the game is 8029 bytes! (excluding the basic loader and relocation code)

- Calling this v1.01. Release on the website is imminent...

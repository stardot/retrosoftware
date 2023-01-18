# Hard Hat Harry 2 by Tom Walker

### Licence

[GNU GPLv3 license](http://en.wikipedia.org/wiki/GNU_General_Public_License)

### Introduction

Hard Hat Harry 2 is a massively expanded sequel to the original platformer, for the BBC Model B.

It was demoed at the _[In Da 80s](http://inda80s.cgeu.info)_ show in Manchester in July 2011.

[Discuss _Hard Hat Harry 2_](http://www.retrosoftware.co.uk/forum/viewforum.php?f=81)

### Features

- MODE 2 graphics

- 62 screens

- A selection of returning and new enemies

- Puzzley bits

### Design Document

<tt>HARD HAT HARRY 2

SON OF HARRY

From Retro Software in ~~2011~~ 2012

An action filled 62 screen arcade adventure for the BBC Micro Model B

It's been 28 years since Hard Hat Harry. Harry has since settled down and become a rich banker type or something, and hasn't looked at a construction site since his showdown with Big Kong. However, when Edwards & Co started up again and needed a work experience kid, they knew where to look.

Entering HARD HAT HARRY JR.

Almost identical to his father, Harry Jr has been sent to work on the new arts centre. Which is 3 miles underground for some reason. It's almost rewarding work, despite the rumours of a 'Cult of Kong' in the caverns.

At least, that was until Harry was knocked out by a flying spanner...

Now he's being offered as a sacrifice by some strangely dressed monkeys. All the other workmen have vanished. It's up to Harry to escape this cavernous building site and defeat his family's age-old enemy...

And just to add to his challenge, there is a gas leak in the cavern, which combined with the poor electrial work, will lead to a huge explosion in only 45 minutes!

Enemies he'll encounter :

Monkeys - They're back. And 28 years in solitude hasn't done their sanity much good.

Birds - Despite stunted growth due to living underground, these birds are vicious and will kill Harry at the slightest provocation.

Fire - Man's oldest tool and enemy, and often spawned by poor quality electrics.

Penguins - These look suspiciously like they're from another game, and have teamed up with the monkeys due to the pleasantly cold climate in the caves.

The Hyper Viper - This foul creature has been bred underground by the cultist monkeys, in preparation for the apocalypse. In the meantime he'll eat Harry and anyone else wearing a hard hat.

Big Kong - will Harry Jr confront his father's nemesis? Will he rescue the girl with no name? Will those barrels move any slower this time?

Items he'll encounter :

Tea - An essential part of any underground construction site.

Switches - Harry pulls these. Stuff happens. Sometimes.

Radioactive Boulder - These will kill Harry, but might prove useful against enemies.

Damsel - Kong's prisoner from the first game was never rescued. Can Harry Jr save her?

Can of Holes - This elusive object grants Harry invincibility and impressive skills with the opposite sex. Or at least that's what the workers told him.</tt>

### Downloads

[Hard Hat Harry 2 V1.0 - BBC Disc version](./images/HardHatHarry2-V1.0.zip "wikilink")

[Hard Hat Harry 2 BBC version P65/Ophis GPL'd source code](./images/HardHatHarry2-Source.zip "wikilink")

### Screenshots

<table>

<tbody>

<tr class="odd">

<td><p>[[Image:hhh2-title.png|320px|<em>Hard Hat Harry 2 WIP title screen<strong><br />

<em>Posted: Jul 27, 2011</em>]]<br />

</strong>Hard Hat Harry 2 WIP title screen</em>'<br />

<em>Posted: Jul 27, 2011</em></p></td>

<td><p>[[Image:HHH2-loadingscreen.png|320px|<em>Hard Hat Harry 2 loading screen<strong><br />

<em>Posted: Feb 25, 2012</em>]]<br />

</strong>Hard Hat Harry 2 loading screen</em>'<br />

<em>Posted: Feb 25, 2012</em></p></td>

</tr>

<tr class="even">

<td><p>[[Image:HHH2-finaltitlescreen.png|320px|<em>Hard Hat Harry 2 title screen<strong><br />

<em>Posted: Feb 25, 2012</em>]]<br />

</strong>Hard Hat Harry 2 title screen</em>'<br />

<em>Posted: Feb 25, 2012</em></p></td>

<td><p>[[Image:hhh2-game1.png|320px|<em>Starting out<strong><br />

<em>Posted: Jul 27, 2011</em>]]<br />

</strong>Starting out</em>'<br />

<em>Posted: Jul 27, 2011</em></p></td>

</tr>

<tr class="odd">

<td><p>[[Image:hhh2-game2.png|320px|<em>Exploring the caverns<strong><br />

<em>Posted: Jul 27, 2011</em>]]<br />

</strong>Exploring the caverns</em>'<br />

<em>Posted: Jul 27, 2011</em></p></td>

<td><p>[[Image:hhh2-game3.png|320px|<em>Locked door - but where's the key?<strong><br />

<em>Posted: Jul 27, 2011</em>]]<br />

</strong>Locked door - but where's the key?</em>'<br />

<em>Posted: Jul 27, 2011</em></p></td>

</tr>

</tbody>

</table>

### Development Diary

#### 30 July 2011

Had a bit of a play with the map data format today. Started out with 25 screens taking 2187 bytes.

HHH1 used a simple form of RLE on map data. In a single byte, bits 0-3 gave the tile number (a total of 16 tiles, though only 10 were used) and bits 4-7 gave the count. Due to an oversight this count was 1-15, though 1-16 should have been easily possible.

HHH2 is based on this system. However it is less efficient as there are now 32 tile types, all of which are used! This means 5 bits are used for tile type, and only 3 bits for count, giving 1-8.

In order to improve efficiency tile type $1C (one of the keys) has been given a double meaning. $1C with a count greater than 1 is interpreted as tile 0 (air) with a count of 9-15. This addition knocked nearly 200 bytes off the total, going down to 1995.

Today's main work has been to counter another problem. The 'earth' uses a collection of 10 tiles and tends to compress badly, as the runs are interrupted by changing from one earth tile to another.

The solution was to reduce all the 'earth' tiles to a single tile, $0F. This is processed by the compressor and leads to much better compression. Then the map draw routine processes all earth tiles, based on the surrounding tiles, and draws the correct image.

This change took a few attempts to get right (I reused the routine used for map collisions, and had quite a few issues with temporary variables being reused), but the end result is the map data down to 1444 bytes (a 551 byte, or 28% saving) and an overall saving of 454 bytes. Not too shabby! Quite a bit more work to go though, especially as there are another 39 screens still to be added!

#### 3 August 2011

Broke the halfway mark, 39/64 screens now exist. Some redesigning will probably be done before the game's over though. I've got a better idea of how the cavern fits together now.

Also did some work on enemy handling. In both HHH games enemies are defined using a compact 3 byte structure :

`Byte 0 - X and D1, or $FF for end of list`

`Byte 1 - bits 7-3 = Y`

`            bits 2-0 = type`

`Byte 2 - bit 7 - direction`

`            bits 6-0 - D2`

D1 and D2 are 'type specific' but are usually start and finish X coordinates. Type is simply what sort of enemy, eg 1 = bird, 2 = monkey etc. On entering a screen this is expanded to a structure in low memory (page 7 at the moment) which has room for 16 enemies per screen.

After this a per-type function is called each frame for movement, then a generic function handles collision detection.

In HHH1 there was an exception to this - Big Kong. BK used some global variables to handle the tracking of barrels. This worked simply because there was only one BK per screen.

A new exception has had to be added for HHH2 - the Hyper Viper. HV consists of several sprites, moving along the bottom of several screens. In order to keep track of this, his location is entirely held in global variables, and a completely separate function has to be called so he moves correctly even when off screen. Each of his 'segments' have to be separately tracked (which makes him not really a viper, but he looks good) - I originally tried to have the segments calculated based on the location of his head, but this caused problems when he was only partly on screen.

With the constraints of the existing sprite engine, this took a few attempts to get right - but he now works quite well methinks (he's certainly a better way of blocking of an area than just another door + key). The only tradeoff is minor slowdown - when all 6 segments are on screen, processing takes longer than the normal 2 frames and you get minor slowdown and flicker. Worth it though I think.

Another change is to allow for vertically moving enemies - reusing the bird sprites in this case. This just means having another enemy type, where the X and Y coordinates are transposed. Just changing the drawing routines means that the existing (horizontal) movement routines can be reused.

#### 17th August 2011

Took a little time off to work on other projects, but back to HHH2. Today's addition is switches. These are used to turn on/off conveyors, to move objects (maybe) or to make areas more/less accessible.

Each switch is an enemy type combined with tile $B. The tile is merely to stop Harry walking through the switch. In order to track switch states, D2 in the sprite structure has been used as a zero page address (though only $00-$7F due to the top bit having a different purpose) containing a switch state. These are used to enable/disable palette animation in the vsync IRQ handler. There is an exception (as ever!), for the master power switch. Messages pop up on screen when enabling master power, or when trying to enable a conveyor when power is off, so that the player doesn't have to rush back to the instructions to see why pressing switches isn't doing anything.

Note, however, that while having the power on enables conveyors, it might enable some other, less helpful, things as well...

#### 19th August 2011

Implemented boulders today. These follow conveyor belts (Harry isn't strong enough to push them) and form something of a puzzle element.

Also juggled memory about a bit. Tiles are now in low memory (below $D00) which leaves about 1.6kb free. This should be just about enough memory for the remaining 25 screens - in theory anyway...

#### 26th August 2011

Another 9 screens, 16 to go. Nearly there... And nearly out of memory. Again. Why did I insist on writing this in MODE 2?

#### 27th August 2011

Another 7 screens done, and most of the game done now. Remaining screens are for after the final door and for the boss! Only 200-odd bytes left so some serious memory-saving needed!

#### 30th August 2011

Another 4 screens, and the endgame is done. Which took up about half a k, and after some more space-saving there's only 76 bytes left. Got to get more memory back somehow (eg removing subtitles, see the forum) as there are 5 screens left to do! Unless I cheat.

#### 31st August 2011

Loads more enemies added, plus more screens. HHH2 is now playable from start to completion, though some tweaks are probably needed.

Things left to do :

- Make Harry vulnerable - Do something with the remaining two screens (maybe) - Add time limit (time takes place of score + lives in HHH2, as all completed games would have the same score) - More testing!

#### 1st September 2011

Most of the above is finished. Which means HHH2 is now essentially finished! Just needs testing.

I did start on an Electron port but decided to scrap it for sanity reasons.

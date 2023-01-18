# White Light by Sarah Walker

### Licence

Software licence TBC

### Introduction

*White Light* is an unofficial sequel to *[FireTrack](http://en.wikipedia.org/wiki/Firetrack)*, publisher Electric Dream's 1987 vertically scrolling shoot-'em-up classic by Orlando. *FireTrack*, later re-released by Superior Software, was loosely based on Tehkan's 1984 arcade game *[Star Force](http://en.wikipedia.org/wiki/Star_Force)* and has long been regarded as one of the most technically advanced games ever made for the BBC Micro.

[Discuss White Light](http://www.retrosoftware.co.uk/forum/viewforum.php?f=49)

### Features

-   Runs at 50 frames per second (scrolling at 25)
-   Multi-loading - a new set of graphics and enemies for each level
-   Weapons can be upgraded through four power-up levels (and will be increased from this!)
-   [Parallax scrolling](http://en.wikipedia.org/wiki/Parallax_scrolling)
-   Supports full use of [BeebSID](BeebSID "wikilink") add-on for background music

### Sample Screenshots

<table>
<tbody>
<tr class="odd">
<td><p>[[Image:Wl2016_title.png|256px|<em>'White Light title screen <strong><br />
<em>Posted: Apr 17, 2016</em>]]<br />
</strong>White Light title screen</em>'<br />
<em>Posted: Apr 17, 2016</em></p></td>
<td><p>[[Image:Wl2016_classic.png|256px|<em>'A familiar looking level <strong><br />
<em>Posted: Apr 17, 2016</em>]]<br />
</strong>A familiar looking level</em>'<br />
<em>Posted: Apr 17, 2016</em></p></td>
</tr>
<tr class="even">
<td><p>[[Image:Wl2016_land.png|256px|<em>'Hitting the planet surface <strong><br />
<em>Posted: Apr 17, 2016</em>]]<br />
</strong>Hitting the planet surface</em>'<br />
<em>Posted: Apr 17, 2016</em><br />
</p></td>
<td><p>[[Image:Wl2016_fleet.png|256px|<em>'Attacking the fleet <strong><br />
<em>Posted: Apr 17, 2016</em>]]<br />
</strong>Attacking the fleet</em>'<br />
<em>Posted: Apr 17, 2016</em><br />
</p></td>
</tr>
</tbody>
</table>

### Sample Video

[`White` `Light` `AVI` `Video`](./images/White Light preview 2.zip "wikilink")` (190 KB zipped, expands to 2.0 MB) (19 June 2009)`
[`White` `Light` `AVI` `Video`](./images/White Light preview.zip "wikilink")` (261 KB zipped, expands to 3.2 MB) (28 April 2009)`
[`White` `Light` `Wakefield` `2016` `demo`](http://www.youtube.com/watch?v=rUPjLI-KeOg)` (17th April 2016)`

### Development Diary

#### 16th July 2016

Finally got John's levels crammed into the game. In addition to the RLE compression previously used for level data, I've added an LZ77-type scheme (where data earlier in the compressed stream can be referred to later via an offset/size pair) which saves a few hundred bytes. As well as that I've limited the number of tiles available to 56 (saving another 512 bytes), limited the number of sprites to 16, and packed the enemy wave definitions in with some of the tiles. I did also have to remove the sound engine. However, the levels now fit and are playable, and look great!

![](./images/Wl2016 20160716 1.png "fig:Wl2016 20160716 1.png") ![](Wl2016 20160716 2.png "fig:Wl2016_20160716_2.png")

#### 10th July 2016

Got the first level from John (after fixing some embarrassing bugs in the level editor!). Looks fantastic but as-is it's too big to fit in the game. Looks like I need to improve the level compression.

#### 9th July 2016

John Blythe (Dethmunk) has offered to do graphics! This is excellent news as I am an appalling artist.

#### 28th June 2016

Used up most of the remaining memory on a basic sound effects engine. I did consider using the OS sound handler, but as that would involve allowing the OS IRQ handler to run I decided against it and wrote a basic engine of my own. It's pretty basic - has frequency + delta, volume + delta, channel number and sound length - but having even basic sound is quite an improvement! I just hope I can claw back enough memory for music at some point.

#### 27th June 2016

Added more enemy types.

#### 23rd June 2016

Optimised memory usage a bit - now a whole 536 bytes free! Bet that will last long...

#### 16th June 2016

Added some more wave types. Ran out of memory (again!)

#### 8th June 2016

Had a play with defining enemy waves, now that the editor supports it. I've confirmed that the current enemy limits (16 enemies on screen at once, ~512 bytes for wave definitions per level) provides for adequate levels of mayhem; I had been worried that I was going to do more re-work to free up memory / CPU time! I added a couple of static enemy types - a completely static box/crate thing for releasing powerups, and a gun turret. But I think more will be needed, at present the enemy waves feel a tad repetitive.

#### 6th June 2016

Level editor now supports enemy positioning. Seems to work, though my UI design leaves something to be desired. I think if I try this sort of project again I will write the editor in something other than plain C.

![](./images/wl2016 editor.png "wl2016_editor.png")

#### 2nd April 2016

Finished up demo for Wakefield. This involved :

-   Restoring the 'attract mode'
-   Adding a basic level selector - a bit tricky, as by the time it's invoked the game has trashed VDU workspace
-   Re-enabled player vulnerability, which has been disabled for a while
-   Sorting out an enemy roster - currently this is present in the game code rather than level data (as it isn't supported by the editor yet), so it's a fixed pattern for every level
-   Put together some kind of level end - the scrolling now stops at the end of the level, but as there's no boss type thing to destroy the game just goes on until the player is killed
-   Bug fixes!

#### 1st April 2016

Implemented powerups. Powerups are generated when a group of enemies are destroyed, and will also be generated once certain ground structures are destroyed (once I implement them!). Currently four types of powerup - smartbomb (not yet implemented), 'spread', 'pulse' and 'multiple'. Random number generator isn't doing a very good job of randomly selecting them though...

#### 28th March 2016

Started creating 'land' tileset, influenced a little by Xevious, and 'fleet' tileset, influenced by Star Force. My current plan is to alternate between space, land, and fleet/comspace levels, with about 5 sets in total (15 levels).

#### 25th March 2016

Added a few more enemy behaviours. Also re-added the ability for enemies to shoot, which got broken at some point a while back.

#### 23rd March 2016

Some experimentation with tilesets, nothing usable yet.

#### 12th March 2016

Some playing around with palettes. Added palette selection to the editor, which does make life a bit easier.

#### 8th March 2016

Added some more sprites, including the ship banking left/right sprites that DaveM kept asking for.

#### 7th March 2016

Fixed up a couple of crashes caused by the last few changes to the game.

#### 4th March 2016

Started modifying the game to handle the new output of the level editor. Discovered in the process quite how little memory is left! I suspect this is something that is going to be a running theme...

#### 13th February 2016

Added a basic sprite editor to the level editor. Very primitive, and needs more work!

#### 31st January 2016

Started altering the level editor to handle the new reality of 2bpp graphics.

Also created a 'classic' Firetrack tile set as an exercise.

#### 24th January 2016

Been coming to terms with an issue I've been aware of for a while now - that there just isn't enough memory for 4 bits-per-pixel tiles and sprites. This limits the game to 32 tiles and a handful of sprites, which are not enough! With the existing limit it's not even possible to use a Firetrack tileset. In addition the routines for plotting 4 bpp sprites and restoring the background just aren't fast enough.

Instead I've reverted to how Firetrack does it - split the 4 bpp screen in half, using 2 bpp for sprites and 2 bpp for tiles.

This has some benefits - more graphics (as sprites and tiles are now effectively interleaved in memory), faster sprite plotting (as masking is no longer required - just replace the sprite half of screen data with the new sprite) and faster sprite erasure (just mask the affected screen data with 0xf0).

This does have the obvious disadvantage of reducing the available colours. Firetrack often uses the same colours for sprites and background, which make it look like a MODE 5 game. It should be possible to mitigate this using palette splitting though.

#### 20th August 2013

Implemented destructible tiles, so that you can shoot at bits of map. After some fun concurrency issues this now mostly works, though there is an odd issue where collisions aren't detected correctly on some rows.

#### 17th August 2013

Added more enemy types, using the new enemy logic. I added a new 'spawn' type, to reduce the size of the enemy list data; this should also allow enemies to be grouped, to allow for extra points and powerups when destroying all in a group.

Enemies can now also fire back at the player, though there's no collision detection for this yet.

#### 14th August 2013

Changed how enemy logic routines worked. WL used to have the typical state machine type code, but now uses a co-operative multi-threading-like system blatantly 'inspired' by SCi's UFO system (used on Silkworm, SWIV, etc; described in [1](http://www.codetapper.com/amiga/interviews/john-croudy/)), mainly because it sounded interesting. This should make it easier to develop complex enemy behaviour.

#### 3rd July 2013

Changed how the main loop functions, particularly with regard to enemies.

So far, White Light has had a regular main loop, triggered by a flag set by the vsync interrupt handler. In order to have a decent number of enemies on screen, enemy plotting is 'strobed', so of the 12 available, 3 are updated per frame. This works, but is a bit inflexible - enemies with smaller sprites could execute quicker, and with more on screen, but with this scheme the numbers are fixed.

Now though, all non-enemy-plotting related functions run in the interrupt handler, on the 50Hz tick, with the regular main loop dedicated to enemy plotting. Enemy logic is run from the interrupt handler, which sets a flag for the main loop to begin drawing.

This is much more flexible, and the benefits can easily be seen in-game; now when only a couple of enemies are on screen they run at 50 fps, with the framerate dropping as more appear. This setup is more complex than normal - enemy sprite routines now have to be completely seperated from everything else (as otherwise the interrupt routine would cause variable corruption) and there were quite a few bugs to be fixed. Anyone who's ever tried multi-thread programming would recognise some of the issues I've had - not quite as bad, but not far off at times!

#### 30th June 2013

Wrote a new level editor. The old one was, frankly, crap, and the new one is better; somewhat better laid out and more logical to use, and with a normal Windows GUI. It also includes a tile editor, which is handy!

#### 29th June 2013

Some internal reorganisation of code. White Light was not very well written, and was in need of desperate improvement! It's now better, though there's still far too much uncommented code and the use of zero page variables is extremely messy.

I also spend some time trying to do some game design. Part of the reason White Light stalled back in 2009 was that there was no real idea of what the game was to be - there was a vague idea that it should be a sort of unofficial sequel to Fire Track (hence the name, derived from the subtitle 'Search for the White Light'), but this lead to no real ideas other than 'throw in everything you can think of'. I therefore spent some time with Fire Track, attempting to come up with some solid design :

- I don't think White Light will follow Fire Track's ending; "Pulled into the spiraling vortex, you re-emerge in strange alien surrounding" sounds pretty vague and would lead to the open ended design that WL's already suffered from.

- This does present the question of what the 'White Light' actually is. Maybe it's stated somewhere, I haven't personally seen an answer.

- Ending each level by destroying power generators works for me, but the implementation is a little dull in FT - a fixed background with the regular enemies over it. I think WL can keep the idea but make it feel a bit more boss-like.

- I think some of the levels could be on land, destroying planet-based generators. Not sure if this entirely fits with FT's 'story', but WL is only a spiritual sequel rather than an actual one, so I think I can get away with it.

- Enemies feel slightly odd in FT; they're not connected to the level at all, simply being a few basic patterns repeated over and over, feeling more like they belong in something like Zalaga rather than a scrolling shooter. WL will implement them properly!

#### 27th June 2013

Background plotting is now working, and is looking to be worthwhile.

It is a bit slower, but this can be partly mitigated by aligning enemy sprites. Of the four possible alignments vs a tile, only one requires an additional horizontal tile to be plotted. For enemies that only move vertically, it's trivial to position them to avoid this and hence save 1/3 of erasure cost.

While I was looking at the sprite routines, I also decided to implement proper masking. To date, sprites have only been masked on a whole-byte basis, with the inner loop looking like :

lda (src),y beq + sta (dst),y \*

This is obviously quite quick, but looks pretty ugly! I decided to take the speed hit to mask them properly, using a 256-entry mask table to avoid having to store separate masks. I reduced the sprites to 16 lines (from an odd 19) to compensate - this also reduced how much background needs to be plotted.

#### 26th June 2013

Picked up White Light again, let's see how long I stick with it this time.

Altered how background is saved & restored when plotting sprites.

Up until now White Light has stored the background before plotting sprites and restored it afterwards. This is normally a reasonable technique, but as WL is extremely short of memory (less than 16k available!), I decided this was unworkable.

Instead WL now just replots the background on top of the sprite when erasing. This required the game to keep track of what tiles are actually on screen, but requires only a 256 byte buffer - much better than the several K that the background store required! This is potentially slower, as in order for this to work the tiles plotted have to be correctly aligned and this may involve more plotting more than is strictly necessary.

It's not quite working 100% yet, so I don't yet know if it will be good enough to stay.

#### 23 June 2009

Re-ordered drawing routines - stars no longer disappear when things get busy, but slightly more flicker on enemies. Added a new, more 'sweeping' fire mode.

#### 20 June 2009

Increased the number of enemies on screen from 4 - initially I wanted 16 but settled on 12 as 16 flickered too much. Fixed most cases of enemies corrupting the background. Also we now have a working score!

#### 19 June 2009

Fixed up collision detection. Enemies now have a 'health' of more than one shot - I added the ability to flash enemies white so this can be seen. Shots no longer pass through enemies.

#### 16 June 2009

Added enemy collision detection - you can now shoot enemies, and they explode! Few bugs though. Also decided to keep a proper diary!

#### May 2009

Added proper enemy routines - enemies turn up at pre-defined points in the level (like most shooters, but unlike Firetrack) using pre-defined movement patterns. The menu system was rewritten, it's now possible to back out of the game back to the menu. Also basic music support was added - a music player can be called in the game, in the menu, and during loading. This version was demonstrated at the RCM open day at the end of May, with a SID tune.

#### April 2009

Quite a bit of progress - the game levels were seperated from the main code (so they can be loaded in independantly), and the player gained the ability to shoot. A second level was added (mainly to show the possibility of multiple levels) - it's almost entirely empty. The main first level was also designed around this time, using a new Windows-based level editor.

#### March 2009

After mentioning the existance of the game at Byte Back, I decided to revive it. I added (slightly) proper graphics, and a few other effects such as parallax scrolling stars.

#### November 2008

Work started, under the pretence of being a different type of game altogether. A basic scrolling demo gained player control, and some basic enemy routines. I intended to show this (privately) at the Retro Computer Museum open day, but for various reasons this never happened. The game was then shelved for a few months.

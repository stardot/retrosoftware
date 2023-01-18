## Castle Raider Development Diary

### Part 4

***by David Boddie***

See the main [Castle Raider](Castle_Raider "wikilink") page for information about the game itself.

I've split the diary into separate parts. See [Part 1](Castle_Raider/DevelopmentDiary "wikilink"), [Part 2](Castle_Raider/DevelopmentDiary/Part2 "wikilink") and [Part 3](Castle_Raider/DevelopmentDiary/Part3 "wikilink") for earlier entries.

An overview of some of the development issues can be found on the [Thoughts](Castle_Raider/DevelopmentDiary/Thoughts "wikilink") page.

#### Variations (2014-12-07)

|                                                                                                                                                                           |
|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <img src="Acorn-Electron-enclosed-inlay.png" title="Work in progress Acorn Electron cassette inlay." alt="Work in progress Acorn Electron cassette inlay." width="382" /> |
| **Work in progress Acorn Electron cassette inlay.**                                                                                                                       |

|                                                                                                                                                                  |
|------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <img src="BBC-Model-B-enclosed-inlay.png" title="Work in progress BBC Model B cassette inlay." alt="Work in progress BBC Model B cassette inlay." width="382" /> |
| **Work in progress BBC Model B cassette inlay.**                                                                                                                 |

#### Release (2014-12-11)

I've done the final tests, updated the README.txt file in the archive and uploaded it to [the main page](Castle_Raider "wikilink"). Any fixes that are made now will cause the version number to increase by small increments. The cassette inlays will be uploaded in due course.

#### Following Up (2014-12-13)

We're getting to the end of this *development* diary. I've moved Castle Raider to the [Releases](RetroReleases#Castle_Raider_by_David_Boddie "wikilink") page and added printable cassette inlays for the Electron and Beeb. The latter of these involved a lot of input from Arcadian, who really knows the Micro Power house style very well - that's the result of many years of collecting and preserving Acorn software for which many people are grateful.

Although more entries may appear here, I'm considering starting a separate page that covers the game's development and talks about what went right and what went wrong. When writing this game, I realised that I could have fit more things into Jungle Journey, and I'm sure that Castle Raider could have been designed to include more features - the gameplay might even have turned out differently - had certain decisions been made to favour some features instead of others.

#### Adding Information (2015-01-08)

I have released version 1.0.2 which only updates the UEF files to contain chunks for title, instructions and license information. I'm not sure how many tools understand these informational chunks, but at least these binary files now contain license information.

#### Following Up Again (2015-01-11)

I started writing the [Thoughts](Castle_Raider/DevelopmentDiary/Thoughts "wikilink") page to discuss some of my thoughts about development of the game.

#### Read Only Remix (2015-03-21)

It would be nice to have a version of the game that runs on the [Mega Games Cartridge](http://stardot.org.uk/forums/viewtopic.php?f=1&t=8246). Unlike Jungle Journey, Castle Raider is quite a small game if you don't count the loader - and it's still not very large even if you do. In fact, until I started to consider making a cartridge version, I hadn't really thought about how much code and data it needs in memory at run-time. It turns out that it's much less than the 16K allowed for a single ROM, and preliminary work reveals the total to be less than 12K, which is not so surprising given that the cassette/disk version has to fit into that amount of space anyway. This got me thinking about the amount of memory traditionally available for games.

When I was younger, I was a bit disappointed that the Electron was only supplied with 32K of RAM when it could support 64K. Of course, the machine needed an operating system and can only address 64K of either RAM or ROM, and while there are ways to overlay banks of these so that you can access more than 32K of RAM while still having access to system routines, that was fairly academic given that there was only 32K in the standard machine. Now, if you only need the memory to hold code then you can rely on the operating system's own ROM paging mechanism to use code stored in additional ROMs, but that required either extra ROMs to be fitted to the machine or the use of ROM cartridges or ROM slots. If the standard machine had included its own external ROM or cartridge slots then maybe more games would have been published on ROM, though I don't know if that would have been economically viable.

One of the inefficient things about ROMs, however, is that while you can include 16K of code and data per ROM, unless you use main memory to hold lots of working data or read in more code and data from cassette or disk, programs distributed on ROM are not going to make full use of the available memory. Perhaps some resources could be supplied in compressed form on ROM and unpacked into RAM. In any case, using a ROM gives us a bit more space to play with than would be otherwise available, especially if we use the two slots in each cartridge to provide 32K of code and data, so it seems ungrateful to complain about wasted RAM. You could use 20K for screen memory to keep the RAM wastage as low as possible.

Anyway, the plan for a ROM version of Castle Raider is to only use one ROM. If there is any free space, I hope to use it to include a couple of extra features.

#### Slowing Things Down (2015-03-22)

The BBC version of Castle Raider was initially found to run too quickly. If you look at the code, you'll see that I just inserted additional delays where I wait for the next vsync, meaning that I drop a frame intentionally just to make the game playable. The Electron didn't have this problem. However, when running from ROM under Elkulator, the game is now unplayably fast, with associated flickering. Adding another wait-for-sync slows things down again, but it feels just a bit too slow. Further experiments are needed to see if there's a way we can keep things smooth but not too quick.

#### Making Choices (2015-03-24)

With plenty of room to spare in the 16K ROM, we can include some things in the game that were previously in the loader. One of these is the character selection screen. At the moment, only keyboard support is implemented for this, but now it occurs to me that a left/right joystick choice, a bit like the one in Arcadians, could also be good to implement.

|                                                                                                                                                 |
|-------------------------------------------------------------------------------------------------------------------------------------------------|
| <img src="2015-03-24-choice.png" title="Choosing a character in the game itself." alt="Choosing a character in the game itself." width="256" /> |
| **Choosing a character in the game itself.**                                                                                                    |

#### Making an Entrance (2015-05-10)

When I originally wrote the music, I had problems queuing the notes, so I wrote some code that supposedly waited for the channel 1 sound buffer to clear before playing each new note. I'm not even sure that it really worked correctly, but it turned out to be broken in the ROM version and unnecessary in the other versions. I reverted to code that simply plays the notes in a loop, using the OSWORD 7 call with a sound channel value that causes the routine to return only when the note has been played. However, this still didn't work in the ROM version.

Some experiments later and it turns out that utility ROMs didn't suffer from this problem, but language ROMs did, so it was time to turn to the collective wisdom [of the Retro Software forum](http://www.retrosoftware.co.uk/forum/viewtopic.php?f=73&t=939). To cut a long story short, I needed to ensure that interrupts are enabled when the language ROM is entered. There are other things that are required, and these are mentioned in section 9.1 of the Electron Advanced User Guide. Things like checking that the accumulator is 1 when the entry code is called and returning otherwise, and resetting the stack pointer. With these things in place, the music plays as intended and a [new release was duly made](http://www.retrosoftware.co.uk/wiki/index.php/Castle_Raider#Downloads).

I had considered adding more features to the ROM version - there are apparently 5160 bytes free - but I'm not so motivated to do so at the moment. It would be easy to add a bit more to the game completion code and even easier to add extra bits to the levels, but I don't have a clear idea of what I would do, so it's probably best to leave it for now.

#### Post Script - Screen Banks (2015-09-14)

While looking for articles describing the ULA, I found an article called *We're taking control* ([first](http://acornelectron.co.uk/mags/eu/ills/7_07/s-p28.jpg) and [second](http://acornelectron.co.uk/mags/eu/ills/7_07/s-p29.jpg) pages) from the April 1990 issue of Electron User, which I seem to vaguely recall reading at some point. The third program in the article uses bank switching to perform flicker-free animations. It's interesting to see that this technique was published during the Electron's heyday.

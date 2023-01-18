# MazezaM by Kian Vincent

### Licence

[GNU GPLv3 license](http://en.wikipedia.org/wiki/GNU_General_Public_License)

### Introduction

In November of 2010 I came across this block sliding puzzle game, by Malcolm Tyrrell, on World Of Spectrum and very quickly became hooked.

The notes from the author positively encouraged conversion to other platforms and after finishing the many other projects which I had on the go at the time - and a few which cropped up in-between - the Easter holidays of 2011 finally gave me the opportunity to have a go.

During this time I wrote a version for the PC, closely followed by one for the TI-83/84 Plus calculators. The following half term I succumbed to the urge to convert it to the BBC. Un-daunted by the very odd way that the Beeb stores its Mode 2 graphics - well, all modes really - and while 6502 asm was never my language of choice, I ploughed on and produced the version found here. This is despite not having used it since I was at school about 25 years ago (how many times should one person have to write a machine code bubble sort ???), when the best I managed was the somewhat ubiquitous 'Snake' program, so the code isn't the neatest in the world, but it works :). I managed to squeeze the program under a Mode 2 graphics screen with 3 bytes to spare, and with plenty of levels and oodles of delicious 8-bit colour.

The game uses the original 'MazezaMs' provided with the Spectrum version, along with the extended set of 'MazezaMs' provided with Malcolm's quite frankly mind-boggling 1k ZX81 version of the game, all of which Mr. Tyrrell kindly made available to me and for which he still retains the copyright.

There are also 8 levels of my own design, taken from my PC remake. They're easy to spot because they are the ones with the distinctly amateur edge to them - although I'm quite proud of 'Duck Commander' and 'The Wumpus Room'. This version contains a total of 39 different levels.

Since then I have created another 3 level sets:

**MazezaM II - Monstrous MazezaM** - _just that bit harder_

**MazezaM In Da 80s** - _these levels were created in The Lass at In Da 80s in the summer of 2011. There is a level for each year of the 80s and, unless anyone can prove me wrong, each can be completed in a number of moves identical to the year number._

**MazezaM III - Malevolent MazezaM** - _As mind-bending as cauliflower custard_

When I let loose the first version of MazezaM, DaveM suggested that a level designer would be kind of nice. It has taken me a while to get round to this one. After many an abortive start and miriad complete rewrites, **MazezaM Designer** will allow you to create, test and compile your own levels as a completely standalone game.

Any thoughts or comments are always welcome - any feedback would be greatly appreciated. I hope you enjoy this game as much as I have.

Kian

[Discuss _MazezaM_](http://www.retrosoftware.co.uk/forum/viewforum.php?f=75)

Read more about the original 2002 ZX Spectrum release of _[MazezaM](http://www.worldofspectrum.org/infoseekid.cgi?id=0014525)_ at _World of Spectrum_, or Kian's other ports to Windows, DOS, TI-83/84+ calculators, Linux, GP2X & Mac at his own developer site, _Glass Fractal Software_: _[MazezaM](http://www.glassfractal.com/games/MazezaM/)_.

### Platforms

#### BBC Micro Model B/Master 128 & Electron

**_Port by Kian Vincent_**

##### Port Details

You must escape from the MazezaMs by navigating through each maze.

From the title screen, press any key to start.

Use the 'Z','X','\*' and '?' keys to move.

Blocks may only be moved by pushing, not pulling.

If you should become trapped, then pressing the 'Esc' key will restart the current level, but lose you 1 of your lives.

To quit to the title screen press the 'Q' key.

Should you be completely defeated by a particular level, then pressing 'f1' will skip to the next one. ('0' on the Elk)

The archives for the BBC & Electron versions contain full instructions for the level designer but it should, by-and-large, be reasonably easy to follow.

##### Downloads

The disc image will autoboot or can be run using ' CH."LOADER" '.

<span style="font-variant:small-caps">BBC Micro Model B/Master 128:</span> [MazezaM Complete v1.0](../../retrosoftwarecouk*wiki-20160918-wikidump/images/MazezaM Complete v1.0 BBC.zip "wikilink") - \_Contains 4 level sets and level designer. The archive also contains separate tape images of the 4 level sets, plus artwork for both disk and tape versions and an 'Instructions' insert. Finally, after being thoroughly inspired by Jason Kelk's type-in game in Retro Gamer \#100, I have also thrown in a type-in listing for them, although I don't expect anyone to be foolhardy enough to ever use them.*

<span style="font-variant:small-caps">Electron:</span> [MazezaM\_Elk\_Complete\_v1.0](../../retrosoftwarecouk*wiki-20160918-wikidump/images/MazezaM Elk Complete v1.0.zip "wikilink") - \_Now with designer, joystick support and nicer selection screen too.*

<span style="font-variant:small-caps">Source code:</span> [MazezaM source files](../../retrosoftwarecouk*wiki-20160918-wikidump/images/MazezaM sources BBC %26 Elk.zip "wikilink") - \_Complete source files for both BBC & Electron versions*

###### Older versions

<span style="font-variant:small-caps">BBC Micro Model B/Master 128</span>

The disc image will autoboot or can be run using ' CH."MENU" '.

[MazezaM v2.1](../../retrosoftwarecouk*wiki-20160918-wikidump/images/MazezaMGemini 2 1.zip "wikilink") - \_A couple of levels shifted about for a steadier learning curve and level 10 made a wee bit sneakier.*

[MazezaM v2.0](../../retrosoftwarecouk_wiki-20160918-wikidump/images/MazezaMGemini.zip "wikilink") - _Version 2 includes another 39 levels to make your brain ache just a little bit more._

'The disc image will autoboot or can be run using ' CH."LOADER" '.

[MazezaM v1.33](../../retrosoftwarecouk_wiki-20160918-wikidump/images/MazezaM BBC v1 33.zip "wikilink") - ''Another improvement inspired by work on the Electron version. The ghosting effect was much less noticeable on the Beeb but, once you know it's there ... ''

[MazezaM v1.32](../../retrosoftwarecouk_wiki-20160918-wikidump/images/MazezaM BBC v1 32.zip "wikilink") - ''While working on the Electron version I had to come up with a faster routine for drawing the background bricks. This new routine was subsequently used in the Beeb version too. ''

[MazezaM v1.31](../../retrosoftwarecouk_wiki-20160918-wikidump/images/MazezaM BBC v1 31.zip "wikilink") - ''Found the bug preventing the game from running on the Master. ''

[MazezaM v1.3](../../retrosoftwarecouk*wiki-20160918-wikidump/images/MazezaM BBC v1 3.zip "wikilink") - \_I have moved the code down 1 page to &1800 to make room for my 'The Wumpus Room' level and a little bit of future tinkering. This also entailed a small amount of recoding as it is wider than all the other levels. So long as I haven't made any calamatous mistakes and this survives the no doubt vigorous play-testing that it will receive, then it should be the version promoted to 'release' status.*

[MazezaM v1.2](../../retrosoftwarecouk*wiki-20160918-wikidump/images/MazezaM BBC v1 2.zip "wikilink") - \_Just a few minor tweaks this one. Moved some storage into zero page for added oomph and also saved a few bytes in the process.*

[MazezaM v1.1](../../retrosoftwarecouk*wiki-20160918-wikidump/images/MazezaM BBC v1 1.zip "wikilink") - \_Thanks to Pitfall and Dave M, the 'Up' and 'Down' keys have now been remapped to make them more Beeb-like, as has the 'Restart' function which is now via the 'Esc' key. Added spanky new 'Retro Software' loading screen. Saved a few bytes. Added a few more. Now have 15 bytes free.*

[MazezaM v1.0](../../retrosoftwarecouk_wiki-20160918-wikidump/images/MazezaM BBC.zip "wikilink")

[MazezaM In Da 80s](../../retrosoftwarecouk_wiki-20160918-wikidump/images/MazezaMInDa80s.zip "wikilink") - _A special set created in honour of the 2011 event._

<span style="font-variant:small-caps">Electron</span>

[MazezaM\_All-In-One\_Elk v1.0](../../retrosoftwarecouk*wiki-20160918-wikidump/images/MazezaM All-In-One Elk v1.0.zip "wikilink") - \_All 4 level sets from the Beeb version in one place plus tape images and tape artwork.*

[MazezaM\_Elk v2.1](../../retrosoftwarecouk*wiki-20160918-wikidump/images/MazezaMElk 2 1.zip "wikilink") - \_The levels in set 1 have now been adjusted in line with the Beeb version.*

[MazezaM\_Elk v2.0](../../retrosoftwarecouk_wiki-20160918-wikidump/images/MazezaMElk 2 0.zip "wikilink") - ''Now comes with MazezaM II - Monstrous MazezaM ''

[MazezaM\_Elk v1.21](../../retrosoftwarecouk_wiki-20160918-wikidump/images/MazezaMElk 1 21.zip "wikilink") - ''Put back the missing !BOOT file. ''

[MazezaM\_Elk v1.2](../../retrosoftwarecouk_wiki-20160918-wikidump/images/MazezaMElk 1 2.zip "wikilink") - ''Got rid of the nasty ghosting which occurred during scrolling. ''

[MazezaM\_Elk v1.1](../../retrosoftwarecouk_wiki-20160918-wikidump/images/MazezaMElk 1 1.zip "wikilink") - ''Prettier title screen, more consistent movement speed and less hanging around at the end of a level. ''

[MazezaM_Elk v1.0](../../retrosoftwarecouk_wiki-20160918-wikidump/images/MazezaMElk.zip "wikilink") - ''A little rougher round the edges, but working. ''

##### Screenshots

<table>

<tbody>

<tr class="odd">

<td><p><img src="Mazezam-spectrum.png" title="fig:Original ZX Spectrum Title Screen Posted: Wed Jun 08, 2011 23:05" alt="Original ZX Spectrum Title Screen Posted: Wed Jun 08, 2011 23:05" width="256" /><br />

<strong>Original ZX Spectrum Title Screen</strong><br />

''Posted: Wed Jun 08, 2011 23:05<br />

</p></td>

<td><p><img src="Mazezam-loadingscreen.png" title="fig:BBC Micro Loading Screen Posted: Wed Jun 08, 2011 23:58" alt="BBC Micro Loading Screen Posted: Wed Jun 08, 2011 23:58" width="256" /><br />

<strong>BBC Micro Loading Screen</strong><br />

''Posted: Wed Jun 08, 2011 23:58<br />

</p></td>

<td><p><img src="Mazezam-titlescreen.png" title="fig:BBC Micro Title Screen Posted: Wed Jun 08, 2011 23:59" alt="BBC Micro Title Screen Posted: Wed Jun 08, 2011 23:59" width="256" /><br />

<strong>BBC Micro Title Screen</strong><br />

''Posted: Wed Jun 08, 2011 23:59<br />

</p></td>

</tr>

<tr class="even">

<td><p><img src="Mazezam-ingame1.png" title="fig:BBC Micro In-Game Screenshot Posted: Wed Jun 08, 2011 21:54" alt="BBC Micro In-Game Screenshot Posted: Wed Jun 08, 2011 21:54" width="256" /><br />

<strong>BBC Micro In-Game Screenshot</strong><br />

<em>Posted: Wed Jun 08, 2011 21:54</em><br />

</p></td>

<td><p>[[Image:elksc.png|256px|<strong>Electron Title Screen</strong><br />

<em>Posted: Thu Apr 12, 2012 11:23]]<br />

<strong>Electron Title Screen</strong><br />

</em>Posted: Thu Apr 12, 2012 11:23<br />

</p></td>

<td><p>[[Image:Designer.png|256px|<strong>BBC Micro level designer Screenshot</strong><br />

<em>Posted: Thu Apr 12, 2012 11:16]]<br />

<strong>BBC Micro level designer Screenshot</strong><br />

</em>Posted: Thu Apr 12, 2012 11:16<br />

</p></td>

</tr>

</tbody>

</table>

##### Video

{{\#ev:youtube|otLhF26FYPY}}

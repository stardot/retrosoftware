# BBC Micro Z-Machine v1.1 (Infocom v3-5) Interpreter by Jon Welch

### Licence

This software is copyrighted [freeware](http://en.wikipedia.org/wiki/Freeware) and can be used for commercial or non-commercial purposes.

### Introduction

**PROJECT STATUS: *On Hold.***

The initial version will be written in BBC BASIC. This will require an ARM co-processor (emulable in BeebEm) or a machine running Risc OS to run, and will be very slow. UPDATE: The BASIC version is pretty much done with and is available to download below.

This version will feed into the development of a native 6502 assembler version, which is aimed at a BBC Micro Model B+ or Master 128 with a standard Acorn DFS disc drive. Features below will be implemented based purely on how much memory is available, how fast the assembled version runs, how much slow-down the disk interaction causes etc.

The assembled code will be supplied as a ROM image. Cassette support is not possible due to the size of Z-Machine games (v5 games can potentially reach 256 KB). Games will instead need to be stored on a standard Acorn DFS disc. Exceptionally large games (&gt; 200K) will need to be split across a double-sided disc.

One of the biggest limitations of fitting an interpreter for the larger v4 and v5 games into a machine family as small as the BBC Microcomputer range is that there isn't a lot of memory available for **Dynamic Storage**, which is the section of memory which is constantly written to to keep track of the status of your game. If this area was left on disk, the game would be extremely slow to play. Consequently, the ROM will run in MODE 0 and use all 64K of sideways RAM for dynamic storage plus all the main memory for cache. This should allow it to play v4 and v5 games, hopefully even those that require the largest amount of Dynamic Storage, such as *ZDungeon*, *Curses*, *Beyond Zork*, *A Mind Forever Voyaging* and *Trinity*.

**TESTERS**: We require testers to playthrough games they are intimately familiar with (or are prepared to follow a walk-through). Please volunteer in the forum, if you're willing to try out any of the games listed in the testing matrix below:

[Discuss BBC Micro Z-Machine Interpreter](http://www.retrosoftware.co.uk/forum/viewforum.php?f=30)

*Use [Inform](http://www.inform-fiction.org/) 7 to develop games for the BBC Micro Model B+ / Master 128 and many other modern platforms.*

#### Potential Feature Support

<table>
<caption><strong><em>Features listed below are described in more detail in the<br />
<a href="http://www.inform-fiction.org/manual/html/s42.html">Inform Designer's Manual Chapter VII</a> and in the Z-Machine standards <a href="http://www.inform-fiction.org/zmachine/standards/z1point0/index.html">v1.0</a> and <a href="http://ifarchive.heanet.ie/if-archive/infocom/interpreters/specification/ZSpec11.txt">v1.1</a></em></strong></caption>
<thead>
<tr class="header">
<th><p>Feature</p></th>
<th><p>Used in Z-Machine Version(s)</p></th>
<th><p>Inform 'Available if' test</p></th>
<th><p>Likely to be included<br />
in BBC interpreter?</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Full conformance to <a href="http://www.inform-fiction.org/zmachine/standards/z1point0/index.html">Z-Machine standard v1.0</a></p></td>
<td><p>-</p></td>
<td><p>-</p></td>
<td><p>?</p></td>
</tr>
<tr class="even">
<td><p>Full conformance to <a href="http://ifarchive.heanet.ie/if-archive/infocom/interpreters/specification/ZSpec11.txt">Z-Machine Standard v1.1</a></p></td>
<td><p>-</p></td>
<td><p>-</p></td>
<td><p>?</p></td>
</tr>
<tr class="odd">
<td><p>Support for Z-Machine v3</p></td>
<td><p>3</p></td>
<td><p>-</p></td>
<td><p>YES</p></td>
</tr>
<tr class="even">
<td><p>Support for Z-Machine v4</p></td>
<td><p>4</p></td>
<td><p>-</p></td>
<td><p>YES</p></td>
</tr>
<tr class="odd">
<td><p>Support for Z-Machine v5</p></td>
<td><p>5</p></td>
<td><p>-</p></td>
<td><p>YES</p></td>
</tr>
<tr class="even">
<td><p>Support for Z-Machine v6 and above</p></td>
<td><p>6,8</p></td>
<td><p>-</p></td>
<td><p>NO</p></td>
</tr>
<tr class="odd">
<td><p>auxiliary files</p></td>
<td><p>5,6,8</p></td>
<td><p>(true)</p></td>
<td><p>?</p></td>
</tr>
<tr class="even">
<td><p>coloured text</p></td>
<td><p>5,6,8</p></td>
<td><p>((0-&gt;1) &amp; 1 ~= 0)</p></td>
<td><p>Partial (2 or 4 colour selectable modes)</p></td>
</tr>
<tr class="odd">
<td><p>input streams</p></td>
<td><p>5,6,8</p></td>
<td><p>(true)</p></td>
<td><p>?</p></td>
</tr>
<tr class="even">
<td><p>menus</p></td>
<td><p>6</p></td>
<td><p>(($10--&gt;0) &amp; 256 ~= 0)</p></td>
<td><p>NO</p></td>
</tr>
<tr class="odd">
<td><p>mouse</p></td>
<td><p>5,6</p></td>
<td><p>(($10--&gt;0) &amp; 32 ~= 0)</p></td>
<td><p>NO</p></td>
</tr>
<tr class="even">
<td><p>output streams</p></td>
<td><p>5,6,8</p></td>
<td><p>(true)</p></td>
<td><p>?</p></td>
</tr>
<tr class="odd">
<td><p>pictures</p></td>
<td><p>6</p></td>
<td><p>(($10--&gt;0) &amp; 8 ~= 0)</p></td>
<td><p>NO</p></td>
</tr>
<tr class="even">
<td><p>sounds</p></td>
<td><p>5,6,8</p></td>
<td><p>(($10--&gt;0) &amp; 128 ~= 0)</p></td>
<td><p>NO</p></td>
</tr>
<tr class="odd">
<td><p>throw/catch stack frames</p></td>
<td><p>5,6,8</p></td>
<td><p>(true)</p></td>
<td><p>?</p></td>
</tr>
<tr class="even">
<td><p>timed keyboard interrupts</p></td>
<td><p>5,6,8</p></td>
<td><p>((0-&gt;1) &amp; 128 ~= 0)</p></td>
<td><p>?</p></td>
</tr>
<tr class="odd">
<td><p>Bold / Italic Text</p></td>
<td><p>5,6,8</p></td>
<td><p>-</p></td>
<td><p>?</p></td>
</tr>
<tr class="even">
<td><p><a href="http://www.inform-fiction.org/zmachine/standards/quetzal/index.html">Quetzal</a> portable save-games support</p></td>
<td><p>-</p></td>
<td><p>-</p></td>
<td><p>?</p></td>
</tr>
<tr class="odd">
<td><p>Limited <a href="http://www.eblong.com/zarf/blorb/">Blorb</a> Support (ability to extract Z-code file from blorb file and play it)</p></td>
<td><p>-</p></td>
<td><p>-</p></td>
<td><p>?</p></td>
</tr>
<tr class="even">
</tr>
</tbody>
</table>

### Downloads

***BBC Micro Z-Machine Interpreter - BASIC program on disk image***
*(BBC BASIC, requires ARM co-processor to run)*
Latest "unofficial" release.
<http://www.g7jjf.com/progs/zmach.zip>

***BBC Micro Z-Machine Interpreter - prototype combined ROM image on disk image***
*(6502 assembled machine code, all V3 opcodes implemented and the majority of the V5 opcodes)*
Latest "unofficial" release.
<http://www.g7jjf.com/progs/zcode.zip>

### Sample Screenshots

<table>
<tbody>
<tr class="odd">
<td><p> <br />
<img src="BBCMasterZMachineInterpreter-Adventz5.png" title="fig:BBC Micro Master 128 version of Z-Machine Interpreter running a Z-code port of the original 350 point Adventure / Colossal Cave by Crowther &amp; Woods with a traditional green font colour Posted: Sat May 31, 2008 16:17" alt="BBC Micro Master 128 version of Z-Machine Interpreter running a Z-code port of the original 350 point Adventure / Colossal Cave by Crowther &amp; Woods with a traditional green font colour Posted: Sat May 31, 2008 16:17" width="375" /><br />
<strong>BBC Micro Master 128 version of Z-Machine Interpreter running a Z-code port of the original 350 point <em>Adventure</em><br />
/ <em>Colossal Cave</em> by Crowther &amp; Woods with a traditional green font colour</strong><br />
<em>Posted: Sat May 31, 2008 16:17</em></p></td>
<td><p>[[Image:BBCMasterZMachineInterpreter-TheHobbitz5.png|375px|'''BBC Micro Master 128 version of Z-Machine Interpreter running IntroComp 2005 entry <em>The Hobbit</em> in the colour style of BBC micro adventure <em>The Lord of the Rings: Game One</em><strong><br />
<em>Posted: Sat May 31, 2008 16:33</em>]]<br />
</strong>BBC Micro Master 128 version of Z-Machine Interpreter running IntroComp 2005 entry <em>The Hobbit</em> in the colour style of BBC micro adventure <em>The Lord of the Rings: Game One'<br />
</em>Posted: Sat May 31, 2008 16:33''</p></td>
</tr>
</tbody>
</table>

### Compatibility Testing Matrix

{| cellspacing="20 px" |+ ***Commercial Infocom Games*** ! Game !! Filename !! Z-code
Version !! File
Length !! Tested First Few Moves !! Tested to
Completion On Date !! Tested with
BBC Interpreter
Version !! Tested By !! Dynamic Storage Size |- ! MILLIWAYS: The Restaurant at the End of the Universe Prototype (v. 15.880512) | milliways\_release15.z4 || v4 || 92,928 || - || - || - || - || 6,333 |- ! A Mind Forever Voyaging | amfv.z4 || v4 || 262,018 || - || - || - || - || 31,691 |- ! Bureaucracy | bureaucr.z4 || v4 || 243,341 || - || - || - || - || 18,207 |- ! Nord and Bert | nordandb.z4 || v4 || 170,285 || - || - || - || - || 14,852 |- ! Trinity | trinity.z4 || v4 || 262,065 || - || - || - || - || 37,726 |- ! Beyond Zork | beyondzo.z5 || v5 || 276,480 || - || - || - || - || 25,720 |- ! Borderzone | borderzo.z5 || v5 || 178,373 || - || - || - || - || 21,562 |- ! Sherlock | sherlock.z5 || v5 || 188,445 || - || - || - || - || 16,441 |- ! Leather Goddesses of Phobos Solid Gold (4/880405) | leather.z5 || v5 || 159,928 || - || - || - || - || 15,145 |- ! Hitchhiker's Guide to the Galaxy Solid Gold (31/871119) | hitchhik.z5 || v5 || 184,320 || - || - || - || - || 15,156 |- ! Planetfall Solid Gold (10/880531) | planetfa.z5 || v5 || 136,560 || - || - || - || - || 17,435 |- ! Wishbringer Solid Gold (23/880706) | wishbrin.z5 || v5 || 164,712 || - || - || - || - || 15,424 |- ! ZORK I Solid Gold (52/871125) | zork1.z5 || v5 || 105,264 || - || - || - || - || 15,166 |- |}

{| cellspacing="20 px" |+ ***Games available from the IF Archive*** ! Game !! Filename !! Z-code
Version !! File
Length !! Tested First Few Moves !! Tested to
Completion On Date !! Tested with
BBC Interpreter
Version !! Tested By !! Dynamic Storage Size |- ! Colossal Cave / Adventure
(350 points) | [Advent.z5](http://mirror.ifarchive.org/if-archive/games/zcode/Advent.z5) || v5 || 138,240 || - || - || - || - || 17,864 |- ! Conan Kill Everything | [ConanKillEverything.z5](http://mirror.ifarchive.org/if-archive/games/zcode/ConanKillEverything.z5) || v5 || 91,136 || - || - || - || - || 5,645 |- ! Crobe | [Crobe.z5](http://mirror.ifarchive.org/if-archive/games/zcode/Crobe.z5) || v5 || 89,088 || - || - || - || - || 16,311 |- ! Countdown to Doom | [CtDoom.z5](http://mirror.ifarchive.org/if-archive/games/zcode/CtDoom.z5) || v5 || 132,608 || - || - || - || - || 16,419 |- ! Curses | [curses.z5](http://mirror.ifarchive.org/if-archive/games/inform/curses.z5) || v5 || 259,072 || - || - || - || - || 26,163 |- ! CZECH | [czech.z5](http://mirror.ifarchive.org/if-archive/infocom/interpreters/tools/czech_0_8.zip) || v5 || 13,312 || - || - || - || - || 2,001 |- ! Fyleet | [Fyleet.z5](http://mirror.ifarchive.org/if-archive/games/zcode/Fyleet.z5) || v5 || 137,728 || - || - || - || - || 23,673 |- ! Interactive Fiction: Quake | [quake.z5](http://mirror.ifarchive.org/if-archive/games/zcode/ifquake.zip) || v5 || 133,120 || - || - || - || - || 9,418 |- ! Last Days of Doom | [LDoDoom.z5](http://mirror.ifarchive.org/if-archive/games/zcode/LDoDoom.z5) || v5 || 200,192 || - || - || - || - || 9,418 |- ! Return to Doom | [RtDoom.z5](http://mirror.ifarchive.org/if-archive/games/zcode/RtDoom.z5) || v5 || 179,200 || - || - || - || - || 18,150 |- ! Scott Adams' Marvel Adventure: Hulk | [HULK.z5](http://mirror.ifarchive.org/if-archive/games/zcode/adamsinform.zip) || v5 || 25,600 || - || - || - || - || 6,564 |- ! Scott Adams' Marvel Adventure: Spider-man | [SPIDERMN.z5](http://mirror.ifarchive.org/if-archive/games/zcode/adamsinform.zip) || v5 || 27,136 || - || - || - || - || 8,016 |- ! Strict Z Test | [strictz.z5](http://mirror.ifarchive.org/if-archive/infocom/interpreters/tools/strictz.z5) || v5 || 4,096 || - || - || - || - || 1,509 |- ! TerpEtude | [etude.z5 and gntests.z5](http://mirror.ifarchive.org/if-archive/infocom/interpreters/tools/etude.tar.Z) || v5 || 16,896 and 7,168 || - || - || - || - || 1,514 and 1,216 |- ! ZDungeon | [zdungeon.z5](http://mirror.ifarchive.org/if-archive/games/zcode/zdungeon.z5) || v5 || 188,928 || - || - || - || - || 32,019 |- ! Zork - The Cavern of Doom | [cavern.z5](http://mirror.ifarchive.org/if-archive/games/zcode/cavern.z5) || v5 || 133,120 || - || - || - || - || 7,967 |- ! Zork: The Undiscovered Underground | [ZTUU.z5](http://mirror.ifarchive.org/if-archive/infocom/demos/ztuu.zip) || v5 || 102,912 || - || - || - || - || 10,445 |}

### Change Log

Not released yet

<img src="z-machineinterpreterv3logo.png" title="fig:BBC Micro Z-Machine v1.1 (Infocom v3) Interpreter" alt="BBC Micro Z-Machine v1.1 (Infocom v3) Interpreter" width="400" height="94" />
=   by Jon Welch =

### Licence

This software is licensed under the [GNU GPLv3 license](http://en.wikipedia.org/wiki/GNU_General_Public_License).

### Introduction

The initial version will be written in BBC BASIC. This will require an ARM co-processor (emulable in BeebEm) or a machine running Risc OS to run, and will be very slow. UPDATE: The BASIC version is pretty much done with and is available to download below.

This version will feed into the development of a native 6502 assembler version, which is aimed to fit into a standard BBC Micro Model B with standard Acorn DFS disc drive. Features below will be implemented based purely on how much memory is available, how fast the assembled version runs, how much slow-down the disk interaction causes etc.

The assembled code will be supplied as a ROM image. Cassette support is not possible due to the size of Z-Machine games and the amount memory available on an unexpanded BBC Micro Model B. Games will instead need to be stored on a standard Acorn DFS disc.

One of the biggest limitations of fitting an interpreter for the larger v4 and v5 games into a machine family as small as the BBC Microcomputer range is that there isn't a lot of memory available for **Dynamic Storage**, which is the section of memory which is constantly written to to keep track of the status of your game. If this area was left on disk, the game would be extremely slow to play. Consequently, this standard Model B version will only run Infocom v3 games will be restricted to MODE 7, due to memory limitations of the various MODEs.

**TESTERS**: We require testers to playthrough games they are intimately familiar with (or are prepared to follow a walk-through). Please volunteer in the forum, if you're willing to try out any of the games listed in the testing matrix below:

[Discuss BBC Micro Z-Machine Interpreter](http://www.retrosoftware.co.uk/forum/viewforum.php?f=30)

*Use Inform 6.15 and the BBC Micro Z-Machine Interpreter in the complete [Inform / Z-Machine v1.1 (Infocom v3) Development Environment](BBC_Micro_Z-Machine_Interpreter_informz3 "wikilink") to develop games for the BBC Micro/GameBoy/C64/Spectrum +3 etc.*

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

***BBC Micro Z-Machine Interpreter alpha - BASIC program on disk image***
*(BBC BASIC, requires ARM co-processor to run)*
Latest "unofficial" release.
<http://www.g7jjf.com/progs/zmach.zip> ([local mirror](./images/Zmach.zip "wikilink"))

***BBC Micro Z-Machine Interpreter beta - prototype combined ROM image on disk image***
*(6502 assembled machine code, all V3 opcodes implemented)*
<http://www.g7jjf.com/progs/zcode.zip> ([local mirror](./images/Zcode.zip "wikilink"))

***BBC Micro Z-Machine Interpreter - v1.0 GPL source code and binary executables for v3 and v5 ROMs***
Latest release.
([v1.0 release zip archive](./images/Bbcmicroz-machineinterpreter-1.0.zip "wikilink"))

### Sample Screenshots

<table>
<tbody>
<tr class="odd">
<td><p><img src="BBCModelBZMachineInterpreter-zorkIz3.png" title="fig:BBC Micro Model B version of Z-Machine v1.1 (Infocom v3) Interpreter running Infocom&#39;s Zork I Posted: Sat May 31, 2008 16:16" alt="BBC Micro Model B version of Z-Machine v1.1 (Infocom v3) Interpreter running Infocom&#39;s Zork I Posted: Sat May 31, 2008 16:16" width="375" /><br />
<strong>BBC Micro Model B version of Z-Machine v1.1 (Infocom v3) Interpreter running Infocom's <em>Zork I</em></strong><br />
<br />
<em>Posted: Sat May 31, 2008 16:16</em><br />
 </p></td>
<td><p><img src="BBCMasterZMachineInterpreter-leatherz3.png" title="fig:BBC Micro Master 128 version of Z-Machine Interpreter running Infocom&#39;s Leather Goddesses of Phobos with a racy red font colour Posted: Sat May 31, 2008 16:18" alt="BBC Micro Master 128 version of Z-Machine Interpreter running Infocom&#39;s Leather Goddesses of Phobos with a racy red font colour Posted: Sat May 31, 2008 16:18" width="375" /><br />
<strong>BBC Micro Master 128 version of Z-Machine v1.1 (Infocom v3) Interpreter running Infocom's <em>Leather Goddesses of Phobos</em><br />
with a racy red font colour</strong><br />
<em>Posted: Sat May 31, 2008 16:18</em><br />
 </p></td>
</tr>
</tbody>
</table>

### Compatibility Testing Matrix

{| cellspacing="20 px" |+ ***Commercial Infocom Games*** ! Game !! Filename !! Z-code
Version !! File
Length !! Tested First Few Moves !! Tested to
Completion On Date !! Tested with
BBC Interpreter
Version !! Tested By !! Dynamic Storage Size |- ! Ballyhoo | ballyhoo.z3 || v3 || 153,600 || - || - || - || - || 11,258 |- ! Cutthroats | cutthroa.z3 || v3 || 112,640 || - || - || - || - || 10,826 |- ! Deadline | deadline.z3 || v3 || 122,880 || - || - || - || - || 12,155 |- ! Enchanter | enchante.z3 || v3 || 122,880 || - || - || - || - || 12,653 |- ! Hitchhiker's Guide to the Galaxy (59/851108) | hitchhik.z3 || v3 || 113,664 || - || - || - || - || 9,738 |- ! Hollywood Hijinx | hollywoo.z3 || v3 || 109,651 || - || - || - || - || 12,142 |- ! Infidel | infidel.z3 || v3 || 122,880 || - || - || - || - || 11,773 |- ! Leather Goddesses of Phobos (59/860730) | leather.z3 || v3 || 129,023 || - || - || - || - || 11,436 |- ! Moonmist | moonmist.z3 || v3 || 153,600 || - || - || - || - || 13,860 |- ! Planetfall (29/840118) | planetfa.z3 || v3 || 122,880 || - || - || - || - || 14,288 |- ! Plundered Hearts | plundere.z3 || v3 || 128,963 || - || - || - || - || 9,715 |- ! Seastalker | seastalk.z3 || v3 || 117,763 || - || - || - || - || 12,727 |- ! Sorcerer | sorcerer.z3 || v3 || 122,880 || - || - || - || - || 11,508 |- ! Spellbreaker | spellbre.z3 || v3 || 153,600 || - || - || - || - || 11,394 |- ! Suspect | suspect.z3 || v3 || 122,880 || - || - || - || - || 12,634 |- ! Starcross | starcros.z3 || v3 || 92,160 || - || - || - || - || 10,600 |- ! Stationfall | stationf.z3 || v3 || 153,600 || - || - || - || - || 11,941 |- ! Suspended | suspend.z3 || v3 || 122,880 || - || - || - || - || 9,862 |- ! The Lurking Horror (includes sound) | lurking.z3 || v3 || 153,600 || - || - || - || - || 11,410 |- ! The Witness | witness.z3 || v3 || 122,880 || - || - || - || - || 11,260 |- ! Wishbringer (68/850501) | wishbrin.z3 || v3 || 128,905 || - || - || - || - || 11,774 |- ! ZORK I (88/840726) | zork1.z3 || v3 || 92,160 || - || - || - || - || 11,859 |- ! ZORK II | zork2.z3 || v3 || 92,160 || - || - || - || - || 11,189 |- ! ZORK III | zork3.z3 || v3 || 92,160 || - || - || - || - || 11,656 |- ! 1984 ZORK I Demo (IF tutorial, ZORK I) | zork\_1\_demo.z3 || v3 || 62,326 || - || - || - || - || 6,588 |- ! 1984/5 Infocom Sampler 1 R55 (IF tutorial,ZORK I,Planetfall,Infidel,The Witness) | sampler1\_R55.z3 || v3 || 126,902 || - || - || - || - || 13,557 |- ! 1987 Infocom Sampler 2 (IF tutorial,ZORK I,Leather Goddesses of Phobos,Trinity) | sampler2.z3 || v3 || 125,315 || - || - || - || - || 11,908 |- ! 1990 MINI-ZORK I | minizork.z3 || v3 || 52,216 || - || - || - || - || 8,583 |- |}

### Change Log

Not released yet

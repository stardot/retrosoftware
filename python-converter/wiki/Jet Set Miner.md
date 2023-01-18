# Jet Set Miner

### Licence

[GNU GPLv3 license](http://en.wikipedia.org/wiki/GNU_General_Public_License)

### Introduction

_Jet Set Miner_ is a 'highly original' platform game originally coded for the C64 for the 2003 Minigame competition (under the name of _Plat 3064_) and subsequently ported to the BBC Micro / Electron and, in 2011, also to the Acorn Atom.

Due to the size limitations of the competition, the game is a bit 'lightweight'. However, it can very easily be expanded should anyone wish to work on it.

_Features_

- Very small size (current binary is under 4k)

- Fully working game engine

- Four levels (though this can be \_very\_ easily expanded - the average level size is 65 bytes)

[Discuss _Jet Set Miner_](http://www.retrosoftware.co.uk/forum/viewforum.php?f=82)

### Platforms

#### Commodore 64

**_Original by Tom Walker_**

##### Downloads

[`Plat` `3064` `C64` `binary` `and` `c64asm` `assembler` `source` `code`](./images/Plat 3064.zip "wikilink")

##### Port Details

The first version of the game which was submitted to the 2003 Minigame competition under the name of _Plat 3064_ but is now known as _Jet Set Miner_. Beware when playing the third level - when traversing the top-most platforms, the height of jumps are limited which makes negotiating them much harder.

##### Screenshots

<table>

<tbody>

<tr class="odd">

<td><p>![](./images/Plat3064Screenshot.png)

<strong>Plat 3064 first level</strong><br />

<em>Posted: Jun 21, 2009</em></p></td>

<td><p>![](./images/Plat3064Screenshot2.png)

<strong>Plat 3064 second level</strong><br />

<em>Posted: Aug 21, 2011</em></p></td>

</tr>

<tr class="even">

<td><p>![](./images/Plat3064Screenshot3.png)

<strong>Plat 3064 third level</strong><br />

<em>Posted: Aug 21, 2011</em></p></td>

<td><p>![](./images/Plat3064Screenshot4.png)

<strong>Plat 3064 fourth level</strong><br />

<em>Posted: Aug 21, 2011</em></p></td>

</tr>

</tbody>

</table>

#### BBC Micro / Electron

**_Port by Tom Walker, with contributions from Murray C / MurrayCakaMuzer_**

##### Downloads

[`Jet` `Set` `Miner` `BBC` `Micro/Electron` `disc` `image` `and` `P65` `assembler` `source` `code`](./images/Jet Set Miner.zip "wikilink")

[`Updated` `Jet` `Set` `Miner` `BBC` `Micro/Electron` `disc` `image` `and` `P65` `assembler` `source` `code` `by` `MurrayCakaMuzer`](./images/Jet Set Miner-MurrayCakaMuzer.zip "wikilink")

##### Port Details

_Features_

- The Acorn port is totally OS legal, so should work on almost anything

- With some modifications, the Acorn port will run on a 16k Model A

Updates to the BBC Micro / Electron port by Murray C (MurrayCakaMuzer) [in August 2009](http://www.retrosoftware.co.uk/forum/viewtopic.php?f=19&t=310&p=2899):

- fixed the bug when returning to the title screen on game over (previously it would crash, since the initial setup routines were being repeated without interrupts being disabled. I added a new label after the initialisation of things like the replacement event routine, etc and modified the jump)

- made the game wait for fire to be released on the title screen, so that you don't jump first thing

- added sound effects for jumping and falling (similar to the ones in Jet Set Willy)

- implemented much more efficient, and smaller, screen clear routine

##### Screenshots

<table>

<tbody>

<tr class="odd">

<td><p>![](./images/JetSetMinerLoadingScreen.png)

<strong>Loading screen</strong><br />

<em>Posted: Jul 30, 2011</em></p></td>

<td><p>![](./images/JetSetMinerScreenshot1.png)

<strong>First level</strong><br />

<em>Posted: Jun 21, 2009</em></p></td>

<td><p>![](./images/JetSetMinerScreenshot2.png)

<strong>Second level</strong><br />

<em>Posted: Jun 21, 2009</em></p></td>

</tr>

<tr class="even">

<td><p>![](./images/JetSetMinerScreenshot3.png)

<strong>Third level</strong><br />

<em>Posted: Jul 30, 2011</em></p></td>

<td><p>![](./images/JetSetMinerScreenshot4.png)

<strong>Fourth level</strong><br />

<em>Posted: Aug 21, 2011</em></p></td>

</tr>

</tbody>

</table>

#### Atom

**_Port by Kees van Oss_**

##### System Requirements

- Standard unexpanded Acorn Atom

- 12 KB RAM (\#2900-\#3C00)

- 6 KB video RAM (\#8000-\#97FF)

- VIA

##### Downloads

[`Jet` `Set` `Miner` `Acorn` `Atom` `disc/tape` `images` `and` `2500AD` `cross` `compiler` `6502` `version` `assembler` `source` `code`](./images/Atom Jet Set Miner.zip "wikilink")

##### Port Details

A new port of _Jet Set Miner_ to the Acorn Atom, complete with a fully-functioning, all-new level editor was first showcased at the [In Da 80s](http://inda80s.cgeu.info/) show in Manchester, July 2011. It runs on a standard unexpanded Atom and does not need any extra ROM or hardware. The code is not optimal due to 1 on 1 conversion. The sprite routine is not flicker-free and has room for improvement.

##### Screenshots

<table>

<tbody>

<tr class="odd">

<td><p>![](./images/AtomicJetSetMiner1.png)

<strong>Atom Jet Set Miner Title Screen</strong><br />

<em>Posted: Jul 14, 2011</em><br />

</p></td>

<td><p>![](./images/AtomicJetSetMiner2.png)

<strong>Atom Jet Set Miner Colour Level 1 screen</strong><br />

<em>Posted: Jul 14, 2011</em><br />

</p></td>

<td><p>![](./images/AtomicJetSetMiner3.png)

<strong>Atom Jet Set Miner Colour Level 2 screen</strong><br />

<em>Posted: Jul 14, 2011</em><br />

</p></td>

</tr>

<tr class="even">

<td><p>![](./images/AtomicJetSetMiner4.png)

<strong>Atom Jet Set Miner Colour Level 3 screen</strong><br />

<em>Posted: Jul 14, 2011</em><br />

</p></td>

<td><p>![](./images/AtomicJetSetMiner8.png)

<strong>Atom Jet Set Miner Colour Level 4 screen</strong><br />

<em>Posted: Aug 18, 2011</em><br />

</p></td>

<td><p>![](./images/AtomicJetSetMiner5.png)

<strong>Atom Jet Set Miner Mono Level 1 screen</strong><br />

<em>Posted: Aug 18, 2011</em><br />

</p></td>

</tr>

<tr class="odd">

<td><p>![](./images/AtomicJetSetMiner6.png)

<strong>Atom Jet Set Miner Mono Level 2 screen</strong><br />

<em>Posted: Aug 18, 2011</em><br />

</p></td>

<td><p>![](./images/AtomicJetSetMiner7.png)

<strong>Atom Jet Set Miner Mono Level 3 screen</strong><br />

<em>Posted: Aug 18, 2011</em><br />

</p></td>

<td><p>![](./images/AtomicJetSetMiner9.png)

<strong>Atom Jet Set Miner Mono Level 4 screen</strong><br />

<em>Posted: Aug 18, 2011</em><br />

</p></td>

</tr>

<tr class="even">

<td><p>![](./images/AtomicJetSetMinerEditor.png)

<strong>Atom Jet Set Miner Editor screen</strong><br />

<em>Posted: Jul 14, 2011</em><br />

</p></td>

<td><p><br />

</p></td>

</tr>

</tbody>

</table>

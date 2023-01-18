# Repton by Tim Tyler & Kees van Oss

### Licence

Freeware (source code included)

*BBC Micro / Electron Repton © 1985 Superior Software / Tim Tyler*
*Acorn Atom Repton by Kees van Oss, 2013*

### Introduction

*Repton* is the best-selling gaming franchise available for all Acorn machines. At least, it is now - never before available for the Acorn Atom, Kees van Oss was inspired by fellow RS coder David Boddie's [reverse engineering of the Electron *Repton* level formats](ReverseEngineered_Repton "wikilink")\* and has successfully ported the original Electron release created by 15-year-old [Tim Tyler](http://timtyler.org/) and published by *[Superior Software](http://www.superiorsoftware.co.uk/)* in 1985.
\* See more reverse engineered games on the [Useful Docs](UsefulDocs#Reverse_Engineered_Software "wikilink") page.
N.B. The modern *Repton* series continues to be developed by *[Superior Interactive](http://www.superiorinteractive.com/)* for Windows and iOS platforms.

[Discuss Repton](http://www.retrosoftware.co.uk/forum/viewforum.php?f=91)

### Platforms

#### Atom

***Port by Kees van Oss***

The Electron version didn't use hardware scrolling so was a good candidate for porting to the Atom. It uses character scrolling so scrolling 8x8 bits. The playfield screen had to be adjusted and the layout rearranged due to the resolution difference but because the playfield is 18x18 instead of 22x22 characters, it scrolls faster and is fast enough to play at 1 MHz.

##### System Requirements

-   Standard Acorn Atom
-   32 KB RAM (\#0000-\#7FFF)
-   6 KB video RAM (\#8000-\#97FF)
-   VIA
-   Joystick (Optional)

##### Joystick Connections

An optional joystick can be connected to PORTB of the AtoMMC interface with software version 2.9.

`AtoMMC  Joystick`
`-----------------`
` PB0  -  Right`
` PB1  -  Left`
` PB2  -  Down`
` PB3  -  Up`
` PB4  -  Jump`
` PB5  -  nc`
` PB6  -  nc`
` PB7  -  nc`
` GND  -  GND`

##### Downloads

[Repton Acorn Atom disc/tape images](./images/repton.zip "wikilink")

This image archive includes both tape and disc versions of the game. Read the included Readme.txt file for more info.

The sourcefiles are available on request and have to be compiled with the CC65 cross compiler.

Type MAKE REPTON to compile the program.

An assembler listing is created in the REPTON.LST file.

##### Videos

<table>
<tbody>
<tr class="odd">
<td><p>{{#ev:youtube|DjPzYFY1IkY}}                 <br />
<strong>Atomic Repton final version <em>by Kees van Oss</em></strong><br />
<em>Posted: Mon Aug 19, 2013</em></p></td>
</tr>
<tr class="even">
<td><p><br />
</p></td>
</tr>
<tr class="odd">
<td><p>{{#ev:youtube|_ZhQzKTnAj8}}                 <br />
<strong>Preview Repton <em>by Kees van Oss</em></strong><br />
<em>Posted: Sat July 13, 2013</em></p></td>
</tr>
</tbody>
</table>

##### Screenshots

<table>
<tbody>
<tr class="odd">
<td><p>![](./images/AtomicReptonKeys.png)
<strong><em>Atom Repton</em> keys screen</strong><br />
<em>Posted: 14:05, 06 Aug 2013</em></p></td>
<td><p>![](./images/AtomicReptonLoading.png)
<strong><em>Atom Repton</em> loading screen</strong><br />
<em>Posted: 14:09, 06 Aug 2013</em></p></td>
<td><p>![](./images/AtomicReptonTitle.png)
<strong><em>Atom Repton</em> title screen</strong><br />
<em>Posted: 14:09, 06 Aug 2013</em></p></td>
</tr>
<tr class="even">
<td><p>![](./images/AtomicReptonInGame1.png)
<strong><em>Atom Repton</em> in-game #1</strong><br />
<em>Posted: 14:10, 06 Aug 2013</em></p></td>
<td><p>![](./images/AtomicReptonInGame2.png)
<strong><em>Atom Repton</em> in-game #2</strong><br />
<em>Posted: 21:57, 06 Aug 2013</em></p></td>
<td><p>![](./images/AtomicReptonInGame3.png)
<strong><em>Atom Repton</em> in-game #3</strong><br />
<em>Posted: 21:57, 06 Aug 2013</em></p></td>
</tr>
<tr class="odd">
<td><p>![](./images/AtomicReptonInGame4.png)
<strong><em>Atom Repton</em> in-game #4</strong><br />
<em>Posted: 21:58, 06 Aug 2013</em></p></td>
<td><p>![](./images/AtomicReptonInGame5.png)
<strong><em>Atom Repton</em> in-game #5</strong><br />
<em>Posted: 21:58, 06 Aug 2013</em></p></td>
<td><p>![](./images/AtomicReptonInGame6.png)
<strong><em>Atom Repton</em> in-game #6</strong><br />
<em>Posted: 21:58, 06 Aug 2013</em></p></td>
</tr>
<tr class="even">
<td><p>![](./images/AtomicReptonInGame7.png)
<strong><em>Atom Repton</em> in-game #7</strong><br />
<em>Posted: 21:58, 06 Aug 2013</em></p></td>
<td><p>![](./images/AtomicReptonInGame8.png)
<strong><em>Atom Repton</em> in-game #8</strong><br />
<em>Posted: 21:59, 06 Aug 2013</em></p></td>
<td><p>![](./images/AtomicReptonInGame9.png)
<strong><em>Atom Repton</em> in-game #9</strong><br />
<em>Posted: 21:59, 06 Aug 2013</em></p></td>
</tr>
<tr class="odd">
<td><p>![](./images/AtomicReptonInGame10.png)
<strong><em>Atom Repton</em> in-game #10</strong><br />
<em>Posted: 13:10, 06 Aug 2013</em></p></td>
</tr>
</tbody>
</table>



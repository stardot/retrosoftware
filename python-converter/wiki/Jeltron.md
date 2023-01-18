# Jeltron by Richard 'tricky' Broadhurst and Gil Jaysmith (né Johnson-Smith)

### Licence

[GNU GPLv3 license](http://en.wikipedia.org/wiki/GNU_General_Public_License)

### Introduction

*Jeltron* was written in the early 80s by Richard 'tricky' Broadhurst and Gil Jaysmith, the author of Spectrum Repton 1 & 2, with graphics from one of Gil's friends. A super-smooth simultaneous two player shoot-'em'up without flicker and a neat MODE split, it was developed as far as a preliminary version that was sent to a publisher for consideration - a contract was offered, but personal circumstances meant the game was never finished. With Gil's permission, Richard has offered the game resources to Retro Software and has also offered to support anyone who might be willing to continue the project:

*On the current status and playing the demo*
There are several waves of aliens (though we never got round to balancing them), then a mother-ship, then the whole things repeats with parallax landscape or star-fields and/or firing aliens. I have a later version of the source code with an orbiting mini-ship shield/blob and spreading bullet shots power-ups, but there is a bug after the first end of level boss.

The best bet is to get two fire/shot power-ups and then two or three turbo speed power-ups, you can then kill the end of level boss by flying backwards nose to nose, going up or down at the last moment ready to swoop in again - note that the laser is "fully-automatic"!

The keyboard layout is a bit tricky as we had to avoid key clashes, your best bet is to use a couple of joysticks.

`Key\Play   1 2`
`Up         Q P`
`Down       A ;`
`Left       E {`
`Right      R L`
`Fire       X DELETE`
`Power-Up   Z RETURN`

*On the game's design / development*
Removing flicker was one of the main aims of the game, though there is flicker between the landscape (not the parallax, of course) and pretty much anything else - I think it was fixed for the players' ships in a later build. The aliens were never meant to get close enough to share a char block. We had four copies of each sprite, although some were to have been used for animation for aliens that always move horizontally by the same amount per frame. The landscape bits are impossible with the aliens - I designed them without aliens, but for the demo we tried to show what would be available to a decent level designer. The renderer chases the scan-line and only ORs where it has to, SToring where there is no overlap.

[Discuss Jeltron](http://www.retrosoftware.co.uk/forum/viewtopic.php?f=23&t=603)

### TODO

The main things that the game needs to be playable is to have all of the alien waves and landscape re-designed and add more game play or levels.

### Downloads

*21/06/2011:* [Jeltron-demo-beebasm-src.zip](./images/Jeltron-demo-beebasm-src.zip "wikilink") - modern updated GPL'd Jeltron BeebAsm source code, data, two line make.bat and Acorn DFS 5.25" SSD disc image

Here are the data files and the BeebAsm 1.4 source code for the Jeltron demo - I have included a disc image and .bat that will require your BeebAsm and BeebEm (any decent emulator should be OK) paths adding.

The original demo loads the data and then splats over the middle with code, so if you have a slow connection to your beeb, you could re-arrange it that way.

PS I would like to thank RichTW for BeebAsm, it only took three hours to port from original BBC basic/asm to BeebAsm!

*01/04/2011:* [JELTRON-demo-make.zip](./images/JELTRON-demo-make.zip "wikilink") - early disc image of the Jeltron demo incl. GPL'd original source code (Acorn DFS 5.25" SSD image)

*To build:*

`CHAIN` `"SOURCE1"`

and then copy last line to \*SAVE RTYPE executable, and:

`CHAIN` `"DGen"`

to build R.Data.

*To run:*

`*LOAD` `R.Data`
`*RTYPE`

*01/04/2011:* [JELTRON.zip](./images/JELTRON.zip "wikilink") - early disc image of the Jeltron demo (Acorn DFS 5.25" SSD image)

### Sample Screenshots

<table>
<tbody>
<tr class="odd">
<td><p>![](./images/Jeltron1.png)
<strong>Jeltron in-game screenshot #1</strong><br />
<em>Posted: 03 Mar 2012</em></p></td>
<td><p>[[Image:Jeltron2.png|330px|<em>'Jeltron in-game screenshot #2 <strong><br />
<em>Posted: 03 Mar 2012</em>]]<br />
</strong>Jeltron in-game screenshot #2</em>'<br />
<em>Posted: 03 Mar 2012</em></p></td>
</tr>
<tr class="even">
<td><p>![](./images/Jeltron3.png)
<strong>Jeltron in-game screenshot #3</strong><br />
<em>Posted: 03 Mar 2012</em></p></td>
<td><p>![](./images/Jeltron4.png)
<strong>Jeltron in-game screenshot #4</strong><br />
<em>Posted: 03 Mar 2012</em></p></td>
</tr>
<tr class="odd">
<td><p>![](./images/Jeltron5.png)
<strong>Jeltron in-game screenshot #5</strong><br />
<em>Posted: 03 Mar 2012</em></p></td>
<td><p>![](./images/Jeltron6.png)
<strong>Jeltron in-game screenshot #6</strong><br />
<em>Posted: 03 Mar 2012</em></p></td>
</tr>
</tbody>
</table>

### Sample Video

<table>
<tbody>
<tr class="odd">
<td><p>{{#ev:youtube|bxUousTHFeU}}   <br />
<strong>Jeltron 1a - First half of Level 1</strong><br />
<em>Posted: April 01, 2011</em><br />
<br />
</p></td>
<td><p>{{#ev:youtube|2kkz_y07kNM}}   <br />
<strong>Jeltron 1b - Second half of Level 1</strong><br />
<em>Posted: April 01, 2011</em><br />
<br />
</p></td>
</tr>
<tr class="even">
<td><p>{{#ev:youtube|52eOSfXzUzo}}   <br />
<strong>Jeltron 2a - First half of Level 2</strong><br />
<em>Posted: April 01, 2011</em><br />
<br />
</p></td>
<td><p>{{#ev:youtube|jlmhSMYxJOs}}   <br />
<strong>Jeltron 2b - Second half of Level 2</strong><br />
<em>Posted: April 01, 2011</em><br />
<br />
</p></td>
</tr>
<tr class="odd">
<td><p>{{#ev:youtube|IkhbK1UjDEo}}   <br />
<strong>Jeltron 3a - First half of Level 3</strong><br />
<em>Posted: April 01, 2011</em><br />
<br />
</p></td>
<td><p>{{#ev:youtube|381WtEoHqnY}}   <br />
<strong>Jeltron 3b - Second half of Level 3</strong><br />
<em>Posted: April 01, 2011</em><br />
<br />
</p></td>
</tr>
<tr class="even">
<td><p>{{#ev:youtube|ZNFMTVwQBvQ}}   <br />
<strong>Jeltron 4a - First half of Level 4</strong><br />
<em>Posted: April 01, 2011</em></p></td>
<td><p>{{#ev:youtube|2-aCeUV_82M}}   <br />
<strong>Jeltron 4b - Second half of Level 4</strong><br />
<em>Posted: April 01, 2011</em></p></td>
</tr>
<tr class="odd">
</tr>
</tbody>
</table>



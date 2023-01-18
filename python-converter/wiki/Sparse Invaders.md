# Sparse Invaders by Neil Beresford

<img src="SparseInvaders-WIPcover.png" title="Sparse Invaders WIP cover by DaveM. Posted: Dec 04, 2008" alt="Sparse Invaders WIP cover by DaveM. Posted: Dec 04, 2008" width="375" />

### Licence

This software is licensed under the [GNU GPLv3 license](http://en.wikipedia.org/wiki/GNU_General_Public_License).

### Introduction

At one point laughingly known as *Pants Invaders*, *Sparse Invaders* is described by the author as a naff version of Taito's *Space Invaders*, developed using [SWIFT](SWIFT "wikilink") with P65.

OK, this is my first attempt at writing something for the Beeb. The reason for writing a simple'ish' game like Space Invaders, was to develop the screen, sprite, keyboard and timers code, plus get a feel for how to actually do stuff on the Beeb. I plan to re-work the guts of the code for my next game.

I've added my source code with Swift project as is, in zip form so that this can allow Sparse Invaders to be changed and re-built. This will also give newcomers a working example game, to play and view source code (note, I didn't say great example! LOL), with documentation on it's workings and the reasoning for it (i.e the invaders being drawn - in two parts, to keep it running in a frame).

[Discuss Sparse Invaders](http://www.retrosoftware.co.uk/forum/viewforum.php?f=42)

### Features

-   Simple Text-Block functionality for intro and current level screens.
-   Over-Complex Sprite Controller ( I learn the hard way.) This system has control for eight sprites active on screen, and store for a total of fifteen...
-   Simple block sprite drawing, used for the invaders.
-   Timer for vertical blank.
-   Keyboard functionality - fast code borrowed from a 'friend' ;-)
-   High score.

### What's Been Done

Sparse Invaders is currently standing at 1.0 so - please use the forum to supply feedback and issue reporting.

This contains the hiscore and more balanced game play, with improved base and better screen transitions. Several bug fixes.

My partner has even play-tested the game, her feedback was 'oh... you are clever!' - sigh! No, she played it several times and enjoyed it, I got the impression the game play seemed about right, but it's always good to get feedback from other gamers.

**Description**

Basically, it's my effort at that classic space invaders game.

Includes introduction, level and game over screens. There is the addition of a simple high score screen. The basic game consists of 24 invaders, one mother ship and you the player. There is basic score displayed below right. You fire, invaders and mother ship will explode and once all the invaders are shot, it moves to the next level - where it gets a little more difficult.

I'm sort of pleased with the bases, I wasn't sure how they would turn out as I am using a three-state block system to get 18 (4x8 size) segments for each base. So, each base uses 3 by 3 character (8x8 size) blocks - making it easy to draw and collision checking.

### Downloads

Latest release: *15 Mar 2012 - Download - Full version, fixed remaining bugs*

[Sparse Invaders v1.1](./images/SparseInvaders 1 1.zip "wikilink")
[Sparse Invaders v1.1 source code](./images/SparseInvaders 1 1 source.zip "wikilink")

### Older Playable Demos

The following is left in to show development of the game.

**PLEASE note, now works on the BBC B!**

Supplied as BBC Micro Model B SSD disc images, they will autoboot and run...
*24 Dec 2009 - Download - Full version, lots of bug fixes*
[Sparse Invaders v1.0\_2412](http://www.retrosoftware.co.uk/forum/download/file.php?id=330)
[Sparse Invaders v1.0\_2412 source code](./images/SparseInvaders 1 0 2412 source.zip "wikilink")

-   Fixed sound issue
-   Fixed slow-down issue
-   Extended the score display to five digits
-   Limited the number of lives to six
-   Increased score required for bonus life to 1500
-   Removed the 'Press Fire' and Sparse Invaders name from the 'next level' screen (added 4-5 second delay instead)
-   Fixed start level, so invaders appear correctly
-   Fixed issue where player wasn't getting drawn until moved on life loss (also added 1 second invincibility to stop deaths happening quickly - this might need to be extended)
-   Changed the intro screen text
-   Pause while playing game (press P during play)
-   Exit game option (while paused, press Esc)
-   Known issue: Invader explosions no longer appear

*3 Nov 2009 - Download - Initial feature-complete release, sound included*
[Sparse Invaders v1.0](./images/SparseInvaders 1 0.zip "wikilink")
Full, working version with sound.

*09 May 2009 - Beta Download with Pitfall Jones' modification - Added sounds*
[Sparse Invaders v0.4 + Pitfall Jones' sounds](http://www.retrosoftware.co.uk/forum/download/file.php?id=241)
PJ disassembled it, then remade it in beebasm and relocated the game from $1100 down to $E00 to make room for the extra code. Original forum post [here](http://www.retrosoftware.co.uk/forum/viewtopic.php?f=42&t=278).

*13 Feb 2009 - Beta Download - Highscore addition and tidy up*
[Sparse Invaders v0.4](./images/SparseInvaders0.4.zip "wikilink")
Addition of hiscore. Bases now working. Major bux fixing and tweeking.

*13 Jan 2009 - Second Alpha Download - Fixed important bug*
[Pants Invaders v0.3](./images/PantsInvaders.zip "wikilink")
Fixed blanking issues with Invaders. Certainly worth another upload. Apologies for those that have already downloaded v0.2.

*12 Jan 2009 - Second Alpha Download*
[Pants Invaders v0.2](./images/PantsInvaders0.2.zip "wikilink")
FIRE - Return/Enter, LEFT - Z, RIGHT - X
*18 Dec 2008 - First Alpha Download*
[Pants Invaders v0.1](./images/PantsInvaders0.1.zip "wikilink")

### Source DOWNLOAD and Write Up

This will show and explain the various files that make up the source for Sparse Invaders.

I have included the complete project as a downloadable ZIP file.

Also Included is a stripped SHELL project as a downloadable ZIP file.

Follow link below and have fun! (PS - I'm still working on the writeup for the files however they are all available to read online)

[Sparse Invaders: Source](Sparse_Invaders:_Source "wikilink")

### Diary Of Development

#### Nov 2008

Decided to spent a more productive lunch time at work by attempting to write a game on the good old beeb in 6502. Haven't done any 6502, in fact it's been several yrs since I'd done any serious asm development ( Z80, 68000, 80x86 etc ). Thought it would be a good challenge, also with the help of [SWIFT](SWIFT "wikilink") (must put link here to wiki page) it made life so much easier. Working on Sprite, Screen, Keyboardand Interrupt routines found that it would be help me get a feel for the performance of the beeb and iron out the any issues if I develop something that would test my functions - thus Invaders was born!

#### Dec 2008

Posted onto the forum the news that I was developing Invaders, just a testing version, and once I was happy with my various functions I would place them on site for a 'working' example of a game in action - for all the new-to-beeb coders to see and work with. I use the term 'working' as this is my first 6502 Beeb attempt, it certainly would not be the 'excellent' code, just 'good' ... ;-)

Sigh - then people wanted to see a work in progress version of Invaders, so I had to make the decision to finish the game - as from the feedback I got, people liked my naff artwork and the general feel of it. I certainly was taken aback, as it felt a good game to me, but I realized this was only my first effort at getting to know the Beeb.

Anyway, work progressed sort of slowly, after the first alpha was made available. This was due to Christmas and being ill.

#### Jan 2009

Worked on the bases, sorting out the firing of the invaders and just tidying up the firing system. Once you view the code, you will notice there are some over complex systems within the game. The main one being the sprite system! It was developed really before I fully understood how SLOW the Beeb was, however I've kept it and worked with it - and for the 6 or 7 active sprites - it does its job. My main aim has been to keep the game running within a frame and also keep the game play good and exciting. The addition of the bases still keeps that within a frame, thou I wonder at the amount of collision checking that is done, \[forced smile!\] ! The base functionality is another slightly complex system, using bit masking for checking and removal of segments of the base. It works quite well considering, certainly good enough for this game anyway.

I must say, that soon the code will be made available, however it should be noted that this code is not optimised and should be taken as a working example only. I've said this before, so just warning that this is not the fastest code out there, thus I would love any positive feedback ONLY! LOL!!!

#### 15 Jan 2009

Things are progressing quite well, I have been nawty and have worked the full lunch hour for the last few days, getting the known issues sorted. Thus I have, I think just about finished the main game, I'm sure there will be issues, but the ones I've seen, I've managed to fix - so after several game plays it's feeling quite good...

The details

-   Added End Game Score, so you know what you got!
-   Added Bonus life, this is for every 500 points gained.
-   Sorted out Invader bullet speed increment as levels progress.
-   Player bullet different gfx.
-   Mother ship now has two frames, and some naff colours, sorry!
-   Added Yellow to upper part of numbers plus life markers changed to yellow.
-   Reduced delay to FIRE action on intro, start level and game over screens.
-   Sorted out the various level restart gfx glitchies.

To Do list

-   Hi-score entry screen and Listing.
-   Quick Tidy of screens etc
-   Release as beta for testing.
-   Once got feedback from guys on site, release as Version 1.0
-   Review code and then release to site for general use.

Oh, will be updating the Wiki page soon, honest!!

#### 17 Feb 2009

After a long pause, I've uploaded the BETA of Sparse Invaders. You can find some sample screens below relating to the latest version.

I won't go on, but at present as I'm sort of around 220 bytes, the game will only run on a Master 128k. I will work on this while awaiting any feedback, before doing the release. However if anyone wants a copy early, please contact via the forum and I will be happy to supply a modified version.

A little request here, as I will be placing the source code on site soon, has anyone any licence text I can use for the source? I am going for a free licence, however the source is not to used for profit type ventures.

On the whole I am very pleased with the outcome of the last few months or so, Sparse Invaders, in my opinion, plays well and feels ok for a first attempt at the Beeb. Let's hope you guys feel the same!

Neil

#### 19 Feb 2009

Working late at work - once that was finished, I thought - lets get it running on the BBC B. I needed to actually find around 350 bytes, so removed debug, rewrote the hi-score and block draws. Thus Sparse Invaders now runs on the BBC B.

For the technical, I've got the .org set to 1100. This doesn't seem to wiping over any important buffers while the main file is loading. I've given it a good bash!

OK, would be lovely to get some feedback!

#### 3 Nov 2009

Sound has been added to the main code, thanks goes to PJ for his hard work disassembling the binary and having the patience to actually understand the code and add in the sound. Steve helped with my total blank moment and relocation now works. I've updated the version to 1.0 to indicate no more development as I plan on adding the source here.

### Sample Screenshots

***Sparse Invaders* Beta Release**

<table>
<tbody>
<tr class="odd">
<td><p>![](./images/Invadersv04 01.jpg)
<strong>Title screen</strong><br />
<em>Posted: Feb 17, 2009</em></p></td>
<td><p>![](./images/Invadersv04 02.jpg)
<strong>Game start</strong><br />
<em>Posted: Feb 17, 2009</em></p></td>
</tr>
<tr class="even">
<td><p>[[Image:Invadersv04_03.jpg|375px|<em>'In-game 2 <strong><br />
<em>Posted: Feb 17, 2009</em>]]<br />
</strong>In-game 2</em>'<br />
<em>Posted: Feb 17, 2009</em><br />
</p></td>
<td><p>[[Image:Invadersv04_04.jpg|375px|<em>'Game over <strong><br />
<em>Posted: Feb 17, 2009</em>]]<br />
</strong>Game over</em>'<br />
<em>Posted: Feb 17, 2009</em><br />
</p></td>
</tr>
<tr class="odd">
<td><p>![](./images/Invadersv04 05.jpg)
<strong>High score</strong><br />
<em>Posted: Feb 17, 2009</em><br />
</p></td>
</tr>
</tbody>
</table>

***Pants Invaders* Pre-Second Alpha Release**

<table>
<tbody>
<tr class="odd">
<td><p>![](./images/Pants Invaders 1812 01.jpg)
<strong>Title screen</strong><br />
<em>Posted: Dec 19, 2008</em></p></td>
<td><p>![](./images/Pants Invaders 1812 02.jpg)
<strong>Entering level screen</strong><br />
<em>Posted: Dec 19, 2008</em></p></td>
</tr>
<tr class="even">
<td><p>[[Image:Pants_Invaders_1812_03.jpg|375px|<em>'In-game 1 <strong><br />
<em>Posted: Dec 19, 2008</em>]]<br />
</strong>In-game 1</em>'<br />
<em>Posted: Dec 19, 2008</em><br />
</p></td>
<td><p>[[Image:Pants_Invaders_1812_04.jpg|375px|<em>'In-game 2 <strong><br />
<em>Posted: Dec 19, 2008</em>]]<br />
</strong>In-game 2</em>'<br />
<em>Posted: Dec 19, 2008</em><br />
</p></td>
</tr>
</tbody>
</table>

***Sparse Invaders* Pre-First Alpha Release**

<table>
<tbody>
<tr class="odd">
<td><p>![](./images/SparseInvaders0.jpg)
<strong>Title screen</strong><br />
<em>Posted: Dec 03, 2008</em></p></td>
<td><p>![](./images/SparseInvaders1.jpg)
<strong>In-game 1</strong><br />
<em>Posted: Dec 03, 2008</em></p></td>
</tr>
<tr class="even">
<td><p>[[Image:SparseInvaders2.jpg|375px|<em>'In-game 2 <strong><br />
<em>Posted: Dec 03, 2008</em>]]<br />
</strong>In-game 2</em>'<br />
<em>Posted: Dec 03, 2008</em><br />
</p></td>
<td><p>[[Image:SparseInvaders3.jpg|375px|<em>'In-game 3 <strong><br />
<em>Posted: Dec 03, 2008</em>]]<br />
</strong>In-game 3</em>'<br />
<em>Posted: Dec 03, 2008</em><br />
</p></td>
</tr>
</tbody>
</table>



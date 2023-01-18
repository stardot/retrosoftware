# Sparse Invaders : v1.0 Source Breakdown

## Introduction

Having never developed for the Beeb, I thought it was about time. Within a matter of minutes I had a document containing the 6502 instruction set, SWIFT installed with P65 and I was watching the videos supplied by Steve. Thus 'Sparse Invaders' was born.

To develop a game or application on the Beeb, the following knowledge is needed:

`  1. The idea - as in the game or app you want to develop!`

`  2. Patience!`

All else can be learnt, by reading and also asking questions. That's what I did, as I'm sure a lot on the forum will agree! Please do not be put off by the fact that it's 6502 assembler.

From my experience the only other assembler as easy as the 6502 is the 8080 (this is from memory as I last did that in 1984). It has a limited register and instruction set, simple to pick up - however it does enable you to do some pretty wonderful stuff on the BBC B. I only need one example, Elite!

Tools for this development -

- SWIFT :<http://www.retrosoftware.co.uk/wiki/index.php/SWIFT>

<!-- -->

- BeebEm :<http://www.mikebuk.dsl.pipex.com/beebem>

SWIFT is perfect for starting your first project. It contains project management, text editor for the source, graphic editor for the sprites and with a simple click on an icon - it will build your app and create the disk THEN launch the BBC B emulator so you can see it playing.

How EASY is that!!

Going back to Sparse Invaders, I picked Space Invaders as my game of choice, as to be honest it's a simple game to write, but not that simple as to not supply a little challenge while writing it.

Final thought, when developing, as long as you understand what you need to code, it's fun. If you have any confusion then take time out to contemplate the problem and discuss the issue.

**Programming on the BBC should be fun!!**

## Summary of the v1.0 source

Sparse Invaders is not optimised. That said, I used techniques in drawing the invaders that allows the game to run very smoothly. However the source code has been left as is, to enable better understanding of what is going on.

I have provided the complete source below giving a brief summary of what is actually happening in each of the files and tried to explain the techniques used and the reasons why.

Please note that this online source breakdown is useful reading, however viewing the source in SWIFT adds colour and correct tabbing etc making it far more pleasing to the eye! :-)

Any questions please ask away on the forum.

## Sparse Invaders Source Files

### The v1.0 Source Zip

At last the v1.0 source is here! Once you have SWIFT setup, just open the Sparse Invaders project and ENJOY!

- THE v1.0 SOURCE \* \\/ \\/ \\/ \\/ \\/

[Sparse Invaders v1.0 Source](../../retrosoftwarecouk_wiki-20160918-wikidump/images/SparseInvaders Source.zip "wikilink")

- THE v1.0 SOURCE \* /\\ /\\ /\\ /\\ /\\

### v1.0 Source Description

<table border=1>

<tr>

<th>

Source

</th>

<th>

Description

</th>

</tr>

<tr>

<td>

[**Main.txt**](Sparse_Invaders_Source_-_Main.txt "wikilink")

</td>

<td>

Starting point, main setup and control loop for game

</td>

</tr>

<tr>

<td>

[**BlockDrawer.txt**](Sparse_Invaders_Source_-_BlockDrawer.txt "wikilink")

</td>

<td>

Basic Block drawer

</td>

</tr>

<tr>

<td>

[**Keyboard.txt**](Sparse_Invaders_Source_-_Keyboard.txt "wikilink")

</td>

<td>

Keyboard handler

</td>

</tr>

<tr>

<td>

[**Screen.txt**](Sparse_Invaders_Source_-_Screen.txt "wikilink")

</td>

<td>

Screen drawing functionality

</td>

</tr>

<tr>

<td>

[**Sound.txt**](Sparse_Invaders_Source_-_Sound.txt "wikilink")

</td>

<td>

Sound initialization and generation

</td>

</tr>

<tr>

<td>

[**Timer.txt**](Sparse_Invaders_Soruce_-_Timer.txt "wikilink")

</td>

<td>

Timer interrupt

</td>

</tr>

<tr>

<td>

[**SpriteController.txt**](Sparse_Invaders_Source_-_SpriteControllert.txt "wikilink")

</td>

<td>

Sprite Controller (Over complex)

</td>

</tr>

<tr>

<td>

[**Invaders_Baddies.txt**](Sparse_Invaders_Source_-_Invaders_Baddies.txt "wikilink")

</td>

<td>

Setup,draw and control for invaders and mother ship

</td>

</tr>

<tr>

<td>

[**Invaders_Bases.txt**](Sparse_Invaders_Source_-_Invaders_Bases.txt "wikilink")

</td>

<td>

Setup, draw and control for the three bases

</td>

</tr>

<tr>

<td>

[**Invaders_Bullets.txt**](Sparse_Invaders_Source_-_Invaders_Bullets.txt "wikilink")

</td>

<td>

Bullet control.

</td>

</tr>

<tr>

<td>

[**Invaders_Hiscore.txt**](Sparse_Invaders_Source_-_Invaders_Hiscore.txt "wikilink")

</td>

<td>

Hiscore calculations and display

</td>

</tr>

<tr>

<td>

[**Invaders_Player.txt**](Sparse_Invaders_Source_-_Invaders_Player.txt "wikilink")

</td>

<td>

Player control

</td>

</tr>

<tr>

<td>

[ **Constants.txt**](Sparse_Invaders_Source_-_Constants.txt "wikilink")

</td>

<td>

Constants used throughout the game

</td>

</tr>

<tr>

<td>

[ **Macros.txt**](Sparse_Invaders_Source_-_Macros.txt "wikilink")

</td>

<td>

Macros used throughout the game

</td>

</tr>

<tr>

<td>

**Blocks.bin**

</td>

<td>

Block sprite collection

</td>

</tr>

<tr>

<td>

**Boot.bin**

</td>

<td>

Boot txt file - loads main and then runs reloc

</td>

</tr>

<tr>

<td>

**LookUpTable640.bin**

</td>

<td>

640 lookup table used for screen navagation.

</td>

</tr>

<tr>

<td>

**SpriteTest.bin**

</td>

<td>

Main sprites (not really test)

</td>

</tr>

<tr>

<td>

[ **Relocate.txt**](Sparse_Invaders_Source_-_Relocate.txt "wikilink")

</td>

<td>

Small code, loaded into 0x880 to relocate invaders down to 0x900

</td>

</tr>

<tr>

<td>

**Beeb-Invaders.swfpj**

</td>

<td>

Swift 4.2.2 (onwards) project file.

</td>

</tr>

<tr>

<td>

**BeebDisk1.ssd**

</td>

<td>

Build disk image

</td>

</tr>

<tr>

<td>

'''LICENSE '''

</td>

<td>

GPLv3 - Please read.

</td>

</tr>

</table>

## The Shell (stripped bare project for starting that new game)

UPDATE: **THE SHELL**

[Shell Source v1.0 Source](../../retrosoftwarecouk_wiki-20160918-wikidump/images/Shell Source.zip "wikilink")

This is the invaders source stripped leaving a basic shell. It does show text display, sprite creation and moving in a good documented effort. Please download and use the shell to create your game, using Sparse Invader source as a working example.

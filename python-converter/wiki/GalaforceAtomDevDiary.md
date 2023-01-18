## Galaforce Acorn Atom Development Diary

**_by Kees van Oss_**

16 August 2011

Galaforce is a shooting game for the BBC/Electron written by Kevin Edwards and distributed by Superior in 1986.

This is a brave attempt to rewrite the source so Galaforce can be played on an Acorn Atom.

===Status/history===

<table>

<tr>

<td>

<b>16-07-2011</b>

</td>

<td>

Went to 'In da 80's' retro-event in Manchester and had a talk with Kevin Edwards

</td>

</tr>

<tr>

<td>

<b>22-07-2011</b>

</td>

<td>

Samwise send me the source files of Galaga BBC version

</td>

</tr>

<tr>

<td>

<b>27-07-2011</b>

</td>

<td>

Rewritten source to be compiled with 2500AD cross-compiler

</td>

</tr>

<tr>

<td>

<b>03-08-2011</b>

</td>

<td>

Found out how the stars are plotted and moved

</td>

</tr>

<tr>

<td>

<b>11-08-2011</b>

</td>

<td>

Analyzed the font and storage

</td>

</tr>

<tr>

<td>

<b>16-08-2011</b>

</td>

<td>

Got the intro screens working except the title in the title screen

</td>

</tr>

<tr>

<td>

<b>18-08-2011</b>

</td>

<td>

Title screen (double height/width) is working

</td>

</tr>

<tr>

<td>

<b>24-08-2011</b>

</td>

<td>

Converted the Electron version sprites to the Atom

</td>

</tr>

<tr>

<td>

<b>31-08-2011</b>

</td>

<td>

Keyscanning, movement myship and shooting works

</td>

</tr>

<tr>

<td>

<b>10-08-2011</b>

</td>

<td>

Alien wave patterns analyzed and starting to convert them

</td>

</tr>

<tr>

<td>

<b>25-09-2011</b>

</td>

<td>

50% of Wavepatterns converted

</td>

</tr>

<tr>

<td>

<b>29-09-2011</b>

</td>

<td>

100% of Wavepatterns converted

</td>

</tr>

<tr>

<td>

<b>13-10-2011</b>

</td>

<td>

Analysing the sound system

</td>

</tr>

<tr>

<td>

<b>08-11-2011</b>

</td>

<td>

Solved input name error at high score

</td>

</tr>

<tr>

<td>

<b>05-02-2012</b>

</td>

<td>

Added fire- and explosion sounds

</td>

</tr>

<tr>

<td>

<b>12-02-2012</b>

</td>

<td>

Added music, started final testing

</td>

</tr>

</table>

<b>TODO list</b>

- Write Basic intro/loader screen

- Optimize some wavepatterns

- Add joystick support

- Align myship sprite with bullet (sprites are 1 pixel shifted)

- Reduce snow on a real Atom

### Atom vs BBC/Electron

To convert a BBC/Electron game to the Atom, you have to deal with a few things:

\* Graphics

- Sound

- Keyboard/joystick

====Graphics====

There is a big difference between the BBC/Electron and Atom graphic modes. Galaforce is written to run in MODE2 on a BBC and in MODE5 on an Electron.

<i>Resolution:</i>

The first difference is the graphic resolution. MODE2/5 have a resolution of 160 x 256 pixels while the max resolution in colour mode CLEAR4a on an Atom is 128 x 192 pixels. If you compare MODE2 with MODE5 then you'll notice that MODE5 is ideal to convert to CLEAR4a on an Atom, the only thing you have to do is reduce the resolution. MODE2 is also possible but then you also have to reduce the nr of colours from 8 to 4.

<i>Colours:</i>

The second difference is the max nr of colours which can be displayed simultaniously on the screen. A BBC/Electron can display 8 colours in MODE2 and 4 colours in MODe5 while the Atom can display 4 colours in CLEAR4a.

Also the interpretation of bits vs colour is different between the BBC/Electron and the Atom, see table below:

![](./images/colours.PNG "fig:colours.PNG")

<i>Colour pallette:</i>

The third big difference is the colour pallete. On a BBC/Electron, you can redefine the colours by changing the colour pallete. The Atom has 2 sets of 4 colours which can not be changed. That's why all coloured games on an Atom always have the same colours

![](./images/coloursets.PNG "fig:coloursets.PNG")

#### Sound

Sound is a very big problem on the Atom. A BBC or Electron have a soundchip to produce sound on multiple channels. You have to send data to this chip and it plays a sound with envelope for a certain duration. The Atom only has a bit connected to a beeper. To produce a tone, you have to toggle this bit with a certain frequency for a certain duration. This means that the Atom needs 100% CPU time to produce a tone.

It is possible to play a very short tone while gameplay without slowing down the game to long. Music can be played if no other processing time is needed so the processor is 100% available for the music. To play some sounds and music, I had to write a sound routine which can be called with a certain pitch, octave and duration.

<i>Music:</i>

The Electron version looks like the best candidate to start analyzing because the Electron only has 1 sound channel instead of 3.

These are my findings so far:

\* Sound works with the event interrupt routine (50 times/sec)

- The StartTune routine initializes:

`- Tune address, start of tune data`

`- Steptime table, 1 step = 1/50 sec`

`- Envelope table, for 3 channels (only first one is used for Electron)`

`- Duration table, for 3 channels (only first one is used for Electron)`

- After initializing, the Refresh routine is called under interrupt

- The Refresh routine checks if the steptime is exceeded, if so then the get next music databyte is read, unpacked and played

- Music databytes are packed like this:

`- bit 0-5, pitch divided by 4`

`- bit 6-7, steptime pointer`

- Music databyte = $00 -&gt; End of Tune marker

- Music databyte &gt;= 63 -&gt; Set new steptime

The game has 5 music parts:

\* **Start game**

- **Die**, when your ship is hit by an alien or bomb

- **Next Level**, after completing a level and entering the next one

- **Bonus**, after completing level 16,32,48

- **Game over**

<i>FX/Sounds:</i>

There are only 2 FX-sounds in the game:

- Fire rocket

- Explosion

#### Keyboard/joystick

<i>Keyboard:</i>

The keyboard scan routine of the Atom is very elementary. There are 2 options to scan the keyboard matrix. The first method is calling OSRDCH and the OS waits until a key is pressed and returns the ASCII code. This is usefull for key input but not for gaming. Gaming needs the keyboard matrix to be scanned and returns the code of a pressed key or returns a code is no key is pressed. There is a call in the F-ROM to do this but it only returns the first key in the matrix which is pressed. Actually you need a keyscan routine which returns wether a certain key is pressed or not and that routine is not available in the Atom OS. This is why I wrote a new keyscan routine equal to the BBC/Electron version:

LDX \#keyval

`LDY#$FF`

`JSR osbyte`

<i>Joystick:</i>

The Atom has no joystick support at all because there's no standard defined. I have written a routine to scan a joystick connected to PORTB of Charlie Robsons AtoMMC interface. The connections must be like this:

`AtoMMC  Joystick`

`-----------------`

`PB0   -  Right`

`PB1   -  Left`

`PB2   -  Down`

`PB3   -  Up`

`PB4   -  Jump`

`PB5   -  nc`

`PB6   -  nc`

`PB7   -  nc`

`GND  -  GND`

If you have an AtoMMC kernal version lower then v2.2, you have to add pull-up resistors to PB0,1,2,3,4 because the pull-up function of the PIC controller was not activated before v2.2.

### Program

Kevin Edwards was so generous to send his original source files for the BBC version to Samwise. Because Galaforce was developed back in '86, these files have to be compiled on an original BBC. The binary files are saved to disk.

The binary is build out of MASTER file:

0 REM SAVE"MASTER"

`  10 MODE7:HIMEM=&7EA0:VDU28,0,24,39,19`

`  20 PRINT'"Game 1.00"`

`  30 *LOAD CONST 1900`

`  40 PAGE=&1900:GOSUB 0`

`  50 *LOAD ZPWORK 1900`

`  60 PAGE=&1900:GOSUB 0`

`  70 *LOAD ABSWORK 1900`

`  80 PAGE=&1900:GOSUB 0`

`  90 FOR pass=4 TO 6 STEP 2`

` 100 P%=&B00:O%=&3000:C%=P%:S%=O%`

` 110 PRINT:FORL=1TO2:VDU141:PRINT"Pass = ";pass:NEXT`

` 120 READfile$`

` 130 IF file$="THE-END" RESTORE:GOTO 170`

` 140 OSCLI"LOAD "+file$+" 1900"`

` 150 PAGE=&1900:GOSUB 0`

` 160 GOTO 120`

` 170 NEXT pass`

` 180 PRINT'"Finished"`

` 190 PRINT"Code start  = &";~C%`

` 200 PRINT"End of code = &";~P%-1`

` 210 PRINT"Length      = &";~P%-C%;"   (";P%-C%;") bytes."`

` 220 PRINT"Bytes left  = &";~&297A-P%;"   (";&297A-P%;") bytes."`

` 230 OSCLI("LOAD O.SPFONT "+STR$~(S%-&200))`

` 240 OSCLI("LOAD O.DIGITS "+STR$~(S%-&100))`

` 250 OSCLI("LOAD GRAPHIC "+STR$~(S%+&297A-C%))`

` 260 *L.:2.O.DOWN 5500`

` 270 OSCLI("SAVE GAME "+STR$~(S%-&200)+" "+STR$~(&3200-C%+S%)+" 4000 1900")`

` 280 PRINT" CH."CHR$34":2.ALLENV1"CHR$34`

` 290 END`

` 300 DATA SPRITES,INIT,ALIENS1`

` 310 DATA ALIENS2,ALIENS3,ALIENS4,ROUT1,ROUT2,ROUT3,ROUT4,STARS`

` 320 DATA BOMBS1,BOMBS2,CHARP,FLAGS`

` 330 DATA MUSIC1,MUSIC2,:2.MUSIC3,:2.TITLE,:2.HIGH`

` 340 DATA WAVE,PATT,PATDAT,VECTORS`

` 350 DATA THE-END`

Description of the files:

\* MASTER, This is the main file for creating the binaries

- CONST, Declaration of game constants

- ZPWORK, Declaration of zeropage variables

- ABSWORK, Declaration of game variables

- SPRITES, Routine to erase/plot sprite

- INIT, Initialisation of game variables and main program loop

- ALIENS1/2/3/4, Initialize, process, plot, move, explode aliens

- ROUT1/2/3/4, Check keys/joystick for action, check collisions, handle demo movements and loop intro screens

- STARS, Star initialisation + scrolling

- BOMBS1/2, process my/alien bombs

- CHARP, Character/string printing

- FLAGS, Plot/erase flags for wavenr

- MUSIC1/2, Handles music and soundeffects

- TITLE, Display title in double height/width font

- HIGH, Handle highscore and name input

- WAVE, Definition of patterns per wave

- PATT, Initial data pattern + pointer to moving patterndata

- PATDAT, Moving pattern data

- VECTORS, Table for fast lookup PATT and PATTDAT data

Unfortunately not all files were included (marked \*\*\* MISSING \*\*\*). Because I could not get in touch with Kevin, I had to 'reverse engineer' these files from the BBC and Electron binaries. Now I have all files to complete the Atom version.

\* MUSIC3, Handles music and soundeffects \*\*\* MISSING \*\*\*

- DIGITS, score digit image from 0-9 for score and high score \*\*\* MISSING \*\*\*

- GRAPHIC, sprite image file \*\*\* MISSING \*\*\*

- DOWN, routine to download the code after loading it into memory \*\*\* MISSING \*\*\*

====Font====

The Galaforce font has 39 characters consisting of digits, letters and symbols and are stored in the file SPFONT.

\* Digits 0-9, character code 0-9

- Letters A-Z , character code 10-35

- Symbols '.', '\_' and SPACE, character code 36-38

![](./images/font.PNG "fig:font.PNG")

You can print single-or double size characters.

To print double size characters, every pixel is scaled to 2 x 2 pixels.

Every pixel is shifted out of the Storage byte and put on screen as a coloured pixel.

A character (5 x 8) is stored 90 degrees rotated (5 bytes).

A character on the screen is 5 x 8 pixels and there's 1 pixel space between 2 characters.

The letter G is stored like this:

![](./images/Letter.PNG "fig:Letter.PNG")

#### Sprites

The size of all sprites is 16 x 16 coloured pixels. There is no animation except an explosion. An explosion is a sequence of 6 sprites, starting at sprite 0.

The sprite will be erased at the old screenaddress and plotted at the new screenaddress in 1 call. The sprite routine is called with 3 parameters:

\* sprite nr., this is 2x spritenr (eg aliens are numbered 12,14,16 ... to 34 and myship is spritenr 38)

- old screenaddress, this is the address where the current sprite is positioned on the screen

- new screenaddress, this is the address where the sprite has to be positioned on the screen

You can see an image off all game sprites in the picture below:

![](./images/Atomsprites.PNG "fig:Atomsprites.PNG")

#### Alien waves

The system to move aliens is a very clever designed system. The game has 16 different wavezones to be played. Every wavezone has between 5-7 Alien waves which are described in the WAVE file. The initial information about an Alien wave is described in the PATT file. Every individual alien is following a certain path which is stored in the PATTDAT table.

So in total there are 3 tables were all the information is stored:

\* Wave table, where general wave data is stored

- Alien wave pattern table, where initial alien pattern data is stored

- Alien path table, where the movement information of the Alien is stored

<i>Wave table:</i>

This table holds the general information about all alien waves of one zone. The table structure is like this:

\* Wavespeed

- Alien wave pattern numbers (see Alien wave pattern table)

- $FF = End of wave marker

E.g. Wavezone 0 looks like this:

wave0

`   .db 10              ; Speed`

`   .db 0,2,43,1,11,10      ; Alien wave patterns`

`   .db $FF             ; end of wave marker`

<i>Alien wave pattern table:</i>

This table holds the initial information about an Alien wave. The table structure is like this:

\* Nr of simultanious patterns to be displayed

- Initial X-pos

- Initial Y-pos

- Delay before next alien appears

- Nr of aliens to show

- Initial X-movement for next alien to be displayed

- Initial Y-movement for next alien to be displayed

- Sprite nr, Sprite nr is alien sprite nr times 2 so sprite nr 12 -&gt; Alien 6

- Alien path, if bit7=1 path is mirrored (see Alien path table)

E.g. Alien pattern 0 looks like this:

patt0

`   .db 1       ; 1 Pattern to be displayed`

`   .db 0,24    ; Initial position X,Y`

`   .db 3       ; Delay before next alien appears`

`   .db 20  ; Stop wave after 20 aliens`

`   .db 0,4 ; Startposition next alien relativeX,Y moved from previ0ous one `

`   .db 12  ; Spritenr=12 -> Alien nr 6`

`   .db 0       ; Alien path 0`

<i>Alien path table</i>

This table holds the information about how an alien must move. The table holds data which can be a movement (&gt;=$80) or an action (&lt;$80):

\* Movement, holds information about repetition, stepsize and direction

`Byte0:`

`--------`

` bit 0-6 = Repetition of movement`

` bit 7    = 1`

`Byte1:`

`--------`

`bit 0-3 = Direction `

`bit 4-6 = Step size`

`bit7     = 0 `

- Action, tells the program which sub to be called

`Byte0:`

`--------`

`00 = Loop, next byte = set offset pointer to step nr`

`02 = New pattern, next byte = pattern nr`

`04 = New alien, next byte = patt nr`

`06 = Die`

`08 = Dropbomb`

`10 = For-loop, next byte = repeat nr`

`12 = Next`

`14 = Move`

E.g. Alien path 0 looks like this (Sx stand for Stepsize and Dx stands for Direction):

patdat0 Rep Step Dir

`   .db $84,12      ; Movement, x000-0100,00001-100    04x  S1  D4`

`   .db $86,15      ; Movement, x000-0110,00001-111    06x  S1  D7`

`   .db $86,12      ; Movement, x000-0110,00001-100    06x  S1  D4`

`   .db 10,100      ; Action 10,    dat_for_loop 100x`

`   .db $82,1       ; Movement, x000-0010,00000-001    02x  S0  D1`

`   .db 4,3     ; Action 4,     Init new_alien pattern 3`

`   .db $82,3       ; Movement, x000-0010,00000-011    02x  S0  D3`

`   .db 12      ; Action 12,    dat_next`

`   .db 6           ; Action 6,     dat-die`

![](./images/Move.PNG "fig:Move.PNG")

<i>Movement off patdat0</i>

<i>Stepsize table:</i>

The stapsize table is a matrix where you can determine how the alien has to move. If you find the cell pointed by the Direction and Stepsize numbers, you'll know the relative movement an Alien has to make. E.g. S3 and D5 determines that the movement stepsize has to be 4x,4y, where x and y stand for stepsizes which are defined as constants.

Stepsize 6 is a special move with predefined stepsizes.

<table border=1>

<tr align=center>

<td>

</td>

<td>

D0

</td>

<td>

D1

</td>

<td>

D2

</td>

<td>

D3

</td>

<td>

D4

</td>

<td>

D5

</td>

<td>

D6

</td>

<td>

D7

</td>

</tr>

<tr align=center>

<td width = 30>

S0

</td>

<td width = 50>

0,-1y

</td>

<td width = 50>

1x,0

</td>

<td width = 50>

0,1y

</td>

<td width = 50>

-1x,0

</td>

<td width = 50>

1x,-1y

</td>

<td width = 50>

1x,1y

</td>

<td width = 50>

-1x,1y

</td>

<td width = 50>

-1x,-1y

</td>

</tr>

<tr align=center>

<td>

S1

</td>

<td>

0,-2y

</td>

<td>

2x,0

</td>

<td>

0,2y

</td>

<td>

-2x,0

</td>

<td>

2x,-2y

</td>

<td>

2x,2y

</td>

<td>

-2x,2y

</td>

<td>

-2x,-2y

</td>

</tr>

<tr align=center>

<td>

S2

</td>

<td>

0,-3y

</td>

<td>

3x,0

</td>

<td>

0,3y

</td>

<td>

-3x,0

</td>

<td>

3x,-3y

</td>

<td>

3x,3y

</td>

<td>

-3x,3y

</td>

<td>

-3x,-3y

</td>

</tr>

<tr align=center>

<td>

S3

</td>

<td>

0,-4y

</td>

<td>

4x,0

</td>

<td>

0,4y

</td>

<td>

-4x,0

</td>

<td>

4x,-4y

</td>

<td>

4x,4y

</td>

<td>

-4x,4y

</td>

<td>

-4x,-4y

</td>

</tr>

<tr align=center>

<td>

S4

</td>

<td>

0,-5y

</td>

<td>

5x,0

</td>

<td>

0,5y

</td>

<td>

-5x,0

</td>

<td>

5x,-5y

</td>

<td>

5x,5y

</td>

<td>

-5x,5y

</td>

<td>

-5x,-5y

</td>

</tr>

<tr align=center>

<td>

S5

</td>

<td>

0,-6y

</td>

<td>

6x,0

</td>

<td>

0,6y

</td>

<td>

-6x,0

</td>

<td>

6x,-6y

</td>

<td>

6x,6y

</td>

<td>

-6x,6y

</td>

<td>

-6x,-6y

</td>

</tr>

<tr>

<td>

</td>

<td>

</td>

<td>

</td>

<td>

</td>

<td>

</td>

<td>

</td>

<td>

</td>

<td>

</td>

<td>

</td>

</tr>

<tr align=center>

<td>

S6

</td>

<td>

2,-16

</td>

<td>

2,4

</td>

<td>

-2,16

</td>

<td>

-2,-4

</td>

<td>

2,-4

</td>

<td>

2,16

</td>

<td>

-2,4

</td>

<td>

-2,-16

</td>

</tr>

</table>

<i>Direction table:</i>

If you visualize the directions from the stepsize matrix, you'll get this diagram:

![](./images/dir.PNG "fig:dir.PNG")

### Screenshots

{| align=left |- |![Galaforce Intro screenshot](./images/Galaforce Intro.PNG "fig:Galaforce Intro screenshot")

**_Galaforce_ Intro screenshot**

_Posted: 16:22, 17 Aug 2011_ |![Galaforce Highscore screenshot](./images/Galaforce Score.PNG "fig:Galaforce Highscore screenshot")

**_Galaforce_ High Score screenshot**

_Posted: 16:22, 17 Aug 2011_ |![Galaforce Gamestart screenshot](./images/Galaforce Gamestart.PNG "fig:Galaforce Gamestart screenshot")

**_Galaforce_ Gamestart screenshot**

_Posted: 15:51, 03 Sep 2011_ | |}

### Video

{{\#ev:youtube|tsaApN-uG-U}}

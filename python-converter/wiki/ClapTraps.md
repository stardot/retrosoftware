# ClapTraps converted by Dave Jeffery

### Licence

GNU GPL v3 or later

### Introduction

_ClapTraps_ is BBC Micro conversion of the PyGame puzzle game written and designed by Richard Barnard _[1](https://sites.google.com/site/testpilotmonkeyproductions/)_.

[Discuss ClapTraps](http://www.retrosoftware.co.uk/forum/viewforum.php?f=92)

### Features

- Mode 4, 256x192 graphics

- 3 sets of 5 levels of varying sizes to explore

- Two tunes (title page and in-game)

### Progress

The game is currently 10% complete.

### Playable Demos

None.

### Credits

PyGame ClapTraps programming, game design and music: Richard Barnard

PyGame ClapTraps graphics: Richard Barnard and Dave Jeffery

BBC Micro ClapTraps: Dave Jeffery

BBC Micro ClapTraps Technical Advice: Rich Talbot-Watkins

### Development Environment

ClapTraps is developed in 6502, using BeebAsm by Rich Talbot-Watkins and Kate running on Fedora Linux, and tested using the Linux version of Tom Walker's B-Em. I used a Kate highlighting file for BeebAsm that I wrote myself.

The graphics were created in The GIMP with a special font created in CHARGEN (by Ian Trackman, on the Making the Most Of the Micro cassette). The CHARGEN graphics were converted into BeebAsm EQUW statements using a short assembler program I wrote in B-Em using the Master 128's EDIT utility.

The GIMP graphics were converted using Francis Loch's BBC Image Converter plus an assembler program I wrote in B-Em using Master 128 EDIT. I use David Boddie's ADF2INF.py utility to transfer text between B-Em and Kate.

### Screen shots

<table>

<tbody>

<tr class="odd">

<td><p>[[Image:claptraps-level1.png|512px|'''The BBC Micro graphics on the first level. <strong><br />

<em>Posted: Feb 17, 2013</em>]]<br />

</strong>The BBC Micro graphics on the first level. <em>'<br />

</em>Posted: Feb 17, 2013''</p></td>

</tr>

<tr class="even">

<td><p>[[Image:Chargen-font.png|512px|'''ClapTraps font designed in CHARGEN. <strong><br />

<em>Posted: Feb 17, 2013</em>]]<br />

</strong>ClapTraps font designed in CHARGEN. <em>'<br />

</em>Posted: Feb 17, 2013''</p></td>

</tr>

<tr class="odd">

</tr>

</tbody>

</table>

### Sample Video

None.

### Development Diary

**2013/02/25**

Having looked at David Boddie's source code for Jungle Journey, I realised I needed something like his PyQt map editor in order to create the maps for ClapTraps. It would be almost impossible to create the maps without some kind of utility as each map symbol takes up 5 bits, so it would take a lot of calculation to design a map by hand!

PyQt was something I had been meaning to learn anyway as I use the K Desktop Environment (KDE) on my own computer.

Therefore I've spent a few days looking at PyQt and refreshing my knowledge of Python. Today, before I could start working on an editor I needed to finalise the format of the level data for the levels sets. The level set format is given below.

The main limitation of BBC Micro ClapTraps compared to the PC Pygame version is the limit of 16 transporters per level - there were unlimited transporters on the PC version. However, on the level sets that come with the Pygame version the maximum number of transporters used on any level is 15, so this won't really be much of a limitation in practice. The other limitation is that there is an upper limit of map data - 16 screens spread over 5 levels. On the PC version you could have as many screens as you wanted which were as large as you wanted. However, the 16 screen limit will mean all the PC Pygame level sets will be able to be reproduced on the BBC Micro.

### ClapTraps Map Format

ClapTraps stores far more (approx. twice as much) ancillary data along with the map data in its level set files than a game like Repton, However, the map data is smaller in total.

Another difference between ClapTraps and, say Repton, is that the level set files can vary in size. This is because ClapTraps levels are not a fixed size. As this is a BBC Micro game there has to be a limit, and in the case of ClapTraps the five levels in total can be a maximum of 16 times the screen area. This may not actually sound a lot but remember in ClapTraps you can see more of the screen at once than in Repton.

A ClapTraps level set file can be between 992 bytes and 2696 bytes. I deliberately wanted relatively small level set files for those loading the game from cassette (or from UEF!).

Of this, there is a fixed introductory block of 392 bytes (& 188 bytes) followed by from 600 to 1920 bytes of map data. An interesting feature of ClapTraps is the text message that appears before you start a level set and when you complete it - this also has to be included in the level set file.

#### Map Data Organization

| | MIN | MAX |

|--------------------------|------------|------------|

| Level Dimensions | 7 bytes | 7 bytes |

| Dave's Staring Positions | 7 bytes | 7 bytes |

| Transporter Locations | 200 bytes | 200 bytes |

| Target Scores | 10 bytes | 10 bytes |

| Intro/Outro Text | 168 bytes | 168 bytes |

| Map Data | 600 bytes | 1920 bytes |

| TOTAL | 992 bytes | 2696 bytes |

| | &3E0 bytes | &A88 bytes |

#### Map symbols

`00` `space`

`01` `wall`

`02` `smiley`

`03` `frog` `(inactive)`

`04` `frog` `(active)`

`05` `box`

`06` `chopper`

`07` `transporter`

`08` `grass`

`09` `red` `frog` `(inactive)`

`10` `red` `frog` `(active)`

`11` `switch` `(on)`

`12` `switch` `(off)`

`13` `gate`

`14` `apple`

`15` `turret` `(up)`

`16` `turret` `(right)`

`17` `turret` `(down)`

`18` `turret` `(left)`

`19` `lazer` `(vertical)`

`20` `lazer` `(horizontal)`

`21` `key`

`22` `lock`

`23` `bush`

`24` `wall2`

`25` `wall3`

`26` `rock`

`27` `-` `31` `unused`

5 bits for each map square lets me store 0-31 i.e. 2^5 values

So, for instance:

16 x 12 map = 16 x 12 x 5 = 960 bits = 120 bytes

32 x 32 map = 32 x 32 x 5 = 5,120 bits = 640 bytes

#### Level Dimensions

Each of the 5 levels in a ClapTraps level set can be a different size.

The size of each level can be from (15, 11) to (31, 31) so you need 5 bits to store the level dimensions.

Therefore for each level the level dimensions takes up 10 bits, and for a level set the level dimensions take up 10 \* 5 = 50bits = 7 bytes.

The six MSBs of the final byte are free.

#### Dave's Starting Position

Dave has a starting position on each level. Dave's starting position can be from (0, 0) to (31, 31) so you need 5 bits to store the X and Y co-ordinate.

Therefore for each level Dave's starting position takes up 10 bits, and for a level set Dave's starting positions take up 10 \* 5 = 50bits = 7 bytes.

The six MSBs of the final byte are free.

#### Transporter locations

A transporter has a location (LX, LY) and a destination (DX, DY).

There can be up to 16 transporters on each level.

Transporter locations/destinations can be from (0, 0) to (31, 31), so you need 5 bits to store each X or Y co-ordinate.

Therefore we need (LX + LY + DX + DY) = 4 \* 5 = 20 bits for each transporter.

And we need 20 \* 16 \* 5 = 1600 bits = 200 bytes to store the transporter locations and destinations for a level set (40 bytes to store the transporter locations and destinations for a single level).

#### Target Scores

The aim of the game is to collect frogs - you have to collect at least as many as the "target score".

The maximum target score for a level could be 1023 (a 32 x 32 field of frogs) - 1 (Dave's starting position). Therefore to store the target score for each level you need 2 bytes, so for a level set you need 10 bytes.

#### Intro and outro text

Text is stored in ClapTraps level set file using 6 bits per character. That means we can use 2^6 = 64 different characters.

We use ASCII codes 32 to 95, so store 0-63 and add 32 afterwards.

ASCII codes 32 - 95 give us digits 0-9, capital A-Z plus some punctuation - more than enough for ClapTraps.

Each level set opens and closes with a message. The messages consists of 4 lines of max. 28 characters.

4 \* 28 \* 6bits = 84 bytes per message \* 2 messages (opening and closing) meaning we need 168 bytes per level set for messages.

#### The messages for RichardB's level sets

<code>0123456789012345678901234567

Level set 1

DAVE DREAMED OF A FROG FARM,

WHERE AMID SOFT RIBBITING

HE WOULD TEND HIS FLOCK.

BUT DAVE NEEDS FROGS!

DAVE COLLECTED HIS FROGS

AT THE END OF A HARD DAY

AND WENT BACK HOME.

GOODNIGHT DAVE!

Level set 2

DAVE HAD SOME FROGS,

BUT NOT ENOUGH

TO START HIS FARM.

GET MORE FROGS!

THERE WERE NOW MANY FROGS

HOPPING AROUND HIS FEET

AND DAVE SMILED.

DAVE LIKES FROGS!

Level set 3

THE FROGS SEEMED TO WANT

FRIENDS TO PLAY WITH

ON THE FARM.

LOTS OF FROGS!

HIS DREAM COME TRUE,

DAVE RESTED HIS FEET AND

LISTENED TO THE CROAKS.

WELL DONE DAVE!</code>

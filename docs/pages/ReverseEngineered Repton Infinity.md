Repton Infinity is a tool for creating Repton-like games released for the BBC Micro/Electron and BBC Master. The game includes 4 sample games and editors for maps, sprites and a programming language compiler for the Reptol language.

The games are designed to be stored on a DFS format disc, using DFS directories (a single alphanumeric character) to segregate the different files.

The filetypes are:

-   D - Combined file for source (BBC Master version only)
-   E - Thumbnail sprites (for the editors)
-   G - Linked game file (i.e. Run this to play)
-   M - Mapfile
-   O - Compiled object code from the source
-   S - Full size sprites (for the game)
-   T - Tokenised source code

## Combined Source File

No information yet.

## Thumbnail Sprites

The file is used to contain the sprites for the editing tools. The game has a fixed number (48) of sprites. So there are 48 chunks of sprite data.

Each chunk consists of 16 bytes in the mode 1 [BBC Micro sprite](BBC_Micro_sprite "wikilink") format. This will make a 4 colour sprite of 8 x 8 pixels.

## Linked Game File

The whole file is encrypted with a basic EOR scheme of:

`byte EOR key`

The key starts at 0 and is decreased by 3 each cycle, so we have:

`byte0 EOR 0`
`byte1 EOR 0xfd`
`byte2 EOR 0xfa`

The file is then munged into the following order, stuff seems to be padded out to fill up spaces, so the file should always be the same size:

`0x0000   Sprites (a direct copy of the sprite file stating from offset 0x114)`
`0x1800   scrap byte followed by Map Name`
`0x1810   scrap byte followed by Sprite Name`
`0x1820   scrap byte followed by Code Name`
`0x1830   scrap byte followed by Game Title (as supplied by Linker)`
`0x1850   scrap byte followed by Ending Message (as supplied by Linker)`
`0x1870   scrap byte followed by Filename (e.g. Rep3A)`
`0x1880   Object Code (as 0xf0 from the object file) padded with NULLs`
`0x1b50   Map data (from the map file)`
`0x2350   Map Sprites (from the sprite file)`
`0x2450   Object Code look up table (from 0x10 in the object file)`
`0x2530   0x8F (?)`

## Mapfile

### Header

| Offset | Length | Use                                                                  |
|--------|--------|----------------------------------------------------------------------|
| 0      | 16     | Name of author terminated with a 0x0d; the rest of the line is junk. |
| 0x10   | 0x200  | Map chunk 1                                                          |
| 0x210  | 0x200  | Map chunk 2                                                          |
| 0x410  | 0x200  | Map chunk 3                                                          |
| 0x610  | 0x200  | Map chunk 4                                                          |

### Map Chunks

| Offset | Length | Use                                                                               |
|--------|--------|-----------------------------------------------------------------------------------|
| 0      | 0x1d0  | Map data                                                                          |
| 0x1d0  | 24     | Teleporters (see below)                                                           |
| 0x1f8  | 1      | Map visible flag (01 = map visible)                                               |
| 0x1f9  | 1      | Password flag (01 = requires a password)                                          |
| 0x1fa  | 2      | Score - a 16 bit number in LLHH form                                              |
| 0x1fc  | 4      | Palette: 1 byte for each colour, the colour number is a standard BBC Micro colour |

The map has dimensions of 32 x 24 characters with 32 possible characters that can be used. The map is presented in a continuous stream of bits, starting from top left to bottom right. Each character is represented by 5 bits and all bits are munged together. E.g. the top right of Rep3 is Rock (6) Soil (7) Diamond (30) Soil (7) Curved Wall (20) Wall (4), which translates into:

`Rock   Soil     Diam  Soil     Wall   Wall `
`00110 00111 11110 00111 10100 00100`
`=0x31 0xfc 0x7a 0x10`

Teleporter data is given as 2 16 bit numbers (in LLHH form) for each teleport: source and destination. Each 16 bit number is an address. To get the co-ordinates divide and mod the numbers by 32. X is the mod, Y is the div

For example:

`source: 0x4a 0x02 => 586 = 10:18`
`dest:   0x95 0x01 => 405 = 12:21`

## Object Code

### Header

| Offset | Length | Use                                                          |
|--------|--------|--------------------------------------------------------------|
| 0      | 16     | Author Name 0xd terminated                                   |
| 0x10   | 32     | Low byte of the address of the DEFINE ACTION routine/sprite  |
| 0x30   | 32     | High byte of the address of the DEFINE ACTION routine/sprite |
| 0x50   | 32     | Low byte of the address of the DEFINE HITS routine/sprite    |
| 0x70   | 32     | High byte of the address of the DEFINE HITS routine/sprite   |
| 0x90   | 32     | System flags (1)/sprite                                      |
| 0xb0   | 32     | System flags (2)/sprite                                      |
| 0xd0   | 32     | User flags/sprite                                            |
| 0xf0   | ...    | 6502 machine code for the DEFINE routines, base is 0x5bb0    |

Code is translated from the Reptol directly to 6502 code. Then optimised to replace jsr xxxx:rts with jmp xxxx. This isn't perfect if the code is followed by an END, which will still stay as RTS.

### Code Equivalents

(Note all JSRs can be turned into JMPs by the optimising if they are the last statement in the logical flow. Also, the BBC Micro convention for hex - i.e. & instead of 0x has been used here.)

**CHANCE(x)** (75% used for the example code)

`  LDA #&FF`
`  STA &33`
`  LDA #&5F`
`  STA &34`
`  JSR &1D43`
`  BCS xxxx (IF)`

&5FFF = 75? Some form of floating point. Range is 0 - 99.99

**CHANGE(x,y)**

`  LDX #x`
`  LDY #y`
`  JSR &1982`

Where x and y are the sprite numbers to change from (x) to (y)

**!CONTENTS x**

`  CMP #x`

Where x is the sprite number (this is returned from the routine for LOOK(x).

**CREATE(x,d)**

`  LDY #d`
`  LDA #x`
`  JSR &19EB`

or, if in the HITS section:

`  LDY #d`
`  LDA #x`
`  JSR &1A54`

Where x is the sprite number

`     d is the direction, listed below. If this is not included d is &42`
`     `

d is the location to create. &42 is the current location on a grid of 32 characters. So W is -1; E is +1; N is -&20; S is +&20; NW is -&21; NE is +&19; SW is +&19; NE is +&21. (Why &42?)

**DEFINE** Is removed - reproduce these from the header

**EASTOF**

`  JSR &18A5`
`  BCC xxxx (IF)`

**EFFECT(x)**

`  LDA #x`
`  JSR &1C13`
`  `

**ELSE** Dealt with by IF. May not be reversible as the code for else looking the same as a GOTO.

**END**

`  RTS`

Not removed in Optimisation(!) even if preceded by a JSR; so you'll see the strange statement of JMP xxxx:RTS

**ENDIF** Dealt with by IF

**EVENT(x)**

`  LDA #&0e`
`  AND #x`
`  BNE xxxx (IF)`

The event timer byte (&000e) has a bit set for each timer that has gone off, so the AND is for the check of the bit:

`  6     &7f`
`  5     &3f`

**FLASH(x)**

`  LDA #x`
`  STA &0069`

Where x is the numeric equivalent of the colour, e.g. 3 = yellow

**FLIP**

`  LDA (&0058),Y`
`  EOR #&40`
`  STA (&0058),Y`

&0058 contains the status byte for the current object, bit 0x40 is the STATE() bit.

**GOTO (x)**

`  JMP xxxx`

xxxx will be the absolute address for the label code; i.e. you'll only have a JMP to 0x5bb0 for a GOTO.

**HITBY(x)**

`  LDA #&0049`
`  BNE xxxx (IF)`
`  `

**IF** Usually just implemented as a branch - this does depend on what's been tested. ELSE will be implemented by a JMP at the end of the first IF condition, so something like:

`  LDA (&0058),Y`
`  AND #&40`
`  BNE .else`
`  ...`
`  JMP .next`

.else JSR &1864

`  ...`

.next RTS

If a JSR has been turned into a JMP by the optimiser, assume that this is the end of the IF branch.

**KEY**

`  JSR &18CB`

**KILLREPTON**

`  INC &0010`
`  `

**LABEL** Not assembled, will have to reform it programatically

**LOOK(x)**

`  JSR xxxx`

These are implemented as separate routines for each direction:

`F  &17EA    SW &1836    W  &1844`
`R  &17EE    SE &1834    E  &1850`
`B  &17F2    NW ?        S  &185A`
`L  &17F6    NE ?        N  &1864`

**MOVE(x)**

`  LDA #x`
`  JSR &19AE`

Where x is the numeric equivalent of the direction:

`0  E     1  S        2  W        3  N`
`4  F     5  R        6  B        7  L`

**MOVING**

`  LDA (&0058),Y`
`  BPL xxxx`

Bit 7 of the object status is the moving flag.

**NAME** Not assembled, with have to reform it programmatically.

**NORTHOF**

`  JSR &18B3`
`  BCC xxxx (IF)`
`  `

**NOT** Swaps the logic over in the IF, e.g. BMI instead of BPL.

**SCORE(x)**

`  LDA #x`
`  JSR &1B37`
`  `

**SOUND(x)**

`  LDA #x`
`  JSR &1c1d`

**SOUTHOF**

`  JSR &188D`
`  BCC xxxx (IF)`
`  `

**STATE(x)**

`  LDA (&0058),Y`
`  AND #&40`
`  BNE xxxx (IF)`

**WESTOF**

`  JSR &189B`
`  BCC xxxx (IF)`

User flags are stored in &64

## Sprite File

### Header

| Offset | Length | Use                                                                |
|--------|--------|--------------------------------------------------------------------|
| 0      | 1      | Colour 0                                                           |
| 1      | 1      | Colour 1                                                           |
| 2      | 1      | Colour 2                                                           |
| 3      | 1      | Colour 3                                                           |
| 4      | 16     | Name of author terminated with 0x0d; the rest of the line is junk. |
| 0x14   | 256    | Map sprite chunk                                                   |
| 0x114  | 6144   | Sprite chunk                                                       |
||

### Map Sprite Chunk

Each entry is 8 bytes in the mode 5 [BBC Micro sprite](BBC_Micro_sprite "wikilink") format (2bpp = 4 ppB), rectangular pixels. The size of each image is 4 x 8.

### Sprite chunk

Each entry is 128 bytes in the mode 5 [BBC Micro sprite](BBC_Micro_sprite "wikilink") format (2bpp = 4 ppB), rectangular pixels. The size of each image is 16 x 32.

## Source Code

### Header

| Offset | Length | Use                                                                  |
|--------|--------|----------------------------------------------------------------------|
| 0      | 16     | Name of author terminated with a 0x0d; the rest of the line is junk. |

### Language Chunks

There are 48 language chunks (one for each sprite, including those that cannot be given any commands). The language chunk will consist of tokenised code, using 0x0d as a line terminator and being terminated by a 0xfe byte. If the language chunk is empty, the contents will be 0x0d 0xfe.

The language tokens are:

| Token | Command | Token | Command    |
|-------|---------|-------|------------|
| 80    | NAME    | 81    | HITBY      |
| 82    | LOOK(   | 83    | DEFINE     |
| 84    | CREATE( | 85    | IF         |
| 86    | MOVING  | 87    | ELSE       |
| 88    | ENDIF   | 89    | GOTO       |
| 8A    | NOT     | 8B    | KILLREPTON |
| 8C    | CHANGE( | 8D    | END        |
| 8E    | SCORE(  | 8F    | SOUND(     |
| 90    | FLIP    | 91    | EFFECT(    |
| 92    | FLASH(  | 93    | CHANCE(    |
| 94    | KEY     | 95    | One        |
| 96    | Two     | 97    | Four       |
| 98    | TYPE    | 99    | ACTION     |
| 9A    | HITS    | 9B    | MOVE(      |
| 9C    | STATE(  | 9D    | LABEL      |
| 9E    | EVENT(  | 9F    | CONTENTS   |
| A0    | Animate | A1    | RED        |
| A2    | GREEN   | A3    | YELLOW     |
| A4    | BLUE    | A5    | MAGENTA    |
| A6    | CYAN    | A7    | WHITE      |
| A8    | WESTOF  | A9    | SOUTHOF    |
| AA    | EASTOF  | AB    | NORTHOF    |

Indents are performed by a byte greater than 0xc8, the indent is byte - 0xc8 spaces. So 0xcf will indent 6 spaces.

There may be junk after the 48 entries, this must be ignored.

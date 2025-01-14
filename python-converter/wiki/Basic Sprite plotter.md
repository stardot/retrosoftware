# Basic Sprite Plotter (Mode 2 no Mask)

These routines will allow a sprite to be plotted anywhere on a 20K screen (Mode 2 for example). Simple adjustments can be made to make it work for other screen modes.

## Provisos and restrictions

- The sprite must be in the format generated by [Swift](SWIFT "wikilink"), see the documentation contained in the Swift download for details.

- The code listed is from a [Swift](SWIFT "wikilink") Project, if you are not assembling and running it within [Swift](SWIFT "wikilink") then you will need to make some adjustments.

- No check is made to see if the sprite is going to be partially (or wholly) off screen. If it goes off screen without you adding in checking code then corruption of your program code may result, or at the very least the sprite will appear partially on the other side of the screen.

- To make full use in a program you'll need an sprite erase routine.

- Written in P65 Ophis assembler and specifically for use as a [Swift](SWIFT "wikilink") Project

## The easy way

Download a copy of [Swift](SWIFT "wikilink") (if you've not already got it) and download the [Swift](SWIFT "wikilink") project in the download section below which has all the code. Once extracted (and your [Swift](SWIFT "wikilink") installation is set up for P65) from the Zip just load the project into [Swift](SWIFT "wikilink") and Run ! This way you'll get about a dozen different sprites to play with as well.

## The hard way

If you can't run [Swift](SWIFT "wikilink") (due to your platform of choice) then you'll need to download the sprites and binary data seperatly (see download links at bottom and adjust the source code to either amalgamate it all together and/or change the [Swift](SWIFT "wikilink") specific links.

## Code

Main

` .org $1900 ; load a traditional Beeb start address for a disk system`

`            ; we'll load in other code lower than this after we've started`

` `

` .require "Macros"`

` .require "AcornConstants"  .merge "SpritePlotter"  `

` .require "DroidConstants"`

` Main:`

` lda #`<MySpriteObject

sta $70

lda #>`MySpriteObject`

` sta $71`

` jsr SpritePlotter.PlotSprite`

` rts`

` `

` MySpriteObject:`

` .byte Stryker,24,141  ; id of sprite (see Droid constants), X nd Y Pos`

Sprite Plotter

` ;Main Sprite plot routine, in mode 1`

` `

` ; MEMORY USED`

` ; $72 - $7A  directly`

` ; $9F in Times8 Macro`

`                                                   `

` ;on entry $70,$71 point to a sprite object structure.`

` ; This is the properties on the sprite, such as which one, x,y etc.`

` ; it does not contain actual sprtie data, that is worked out from the`

` ; sprite id Structure is`

` `

` ;offset   meaning`

` ;00       SpriteID ; so supports 128 different sprites (0-127)`

` ;01       X Pos    ; it's only 128 as we use this value * 2 to index into the sprite`

` ;02       Y Pos    ; data structure pointer table`

`                                    `

` ; Sprite ID's. These index into a look up table of  memory locations`

` ; that points to the Sprite graphic data structure.`

` `

` ;Sprite Graphic Structure `

` ; `

` `

` ;offset       meaning`

` ;00           width`

` ;01           height`

` ;02->to end   graphic data `

`   `

` .require "Macros"  `

` .require "DroidConstants"`

` ;definitions for this file`

` .alias SpriteObjectStructure $70`

` .alias SpriteGraphicStructure $72`

` .alias XOrd $74`

` .alias YOrd $75`

` .alias Width $76`

` .alias Height $77`

` .alias YScreenAddress $78 ; and 79`

` .alias SpritePixel $7A    `

` .alias XStartOffset $7B ; remember X offset start, which needs to be the same at start of every new column`

` .alias ScreenStartHighByte $30`

` `

` PlotSprite:`

`   ; work out screen address that sprite starts at from xy ords`

`   ldy #0`

`   sty YScreenAddress ; just ensure is 0`

`   lda #ScreenStartHighByte`

`   sta YScreenAddress+1`

`   lda(SpriteObjectStructure ),Y  ; sprite ID`

`   asl ; get start of sprite graphics, this gets the address of it`

`   tax ; so got the index into the data`

`   clc`

`   lda GameSprites,x`

`   adc #`<GameSprites

    sta SpriteGraphicStructure

    inx

    lda GameSprites,x

    adc #>`GameSprites`

`   sta SpriteGraphicStructure+1              ; so now point to sprite graphic data  `

`   lda (SpriteGraphicStructure),Y ; width`

`   sta Width`

`   iny`

`   lda(SpriteObjectStructure ),Y   ; X`

`   sta XOrd`

`   lda(SpriteGraphicStructure),Y   ; height `

`   sta Height`

`   iny`

`   lda(SpriteObjectStructure),Y  ; YOrd   `

`   sec`

`   sbc #1`

`   clc`

`   adc Height  ; but only to nearest character row start`

`   sta YOrd`

`   and #7     ; put low order bits in X  for index addressing`

`   tax     `

`   sta XStartOffset ; preserve this for use later`

`   lda YOrd      ; then store the other bits 3-7 in YOrd to get screen address of nearest character start row`

`   and #248`

`   sta YOrd`

`   jsr ScreenStartAddress                 `

`   ; now we've got the screen start address, and address of alien, lets plot it`

`   lda YScreenAddress ; put address in code below`

`   sta ScreenPixelAddress+1      `

`   lda YScreenAddress+1        `

`   sta ScreenPixelAddress+2     `

`   clc`

`   lda SpriteGraphicStructure     ; move to start of actual graphics data`

`   adc #2 ; to move past width and height`

`   sta SpritePixelAddress+1`

`   lda SpriteGraphicStructure+1`

`   adc #0`

`   sta SpritePixelAddress+2`

`   `

`   ;ok the main plot bit`

`   `

`   PlotXLoop:`

`     ldy Height `

`     dey  `

`     PlotLoop:   `

`       SpritePixelAddress:`

`       lda $FFFF,Y     ;dummy address, will be filled in by code`

`       ScreenPixelAddress:`

`       sta $FFFF,X     ; dummy address, will be filled in by code`

`       ; are we at a boundary`

`       dex                  `

`       bpl NotAtRowBoundary   ;   no, so carry on`

`         ;yes we moved to another character row, so we really want this to be the start of next screen row`

`         sec                     ; we do this by adding &279 to value to get to next row`

`         lda ScreenPixelAddress+1`

`         sbc #$80`

`         sta ScreenPixelAddress+1  `

`         lda ScreenPixelAddress+2`

`         sbc #2`

`         sta ScreenPixelAddress+2   `

`         ldx #7 ; reset X to 7 (bottom of this character row)`

`       NotAtRowBoundary:`

`       dey`

`       bpl PlotLoop    ; have we finished a full column, go to plot loop if not`

`       dec Width`

`       beq EndPlotSprite   ; no more to plot, exit routine`

`     ; move to next column`

`     clc`

`     lda SpritePixelAddress+1`

`     adc Height`

`     sta SpritePixelAddress+1`

`     lda SpritePixelAddress+2`

`     adc #0  `

`     sta SpritePixelAddress+2      `

`     lda YScreenAddress`

`     clc`

`     adc #8`

`     sta YScreenAddress`

`     sta ScreenPixelAddress+1  `

`     lda YScreenAddress+1`

`     adc #0                     `

`     sta YScreenAddress+1`

`     sta ScreenPixelAddress+2 `

`     ldx XStartOffset  `

`   jmp PlotXLoop ;never zero so always branches`

`   EndPlotSprite:`

` `

` rts`

` GameSprites:  `

` .incbin "DroidSprites"`

` LookUp640:  ; a 640x multiplication table`

` .incbin "LookUpTable640"`

` `

` ScreenStartAddress:`

`   ; calculates the screen start address for a mode 2 screen given an X,Y address`

`   ; if X or Y go beyond screen limits then returns 0 else the address`

`   ; on entry $74=X, $75=Y, returns result in $78,$79`

` `

`   ; We use a 640 multiplication look up table`

`   ; to speed things up. The Y ord is actually in pixels but due to the way the`

`   ; screen is made up by the 6850 we only need the multiplication for character`

`   ; rows (every 9th row, i.e. 8 rows per character)`

`   ; so divide Y by 8 to get character rows  but as there stored as two byte per entry in multiplication table`

`   ; each we only need to divide by 4 to get our index into the table`

`   `

`   lda YOrd`

`   and #248   ; FIRST REMOVE THE 0 TO 7 VALUE that we don't need to resolve, as screen`

`              ; goes down from 0 to 7 ok, just for rest of bits we need to calc 640`

`   lsr`

`   lsr`

`   tay`

`   lda LookUp640,Y`

`   clc`

`   adc YScreenAddress ; lo byte value of the 640 look up`

`   sta YScreenAddress`

`   iny`

`   lda LookUp640,Y  ;accumulator now has hi byte`

`   adc YScreenAddress+1`

`   sta YScreenAddress+1  ; so should have base row for Y`

`   ; now we have the character row that the sprite is going to plot at`

`   ; we need to refine this to a actual row. all we need do is add on`

`   ; the lower 3 bits of the Y address that we shifted out with lsr a few lines ago`

`   ; and due to the way the address is, we will never get a carry so only a normal`

`   ; 8 bit addition`

`   ; no need to clc as still clear from earlier`

`   lda YOrd`

`   and #7 ; remove unwanted high order bits leaving us with just the lower 3 bits`

`   clc`

`   adc YScreenAddress  ; don't need to add n carry to hi byteas will never occur as`

`   sta YScreenAddress  ; the max of 7 added to the start of a character row will never go ovr 255`

`   ; right we've now got the Y component of the address, now we've to add in the`

`   ; X component. For every X pixel we need to add 8 bytes, for this we won't use`

`   ; a look of table as it's quite easy and quickish to multiply by 8. `

`   ; It is true that it would be quicker with a look uo table but it would take`

`   ; about 320 bytes for only a small gain`

``   `Times8 XOrd, YScreenAddress``

`   rts`

` ; end ScreenStartAddress`

` `

` `

`  `

Acorn Constants

`.alias oswrch $ffee`

Macros

general macros not acorn specific

` .macro mode`

`   lda #$16`

`   jsr oswrch`

`   lda #_1`

`   jsr oswrch`

` .macend`

` `

` .macro lsr3`

`   ; shifts the accumulator left parameter 1 number of times`

`   lsr`

`   lsr`

`   lsr`

` .macend`

` `

` .macro Times8`

`   ; multiply contents of param1 and add result to`

`   ; contents of param1 and param1+1`

`   ; uses 9F as scratchpad space`

`   ; A corrupted, param1 corrupted`

`   lda #0`

`   sta $9F    ; clear out hi part of result `

`   clc`

`   asl _1`

`   rol $9F`

`   asl _1`

`   rol $9F`

`   asl _1`

`   rol $9F`

`   ; ok got result of multiplication, now add to param2 contents`

`   lda _1`

`   clc`

`   adc _2`

`   sta _2`

`   lda $9F`

`   adc _2+1`

`   sta _2+1`

` .macend`

Droid Constants

`.alias Stryker 9`

Boot File

`MO.2`

`VDU 19,8,0,0,0,0`

`*MAIN`

LookUpTable640 (download below if required)

`00 00 80 02 00 05 80 07 00 0A 80 0C 00 0F 80 11`

`00 14 80 16 00 19 80 1B 00 1E 80 20 00 23 80 25`

`00 28 80 2A 00 2D 80 2F 00 32 80 34 00 37 80 39`

`00 3C 80 3E 00 41 80 43 00 46 80 48 00 4B 80 4D`

## Downloads

[The enitre Swift Project](../../retrosoftwarecouk_wiki-20160918-wikidump/images/Swift CodeNameDroid.zip "wikilink") (Highly recommended, just load into Swift and run ! )

[ LookUpTable640](../../retrosoftwarecouk_wiki-20160918-wikidump/images/Swift SpritePlotter LookUpTable640.zip "wikilink") ( 640 times look up table)

[Sprite data](../../retrosoftwarecouk_wiki-20160918-wikidump/images/Swift SpritePlotter DroidSprites.zip "wikilink") (The sample sprites)

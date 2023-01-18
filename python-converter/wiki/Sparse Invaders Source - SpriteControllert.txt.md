## Sparse Invaders Source - SpriteController.txt

The Sprite Controller manages any active sprites. This was the first module I really implemented when first working on the Sparse Invaders. That's really trying to explain that it's a little overly complex for the Beeb. In Sparse Invaders, the only sprites under this controller are the player, bullets, mothership and explosions. If you are to use this sprite controller then please be aware that it has limitations. To keep the game running faster the Invaders are drawn using a much more simplier and faster technique. However that said, when initializing the sprite, it does pre-calculate and store certain parameters within the sprite structure to speed things along alittle when drawing the sprite. There are certainly pro's and con's when using this controller, however for simple games this more then does the job.

Please refer to constants.txt for details for the sprite structure.

`  ;-------------------------------------------------------------------------------`

`   ;  SpriteController`

`   ;  Written by Neil Beresford.`

`   ;`

`   ;  Copyright 2008,2009 Neil Beresford`

`   ;`

`   ;    This file is part of Sparse Invaders.`

`   ;    Sparse Invaders is free software: you can redistribute it and/or modify`

`   ;    it under the terms of the GNU General Public License as published by`

`   ;    the Free Software Foundation, either version 3 of the License, or`

`   ;    (at your option) any later version.`

`   ;`

`   ;    Sparse Invaders is distributed in the hope that it will be useful,`

`   ;    but WITHOUT ANY WARRANTY; without even the implied warranty of`

`   ;    MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the`

`   ;    GNU General Public License for more details.`

`   ;`

`   ;    You should have received a copy of the GNU General Public License`

`   ;    along with Sparse Invaders.  If not, see <`[`http://www.gnu.org/licenses/`](http://www.gnu.org/licenses/)`>.`

`   ;`

`   ;`

`   ;   Notes:`

`   ;`

`   ;  Sprite fix array, screen active list`

`   ;`

`   ;  Functionality...`

`   ;  Sprite core system:`

`   ;     SpriteInit           - pressetup for sprite system - holds test code at present.`

`   ;     SpriteStart          - Adds sprite into control system`

`   ;     SpritesDrawActive    - Draws all activate sprites - max limit of 6`

`   ;     SpritesWipeActive    - Wipes the area that the sprite was drawn to`

`   ;     SpriteDraw           - sprite drawer`

`   ;     SpriteWipe           - sprite wipe`

`   ;`

`   ;  Support Functionality;`

`   ;     SpriteClear          - clears the sprite structure within the active array`

`   ;     SpriteActivate       - marks the active position within `

`   ;     SpriteCalcScreenPos  - calculates the screen position address from X,Y`

`   ;     SpriteRetreiveDetails- gets the sprite data, width and height for the sprite from its data`

`   ;`

`   ;-------------------------------------------------------------------------------`

`   .require "Constands"`

`   .require "Macros"`

`   ;-------------------------------------------------------------------------------`

`   ; SpriteInit - `

`   ;     inits the sprite system`

`   ;`

`   ;-------------------------------------------------------------------------------`

`   SpriteInit:`

`      ; clear the sprite data ...`

`      ; [NOTE] this assumes at present, less then 255 bytes for the data ... `

`      LDA  #0`

`      LDX  #TOTAL_SPRITE_SPACE `

`   SI_Clearlist:`

`      DEX`

`      STA  SPRArray,X`

`      BNE  SI_Clearlist`

`      ; clear the active list ...`

`      LDX  #TOTAL_ACTIVE_SPRITES - 1`

`      LDA #$ff`

`   SI_ClearActives:   `

`      STA  SPRActive,X`

`      DEX`

`      BPL  SI_ClearActives`

`      RTS`

` `

`   ;-------------------------------------------------------------------------------`

`   ;  SpriteStart:   `

`   ;         Starts the sprite, activating it...`

`   ;   Regs - A sprite number for storage. (SprArray)`

`   ;          X sprite X`

`   ;          Y sprite Y`

`   ;     SPRITE sprite frame  <--- SPRITE is in Zero page`

`   ; CALLPARMA1 used for the callback for the control... `

`   ; CALLPARMA2 ... ( have blank if not needed ) `

`   ;-------------------------------------------------------------------------------`

`   SpriteStart:`

`      CLC`

`      ROL`

`      ROL`

`      ROL`

`      ROL`

`      STA  SCRATCH1`

`      STX  XPOS`

`      STY  YPOS`

`      JSR  SpriteClear`

`      LDA  SCRATCH1`

`      JSR  SPriteActivate`

`      STX   CURRENT_SPRITE`

`      CLC`

`      LDA   #`<SPRArray

       ADC   SCRATCH1

       STA   TEMPPTR

       LDA   #>`SPRArray`

`      ADC   #0`

`      STA   TEMPPTR+1`

`      LDY   #0   `

`      LDA   XPOS                ; 0 Xpos`

`      STA   (TEMPPTR), Y `

`      INY`

`      LDA   YPOS                ; 1 Ypos`

`      STA   (TEMPPTR), Y `

`      INY`

`      LDA   SPRITE              ; 2 frame`

`      STA   (TEMPPTR), Y    `

`      INY`

`      LDA   CALLPARAM1          ; 3 control`

`      STA   (TEMPPTR), Y `

`      LDA   CALLPARAM2`

`      INY`

`      STA   (TEMPPTR), Y        ; 4 ... `

`                        `

`      ; PLEASE PLEASE do not move this away from the YPOS adjust as I did! Sigh!`

`      LDA   SPRITE`

`      JSR   SpriteRetreiveDetails`

`      LDY   #SPRBLK_WIDTH`

`      STA   (TEMPPTR), Y        ; store width`

`      TXA`

`      INY`

`      STA   (TEMPPTR), Y        ; store height`

`     `

`      ; adjust Y pos to bottom of sprite,`

`      CLC`

`      ADC  YPOS`

`      SEC`

`      SBC  #1`

`      STA  YPOS`

`      ; adjust the YPOS to character based and store the offset in x for indexing`

`      AND  #$07`

`      STA  XOFFSET`

`      LDA  YPOS`

`      AND  #$f8`

`      STA  YPOS`

`      jsr   SpriteCalcScreenPos`

`      `

`      LDA   #SPRFLAG_REDRAW`

`      LDY   #SPRBLK_FLAG`

`      STA   (TEMPPTR), Y        ; Mark the sprite for redraw`

`      LDY   #SPRBLK_SPRDATA`

`      LDA   CURRENTSPRITEDATA`

`      STA   (TEMPPTR),Y         ; store sprite data  `

`      INY`

`      LDA   CURRENTSPRITEDATA+1  `

`      STA   (TEMPPTR),Y  `

`      LDY   #SPRBLK_XOFFSET    ; Xoffset`

`      LDA   XOFFSET`

`      STA   (TEMPPTR),Y    `

`      LDY   #SPRBLK_XOFFBACK`

`      STA   (TEMPPTR),Y`

`      LDA   SCREENADD          ; 6 SCREEN ADD`

`      LDY   #SPRBLK_SCREENADD`

`      STA   (TEMPPTR),Y    `

`      INY`

`      LDA   SCREENADD+1        ; 7  /\  /\`

`      STA   (TEMPPTR),Y    `

`      LDY   #SPRBLK_SCRBACK    ; screen position used for wiping spr`

`      LDA   SCREENADD`

`      STA   (TEMPPTR),Y`

`      INY`

`      LDA   SCREENADD+1`

`      STA   (TEMPPTR),Y`

`   SI_Debug:`

`       `

`      RTS`

`   ;-------------------------------------------------------------------------------`

`   ; SpriteMoveSprite - `

`   ;     Moves the sprite to the adsolute pos passed in`

`   ;     A - sprite slot index ( sprite * 8 )`

`   ;     X - x pos`

`   ;     y - y pos`

`   ;-------------------------------------------------------------------------------`

`   SpriteMoveSprite:`

`      CLC`

`      ROL`

`      ROL`

`      ROL`

`      ROL`

`      STA  SCRATCH1`

`      STX  XPOS`

`      STY  YPOS`

`      CLC`

`      LDA   #`<SPRArray

       ADC   SCRATCH1

       STA   TEMPPTR

       LDA   #>`SPRArray`

`      ADC   #0`

`      STA   TEMPPTR+1`

`   SpriteMoveSpr:`

`      ; store the x and y position`

`      LDA   XPOS`

`      LDY   #SPRBLK_X`

`      STA   (TEMPPTR), Y`

`      LDA   YPOS`

`      INY`

`      STA   (TEMPPTR), Y`

`      `

`            `

`      ; get the width and height for drawing the sprite`

`      LDY   #SPRBLK_WIDTH`

`      LDA   (TEMPPTR), Y`

`      STA   WIDTH`

`      INY`

`      LDA   (TEMPPTR), Y`

`      STA   HEIGHT`

`      ; adjust Y pos to bottom of sprite,`

`      CLC`

`      ADC  YPOS`

`      SEC`

`      SBC  #1`

`      STA  YPOS`

`      ; adjust the YPOS to character based and store the offset in x for indexing`

`      AND  #$07`

`      STA  XOFFSET`

`      LDA  YPOS`

`      AND  #$f8`

`      STA  YPOS`

`      jsr   SpriteCalcScreenPos`

`    `

`      LDA   XOFFSET`

`      LDY   #SPRBLK_XOFFSET    ; 5 Xoffset`

`      STA   (TEMPPTR),Y    `

`      LDA   SCREENADD          ; 6 SCREEN ADD`

`      INY`

`      STA   (TEMPPTR),Y    `

`      LDA   SCREENADD+1        ; 7  /\  /\`

`      INY`

`      STA   (TEMPPTR),Y    `

`      LDY   #SPRBLK_FLAG`

`      LDA   (TEMPPTR), Y`

`      ORA   #SPRFLAG_REDRAW`

`      STA   (TEMPPTR), Y        ; Mark the sprite for redraw`

`      RTS`

`   ;-------------------------------------------------------------------------------`

`   ; SpriteActivate - `

`   ;     Activates the sprite slot`

`   ;     A - sprite slot index ( sprite * 8 )`

`   ;-------------------------------------------------------------------------------`

`   SpriteActivate:`

`      TAY`

`      `

`      LDX   #TOTAL_ACTIVE_SPRITES-1`

`      LDA   #$ff`

`   SA_Loop:`

`      CMP   SPRActive,X`

`      BEQ   SA_found`

`      DEX`

`      BPL   SA_loop`

`      RTS`

`   SA_found:`

`      TYA`

`      STA   SPRActive,X`

`      RTS`

`         `

`   ;-------------------------------------------------------------------------------`

`   ; SpriteClear - `

`   ;     clears sprite data and removes from active list if present..`

`   ;     A - sprite slot indexed ( sprite * 16 )`

`   ;`

`   ;-------------------------------------------------------------------------------`

`   SpriteClear:`

`      PHA   `

`      ; firstly check and remove if found in active list`

`      LDX   #TOTAL_ACTIVE_SPRITES-1`

`   SC_checkActive:   `

`      CMP  SPRActive,X`

`      BNE  SC_decIndex`

`   SC_foundActive:   `

`      LDA  #$ff`

`      STA  SPRActive,X`

`      ; now clear the sprite slot ...`

`      PLA`

`   SC_ClearData:`

`      STA  SCRATCH1`

`      LDA  #`<SPRArray

       CLC

       ADC  SCRATCH1

       STA  TEMPPTR

       LDA  #>`SPRArray`

`      ADC  #0`

`      STA  TEMPPTR+1`

`      `

`      LDY  #SIZEOF_SPRITE_BLOCK -1  `

`   SC_clear:`

`      STA  (TEMPPTR),Y`

`      DEY`

`      BPL  SC_clear`

`      RTS`

`   SC_decIndex:`

`      DEX`

`      BPL  SC_checkActive`

`      PLA           ; pop stack...`

`      RTS`

`   ;-------------------------------------------------------------------------------`

`   ; SpriteDrawActive`

`   ;        worth through the active sprites, drawing any that are needed.`

`   ;-------------------------------------------------------------------------------`

`   SpritesDrawActive:`

`      ; firstly check and remove if found in active list`

`      LDX   #TOTAL_ACTIVE_SPRITES-1`

`   SDA_Loop:`

`      STX   ACTIVEINDEX`

`      LDA   SPRActive,X`

`      CMP   #$ff`

`      BEQ   SDA_Next`

`      `

`   SDA_Found:`

`      ; calculate the offset to the start of active sprite data`

`      STA   SPRITE`

`      CLC`

`      LDA   #`<SPRArray

       ADC   SPRITE

       STA   TEMPPTR

       LDA   #>`SPRArray`

`      ADC   #0`

`      STA   TEMPPTR+1`

`      LDY   #SPRBLK_FLAG`

`      LDA   (TEMPPTR),Y`

`      AND   #SPRFLAG_REDRAW`

`      BEQ   SDA_Next`

`      STX   SCRATCH1`

`            `

`      jsr SDA_SetupSprite `

`    `

`      LDX   STOREX`

`      LDY   STOREY`

`      ; draw the sprite to screen...`

`      JSR   SpriteDraw`

`      ; clear the redraw flag...`

`      LDY   #SPRBLK_FLAG`

`      LDA   (TEMPPTR),Y`

`      AND   #SPRFLAG_NOT_REDRAW`

`      STA   (TEMPPTR),Y`

`      LDY   #SPRBLK_CTRL   `

`      LDA   (TEMPPTR),Y`

`      BEQ   SDA_Next`

`      STA   USERPTR`

`      INY`

`      LDA   (TEMPPTR),Y`

`      STA   USERPTR+1`

`      ; NOTE - RTS pops the low then high byte, adds one`

`      ; then sets the PC to that address. The example in`

`      ; 6502.org shows the high byte od SDA_Return with -1`

`      ; on it as well. I can only assume it's parsed left `

`      ; to right -  I'm concerned if this address falls on a 256`

`      ; boundary.`

`      ; might be a bug in p65 - investigate later, as address calculated`

`      ; correctly as of writting. `

`      LDA   #>SDA_Return`

`      PHA`

`      LDA   #`<SDA_Return-1

       PHA

       JMP   (USERPTR)



    SDA_Return:

    SDA_Next:



       LDX   ACTIVEINDEX

       DEX

       BPL   SDA_Loop



       RTS



    SDA_SetupSprite:



       ; get the x and y and frame for drawing the sprite

       LDY   #0

       LDA   (TEMPPTR), Y

       STA   STOREX

       INY

       LDA   (TEMPPTR), Y

       STA   STOREY

       INY

       LDA   (TEMPPTR), Y



       TAX                          ; frame saved



       ; retrieve the screen position for drawing the sprite ...



       LDY   #SPRBLK_XOFFSET        ; sprite screen drawing

       LDA   (TEMPPTR), Y

       STA   XOFFSET

       INY

       LDA   (TEMPPTR), Y

       STA   SCREENADD

       STA   SCREENADD_BACK

       INY

       LDA   (TEMPPTR), Y

       STA   SCREENADD+1

       STA   SCREENADD_BACK+1



       LDY   #SPRBLK_WIDTH          ; sprite width and height

       LDA   (TEMPPTR), Y

       STA   WIDTH

       STA   CURRENT_SPR_W

       INY

       LDA   (TEMPPTR), Y

       STA   HEIGHT

       STA   CURRENT_SPR_H



       LDY   #SPRBLK_SPRDATA        ; sprite data

       LDA   (TEMPPTR),Y

       STA   CURRENTSPRITEDATA

       INY

       LDA   (TEMPPTR),Y

       STA   CURRENTSPRITEDATA+1



       TXA

       RTS





    ;-------------------------------------------------------------------------------

    ; SpriteWipeActive

    ;        worth through the active sprites, clearing any that are needed.

    ;-------------------------------------------------------------------------------

    SpritesWipeActive:



       ; firstly check and remove if found in active list

       LDX   #TOTAL_ACTIVE_SPRITES-1



    SWA_Loop:

       STX   ACTIVEINDEX



       LDA   #$ff

       CMP   SPRActive,X

       BEQ   SWA_Next



    SWA_Found:



       LDA   SPRActive,X

       STA   SPRITE



       ; check the redraw flag ...

       CLC

       ADC   #SPRBLK_FLAG

       TAX

       LDA   SPRArray,X



       AND   #SPRFLAG_REDRAW

       BEQ   SWA_Next



       ; clear the sprite to screen...



       LDA   SPRITE

       JSR   SpriteWipe



       ;

       ; tempptr has been set within the spritewipe function

       ; Set the new screen position to be the old one ...



       LDY   #SPRBLK_FLAG

       LDA   (TEMPPTR),Y

       AND   #SPRFLAG_KILL

       BEQ   SWA_SetScreen



       ; kill sprite ... remove from list

       LDX   ACTIVEINDEX

       LDA   #$ff

       STA   SprActive,X



       JMP   SWA_Next



    SWA_SetScreen:



       LDY   #SPRBLK_SCREENADD

       LDA   (TEMPPTR),Y

       LDY   #SPRBLK_SCRBACK

       STA   (TEMPPTR),Y

       LDY   #SPRBLK_SCREENADD2

       LDA   (TEMPPTR),Y

       LDY   #SPRBLK_SCRBACK2

       STA   (TEMPPTR),Y



       LDY   #SPRBLK_XOFFSET

       LDA   (TEMPPTR),Y

       LDY   #SPRBLK_XOFFBACK

       STA   (TEMPPTR),Y



    SWA_Next:



       LDX   ACTIVEINDEX

       DEX

       BPL   SWA_Loop



       RTS



    ;-------------------------------------------------------------------------------

    ; SpriteRetreiveDetails - a Sprite number

    ;              returns A - width, X - heighht

    ;

    ;-------------------------------------------------------------------------------

    SpriteRetreiveDetails:



       ; calculate the index...

       ASL

       TAX

       CLC



       ; get and store the pointer to the sprtie data ...

       LDA  spriteData,X

       ADC  #<spriteData

       STA  CURRENTSPRITEDATA

       INX

       LDA  spriteData,X

       ADC  #>`spriteData`

`      STA  CURRENTSPRITEDATA+1`

`      ; grab the sprite info ...`

`      LDY  #SPRDATA_HEIGHT`

`      LDA  (CURRENTSPRITEDATA),Y`

`      TAX`

`      DEY`

`      LDA  (CURRENTSPRITEDATA),Y`

`      `

`      RTS`

`   ;-------------------------------------------------------------------------------`

`   ; SpriteDraw - a Sprite number = referenced from SPRArray`

`   ;              The following need to be setup prior to calling this...`

`   ;              SPRITEADD, WIDTH, HEIGHT, XOFFSET, CURRENTSPRITEDATA`

`   ;-------------------------------------------------------------------------------`

`   SpriteDraw:`

`      ; store the sprite number, x and y position`

`      STA  SPRITE`

`      STX  XPOS`

`      STY  YPOS`

`    `

`      ; now store sprite data and screen address in code`

`      LDA  SCREENADD`

`      STA  ScreenAddPtr+1`

`      LDA  SCREENADD+1`

`      STA  ScreenAddPtr+2`

`      `

`      CLC`

`      LDA  CURRENTSPRITEDATA`

`      ADC  #2`

`      STA  SpriteDataPtr+1`

`      LDA  CURRENTSPRITEDATA+1`

`      ADC  #0`

`      STA  SpriteDataPtr+2`

`      LDX  XOFFSET`

`      `

`   SW_Width:`

`      LDY  HEIGHT`

`      DEY`

`   SW_Height:   `

`   SpriteDataPtr:         ; please note - self modifying code`

`      LDA  $FFFF,Y        `

`      BEQ  SW_SkipWrite`

`    ScreenAddPtr:          ; please note - self modifying code`

`      STA  $FFFF,X       ; is ->   STA  ScreenAddPtr+1,X`

`   SW_SkipWrite:`

`      `

`      DEX`

`      BPL  SW_CheckHeight`

`   SW_AtCharPos:`

`      SEC`

`      LDA  ScreenAddPtr+1`

`      SBC  #$80`

`      STA  ScreenAddPtr+1`

`      LDA  ScreenAddPtr+2`

`      SBC  #2`

`      STA  SCreenAddPtr+2`

`      `

`      LDX  #7`

`   SW_CheckHeight:`

`      DEY`

`      BPL  SW_Height`

`      DEC  WIDTH`

`      BEQ  SW_End`

`     `

`      `

`      ; move to the next column`

`      `

`      CLC`

`      LDA  SpriteDataPtr+1`

`      ADC  HEIGHT`

`      STA  SpriteDataPtr+1`

`      LDA  SpriteDataPtr+2`

`      ADC  #0`

`      STA  SpriteDataPtr+2`

`         `

`      LDA  SCREENADD`

`      CLC`

`      ADC  #8`

`      STA  SCREENADD`

`      STA  ScreenAddPtr+1`

`      LDA  SCREENADD+1`

`      ADC  #0`

`      STA  SCREENADD+1`

`      STA  ScreenAddPtr+2`

`      LDX  XOFFSET`

`      JMP  SW_Width`

`   SW_End:`

`      `

`      RTS`

`   ;-------------------------------------------------------------------------------`

`   ; SpriteNoMaskDraw - a Sprite number = referenced from SPRArray`

`   ;              The following need to be setup prior to calling this...`

`   ;              SPRITEADD, WIDTH, HEIGHT, XOFFSET, CURRENTSPRITEDATA`

`   ;-------------------------------------------------------------------------------`

`   SpriteNoMaskDraw:`

`      ; store the sprite number, x and y position`

`      STA  SPRITE`

`      STX  XPOS`

`      STY  YPOS`

`      `

`      ; now store sprite data and screen address in code`

`      LDA  SCREENADD`

`      STA  SScreenAddPtr+1`

`      LDA  SCREENADD+1`

`      STA  SScreenAddPtr+2`

`      `

`      CLC`

`      LDA  CURRENTSPRITEDATA`

`      ADC  #2`

`      STA  SSpriteDataPtr+1`

`      LDA  CURRENTSPRITEDATA+1`

`      ADC  #0`

`      STA  SSpriteDataPtr+2`

`      LDX  XOFFSET`

`      `

`   SNMW_Width:`

`      LDY  HEIGHT`

`      DEY`

`   SNMW_Height:   `

`    SSpriteDataPtr:         ; please note - self modifying code`

`     LDA  $FFFF,Y        `

`   SScreenAddPtr:          ; please note - self modifying code`

`      STA  $FFFF,X       ; is ->   STA  ScreenAddPtr+1,X`

`      DEX`

`      BPL  SNMW_CheckHeight`

`   SNMW_AtCharPos:`

`      SEC`

`      LDA  SScreenAddPtr+1`

`      SBC  #$80`

`      STA  SScreenAddPtr+1`

`      LDA  SScreenAddPtr+2`

`      SBC  #2`

`      STA  SSCreenAddPtr+2`

`      `

`      LDX  #7`

`   SNMW_CheckHeight:`

`      DEY`

`      BPL  SNMW_Height`

`      DEC  WIDTH`

`      BEQ  SNMW_End`

`     `

`      `

`      ; move to the next column`

`      `

`      CLC`

`      LDA  SSpriteDataPtr+1`

`      ADC  HEIGHT`

`      STA  SSpriteDataPtr+1`

`      LDA  SSpriteDataPtr+2`

`      ADC  #0`

`      STA  SSpriteDataPtr+2`

`         `

`      LDA  SCREENADD`

`      CLC`

`      ADC  #8`

`      STA  SCREENADD`

`      STA  SScreenAddPtr+1`

`      LDA  SCREENADD+1`

`      ADC  #0`

`      STA  SCREENADD+1`

`      STA  SScreenAddPtr+2`

`      LDX  XOFFSET`

`      JMP  SNMW_Width`

`   SNMW_End:`

`      `

`      RTS`

`   ;-------------------------------------------------------------------------------`

`   ; SpriteWipe - a Sprite number`

`   ;-------------------------------------------------------------------------------`

`   SpriteWipe:`

`      STA   SCRATCH1`

`      CLC`

`      LDA   #`<SPRArray

       ADC   SCRATCH1

       STA   TEMPPTR

       LDA   #>`SPRArray`

`      ADC   #0`

`      STA   TEMPPTR+1`

`      LDY   #SPRBLK_XOFFBACK`

`      LDA   (TEMPPTR),Y`

`      STA   XOFFSET`

`      LDY   #SPRBLK_SCRBACK`

`      LDA   (TEMPPTR),Y`

`      STA   SCREENADD`

`      INY`

`      LDA   (TEMPPTR),Y`

`      STA   SCREENADD+1`

`      LDY   #SPRBLK_WIDTH`

`      LDA   (TEMPPTR),Y`

`      STA   WIDTH`

`      INY`

`      LDA   (TEMPPTR),Y`

`      STA   HEIGHT`

`   Sprite_Blank:`

`      ; now store screen address in code`

`      LDA  SCREENADD`

`      STA  ScreenAddPtr2+1`

`      LDA  SCREENADD+1`

`      STA  ScreenAddPtr2+2`

`      `

`      LDX  XOFFSET`

`   SWipe_Width:`

`      LDY  HEIGHT`

`      DEY`

`   SWipe_Height:   `

`      LDA  #$00 `

`   ScreenAddPtr2:          ; please note - self modifying code`

`      STA  $FFFF,X         ; is ->   STA  ScreenAddPtr+1,X`

`   SWipe_SkipWrite:`

`      `

`      DEX`

`      BPL  SWipe_CheckHeight`

`   SWipe_AtCharPos:`

`      SEC`

`      LDA  ScreenAddPtr2+1`

`      SBC  #$80`

`      STA  ScreenAddPtr2+1`

`      LDA  ScreenAddPtr2+2`

`      SBC  #2`

`      STA  SCreenAddPtr2+2`

`      `

`      LDX  #7`

`   SWipe_CheckHeight:`

`      DEY`

`      BPL  SWipe_Height`

`      DEC  WIDTH`

`      BEQ  SWipe_End`

`     `

`      `

`      ; move to the next column`

`      LDA  SCREENADD`

`      CLC`

`      ADC  #8`

`      STA  SCREENADD`

`      STA  ScreenAddPtr2+1`

`      LDA  SCREENADD+1`

`      ADC  #0`

`      STA  SCREENADD+1`

`      STA  ScreenAddPtr2+2`

`      LDX  XOFFSET`

`      JMP  SWipe_Width`

`   SWipe_End:`

`      `

`      RTS`

`   ;-------------------------------------------------------------------------------`

`   ;  SpriteCalcScreenPos:`

`   ;    calculates the screen address - please note that `

`   ;    xpos($75) and ypos($76) need to be set up before.`

`   ;    This also uses $70+$71 for the screen address ( screenAdd )`

`   ;`

`   ;-------------------------------------------------------------------------------`

`   SpriteCalcScreenPos:`

`      ; reset the screen address ... `

`      LDA  #SCREENLOW`

`      STA  SCREENADD`

`      LDA  #SCREENHIGH`

`      STA  SCREENADD+1 `

`      ; now calculate the Y position in chars ( *640 ) and add`

`      ; to the screen Address`

`      LDA  YPOS`

`      AND  #$f8`

`      LSR`

`      LSR`

`      TAY`

`      CLC`

`      LDA  LookUp640, Y`

`      ADC  SCREENADD`

`      STA  SCREENADD`

`      INY`

`      LDA  LookUp640,Y `

`      ADC  SCREENADD+1`

`      STA  SCREENADD+1`

`      ; now the X multiply then addition to screen address    `

``      `MUL8ADDTOADDRESS XPOS, SCREENADD``

`      ; finally the first 3 bits of the YPos`

`      LDA  YPOS`

`      AND  #$07`

`      CLC`

`      ADC  SCREENADD`

`      STA  SCREENADD`

`      LDA  SCREENADD`

`      STA  SCREENADD_BACK`

`      LDA  SCREENADD+1`

`      STA  SCREENADD_BACK+1`

`      RTS`

`   ;-------------------------------------------------------------------------------`

`   ;`

`   ;  Sprite_SetFlag`

`   ;     A - SPrite slot * 16`

`   ;     X - bits to set...`

`   ;`

`   ;-------------------------------------------------------------------------------`

`   Sprite_SetFlag:`

`      STX  SCRATCH1`

`      CLC`

`      ADC  #SPRBLK_FLAG`

`      TAX`

`      LDA  SprArray,X`

`      ORA  SCRATCH1`

`      STA  SPrArray,X`

`    `

`      RTS`

`   ;-------------------------------------------------------------------------------`

`   ; TOTAL_SPRITE_SPACE = 8 * 15 sprites = 240 bytes     `

`   SPRArray: .byte 0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0`

`             .byte 0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0`

`             .byte 0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0`

`             .byte 0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0`

`             .byte 0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0`

`             .byte 0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0`

`             .byte 0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0`

`             .byte 0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0`

`   SPRActive:`

`             .byte $ff,$ff,$ff,$ff,$ff,$ff,$ff,$ff            ; the eight active sprites ... `

`   ;-------------------------------------------------------------------------------`

`   LookUp640:`

`      .incbin "LookUpTable640"`

`   SpriteData:`

`      .incbin "Sprites"`

`   ;-------------------------------------------------------------------------------`

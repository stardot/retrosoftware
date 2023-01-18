# Sparse Invaders - BlockDrawer.txt

Blocks are basically 8 pixel by 8 pixel graphics that are drawn to the screen. Plotting to the screen is done as with characters, in that drawing a block to 2,1 would draw it at pixel coords of 16,8. Hmm I'm sure I will be revisiting this and trying to explain it a little better.

`   ;-------------------------------------------------------------------------------`
`   ;  BlockDrawer`
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
`   ;    Draws the block to the screen - using character positioning...`
`   ;    The blocks are 8 by 8...`
`   ;-------------------------------------------------------------------------------`
`   .require "Constands"`
`   .require "Macros"`
`   ;-------------------------------------------------------------------------------`
`   ;-------------------------------------------------------------------------------`
`   ;`
`   ;`
`   ;`
`   ;-------------------------------------------------------------------------------`
`   BlockInit:`
`      `
`       RTS`

**BlockColorDraw** draws a soild coloured block to the position passed in. This is commented out, as wasn't needed with Invaders. But I've left the function here for reference.

`   ;-------------------------------------------------------------------------------`
`   ; BlockColourDraw`
`   ;             a - block colour`
`   ;             x - characters across`
`   ;             y - characters down`
`   ;`
`   ;  This is not used in Invaders, so commented out.`
`   ;`
`   ;-------------------------------------------------------------------------------`
`   ;BlockColourDraw:`
`   ;`
`   ;   ; store the sprite number, x and y position`
`   ;   STA  SCRATCH1`
`   ;   STX  XPOS`
`   ;   STY  YPOS`
`   ; `
`   ;   ; calculate the screen position...`
`   ;   LDA  #SCREENLOW`
`   ;   STA  SCREENADD`
`   ;   LDA  #SCREENHIGH`
`   ;   STA  SCREENADD+1   `
`   ;`
`   ;   ; muli x by 32 then add to screen address`
`   ;   STX  TEMPPTR`
`   ;   LDA  #0`
`   ;   STA  TEMPPTR+1  `
``    ;   `MUL32 TEMPPTR ``
``     ;  `ADD16BIT TEMPPTR,SCREENADD,SCREENADD ``
`   ;`
`   ;   TYA`
`   ;   ASL`
`   ;   TAY`
`   ;   LDA  LookUp640, Y`
`   ;   ADC  SCREENADD`
`   ;;   STA  SCREENADD`
`   ;   INY`
`   ;   LDA  LookUp640,Y `
`   ;   ADC  SCREENADD+1`
`   ;   STA  SCREENADD+1`
`   ;`
`   ;`
`   ;   ; lets do a coloured block for now...`
`   ;   LDA  SCREENADD`
`   ;   STA  BCD_ScrPtr+1`
`   ;   LDA  SCREENADD+1`
`   ;   STA  BCD_ScrPtr+2`
`   ;`
`   ;   ; the draw ...   `
`   ;`
`   ;   LDX  #4`
`   ;`
`   ;BCD_Height:`
`    ;`
`   ;   LDY  #7`
`   ;`
`   ;BCD_Draw:`
`   ;`
`   ;   LDA  SCRATCH1`
`   ;BCD_ScrPtr:`
`   ;   STA  $ffff,Y`
`   ;   DEY`
`   ;   BPL  BCD_Draw`
`   ;`
`   ;   LDA  BCD_ScrPtr+1`
`   ;   CLC`
`   ;   ADC  #8`
`   ;   STA  BCD_ScrPtr+1`
`   ;   LDA  BCD_ScrPtr+2`
`   ;   ADC  #0`
`   ;   STA  BCD_ScrPtr+2`
`   ;`
`   ;   DEX`
`   ;   BNE  BCD_Height`
`   ;   `
`   ;   RTS`

**BlockDraw** draws a block graphic to the passed in position on the screen. Block graphics include the font for the text, the score, the lifes etc. You will notice after this function the 'blocks' are incbin'ed along with the look up table to quickly calculated screen positions.

`   ;-------------------------------------------------------------------------------`
`   ; BlockDraw - a - block number`
`   ;             x - characters across`
`   ;             y - characters down`
`   ;-------------------------------------------------------------------------------`
`   BlockDraw:`
`      ; store the sprite number, x and y position`
`      STA  SCRATCH1`
`      STX  XPOS`
`      STY  YPOS`
`    `
`      ; calculate the screen position...`
`      LDA  #SCREENLOW`
`      STA  SCREENADD`
`      LDA  #SCREENHIGH`
`      STA  SCREENADD+1   `
`       ; muli x by 32 then add to screen address`
`      STX  SCREENPTR`
`      LDA  #0`
`      STA  SCREENPTR+1  `
``       `MUL32 SCREENPTR ``
``       `ADD16BIT SCREENPTR,SCREENADD,SCREENADD ``
`    `
`      TYA`
`      ASL`
`      TAY`
`      LDA  LookUp640, Y`
`      ADC  SCREENADD`
`      STA  SCREENADD`
`      INY`
`      LDA  LookUp640,Y `
`      ADC  SCREENADD+1`
`      STA  SCREENADD+1`
`      ; calculate the gfx for the block data...`
`      LDA  SCRATCH1`
`      ASL `
`      TAX`
`      CLC`
`      LDA  BlockData,X`
`      ADC  #2`
`      ADC  #`<BlockData
       STA  CURRENTSPRITEDATA
       INX
       LDA  BlockData,X
       ADC  #>`BlockData`
`      STA  CURRENTSPRITEDATA+1`
`      ; setup the screen position`
`      LDA  SCREENADD`
`      STA  BD_ScrPtr+1`
`      LDA  SCREENADD+1`
`      STA  BD_ScrPtr+2`
`      LDA  CURRENTSPRITEDATA`
`      STA  BD_GfxPtr+1`
`      LDA  CURRENTSPRITEDATA+1`
`      STA  BD_GfxPtr+2`
`      ; the draw ...   `
`      LDX  #4`
`   BD_Height:`
`      LDY  #7`
`   BD_Draw:`
`   BD_GfxPtr:`
`      LDA  $ffff,Y`
`   BD_ScrPtr:`
`      STA  $ffff,Y`
`      DEY`
`      BPL  BD_Draw`
`      LDA  BD_ScrPtr+1`
`      CLC`
`      ADC  #8`
`      STA  BD_ScrPtr+1`
`      LDA  BD_ScrPtr+2`
`      ADC  #0`
`      STA  BD_ScrPtr+2`
`      LDA  BD_GfxPtr+1`
`      CLC`
`      ADC  #8`
`      STA  BD_GfxPtr+1`
`      LDA  BD_GfxPtr+2`
`      ADC  #0`
`      STA  BD_GfxPtr+2`
`      DEX`
`      BNE  BD_Height`
`      `
`      RTS`
`   ;-------------------------------------------------------------------------------`
`   BlockData:`
`      .incbin "Blocks"`
`   LookUp640:`
`      .incbin "LookUpTable640"`
`   ;-------------------------------------------------------------------------------`
`   ;  End of BlockDrawer`
`   ;-------------------------------------------------------------------------------`

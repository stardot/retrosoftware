## Sparse Invaders Source - Invader\_Bases.txt

`   ;-------------------------------------------------------------------------------`
`   ;  Invader_Bases`
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
`   ;    Controls the bases, setup, drawing and removal plus collison.`
`   ;`
`   ;-------------------------------------------------------------------------------`
`   `
`   .require "Constands"`
`   .require "Macros"`
`   `
`   ;-------------------------------------------------------------------------------`
`   `
`   .alias   BLOCKS_BOTH  36            ; block number for drawing`
`   .alias   BLOCKS_LEFT  37        ; ...`
`   .alias   BLOCKS_RIGHT 38            ; ...`
`   .alias   BLOCKS_BLANK 40        ; ... `
`   `
`   .alias   BASE_Y       22            ; block line for top of base`
`   .alias   BASE_Y2      23            ; block line for mid section of base`
`   .alias   BASE_Y3      24            ; block line for bottom f base`
`   .alias   BASE1_X      4             ; block x start for base 1`
`   .alias   BASE2_X      9             ; block x start for base 2`
`   .alias   BASE3_X      14            ; block x start for base 3`
`   `
`   .alias   PIXELS_BASE_Y1START 22*8   ; pixel start for Y position of top row`
`   .alias   PIXELS_BASE_Y2START 23*8   ; pixel start for Y position of mid row`
`   .alias   PIXELS_BASE_Y3START 24*8   ; pixel start for Y position of bottom row`
`   `
`   .alias   PIXELS_BASE1_XSTART 32     ; pixel start for X position for base one`
`   .alias   PIXELS_BASE1_XEND   56     ; pixel end for X position for base one`
`   .alias   PIXELS_BASE2_XSTART 72     ; pixel start for X position for base two`
`   .alias   PIXELS_BASE2_XEND   96     ; pixel end for X position for base two`
`   .alias   PIXELS_BASE3_XSTART 112    ; pixel start for X position for base three`
`   .alias   PIXELS_BASE3_XEND   136    ; pixel end for X position for base three`
`   `
`   ; masking for the block sections ...`
`   .alias   BLOCKRIGHT_MASK     $03    ; bit mask for both segments for the right block`
`   .alias   BLOCKRIGHT_BOTH     $03    ; bit value for both segments for the right block`
`   .alias   BLOCKRIGHT_LEFT     $02    ; bit value for left segment for the right block`
`   .alias   BLOCKRIGHT_RIGHT    $01    ; bit value for right segment for the right block`
`   .alias   BLOCKMID_MASK       $0c    ; bit mask for both segments for the mid block`
`   .alias   BLOCKMID_BOTH       $0c    ; bit value for both segments for the mid block`
`   .alias   BLOCKMID_LEFT       $08    ; bit value for left segment for the mid block`
`   .alias   BLOCKMID_RIGHT      $04    ; bit value for right segment for the mid block`
`   .alias   BLOCKLEFT_MASK      $30    ; bit mask for both segments for the left block`
`   .alias   BLOCKLEFT_BOTH      $30    ; bit value for both segments for the left block`
`   .alias   BLOCKLEFT_LEFT      $20    ; bit value for left segment for the left block`
`   .alias   BLOCKLEFT_RIGHT     $10    ; bit value for right segment for the left block`
`   `
`   `
`   ;-------------------------------------------------------------------------------`
`   ; Init:`
`   ;   initializes the bases`
`   ;-------------------------------------------------------------------------------`
`   Init:`
`   `
`     ; sort out the bit mask for the blocks`
`     LDA  #$3f`
`     STA  BASE1_1`
`     STA  BASE2_1`
`     STA  BASE3_1`
`     STA  BASE1_2`
`     STA  BASE2_2`
`     STA  BASE3_2`
`     STA  BASE1_3`
`     STA  BASE2_3`
`     STA  BASE3_3`
`   `
`     ; clear the flag for clearing  the base lines if the invaders reach that pos`
`     LDA  #0`
`     STA  BASELINEFLAG`
`   `
`     RTS`
`   `
`   `
`   ;-------------------------------------------------------------------------------`
`   `
`   `
`   ;-------------------------------------------------------------------------------`
`   ; CheckCollison:`
`   ;    Checks the collison, retruns Carry clear if no collisons...`
`   ;    This checks the collision with the three bases. It's a little long winded`
`   ;    as I decided, for better or worse, to use bit masks for the shootable blocks`
`   ;    within the bases.`
`   ;    X - x position`
`   ;    y - y position`
`   ;-------------------------------------------------------------------------------`
`   CheckCollison:`
`   `
`     ; firstly, do the Y check, as easy ... `
`     TYA`
`     LSR`
`     LSR`
`     LSR`
`     STA  STOREY`
`     CMP  #BASE_Y`
`     BMI  CC_end `
`     CMP  #BASE_Y3+1`
`     BPL  CC_end`
`   `
`     ; now the x positions... `
`     LDA  #0`
`     STA  SCRATCH1`
`     TXA`
`     ASL`
`     STA  SCRATCH4`
`     STA  STOREX`
`     CMP  #PIXELS_BASE1_XSTART`
`     BMI  CC_end `
`     CMP  #PIXELS_BASE1_XEND`
`     BMI  CC_gotya1`
`     INC  SCRATCH1`
`     CMP  #PIXELS_BASE2_XSTART`
`     BMI  CC_end `
`     CMP  #PIXELS_BASE2_XEND`
`     BMI  CC_gotya2`
`     INC  SCRATCH1`
`     CMP  #PIXELS_BASE3_XSTART`
`     BMI  CC_end `
`     CMP  #PIXELS_BASE3_XEND`
`     BMI  CC_gotya3`
`   `
`   CC_end:    `
`   `
`     CLC`
`     RTS`
`   `
`   CC_gotya1:`
`   `
`   ;  ok got a collison with a block base 1 ...`
`   `
`     LDA  STOREX`
`     SEC`
`     SBC  #PIXELS_BASE1_XSTART`
`     LSR`
`     LSR`
`     TAX`
`     LSR`
`     STA  STOREX`
`     JMP  CC_cont`
`   `
`   CC_gotya2:`
`   `
`   ;  ok got a collison with a block base 2 ...`
`   `
`     LDA  STOREX`
`     SEC`
`     SBC  #PIXELS_BASE2_XSTART`
`     LSR`
`     LSR`
`     TAX`
`     LSR`
`     STA  STOREX`
`     JMP  CC_cont`
`   `
`   CC_gotya3:`
`   `
`   ;  ok got a collison with a block base 3 ...`
`   `
`     LDA  STOREX`
`     SEC`
`     SBC  #PIXELS_BASE3_XSTART`
`     LSR`
`     LSR`
`     TAX`
`     LSR`
`     STA  STOREX`
`    `
`   CC_cont:`
`    `
`     ; calculate the position / segment within the block that has collided`
`     LDA  STOREY              `
`     SEC`
`     SBC  #BASE_Y`
`     STA  STOREY`
`     `
`     LDA  SCRATCH1`
``      `MUL3 TEMP ``
`     CLC`
`     ADC  STOREY`
`     CLC`
`     ADC  #BASE1_1`
`     STA  USERPTR`
`     LDA  #0`
`     STA  USERPTR+1`
`   `
`     ; create mask for the segment within the byte ( note six segments per row )`
`     LDA  #$DF                   ;  11011111`
`     CPX  #0`
`     BEQ  CC_sortmask`
`     ROR                         ;  11101111`
`     DEX`
`     BEQ  CC_sortmask`
`     ROR                         ;  11110111`
`     DEX`
`     BEQ  CC_sortmask`
`     ROR                         ;  11111011`
`     DEX`
`     BEQ  CC_sortmask`
`     ROR                         ;  11111101`
`     DEX`
`     BEQ  CC_sortmask`
`     ROR                         ;  11111110`
`   `
`   CC_sortmask:`
`   `
`     ;  scratch1 - block number   `
`     ;  scratch2 - block mask position (starting at Base1_1 )`
`     ;  scratch3 - bit to lose in collison`
`   `
`     STA  SCRATCH3`
`     EOR  #255`
`     STA  SCRATCH4`
`   `
`     ; better check and if removed, don't draw ... This is not optinal as check at end of function`
`     LDX  #0`
`     LDA  (USERPTR,X)`
`     AND  SCRATCH4`
`     BEQ  CC_alreadygot`
`   `
`     ; store the new bit mask ...`
`     LDA  (USERPTR,X)`
`     AND  SCRATCH3`
`     STA  (USERPTR,X) `
`    `
`     ; redraw the block .... note it's BLANK, LEFT, RIGHT, BOTH`
`     LDA  SCRATCH1`
`     LDX  STOREX`
`     LDY  STOREY`
`   `
`     JSR  RedrawBlock`
`   `
`     ; collision - so set carry before return...`
`     SEC`
`     RTS`
`   `
`   CC_alreadygot:`
`   `
`     ; no collision so clear carry ...`
`     CLC`
`     RTS`
`     `
`   `
`   `
`   `
`   ;-------------------------------------------------------------------------------`
`   ;  RedrawBlock`
`   ;     A - Block number`
`   ;     X - Block x - i.e  0,1 or 2`
`   ;     y - Block y position - i.e  0,1 or 2`
`   ;-------------------------------------------------------------------------------`
`   RedrawBlock:`
`   `
`     ; store the information passed in ...  `
`     STA  STOREA`
`     STX  STOREX`
`     STY  STOREY`
`   `
`     ; calculate line for block details ...`
``      `MUL3 TEMP ``
`     CLC`
`     ADC  #BASE1_1  `
`     CLC`
`     ADC  STOREY`
`     STA  USERPTR`
`     LDX  #0`
`     STX  USERPTR+1`
`     LDA  (USERPTR,X)`
`     STA  SCRATCH1`
`     `
`     ; store the block line address`
`     LDA  STOREX`
`     BEQ  RW_CALCL`
`     CMP  #1`
`     BEQ  RW_CALCM`
`   `
`   RW_CALCR:`
`   `
`     LDA  SCRATCH1`
`     LDX  #BLOCKS_BLANK `
`     AND  #BLOCKRIGHT_MASK`
`     BEQ  RW_DrawBlock`
`     LDX  #BLOCKS_BOTH `
`     CMP  #BLOCKRIGHT_BOTH`
`     BEQ  RW_DrawBlock`
`     LDX  #BLOCKS_LEFT `
`     CMP  #BLOCKRIGHT_LEFT`
`     BEQ  RW_DrawBlock`
`     LDX  #BLOCKS_RIGHT `
`     JMP  RW_DrawBlock`
`     `
`   RW_CALCM:`
`   `
`     LDA  SCRATCH1`
`     LDX  #BLOCKS_BLANK `
`     AND  #BLOCKMID_MASK`
`     BEQ  RW_DrawBlock`
`     LDX  #BLOCKS_BOTH `
`     CMP  #BLOCKMID_BOTH`
`     BEQ  RW_DrawBlock`
`     LDX  #BLOCKS_LEFT `
`     CMP  #BLOCKMID_LEFT`
`     BEQ  RW_DrawBlock`
`     LDX  #BLOCKS_RIGHT `
`     JMP  RW_DrawBlock`
`     `
`   RW_CALCL:`
`   `
`     LDA  SCRATCH1`
`     LDX  #BLOCKS_BLANK `
`     AND  #BLOCKLEFT_MASK`
`     BEQ  RW_DrawBlock`
`     LDX  #BLOCKS_BOTH `
`     CMP  #BLOCKLEFT_BOTH`
`     BEQ  RW_DrawBlock`
`     LDX  #BLOCKS_LEFT `
`     CMP  #BLOCKLEFT_LEFT`
`     BEQ  RW_DrawBlock`
`     LDX  #BLOCKS_RIGHT `
`   `
`   RW_DrawBlock:`
`   `
`     STX  SCRATCH1`
`   `
`     LDA  STOREY`
`     CLC`
`     ADC  #BASE_Y`
`     TAY`
`   `
`     INC  STOREA`
`     LDA  STOREA`
``      `MUL5 TEMP ``
`     SEC`
`     SBC  #1  `
`     CLC`
`     ADC  STOREX`
`     TAX`
`   `
`     LDA  SCRATCH1  ; block    `
`   `
`     JMP  BlockDrawer.BlockDraw    `
`   `
`   `
`   ;-------------------------------------------------------------------------------`
`   ;  BlankLine`
`   ;    draws the base, y block coords for the line to remove...`
`   ;    Note - this was written for when the ivaders reach the y position just`
`   ;    before the row in question. This row is then completey removed...`
`   ;-------------------------------------------------------------------------------`
`   BlankLine:`
`   `
`     ; better blank the mask...`
`     TYA`
`     CMP  #BASE_Y`
`     BNE  BL_try2`
`   `
`     LDA  BASELINEFLAG`
`     AND  #$01`
`     BNE  BL_end `
`     ORA  #$01`
`     STA  BASELINEFLAG`
`     `
`     LDA  #0`
`     STA  BASE1_1  `
`     STA  BASE2_1  `
`     STA  BASE3_1  `
`     JMP  BL_Hmm`
`     `
`   BL_try2:`
`     CMP  #BASE_Y2`
`     BNE  BL_try3`
`   `
`     LDA  BASELINEFLAG`
`     AND  #$02`
`     BNE  BL_end `
`     ORA  #$02`
`     STA  BASELINEFLAG`
`   `
`     LDA  #0`
`     STA  BASE1_2  `
`     STA  BASE2_2  `
`     STA  BASE3_2  `
`     JMP  BL_Hmm`
`   `
`   `
`   BL_try3:`
`     CMP  #BASE_Y3`
`     BEQ  BL_do3`
`   `
`   BL_end:`
`    `
`     RTS`
`     `
`   BL_do3:`
`   `
`     LDA  BASELINEFLAG`
`     AND  #$04`
`     BNE  BL_end `
`     ORA  #$04`
`     STA  BASELINEFLAG`
`   `
`     LDA  #0`
`     STA  BASE1_3  `
`     STA  BASE2_3  `
`     STA  BASE3_3  `
`   `
`   BL_Hmm:`
`   `
`     ; blank the whole line, even if already partially blanked...`
`     LDX  #BASE1_x`
`     STX  XPOS`
`     STY  YPOS`
`     `
`     LDA  #40`
`     JSR  BlockDrawer.BlockDraw`
`     INC  XPOS`
`     LDA  #40`
`     LDX  XPOS`
`     LDY  YPOS`
`     JSR  BlockDrawer.BlockDraw`
`     INC  XPOS`
`     LDA  #40`
`     LDX  XPOS`
`     LDY  YPOS`
`     JSR  BlockDrawer.BlockDraw`
`     `
`     LDX  #BASE2_X`
`     STX  XPOS`
`     LDA  #40`
`     LDY  YPOS`
`     JSR  BlockDrawer.BlockDraw`
`     INC  XPOS`
`     LDA  #40`
`     LDX  XPOS`
`     LDY  YPOS`
`     JSR  BlockDrawer.BlockDraw`
`     INC  XPOS`
`     LDA  #40`
`     LDX  XPOS`
`     LDY  YPOS`
`     JSR  BlockDrawer.BlockDraw`
`   `
`     LDX  #BASE3_X`
`     STX  XPOS`
`     LDA  #40`
`     LDY  YPOS`
`     JSR  BlockDrawer.BlockDraw`
`     INC  XPOS`
`     LDA  #40`
`     LDX  XPOS`
`     LDY  YPOS`
`     JSR  BlockDrawer.BlockDraw`
`     INC  XPOS`
`     LDA  #40`
`     LDX  XPOS`
`     LDY  YPOS`
`     JMP  BlockDrawer.BlockDraw`
`   `
`   `
`   `
`   `
`   ;-------------------------------------------------------------------------------`
`   ;  DrawBases`
`   ;    draws the bases...`
`   ;-------------------------------------------------------------------------------`
`   DrawBases:`
`   `
`     LDX  #BASE1_x`
`     LDY  #BASE_Y`
`     JSR  DrawBase`
`     LDX  #BASE2_x`
`     LDY  #BASE_Y`
`     JSR  DrawBase`
`     LDX  #BASE3_x`
`     LDY  #BASE_Y`
`     JMP  DrawBase`
`   `
`   ;-------------------------------------------------------------------------------`
`   ;  DrawBase`
`   ;    draws the base, x,y block coords for top left of base...`
`   ;-------------------------------------------------------------------------------`
`   DrawBase:`
`   `
`      STX  XPOS`
`      STY  YPOS`
`      LDA  #BLOCKS_BOTH`
`      JSR  BlockDrawer.BlockDraw   `
`      INC  XPOS`
`      LDA  #BLOCKS_BOTH`
`      LDX  XPOS`
`      LDY  YPOS`
`      JSR  BlockDrawer.BlockDraw   `
`      INC  XPOS`
`      LDA  #BLOCKS_BOTH`
`      LDX  XPOS`
`      LDY  YPOS`
`      JSR  BlockDrawer.BlockDraw   `
`      DEC  XPOS`
`      DEC  XPOS`
`      INC  YPOS`
`      `
`      `
`      LDA  #BLOCKS_BOTH`
`      LDX  XPOS`
`      LDY  YPOS`
`      JSR  BlockDrawer.BlockDraw   `
`      INC  XPOS`
`      LDA  #BLOCKS_BOTH`
`      LDX  XPOS`
`      LDY  YPOS`
`      JSR  BlockDrawer.BlockDraw   `
`      INC  XPOS`
`      LDA  #BLOCKS_BOTH`
`      LDX  XPOS`
`      LDY  YPOS`
`      JSR  BlockDrawer.BlockDraw   `
`      DEC  XPOS`
`      DEC  XPOS`
`      INC  YPOS`
`      `
`      LDA  #BLOCKS_BOTH`
`      LDX  XPOS`
`      LDY  YPOS`
`      JSR  BlockDrawer.BlockDraw   `
`      INC  XPOS`
`      LDA  #BLOCKS_BOTH`
`      LDX  XPOS`
`      LDY  YPOS`
`      JSR  BlockDrawer.BlockDraw   `
`      INC  XPOS`
`      LDA  #BLOCKS_BOTH`
`      LDX  XPOS`
`      LDY  YPOS`
`      JSR  BlockDrawer.BlockDraw   `
`   `
`      RTS`
`      `
`   ;-------------------------------------------------------------------------------`

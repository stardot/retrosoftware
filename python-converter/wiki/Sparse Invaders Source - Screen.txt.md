# Sparse Invaders Source - Screen.txt

Screen Functionality. This includes displaying on screen messages, score and clearing the screen. This file also contains support functionality for handling the score etc.

the score is processed simply as you will notice once seeing the code, it's handled numbers up to 9999 which is more then enough for invaders.

`   ;-------------------------------------------------------------------------------`

`   ;  ScreenFunctionality`

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

`   ;`

`   ;-------------------------------------------------------------------------------`

`   .require "Constands"`

`   .require "Macros"`

`   ;-------------------------------------------------------------------------------`

`   ;-------------------------------------------------------------------------------`

SCREEN_UPDATE_COUNT - this is the delay before update the score.

`   .alias SCREEN_UPDATE_COUNT 5`

**UpdateScreen** updates the game on screen items like number of lives left and score. Please note the use of the SCREEN_UPDATE, this means that screen information is only updated every 5 game frames. This reduces unwanted drawing every frame, as the area of screen where this is drawn isn't drawn over. This could be a little smarter - and just be flagged when needed to be updated. However as killing an invader increases the score, this function would generally be called as much as it is.

`   ;-------------------------------------------------------------------------------`

`   ; UpdateScreen - `

`   ;     Invaders screen update, score etc`

`   ;`

`   ;-------------------------------------------------------------------------------`

`   UpdateScreen:`

`      ; check to see if update to screen needed...`

`      LDA   SCREEN_UPDATE`

`      BEQ   US_Update  `

`      RTS`

`      `

`   US_Update:`

`      ; update the player lifes `

`      LDA   PLAYER_LIFES`

`      STA   SCRATCH3`

`      LDA   #39`

`      LDX   #1`

`      STX   SCRATCH4`

`   US_Lives:`

`      LDA   #39`

`      LDX   SCRATCH4`

`      LDY   #29`

`      jsr   BLockDrawer.BlockDraw`

`      INC   SCRATCH4`

`      `

`      DEC   SCRATCH3`

`      BNE   US_Lives`

`   US_ClearRest:`

`      LDA   #40`

`      LDX   SCRATCH4`

`      LDY   #29`

`      jsr   BLockDrawer.BlockDraw`

`      INC   SCRATCH4`

`      LDA   SCRATCH4`

`      CMP   #11   `

`      BNE   US_ClearRest`

`      ; reset count, this means screen update every 5 frames`

`      LDA   #SCREEN_UPDATE_COUNT`

`      STA   SCREEN_UPDATE`

`      ; check to see score addition needed...`

`      LDA   SCORE_ADDITION`

`      BEQ   US_End`

`      ; dec the score and then update the values ...`

`      DEC   SCORE_ADDITION`

`      `

`      ; use X for clearer...`

`      LDX   #0      `

`      ; inc the units, if less then 10, then update units only`

`      INC   ScreenScore+3`

`      LDA   ScreenScore+3`

`      CMP   #10`

`      BCC   US_D000X `

`      STX   ScreenScore+3`

`      ; inc the tens, if less then 10, then update tens and units only`

`      INC   ScreenScore+2`

`      LDA   ScreenScore+2`

`      CMP   #10`

`      BCC   US_D00X0 `

`      STX   ScreenScore+2`

`      ; inc the hundreads, if less then 10, then update hundreds tens and units only`

`      INC   ScreenScore+1`

`      LDA   ScreenScore+1`

`      CMP   #10`

`      BCC   US_D0X00 `

`      STX   ScreenScore+1`

`      ; inc the thousands, then update all values`

`      INC   ScreenScore`

`      LDA   ScreenScore`

`      CMP   #10`

`      BCC   US_DX000 `

`      ; score wrap around - `

`      STX   ScreenScore`

`      `

`   US_DX000:                     ; update the thousands`

`      LDA  ScreenScore`

`      LDX  #15`

`      LDY  #29`

`      jsr  BLockDrawer.BlockDraw`

`      `

`   US_D0X00:                     ; update the hundreds`

`      LDA  ScreenScore+1`

`      LDX  #16`

`      LDY  #29`

`      jsr  BLockDrawer.BlockDraw`

`      `

`   US_D00X0:                     ; update the tens`

`      LDA  ScreenScore+2`

`      LDX  #17`

`      LDY  #29`

`      jsr  BLockDrawer.BlockDraw`

`      `

`   US_D000X:                     ; update the units`

`      LDA  ScreenScore+3`

`      LDX  #18`

`      LDY  #29`

`      jsr  BLockDrawer.BlockDraw`

`      `

`   US_End:`

`      RTS`

**AdjustScore** updates the score using SCORE_ADDITION. Any score achived would be added to this value - and the score would increment accordingly. The speed of the increment is fast enough as to keep up with the scores achived within Invaders.

`   ;-------------------------------------------------------------------------------`

`   ; AdjustScore  - `

`   ;     Updates the score value only...`

`   ;-------------------------------------------------------------------------------`

`   AdjustScore:`

`      ; check to see score addition needed...`

`      LDA   SCORE_ADDITION`

`      BEQ   US_End`

`      ; dec the score and then update the values ...`

`      DEC   SCORE_ADDITION`

`      `

`      ; use X for clearer...`

`      LDX   #0      `

`      ; inc the units, if less then 10, then update units only`

`      INC   ScreenScore+3`

`      LDA   ScreenScore+3`

`      CMP   #10`

`      BCC   AS_end `

`      STX   ScreenScore+3`

`      ; inc the tens, if less then 10, then update tens and units only`

`      INC   ScreenScore+2`

`      LDA   ScreenScore+2`

`      CMP   #10`

`      BCC   AS_end `

`      STX   ScreenScore+2`

`      ; inc the hundreads, if less then 10, then update hundreds tens and units only`

`      INC   ScreenScore+1`

`      LDA   ScreenScore+1`

`      CMP   #10`

`      BCC   AS_end `

`      STX   ScreenScore+1`

`      ; inc the thousands, then update all values`

`      INC   ScreenScore`

`      LDA   ScreenScore`

`      CMP   #10`

`      BCC   AS_end `

`      ; score wrap around - `

`      STX   ScreenScore`

`      `

`   AS_end:`

`      RTS`

`       `

**DrawScore** jumps into the score drawing functionality.

`   ;-------------------------------------------------------------------------------`

`   ; DrawScore - `

`   ;     Updates the score on the screen...`

`   ;`

`   ;-------------------------------------------------------------------------------`

`   DrawScore:`

`      JMP  US_DX000  ; i'M SURE this label makes sence, just give me a moment ... ;-)`

`   ;-------------------------------------------------------------------------------`

**ClearScore** clears the stored values.

`   ClearScore:`

` `

`      LDA #0`

`      STA ScreenScore`

`      STA ScreenScore+1`

`      STA ScreenScore+2`

`      STA ScreenScore+3`

`      RTS   `

`   ScreenScore:`

`      .byte 0,0,0,0`

**Screen_CopyScoreToString** converts the score into ascii and stores in the string (USERPTR points to this)

`   ;-------------------------------------------------------------------------------`

`   ; Screen_CopyScoreToString:`

`   ;   USERPTR - points to string`

`   ;-------------------------------------------------------------------------------`

`   Screen_CopyScoreToString:`

`      LDY  #0`

`      LDA  ScreenScore`

`      CLC`

`      ADC  #48`

`      STA  (USERPTR),Y`

`      INY`

`      LDA  ScreenScore+1`

`      CLC`

`      ADC  #48`

`      STA  (USERPTR),Y`

`      INY`

`      LDA  ScreenScore+2`

`      CLC`

`      ADC  #48`

`      STA  (USERPTR),Y`

`      INY`

`      LDA  ScreenScore+3`

`      CLC`

`      ADC  #48`

`      STA  (USERPTR),Y`

`      RTS   `

**Screen_PositionedMessage** displays the string onto the screen. The first two bytes are screen position then follows the NULL terminated string.

`   ;-------------------------------------------------------------------------------`

`   ; Screen_PositionedMessage:`

`   ;     displays message, using blocks`

`   ;     No gramma please in string - and only lowercase and numbers!`

`   ;     USERPTR - string to display... first two chars position...`

`   ;-------------------------------------------------------------------------------`

`   Screen_PositionedMessage:`

`      LDY  #0`

`      LDA  (USERPTR),Y`

`      STA  SCRATCH2`

`      INY`

`      LDA  (USERPTR),Y`

`      INY`

`      STA  SCRATCH3`

`      JMP  SM_Loop   `

`   ;-------------------------------------------------------------------------------`

`   ; Screen_Message - `

`   ;     displays message, using blocks (starting at 10)`

`   ;     zero terminated.`

`   ;     No gramma please in string - and only lowercase!`

`   ;     USERPTR - string to display...`

`   ;     x - xpos in 8x8 blocks`

`   ;     y - ypos in 8x8 blocks`

`   ;-------------------------------------------------------------------------------`

`   Screen_Message:`

`      STX  SCRATCH2`

`      STY  SCRATCH3`

`      LDY  #0`

`       `

`   SM_loop:`

`      LDA  (USERPTR),Y`

`      BEQ  SM_end`

`      CMP  #32    ; space value ...`

`      BNE  SM_checknum`

`      ; DRAW SPACE ...`

`      STY  SCRATCH4`

`      LDA  #40`

`      LDX  SCRATCH2`

`      LDY  SCRATCH3`

`      JSR  BlockDrawer.BlockDraw`

`      LDY  SCRATCH4`

`      JMP  SM_next`

`   SM_checknum:`

`      CMP  #96`

`      BCS  SM_char `

`      SEC`

`      SBC  #48`

`      JMP  SM_draw   `

` `

`   SM_char:`

`       `

`      SEC`

`      SBC  #97-10   ; lower 'a' then plus the numbers`

`   SM_draw:`

`       `

`      STY  SCRATCH4`

`      LDX  SCRATCH2`

`      LDY  SCRATCH3`

`      JSR  BlockDrawer.BlockDraw`

`      LDY  SCRATCH4 `

` `

`   SM_Next:`

` `

`      INC  SCRATCH2`

`      INY`

`      JMP  SM_Loop`

` `

`   SM_end:`

` `

`      RTS`

**Screen_Clear** clears the full screen, setting it to colour ZERO (black in game)

`   ;-------------------------------------------------------------------------------`

`   ; Screen_Clear - `

`   ;     clears the screen to colour zero`

`   ;`

`   ;-------------------------------------------------------------------------------`

`   Screen_Clear:`

` `

`      LDA  #SCREENLOW`

`      STA  ScreenClearAddPtr+1`

`      LDA  #SCREENHIGH`

`      STA  ScreenClearAddPtr+2`

` `

`   SC_Reset:`

` `

`      LDA  #0`

` `

`   SC_Loop:`

`   ScreenClearAddPtr:`

`      STA  $FFFF`

` `

`      INC  ScreenClearAddPtr+1`

`      BNE  SC_Loop`

`      LDA  ScreenClearAddPtr+2`

`      CLC`

`      ADC  #1`

`      STA  ScreenClearAddPtr+2`

`      CMP  #$80`

`      BNE  SC_Reset`

` `

`      RTS`

`  `

` `

`   ;-------------------------------------------------------------------------------`

`   ; End of ScreenFunctionality`

`   ;-------------------------------------------------------------------------------`

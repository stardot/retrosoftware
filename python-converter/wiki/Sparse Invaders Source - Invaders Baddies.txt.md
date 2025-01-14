## Sparse Invaders Source - Invaders_Baddies.txt

`   ;-------------------------------------------------------------------------------    ;`

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

`   ;-------------------------------------------------------------------------------`

`   `

`   .require "Constands"`

`   .require "Macros"`

`   `

`   ;-------------------------------------------------------------------------------`

`   `

`   .alias  FRAME_UPDATESTARTDELAY   25`

`   .alias  MOTHER_DELAYMOVE         2`

`   `

`   .alias  MOTHER_STATE_INACTIVE    0`

`   .alias  MOTHER_STATE_MOVE        1`

`   .alias  MOTHER_STATE_END         2`

`   .alias  MOTHER_STATE_SHOT        3`

`   `

`   ;-------------------------------------------------------------------------------`

`   `

`   ;-------------------------------------------------------------------------------`

`   ;  BaddiesNewGame:`

`   ;    initializes at the start of game...`

`   ;-------------------------------------------------------------------------------`

`   BaddiesNewGame:`

`   `

`      LDA  #40`

`      STA  BadStartHeight`

`      LDA  #FRAME_UPDATESTARTDELAY  `

`      STA  INVADER_RESTARTDELAY`

`   `

`      JSR  ScreenFunctionality.ClearScore`

`      `

`      ; setup graphic details for sprite 1`

`      LDA  #2`

`      JSR  SpriteController.SpriteRetreiveDetails`

`      STA  BadGfxWidth`

`      STX  BadGfxHeight   `

`      LDA  CURRENTSPRITEDATA`

`      STA  BadGfx1`

`      STA  BadGfx3`

`      LDA  CURRENTSPRITEDATA+1`

`      STA  BadGfx1+1`

`      STA  BadGfx3+1`

`   `

`      ; setup graphic details for sprite 2`

`      LDA  #3`

`      JSR  SpriteController.SpriteRetreiveDetails`

`      LDA  CURRENTSPRITEDATA`

`      STA  BadGfx2`

`      LDA  CURRENTSPRITEDATA+1`

`      STA  BadGfx2+1`

`   `

`      ; setup graphic details for mother ship`

`      LDA  #4`

`      STA  BadMotherGfxNum`

`      JSR  SpriteController.SpriteRetreiveDetails`

`      LDA  CURRENTSPRITEDATA`

`      STA  BadMotherGfx`

`      LDA  CURRENTSPRITEDATA+1`

`      STA  BadMotherGfx+1`

`    `

`      ; setup the details for the mother ship...`

`   `

`      LDA  #MOTHER_STATE_INACTIVE`

`      STA  BadMotherState`

`      LDA  #$ff`

`      STA  BadMotherCount`

`      LDA  #2`

`      STA  BadMotherXPos`

`   `

`   `

`   `

`      ; setup the bullet system for the invaders`

`      JMP  Invader_Bullets.Init`

`   `

`   `

`        `

`   ;-------------------------------------------------------------------------------`

`   ;  BaddiesInit:`

`   ;    initializes the baddies at the start of the level and game...`

`   ;-------------------------------------------------------------------------------`

`   BaddiesInit:`

`   `

`      LDA  #24`

`      STA  TOTAL_INVADERS`

`   `

`      ; setup the details for positioning of the baddies...`

`      LDA  #3`

`      STA  XPOS`

`      STA  BadXPos`

`      LDA  BadStartHeight`

`      STA  YPOS`

`      STA  BadYPos`

`   `

`   BI_reposition:`

`   `

`      LDX  #0      ; first sprite ...`

`      LDY  #2      ; starting frame ...`

`      LDA  #6  ; TEst was 6`

`      STA  SCRATCH1`

`      LDA  #4  ; TEST was 4`

`      STA  SCRATCH2`

`   `

`   BI_SetupBaddies:   `

`   `

`      LDA  BadXPos`

`      STA  XPOS`

`      LDA  BadYPos`

`      STA  YPOS`

`   `

`      ; adjust Y pos to bottom of sprite,`

`      LDA  BadGfxHeight`

`      CLC`

`      ADC  YPOS`

`      SEC`

`      SBC  #1`

`      STA  YPOS`

`   `

`      ; adjust the YPOS to character based and store the offset in x for indexing`

`      AND  #$07`

`      STA  XOFFSET`

`      LDA  YPOS`

`      AND  #$f8`

`      STA  YPOS`

`   `

`      TXA`

`      PHA`

`      TYA`

`      PHA`

`      JSR  SpriteController.SpriteCalcScreenPos`

`      PLA`

`      TAY`

`      PLA`

`      TAX`

`   `

`      ;store all the details...`

`      LDA  SCREENADD`

`      STA  BaddieData,X`

`      INX`

`      LDA  SCREENADD+1`

`      STA  BaddieData,X`

`      INX`

`      LDA  XOFFSET`

`      STA  BaddieData,X   `

`      INX`

`      LDA  BadXPos`

`      STA  BaddieData,X`

`      INX`

`      LDA  BadYPos`

`      STA  BaddieData,X`

`      INX`

`      LDA  #INV_STATE_ACTIVE`

`      STA  BaddieData,X`

`      INX`

`   `

`   `

`   `

`      ; calc the new baddies position...`

`      LDA  BadXPos`

`      CLC`

`      ADC  #6`

`      STA  BadXPos`

`   `

`      DEC  SCRATCH1`

`      BNE  BI_SetupBaddies`

`   `

`   `

`      LDA  #3`

`      STA  BadXPos`

`      LDA  BadYPos`

`      CLC`

`      ADC  #12`

`      STA  BadYPos`

`      LDA  #6`

`      STA  SCRATCH1`

`      `

`      DEC  SCRATCH2`

`      BNE  BI_SetupBaddies`

`   `

`      LDA  #1`

`      STA  INV_MOVDIR`

`      LDA  #INV_MODE_STARTUP`

`      STA  BadMode`

`   `

`      ; speed the bullet rate up on `

`      LDA  #150`

`      STA  BULLET_DELAY`

`   `

`      LDA  BULLET_REFRESHDELAY`

`      SEC`

`      SBC  #10`

`      CMP  #10`

`      BPL  BI_Cont`

`      LDA  #10`

`   `

`   BI_cont:`

`   `

`      STA  BULLET_REFRESHDELAY`

`   `

`      ; finally sort out the frame delay ...`

`      LDA  INVADER_RESTARTDELAY`

`      STA  INV_DELAYCOUNT`

`      STA  INV_DELAYUPDATE`

`   `

`   `

`      jsr  Invader_Bases.Init`

`   `

`      RTS`

`      `

`   `

`      `

`   ;-------------------------------------------------------------------------------`

`   ;  BaddiesDraw:`

`   ;    draws all the invaders to screen at start of level...`

`   ;-------------------------------------------------------------------------------`

`   BaddiesDraw:`

`   `

`      LDY  #24`

`      LDX  #0`

`   `

`   DB_DrawInvaders:`

`   `

`      TYA`

`      PHA`

`      `

`      TXA`

`      CLC`

`      ADC  #5`

`      TAY`

`      `

`      LDA  BaddieData,Y`

`      CMP  #INV_STATE_ACTIVE`

`      BEQ  DB_draw`

`      CMP  #INV_STATE_DEAD`

`      BEQ  DB_SkipRemove`

`   `

`      LDA  #INV_STATE_DEAD`

`      STA  BaddieData,Y`

`      `

`      TXA`

`      PHA`

`      JSR  Baddies_RemoveInvader`

`      PLA`

`      TAX`

`   `

`   DB_skipRemove:   `

`      `

`      TXA`

`      CLC`

`      ADC  #6`

`      TAX`

`      JMP  DB_SkipDraw`

`   `

`   DB_draw:   `

`   `

`      TAY`

`      `

`      LDA  BaddieData,X`

`      STA  SCREENADD`

`      INX   `

`      LDA  BaddieData,X`

`      STA  SCREENADD+1`

`      INX   `

`      LDA  BaddieData,X`

`      STA  XOFFSET`

`      INX   `

`      INX   `

`      INX`

`      INX`

`      `

`   `

`      LDA  BadGfx1`

`      STA  CURRENTSPRITEDATA`

`      LDA  BadGfx1+1`

`      STA  CURRENTSPRITEDATA+1`

`   `

`      LDA  BadGfxWidth`

`      STA  WIDTH`

`      LDA  BadGfxHeight`

`      STA  HEIGHT`

`   `

`      TXA`

`      PHA`

`      JSR  SpriteController.SpriteNoMaskDraw`

`      PLA`

`      TAX   `

`   `

`   DB_SkipDraw:`

`   `

`      PLA`

`      TAY`

`      `

`      DEY`

`      BNE  DB_DrawInvaders`

`      `

`      RTS`

`   `

`   `

`   BaddieSound:`

`   `

`       LDA MISSFIRSTSOUND`

`       BEQ over`

`   `

`       LDA BadMotherState`

`       CMP  #1`

`       BEQ  over2`

`   `

`       LDA #9     ;invader step sound`

`       JSR Sound._MAKE_SOUND`

`   `

`   over:`

`     LDA #1`

`       STA MissFirstSound`

`   `

`   over2:`

`     RTS`

`   `

`   ;-------------------------------------------------------------------------------`

`   ;  BaddiesUpdate:`

`   ;    Updates the invaders ...`

`   ;-------------------------------------------------------------------------------`

`   BaddiesUpdate:`

`   `

`      LDA  INV_DELAYCOUNT`

`      BEQ  BU_Update`

`   `

`      DEC  INV_DELAYCOUNT`

`      BEQ  BU_jump`

`      RTS`

`   `

`   BU_jump:`

`   `

`      jsr BaddieSound`

`   `

`      LDA  BadMode`

`      ASL`

`      TAX`

`      LDA  BadModeJump,X`

`      STA  TEMPPTR`

`      INX`

`      LDA  BadModeJump,X`

`      STA  TEMPPTR+1`

`      JMP  (TEMPPTR)`

`             `

`   `

`   BadModeJump:`

`   `

`      .word BadddiesUpdate_Mode_startup`

`      .word BadddiesUpdate_Mode_WalkLeft`

`      .word BadddiesUpdate_Mode_WalkRight`

`      .word BadddiesUpdate_Mode_WalkDown`

`      .word BadddiesUpdate_Mode_Invaded`

`   `

`   `

`   ;-------------------------------------------------------------------------------`

`   ;  BadddiesUpdate_Mode_startup:`

`   ;    initializes the baddies, starting them ...`

`   ;-------------------------------------------------------------------------------`

`   BadddiesUpdate_Mode_startup:`

`   `

`      LDA  INV_DELAYUPDATE`

`      ASL`

`      ASL`

`      STA  INV_DELAYCOUNT`

`      LDA  #INV_MODE_WALKRIGHT`

`      STA  BadMode`

`      LDA  #2`

`      STA  INV_FRAME`

`      LDA  #0`

`      STA  INV_YMOVDIR`

`      RTS`

`   `

`   ;-------------------------------------------------------------------------------`

`   ;  BadddiesUpdate_Mode_WalkLeft:`

`   ;    Walks the baddies left - this checks for the left limit then makes them `

`   ;    go down...`

`   ;-------------------------------------------------------------------------------`

`   BadddiesUpdate_Mode_WalkLeft:`

`   `

`      LDA  #$ff`

`      STA  INV_MOVDIR`

`      JMP  BU_Update`

`   `

`   ;-------------------------------------------------------------------------------`

`   ;  BadddiesUpdate_Mode_WalkRight:`

`   ;    Walks the baddies right - this checks for the right limit then makes them `

`   ;    go down...`

`   ;-------------------------------------------------------------------------------`

`   BadddiesUpdate_Mode_WalkRight:`

`   `

`      LDA  #1`

`      STA  INV_MOVDIR`

`      JMP  BU_Update`

`   `

`   ;-------------------------------------------------------------------------------`

`   ;  BadddiesUpdate_Mode_WalkDown:`

`   ;    Walks the baddies down 8 pixels - then starts invaders going left or right `

`   ;-------------------------------------------------------------------------------`

`   BadddiesUpdate_Mode_WalkDown:`

`   `

`      DEC  BadInvYRef`

`      BNE  BU_godown`

`   `

`      LDA  INV_DELAYUPDATE`

`      STA  INV_DELAYCOUNT`

`      LDA  #2`

`      STA  INV_FRAME`

`    `

`      LDA  #0`

`      STA  INV_YMOVDIR`

`      LDA  BadFLag+2`

`      STA  BadMode`

`      RTS`

`      `

`   BU_godown:`

`   `

`      LDA  #1`

`      STA  INV_YMOVDIR`

`      LDA  #0`

`      STA  INV_MOVDIR`

`      JMP  BU_Update`

`   `

`   `

`   ;-------------------------------------------------------------------------------`

`   ;  BadddiesUpdate_Mode_Invaded:`

`   ;    Invaders have won - sigh`

`   ;-------------------------------------------------------------------------------`

`   BadddiesUpdate_Mode_Invaded:`

`   `

`      LDA  INV_DELAYUPDATE`

`      STA  INV_DELAYCOUNT`

`      LDA  #0`

`      STA  INV_YMOVDIR`

`   `

`      jsr  Invader_Player.Player_GameOver`

`      jsr  ScreenFunctionality.Screen_Clear  ; clear the screen...`

`   `

`      JMP  Main.main_restart`

`   `

`   `

`   ;-------------------------------------------------------------------------------`

`   ;  BU_Update:`

`   ;    Moves the invader according to mode, checks limits then draws them`

`   ;-------------------------------------------------------------------------------`

`   BU_Update:`

`   `

`       DEC  INV_FRAME`

`       BNE  BU_checkGroup  `

`       LDA  #2`

`       STA  INV_FRAME`

`   `

`   BU_checkGroup:`

`      `

`      LDA  #0`

`      LDX  INV_FRAME`

`      CPX  #1`

`      BEQ  BU_dotop`

`      `

`      LDA  #72`

`   `

`      ; move the top row of invaders one place`

`   BU_dotop:`

`   `

`      LDY  #12`

`      STA  SCRATCH1`

`   `

`   BU_Loop:`

`   `

`      PHA`

`   `

`      CLC`

`      ADC  #3`

`      TAX`

`   `

`      TYA`

`      PHA`

`   `

`      TXA`

`      CLC`

`      ADC  #2`

`      TAY`

`   `

`      LDA  BaddieData,Y`

`      CMP  #INV_STATE_ACTIVE`

`      BEQ  BU_CalcMove`

`      `

`      PLA`

`      TAY`

`   `

`      TXA`

`      CLC`

`      ADC  #3`

`      TAX`

`   `

`      PLA`

`      CLC`

`      ADC  #6`

`   `

`      JMP BU_SkipInvader`

`   `

`      `

`   BU_CalcMove:   `

`   `

`      PLA`

`      TAY`

`      `

`      LDA  BaddieData,X`

`      CLC`

`      ADC  INV_MOVDIR`

`      STA  XPOS`

`      STA  BadXPos`

`   `

`      INX`

`      LDA  BaddieData,X  `

`      CLC`

`      ADC  INV_YMOVDIR`

`      STA  YPOS`

`      STA  BadYPos`

`   `

`   `

`      ; adjust Y pos to bottom of sprite,`

`      LDA  BadGfxHeight`

`      CLC`

`      ADC  YPOS`

`      SEC`

`      SBC  #1`

`      STA  YPOS`

`   `

`      ; adjust the YPOS to character based and store the offset in x for indexing`

`      AND  #$07`

`      STA  XOFFSET`

`      LDA  YPOS`

`      AND  #$f8`

`      STA  YPOS`

`   `

`      TYA`

`      PHA`

`      JSR  SpriteController.SpriteCalcScreenPos`

`      PLA`

`      TAY`

`   `

`      PLA`

`      TAX`

`      `

`      ;store all the details...`

`   `

`      LDA  SCREENADD`

`      STA  BaddieData,X`

`      INX`

`      LDA  SCREENADD+1`

`      STA  BaddieData,X`

`      INX`

`      LDA  XOFFSET`

`      STA  BaddieData,X   `

`      INX`

`      LDA  BadXPos`

`      STA  BaddieData,X`

`      INX`

`      LDA  BadYPos`

`      STA  BaddieData,X`

`      INX`

`      INX   `

`   `

`      ; skip leftright check if going down...`

`      LDA  BadMode`

`      CMP  #INV_MODE_WALKDOWN`

`      BEQ  BU_SkipChange`

`      `

`      ; check and change direction...`

`      LDA  BadMode`

`      CMP  #INV_MODE_WALKLEFT`

`      BEQ  BU_CheckLeft`

`      LDA  BadXPos`

`      CMP  #74`

`      BCC  BU_CheckLeft`

`   `

`      LDA  BadInvYRef`

`      BNE  BU_CheckLeft`

`      LDA  #INV_MODE_WALKLEFT`

`      STA  BadFlag+2`

`      LDA  #INV_MODE_WALKDOWN`

`      STA  BadFlag+1`

`      LDA  #8`

`      STA  BadInvYRef`

`      JMP  BU_skipChange   `

`   `

`   BU_checkLeft:`

`   `

`      LDA  BadMode`

`      CMP  #INV_MODE_WALKRIGHT`

`      BEQ  BU_skipChange`

`      LDA  BadXPos`

`      CMP  #2`

`      BCS  BU_skipChange`

`   `

`      `

`      LDA  BadInvYRef`

`      BNE  BU_skipChange`

`      LDA  #INV_MODE_WALKRIGHT`

`      STA  BadFlag+2`

`      LDA  #INV_MODE_WALKDOWN`

`      STA  BadFlag+1`

`      LDA  #8`

`      STA  BadInvYRef`

`   `

`   BU_skipChange:`

`   `

`      TXA`

`   `

`   BU_skipInvader:`

`      `

`      DEY`

`      BEQ  BU_DoDraw`

`      JMP  BU_Loop         `

`   `

`   BU_DoDraw: `

`   `

`      ; if needed - blank the base line when invader reaches it`

`      PHA`

`      LDA SCRATCH1`

`      PHA`

`   `

`      ; calc the Y height in blocks - reference the bottom of the last invader`

`      ; calculated .... `

`      LDA  BadYPos`

`      CLC`

`      ADC  #6`

`      LSR`

`      LSR`

`      LSR`

`      TAY`

`      JSR  Invader_Bases.BlankLine`

`   `

`      PLA`

`      STA  SCRATCH1`

`      PLA`

`   `

`      LDX  SCRATCH1`

`      LDY  #12`

`      JSR  DB_DrawInvaders`

`   `

`      LDA  SCRATCH1`

`      BEQ  BU_Cont`

`   `

`      LDA  INV_DELAYUPDATE`

`      STA  INV_DELAYCOUNT`

`      LDA  #2`

`      STA  INV_FRAME`

`   `

`      LDA  BadYPos`

`      CMP  #215`

`      BCC  BU_ChangeGfx`

`      `

`      LDA  #INV_MODE_INVADED  `

`      STA  BadMode`

`   `

`      RTS`

`   `

`   BU_ChangeGfx:`

`   `

`      LDA  BadGfx3`

`      STA  BadGfx1`

`      LDA  BadGfx3+1`

`      STA  BadGfx1+1`

`      LDA  BadFLag`

`      EOR  #1`

`      STA  BadFlag`

`      BEQ  BU_cont`

`   `

`      LDA  BadGfx2`

`      STA  BadGfx1`

`      LDA  BadGfx2+1`

`      STA  BadGfx1+1`

`   `

`      LDA  BadFlag+1`

`      BEQ  BU_cont`

`      STA  BadMode`

`      LDA  #0`

`      STA  BadFlag+1`

`     `

`   `

`   BU_cont:`

`   `

`      RTS`

`   `

`   ;-------------------------------------------------------------------------------`

`   ;  Check Various Game states`

`   ;-------------------------------------------------------------------------------`

`   ;-------------------------------------------------------------------------------`

`   ;  BaddiesGeneralUpdate:`

`   ;    General updates and checks`

`   ;-------------------------------------------------------------------------------`

`   BaddiesGeneralUpdate:`

`   `

`      ; These should be impemented as states or flagged for process...`

`      ; Will no doubt revisit later...`

`      `

`      ; ok - monitor explosion here ... sigh!`

`      LDA  EXPLOSION_COUNT`

`      BEQ  BGU_Checkexp2`

`   `

`      LDA  #EXPLOSION_SPRITE_SLOT*16`

`      LDX  #SPRFLAG_REDRAW`

`      JSR  SpriteController.Sprite_SetFlag`

`   `

`      DEC  EXPLOSION_COUNT`

`      BNE  BGU_End`

`   `

`      LDA  #EXPLOSION_SPRITE_SLOT*16`

`      LDX  #SPRFLAG_KILL + SPRFLAG_REDRAW`

`      JSR  SpriteController.Sprite_SetFlag`

`   `

`   BGU_Checkexp2:`

`   `

`      LDA  EXPLOSION2_COUNT`

`      BEQ  BGU_Checkend`

`   `

`      LDA  #EXPLOSION2_SPRITE_SLOT*16`

`      LDX  #SPRFLAG_REDRAW`

`      JSR  SpriteController.Sprite_SetFlag`

`   `

`      DEC  EXPLOSION2_COUNT`

`      BNE  BGU_End`

`   `

`      LDA  #EXPLOSION2_SPRITE_SLOT*16`

`      LDX  #SPRFLAG_KILL + SPRFLAG_REDRAW`

`      JSR  SpriteController.Sprite_SetFlag`

`   `

`   BGU_Checkend:`

`   `

`   `

`      ; check for end of game`

`      LDA  TOTAL_INVADERS`

`      BNE  BGU_End`

`   `

`      JSR  Invader_Bullets.RemoveBullets`

`      JSR  Invader_Player.PBM_killBullet`

`      LDA  #EXPLOSION_SPRITE_SLOT * 16`

`      JSR  SpriteController.SpriteClear`

`      LDA  #EXPLOSION2_SPRITE_SLOT * 16`

`      JSR  SpriteController.SpriteClear`

`      jsr  SpriteController.SpritesWipeActive `

`   `

`      INC  GAME_LEVEL`

`      jsr  Invader_Player.Player_StartLevel`

`      jsr  ScreenFunctionality.Screen_Clear  ; clear the screen...`

`      jsr  ScreenFunctionality.DrawScore`

`      LDA  #PLAYER_SPRITE_SLOT*16`

`      LDX  #SPRFLAG_REDRAW`

`      JSR  SpriteController.Sprite_SetFlag`

`      LDA   #100`

`      STA   FIREBUTTON_DELAY`

`      `

`      ; new level ...`

`      LDA  BadStartHeight`

`      CLC`

`      ADC  #12`

`      STA  BadStartHeight`

`   `

`      LDX  INVADER_RESTARTDELAY`

`      DEX`

`      DEX`

`      STX  INVADER_RESTARTDELAY     `

`   `

`   `

`      JSR  BaddiesInit`

`   `

`      jsr  Invader_Bases.DrawBases`

`   `

`   BGU_End:`

`   `

`      LDA  FIREBUTTON_DELAY`

`      BEQ  BGU_term`

`      DEC  FIREBUTTON_DELAY`

`   `

`   BGU_term:`

`   `

`     RTS`

`   `

`   ;-------------------------------------------------------------------------------`

`   ;  Mother Ship Functionality`

`   ;-------------------------------------------------------------------------------`

`   `

`   `

`   ;-------------------------------------------------------------------------------`

`   ;  BaddiesUpdateMother:`

`   ;    Control for the mother ship...`

`   ;-------------------------------------------------------------------------------`

`   BaddiesUpdateMother:`

`   `

`      LDA  BadMotherCount`

`      BEQ  BU_Mother`

`   `

`      DEC  BadMotherCount`

`      RTS`

`   `

`   BU_Mother:`

`   `

`      LDA  BadMotherState`

`      ASL`

`      TAX`

`      LDA  BadMotherJump,X`

`      STA  TEMPPTR`

`      INX`

`      LDA  BadMotherJump,X`

`      STA  TEMPPTR+1`

`      JMP  (TEMPPTR)`

`   `

`   BadMotherJump:`

`   `

`      .word BadMother_inactive`

`      .word BadMother_move`

`      .word BadMother_end`

`      .word BadMother_shot`

`      `

`   `

`   ;-------------------------------------------------------------------------------`

`   ;  BadMother_inactive:`

`   ;    pause before activating the mother ship...`

`   ;-------------------------------------------------------------------------------`

`   BadMother_inactive:`

`   `

`       LDA #7`

`       jsr Sound._MAKE_SOUND   ;;;//top alien loop sound`

`      LDA  #MOTHER_DELAYMOVE`

`      STA  BadMotherCount`

`      LDA  #MOTHER_STATE_MOVE`

`      STA  BadMotherState`

`      RTs  `

`   `

`   ;-------------------------------------------------------------------------------`

`   ;  BadMother_move:`

`   ;    moves the mother ship from left to right`

`   ;-------------------------------------------------------------------------------`

`   BadMother_Move:`

`   `

`      LDA  #MOTHER_DELAYMOVE`

`      STA  BadMotherCount`

`   `

`      LDA  BadMotherXPos`

`      CLC`

`      ADC  #1`

`      STA  BadMotherXPos`

`   `

`      PHA`

`      `

`      AND  #3`

`      BNE  BM_Move2  `

`   `

`      ; Every time the mother ship reaches on a position div'ed by 4 ...`

`      ; swap the image of the mother ship, to give the impression of life!`

`      ; Well, nearly. Sprite frames are 4 and 7, so XOR 3 to initial value`

`      ; of 4 - flips then between the two images ...`

`      LDA  BadMotherGfxNum`

`      EOR  #3`

`      STA  BadMotherGfxNum`

`      JSR  SpriteController.SpriteRetreiveDetails`

`      LDA  CURRENTSPRITEDATA`

`      STA  BadMotherGfx`

`      LDA  CURRENTSPRITEDATA+1`

`      STA  BadMotherGfx+1`

`   `

`   BM_Move2:`

`      `

`      PLA`

`   `

`      CLC`

`      CMP  #74`

`      BCC  BadMother_DraW `

`   `

`   `

`      LDA  #255`

`      STA  BadMotherCount`

`      LDA  #MOTHER_STATE_INACTIVE`

`      STA  BadMotherState`

`   `

`      JSR  BadMother_Clear`

`      LDA  #2`

`      STA  BadMotherXPos`

`      RTS`

`      `

`   ;-------------------------------------------------------------------------------`

`   ;  BadMother_end:`

`   ;    mother ship has reached it's end stop...`

`   ;-------------------------------------------------------------------------------`

`   BadMother_end:`

`      RTS`

`      `

`   ;-------------------------------------------------------------------------------`

`   ;  BadMother_shot:`

`   ;    the mother ship has been shot...`

`   ;-------------------------------------------------------------------------------`

`   BadMother_shot:`

`   `

`      JSR  BadMother_Clear`

`   `

`      LDA  #MOTHER_STATE_INACTIVE`

`      STA  BadMotherState`

`      LDA  #$ff`

`      STA  BadMotherCount`

`      LDA  #2`

`      STA  BadMotherXPos`

`      `

`      RTS `

`   `

`   ;-------------------------------------------------------------------------------`

`   ;  BadMother_Draw:`

`   ;    calculte the screen position then draw the mother ship...`

`   ;-------------------------------------------------------------------------------`

`   BadMother_Draw:`

`   `

`      LDA  BadMotherXPos`

`      STA  XPOS`

`   `

`      LDA  #10  `

`      STA  YPOS`

`   `

`   `

`      ; adjust Y pos to bottom of sprite,`

`      LDA  #10`

`      CLC`

`      ADC  YPOS`

`      SEC`

`      SBC  #1`

`      STA  YPOS`

`   `

`      ; adjust the YPOS to character based and store the offset in x for indexing`

`      AND  #$07`

`      STA  XOFFSET`

`      LDA  YPOS`

`      AND  #$f8`

`      STA  YPOS`

`   `

`      JSR  SpriteController.SpriteCalcScreenPos`

`   `

`      LDA  BadMotherGfx`

`      STA  CURRENTSPRITEDATA`

`      LDA  BadMotherGfx+1`

`      STA  CURRENTSPRITEDATA+1`

`      LDA  #5`

`      STA  WIDTH`

`      LDA  #10`

`      STA  HEIGHT`

`   `

`      JMP  SpriteController.SpriteNoMaskDraw`

`   `

`   ;-------------------------------------------------------------------------------`

`   ;  BadMother_Clear:`

`   ;    Screen clear, block clear the size of the sprite...`

`   ;-------------------------------------------------------------------------------`

`   BadMother_Clear:`

`   `

`      LDA  BadMotherXPos`

`      STA  XPOS`

`   `

`      LDA  #10  `

`      STA  YPOS`

`   `

`   `

`      ; adjust Y pos to bottom of sprite,`

`      LDA  #10`

`      CLC`

`      ADC  YPOS`

`      SEC`

`      SBC  #1`

`      STA  YPOS`

`   `

`      ; adjust the YPOS to character based and store the offset in x for indexing`

`      AND  #$07`

`      STA  XOFFSET`

`      LDA  YPOS`

`      AND  #$f8`

`      STA  YPOS`

`   `

`      JSR  SpriteController.SpriteCalcScreenPos`

`   `

`      LDA  #5`

`      STA  WIDTH`

`      LDA  #10`

`      STA  HEIGHT`

`   `

`      JMP  SpriteController.Sprite_Blank`

`   `

`   ;-------------------------------------------------------------------------------`

`   ;  Misc Baddie Functionality`

`   ;-------------------------------------------------------------------------------`

`   `

`   ;-------------------------------------------------------------------------------`

`   ;  Baddie_CheckKill:`

`   ;    Checks the bullet with the invaders that are active...`

`   ;    X - Xpos`

`   ;    Y - Ypos`

`   ;    Returns - `

`   ;    A - -1 or offset for baddie to kill... `

`   ;-------------------------------------------------------------------------------`

`   Baddie_CheckKill:`

`   `

`      STX  XPOS`

`      STY  YPOS`

`   `

`      ; check the mother ship ...`

`      LDA  BadMotherState`

`      CMP  #MOTHER_STATE_MOVE`

`      BNE  BCK_CheckInvaders   `

`   `

`   `

`      CPY  #15`

`      BCS  BCK_CheckInvaders`

`      LDA  BadMotherXPos`

`      CMP  XPOS`

`      BCS  BCK_CHeckInvaders`

`      CLC`

`      ADC  #5`

`      CMP  XPOS`

`      BCC  BCK_CheckInvaders   `

`   `

`   `

`      ; Hit the mother ship, award points and remove ship`

`      LDX  BadMotherXPos`

`      LDY  #10`

`      JSR  Invader_Player.Player_MotherExplosionStart`

`    `

`     LDA #8  ;;//stop loop`

`       JSR Sound._MAKE_SOUND`

`   `

`       LDA #3  ;;//long exp`

`       JSR Sound._MAKE_SOUND`

`   `

`      LDA  SCORE_ADDITION`

`      CLC`

`      ADC  #25`

`      STA  SCORE_ADDITION  `

`   `

`      LDA  #25`

``      `ADDTO16BIT  SCORE_LO   ``

`   `

`      ; check the bonus and see if we need another life `

`   `

`   BCK_DEBUG:`

`   `

`      LDA  SCORE_HI`

`      CMP  BONUSSCORE_HI`

`      BCC  BCK_Cont`

`      LDA  SCORE_LO`

`      CMP  BONUSSCORE_LO`

`      BCC  BCK_Cont`

`   `

`      INC  PLAYER_LIFES`

`      LDA  #<500`

`      CLC`

`      ADC  BONUSSCORE_LO`

`      STA  BONUSSCORE_LO`

`      LDA  #>500`

`      ADC  BONUSSCORE_HI`

`      STA  BONUSSCORE_HI      `

`   `

`   BCK_Cont:`

`   `

`      LDA  #MOTHER_STATE_SHOT   `

`      STA  BadMotherState`

`      `

`   BCK_CheckInvaders:`

`   `

`      LDA  #0`

`      STA  SCRATCH1`

`   `

`      LDX  #0 + 3      ; index to xpos`

`      LDY  #0 + 5      ; index to active state   `

`   `

`   BCK_loop:`

`   `

`      STX  SCRATCH2`

`      STY  SCRATCH3`

`   `

`      LDA  BaddieData,Y`

`      BEQ  BCK_Skip`

`   `

`      `

`      ; check left, right `

`      LDA  BaddieData,X`

`      CMP  XPOS  `

`      BCS  BCK_Skip`

`      CLC`

`      ADC  #3     `

`      CMP  XPOS`

`      BCC  BCK_Skip`

`   `

`      ; check top, bottom `

`      INX`

`      LDA  BaddieData,X`

`      CMP  YPOS  `

`      BCS  BCK_Skip`

`      CLC`

`      ADC  #6     `

`      CMP  YPOS`

`      BCC  BCK_Skip`

`   `

`      ; hit invader ...`

`      `

`      INX`

`       TXA`

`       PHA`

`       LDA #4  ;;//exp`

`       JSR Sound._MAKE_SOUND`

`       PLA`

`       TAX`

`   `

`   `

`      LDA  #INV_STATE_REMOVE`

`      STA  BaddieData,X`

`   `

`   ;`

`   ;  ; store the bullet details...`

`   ;   LDA  SCRATCH1`

`   ;   LDX  #$ff`

`   ;   CMP  INV_PICKED1`

`   ;   BNE  C_try2`

`   ;   STX  INV_PICKED1`

`   ;   JMP  C_cont;;`

`   ;`

`   ;C_try2:`

`   ;   CMP  INV_PICKED2`

`   ;   BNE  C_try3`

`   ;   STX  INV_PICKED2`

`   ;   JMP  C_cont`

`   ;  `

`   ;C_try3:`

`   ;   CMP  INV_PICKED3`

`   ;   BNE  C_cont`

`   ;   STX  INV_PICKED3;;`

`   `

`   ;C_cont:`

`   `

`   ;   JSR  Invader_bullets.RemoveFromLink`

`   `

`      ; set off the explosion ...`

`      LDX  SCRATCH2`

`      LDA  BaddieData,X`

`      INX`

`      LDY  BaddieData,X`

`      TAX   `

`      `

`      JMP  Invader_Player.Player_ExplosionStart`

`      `

`   BCK_Skip:`

`   `

`      LDX  SCRATCH2`

`      LDY  SCRATCH3`

`   `

`      TXA`

`      CLC`

`      ADC  #6`

`      TAX`

`       `

`      TYA`

`      CLC`

`      ADC  #6`

`      TAY`

`       `

`         `

`      INC  SCRATCH1`

`      LDA  SCRATCH1`

`      CMP  #24`

`      BNE  BCK_loop`

`   `

`      LDA  #$ff`

`      RTS`

`   `

`   `

`   `

`   ;-------------------------------------------------------------------------------`

`   ;  Baddies_RemoveInvader:`

`   ;    Draws an blank where the invader used to be...`

`   ;    X - index to invader data`

`   ;-------------------------------------------------------------------------------`

`   Baddies_RemoveInvader:`

`   `

`      ; adjust the score - here seems a good enough place as any`

`      LDA  SCORE_ADDITION`

`      CLC`

`      ADC  #10`

`      STA  SCORE_ADDITION`

`   `

`      LDA  #10`

``      `ADDTO16BIT SCORE_LO``

`   `

`      LDA  SCORE_HI`

`      CMP  BONUSSCORE_HI`

`      BCC  BIV_skipbonuscheck`

`      LDA  SCORE_LO`

`      CMP  BONUSSCORE_LO`

`      BCC  BIV_skipbonuscheck`

`   `

`   BIV_debug:`

`   `

`   `

`      INC  PLAYER_LIFES`

`      LDA  #<500`

`      CLC`

`      ADC  BONUSSCORE_LO`

`      STA  BONUSSCORE_LO`

`      LDA  #>500`

`      ADC  BONUSSCORE_HI`

`      STA  BONUSSCORE_HI      `

`   `

`   BIV_skipbonuscheck:`

`   `

`   `

`   `

`      DEC  TOTAL_INVADERS`

`   `

`      LDA  INV_DELAYUPDATE`

`      CMP  #1`

`      BEQ  BIV_cont`

`   `

`      DEC  INV_DELAYUPDATE ; slightly speed things up a little`

`   `

`   BIV_cont:`

`   `

`   `

`      LDA  BaddieData,X`

`      STA  SCREENADD`

`      INX   `

`      LDA  BaddieData,X`

`      STA  SCREENADD+1`

`      INX   `

`      LDA  BaddieData,X`

`      STA  XOFFSET`

`      INX   `

`      LDA  BaddieData,X`

`      INX   `

`      LDY  BaddieData,X`

`      INX   `

`      INX   `

`   `

`      `

`   ;   TAX`

`   ;   LDA  SCRATCH1`

`   ;   PHA`

`   ;   JSR  Invader_Player.Player_ExplosionStart`

`   ;   PLA`

`   ;   STA  SCRATCH1`

`      `

`      LDA  BadGfx1`

`      STA  CURRENTSPRITEDATA`

`      LDA  BadGfx1+1`

`      STA  CURRENTSPRITEDATA+1`

`      LDA  BadGfxWidth`

`      STA  WIDTH`

`      LDA  BadGfxHeight`

`      STA  HEIGHT`

`   `

`      JMP  SpriteController.Sprite_Blank`

`   `

`   `

`   `

`   ;-------------------------------------------------------------------------------`

`   ;  Baddies_GetInvader:`

`   ;    a - index start position - the search is in reverse order`

`   ;    Returns the invader data in USERPTR`

`   ;    a - number of invader picked...`

`   ;-------------------------------------------------------------------------------`

`   Baddies_GetInvader:`

`   `

`      STA  SCRATCH1`

`      LDA  #1`

`      STA  SCRATCH2`

`   `

`   BGI_Loop:`

`   `

`   `

`   `

`      LDA  SCRATCH1`

`   `

`      CMP  INV_PICKED1`

`      BEQ  BGI_Skip`

`      CMP  INV_PICKED2`

`      BEQ  BGI_Skip`

`      CMP  INV_PICKED3`

`      BEQ  BGI_Skip`

`      `

`         `

``      `MUL6 TEMP  ; multipy A by 6 and store in TEMP ``

`      LDA  TEMP`

`      CLC`

`      ADC  #5`

`      TAY`

`      `

`      LDA  BaddieData,Y`

`      BNE  BGI_FOund`

`   `

`   `

`   BGI_Skip:`

`   `

`      DEC  SCRATCH1`

`      BPL  BGI_Loop`

`   `

`      DEC  SCRATCH2`

`      BMI  BGI_failed  `

`      LDA  #24-1`

`      STA  SCRATCH1`

`      JMP  BGI_Loop`

`   `

`   BGI_Found:`

`   `

`      LDA  #`<BaddieData

       CLC

       ADC  TEMP

       STA  USERPTR

       LDA  #>`BaddieData`

`      ADC  #0`

`      STA  USERPTR+1   `

`   `

`      LDA  SCRATCH1`

`   `

`      RTS`

`   `

`   BGI_failed:`

`   `

`      LDA  #$ff`

`      RTS`

`   `

`   `

`   `

`   ;-------------------------------------------------------------------------------`

`   `

`   BaddieData:`

`   `

`      .byte 0,0,0,0,0,0     ; 01 screen add (2 bytes), Xoffset, xpos, ypos, State   `

`      .byte 0,0,0,0,0,0     ; 02`

`      .byte 0,0,0,0,0,0     ; 03`

`      .byte 0,0,0,0,0,0     ; 04`

`      .byte 0,0,0,0,0,0     ; 05`

`      .byte 0,0,0,0,0,0     ; 06`

`      .byte 0,0,0,0,0,0     ; 07`

`      .byte 0,0,0,0,0,0     ; 08`

`      .byte 0,0,0,0,0,0     ; 09`

`      .byte 0,0,0,0,0,0     ; 10`

`      .byte 0,0,0,0,0,0     ; 11`

`      .byte 0,0,0,0,0,0     ; 12`

`      .byte 0,0,0,0,0,0     ; 13`

`      .byte 0,0,0,0,0,0     ; 14`

`      .byte 0,0,0,0,0,0     ; 15`

`      .byte 0,0,0,0,0,0     ; 16`

`      .byte 0,0,0,0,0,0     ; 17`

`      .byte 0,0,0,0,0,0     ; 18`

`      .byte 0,0,0,0,0,0     ; 19`

`      .byte 0,0,0,0,0,0     ; 20`

`      .byte 0,0,0,0,0,0     ; 21`

`      .byte 0,0,0,0,0,0     ; 22`

`      .byte 0,0,0,0,0,0     ; 23`

`      .byte 0,0,0,0,0,0     ; 24`

`   `

`   `

`   `

`   `

`   `

`   ;-------------------------------------------------------------------------------`

`   `

`   BadStartHeight:    .byte 0`

`   BadGfx1:           .byte 0,0`

`   BadGfx2:           .byte 0,0`

`   BadGfx3:           .byte 0,0`

`   BadGfxWidth:       .byte 0`

`   BadGfxHeight:      .byte 0`

`   BadXpos:           .byte 0`

`   BadYpos:           .byte 0`

`   BadFlag:           .byte 0,0,0`

`   BadMode:           .byte 0`

`   BadInvYRef:        .byte 0`

`   BadMotherGfx:      .byte 0,0`

`   BadMotherXPos:     .byte 0`

`   BadMotherCount:    .byte 0         `

`   BadMotherState:    .byte 0         `

`   BadMotherGfxNum:   .byte 0`

`   `

`   `

`   ;-------------------------------------------------------------------------------`

`   ; End of Invader_Baddies`

`   ;-------------------------------------------------------------------------------`

## Sparse Invaders Source - Invader\_Player.txt

`   ;-------------------------------------------------------------------------------`
`   ;  Invader_Player`
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
`   .alias  EXPLOSION_TIME 20             ; explosion time for invader and mother etc`
`   .alias  PLAYER_BULLET_SPRITE 6        ; sprtie for the player's bullet `
`   `
`   ;-------------------------------------------------------------------------------`
`   ;  PlayerInit:`
`   ;    initializes the player at the start of the level and game...`
`   ;-------------------------------------------------------------------------------`
`   PlayerInit:`
`   `
`      ; initialize the player and bullet`
`      LDA   #PLAYER_STARTX`
`      STA   PLAYER_X`
`      LDA   #PLAYER_STARTY`
`      STA   PLAYER_Y`
`      LDA   #0`
`      STA   PLAYER_FRAME`
`        `
`      LDA   #$ff`
`      STA   PLAYER_BULLET_X`
`      STA   PLAYER_BULLET_Y`
`      STA   PLAYER_BULLET_F`
`      `
`   `
`      ;kick off the player...`
`      LDA   #0`
`      STA   SPRITE`
`      STA   CALLPARAM1`
`      STA   CALLPARAM2`
`      LDA   #PLAYER_SPRITE_SLOT `
`      LDX   PLAYER_X`
`      LDY   PLAYER_Y`
`      JSR   SpriteController.SpriteStart`
`   `
`      LDA   #1`
`      STA   GAME_LEVEL`
`   `
`      LDA   #3`
`      STA   PLAYER_LIFES`
`      LDA   #ONE_HALF_SEC_DELAY`
`      STA   DELAY_COUNT`
`   `
`      LDA   #0`
`      STA   INPUTCHECK`
`      STA   SCORE_LO`
`      STA   SCORE_HI`
`      `
`      LDA   #<500`
`      STA   BONUSSCORE_LO`
`      LDA   #>500`
`      STA   BONUSSCORE_HI`
`      RTS`
`   `
`   ;-------------------------------------------------------------------------------`
`   ;`
`   ;   Bullet functionality...`
`   ;`
`   ;-------------------------------------------------------------------------------`
`   `
`   ;-------------------------------------------------------------------------------`
`   ;  Player_BulletStart:`
`   ;    initializes the player bullet...`
`   ;-------------------------------------------------------------------------------`
`   Player_BulletStart:`
`   `
`      LDA #0       ;fire bullet`
`      JSR Sound._MAKE_SOUND`
`   `
`      LDA  PLAYER_X`
`      CLC`
`      ADC  #1`
`      STA  PLAYER_BULLET_X`
`      `
`      LDA  PLAYER_Y`
`      SEC`
`      SBC  #5`
`      STA  PLAYER_BULLET_Y`
`      `
`      LDA   #PLAYER_BULLET_SPRITE`
`      STA   SPRITE`
`      LDA   #0`
`      STA   CALLPARAM1`
`      STA   CALLPARAM2`
`      LDA   #BULLET_SPRITE_SLOT   `
`      LDX   PLAYER_BULLET_X`
`      LDY   PLAYER_BULLET_Y`
`      JSR   SpriteController.SpriteStart`
`     `
`      RTS `
`   `
`   `
`   ;-------------------------------------------------------------------------------`
`   ;  Player_BulletStart:`
`   ;    initializes the player bullet...`
`   ;-------------------------------------------------------------------------------`
`   Player_BulletMove:`
`   `
`      LDA  PLAYER_BULLET_Y`
`      CMP  #$ff`
`      BEQ  PBM_End`
`   `
`      LDA  PLAYER_BULLET_Y`
`      SEC`
`      SBC  #4`
`      CMP  #8`
`      BCS  PBM_checkInvaders`
`   `
`   PBM_killBullet:`
`   `
`      LDA  #BULLET_SPRITE_SLOT*16`
`      LDX  #SPRFLAG_KILL + SPRFLAG_REDRAW`
`      JSR  SpriteController.Sprite_SetFlag`
`   `
`      LDA   #$ff`
`      STA   PLAYER_BULLET_X`
`      STA   PLAYER_BULLET_Y`
`      STA   PLAYER_BULLET_F`
`   `
`      RTS`
`      `
`   PBM_checkInvaders:   `
`   `
`      STA  PLAYER_BULLET_Y`
`   `
`      ; but ... first check the bases ...  ;-)`
`      LDX  PLAYER_BULLET_X`
`      LDY  PLAYER_BULLET_Y`
`      JSR  Invader_Bases.CheckCollison`
`      BCS  PBM_KillBullet`
`   `
`   `
`      LDX  PLAYER_BULLET_X`
`      LDY  PLAYER_BULLET_Y`
`      JSR  Invader_Baddies.Baddie_CheckKill`
`      CMP  #$ff`
`      BNE  PBM_KillBullet`
`     `
`   `
`   PBM_moveSprite:`
`   `
`      LDA  #BULLET_SPRITE_SLOT`
`      LDX  PLAYER_BULLET_X`
`      LDY  PLAYER_BULLET_Y`
`      JMP  SpriteController.SpriteMoveSprite    `
`   `
`   PBM_End:`
`      `
`      RTS`
`   `
`   ;-------------------------------------------------------------------------------`
`   ;   Explosion`
`   ;-------------------------------------------------------------------------------`
`   `
`   `
`   ;-------------------------------------------------------------------------------`
`   ;  Player_ExplosionStart:`
`   ;    initializes the player or invader explosion...`
`   ;    x - XPOS`
`   ;    y - YPOS`
`   ;-------------------------------------------------------------------------------`
`   Player_ExplosionStart:`
`   `
`      LDA   EXPLOSION_COUNT`
`      BNE   PES_end`
`      `
`      LDA   #EXPLOSION_TIME`
`      STA   EXPLOSION_COUNT`
`      LDA   #0`
`      STA   CALLPARAM1`
`      STA   CALLPARAM2`
`      LDA   #5`
`      STA   SPRITE`
`      LDA   #EXPLOSION_SPRITE_SLOT   `
`      JMP   SpriteController.SpriteStart`
`   `
`   PES_end:`
`   `
`      RTS`
`   `
`   ;-------------------------------------------------------------------------------`
`   ;-------------------------------------------------------------------------------`
`   ;  Player_MotherExplosionStart:`
`   ;    initializes the other explosion...`
`   ;    x - XPOS`
`   ;    y - YPOS`
`   ;-------------------------------------------------------------------------------`
`   Player_MotherExplosionStart:`
`   `
`      LDA   EXPLOSION2_COUNT`
`      BNE   PES_end`
`   `
`      INX`
`      INX`
`      LDA   #EXPLOSION_TIME`
`      STA   EXPLOSION2_COUNT`
`      LDA   #0`
`      STA   CALLPARAM1`
`      STA   CALLPARAM2`
`      LDA   #5`
`      STA   SPRITE`
`      LDA   #EXPLOSION2_SPRITE_SLOT`
`      JMP   SpriteController.SpriteStart`
`   `
`   `
`   ;-------------------------------------------------------------------------------`
`   ;   Game Messages ... `
`   ;-------------------------------------------------------------------------------`
`   `
`   ;-------------------------------------------------------------------------------`
`   ;  Player_GameMessage:`
`   ;    displays the start game message`
`   ;-------------------------------------------------------------------------------`
`   Player_GameMessage:`
`   `
`     LDA  #GAME_STATE_INTRO                 ; GAME state`
`     STA  GAME_STATE`
`     LDA  #ONE_HALF_SEC_DELAY`
`     STA  DELAY_COUNT`
`     LDA   #0`
`     STA   INPUTCHECK`
`   `
`     LDA  #`<GM_1
      STA  USERPTR 
      LDA  #>`GM_1`
`     STA  USERPTR+1`
`     JSR  ScreenFunctionality.Screen_PositionedMessage`
`     LDA  #`<GM_11
      STA  USERPTR 
      LDA  #>`GM_11`
`     STA  USERPTR+1`
`     JSR  ScreenFunctionality.Screen_PositionedMessage`
`   `
`     LDA  #`<GM_2
      STA  USERPTR 
      LDA  #>`GM_2`
`     STA  USERPTR+1`
`     JSR  ScreenFunctionality.Screen_PositionedMessage`
`     LDA  #`<GM_3
      STA  USERPTR 
      LDA  #>`GM_3`
`     STA  USERPTR+1`
`     JSR  ScreenFunctionality.Screen_PositionedMessage`
`     LDA  #`<GM_31
      STA  USERPTR 
      LDA  #>`GM_31`
`     STA  USERPTR+1`
`     JSR  ScreenFunctionality.Screen_PositionedMessage`
`     LDA  #`<GM_32
      STA  USERPTR 
      LDA  #>`GM_32`
`     STA  USERPTR+1`
`     JSR  ScreenFunctionality.Screen_PositionedMessage`
`     LDA  #`<GM_4
      STA  USERPTR 
      LDA  #>`GM_4`
`     STA  USERPTR+1`
`     JSR  ScreenFunctionality.Screen_PositionedMessage`
`   `
`   PGM_waitFire:`
`   `
`     LDA  #0`
`     STA  INPUTCHECK`
`   `
`   PGM_CheckKeys:`
`   `
`     LDA  DELAY_COUNT`
`     BNE  PGM_CK`
`   `
`     LDA  #`<IN_1
      STA  USERPTR 
      LDA  #>`IN_1`
`     STA  USERPTR+1`
`     JSR  ScreenFunctionality.Screen_PositionedMessage`
`   `
`   PGM_CK:`
`   `
`     JSR  Keyboard.Keyboard_checkkeys`
`     LDA  INPUTCHECK`
`     AND  #INPUTFLAG_FIRE`
`     BEQ  PGM_CheckKeys`
`   `
`     RTS`
`   `
`   `
`   ;-------------------------------------------------------------------------------`
`   ;  Player_StartLevel:`
`   ;    displays the game message, passing in the message number`
`   ;-------------------------------------------------------------------------------`
`   Player_StartLevel:`
`   `
`      LDA  #GAME_STATE_STARTLEVEL            ; GAME state`
`      STA  GAME_STATE`
`      `
`      ; convert the number ...`
`      LDX  #11`
`      LDA  GAME_LEVEL`
`   `
`      CMP  #10`
`      BCC  PSL_dounits`
`   `
`   PSL_dotens:`
`   `
`      SEC`
`      SBC  #10`
`   `
`      PHA`
`      LDA  SL_1,X`
`      CLC`
`      ADC  #1`
`      STA  SL_1,X`
`      PLA`
`      `
`      CMP  #10`
`      BCS  PSL_dotens  `
`   `
`      INX`
`   `
`   `
`   PSL_dounits:`
`   `
`     CLC`
`     ADC  #48`
`     STA  SL_1,X`
`     INX`
`     LDA  #0`
`     STA  SL_1,X`
`       `
`   `
`     JSR  ScreenFunctionality.Screen_Clear  ; Display main message...`
`   `
`     LDA  #`<GM_1
      STA  USERPTR 
      LDA  #>`GM_1`
`     STA  USERPTR+1`
`     JSR  ScreenFunctionality.Screen_PositionedMessage`
`     LDA  #`<GM_11
      STA  USERPTR 
      LDA  #>`GM_11`
`     STA  USERPTR+1`
`     JSR  ScreenFunctionality.Screen_PositionedMessage`
`   `
`     LDA  #`<SL_1
      STA  USERPTR 
      LDA  #>`SL_1`
`     STA  USERPTR+1`
`     JSR  ScreenFunctionality.Screen_PositionedMessage`
`     LDA  #GAME_STATE_PLAYING            ; GAMe state`
`     STA  GAME_STATE`
`     LDA  #ONE_HALF_SEC_DELAY`
`     STA  DELAY_COUNT`
`     `
`     JMP  PGM_waitFire`
`   `
`   ;-------------------------------------------------------------------------------`
`   ;  Player_GameOver:`
`   ;    displays the game over message`
`   ;-------------------------------------------------------------------------------`
`   Player_GameOver:`
`   `
`       LDA #8  ;;//stop loop`
`       JSR Sound._MAKE_SOUND`
`   `
`   `
`     LDA  #GAME_STATE_INVADED                 ; GAME state`
`     STA  GAME_STATE`
`   `
`   PG_AdjustScore:`
`   `
`     LDA  SCORE_ADDITION`
`     BEQ  PG_Cont`
`     JSR  ScreenFunctionality.AdjustScore`
`     JMP  PG_AdjustScore`
`     `
`   PG_Cont:`
`   `
`     LDX  SCORE_LO`
`     LDY  SCORE_HI`
`     JSR  Invader_Hiscore.Invader_CheckScore`
`   `
`     LDA  #`<GO_2
      CLC
      ADC  #10
      STA  USERPTR
      LDA  #>`GO_2`
`     ADC  #0`
`     STA  USERPTR+1`
`     JSR  ScreenFunctionality.Screen_CopyScoreToString`
`   `
`     JSR  ScreenFunctionality.Screen_Clear  ; Display main message...`
`   `
`     LDA  #`<GM_1
      STA  USERPTR 
      LDA  #>`GM_1`
`     STA  USERPTR+1`
`     JSR  ScreenFunctionality.Screen_PositionedMessage`
`   `
`     LDA  #`<GO_1
      STA  USERPTR 
      LDA  #>`GO_1`
`     STA  USERPTR+1`
`     JSR  ScreenFunctionality.Screen_PositionedMessage`
`   `
`     LDA  #`<GO_2
      STA  USERPTR 
      LDA  #>`GO_2`
`     STA  USERPTR+1`
`     JSR  ScreenFunctionality.Screen_PositionedMessage`
`   `
`     LDA  #ONE_HALF_SEC_DELAY`
`     STA  DELAY_COUNT`
`     LDA   #0`
`     STA   INPUTCHECK`
`   `
`     JSR  PGM_waitFire`
`   `
`     JMP  Invader_Hiscore.Invader_Hiscore_Display`
`   `
`   `
`   ;-------------------------------------------------------------------------------`
`   ;  strings used for game`
`   ;-------------------------------------------------------------------------------`
`   `
`   GM_1:  .byte 2,3,"sparse invaders",0`
`   GM_11: .byte 1,5,"a small production",0`
`   GM_2:  .byte 4,9,"written by",0`
`   GM_3:  .byte 3,11,"neil beresford",0`
`   GM_31: .byte 4,18,"sound by pj",0`
`   GM_32: .byte 3,20,"misc by steve o ",0`
`   GM_4:  .byte 2,24,"date  3 nov 2009",0`
`   SL_1:  .byte 5,10,"level       ",0`
`   GO_1:  .byte 5,11,"game over",0`
`   GO_2:  .byte 4,17,"score   xxxx",0`
`   IN_1:  .byte 3,26,"fire to start",0`
`   `
`   `
`   ;-------------------------------------------------------------------------------`
`   ;   End of Invader_Player`
`   ;-------------------------------------------------------------------------------`

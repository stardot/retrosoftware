## Sparse Invaders Source - Invaders_Bullets.txt

`   ;-------------------------------------------------------------------------------`

`   ;  Invader_Bullets`

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

`   ;    Controls the bullet rate, speed and also collision.`

`   ;`

`   ;-------------------------------------------------------------------------------`

`   `

`   .require "Constands"`

`   .require "Macros"`

`   `

`   ;-------------------------------------------------------------------------------`

`   `

`   .alias INIT_BULLETDELAY     60   ; initial delay between bullets`

`   .alias MAX_BULLETS          3    ; limited to three as want to keep in a frame - plus the complex sprite controller ... hmmm!`

`   .alias BULLET_SPEED         2    ; pixel speed of the bullet`

`   `

`   ;-------------------------------------------------------------------------------`

`   ; Init:`

`   ;   initializes the bullet system`

`   ;-------------------------------------------------------------------------------`

`   Init:`

`   `

`     LDA  #0`

`     STA  BULLET_COUNT`

`     LDA  #$ff`

`     STA  INV_PICKED1`

`     STA  INV_PICKED2`

`     STA  INV_PICKED3`

`     `

`     LDA  #INIT_BULLETDELAY`

`     STA  BULLET_DELAY`

`     STA  BULLET_REFRESHDELAY`

`   `

`     LDA  #24-1     ; total invaders - starts at the bottom...`

`     STA  BULLETINVLAST`

`   `

`     RTS`

`   `

`   ;-------------------------------------------------------------------------------`

`   ; Control:`

`   ;   controls the spawning of the bullets ...`

`   ;-------------------------------------------------------------------------------`

`   Control:`

`   `

`     LDA  GAME_STATE`

`     CMP  GAME_STATE_PLAYING`

`     BNE  C_end`

`   `

`     DEC  BULLET_DELAY`

`     BNE  C_end`

`   `

`     LDA  BULLET_REFRESHDELAY`

`     STA  BULLET_DELAY`

`     `

`     ;  check number of active bullets ...`

`     LDA  BULLET_COUNT`

`     CMP  #MAX_BULLETS`

`     BEQ  C_end`

`     `

`     ;  start bullet off ...`

`     LDA  BULLETINVLAST`

`     JSR  Invader_Baddies.Baddies_GetInvader`

`   `

`     CMP  #$ff`

`     BEQ  C_end`

`    `

`     ; store the bullet details...`

`   `

`     LDX  #$ff`

`     CPX  INV_PICKED1`

`     BNE  C_try2`

`     STA  INV_PICKED1`

`     LDX  #0`

`     STX  SCRATCH3`

`     `

`     JMP  C_cont`

`   `

`   C_try2:`

`     CPX  INV_PICKED2`

`     BNE  C_try3`

`     STA  INV_PICKED2`

`     LDX  #1`

`     STX  SCRATCH3`

`     JMP  C_cont`

`     `

`   C_try3:`

`     CPX  INV_PICKED3`

`     BNE  C_end`

`     STA  INV_PICKED3`

`     LDX  #2`

`     STX  SCRATCH3`

`   `

`   C_cont:`

`   `

`     STA  SCRATCH4`

`   `

`   `

`     LDY  #3`

`     LDA  (USERPTR),Y`

`     TAX`

`     INX`

`     INX`

`     INY`

`     LDA  (USERPTR),Y`

`     CLC`

`     ADC  #6`

`     TAY`

`     `

`     LDA  #`<Bullet_SprControl

      STA  CALLPARAM1

      LDA  #>`Bullet_SprControl`

`     STA  CALLPARAM2`

`     LDA  #1`

`     STA  SPRITE`

`   `

`     INC  BULLET_COUNT`

`     LDA  #INVBULLET1_SPRITE_SLOT`

`     CLC`

`     ADC  SCRATCH3`

`     JSR  SpriteController.SpriteStart`

`     LDX  CURRENT_SPRITE`

`   `

`     LDA  SCRATCH4`

`     STA  Bullet_InvaderLink,X`

`     `

`   C_end:`

`   `

`     RTS`

`   `

`   `

`   ;-------------------------------------------------------------------------------`

`   ; Bullet_SprControl:`

`   ;   control for the sprite routine...`

`   ;   TEMPPTR is set ot point to the sprite data.`

`   ;-------------------------------------------------------------------------------`

`   Bullet_SprControl:`

`   `

`     LDA  GAME_STATE`

`     CMP  GAME_STATE_PLAYING`

`     BNE  BCS_Kill`

`   `

`     ; store the position for reference ...`

`     LDY  #SPRBLK_X`

`     LDA  (TEMPPTR),Y`

`     STA  XPOS`

`     INY`

`     LDA  (TEMPPTR),Y`

`   `

`     ; move the position of the bullet ...`

`     CLC`

`     ADC  #BULLET_SPEED   `

`     STA  (TEMPPTR),Y`

`     STA  YPOS`

`   `

`     CMP  #PLAYER_STARTY+8`

`     BCS  BCS_kill`

`   `

`     CMP  #PLAYER_STARTY`

`     BCC  BCS_end`

`   `

`     ; check x position for hitting the player`

`   `

`     LDA  PLAYER_X`

`     SEC`

`     SBC  #1`

`     `

`     CMP  XPOS`

`     BCS  BCS_end`

`   `

`     CLC`

`     ADC  #3`

`     CMP  XPOS`

`     BCS  BCS_hitplayer`

`   `

`   BCS_end:`

`   `

`     ; check for base collison ...`

`     LDX  XPOS`

`     LDY  YPOS`

`     JSR  Invader_Bases.CheckCollison`

`     BCS  BCS_kill`

`   `

`     ; flag sprite for redraw and continue...`

`     LDY  #SPRBLK_FLAG`

`     LDA  (TEMPPTR),Y`

`     ORA  #SPRFLAG_REDRAW`

`     STA  (TEMPPTR),Y`

`   `

`     LDA  ACTIVEINDEX`

`     STA  SCRATCH1`

`     JMP  SpriteController.SpriteMoveSpr    `

`   `

`   BCS_hitplayer:`

`   `

`     ; sort out the player ...`

`       LDA #3          ;long exp`

`       JSR Sound._MAKE_SOUND`

`     DEC  PLAYER_LIFES`

`     BNE  BCS_startexplosion`

`   `

`   `

`     JSR  Invader_Bullets.RemoveBullets`

`     JSR  Invader_Player.PBM_killBullet`

`     JSR  SpriteController.SpritesWipeActive `

`     JSR  Invader_Player.Player_GameOver`

`     JSR  ScreenFunctionality.Screen_Clear  ; clear the screen...`

`     JMP  Main.main_restart`

`   `

`   `

`   BCS_startexplosion:`

`   `

`     LDA  #1`

`     STA  SCREEN_UPDATE`

`   `

`     ; try and start an explosion off`

`     LDA  TEMPPTR`

`     PHA`

`     LDA  TEMPPTR+1`

`     PHA`

`     LDA  ACTIVEINDEX`

`     PHA`

`   `

`     LDX  PLAYER_X`

`     DEX`

`     LDY  PLAYER_Y`

`     JSR  Invader_Player.Player_ExplosionStart`

`   `

`     PLA`

`     STA  ACTIVEINDEX`

`     PLA`

`     STA  TEMPPTR+1`

`     PLA`

`     STA  TEMPPTR`

`     `

`   `

`   BCS_Kill:`

`   `

`     DEC  BULLET_COUNT`

`   `

`     LDY  #SPRBLK_FLAG`

`     LDA  (TEMPPTR),Y`

`     ORA  #SPRFLAG_REDRAW + SPRFLAG_KILL`

`     STA  (TEMPPTR),Y`

`   `

`     LDY  ACTIVEINDEX`

`     LDX  Bullet_InvaderLink,Y`

`     LDA  #$ff               `

`     STA  Bullet_InvaderLink,Y`

`     TXA`

`     LDX  #$ff`

`     CMP  INV_PICKED1`

`     BNE  BCS_try2`

`     STX  INV_PICKED1`

`     RTS`

`   BCS_try2:`

`     CMP  INV_PICKED2`

`     BNE  BCS_try3`

`     STX  INV_PICKED2`

`     RTS`

`   BCS_try3:`

`     CMP  INV_PICKED3`

`     BNE  BCS_skip3`

`     STX  INV_PICKED3`

`   `

`   BCS_skip3:`

`   `

`     RTS`

`   `

`   `

`   ;-------------------------------------------------------------------------------`

`   ; RemoveFromLink:`

`   ;   Removes the invader from the link data...`

`   ;   A - invader to remove.`

`   ;-------------------------------------------------------------------------------`

`   RemoveFromLink:`

`   `

`      LDY  #INVBULLET1_SPRITE_SLOT `

`   `

`      CMP  Bullet_InvaderLink,Y`

`      BNE  RFL_try2  `

`      LDA  #$ff`

`      STA  Bullet_InvaderLink,Y  `

`      RTS`

`      `

`   RFL_try2:  `

`   `

`      INY `

`      CMP  Bullet_InvaderLink,Y`

`      BNE  RFL_try3  `

`      LDA  #$ff`

`      STA  Bullet_InvaderLink,Y  `

`      RTS`

`   `

`   RFL_try3:  `

`   `

`      INY `

`      CMP  Bullet_InvaderLink,Y`

`      BNE  RFL_end  `

`      LDA  #$ff`

`      STA  Bullet_InvaderLink,Y  `

`   `

`   RFL_end:`

`   `

`      RTS`

`   `

`   `

`   `

`   ;-------------------------------------------------------------------------------`

`   ; RemoveFromLink:`

`   ;   Removes the invader bullets, this is end of level or game...`

`   ;-------------------------------------------------------------------------------`

`   RemoveBullets:`

`   `

`      ; clear the bullet count   `

`      LDA  #0`

`      STA  BULLET_COUNT`

`   `

`      ; clear the buffers ...`

`      LDY  #INVBULLET1_SPRITE_SLOT `

`      LDA  #$ff`

`      STA  Bullet_InvaderLink,Y   `

`      INY`

`      STA  Bullet_InvaderLink,Y   `

`      INY`

`      STA  Bullet_InvaderLink,Y   `

`      STA  INV_PICKED1`

`      STA  INV_PICKED2`

`      STA  INV_PICKED3`

`   `

`    `

`      ; clear the sprite bank...`

`      LDA  #INVBULLET1_SPRITE_SLOT*16`

`      LDX  #SPRFLAG_KILL + SPRFLAG_REDRAW`

`      JSR  SpriteController.Sprite_SetFlag`

`      LDA  #INVBULLET2_SPRITE_SLOT*16`

`      LDX  #SPRFLAG_KILL + SPRFLAG_REDRAW`

`      JSR  SpriteController.Sprite_SetFlag`

`      LDA  #INVBULLET3_SPRITE_SLOT*16`

`      LDX  #SPRFLAG_KILL + SPRFLAG_REDRAW`

`      JMP  SpriteController.Sprite_SetFlag`

`   `

`   `

`     `

`   ;-------------------------------------------------------------------------------`

`   `

`   Bullet_InvaderLink:`

`   `

`     .byte  0,0,0,0,0,0,0,0  ; linked to the 8 possible active sprites...`

`                             ; to be honest, this could be 3 bytes!`

`   `

`   ;-------------------------------------------------------------------------------`

`   ;  End of Invader_Bullets`

`   ;-------------------------------------------------------------------------------`

# Sparse Invaders Source - Keyboard.txt

Keyboard handling is shown here, the keycodes are to be found in the constants.txt file.

I've been slightly lazy here and you will find the player keyboard controller here as well.

`   ;-------------------------------------------------------------------------------`

`   ;  Keyboard`

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

`   ;  Keyboard functionality for Invaders`

`   ;`

`   ;-------------------------------------------------------------------------------`

`   .require "Constands"`

`   .require "Macros"`

**Keyboard_checkKeys** checks the left and right direction ( Invaders has this set to 'Z' and 'X' ) and also the fire action key ( Invaders has this set to 'ENTER' ).

`   ;-------------------------------------------------------------------------------`

`   ; Keyboard_CheckKeys - `

`   ;     checks for the keys for Invaders...`

`   ;`

`   ;-------------------------------------------------------------------------------`

`   Keyboard_checkkeys:`

`      ; check for delay, this is really for menus etc ...`

`      LDA DELAY_COUNT`

`      BNE KCK_End`

`      SEI`

`      ; Initialise hardware for keyboard read`

`      LDA #$7F`

`      STA $FE43`

`      LDA #$0F`

`      STA $FE42`

`      LDA #$03`

`      STA $FE40`

`      ; clear the flag system`

`      LDA  #0`

`      STA  INPUTCHECK`

`       ; Test the keys`

`      LDA #KEYCODE_LEFT`

`      STA $FE4F`

`      LDA $FE4F `

`      BPL checkRight`

`      LDA INPUTCHECK`

`      ORA #INPUTFLAG_LEFT`

`      STA INPUTCHECK`

`   CheckRight:`

`      LDA #KEYCODE_RIGHT`

`      STA $FE4F`

`      LDA $FE4F `

`      BPL checkFire`

`      LDA INPUTCHECK`

`      ORA #INPUTFLAG_RIGHT`

`      STA INPUTCHECK`

`   CheckFire:`

`      LDA FIREBUTTON_DELAY`

`      BNE KCK_end`

`      LDA #KEYCODE_SPACE`

`      STA $FE4F`

`      LDA $FE4F `

`      BPL KCK_end`

`      LDA INPUTCHECK`

`      ORA #INPUTFLAG_FIRE`

`      STA INPUTCHECK`

`   KCK_end:`

`      CLI`

`      RTS`

**Keyboard_MovePlayer** checks the left and right direction ( Invaders has this set to 'Z' and 'X' ) and also the fire action key ( Invaders has this set to 'ENTER' ). With this function it moves the player sprite (checking for playing limits) and on a fire action checks to see if a player bullet is active, if not starts the bullet.

`   ;-------------------------------------------------------------------------------`

`   ; Keyboard_MovePlayer - `

`   ;     checks, moves player and fires as well`

`   ;`

`   ;-------------------------------------------------------------------------------`

`   Keyboard_MovePlayer:`

`     ; always do the fire, as well as the move left or right `

`     LDA  INPUTCHECK`

`      `

`     AND  #INPUTFLAG_FIRE`

`     BEQ  KMP_Left`

`     ; check to see if bullet already active...`

`     LDA  PLAYER_BULLET_Y`

`     CMP  #$ff`

`     BNE  KMP_Left`

`      `

`     JMP  Invader_Player.Player_BulletStart `

`   KMP_Left:`

`     LDA  INPUTCHECK`

`     AND  #INPUTFLAG_LEFT`

`     BNE  __playerleft`

`     LDA  INPUTCHECK`

`     AND  #INPUTFLAG_RIGHT`

`     BNE  __playerright`

`   KMP_End:`

`     LDA  #0`

`     STA  INPUTCHECK`

`     rts`

`   __playerleft:`

`    LDA   PLAYER_X`

`     SEC`

`     SBC   #1`

`     CMP   #PLAYER_LEFT_LIMIT`

`     BPL   __playerupdate`

`     LDA   #PLAYER_LEFT_LIMIT`

`   __playerupdate:`

`     STA   PLAYER_X`

`     TAX`

`     LDA   #PLAYER_SPRITE_SLOT`

`     LDY   PLAYER_Y`

`     JMP   SpriteController.SpriteMoveSprite    `

`      `

`   __playerright:`

`     LDA   PLAYER_X`

`     CLC`

`     ADC   #1`

`     CMP   #PLAYER_RIGHT_LIMIT`

`     BCC   __playerupdate`

`     LDA   #PLAYER_RIGHT_LIMIT`

`     JMP   __playerupdate  `

**Keyboard_Init** clears the INPUTCHECK

`   ;-------------------------------------------------------------------------------`

`   ; Keyboard_Init - `

`   ;     inits the keyboard...`

`   ;`

`   ;-------------------------------------------------------------------------------`

`   Keyboard_Init:`

` `

`     LDA  #0`

`     STA  INPUTCHECK`

`     RTS`

`   ;-------------------------------------------------------------------------------`

`   ; End of keyboard`

`   ;-------------------------------------------------------------------------------`

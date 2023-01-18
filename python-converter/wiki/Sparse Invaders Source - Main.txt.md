# Sparse Invaders Main.txt

This is the main entry point for Invaders. At the top of this file, please note the **.merge** commands to load in the other source. Please refer to SWIFT help, however this is a very good feature, allowing moduled code development and when calling functions you will note the prefix (file name) before the function name. Allow flexable function names and is more readable.

`   ;-------------------------------------------------------------------------------`
`   ;  Main  - Invaders ...`
`   ;  Written by Neil Beresford.`
`   ;`
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
`   `
`   .ORG $0900                         ; Good place to start, so it fits ...`
`   ;.ORG $0900`
`   `
`   .require "Constands"               ; BBC and general constants`
`   .require "Macros"                  ; general macros`
`   `
`   .merge   "ScreenFunctionality"     ; screen functionality`
`   .merge   "SpriteController"        ; Sprite controller and drawer`
`   ;.merge   "FileLoad"                ; File System loading `
`   ;.merge   "Debug"                   ; debug functionality`
`   .merge   "Timer"                   ; VSync timer`
`   .merge   "Keyboard"                ; Keyboard handling`
`   .merge   "Invader_Player"          ; Invader code - player setup`
`   .merge   "BlockDrawer"             ; Block Drawer ...`
`   .merge   "Invader_Baddies"         ; Baddies for the invader game`
`   .merge   "Invader_Bullets"         ; Baddie bullets`
`   .merge   "Invader_Bases"           ; Bases, logic and drawing...`
`   .merge   "Invader_Hiscore"         ; Hiscore display...`
`   .merge   "Sound"                   ; Sound init and generation...`

**Main** is the starting point (0x900), this initializes the sound, video, keyboard and timer etc.

`   ;-------------------------------------------------------------------------------`
`   ;  Main - `
`   ;     Main Entry Point`
`   ;-------------------------------------------------------------------------------`
`   `
`   Main:`
`  `
`      ; initialization of the system...`
`      jsr  Sound._INITSOUND`
``       `MODE 2 ``
``       `CURSOROFF ``
`   `
`   `
`      jsr  ScreenFunctionality.Screen_Clear   ; clear the screen...`
`   `
`   `
`      jsr  SpriteController.SpriteInit          ; init the sprite system`
`   `
`      jsr  BlockDrawer.BlockInit                ; init the block system`
`      jsr  Keyboard.Keyboard_Init               ; setup the keyboard handling`
`   `
`   `
`      jsr  Timer.Timer_Init                     ; set the user timer off to handle VBlanks our own way...`
`      jsr  Invader_Hiscore.Invader_Hiscore_Init ; init the hiscore, only done here to allow the score to be kept between games`
`   `
`      LDA  #0`
`      STA  FIREBUTTON_DELAY`

**main\_restart** main drops through into 'main\_restart'. At this point the game is setup, so this is a good point to jump to upon game over.

Intro screen is displayed, followed by start level screen - then clears and draws the score, life, invaders and bases.

`   main_restart:`
`   `
`      LDA #0       ;fire bullet`
`      JSR Sound._MAKE_SOUND`
`     `
`      jsr  ScreenFunctionality.Screen_Clear  ; Display main message...`
`      jsr  Invader_Player.Player_GameMessage`
`      jsr  ScreenFunctionality.Screen_Clear  ; clear the screen...`
`   `
`      LDA #0       ;fire bullet`
`      JSR Sound._MAKE_SOUND`
`   `
`      ; main game initialization`
`      jsr  Invader_Baddies.BaddiesNewGame     ; initializes a new game`
`      jsr  Invader_Bases.Init`
`   `
`      jsr  Invader_Player.PlayerInit          ; initialize the player, `
`      jsr  Invader_Baddies.BaddiesInit`
`          `
`      jsr  Invader_Player.Player_StartLevel`
`      jsr  ScreenFunctionality.Screen_Clear   ; clear the screen...`
`      LDA   #100`
`      STA   FIREBUTTON_DELAY`
`   `
`      ; pre-draw the screen ...`
`      jsr  ScreenFunctionality.DrawScore      ; draw score and lifes`
`      jsr  Invader_Baddies.BaddiesDraw        ; draw the invaders`
`      jsr  Invader_Bases.DrawBases            ; draw the bottom bases`
`   `
`      LDA #0       ;fire bullet`
`      JSR Sound._MAKE_SOUND`
`      `

**main\_loop** is the main game loop. It basically does the following

-   Sprite Draw
-   Game Logic
-   Sprite Wipe

Please note the commented out macros that change the background colour. This allows for timing of functionality, I used to this when sorting out the game so it ran in one game timer frame. Once the game logic has been processed the loop waits for a vertical blank before removing the sprites.

`   main_loop: `
`   `
`      ;`
`      ;  Please note the importance of the spritewipe being just`
`      ;  before the spritedraw and where the vsync timer flag is `
`      ;  placed...`
`      ;`
`   `
``    ;;   `BORDERCOLOUR 2 ``
`   `
`      jsr  SpriteController.SpritesDrawActive `
`   `
``    ;;   `BORDERCOLOUR 3 ``
`   `
`      jsr  keyboard.Keyboard_checkkeys`
`      jsr  keyboard.Keyboard_MovePlayer`
`      jsr  Invader_Baddies.BaddiesUpdate`
`      jsr  Invader_Baddies.BaddiesUpdateMother`
`      jsr  Invader_Player.Player_BulletMove`
`      jsr  ScreenFunctionality.UpdateScreen`
`   `
`      jsr  Invader_Baddies.BaddiesGeneralUpdate`
`   `
``    ;;   `BORDERCOLOUR 0 ``
`   `
`      LDA  #0`
`      STA  TIMER_FLAG`
`   VB:`
`      LDA  TIMER_FLAG`
`      BEQ  VB`
`      LDA  #0`
`      STA  TIMER_FLAG`
`   `
``    ;;   `BORDERCOLOUR 1 ``
`    `
`      jsr  SpriteController.SpritesWipeActive `
`      jsr  Invader_Bullets.Control`
`   `
`      jmp  main_loop`
`      `
`   end:   `
`      rts`
`      `
`   `
`   `
`   ;-------------------------------------------------------------------------------`
`   ;-------------------------------------------------------------------------------`
`   ; End of Main`
`   ;-------------------------------------------------------------------------------`

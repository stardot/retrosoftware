## Sparse Invaders Source - Constants.txt

`   ;-------------------------------------------------------------------------------`

`   ;  Constants`

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

`   ;   Notes:`

`   ;`

`   ;-------------------------------------------------------------------------------`

`   `

`   .alias oswrch $ffee`

`   .alias osbyte $fff4`

`   .alias osword $fff1`

`   `

`   ;-------------------------------------------------------------------------------`

`   ; General System related constances`

`   ;-------------------------------------------------------------------------------`

`   `

`   .alias SCREENHIGH     $30     ; screen start - high byte`

`   .alias SCREENLOW      $00     ; screen start - low byte`

`   `

`   .alias  KEYCODE_LEFT  $61  ; z key      -$19     ; keys used - left`

`   .alias  KEYCODE_RIGHT $42  ; x key      -$79     ; right key`

`   .alias  KEYCODE_SPACE $49  ; Return key -$62     ; space fire key`

`   `

`   ;-------------------------------------------------------------------------------`

`   ;`

`   ;  Zero page usage ...`

`   ;  Please note, never assume that these are setup`

`   ;  as you left them.`

`   ;`

`   ;-------------------------------------------------------------------------------`

`   `

`   `

`   .alias STOREA               $0C  ; general store  for A`

`   .alias STOREX               $0D  ; general store  for X`

`   .alias STOREY               $0E  ; general store  for Y`

`   .alias ACTIVEINDEX          $0F  ; active index, used when drawing the sprite via the active sprite control system`

`   .alias SCREENADD            $10  ; ( and $71 ) - Screen address`

`   .alias SPRITE               $12  ; current sprite`

`   .alias WIDTH                $13  ; width, generally the sprite`

`   .alias HEIGHT               $14  ; height, generally the sprite`

`   .alias XPOS                 $15  ; xpos store`

`   .alias YPOS                 $16  ; ypos store`

`   .alias TEMP                 $17  ; temp`

`   .alias CURRENTSPRITEDATA    $18  ; ( and $79 ) used for storing the address of the data for the current sprite `

`   .alias XOFFSET              $1A  ; x offset within the charactor, used for sprite draw`

`   .alias SCRATCH1             $1B  ; scratch`

`   .alias SCRATCH2             $1C  ; scratch`

`   .alias SCRATCH3             $1D  ; scratch`

`   .alias SCRATCH4             $1E  ; scratch`

`   .alias TEMPPTR              $1F  ; ( and $80 ) general purpose ptr`

`   .alias USERPTR              $21  ; ( and $82 ) userptr, used when calling functions `

`   .alias CURRENT_SPR_W        $23  ; current sprite width`

`   .alias CURRENT_SPR_H        $24  ; current sprite height`

`   .alias SCREENADD_BACK       $25  ; ( and $86 ) - Screen address`

`   .alias TIMERCOUNT           $27  ; TImer count - do not use!`

`   .alias TIMER_FLAG           $28  ; TImer flagged - do not write to!`

`   .alias PLAYER_X             $29  ; Player X position`

`   .alias PLAYER_Y             $30  ; Player X position`

`   .alias PLAYER_FRAME         $31  ; Player Frame`

`   .alias PLAYER_BULLET_X      $32  ; Player - Bullet x`

`   .alias PLAYER_BULLET_Y      $33  ; Player - Bullet y`

`   .alias PLAYER_BULLET_F      $34  ; Player - Bullet frame`

`   .alias INPUTCHECK           $35  ; keyboard input flags`

`   .alias SCREEN_UPDATE        $36  ; Screen update counter`

`   .alias SCORE_ADDITION       $37  ; Score addition`

`   .alias INV_DELAYCOUNT       $38  ; Invader frame count`

`   .alias INV_DELAYUPDATE      $39  ; Invader frame refresh value`

`   .alias INV_FRAME            $3a  ; Invader frame reference`

`   .alias INV_MOVDIR           $3b  ; horizontal movement for the invader...`

`   .alias INV_YMOVDIR          $3c  ; vertical movement for the invader...`

`   .alias EXPLOSION_COUNT      $3d  ; expolosion time on screen`

`   .alias EXPLOSION2_COUNT     $3e  ; expolosion2 time on screen`

`   .alias INVADER_RESTARTDELAY $3f  ; invader restart delay...`

`   .alias TOTAL_INVADERS       $40  ; total invaders`

`   .alias CALLPARAM1           $41  ; call param1`

`   .alias CALLPARAM2           $42  ; call param1`

`   .alias GAME_LEVEL           $43  ; game level ...`

`   .alias BULLET_COUNT         $44  ; total invader bullet count`

`   .alias BULLET_DELAY         $45  ; invader bullet delay`

`   .alias BULLET_REFRESHDELAY  $46  ; invader bullet frefresh for delay`

`   .alias BULLETINVLAST        $47  ; current invader that has fired...`

`   .alias GAME_STATE           $48  ; Game state ... `

`   .alias INV_PICKED1          $49  ; invader picked via invader bullet shooting`

`   .alias INV_PICKED2          $4a  ; invader picked via invader bullet shooting`

`   .alias INV_PICKED3          $4b  ; invader picked via invader bullet shooting`

`   .alias CURRENT_SPRITE       $4c  ; current sprite reference number for the spritedata`

`   .alias PLAYER_LIFES         $4d  ; number of player lifes left ...`

`   .alias BASE1_1              $4e  ; Base mask for line. <<^^>> - 6 bits for the three blocks per line `

`   .alias BASE1_2              $4f  ;`

`   .alias BASE1_3              $50  ;`

`   .alias BASE2_1              $51  ;`

`   .alias BASE2_2              $52  ;`

`   .alias BASE2_3              $53  ;`

`   .alias BASE3_1              $54  ;`

`   .alias BASE3_2              $55  ;`

`   .alias BASE3_3              $56  ;`

`   .alias SCREENPTR            $57  ; screen data ptr lo`

`   .alias SCREENPTR2           $58  ; screen data ptr hi `

`   .alias DELAY_COUNT          $59  ; delay for the menu ...`

`   .alias FIREBUTTON_DELAY     $5a  ; stop firing ...`

`   .alias BASELINEFLAG         $5b  ; flag for blanked lines etc ...`

`   .alias SCORE_LO             $5c  ; score - lo byte`

`   .alias SCORE_HI             $5d  ; score - hi byte`

`   .alias BONUSSCORE_LO        $5e  ; bonushiscore - lo byte - to aim for for bonus life`

`   .alias BONUSSCORE_HI        $5f  ; bonushiscore - hi byte`

`   `

`   .alias HISCORE1_LO          $60  ;  Hi score store`

`   .alias HISCORE1_HI          $61  ;  ...`

`   .alias HISCORE2_LO          $62  ;  ...`

`   .alias HISCORE2_HI          $63  ;  ...`

`   .alias HISCORE3_LO          $64  ;  ...`

`   .alias HISCORE3_HI          $65  ;  ...`

`   .alias HISCORE4_LO          $66  ;  ...`

`   .alias HISCORE4_HI          $67  ;  ...`

`   .alias HISCORE5_LO          $68  ;  ...`

`   .alias HISCORE5_HI          $69  ;  ...`

`   .alias HISCORE6_LO          $6a  ;  ...`

`   .alias HISCORE6_HI          $6b  ;  ...`

`   .alias HISCORE7_LO          $6c  ;  ...`

`   .alias HISCORE7_HI          $6d  ;  ...`

`   .alias HISCORE8_LO          $6e  ;  ...`

`   .alias HISCORE8_HI          $6f  ;  ...`

`   .alias HISCORE9_LO          $70  ;  ...`

`   .alias HISCORE9_HI          $71  ;  ...`

`   .alias HISCORE10_LO         $72  ;  ...`

`   .alias HISCORE10_HI         $73  ;  ...`

`   .alias MISSFIRSTSOUND       $76  ; Miss the first sound...`

`   `

`   ;-------------------------------------------------------------------------------`

`   ;  Constants used for monitoring the GAME STATE`

`   ;-------------------------------------------------------------------------------`

`   `

`   .alias  GAME_STATE_INTRO       0  ; game state - intro screen`

`   .alias  GAME_STATE_STARTLEVEL  1  ; starting level screen`

`   .alias  GAME_STATE_PLAYING     2  ; playing game`

`   .alias  GAME_STATE_INVADED     3  ; game ended.`

`   `

`   ;-------------------------------------------------------------------------------`

`   ;  Constants used within Invader_Player`

`   ;-------------------------------------------------------------------------------`

`   `

`   .alias  INPUTFLAG_LEFT       1    ; flag for player movement left`

`   .alias  INPUTFLAG_RIGHT      2    ; flag for player movement right`

`   .alias  INPUTFLAG_FIRE       4    ; flag for when player fires`

`   `

`   .alias  PLAYER_SPRITE_SLOT     0  ; sprite slot allocation - player`

`   .alias  BULLET_SPRITE_SLOT     1  ;   ... player bullet`

`   .alias  EXPLOSION_SPRITE_SLOT  2  ;   ... explosion for invader`

`   .alias  EXPLOSION2_SPRITE_SLOT 3  ;   ... explosion for mothership`

`   .alias  INVBULLET1_SPRITE_SLOT 4  ;   ...  invader bullet 1`

`   .alias  INVBULLET2_SPRITE_SLOT 5  ;   ...  invader bullet 2`

`   .alias  INVBULLET3_SPRITE_SLOT 6  ;   ...  invader bullet 3`

`   `

`   .alias  PLAYER_STARTX        38   ;  player starting and movement limits`

`   .alias  PLAYER_STARTY        220  ;  ...`

`   .alias  PLAYER_LEFT_LIMIT    4    ;  ...`

`   .alias  PLAYER_RIGHT_LIMIT   73   ;  ...`

`   `

`   .alias  INV_MODE_STARTUP     0    ; invader states - startup`

`   .alias  INV_MODE_WALKLEFT    1    ; invaders move left`

`   .alias  INV_MODE_WALKRIGHT   2    ; invaders move right`

`   .alias  INV_MODE_WALKDOWN    3    ; invaders move down`

`   .alias  INV_MODE_INVADED     4    ; invaders won!!`

`   `

`   .alias  INV_STATE_DEAD       0    ; indivual invader state - dead`

`   .alias  INV_STATE_ACTIVE     1    ; active`

`   .alias  INV_STATE_REMOVE     2    ; killed, awaiting to be removed`

`   `

`   .alias  ONE_HALF_SEC_DELAY   50   ; used for delay ... Err, change value so less! `

`   `

`   `

`   ;-------------------------------------------------------------------------------`

`   ;  Constants used within SpriteController`

`   ;-------------------------------------------------------------------------------`

`   `

`   .alias TOTAL_SPRITES           8   ; total sprite - PLEASE remember to recalc the total_sprite_space`

`   .alias SIZEOF_SPRITE_BLOCK     16   ; see above ... `

`   .alias TOTAL_ACTIVE_SPRITES    8    ; toal active sprites - PLEASE remember to adjust the slots in memory`

`   .alias TOTAL_SPRITE_SPACE      128  ; TOTAL_SPRITES*SIZEOF_SPRITE_BLOCK`

`   `

`   .alias SPRBLK_X                0    ; sprite block data - sprite x position`

`   .alias SPRBLK_Y                1    ; y position`

`   .alias SPRBLK_FRAME            2    ; frame (sprite)`

`   .alias SPRBLK_CTRL             3    ; ctrl function - if non-zero, called every draw`

`   .alias SPRBLK_CTRL1            4    ; ...`

`   .alias SPRBLK_XOFFSET          5    ; internal sprite drawer  xoffset`

`   .alias SPRBLK_SCREENADD        6    ; internal sprite drawer  screen address`

`   .alias SPRBLK_SCREENADD2       7    ; ... `

`   .alias SPRBLK_WIDTH            8    ; sprite width ( in 2pixel steps )`

`   .alias SPRBLK_HEIGHT           9    ; sprite height`

`   .alias SPRBLK_FLAG             10   ; sprite flags for drawing etc - see below`

`   .alias SPRBLK_SPRDATA          11   ; internal sprite drawer - gfx data`

`   .alias SPRBLK_SPRDATA2         12   ; ...`

`   .alias SPRBLK_SCRBACK          13   ; internal sprite drawer - backup for screen address`

`   .alias SPRBLK_SCRBACK2         14   ; ...`

`   .alias SPRBLK_XOFFBACK         15   ; internal sprite drawer - backup for xoffset`

`   `

`   .alias SPRDATA_WIDTH           0    ; sprite data defines`

`   .alias SPRDATA_HEIGHT          1`

`                                       ; flags for the sprite system ...`

`   .alias SPRFLAG_DISABLED        $00  ; not bit flag - if whole byte zero - disabled`

`   .alias SPRFLAG_ACTIVE          $01  ; bit 01 - sprite Active...`

`   .alias SPRFLAG_DISPLAYED       $02  ; bit 02 - sprite in display list...`

`   .alias SPRFLAG_REDRAW          $04  ; bit 03 - sprite needs redrawing...`

`   .alias SPRFLAG_KILL            $08  ; bit 04 - makrs the sprite to be removed from active list`

`   `

`   .alias SPRFLAG_NOT_REDRAW      $fb  ; NOT bit 03 - sprite needs redrawing...`

`   `

`   ;-------------------------------------------------------------------------------`

`   ;  End of Constants`

`   ;-------------------------------------------------------------------------------`

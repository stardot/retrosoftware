## Sparse Invaders Source - Invader\_Hiscore.txt

`   ;-------------------------------------------------------------------------------`
`   ;  Invader_Hiscore`
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
`   ;-------------------------------------------------------------------------------`
`   ;  Calculations etc`
`   ;-------------------------------------------------------------------------------`
`   `
`   ;-------------------------------------------------------------------------------`
`   ;  Invader_CheckScore:`
`   ;    Converts the hiscore to string ....`
`   ;       X - LO byte hiscore`
`   ;       y - HI byte hiscore`
`   ; RETURNS - C set if added.`
`   ;-------------------------------------------------------------------------------`
`   Invader_CheckScore:`
`   `
`     STX  SCRATCH1`
`     STY  SCRATCH2`
`   `
`     ; index for comparing the numbers, starting at the bottom ...`
`     LDX  #19`
`     LDY  #0`
`   `
`   ICS_checkPos:`
`   `
`     STX  SCRATCH4`
`     `
`     LDA  SCRATCH2`
`     CMP  HISCORE1_LO,X`
`     BCC  ICS_Checked`
`     BNE  ICS_itshigh`
`     DEX`
`     LDA  SCRATCH1`
`     CMP  HISCORE1_LO,X`
`     BCC  ICS_Checked`
`   `
`   ICS_itshigh:`
`   `
`     INY`
`   `
`     LDX  SCRATCH4`
`     DEX`
`     DEX`
`     CPX  #$fe`
`     BPL  ICS_checkPos`
`   `
`   ICS_Checked:`
`   `
`     CPY  #0`
`     BNE  ICS_add  `
`     `
`   ICS_notadded:`
`   `
`     CLC  `
`     RTS`
`   `
`   ICS_Add:`
`   `
`     DEY`
`   `
`     LDA  #HISCORE9_LO`
`     STA  USERPTR`
`     LDA  #HISCORE10_LO`
`     STA  TEMPPTR`
`     LDA  #0`
`     STA  USERPTR+1`
`     STA  TEMPPTR+1`
`   `
`     STY  SCRATCH3`
`     TYA`
`     TAX`
`   `
`   ICS_MoveScoreDown:`
`   `
`     LDY  #0`
`     LDA  (USERPTR),Y`
`     STA  (TEMPPTR),Y`
`     INY`
`     LDA  (USERPTR),Y`
`     STA  (TEMPPTR),Y`
`   `
`     LDA  USERPTR`
`     SEC`
`     SBC  #2`
`     STA  USERPTR`
`     `
`     LDA  TEMPPTR`
`     SEC`
`     SBC  #2`
`     STA  TEMPPTR`
`     `
`     DEX`
`     BNE  ICS_MoveScoreDown`
`           `
`     ; now store the score in the new free slot...`
`     LDY  #0`
`     LDA  SCRATCH3`
`     ASL`
`     STA  SCRATCH3`
`     LDA  #HISCORE10_LO`
`     SEC`
`     SBC  SCRATCH3`
`     STA  USERPTR     ; note, hi byte already cleared`
`     LDA  SCRATCH1`
`     STA  (USERPTR),Y`
`     INY`
`     LDA  SCRATCH2`
`     STA  (USERPTR),Y`
`             `
`     ; set the carry, stored the new hiscore ...`
`     SEC`
`     RTS`
`   `
`     `
`          `
`   `
`   `
`   `
`   `
`   `
`   ;-------------------------------------------------------------------------------`
`   ;  Invader_HS_ConvertString:`
`   ;    Converts the hiscore to string ....`
`   ;    this is th old fastioned way, I know using`
`   ;    ALso, this is totally un-optimised, I just got`
`   ;    it to work. BCD would be quicker, but this is good practise for me!`
`   ;       X - LO byte hiscore`
`   ;       y - HI byte hiscore`
`   ; USERPTR - pointer to string`
`   ;-------------------------------------------------------------------------------`
`   Invader_HS_ConvertString:`
`   `
`     `
`     STX  SCRATCH1`
`     STY  SCRATCH2  `
`   `
`   `
`   `
`     ; this assumes the score is limited to 9999`
`     ; do thousands ...`
`     `
`     LDA  #<1000`
`     STA  SCRATCH3`
`     LDA  #>1000`
`     STA  SCRATCH4`
`     LDY  #2`
`     LDX  #48`
`   `
`   IHS_thousands:`
`   `
`     LDA  SCRATCH2`
`     CMP  SCRATCH4`
`     BCC  IHS_dohundreds  `
`     BNE  IHS_thousandssub`
`     LDA  SCRATCH1`
`     CMP  SCRATCH3`
`     BCC  IHS_dohundreds  `
`   `
`   IHS_thousandssub:`
`   `
``      `SUB16BIT  SCRATCH1,SCRATCH3,SCRATCH1 ``
`   `
`     INX  `
`     JMP  IHS_thousands`
`   `
`   IHS_dohundreds:`
`   `
`     TXA`
`     STA  (USERPTR),Y  `
`   `
`     LDA  #<100`
`     STA  SCRATCH3`
`     LDA  #>100`
`     STA  SCRATCH4`
`     INY`
`     LDX  #48`
`   `
`   IHS_Hundreds:`
`   `
`     LDA  SCRATCH2`
`     CMP  SCRATCH4`
`     BCC  IHS_dotens  `
`     BNE  IHS_hundredsssub`
`     LDA  SCRATCH1`
`     CMP  SCRATCH3`
`     BCC  IHS_dotens  `
`   `
`   IHS_hundredsssub:`
`   `
``      `SUB16BIT  SCRATCH1,SCRATCH3,SCRATCH1 ``
`   `
`     INX   `
`     JMP  IHS_Hundreds`
`   `
`   IHS_dotens:`
`   `
`     TXA`
`     STA  (USERPTR),Y  `
`   `
`     LDA  #10`
`     STA  SCRATCH3`
`     INY`
`     LDX  #48`
`   `
`   IHS_tens:`
`   `
`     LDA  SCRATCH1`
`     CMP  SCRATCH3`
`     BCC  IHS_dounits  `
`   `
`     LDA  SCRATCH1`
`     SEC`
`     SBC  #10`
`     STA  SCRATCH1`
`   `
`     INX`
`     JMP  IHS_tens`
`   `
`   IHS_dounits:`
`   `
`     TXA`
`     STA  (USERPTR),Y  `
`   `
`     INY`
`     LDA  #48`
`     CLC`
`     ADC  SCRATCH1`
`     STA  (USERPTR),Y  `
`   `
`   `
`     RTS`
`   `
`   `
`   `
`   `
`   ;-------------------------------------------------------------------------------`
`   ;  Setup and display`
`   ;-------------------------------------------------------------------------------`
`   `
`   ;-------------------------------------------------------------------------------`
`   ;  Invader_Hiscore_Init:`
`   ;    initializes the hiscore system...`
`   ;-------------------------------------------------------------------------------`
`   Invader_Hiscore_Init:`
`   `
`     ; set the hiscore table ... nice!`
`     LDx  #<2000 `
`     LDY  #>2000 `
`     STX  HISCORE1_LO`
`     STY  HISCORE1_HI`
`     LDx  #<1300 `
`     LDY  #>1300 `
`     STX  HISCORE2_LO`
`     STY  HISCORE2_HI`
`     LDx  #<1200 `
`     LDY  #>1200 `
`     STX  HISCORE3_LO`
`     STY  HISCORE3_HI`
`     LDx  #<1100 `
`     LDY  #>1100 `
`     STX  HISCORE4_LO`
`     STY  HISCORE4_HI`
`     LDx  #<1000 `
`     LDY  #>1000 `
`     STX  HISCORE5_LO`
`     STY  HISCORE5_HI`
`     LDx  #<900 `
`     LDY  #>900 `
`     STX  HISCORE6_LO`
`     STY  HISCORE6_HI`
`     LDx  #<800 `
`     LDY  #>800 `
`     STX  HISCORE7_LO`
`     STY  HISCORE7_HI`
`     LDx  #<700 `
`     LDY  #>700 `
`     STX  HISCORE8_LO`
`     STY  HISCORE8_HI`
`     LDx  #<600 `
`     LDY  #>600 `
`     STX  HISCORE9_LO`
`     STY  HISCORE9_HI`
`     LDx  #<500 `
`     LDY  #>500 `
`     STX  HISCORE10_LO`
`     STY  HISCORE10_HI`
`   `
`     RTS`
`   `
`   ;-------------------------------------------------------------------------------`
`   ;  Invader_Hiscore_Display:`
`   ;    Displays the  the hiscore screen...`
`   ;-------------------------------------------------------------------------------`
`   Invader_Hiscore_Display:`
`   `
`   `
`     JSR  ScreenFunctionality.Screen_Clear`
`   `
`     ; setup the hiscores ...`
`   ;  JSR  Invader_Hiscore_SetStrings`
`   `
`   `
`   `
`   `
`     ; display the title ...`
`     LDA  #`<HSTitle1
      STA  USERPTR 
      LDA  #>`HSTitle1`
`     STA  USERPTR+1`
`     JSR  ScreenFunctionality.Screen_PositionedMessage`
`   `
`     ; display the scores`
`     LDX  HISCORE1_LO`
`     LDY  HISCORE1_HI`
`     LDA  #`<HSstring1
      STA  USERPTR
      LDA  #>`HSstring1`
`     STA  USERPTR+1`
`   `
`     JSR  Invader_HS_ConvertString`
`     LDA  #5`
`     STA  HSstring1+1  `
`     JSR  ScreenFunctionality.Screen_PositionedMessage`
`   `
`     LDX  HISCORE2_LO`
`     LDY  HISCORE2_HI`
`     JSR  Invader_HS_ConvertString`
`     LDA  #7`
`     STA  HSstring1+1  `
`     JSR  ScreenFunctionality.Screen_PositionedMessage`
`   `
`     LDX  HISCORE3_LO`
`     LDY  HISCORE3_HI`
`     JSR  Invader_HS_ConvertString`
`     LDA  #9`
`     STA  HSstring1+1  `
`     JSR  ScreenFunctionality.Screen_PositionedMessage`
`   `
`     LDX  HISCORE4_LO`
`     LDY  HISCORE4_HI`
`     JSR  Invader_HS_ConvertString`
`     LDA  #11`
`     STA  HSstring1+1  `
`     JSR  ScreenFunctionality.Screen_PositionedMessage`
`   `
`     LDX  HISCORE5_LO`
`     LDY  HISCORE5_HI`
`     JSR  Invader_HS_ConvertString`
`     LDA  #13`
`     STA  HSstring1+1  `
`     JSR  ScreenFunctionality.Screen_PositionedMessage`
`   `
`     LDX  HISCORE6_LO`
`     LDY  HISCORE6_HI`
`     JSR  Invader_HS_ConvertString`
`     LDA  #15`
`     STA  HSstring1+1  `
`     JSR  ScreenFunctionality.Screen_PositionedMessage`
`   `
`     LDX  HISCORE7_LO`
`     LDY  HISCORE7_HI`
`     JSR  Invader_HS_ConvertString`
`     LDA  #17`
`     STA  HSstring1+1  `
`     JSR  ScreenFunctionality.Screen_PositionedMessage`
`   `
`     LDX  HISCORE8_LO`
`     LDY  HISCORE8_HI`
`     JSR  Invader_HS_ConvertString`
`     LDA  #19`
`     STA  HSstring1+1  `
`     JSR  ScreenFunctionality.Screen_PositionedMessage`
`   `
`     LDX  HISCORE9_LO`
`     LDY  HISCORE9_HI`
`     JSR  Invader_HS_ConvertString`
`     LDA  #21`
`     STA  HSstring1+1  `
`     JSR  ScreenFunctionality.Screen_PositionedMessage`
`   `
`     LDX  HISCORE10_LO`
`     LDY  HISCORE10_HI`
`     JSR  Invader_HS_ConvertString`
`     LDA  #23`
`     STA  HSstring1+1  `
`     JSR  ScreenFunctionality.Screen_PositionedMessage`
`   `
`     LDA  #100`
`     STA  DELAY_COUNT`
`     JSR  Invader_Player.PGM_waitFire`
`   `
`     RTS`
`     `
`   `
`   `
`   ;-------------------------------------------------------------------------------`
`   ; Strings for displaying the hiscore...`
`   ;-------------------------------------------------------------------------------`
`   `
`   HSTitle1:    .byte  2,2,"high score table",0`
`   HSstring1:   .byte  8,5`
`   HSstring_1:  .byte  "0000",0`
`   `
`   `
`   ;-------------------------------------------------------------------------------`
`   ;   End of Invader_Hiscore`
`   ;-------------------------------------------------------------------------------`

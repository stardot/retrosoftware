## Sparse Invaders Source - Timer.txt

The following Timer functionality handles the vertical blank triggering, it triggers at the bottom of visiable screen setting a flag once reached. This code is quite well documented, however please refer to the advanced BBC B manual as to the workings of the timers.

`   ;-------------------------------------------------------------------------------`
`   ;  Timer Interrupt`
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
`   ;   The timer times out at $4730, this corrasponds to the bottom of the screen`
`   ;   give or take a scan line. Once timed, this inc TIMER_FLAG.`
`   ;   On the VBlank interrupt, this activates the timer again. `
`   ;`
`   ;   Functionality...`
`   ;`
`   ;   External - Setup`
`   ;   Timer_Init            - starts the interrupt off, activating the timer`
`   ;`
`   ;   Internal -`
`   ;   Timer_IRQCheck        - checks to see if VB or timer2 then acts on it...`
`   ;        TI_VSync         - restarts user timer2`
`   ;        TI_Timer         - inc timer flag`
`   ;`
`   ;-------------------------------------------------------------------------------`
`   .require "Constands"`
`   .require "Macros"`
`   ;-------------------------------------------------------------------------------`
` `
`   ;-------------------------------------------------------------------------------`
`   ;  Timer_Init - `
`   ;`
`   ;     Activates the interrupt handler that on the next VBlank - will`
`   ;     start the timer, so allowing monitoring when the scan line reaches the`
`   ;     bottom edge of the screen`
`   ;`
`   ;-------------------------------------------------------------------------------`
`   Timer_Init:`
`      ; reset the timer flag`
`      LDA  #0`
`      STA  TIMER_FLAG`
`      ; Stop interrupts as we change the interrupt handler ...`
`      SEI`
`      ; store the old interrupt handler`
`      LDA  $204`
`      STA  OldInt`
`      LDA  $205`
`      STA  OldInt+1`
`      ; patch in our interrupt handler`
`      LDA  #`<Timer_IRQCheck
       STA  $204
       LDA  #>`Timer_IRQCheck`
`      STA  $205`
`      `
`      ; sets user timer 2 mode to countdown`
`      LDA  #0`
`      STA  $FE6B`
`      `
`      CLI`
`      RTS`
`   ;-------------------------------------------------------------------------------`
`   OldInt:                  ; Store for old handler ...`
`      .byte 0,0   `
`   ;-------------------------------------------------------------------------------`
`   ;-------------------------------------------------------------------------------`
`   ;  Timer_IRQCheck - `
`   ;`
`   ;   Chceks for timer2 and VBlank.. Timer2 inc timer_flag, VBlank re-activates`
`   ;   timer2 `
`   ;`
`   ;-------------------------------------------------------------------------------`
`   Timer_IRQCheck:`
`      ; check the interrupt to see if we need to act on it...`
`      LDA  $FE4D                 ; check and jump to VBlank...`
`      AND  #2`
`      BNE  TI_VSync`
`      `
`      LDA  $FE6D                 ; check and jump to timer 2... `
`      AND  #$20`
`      BNE  TI_Timer`
`      ; jmp to the old interrupt handler...`
`      jmp  (OldInt)              ; let system handle others`
`   TI_VSync:`
`      ; reset the timer to trigger at bottom of screen... `
`      LDA  #$30`
`      STA  $FE68`
`      LDA  #$47`
`      STA  $FE69`
`      `
`      ; enable user timer 2 interrupts`
`      LDA  #$A0`
`      STA  $FE6E             `
`      ; jmp to the old interrupt handler...`
`      jmp  (OldInt)`
`   TI_Timer:`
`      ; handle the interrupt`
`      STA  $FE6D`
`      STA  $FE6E`
`      ; check standard delay and dec if needed...`
`      LDA  DELAY_COUNT`
`      BEQ  TI_Timercont`
`      DEC  DELAY_COUNT`
`   TI_Timercont:`
`      ; and set the timer flag ...`
`      INC  TIMER_FLAG`
`      ; update the counters for various game updates`
`      LDA  SCREEN_UPDATE`
`      BEQ  TIT_skipSU`
`      DEC  SCREEN_UPDATE`
`   TIT_skipSU:`
`      `
`      `
`      ; jmp to the old interrupt handler...`
`      jmp  (OldInt)`
`                   `
`   ;-------------------------------------------------------------------------------`
`   ; End of Timer`
`   ;-------------------------------------------------------------------------------`

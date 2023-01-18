## Sparse Invaders Source - Macros.txt

`   ;-------------------------------------------------------------------------------`

`   ;  Macros ...`

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

`   ;-------------------------------------------------------------------------------`

`   `

`   ;-------------------------------------------------------------------------------`

`   ; Mode change ...`

`   ; A trashed `

`   ;-------------------------------------------------------------------------------`

`   .macro MODE`

`      LDA #$16`

`      JSR oswrch`

`      LDA _1`

`      JSR oswrch`

`   .macend`

`   `

`   ;-------------------------------------------------------------------------------`

`   `

`   .macro CURSOROFF `

`      LDA #10`

`      STA $FE00`

`      LDA #32`

`      STA $FE01`

`   .macend`

`   `

`   `

`   ;-------------------------------------------------------------------------------`

`   .macro WAIT_VBLANK`

`      LDA #19`

`      jsr osbyte`

`   .macend`

`   `

`   ;-------------------------------------------------------------------------------`

`   ; PushRegs`

`   ;`

`   ;-------------------------------------------------------------------------------`

`   .macro PUSHREGS`

`      PHA            ; preserve the registers`

`      TXA`

`      PHA`

`      TYA`

`      PHA`

`   .macend`

`   `

`   ;-------------------------------------------------------------------------------`

`   ; PopRegs`

`   ;`

`   ;-------------------------------------------------------------------------------`

`   .macro POPREGS`

`      PLA            ; restore the regs`

`      TAY`

`      PLA`

`      TAX`

`      PLA`

`   .macend`

`   `

`   `

`   ;-------------------------------------------------------------------------------`

`   ;-------------------------------------------------------------------------------`

`   .macro CHECK_KEY  ; checks the key, trashes the regs ...`

`      LDA  #$81`

`      LDX  #0`

`      LDY  #0`

`      JSR  osbyte`

`      CPY  #0`

`   .macend`

`   `

`   `

`   ;-------------------------------------------------------------------------------`

`   ; Change background colour`

`   ;  _1 Colour to change to `

`   ;  all regs trashed...`

`   ;`

`   ;-------------------------------------------------------------------------------`

`   .macro BORDERCOLOUR`

`      lda #155`

`      ldx #_1`

`      jsr $fff4`

`   .macend`

`   `

`   ;-------------------------------------------------------------------------------`

`   ; Store16bit - _1 Value to be stored`

`   ;              _2 Place to store`

`   ;   A trashed`

`   ;`

`   ;-------------------------------------------------------------------------------`

`   .macro STORE16BIT`

`      LDA _1`

`      STA _2`

`      LDA _1+1`

`      STA _2+1`

`   .macend`

`   `

`   ;-------------------------------------------------------------------------------`

`   ; Add16bit - _1 Value 1`

`   ;            _2 Value 2`

`   ;            _3 Result`

`   ;   A trashed and also carry`

`   ;-------------------------------------------------------------------------------`

`   .macro ADD16BIT`

`      CLC             ;Ensure carry is clear`

`      LDA _1+0       ;Add the two least significant bytes`

`      ADC _2+0`

`      STA _3+0       ;... and store the result`

`      LDA _1+1       ;Add the two most significant bytes`

`      ADC _2+1       ;... and any propagated carry bit`

`      STA _3+1       ;... and store the result`

`   .macend`

`   `

`   ;-------------------------------------------------------------------------------`

`   ; Sub16bit - _1 Value 1`

`   ;            _2 Value 2`

`   ;            _3 Result`

`   ;   A trashed and also carry`

`   ;-------------------------------------------------------------------------------`

`   .macro SUB16BIT`

`      SEC             ;Ensure carry is clear`

`      LDA _1+0       ;Sub the two most significant bytes`

`      SBC _2+0`

`      STA _3+0       ;... and store the result`

`      LDA _1+1       ;sub the two least significant bytes`

`      SBC _2+1       ;... and any propagated carry bit`

`      STA _3+1       ;... and store the result`

`   .macend`

`   `

`   `

`   ;-------------------------------------------------------------------------------`

`   ; Multiply by 8 the 16bit contents in`

`   ;`

`   ;`

`   ;-------------------------------------------------------------------------------`

`   .macro MUL8`

`      CLC`

`      LDA _1`

`      ASL`

`      ROL _1+1`

`      ASL`

`      ROL _1+1`

`      ASL`

`      ROL _1+1`

`      STA _1`

`   .macend`

`   `

`   ;-------------------------------------------------------------------------------`

`   ; Multiply by 6  A and store in _1`

`   ;`

`   ;`

`   ;-------------------------------------------------------------------------------`

`   .macro MUL6`

`      ASL`

`      STA  _1`

`      ASL`

`      CLC`

`      ADC  _1`

`      STA  _1`

`   .macend`

`   `

`   ;-------------------------------------------------------------------------------`

`   ; Multiply by 3  A and store in _1`

`   ;`

`   ;`

`   ;-------------------------------------------------------------------------------`

`   .macro MUL3`

`      STA  _1`

`      ASL`

`      CLC`

`      ADC  _1`

`      STA  _1`

`   .macend`

`   `

`   ;-------------------------------------------------------------------------------`

`   ; Multiply by 5  A and store in _1`

`   ;`

`   ;`

`   ;-------------------------------------------------------------------------------`

`   .macro MUL5`

`      STA  _1`

`      ASL`

`      ASL`

`      CLC`

`      ADC  _1`

`      STA  _1`

`   .macend`

`   `

`   `

`   `

`   `

`   `

`   ;-------------------------------------------------------------------------------`

`   ; Multiply by 32 the 16bit contents in`

`   ;`

`   ;`

`   ;-------------------------------------------------------------------------------`

`   .macro MUL32`

`      CLC`

`      LDA _1`

`      ASL`

`      ROL _1+1`

`      ASL`

`      ROL _1+1`

`      ASL`

`      ROL _1+1`

`      ASL`

`      ROL _1+1`

`      ASL`

`      ROL _1+1`

`      STA _1`

`   .macend`

`   `

`   ;-------------------------------------------------------------------------------`

`   ; Divide by 6  A and store in _1`

`   ;`

`   ;`

`   ;-------------------------------------------------------------------------------`

`   .macro DIV6`

`      LSR`

`      STA  _1`

`      LSR`

`      SEC`

`      SBC  _1`

`      STA  _1`

`   .macend`

`   `

`   `

`   ;-------------------------------------------------------------------------------`

`   ; Multipy 8bit by 8, then add to 16bit address`

`   ; uses scratch reg temp($76) for uppper 8bits in`

`   ; multiply by 8`

`   ;`

`   ;-------------------------------------------------------------------------------`

`   .macro MUL8ADDTOADDRESS`

`      LDA  #0       ; multiply by 8`

`      STA  TEMP`

`      CLC`

`      ASL  _1`

`      ROL  TEMP`

`      ASL  _1`

`      ROL  TEMP`

`      ASL  _1`

`      ROL  TEMP`

`      LDA  _1       ; now the addition to the 16bit   `

`      CLC`

`      ADC  _2`

`      STA  _2`

`      LDA  TEMP`

`      ADC  _2+1`

`      STA  _2+1`

`   .macend  `

`   `

`   `

`   ;-------------------------------------------------------------------------------`

`   ;  Add A to 16bit value ...`

`   ;-------------------------------------------------------------------------------`

`   .macro ADDTO16BIT`

`      `

`      CLC`

`      ADC  _1`

`      STA  _1`

`      LDA  _1+1`

`      ADC  #0   `

`      STA  _1+1`

`   `

`   .macend`

`   `

`   `

`   `

`   ;-------------------------------------------------------------------------------`

`   ; End of Macros`

`   ;-------------------------------------------------------------------------------`

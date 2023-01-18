## Sparse Invaders Source - Relocate.txt

`   ;-------------------------------------------------------------------------------`
`   ;  Relocate`
`   ;  Written by Steve O'Leary`
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
`   .org $880        ; printer buffer`
`   `
`   Main:`
`   `
`   ; we have loaded the code at 1900 but it's been assembled to run from E00, so just copy`
`   ; the code from 1900 down to 900. We know it's length of the block we've loaded as Swift`
`   ; will tell you this from the properties of Sparse Invaders source file. You can `
`   ; also find it out by exmaining the disk image created. `
`   `
`   .alias LastAddress $1900+ $2200  ;  2200 is the size of our code,just setting address`
`                                    ; that we stop copying at when we reach it.`
`   `
`   `
`   `
`   CopyFrom:`
`   lda $1900`
`   CopyTo:`
`   sta $900`
`   inc CopyFrom+1                   ; lo byte`
`   bne NoCarry                      ; Not gone to zeror, so effectivly no carry`
`   `
`                                    ; If we get here however....`
`   inc CopyFrom+2                   ; add in the effective carry (note we use BEQ above to`
`                                    ; detect for rolling over from 255 to 0 as the command`
`                                    ; INC does not effect the carry flag. `
`    `
`   NoCarry:                                `
`   `
`   ; we now do the same increment for the copyto position`
`                                    `
`   inc CopyTo+1                   ; lo byte`
`   bne NoCarry2                      ; Not gone to zeror, so effectivly no carry`
`   `
`                                    ; If we get here however....`
`   inc CopyTo+2                     ; add in the effective carry (note we use BEQ above to`
`                                    ; detect for rolling over from 255 to 0 as the command`
`                                    ; INC does not effect the carry flag. `
`   `
`   NoCarry2:`
`   `
`   ; now wecheck if we've copied all the bytes`
`   lda CopyFrom+2                   ; check hi byte first`
`   cmp #>LastAddress`
`   BNE CopyFrom                      ; Go back to start of loop if not equal`
`   `
`   ; high byte is equal, check lo byte`
`   lda CopyFrom+1`
`   cmp #<LastAddress`
`   BNE CopyFrom                      ; if no equal, carry on copying`
`   `
`   ; we've finished copying all the bytes, run the code at the new address`
`   JSR $0900        ; start of code to run`
`   RTS`

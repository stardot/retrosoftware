# Detecting the TUBE

Not all software routines are compatible with the TUBE (e.g. the 6502 co-processor) in use so being able to check for this can be handy.

The code below will test for the TUBE and if detected notify the user and end the program. If the TUBE is not detected then the program will branch to the label 'routine' where your own code can go.

## The Code

<code >`  10 DIM mc% 100`

`  20 osasci=&FFE3`

`  30 osbyte=&FFF4`

`  40 FOR opt%=0 TO 2 STEP 2`

`  50 P%=mc%`

`  60[          OPT opt%`

`  70           LDA #&EA`

`  80           LDX #&00`

`  90           LDY #&FF`

` 100           JSR osbyte`

` 110           CPX #&00`

` 120           BEQ routine`

` 130           LDY #&00`

` 140.loop      LDA message,Y`

` 150           JSR osasci`

` 160           INY`

` 170           CMP #&0D`

` 180           BNE loop`

` 190           RTS`

` 200.message   EQUS "TUBE detected!"`

` 210           EQUB &0D`

` 220.routine   \ rest of program here`

` 230           RTS`

` 240]`

` 250 NEXT`

` 260 CALL mc%`

</code >

## Edit by J.G.Harston

The proper way is to detect which <i>side</i> of the Tube you are executing on. If you're executing in the I/O processor it's irrelavant whether there's a Tube active or not.

<code >` LDA #130:JSR OSBYTE   :\ Read address high word`

` INX:BNE LangProcessor :\ Not &xxFF`

` INY:BNE LangProcessor :\ Not &FFxx`

` \ &FFFFxxxx, executing in I/O processor`

</code>

# Text Wrapping Routine

This is a little routine that could be useful for people writing text adventures or any other program that requires text to be wrapped on the fly.

## The Code

<code>`  10 MODE 0`
`  20 A$="This is a text wrapping example. Here you can see the text being dynamically wrapped to a user defined width. Pretty neat stuff isn't it?"`
`  30 REPEAT`
`  40 INPUT'"Enter text width: " W%`
`  50 IF W% THEN PRINT'STRING$(W%,"-"):PROCwrap(A$):PRINT`
`  60 UNTIL W%=0`
`  70 END`
`  80 `
`  90 DEF PROCwrap(A$)`
` 100 L%=W%:O%=1`
` 110 REPEAT`
` 120 P%=INSTR(A$," ",O%)`
` 130 IF P%=0 THEN P%=LEN(A$)`
` 140 S%=P%-O%`
` 150 IF S%>=L% AND POS>1 THEN PRINT `
` 160 IF S%>=L% THEN L%=W%-S%-1 ELSE L%=L%-S%-1`
` 170 PRINT MID$(A$,O%,S%+1);`
` 180 IF POS=1 THEN PRINT CHR$(127);`
` 190 O%=P%+1`
` 200 UNTIL P%=LEN(A$)`
` 210 ENDPROC`

</code>

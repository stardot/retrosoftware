*[Sample Code Library](SampleCodeLibrary "wikilink") &gt; Linear time bucket sort*

# Linear time bucket sort

I have been going through some of the old stuff on my BBC disks and found this - I used it for some demos to sort sprites to allow them to be rendered top-down to chase/run ahead of the raster.

It is a linear time bucket sort 53 bytes (60 if buckets is not in ZP) that takes &lt;2k cycles for 32 sprites indexed by character line and &lt;6k cycles for 128 sprites. I am happy to discuss it on the forums.

I have tidied the code and added a few lines of basic to help see how it works. This is the generic version, I tailored it for each demo by changing the way each bucket index is calculated eg ignoring hidden sprites when iterating the two src lists.

The algorithm is very simple and probably has a great explanation on the web now!

The fast version here only supports up to 255 numbers in up to 255 buckets - I think - anyway 32 buckets fits nicely even for BASIC use and sorting over 100 items doesn't happen very often in real time.

I would be happy to hear comments / improvements etc on the forums. [1](http://www.retrosoftware.co.uk/forum/viewtopic.php?f=3&t=614)

Richard (tricky) Broadhurst.

<code>

`  10 src_count = &F8 : REM contains num to sort - 1`
`  20 bkt_count = &F9 : REM contains num buckets - 1`
`  30 buckets   = &70 : REM address in zp of buckets`
`  40 REM B=buckets, N=numbers (20.5B + 41N + ~22) (B=32 N=128 ~ 5926)`
`  50 REM (32/32) RESET 250 + SIZE 482 + OFFSET 422 + WRITE 772 + RTS 6 = 1990`
`  60 DIM linear_sort 200, src 255, dst 255`
`  70 FOR pass = 0 TO 3 STEP 2`
`  80 P% = linear_sort`
`  90 [OPT pass`
` 100 .sort                    \\ call with X = number of buckets and Y = number of numbers to sort`
` 110   LDX bkt_count          \\ change to STX bkt_count if X is passed in (count = 1 based)`
` 120   TXA`
` 130   LSR A`
` 140   LDA #0                 \\ zero the count of each valid number's bucket`
` 150   BCS odd                \\ unroll loop in pairs, odd total, jump to second half - break even B=4 faster B=6+`
` 160 .reset_buckets`
` 170   STA buckets-1,X`
` 180   DEX`
` 190 .odd`
` 200   STA buckets-1,X`
` 210   DEX`
` 220   BNE reset_buckets`
` 230                          \\ A=0 X=0 Y=? Z=1 N=0 C=?`
` 240   LDY src_count          \\ remove this line if passed in in Y`
` 250 .size_buckets`
` 260   LDX src-1,Y            \\ get value to be sorting by [0..bkt_count)`
` 270   INC buckets,X          \\ increment how many of this buckets number we have`
` 280   DEY`
` 290   BNE size_buckets`
` 300                          \\ A=0 X=? Y=0 Z=1 N=0 C=?`
` 310   CLC`
` 320   LDX bkt_count          \\ making X 1 based`
` 330 .accumulate_buckets      \\ offset bucket base by total of previous entries`
` 340   ADC buckets-1,X`
` 350   STA buckets-1,X`
` 360   DEX`
` 370   BNE accumulate_buckets`
` 380                          \\ A=src_count X=0 Y=0 C=0 Z=1 N=0`
` 390   SEC`
` 400 .write_results           \\ this is where you would make changes to save another pass over the generated indices`
` 410   TAY                    \\ A = Y = original index of value (1 based)`
` 420   LDX src-1,Y            \\ X = original value to sort on`
` 430   DEC buckets,X          \\ bucket value needs pre decrementing to give a zero based index`
` 440   LDY buckets,X          \\ Y = final index of original value`
` 450   SBC #1`
` 460   STA dst,Y              \\ store original index in dst[final index]`
` 470   BNE write_results `
` 480                          \\ A=0 X=? Y=? Z=1 N=0 C=1`
` 490   RTS`
` 500 ]`
` 510 PRINT "sort &";~sort;" [";P%-linear_sort;"] src &";~src;" dst &";~dst`
` 520 NEXT pass`
` 530 :`
` 540 ?bkt_count = 32`
` 550 FOR m = 1 TO 200`
` 560 ?src_count = m`
` 570 FOR n = 0 TO m-1 : src?n = RND AND 31 : NEXT`
` 580 PRINT`
` 590 PRINT "src: "; : FOR n = 0 TO m-1 : PRINT ;src?n;" "; : NEXT : PRINT`
` 600 CALL sort`
` 610 PRINT "bkt: "; : FOR B = 0 TO 31 : PRINT ;buckets?B;" "; : NEXT : PRINT`
` 620 PRINT "dst: "; : FOR n = 0 TO m-1 : PRINT ;dst?n;" "; : NEXT : PRINT`
` 630 PRINT "ord: "; : FOR n = 0 TO m-1 : PRINT ;?(src+dst?n);" "; : NEXT : PRINT`
` 640 NEXT`
` 650 REM with buckets in ZeroPage sort is 53 bytes, otherwise 60 bytes, but no code changes are required`
` 660 REM could use N based indices by offsetting lookups (try not to cross page boundaries)`
` 670 REM could also easily unroll the size_buckets loop in pairs (would need to set A=0 before .accumulate_buckets)`
` 680 REM if you just wanted a sorted list of numbers, you can replace accumulate_buckets and write_results with a loop over the buckets printing each index the number of times in each bucket`

</code>

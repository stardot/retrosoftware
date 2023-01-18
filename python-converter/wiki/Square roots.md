<code>` eg, in=&70:out=&72`

`  `

` .sqr                            :\ On entry, !in=input value`

` LDY #1:STY out+0:DEY:STY out+1  :\ Initialise out to first subtrand`

` .sqr_loop                       :\ Repeatedly subtract increasing`

` SEC                             :\   odd numbers until in<0`

` LDA in+0:TAX:SBC out+0:STA in+0 :\ in=in-subtrand, remainder in X`

` LDA in+1:SBC out+1:STA in+1`

` BCC sqr_done                    :\ in<0, all done`

` INY                             :\`

` LDA out+0:ADC #1:STA out+0      :\ step +2 to next odd number`

` BCC sqr_loop                    :\ no overflow, subtract again`

` INC out+1:BNE sqr_loop          :\ INC high byte and subtract again`

` .sqr_done`

` STY out+0:STX out+1             :\ out?0=root, out?1=remainder`

` RTS`

` :`

` This works by counting how many times increasing odd numbers`

` can be subtracted until there's nothing left. For example:`

`  `

` 32-1=31 -> 31-3=28 -> 28-5=23 -> 23-7=16 -> 16-9=7 -> 7-11<0`

`     1          2          3          4          5`

`  `

` -> SQR(32)=5, remainder 7`

`  `

` You can test it with:`

` FOR A%=1 to 65535:!in=A%:CALL sqr:P.A%,out?0,out?1:NEXT`

</code>

See <http://mdfs.net/Info/Comp/6502/ProgTips>

## Printing decimal integers

<tt>

`\ On entry,  num+0,num+1,num+2 holds 24-bit number`

`\            A=leading character or &00 for none`

`\ Workspace, sub+0, sub+1, sub+2, pad`

`.PrDec24`

`STA pad                                :\ Set pad character`

`LDA #&98:LDY #&96:LDX #&80:JSR SubNumP :\ 10000000s`

`LDA #&0F:LDY #&42:LDX #&40:JSR SubNumP :\ 1000000s`

`LDA #&01:LDY #&86:LDX #&A0:JSR SubNumP :\ 100000s`

`LDA #&00:LDY #&27:LDX #&10:JSR SubNumP :\ 10000s`

`LDA #&00:LDY #&03:LDX #&E8:JSR SubNumP :\ 1000s`

`LDA #&00:TAY:LDX #&64:JSR SubNumP      :\ 100s`

`LDA #&00:TAY:LDX #&0A:JSR SubNumP      :\ 10s`

`LDA num:BPL SubDigit                   :\ 1s`

`:`

`.SubNumP                               :\ Subtract and print`

`JSR SubNum:BEQ SubZero`

`.SubDigit`

`ORA #48:JSR OSASCI:LDA #48:STA pad`

`.SubZeroOk`

`RTS`

`.SubZero`

`LDA pad:BEQ SubZeroOk`

`JMP OSASCI`

`:`

`.SubNum                                :\ &AYX = 24bit divisor`

`STX sub:STY sub+1:STA sub+2`

`LDX #255`

`.SubLp:INX:SEC`

`LDA num+0:SBC sub+0:STA num+0`

`LDA num+1:SBC sub+1:STA num+1`

`LDA num+2:SBC sub+2:STA num+2`

`BCS SubLp:CLC`

`LDA num+0:ADC sub+0:STA num+0`

`LDA num+1:ADC sub+1:STA num+1`

`LDA num+2:ADC sub+2:STA num+2`

`TXA:RTS                                :\ A=num DIV sub`

`:`

</tt>

See <http://mdfs.net/Info/Comp/6502/ProgTips>

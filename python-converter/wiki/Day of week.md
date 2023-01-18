## Calculating the day of the week for a given date

<tt>

`\ Based on code at `[`http://6502.org/source/misc/dow.htm`](http://6502.org/source/misc/dow.htm)` by Paul Guertin.`

`\ This routine works for any date from 1900-03-01 to 2155-12-31.`

`\ No range checking is done, so validate input before calling.`

`\`

`\ It uses the formula`

`\     Weekday = (day + offset[month] + year + year/4 + fudge) mod 7`

`\ where the value of fudge depends on the century.`

`\`

`\ On entry, A=day, 1..31`

`\           X=month, 1..12`

`\           Y=year-1900, 0..255`

`\ On exit,  A=day of week 1..7 for Sun..Sat`

`.DayOfWeek`

`CPX #3:BCS dow_march    :\ Year starts in March to bypass leap year problem`

`DEY                     :\ If Jan or Feb, decrement year`

`.dow_march`

`EOR #&7F                :\ Invert A so carry works right`

`CPY #200                :\ Carry will be 1 if 22nd century`

`ADC dow_months-1,X      :\ A is now day+month offset`

`STA dow_tmp`

`TYA:JSR dow_mod7        :\ Get the year MOD 7`

`SBC dow_tmp:STA dow_tmp :\ Combine with day+month`

`TYA:LSR A:LSR A         :\ Get the year DIV 4`

`CLC:ADC dow_tmp         :\ Add it to y+m+d and fall through to MOD 7`

`.dow_mod7`

`ADC #7:BCC dow_mod7     :\ Reduce A to A MOD 7`

`ADC #0:RTS              :\ Increment to standard 1..7 range`

`.dow_months`

`EQUB 1:EQUB 5:EQUB 6:EQUB 3  :\ Month offsets`

`EQUB 1:EQUB 5:EQUB 3:EQUB 0`

`EQUB 4:EQUB 2:EQUB 6:EQUB 4`

`.dow_tmp`

`EQUB 0                  :\ Temporary storage`

</tt>

You can test this with: <tt>

`FOR Y%=1 TO 255`

`FOR X%=1 TO 12`

`FOR A%=1 TO 31`

`PRINT A%;"/";X%;"/";1900+Y%;" ";`

`PRINT MID$("SunMonTueWedThuFriSat",((USRDayOfWeek)AND&FF)*3-2,3)`

`NEXT A%:NEXT X%:NEXT Y%`

</tt>

I must say that this is an impressive bit of code!

See <http://mdfs.net/Info/Comp/6502/ProgTips>

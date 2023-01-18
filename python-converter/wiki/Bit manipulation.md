## Setting Clearing and Copying bits of data

`AND` `xx` will clear the bits in A that are also clear in xx, for example: <tt>

`      A            xx      after AND xx`

`  %abcdefgh    %01010101    %0b0d0f0h`

</tt>

`ORA` `xx` will set the bits in A that are also set in xx, for example: <tt>

`      A            xx      after ORA xx`

`  %abcdefgh    %01010101    %a1c1e1g1`

</tt>

`EOR` `xx` will toggle the bits in A that are set in xx, for example: <tt>

`      A            xx      after EOR xx`

`  %abcdefgh    %01010101    %aBcDeFgH`

</tt>

To clear the bits in A that are _set_ in xx, use both `ORA` and `EOR`, for example: <tt>

`      A            xx      after OR xx  after EOR xx`

`  %abcdefgh    %01010101    %a1c1e1g1    %a0c0e0g0`

</tt>

You can copy a number of bits to a memory location without changing the other bits using `EOR` and `AND`. For example, to copy the top four bits of A into a memory location without changing the bottom four bits, use the following: <tt>

`               A=12345678  dst=abcdefgh`

`   EOR dst       ********      abcdefgh`

`   AND #&F0      ****0000      abcdefgh`

`   EOR dst       1234efgh      abcdefgh`

`   STA dst       1234efgh      1234efgh`

</tt>

This is much more efficient than the usual code: <tt>

`   PHA`

`   LDA dst:AND #&0F:STA dst`

`   PLA`

`   AND #&F0:ORA dst:STA dst`

</tt>

See <http://mdfs.net/Info/Comp/6502/ProgTips>

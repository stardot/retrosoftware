## Crunching data with puCrunch

After a brief discussion recently, it was suggested I try using puCrunch to pack data for my game. I've had a quick look, and indeed it's very easy to get up and running with it. I've not explored all the features, but here I will explain to what end I've made it work for me.

## Prerequisites

You'll only need one tool binary; the cruncher. Visit [this site](http://www.cs.tut.fi/~albert/Dev/pucrunch/#Progs) and download the pucrunch executable. Sources are included if you need to compile for a particular platform, but I just used the vanilla Windows one. You'll need this to pack your data down.

## Packing your data

Packing your data down is very easy and is achieved from the command line thus:

`./pucrunch.exe` `-d` `-c0` `-l0x900` `-s` `BIN/BBCTLE.DAT` `BIN/BBCTLE.PAK`

The few flags of note here are "-l" which tells it the address to unpack to, and "c0" to tell the cruncher we're not on a C64 :)

## Unpacking your data

Now the data is packed, you'll need to include the 'standalone' decruncher into your sources, which I've modified to assemble under BeebASM. So grab <Media:Unpack.zip> and save in a separate file, eg 'unpacker.asm'. Then all that remains is for you to unpack the data.

The routine will unpack to the address specified on the cruncher command line, but that's just a few bytes into the header data so should be easy enough to change on the fly.

`ORG` `&70`

`.LZPOS` `EQUW` `&9e` `;` `2` `ZeroPage` `temporaries`

`.bitstr` `EQUB` `&fb` `;` `1` `temporary` `(does` `not` `need` `to` `be` `ZP)`

`ORG` `&1900`

`{`

`.start:`

`CLC`

`LDX` `#HI(packedData+2)`

`LDY` `#LO(packedData+2)`

`JSR` `unpack`

`BCC` `unpackOK`

`LDA` `#70`

`JSR` `&FFEE`

`JSR` `&FFE7`

`RTS`

`.unpackOK:` `;` `At` `this` `stage` `0x900` `will` `contain` `our` `unpacked` `data!`

`LDA` `#48`

`JSR` `&FFEE`

`JSR` `&FFE7`

`RTS`

`.end:`

`}`

`INCLUDE` `"unpacker.asm"`

`.packedData:`

`INCBIN` `"BIN/BBCTLE.PAK"`

## Et Voila!

And that's all there is to it! As I say, I've not investigated too much the options available for crunching, so please explore and expand this Wiki if you find out anything of interest!

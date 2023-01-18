## Electron Version

Repton 2 levels appear start at 0x2e00 and encode the data in rows of 20 bytes (5 bits per tile).

Sprites start at 0x2340.

Spirits are 4 by 8 pixels. Other sprites are 12 by 24 pixels.

### Level data

Each set of four bytes, from 0x2000 to 0x203f, contain four indices into the level data which each refer to eight rows of level data. The special index, 0x80, is the empty space at the bottom of Screen A.

By inspecting the 64 bytes of level data and comparing them to the maps on the Stairway to Hell site, values of 0x80 and above appear to be placeholders for eight rows that contain a single type of tile. So, 0x80 is eight rows of empty space, 0x86 is diamonds (as used in Screen P), and 0x83 is earth.

### Puzzle pieces

Puzzle piece definitions are defined from 0x1da0 to 0x1e47. There are also two incompletely defined entries at 0x1e48 and 0x1e4c. Each block of four bytes contains a screen number, x and y coordinates and the piece's location in the display area on Screen A.

The puzzle piece sprites are defined from 0x1c20 to 0x1d9f. Each group of 9 bytes represents offsets into the sprite area to refer to the sprites used for the 9 parts of each puzzle piece. Note that 42 \* 9 = 378 and that the area from 0x1c20 and 0x1d9f accommodates this number of bytes with six bytes to spare at the end.

### Transporters

Transporters are defined from 0x1e50 to 0x1fcf. Each definition is six bytes long: the first four bytes represent screen number, x and y coordinates, and screen number for the transporter destination. The following two bytes are the x and y coordinates of the transporter destination.

The end of the transporter definitions is at 0x1fcf. There are null bytes from 0x1fd0 to 0x1fff.

Although transporters and transporter destinations are defined in the level data, it seems that they are only there as placeholders to reserve space.

### Tile

The tile sprites are defined in the same way as the puzzle piece sprites, from 0x1b00 to 0x1c1f. However, the transporter sprite is defined as tile 11 and tile 2 is used to represent transporters in the level data.

### Totals

The total number of earth tiles is stored in two bytes at 0x102f and 0x1034 as part of a routine. The values are encoded as binary coded decimal with the lowest first.

The total number of diamonds is stored in 0x1025 and 0x102a. Total monsters is at 0x1020, transporters at 0x0164, puzzle pieces at 0x132.

The monsters, earth and diamonds totals are stored in locations from 0x0be0 to 0x0be4.

Looking at the code from 0x132 to 0x14b, it appears that the running total for the puzzle pieces is stored at 0x0b81. Similarly, at 0x18b, the running total for the transporters is stored at 0x0b80.

### Start position

This is stored at 0x1060 (x) and 0x1064 (y).

### Skulls

The skulls at the top of Screen A disappear when certain totals reach zero and Repton visits the status character. The first skull and its counterpart below disappear when all monsters have been killed, the second when all diamonds are collected, the third when all earth is collected, the fourth when all transporters have been used, and the fifth when there is only one puzzle piece left to collect.

The start of the file appears to contain code to check the values from 0x0be0 to 0x0be4 (the monsters, earth and diamonds totals). The code at 0x132 which includes the puzzle piece total, appears to read the table at 0x1da0 (0x29a0).

Later, at 0x19c, the totals are checked and a value of 2 written to the addresses, 0x421, 0x4a1, 0x423, 0x4a3, 0x424 and 0x4a5.

The puzzle piece and transporter totals are checked at 0x1cd and 0x1dc, and a value of 2 written to 0x429, 0x4a9, 0x427 and 0x4a7 as a result.

This may mean that the working level, or persistent Screen A, is stored at 0x420 or thereabouts.

### Score

| Item                          | Value |
|-------------------------------|-------|
| Diamond                       | 6     |
| Earth (cross)                 | 3     |
| Earth (top-left/bottom-right) | 4     |
| Earth (top-right/bottom-left) | 5     |
| Monster                       | 0     |
| Transporter                   | 0     |
| Puzzle piece                  | 0     |
||

### Palette

At 0x394, there is the start of a VDU 19 sequence. This appears to split bytes obtained from zero page into the two logical and physical colour values, with the top four bits as the logical value and the lower four as the physical value.

### Memory layout

| Offsets   | Description                       |
|-----------|-----------------------------------|
| 1da0-1e48 | Puzzle piece locations            |
| 1e50-1fcf | Transporter definitions           |
| 1fd0-1fff | ...                               |
| 2000-203f | Screen area definitions           |
| 2040-233f | Text character sprite definitions |
| 2340-273f | Game sprites                      |
| 2740-2757 | ?                                 |
| 2758-287f | Game sprites                      |
| 2880-2897 | ?                                 |
| 2898-29bf | Game sprites                      |
| 29c0-29d7 | ?                                 |
| 29d8-2a87 | Game sprites                      |
| 2a88-2a97 | ?                                 |
| 2a98-2dff | Game sprites                      |
| 2e00-4bff | Level definitions                 |
||

### Code

A map editor for the game is available from the [ReptonMaps repository at Bitbucket](https://bitbucket.org/dboddie/reptonmaps).

### Discussion

The format of Repton and Repton 2 levels was a distraction that occurred [part way through a stardot thread](http://stardot.org.uk/forums/viewtopic.php?f=1&t=6377&p=66669#p66122), leading to the above set of tools. As noted in the thread, and above, various aspects of the game are hard-coded, requiring code to be patched out of the game for custom levels to behave as intended.

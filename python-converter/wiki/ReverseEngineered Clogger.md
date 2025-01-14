# Electron Version

## Overview

The levels in the SLIPPER file start at 0xf7d. There are 5 levels per file.

Each level consists of 32 by 32 tiles, stored using one byte per tile. Values 0x00 to 0x0f are ordinary scenery or collectable tiles, tiles 0x26 to 0x2a are moveable objects, and tiles 0x10 to 0x24 are puzzle pieces.

Loading the SLIPPER file at 0x5403 in order to align the graphics to rows on screen, it appears that the wall sprite starts at 0xabd.

Puzzle pieces are arrays of 4 by 4 blocks, with 8 bits per block, so each piece is 16 bytes long. Each puzzle is therefore 21 \* 16 bytes long (336 bytes).

The puzzle pieces start at 0x3a5 in each level file.

The pieces are positioned from left to right and from top to bottom when arranged on screen, so the pieces as extracted from the level data are placed in the following arrangement in order to reconstruct the complete puzzle:

` 0  1  2  3  4  5  6`

` 7  8  9  a  b  c  d`

` e  f 10 11 12 13 14`

Each piece is stored as a sequence of columns from left to right, with each column containing four elements. So the bytes in a piece need to be arranged in the following way when creating a sprite:

` 0 4 8 c`

` 1 5 9 d`

` 2 6 a e`

` 3 7 b f`

The passwords are stored at the start of each level file as 5 strings of 7 bytes in length, with each byte scrambled using the EOR of the offset into the file, so the first byte is actually unscrambed since (X EOR 0) is X.

There is a collection of 210 non-zero values immediately following the password data. These are a series of coordinate pairs that can be interpreted either as offsets into the level data, or as two 5 bit values packed together. Each pair is stored in little-endian form and combined with 0x0400 using an OR operation, so we need to mask off the upper 6 bits when we read the values put back the extra bit when we write them.

Each two bytes containing a coordinate pair correspond to the final location of a puzzle piece. The pairs are stored according to the location of the piece within the puzzle, with the first seven coordinate pairs describing the top row of the puzzle, then the middle row, and the last seven describing the bottom row.

Five sets of 21 coordinates are given, describing the locations of the puzzle pieces on each level in ascending order.

## Code

A map viewer for levels in the Electron version of the game is available from the [CloggerMaps repository on Bitbucket](https://bitbucket.org/dboddie/cloggermaps).

<img src="2015-02-16-CloggerMaps-editor-half.png" title="x" alt="x" width="258" />

## Discussion

The above code was announced in a [stardot thread](http://stardot.org.uk/forums/viewtopic.php?f=1&t=9108).

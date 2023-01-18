## BBC Version

All game data is found in the "SURVIV2" file, starting at 0x2400. There are four levels, with the level data taking up 0x600 bytes. There is a lot of padding both before and after each level.

It's hard to pinpoint down an exact length and width, but the dimensions of 30 x 47, using 16 x 32 mode 5 tiles (so 32 x 32 square pixel tiles) cover all 4 levels with no cutoffs.

The lower nybble of each byte in the level definition can be match to a tile ID, as listed below:

### Tile definitions

| Number (hex) | Description |

|--------------|--------------|

| 0 | Space |

| 1 | Soil |

| 2 | Unused |

| 3 | Unused |

| 4 | Rock |

| 5 | Robot 1 |

| 6 | Robot 2 |

| 7 | Robot 3 |

| 8 | Survivor |

| 9 | Moving Enemy |

||

The use of the first nybble is unknown and seems to have no effect on the tile.

The starting position of the robots is unknown, it may be that they are always at positions 15, 16 and 17 on row 0 of the map.

### Sprites

The sprites are stored at the end of "SURVIV2" (offset 0x4400). Each tile is 2 by 4 characters in size (16 by 32 pixels).

### Code

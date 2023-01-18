## Electron Version

Repton levels are maps of 32 row by 32 columns.

The level data was found by loading the REPTON2 file into memory in MODE 5 and visually inspecting the data. The assumption was that level data follows the sprite data.

Level data starts at 0x2c00.

Each row of the level is 20 bytes long. Each tile is stored in 5 bits.

### Tiles

| Number (hex) | Description |

|--------------|--------------------------------|

| 00 | space |

| 01 | diamond |

| 02 | boulder |

| 03 | egg |

| 04 | key |

| 05 | earth |

| 06 | earth |

| 07 | earth |

| 08 | safe |

| 09 | brick wall |

| 0a | double (top/bottom) wall |

| 0b | double (left/right) wall |

| 0c | quadruple wall |

| 0d | fancy wall |

| 0e | smooth wall |

| 0f | lower edged smooth wall |

| 10 | upper edged smooth wall |

| 11 | right edged smooth wall |

| 12 | left edged smooth wall |

| 13 | lower right curved smooth wall |

| 14 | lower left curved smooth wall |

| 15 | upper right curved smooth wall |

| 16 | upper left curved smooth wall |

| 17 | map |

| 18 | lower edged brick wall |

| 19 | upper edged brick wall |

| 1a | right edged brick wall |

| 1b | left edged brick wall |

| 1c | lower right curved brick wall |

| 1d | lower left curved brick wall |

| 1e | upper right curved brick wall |

| 1f | upper left curved brick wall |

||

Sprites are stored at 0x2500 in the REPTON2 file and are 8 by 16 pixels. See the table in the sprites module of the Repton package for the offsets into the sprite data.

### Code

A map editor for the game is available from the [ReptonMaps repository at Bitbucket](https://bitbucket.org/dboddie/reptonmaps). This repository also contains a Repton Python package that includes the sprites module mentioned above.

### Discussion

The format of Repton and Repton 2 levels was a distraction that occurred [part way through a stardot thread](http://stardot.org.uk/forums/viewtopic.php?f=1&t=6377&p=66669#p66122), leading to the above set of tools.

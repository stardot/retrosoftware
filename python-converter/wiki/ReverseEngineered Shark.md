## Electron Version

In the "CODE" file, some sprite data is found at 0x1d40.

Character movement (jumping) appears to be defined at around 0x4a0.

Map data starts at 0x2be0 and begins describing data almost half way across the first screen, column-by-column, starting from the top of the screen and ending at the bottom.

A side effect of setting the byte at 0x2be0 is that the player's bullet sprite is corrupted.

Tiles:

| Number (hex) | Description |

|--------------|------------------------------------------|

| 0 | blank |

| 1 | ledge with magenta background underneath |

| 2 | magenta background |

| 3 | ground |

| 4 | horizontal branch |

| 5 | thick foliage |

| 6 | medium foliage |

| 7 | thin foliage |

| 8 | left trunk |

| 9 | right trunk |

| a | blank |

| b | yellow flower |

| c | magenta flower |

| d | vine with ledge |

| e | vine |

| f | vertical branch |

Each byte describes two columns in the map with the low four bits on the left and the high four bits on the right. Each column is 12 tiles high.

The first level ends at 0x2fe8 and the second level starts at 0x2fe8.

Tiles:

| Number (hex) | Description |

|--------------|-------------------------------|

| 0 | blank |

| 1 | girder |

| 2 | brick background |

| 3 | ground |

| 4 | horizontal pipe |

| 5 | up-left curved pipe |

| 6 | vertical pipe |

| 7 | down-left curved pipe |

| 8 | down-right curved pipe |

| 9 | up-right curved pipe |

| a | thin vertical pipe |

| b | chequered background |

| c | ledge on chequered background |

| d | window |

| e | thin pipe junction |

| f | thin horizontal pipe |

The second level ends at 0x33f0 and the third level starts at 0x33f0.

Tiles:

| Number (hex) | Description |

|--------------|--------------------------------------------|

| 0 | blank |

| 1 | ledge above brick background |

| 2 | brick background |

| 3 | ground |

| 4 | rock background |

| 5 | ledge above rock background |

| 6 | ledge above small brick background |

| 7 | small brick background |

| 8 | windows |

| 9 | right edge of window frame with brick wall |

| a | right edge of window frame with rock wall |

| b | top part of door |

| c | bottom part of door |

| d | chimney |

| e | wall with top-right part missing |

| f | wall with top-left part missing |

The game runs in mode 2. Sprite data for level 3 starts at 0x0000 and continues until 0x400. Sprite data for level 1 starts at 0x1d00 and continues until 0x2100. Sprite data for level 2 starts at 0x2100 and continues until 0x2500.

Note that tile 3 (ground) is used to generate soldiers and must be placed at the bottom-right of each screen if soldiers are to be generated.

## Code

A map editor for the game is available from the [SharkMaps repository at Bitbucket](https://bitbucket.org/dboddie/sharkmap/overview). Ready to use tape and disk images can be found in [this Shark maps thread](http://stardot.org.uk/forums/viewtopic.php?f=1&t=3692) in the stardot forums.

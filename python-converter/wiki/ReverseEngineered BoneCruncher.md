## Electron Version

Level data is found in the "BONE_2" file at around 0x2500 by examining the comparable data in four additional files containing maps: "SCREEN 1", "SCREEN 2", "SCREEN 3" and "SCREEN 4".

Each row is at least 20 bytes in length, with each four bits representing a tile in the map, the lower four bits appearing on the left and the upper four bits on the right. Each special tile requires an additional half byte, so rows with special tiles are longer than 20 bytes in length.

### Tile definitions

| Number (hex) | Description |

|--------------|------------------------------------------|

| 0 | Space |

| 1 | Horizontal wall |

| 2 | Vertical wall |

| 3 | Corner wall |

| 4 | Cauldron |

| 5 | Door/gate |

| 6 | Key |

| 7 | Earth |

| 8 | Trapdoor |

| 9 | Sea |

| A | Glook |

| B | Skeleton |

| C | Monster |

| D | Spider |

| E | Space (unknown/unused) |

| F | Special tile (Fozzy/stairs/Bono/volcano) |

||

F tiles are always followed by another value which determines which special tile is used:

| Number (hex) | Description |

|--------------|------------------|

| 0 | Fozzy |

| 1 | Rightward stairs |

| 2 | Leftward stairs |

| 3 | Upward stairs |

| 4 | Downward stairs |

| 5 | Bono |

| 6 | Volcano |

||

### Sprites

The sprites are stored at the start of "BONE_2". Each tile is 2 by 4 characters in size (16 by 32 pixels).

### Code

A map editor for the game is available from the [BoneCruncherMaps repository at Bitbucket](https://bitbucket.org/dboddie/bonecrunchermaps).

### Discussion

A discussion related to this file format can be found in [this stardot thread](http://stardot.org.uk/forums/viewtopic.php?f=1&t=6788&p=67168).

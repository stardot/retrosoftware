## Electron Version

Each level map is stored in a file, from "DECKB" to "DECKT" except for the first level, which is stored at the start of the "Prog2" file.

The levels in separate files are scrambled using a counter that starts with a value of 1 and increases for each byte read, wrapping around after 255 to 0. The counter value is combined with each byte from the file using an EOR operation.

It is difficult to modify the game by creating a new UEF file because the UEFfile module does not preserve the block headers in data chunks from the original Icarus.uef file when it writes extracted files to a new UEF file. The "Game" and "Icarus" files are locked, and the "Game" file appears to rely on a value stored in the "next address" block header. Applying an EOR 0xa5 operation to the file unscrambles it, but how this is obtained from the header, and whether the locked bit influences that process is unknown.

| Number (hex) | Description                                    |
|--------------|------------------------------------------------|
| 00           | wall                                           |
| 01           | space                                          |
| 02           | vending machine                                |
| 0b           | beam                                           |
| 20           | monster                                        |
| 46           | lift (for monsters)                            |
| 63           | crate                                          |
| 64-6f        | destructable block (solid to almost destroyed) |
| cf           | switch 1                                       |
| d0           | switch 2                                       |
| d1           | switch 3                                       |
| d2           | switch 4                                       |
| d9           | door label 1                                   |
| da           | door label 2                                   |
| db           | door label 3                                   |
| dc           | door label 4                                   |
| dd           | door label 5                                   |
| de           | door label 6                                   |
| df           | access card 1                                  |
| e0           | access card 2                                  |
| e1           | access card 3                                  |
| e2           | access card 4                                  |
| e3           | access card 5                                  |
| e4           | access card 6                                  |
| e6           | one-way door (up)                              |
| e7           | one-way door (right)                           |
| e8           | one-way door (down)                            |
| e9           | one-way door (left)                            |
| ea           | mine                                           |
| eb           | vertical pipe                                  |
| ec           | horizontal pipe                                |
| ed           | top-left diagonal pipe                         |
| ee           | top-right diagonal pipe                        |
| ef           | bottom-right diagonal pipe                     |
| f0           | bottom-left diagonal pipe                      |
| f1           | beam nozzle (facing up)                        |
| f2           | beam nozzle (facing right)                     |
| f3           | beam nozzle (facing down)                      |
| f4           | beam nozzle (facing left)                      |
| f7           | door (vertical, below door label)              |
| f8           | door (horizontal, left of door label)          |
| f9           | armour                                         |
| fa           | power (gun)                                    |
| fb           | reload speed                                   |
| fe           | credit                                         |
| fd           | exit                                           |



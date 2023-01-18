# Hobgoblin

The map data seems to be the same for both the Beeb and Electron. With the Electron its stored in $.HOB-4; on the BBC it's encapsulated in the $.HOB-2 file; but still loads to the same address. So I'm going to use absolute addresses as they'll apply to both types.

When sprites are used; these are normally mode 5 sprites stored sequentially from &3C70 (the file in $.HOB-2 on the Electron). The order for these seems to be moving sprites (e.g. main character, enemies, bullets) followed by masks followed by scenery sprites.

The BBC file seems to be the Electron source files mangled together. It should be noted that the Electron version of Hobgoblin will crash on a BBC.

The Electron files are:

| Filename | Use                   |
|----------|-----------------------|
| $.HOB-1  | Machine Code Loader   |
| $.HOB-2  | Mode 5 Sprites        |
| $.HOB-3  | Mode 5 half size font |
| $.HOB-4  | Map data              |
| $.HOB-5  | Machine Code          |

## Sprites

The sprite file contains all of the game's sprites. These are stored in the following order:

-   Animation Sprites
-   Object Sprites
-   Animation Masks
-   Scenery

The size of the sprite depends on the rendered version of the item. The mask is the same size as the sprite.

Scenery sprites are 12 x 16 pixels.

## Maps

The maps themselves start at &3000. The first &B70 bytes are map scenery data; they describe the map in columns, with one byte for each 8x8 chunk; which leaves 8 bytes/column, so it looks like:

    0 8
    1 9
    2 10
    3 11
    4 12
    5 13
    6 14
    7 15

&B70/8 is 366; so there's 366 columns of data in the game, though the last column seems to consist of rubbish data.

Each byte is a pointer to a sprite. There are two exceptions: if bit 7 of the byte is set, then the scenery is solid and will block the player and will allow the player to walk on it. If bit 6 is set then it marks a monster spawn point (see below).

The monster data is in two blocks of 128 bytes. The first block from &3B70 to &3BEF controls the type of monster. The second block from &3BF0 to &3C6F controls the monster health and delay.

The first block contains a byte/monster and encodes direction, type and weapon type in the below bits:

    DUWWWTTT

Where:

-   **D** is the facing direction, if set the monster is pointing left
-   **U** is unused and if set just kills the creature immediately
-   **W** is the weapon type and follows the following pattern:

<!-- -->

    000 = knife
    001 = axe
    010 = lance
    011 = fireball
    100 = arrows
    101 = arrow thingy
    110 = skull
    111 = backward dagger

Note that these follow the order of the sprites in the sprite file with the exception of the knife and axe (which are the opposite way around). The game seems to add bit **D** to the sprite value to manage direction. Values 110 and 111 are never used and just show the algorithm in use.

-   **TTT** is the type of the monster and follows the following pattern:

<!-- -->

    000 = bobbing creature
    001 = skeleton
    010 = hornet
    011 = archer
    100 = alien thing
    101 = ghost
    110 = face
    111 = lizard man

Movement is handled in the code, so a bobbing creature will always bob and a skeleton will always move in a straight line.

The second block contains a byte/monster and encodes health and spawn time in the below bits:

    AHHHHSSS

Where:

-   **A** is set if the creature should spawn (it's always set AFAICS, clearing it causes the monster to immediately spawn, then disappear).
-   **HHHH** is the number of hits it take to kill the monster (I'm not 100% convinced all bits are used)
-   **SSS** is the delay in spawning of the monster. This seems to be in time ticks; it may be performed by moving the monster back that many columns.

Note the spawn points in the scenery and bytes for monsters should match up or monsters may spawn strangely or out of order.

For some reason &3BEF is set to &88 which doesn't make sense; this may be an error in the data.

## Enemy Definitions

Enemy definitions are stored in the middle of the code block (HOB-5 on the Electron). The offsets vary depending on the platform and are listed below:

    Electron = &fae
    BBC B = &f7b

(Note: the entire code is relocated down to &900 after loading, so if reading from the file, ensure offsets are set correctly).

The block consists of 5 bytes for each enemy, using the number TTT \* 5:

    ?0 = Low byte of address of start sprite
    ?1 = High byte of address of start sprite
    ?2 = Low byte of address of start mask
    ?3 = High byte of address of start mask
    ?4 = Number of sprites

So ?1?0 will point to address of the sprite definition, the next ?4 bytes are plotted in a column. They will be masked by the sprites at address ?3?2.

# Hobgoblin 2

Hobgoblin 2 seems to use an enhanced version of the Hobgoblin engine. The offsets differ and the control blocks haven't been reverse engineered yet. The offsets below are calculated from the BBC Micro version (file HOBBY3) - though the memory address ought to be the same:

| Data     | Start Address |
|----------|---------------|
| Sprites  | &6370         |
| Map data | &5700         |



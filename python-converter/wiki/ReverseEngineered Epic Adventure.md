# Epic Database format

This is a simple description of some reverse engineering performed on the Epic Adventures database format. It is a work in progress, so mistakes may exist.

All work has so far only been performed on _Castle Frankenstein_, although patterns have been noticed in some of the other games.

## Files

All game data and code is stored in the file $.FRANK2. Once loaded, the file is relocated down to &0C00. All offsets used below are offsets from the start of the file. Unless noted otherwise, memory pointers will be to locations in the BBC memory, so will need &0C00 deducted to get the file offset.

## Text Encoding

Verbs, nouns and the dictionary are trivial obfuscated by a single roll left to prevent dumping the game file to give clues.

Strings, such as system messages, messages and room descriptions are stored as a stream of &00 terminated bytes. Each byte is an index to an entry in the dictionary, which are then concatenated together to form the string.

Colour is defined by the a byte of greater than &F8 (which returns a dictionary entry of &01 to &08. The mapping has been completely resolved yet.

**Note:** there are some grey areas around the creation of strings as some words seem to lack space around the edge of the screen. It is possible that some form of wordwrap is in place which has been discovered yet.

## Data Chunks

The following chunks have been identified:

| Chunk Start | Chunk End | Use |

|-------------|-----------|----------------------------------|

| &0000 | &0045 | Header |

| &0045 | &0100 | OSFILE block used for save games |

| &0200 | &0364 | Save game data |

| &0700 | &0900 | Room Exits |

| &0e00 | &1000 | System Messages |

| &1ef8 | &3c43 | Location Descriptions |

| &3c44 | &4607 | Game Messages |

| &4608 | &4be3 | Unknown |

| &4be4 | &4dd7 | Unknown |

| &4dd8 | &4fcb | Verbs |

| &4fcc | &51bf | Nouns |

| &4fcc | &51bf | Dictionary |

### Header

The header has the following known fields:

| Start | End | Use |

|-------|-------|------------------------------------------------------------------|

| &0000 | &0001 | Pointer to Message Chunk |

| &0002 | &0003 | Pointer to 0x4608 |

| &0004 | &0005 | Pointer to 0x4be8 |

| &0006 | &0007 | Pointer to Verb Chunk |

| &0008 | &0009 | Pointer to Noun Chunk |

| &000a | &000b | Used as a temporary pointer to verbs or nouns |

| &000c | &000d | Used as a temporary pointer to the typed command |

| &000e | &000f | Pointer to Location Description Chunk |

| &0010 | &0010 | Used to store the parsed verb number |

| &0011 | &0011 | Used to store the parsed noun numbers |

| &0012 | &0013 | Pointer to Dictionary |

| &0014 | &001d | Unknown - appears to be used to store temporary action variables |

| &001e | &001e | Redraw flag - if not set to zero, display the room |

| &001f | &0042 | Space reserved for the typed command |

| &00d4 | &0138 | Initial Locations for Objects |

### Save Game Data

All data is initially set to &00; it will be update during the game. The filename use is stored at &57 and potentially could be used as a magic number for the game.

Known fields in the memory area are:

| Start | End | Use |

|-------|-------|-----------------------------|

| &0202 | &0202 | Last room visited |

| &0203 | &0203 | Current room |

| &0264 | ? | Current location of objects |

### Room Exits

This chunk comprises of 6 bytes for each room; each byte holds the destination room for the direction. The order of bytes is NSEWUD.

So to get the destination room for South from room 10, the formula is: &0700+(room\*6)+1

### System Messages

This chunk comprises of 25 system (engine) messages. These are usually referred to in the code by address rather than by index. All the messages are in the standard message format listed above.

### Location Descriptions

This chunk contains a messages for each room, starting from room 0. The messages are in the standard message format.

No field has been found to contain the number of rooms.

### Messages

This chunk comprises of game messages. All the messages are in the standard message format listed above.

No field has been found to contain the number of messages.

### Verbs

Verbs are stored as a list of words followed by a byte to indicate the word number. The words are encoded, like the dictionary by having the byte rolled left once. The end of the word is signified by having bit 0 set. The word number is not encoded.

Synonyms (e.g. GET and DROP) are marked by all the words having the same word number.

### Nouns

Nouns are stored in the same way as verbs.

### Dictionary

The dictionary is stored as a list of dictionary entries. Each byte is encoded by being rolled left once. The end of the word is signified by having bit 0 set.

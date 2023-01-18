# SAGA Rework Diary

## Background

I've often wondered why the BBC never got graphical versions of the Scott Adams and Mysterious Adventures games. Yes, the BBC was short of memory and only had a limited colour palette; but it still should've been possible to supply some graphics; even mode 7 ones!

So, I've decided that I'm going to add some graphics to the games on a BBC. My target platform is to fit on a BBC B with standard PAGE &1900 DFS to allow full saving.

## How To Start

There are a couple of ways this can be done:

1.  Hack the current engines to add graphics on a new room.
2.  Write a new interpreter.

I've decided to go for the second route, even though it would take the most amount of effort. There's many reasons for this, some due to laziness (both mine and Brian Howarth - the original author of the engine), others due to technical constraints.

The most important reason is that there doesn't seem to be just one engine, with each new game that came out, the engines got updated and twiddled.

The second is that the engines do some quite nasty stuff. The original engine (for the Golden Baton on the BBC Micro) relocates all code to &D00 - so messing up any NMIs and anything to do with discs.

## Step One: Compress Incoming Data

The Scott Adams database format (will be referred to as 'SAGA' from now on). Is well documented and publicised, since it was documented in a 1980 issue of *Byte* magazine by Scott Adams. An interpreter, ScottFree, written by Alan Cox of Adventuresoft and Linux kernel fame; is available for modern machines. The default format of the data is as an ASCII file, including comments, which makes the files vary between 12 and 32 KB (depending on the game).

Obviously this is of no real use to us. So we need to compress it into a more BBC friendly size. The original drivers for the BBC compressed all integers into 16 bits. reducing the size to around 6 - 10 KB. That's still not enough!

So, the logical decision is to compress the files using a modern machine to be as small as possible without altering the data. Whilst we're at it, we may as well make some tunings to make the engine code size smaller.

The data file falls into several sections as detailed below:

### Header

This consists of 13 16-bit numbers to refer to number of words, actions etc. The easy choice here is to reduced them all to 8-bit numbers. We can pretty much ensure that this is safe by checking the format files, where most things are restricted to 150.

There's one exception: the number of actions. These don't seem to have an upper limit. But, the largest number I've seen is for Seas of Blood, being 347. We can squeeze this number into 9-bits, and we have a header item (word length, which is usually between 3 and 5) which we can be sure will never use the top bit (word length). So we can munge the extra bit in there.

Some more amendments are needed though. We can drop number 0 and 12 as they're not used by the engine. But, to make things quicker on the engine we need to add a field: by default there is one number to cover both verbs and nouns, with the smaller list being padded out to match the larger list. This is wasteful, so I'm going to have separate byte counts for both verbs and nouns.

I'm also going to add some 16-bit numbers at the start of the header to give an easy to use offset for the start of each section, just to make things easier for the engine. I can technically work this out programatically at game initialisation, but for now I'm going to keep the table.

### Actions

Actions in SAGA are a group of 8 16-bit numbers, these consist of:

-   verb and noun
-   5 counts of condition
-   2 counts of actions

For some reason, verb/noun and the actions are in multiples of 150. So I'm going to change this multiple to 256 to make it easier for the engine. The conditions are in multiples of 20, again I'm going to change this to 256 to make it easier. Net gain in size = 0.

But, as there's a static number of conditions and actions, several of them end up unused. So we can remove empty conditions and actions and add a byte to list the number of conditions and actions in a nibble each. So the end result will be (in bytes):

-   verb
-   noun
-   count of conditions&lt;&lt;4 + count of actions
-   up to 5 of
    -   condition
    -   argument
-   up to 4 of
    -   action

This looks like it doesn't save us much space, but trying this over a range of games reduces the size of the actions segment to around 60%!

### Verbs and Nouns

The SAGA format allows a collection of verbs and nouns of which must be up to wlen (as defined in the header). In practice wlen has always been 3, 4 or 5. In traditional engines, these have been stored as a list of words with verbs and nouns interleaved with a divider character between each word.

The two ways to save memory here are to make a separate count of verbs and nouns to remove excess padding and to remove the separator character, by setting bit 8 of the last character.

One other feature is that synonyms can be made by adding a \* to the start of the synonym, for example:

    LIGH *BURN *IGNI

Rather than waste a whole byte to indicate this. We can set bit 8 of the first character to indicate that this word is a synonym of the previous one.

Finally, to make life easier, I'm going to separate the lists so that verbs and nouns are stored in separate locations.

### Rooms

Rooms are defined as 6 bytes to give the room pointers for each exit (in the order north, south, east, west, up and down) followed by a description string to give the room description.

There's not much we can do here to compress this data. One potential may be to allow the number of exits to be variable, but this needs further experimentation.

I am going to compress the text in the room description, this will be described later.

### Messages

The messages section just contains a list of messages. This is going to be text compressed (qv).

### Objects

Objects are listed as a string to defined the name of the object as seen in the game, which may have an optional noun attached; followed by a byte for starting location.

An example of an object with an attached noun is:

    Jewelled Knife/KNIF/

We will try and squash these by:

-   Compressing the text
-   Separating out the noun and storing the value as a byte (listing the noun number), or a 0 if no noun
-   Storing the room as a byte

### Text Compression

Text compression was often used in text adventures to ensure maximum space. When trying to choose the best algorithm several things need to be taken into account:

-   Size of text (as lots of text can give a much better dictionary for compression)
-   Size of dictionary
-   Complexity of encoding
-   Complexity of text
-   Complexity of decoding

If we look at other text adventures we can see a variety of schemes being used:

-   Robico used *Midge*, which was a dictionary compression scheme, which worked well due to the large amount of text.
-   The Quill used a dual byte token scheme, where two letters where replaced by a token
-   Infocom uses *ZSCII*, essentially a 3:2 encoding scheme where 3 characters are mangled into 2 bytes.

I did some messing with dictionaries, 2 character tokens, 3 character tokens etc and came to the conclusion that the compression that is easiest to decode, encode and got the best compression ratio is, similar to the Quill, to replace common repeated characters with a single byte token. The problem with this scheme is that the maximum compression ratio is 2:1; and we don't get anywhere near that!

My table of different tests:

| Scheme         | Messages | Rooms | Objects | Dictsize | Total |
|----------------|----------|-------|---------|----------|-------|
| Uncompressed   | 2282     | 1019  | 2379    | 0        | 5680  |
| Words          | 1799     | 710   | 1813    | 584      | 4906  |
| Letters        | 1619     | 700   | 1698    | 254      | 4271  |
| Mixed          | 1602     | 671   | 1663    | 385      | 4321  |
| Letters unnorm | 1572     | 684   | 1662    | 254      | 4172  |
| Letters 3      | 1701     | 651   | 1690    | 376      | 4418  |

| Scheme         | Messages | Rooms | Objects | Dictsize | Total |
|----------------|----------|-------|---------|----------|-------|
| Uncompressed   | 3972     | 1751  | 2945    | 0        | 8668  |
| Words          | 3061     | 1474  | 2448    | 657      | 7640  |
| Letters        | 2642     | 1160  | 1953    | 254      | 6009  |
| Mixed          | 2608     | 1160  | 1948    | 408      | 6124  |
| Letters unnorm | 2577     | 1032  | 1788    | 254      | 5651  |
| Letters 3      | 2609     | 794   | 1548    | 376      | 5327  |

I decided that the best results across a selection of games came from unnormalised letters, i.e. I don't mess around with them first. The algorithm for encoding is simple:

-   Go through all strings 2 letters at a time
-   Enter letters into a dictionary and count the number of occurrences
-   Sort the dictionary by largest counts
-   Take the top 127 entries; this is our final dictionary
-   Go through the strings again, this time by dictionary entries
-   Replace any matched characters with the token from the dictionary with bit 8 set

This also makes the decoding algorithm easy:

-   Go through the string
-   If bit 8 is set insert token
-   If bit 8 not set insert character

The other advantage is that the dictionary size is less than a page, so we can use an index register to find the tokens!

Finally we need to store the dictionary at the end of the file. As the dictionary entries are a known size, we can just place it as a stream with no separators.

## 14/11/2010: [Coding Starts](saga20101114 "wikilink")

## 15/11/2010: [More Coding](saga20101115 "wikilink")

## 16/11/2010: [Objects and Engine State](saga20101116 "wikilink")

## 19/11/2010: [More Compression](saga20101119 "wikilink")

## 22/11/2010: [Parsing Input](saga20101122 "wikilink")

## 26/11/2010: [Conditions](saga20101126 "wikilink")

## 01/12/2010: [Responses](saga20101201 "wikilink")

## 05/12/2010: [Play through!](saga20101205 "wikilink")

## 05/12/2010: [A Quick Mock-up](saga201012052 "wikilink")

## 12/12/2010: [Tidying up](saga20101212 "wikilink")

## 17/12/2010: [More additions and code reduction](saga20101217 "wikilink")

## 22/01/2011: [Not much stuff done](saga20110122 "wikilink")

## 13/02/2011: [Bug Fixing and Screen Layout](saga20110213 "wikilink")

## 14/02/2011: [Lone Survivor and Beta Release](saga20110214 "wikilink")

## 15/02/2011: [Graphics Routines and a Roadmap](saga20110215 "wikilink")

## 20/02/2011: [A Complete Master Version](saga20110220 "wikilink")

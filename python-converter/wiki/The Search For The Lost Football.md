# The Search For The Lost Football by Francis G. Loch

### Licence

Software licence TBC

### Introduction

_The Search For The Lost Football_ was a text adventure I originally wrote for the Amiga computer many moons ago, although it was never completed. After some recent discussions about text adventures in the forums here I had the urge to recreate my adventure game for the BBC Micro.

The basic synopsis of the game is that a young boy loses his football by kicking it through the window of an abandoned house. The game starts at the point of the boy attempting to break in and find his ball. The game includes the usual type of finding objects and solving puzzles associated with the genre.

The BBC Micro version of the game will not be a 100% accurate remake of the original Amiga version as it suffered from a number of game design flaws which will be amended.

[Play The Search For The Lost Football Pre-Release \#4 Online](http://www.retrosoftware.co.uk/jbeebapplet/)

[Discuss The Search For The Lost Football](http://www.retrosoftware.co.uk/forum/viewforum.php?f=29)

### Downloads

**_The Search For The Lost Football_**

[12th March 2008: Very early developmental version for testing purposes](./images/Football pre.zip "wikilink").

[18th March 2008: Early developmental version for testing purposes](./images/Football pre2.zip "wikilink").

[28th March 2008: Early developmental version for testing purposes](./images/Football pre3.zip "wikilink").

[6th July 2009: Early developmental version for testing purposes](./images/Football pre4.zip "wikilink").

[1st February 2011: Early developmental version for testing purposes](./images/Football pre5.zip "wikilink").

### Sample Screenshots

An early developmental screen shot:

![](./images/Football screenshot1.png "fig:Football_screenshot1.png")

Another early developmental screen shot:

![](./images/Football screenshot2.png "fig:Football_screenshot2.png")

### Change Log

Not released yet

### Diary

**Thursday 28th February 2008**

Since I no longer have the source code or plans for the original Amiga version I started trying to reconstruct the basics of the game design based on what I could remember.

**Friday 29th February 2008**

Started programming the game. So far the locations with basic descriptions are in place and the player has the ability to move between them.

**Friday 7th March 2008**

Added a basic text encryption/decryption routine so that locations, objects, etc. are not easily readable.

**Saturday 8th March 2008**

GregC was kind enough to provide me with some nice code enabling a dramatic speed up of my text routines. Thanks Greg! :)

**Sunday 9th March 2008**

Location descriptions are now stored as an external encrypted data file which can then be read from as and when required. Each location can have a description of upto about 1000 characters and the data file can cater for full or abridged versions of the descriptions.

**Tuesday 11th March 2008**

Minor improvement made to the encryption/decryption routine. Main game program rewritten to utilise the external encrypted data files and tidy up the layout of the screen. Added early development screenshot to wiki.

**Wednesday 12th March 2008**

Expanded the understood vocabulary to include 'GO' (e.g. 'GO NORTH') and 'LOOK'. Started programming the routines to handle objects. Started adding conditional restrictions on movement, e.g. not being able to go through a door unless it is unlocked. A very early developmental version has been released for people to try for feedback (see downloads above).

**Sunday 16th March 2008**

Improved the interpretation of user commands. Added 'INVENTORY' (or 'INV'), 'GET', 'TAKE' and 'DROP' to the list of understood commands. Also added the facility to toggle a clear screen when moving between locations by typing 'CLS'.

**Monday 17th March 2008**

Spent time going over the game's design making revisions to the content to improve the overall game play. The original Amiga version was criticised for being too difficult too early on in the game so the puzzles have been reworked to hopefully make the game easier to get into.

**Tuesday 18th March 2008**

New screen shot added showing off some of the new features such as the objects and inventory. Added 'EXAMINE' to vocabulary so player can now examine objects. Updated the 'get object' routine so that some objects cannot be taken, e.g. if something is too heavy to be carried. Released a newer developmental version for people to try for feedback purposes (see downloads above).

**Wednesday 19th March 2008**

Added 'LOAD' and 'SAVE' to the command list so that the player can now save their progress.

**Wednesday 26th March 2008**

Programmed a separate utility which allows the user to customise the colouring of the various types of text in the game.

**Friday 28th March 2008**

Changes made to cater for the new customised colours created using the colour editor utility. Coloured text can now also be toggled by typing 'COLOUR'. New developmental version available for download for feedback purposes.

**Saturday 29th March 2008**

Incorporated a new text engine which can now word wrap text dynamically rather than using preformatted text.

**Friday 4th April 2008**

Spent time refining and optimising some of the code. Known bugs and some redundant code removed. Improved the storage of location data to remove unnecessary data.

**Wednesday 23rd April 2008**

Redesigned the text parser to allow for a more flexible and natural input. Rather than using a simple verb-noun syntax, e.g. 'GET KEY', it is possible for the player to use more complex instructions such as 'PICK UP SWORD AND THEN SLAY THE DRAGON'.

**Thursday 1st May 2008**

Commas can now also be included in commands, e.g. 'PICK UP THE SWORD, KILL THE DRAGON AND THEN GET THE TREASURE'. This involved me writing my own text input routine since the BBC Micro's standard INPUT command cannot handle commas in this context. Also made a number of other improvements and bug fixes to the text parsing engine.

**Friday 2nd May 2008**

Updated the text parser to be able to handle indirect objects, e.g. 'KILL THE DRAGON WITH THE SWORD' where the sword is the indirect object in this case (the dragon would be the direct object).

**Friday 9th May 2008**

Started the process of converting some of the existing BASIC code into assembler primarily for reasons of execution speed.

**Monday 12th May 2008**

Made some improvements to the text wrapping routine.

**Monday 6th July 2009**

Released a new developmental version of the current snapshot of the game (see downloads section above).

**Sunday 30th January 2011**

Just to let everyone know that things are still progressing with this game. I've just recently added a new feature that utilises shadow screens so that systems with shadow memory can optionally use screen modes other than mode 7. I also discovered an overflow bug in the encryption algorithm which has now been fixed. I'm also looking at removing the dependency on loading location data from the disc so that a cassette version of the game will be possible.

**Monday 31st January 2011**

Location data is now loaded in a single load rather than continuously reading it from the disc whenever the player moves location. I'll need to see how feasible it is to keep things this way once the location descriptions are fleshed out or whether I will need to look at compressing the data.

**Tuesday 1st February 2011**

Started fleshing out some of the gameplay a bit, particularly at the start of the game. Messages are now encrypted too so players are less likely to get clues by just listing the program.

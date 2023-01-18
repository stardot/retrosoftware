# Adventurescape V by Paul Aslin

### Licence

Software licence TBC

### Introduction

An improved version of the *Adventurescape* interactive fiction engine, which was originally published in the 8-bit Acorn magazine *A&B Computing*. Several games built with the system including *Amnesia*, *Lost in Xanadu*, *The Cube of Zoth*, *Pirate's Peril*, *Stranded!* and *Rise in Crime* were either subsequently published in the same magazine or released commercially by software houses like [Heyley Software](http://www.vocks.org.uk/heyley/) and Robico Software. An improved disc version of the engine was also published in later issues of *A&B Computing*.

I played around with the original *Adventurescape* generator at school, but for reasons best known to itself I couldn't actually make it produce a working game at the end. I recall a wad of paper notes, hand drawn map, etc. and I do still have a print out of what I made all those years ago, though its not that good to be honest. No matter - I wanted to play around with the system anyway. Looking back, I had forgotten what a pain it is to make everything with the original system, including that annoying four letter verb limit! Most people have Compact Flash cards and the like, so disk space for such games is also no longer such an issue. In the end, I hope it should at least be fun to use the *Adventurescape II* generator once I get rid of all the enter filename, enter item short name, Y/N nonsense everywhere.

[Discuss *Adventurescape V*](http://www.retrosoftware.co.uk/forum/viewforum.php?f=65)

### Planned Features

-   No limits on word length for verbs and objects \[sample code complete\]
-   Upgrade the naming method and general editing on objects.
-   Standardise datafile names, should be 4 letter game name and 3 letter type. eg: xxxxloc xxxxmes etc, and put each game file set in its own directory.
-   Generally fix workflow in game editor, eg enter game name once instead of 4 or 5 file names over and over.
-   Fix bugs which leaves files open when an error occurs (really annoying).

**New features not in the original *Adventurescape* release:**

-   Option for game images (static in graphic window)
-   auto menu for games, just copy the game's folder over and the main menu finds it.
-   Some sort of text based automap, even if only for the editor.
-   import and upgrade adventures made with earlier releases of Adventurescape (maybe)

### Sample Screenshots

<table>
<tbody>
<tr class="odd">
<td><p>[[Image:AdventurescapeIIPuzzleEditorConditions.jpg|375px|<em>'Adventurescape V replacement Puzzle Editor conditions screenshot <strong><br />
<em>Posted: 02:43, 5 Jan 2011</em>]]<br />
</strong></em>Adventurescape V'' replacement<br />
Puzzle Editor conditions screenshot<em>'<br />
</em>Posted: 02:43, 5 Jan 2011''</p></td>
<td><p>[[Image:AdventurescapeIIPuzzleEditorActions.jpg|375px|<em>'Adventurescape V replacement Puzzle Editor actions screenshot <strong><br />
<em>Posted: 02:43, 5 Jan 2011</em>]]<br />
</strong></em>Adventurescape V'' replacement<br />
Puzzle Editor actions screenshot<em>'<br />
</em>Posted: 02:43, 5 Jan 2011''</p></td>
<td><p><br />
</p></td>
</tr>
</tbody>
</table>

### Sample Video

Coming soon

### Playable Demo

Coming soon

### Development Diary

#### July 2010

*31st July*
Not much work done on the code today, was fixing my rom cartridge. However I do have a function to convert strings to all caps. Going to use it to convert item names so a copy can be in uppercase in memory but not on the drive, needed for text input decoding.

I'm looking at the code used in xanadu which is v 1.1, will have to look at a v2 game as well and see how that works.

The code isn't too bad, uses procedures but the text input string processing code seems spread everywhere and could be a lot better. S$ is used for both input strings and strings printed on screen, which will need fixing.

*4th August*
I've added back in code from Xanandu (adventurescape 1.5) a bit at a time with some tweeks and var renaming. The renaming was needed as it was very hard to follow the code with var names like Cy% (object state).

Blocks reinstalled are: a) get/drop object b) examine object c) look d) inventory e) the puzzle code, though not working yet some minor bugs to find. f) move, I changed the byte ordering so its NESWUD instead of NEWSUD, so its like a compass.

The verb list also allows the disabling of inbuilt commands, 'wear' for examine, need to relocate the 'I don't know how to xxx' code as a result though. I added some extra code to allow worn items to be removed rather than just dropped.

#### August 2010

*7th August*
Currently stuck on the Puzzles section of the code, some undocumented flags in there. The editor doesn't really describe what they do, and neither does the code.

Editor still doesn't create a working adventure, not entirely sure why. So going to try plugging values directly into the arrays in version 3.0 code I'm working on. Should have a working adventure soon then.

#### October 2010

*23rd October*
Finally [found](http://nvg.org/bbc/sw/AB/Adventurescape-disk.zip) the information I needed on the file format etc, in the 'generator' folder is a subfolder called 'X' ie generator.X

#### November 2010

*7th November*
Spent this weekend working on reading and writing the data files that store all the messages, rooms, objects, puzzles etc. Prior to this I just had all the array data stored in a big proto, which was getting unwieldy.

Messages and rooms were easy, as they are single files containing only that data. The rest of the data is just lumped into the puzzle file in one big lump. A pointer system keeps track of what is stored where, plus what is actually used, eg objects used 4 out of 50.

Its all very complicated so I'm using what I can from the original code, which means digging around in various files to find the nicely written procs.

So now I have all the data for a basic test game loaded into a set of procs that produce the end output. Its not finished yet so it does crash the editor, but works fine in the datadump programs I wrote to investigate this mess.

Next stage is to make sense of this pointer system, as I have to re-write that soon to store longer verbs and fix a few other problems. At the moment verbs are stored as 4 letter words, which means more 4 letter words :twisted: while I try and increase that to 12.

*11th November*
Turns out fixing the verb length was the only easy part. So now it can use words like 'examine', I also discovered the code I'm using at the moment copes with multi word items, say "pay 5 dollars"

The locations file format had to be rewritten for various reasons. It was slow to write the entire file and would sometimes crash the file system. So its now faster and less bloated code wise. The "write" program actually plays nicely now with \*CLOSE thrown into line 65 under the comments.

I did a general clean up of the code, got rid of a lot of duplicated stuff. Weird programming style, its as if different people wrote each separate basic listing. Some sort of attempt to use the same variable names, but some naming conflicts.

Plus I have a piece of paper with the first proper adventure planned out on it. Some annoying puzzles for you already. lol Actually has a long story behind it all, not just blundering around trying to escape from something.

*23 November*
Been some pretty major changes to the code base, it is actually a lot neater now. Not sure if it still looks the same, the text colours etc, as I've not really been checking that. I've made some changes so it can support coloured text in none Mode7 displays.

#### December 2010

*26th December*
Had a bit of a disaster since my last post, involving a corupted NFS volume (I use a Level 3 Fileserver sometimes). Being a NFS volume there is no limited to no tools to help recover files. Hence I had to write my own, which while having bugs allowed me to recover much of what was lost. The dreaded Bad Folder bug.

But first an explanation of what files currently exist for this project. The program files consist of three main programs, ADV4 - adventure game itself, ADV4W - writes adventure game datafiles, ADV4R - reads adventure game datafiles. Now all the game data itself is stored in binary format, but ADV4W contains this in a usable format (basic arrarys etc). In addition there are backups of the 'data' sections of basic from ADV4W stored in a backup folder, in plain text form (\*EXEC data).

Anyway, in the process of backing up several weeks worth of changes to a second CF card the original became corrupted. This resulted in the loss off ADV4W, the current ADV4R and ALL data files that contained the test adventure. This test adventure alone would take a week to rewrite, and I'd effectively lost the ability to make new datafiles. Hence recovering the files was the only real option, nothing to loose trying.

Multiple fragmented sections of ADV4W were located, with 20 lines of missing write file code being replaced with altered ADV4 read file. All the missing basic text files with the game data in was also found, so be it slightly out of date.

#### April 2011

*11th April*
tautology discovered first issue of Disk User contains an advert for "Adventurescape III", so suggests skipping to "V" to avoid any issues. Will involve changing various directory/forum names and redoing the graphic. The game itself is using version 5 (beta 5) internally anyway.

I now have extra BBC Master hardware, so can now implement plans to add Econet multiplayer and second processor support to the game. Special thanks to the individual that donated a working Master Turbo and so much needed spare parts for the machines I have.

The second processor being required for the game to run on a Model B in non mode7 graphics modes. While the Master has shadow ram (the Model B doesn't have that luxury unless its a B+) the planned loading of graphics screens requires some way to access the shadowed ram.

*25th April*
Been experimenting with loading images into Shadow screen memory direct from disk. Actually way easier than I expected, but still pondering why it doesn't work with DFS when it does with ADFS. It works over the TUBE as well, as it offloads all the work to the host machine.

Not sure the ADFS only code is major problem, as the game system is really something best used on a CF type setup, especially if multiple games are installed.

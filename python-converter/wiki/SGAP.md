# System-Generated Adventures and Ports by Andy Ford

### Licence

Freeware (game database sources included)

### Introduction

In 2011, I started a conversion of the Spectrum game *[Urban Upstart](http://www.worldofspectrum.org/infoseekid.cgi?id=0007149)* to the BBC Micro. I started by looking at a direct port of the underlying code, before choosing to switch to recreating the game using the *[Graphic Adventure Creator](wikipedia:Graphic_Adventure_Creator "wikilink")* system to avoid some of the tricky issues that I'd encountered. I found the GAC package to have its own idiosyncrancies, and in the meantime I used the text-only system *[The Quill](wikipedia:The_Quill "wikilink")* to produce BBC Micro ports of two other adventures, originally built with *[The Quill](wikipedia:The_Quill "wikilink")* system for the ZX Spectrum - *Galaxias* and *Project-X: The Micro Man*. Despite not having played with *The Quill* system on other platforms such as the C64 or Amstrad, I had used it a little on the Spectrum back "in the day" so to speak, so I was fairly sure these conversions would be easy.

After getting these two titles out, I have returned to *Urban Upstart* and decided it will be simplest to re-start the project again, this time using *The Quill*.

On my potential list of projects, in no particular order, I am also considering these ZX Spectrum adventures as possible future ports:

*[Madcap Manor](http://www.worldofspectrum.org/infoseekid.cgi?id=0006624)*
*[Orc Island](http://www.worldofspectrum.org/infoseekid.cgi?id=0006768)*
*[Rifts Of Time](http://www.worldofspectrum.org/infoseekid.cgi?id=0006892)*
*[Sealed City](http://www.worldofspectrum.org/infoseekid.cgi?id=0006937)*
*[The Traveller](http://www.worldofspectrum.org/infoseekid.cgi?id=0010947)*
*[Urquahart Castle](http://www.worldofspectrum.org/infoseekid.cgi?id=0007150)*

<span style="font-variant:small-caps">**Request for Help: All of these ports suffer from not having a save/load function, which really requires an original disc copy of *The Quill* for the BBC Micro to generate the game, but I have yet to track a copy down. Please let me know in the forum, if you can help get hold of a copy.**</span>

[Discuss *System-Generated Adventures and Ports*](http://www.retrosoftware.co.uk/forum/viewforum.php?f=89)

### Adventures

#### Urban Upstart

**''BBC Micro port using *[The Quill](wikipedia:The_Quill "wikilink")* by Andy Ford from an [original Spectrum game](http://www.worldofspectrum.org/infoseekid.cgi?id=0007149), by Pete Cooke and published by *Richard Shepherd Software Ltd* in 1983.**''

##### Downloads

This conversion is currently "on hold" until at least two of the other ones listed above are completed partly due to the need to completely rewrite it again via Quill instead of GAC.

##### Port Details

There's a few issues with this conversion. Although the game is 80% BASIC, the location map, object map and graphics are stored in assembled machine code. I could not find an easy way of turning these into a useable form. I had initially planned on using a single byte for movement by using a bit for NSEWUDIN (North / South / East / West / Up / Down / In / Out) to save space. After converting the extracted BASIC and fixing a few things up, it did sort of work but it seemed too much trouble so I decided to re-create it with the BBC Micro version of *[Graphic Adventure Creator](wikipedia:Graphic_Adventure_Creator "wikilink")* instead - a package I'd used before years ago. I got as far as inserting all the room descriptions, creating an initial movement table, created an object and got a rough loading screen up. I also changed the room map around by drawing on an existing game map so I knew what went where etc. After all this though, I decided to re-start the conversion using the - albeit slightly cruder - *The Quill* package instead, as the GAC project simply became too short of memory and had other annoyances.

A solution to the adventure is available [here](http://www.the-tipshop.co.uk/cgi-bin/info.pl?wosid=0007149).

##### Screenshots

<table>
<tbody>
<tr class="odd">
<td><p>![](./images/UrbanUpstart1.jpg)
<strong>BBC Micro <em>Urban Upstart</em> early loading screen</strong><br />
<em>Posted: 16:07, 31 Jul 2011</em></p></td>
<td><p>![](./images/UrbanUpstartLoadingScreen.png)
<strong>BBC Micro <em>Urban Upstart</em> loading screen</strong><br />
<em>Posted: 11:45, 22 Jun 2012</em></p></td>
</tr>
<tr class="even">
<td><p>![](./images/UrbanUpstart2.jpg)
<strong>BBC Micro <em>Urban Upstart</em> screenshot #1</strong><br />
<em>Posted: 18:35, 04 Oct 2011</em></p></td>
<td><p>![](./images/UrbanUpstart3.jpg)
<strong>BBC Micro <em>Urban Upstart</em> screenshot #2</strong><br />
<em>Posted: 18:35, 04 Oct 2011</em></p></td>
</tr>
<tr class="odd">
</tr>
</tbody>
</table>

#### Galaxias

**''BBC Micro port using *[The Quill](wikipedia:The_Quill "wikilink")* by Andy Ford with the kind permission of original Spectrum author, Fergus McNeill. Original published by *Delta4 Software* in 1986.**''

##### Downloads

[*Galaxias* BBC micro port, release B27](./images/GalaxiasB27.zip "wikilink") - DFS disc version incl. database for The Quill
Created from: [*Galaxias* textual data output](./images/GalaxiasUnPAWSOutput.zip "wikilink") from [UnPAWS](http://www.ifarchive.org/indexes/if-archiveXprogrammingXquill.html) tool used with the [original Spectrum *Galaxias*](http://www.worldofspectrum.org/infoseekid.cgi?id=0006344) database

##### Port Details

It was not \*that\* bad to port this title, although I had to manually change the IDs then constantly cross reference as they were not identical on a 'B vs a Spectrum. All good fun (and headaches!) =D&gt;

As a quick note: One thing that is (purposely) missing is save / load as they were originally tape routines. I will try to add them as disc features later but, as it's about 'OK' as it is, I figured most people would be using an emulator so it wouldn't be an issue to use a save state. What would be best for this would be to use an original disc copy of *The Quill* for the BBC Micro to generate the game, but I have yet to track a copy down.

It's not a difficult game, although as usual there are a few traps for the unwary. I did actually think I'd missed a few things out after trying it with a solution but, no, it's quite possible and originally intended to be completable without doing all the 'extra' stuff. Exploring is part of the fun, anyways. :)

A solution to the adventure is available [here](http://www.the-tipshop.co.uk/cgi-bin/info.pl?wosid=0006344).

##### Screenshots

<table>
<tbody>
<tr class="odd">
<td><p>![](./images/GalaxiasLoadingScreen.png)
<strong>BBC Micro <em>Galaxias</em> Retro Software loading screen</strong><br />
<em>Posted: 17:40, 18 Feb 2012</em></p></td>
<td><p>![](./images/G1.jpg)
<strong>BBC Micro <em>Galaxias</em> loading screen</strong><br />
<em>Posted: 14:18, 30 Oct 2011</em></p></td>
</tr>
<tr class="even">
<td><p>![](./images/G2.jpg)
<strong>BBC Micro <em>Galaxias</em> instructions screen</strong><br />
<em>Posted: 14:18, 30 Oct 2011</em></p></td>
<td><p>![](./images/G3.jpg)
<strong>BBC Micro <em>Galaxias</em> screenshot #1</strong><br />
<em>Posted: 14:18, 30 Oct 2011</em></p></td>
</tr>
<tr class="odd">
<td><p>![](./images/G4.jpg)
<strong>BBC Micro <em>Galaxias</em> screenshot #2</strong><br />
<em>Posted: 14:18, 30 Oct 2011</em></p></td>
<td><p>![](./images/G5.jpg)
<strong>BBC Micro <em>Galaxias</em> screenshot #3</strong><br />
<em>Posted: 14:18, 30 Oct 2011</em></p></td>
</tr>
</tbody>
</table>

#### Project-X: The Micro Man

**''BBC Micro port using *[The Quill](wikipedia:The_Quill "wikilink")* by Andy Ford from an original Spectrum game, by Jon R. Lemmon and Tim Kemp and published by *Compass Software* in 1985.**''

##### Downloads

[*Project-X: The Micro Man* BBC micro port, release B25](./images/ProjectXMicroManB25.zip "wikilink") - DFS disc version incl. database for The Quill
Created from: [*Project-X: The Micro Man* textual data output](./images/ProjectXMicroManUnPAWSOutput.zip "wikilink") from [UnPAWS](http://www.ifarchive.org/indexes/if-archiveXprogrammingXquill.html) tool used with the [original Spectrum *Project-X: The Micro Man*](http://www.worldofspectrum.org/infoseekid.cgi?id=0006828) database

##### Port Details

*A fantastic voyage where life itself is a nightmare. Experience the frustration of needed a superhuman effort to do even the simplest of things.*

Another Spectrum conversion to our platform. The original is a *Quill* and *Illustrator* game although it has been modified with both *Patch* and *Press* (not available for the Acorn platform) so its not as straightforward as it should be as it plays with the database a bit to say the least. :D Although, between the two platforms there are certain hardcoded flags that do not perform the same function anyway so a lot of the conditionals I've had to figure out and rewrite from scratch, and it's a fairly large game too. It's a squeeze. The conversion process was quite annoying due to differences between the ZX Spectrum version of *The Quill* and the BBC Micro version. In particular, functions are missing in the 'B version so I've had to be creative to say the least, not to mention the addition of *Patch* / *Press* playing about with the original *Quill* database once I'd extracted it. Much headaches :lol:

It was not that bad but some flags have different purposes, in particular one flag on the ZX is decreased per turn (but not below zero, so you can set it to x and then do a test for zero later on etc) but that one is used for the current room ID on the BBC version, which lacks said turns flag unfortunately, much fun. :) The BBC version is actually a lot easier to work with compared to the ZX version, although to be fair that one offers a bit more colour etc. Extracted databases are a bit strange too in that message IDs are incorrect, I usually add + sys messages to them, so if there are 30 system messages then what would be message 10 would be message 40 etc obviously have to change all the conditionals around. Another thing is using *Patch* / *Press* which afaik is a ZX only addon. It seems to mess the event / status tables up when extracted so I have to read them all carefully and cross reference them to be sure. Usually by playing the game via a solution on a Spectrum emulator to be sure its right.

I'm pleased to have finished this conversion though and, hopefully, it's bug free. It's quite a fun albeit sometimes slightly difficult adventure with traps for the unwary. It's taken quite a considerable time to do this one given its relatively complex nature. I was not able to contact the original authors unfortunately although, given the original has been floating around for years, I did not see any issue.

I may update it with a loading pic (cannot use ZX Spectrum one) at a later date although the story is shown on the crude loader I whipped up, anyway.

As a quick note: As with Galaxias, the save / load functions are missing as they were originally tape routines. I will try to add them as disc features later but, as it's about 'OK' as it is, I figured most people would be using an emulator so it wouldn't be an issue to use a save state. What would be best for this would be to use an original disc copy of *The Quill* for the BBC Micro to generate the game, but I have yet to track a copy down.

A solution to the adventure is available [here](http://www.the-tipshop.co.uk/cgi-bin/info.pl?wosid=0006828).

##### Screenshots

<table>
<tbody>
<tr class="odd">
<td><p>![](./images/ProjectXMicroManLoadingScreen.png)
<strong>BBC Micro <em>Project-X: The Micro Man</em> loading screen</strong><br />
<em>Posted: 17:40, 18 Feb 2012</em></p></td>
<td><p>![](./images/ProjectXMicroMan1.png)
<strong>BBC Micro <em>Project-X: The Micro Man</em> instructions screen</strong><br />
<em>Posted: 15:04, 12 Feb 2012</em></p></td>
</tr>
<tr class="even">
<td><p>![](./images/ProjectXMicroMan2.png)
<strong>BBC Micro <em>Project-X: The Micro Man</em> screenshot #1</strong><br />
<em>Posted: 15:05, 12 Feb 2012</em></p></td>
<td><p> </p></td>
</tr>
</tbody>
</table>

#### Micro Man II: The O Zone

**''BBC Micro port using *[The Quill](wikipedia:The_Quill "wikilink")* by Andy Ford from an original Spectrum game, by Jon R. Lemmon and Tim Kemp and published by *Compass Software* in 1986.**''

##### Downloads

[*Micro Man II: The O Zone* BBC micro port, release B22](./images/Ozone B22.zip "wikilink") - DFS disc version incl. database for The Quill

##### Scenario

*Professor Neil Richards, a brilliant scientist working on top secret miniaturisation experiments - code named Project-X, has mysteriously vanished from his countryside laboratory. Your task is a simple one...As the world Intelligence Network's leading secret agent you must solve the mystery of Professor Richards disappearance, and if possible recover the missing Project -X papers! Agent 37, you will hardly need reminding that your mission will be extremely dangerous! Success in finding Professor Richards before he does something catastrophic whilst in his highly irrational state is all important*

##### Port Details

Another Spectrum conversion to our platform. The original is a *Quill* and *Illustrator* game although it has been modified with both *Patch* and *Press* (not available for the Acorn platform) so its not as straightforward as it should be as it plays with the database a bit to say the least.

The conversion process was a little bit easier this time due to having already converted the first Project-X. The usual changes apply such as renumbering the messages and some of the vocabulary too, to ensure it all functions correctly on another platform.

I'm again pleased to have finished this next conversion though and I hope it is bug free. Again, I was not able to contact the original authors unfortunately although, given the original has been floating around for years, I did not see any issue.

I was unable to use the existing loading picture although I created something that looked not too far off the original though, but in Mode0 for a reasonable resolution.

I have left the tape save / load routines present this time. What would be best for this would be to use an original disc copy of *The Quill* for the BBC Micro to generate the game, but I have yet to track a copy down.

A solution to the adventure is available [here](http://www.the-tipshop.co.uk/cgi-bin/info.pl?name=O%20Zone%2c%20The).

##### Screenshots

<table>
<tbody>
<tr class="odd">
<td><p>![](./images/Ozone1.png)
<strong>BBC Micro <em>Micro Man II: The O Zone</em> RS loading screen</strong><br />
<em>Posted: 17:40, 17:37, 24 Jun 2012</em></p></td>
<td><p>![](./images/Ozone2.png)
<strong>BBC Micro <em>Micro Man II: The O Zone</em> instructions screen</strong><br />
<em>Posted: 17:38, 24 Jun 2012</em></p></td>
</tr>
<tr class="even">
<td><p>![](./images/Ozone3.png)
<strong>BBC Micro <em>Micro Man II: The O Zone</em> screenshot #1</strong><br />
<em>Posted: 17:38, 24 Jun 2012</em></p></td>
<td><p> </p></td>
</tr>
</tbody>
</table>

#### Subsunk

**''BBC Micro port using *[The Quill](wikipedia:The_Quill "wikilink")* by Andy Ford from an original Spectrum game, by Peter Torrance and Colin Liddle and published by *Firebird Software Ltd* in 1985.**''

##### Downloads

COMING SOON

##### Port Details

A solution to the adventure is available [here](http://www.solutionarchive.com/game/id%2C524/Subsunk.html).

##### Screenshots

![](./images/Subsunk1.png)
**BBC Micro *Subsunk* loading screen**
*Posted: 17:40, 21:36, 2 Jul 2012*

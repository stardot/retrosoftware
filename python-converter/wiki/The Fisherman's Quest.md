# The Fisherman's Quest by Paul Dryden

### Licence

Software licence TBC

### Introduction

Tarn has lived on the coast of Arcila all his life, along with his sister and father. His mother is only a distant memory having been murdered when he was only a baby by Quedarn Pirates after they raided his village.

The land of Arcila has fallen on bad times; the new king has stripped it of its wealth and has forced its people into slavery, to fuel his own greed for richness and power.

One day while fishing Tarn and his father find a wooden box floating strangely in the water. Inside is a scroll and key, the latter inscribed with strange symbols.

Been poor fisherman neither Tarn nor his father can read the scroll, so they take it into the city hoping that maybe someone can read it for them. Unfortunately a rogue conman steals the scroll and takes it to the king hoping to sell it. There a wise man of the king’s court is able to decipher the scroll.

The scroll describes a land far North across the sea where an object has been hidden from all man, this object used in the right way can wield great power. The object was hidden by settlers from another world, hundreds of years ago, in a place called 'The Tears Of The Moon', behind the 'Door Of Secrets'.

The king driven by the prospect of more power and wealth orders his guards to find Tarn's father and bring them to the castle. That night while Tarn is out his father and sister are arrested and taken to the castle.

The king believing that Tarn's father knows where the land is, tortures him for information, after several days without learning anything the king gives up and throws him into the dungeon to rot until he will confess. The king then forces Tarn's sister to be his bride or he will kill her father.

Tarn knows that he alone can never rescue his father or sister and that the only hope is for him to travel across the sea and find this place called 'The Tears Of The Moon'. Find the object and hopeful bring it back in exchange for his fathers and sisters lives. He has but one hope over the king, he still has the key!

Knowing only that he must travel North, Tarn sets of in his father’s boat....

### Expected Features

- A text/graphic adventure for an enhanced Electron with 64k.

- Disk based for loading of pictures.

- Several Chapters covering the life of the central character.

- Load / Save option.

- Alternative endings to each chapter making several possible different outcomes to the story.

- 3 different scoring systems - Quest,Treasure and Honour.

- Hint system.

[Discuss The Fisherman's Quest](http://www.retrosoftware.co.uk/forum/viewforum.php?f=28)

### Downloads

**_The Fisherman's Quest_**

Not released yet.

http://www.retrosoftware.co.uk/???

### Sample Screenshots

This is a very early working demo of a split screen page.

![](./images/dragon4.jpg "dragon4.jpg")

### Diary

**Saturday 2nd Febuary - The story so far.**

Wiki page started, please feel free to point out any spelling mistakes, I do apologise in advance if any creep in. I will try to keep my diary upto date with what is going on. If people think that its getting boring let me know and ill stop.

There are are two main parts to the programing. The first is the main text engine which covers everything that is displayed on screen as well as commands that are typed in by the user and the responses that are given. Also within this is all the data handling for the locations as well as the puzzles. The second is basicly the displaying of pictures for locations. Other small parts which will be added upon near complition are saving and loading of game possition and scoring and hints, these last two play an important part in the game, I will go through these at a latter date.

After 3 weeks of programing the game text engine is starting to take shape, the player can now walk around the locations. Objects and props are where they should be, but few can be interacted with. So far the game understand the commands 'N,S,E,W' also 'Read' and 'Examine'.

Allthough two basic concepts for displaying pictures have been designed (Full & Split Screen), I have yet to decide which suits the game better, my personal feel is towards 'Full' though opinion amongs others is divided. I have decided today to leave the pictures section for a while until the main engine of the game is complete. This will make it easier to test, debug and _spell check_

**Wedensday 6th Febuary - Enhancements**

Added the word's 'Inventory','Get' & 'Drop' plus some variations, ie 'Carrying' for 'Inventory' and 'Inspect' for 'Examine'

Bit more work done on the concepts of the word 'Examine' now certain objects examined from where you stand can be examined more closely when held in your hand, for example.

If you _Examine_ a bottle that is on a table, the response could be, _The Bottle is red in colour._

However if you _Examine_ a bottle that you have picked up, the response might be, _After a closer look you notice the bottle in fact contains a red liquid._

Im hoping this will make the world more realistic.

**Sunday 17th Febuary - Maps & Letters**

Lots been done this week, the interpreter now understands around 50 words, though there is still a lot to do and I foresee another couple of months alone just getting this right. Have also added a map feature and an alphabet that you learn as you progress. Maps will be displayed like pictures by basically just typing for example 'Castle Map'. There are going to be several maps all with unique names. (Though no castle map!). The alphabet is a little different and totally unique to a BBC/Electron adventure. You can collect various scrolls which when read initially will display only symbols, as you travel around the game you will learn what the symbols actually mean, this is an automatic feature that does not require you to solve any puzzles. The scrolls will give more of an insight to locations as apposed to hints to various puzzles.

Also in the last couple of days, Ive added a few condition's to some of the props that appear. You can now fill a container (bottle,vial,bucket, ect) from any water source that you come across. Torches and lamps will eventually burn out once lit, again these can be lit from any source of fire.

To test things I've been using an adventure with only two rooms, this way I can test the various words and conditions without having to travel through the whole adventure. I basiclly just place any prop I want to interact with in the room one then test if what I want to do actually happens, the second room comes in handy if what you do in room one changes an event in room two.

I had wanted to wait until I had the interpreter almost finished before I started adding rooms and descriptions, but there are things that need to have all rooms present, like other characters that move around. So Ive mapped out the first chapter and this week hopefully will start putting all the different parts together. Hopefully get a few more screenshots up.

**Wedensday 27th Febuary**

With the first chapter locations now in place more work can start on the difficult parts of the game engine. Characters now move freely around the game, these can be interacted with in various ways. Also this week we have another feature unique to BBC/Electron games, ‘Weather’, now this isn’t just there to make the game more realistic it’s an important part of the game and in some cases important to puzzles. Weather is unique to locations and changes with time. The main engine of the game is now quite large, there are still things that need to be added and some to be fine tuned but overall it’s looking real good. So far everything still works on a normal Electron, but with still lots to add eventually I will be using the extra memory of an expanded 64k machine.

### Change Log

Not Released Yet

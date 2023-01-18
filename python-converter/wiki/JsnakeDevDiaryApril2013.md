[&lt;----Back to JSnake Dev Diary Index](JSnakeDevDiary "wikilink")

## Wakefield RISC OS Show – April 2013

I wanted to show off the game at the Wakefield Acorn/RISC OS show. There was a slight snag. I’d written the high score code as a separate program (to ease debugging). The show was on Saturday, so I arrived Friday and stayed in the hotel where the show was. I didn’t sleep well. This may have been due to supping a few beverages (and engaging in “discourse” with some RISC OS enthusiasts, much to the amusement of some in the bar :-) ). I ended up in a café at 7am on the Saturday morning, drinking much coffee, nursing a hangover, and trying to graft the high score table on to the game in time for the show. NEARLY did it, but I had a bug that I wasn’t able to solve in time.

I was a bit disappointed, but work continued on the code for a week thereafter. I solved the bug, so I had a working high score table in the game. At this point the game was pretty much “done”…but I wanted to add a bit of spit and polish before release.

## July-September 2013

- Added joystick support.

- Finally added some sound (rudimentary, but at least it’s there!)

- Made the Intro and Hi Score table screens more colourful

#### Food

The food at this point was still a yellow square. I still wasn’t using sprites at this point. I decided to change this as plotting individual pixels in code becomes tedious after a while. I used Richard Talbot-Watkins’s excellent [Beebspriter](http://www.retrosoftware.co.uk/beebspriter) . I decided that the food should be a lemon. Why? Because my collision detection is done by colour (the “old” food was yellow and a lemon is yellow) and a lemon is easy to draw! I had to amend the collision detection as it only handled yellow squares.

![](../../retrosoftwarecouk_wiki-20160918-wikidump/images/Jsnake lemon beebspriter.png)

#### Crashing

I made the screen background flash black and white when the Snake crashes in to itself or screen border.

### August 17 2013. Stardot hardware hacking meetup

#### V 1.0

I was going to go to this meetup but couldn’t make it due to family commitments. I sent a copy of v1.0 jsnake to Arcadian and Samwise for testing and requested photos of people playing the game. The full set can be seen [here](http://www.retrosoftware.co.uk/forum/viewtopic.php?f=94&t=844&sid=5ba3a71754f4e51b01ae2c4fe261e344) . with a screenshot below. I had some constructive feedback via Samwise. The awesome Atom man Kees van Oss had tried playing the game via joystick and found that the response was too insensitive for analogue joysticks: i.e. one had to push the stick too far before the direction was recognised. The speed of the snake was also commented on (big speed jumps). I have set the score threshold higher before speed increases, but behaviour is otherwise the same. I don’t have the coding skillz as yet to make the snake speed more gradual with smooth animation.

![](../../retrosoftwarecouk_wiki-20160918-wikidump/images/JSnake 001 Beebmaster.JPG)

### September 2013

#### Release

Having spent many hours on this over the course of more than a year, I’ve decided to release this as “v1.01” of JSnake. I’d like to move on to write another game which is more sophisticated. Jsnake could still be modified and I may decide to in the future.

Ideas for future expansion:

- Food shrinking in size over time, like Acornsoft Snake

- Obstacles – like HyperVyper

- Better sound

- In game music

- Better graphics

- Better snake (perhaps a head for the snake instead of a thick green line)

- Better food – different food types?

I hope you enjoyed reading the diary, and hope you enjoy playing my first game written in assembler.

Thanks,

Jbnbeeb, September 14, 2013.

#### February 2014 Minor update - bugfixes

Version 1.02 released with bugfixes and RS logo branded load screen following feedback from Samwise.

[&lt;----Back to JSnake Dev Diary Index](JSnakeDevDiary "wikilink")

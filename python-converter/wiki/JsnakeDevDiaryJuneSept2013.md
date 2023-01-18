## July-September 2013

- Added joystick support.

- Finally added some sound (rudimentary, but at least it’s there!)

- Made the Intro and Hi Score table screens more colourful

#### Food

The food at this point was still a yellow square. I still wasn’t using sprites at this point. I decided to change this as plotting individual pixels in code becomes tedious after a while. I used Richard Talbot-Watkins’s excellent [Beebspriter](http://www.retrosoftware.co.uk/beebspriter) . I decided that the food should be a lemon. Why? Because my collision detection is done by colour (the “old” food was yellow and a lemon is yellow) and a lemon is easy to draw! I had to amend the collision detection as it only handled yellow squares.

#### Crashing

I made the screen background flash black and white when the Snake crashes in to itself or screen border.

## August 17 2013. Stardot hardware hacking meetup

#### V 1.0

I was going to go to this meetup but couldn’t make it due to family commitments. I sent a copy of v1.0 jsnake to Arcadian and Samwise for testing and requested photos of people playing the game. The full set can be seen [here](http://www.retrosoftware.co.uk/forum/viewtopic.php?f=94&t=844&sid=5ba3a71754f4e51b01ae2c4fe261e344) . with a screenshot below. I had some constructive feedback via Samwise. The awesome Atom man Kees van Oss had tried playing the game via joystick and found that the response was too insensitive for analogue joysticks: i.e. one had to push the stick too far before the direction was recognised. The speed of the snake was also commented on (big speed jumps). I have set the score threshold higher before speed increases, but behaviour is otherwise the same. I don’t have the coding skillz as yet to make the snake speed more gradual with smooth animation.

## September 2013

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

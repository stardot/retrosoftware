## JSnake Dev Diary 28/04/2012

[&lt;----Back to JSnake Dev Diary Index](JSnakeDevDiary "wikilink")

### Update

OK, since I last updated the diary at end of February, I’ve continued to work on Jsnake in bursts here and there. I’ve done quite a bit. The bare-bones game is mostly done, but there are still some bugs to fix. After they're fixed, I’ll start on what I’m calling the “window dressing” – nice to have stuff that will make the game more playable or prettier.

#### Make the snake grow mk II

I spent far too long writing the routines for this. After the snake crashed into a boundary (or itself), I then wanted it to grow from tiny (ie size when you first start game with 0 score) to the size it was before you lost a life - i.e. just like Acornsoft Snake.

I'm now using 1k of RAM to store the Snake segment X Y coordinates, which means the maximum size of the Snake is 512 snake segments. Originally I was only using 256 bytes, which meant the code was simpler but Snake too short! I adapted the syntax from some macros I found [here](http://www.obelisk.demon.co.uk/6502/algorithms.html) for 16 bit increment, decrement, add and subract and compare.

To work out the length of the snake at the time of losing a life I count the number of bytes between the tail and head pointers - as per this back of envelope scribble here (keeping it old school). Note: I then divide the result by two to give the number of snake segments (each snake segment is recorded in the 1k circular list as X Y ords which = 2 bytes per segment)

![](../../retrosoftwarecouk_wiki-20160918-wikidump/images/backofenvelope.jpg "backofenvelope.jpg")

But there are a couple of other cases to watch out for:

- Snake crashes, but hasn't grown to full size yet (from losing a previous life)

- Snake crashes, but hasn't grown to full size (eats food then crashes)

I record the number of segments that the snake is due to grow by in a counter which decrements by one until the snake has finished growing.

To take into account the two cases above, after snake has crashed (and there are still life/lives remaining) I store the value of the counter in a temp location. I then work out length of Snake as per scribble-on-back-of-envelope above and add this to the temp value. The result is stored in the snake grow counter and the game loop starts again. This can be seen in the Youtube clip at the bottom of the page.

The counter changes if the snake eats food or a life is lost and the counter is set to the full size of the snake prior to loss of life.

### Bugs

Here is a list of bugs I've encountered. Most are fixed.

<tt>

    id  desc

    1   food boundary                                             food overlaps screen boundaries. '''FIXED'''

    2   food overlap                                              food can be plotted over the snake. It shouldn’t be.  '''FIXED'''

    3   opposite dir die                                              if you press opposite key to direction you are going in , you die. Harsh. '''FIXED'''

    4   boundary needs to be defined properly   Play area overlaps score banner

    5   snake size limitation                               256 bytes = 128 2x3 blobs. Not long enough snake. A kilobyte would = 512 2x3 blobs '''FIXED'''

    6   eat food not +=                                           when eating food, growsnakecounter needs to be += food, not = '''FIXED'''

    7   No pause between lives lost                             '''FIXED'''

    8   still snake size limit                                          snake is bigger (1kbyte)..  Going >512 snake segs,pointer "wraps around". No range check /reset..

    9   snake speeds up                                               snake goes faster when some direction keys are held down.

</tt>

#### Snake speeding up when it shouldn't. Grrr

Bug id 9 is the one that's bugging me the most. I have had some useful suggestions in the forums to investigate, but still haven't managed to fix. I'll upload the source code and an ssd soon. I'll continue to try and fix the bug myself, but if stuck I shall once again cry for help on the forums :/

See forum thread [here](http://www.retrosoftware.co.uk/forum/viewtopic.php?f=73&t=763)

#### Food over lap bug

Bugs 1 and 2 were interesting to tackle. I'm using EOR (exclusive or) of pixel colours for collision detection. Very primitive. The food is yellow. If I EOR yellow with black, result is yellow. If yellow is EORed with yellow, then I get black (useful in another routine for "removing" the food when it is eaten). If yellow EORed with any other colour, I get another colour.

So my solution to prevent plotting the food over the snake's body is to EOR food pixel colour with the screen, but I don't plot the pixels yet. If the result of the eor operation for any food pixel is anything other than yellow, I jump back to the top of the plot food routine which will choose another random area of the screen. This continues until an area of the screen is found that the food will fit on without plotting over any non-black pixel.

### Features

Here is a list of features that I'd like to implement:

<tt>

    id  Feature title                 description

    f1  frame screen boundary   draw a coloured frame around the game play area '''DONE'''

    f2  keep highest score

    f3  high score table

    f4  joystick support

    f5  nicer food                make the food more pretty than just a square

    f6  speed up                                after x points, snake goes faster

    f7  different food sizes                  different sized food and different score and growth increment for each size

    f8           Sound!

</tt>

### WIP video

The snake moves pretty smoothly at certain speeds (I can alter speed of snake movement in code. This is fixed at the moment). It's smoother under B-Em than Beebem.

<table>

<tbody>

<tr class="odd">

<td><p>{{#ev:youtube|NqqqVCGdnlQ}}   <br />

<strong>JSnake WIP</strong><br />

<em>Posted: April 28, 2012</em><br />

<br />

</p></td>

</tr>

<tr class="even">

</tr>

</tbody>

</table>

[&lt;----Back to JSnake Dev Diary Index](JSnakeDevDiary "wikilink")

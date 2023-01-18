## JSnake Dev Diary 29/02/2012

[&lt;----Back to JSnake Dev Diary Index](JSnakeDevDiary "wikilink")

OK, at this point, I had a moving snake, a yellow square of food and some rudimentary collision detection. What next? Well.. the food didn't even get replotted on screen once eaten, and it was plotted to the same place everytime.

Next goal was to plot food randomly on screen, grow the snake each time food is eaten and lose a life if it collides with self or boundary.

##### Randomness

Once again, I've nicked a routine! [Random Number Generator](http://www.retrosoftware.co.uk/wiki/index.php/Random_number_generator_%28very_fast_-_very_basic%29) by Richard Broadhurst works well .. though unmodified, it will create the same sequence of numbers every time. However if you jump to the related [forum thread](http://www.retrosoftware.co.uk/forum/viewtopic.php?f=73&t=640) you will find a top tip from Richard Talbot-Watkins : "If you weren't worried about reproducibility, you could EOR with a timer at the end, e.g. EOR &FE44, which should add a bit more randomness!"

This worked a treat, I had randomness :) So I could now create random XY coordinates from which to plot the new bit of food.

##### Making the snake grow

This is fairly trivial. I set a "Grow snake" counter to 4 (currently). If the counter &gt; 0 , each time I enter the Move snake routine, I decrement the counter and skip the "erase tail" subroutine and jump straight to the bit where I'm going to plot the new head location. This way, having eaten a bit of food, the snake will increase in size by 4 blobs.

<tt>

    lda GrowSnakeCounter

        beq WipeTail



        dec GrowSnakeCounter

        jmp GetOldHead

</tt>

##### Lives

Lives and snake grow are still a bit hack-y at the moment. Growsnake is just fixed at 4.. probably needs to vary - depending on food size like Acornsoft Snake?

Lives at the moment is simply the in-game loop (following a collision that is not food) looping 3 times until a counter = 0! THis was just to test lives working. I ought to have a proper routine which updates score, and banner etc.. so I will go on to write these routines next..

And that's where I'm currently at!

[&lt;----Back to JSnake Dev Diary Index](JSnakeDevDiary "wikilink")

![](./images/snakeandfood.png "snakeandfood.png")

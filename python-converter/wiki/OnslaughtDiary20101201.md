## 1st December 2010

Today I thought of a new cunning scheme for fitting a bit more stuff into the game, so I thought I'd add it here while it's still fresh in my mind.

As you know by now, my aim is to implement as many different types of monsters as I can possibly fit in, in order to keep each level interesting and fresh. Considering what we've got so far (mice, ghosts, daleks, jellyfish, and a yet-to-be-implemented pacman dude), a reasonably common trait is that each monster has four sprites - 2 facing left and 2 facing right. This won't always be the case (for example, the jellyfish doesn't face any particular direction), and I may want more intricately animated creatures in the future (i.e. with more than 2 animation frames!), or creatures with much more irregular animations. However, one thing which seems to be true is that left-facing animations are always an exact mirror image of their equivalent right-facing animation. This being so, it seems wasteful to bother storing their definitions, when they can be created at runtime.

There are two options: either create a new version of the sprite plotter which can plot a mirrored sprite on-the-fly, or generate mirrored versions of sprites as I need them. The first option is out, because the sprite plotting has to be super-fast, so let's consider option 2.

Bearing in mind that each level is never going to contain an instance of every monster type we have, I can prebuild mirrored versions of any of the sprites I need for a particular level just before it starts - this needn't be a quick routine, so I needn't waste memory on any kind of lookup table to perform the reflection. If I reserve 8 sprites' worth of memory, this allows me up to 4 different types of monster per level, which should be fine. Since I'm already storing in the executable 8 sprites which are mirrored versions of others, I don't lose anything, and for every new type of monster I add, I can only make a saving!

What I'll do is assign each sprite for every monster type an index, and create a table mapping indices to sprite addresses. If the table contains an address of 0, this indicates that it needs to be generated dynamically by reflecting the sprite before it. Then I amend the table by putting the address of the dynamically generated sprite there. When the level finishes, I can spot the dynamically generated entries (they will have a different range of memory addresses to those stored in the executable), and reset their entry to 0, ready for next time.

Finally, I need a couple of other tables which denote the start and end sprite indices for every monster type, so that the map generation can automatically perform the sprite generation at the beginning of the level.

I went back to the collision code for bullets/monsters and, surprisingly, it didn't make my eyes bleed, so I left it exactly as it was. I've refactored the monster logic a little by identifying code which is quite common to many of them (for example, checking for falling). The result of this is I now have quite a few very handy high-level subroutines which make writing detailed AI much easier and more readable. Watch out for a new breed of clever creature, heading your way soon!

*[&lt;&lt; Previous entry](OnslaughtDiary20101129 "wikilink") --- [Next entry &gt;&gt;](OnslaughtDiary20101203 "wikilink")*

*[Home](OnslaughtDiary "wikilink")*

------------------------------------------------------------------------

### Comments

-   (Example comment to demonstrate markup).
    -   [Richtw](User%3ARichtw "wikilink") 10:03, 1 December 2010 (GMT)


## 28th November 2010

It's been a while since I updated the diary, so here's what I've been up to recently.

![I ain't afraid of no mouse...](./images/Onslaughtaction.png "fig:I ain't afraid of no mouse...") Well, the good news is that most of the game code is working fine in its new framework, as you can see from the _crazy action shot_ to the left - the only things which remain are the handling of the time bar and the score, mostly because I haven't decided how I'd like them to be displayed yet.

It's taken me a little while longer than I expected because, rather than blindly bringing the code over from one codebase to the other, I've been making plenty of improvements along the way, both speed and space optimisations, and adding readability and a little more structure.

The first improvement I made was to the rendering of the map each frame. As you remember, the screen is double buffered, which means I do a complete redraw of the entire playing area each frame. The old codebase was using a routine to quickly clear the back buffer to blue, and then rendering over the top any platforms which were visible. This is quite wasteful, because - particularly with a lot of visible platforms on-screen - certain screen tiles get written twice, firstly by the clear screen routine, and then afterwards by the tile plotter. I figured that, since the map plotter is iterating through every visible map tile at the rendering stage, regardless of whether it's empty or not, I may as well plot a blank space with a fast routine here instead, and this way each screen byte only gets written once. This works out faster, and also means there's not so great a speed penalty when there are a lot of non-blank map tiles visible in the playing window.

The second improvement I made was to the dot plotter. This remains the only piece of code I've ever written that uses a BVC instruction to actually test an overflow condition (i.e. that adding two signed numbers has caused an incorrect change in sign) - and for this I'm proud! In this case, it's used as the condition which kills the dot, specifically when its downward velocity becomes so great that it causes an incorrect change of sign. The main motivation for this was that I didn't need to store the lifetime of each dot, although this leads to the strange effect that dots with upward velocities end up lasting much longer than dots with downward velocities; I don't really like this, so perhaps my only ever BVC instruction's days are numbered.

While on the subject of the dots, I fixed a bug which occurred at the screen wrap around point (where 0, 0 becomes 47, 47) and apparently 'lost' dots, and I thought of a cunning little optimisation which I'm not claiming is new, but only occurred to me the other day. Dots' coordinates are stored in two bytes; the MSB is the map position (between 0-47), and the LSB is a fractional part of which the top two bits represent the fractional position inside a character block, and the remaining 6 bits are just thrown away, but used as a fixed-point accumulator so dots can move at speeds less than one pixel.

Before, in order to extract the fractional position inside a character block, I was using:

<tt>

`LDA dotx,X`

`LSR A`

`LSR A`

`LSR A`

`LSR A`

`LSR A`

`LSR A`

</tt>

I never liked this much, and I realised you could achieve the same thing like this:

<tt>

`LDA dotx,X`

`ASL A`

`ROL A`

`ROL A`

`AND #3`

</tt>

...which is a byte smaller, but - crucially - 4 cycles quicker, which multiplied by 2 (for both x and y coordinates) and 128 dots, saves us 1024 cycles per frame, which is great!

After adding all this code into the build, my free memory count was &1B00 bytes, more or less - or a bit under 7k. This set off a few alarm bells, as I was budgeting for trebling the number of scenery tiles, adding loads more monster types (of which each one typically requires at least 288 bytes for graphics, plus the logic code, maybe another 128 bytes), and lots of levels. Also I kinda wanted a different tune for the menu screen. As you may have noticed from the screenshot, I removed a line from the status bar, to free up another 256 bytes, and started earmarking extravagant tables, and unrolled bits of code which might have to get the chop one day.

And then I remembered a &900 byte table (a little over 2k) which I've never been entirely happy with. It's a 48x48 image used as a collision map, and its purpose was always to yield quickly whether there is something significant at a given (x, y) position in the world. Monsters and the player update a 3x3 square of it as they move through the map. The player uses it to see if they have just collided with a monster (prior to writing their own details to it), and bullets and tokens use it to see if they have hit a monster, or been collected by the player, respectively.

But this is over 2k of scratch space which I really can't justify. So my next step is going to be to remove this entirely and check for overlapping collision boxes with Maths (TM).

In the case of monsters and the player colliding, this is simple - each monster will be responsible for determining whether they are overlapping with the player's collision box (it is just one check per monster!) and that's fine. Effectively, I just need to check whether (player position - monster position) is less than (monster xsize, monster ysize) and greater than (-3, -3), the size of the player. That's easy, and probably just as fast as the collision map method.

Tokens similarly can just check each frame whether they intersect with the player's collision box (i.e. if their position minus the player's position is less than (3, 3)).

The tricky one is detecting bullets against monsters. There are up to 16 monsters active at once, and _potentially_ 32 bullets (although this is an upper bound for all small sprites, which includes tokens - typically I'd expect no more than 16 bullets ever to be active at once). But - do the "math" (ugh) and we see that that's a worst case of 256 collision box checks per update, which I can't really justify. I'm going to need to try something else.

My best idea for the moment is this one: Bearing in mind that bullets only travel horizontally, the first thing they need to know really quickly is whether they could possibly be on a collision course with anything on their row. If there's nothing on their row, we can forget even trying any collision checks. Even better would be if they had a list of which monsters _are_ on their row, and then we can do collision checks on only those. So I'm going to try a 1-dimensional version of the collision map: I'll have an array of 48 16-bit values, one bit per monster which appears on that map row. As monsters move, they'll set or reset bits in this table accordingly. As a further optimisation, only visible monsters will set bits in the table (as bullets don't harm offscreen monsters; instead, the bullet dies when it goes offscreen). Then each bullet can instantly get a list of which monsters are on its row and then perform collision checks with only those. Mercifully, this will save me 2208 bytes (if it works quickly enough!), which is space for maybe 6 new monster types!

Results soon!

_[&lt;&lt; Previous entry](OnslaughtDiary20101117 "wikilink") --- [Next entry &gt;&gt;](OnslaughtDiary20101129 "wikilink")_

_[Home](OnslaughtDiary "wikilink")_

---

### Comments

- (Example comment to demonstrate markup).

  - [Richtw](User%3ARichtw "wikilink") 08:33, 26 November 2010 (GMT)

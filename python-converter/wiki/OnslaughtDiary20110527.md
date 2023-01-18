## 27th May 2011

![The title page with obligatory fireworks effects (they look better when they're moving, honest guv)](./images/blurptitlepage.png "fig:The title page with obligatory fireworks effects (they look better when they're moving, honest guv)") ![More recent in-game shot...](blurp ingame.png "fig:More recent in-game shot...") They say "less is more", which is my lame excuse for not having updated this blog since last December. Unfortunately, I haven't had any time to work on Blurp recently... until now! So this is just a quick update with some more up-to-date screenshots, without giving too much away!

The "less is more" mantra also applies to the title page, which is now finished. Faced with trimming things down so they'll fit into the tiny amount of memory available, I decided not to make it too flashy, but instead to reuse as much stuff as I already had in-game. So we've got a simple black background (to contrast with the more colourful in-game screens), with a bit of colour, and the dot explosion code reused to create a little background fireworks display at 50Hz.

The title graphic may be chopped if I need the memory for something more important - although it only takes up 70 bytes (plus it reuses the text plotting code to render it) - so it'll be a desperate measure. More likely to face the chop first is the extravagant lookup table I use to get the addresses of scenery tiles when rendering the map...

As you can see, there's also no high score table. I know they're popular around these parts, but I had to let it go for two reasons:

- it takes up memory which I just don't have

- it would require me to write a proper keyboard handler (because I'm shutting out the OS) which takes up memory which I just don't have

Something of a common theme with Beeb development, there.

My plan is to allow three initials to be entered with left/right/fire, like the old arcade machines, but I'll see how much memory I've got left...

At the moment, my main priority is to get some better scenery graphics in. I have room reserved for 64 map tiles (which can be either solid or passable), which I'd love to start using, to give a better feel for how the game will finally look. If any of our resident doodlers fancy having a go at designing some background scenery, do give me a shout!

OK, pub quiz time: At the bottom of the screen is a time bar, and if you look carefully at that screen row, you'll see it contains 5 colours simultaneously (black, cyan, green, magenta and red). Bearing in mind that it's a Mode 5 screen, any guesses how I'm doing it? I've never seen this technique used before on the Beeb, and it's quite good for adding a little bit of extra colour...

See you next time!

_[&lt;&lt; Previous entry](OnslaughtDiary20101203 "wikilink")_ --- _[Next entry &gt;&gt;](OnslaughtDiary20110604 "wikilink")_

_[Home](OnslaughtDiary "wikilink")_

---

### Comments

- As the cyan is only at the start of the time bar, I'm guessing that this is some form of position based jiggery-pokery, such as poking the "duplicate" ULA colour registers.

  - [Tautology](User%3ATautology "wikilink") 22:25, 27 May 2011 (BST)

- (Example comment to demonstrate markup).

  - [Richtw](User%3ARichtw "wikilink") 18:09, 27 May 2011 (BST)

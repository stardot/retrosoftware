## 29th November 2010

Just a quick update before I go to bed!

So, tonight I hastily put together a version of the collision detection algorithm I talked about yesterday. It differs very slightly in that the collision table records monsters by column rather than by row. I figured that when the player fires a bullet, he's most likely aiming at something to his left or right, and if I were to have a list of monsters per row, this would be getting a match over many updates. By recording monsters by column instead, there are (hopefully) fewer moments when the bullet's column and that of any monsters coincide, which makes it run a bit faster still.

Anyway, so far so good! It seems to work pretty well, with no discernable slowdown - and it's just as accurate as before. And more importantly, I now have 2k extra to fill with nice things. Tomorrow I guess I'll have to revisit it and tidy it up a bit, as it was written very quickly and it's probably the sort of code that'll make my eyes bleed in the morning.

Great to have some encouraging comments on the forum thread - it'll keep motivation high, particularly if DaveJ's happy to contribute a little bit of artwork and make it look really professional! I _promise_ I'll try and see this one through!

Well, that's it, I'm knackered! 'Night all.

_[&lt;&lt; Previous entry](OnslaughtDiary20101128 "wikilink") --- [Next entry &gt;&gt;](OnslaughtDiary20101201 "wikilink")_

_[Home](OnslaughtDiary "wikilink")_

---

### Comments

- (Example comment to demonstrate markup).

  - [Richtw](User%3ARichtw "wikilink") 23:57, 29 November 2010 (GMT)

## 10th November 2010

![Aaargh! Sprites! Thousands of 'em!](./images/Spritetest.png "fig:Aaargh! Sprites! Thousands of 'em!") Today I revamped the high-level routine responsible for plotting moving sprites (the main character and any monsters). I already had the core of the sprite routine done (the one I mentioned in an earlier entry which lives in the zero page, and uses a table to treat colour 0 as a transparent colour), but there was no high-level code responsible for clipping slightly offscreen sprites and rejecting totally offscreen ones.

The original code was hardcoded to deal only with 3x3 sprites - however I already decided that I'd like a bit more freedom with this, as I have ideas for creatures which will occupy different sizes as they animate, so it was time for a rewrite.

The results are to the left - I wrote a quick test which placed 64 monsters in the world, and moved them in random directions. On average there tends to be about 40% of them onscreen at any time, and the sprite engine ably plots all of them within the required frame rate! It's nice to know that, should I wish to, I'll be able to increase the maximum monster count from 16.

_[&lt;&lt; Previous entry](OnslaughtDiary20101108 "wikilink") --- [Next entry &gt;&gt;](OnslaughtDiary20101112 "wikilink")_

_[Home](OnslaughtDiary "wikilink")_

---

### Comments

- (Example comment to demonstrate markup).

  - [Richtw](User%3ARichtw "wikilink") 08:33, 26 November 2010 (GMT)

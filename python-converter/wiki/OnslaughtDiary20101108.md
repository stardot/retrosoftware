## 8th November 2010

Hello once again! Well, on the 2nd November, I thought I'd wrapped up the sound code. Truth is - it didn't really work very well. I decided to restructure it as it wasn't really as efficient as it could be. Remember all that stuff I said in the last entry about creating high-level code structure out of 6502 assembler? _Forget it._ It turns out it was far better to dispense with all the stuff which looked good on paper, and just go for a quick and dirty approach. Also, it turns out that at the same time, I inadvertantly added some structure by separating the low-level sound handler from the routine which updates the tune.

So, what the sound routine does now is this:

For each channel -

- check whether there is a pending note request

  - if so, fetch and store its data somewhere safe, and write to the sound chip to make the initial tone

  - if not, see if there's a note already playing on this channel, update it, and write the updated pitch and volume (if either have changed) to the sound chip

- that's it.

It turned out that I had a stupid bug in my code which was causing the noise channel to output, well, noise - but unfortunately not the sort that I was hoping for. (Big thanks to Tom Walker for spotting the fruit of my stupidity!)

So, over the last couple of days, I've been writing the in-game tune, and the code that plays it. The tune updater gets called just before the sound updater, and simply fills the note requests for each channel as if it were any other sound - nice and simple, and it means I can pull the tune update out of the game flow completely, and the sound will still work... phew!

The tune is finally finished, composed painstakingly with lists of EQUB statements. Luckily, it's not as obfuscated as it sounds. As an example, here's a snippet which defines the first part of the melody line:

<tt>

`.melody_seg1`

`EQUB G_1+l2, G_1+l2, G_1+l1, A_1+l1, B_1+l1, C_2+l1, D_2+l2, B_1+l2, A_1+l2, G_1+l2`

`EQUB E_2+l2, E_2+l1, Fs2+l1, G_2+l1, Fs2+l1, E_2+l2, D_2+l6, D_1+l2`

`EQUB G_1+l2, G_1+l2, G_1+l1, A_1+l1, B_1+l1, C_2+l1, D_2+l2, B_1+l2, G_1+l2, E_1+l2`

`EQUB A_1+l2, Cs2+l1, D_2+l1, E_2+l1, D_2+l1, Cs2+l2, D_2+l6, D_2+l2`

`.melody_seg1_end`

</tt>

In BeebAsm, I've defined these variables G_1, A_1, etc to be the value that represents that particular pitch (e.g. G, octave 1). The note length is defined by the variables l1, l2, etc, which just get added into the same byte, occupying the bottom 3 bits of each note. It's a reasonably painless solution (those of you with any muscial aptitude might be able to 'decode' the beginning of the theme tune from this snippet!).

The music system works by defining a number of 'segments' of music, and then specifying a high-level running order of segments. This eliminates redundant repetition of data - I suppose you could call it a very primitive compression system.

In this case, the code is tailored for the data - in other words, it's not a generic tune engine which can be given new data and be expected to work. I considered this at the beginning, but realised that I can squeeze much more data in if I rely on certain properties of the tune data, and hardcode the player code accordingly. For example, the 'chords' channel has a fairly unchanging rhythm (which repeats every 64 beats), so their rhythm is handled separately, which gives me more space to pack other data in!

Previously, I mentioned that I was giving myself a budget of 1k for the in-game tune. Well, it turns out that the code and the data for the in-game tune comes to a grand total of... 756 bytes! Hurrah! Now I might even have a bit of room for a separate title screen tune!

Anyway, that brings all the sound stuff to a close for now. Now I can get on with writing the game!

_[&lt;&lt; Previous entry](OnslaughtDiary20101102 "wikilink") --- [Next entry &gt;&gt;](OnslaughtDiary20101110 "wikilink")_

_[Home](OnslaughtDiary "wikilink")_

---

### Comments

- (Example comment to demonstrate markup).

  - [Richtw](User%3ARichtw "wikilink") 08:33, 26 November 2010 (GMT)

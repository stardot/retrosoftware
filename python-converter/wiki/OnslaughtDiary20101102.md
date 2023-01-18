## 2nd November 2010

Today my attention has been turned towards the sound code - a whole new system that the original _Onslaught_ didn't yet have. Because I want complete control over everything, particularly the interrupt handler, I'm going to have to discard the OS's sound code, as versatile as it is, and roll my own. Hopefully, the advantage of this will be that I can process the sound more quickly than the OS would have done, and win back some CPU cycles.

![A piano keyboard, yesterday](../../retrosoftwarecouk_wiki-20160918-wikidump/images/musicalnotes.png "fig:A piano keyboard, yesterday") The other advantage of this is that I can do things that the OS _can't_ do. If you've ever played about with the Beeb's sound capabilities, you might have noticed that its pitch range is not so great - the lowest note you can make is 122Hz - roughly the B an octave and a bit below Middle C, and the result is that it's very hard to make music with rich, deep bassline like the C64 and even the Spectrum 128 can manage. Beeb tunes tend to sound quite high pitched and without presence - of course there are some exceptions, such as the excellent music on the title screen of _Icarus_. This actually uses a trick, by playing a deep-pitched bassline using the periodic noise channel, but then the problem is that there is no capacity for percussion-type effects using white noise.

The trick I'm going to use is one pioneered by Tom Walker in his music conversions, in that deeper bass notes can be synthesised by generating a square wave ourselves. Normally the sound chip generates a square wave at the frequency specified, down to a minimum of 122Hz. If however we were to use a timer to switch between zero volume and full volume at a frequency of our choosing, it would be as if we were creating the waveform ourselves. The only problem is that we can't stop the sound chip from generating a square wave itself (ideally we'd prefer it to just output a constant level). So the solution is to have it generating such a high frequency waveform that, on average, it appears as if a constant level - then we modulate this waveform with our low frequency square wave controlled by timer interrupts, and _voilà_, we have our bass note!

The sound code has three layers:

Lowest level

This is responsible for nothing more than sending the pitch and volume of each channel to the sound chip. If either (or both) change on any channel, the new value is written. Since writing to the sound chip is a little slow, we only do this if anything has changed.

<!-- -->

Medium level

This is responsible for ornamenting the note being played with pitch and volume envelopes. A pitch envelope defines how the pitch of the note changes with time - it can be used to put some subtle tremolo on the note, or even to create the illusion of whole chords being played on one channel by rapidly alternating between three or more different notes. It's also useful for sound effects, for example a 'firing' sound which needs to decrease rapidly in pitch. A volume envelope describes how the volume changes over time, for example whether it fades slowly or builds to a climax. This data is fed to the lowest level layer in order to update the sound being played.

<!-- -->

Highest level

This feeds notes from the in-game tune to the two subsystems - the pitch to the lowest level layer, and the envelopes to the medium level layer. It also has to override the in-game tune with any sound effects which need to be played (which always take priority).

This is suprisingly structured, and even reflects the kind of code design used in modern-day engines, which just goes to show how timeless these kind of techniques really are.

The low-level layer has a bit of work to do, because whilst the notes are linear, this has to be translated into a frequency to be sent to the sound chip which is exponential - from one note to the note a semitone above, the frequency is multiplied by 2 to the power of 1/12th. Obviously, the easiest way to do this is with a table, but a table for every note (in fact, each semitone is further subdivided into quarters) would be huge. So I take advantage of the fact that, from one octave to the next, all the frequencies are doubled. So I only need to store one octave's worth of frequency values. This means first I have to divide the incoming note by 48 (48 quarter-semitones in an octave!) to see which octave number it is, and then the remainder is the index of the lookup table.

As I alluded to [here](http://www.retrosoftware.co.uk/forum/viewtopic.php?p=3649#p3649), there's a further optimisation to be made, in that the 10 bit frequency always has the MSB as 2 or 3, so we don't have to store a table for that.

Finally the code to calculate the sound chip frequency from the note looks like this:

<tt>

`.freqlo`

`    FOR n, 0, 47`

`        EQUB LO(INT(1016 / 2^(n/48) + 0.5))`

`    NEXT`

`; indexes 0-19: freqhi=3`

`; indexes 20-47: freqhi=2`

`freqhitransition = 20`

`.writepitch`

`    ; A = note (0-255)`

`    ; Find the octave and the note within the octave -`

`    ; This is a super-efficient way to divide an 8-bit number by 48,`

`    ; and also yield a remainder.`

`    LDX #0`

`    CMP #48*4`

`    BCC div48a`

`    SBC #48*4`

`    LDX #4`

`.div48a`

`    CMP #48*2`

`    BCC div48b`

`    SBC #48*2`

`    INX`

`    INX`

`.div48b`

`    CMP #48`

`    BCC div48c`

`    SBC #48`

`    INX`

`.div48c`

`    ; X = octave number`

`    ; A = note within the octave`

`    ; Get 10-bit frequency for this note`

`    ; the top 2 bits are either 2 or 3, so we don't use a table for this`

`    TAY`

`    LDA #2`

`    CPY #freqhitransition`

`    ADC #0`

`    EOR #1`

`    STA temp`

`    LDA freqlo,Y`

`    ; Shift down according to octave`

`    CPX #0`

`    BEQ nooctaveshift`

`.octaveshift`

`    LSR temp`

`    ROR A`

`    DEX`

`    BNE octaveshift`

`.nooctaveshift`

`    ; Frequency LSB in A, MSB in temp`

</tt>

For me, it was important to implement this sound code early, as it's far too easy to overlook sound until the end, and then realise there's not enough memory for the code or its data, or that there's not enough CPU time to accommodate it. Since I want to make sure the sound is an important component of the game, I decided to get this system in place more or less from that start. Now all I have to do is get that music written... For the moment, I'm giving myself a budget of 1k for the music data (the memory I liberated from the status area of the screen!) - let's see if it'll fit ok...

_[&lt;&lt; Previous entry](OnslaughtDiary20101031 "wikilink") --- [Next entry &gt;&gt;](OnslaughtDiary20101108 "wikilink")_

_[Home](OnslaughtDiary "wikilink")_

---

### Comments

- (Example comment to demonstrate markup).

  - [Richtw](User%3ARichtw "wikilink") 08:33, 26 November 2010 (GMT)

[&lt; --- Back to previous page of JBiplane Dev Diary](http://www.retrosoftware.co.uk/wiki/index.php/JbipDevDiary)

![](./images/Jbipwipscreenshot180.png "Jbipwipscreenshot180.png")

# JBiplane Development Diary continued

## January 2014

So armed with this info, throughout Christmas and January, I created a sprite movement routine which did the following:

.. if moving horizontally, and moving within one character address, select one of the "sprite offsets" .. or if on to next char address, select correct sprite offset and update char address of sprite

I updated sprite plotting routine which plotted in column major order. This routine doesn’t need to calculate an X / Y co-ordinate for any (or ALL like earlier in diary) pixels. This means many fewer clock cycles used per sprite plot, which in turn helps avoid sprite tear. Now that my plotting was quicker, I was able to plot a sprite (almost) between screen refreshes and thus no tear.

## March-May 2014

Real Life got in the way for a while. In a bid to make some time, I took to writing code on my train commute (if I was awake!) Over this time, I worked on rotating the sprite – so more work on the movement and plot routines.. and also a keyboard routine. All very fiddly. It took a long time to debug. As per start of the diary, much of this can be blamed on my wrangling with screen address layout of the Beeb (plus my coding ability or lack thereof). There were many instances of loops exiting after one too many or too few iterations.. ie 7 instead of 8 etc. All ironed out eventually. In April, I got to meet Tricky at Wakefield.. he showed me how his routines in Carnivale <link> worked. Some of it went over my head.. but I would recall conversations about interrupts later in the year.

## July-October 2014

#### More sprite work

At this point I noticed a problem with the speed of the plane sprites… they moved too quickly. The slowest speed was one pixel movement per frame. Greater speeds were set at two three and four pixels per frame. I concluded that this was too much for acceptable game play. I decided that the fastest speed should be one pixel movement per frame. This meant that I had to modify the sprite movement routines to only update sprite every X number of frames. This proved to be troublesome but I got there in the end. However, this led to another problem. My keyboard routine now gave unpredictable responses when the sprite was moving at slower speeds. It took me some time to put together a keyboard routine which worked acceptably.

After some initial hints from Tricky on the forums, I spent some time wrangling with diagrams and pseudo code. I ended up using a series of tables which were used to count down the number of frames before a key press(es) would be acted upon. This worked quite neatly and could be tweaked to tune the responsiveness.

#### Halifax and London RISC OS

![](./images/RISCOs.png "RISCOs.png")

I went along to a Stardot Halifax meet up in August where I got to meet a lot of clever people working on their hardware projects. Kees, RetroSoftware’s renowned Atom game extraordinaire was in attendance. He took me through his ingenious code for his Atomic Flappy birds game and was very encouraging when I showed him my efforts. I didn’t get much coding done – I was having too much fun finding out what everyone else was up to! But it gave me a bit of a boost to carry on with the game. In September I went to the London RISC OS show, where Tricky was demo-ing his trio of excellent conversions – Carnivale, Phoenix and AstroBlaster. I ran my game code on a real Beeb and discovered it didn’t run properly. It seemed that I wasn’t handling interrupts properly, which B-EM forgave, unlike the real thing.

## November-December 2014

Eventually I managed to handle interrupts properly. This involved disabling all unwanted interrupts and correctly handling those I wanted – namely vsync and Timer 1. This bought me more time between screen refreshes – and didn’t freeze the game when a key was pressed on a real Beeb .

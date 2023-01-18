# XTHOPAC STUARC (working title) by Xavier Tardy

### Licence

Software licence TBC

### Introduction

Xavier Tardy's *Highly Optimized Pure Arm Code Shoot'Them Up for the Archimedes Range of Computers* is a vertical shoot-'em-up. It works perfectly on an A3010, 50 frames per second with huge sprites, as if the machine was a Neo Geo. The plotting and unplotting routines are just perfect in terms of CPU usage. The intention is to demonstrate the great possibilities of the Acorn Archimedes range and to show how many 2D games have been poorly programmed for these fantastic machines. The game should fit on a minimal number of floppy discs, and work on a 2 MB machine. A demo available for download below shows off some of the tricks used in the development of the game.

### Features

-   overscan 416\*288, 256 colour playing area
-   up to 259 different colours on screen (as I use the 3 colour cursor hardware sprite to plot the score)
-   thanks to hardware scrolling (MEMC) and highly optimised clipped plotting/unplotting routines, dozens of normal sized sprites can move on screen, and several huge (for example 4 80\*80 sprites) all this in the VBL

### Still To Do

-   include real graphics for the background
-   design the levels
-   original music and some samples including an 8 channel (or better if QTM handles it) soundtrack for the opening (welcome) title screen, and a 4 channel QTM soundtracker song for the following:
    -   game levels
    -   specific end levels with big bosses
    -   you win and reach the next level
    -   you miserably lose
-   a second set of routines to save time when plotting multiple identical sprites on screen.(1 LDMIA for n STMIA)

### Unpublished Archimedes Demo from circa 1992/93

Xavier Tardy's [1992/93 Unpublished Archimedes Demo](./images/!preview.zip "wikilink"), RISC OS archive packed with PackDir then ZIPped.
Xavier Tardy's [1992/93 Unpublished Archimedes Demo](./images/preview.zip "wikilink"), ZIPped .adf ADFS disc image.

You'll need a TV, RGB monitor, or a real multiscan monitor as the screen mode is 50 Hz. The demo uses an independent module to set up this resolution, so it's only a matter of replacing it with your own if you want another frequency. For example I remember creating a 116 Hz mode for my very old 22" inch VGA/false multisync monitor.

This 18 year old demo is more to check routines than to provide a sophisticated visual experience, and was never released for that reason. The bugs will help you understand where some of the tricks are (although it's been improved for the new game and CPU usage has been slashed down to 25% or 50% of what you should see in this demo. Keep your eyes open !) Should be smooth as it is smooth even on an A310 ...

Note: this demo does not work with Arculator emulator.

### Development Diary

#### January 2011

*31st January*
I've recently spent some time rewriting the 'memory hungry' generated code routines, to get something still very fast (to plot / unplot sprites) and which won't need a lot of memory, and can also do horizontal clipping (a real one, not a 'fake' clipping where the sprite is fully plotted but seen only in the visible area).

Once the vertical clipping routines are completed (I now know how to implement that) I'll be able to show what a 'slow' ARM2 machine with no blitter can do =&gt; more than the Amiga, of course.

# Freeware Loading Screen

In order to establish a consistent branding of our products, all Retro Software freeware releases will feature a Micro Power style cassette inlay and loading screen as shown below.

This document describes how to configure and use such a loading screen in your own projects.

<img src="SparseInvaders-WIPcover.png" title="fig:SparseInvaders-WIPcover.png" alt="SparseInvaders-WIPcover.png" width="260" height="256" /> ![](./images/Sparse Invaders load screen.png "fig:Sparse_Invaders_load_screen.png")

## Downloads

These disk images contain a blank template loading screen, a BASIC configuration program and a template BASIC loader program to use as a starting point.

The DFS image is intended for BBC B, B+ and Master users. It is also suitable for Electron users with an appropriate DFS interface such as those from Pegasus or ACP.

The ADFS image is intended for Master Compact users and Electron users with a Plus 3 unit or equivalent. It is also suitable for a BBC B or B+ fitted with ADFS.

[FreewareLoader\_DFS.zip](./images/FreewareLoader DFS.zip "wikilink")
[FreewareLoader\_ADFS.zip](./images/FreewareLoader ADFS.zip "wikilink")

## How To Use

This section describes how to use the provided disk images to create your own RS loader. It is organised as a walkthrough tutorial and should only take around 5 minutes to complete.

### Getting started

• Load the appropriate disk into your machine or favourite emulator. If using an emulator, be sure to check that disk writes are allowed. The disk won't boot at this point because there's no loader present. We're going to make one!

• If you list the disk catalogue you will see several programs. These will be introduced one at a time.

• The file called BLANK is an empty template of the loading screen. Running this file shows a Retro Software logo inspired by the familiar Micro Power layout.

`>*/BLANK`

![](./images/RS Loader empty.png "RS_Loader_empty.png")

The two windows below the logo are currently empty. So let's fill in some game details. Press Break first to clear the screen.

### Configuring the screen display

• The program called CONFIG is used to add the game details to the loader screen. Load this in now:

`>LOAD "CONFIG"`
`>_`

• List the program to see what it looks like. The section that needs to be modified for your game starts at line 200. The CONFIG program has already been populated with some dummy text:

` 200 PROCentry(10+DH, 1, "GAME")`
` 210 PROCentry(13+DH, 1, "TITLE")`
` 220 PROCentry(17, 0, "by")`
` 230 PROCentry(19, 0, "Your Name")`

Each entry contains information about one line of the display:

-   the row number (9-20) +DH for double size text
-   the colour of the text (0-3)
-   the text itself (up to 16 characters)

You can create as many entries as you like providing you only use rows between 9 and 20. The default entries show the suggested layout style for most projects.

By default, the CONFIG program puts a delay of 3 seconds into the load screen. This is the length of time between showing the screen and returning back to BASIC to load the main program. This feature is controlled by line 260:

` 260 config?3=150:REM delay`

If you want a different delay, change the value 150 to the time you require (in 1/50ths of a second).

Note that the delay is only used when loading from fast filesystems. If the load screen is run from tape, it will return immediately with no delay.

Leave the defaults as they are for your first time through this tutorial. It will make it easier to follow some of the instructions.

• Run the CONFIG program and it will ask for an output filename. Press ESCAPE for now to leave the configured screen in memory without saving it to a file.

The screen can be displayed by entering the command CALL &5000.

`>RUN`
`Output filename (SCREEN) : {press ESCAPE}`
`Escape at line 320`
`>CALL &5000`

![](./images/RS Loader default.png "RS_Loader_default.png")

You will notice that a text window has been created in the bottom panel of the screen. This is where the loading messages will appear.

Before we continue, let's get back to mode 7:

`>MODE 7`

• Now run the CONFIG program again and, this time, press RETURN when asked for an output filename to accept the default name of SCREEN:

`>RUN`
`Output filename (SCREEN) : {press RETURN}`
`*SAVE SCREEN FFFF5000+3FE`
`>_`

The CONFIG program will show the command that it used to save the file.

• There will now be a version of the title screen on the disk called SCREEN that is populated with the default game details. You can run it to see the screen if you like:

`>*/SCREEN`

• We are done with the CONFIG program now, so press Break.

### The BASIC loader program

• Next, let's take a look at the BASIC loader program. It's the file called BASLOAD on the disk:

`>LOAD "BASLOAD"`
`>LIST`
`   10 *EXEC`
`   20 *FX229,1`
`   30 *FX200,2`
`   40 HIMEM=&5800`
`   50 FORI%=0TO&420STEP4:I%!&5000=I%!TOP:NEXT:CALL&5000`
`   60 *RUN GAME`
`>_`

Line 10 closes any open exec channel (the script used to boot the disk).

Line 20 disables the Escape key

Line 30 causes the memory to be cleared on Break.

Line 40 sets HIMEM to the correct value for a MODE 5 screen.

Line 50 relocates the screen display code to its execute address (&5000) then calls it. More on this shortly.

Line 60 onwards is the code to run your game. For this tutorial we've (imaginatively) called it GAME!

This program is intended to be the starting point of your own custom loader. Again, for the purposes of the tutorial, just use it as-is for now.

### Merging in the load screen

• The next step is to take our loading screen file and bolt it onto the end of this BASIC loader program. There is a program called MERGE on the disk that will do this for you. Run this program now:

`>CHAIN "MERGE"`
`Press RETURN for defaults`
`BASIC loader (BASLOAD)  : _`

• You may enter any file name you wish at the prompts or just press RETURN to accept the default file name in parenthesis. For the purposes of this tutorial, just press RETURN at each prompt:

`BASIC loader (BASLOAD)  : {press RETURN}`
`Loading screen (SCREEN) : {press RETURN}`
`Merged loader (LOADER)  : {press RETURN}`
`  in:  3000 3069 BASLOAD +69`
`  in:  3069 3467 SCREEN +3FE`
`  out: 3000 3467 LOADER +467`
`>_`

• That's it, you're done! Press the usual Shift/Break combo to boot the loader and check it out. After a short delay, the program will fail with a "Bad command" error because there isn't actually a GAME file on the disk for it to load. But you get the idea.

### Final notes

• Always remember to edit the BASLOAD file and not the LOADER file if you want to change the BASIC part of the loader. Then re-create the LOADER file using the steps above.

• If you're using cross-development tools you can, of course, just append the screen display binary (SCREEN) to the end of your BASIC loader to create the LOADER program.

• Strictly speaking, the loader screen doesn't need to be attached to the BASIC loader, it could just be run separately. Like this, for example:

`  10 *EXEC`
`  20 *FX229,1`
`  30 *FX200,2`
`  40 HIMEM=&5800`
`  50 *RUN MYSCREEN`
`  60 *RUN GAME`

or even with a simple !BOOT script, bypassing the BASIC loader altogether:

`*RUN SCREEN`
`*RUN GAME`

Normally, we would advise against doing this. The recommended method is a little more work but it makes for a more pleasant user experience when loading from tape.

However, there are certain circumstances when these other methods may be preferable.

If your program needs to support a second processor over the Tube, for example, the loader *must* use one of these alternative techniques.

### Release history

15/01/2011 Initial release.
17/03/2012 Added configurable delay option.

Mode 2 sprite movement

# Demo Video

{{\#ev:youtube|3XyDfNxDYrc}} **Note :** The video seems to make the fastest sprite look a little jerky, in reality it isn't so. And sometimes (not always) the video will jerk all over the place but again nothing to do with the demo, just You Tube caching/speed issues etc.

# Introduction

This project demonstrates three techniques; plotting, moving and erasing sprites. This page may be expanded upon in more detail in the future but for the moment apologies for the brief explanation.

## Moving sprites

Moving sprites around a screen is not just a simple matter of changing the X,Y coordinates, if only it was ! When a sprite is plotted to screen you are physically writing to the screen memory and if you change the X ordinate and re-plot then the old copy will still be there. So the principle is before plotting in a different position you have to erase first before you can do this.

This routine plots fully masked Mode 2 sprites. Which means anything behind a sprite will show through rather than having an ugly black block around our sprite. If your sprites never cross over each other or you don't move them over anything more than a plain background then you can get away without using masked sprites, and these are very much faster to plot so worth considering if you don't need a masked sprite.

## The Raster and vertical sync

For now I'm afraid I'm going to have to presume you know what the raster and vertical sync is as time does not allow me to explain it here. But basically you must time all your sprite plots to the screen sync pulse, otherwise you will get flicker (Some flicker is often unavoidable for complex games). You need to do all your erasing and plotting before the raster beam starts to redraw the screen. To do this we wait for a system even called the screen sync, when this occurs the beam has finished drawing the display and is about to start another. This is when we do our sprite plotting and hope that we get it all done before the beam gets to out sprites otherwise the dreaded flicker can occur.

In fact the screen sync actually occurs a couple of rows after the visible part of the display has been drawn. So if we use the sync for our sprite plotting timing we do in fact waste some time. What this demo does is to use a system timer to indicated when the visible screen has just been completed. It's at this point that we fire off our drawing code to try and gain maximum time.

# Limitations

The demo is flicker free, but that is not to say that the raster isn't well onto the screen by the time we've finished plotting the sprites, because it is. By choosing the order in which the sprites are plotted in the demo means the plotting stays ahead of the raster for all sprites and is flicker free. If you draw too many sprites near the top of the screen you will get sprite "shearing". One easy solution is to limit how high you plot your sprites (put in a nice big status bar so that the user doesn't feel cheated of screen space) and also to reduce the sprite sizes to speed up plotting. the sprites used are a reasonable size for a Beeb game and could be reduced in size if required. Another option would be to use a lower memory screen (i.e. Mode 5) and for the loss in colour you're sprites end up physically the same size but using much less memory and thus plotting very much faster.

# Why not try

## Playing with the code

There are three sections you should look at if you want to include the source in you own project or just to have a tinker.

### Structures section

This shows you the structure of the sprite data in the computers memory. Note that the data is not necessarily laid out logically, the structure was created as the demo was written and should really be tidied up a little.

### Sprite data section

This is the actual data (conforming to the structure described in the structure section). Here you can change the sprite graphic by just changing one value, change the sprite positions and change whether they move and the speed they move. Four Sprites are defined.

### Constants section

You'll find many constants for the demo here. The ones you need to be aware of if you want to make changes are;

_SpriteObjectStructureSize_ If you expand (or reduce) on the sprite structure to give the sprites more functionality then this constant defines the current size of the structure. Failure to set this to the current Sprite structure size would result in the code not working correctly.

_Const_NumSprites_ The current number of sprites to plot/move etc. Currently set to the 4 sprites there are. If you want to have more or less sprites ensure you alter this value.

## Improving the code

This routine is reasonable for some games but for others the dreaded sprite shearing may be an issue. But... there are still other things you can put into the code to improve this. For example write a routine to order your sprites so that they avoid the raster beam as much as possible. Think also about when you do your erasing, is the point that it happens in this demo really the best point ?

# Download source

[The enitre Swift Project](./images/Mode2SpriteMovement.zip "wikilink") (Highly recommended, just load into Swift and run !, contains all files you need even if not running in Swift )

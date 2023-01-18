# BeebSpriter

![](./images/BeebSpriterScreen.jpg "BeebSpriterScreen.jpg")

## Introduction

While working on [Onslaught](OnslaughtDiary "wikilink"), I realised that I no longer had a good way of designing all my in-game graphics. Back in the day, when coding was painstakingly done on a real Beeb, I used to use the Acornsoft Sprite Rom to design my graphics, with a Basic program to convert them into binary form and test their animations.

Well, that's all a bit 'last century', and hence BeebSpriter was born: a super-duper 21st century way of designing sets of BBC graphics for any screen mode, with a bunch of useful facilities to help make life easier. Read on if you're interested...

## How does BeebSpriter work?

The best start is probably just to download the pre-release version (below) and fire it up!

BeebSpriter works with 'sprite sheets' - a collection of sprites which are all designed to be exported in the same way, in one block. Perhaps you have two types of sprites: the first are scenery tiles, which are always plotted directly to character aligned positions and require no masking; the second are character sprites, which may be plotted at any screen line, and require a mask. Using BeebSpriter, you would put all the scenery tiles in one sprite sheet, and the character sprites in another.

BeebSpriter saves/loads sprite sheets in its own human-readable XML format. When you're ready to try out your graphics on the Beeb, you must *export* them - a one-way process which generates a binary file designed to be loaded directly on a Beeb (or included in an executable). All sprites in a sprite sheet are exported with the same settings, hence the need to put different kinds of sprites into their own sprite sheets. To go back to the above example, one obvious difference between the two sprite sheets would be that the scenery tiles should be exported without masks, and the monster sprites *with* masks. More about exporting later.

## Tutorial

![](./images/NewSprite.png "fig:NewSprite.png") Let's create a new sprite sheet. Go to File -&gt; New -&gt; and specify which screen mode you'd like to use for your sprite sheet. All being well, you now have a blank sprite sheet ready to use. Right click anywhere in the empty area, and you'll be able to create a 'New sprite'.

Give it a name if you want, put in the dimensions you want, hit OK, and *voilà!*, your first sprite. Note that, although the sprite sheet is tied to one particular screen mode, each sprite in it can have any size you wish. It's far more flexible than a simple tile set of equally sized sprites. Back to our new sprite - it's a bit uninteresting right now, just a black square. Double-click it, and it will bring up the editor window.

The available colours are on the left. The grey colour is transparent - use it to specify transparent pixels, which later on can either be exported as a separate mask sprite, or just converted to colour 0 if you prefer. Left-click a colour to set it as the current draw colour, right-click to set it as the erase colour. Double-clicking will change it to the next available palette colour. Each sprite remembers the palette you've set for it.

Along the top are the various editing modes: draw pixels, flood fill, insert/delete rows or columns, select mode, paste selection, and resize. Hopefully all of them are reasonably self explanatory. Use select mode along with the various options available in the edit menu (to cut/copy, or reflect the currently selected area).

Note that the true size preview of the sprite being edited is in the sprite sheet itself - it changes as you edit it. Note also that, during editing, undo/redo (Ctrl-Z/Ctrl-Y) are available to rescue mistakes, but their history is lost if the editing window is closed.

Now try adding another sprite. Either do this by right-clicking on a blank area of the sprite sheet, or by right-clicking on an existing sprite and selecting 'Make copy...'. Again, hopefully this is self-explanatory! If you wish to re-order the sprites in the sprite sheet, just click and drag it to your preferred position.

The background colour of the sprite sheet can be set from the 'View' menu. This is handy for simulating the appearance of the sprite in a Beeb environment. Probably a lot of the time you'll want to set it to black. In the case of Onslaught, blue is the usual background colour.

## Animation preview

BeebSpriter has a basic facility for previewing animations. Go to the Tools menu to open the animation preview window. Then right-click on sprites you wish to add to the animation sequence, and select 'Add to animation preview'. It's possible to change the type of animation (cyclic, yo-yo or one shot), the speed, and the order of the frames. I intend to also put in the ability to advance the sprite by a byte position at any point you wish inside the animation sequence (but I haven't done it yet).

One useful feature of the animation preview is that sprites in the animation sequence can be edited while the animation is playing, which gives you immediate feedback as to whether the animation looks OK.

## Exporting

![](./images/ExportOptions.png "fig:ExportOptions.png") Here's a quick explanation of the currently available export options.

**Sprite layout**

'Row major' specifies that the sprite is laid out row-by-row, e.g. in a Mode 1 16x16 sprite, the first 32 bytes would be the top character row, and the next 32 bytes would be the bottom character row. This is the natural format for sprites which are only going to be displayed at character block aligned positions.

'Column major' is the natural data format for sprites which are to be displayed at any pixel line. Using the same example, the leftmost byte column of 4 pixels would be exported as a concurrent 16 bytes, then the next 3 columns in turn.

'Linear' specifies that the sprite is laid out line-by-line (actual pixel lines, as opposed to character rows).

**Sprite size**

Suppose you have a sprite sheet defining a set of background scenery tiles of 8x16 pixels in Mode 5 (i.e. 2 character blocks across by 2 character blocks down). It's fairly likely that some of these tiles are going to be designed to fit together to make a bigger piece of scenery. Using BeebSpriter, it would be possible to define a sprite which was 24x32, i.e. composed of a 3x2 group of tiles. If 'Break sprites into smaller pieces (of size 2 character blocks across, and 2 character blocks down)' is then specified, this big sprite will be broken into its component parts, as if it were 6 individual 8x16 sprites. This provides a very natural way of designing big graphics which are designed to be part of a equally sized tile set.

'Export sprites at their defined size' just exports them exactly as they are.

**Transparency/masking**

If 'Export separate sprite mask' is checked, then the sprite sheet is exported in two batches - first the actual sprites, followed immediately after by all their masks. This obviously doubles the space used, but sometimes it's necessary for nicely masked sprites, e.g. those in Thunderstruck or Spycat.

'Export transparent pixels as colour 0' does just that.

**Header file generation**

With sprites of different sizes in a sprite sheet, it might be awkward to figure out exactly their location in the exported data. Luckily, BeebSpriter has a facility to output an assembler source file containing symbols defining the offset in the binary file of each named sprite in the sprite sheet, and also their sizes. Because different assemblers may have different syntaxes for defining constant symbols, you can specify the syntax to be used here, where {n} will be substituted by the symbol name, and {v} for the unprefixed hex value which it represents.

For BeebAsm, it's: <tt>

`{n} = &{v}`

</tt>

For P65, it's: <tt>

`.alias {n} ${v}`

</tt>

Note that you have to even specify here what prefix should be used for a hex literal.

## Download

This is the latest version (pre-release), and is reasonably untested! You can start a discussion on any issues encountered, here in the [BeebSpriter forum](http://www.retrosoftware.co.uk/forum/viewforum.php?f=64).

[BeebSpriter v0.03 - executable and source code](http://www.retrosoftware.co.uk/wiki/images/2/2b/BeebSpriter-0.03.zip)

Older versions are available here:

[BeebSpriter v0.02 - executable and source code](http://www.retrosoftware.co.uk/wiki/images/6/66/BeebSpriter-0.02.zip)

It's been developed and tested on Windows 7, running .NET framework 4.0 - I have no guarantee or even idea if it'll run on earlier .NET frameworks. However, the source code is included so it should be possible to build for your system if you wish. It also *ought* to be possible to compile it for Mono, thus opening it up to Linux / Mac OS X. However, [DaveJ](http://www.retrosoftware.co.uk/forum/memberlist.php?mode=viewprofile&u=62) has been busy recently porting an early version of this sprite editor to run natively in Linux, using [Vala](http://en.wikipedia.org/wiki/Vala_%28programming_language%29), and it's looking great so far! (So watch this space...)

--[Richtw](User%3ARichtw "wikilink") 19:17, 26 December 2010 (GMT)

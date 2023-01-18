## 4th June 2011

One part of the development process I've not yet gone into much is the tools I wrote to help with the creation of assets. A little while ago, I talked about the [Onslaught Monster Designer](OnslaughtDiary20101203 "wikilink"), which ended up evolving into [BeebSpriter](BeebSpriter "wikilink") - a nice generic sprite editor which I use for creating all the graphics in the game - monsters, scenery, and even incidental graphics like the time bar.

I decided that a Windows screen editor would be a good idea, as it beats drawing levels on graph paper, and entering their data meticulously by hand. Below you can see the results:

![Screenshot of the map editor](./images/blurpmapeditor.png "Screenshot of the map editor")

As you might remember, Blurp stores its screens, not as a 2d array of tiles, but "Chuckie Egg" style, by specifying a list of platforms, columns and blocks with their positions, lengths and which scenery tiles to use. One thing I wanted to do was to create an application which could load/save screen definitions in plain text XML, with an 'export' option (exactly like BeebSpriter) to output a binary Beeb-ready file. This of course is well-compressed in order that I can fit loads of levels in.

The above level ends up being saved out like this:

     <?xml version="1.0" encoding="utf-8"?>
     <ScreenSet xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema">
       <Screens>
         <Screen>
           <BackgroundColour>Blue</BackgroundColour>
           <EyeColour>Green</EyeColour>
           <MapItems>
             <MapItem xsi:type="Block" StartX="5" StartY="4" TileName="tree" Length="2" Height="3" />
             <MapItem xsi:type="Platform" StartX="16" StartY="14" TileName="wall5" Length="12" />
             <MapItem xsi:type="Platform" StartX="1" StartY="17" TileName="wall5" Length="6" />
             <MapItem xsi:type="Platform" StartX="4" StartY="20" TileName="wall5" Length="6" />
             <MapItem xsi:type="Block" StartX="4" StartY="16" TileName="tree" Length="2" Height="1" />
             <MapItem xsi:type="Platform" StartX="9" StartY="14" TileName="wall1" Length="2" />
             <MapItem xsi:type="ColumnWithEnds" StartX="2" StartY="15" TileName="pillar" Height="2" />
             <MapItem xsi:type="ColumnWithEnds" StartX="5" StartY="18" TileName="pillar" Height="2" />
             <MapItem xsi:type="Block" StartX="21" StartY="11" TileName="tree" Length="2" Height="3" />
             <MapItem xsi:type="Platform" StartX="17" StartY="13" TileName="fence" Length="3" />
             <MapItem xsi:type="Platform" StartX="20" StartY="13" TileName="fence_1" Length="1" />
             <MapItem xsi:type="Block" StartX="9" StartY="6" TileName="tree" Length="2" Height="1" />
             <MapItem xsi:type="PlatformWithEnds" StartX="3" StartY="7" TileName="platform1" Length="9" />
             <MapItem xsi:type="Platform" StartX="7" StartY="10" TileName="wall6" Length="11" />
             <MapItem xsi:type="ColumnWithEnds" StartX="8" StartY="8" TileName="pillar" Height="2" />
             <MapItem xsi:type="Block" StartX="14" StartY="9" TileName="generator" Length="2" Height="1" />
             <MapItem xsi:type="Block" StartX="9" StartY="13" TileName="generator" Length="2" Height="1" />
           </MapItems>
         </Screen>
       </Screens>
     </ScreenSet>

An advantage of this scheme is that I can save all kinds of metadata in the regular saved file. One nice thing is that, instead of referring to scenery tiles by their index (which would be subject to change, if I were to delete, add, or rearrange sprites in the BeebSpriter sprite sheet), I can actually refer to them by name.

Anyway, today I finished off the map editor (meaning now I can replace the mapped generators with 'proper' generator MapItems), integrated it into the build process, and rewrote the map building code in the game to use the new super-compressed maps.

Seems like there's hardly anything left to do!

*[&lt;&lt; Previous entry](OnslaughtDiary20110527 "wikilink")* --- *[ Next entry &gt;&gt;](OnslaughtDiary20110701 "wikilink")*

*[Home](OnslaughtDiary "wikilink")*

------------------------------------------------------------------------

### Comments

-   (Example comment to demonstrate markup).
    -   [Richtw](User%3ARichtw "wikilink") 17:00, 4 June 2011 (BST)


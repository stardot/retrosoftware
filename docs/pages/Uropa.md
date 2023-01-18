# Uropa by Stephen Smith

### Licence

Software licence TBC

### Introduction

*Uropa* is the second game for the BBC worked on by Stephen, author of *[The Krystal Connection](The_Krystal_Connection "wikilink")*, around 1988 and is a 2D/3D game with split screen modes inspired by *[Battlezone](wikipedia:Battlezone_(1980_video_game) "wikilink")* and titles from *[Ultimate: Play The Game](wikipedia:Ultimate_Play_the_Game "wikilink")*.

The basic idea of the game is to complete missions which are played out on the surface of Uropa (ex-Europa), the re-built moon of Jupiter and within the colonist base stations (isometric).

Originally the base section of the game was to be like small cities with random layouts and a multitude of rooms, however it became apparent that there are too many to explore and it would become boring quickly. The base section allows the player to pick up objects from items within the room (such as food, metal, disks etc..) and sell or use these items for money (kind of like Elite trading). For instance, you can go into the "Order" room and press F7 when facing a computer terminal and purchase items for your surface vehicle (such as mining pods or negatron bombs).

While in the 3D surface section, you can hyper drive to other bases. By pressing F4 you can use the cursors keys to select a base. Once the base is highlighted you press F0 (front view) and then H for hyperdrive. Of course, if there are enemies around you can't do this.

Some other notes regarding the 3D section:-

1. Pressing V will toggle front / rear view.
2. Pressing M will mask your ship (cloak) at the expense of increased fuel usage and also disables the radar.
3. If your shields are badly damaged, then cloaking and other operations may not work properly.

[Discuss Uropa](http://www.retrosoftware.co.uk/forum/viewtopic.php?f=19&t=747)

### TODO

The game is not complete - there are a number of things I would change and I estimate it would require quite a bit of work to complete.

The 3D section can be improved quite a lot. The fastest way to draw lines is by using the Bresenham algorithm. The game does not use this (Elite does though), so this would speed up the 3D graphics quite a bit. There is another improvement related to how 3D objects are projected to the screen which I was aware of and never implemented improving speed even more.

The following is a list of major items to change:-

1. Base station layouts smaller with fixed rooms.
2. Base station map shows actual room types including entry/exit points.
3. The dashboard indicates if there are items that can be picked up within a room by lighting the "SCN" (scan) icon. It might be good to highlight the objects in the rooms to avoid wasting time searching every object in a room.
4. 3D section speed improvements by using Bresenham algorithm plus 3D projection fixes.
5. Create missions for the game.
6. Update Isometric and 3D objects.

I would like to at least keep some control over the storyline and missions if possible since the game was updated and released on the Amiga (Uropa2). I would like to look at creating missions based on those that were implemented on that version of the game, although they would be reduced in scope accordingly.

The game was originally being developed in assembler (BBC Basic), however I had updated whole sections to use the ADE Macro Assembler. It currently doesn't run on the Master, however I would obviously like to fix that. I would even consider updating the code to handle a second processor allowing colour in the Isometric and 3D sections (like the extended versions of Elite).

### Downloads

[DDFS Uropa Demo](./images/Uropademo.zip "wikilink") (Watford Electronics DDFS 5.25" SSD image)
[DFS Uropa Demo](./images/UropaDemoDFS.zip "wikilink") (Acorn DFS 5.25" SSD images)

To run the DDFS SSD, you need to use the Watford Electronics DDFS since there are more than 31 files on the disc. At the demo boot menu it will ask for "City or Surface" where you can enter "C" or "S", however if you enter "T" it will show the original starting title (unfortunately it crashes if you press space to start).

The DFS SSD contains the two City and Surface demos on one disc image, but the original starting title sequence has been separated out to a new disc image due to the 31 files limitation of standard DFS.

<tt>

`City (base) keys`
`----------------`
`,               rotate left`
`.               rotate right`
`A               fire weapon`
`S               move forward`
`P               pickup object`
`T               use transporter pad`
`E               restore energy`
`F0              normal view`
`F1              status`
`F2              cargo hold`
`F3              kill sheet`
`F4              moon map`
`F5              base information`
`F6              inventory`
`F7              communication link`
`F8              trade market`

`3D section keys`
`---------------`
` ,               rotate left`
` .               rotate right`
` A               fire lasers`
` S               decrease height`
` X               increase height`
` M               cloak mode`
` H               hyperdrive travel`
` N               launch negatron (if fitted)`
` P               launch mining pod (if fitted)`
` F0              normal view`
` F1              status`
` F2              cargo hold`
` F3              kill sheet`
` F4              moon map`
` F5              base information`

</tt>

### Sample Screenshots

<table>
<tbody>
<tr class="odd">
<td><p>[[Image:Uropa00.jpg|320px|<em>'Uropa 00 screenshot <strong><br />
<em>Posted: Jul 05, 2011</em>]]<br />
</strong>Uropa 00 screenshot</em>'<br />
<em>Posted: Jul 05, 2011</em></p></td>
<td><p>[[Image:Uropa01.jpg|320px|<em>'Uropa 01 screenshot <strong><br />
<em>Posted: Jul 05, 2011</em>]]<br />
</strong>Uropa 01 screenshot</em>'<br />
<em>Posted: Jul 05, 2011</em></p></td>
</tr>
<tr class="even">
<td><p>[[Image:Uropa02.jpg|320px|<em>'Uropa 02 screenshot <strong><br />
<em>Posted: Jul 05, 2011</em>]]<br />
</strong>Uropa 02 screenshot</em>'<br />
<em>Posted: Jul 05, 2011</em></p></td>
<td><p>[[Image:Uropa03.jpg|320px|<em>'Uropa 03 screenshot <strong><br />
<em>Posted: Jul 05, 2011</em>]]<br />
</strong>Uropa 03 screenshot</em>'<br />
<em>Posted: Jul 05, 2011</em></p></td>
</tr>
<tr class="odd">
<td><p>[[Image:Uropa04.jpg|320px|<em>'Uropa 04 screenshot <strong><br />
<em>Posted: Jul 05, 2011</em>]]<br />
</strong>Uropa 04 screenshot</em>'<br />
<em>Posted: Jul 05, 2011</em></p></td>
<td><p>[[Image:Uropa05.jpg|320px|<em>'Uropa 05 screenshot <strong><br />
<em>Posted: Jul 05, 2011</em>]]<br />
</strong>Uropa 05 screenshot</em>'<br />
<em>Posted: Jul 05, 2011</em></p></td>
</tr>
<tr class="even">
<td><p>[[Image:Uropa06.jpg|320px|<em>'Uropa 06 screenshot <strong><br />
<em>Posted: Jul 05, 2011</em>]]<br />
</strong>Uropa 06 screenshot</em>'<br />
<em>Posted: Jul 05, 2011</em></p></td>
<td><p>[[Image:Uropa07.jpg|320px|<em>'Uropa 07 screenshot <strong><br />
<em>Posted: Jul 05, 2011</em>]]<br />
</strong>Uropa 07 screenshot</em>'<br />
<em>Posted: Jul 05, 2011</em></p></td>
</tr>
<tr class="odd">
<td><p>[[Image:Uropa08.jpg|320px|<em>'Uropa 08 screenshot <strong><br />
<em>Posted: Jul 05, 2011</em>]]<br />
</strong>Uropa 08 screenshot</em>'<br />
<em>Posted: Jul 05, 2011</em></p></td>
<td><p>[[Image:Uropa09.jpg|320px|<em>'Uropa 09 screenshot <strong><br />
<em>Posted: Jul 05, 2011</em>]]<br />
</strong>Uropa 09 screenshot</em>'<br />
<em>Posted: Jul 05, 2011</em></p></td>
</tr>
<tr class="even">
<td><p>[[Image:Uropa10.jpg|320px|<em>'Uropa 10 screenshot <strong><br />
<em>Posted: Jul 05, 2011</em>]]<br />
</strong>Uropa 10 screenshot</em>'<br />
<em>Posted: Jul 05, 2011</em></p></td>
<td><p>[[Image:Uropa11.jpg|320px|<em>'Uropa 11 screenshot <strong><br />
<em>Posted: Jul 05, 2011</em>]]<br />
</strong>Uropa 11 screenshot</em>'<br />
<em>Posted: Jul 05, 2011</em></p></td>
</tr>
<tr class="odd">
<td><p>[[Image:Uropa12.jpg|320px|<em>'Uropa 12 screenshot <strong><br />
<em>Posted: Jul 05, 2011</em>]]<br />
</strong>Uropa 12 screenshot</em>'<br />
<em>Posted: Jul 05, 2011</em></p></td>
<td><p>[[Image:Uropa13.jpg|320px|<em>'Uropa 13 screenshot <strong><br />
<em>Posted: Jul 05, 2011</em>]]<br />
</strong>Uropa 13 screenshot</em>'<br />
<em>Posted: Jul 05, 2011</em></p></td>
</tr>
</tbody>
</table>



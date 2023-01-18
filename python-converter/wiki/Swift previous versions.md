# SWIFT Previous Versions

**_A BBC Micro Integrated Development Environment, for Windows_**

**_Previous versions - for historical reference only, please download the latest version from_**

[<http://www.retrosoftware.co.uk/swift>](http://www.retrosoftware.co.uk/swift)

## Historical Versions

### Download

<table style="width:10%;">

<colgroup>

<col width="2%" />

<col width="8%" />

</colgroup>

<thead>

<tr class="header">

<th><p>Date:</p></th>

<th><p>02-November-2009</p></th>

</tr>

</thead>

<tbody>

<tr class="odd">

<td><p>Filename:</p></td>

<td><p><a href="Media:Swift_4.2.4.zip" title="wikilink">Swift 4.2.4.zip</a> <strong>Important : You need at least version 7 of Adobe PDF Reader installed to use this version.</strong></p></td>

</tr>

<tr class="even">

<td><p>Filesize:</p></td>

<td><p>747kb</p></td>

</tr>

<tr class="odd">

<td><p>Stable release</p></td>

<td><ul>

<li>Fixed bug where on closing project, previous projects title was left in the windows title bar</li>

<li>Fixed : If a comment had a period surrounded by alpha chars (i.e. SpriteObject.X) then Swift would think this was a reference to X within module SpriteObject.</li>

</ul></td>

</tr>

</tbody>

</table>

<table style="width:10%;">

<colgroup>

<col width="2%" />

<col width="8%" />

</colgroup>

<thead>

<tr class="header">

<th><p>Date:</p></th>

<th><p>02-November-2009</p></th>

</tr>

</thead>

<tbody>

<tr class="odd">

<td><p>Filename:</p></td>

<td><p><a href="Media:Swift_4.2.3.zip" title="wikilink">Swift 4.2.3.zip</a></p></td>

</tr>

<tr class="even">

<td><p>Filesize:</p></td>

<td><p>747kb</p></td>

</tr>

<tr class="odd">

<td><p>Beta release</p></td>

<td><ul>

<li>Fixed bug where on cancelling an Add or Add Copy Item dialog, if you clicked the red cross to close the dialog box, you got an access violation</li>

<li>Fixed : Creating a new project would not add it to the recent projects list.</li>

<li>Fixed : Would save the project multiple times when multiple windows were saved at once.</li>

<li>Fixed : Undo on sprite window would not update title bar with asterisk to say the file was changed</li>

<li>Fixed : Access violation when selecting properties for new sprite and the sprite collection not yet saved.</li>

<li>Fixed : When closing windows Project items would all be collapsed. Now stays open</li>

<li>Fixed : Save icon would not enable when sprite altered.</li>

<li>General tidy up to try and reduce some access violations</li>

</ul></td>

</tr>

</tbody>

</table>

<table style="width:10%;">

<colgroup>

<col width="2%" />

<col width="8%" />

</colgroup>

<thead>

<tr class="header">

<th><p>Date:</p></th>

<th><p>02-November-2009</p></th>

</tr>

</thead>

<tbody>

<tr class="odd">

<td><p>Filename:</p></td>

<td><p><a href="Media:Swift_4.2.2.zip" title="wikilink">Swift 4.2.2.zip</a></p></td>

</tr>

<tr class="even">

<td><p>Filesize:</p></td>

<td><p>747kb</p></td>

</tr>

<tr class="odd">

<td><p>Beta release</p></td>

<td><ul>

<li>User interface revamped with a control centre panel that contains all other panels (Project Manger, Snippets) as well as the new Books panel.</li>

<li>New Books panel for easy access to all books and views of their contents.</li>

<li>Progress window when project file is being updated. (Before it was not obvious what was causing a delay in operation)</li>

<li>Internal changes to sprite definer and Hex Editor (They were sharing the same window type, now split out into their own)</li>

</ul></td>

</tr>

</tbody>

</table>

<table style="width:10%;">

<colgroup>

<col width="2%" />

<col width="8%" />

</colgroup>

<thead>

<tr class="header">

<th><p>Date:</p></th>

<th><p>18-June-2009</p></th>

</tr>

</thead>

<tbody>

<tr class="odd">

<td><p>Filename:</p></td>

<td><p><a href="Media:Swift-v4.1_beta4.zip" title="wikilink">Swift-v4.1_beta4.zip</a></p></td>

</tr>

<tr class="even">

<td><p>Filesize:</p></td>

<td><p>722kb</p></td>

</tr>

<tr class="odd">

<td><p>Release Notes: NOTE, this is a Beta version.</p></td>

<td><ul>

<li>Recent Projects List for quick loading (number of items configurable)</li>

<li>Hex editor can load files directly via pop up menu</li>

<li>Bug Fix : Hex Editor delete key (not backspace) did not create undo entry</li>

<li>bug Fix : Hex Editor delete key (not backspace) did not always delete correctly</li>

</ul></td>

</tr>

</tbody>

</table>

<table style="width:10%;">

<colgroup>

<col width="2%" />

<col width="8%" />

</colgroup>

<thead>

<tr class="header">

<th><p>Date:</p></th>

<th><p>16-June-2009</p></th>

</tr>

</thead>

<tbody>

<tr class="odd">

<td><p>Filename:</p></td>

<td><p><a href="Media:Swift-v4.1_beta3.zip" title="wikilink">Swift-v4.1_beta3.zip</a></p></td>

</tr>

<tr class="even">

<td><p>Filesize:</p></td>

<td><p>720kb</p></td>

</tr>

<tr class="odd">

<td><p>Release Notes: NOTE, this is a Beta version.</p></td>

<td><ul>

<li>New Pop up menu on code editor. If right click over a label name (not neccasarily a label definition) then you get two options. &quot;Goto Label&quot; and &quot;Find all local references to label&quot;. Allowing you to quickly jump to you label definition or list all occurances of your label in your source code.

<dl>

<dd>![](../../retrosoftwarecouk_wiki-20160918-wikidump/images/EditorlabelMenu.gif)

</dd>

<dd><br />

<br />

</dd>

</dl></li>

<li>Search enhanced to have additional options :

<ul>

<li><strong>Ignore Comments</strong>. Any occurances of your search term will be ignored if within a comment.</li>

<li><strong>Matching options</strong>, the following options can be used to specify how a match is determined

<ul>

<li><strong>All.</strong> Matches the search test anywhere withing the text including within other words.<br />

<br />

</li>

<li><strong>Exact.</strong> Only match if no other characters next to word, for example searching for 'tin'</li>

</ul>

<dl>

<dd><em>Matches</em>

</dd>

<dd><strong>tin</strong>

</dd>

<dd>the <strong>tin</strong> was kicked<br />

<br />

</dd>

<dd><em>No match</em>

</dd>

<dd>tinned

</dd>

<dd>3tin

</dd>

<dd>tin%<br />

<br />

</dd>

</dl>

<ul>

<li><strong>Exact and none alphanumeric.</strong> Only match if no alpha numeric characters next to word (excluding white space), searching for &quot;tin&quot;</li>

</ul>

<dl>

<dd><em>Matches</em>

</dd>

<dd><strong>tin</strong>

</dd>

<dd>the <strong>tin</strong> was kicked

</dd>

<dd><strong>tin</strong>%

</dd>

<dd>&lt;<strong>tin</strong>

</dd>

<dd><ul>

<li><strong>tin</strong>+gold<br />

<br />

</li>

</ul>

</dd>

<dd><em>No match</em>

</dd>

<dd>expecting

</dd>

<dd>tin4

</dd>

</dl></li>

</ul></li>

<li>Search results now include the line the search term occurs in within

<dl>

<dd>![](../../retrosoftwarecouk_wiki-20160918-wikidump/images/SearchResults.gif)

</dd>

</dl></li>

</ul></td>

</tr>

</tbody>

</table>

<table style="width:10%;">

<colgroup>

<col width="2%" />

<col width="8%" />

</colgroup>

<thead>

<tr class="header">

<th><p>Date:</p></th>

<th><p>05-May-2009</p></th>

</tr>

</thead>

<tbody>

<tr class="odd">

<td><p>Filename:</p></td>

<td><p><a href="Media:Swift-v4.1_beta1.zip" title="wikilink">Swift-v4.1_beta2.zip</a></p></td>

</tr>

<tr class="even">

<td><p>Filesize:</p></td>

<td><p>879kb</p></td>

</tr>

<tr class="odd">

<td><p>Known bugs:</p></td>

<td><p>Exception raised when creating new projects (although project would still be created)</p></td>

</tr>

<tr class="even">

<td><p>Release Notes: NOTE, this is a Beta version.</p></td>

<td><ul>

<li>Various changes to sprite files, with new options on how the data is stored and organised. Full explanations can be found in the sprites document that is included in the zip file. Old sprite files should import and convert ok. Older versions of Swift will not be able to open most sprite files created with this version.</li>

<li>Now supports B-Em emulator.</li>

<li>Emulators now have &quot;emulator profiles&quot;, currently there are three; generic,BeebEm and B-Em. Any emulator you add must have a profile.</li>

<li>Speed of assembly vastly improved, most notable on multi file projects</li>

<li>Any object code can now have the option of saving to your project folder as well as DFS disk</li>

<li>The check for whether a DFS filename had been entered for files that weren't included in any other files has been removed. Now if DFS filename is empty it does not transfer to disk else it does.</li>

</ul>

<p><strong>Bug Fixes</strong></p>

<ul>

<li>Label names for source files in the project manager window are now sorted in a case insensitive order</li>

<li>Fixed : Label names that occur within other label names would cause Swift to find first occurrence i.e. if looking for label &quot;Start&quot; and the label &quot;GF_PLotStart&quot; occurred in the source file first then it would go to label GF_PLotStart becuase it contains the word &quot;Start&quot;.</li>

</ul></td>

</tr>

</tbody>

</table>

<table style="width:10%;">

<colgroup>

<col width="2%" />

<col width="8%" />

</colgroup>

<thead>

<tr class="header">

<th><p>Date:</p></th>

<th><p>23-May-2008</p></th>

</tr>

</thead>

<tbody>

<tr class="odd">

<td><p>Filename:</p></td>

<td><p><a href="Media:Swift-v4.0_beta3.zip" title="wikilink">Swift-v4.0_beta3.zip</a></p></td>

</tr>

<tr class="even">

<td><p>Filesize:</p></td>

<td><p>804kb</p></td>

</tr>

<tr class="odd">

<td><p>Release Notes: NOTE, this is a Beta version.</p></td>

<td><ul>

<li>Snippets : There is now a dockable (or not, it's configurable) snippets window, where you can drag highlighted bits of code or text from project item windows to. Once dragged to the snippets window Swift will store this code &quot;snippet&quot; and allow you to drag it back from the snippet window to a source or text window for any project at any time (Snippets live for as long as you wish them to). This allows you to create a library of useful functions available instantly across all your projects. Each snippet can be given a name and using a context sensitive menu you can create unlimitted categories and sub categories to organise your snippets. Categories and snippets can be moved about and re-organised freely by dragging and dropping.</li>

</ul>

<ul>

<li>The project manager window can now be docked to Swift on the left or right sides, and the display of items and labels swapped between horizontal and vertical. All options can be configured in the settings or changed on the fly from the context sensitive menus.</li>

</ul>

<ul>

<li>A tab control has been implemented at the top to enable quick switching between project items. Project items can be maximised and switched between easily in a very similer fashion to other popular IDE's</li>

</ul>

<ul>

<li>Assembly results and search results can now be docked to the Swift window or undocked/re-docked at will and dragged out of the main Swift work area. Again, giving Swift a more familier feel for people using other industry standard IDE's.</li>

</ul>

<ul>

<li>Indenting/un-indenting shortcut configurable between CTRL+SHIFT+I / CTRL+SHIFT+U and TAB / SHIFT + TAB</li>

</ul>

<ul>

<li>Configuration option to save all changed files to disk on assembly</li>

</ul>

<ul>

<li>Keyboard shortcut to save file CTRL+S, F12 to &quot;Save As&quot;</li>

</ul>

<ul>

<li>Project Item properties show exact disk location of file</li>

</ul>

<ul>

<li>Progress bar for assembly.</li>

</ul>

<ul>

<li>Removed adding of files in project properties as this is now handled from project manager.</li>

</ul>

<ul>

<li>A bug would occur if you tried to include project items from different volumes, this was because Swift uses relative paths and the underlying windows API to get relative paths cannot relate across volumes. Swift will now detect different volumes and if neccasary use the full qualified path if the volume of a project item is different than where the project file is stored.</li>

</ul></td>

</tr>

</tbody>

</table>

<table style="width:10%;">

<colgroup>

<col width="2%" />

<col width="8%" />

</colgroup>

<thead>

<tr class="header">

<th><p>Date:</p></th>

<th><p>01-May-2008</p></th>

</tr>

</thead>

<tbody>

<tr class="odd">

<td><p>Filename:</p></td>

<td><p><a href="Media:Swift-v3.2_beta2.zip" title="wikilink">Swift-v3.2_beta2.zip</a></p></td>

</tr>

<tr class="even">

<td><p>Filesize:</p></td>

<td><p>770kb</p></td>

</tr>

<tr class="odd">

<td><p>Release Notes: NOTE, this is a Beta version.</p></td>

<td><p>Bug Fixes:</p>

<ul>

<li>Fixes issue in the Sprite Designer introduced in version 3.1 where changing a pallete colour would not show the updated colour on the sprite</li>

</ul></td>

</tr>

</tbody>

</table>

<table style="width:10%;">

<colgroup>

<col width="2%" />

<col width="8%" />

</colgroup>

<thead>

<tr class="header">

<th><p>Date:</p></th>

<th><p>30-Apr-2008</p></th>

</tr>

</thead>

<tbody>

<tr class="odd">

<td><p>Filename:</p></td>

<td><p><a href="Media:Swift-v3.2_beta1.zip" title="wikilink">Swift-v3.2_beta1.zip</a></p></td>

</tr>

<tr class="even">

<td><p>Filesize:</p></td>

<td><p>770kb</p></td>

</tr>

<tr class="odd">

<td><p>Release Notes: NOTE, this is a Beta version.</p></td>

<td><p>Changes:</p>

<ul>

<li>Animation data can now be stored in the Sprite Collection data file - user selectable</li>

<li>Sprite Data Formats document updated to include details on how animations are stored</li>

</ul>

<p>Bug Fixes:</p>

<ul>

<li>Sprites who's data did not come to an even number would be regarded as corrupted even though they were not.</li>

<li>New sprites could not be created (a bug that only seems to appear in version 3.1)</li>

<li>DFS Module : Did not pad unused bytes in the last sector used on a disk to it's full size. This caused a problem for DFS Explorer/XFER51 when transferring your DFS disk to a real beeb over a serial link.</li>

</ul></td>

</tr>

</tbody>

</table>

<table style="width:10%;">

<colgroup>

<col width="2%" />

<col width="8%" />

</colgroup>

<thead>

<tr class="header">

<th><p>Date:</p></th>

<th><p>04-Apr-2008</p></th>

</tr>

</thead>

<tbody>

<tr class="odd">

<td><p>Filename:</p></td>

<td><p><a href="Media:Swift-v3.1_beta1.zip" title="wikilink">Swift-v3.1_beta1.zip</a></p></td>

</tr>

<tr class="even">

<td><p>Filesize:</p></td>

<td><p>770kb</p></td>

</tr>

<tr class="odd">

<td><p>Release Notes: NOTE, this is a Beta version.</p></td>

<td><p>Changes:</p>

<ul>

<li>New &quot;Text&quot; category for project manager. Allows text files to be created for notes, BASIC programs or boot files</li>

<li>Support for writing BASIC programs and ability to strip REMS/ empty lines prior to sending to emulator</li>

</ul>

<p>Bug Fixes:</p>

<ul>

<li>Warning appears if you try to add an item when no project active, previously exception occurred.</li>

</ul>

<p>Limitations:</p>

<ul>

<li>Cannot handle REMs on multiple statement lines, i.e. 10 PRINT &quot;Hello&quot;:REM Prints Hello, would not remove the REM</li>

</ul>

<ul>

<li>This is a Beta version, release candidate 1. This is because time is not available to thoroughly test all the new facilities with the various new modes added. All have been initially tested but not as extensively as Mode 2 sprites.</li>

</ul></td>

</tr>

</tbody>

</table>

<table style="width:10%;">

<colgroup>

<col width="2%" />

<col width="8%" />

</colgroup>

<thead>

<tr class="header">

<th><p>Date:</p></th>

<th><p>24-Mar-2008</p></th>

</tr>

</thead>

<tbody>

<tr class="odd">

<td><p>Filename:</p></td>

<td><p><a href="Media:Swift-v3.0_beta1.zip" title="wikilink">Swift-v3.0_beta1.zip</a></p></td>

</tr>

<tr class="even">

<td><p>Filesize:</p></td>

<td><p>671kb</p></td>

</tr>

<tr class="odd">

<td><p>Release Notes: NOTE, this is a Beta version.</p></td>

<td><p>Changes:</p>

<ul>

<li>All bit mapped graphic modes supported</li>

<li>Sprite animations</li>

<li>Horizontal and Verical flips</li>

<li>Rotate</li>

<li>Sprites can now be dragged and dropped to change index in the data file</li>

</ul>

<p>Limitations:</p>

<ul>

<li>Sprite animations are not saved as Beeb data, user must note index numbers used if they want to implement on Beeb. As it's only a handful of bytes this not time consuming and allows user flexibility to implement animations however they wish on the Beeb side.</li>

</ul>

<ul>

<li>This is a Beta version, release candidate 1. This is because time is not available to thoroughly test all the new facilities with the various new modes added. All have been initially tested but not as extensively as Mode 2 sprites.</li>

</ul></td>

</tr>

</tbody>

</table>

<table style="width:10%;">

<colgroup>

<col width="2%" />

<col width="8%" />

</colgroup>

<thead>

<tr class="header">

<th><p>Date:</p></th>

<th><p>8-Mar-2008</p></th>

</tr>

</thead>

<tbody>

<tr class="odd">

<td><p>Filename:</p></td>

<td><p><a href="Media:Swift-v2.5.zip" title="wikilink">Swift-v2.5.zip</a></p></td>

</tr>

<tr class="even">

<td><p>Filesize:</p></td>

<td><p>671kb</p></td>

</tr>

<tr class="odd">

<td><p>Release Notes:</p></td>

<td><p>Changes:</p>

<ul>

<li>Sprite Editor added</li>

<li>Data format for Sprite Collections included as PDF</li>

</ul>

<p>Limitations:</p>

<ul>

<li>Only supports Mode 2 with or without logical colour mask</li>

</ul></td>

</tr>

</tbody>

</table>

<table style="width:10%;">

<colgroup>

<col width="2%" />

<col width="8%" />

</colgroup>

<thead>

<tr class="header">

<th><p>Date:</p></th>

<th><p>1-Feb-2008</p></th>

</tr>

</thead>

<tbody>

<tr class="odd">

<td><p>Filename:</p></td>

<td><p><a href="Media:Swift-v2.zip" title="wikilink">Swift-v2.zip</a></p></td>

</tr>

<tr class="even">

<td><p>Filesize:</p></td>

<td><p>610kb</p></td>

</tr>

<tr class="odd">

<td><p>Release Notes:</p></td>

<td><p>Changes:</p>

<ul>

<li>Project Manager control window

<ul>

<li>All files in project viewable and accessible from floating Project Manager window</li>

<li>New files can be added/linked to/copied and added via the Project Manager</li>

<li>All labels in source files are listed in Project Manager

<ul>

<li>After successful assembly labels will have address values</li>

<li>Double clicking labels takes you to that label in the source file</li>

</ul></li>

</ul></li>

<li>Print function for source code windows.</li>

<li>Support for BeebASM 0.6</li>

<li>Open Project item removed</li>

<li>Default editor colours changed for colours that show up well on a colour printer</li>

<li>Bugs fixed from previous version that prevented new items being added to new projects</li>

</ul></td>

</tr>

</tbody>

</table>

<table style="width:10%;">

<colgroup>

<col width="2%" />

<col width="8%" />

</colgroup>

<thead>

<tr class="header">

<th><p>Date:</p></th>

<th><p>1-Jan-2008</p></th>

</tr>

</thead>

<tbody>

<tr class="odd">

<td><p>Filename:</p></td>

<td><p><a href="Media:Swift-v1.1.zip" title="wikilink">Swift-v1.1.zip</a></p></td>

</tr>

<tr class="even">

<td><p>Filesize:</p></td>

<td><p>544kb</p></td>

</tr>

<tr class="odd">

<td><p>Release Notes:</p></td>

<td><p>Changes:</p>

<ul>

<li>BeebASM profile added, can now handle projects written in BeebASM</li>

<li>Editor has had a major revamp and now has the following user settable options:

<ul>

<li>Line Numbers</li>

<li>Page width indicator (right margin indicator)</li>

<li>Tab amount (number of spaces inserted when tab pressed)</li>

<li>The colours and styles of the following elements can be set:

<ul>

<li>Comments</li>

<li>Instructions (i.e. LDA, STA)</li>

<li>Strings</li>

<li>Selections</li>

</ul></li>

</ul></li>

<li>Keys to indent blocks of text has changed from [CTRL]+[SHIFT] + (&gt; or &lt;) to [CTRL]+[SHIFT] + (I or U)</li>

<li>the undo limit previously was 1, now it's for practical purposes unlimited</li>

<li>[Bug-Fix] Swift could save files in the wrong place if many projects were opened and closed in one session.</li>

</ul></td>

</tr>

</tbody>

</table>

<table style="width:10%;">

<colgroup>

<col width="2%" />

<col width="8%" />

</colgroup>

<thead>

<tr class="header">

<th><p>Date:</p></th>

<th><p>15-Dec-2007</p></th>

</tr>

</thead>

<tbody>

<tr class="odd">

<td><p>Filename:</p></td>

<td><p><a href="Media:Swift-v1.0.zip" title="wikilink">Swift-v1.0.zip</a></p></td>

</tr>

<tr class="even">

<td><p>Filesize:</p></td>

<td><p>470kb</p></td>

</tr>

<tr class="odd">

<td><p>Release Notes:</p></td>

<td><p>Changes:</p>

<ul>

<li>N/A (initial release).</li>

</ul></td>

</tr>

</tbody>

</table>

---

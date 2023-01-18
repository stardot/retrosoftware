# Classic Development Tools

![](./images/Exmon main screen.JPG "Exmon_main_screen.JPG")

### BeebugSoft's [Exmon II](http://bbc.nvg.org/rom/Beebug/lang/)

*Target Systems:* **BBC Micro Model B and Master 128**
*Medium:* **ROM**
; *Documentation :*

:
[Exmon II Manual](./images/EXMON II manual.zip "wikilink")
[Command Reference only](http://bbc.nvg.org/rom/Beebug/lang/Exmon2-reference.pdf)
  

**Machine code monitor for the BBC Micro**
Exmon II is probably the most widely used MC monitor rom on the BBC Micro and Master series computers. It's major appeal lies in it's no-fuss interface, clear Mode 7 display and intuitive command set. Being permanently resident as a rom, Exmon II can be invoked at any time with a simple **\*E** (note no ‘dot’) and it will not corrupt any user workspace so is ideal as a software development companion tool. Sideways roms and ram can be accessed and edited (if ram) directly by typing **!n** where n is the socket number into which the target rom or ram is fitted. A help summary page is available at any time by typing a **?** at the Exmon command prompt.
One of the more advanced and notable features of Exmon II is it’s ability to trace and single step a machine code program whilst allowing the user to switch between the Exmon control screen and the subject program's text and/or graphical output screen. This is ideal for debugging games and applications where the output display is of primary interest. The last release of Exmon II, version 2.02, supports the CMOS 6502 extended instruction set and hence is fully compatible with the Master series. Exmon’s only significant deficiency is that it does not support the 6502 Second Processor (or 2P) and hence cannot be used to debug Tube® based applications.
The Exmon II manual, after many years in obscurity, has only recently been unearthed by this site. Following a professional OCR scan and conversion to pdf, this rare manual is now available for download above.
There is known to be an Acorn Electron (familiarly the **Elk**) version of Exmon II but at the time of writing this has yet to be re-discovered. The manual refers to the Electron rom and indicates that it is a full implementation apart from the colour display and dual-screen feature.

*Recommended by:* **Samwise and MartinB**
![](./images/ismec disassembler.JPG "fig:ismec disassembler.JPG")

### Ismec's [Monitor 2.01](http://bbc.nvg.org/rom/Various/prog/)

*Target Systems:* **BBC Micro Model B and Master 128**
*Medium:* **ROM**
*Documentation :* [ISMEC Monitor 2.01 manual](./images/ISMEC Monitor.zip "wikilink") and a [third party guide](Ismec.zip "wikilink") from 8BS.com's [TBI48](http://8bs.com/pool/tbi/tbi48.zip) 'Hints & Tips' disc
**Machine code monitor for the BBC Micro**
Monitor 2.01 by Ismec (hereinafter Ismec) is a bespoke BBC & Master 6502 machine code monitor rom which is, despite it's initially simple appearance, an incredibly powerful debugging tool and includes many features not offered by it's contemporaries such as Exmon II. Ismec permanently displays a full Help menu which can be cycled through using the **<Return>** key. Virtually all the commands are initiated by a red Function Key (with and without **<Shift>**) and a DIY overlay key strip makes operation very straightforward with the remaining keys being itemised in the Help menus. All operation is in Mode 7 with bright, clear displays making excellent use of colour. Indeed, it is this ‘high level’ feel to the user interface which may discourage some low-level purists who often prefer a blank screen and cursor but appearances are very definitely deceptive in this case.

A brief overview of Ismec's features is given below highlighting some of it’s perhaps less obvious refinements. If you are familiar with the very capable Exmon II you will see that Ismec’s extended functionality often significantly betters that of BeebugSoft's offering.

The monitor can be invoked from the Basic command prompt via **\*MONITOR** or the usual ‘dot’ abbreviation down to the minimum of **\*MON.**

The Hex/Ascii memory display can be continuously scrolled up and down via the cursor keys (in display pages with **<Shift>**) and **<Escape>** toggles between Hex or Ascii edit mode. A simple but often helpful feature here is that holding down the **<Copy>** key will show the contents of the location under the edit cursor in Binary notation.

**<TAB>** toggles between memory display/edit and the disassembler. The latter is unusual in that it is ‘OS aware’ and will translate known system calls and addresses into their familiar OS names. This includes calls such as **OSBYTE** & **OSWORD**, the system vectors (e.g. **IRQ1V**) and memory mapped I/O where an address is expressed as the base name, e.g. **SHEILA**, plus an offset. This is an extremely useful feature when debugging or analysing unfamiliar software. See the screen dump for some examples.

The line assembler complements the disassembler recognising named OS calls and I/0 addresses and has facilities for a pre-defined and extendable label table.

There is the usual but thorough Trace (via successive **F4** presses), Breakpoint set/reset (8 off) and a full register edit page including processor status flags.

Finally, and perhaps most usefully, Ismec fully supports the 6502 Second Processor (**2P**) and Shadow Ram on the Master. Selecting **<Shift><F4>** displays the settings page and if a 2P or Shadow Ram is present then there is an option to map into this memory or that of the I/O processor.

All in all, an excellent monitor rom and very deserving of a socket in the serious programmer’s BBC B or Master.

(The ***Third-Party User Guide*** available for download is taken from an 8bs compilation disc and is not the original Ismec manual. However, this 8Bs text in combination with the above description provides sufficient information for full use of the rom. The 8bs text also indicates that the Ismec rom was originally supplied with a utilities disc containing further low-level tools such as a disc sector editor. At the time of writing, this disc has not yet come to light.)

***UPDATE:** TopBanana has recently sourced and scanned a copy of the [Monitor 2.01 manual](./images/ISMEC Monitor.zip "wikilink")! We are still missing the accompanying cassette, however, if anyone comes across it.*

***UPDATE \#2:** Forum member s1paulr [points out](http://www.retrosoftware.co.uk/forum/viewtopic.php?p=5986#p5986) that v1.60, available from the The BBC Lives! archive link above as well as our own forum, works equally well with a co-processor enabled or disabled in software (which 2.01 does not).*

*Recommended by:* **MartinB**

### BeebugSoft's [Toolkit Plus](http://bbc.nvg.org/rom/Beebug/util/)

*Target Systems:* **BBC Micro**
*Medium:* **ROM**
*Documentation:* [Manual](http://www.bbcdocs.com/software.htm)
Toolkit Plus is designed to assist Basic programming on the BBC micro. It provides the user with more than 50 new command features which not only speed up the process of programming, but assist in the task of debugging, and generally streamline the activity of programming in Basic. Toolkit Plus also includes a full screen program editor to help you enter and modify your programs more easily.

*Recommended by:* **Samwise**
It has a command called \*CRUNCH which I used to use for compressing BASIC programs in the past to great effect.

### Computer Concept's [Disc Doctor](http://bbc.nvg.org/rom/ComputerConcepts/util/DiscDoctor-1.10.rom)

*Target Systems:* **BBC Micro**
*Medium:* **ROM**
*Documentation:* [Manual](http://www.bbcdocs.com/software.htm)
A set of disc utilities. Also includes a disassembler.

*Recommended by:* **FrancisL**, **frankoid**


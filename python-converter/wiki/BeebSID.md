# BeebSID by Martin Barr and Tom Walker

<http://www.retrosoftware.co.uk/images/BeebSIDlogothumb.png>

### Licence

Non-Profit Commercial

### Introduction

*BeebSID* is an add-on for the BBC Micro that attaches via a ribbon cable to the 1 MHz Bus and exposes a SID chip as famously employed by the Commodore 64. It was conceived from an idea by Tom Walker, built by Martin Barr and first demonstrated playing stunning 8-Bit retro music on a Master 128 running an early version of [White Light](White_Light "wikilink") at the [Retro Computer Museum Open Day](http://www.stairwaytohell.com/sthforums/viewforum.php?f=25) in Swannington, Leicestershire on the 31st May 2009.

Martin has designed, developed and ordered 25 PCBs which he will be selling for the not-for-profit price of £7. This limited number are available for pre-order [now](http://www.stairwaytohell.com/sthforums/viewtopic.php?p=21406#p21406) and will certainly sell out very quickly.

The hope is that one/some of the many capable hardware builders out there will volunteer to build and assemble *BeebSID*s for the cost of components so that as many people as possible can benefit from this tremendous bit of kit.

<table>
<tbody>
<tr class="odd">
<td><div class="floatleft">
<div class="figure">
![](./images/BeebSID complete.JPG)
<p class="caption">'''BeebSID complete <em>'<br />
</em>Posted: Tue December 29, 2009 23:25''</p>
</div>
</div></td>
<td><div class="floatright">
<div class="figure">
![](./images/BeebSID Iss 2 PCB Top.JPG)
<p class="caption">'''BeebSID Issue 2 Printed Circuit Board Design Top <em>'<br />
</em>Posted: Tue December 01, 2009 22:00''</p>
</div>
</div></td>
</tr>
<tr class="even">
<td><p><strong><em>BeebSID</em> complete</strong><br />
<em>Posted: Tue December 29, 2009 23:25</em></p></td>
<td><p><strong><em>BeebSID</em> Issue 2 Printed Circuit Board Design Top</strong><br />
<em>Posted: Tue December 01, 2009 22:00</em></p></td>
</tr>
</tbody>
</table>

<table>
<tbody>
<tr class="odd">
<td><p>Most of it's obscured by the cable, but the big chip (with the Commodore logo) at the left of the Veroboard Prototype photograph below is the 8580 SID (which the board is designed for - 6581 SIDs will need at least one modification). There are two other (smaller) chips which are just 1 MHz bus address decoding, a 9V regulator, and a few caps dotted around (the two just-visible ones to the right of the SID are the filter caps, rest are decoupling or related to voltage regulation).</p>
<p>The big cable is obviously the 1 MHz bus cable. The red/blue at the top is the power cable (drawing 5V and 12V from the Beeb's auxiliary connector). The grey cable is a phono cable for audio out - audio is also output to the 1 MHz bus and should be output through the internal speaker (or the external connector on a Master) but this doesn't seem to work on all machines. Besides, the internal speaker doesn't really do the SID justice!</p>
<p>Coding's fairly simple. The SID registers are described on the net, though here they're at $FC2x/$FC3x instead of $D4xx on the '64. It should be easy to modify a C64 SID player to the new addresses, though Tom's menu system (as shown at shows) uses a different trick - on the Master you can map RAM into $Dxxx, so the player is run unmodified and data is just copied from $D4xx to $FCxx as necessary.</p>
<p>The 1 MHz bus allows memory mapped devices (a huge number if required) to reside at fixed expansion addresses so in the case of a SID, as long as any and all implementations map the chip registers to the same addresses then commonality, and hence software compatibility with other 1 MHz bus additions, is assured.</p>
<p><a href="http://www.retrosoftware.co.uk/forum/viewforum.php?f=62">Discuss BeebSID</a></p>
<p>[[Image:BeebSidVeroboardPrototype.jpg|450px|<em>'BeebSID Veroboard Prototype <strong><br />
<em>Posted: Fri September 04, 2009 13:56</em>]]<br />
</strong></em>BeebSID'' Veroboard Prototype<em>'<br />
</em>Posted: Fri September 04, 2009 13:56''</p></td>
<td><p>[[Image:BBCMaster_C64SidMusic.JPG|450px|right|'''BBC Master 128 with BeebSID prototype at RCM Open Day - 31/05/09 <strong><br />
<em>Posted: Mon June 15, 2009 14:52</em>]]<br />
</strong>BBC Master 128 with <em>BeebSID</em> prototype at RCM Open Day - 31/05/09<em>'<br />
</em>Posted: Mon June 15, 2009 14:52''</p></td>
</tr>
</tbody>
</table>

### Videos

<table>
<tbody>
<tr class="odd">
<td><div class="floatleft">
<p>{{#ev:youtube|ySMBOMTcIaQ}}</p>
</div></td>
<td><div class="floatright">
<p>{{#ev:youtube|SzM01o86YaI}}</p>
</div></td>
</tr>
<tr class="even">
<td><p><strong>Martin Barr's first production <em>BeebSID</em><br />
running two of Tom Walker's early demos</strong><br />
<em>Posted: Wed December 30, 2009 23:51</em></p></td>
<td><p><strong>Martin Barr's first production <em>BeebSID</em> running Tom<br />
Walker's implementation of <em>Visage</em> by Link/Vibrants</strong><br />
<em>Posted: Tue January 05, 2010 01:04</em></p></td>
</tr>
</tbody>
</table>

### Parts List

I've put together a parts list for *BeebSID* which follows below. I'll itemise everything with a few words of explanation where necessary and since I tend to use Rapid for most of my supplies there will mostly be a Rapid reference but this can be used to read-across (they have pictures and data-sheets) to other suppliers. Anyway, I'll just get on with it because it's surprising how verbose and time consuming these things can become…. ;)

(Oh yes, and watch out for the highly amusing err.., anomaly regarding the DC and Phono connectors!)

1.  **BeebSID Issue 2 Printed Circuit Board** - *Posted: Tue December 29, 2009 10:32* !['''BeebSID Issue 2 Printed Circuit Board *'
    *Posted: Tue December 29, 2009 10:32''](./images/BeebSID PCB.JPG "fig:'''BeebSID Issue 2 Printed Circuit Board ' Posted: Tue December 29, 2009 10:32''")
2.  **IC1** : 74LS30
3.  **IC2** : 74LS02
4.  **IC3** : 74LS04
    -   Stick with LS for these first three because the Beeb end of the 1MHz bus and (I'm assuming) SID are TTL and I can't guarantee that CMOS or HCT etc. will play ball.

5.  **IC4** : SID 6581 (Vdd 12v) 6582 (Vdd 9v) 8580 (Vdd 9v)
    -   The Vdd voltage rating is particularly relevant to the power supply components & configuration.

6.  **IC5** : LM7805 (Both TO-220 package)
7.  **IC6** : LM7809 (could be LM7812 – see notes)
    -   The power supply side has a number of possible permutations depending on the type of SID (9v or 12v) fitted and depending on the external power supply being used. The absolute minimum config would be a 12v SID and the board being powered directly from the Beeb auxiliary power socket. In this instance, no *BeebSID* power components need be fitted and the 5v and 12v can be patched straight onto the board rails. The next simplest would be where a 12v SID is to be powered from a regulated (i.e. clean & stable) 12v supply and in this instance only the 5v regulator (IC5) and it's two caps need be fitted and the incoming 12v can be patched directly to the Vdd rail. Another possibility, again for a 12v SID, would be to replace the 7809 with a 7812 and then the board could be powered from a &gt;14v supply. If doing this, bear in mind that the greater the incoming voltage, harder the regs have to work to 'dump' the excess. Thus, at say 18v incoming, the 7812 would be fine but the 7805 would be dumping 13v at say 200mA which would be a dissipation of 2.6W – getting warm!
    -   All of the above is just standard DC regulation chit-chat and is not peculiar to *BeebSID* and the basic assumption is that a 9v SID is in use, people fit the 7805 and 7809 as advertised and power the unit from something like a 12v DC supply. In this case, LK2 is set SOUTH which take the regulated 9v to SID Vdd. If a 12v SID is being used in conjunction with a clean 12v supply then LK2 is set NORTH which will take the incoming 12v directly to the SID Vdd. Hopefully there's enough info there for folk to figure out what's needed.
    -   !['''BeebSID DC Connector Mount *'
        *Posted: Fri December 18, 2009 01:07''](./images/DC connector mount.JPG "fig:'''BeebSID DC Connector Mount ' Posted: Fri December 18, 2009 01:07''") This brings me to the DC power connector itself where I've subsequently discovered a layout error on my part which affects this connector, SK2, and also the Phono connector, SK1. I originally thought I'd just arbitrarily 'pad' these for flying leads to chassis (box) mounted connectors (which I still think is the better option) but I then decided that I might as well go the extra mile and use a pad layout to support PCB mount connectors. I duly imported some patterns from somewhere, tracked them in, did trial 'paper' fits and moved on. Now, I've subsequently realised that for both connector types I assumed the front and centre pin is +ve (or signal) and that the rear pad or pads are –ve (or ground). However, the reality is that they are both (of course) the opposite to my assumption and hence the pattern cannot be used as I intended. (A further shortfall of the patterns I imported is that they both employ circular pin holes when again in reality, these types of connector actually have 'tabs' which require slots in the PCB rather than holes.) Anyway, no panic, there is an easy work-round. !['''BeebSID RCA Connector Mount *'
        *Posted: Fri December 18, 2009 01:07''](./images/RCA connector mount.JPG "fig:'''BeebSID RCA Connector Mount ' Posted: Fri December 18, 2009 01:07''") If we are using PCB mount, we will actually solder the connectors vertically onto the PCB (sitting on their backs) by soldering the +ve (signal) tab directly to the front pad and use a short length of reasonably stiff component wire to both connect the –ve (or ground) tab to the rear PCB pad and to provide the necessary rigidity. I've done a trial fit of both types of connector to a junked PCB with similar pads as shown in the photos and happily this mounting is perfectly satisfactory.
    -   That all said, I still prefer the option of using chassis-mount connectors on flying leads soldered directly to the PCB for the DC & Phono sockets (the pad layout then being irrelevant) and for the LED as this will allow much simpler and neater installation of *BeebSID* in a plastic box. Anyway, if you have any questions on this just ask.
    -   The types I recommend are Rapid 20-0975 & 20-1120 for PCB mount and 20-1096 & 20-0226 for chassis mount.

8.  **Q1** : IRFD9024 60V P CHANNEL DIL MOSFET (Rapid 47-0230)
    -   This is for reverse-supply protection and is recommended but can be omitted by linking the D & S pads of Q1. A simple diode can be used (Cathode to S, Anode to D) but do bear in mind that there will be a 0.6v drop across a diode which may affect the 9v voltage regulator if a 'marginal' 12v supply is being used.

9.  **C1 & C2** : 6800pf Polystyrene Axial
    -   Please only use Polystyrene (Film) as other constructions will degrade the audio quality. These should be about 15mm long (body) but there is around 18mm and lots of width to play with.

10. **C4, C5, C6, C7, C13** : 0.1uf Disc Ceramic 5mm pin spacing
    -   The following 4 Electrolytic caps are 2mm pin spacing…

11. **C3** : 1uf Electrolytic (probably will be 63v but not critical)
12. **C8** : 47uf 25v
13. **C9, C11** : 10uf 25v
14. **J1, J2** : 34-way IDC straight header plug (0.1” / 2.5mm)
15. **LED1** : Red LED
    -   Any type will do, pins can be formed to fit as necessary (PCB is 2.5mm) but I suggest flying leads to a case-mounted LED

16. **R1** : 150 ohm 0.25W
17. **RP 1 - 4** : 2k2 x 8 SIL commoned resistor network ( 9 pin, common pin 1, 0.1” / 2.54mm)
    -   (Rapid 63-0220)
    -   May want to use SIL socket strip to allow optional fitting & removal ?

18. **LK1 & LK2** : These can just be soldered as required or pin-links (as used on Beebs etc.) can be fitted. Standard 0.1” / 2.54mm spacing.
19. Other items: 3 x 14 pin DIL sockets, 1 x 28 pin DIL socket, ribbon cable (length to suit) with 2 x 34-way IDC sockets.
    -   (If a ZIF socket is being considered for the SID, have a look at Rapid 22-1525 – far cheaper but a good 'half-way;' house solution.)

### *BeebSID* Software

### Tom Walker's Disks

![](./images/Sid music1.jpg "fig:Sid_music1.jpg")
**[*BeebSID* Demo](./images/BeebSID demo.zip "wikilink")** *- Tom Walker's conversion of Visage by Link/Vibrants*
 - for BBC Micro Model B and above, with *BeebSID*

[Tom's BeebSID Music Disks 1 & 2](http://www.tommowalker.co.uk/music.html) For the BBC Master 128

### PJ's SID Disks

[Disk\#1](http://stardot.org.uk/forums/viewtopic.php?f=3&t=2530&start=390#p23445) The Bill Carr Collection (Feb 2010)

[Disk\#2](http://stardot.org.uk/forums/viewtopic.php?f=3&t=2530&start=420#p25248) Music in BBC Games (May 2010)

[Disk\#3](http://stardot.org.uk/forums/viewtopic.php?f=3&t=2530&start=420#p25749) The 80s (June 2010)

[Disk\#4](http://stardot.org.uk/forums/viewtopic.php?f=3&t=2530&start=450#p26326) The Beatles (July 2010)

[Disk\#5](http://stardot.org.uk/forums/viewtopic.php?f=3&t=2530&start=450#p27297) The Movies (Aug 2010)

[Disk\#6](http://stardot.org.uk/forums/viewtopic.php?f=3&t=2530&start=480#p29432) Madonna (Oct 2010)

[Disk\#7](http://stardot.org.uk/forums/viewtopic.php?f=3&t=3651) Xmas Time (Dec 2010)

[Disk\#8](http://www.stardot.org.uk/forums/viewtopic.php?f=3&t=4516) Queen (Sept 2011)

[Disk\#9](http://www.stardot.org.uk/forums/viewtopic.php?f=3&t=2530&p=43042&hilit=1981#p43042) 1981 (Jan 2012)

### PJ's SID Games

[Game\#1](http://stardot.org.uk/forums/viewtopic.php?f=3&t=2530&start=450#p28404) Carousel 'O' Sid (Sept 2010)

[Game\#2](http://stardot.org.uk/forums/viewtopic.php?f=1&t=3578) Beeb SID Quiz (Nov 2010)

[Game\#3](http://www.stardot.org.uk/forums/viewtopic.php?f=1&t=5111) Nyan SID (April 2012)

### Preliminary Build Instructions

Fit all components except the three LS IC's and the SID. With the board stand-alone, set LK2 south and apply 12v DC. Check that the LED lights at an appropriate brightness and using a DVM confirm that 5v DC is present at Pin 14 of each LS IC socket and at Pin 25 of the SID socket. Confirm that 9v DC is present at Pin 28 of the SID socket. Switch off, set LK2 North, switch on and confirm that 12v DC is now present at Pin 28 of the SID socket. Switch off and set LK2 as appropriate to the SID type to be fitted.

Connect the unpowered board to the Beeb 1MHz bus socket via either J1 or J2 and power up the Beeb. Confirm that the Beeb is behaving normally and switch on *BeebSID*. Confirm again that the Beeb is running normally and switch off both the Beeb and *BeebSID*. Fit the three LS IC's and switch on both *BeebSID* and the Beeb, again confirming normal operation of the Beeb. Switch off the Beeb and *BeebSID* and fit the SID chip. Switch everything on and run the short 3-Voice test program confirming that the three pure tones can be clearly heard over the monitor or Beeb audio. (For the latter, LK1 must be made.)

*Note:* When (if) PCB mounting an RCA Phono socket vertically (sorry about that :/) and where the RCA has an exposed metal frame, place some insulation along the edges of the socket if it is likely to bear down on any tracks on the PCB. Although the latter are lightly insulated with solder resist, the RCA connector frame may wear through this with repeated plug/unplug operations. A simple square of insulation tape would be quite adequate or the edges of the RCA frame could be 'sleeeved' with some split sleeving. You'll see what I mean if this applies to your connector and mounting position. This is just me being cautious... ;)

That's it then - run Tom's demo as above and be amazed.... :D

### Example C64 BASIC SID program conversion to BBC BASIC / *BeebSID*

<span style="font-variant:small-caps">Although it's all C64 based, most SID examples are coded in C64 BASIC and 6502 assembler so are very easily ported to *BeebSID* by simply changing the base address of SID from $D400 (C64) to $FC20 (*BeebSID*). The C64 only used Peek and Poke (our d=?n and ?n=d) so lots of stuff can be converted in seconds.</span>

First of all, over to the original author, Ray Carlsen…

*For those wishing to test the 3 voices of the SID chip, I'll include a BASIC program to do that:*

    5 REM C64 SID 3-VOICE TEST PROGRAM
    10 FORL=54272TO54296:POKEL,0:NEXT:POKE54296,15:GOSUB60
    20 POKEW,17:POKEA,9:POKEHF,15:POKELF,35:POKES,128:GOSUB50:GOSUB70
    30 POKEW,17:POKEA,9:POKEHF,20:POKELF,40:POKES,128:GOSUB50:GOSUB80
    40 POKEW,17:POKEA,9:POKEHF,25:POKELF,50:POKES,128:GOSUB50:GOTO10
    50 FORX=1TO2000:NEXTX:RETURN
    60 W=54276:A=54277:HF=54273:LF=54272:S=54278:RETURN
    70 W=54283:A=54284:HF=54280:LF=54279:S=54285:RETURN
    80 W=54290:A=54291:HF=54287:LF=54286:S=54292:RETURN

*Line 10 resets the SID and POKEs maximum volume to the three voices. Line 20 POKEs values to voice 1 and plays a note for a few seconds. Line 30 adds voice two and plays a note mixed with voice 1 for a few seconds. Line 40 adds the third voice to the first two for a few seconds, then the program loops back to the beginning. The parameters for the three voices are in the subroutines in lines 60, 70 and 80. The subroutine in line 50 adds a delay so each voice can be monitored as the program advances. If any/all of the voices are missing or sound "muddy", suspect a bad SID.*

On the C64 the SID chip is located at address **$D400 = 54272** decimal. On *BeebSID*, the SID chip is located at **$FC20 = 64544** decimal. Therefore, all we need to do is modify any references to the C64 SID registers by **adding $2820 = 10272** decimal to the register addresses. Many C64 programs sensibly only declare the base address of SID by using something such as S=54272 and then all subsequent accesses to the sequential registers are made via S+n references and in this case we only need to change to the S=54272 to S=64544. You get the idea…

Whilst C64 machine-code is of course the same 6502 'language' as on the Beeb, the BASIC has many different syntax structures and significantly for us, direct hardware control is one of them. To directly manipulate bytes of memory or hardware registers on the Beeb, we use **?A=D** to put data into a location (where A is the address and D is the data) and **D=?A** to read a location. On the C64, the syntax is **POKE A,D** to write to a location and **D=PEEK(A)** to read a location. Therefore, to convert the above example SID program from C64 BASIC to BBC *BeebSID* BASIC, I've simply modified all the register references by adding 10272 and changed all **POKE A,D** to **?A=D** as follows…

    5 REM BeebSID 3-VOICE TEST PROGRAM
    10 FORL=64544TO64568:?L=0:NEXT:?64568=15:GOSUB60
    20 ?W=17:?A=9:?HF=15:?LF=35:?S=128:GOSUB50:GOSUB70
    30 ?W=17:?A=9:?HF=20:?LF=40:?S=128:GOSUB50:GOSUB80
    40 ?W=17:?A=9:?HF=25:?LF=50:?S=128:GOSUB50:GOTO10
    50 FORX=1TO2000:NEXTX:RETURN
    60 W=64548:A=64549:HF=64545:LF=64544:S=64550:RETURN
    70 W=64555:A=64556:HF=64552:LF=64551:S=64557:RETURN
    80 W=64562:A=64563:HF=64559:LF=64558:S=64564:RETURN

Of course, BBC BASIC has more sophisticated structures available and we could change the GOSUBs to PROCs etc. but that's 'off topic' for SID specific programming.

This is a trivial example but it adequately demonstrates what is needed when converting C64 SID software for use with *BeebSID* and hopefully between us we can start to get our teeth into converting the masses of tremendous music and audio software available for the C64. The technique for converting assembler programs is exactly the same but of course requires a liitle more analysis to determine the specific mechanisms of a given application.

### Further SID Resources

A scanned PDF copy of the C64 Programmers Reference Guide, split by chapter can be found here:
<http://www.commodore.ca/manuals/c64_programmers_reference/c64-programmers_reference.htm>

The chapter specific to programming sound is here:
<http://www.commodore.ca/manuals/c64_programmers_reference/c64-programmers_reference_guide-04-programming_sound.pdf>

<http://codebase64.org/doku.php?id=base:sid_programming> <http://www.atarimagazines.com/compute/issue146/G3_SID_simplified.php> <http://digilander.libero.it/ice00/tsid/index.html>

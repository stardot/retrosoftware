# Atomic Jet Set Willy by Kees van Oss

### Licence

Freeware (source code [available on request](mailto:contact@retrosoftware.co.uk), subject to copyright holders' permission)

_BBC Micro / Electron Jet Set Willy © 1985 Tynesoft (C) Software Projects / Chris Robson & Matthew Smith_

_Atomic Jet Set Willy by Kees van Oss, 2015_

### Introduction

Jet Set Willy is a platform video game originally written by Matthew Smith for the ZX Spectrum home computer. It was published in 1984 by Software Projects and ported to most home computers of the time. The game is a sequel to Manic Miner published in 1983, and is the second game in the Miner Willy Series. It was a significant development in the platform game genre on the home computer.

Retro Software is therefore proud to reveal a brand new Atom port by the Dutch coder Kees van Oss. This new release is an astonishingly accurate version of the original title. The conversion was 'relative' easy because the resolution of the screen matches perfectly the Atom CLEAR4 resolution. Because it's a monochrome game, the graphics are exactly the same as the original Electron game. In the original game there were not many sound effects but they are also included in the Atom version.

![ZX Spectrum cassette tape cover](../../retrosoftwarecouk_wiki-20160918-wikidump/images/JetSet.jpg "ZX Spectrum cassette tape cover")

### Platforms

====Atom==== **_Port by Kees van Oss_**

##### System Requirements

- Standard Acorn Atom

- 32 KB RAM (\#0000-\#7FFF)

- 6 KB video RAM (\#8000-\#97FF)

- Joystick connected to keyboard matrix (Optional)

- Joystick connected to PORTB AtoMMC interface (Optional)

##### Joystick Connections

An optional joystick can be connected parallel to the first row of the keyboard matrix according to the Dutch Atom Group standard:

` row      column`

`#B000     #B001`

`write      read   Joystick`

`--------------------------`

`  0   - PB0 - #01 - Jump`

`  0   - PB1 - #02 - Left`

`  0   - PB2 - #04 - Up`

`  0   - PB3 - #08 - Right`

`  0   - PB4 - #10 - Down`

An optional joystick can be connected to PORTB of the AtoMMC interface with software version 2.9.

`AtoMMC  Joystick`

`-----------------`

` PB0  -  Right`

` PB1  -  Left`

` PB2  -  Down`

` PB3  -  Up`

` PB4  -  Jump`

` PB5  -  nc`

` PB6  -  nc`

` PB7  -  nc`

` GND  -  GND`

##### Downloads

[Jet Set Willy tape/disc/AtoMMC images](../../retrosoftwarecouk_wiki-20160918-wikidump/images/JSW.zip "wikilink")

This image archive includes tape, disc and AtoMMC versions of the game. Read the included Readme.txt file for more info.

The sourcefiles are available on request and have to be compiled with the CC65 cross compiler.

Type MAKE JSW to compile the program.

An assembler listing is created in the JSW.LST file.

##### Screenshots

<table>

<tbody>

<tr class="odd">

<td><p><img src="JSW-instructions.png" title="fig:JSW instructions screenshot" alt="JSW instructions screenshot" /><br />

<strong><em>Jet Set Willy</em> instructions</strong><br />

<em>Posted: 21:00, 09 Dec 2015</em></p></td>

<td><p><img src="JSW-controls.png" title="fig:JSW controls screenshot" alt="JSW controls screenshot" /><br />

<strong><em>Jet Set Willy</em> controls</strong><br />

<em>Posted: 21:00, 09 Dec 2015</em></p></td>

<td><p><img src="JSW-intro.png" title="fig:JSW intro screenshot" alt="JSW intro screenshot" /><br />

<strong><em>Jet Set Willy</em> introscreen</strong><br />

<em>Posted: 21:00, 09 Dec 2015</em></p></td>

</tr>

<tr class="even">

<td><p><img src="JSW-bathroom.png" title="fig:JSW bathroom screenshot" alt="JSW bathroom screenshot" /><br />

<strong><em>Jet Set Willy</em> Bathroom</strong><br />

<em>Posted: 21:00, 09 Dec 2015</em></p></td>

<td><p><img src="JSW-toplanding.png" title="fig:JSW toplanding screenshot" alt="JSW toplanding screenshot" /><br />

<strong><em>Jet Set Willy</em> Top landing</strong><br />

<em>Posted: 21:00, 09 Dec 2015</em></p></td>

<td><p><img src="JSW-firstlanding.png" title="fig:JSW firstlanding screenshot" alt="JSW firstlanding screenshot" /><br />

<strong><em>Jet Set Willy</em> First landing</strong><br />

<em>Posted: 21:00, 09 Dec 2015</em></p></td>

</tr>

<tr class="odd">

<td><p><img src="JSW-kitchen.png" title="fig:JSW kitchen screenshot" alt="JSW kitchen screenshot" /><br />

<strong><em>Jet Set Willy</em> To the kitchens main stairway</strong><br />

<em>Posted: 21:00, 09 Dec 2015</em></p></td>

<td><p><img src="JSW-bedroom.png" title="fig:JSW bedroom screenshot" alt="JSW bedroom screenshot" /><br />

<strong><em>Jet Set Willy</em> Bedroom</strong><br />

<em>Posted: 21:00, 09 Dec 2015</em></p></td>

<td><p><img src="JSW-end.png" title="fig:JSW end screenshot" alt="JSW end screenshot" /><br />

<strong><em>Jet Set Willy</em> endscreen</strong><br />

<em>Posted: 21:00, 09 Dec 2015</em></p></td>

</tr>

</tbody>

</table>

##### Videos

{{\#ev:youtube|DqhyjmYD540}}

**_Atomic Jet Set Willy_ by Kees van Oss**

_Posted: Wed Dec 09._

# Videolympics / Homebrew Gaming Weekend (4-5 August 2012)

## Pictures David:

| | | | |

|--------------------------------------------|--------------------------------------------|--------------------------------------------------------------------|-----|

| ![](./images/Dscf3468-half.jpg "Dscf3468-half.jpg") | ![](Dscf3470-half.jpg "Dscf3470-half.jpg") | ![](Atom-bounce-dscf3472-half.jpg "Atom-bounce-dscf3472-half.jpg") | |

{| |- |![](./images/Electron-and-BBC-dscf3473-half.jpg "fig:Electron-and-BBC-dscf3473-half.jpg") |![](ZX81-dscf3471-half.jpg "fig:ZX81-dscf3471-half.jpg") |![](Manchester-town-hall-dscf3480-half.jpg "fig:Manchester-town-hall-dscf3480-half.jpg") | |}

## Atom Kees van Oss:

I want to give a short explanation of the hard-/software I demonstrated at the Videolympics.

### HARDWARE:

#### ATOM:

| | | |

|--------------------------|------------------------|------------------------|

| ![](./images/Atom.jpg "Atom.jpg") | ![](SD1.jpg "SD1.jpg") | ![](SD2.jpg "SD2.jpg") |

First a list of expansion boards which are mounted in my Atom:

_RAM/ROM board:_

- 32 kB user RAM

- 16 kB system ROM

- 16 ROM banks of 4 kB at \#A000

- Turbo switch for 1,8 mHz with noise killer for 1,8 mHz

_Colourboard:_

- 8 kB video RAM

- Standard Atom colours with SCART output

- Noise killer for 1 mHz

_AtoMMC interface:_

- SD-card interface

- Digital joystick connected to PORT B

#### ATOMSID:

| | |

|--------------------------------|----------------------------------|

| ![](./images/Atomsid.jpg "Atomsid.jpg") | ![](AtomSID1.jpg "AtomSID1.jpg") |

The second expansion board on PL6 is the AtomSID. It's a SID chip addressed at \#BDC0-BDDF. The board needs an external amplifier to hear the sound.

#### ISA-BUS:

![](./images/ISAbus.jpg "fig:ISAbus.jpg") The third expansion board is an ISA-bus board connected to PL7 with a 64-wired flat cable. What is an ISA bus: it's a bus to use standard 8-bits PC boards which are accessible by the I/O addresses. The bus maps the PC I/O addresses \#0000-\#03FF onto the Atom addresses \#BC00-\#BFFF. This way you can address the PC boards directly with the Atom. The ISA-bus has following connections:

- 16 Address lines

- 8 Data lines

- Reset line (is inverted to use with PC-boards)

- Read/Write lines

- Address selection line (\#BC00-\#BFFF)

- GND, +5V, +12V and -12V

The bus print is powered by an old PC power supply unit which has all the right voltages. I don't use the -5V line because there are not many boards which need this. The -12V is needed for eg the serial port.

#### ISA MODEM BOARD:

This is an old board which I had and it is mainly used to test serial communication. If you send commands to the modem, it will reply. This board is addressed at COM4 which is the PC I/O address \#02E8 and accessible with the Atom at \#BE78.

#### ISA ETHERNET BOARD:

The Ethernet board is a 16-bit board based upon a RTL8019AS Ethernet controller. The advantage of this board is that it automatically switches to 8-bit if mounted in an 8-bit ISA bus. You can find a lot of information about how to program the RTL8019AS including some example programs. I have connected this board with my laptop by using a crosswire network cable. This board is addressed at the PC I/O address \#0300 and accessible with the Atom at \#BF00.

#### ISA PARALLEL/SERIAL BOARD:

The board I used also has a floppy- and hard disk controller but they require 16-bit. The parallel-/serial ports are accessible with 8-bits. The serial port is addressed at COM2, the PC I/O address \#02F8 and accessible with the Atom at \#BEF8. The parallel port is addressed at LPT1, the PC I/O address \#0378 and accessible with the Atom at \#BF78.

#### I2C BUS:

![](./images/I2Cbus.jpg "fig:I2Cbus.jpg") This is a 2-wire bus system defined by Philips. You can define masters and slaves to communicate with. The communication is done by sending serial packages onto the bus. I have made a I2C interface (a 74LS05 with a few pull-up resistors) in the cable and am using a clock-chip and an 8-bit I/O chip to control connected to the PC parallel port. The 8-bit I/O chip is installed on a board with 4 numeric displays, 4 buttons and 1 led. To send I2C commands onto the bus, I'm using a program written in Atomic Windows to get a nice interface.

---

### SOFTWARE:

#### ATOMIC HTTP-/PING SERVER:

| | | |

|--------------------------|--------------------------|------------------------------------|

| ![](./images/HTTP.jpg "HTTP.jpg") | ![](Ping.jpg "Ping.jpg") | ![](Webserver.jpg "Webserver.jpg") |

On the Atom I can run a program which acts as a HTTP server. First you have to set the IP address of the Atom in the range of the PC IP-address. Then you can do a HTTP request on the PC in a browser to get the index page from the Atom IP-address. The Atom establishes a TCP connection with the PC and answers with a HTML-page. The program on the Atom also reply's ping requests so you can ping the Atoms IP-address from the PC.

#### ATOMIC TERMINAL:

| | |

|------------------------------------|------------------------------------|

| ![](./images/Terminal1.jpg "Terminal1.jpg") | ![](Terminal2.jpg "Terminal2.jpg") |

This is a terminal program to communicate through the serial port with a PC. You can set the com-port, baudrate, parity, byte length and nr of stop bits. On the top screen you see the local characters typed and in the bottom screen you can see the characters from the remote PC.

#### ATOMIC I2C BUS:

| | | | |

|--------------------------|--------------------------|--------------------------|--------------------------|

| ![](./images/I2C1.jpg "I2C1.jpg") | ![](I2c2.jpg "I2c2.jpg") | ![](I2C3.jpg "I2C3.jpg") | ![](I2C4.jpg "I2C4.jpg") |

This is a 2-wire bus system defined by Philips. You can define masters and slaves to communicate with. The communication is done by sending serial packages onto the bus. I have made a I2C interface (a 74LS05 with a few pull-up resistors) in the cable and am using a clock-chip and an 8-bit I/O chip to control connected to the PC parallel port. The 8-bit I/O chip is installed on a board with 4 numeric displays, 4 buttons and 1 led. To send I2C commands onto the bus, I'm using a program written in Atomic Windows to get a nice interface.

#### ATOMIC WINDOWS:

| | | |

|------------------------|------------------------|------------------------|

| ![](./images/AW1.PNG "AW1.PNG") | ![](AW2.PNG "AW2.PNG") | ![](AW3.PNG "AW3.PNG") |

This is a utility ROM for easy use of dialog boxes based on macro usage in WP6. You have extra Basic commands to build a dialog box. Every selectable object has a unique exit-code and is returned in a variable when the object is pressed. You also have the ability to change the font because it's a software font. This font can be displayed using attributes to print bold, italic, underlined, inverted, greyed or double height. These attributes may also be combined. Origianally it's written to be used with a mouse but most actions can be done with key strokes.

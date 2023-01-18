# Limitless commenting in BASIC

Recently picking up some work I did on a sequel to *[Dominion](RetroReleases#Dominion_by_Andrew_Weston "wikilink")* a few years ago now I realised that it'd be necessary to comment it as I refamiliarised with the structure let alone get used to programming again not being a programmer by trade.

So having heard of the crunching utilities for the Beeb as well as trying them a couple of times with RISC OS it seemed possible to make the listing as long as you liked in the RISC OS desktop (or potentially any other OS desktop) and then on runtime just have Crunch remove the REMs.

I haven't yet tested it with assembler comments although for Dominion I just \*LOADed the pre-assembled code into memory before the main game loaded.

For RISC OS BBC emulators there are "scriptfiles" which provide information to the RISC OS environment that you're running a BBC program and a limited amount of instructions to emulator.

So using [Toolkit+2](Classic_Development_Tools#BeebugSoft.27s_Toolkit_Plus "wikilink") with Beebit (put the ROM in the ROMs directory first), the ROM is loaded followed by a series of command lines to crunch. The script is as follows and sits within the application directory:

    BBC Script
    Machine BBC B
    LoadROM Toolkit+-2
    OSCLI"EXEC CRUNCHER

The EXEC file is a BASIC file (not sure what its parameters were on the Beeb?) that's in the application directory for the new game:

    REM CRUNCHER
    LOAD "VICTORY"
    OSCLI"CRUNCH BCLSVT:"
    SAVE "VICTORY2"
    CH."HMLOAD"

What's happening is simply the main game program file "Victory" is being programmed in a RISC OS text editor (I find !StrongEd far better than !Zap) thus opening up theoretically limitless programming space. However the program needs to be crunch'd using the Beeb environment so it has to be within the limits of the emulator machine that is operating Crunch.

The object is however to reduce the game to below 20K which is probably what any author of almost any game using machine code and/or graphics would have as an upper limit I would imagine. So using the BBC to crunch is fine and a RISC OS cruncher might well object to 6502 assembler.

The listing is duly saved with REM's removed and the game is started as normal with "HMLoad" that sets up integer variables, \*key's, assembler \*Loads and then of course loads the main game program that was just crunch'd.

I hope this is useful - any comments, improvements and suggestions welcome.

Thanks to Jonathan G.Harston for some help with this as well.

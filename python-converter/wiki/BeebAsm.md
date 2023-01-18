# BeebAsm

## Licence

This software is licensed under the [GNU GPLv3 license](http://en.wikipedia.org/wiki/GNU_General_Public_License) and can be used for commercial or non-commercial purposes.

## Downloads

Never mind all the waffle! Where can I download this thing?!

#### Windows

The latest version of BeebAsm (1.08) for Windows is available from the RS Mercurial repository. You can download it with a Mercurial client from the read-only repository:

<http://www.retrosoftware.co.uk/hg/beebasm>

Or you can download the 1.08 zip archive [here](http://www.retrosoftware.co.uk/hg/beebasm/archive/tip.zip).

Previous releases have all been tagged here:

<http://www.retrosoftware.co.uk/hg/beebasm/tags>

Choose the tagged release and then click the Zip link to download an archive manually.

Previous wiki versions are available here, should you wish to try them for some reason:

[`BeebASM-v1.04.zip`](./images/BeebASM-v1.04.zip "wikilink") `  Dec` `02` `2009` `21:24:57` `  265462` `bytes`
[`BeebASM-v1.03.zip`](./images/BeebASM-v1.03.zip "wikilink") `  Jul` `27` `2009` `21:35:01` `  246534` `bytes`
[`BeebASM-v1.02.zip`](./images/BeebASM-v1.02.zip "wikilink") `  Nov` `06` `2008` `11:06:45` `  258048` `bytes`
[`BeebASM-v1.01.zip`](./images/BeebASM-v1.01.zip "wikilink") `  Apr` `14` `2008` `14:21:36` `  225920` `bytes`
[`BeebASM-v1.00.zip`](./images/BeebASM-v1.00.zip "wikilink") `  Mar` `30` `2008` `13:02:19` `  217612` `bytes`
[`BeebASM-v0.06.zip`](./images/BeebASM-v0.06.zip "wikilink") `  Jan` `22` `2008` `19:21:21` `  231418` `bytes`
[`BeebASM-v0.05.zip`](./images/BeebASM-v0.05.zip "wikilink") `  Jan` `10` `2008` `10:55:42` `  231063` `bytes`
[`BeebASM-v0.04.zip`](./images/BeebASM-v0.04.zip "wikilink") `  Jan` `07` `2008` `09:14:08` `  220084` `bytes`
[`BeebASM-v0.02.zip`](./images/BeebASM-v0.02.zip "wikilink") `  Dec` `20` `2007` `13:41:35` `  218016` `bytes`
[`BeebASM-v0.01.zip`](./images/BeebASM-v0.01.zip "wikilink") `  Dec` `20` `2007` `13:50:25` `  210048` `bytes`

##### Programming Editor BeebAsm Language Syntax Files

Use the files below to add syntax highlighting for BeebAsm and BBC BASIC files to popular Windows editor [Notepad++](http://notepad-plus-plus.org/) or shareware editor [TextPad](http://www.textpad.com/) (BeebAsm only).

TextPad [BeebAsm syntax definition file](./images/TextPad BeebAsm Syn.zip "wikilink") by Rich Talbot-Watkins
Notepad++ [BeebAsm UDL File](./images/BeebAsm.zip "wikilink") by Rich Talbot-Watkins with contributions by David Lodge
Notepad++ [BBC BASIC UDL File](./images/BBC Basic.zip "wikilink") contributed by Stephen Coombes
For the Notepad++ UDL files, download and unzip them, then open the User Defined Language panel in Notepad++ and click Import... Choose the appropriate downloaded XML file to import them to your installation.

#### Linux

**v1.04** Download the BeebAsm 1.04 release zip archive above and extract it. Download and unzip this patch to the same directory:

[`Beebasm-linuxsupport-1.04.patch.zip`](./images/Beebasm-linuxsupport-1.04.patch.zip "wikilink") `  Feb` `23` `2011` `01:04` `  1275` `bytes`

In a console, change to that working directory and apply the patch with:

`patch` `-p1` `<` `./beebasm-linuxsupport-1.04.patch`

Then change to the src sub-directory and compile with:

`OSTYPE=$OSTYPE` `make` `code`

The executable will be built into the parent BeebAsm working directory.

**v1.01** Linux version of BeebAsm 1.01 can be downloaded [here](http://www.angelfire.com/planet/polidattilia).

#### Mac OS X

Mac OS X version of BeebAsm 1.08 can be downloaded [here](http://www.bogus.net/~dave/beebasm-osx-1.08.zip).

#### RISC OS

The latest version of BeebAsm (1.02) for RISC OS is available here:

[`BeebASM-v1.02-RISCOS.zip`](./images/BeebASM-v1.02-RISCOS.zip "wikilink") `  Dec` `15` `2008` `20:17:23` `  530530` `bytes`

Previous versions are available here, should you wish to try them for some reason:

[`BeebASM-v1.01-RISCOS.zip`](./images/BeebASM-v1.01-RISCOS.zip "wikilink") `  Apr` `15` `2008` `20:33:46` `  514750` `bytes`

![](./images/Beebasm.png "Beebasm.png")

## About BeebAsm

BeebAsm is a 6502 assembler designed specially for developing assembler programs for the BBC Micro. It uses syntax reminiscent of BBC BASIC's built-in assembler, and is able to output its object code directly into emulator-ready DFS disc images.

Many of the luxuries which come from assembling within the BBC BASIC environment on a real BBC Micro are also available here, including FOR...NEXT loops, conditional assembly (IF...ELSE...ENDIF), and all of BASIC's numerical functions, including SIN, COS and SQR - very useful for building lookup tables directly within a source file.

BeebAsm is distributed with source code, and should be easily portable to any platform you wish.

## BeebAsm 'philosophy'

BeebAsm is not like most modern assemblers, in that it doesn't just accept a source file, and output the corresponding object code file - after all, what use is a raw 6502 executable file on a PC, outside of an emulated BBC Micro environment?

Although BeebAsm *is* able to do this, this isn't the way it was intended to be used. Instead, BeebAsm can be pointed at a BBC Micro DFS disc image (.ssd or .dsd file), and can save blocks of assembled object code directly onto the 'disc', as many or as few as you wish. It is up to the source code to specify which blocks of assembled code to save, and with which name, just as if you were assembling from within BBC BASIC itself.

## Features

-   Uses standard 6502 syntax
-   Supports 65C02 instruction set
-   Denote hex literals with '&' or '$'
-   Denote binary literals with '%'
-   Multiple statement lines, statements separated by colons
-   Define labels with .label, like BBC BASIC
-   Assign variables with addr=&70, like BBC BASIC
-   Add bytes, words and strings with EQUB, EQUW, EQUD and EQUS - as an extension to BBC BASIC, these can take a comma-separated list
-   FOR...NEXT
-   IF...ELIF...ELSE...ENDIF
-   Supports all of the BBC BASIC functions and operators in expressions, e.g. SIN, COS, SQR, DIV, MOD, etc etc
-   Save object code to a disc image or to a standalone file
-   INCLUDE "file" to include another source file
-   Ability to set a guard on a memory address so it will warn you if it is assembled over
-   Use braces { } to enclose blocks of code so that all labels and variables defined within will be local to that block.
-   INCBIN command to include a binary file in the object code.
-   SKIPTO <addr> to move the address pointer to the specified address, generating an error if we are already beyond this address.
-   MAPCHAR command to allow strings to be assembled using non-ASCII codes (this is maybe more useful than it sounds; there's an example in the documentation).
-   Warns if there is no SAVE command in the source code.

## Example

Rather than trying to explain anything about BeebAsm now, let's leap straight into an example, as it can probably illustrate more about how BeebAsm should be used than a thousand lines of text.

Take the following highly contrived source file: simple.asm

<tt>

<span style="color:#008000">`\ Simple example illustrating use of BeebAsm`</span>
`oswrch = &FFEE`
`osasci = &FFE3`
`addr = &70`
<span style="color:#8000C0">`ORG`</span>` &2000         `<span style="color:#008000">`; code origin (like P%=&2000)`</span>
`.start`
`    `<span style="color:#0000C0">`LDA`</span>` #22:`<span style="color:#0000C0">`JSR`</span>` oswrch`
`    `<span style="color:#0000C0">`LDA`</span>` #7:`<span style="color:#0000C0">`JSR`</span>` oswrch`
`    `<span style="color:#0000C0">`LDA`</span>` #mytext MOD 256:`<span style="color:#0000C0">`STA`</span>` addr`
`    `<span style="color:#0000C0">`LDA`</span>` #mytext DIV 256:`<span style="color:#0000C0">`STA`</span>` addr+1`
`    `<span style="color:#0000C0">`LDY`</span>` #0`
`.loop`
`    `<span style="color:#0000C0">`LDA`</span>` (addr),Y`
`    `<span style="color:#0000C0">`BEQ`</span>` finished`
`    `<span style="color:#0000C0">`JSR`</span>` osasci`
`    `<span style="color:#0000C0">`INY`</span>
`    `<span style="color:#0000C0">`BNE`</span>` loop`
`.finished`
`    `<span style="color:#0000C0">`RTS`</span>
`.mytext `<span style="color:#0000C0">`EQUS`</span>` `<span style="color:#0080C0">`"Hello world!"`</span>`, 13, 0`
`.end`
<span style="color:#8000C0">`SAVE`</span>` `<span style="color:#0080C0">`"MyCode"`</span>`, start, end`

</tt>

...and then build it with the following command:

<tt>

`beebasm -i simple.asm -do test.ssd -boot MyCode -v`

</tt>

This will do the following:

-   create a new disc image called test.ssd, set to \*OPT 4,3
-   assemble the 6502 code and create an executable on the disc called 'MyCode'
-   create a !Boot file containing '\*RUN MyCode'
-   output a listing of the assembled code

Note how the syntax in the source file is very much like BBC BASIC, with a few small differences which we'll look at in detail later.

Note also that the source code tells the assembler what should be saved - in this example, all of the assembled code (from .start to .end), with the filename 'MyCode'. This might at first seem strange, but it's actually very simple and powerful: you have absolute control over what gets saved. If we wished, we could assemble more code elsewhere and save it as a separate file, whilst all the defined labels remained visible to both chunks of code.

## Command line options

At its very most basic, you need know only one command line option:

`-i` `<filename>`

This specifies the name of the source file for BeebAsm to process. In the absence of any switches specifying disc image filenames, SAVE commands in the source code will write out object files directly to the current directory.

`-o` `<filename>`

If this is specified, then the SAVE command can be used without supplying a filename, and this one will be used instead. This allows BeebAsm to be used like a conventional assembler, specifying both input and output filenames from the command line.

`-do` `<filename>`

This specifies the name of a new disc image to be created. All object code files will be saved to within this disc image.

`-boot` `<DFS` `filename>`

If specifed, BeebAsm will create a !Boot file on the new disc image, containing the command '\*RUN <DFS filename>'. The new disc image will already be set to \*OPT 4,3 (\*EXEC !Boot).

`-opt` `<value>`

If specified, the \*OPT 4 disc option of the generated disc image will be set to the specified value.

`-di` `<filename>`

If specified, BeebAsm will use this disc image as a template for the new disc image, rather than creating a new blank one. This is useful if you have a BASIC loader which you want to run before your executable. Note this cannot be the same as the -do filename!

`-v`

Verbose output. Assembled code will be output to the screen.

`-d`

Dumps all global symbols in Swift-compatible format after assembly. This is used internally by Swift, and is just documented for completeness.

## Source file syntax

Assembler instructions are written with the standard 6502 syntax, using either upper- or lower-case.

A label is defined by preceding it with a ".", as per the BBC Micro assembler, e.g. .loop

Instructions can be written one-per-line, or many on one line, separated by colons. A label need not be followed by a colon.

Comments are introduced by a semicolon or backslash. Unlike the BBC Micro assembler, these continue to the end of the line, and are not terminated by a colon (because this BBC Micro feature is horrible!).

Numeric literals are in decimal by default, and can be integers or reals.

Hex literals are prefixed with "&", like BBC BASIC, or with "$", like other assemblers.

A binary literal can be written prefixed with "%", e.g. %01010101

A character in single quotes (e.g. 'A') returns its ASCII code. To express the single quote character, write '''

BeebAsm can accept complex expressions, using a wide variety of operators and functions. Here's a summary:

|                   |                                                                                   |
|-------------------|-----------------------------------------------------------------------------------|
| `+` `-` `*` `/`   | Addition, subtraction, multiplication, division                                   |
| `<<`              | Arithmetic shift left; same precedence as multiplication                          |
| `>>`              | Arithmetic shift right; same precedence as division                               |
| `^`               | Raise to the power of                                                             |
| `()` or `[]`      | Bracketed expression. Use \[\] to avoid confusion with 6502 indirect instructions |
| `=` or `==`       | Test equality; returns 0 or -1                                                    |
| `<>` or `!=`      | Test non-equality; returns 0 or -1                                                |
| `<` `>` `<=` `>=` | Other comparisons; returns 0 or -1                                                |
| `AND`             | Bitwise AND                                                                       |
| `OR`              | Bitwise OR                                                                        |
| `EOR`             | Bitwise EOR                                                                       |
| `DIV`             | Integer division                                                                  |
| `MOD`             | Integer modulus                                                                   |

<table>
<tbody>
<tr class="odd">
<td><p><code>LO(val)</code> or <code>&lt;val</code></p></td>
<td><p>Return lsb of 16-bit expression (like 'val MOD 256')</p></td>
</tr>
<tr class="even">
<td><p><code>HI(val)</code> or <code>&gt;val</code></p></td>
<td><p>Return msb of 16-bit expression (like 'val DIV 256')</p></td>
</tr>
<tr class="odd">
<td><p><code>-</code></p></td>
<td><p>Negate (unary minus)</p></td>
</tr>
<tr class="even">
<td><p><code>SQR(val)</code></p></td>
<td><p>Return square root of val</p></td>
</tr>
<tr class="odd">
<td><p><code>SIN(val)</code></p></td>
<td><p>Return sine of val</p></td>
</tr>
<tr class="even">
<td><p><code>COS(val)</code></p></td>
<td><p>Return cosine of val</p></td>
</tr>
<tr class="odd">
<td><p><code>TAN(val)</code></p></td>
<td><p>Return tangent of val</p></td>
</tr>
<tr class="even">
<td><p><code>ASN(val)</code></p></td>
<td><p>Return arc-sine of val</p></td>
</tr>
<tr class="odd">
<td><p><code>ACS(val)</code></p></td>
<td><p>Return arc-cosine of val</p></td>
</tr>
<tr class="even">
<td><p><code>ATN(val)</code></p></td>
<td><p>Return arc-tangent of val</p></td>
</tr>
<tr class="odd">
<td><p><code>RAD(val)</code></p></td>
<td><p>Convert degrees to radians</p></td>
</tr>
<tr class="even">
<td><p><code>DEG(val)</code></p></td>
<td><p>Convert radians to degrees</p></td>
</tr>
<tr class="odd">
<td><p><code>INT(val)</code></p></td>
<td><p>Round to integer (towards zero)</p></td>
</tr>
<tr class="even">
<td><p><code>ABS(val)</code></p></td>
<td><p>Take the absolute value</p></td>
</tr>
<tr class="odd">
<td><p><code>SGN(val)</code></p></td>
<td><p>Return -1, 0 or 1, depending on the sign of the argument</p></td>
</tr>
<tr class="even">
<td><p><code>RND(val)</code></p></td>
<td><p>RND(1) returns a random number between 0 and 1<br />
RND(n) returns an integer between 0 and n-1</p></td>
</tr>
<tr class="odd">
<td><p><code>NOT(val)</code></p></td>
<td><p>Return the bitwise 1's complement of val</p></td>
</tr>
<tr class="even">
<td><p><code>LOG(val)</code></p></td>
<td><p>Return the base 10 log of val</p></td>
</tr>
<tr class="odd">
<td><p><code>LN(val)</code></p></td>
<td><p>Return the natural log of val</p></td>
</tr>
<tr class="even">
<td><p><code>EXP(val)</code></p></td>
<td><p>Return e raised to the power of val</p></td>
</tr>
</tbody>
</table>

Also, some constants are defined:

|             |                                                                        |
|-------------|------------------------------------------------------------------------|
| `PI`        | The value of PI (3.1415927...)                                         |
| `FALSE`     | Returns 0                                                              |
| `TRUE`      | Returns -1                                                             |
| `*` or `P%` | A special symbol which returns the current address being assembled at. |

Note that all of the above must be written in upper-case.

Variables can be defined at any point using the BASIC syntax, i.e. addr = &70.

Note that it is not possible to reassign variables once defined. However FOR...NEXT blocks have their own scope (more on this later).

## Assembler directives

These are keywords which control the assembly of the source file.

Here's a summary:

`ORG` `<addr>`

Set the address to be assembled from. This can be changed multiple times during a source file if you wish (for example) to assemble two separate blocks of code at different addresses, but share the labels between both blocks. This is exactly equivalent to BBC BASIC's 'P%=<addr>'.

`CPU` `<n>`

Selects the target CPU, which determines the range of instructions that will be accepted. The default is 0, which provides the original 6502 instruction set. The only current alternative is 1, which provides the 65C02 instruction set (including PLX, TRB etc, but not the Rockwell additions like BBR).

`SKIP` `<bytes>`

Moves the address pointer on by the specified number of bytes. Use this to reserve a space of a fixed size in the code.

`SKIPTO` `<addr>`

Moves the address pointer to the specified address. An error is generated if this address is behind the current address pointer.

`ALIGN` `<alignment>`

Used to align the address pointer to the next boundary, e.g. use ALIGN &100 to move to the next page (useful perhaps for positioning a table at a page boundary so that index accesses don't incur a "page crossed" penalty.

`INCLUDE` `"filename"`

Includes the specified source file in the code at this point.

`INCBIN` `"filename"`

Includes the specified binary file in the object code at this point.

`EQUB` `a` `[,` `b,` `c,` `...]`

Insert the specified byte(s) into the code. Note, unlike BBC BASIC, that a comma-separated sequence can be inserted.

`EQUW` `a` `[,` `b,` `c,` `...]`

Insert the specified 16-bit word(s) into the code.

`EQUD` `a` `[,` `b,` `c,` `...]`

Insert the specified 32-bit word(s) into the code.

`EQUS` `"string"` `[,` `"string",` `byte,` `...]`

Inserts the specified string into the code. Note that this can take a comma-separated list of parameters which may also include bytes. So, to zero-terminate a string, you can write:

<tt>

<span style="color:#0000C0">`EQUS`</span>` `<span style="color:#0080C0">`"My string"`</span>`, 0`

</tt>

In fact, under the surface, there is no difference between EQUS and EQUB, which is also able to take strings!

`MAPCHAR` `<ascii` `code>,` `<remapped` `code>`
`MAPCHAR` `<start` `ascii` `code>,` `<end` `ascii` `code>,` `<remapped` `code>`

By default, when EQUS "string" is assembled, the ASCII codes of each character are written into the object code. MAPCHAR allows you to specify which value should be written to the object code for each character. Suppose you have a font which contains the following symbols - space, followed by A-Z, followed by digits 0-9, followed by .,!?-'

You could specify this with MAPCHAR as follows:

<tt>

<span style="color:#8000C0">`MAPCHAR`</span>` `<span style="color:#0080C0">`' '`</span>`, 0`
<span style="color:#8000C0">`MAPCHAR`</span>` `<span style="color:#0080C0">`'A'`</span>`,`<span style="color:#0080C0">`'Z'`</span>`, 1`
<span style="color:#8000C0">`MAPCHAR`</span>` `<span style="color:#0080C0">`'0'`</span>`,`<span style="color:#0080C0">`'9'`</span>`, 27`
<span style="color:#8000C0">`MAPCHAR`</span>` `<span style="color:#0080C0">`'.'`</span>`, 37`
<span style="color:#8000C0">`MAPCHAR`</span>` `<span style="color:#0080C0">`','`</span>`, 38`
<span style="color:#8000C0">`MAPCHAR`</span>` `<span style="color:#0080C0">`'!'`</span>`, 39`
<span style="color:#8000C0">`MAPCHAR`</span>` `<span style="color:#0080C0">`'?'`</span>`, 40`
<span style="color:#8000C0">`MAPCHAR`</span>` `<span style="color:#0080C0">`'-'`</span>`, 41`
<span style="color:#8000C0">`MAPCHAR`</span>` `<span style="color:#0080C0">`'''`</span>`, 42`

</tt>

Now, when writing strings with EQUS, these codes will be written out instead of the default ASCII codes.

`GUARD` `<addr>`

Puts a 'guard' on the specified address which will cause an error if you attempt to assemble code over this address.

`CLEAR` `<start>,` `<end>`

Clears all guards between the <start> and <end> addresses specified. This can also be used to reset a section of memory which has had code assembled in it previously. BeebAsm will complain if you attempt to assemble code over previously assembled code at the same address without having CLEARed it first.

`SAVE` `["filename"],` `start,` `end` `[,` `exec` `[,` `reload]` `]`

Saves out object code to either a DFS disc image (if one has been specified), or to the current directory as a standalone file. A source file must have at least one SAVE statement in it, otherwise nothing will be output. BeebAsm will warn if this is the case.

If no filename is specified, the filename specified in the command line by -o will be used.

'exec' can be optionally specified as the execution address of the file when saved to a disc image.

'reload' can additionally be specified to save the file on the disc image to a different address to that which it was saved from. Use this to assemble code at its 'native' address, but which loads at a DFS-friendly address, ready to be relocated to its correct address upon execution. There is an example of this in the distribution, called 'relocdemo.asm'.

`PRINT`

Displays some text. PRINT takes a comma-separated list of strings or values. To print a value in hex, prefix the expression with a '~' character.

Examples:

<tt>

<span style="color:#8000C0">`PRINT`</span>` `<span style="color:#0080C0">`"Value of label 'start' ="`</span>`, ~start`
<span style="color:#8000C0">`PRINT`</span>` `<span style="color:#0080C0">`"numdots ="`</span>`, numdots, `<span style="color:#0080C0">`"dottable size ="`</span>`, dotend-dotstart`

</tt>

`ERROR` `"message"`

Causes BeebAsm to abort assembly with the provided error message. This can be useful for enforcing certain constraints on generated code, for example:

<tt>

`.table`
`    `<span style="color:#8000C0">`FOR`</span>` n, 1, 32`
`        `<span style="color:#0000C0">`EQUB`</span>` 255 / n`
`    `<span style="color:#8000C0">`NEXT`</span>
<span style="color:#8000C0">`IF`</span>` `<span style="color:#8000C0">`HI`</span>`(P%)<>`<span style="color:#8000C0">`HI`</span>`(table)`
`   `<span style="color:#8000C0">`ERROR`</span>` `<span style="color:#0080C0">`"Table crosses page boundary"`</span>
<span style="color:#8000C0">`ENDIF`</span>

</tt>

`FOR` `<var>,` `start,` `end` `[,` `step]` `...` `NEXT`

I wanted this to have exactly the same syntax as BASIC, but I couldn't without rewriting my expression parser, so we're stuck with this for now.

It works exactly like BASIC's FOR...NEXT. For example:

<tt>

<span style="color:#8000C0">`FOR`</span>` n, 0, 10, 2    `<span style="color:#008000">`; loop with n = 0, 2, 4, 6, 8, 10`</span>
`    `<span style="color:#8000C0">`PRINT`</span>` n`
`    `<span style="color:#0000C0">`LDA`</span>` #0:`<span style="color:#0000C0">`STA`</span>` &900+n`
`    `<span style="color:#0000C0">`LDA`</span>` #n:`<span style="color:#0000C0">`STA`</span>` &901+n`
<span style="color:#8000C0">`NEXT`</span>

</tt>

The variable n only exists for the scope of the FOR...NEXT loop. Also, any labels or variables defined within the loop are only visible within it. However, unlike BBC BASIC, forward references to labels inside the loop will work properly, so, for example, this little multiply routine is perfectly ok:

<tt>

`.multiply`
`    `<span style="color:#008000">`\\ multiplies A*X, puts result in product/product+1`</span>
`    `<span style="color:#0000C0">`CPX`</span>` #0:`<span style="color:#0000C0">`BEQ`</span>` zero`
`    `<span style="color:#0000C0">`DEX`</span>`:`<span style="color:#0000C0">`STX`</span>` product+1`
`    `<span style="color:#0000C0">`LSR`</span>` A:`<span style="color:#0000C0">`STA`</span>` product:`<span style="color:#0000C0">`LDA`</span>` #0`
`    `<span style="color:#8000C0">`FOR`</span>` n, 0, 7`
`        `<span style="color:#0000C0">`BCC`</span>` skip:`<span style="color:#0000C0">`ADC`</span>` product+1:.skip   `<span style="color:#008000">`\\ would break BBC BASIC!`</span>
`        `<span style="color:#0000C0">`ROR`</span>` A:`<span style="color:#0000C0">`ROR`</span>` product`
`    `<span style="color:#8000C0">`NEXT`</span>
`    `<span style="color:#0000C0">`STA`</span>` product+1:`<span style="color:#0000C0">`RTS`</span>
`.zero`
`    `<span style="color:#0000C0">`STX`</span>` product:`<span style="color:#0000C0">`STX`</span>` product+1:`<span style="color:#0000C0">`RTS`</span>

</tt>

`IF...ELIF...ELSE...ENDIF`

Use to assemble conditionally. Like anything else in BeebAsm, these statements can be placed on one line, separated by colons, but even if they are, ENDIF must be present to denote the end of the IF block (unlike BBC BASIC).

Examples of use:

<tt>

<span style="color:#008000">`\\ build a rather strange table`</span>
<span style="color:#8000C0">`FOR`</span>` n, 0, 9`
`    `<span style="color:#8000C0">`IF`</span>` (n `<span style="color:#8000C0">`AND`</span>` 1) = 0`
`        a = n*n`
`    `<span style="color:#8000C0">`ELSE`</span>
`        a = -n*n`
`    `<span style="color:#8000C0">`ENDIF`</span>
`    `<span style="color:#0000C0">`EQUB`</span>` a`
<span style="color:#8000C0">`NEXT`</span>

<span style="color:#8000C0">`IF`</span>` debugraster:`<span style="color:#0000C0">`LDA`</span>` #3:`<span style="color:#0000C0">`STA`</span>` &FE21:`<span style="color:#8000C0">`ENDIF`</span>

<span style="color:#8000C0">`IF`</span>` rom`
`    `<span style="color:#8000C0">`ORG`</span>` &8000`
`    `<span style="color:#8000C0">`GUARD`</span>` &C000`
<span style="color:#8000C0">`ELIF`</span>` tube`
`    `<span style="color:#8000C0">`ORG`</span>` &B800`
`    `<span style="color:#8000C0">`GUARD`</span>` &F800`
<span style="color:#8000C0">`ELSE`</span>
`    `<span style="color:#8000C0">`ORG`</span>` &3C00`
`    `<span style="color:#8000C0">`GUARD`</span>` &7C00`
<span style="color:#8000C0">`ENDIF`</span>

</tt>

`{` `...` `}`

Curly braces can be used to specify a block of code in which all symbols and labels defined will exist only within this block. Effectively, this is a mechanism for providing 'local labels' without the slightly cumbersome syntax demanded by some other assemblers. These can be nested. Any symbols defined within a block will override any of the same name outside of the block, exactly like C/C++ - not sure if I like this behaviour, but for now it will stay.

Example of use:

<tt>

`.initialise`
`{`
`    `<span style="color:#0000C0">`LDY`</span>` #31`
`    `<span style="color:#0000C0">`LDA`</span>` #0`
`.loop              `<span style="color:#008000">`; label visible only within the braces`</span>
`    `<span style="color:#0000C0">`STA`</span>` buffer,Y`
`    `<span style="color:#0000C0">`DEY`</span>
`    `<span style="color:#0000C0">`BPL`</span>` loop`
`    `<span style="color:#0000C0">`RTS`</span>
`}`
`.copy`
`{`
`    `<span style="color:#0000C0">`LDY `</span>`#31`
`.loop              `<span style="color:#008000">`; perfectly ok to define .loop again in a new block`</span>
`    `<span style="color:#0000C0">`LDA`</span>` source,Y`
`    `<span style="color:#0000C0">`STA`</span>` dest,Y`
`    `<span style="color:#0000C0">`DEY`</span>
`    `<span style="color:#0000C0">`BPL`</span>` loop`
`    `<span style="color:#0000C0">`RTS`</span>
`}`

</tt>

`PUTFILE` `"host` `filename",` `["beeb` `filename",]` `<start` `addr>` `[,<exec` `addr>]`

This provides a convenient way of copying a file from the host OS directly to the output disc image. If no "beeb filename" is provided, the host filename will be used (and must therefore be 7 characters or less in length). A start address must be provided (and optionally an execution address can be provided too).

`PUTBASIC` `"host` `filename"` `[,` `"beeb` `filename"]`

This takes a BASIC program as a plaintext file on the host OS, tokenises it, and outputs it to the disc image as a native BASIC file. Credit to Thomas Harte for the BASIC tokenising routine.

`MACRO` `<name>` `[,<parameter` `list...>]` `...` `ENDMACRO`

This pair of commands is used to define assembler macros. Their use is best illustrated by an example:

<tt>

<span style="color:#8000C0">`MACRO`</span>` ADDI8 addr, val`
`    `<span style="color:#8000C0">`IF`</span>` val=1`
`        `<span style="color:#0000C0">`INC`</span>` addr`
`    `<span style="color:#8000C0">`ELIF`</span>` val>1`
`        `<span style="color:#0000C0">`CLC`</span>
`        `<span style="color:#0000C0">`LDA`</span>` addr`
`        `<span style="color:#0000C0">`ADC`</span>` #val`
`        `<span style="color:#0000C0">`STA`</span>` addr`
`    `<span style="color:#8000C0">`ENDIF`</span>
<span style="color:#8000C0">`ENDMACRO`</span>

</tt>

This defines a macro called ADDI8 ("ADD Immediate 8-bit") whose function is to add a constant to a memory address. It expects two parameters: the memory address and the constant value. The body of the macro contains an IF block which will generate the most appropriate code according to the constant value passed in.

Then, at any point afterwards, the macro can be used as follows:

<tt>

`ADDI8 &900, 1         `<span style="color:#008000">`; increment address &900 by 1`</span>
`ADDI8 bonus, 10      `<span style="color:#008000">`; add 10 to the memory location 'bonus'`</span>
`ADDI8 pills, pill_add  `<span style="color:#008000">`; pills += pill_add`</span>

</tt>

Macros can also be called from other macros, as demonstrated by this somewhat contrived example:

<tt>

<span style="color:#8000C0">`MACRO`</span>` ADDI16 addr, val`
`    `<span style="color:#8000C0">`IF`</span>` val=0`
`        ; do nothing`
`    `<span style="color:#8000C0">`ELIF`</span>` val=1`
`        `<span style="color:#0000C0">`INC`</span>` addr`
`        `<span style="color:#0000C0">`BNE`</span>` skip1`
`        `<span style="color:#0000C0">`INC`</span>` addr+1`
`        .skip1`
`    `<span style="color:#8000C0">`ELIF HI`</span>`(val)=0`
`        ADDI8 addr, val`
`        `<span style="color:#0000C0">`BCC`</span>` skip2`
`        `<span style="color:#0000C0">`INC`</span>` addr+1`
`        .skip2`
`    `<span style="color:#8000C0">`ELSE`</span>
`        `<span style="color:#0000C0">`CLC`</span>
`        `<span style="color:#0000C0">`LDA`</span>` addr`
`        `<span style="color:#0000C0">`ADC`</span>` #`<span style="color:#8000C0">`LO`</span>`(val)`
`        `<span style="color:#0000C0">`STA`</span>` addr`
`        `<span style="color:#0000C0">`LDA`</span>` addr+1`
`        `<span style="color:#0000C0">`ADC`</span>` #`<span style="color:#8000C0">`HI`</span>`(val)`
`        `<span style="color:#0000C0">`STA`</span>` addr+1`
`    `<span style="color:#8000C0">`ENDIF`</span>
<span style="color:#8000C0">`ENDMACRO`</span>

</tt>

Care should be taken with macros, as the details of the assembled code are hidden. In the above ADDI16 example, the C flag is not set consistently, depending on the inputs to the macro (e.g. it remains unchanged if val=0 or 1, and will not be correct if val&lt;256).

## Tips and tricks

BeebAsm's approach of treating memory as a canvas which can be written to, saved, and rewritten if desired makes it very easy to create certain types of applications.

Imagine wanting to create a program which used the BBC Micro's main RAM, plus 2 sideways RAM banks. If there was executable code in main RAM and in both banks, it's quite likely that you'd want to share label names amongst all of these blocks of code, so that main RAM routines could page in the appropriate RAM bank and call a routine in it, and likewise sideways RAM banks could call routines in main RAM.

Here's one way you could do that in BeebAsm:

<tt>

`   `<span style="color:#008000">`\\ Declare origin of main RAM code`</span>
`   `<span style="color:#8000C0">`ORG &1100`</span>
`   `<span style="color:#008000">`\\ Put a guard at the start of screen`</span>
`   `<span style="color:#8000C0">`GUARD &5800`</span>
`   .mainstart`
`     `<span style="color:#0000C0">`LDA`</span>` #5:`<span style="color:#0000C0">`STA`</span>` &F4:`<span style="color:#0000C0">`STA`</span>` &FE30   `<span style="color:#008000">`; page in RAM bank 2`</span>
`     `<span style="color:#0000C0">`JSR`</span>` bank2routine`
`     `<span style="color:#909090">`...`</span>
`   .mainroutine`
`     `<span style="color:#909090">`...`</span>
`   .mainend`
`   `<span style="color:#8000C0">`SAVE`</span>` `<span style="color:#0080C0">`"Main"`</span>`, mainstart, mainend, mainentry`
`   `<span style="color:#008000">`\\ Declare origin of bank 1 code`</span>
`   `<span style="color:#8000C0">`ORG`</span>` &8000`
`   `<span style="color:#008000">`\\ Put a guard after the RAM bank so we don't stray over our boundary`</span>
`   `<span style="color:#8000C0">`GUARD`</span>` &C000`
`   .bank1start`
`     `<span style="color:#909090">`...`</span>
`     `<span style="color:#0000C0">`JSR`</span>` mainroutine`
`     `<span style="color:#909090">`...`</span>
`   .bank1end`
`   `<span style="color:#8000C0">`SAVE`</span>` `<span style="color:#0080C0">`"Bank1"`</span>`, bank1start, bank1end`
`   `<span style="color:#008000">`\\ Clear memory used by previous bank`</span>
`   `<span style="color:#8000C0">`CLEAR`</span>` &8000, &C000`
`   `<span style="color:#008000">`\\ Declare origin of bank 2 code`</span>
`   `<span style="color:#8000C0">`ORG`</span>` &8000`
`   `<span style="color:#008000">`\\ Put a guard after the RAM bank so we don't stray over our boundary`</span>
`   `<span style="color:#8000C0">`GUARD`</span>` &C000`
`   .bank2start`
`     `<span style="color:#909090">`...`</span>
`   .bank2routine`
`     `<span style="color:#0000C0">`RTS`</span>
`     `<span style="color:#909090">`...`</span>
`   .bank2end`
`   `<span style="color:#8000C0">`SAVE`</span>` `<span style="color:#0080C0">`"Bank2"`</span>`, bank2start, bank2end`

</tt>

Because all of this code is assembled in one session, label and variable names persist across the assembly of all blocks of code.

For tidiness, you could move the source code for each block of code into a different file, and then just INCLUDE these in your main source file:

<tt>

`   `<span style="color:#8000C0">`INCLUDE`</span>` `<span style="color:#0080C0">`"main.asm"`</span>
`   `<span style="color:#8000C0">`INCLUDE`</span>` `<span style="color:#0080C0">`"bank1.asm"`</span>
`   `<span style="color:#8000C0">`INCLUDE`</span>` `<span style="color:#0080C0">`"bank2.asm"`</span>

</tt>

![](./images/Beebasm demoscreen.png "Beebasm_demoscreen.png")

## Demo

There's a little assembler demo included called "demo.asm".

Build it with something like:

<tt>

`beebasm -i demo.asm -do demo.ssd -boot Code -v`

</tt>

and it will create a bootable disc image.

As well as demonstrating some of the features of BeebAsm (including building lookup tables), it's also a fairly good demo of pushing the hardware to its limits, in terms of creating a flicker-free animation, updating at 50Hz. (This is not to say that it's particularly impressive, but nonetheless, it really is pushing the hardware!!). Use 'Z' and 'X' to change the rotation speed and direction of the star globe.

There is also a demo called "relocdemo.asm", which shows how the 'reload address' feature of SAVE can be used to write self-relocating code. This is based on the above demo, but it runs at a low address (&300).

## Version history

<table>
<tbody>
<tr class="odd">
<td><p>16/06/2011</p></td>
<td><p>1.06</p></td>
<td><p>Bugfix: Fixed bug in EQUD.<br />
Added ERROR directive for aborting assembly.<br />
Added -opt command line switch for setting the *OPT 4 value of the generated disc image.</p></td>
</tr>
<tr class="even">
<td><p>25/04/2011</p></td>
<td><p>1.05</p></td>
<td><p>Added macros.<br />
Added PUTFILE (to add a binary file to the disc image) and PUTBASIC (to add a tokenised BASIC program to the disc image, converted from a plaintext file). <strong>Credit to Thomas Harte for the BASIC tokenisation code.</strong><br />
Fixed an almighty bug which read beyond the bounds of the lines of the source code.<br />
Added a version of the SAVE command which uses an output filename passed in the command line.</p></td>
</tr>
<tr class="odd">
<td><p>02/12/2009</p></td>
<td><p>1.04</p></td>
<td><p><strong>Additions by Kevin Bracey:</strong><br />
Added 65C02 instruction set and CPU directive.<br />
Added ELIF, EQUD.<br />
SKIP now lists the current address.</p></td>
</tr>
<tr class="even">
<td><p>27/07/2009</p></td>
<td><p>1.03</p></td>
<td><p>Bugfix: swapped around the operation of the unary &lt; and &gt; operators to match the documentation, and other assemblers.<br />
Added '$' as a valid hex literal prefix.<br />
Added '%' as a binary literal prefix.</p></td>
</tr>
<tr class="odd">
<td><p>06/11/2008</p></td>
<td><p>1.02</p></td>
<td><p>Bugfix: now it's possible to save location &amp;FFFF.<br />
Added 'reload address' parameter to SAVE.<br />
Properly integrated the GPL License text into the distribution.</p></td>
</tr>
<tr class="even">
<td><p>14/04/2008</p></td>
<td><p>1.01</p></td>
<td><p>Bugfixes: allow lower case index in abs,x or abs,y.<br />
Fails if the output file already exists in the output disc image.<br />
Symbol names may now begin with assembler opcode or command names.</p></td>
</tr>
<tr class="odd">
<td><p>30/03/2008</p></td>
<td><p>1.00</p></td>
<td><p>First stable release. Corrected a few C++ compliance issues in the source code.</p></td>
</tr>
<tr class="even">
<td><p>22/01/2008</p></td>
<td><p>0.06</p></td>
<td><p>Fixed bug with forward-referenced labels in indirect instructions.</p></td>
</tr>
<tr class="odd">
<td><p>09/01/2008</p></td>
<td><p>0.05</p></td>
<td><p>Added MAPCHAR.<br />
Fixed SKIPTO (see, told you I was doing it quickly!).<br />
Enforce '%' as an end-of-symbol character.<br />
Fixed bug in overlayed assembly.<br />
Warns if there is no SAVE command in the source file.</p></td>
</tr>
<tr class="even">
<td><p>06/01/2008</p></td>
<td><p>0.04</p></td>
<td><p>Added braces for scoping labels.<br />
Added INCBIN, SKIPTO.<br />
Added some missing functions (NOT, LOG, LN, EXP).<br />
Tightened up error checking on assembling out of range addresses (negative, or greater than &amp;FFFF).<br />
Now distinguishes internally between labels and other symbols.</p></td>
</tr>
<tr class="odd">
<td><p>05/01/2008</p></td>
<td><p>0.03</p></td>
<td><p>Added symbol dump for use with Swift.</p></td>
</tr>
<tr class="even">
<td><p>20/12/2007</p></td>
<td><p>0.02</p></td>
<td><p>Fixed small bug which withheld filename and line number display in error messages.</p></td>
</tr>
<tr class="odd">
<td><p>16/12/2007</p></td>
<td><p>0.01</p></td>
<td><p>First released version.</p></td>
</tr>
</tbody>
</table>

## Reporting bugs

There are bound to be loads. I wrote it quickly! Please help me zap all the problems by reporting any bugs to me, Rich Talbot-Watkins, [here](http://www.retrosoftware.co.uk/forum/viewforum.php?f=17) or via [email](http://www.retrosoftware.co.uk/forum/memberlist.php?mode=viewprofile&u=57).

Thank you!

[Richtw](User%3ARichtw "wikilink") 13:10, 28 July 2009 (BST)

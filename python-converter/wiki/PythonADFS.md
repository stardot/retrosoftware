# Python ADFS modules and tools by David Boddie

## Licence

This software is licensed under the [GNU GPLv3 license](http://en.wikipedia.org/wiki/GNU_General_Public_License) and can be used for commercial or non-commercial purposes.

## Downloads

The latest version of Python ADFS is available from the RS Mercurial repository. You can download it with a Mercurial client from the read-only repository:

<http://www.retrosoftware.co.uk/hg/python-adfs>

Or you can download a zip archive of the latest code [here](http://www.retrosoftware.co.uk/hg/python-adfs/archive/tip.zip).

Previous releases have all been tagged here:

<http://www.retrosoftware.co.uk/hg/python-adfs/tags>

Choose the tagged release and then click the Zip link to download an archive manually.

## About Python ADFS

This project is a collection of Python modules and tools for reading Advanced Disc Filing System (ADFS) data from floppy disk images and extracting data from them. The project was first published on the 4 September 2010 and was [originally hosted](https://developer.berlios.de/projects/python-adfs/) by _BerliOS Developer_, before the announcement of that service's planned closure at the end of 2011.

## ADFSlib and ADF2INF

Name : **ADFSlib.py** and **ADF2INF.py**

Author : David Boddie

Created : Wed 18th October 2000

Purpose : Convert ADFS disc images (ADF) to INF files

This is a snapshot of my ADFS floppy disc image reading library and its associated utility.

The Advanced Disc Filing System (ADFS), the native filing system in use on RISC OS machines, was initially introduced by Acorn as a replacement for their Disc Filing System (DFS), appearing for microcomputers such as the Electron and Master Compact. Just as these computers used certain formats of disc with various capacities, all having a common structure, emulators of these systems are able to create, read and write "images" of such discs. This gives the modern user access to applications, data and games without the need to setup and maintain ageing hardware.

Emulators typically allow the original filing system software to be used, providing some abstraction at the emulated hardware level so that images rather than actual discs are manipulated. This is useful for accessing files in their original setting. However, if data is to be extracted for other purposes, tools are required to decode such images to recover files and, where possible, the directory structure. One such tool, ADF2INF, is able to manage this process for a number of disc image formats, using the ADFSlib library to interpret data found in disc images. Other tools may be found via the [Stairway To Hell](http://www.stairwaytohell.com/) website.

The ADFSlib module provides a class with the minimum functionality required to _attempt_ to read and interpret various formats of ADFS disc image. Since detailed documentation on many of these formats is not readily available and, since there is a scarcity of disc images for some, provision for reading the older formats is as yet untested. Having said that, it aims to be able to read the following formats:

- 160K (S format)

- 320K (M format)

- 640K (L format)

- 800K (D format)

- 800K (E format)

- 1600K (E format)

''WARNING: note that in previous versions of the _ADF2INF_ tool, E format disc images were read **incorrectly**. The user is strongly advised to verify that their data has been transferred correctly when using this library or dependent tools to extract files from disc images.''

The ADF2INF tool provides a command line interface to the ADFSlib library and replaces the tool of the same name which was distributed in the [T2Tools](http://www.boddie.org.uk/david/Projects/Emulation/T2Tools) package. The ADF2INF utility will take advantage of my Python _[CMDSyntax](http://www.boddie.org.uk/david/Projects/Python/CMDSyntax)_ module, if available.

Install ADFSlib and ADF2INF (as root) by typing

`python setup.py install`

or just use them from the directory in which you unpack them.

## Command line options

**Syntax:** `ADF2INF.py` `[-l]` `[-d]` `[-t]` `[-s` `separator]` `[-v]` `[-c` `characters]` `[-m]` `<ADF` `file>` `<destination` `path>`

_ADF2INF version 0.42 (Sun 29th August 2010)_

_ADFSlib version 0.42_

Take the files stored in the directory given and store them as files with corresponding INF files.

If the `-l` flag is specified then the catalogue of the disc will be printed.

The `-d` flag specifies that a directory should be created using the disc's name into which the contents of the disc will be written.

The `-t` flag causes the load and execution addresses of files to be interpreted as file type information for files created on RISC OS. A separator used to append a suffix onto the file is optional and defaults to the standard period character; e.g. myfile.fff

The `-s` flag is used to specify the character which joins the file name to the file type. This can only be specified when extracting files from a disc image.

The `-v` flag causes the disc image to be checked for simple defects and determines whether there are files and directories which cannot be correctly located by this tool, whether due to a corrupted disc image or a bug in the image decoding techniques used.

The `-c` flag allows the user to define a conversion dictionary for the characters found in ADFS filenames. The format of the string used to define this dictionary is a comma separated list of character pairs:

`<src1><dest1>[,<src2><dest2>]...`

If no conversion dictionary is specified then a default dictionary will be used. This is currently defined as

`{'/':` `'.'}`

The `-m` flag determines whether the files extracted from the disc image should retain their time stamps on the target system.

## Version history

| | | |

|------------|------|---------------------------------------------------------------|

| 05/10/2011 | 0.42 | Migration from BerliOS Developer to Retro Software repository |

| 21/08/2010 | 0.40 | First released version. |

## Acknowledgements

Thanks to John Kortink and David Ruck for their assistance and advice. Any errors or faults in this tool are not theirs.

## Reporting bugs

If you discover a bug please let me, David Boddie, know about it by posting about it [here](http://www.retrosoftware.co.uk/forum/viewtopic.php?f=19&t=592) or via [PM](http://www.retrosoftware.co.uk/forum/memberlist.php?mode=viewprofile&u=237).

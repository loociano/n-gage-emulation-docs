# N-Gage Emulation Docs
_Work in Progress by [@loociano](https://github.com/loociano), last update on June 2017_

![ ](https://raw.githubusercontent.com/loociano/N-Gage-emu-docs/master/img/ngage-motherboard.png)

## Contents

- [Emulators](#emulators)
- [Tools](#tools)
- [System Specs](#system-specs)
- [Memory Map](#memory-map)
- [S60](#s60)
  - [SDK](#sdk)
- [File Formats](#file-formats)
  - [Utilities](#utilities)
  - [E32Image Header](#e32image-header)
    - [UIDs](#uids)
- [Tutorials](#tutorials)
- [References](#references)
- [Books](#books)
- [Thanks](#thanks)

## Emulators
* [NGEmu](https://github.com/NGEmu/NGEmu) by [@tambry](https://github.com/tambry): HLE N-Gage emulator written in C++ for Windows

## Tools
* [Rusty Starship](https://gitlab.com/tambre/rusty-starship) by [@tambre](https://gitlab.com/tambre): a collection of tools
  * SDumper: dumps the ROM and the BOOT sector of the device.
* [Deark](http://entropymine.com/deark/) to extract and convert images to `.png` from an multibitmap `.mbm` or `.aif`
* [RomBrowser](https://github.com/Florin9doi/rombrowser) by [@Florin9doi](https://github.com/Florin9doi): to display the content of a dump of the rom.
* [E32Explorer](https://github.com/mrRosset/E32Explorer) by [@mrRosset](https://github.com/mrRosset): to read E32Image and partially read TRomImage
* S60 SDK Utilities:
  * `bmconv` to extract images from a multibitmap `.mbm`
  * `petran` to read E32Image
* [FExplorer](http://gosymbian.com) by Dominique Hugo: to explore the filesystem and run `.exe` on S60.

## System Specs

* CPU: [ARM920T](https://en.wikipedia.org/wiki/ARM9#ARM920T) @ 104 MHz
  + ARM9T Technical Reference Manual [PDF](http://www.atmel.com/Images/ARM_920T_TRM.pdf) · [HTML](http://infocenter.arm.com/help/index.jsp?topic=/com.arm.doc.ddi0151c/I1004722.html)
* Memory: 3.4 MB internal memory, MultiMediaCard (MMC) external memory
* OS: [S60](https://en.wikipedia.org/wiki/S60_(software_platform)) 1st Edition, Feature Pack 1 (S60 1.2, or Symbian OS 6.1)
* Display: TFT 176x208 pixels, 4096 colors

## Memory Map

Virtual Address Map:

```
0x0040 0000 - 0x2FFF FFFF  : User Data
0x3000 0000 - 0x3FFF FFFF  : Static data for Java
0x4000 0000 - 0x4000 1FFF  : Super page + CPU page
0x4001 0000 - 0x4001 0FFF  : Shadow RAM page temporary address
0x4100 0000 - 0x4100 3FFF  : Page Directory
0x4108 0000 - 0x4108 3FFF  : Page table info
0x4200 0000 - 0x423F FFFF  : Page tables
0x5000 0000 - 0x57FF FFFF  : ROM image
0x5800 0000 - 0x5EFF FFFF  : Memory-mapped I/O
0x5F00 0000 - 0x5FFF FFFF  : Video RAM
0x6000 0000 - 0x7FFF FFFF  : RAM
0x8000 0000 - 0xXXXX XXXX  : Kernel data/bss section
0xXXXX XXXX - 0xXXXX XXXX  : Reentrant/IRQ/FIQ/Null/Exception kernel stack
0xXXXX XXXX - 0xXXXX XXXX  : Fixed chunks data for ROM fixed processes
0xXXXX XXXX - 0xXXXX XXXX  : Kernel server heap and stack
0xXXXX XXXX - 0xXXXX XXXX  : Home Section / All Processes
0xXXXX XXXX - 0xXXXX XXXX  : RAM-loaded EXE & DLL code
0xFFF0 0000 - 0xFFFE FFFF  : Empty
0xFFFF 0000 - 0xFFFF FFFF  : Vectors
```

## S60

* [S60 version comparison (Wikipedia)](https://en.wikipedia.org/wiki/Symbian#Symbian_.28S60.29_version_comparison)
* [S60 versions and supported devices (Wikipedia)](https://en.wikipedia.org/wiki/S60_(software_platform)#Versions_and_supported_devices)
* [Getting Started with C++ Development on the Series 60 SDK (Web Archive, 2002)](https://web.archive.org/web/20050228053950/http://www.symbian.com/developer/techlib/papers/series60/series60.html)

### SDK

* [S60 SDK 1.2 for Windows](http://urjaman.ddns.net/sissshare/s60-2ndEd-dev/1stEd/nS60_sdk_v1_2.zip). Minimum requirements:
  * [Java 2 Runtime Environment 1.3.1](http://www.oracle.com/technetwork/java/javasebusiness/downloads/java-archive-downloads-javase13-419413.html)
  * [Active Perl 5.1.8](https://sourceforge.net/p/wpbdc/website/ci/2ee71367b1932176847e8f969af85168d94c89f4/tree/Download/ActivePerl-5.6.1.635-MSWin32-x86.msi?format=raw)
  * nmake any version from Visual Studio
 
### IDE

* Carbide C++
* Microsoft Visual C++ 6.0

## File Formats

* .sis [SIS File Format](http://www.thouky.co.uk/sis.html)
* .app [E32Image](http://web.archive.org/web/20141018215857/http://www.antonypranata.com/node/10)
* .mbm [Multibitmap](http://fileformats.archiveteam.org/wiki/EPOC_MBM)
* .aif [Application Information File](http://fileformats.archiveteam.org/wiki/EPOC_AIF)
* .rsc [Resource file](https://www.reviversoft.com/file-extensions/rsc) (compiled from .rss)
* .dll Dynamic-link library
* .txt Plain text file (ASCII encoding)
* .amr Adaptive Multi-Rate codec
* .wav Waveform Audio File Format
* .bin Binary file
* .dat ?
* .cfg ?
* .vpxh ?
* .ngf ?
* .tkmf ?
* .off ?
* .cwa ?

### File formats used by a single game

* .cfl (Alien Front)
* .lib (Alien Front)
* .rle (Asphalt Urban GT 2)
* .sbi (Barakel)
* .gra (Bomberman)
* .snd (Bomberman)
* .s (Call of Duty)
* .ogg (Call of Duty)
* .ent (Call of Duty)
* .msk (Call of Duty)
* .pal (Call of Duty)
* .pth (Call of Duty)
* .sur (Call of Duty)
* .zcp (Call of Duty)
* .zfg (Call of Duty)
* .zlu (Call of Duty)
* .zmp (Call of Duty)
* .zon (Call of Duty)
* .zsk (Call of Duty)
* .ztx (Call of Duty)
* .npk (Catan)
* .gdr (Civilazation)
* .dz (Colin McRae Rally 2005)
* .nax (Colin McRae Rally 2005)
* .gob (Crash Bandicoot)
* .xrl (FIFA 2004)
* .cs (Flo Boarding)
* .cs.tst (Flo Boarding)
* .hdr (Glimmerati)

### Utilities

Use `deark` to extract images from .aif:
```
$ deark file.aif

Module: epocimage
Format: EPOC AIF
Error: Unsupported bits/pixel (1) for grayscale image
Writing output.000.png
Error: Unsupported bits/pixel (1) for grayscale image
Writing output.001.png
```

Use utility `bmconv` from SDK to extract images from .mbm:
```
$ bmconv /v images.mbm

BMCONV version 103.
images.mbm is a File store containing 3 bitmaps

Bitmap 1 information:
Pixel size 176 x 44
Twips size 352 x 88
24 Bpp Colour
24 bit RLE compression 72%

Bitmap 2 information:
Pixel size 176 x 44
Twips size 352 x 88
24 Bpp Colour
24 bit RLE compression 72%

Bitmap 3 information:
Pixel size 176 x 208
Twips size 263 x 311
24 Bpp Colour
24 bit RLE compression 15%

$ bmconv /u images.mbm 1.bmp 2.bmp 3.bmp

BMCONV version 103.
Decompiling...
Epoc file: images.mbm

Bitmap file 1   : 1.bmp
Bitmap file 2   : 2.bmp
Bitmap file 3   : 3.bmp
Success.
```

### E32Image Header

[Source](https://github.com/loociano/symbian-build-tools/blob/master/e32tools/INC/E32IMAGE.H)
```
0x0000 Uid1
0x0004 Uid2
0x0008 Uid3
0x000c Check                // UID checksum
0x0010 Signature
0x0014 Cpu                  // 0x1000 = X86, 0x2000 = ARM, 0x4000 = M*Core
0x0018 CheckSumCode         // sum of all 32 bit words in .text
0x001c CheckSumData         // sum of all 32 bit works in .data
0x0020 Version (minor)
0x0022 Version (major)
0x0024 Timestamp (msb)
0x0028 Timestamp (lsb)
0x002c Flags                // 0 = exe, 1 = dll, +2 = no call entry points
0x0030 CodeSize             // size of code, import address table, constant data and export dir
0x0034 DataSize             // size of initialised data
0x0038 HeapSizeMin
0x003c HeapSizeMax
0x0040 StackSize
0x0044 BssSize
0x0048 EntryPoint           // offset into code of entry point
0x004c CodeBase             // where the code is linked for
0x0050 DataBase             // where the data is linked for
0x0054 DllRefTableCount     // filling this in enables E32ROM to leave space for it
0x0058 ExportDirOffset      // offset into the file of the export address table
0x005c ExportDirCount
0x0060 TextSize             // size of just the text section
0x0064 CodeOffset           // file offset to code section
0x0068 DataOffset           // file offset to data section
0x006c ImportOffset         // file offset to import section
0x0070 CodeRelocOffset      // relocations for code and const
0x0074 DataRelocOffset      // relocations for data
0x0078 Priority             // priority of this process
```

Flags:

```
Bit 28-32: Import format
Bit 24-27: Header format
Bit 8-23: ???
Bit 5-7: Entry point type
Bit 3-4: ABI
Bit 2: Fixed address
Bit 1: Call entry point
Bit 0: Executable type     // 0 = exe, 1 = dll
```

#### UIDs

Symbian OS uses Unique IDentifiers (UID) for identifying components. Each component is identified by three 32-bit UID inte-
gers: UID1, UID2 and UID3.

* UID1: specifies the type of component.
```
0x1000007a = Executable (EXE)
0x10000079 = Library (DLL)
```
* UID2: more specific type of component. It can be zero if UID1 is `EXE`.
* UID3: it is the most specific identifier, must be unique. It can be zero if UID1 is `EXE`.

## Tutorials

* [How to build helloworld on S60](http://n-gage.org/tutorials/how-to-build-helloworld-on-s60.html)
* [Helloworld disassembly](http://n-gage.org/tutorials/helloworld-disassembly.html)
* [How to compile and decompile mbm files](http://n-gage.org/tutorials/how-to-compile-and-decompile-mbm-files.html)
* [How to make a standalone application (using py2sis)](http://www.mobilenin.com/pys60/info_standalone_application.htm)

## References

### Books
* [Jo Stichbury. Symbian OS Explained. Effective C++ programming for Smartphones, 2005](https://books.google.ie/books?id=EyrSpjsIFNAC&lpg=PP1&dq=isbn%3A0470021314&pg=PP1#v=onepage&q&f=false)
* [Jane Sales. Symbian OS Internals. Real-time Kernel Programming, 2005](https://books.google.ie/books?id=AqS5W0MJOI0C&lpg=PP1&dq=isbn%3A0470025255&pg=PP1#v=onepage&q&f=false)

### Symbian
* [Symbian OS v6.1 Edition for C++. Symbian Developer Library](http://n-gage.org/symbian-sdk-doc/6.1/developerlibrary/Product/Generic/index.html)
* [Symbian OS v6.1 Example Code. Symbian Developer Library](http://n-gage.org/symbian-sdk-doc/6.1/examples/Examples/index.html)

### Various authors
* [NGEmu Wiki](https://github.com/NGEmu/NGEmu/wiki)
* [@mrRosset's Symbian Archive](https://mrrosset.github.io/Symbian-Archive/)
* [EPOC32 File formats](http://www.koeniglich.de/epoc32_fileformats.txt)
* [Shub-Nigurrath (Arteam). Primer on Reversing Symbian S60 Applications, 2007](http://185.62.190.110/accessroot/arteam/site/download.php?view.194)

### Wikipedia
* [N-Gage – Wikipedia](https://en.wikipedia.org/wiki/N-Gage_(device))
* [N-Gage QD – Wikipedia](https://en.wikipedia.org/wiki/N-Gage_QD)
* [List of N-Gage games – Wikipedia](https://en.wikipedia.org/wiki/List_of_N-Gage_games)

## Thanks

[@tambry](https://github.com/tambry), [@mrRosset](https://github.com/mrRosset), [THC.org](http://www.thc.org).

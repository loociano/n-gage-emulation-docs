# N-Gage Emulation Docs

![ ](https://github.com/loociano/N-Gage-emu-docs/blob/master/ngage-motherboard.png?raw=true)

## Emulators

* [NGEmu](https://github.com/NGEmu/NGEmu) HLE N-Gage emulator written in C++ for Windows

## System Specs

* CPU: [ARM920T](https://en.wikipedia.org/wiki/ARM9#ARM920T) @ 104 MHz
  + ARM9T Technical Reference Manual [PDF](http://www.atmel.com/Images/ARM_920T_TRM.pdf) · [HTML](http://infocenter.arm.com/help/index.jsp?topic=/com.arm.doc.ddi0151c/I1004722.html)
* Memory: 3.4 MB internal memory, MultiMediaCard (MMC) external memory
* OS: [Series 60](https://en.wikipedia.org/wiki/S60_(software_platform)) 1st Edition, Feature Pack 1 (S60 1.2, or Symbian OS 6.1)
* Display: TFT 176x208 pixels, 4096 colors

## S60

* [Symbian SDKs developers.nokia.com (Web Archive)](http://web.archive.org/web/20141028092534/http://developer.nokia.com/community/wiki/Symbian_C%2B%2B#Symbian_SDKs)
* [Symbian (S60) version comparison (Wikipedia)](https://en.wikipedia.org/wiki/Symbian#Symbian_.28S60.29_version_comparison)
* [S60 Versions and supported devices (Wikipedia)](https://en.wikipedia.org/wiki/S60_(software_platform)#Versions_and_supported_devices)
* [Getting Started with C++ Development on the Series 60 SDK (Web Archive, 2002)](https://web.archive.org/web/20050228053950/http://www.symbian.com/developer/techlib/papers/series60/series60.html)
* [S60 Platform SDKs for Symbian OS, for C++ (Web Archive, 2007)](http://web.archive.org/web/20071022045723/http://www.forum.nokia.com:80/info/sw.nokia.com/id/4a7149a5-95a5-4726-913a-3c6f21eb65a5/S60-SDK-0616-3.0-mr.html)
  + Download links are broken
* [S60 Platform SDKs for Symbian OS, for Java (Web Archive, 2007)](https://web.archive.org/web/20070302194338/http://developer.nokia.com:80/info/sw.nokia.com/id/6e772b17-604b-4081-999c-31f1f0dc2dbb/S60_Platform_SDKs_for_Symbian_OS_for_Java.html)
  + Download links are broken

### Downloads 

* S60 3rd Edition SDK for Symbian OS [S60_3rd_SDK_v1.0.zip](http://www.mediafire.com/file/kc94rnlrrs1wh90/S60_3rd_SDK_v1.0.zip)
* S60 3rd Edition SDK for Symbian OS 9.2, Feature Pack 1, v1.0.1 [s60v3.1_SDK.zip](http://www.mediafire.com/file/9uc7fjb2ynmxlud/s60v3.1_SDK.zip)
* S60 3rd Edition SDK for Symbian OS, Feature Pack 2 v1.1 [S60_SDK_3.2_v1.1.1_en.zip](http://www.mediafire.com/file/p0boxl3gy9opw9u/S60_SDK_3.2_v1.1.1_en.zip)

### Building a S60 Application on Windows

Check that `devices` and `epoc` commands are working.

Build:

```
cd C:\Symbian\9.1\S60_3rd\S60Ex\helloworldbasic\group
bldmake bldfiles
abld build
epoc
```

## ROM disassembly

```
.sis = Application Installation file
  .app = Application
  .rsc = Resource binary
  .aif = Icon bitmaps
```

### ROM Header

_Extracted from NGEmu_

```
0x0000 UID1
0x0004 UID2
0x0008 UID3
0x000c UID checksum
0x0010 Signature
0x0014 CPU
0x0018 Code checksum
0x001c Data checksum
0x0020 Build (minor)
0x0022 Build (major)
0x0024 Timestamp (msb)
0x0028 Timestamp (lsb)
0x002c Flags
0x0030 Code size
0x0034 Data size
0x0038 Heap minimum size
0x003c Heap maximum size
0x0040 Stack size
0x0044 BSS size
0x0048 Entry point offset
0x004c Code base address
0x0050 Data base address
0x0054 DLL count
0x0058 Export offset
0x005c Export count
0x0060 Text size
0x0064 Code offset
0x0068 Data offset
0x006c Import offset
0x0070 Code relocation offset
0x0074 Data relocation offset
0x007c Priority 
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
Bit 0: Executable type
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

## References

* [N-Gage (device) - Wikipedia](https://en.wikipedia.org/wiki/N-Gage_(device))
* [N-Gage QD - Wikipedia](https://en.wikipedia.org/wiki/N-Gage_QD)
* [Symbian Development - Mediafire repo by "freaxs_r_us"](https://www.mediafire.com/folder/79jhy594xb3uk/Symbian_Development)

---
title: How to build helloworld on S60
---

# How to build helloworld on S60

## Prerequisites

Install the [S60 SDK](http://urjaman.ddns.net/sissshare/s60-2ndEd-dev/1stEd/nS60_sdk_v1_2.zip), [Java 1.3.1](http://www.oracle.com/technetwork/java/javasebusiness/downloads/java-archive-downloads-javase13-419413.html), Visual C++ and [Active Perl 5.1.8](https://sourceforge.net/p/wpbdc/website/ci/2ee71367b1932176847e8f969af85168d94c89f4/tree/Download/ActivePerl-5.6.1.635-MSWin32-x86.msi?format=raw). Verify that `perl`, `java`, `nmake` and `epoc` commands are working.

```
$ perl -version
$ java -version
$ nmake /HELP
$ epoc
```

## Build for the S60 Windows simulator

1. Go to the `group` directory
```
$ cd C:\Symbian\6.1\Series60\Series60Ex\helloworld\group
```
2. Generate MAKE files. This will create MAKE files for all supported targets under `${EPOCROOT}\Epoc32\BUILD\SYMBIAN\6.1\SERIES60\SERIES60EX\HELLOWORLD\GROUP`
```
$ bldmake bldfiles
```
3. Build
```
$ abld build
```
4. Run the emulator. The application should be automatically installed
```
$ epoc
```
![](https://raw.githubusercontent.com/loociano/N-Gage-emu-docs/master/img/helloworld-emulator-1.png)
![](https://raw.githubusercontent.com/loociano/N-Gage-emu-docs/master/img/helloworld-emulator-2.png)

## Build for the actual device

```
$ cd C:\Symbian\6.1\Series60\Series60Ex\helloworld\group
$ bldmake bldfiles
$ abld build armi urel
$ cd ..\
$ makesis helloworld.pkg
```

## References

1. [How to use the Symbian build process. Symbian Developer Library](http://n-gage.org/symbian-sdk-doc/6.1/developerlibrary/Common/ToolsAndUtilities/Build/HowtoBuildProcess.guide.html#PracticalGuide%2eHowtoBuildProcess)
2. [How to use bldmake. Symbian Developer Library](http://n-gage.org/symbian-sdk-doc/6.1/developerlibrary/Common/ToolsAndUtilities/Build/UsingBldmake.guide.html#PracticalGuide%2eusing%2dbldmake)
3. [How to use abld. Symbian Developer Library](http://n-gage.org/symbian-sdk-doc/6.1/developerlibrary/Common/ToolsAndUtilities/Build/UsingAbld.guide.html#PracticalGuide%2eusing%2dabld)
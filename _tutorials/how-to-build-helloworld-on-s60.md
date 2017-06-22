---
title: How to build helloworld on S60
---

# How to build helloworld on S60

## Prerequisites

Check that `perl`, `java`, `nmake` and `epoc` commands are working.
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
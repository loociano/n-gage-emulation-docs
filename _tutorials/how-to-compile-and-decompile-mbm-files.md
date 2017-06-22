---
title: How to compile and decompile mbm files
---
# How to compile and decompile mbm files
_Unknown author_

## Decompile

To decompile the mbm files place `bmconv.exe` into the directory with the .mbm file in and type:

```
bmconv /v filename.mbm
```

This produces information on how many bitmaps are stored in there, there colour settings, pixel sizes and compression rates.
Obviously when creating the text files (create and extract) in the next part match the amount of bitmaps to the amount stated when running the `bmconv /v filename.mbm` utility.

In this instance, for the `irRemote.mbm` file, we need to decompile the individual bitmaps for editing to do this we create a text file called `extract.txt` with the following text in:

```
/u irRemote.mbm

bitmap1.bmp
bitmap2.bmp
bitmap3.bmp
bitmap4.bmp
bitmap5.bmp
bitmap6.bmp
bitmap7.bmp
bitmap8.bmp
bitmap9.bmp
bitmap10.bmp
bitmap11.bmp
bitmap12.bmp
bitmap13.bmp
bitmap14.bmp
```

Save this `extract.txt` file in the directory where the `bmconv.exe` and the `irRemote.mbm` file is. At the command prompt type `bmconv extract.txt`, this will then create 14 Bitmaps for editing!

Edit the bitmaps that you want to, you must keep to the pixel sizes and files sizes previously used.

## Compile

To recompile into a mbm file, create a text file called "create.txt" and put the following text in:

```
irRemote.mbm

/c12bitmap1.bmp
/c12bitmap2.bmp
/c12bitmap3.bmp
/c12bitmap4.bmp
/c12bitmap5.bmp
/c12bitmap6.bmp
/c12bitmap7.bmp
/c12bitmap8.bmp
/c12bitmap9.bmp
/c12bitmap10.bmp
/c12bitmap11.bmp
/c12bitmap12.bmp
/c12bitmap13.bmp
/c12bitmap14.bmp
```

Note: the `/c12` setting means that the bmp files will be compressed to 4096 colours, the same as used on the Nokia 7650 screen.

Then go to the command prompt and type `bmconv create.txt` and you will have a new file with edited .bmps compiled into a `irRemote.mbm` file.
---
title: Helloworld disassembly
---

# Helloworld disassembly

Source code:
```
#include <stdio.h>

int main (int argc, char *argv[]) {
  argc=0;
  argv=NULL;
  printf("Hello World\n");
  return 0;
}
```

`helloworld` imports these functions from the following two libraries:

* `estlib.dll`
  + 73 `printf`
  + 104 `exit` (implicit)
  + 262 `_crt0__FRiRPPcT1` (implicit)
* `euser.dll`
  + 746 `New__12CTrapCleanup` (implicit)

Compiled E32ImageFile, explained:
```
Header: from 0 to 0x7c (code offset)

7a00 0010 = Uid1 (0x1000007a)
0000 0000 = Uid2 (0)
0000 0000 = Uid3 (0)
9ec3 5a04 = iCheck (0x5a04c39e)
4550 4f43 = Signature, 'EPOC' in ASCII
0020 0000 = ARM CPU (0x2000)
b1ed 6d24 = Checksum code (0x246dedb1)
0000 0000 = Checksum data (0)
0100 af00 = PETRAN version (Build=0xaf Minor=0, Mayor=1 = Version 1 Build 175)
4033 5cb3 9630 e200 = timestamp (0xe23096 0xb35c3340)
0200 0000 = Flags (0x2 = no call of entry points)
9001 0000 = Code size (0x190)
0000 0000 = Data Size (0)
0010 0000 = Heap size min (0x1000)
0000 1000 = Heap size max (0x100000)
0020 0000 = Stack size (0x2000)
0000 0000 = Bss size (0)
0000 0000 = Entry point (0)
0000 4000 = Code link offset (0x400000)
0000 0000 = Data link offset (0)
0200 0000 = DllRefTableCount = 2 dlls
0000 0000 = Export address table offset (0)
0000 0000 = Export dir count (0)
7c01 0000 = Text size (0x17c)
7c00 0000 = Code offset (0x7c)
0000 0000 = Data offset (0)
0c02 0000 = Import offset (0x20c)
5c02 0000 = Code relocation offset (0x25c)
0000 0000 = Data relocation offset (0)
5e01 0000 = Priority (0x15e = EPriorityForeground)

Code: from 0x7c (code offset) to 0x20c (import offset). 0x20c-0x7c = 0x190 (code size)

7040 2de9 0140 a0e3 8420 9fe5 0431 a0e1 0310 a0e1 0330 92e7 0000 53e3 0800 000a
0250 a0e1 0140 84e2 01c0 95e7 0fe0 a0e1 1cff 2fe1 0411 a0e1 0130 95e7 0000 53e3
f7ff ff1a 1f00 00eb 0060 a0e1 0140 a0e3 4020 9fe5 0431 a0e1 0310 a0e1 0330 92e7
0000 53e3 0800 000a 0250 a0e1 0140 84e2 01c0 95e7 0fe0 a0e1 1cff 2fe1 0411 a0e1
0130 95e7 0000 53e3 f7ff ff1a 0600 a0e1 0100 00ea 5c01 4000 6401 4000 7040 bde8
1eff 2fe1 1eff 2fe1 0040 2de9 1800 00eb 0c00 9fe5 1800 00eb 0000 a0e3 0010 bde8
1cff 2fe1 6c01 4000 0040 2de9 0cd0 4de2 1d00 00eb 0030 a0e3 0830 8de5 0430 8de5
0030 8de5 0800 8de2 0410 8de2 0d20 a0e1 0d00 00eb 0800 9de5 0410 9de5 0020 9de5
e8ff ffeb 0c00 00eb 0cd0 8de2 0040 bde8 1eff 2fe1 1eff 2fe1 b8ff ffea 04c0 9fe5
00c0 9ce5 1cff 2fe1 7c01 4000 04c0 9fe5 00c0 9ce5 1cff 2fe1 8401 4000 04c0 9fe5
00c0 9ce5 1cff 2fe1 8001 4000 04c0 9fe5 00c0 9ce5 1cff 2fe1 8801 4000 ffff ffff
0000 0000 ffff ffff 0000 0000 4865 6c6c 6f20 576f 726c 640a 0000 0000 4900 0000
6800 0000 0601 0000 ea02 0000 0000 0000

Imports: from 0x20c (import offset) to 0x25c (code relocation offset) = 0x25c-0x20c=0x50

5000 0000 = import size 0x50
2400 0000 = offset of dll name 0x24 = 36 bytes
0300 0000 = number of imports
4900 0000 = import1 0x49
6800 0000 = import2 0x68
0601 0000 = import3 0x106
3900 0000 = offset of dll name 0x39 = 57 bytes
0100 0000 = number of imports
ea02 0000 = import1 0x2ea
4553 544c 4942 5b31 3030 3033 6230 625d 2e44 4c4c 0045 5553 4552 5b31 3030 3033
3965 355d 2e44 4c4c 0000 0000 = library names in ASCII: “ESTLIB[10003b0b].DLL EUSER[100039e5].DLL”

Code Relocation: from 0x25c (relocation offset) to 0x27b (file end). 0x27b-0x25c=0x1f

1800 0000 = Size of the relocation section 0x18 = 24 bytes
0700 0000 = number of relocs 7
0000 = ignore
0000 = ignore
1800 = ignore
0000 = ignore
9430 = rec1 0x94
9830 = rec2 0x98
c430 = rec3 0xc4
2831 = rec4 0x128
3831 = rec5 0x138
4831 = rec6 0x148
5831 = rec7 0x158
0000 = ignore
```

PETRAN analysis:
```
petran HELLO.EXE

PETRAN - PE file preprocessor V01.00 (Build 175)
Copyright (c) 1996-2001 Symbian Ltd.

E32ImageFile 'HELLO.EXE'
V1.00(175)      Time Stamp: 00e23096,b35c3340
EPOC Exe for ARM CPU
Priority Foreground
Entry points are not called
Uids:           1000007a 00000000 00000000 (045ac39e)
File Size:      0000027c
Code Size:      00000190
Data Size:      00000000
Chk code/data:  246dedb1/00000000
Min Heap Size:  00001000
Max Heap Size:  00100000
Stack Size:     00002000
Code link addr: 00400000
Data link addr: 00000000
Code reloc offset:      0000025c
Data reloc offset:      00000000
Dll ref table count: 2
        Offset  Size    Relocs  NumOfRelocs
Code    00007c  000190  00025c  000007          +000000 (entry pnt)
Data    000000  000000
Bss             000000
Import  00020c

Code (text size=0000017c)
000000: e92d4070 e3a04001 e59f2084 e1a03104 e1a01003 e7923003 e3530000 0a000008
000020: e1a05002 e2844001 e795c001 e1a0e00f e12fff1c e1a01104 e7953001 e3530000
000040: 1afffff7 eb00001f e1a06000 e3a04001 e59f2040 e1a03104 e1a01003 e7923003
000060: e3530000 0a000008 e1a05002 e2844001 e795c001 e1a0e00f e12fff1c e1a01104
000080: e7953001 e3530000 1afffff7 e1a00006 ea000001 0040015c 00400164 e8bd4070
0000a0: e12fff1e e12fff1e e92d4000 eb000018 e59f000c eb000018 e3a00000 e8bd1000
0000c0: e12fff1c 0040016c e92d4000 e24dd00c eb00001d e3a03000 e58d3008 e58d3004
0000e0: e58d3000 e28d0008 e28d1004 e1a0200d eb00000d e59d0008 e59d1004 e59d2000
000100: ebffffe8 eb00000c e28dd00c e8bd4000 e12fff1e e12fff1e eaffffb8 e59fc004
000120: e59cc000 e12fff1c 0040017c e59fc004 e59cc000 e12fff1c 00400184 e59fc004
000140: e59cc000 e12fff1c 00400180 e59fc004 e59cc000 e12fff1c 00400188 ffffffff
000160: 00000000 ffffffff 00000000 6c6c6548 6f57206f 0a646c72 00000000 00000049
000180: 00000068 00000106 000002ea 00000000
7 relocs
00000094 00000098 000000c4 00000128 00000138 00000148 00000158

Idata   Size=00000050
Offset of import address table (relative to code section): 0000017c
3 imports from ESTLIB[10003b0b].DLL
        73
        104
        262
1 imports from EUSER[100039e5].DLL
        746
```

IDA Pro disassembly:

```
    EXPORT start
start
    STMFD SP!, {R4-R6,LR}
    MOV R4, #1
    LDR R2, =dword_40015C
    MOV R3, R4,LSL#2
    MOV R1, R3
    LDR R3, [R2,R3]
    CMP R3, #0
    BEQ loc_400044
    MOV R5, R2

loc_400024
    ADD R4, R4, #1
    LDR R12, [R5,R1]
    MOV LR, PC
    BX  R12
    MOV R1, R4,LSL#2
    LDR R3, [R5,R1]
    CMP R3, #0
    BNE loc_400024

loc_400044
    BL  sub_4000C8
    MOV R6, R0
    MOV R4, #1
    LDR R2, =dword_400164
    MOV R3, R4,LSL#2
    MOV R1, R3
    LDR R3, [R2,R3]
    CMP R3, #0
    BEQ loc_40008C
    MOV R5, R2

loc_40006C
    ADD R4, R4, #1
    LDR R12, [R5,R1]
    MOV LR, PC
    BX  R12
    MOV R1, R4,LSL#2
    LDR R3, [R5,R1]
    CMP R3, #0
    BNE loc_40006C

loc_40008C
    MOV R0, R6
    B loc_40009C
; ---------------------------------------------------------------------------
off_400094  DCD dword_40015C
off_400098  DCD dword_400164
; ---------------------------------------------------------------------------

loc_40009C
    LDMFD SP!, {R4-R6,LR}
    BX  LR
; End of function start

; ---------------------------------------------------------------------------
    BX  LR

; =============== S U B R O U T I N E =======================================

sub_4000A8
    STMFD SP!, {LR}
    BL  nullsub_1
    LDR R0, =aHelloWorld ; "Hello World\n"
    BL  j_aI
    MOV R0, #0
    LDMFD SP!, {R12}
    BX  R12
; End of function sub_4000A8

; ---------------------------------------------------------------------------
off_4000C4  DCD aHelloWorld
          ; "Hello World\n"

; =============== S U B R O U T I N E =======================================

sub_4000C8

var_10    = -0x10
var_C   = -0xC
var_8   = -8

    STMFD SP!, {LR}
    SUB SP, SP, #0xC
    BL  sub_40014C
    MOV R3, #0
    STR R3, [SP,#0x10+var_8]
    STR R3, [SP,#0x10+var_C]
    STR R3, [SP,#0x10+var_10]
    ADD R0, SP, #0x10+var_8
    ADD R1, SP, #0x10+var_C
    MOV R2, SP
    BL  sub_40012C
    LDR R0, [SP,#0x10+var_8]
    LDR R1, [SP,#0x10+var_C]
    LDR R2, [SP,#0x10+var_10]
    BL  sub_4000A8
    BL  j_aH
    ADD SP, SP, #0xC
    LDMFD SP!, {LR}
    BX  LR
; End of function sub_4000C8

; =============== S U B R O U T I N E =======================================

nullsub_1
    BX  LR
; End of function nullsub_1

; ---------------------------------------------------------------------------
    B start

; =============== S U B R O U T I N E =======================================

; Attributes: thunk

j_aI
    LDR R12, =aI  ; "I"
    LDR R12, [R12]  ; "I"
    BX  R12
; End of function j_aI

; ---------------------------------------------------------------------------
off_400128  DCD aI     ; "I"

; =============== S U B R O U T I N E =======================================

; Attributes: thunk

sub_40012C
    LDR R12, =off_400184
    LDR R12, [R12]
    BX  R12
; End of function sub_40012C

; ---------------------------------------------------------------------------
off_400138  DCD off_400184

; =============== S U B R O U T I N E =======================================

; Attributes: thunk

j_aH
    LDR R12, =aH  ; "h"
    LDR R12, [R12]  ; "h"
    BX  R12
; End of function j_aH

; ---------------------------------------------------------------------------
off_400148  DCD aH      ; "h"

; =============== S U B R O U T I N E =======================================

; Attributes: thunk

sub_40014C
    LDR R12, =off_400188
    LDR R12, [R12]
    BX  R12
; End of function sub_40014C

; ---------------------------------------------------------------------------
off_400158  DCD off_400188
dword_40015C  DCD 0xFFFFFFFF, 0
dword_400164  DCD 0xFFFFFFFF, 0
aHelloWorld DCB "Hello World",0xA,0
    DCB 0, 0, 0
;
; Imports from ESTLIB[10003b0b].DLL
;
aI    DCB "I",0
    DCW 0
aH    DCB "h",0
    DCW 0
off_400184  DCD 0x106
;
; Imports from EUSER[100039e5].DLL
;
off_400188  DCD 0x2EA
    ALIGN 0x10
; .text   ends

    END start
```


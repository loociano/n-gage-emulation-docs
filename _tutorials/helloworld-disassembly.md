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

Petran analysis:
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


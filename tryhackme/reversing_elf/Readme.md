# crackme1
```
root@kali:~# ./crackme1
xxxxx
```

# crackme2
```
root@kali:~# ./crackme2
Usage: ./crackme2 password
root@kali:~# strings crackme2
/lib/ld-linux.so.2
libc.so.6
_IO_stdin_used
puts
printf
memset
strcmp
__libc_start_main
/usr/local/lib:$ORIGIN
__gmon_start__
GLIBC_2.0
PTRh
j3jA
[^_]
UWVS
t$,U
[^_]
Usage: %s password
super_XXXXXXXXXXXXXXX
Access denied.
Access granted.

```

```
root@kali:~# ./crackme2 super_secret_password
Access granted.
XXXXXXXXXXXXXX
```

# crackme3
```
root@kali:~# strings crackme3
/lib/ld-linux.so.2
__gmon_start__
libc.so.6
_IO_stdin_used
puts
strlen
malloc
stderr
fwrite
fprintf
strcmp
__libc_start_main
GLIBC_2.0
PTRh
iD$$
D$,;D$
UWVS
[^_]
Usage: %s PASSWORD
malloc failed
XXXXXXXXXXXXXXXXXXXXX
Correct password!
```

```
root@kali:~# echo "XXXXXX=="| base64 -d
XXXXXX@kali:~# ./crackme3  XXXXXX
Correct password!
root@kali:~#
```

# crackme4
```
[0x7f59496df090]> pdf @sym.compare_pwd
/ (fcn) sym.compare_pwd 156
|   sym.compare_pwd (int32_t arg1);
|           ; var int32_t var_28h @ rbp-0x28
|           ; var int32_t var_20h @ rbp-0x20
|           ; var int32_t var_18h @ rbp-0x18
|           ; var int32_t var_10h @ rbp-0x10
|           ; var int32_t var_eh @ rbp-0xe
|           ; var int32_t var_8h @ rbp-0x8
|           ; arg int32_t arg1 @ rdi
|           ; CALL XREF from main @ 0x400754
|           0x0040067a      55             push rbp
|           0x0040067b      4889e5         mov rbp, rsp
|           0x0040067e      4883ec30       sub rsp, 0x30
|           0x00400682      48897dd8       mov qword [var_28h], rdi    ; arg1
|           0x00400686      64488b042528.  mov rax, qword fs:[0x28]
|           0x0040068f      488945f8       mov qword [var_8h], rax
|           0x00400693      31c0           xor eax, eax
|           0x00400695      48b8495d7b49.  movabs rax, 0x7b175614497b5d49
|           0x0040069f      488945e0       mov qword [var_20h], rax
|           0x004006a3      48b857414751.  movabs rax, 0x547b175651474157
|           0x004006ad      488945e8       mov qword [var_18h], rax
|           0x004006b1      66c745f05340   mov word [var_10h], 0x4053  ; 'S@'
|           0x004006b7      c645f200       mov byte [var_eh], 0
|           0x004006bb      488d45e0       lea rax, qword [var_20h]
|           0x004006bf      4889c7         mov rdi, rax
|           0x004006c2      e866ffffff     call sym.get_pwd
|           0x004006c7      488b55d8       mov rdx, qword [var_28h]
|           0x004006cb      488d45e0       lea rax, qword [var_20h]
|           0x004006cf      4889d6         mov rsi, rdx
|           0x004006d2      4889c7         mov rdi, rax
|           0x004006d5      e846feffff     call sym.imp.strcmp         ; int strcmp(const char *s1, const char *s2)
|           0x004006da      85c0           test eax, eax
|       ,=< 0x004006dc      750c           jne 0x4006ea
|       |   0x004006de      bfe8074000     mov edi, str.password_OK    ; 0x4007e8 ; "password OK"
|       |   0x004006e3      e8f8fdffff     call sym.imp.puts           ; int puts(const char *s)
|      ,==< 0x004006e8      eb16           jmp 0x400700
|      |`-> 0x004006ea      488b45d8       mov rax, qword [var_28h]
|      |    0x004006ee      4889c6         mov rsi, rax
|      |    0x004006f1      bff4074000     mov edi, str.password___s__not_OK ; 0x4007f4 ; "password \"%s\" not OK\n"
|      |    0x004006f6      b800000000     mov eax, 0
|      |    0x004006fb      e800feffff     call sym.imp.printf         ; int printf(const char *format)
|      |    ; CODE XREF from sym.compare_pwd @ 0x4006e8
|      `--> 0x00400700      488b45f8       mov rax, qword [var_8h]
|           0x00400704      644833042528.  xor rax, qword fs:[0x28]
|       ,=< 0x0040070d      7405           je 0x400714
|       |   0x0040070f      e8dcfdffff     call sym.imp.__stack_chk_fail ; void __stack_chk_fail(void)
|       `-> 0x00400714      c9             leave
\           0x00400715      c3             ret
[0x7f59496df090]> db 0x004006d2
```

```
[0x7f59496df090]> dc
hit breakpoint at: 4006d2
```

```
[0x004006d2]> pdf @sym.compare_pwd
/ (fcn) sym.compare_pwd 156
|   sym.compare_pwd (int32_t arg1);
|           ; var int32_t var_28h @ rbp-0x28
|           ; var int32_t var_20h @ rbp-0x20
|           ; var int32_t var_18h @ rbp-0x18
|           ; var int32_t var_10h @ rbp-0x10
|           ; var int32_t var_eh @ rbp-0xe
|           ; var int32_t var_8h @ rbp-0x8
|           ; arg int32_t arg1 @ rdi
|           ; CALL XREF from main @ 0x400754
|           0x0040067a      55             push rbp
|           0x0040067b      4889e5         mov rbp, rsp
|           0x0040067e      4883ec30       sub rsp, 0x30
|           0x00400682      48897dd8       mov qword [var_28h], rdi    ; arg1
|           0x00400686      64488b042528.  mov rax, qword fs:[0x28]
|           0x0040068f      488945f8       mov qword [var_8h], rax
|           0x00400693      31c0           xor eax, eax
|           0x00400695      48b8495d7b49.  movabs rax, 0x7b175614497b5d49
|           0x0040069f      488945e0       mov qword [var_20h], rax
|           0x004006a3      48b857414751.  movabs rax, 0x547b175651474157
|           0x004006ad      488945e8       mov qword [var_18h], rax
|           0x004006b1      66c745f05340   mov word [var_10h], 0x4053  ; 'S@'
|           0x004006b7      c645f200       mov byte [var_eh], 0
|           0x004006bb      488d45e0       lea rax, qword [var_20h]
|           0x004006bf      4889c7         mov rdi, rax
|           0x004006c2      e866ffffff     call sym.get_pwd
|           0x004006c7      488b55d8       mov rdx, qword [var_28h]
|           0x004006cb      488d45e0       lea rax, qword [var_20h]
|           0x004006cf      4889d6         mov rsi, rdx
|           ;-- rip:
|           0x004006d2 b    4889c7         mov rdi, rax
|           0x004006d5      e846feffff     call sym.imp.strcmp         ; int strcmp(const char *s1, const char *s2)
|           0x004006da      85c0           test eax, eax
|       ,=< 0x004006dc      750c           jne 0x4006ea
|       |   0x004006de      bfe8074000     mov edi, str.password_OK    ; 0x4007e8 ; "password OK"
|       |   0x004006e3      e8f8fdffff     call sym.imp.puts           ; int puts(const char *s)
|      ,==< 0x004006e8      eb16           jmp 0x400700
|      |`-> 0x004006ea      488b45d8       mov rax, qword [var_28h]
|      |    0x004006ee      4889c6         mov rsi, rax
|      |    0x004006f1      bff4074000     mov edi, str.password___s__not_OK ; 0x4007f4 ; "password \"%s\" not OK\n"
|      |    0x004006f6      b800000000     mov eax, 0
|      |    0x004006fb      e800feffff     call sym.imp.printf         ; int printf(const char *format)
|      |    ; CODE XREF from sym.compare_pwd @ 0x4006e8
|      `--> 0x00400700      488b45f8       mov rax, qword [var_8h]
|           0x00400704      644833042528.  xor rax, qword fs:[0x28]
|       ,=< 0x0040070d      7405           je 0x400714
|       |   0x0040070f      e8dcfdffff     call sym.imp.__stack_chk_fail ; void __stack_chk_fail(void)
|       `-> 0x00400714      c9             leave
\           0x00400715      c3             ret
```
```
[0x004006d2]> dr
rax = 0x7ffefbac53d0
rbx = 0x00000000
rcx = 0x00000011
rdx = 0x7ffefbac5e08
r8 = 0x7f59496c2a50
r9 = 0x7f59496ed780
r10 = 0xfffffffffffff11e
r11 = 0x7f594952dad0
r12 = 0x00400540
r13 = 0x7ffefbac54f0
r14 = 0x00000000
r15 = 0x00000000
rsi = 0x7ffefbac5e08
rdi = 0x7ffefbac53d0
rsp = 0x7ffefbac53c0
rbp = 0x7ffefbac53f0
rip = 0x004006d2
rflags = 0x00000246
orax = 0xffffffffffffffff
```
```
[0x004006d2]> px @ 0x7ffefbac53d0
- offset -       0 1  2 3  4 5  6 7  8 9  A B  C D  E F  0123456789ABCDEF
0x7ffefbac53d0  XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX
0x7ffefbac53e0  XXXX 0000 0000 0000 009e 765e 8e1e 8901  XX........v^....
0x7ffefbac53f0  1054 acfb fe7f 0000 5907 4000 0000 0000  .T......Y.@.....
0x7ffefbac5400  f854 acfb fe7f 0000 0000 0000 0200 0000  .T..............
0x7ffefbac5410  6007 4000 0000 0000 bbdb 5249 597f 0000  `.@.......RIY...
0x7ffefbac5420  0000 0000 0000 0000 f854 acfb fe7f 0000  .........T......
0x7ffefbac5430  0000 0000 0200 0000 1607 4000 0000 0000  ..........@.....
0x7ffefbac5440  0000 0000 0000 0000 f5cf 32ce e531 d2d3  ..........2..1..
0x7ffefbac5450  4005 4000 0000 0000 f054 acfb fe7f 0000  @.@......T......
0x7ffefbac5460  0000 0000 0000 0000 0000 0000 0000 0000  ................
0x7ffefbac5470  f5cf b268 3dc6 2f2c f5cf 1476 c0a3 602d  ...h=./,...v..`-
0x7ffefbac5480  0000 0000 0000 0000 0000 0000 0000 0000  ................
0x7ffefbac5490  0000 0000 0000 0000 0000 0000 0000 0000  ................
0x7ffefbac54a0  0000 0000 0000 0000 0000 0000 0000 0000  ................
0x7ffefbac54b0  0000 0000 0000 0000 0000 0000 0000 0000  ................
0x7ffefbac54c0  4005 4000 0000 0000 f054 acfb fe7f 0000  @.@......T......
[0x004006d2]>
```

# crackme5
```
[0x7f4470e39090]> db 0x0040082c
[0x7f4470e39090]> dc
Enter your input:
test
hit breakpoint at: 40082c
[0x0040082c]> pdf @main
/ (fcn) main 251
|   int main (int argc, char **argv, char **envp);
|           ; var int32_t var_70h @ rbp-0x70
|           ; var int32_t var_64h @ rbp-0x64
|           ; var int32_t var_54h @ rbp-0x54
|           ; var int32_t var_50h @ rbp-0x50
|           ; var int32_t var_30h @ rbp-0x30
|           ; var int32_t var_2fh @ rbp-0x2f
|           ; var int32_t var_2eh @ rbp-0x2e
|           ; var int32_t var_2dh @ rbp-0x2d
|           ; var int32_t var_2ch @ rbp-0x2c
|           ; var int32_t var_2bh @ rbp-0x2b
|           ; var int32_t var_2ah @ rbp-0x2a
|           ; var int32_t var_29h @ rbp-0x29
|           ; var int32_t var_28h @ rbp-0x28
|           ; var int32_t var_27h @ rbp-0x27
|           ; var int32_t var_26h @ rbp-0x26
|           ; var int32_t var_25h @ rbp-0x25
|           ; var int32_t var_24h @ rbp-0x24
|           ; var int32_t var_23h @ rbp-0x23
|           ; var int32_t var_22h @ rbp-0x22
|           ; var int32_t var_21h @ rbp-0x21
|           ; var int32_t var_20h @ rbp-0x20
|           ; var int32_t var_1fh @ rbp-0x1f
|           ; var int32_t var_1eh @ rbp-0x1e
|           ; var int32_t var_1dh @ rbp-0x1d
|           ; var int32_t var_1ch @ rbp-0x1c
|           ; var int32_t var_1bh @ rbp-0x1b
|           ; var int32_t var_1ah @ rbp-0x1a
|           ; var int32_t var_19h @ rbp-0x19
|           ; var int32_t var_18h @ rbp-0x18
|           ; var int32_t var_17h @ rbp-0x17
|           ; var int32_t var_16h @ rbp-0x16
|           ; var int32_t var_15h @ rbp-0x15
|           ; var int32_t var_8h @ rbp-0x8
|           ; arg int argc @ rdi
|           ; arg char **argv @ rsi
|           ; DATA XREF from entry0 @ 0x4005fd
|           ; CALL XREF from sym.check @ 0x4008c3
|           0x00400773      55             push rbp
|           0x00400774      4889e5         mov rbp, rsp
|           0x00400777      4883ec70       sub rsp, 0x70
|           0x0040077b      897d9c         mov dword [var_64h], edi    ; argc
|           0x0040077e      48897590       mov qword [var_70h], rsi    ; argv
|           0x00400782      64488b042528.  mov rax, qword fs:[0x28]
|           0x0040078b      488945f8       mov qword [var_8h], rax
|           0x0040078f      31c0           xor eax, eax
|           0x00400791      c645d04f       mov byte [var_30h], 0x4f    ; 'O' ; 79
|           0x00400795      c645d166       mov byte [var_2fh], 0x66    ; 'f' ; 102
|           0x00400799      c645d264       mov byte [var_2eh], 0x64    ; 'd' ; 100
|           0x0040079d      c645d36c       mov byte [var_2dh], 0x6c    ; 'l' ; 108
|           0x004007a1      c645d444       mov byte [var_2ch], 0x44    ; 'D' ; 68
|           0x004007a5      c645d553       mov byte [var_2bh], 0x53    ; 'S' ; 83
|           0x004007a9      c645d641       mov byte [var_2ah], 0x41    ; 'A' ; 65
|           0x004007ad      c645d77c       mov byte [var_29h], 0x7c    ; '|' ; 124
|           0x004007b1      c645d833       mov byte [var_28h], 0x33    ; '3' ; 51
|           0x004007b5      c645d974       mov byte [var_27h], 0x74    ; 't' ; 116
|           0x004007b9      c645da58       mov byte [var_26h], 0x58    ; 'X' ; 88
|           0x004007bd      c645db62       mov byte [var_25h], 0x62    ; 'b' ; 98
|           0x004007c1      c645dc33       mov byte [var_24h], 0x33    ; '3' ; 51
|           0x004007c5      c645dd32       mov byte [var_23h], 0x32    ; '2' ; 50
|           0x004007c9      c645de7e       mov byte [var_22h], 0x7e    ; '~' ; 126
|           0x004007cd      c645df58       mov byte [var_21h], 0x58    ; 'X' ; 88
|           0x004007d1      c645e033       mov byte [var_20h], 0x33    ; '3' ; 51
|           0x004007d5      c645e174       mov byte [var_1fh], 0x74    ; 't' ; 116
|           0x004007d9      c645e258       mov byte [var_1eh], 0x58    ; 'X' ; 88
|           0x004007dd      c645e340       mov byte [var_1dh], 0x40    ; '@' ; 64
|           0x004007e1      c645e473       mov byte [var_1ch], 0x73    ; 's' ; 115
|           0x004007e5      c645e558       mov byte [var_1bh], 0x58    ; 'X' ; 88
|           0x004007e9      c645e660       mov byte [var_1ah], 0x60    ; '`' ; 96
|           0x004007ed      c645e734       mov byte [var_19h], 0x34    ; '4' ; 52
|           0x004007f1      c645e874       mov byte [var_18h], 0x74    ; 't' ; 116
|           0x004007f5      c645e958       mov byte [var_17h], 0x58    ; 'X' ; 88
|           0x004007f9      c645ea74       mov byte [var_16h], 0x74    ; 't' ; 116
|           0x004007fd      c645eb7a       mov byte [var_15h], 0x7a    ; 'z' ; 122
|           0x00400801      bf54094000     mov edi, str.Enter_your_input: ; 0x400954 ; "Enter your input:"
|           0x00400806      e865fdffff     call sym.imp.puts           ; int puts(const char *s)
|           0x0040080b      488d45b0       lea rax, qword [var_50h]
|           0x0040080f      4889c6         mov rsi, rax
|           0x00400812      bf66094000     mov edi, 0x400966
|           0x00400817      b800000000     mov eax, 0
|           0x0040081c      e89ffdffff     call sym.imp.__isoc99_scanf ; int scanf(const char *format)
|           0x00400821      488d55d0       lea rdx, qword [var_30h]
|           0x00400825      488d45b0       lea rax, qword [var_50h]
|           0x00400829      4889d6         mov rsi, rdx
|           ;-- rip:
|           0x0040082c b    4889c7         mov rdi, rax
|           0x0040082f      e8a2feffff     call sym.strcmp             ; int strcmp(const char *s1, const char *s2)
|           0x00400834      8945ac         mov dword [var_54h], eax
|           0x00400837      837dac00       cmp dword [var_54h], 0
|       ,=< 0x0040083b      750c           jne 0x400849
|       |   0x0040083d      bf69094000     mov edi, str.Good_game      ; 0x400969 ; "Good game"
|       |   0x00400842      e829fdffff     call sym.imp.puts           ; int puts(const char *s)
|      ,==< 0x00400847      eb0a           jmp 0x400853
|      |`-> 0x00400849      bf73094000     mov edi, str.Always_dig_deeper ; 0x400973 ; "Always dig deeper"
|      |    0x0040084e      e81dfdffff     call sym.imp.puts           ; int puts(const char *s)
|      |    ; CODE XREF from main @ 0x400847
|      `--> 0x00400853      b800000000     mov eax, 0
|           0x00400858      488b4df8       mov rcx, qword [var_8h]
|           0x0040085c      6448330c2528.  xor rcx, qword fs:[0x28]
|       ,=< 0x00400865      7405           je 0x40086c
|       |   0x00400867      e824fdffff     call sym.imp.__stack_chk_fail ; void __stack_chk_fail(void)
|       `-> 0x0040086c      c9             leave
\           0x0040086d      c3             ret
```
```
[0x0040082c]> dr
rax = 0x7fff8020fc20
rbx = 0x00000000
rcx = 0x00000000
rdx = 0x7fff8020fc40
r8 = 0x00000000
r9 = 0x00000000
r10 = 0x00000004
r11 = 0x00000246
r12 = 0x004005e0
r13 = 0x7fff8020fd50
r14 = 0x00000000
r15 = 0x00000000
rsi = 0x7fff8020fc40
rdi = 0x7fff8020f6c0
rsp = 0x7fff8020fc00
rbp = 0x7fff8020fc70
rip = 0x0040082c
rflags = 0x00000202
orax = 0xffffffffffffffff
[0x0040082c]> px @ 0x7fff8020fc20
- offset -       0 1  2 3  4 5  6 7  8 9  A B  C D  E F  0123456789ABCDEF
0x7fff8020fc20  7465 7374 0000 0000 0000 0000 0000 0000  test............
0x7fff8020fc30  0100 0000 0000 0000 1d09 4000 0000 0000  ..........@.....
0x7fff8020fc40  XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX
0x7fff8020fc50  XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX
0x7fff8020fc60  50fd 2080 ff7f 0000 006f a4a1 c6b6 1a1e  P. ......o......
0x7fff8020fc70  d008 4000 0000 0000 bb7b c870 447f 0000  ..@......{.pD...
0x7fff8020fc80  0000 0000 0000 0000 58fd 2080 ff7f 0000  ........X. .....
0x7fff8020fc90  0000 0000 0200 0000 7307 4000 0000 0000  ........s.@.....
0x7fff8020fca0  0000 0000 0000 0000 e3f2 9b85 31c3 298e  ............1.).
0x7fff8020fcb0  e005 4000 0000 0000 50fd 2080 ff7f 0000  ..@.....P. .....
0x7fff8020fcc0  0000 0000 0000 0000 0000 0000 0000 0000  ................
0x7fff8020fcd0  e3f2 3b6d f0c3 d671 e3f2 dd62 2122 a170  ..;m...q...b!".p
0x7fff8020fce0  0000 0000 0000 0000 0000 0000 0000 0000  ................
0x7fff8020fcf0  0000 0000 0000 0000 0000 0000 0000 0000  ................
0x7fff8020fd00  9021 e670 447f 0000 b976 e470 447f 0000  .!.pD....v.pD...
0x7fff8020fd10  0000 0000 0000 0000 0000 0000 0000 0000  ................
[0x0040082c]> px @ 0x7fff8020fc40
- offset -       0 1  2 3  4 5  6 7  8 9  A B  C D  E F  0123456789ABCDEF
0x7fff8020fc40  XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX
0x7fff8020fc50  XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX
0x7fff8020fc60  50fd 2080 ff7f 0000 006f a4a1 c6b6 1a1e  P. ......o......
0x7fff8020fc70  d008 4000 0000 0000 bb7b c870 447f 0000  ..@......{.pD...
0x7fff8020fc80  0000 0000 0000 0000 58fd 2080 ff7f 0000  ........X. .....
0x7fff8020fc90  0000 0000 0200 0000 7307 4000 0000 0000  ........s.@.....
0x7fff8020fca0  0000 0000 0000 0000 e3f2 9b85 31c3 298e  ............1.).
0x7fff8020fcb0  e005 4000 0000 0000 50fd 2080 ff7f 0000  ..@.....P. .....
0x7fff8020fcc0  0000 0000 0000 0000 0000 0000 0000 0000  ................
0x7fff8020fcd0  e3f2 3b6d f0c3 d671 e3f2 dd62 2122 a170  ..;m...q...b!".p
0x7fff8020fce0  0000 0000 0000 0000 0000 0000 0000 0000  ................
0x7fff8020fcf0  0000 0000 0000 0000 0000 0000 0000 0000  ................
0x7fff8020fd00  9021 e670 447f 0000 b976 e470 447f 0000  .!.pD....v.pD...
0x7fff8020fd10  0000 0000 0000 0000 0000 0000 0000 0000  ................
0x7fff8020fd20  e005 4000 0000 0000 50fd 2080 ff7f 0000  ..@.....P. .....
0x7fff8020fd30  0000 0000 0000 0000 0906 4000 0000 0000  ..........@.....
[0x0040082c]>
```

# crackme6
```
[0x004006e9]> pdf @sym.my_secure_test
/ (fcn) sym.my_secure_test 340
|   sym.my_secure_test (int32_t arg1);
|           ; var int32_t var_8h @ rbp-0x8
|           ; arg int32_t arg1 @ rdi
|           ; CALL XREF from sym.compare_pwd @ 0x4006e4
|           0x0040057d      55             push rbp
|           0x0040057e      4889e5         mov rbp, rsp
|           0x00400581      48897df8       mov qword [var_8h], rdi     ; arg1
|           0x00400585      488b45f8       mov rax, qword [var_8h]
|           0x00400589      0fb600         movzx eax, byte [rax]
|           0x0040058c      84c0           test al, al
|       ,=< 0x0040058e      740b           je 0x40059b
|       |   0x00400590      488b45f8       mov rax, qword [var_8h]
|       |   0x00400594      0fb600         movzx eax, byte [rax]
|       |   0x00400597      3c31           cmp al, 0x31                ; 49
|      ,==< 0x00400599      740a           je 0x4005a5
|      |`-> 0x0040059b      b8ffffffff     mov eax, 0xffffffff         ; rax
|      |,=< 0x004005a0      e92a010000     jmp 0x4006cf
|      `--> 0x004005a5      488b45f8       mov rax, qword [var_8h]
|       |   0x004005a9      4883c001       add rax, 1
|       |   0x004005ad      0fb600         movzx eax, byte [rax]
|       |   0x004005b0      84c0           test al, al
|      ,==< 0x004005b2      740f           je 0x4005c3
|      ||   0x004005b4      488b45f8       mov rax, qword [var_8h]
|      ||   0x004005b8      4883c001       add rax, 1
|      ||   0x004005bc      0fb600         movzx eax, byte [rax]
|      ||   0x004005bf      3c33           cmp al, 0x33                ; 51
|     ,===< 0x004005c1      740a           je 0x4005cd
|     |`--> 0x004005c3      b8ffffffff     mov eax, 0xffffffff         ; rax
|     |,==< 0x004005c8      e902010000     jmp 0x4006cf
|     `---> 0x004005cd      488b45f8       mov rax, qword [var_8h]
|      ||   0x004005d1      4883c002       add rax, 2
|      ||   0x004005d5      0fb600         movzx eax, byte [rax]
|      ||   0x004005d8      84c0           test al, al
|     ,===< 0x004005da      740f           je 0x4005eb
|     |||   0x004005dc      488b45f8       mov rax, qword [var_8h]
|     |||   0x004005e0      4883c002       add rax, 2
|     |||   0x004005e4      0fb600         movzx eax, byte [rax]
|     |||   0x004005e7      3c33           cmp al, 0x33                ; 51
|    ,====< 0x004005e9      740a           je 0x4005f5
|    |`---> 0x004005eb      b8ffffffff     mov eax, 0xffffffff         ; rax
|    |,===< 0x004005f0      e9da000000     jmp 0x4006cf
|    `----> 0x004005f5      488b45f8       mov rax, qword [var_8h]
|     |||   0x004005f9      4883c003       add rax, 3
|     |||   0x004005fd      0fb600         movzx eax, byte [rax]
|     |||   0x00400600      84c0           test al, al
|    ,====< 0x00400602      740f           je 0x400613
|    ||||   0x00400604      488b45f8       mov rax, qword [var_8h]
|    ||||   0x00400608      4883c003       add rax, 3
|    ||||   0x0040060c      0fb600         movzx eax, byte [rax]
|    ||||   0x0040060f      3c37           cmp al, 0x37                ; 55
|   ,=====< 0x00400611      740a           je 0x40061d
|   |`----> 0x00400613      b8ffffffff     mov eax, 0xffffffff         ; rax
|   |,====< 0x00400618      e9b2000000     jmp 0x4006cf
|   `-----> 0x0040061d      488b45f8       mov rax, qword [var_8h]
|    ||||   0x00400621      4883c004       add rax, 4
|    ||||   0x00400625      0fb600         movzx eax, byte [rax]
|    ||||   0x00400628      84c0           test al, al
|   ,=====< 0x0040062a      740f           je 0x40063b
|   |||||   0x0040062c      488b45f8       mov rax, qword [var_8h]
|   |||||   0x00400630      4883c004       add rax, 4
|   |||||   0x00400634      0fb600         movzx eax, byte [rax]
|   |||||   0x00400637      3c5f           cmp al, 0x5f                ; 95
|  ,======< 0x00400639      740a           je 0x400645
|  |`-----> 0x0040063b      b8ffffffff     mov eax, 0xffffffff         ; rax
|  |,=====< 0x00400640      e98a000000     jmp 0x4006cf
|  `------> 0x00400645      488b45f8       mov rax, qword [var_8h]
|   |||||   0x00400649      4883c005       add rax, 5
|   |||||   0x0040064d      0fb600         movzx eax, byte [rax]
|   |||||   0x00400650      84c0           test al, al
|  ,======< 0x00400652      740f           je 0x400663
|  ||||||   0x00400654      488b45f8       mov rax, qword [var_8h]
|  ||||||   0x00400658      4883c005       add rax, 5
|  ||||||   0x0040065c      0fb600         movzx eax, byte [rax]
|  ||||||   0x0040065f      3c70           cmp al, 0x70                ; 112
| ,=======< 0x00400661      7407           je 0x40066a
| |`------> 0x00400663      b8ffffffff     mov eax, 0xffffffff         ; rax
| |,======< 0x00400668      eb65           jmp 0x4006cf
| `-------> 0x0040066a      488b45f8       mov rax, qword [var_8h]
|  ||||||   0x0040066e      4883c006       add rax, 6
|  ||||||   0x00400672      0fb600         movzx eax, byte [rax]
|  ||||||   0x00400675      84c0           test al, al
| ,=======< 0x00400677      740f           je 0x400688
| |||||||   0x00400679      488b45f8       mov rax, qword [var_8h]
| |||||||   0x0040067d      4883c006       add rax, 6
| |||||||   0x00400681      0fb600         movzx eax, byte [rax]
| |||||||   0x00400684      3c77           cmp al, 0x77                ; 119
| ========< 0x00400686      7407           je 0x40068f
| `-------> 0x00400688      b8ffffffff     mov eax, 0xffffffff         ; rax
| ,=======< 0x0040068d      eb40           jmp 0x4006cf
| --------> 0x0040068f      488b45f8       mov rax, qword [var_8h]
| |||||||   0x00400693      4883c007       add rax, 7
| |||||||   0x00400697      0fb600         movzx eax, byte [rax]
| |||||||   0x0040069a      84c0           test al, al
| ========< 0x0040069c      740f           je 0x4006ad
| |||||||   0x0040069e      488b45f8       mov rax, qword [var_8h]
| |||||||   0x004006a2      4883c007       add rax, 7
| |||||||   0x004006a6      0fb600         movzx eax, byte [rax]
| |||||||   0x004006a9      3c64           cmp al, 0x64                ; 100
| ========< 0x004006ab      7407           je 0x4006b4
| --------> 0x004006ad      b8ffffffff     mov eax, 0xffffffff         ; rax
| ========< 0x004006b2      eb1b           jmp 0x4006cf
| --------> 0x004006b4      488b45f8       mov rax, qword [var_8h]
| |||||||   0x004006b8      4883c008       add rax, 8
| |||||||   0x004006bc      0fb600         movzx eax, byte [rax]
| |||||||   0x004006bf      84c0           test al, al
| ========< 0x004006c1      7407           je 0x4006ca
| |||||||   0x004006c3      b8ffffffff     mov eax, 0xffffffff         ; rax
| ========< 0x004006c8      eb05           jmp 0x4006cf
| --------> 0x004006ca      b800000000     mov eax, 0
| |||||||   ; XREFS: CODE 0x004005a0  CODE 0x004005c8  CODE 0x004005f0  CODE 0x00400618  CODE 0x00400640
| |||||||   ; XREFS: CODE 0x00400668  CODE 0x0040068d  CODE 0x004006b2  CODE 0x004006c8
| ```````-> 0x004006cf      5d             pop rbp
\           0x004006d0      c3             ret
````

```
31 33 33 37 5f 70 77 64
```

# crackme7

```
| |||| |    0x08048665      3d697a0000     cmp eax, 0x7a69
| |||| |,=< 0x0804866a      7517           jne 0x8048683
| |||| ||   0x0804866c      83ec0c         sub esp, 0xc
| |||| ||   0x0804866f      68bc880408     push str.Wow_such_h4x0r     ; 0x80488bc ; "Wow such h4x0r!"
| |||| ||   0x08048674      e8f7fcffff     call sym.imp.puts           ; int puts(const char *s)
| |||| ||   0x08048679      83c410         add esp, 0x10
```

```
root@kali:~# ./crackme7
Menu:

[1] Say hello
[2] Add numbers
[3] Quit

[>] 31337
Wow such h4x0r!
XXXXXXXXXXXXXXXXXXXXXX
```


# crackme8
```
|           0x0804849b      8d4c2404       lea ecx, dword [arg_4h]
|           0x0804849f      83e4f0         and esp, 0xfffffff0
|           0x080484a2      ff71fc         push dword [ecx - 4]
|           0x080484a5      55             push ebp
|           0x080484a6      89e5           mov ebp, esp
|           0x080484a8      51             push ecx
|           0x080484a9      83ec04         sub esp, 4
|           0x080484ac      89c8           mov eax, ecx
|           0x080484ae      833802         cmp dword [eax], 2
|       ,=< 0x080484b1      741d           je 0x80484d0
|       |   0x080484b3      8b4004         mov eax, dword [eax + 4]
|       |   0x080484b6      8b00           mov eax, dword [eax]
|       |   0x080484b8      83ec08         sub esp, 8
|       |   0x080484bb      50             push eax
|       |   0x080484bc      6860860408     push str.Usage:__s_password ; 0x8048660 ; "Usage: %s password\n"
|       |   0x080484c1      e87afeffff     call sym.imp.printf         ; int printf(const char *format)
|       |   0x080484c6      83c410         add esp, 0x10
|       |   0x080484c9      b801000000     mov eax, 1
|      ,==< 0x080484ce      eb4c           jmp 0x804851c
|      |`-> 0x080484d0      8b4004         mov eax, dword [eax + 4]
|      |    0x080484d3      83c004         add eax, 4
|      |    0x080484d6      8b00           mov eax, dword [eax]
|      |    0x080484d8      83ec0c         sub esp, 0xc
|      |    0x080484db      50             push eax
|      |    0x080484dc      e89ffeffff     call sym.imp.atoi           ; int atoi(const char *str)
|      |    0x080484e1      83c410         add esp, 0x10
|      |    0x080484e4      3d0df0feca     cmp eax, 0xcafef00d
|      |,=< 0x080484e9      7417           je 0x8048502
|      ||   0x080484eb      83ec0c         sub esp, 0xc
|      ||   0x080484ee      6874860408     push str.Access_denied.     ; 0x8048674 ; "Access denied."
|      ||   0x080484f3      e858feffff     call sym.imp.puts           ; int puts(const char *s)
|      ||   0x080484f8      83c410         add esp, 0x10
|      ||   0x080484fb      b801000000     mov eax, 1
|     ,===< 0x08048500      eb1a           jmp 0x804851c
|     ||`-> 0x08048502      83ec0c         sub esp, 0xc
|     ||    0x08048505      6883860408     push str.Access_granted.    ; 0x8048683 ; "Access granted."
|     ||    0x0804850a      e841feffff     call sym.imp.puts           ; int puts(const char *s)
|     ||    0x0804850f      83c410         add esp, 0x10
|     ||    0x08048512      e80d000000     call sym.giveFlag
```

```
cafef00d
1100 1010 1111 1110 1111 0000 0000 1101
0011 0101 0000 0001 0000 1111 1111 0011
-xxxxxx
```
```
root@kali:~# ./crackme8 -XXXXXXXXX
Access granted.
XXXXXXXXXXXXXXXXXXXX
```

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

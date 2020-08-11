# crackme1

```
root@kali:~# strings crackme1.bin
/lib64/ld-linux-x86-64.so.2
libc.so.6
__isoc99_scanf
puts
__stack_chk_fail
__cxa_finalize
strcmp
__libc_start_main
GLIBC_2.7
GLIBC_2.4
GLIBC_2.2.5
_ITM_deregisterTMCloneTable
__gmon_start__
_ITM_registerTMCloneTable
=y
=9
52
AWAVI
AUATL
[]A\A]A^A_
enter password
password is correct
password is incorrect
hax0r
;*3$"
GCC: (Ubuntu 7.3.0-27ubuntu1~18.04) 7.3.0
crtstuff.c
deregister_tm_clones
__do_global_dtors_aux
completed.7696
__do_global_dtors_aux_fini_array_entry
frame_dummy
__frame_dummy_init_array_entry
crackme1.c
__FRAME_END__
__init_array_end
_DYNAMIC
__init_array_start
__GNU_EH_FRAME_HDR
_GLOBAL_OFFSET_TABLE_
__libc_csu_fini
_ITM_deregisterTMCloneTable
puts@@GLIBC_2.2.5
_edata
__stack_chk_fail@@GLIBC_2.4
__libc_start_main@@GLIBC_2.2.5
__data_start
strcmp@@GLIBC_2.2.5
__gmon_start__
__dso_handle
_IO_stdin_used
__libc_csu_init
__bss_start
main
__isoc99_scanf@@GLIBC_2.7
__TMC_END__
_ITM_registerTMCloneTable
__cxa_finalize@@GLIBC_2.2.5
.symtab
.strtab
.shstrtab
.interp
.note.ABI-tag
.note.gnu.build-id
.gnu.hash
.dynsym
.dynstr
.gnu.version
.gnu.version_r
.rela.dyn
.rela.plt
.init
.plt.got
.text
.fini
.rodata
.eh_frame_hdr
.eh_frame
.init_array
.fini_array
.dynamic
.data
.bss
.comment
root@kali:~# ./crackme1.bin
enter password
XXXXX
password is correct
root@kali:~#
```


# crackme2
```
root@kali:~# r2 -d -A crackme2.bin
Process with PID 1800 started...
= attach 1800 1800
bin.baddr 0x556317cc4000
Using 0x556317cc4000

```

```
[0x7ff0e12e9090]> pdf @main
/ (fcn) main 122
|   int main (int argc, char **argv, char **envp);
|           ; var int32_t var_ch @ rbp-0xc
|           ; var int32_t var_8h @ rbp-0x8
|           ; DATA XREF from entry0 @ 0x556317cc462d
|           0x556317cc471a      55             push rbp
|           0x556317cc471b      4889e5         mov rbp, rsp
|           0x556317cc471e      4883ec10       sub rsp, 0x10
|           0x556317cc4722      64488b042528.  mov rax, qword fs:[0x28]
|           0x556317cc472b      488945f8       mov qword [var_8h], rax
|           0x556317cc472f      31c0           xor eax, eax
|           0x556317cc4731      488d3dec0000.  lea rdi, qword str.enter_your_password ; 0x556317cc4824 ; "enter your password"
|           0x556317cc4738      e893feffff     call sym.imp.puts       ; int puts(const char *s)
|           0x556317cc473d      488d45f4       lea rax, qword [var_ch]
|           0x556317cc4741      4889c6         mov rsi, rax
|           0x556317cc4744      488d3ded0000.  lea rdi, qword [0x556317cc4838] ; "%d"
|           0x556317cc474b      b800000000     mov eax, 0
|           0x556317cc4750      e89bfeffff     call sym.imp.__isoc99_scanf ; int scanf(const char *format)
|           0x556317cc4755      8b45f4         mov eax, dword [var_ch]
|           0x556317cc4758      3d7c130000     cmp eax, 0x137c
|       ,=< 0x556317cc475d      750e           jne 0x556317cc476d
|       |   0x556317cc475f      488d3dd50000.  lea rdi, qword str.password_is_valid ; 0x556317cc483b ; "password is valid"
|       |   0x556317cc4766      e865feffff     call sym.imp.puts       ; int puts(const char *s)
|      ,==< 0x556317cc476b      eb0c           jmp 0x556317cc4779
|      |`-> 0x556317cc476d      488d3dd90000.  lea rdi, qword str.password_is_incorrect ; 0x556317cc484d ; "password is incorrect"
|      |    0x556317cc4774      e857feffff     call sym.imp.puts       ; int puts(const char *s)
|      |    ; CODE XREF from main @ 0x556317cc476b
|      `--> 0x556317cc4779      b800000000     mov eax, 0
|           0x556317cc477e      488b55f8       mov rdx, qword [var_8h]
|           0x556317cc4782      644833142528.  xor rdx, qword fs:[0x28]
|       ,=< 0x556317cc478b      7405           je 0x556317cc4792
|       |   0x556317cc478d      e84efeffff     call sym.imp.__stack_chk_fail ; void __stack_chk_fail(void)
|       `-> 0x556317cc4792      c9             leave
\           0x556317cc4793      c3             ret
^C
[0x7ff0e12e9090]>
[0x7ff0e12e9090]>
[1]+  Stopped                 r2 -d -A crackme2.bin
root@kali:~# ./crackme2.bin
enter your password
XXXX
password is valid
root@kali:~#
```

# crackme3
```
root@kali:~# r2 -d -A crackme3.bin
Process with PID 1935 started...
= attach 1935 1935
bin.baddr 0x556a60083000
Using 0x556a60083000
asm.bits 64
[x] Analyze all flags starting with sym. and entry0 (aa)
[Warning: Invalid range. Use different search.in=? or anal.in=dbg.maps.x
Warning: Invalid range. Use different search.in=? or anal.in=dbg.maps.x
[x] Analyze function calls (aac)
[x] Analyze len bytes of instructions for references (aar)
[x] Check for objc references
[x] Check for vtables
[TOFIX: aaft can't run in debugger mode.ions (aaft)
[x] Type matching analysis for all functions (aaft)
[x] Propagate noreturn information
[x] Use -AA or aaaa to perform additional experimental analysis.
[0x7fde10dc5090]> pdf @main
/ (fcn) main 170
|   int main (int argc, char **argv, char **envp);
|           ; var int32_t var_28h @ rbp-0x28
|           ; var int32_t var_23h @ rbp-0x23
|           ; var int32_t var_21h @ rbp-0x21
|           ; var int32_t var_20h @ rbp-0x20
|           ; var int32_t var_8h @ rbp-0x8
|           ; DATA XREF from entry0 @ 0x556a6008362d
|           0x556a6008371a      55             push rbp
|           0x556a6008371b      4889e5         mov rbp, rsp
|           0x556a6008371e      4883ec30       sub rsp, 0x30
|           0x556a60083722      64488b042528.  mov rax, qword fs:[0x28]
|           0x556a6008372b      488945f8       mov qword [var_8h], rax
|           0x556a6008372f      31c0           xor eax, eax
|           0x556a60083731      66c745dd617a   mov word [var_23h], 0x7a61 ; 'az'
|           0x556a60083737      c645df74       mov byte [var_21h], 0x74 ; 't' ; 116
|           0x556a6008373b      488d3d120100.  lea rdi, qword str.enter_your_password ; 0x556a60083854 ; "enter your password"
|           0x556a60083742      e889feffff     call sym.imp.puts       ; int puts(const char *s)
|           0x556a60083747      488d45e0       lea rax, qword [var_20h]
|           0x556a6008374b      4889c6         mov rsi, rax
|           0x556a6008374e      488d3d130100.  lea rdi, qword [0x556a60083868] ; "%s"
|           0x556a60083755      b800000000     mov eax, 0
|           0x556a6008375a      e891feffff     call sym.imp.__isoc99_scanf ; int scanf(const char *format)
|           0x556a6008375f      c745d8000000.  mov dword [var_28h], 0
|       ,=< 0x556a60083766      eb2f           jmp 0x556a60083797
|      .--> 0x556a60083768      8b45d8         mov eax, dword [var_28h]
|      :|   0x556a6008376b      4898           cdqe
|      :|   0x556a6008376d      0fb65405e0     movzx edx, byte [rbp + rax - 0x20]
|      :|   0x556a60083772      8b45d8         mov eax, dword [var_28h]
|      :|   0x556a60083775      4898           cdqe
|      :|   0x556a60083777      0fb64405dd     movzx eax, byte [rbp + rax - 0x23]
|      :|   0x556a6008377c      38c2           cmp dl, al
|     ,===< 0x556a6008377e      7413           je 0x556a60083793
|     |:|   0x556a60083780      488d3de40000.  lea rdi, qword str.password_is_incorrect ; 0x556a6008386b ; "password is incorrect"
|     |:|   0x556a60083787      e844feffff     call sym.imp.puts       ; int puts(const char *s)
|     |:|   0x556a6008378c      b800000000     mov eax, 0
|    ,====< 0x556a60083791      eb1b           jmp 0x556a600837ae
|    |`---> 0x556a60083793      8345d801       add dword [var_28h], 1
|    | :|   ; CODE XREF from main @ 0x556a60083766
|    | :`-> 0x556a60083797      837dd802       cmp dword [var_28h], 2
|    | `==< 0x556a6008379b      7ecb           jle 0x556a60083768
|    |      0x556a6008379d      488d3ddd0000.  lea rdi, qword str.password_is_correct ; 0x556a60083881 ; "password is correct"
|    |      0x556a600837a4      e827feffff     call sym.imp.puts       ; int puts(const char *s)
|    |      0x556a600837a9      b800000000     mov eax, 0
|    |      ; CODE XREF from main @ 0x556a60083791
|    `----> 0x556a600837ae      488b4df8       mov rcx, qword [var_8h]
|           0x556a600837b2      6448330c2528.  xor rcx, qword fs:[0x28]
|       ,=< 0x556a600837bb      7405           je 0x556a600837c2
|       |   0x556a600837bd      e81efeffff     call sym.imp.__stack_chk_fail ; void __stack_chk_fail(void)
|       `-> 0x556a600837c2      c9             leave
\           0x556a600837c3      c3             ret
[0x7fde10dc5090]> db 0x556a6008377c
[0x7fde10dc5090]> dc
enter your password
xxx
hit breakpoint at: 556a6008377c
[0x556a6008377c]> dc
hit breakpoint at: 556a6008377c
[0x556a6008377c]> dc
hit breakpoint at: 556a6008377c
[0x556a6008377c]> dr
rax = 0x00000074
rbx = 0x00000000
rcx = 0x00000000
rdx = 0x00000033
r8 = 0x00000000
r9 = 0x00000000
r10 = 0x00000003
r11 = 0x00000246
r12 = 0x556a60083610
r13 = 0x7ffc7da47430
r14 = 0x00000000
r15 = 0x00000000
rsi = 0x0000000a
rdi = 0x7ffc7da46de0
rsp = 0x7ffc7da47320
rbp = 0x7ffc7da47350
rip = 0x556a6008377c
rflags = 0x00000246
orax = 0xffffffffffffffff
[0x556a6008377c]> dc
password is incorrect
[0x7fde10cb4e56]> exit
Do you want to quit? (Y/n)
Do you want to kill the process? (Y/n)
root@kali:~# ./crackme3.bin
enter your password
xxx
password is correct
```

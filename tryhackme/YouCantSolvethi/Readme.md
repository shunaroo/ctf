```
oot@kali:~# nmap -sV -sC -T5 -p- 10.10.106.254
Starting Nmap 7.80 ( https://nmap.org ) at 2020-07-22 14:21 UTC
Nmap scan report for ip-10-10-106-254.eu-west-1.compute.internal (10.10.106.254)
Host is up (0.0013s latency).
Not shown: 65533 closed ports
PORT      STATE SERVICE VERSION
22/tcp    open  ssh     OpenSSH 7.6p1 Ubuntu 4ubuntu0.3 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey:
|   2048 b5:5a:45:3b:25:5a:e8:4a:0e:fd:ff:b9:d2:0e:33:15 (RSA)
|   256 2e:a7:17:5d:d1:82:73:17:e6:e2:f9:d3:4e:27:9e:4a (ECDSA)
|_  256 92:64:bb:7c:70:ae:bd:f6:cb:7f:81:d1:13:0d:26:ab (ED25519)
64695/tcp open  http    SimpleHTTPServer 0.6 (Python 3.6.8)
|_http-server-header: SimpleHTTP/0.6 Python/3.6.8
|_http-title: Hey there!
MAC Address: 02:69:36:70:F2:1A (Unknown)
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 12.01 seconds
root@kali:~#
```



```html
<html>
    <head>
        <title>Hey there!</title>
        <style>
        * {
            font-size: 150%;
            font-family: "Comic Sans MS";
        }
        h4 {
            visibility: hidden;
        }
        /* TODO: remove robots we don't want to give them a flag too easily*/
	/* list of available files. wannacry.html, ssh.html, flag.html, answer.html */
        </style>
        <meta http-equiv="refresh" content="0.1;url=index2.html" />
        <script>
        document.addEventListener('contextmenu', event => event.preventDefault() & alert("You can't right click lol"));
        </script>
    </head>
    <body background="bob.jpg">
        <h1>Welcome to <code>YouCantSolveThis</code>!</h1>
        <h3>Please note: This fun activity is intended for those aged 9 to 12.</h3>
        <h4>TODO: remove robots we don't want to give them a flag too flag4(XXXXX)</h4>
    </body>
</html>
```

- http://10.10.106.254:64695/ssh.html
```
ssh means secure shell it lets you remotely connect to a computer from your own computer the ssh details are apraximately:
iamstupid
password
have fun u dumby

you'll find some hints in hints.txt heres something important, a flag can be anything in this format flag($text) and $text is the text that belongs to the flag as a headsup, to see the flags, you need eyes. but a screenreader will work too. 
```

```
root@kali:~# ssh iamstupid@10.10.106.254
iamstupid@10.10.106.254's password:
Welcome to Ubuntu 18.04.3 LTS (GNU/Linux 4.15.0-58-generic x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/advantage

  System information as of Wed Jul 22 14:26:53 UTC 2020

  System load:  0.08               Processes:           86
  Usage of /:   30.9% of 40.05GB   Users logged in:     0
  Memory usage: 16%                IP address for eth0: 10.10.106.254
  Swap usage:   0%


 * Canonical Livepatch is available for installation.
   - Reduce system reboots and improve kernel security. Activate at:
     https://ubuntu.com/livepatch

11 packages can be updated.
0 updates are security updates.



The programs included with the Ubuntu system are free software;
the exact distribution terms for each program are described in the
individual files in /usr/share/doc/*/copyright.

Ubuntu comes with ABSOLUTELY NO WARRANTY, to the extent permitted by
applicable law.

Last login: Wed Aug 21 10:35:57 2019
iamstupid@bluepeter:~$ ls
anotherFolder  cbbcBestPrograms.txt  firefox.txt  hints.txt       runme.py
bob            coolFolder            flag.txt     not_a_flag.txt
iamstupid@bluepeter:~$ cat flag.txt
flag1(XXXXXX)
```

```
iamstupid@bluepeter:~$ cat hints.txt
# flag1
Hi! To start you off, let's go easy.
Firstly, you'll need some background as this is your FIRST TIME USING A COMPUTER! xD

cd is a command used to change directories. The file is stored in /home/iamstupid
so write "cd /home/iamstupid")

ls is a command used to list all files. type ls to see all the files in a directory.
As you have no idea what you're doing and this is the first flag, you are not expected to do much.
My boss told me to go easy on you as you are a little bit stupid. So here's some more hints for you.
On average, you'll need to type:
ls - 5 times
cd - 3 times

The flag is incredibly obviously named. You must be an absolute moron if you can't spot the flag
the second you cd into the right directory.

Now, you need to learn how to read.
I know, reading must be so tough for someone of your calibre. Do not fear. Use Nano to read the file.
Now go on, you got this! Make your parents proud.

# flag2
it's inside a file, there's only like 5 files here. just look for it. if you're not stupid, you'll definitely find it.

# flag3
Do you not even remember what you worked on last night?
Try to remember what you worked on the other day. You finished it, and then what did you do...?
Come on! You've got to remember this! flag8(Just think, soon you'll get to enjoy the sweet rewards that you've gotten!)

# flag4
Did you even nmap scan this site... come on... there's a massive hint. think: how did you get here?
# flag5
TODO ask steve to fill this out, i dont understand what u put in the goolle doc??

# flag6
Do you even know who you are? Like seriously? This flag is SO easy! You just need to use your phone number.
Can you remember that? That's all you need. Is your own PHONE NUMBER. Oh my god! What don't you understand?
Like literally. It is LITERALLY your phone number. I am LITERALLY GIVING THIS AWAY TO YOU
and you are too dumb to read this text! How do you not get it yet? IT. IS. LITERALLY. YOUR. PHONE. NUMBER.

still looking for hints? what don't you understand about "your phone number"?
# flag8
you have eyes btw
theres only like 5 files lol

# flag11
its hidden in a folder
unix philosplogy remember that bob
ia
```

```
iamstupid@bluepeter:~/coolFolder$ getfattr -d cool_story_bro.txt
# file: cool_story_bro.txt
user.comment="flag2(XXXX)"

iamstupid@bluepeter:~/coolFolder$
```

```
iamstupid@bluepeter:~$ grep -rnw '/home/iamstupid' -e 'flag'
/home/iamstupid/bob/.git/hooks/fsmonitor-watchman.sample:100:           # return the fast "everything is dirty" flag to git and do the
/home/iamstupid/bob/.git/logs/refs/heads/master:1:0000000000000000000000000000000000000000 fdc83516be82cfd6c5fbe1c5d69e0669d948526e iamstupid <flag3(jXXXX)@example.com> 1566312678 +0000     commit (initial): initial commit
/home/iamstupid/bob/.git/logs/HEAD:1:0000000000000000000000000000000000000000 fdc83516be82cfd6c5fbe1c5d69e0669d948526e iamstupid <flag3(XXXXX)@example.com> 1566312678 +0000  commit (initial): initial commit
Binary file /home/iamstupid/bob/.git/index matches
/home/iamstupid/flag.txt:1:flag1(XXXXXX

```

```
iamstupid@bluepeter:~$ cat /etc/passwd
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
cbbcadmin:x:1000:1000:Bob the Builder:/home/cbbcadmin:/bin/bash
iamstupid:x:1001:1001:i am stupid,1,2,2,flag6(327a6c4304ad5938eaff0efb6cc3e53dc):/home/iamstupid:/bin/bash
iamstupid@bluepeter:~$
```

```
flag8(XXXXXXk, soon you'll get to enjoy the sweet rewards that you've gotten!)
```


```
cbbcadmin@bluepeter:~/CTF-Server$ cat server.py
# Make sure this file is set to chmod 700!
# flag10(XXXX)

import http.server
import socketserver
import os


PORT = 64695

web_dir = os.path.join(os.path.dirname(__file__), 'web')
os.chdir(web_dir)

Handler = http.server.SimpleHTTPRequestHandler
with socketserver.TCPServer(("", PORT), Handler) as httpd:
    httpd.serve_forever()
cbbcadmin@bluepeter:~/CTF-Server$
```

```
cbbcadmin@bluepeter:~/CTF-Server$ sudo -l
[sudo] password for cbbcadmin:
Sorry, try again.
[sudo] password for cbbcadmin:
Sorry, try again.
[sudo] password for cbbcadmin:
Matching Defaults entries for cbbcadmin on bluepeter:
    env_reset, mail_badpass,
    secure_path=/usr/local/sbin\:/usr/local/bin\:/usr/sbin\:/usr/bin\:/sbin\:/bin\:/snap/bin

User cbbcadmin may run the following commands on bluepeter:
    (ALL : ALL) ALL
cbbcadmin@bluepeter:~/CTF-Server$ sudo su
root@bluepeter:/home/cbbcadmin/CTF-Server#
```

```
root@bluepeter:/home/iamstupid# getfattr -d anotherFolder/
# file: anotherFolder/
user.comment="flag11(XXXXXXX)"

root@bluepeter:/home/iamstupid#
```

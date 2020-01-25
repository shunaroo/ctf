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


# Levelx


```Bash


```

```Bash
ssh bandit.labs.overthewire.org -p 2220 -l banditx
```












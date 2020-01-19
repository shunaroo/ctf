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


# Levelx


```Bash


```

```Bash
ssh bandit.labs.overthewire.org -p 2220 -l banditx
```












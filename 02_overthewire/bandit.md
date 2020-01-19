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














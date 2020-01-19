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

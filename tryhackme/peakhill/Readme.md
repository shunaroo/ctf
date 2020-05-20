ftp://10.10.26.114/
```
root@kali:~# ftp 10.10.26.114
Connected to 10.10.26.114.
220 (vsFTPd 3.0.3)
Name (10.10.26.114:root): anonymous
331 Please specify the password.
Password:
230 Login successful.
Remote system type is UNIX.
Using binary mode to transfer files.
ftp> ls
200 PORT command successful. Consider using PASV.
150 Here comes the directory listing.
-rw-r--r--    1 ftp      ftp            17 May 15 18:37 test.txt
226 Directory send OK.
ftp> get test.txt
local: test.txt remote: test.txt
200 PORT command successful. Consider using PASV.
150 Opening BINARY mode data connection for test.txt (17 bytes).
226 Transfer complete.
17 bytes received in 0.00 secs (313.2370 kB/s)
ftp> exot
?Invalid command
ftp> exit
221 Goodbye.
root@kali:~# cat test.txt
vsftpd test file
root@kali:~#


root@kali:~# nmap -vv -sV -p- --script vuln 10.10.26.114

PORT     STATE  SERVICE  REASON         VERSION
20/tcp   closed ftp-data reset ttl 64
21/tcp   open   ftp      syn-ack ttl 64 vsftpd 3.0.3
|_clamav-exec: ERROR: Script execution failed (use -d to debug)
|_sslv2-drown:
22/tcp   open   ssh      syn-ack ttl 64 OpenSSH 7.2p2 Ubuntu 4ubuntu2.8 (Ubuntu Linux; protocol 2.0)
|_clamav-exec: ERROR: Script execution failed (use -d to debug)
7321/tcp open   swx?     syn-ack ttl 64
|_clamav-exec: ERROR: Script execution failed (use -d to debug)
| fingerprint-strings:
|   DNSStatusRequestTCP, DNSVersionBindReqTCP, FourOhFourRequest, GenericLines, GetRequest, HTTPOptions, Help, JavaRMI, Kerberos, LANDesk-RC, LDAPBindReq, LDAPSearchReq, LPDString, NCP, NotesRPC, RPCCheck, RTSPRequest, SIPOptions, SMBProgNeg, SSLSessionReq, TLSSessionReq, TerminalServer, TerminalServerCookie, WMSRequest, X11Probe, afp, giop, ms-sql-s, oracle-tns:
|     Username: Password:
|   NULL:
|_    Username:
1 service unrecognized despite returning data. If you know the service/version, please submit the following fingerprint at https://nmap.org/cgi-bin/submit.cgi?new-service :
SF-Port7321-TCP:V=7.80%I=7%D=5/20%Time=5EC53A13%P=x86_64-pc-linux-gnu%r(NU
SF:LL,A,"Username:\x20")%r(GenericLines,14,"Username:\x20Password:\x20")%r
SF:(GetRequest,14,"Username:\x20Password:\x20")%r(HTTPOptions,14,"Username
SF::\x20Password:\x20")%r(RTSPRequest,14,"Username:\x20Password:\x20")%r(R
SF:PCCheck,14,"Username:\x20Password:\x20")%r(DNSVersionBindReqTCP,14,"Use
SF:rname:\x20Password:\x20")%r(DNSStatusRequestTCP,14,"Username:\x20Passwo
SF:rd:\x20")%r(Help,14,"Username:\x20Password:\x20")%r(SSLSessionReq,14,"U
SF:sername:\x20Password:\x20")%r(TerminalServerCookie,14,"Username:\x20Pas
SF:sword:\x20")%r(TLSSessionReq,14,"Username:\x20Password:\x20")%r(Kerbero
SF:s,14,"Username:\x20Password:\x20")%r(SMBProgNeg,14,"Username:\x20Passwo
SF:rd:\x20")%r(X11Probe,14,"Username:\x20Password:\x20")%r(FourOhFourReque
SF:st,14,"Username:\x20Password:\x20")%r(LPDString,14,"Username:\x20Passwo
SF:rd:\x20")%r(LDAPSearchReq,14,"Username:\x20Password:\x20")%r(LDAPBindRe
SF:q,14,"Username:\x20Password:\x20")%r(SIPOptions,14,"Username:\x20Passwo
SF:rd:\x20")%r(LANDesk-RC,14,"Username:\x20Password:\x20")%r(TerminalServe
SF:r,14,"Username:\x20Password:\x20")%r(NCP,14,"Username:\x20Password:\x20
SF:")%r(NotesRPC,14,"Username:\x20Password:\x20")%r(JavaRMI,14,"Username:\
SF:x20Password:\x20")%r(WMSRequest,14,"Username:\x20Password:\x20")%r(orac
SF:le-tns,14,"Username:\x20Password:\x20")%r(ms-sql-s,14,"Username:\x20Pas
SF:sword:\x20")%r(afp,14,"Username:\x20Password:\x20")%r(giop,14,"Username
SF::\x20Password:\x20");
MAC Address: 02:1A:34:4A:4C:98 (Unknown)
Service Info: OSs: Unix, Linux; CPE: cpe:/o:linux:linux_kernel

NSE: Script Post-scanning.
NSE: Starting runlevel 1 (of 2) scan.
Initiating NSE at 14:11
Completed NSE at 14:11, 0.00s elapsed
NSE: Starting runlevel 2 (of 2) scan.
Initiating NSE at 14:11
Completed NSE at 14:11, 0.00s elapsed
Read data files from: /usr/bin/../share/nmap
Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 276.13 seconds
           Raw packets sent: 131146 (5.770MB) | Rcvd: 91 (3.979KB)
root@kali:~#

# nmap
```
root@kali:~# nmap -sC -sV -p- 10.10.194.177
Starting Nmap 7.80 ( https://nmap.org ) at 2020-05-16 13:07 UTC
Nmap scan report for ip-10-10-194-177.eu-west-1.compute.internal (10.10.194.177)
Host is up (0.00045s latency).
Not shown: 65521 closed ports
PORT      STATE SERVICE       VERSION
80/tcp    open  http          Microsoft HTTPAPI httpd 2.0 (SSDP/UPnP)
| http-robots.txt: 4 disallowed entries
|_/bin/ /config/ /umbraco/ /umbraco_client/
|_http-title: Anthem.com - Welcome to our blog
135/tcp   open  msrpc         Microsoft Windows RPC
139/tcp   open  netbios-ssn   Microsoft Windows netbios-ssn
445/tcp   open  microsoft-ds?
3389/tcp  open  ms-wbt-server Microsoft Terminal Services
| rdp-ntlm-info:
|   Target_Name: WIN-LU09299160F
|   NetBIOS_Domain_Name: WIN-LU09299160F
|   NetBIOS_Computer_Name: WIN-LU09299160F
|   DNS_Domain_Name: WIN-LU09299160F
|   DNS_Computer_Name: WIN-LU09299160F
|   Product_Version: 10.0.17763
|_  System_Time: 2020-05-16T13:14:33+00:00
| ssl-cert: Subject: commonName=WIN-LU09299160F
| Not valid before: 2020-04-04T22:56:38
|_Not valid after:  2020-10-04T22:56:38
|_ssl-date: 2020-05-16T13:14:40+00:00; +1s from scanner time.
5985/tcp  open  http          Microsoft HTTPAPI httpd 2.0 (SSDP/UPnP)
|_http-server-header: Microsoft-HTTPAPI/2.0
|_http-title: Not Found
47001/tcp open  http          Microsoft HTTPAPI httpd 2.0 (SSDP/UPnP)
|_http-server-header: Microsoft-HTTPAPI/2.0
|_http-title: Not Found
49664/tcp open  msrpc         Microsoft Windows RPC
49665/tcp open  msrpc         Microsoft Windows RPC
49666/tcp open  msrpc         Microsoft Windows RPC
49668/tcp open  msrpc         Microsoft Windows RPC
49669/tcp open  msrpc         Microsoft Windows RPC
49670/tcp open  msrpc         Microsoft Windows RPC
49672/tcp open  msrpc         Microsoft Windows RPC
MAC Address: 02:00:05:8B:A1:50 (Unknown)
Service Info: OS: Windows; CPE: cpe:/o:microsoft:windows

Host script results:
|_nbstat: NetBIOS name: WIN-LU09299160F, NetBIOS user: <unknown>, NetBIOS MAC: 02:00:05:8b:a1:50 (unknown)
| smb2-security-mode:
|   2.02:
|_    Message signing enabled but not required
| smb2-time:
|   date: 2020-05-16T13:14:32
|_  start_date: N/A

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 402.32 seconds
root@kali:~#
```


```

HTTP/1.1 200 OK
Content-Type: text/plain
Last-Modified: Sun, 05 Apr 2020 23:02:00 GMT
Accept-Ranges: bytes
ETag: "d296b3369ebd61:0"
X-MiniProfiler-Ids: ["0ed44f1d-4501-4a57-b827-58b7e6b0bacb"]
Date: Sat, 16 May 2020 13:07:37 GMT
Connection: close
Content-Length: 192

UmbracoIsTheBest!

# Use for all search robots
User-agent: *

# Define the directories not to crawl
Disallow: /bin/
Disallow: /config/
Disallow: /umbraco/
Disallow: /umbraco_client/

```


```
Married Buried
Born on a Monday,
Christened on Tuesday,
Married on Wednesday,
Took ill on Thursday,
Grew worse on Friday,
Died on Saturday,
Buried on Sunday.
That was the end…  

https://en.wikipedia.org/wiki/Solomon_Grundy_(nursery_rhyme)
```

```
JD@anthem.com
Jane Doe

Solomon Grundy
SG@anthem.com

```

# flag1
```html
view-source:http://10.10.194.177/archive/we-are-hiring/
<html>
<head>
    <meta http-equiv="Content-Type" content="text/html" charset="UTF-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge,chrome=1" />

    <title>We are hiring - Anthem.com</title>
    <meta name="description" content="Hi fellow readers,We are currently hiring. We are looking for young talented to join a good cause and keep this community alive!If you have an interest in being a part of the movement send me your CV" />
    <meta name="twitter:card" value="summary">
<meta content="We are hiring" property="og:title" />
<meta content="article" property="og:type" />
<meta content="http://10.10.194.177/archive/we-are-hiring/" property="og:url" />
<meta content="THM{L0L_WH0_US3S_M3T4}" property="og:description" />
```


# flag2
```html
GET / HTTP/1.1
Host: 10.10.194.177
User-Agent: Mozilla/5.0 (X11; CrOS armv7l 9592.96.0) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/60.0.3112.114 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,*/*;q=0.8
Accept-Language: ja,en-US;q=0.7,en;q=0.3
Accept-Encoding: gzip, deflate
Connection: close
Upgrade-Insecure-Requests: 1
-----------------
    <form method="get" action="/search">
        <input type="text" name="term" placeholder="Search... 								THM{G!T_G00D}" />
        <button type="submit" class="fa fa-search fa"></button>
    </form>

```


# flag3
```
http://10.10.194.177/authors/jane-doe/

Author for Anthem blog
***{*****************}
Website: THM{L0L_WH0_D15} 
```

# flag4
```html
/archive/a-cheers-to-our-it-department/
<head>
    <meta http-equiv="Content-Type" content="text/html" charset="UTF-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge,chrome=1" />

    <title>A cheers to our IT department - Anthem.com</title>
    <meta name="description" content="During our hard times our beloved admin managed to save our business by redesigning the entire website.As we all around here knows how much I love writing poems I decided to write one about him:Born" />
    <meta name="twitter:card" value="summary">
<meta content="A cheers to our IT department" property="og:title" />
<meta content="article" property="og:type" />
<meta content="http://10.10.246.78/archive/a-cheers-to-our-it-department/" property="og:url" />
<meta content="THM{AN0TH3R_M3TA}" property="og:description" />
```




## robots.txt
```
http://cmess.thm/robots.txt
User-agent: *
Disallow: /src/
Disallow: /themes/
Disallow: /lib/
```

## nikto
```
root@kali:~# nikto -h cmess.thm
- Nikto v2.1.6
-----------------------------------------------------------------
+ Target IP:          10.10.94.111
+ Target Hostname:    cmess.thm
+ Target Port:        80
+ Start Time:         2020-05-10 04:25:47 (GMT0)
-----------------------------------------------------------------
+ Server: Apache/2.4.18 (Ubuntu)
+ The anti-clickjacking X-Frame-Options header is not present.
+ The X-XSS-Protection header is not defined. This header can hin                                                     XSS
+ The X-Content-Type-Options header is not set. This could allow                                                     a different fashion to the MIME type
+ No CGI Directories found (use '-C all' to force check all possi
+ "robots.txt" contains 3 entries which should be manually viewed
+ Apache/2.4.18 appears to be outdated (current is at least Apach                                                    ch.
+ Web Server returns a valid response with junk HTTP methods, thi
+ Cookie PHPSESSID created without the httponly flag
+ /admin/config.php: PHP Config file may contain database IDs and
+ /admin/cplogfile.log: DevBB 1.0 final (http://www.mybboard.com)                                                    t version.
+ /admin/system_footer.php: myphpnuke version 1.8.8_final_7 revea
+ OSVDB-3233: /admin/admin_phpinfo.php4: Mon Album from http://ww                                                    s. This should be protected.
+ OSVDB-5034: /admin/login.php?action=insert&username=test&passwo                                                     be inserted without proper authentication. Attempt to log in wit
+ OSVDB-376: /admin/contextAdmin/contextAdmin.html: Tomcat may be                                                    estrict access to /admin.
+ OSVDB-4804: //admin/admin.shtml: Axis network camera may allow
+ OSVDB-2813: /admin/database/wwForum.mdb: Web Wiz Forums pre 7.5                                                    ult login/pass is Administrator/letmein
+ OSVDB-2842: //admin/aindex.htm: FlexWATCH firmware 2.2 is vulne                                                    a '/'. http://packetstorm.linuxsecurity.com/0310-exploits/FlexWAT
+ OSVDB-2922: /admin/wg_user-info.ml: WebGate Web Eye exposes use
+ OSVDB-3092: /admin/: This might be interesting...
+ OSVDB-3092: /login/: This might be interesting...
+ OSVDB-3093: /admin/auth.php: This might be interesting... has b
+ OSVDB-3093: /admin/cfg/configscreen.inc.php+: This might be int                                                    n scanner.
+ OSVDB-3093: /admin/cfg/configsite.inc.php+: This might be inter                                                    scanner.
+ OSVDB-3093: /admin/cfg/configsql.inc.php+: This might be intere                                                    canner.
+ OSVDB-3093: /admin/cfg/configtache.inc.php+: This might be inte                                                     scanner.
+ OSVDB-3093: /admin/cms/htmltags.php: This might be interesting.                                                    .
+ OSVDB-3093: /admin/credit_card_info.php: This might be interest                                                    nner.
+ OSVDB-3093: /admin/exec.php3: This might be interesting... has
+ OSVDB-3093: /admin/index.php: This might be interesting... has
+ OSVDB-3093: /admin/modules/cache.php+: This might be interestin                                                    er.
+ OSVDB-3093: /admin/objects.inc.php4: This might be interesting.                                                    .
+ OSVDB-3093: /admin/script.php: This might be interesting... has
+ OSVDB-3093: /admin/settings.inc.php+: This might be interesting                                                    r.
+ OSVDB-3093: /admin/templates/header.php: This might be interest                                                    nner.
+ OSVDB-3093: /admin/upload.php: This might be interesting... has
+ OSVDB-4238: /admin/adminproc.asp: Xpede administration page may                                                    ted.
+ OSVDB-4239: /admin/datasource.asp: Xpede page reveals SQL accou
+ OSVDB-6666: /cgi-bin/hpnst.exe?c=p+i=SrvSystemInfo.html: HP Ins                                                    nerable to a DoS.
+ OSVDB-9624: /admin/admin.php?adminpy=1: PY-Membres 4.2 may allo
+ OSVDB-3233: /icons/README: Apache default file found.
+ OSVDB-3092: /fm/: This might be interesting... potential countr
+ /admin/account.asp: Admin login page/section found.
+ /admin/account.html: Admin login page/section found.
+ /admin/account.php: Admin login page/section found.
+ /admin/controlpanel.asp: Admin login page/section found.
+ /admin/controlpanel.html: Admin login page/section found.
+ /admin/controlpanel.php: Admin login page/section found.
+ /admin/cp.asp: Admin login page/section found.
+ /admin/cp.html: Admin login page/section found.
+ /admin/cp.php: Admin login page/section found.
+ /admin/home.asp: Admin login page/section found.
+ /admin/home.php: Admin login page/section found.
+ /admin/index.asp: Admin login page/section found.
+ /admin/index.html: Admin login page/section found.
+ /admin/login.asp: Admin login page/section found.
+ /admin/login.html: Admin login page/section found.
+ /admin/login.php: Admin login page/section found.
+ /admin/html: Tomcat Manager / Host Manager interface found (pas
+ /admin/status: Tomcat Server Status interface found (pass prote
+ /admin/sites/new: ComfortableMexicanSofa CMS Engine Admin Backe
+ 7788 requests: 0 error(s) and 59 item(s) reported on remote hos
+ End Time:           2020-05-10 04:26:54 (GMT0) (67 seconds)
-----------------------------------------------------------------
+ 1 host(s) tested
```



## subdomain fuzz
````
root@kali:~# wfuzz -c -f sub-fighter -w subdomains-top1million-5000.txt -u "http://cmess.thm" -H "Host: FUZZ.cmess.thm" --hw 290

Warning: Pycurl is not compiled against Openssl. Wfuzz might not work correctly when fuzzing SSL sites. Check Wfuzz's documentation for more information.

********************************************************
* Wfuzz 2.4 - The Web Fuzzer                           *
********************************************************

Target: http://cmess.thm/
Total requests: 4997

===================================================================
ID           Response   Lines    Word     Chars       Payload
===================================================================

000000019:   200        30 L     104 W    934 Ch      "dev"

Total time: 19.60935
Processed Requests: 4997
Filtered Requests: 4996
Requests/sec.: 254.8273
```


## access subdomain
```
root@kali:~# curl dev.cmess.thm
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Development</title>
</head>
<body>
    <h2>Development Log</h2>
<article>
    <h3>andre@cmess.thm</h3>
    <p>Have you guys fixed the bug that was found on live?</p>
</article>
    <article>
        <h3>support@cmess.thm</h3>
        <p>Hey Andre, We have managed to fix the misconfigured .htaccess file, we're hoping to patch it in the upcoming patch!</p>

    </article>
    <article>
        <h3>support@cmess.thm</h3>
        <p>Update! We have had to delay the patch due to unforeseen circumstances</p>
    </article>
    <article>
        <h3>andre@cmess.thm</h3>
        <p>That's ok, can you guys reset my password if you get a moment, I seem to be unable to get onto the admin panel.</p>
    </article>
    <article>
        <h3>support@cmess.thm</h3>
        <p>Your password has been reset. Here: KPFTN_f2yxe% </p>
    </article>
</body>
</html>root@kali:~#
```




```
http://cmess.thm/admin/

Page created in 0.533472 seconds.
Gila CMS version 1.10.9 
→serach vuln
https://www.exploit-db.com/exploits/47407



http://cmess.thm/admin/fm

change index.php to revershell
https://raw.githubusercontent.com/pentestmonkey/php-reverse-shell/master/php-reverse-shell.php


linenum
/opt/.backup
get password


ssh andre@targetip


linenum
cronjob
https://www.hackingarticles.in/exploiting-wildcard-for-privilege-escalation/

```

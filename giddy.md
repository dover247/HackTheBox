# Giddy

### Foothold

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
| Public Key type: rsa
| Public Key bits: 1024
| Signature Algorithm: sha1WithRSAEncryption
| Not valid before: 2018-06-16T21:28:55
| Not valid after:  2018-09-14T21:28:55
| MD5:   78a7 4af5 3b09 c882 a149 f977 cf8f 1182
| SHA-1: 8adc 3379 878a f13f 0154 406a 3ead d345 6967 6a23
| -----BEGIN CERTIFICATE-----
| MIICHTCCAYagAwIBAgIQG2rbVjzfZqJIr005rMK4xTANBgkqhkiG9w0BAQUFADAp
| MScwJQYDVQQDDB5Qb3dlclNoZWxsV2ViQWNjZXNzVGVzdFdlYlNpdGUwHhcNMTgw
| NjE2MjEyODU1WhcNMTgwOTE0MjEyODU1WjApMScwJQYDVQQDDB5Qb3dlclNoZWxs
| V2ViQWNjZXNzVGVzdFdlYlNpdGUwgZ8wDQYJKoZIhvcNAQEBBQADgY0AMIGJAoGB
| ALOvHao3JEpJzzBHR9oCc+934QLPu2vRlC7jZAwySPX6v6fkvzsDr7uD50maLVtW
| 9etn9KVwfmgkYd6YtY+86YCc935s1rppNtNKeVXsG/PM4G+4HdPFf1Ik3Vj6fc1y
| w1nx2PLSNvlC74kkc33MA8y//vxqIckSJiHiVa5ZzdR/AgMBAAGjRjBEMBMGA1Ud
| JQQMMAoGCCsGAQUFBwMBMB0GA1UdDgQWBBS4T3PavA05OLCMaCa6GqgXsjCoozAO
| BgNVHQ8BAf8EBAMCBSAwDQYJKoZIhvcNAQEFBQADgYEAm6FzHooZ+SSLNp9KvPdX
| jjFPpf9Jv4j8Ao9qv1RnbwmTE5SSHhusXDOiAIOsErTVdaNa0VRcduMt+H054kfp
| 1MeoYvKXuXlMLbGe+orEIiVPjC/7cTJIVyfgyhdl5PdtetlZGrspK8h+2QqvxXpF
| im+bXy93yFQ6G9tOrzpBmFY=
|_-----END CERTIFICATE-----
|_ssl-date: 2022-11-06T01:45:58+00:00; -1s from scanner time.
| tls-alpn: 
|   h2
|_  http/1.1
| rdp-ntlm-info: 
|   Target_Name: GIDDY
|   NetBIOS_Domain_Name: GIDDY
|   NetBIOS_Computer_Name: GIDDY
|   DNS_Domain_Name: Giddy
|   DNS_Computer_Name: Giddy
|   Product_Version: 10.0.14393
|_  System_Time: 2022-11-06T01:45:52+00:00
| ssl-cert: Subject: commonName=Giddy
| Issuer: commonName=Giddy
| Public Key type: rsa
| Public Key bits: 2048
| Signature Algorithm: sha256WithRSAEncryption
| Not valid before: 2022-11-05T01:42:12
| Not valid after:  2023-05-07T01:42:12
| MD5:   a710 a80c 763e 589c f3e3 0852 aa17 53d9
| SHA-1: b50a b303 da55 c155 612b 9e5a f31e bda7 b5b4 2333
| -----BEGIN CERTIFICATE-----
| MIICzjCCAbagAwIBAgIQcH8x+QH8W5xNRVHFenM6KjANBgkqhkiG9w0BAQsFADAQ
| MQ4wDAYDVQQDEwVHaWRkeTAeFw0yMjExMDUwMTQyMTJaFw0yMzA1MDcwMTQyMTJa
| MBAxDjAMBgNVBAMTBUdpZGR5MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKC
| AQEAvsp+27XLcyVgm2kfqvvnI5tvkJvOX8HaAY3RCzUriGDpe7I+WwbigXBeTkqW
| TyOYKwRabkKcqh8hZR+mOi3GGlayj1wHDcRYL6reJRhGA7iwTeLbS6CJsGlpS33I
| YXIbY59pyYZPZQsKnBG1Wqyfe3xXsq/jd0xHHQWrqlCwRhUy/VFbSbX3CT1ga58y
| gc5rc11UfHuId3p7EbMV6wOitRW7N/bCWFYEdgz9bpASyiNMVtf05V9xJYZYX4+Z
| Dgu2l2c/MOuz/Ic+wRJmnvIeUwN2RG4E+n2MAY89zZufNfimg4IISqX870EEIwJF
| jS7XxNgcOPe2B6etBHljoguXMQIDAQABoyQwIjATBgNVHSUEDDAKBggrBgEFBQcD
| ATALBgNVHQ8EBAMCBDAwDQYJKoZIhvcNAQELBQADggEBAFOoKvTvtG96gkmrOI5Q
| HOxQzzTHtqehxFR9BHo8/Fak1iElbTkD+RyQZDk5tsJ4DUmOR4JhVpPPx8bsQlk9
| ytEDTQfW8/M+GKh/OJAIQDFRavgYNKy4k7JVfXi5qY7G8hrnRqrqy02B+LcNcy1n
| Q0fNhJR/wmJGUJhbN4KFT3yjmv5iXmbgKHf+PyNUXYbSJo1alsmZLgH0OOb2dyo1
| Q4O85f7t1iZgpXwIWe8NyXdJd+kSfaeztxBN53yb8sKrWyiftwwahMawUksA1rH6
| MtH9KyrGut5ZznkoGJndm6qtDKjz4fSH92YKnMzoy1U2e6kpe1O318qOd0cByUNA
| LsQ=
|_-----END CERTIFICATE-----
|_ssl-date: 2022-11-06T01:45:59+00:00; 0s from scanner time....3389/tcp open  ms-wbt-server syn-ack ttl 127 Microsoft Terminal Services
|_http-server-header: Microsoft-HTTPAPI/2.0

```

<figure><img src=".gitbook/assets/image (6).png" alt=""><figcaption><p>Landing Page. Nothing of Interest.</p></figcaption></figure>

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

aspnet_client           [Status: 403, Size: 1233, Words: 73, Lines: 30, Duration: 78ms]
<strong>remote                  [Status: 302, Size: 160, Words: 6, Lines: 4, Duration: 641ms]
</strong>                        [Status: 200, Size: 700, Words: 27, Lines: 32, Duration: 63ms]
mvc                     [Status: 200, Size: 9902, Words: 754, Lines: 152, Duration: 3917ms]</code></pre>

<figure><img src=".gitbook/assets/image (7).png" alt=""><figcaption><p>Some Kind Store Web App</p></figcaption></figure>

<figure><img src=".gitbook/assets/image.png" alt=""><figcaption><p>Entering an Apostrophe in the Search Field Confirms That It's Vulnerable to SQL Injection </p></figcaption></figure>

<figure><img src=".gitbook/assets/image (5).png" alt=""><figcaption><p>Confirmed SQL Injection</p></figcaption></figure>

<figure><img src=".gitbook/assets/image (3).png" alt=""><figcaption><p>Redoing The Injection Using Burp Suite Using A Different Payload To Capture an NTLMv2 Hash </p></figcaption></figure>

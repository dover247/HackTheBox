# Search

## Penetration Test Report

### Introduction

The penetration test report contains all efforts that were conducted during client engagement. The purpose of this report is to ensure that the client has a full understanding of penetration testing methodologies as well as the technical knowlegde to remediate any security flaws.

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

* 10.129.227.156 (hostname) - Name of initial exploit

### Recommendations

I recommend patching the vulnerabilities identified during the testing to ensure that an attacker cannot exploit these systems in the future. One thing to remember is that these systems require frequent patching and once patched, should remain on a regular patch program to protect additional vulnerabilities that are discovered at a later date.

## Methodologies

I utilized a widely adopted approach to performing penetration testing that is effective in testing how well the environments is secured. Below is a breakout of how I was able to identify and exploit the variety of systems and includes all individual vulnerabilities found.

### Information Gathering

The information gathering portion of a penetration test focuses on identifying the scope of the penetration test. During this penetration test, I was tasked with exploiting the client network. The specific IP addresses were:

**Network**

* 10.129.227.0/24

### Penetration

The penetration testing portions of the assessment focus heavily on gaining access to a variety of systems. During this penetration test, I was able to successfully gain access to _X_ out of the _X_ systems.

#### System IP: 10.129.227.156

**Service Enumeration**

The service enumeration portion of a penetration test focuses on gathering information about what services are alive on a system or systems. This is valuable for an attacker as it provides detailed information on potential attack vectors into a system. Understanding what applications are running on the system gives an attacker needed information before performing the actual penetration test. In some cases, some ports may not be listed.

| Server IP Address | Ports Open                                                                                          |
| ----------------- | --------------------------------------------------------------------------------------------------- |
| 10.129.227.156    | **TCP**: 53,80,88,135,139,389,443,445,464,593,636,3268,3269,8172,9389,49667,49693,49694,49704,49719 |
|                   | **UDP**:                                                                                            |

**Nmap Scan Results**

```
┌──[Thu Nov 10 07:03:19 PM CST 2022]-[TheScriptKid]-[/tmp]
├──[wlan0: 192.168.1.153]-[tun0: 10.10.16.2]-[ip: 10.129.227.156]
└──# rscan $ip        
rustscan --accessible -u 5000 -b 2500 -a 10.129.227.156 -- -Pn -A

Automatically increasing ulimit value to 5000.
Open 10.129.227.156:53
Open 10.129.227.156:80
Open 10.129.227.156:88
Open 10.129.227.156:135
Open 10.129.227.156:139
Open 10.129.227.156:389
Open 10.129.227.156:443
Open 10.129.227.156:445
Open 10.129.227.156:464
Open 10.129.227.156:593
Open 10.129.227.156:636
Open 10.129.227.156:3268
Open 10.129.227.156:3269
Open 10.129.227.156:8172
Open 10.129.227.156:9389
Open 10.129.227.156:49667
Open 10.129.227.156:49693
Open 10.129.227.156:49694
Open 10.129.227.156:49704
Open 10.129.227.156:49719
Starting Script(s)
Running script "nmap -vvv -p {{port}} {{ip}} -Pn -A" on ip 10.129.227.156
Depending on the complexity of the script, results may take some time to appear.
Host discovery disabled (-Pn). All addresses will be marked 'up' and scan times may be slower.
Starting Nmap 7.92 ( https://nmap.org ) at 2022-11-10 19:04 CST
NSE: Loaded 155 scripts for scanning.
NSE: Script Pre-scanning.
NSE: Starting runlevel 1 (of 3) scan.
Initiating NSE at 19:04
Completed NSE at 19:04, 0.00s elapsed
NSE: Starting runlevel 2 (of 3) scan.
Initiating NSE at 19:04
Completed NSE at 19:04, 0.00s elapsed
NSE: Starting runlevel 3 (of 3) scan.
Initiating NSE at 19:04
Completed NSE at 19:04, 0.00s elapsed
Initiating Parallel DNS resolution of 1 host. at 19:04
Completed Parallel DNS resolution of 1 host. at 19:04, 0.00s elapsed
DNS resolution of 1 IPs took 0.00s. Mode: Async [#: 2, OK: 0, NX: 1, DR: 0, SF: 0, TR: 1, CN: 0]
Initiating SYN Stealth Scan at 19:04
Scanning 10.129.227.156 [20 ports]
Discovered open port 443/tcp on 10.129.227.156
Discovered open port 135/tcp on 10.129.227.156
Discovered open port 80/tcp on 10.129.227.156
Discovered open port 53/tcp on 10.129.227.156
Discovered open port 139/tcp on 10.129.227.156
Discovered open port 8172/tcp on 10.129.227.156
Discovered open port 445/tcp on 10.129.227.156
Discovered open port 636/tcp on 10.129.227.156
Discovered open port 88/tcp on 10.129.227.156
Discovered open port 389/tcp on 10.129.227.156
Discovered open port 593/tcp on 10.129.227.156
Discovered open port 49667/tcp on 10.129.227.156
Discovered open port 49719/tcp on 10.129.227.156
Discovered open port 3269/tcp on 10.129.227.156
Discovered open port 464/tcp on 10.129.227.156
Discovered open port 49704/tcp on 10.129.227.156
Discovered open port 49693/tcp on 10.129.227.156
Discovered open port 3268/tcp on 10.129.227.156
Discovered open port 9389/tcp on 10.129.227.156
Discovered open port 49694/tcp on 10.129.227.156
Completed SYN Stealth Scan at 19:04, 0.51s elapsed (20 total ports)
Initiating Service scan at 19:04
Scanning 20 services on 10.129.227.156
Completed Service scan at 19:05, 56.41s elapsed (20 services on 1 host)
Initiating OS detection (try #1) against 10.129.227.156
Retrying OS detection (try #2) against 10.129.227.156
Initiating Traceroute at 19:05
Completed Traceroute at 19:05, 0.17s elapsed
Initiating Parallel DNS resolution of 2 hosts. at 19:05
Completed Parallel DNS resolution of 2 hosts. at 19:05, 0.00s elapsed
DNS resolution of 2 IPs took 0.00s. Mode: Async [#: 2, OK: 0, NX: 2, DR: 0, SF: 0, TR: 2, CN: 0]
NSE: Script scanning 10.129.227.156.
NSE: Starting runlevel 1 (of 3) scan.
Initiating NSE at 19:05
NSE Timing: About 99.96% done; ETC: 19:05 (0:00:00 remaining)
Completed NSE at 19:05, 40.05s elapsed
NSE: Starting runlevel 2 (of 3) scan.
Initiating NSE at 19:05
Completed NSE at 19:05, 2.62s elapsed
NSE: Starting runlevel 3 (of 3) scan.
Initiating NSE at 19:05
Completed NSE at 19:05, 0.00s elapsed
Nmap scan report for 10.129.227.156
Host is up, received user-set (0.15s latency).
Scanned at 2022-11-10 19:04:10 CST for 105s

PORT      STATE SERVICE       REASON          VERSION
53/tcp    open  domain        syn-ack ttl 127 Simple DNS Plus
80/tcp    open  http          syn-ack ttl 127 Microsoft IIS httpd 10.0
|_http-title: Search &mdash; Just Testing IIS
| http-methods: 
|   Supported Methods: OPTIONS TRACE GET HEAD POST
|_  Potentially risky methods: TRACE
|_http-server-header: Microsoft-IIS/10.0
88/tcp    open  kerberos-sec  syn-ack ttl 127 Microsoft Windows Kerberos (server time: 2022-11-11 01:04:17Z)
135/tcp   open  msrpc         syn-ack ttl 127 Microsoft Windows RPC
139/tcp   open  netbios-ssn   syn-ack ttl 127 Microsoft Windows netbios-ssn
389/tcp   open  ldap          syn-ack ttl 127 Microsoft Windows Active Directory LDAP (Domain: search.htb0., Site: Default-First-Site-Name)
|_ssl-date: 2022-11-11T01:05:53+00:00; 0s from scanner time.
| ssl-cert: Subject: commonName=research
| Issuer: commonName=search-RESEARCH-CA/domainComponent=search
| Public Key type: rsa
| Public Key bits: 2048
| Signature Algorithm: sha256WithRSAEncryption
| Not valid before: 2020-08-11T08:13:35
| Not valid after:  2030-08-09T08:13:35
| MD5:   0738 614f 7bc0 29d0 6d1d 9ea6 3cdb d99e
| SHA-1: 10ae 5494 29d6 1e44 276f b8a2 24ca fde9 de93 af78
| -----BEGIN CERTIFICATE-----
| MIIFZzCCBE+gAwIBAgITVAAAABRx/RXdaDt/5wAAAAAAFDANBgkqhkiG9w0BAQsF
| ADBKMRMwEQYKCZImiZPyLGQBGRYDaHRiMRYwFAYKCZImiZPyLGQBGRYGc2VhcmNo
| MRswGQYDVQQDExJzZWFyY2gtUkVTRUFSQ0gtQ0EwHhcNMjAwODExMDgxMzM1WhcN
| MzAwODA5MDgxMzM1WjAxMRwwGgYDVQQDExNyZXNlYXJjaC5zZWFyY2guaHRiMREw
| DwYDVQQDEwhyZXNlYXJjaDCCASIwDQYJKoZIhvcNAQEBBQADggEPADCCAQoCggEB
| AJryZQO0w3Fil8haWl73Hh2HNnwxC3RxcPGE3QrXLglc2zwp1AsHLAKhUOuAq/Js
| OMyVBQZo13cmRh8l7XOcSXUI4YV/ezXr7GbznlN9NTGooZkzYuMBa21afqTjBgPk
| VYByyfYcECv8TvKI7uc78TpkwpZfmAKi6ha/7o8A1rCSipDvp5wtChLsDK9bsEfl
| nlQbMR8SBQFrWWjXIvCGH2KNkOI56Xz9HV9F2JGwJZNWrHml7BuK18g9sMs0/p7G
| BZxaQLW18zOQnKt3lNo97ovV7A2JljEkknR4MckN4tAEDmOFLvTcdAQ6Y3THvvcr
| UMg24FrX1i8J5WKfjjRdhvkCAwEAAaOCAl0wggJZMDwGCSsGAQQBgjcVBwQvMC0G
| JSsGAQQBgjcVCIqrSYT8vHWlnxuHg8xchZLMMYFpgcOKV4GUuG0CAWQCAQUwEwYD
| VR0lBAwwCgYIKwYBBQUHAwEwDgYDVR0PAQH/BAQDAgWgMBsGCSsGAQQBgjcVCgQO
| MAwwCgYIKwYBBQUHAwEwHQYDVR0OBBYEFFX1E0g3TlBigM7mdF25TuT8fM/dMB8G
| A1UdIwQYMBaAFGqRrXsob7VIpls4zrxiql/nV+xQMIHQBgNVHR8EgcgwgcUwgcKg
| gb+ggbyGgblsZGFwOi8vL0NOPXNlYXJjaC1SRVNFQVJDSC1DQSxDTj1SZXNlYXJj
| aCxDTj1DRFAsQ049UHVibGljJTIwS2V5JTIwU2VydmljZXMsQ049U2VydmljZXMs
| Q049Q29uZmlndXJhdGlvbixEQz1zZWFyY2gsREM9aHRiP2NlcnRpZmljYXRlUmV2
| b2NhdGlvbkxpc3Q/YmFzZT9vYmplY3RDbGFzcz1jUkxEaXN0cmlidXRpb25Qb2lu
| dDCBwwYIKwYBBQUHAQEEgbYwgbMwgbAGCCsGAQUFBzAChoGjbGRhcDovLy9DTj1z
| ZWFyY2gtUkVTRUFSQ0gtQ0EsQ049QUlBLENOPVB1YmxpYyUyMEtleSUyMFNlcnZp
| Y2VzLENOPVNlcnZpY2VzLENOPUNvbmZpZ3VyYXRpb24sREM9c2VhcmNoLERDPWh0
| Yj9jQUNlcnRpZmljYXRlP2Jhc2U/b2JqZWN0Q2xhc3M9Y2VydGlmaWNhdGlvbkF1
| dGhvcml0eTANBgkqhkiG9w0BAQsFAAOCAQEAOkRDrr85ypJJcgefRXJMcVduM0xK
| JT1TzlSgPMw6koXP0a8uR+nLM6dUyU8jfwy5nZDz1SGoOo3X42MTAr6gFomNCj3a
| FgVpTZq90yqTNJEJF9KosUDd47hsBPhw2uu0f4k0UQa/b/+C0Zh5PlBWeoYLSru+
| JcPAWC1o0tQ3MKGogFIGuXYcGcdysM1U+Ho5exQDMTKEiMbSvP9WV52tEnjAvmEe
| 7/lPqiPHGIs7mRW/zXRMq7yDulWUdzAcxZxYzqHQ4k5bQnuVkGEw0d1dcFsoGEKj
| 7pdPzYPnCzHLoO/BDAKJvOrYfI4BPNn2JDBs46CkUwygpiJpL7zIYvCUDQ==
|_-----END CERTIFICATE-----
443/tcp   open  ssl/http      syn-ack ttl 127 Microsoft IIS httpd 10.0
|_ssl-date: 2022-11-11T01:05:53+00:00; 0s from scanner time.
| ssl-cert: Subject: commonName=research
| Issuer: commonName=search-RESEARCH-CA/domainComponent=search
| Public Key type: rsa
| Public Key bits: 2048
| Signature Algorithm: sha256WithRSAEncryption
| Not valid before: 2020-08-11T08:13:35
| Not valid after:  2030-08-09T08:13:35
| MD5:   0738 614f 7bc0 29d0 6d1d 9ea6 3cdb d99e
| SHA-1: 10ae 5494 29d6 1e44 276f b8a2 24ca fde9 de93 af78
| -----BEGIN CERTIFICATE-----
| MIIFZzCCBE+gAwIBAgITVAAAABRx/RXdaDt/5wAAAAAAFDANBgkqhkiG9w0BAQsF
| ADBKMRMwEQYKCZImiZPyLGQBGRYDaHRiMRYwFAYKCZImiZPyLGQBGRYGc2VhcmNo
| MRswGQYDVQQDExJzZWFyY2gtUkVTRUFSQ0gtQ0EwHhcNMjAwODExMDgxMzM1WhcN
| MzAwODA5MDgxMzM1WjAxMRwwGgYDVQQDExNyZXNlYXJjaC5zZWFyY2guaHRiMREw
| DwYDVQQDEwhyZXNlYXJjaDCCASIwDQYJKoZIhvcNAQEBBQADggEPADCCAQoCggEB
| AJryZQO0w3Fil8haWl73Hh2HNnwxC3RxcPGE3QrXLglc2zwp1AsHLAKhUOuAq/Js
| OMyVBQZo13cmRh8l7XOcSXUI4YV/ezXr7GbznlN9NTGooZkzYuMBa21afqTjBgPk
| VYByyfYcECv8TvKI7uc78TpkwpZfmAKi6ha/7o8A1rCSipDvp5wtChLsDK9bsEfl
| nlQbMR8SBQFrWWjXIvCGH2KNkOI56Xz9HV9F2JGwJZNWrHml7BuK18g9sMs0/p7G
| BZxaQLW18zOQnKt3lNo97ovV7A2JljEkknR4MckN4tAEDmOFLvTcdAQ6Y3THvvcr
| UMg24FrX1i8J5WKfjjRdhvkCAwEAAaOCAl0wggJZMDwGCSsGAQQBgjcVBwQvMC0G
| JSsGAQQBgjcVCIqrSYT8vHWlnxuHg8xchZLMMYFpgcOKV4GUuG0CAWQCAQUwEwYD
| VR0lBAwwCgYIKwYBBQUHAwEwDgYDVR0PAQH/BAQDAgWgMBsGCSsGAQQBgjcVCgQO
| MAwwCgYIKwYBBQUHAwEwHQYDVR0OBBYEFFX1E0g3TlBigM7mdF25TuT8fM/dMB8G
| A1UdIwQYMBaAFGqRrXsob7VIpls4zrxiql/nV+xQMIHQBgNVHR8EgcgwgcUwgcKg
| gb+ggbyGgblsZGFwOi8vL0NOPXNlYXJjaC1SRVNFQVJDSC1DQSxDTj1SZXNlYXJj
| aCxDTj1DRFAsQ049UHVibGljJTIwS2V5JTIwU2VydmljZXMsQ049U2VydmljZXMs
| Q049Q29uZmlndXJhdGlvbixEQz1zZWFyY2gsREM9aHRiP2NlcnRpZmljYXRlUmV2
| b2NhdGlvbkxpc3Q/YmFzZT9vYmplY3RDbGFzcz1jUkxEaXN0cmlidXRpb25Qb2lu
| dDCBwwYIKwYBBQUHAQEEgbYwgbMwgbAGCCsGAQUFBzAChoGjbGRhcDovLy9DTj1z
| ZWFyY2gtUkVTRUFSQ0gtQ0EsQ049QUlBLENOPVB1YmxpYyUyMEtleSUyMFNlcnZp
| Y2VzLENOPVNlcnZpY2VzLENOPUNvbmZpZ3VyYXRpb24sREM9c2VhcmNoLERDPWh0
| Yj9jQUNlcnRpZmljYXRlP2Jhc2U/b2JqZWN0Q2xhc3M9Y2VydGlmaWNhdGlvbkF1
| dGhvcml0eTANBgkqhkiG9w0BAQsFAAOCAQEAOkRDrr85ypJJcgefRXJMcVduM0xK
| JT1TzlSgPMw6koXP0a8uR+nLM6dUyU8jfwy5nZDz1SGoOo3X42MTAr6gFomNCj3a
| FgVpTZq90yqTNJEJF9KosUDd47hsBPhw2uu0f4k0UQa/b/+C0Zh5PlBWeoYLSru+
| JcPAWC1o0tQ3MKGogFIGuXYcGcdysM1U+Ho5exQDMTKEiMbSvP9WV52tEnjAvmEe
| 7/lPqiPHGIs7mRW/zXRMq7yDulWUdzAcxZxYzqHQ4k5bQnuVkGEw0d1dcFsoGEKj
| 7pdPzYPnCzHLoO/BDAKJvOrYfI4BPNn2JDBs46CkUwygpiJpL7zIYvCUDQ==
|_-----END CERTIFICATE-----
| http-methods: 
|   Supported Methods: OPTIONS TRACE GET HEAD POST
|_  Potentially risky methods: TRACE
|_http-title: Search &mdash; Just Testing IIS
|_http-server-header: Microsoft-IIS/10.0
| tls-alpn: 
|_  http/1.1
445/tcp   open  microsoft-ds? syn-ack ttl 127
464/tcp   open  kpasswd5?     syn-ack ttl 127
593/tcp   open  ncacn_http    syn-ack ttl 127 Microsoft Windows RPC over HTTP 1.0
636/tcp   open  ssl/ldap      syn-ack ttl 127 Microsoft Windows Active Directory LDAP (Domain: search.htb0., Site: Default-First-Site-Name)
|_ssl-date: 2022-11-11T01:05:53+00:00; 0s from scanner time.
| ssl-cert: Subject: commonName=research
| Issuer: commonName=search-RESEARCH-CA/domainComponent=search
| Public Key type: rsa
| Public Key bits: 2048
| Signature Algorithm: sha256WithRSAEncryption
| Not valid before: 2020-08-11T08:13:35
| Not valid after:  2030-08-09T08:13:35
| MD5:   0738 614f 7bc0 29d0 6d1d 9ea6 3cdb d99e
| SHA-1: 10ae 5494 29d6 1e44 276f b8a2 24ca fde9 de93 af78
| -----BEGIN CERTIFICATE-----
| MIIFZzCCBE+gAwIBAgITVAAAABRx/RXdaDt/5wAAAAAAFDANBgkqhkiG9w0BAQsF
| ADBKMRMwEQYKCZImiZPyLGQBGRYDaHRiMRYwFAYKCZImiZPyLGQBGRYGc2VhcmNo
| MRswGQYDVQQDExJzZWFyY2gtUkVTRUFSQ0gtQ0EwHhcNMjAwODExMDgxMzM1WhcN
| MzAwODA5MDgxMzM1WjAxMRwwGgYDVQQDExNyZXNlYXJjaC5zZWFyY2guaHRiMREw
| DwYDVQQDEwhyZXNlYXJjaDCCASIwDQYJKoZIhvcNAQEBBQADggEPADCCAQoCggEB
| AJryZQO0w3Fil8haWl73Hh2HNnwxC3RxcPGE3QrXLglc2zwp1AsHLAKhUOuAq/Js
| OMyVBQZo13cmRh8l7XOcSXUI4YV/ezXr7GbznlN9NTGooZkzYuMBa21afqTjBgPk
| VYByyfYcECv8TvKI7uc78TpkwpZfmAKi6ha/7o8A1rCSipDvp5wtChLsDK9bsEfl
| nlQbMR8SBQFrWWjXIvCGH2KNkOI56Xz9HV9F2JGwJZNWrHml7BuK18g9sMs0/p7G
| BZxaQLW18zOQnKt3lNo97ovV7A2JljEkknR4MckN4tAEDmOFLvTcdAQ6Y3THvvcr
| UMg24FrX1i8J5WKfjjRdhvkCAwEAAaOCAl0wggJZMDwGCSsGAQQBgjcVBwQvMC0G
| JSsGAQQBgjcVCIqrSYT8vHWlnxuHg8xchZLMMYFpgcOKV4GUuG0CAWQCAQUwEwYD
| VR0lBAwwCgYIKwYBBQUHAwEwDgYDVR0PAQH/BAQDAgWgMBsGCSsGAQQBgjcVCgQO
| MAwwCgYIKwYBBQUHAwEwHQYDVR0OBBYEFFX1E0g3TlBigM7mdF25TuT8fM/dMB8G
| A1UdIwQYMBaAFGqRrXsob7VIpls4zrxiql/nV+xQMIHQBgNVHR8EgcgwgcUwgcKg
| gb+ggbyGgblsZGFwOi8vL0NOPXNlYXJjaC1SRVNFQVJDSC1DQSxDTj1SZXNlYXJj
| aCxDTj1DRFAsQ049UHVibGljJTIwS2V5JTIwU2VydmljZXMsQ049U2VydmljZXMs
| Q049Q29uZmlndXJhdGlvbixEQz1zZWFyY2gsREM9aHRiP2NlcnRpZmljYXRlUmV2
| b2NhdGlvbkxpc3Q/YmFzZT9vYmplY3RDbGFzcz1jUkxEaXN0cmlidXRpb25Qb2lu
| dDCBwwYIKwYBBQUHAQEEgbYwgbMwgbAGCCsGAQUFBzAChoGjbGRhcDovLy9DTj1z
| ZWFyY2gtUkVTRUFSQ0gtQ0EsQ049QUlBLENOPVB1YmxpYyUyMEtleSUyMFNlcnZp
| Y2VzLENOPVNlcnZpY2VzLENOPUNvbmZpZ3VyYXRpb24sREM9c2VhcmNoLERDPWh0
| Yj9jQUNlcnRpZmljYXRlP2Jhc2U/b2JqZWN0Q2xhc3M9Y2VydGlmaWNhdGlvbkF1
| dGhvcml0eTANBgkqhkiG9w0BAQsFAAOCAQEAOkRDrr85ypJJcgefRXJMcVduM0xK
| JT1TzlSgPMw6koXP0a8uR+nLM6dUyU8jfwy5nZDz1SGoOo3X42MTAr6gFomNCj3a
| FgVpTZq90yqTNJEJF9KosUDd47hsBPhw2uu0f4k0UQa/b/+C0Zh5PlBWeoYLSru+
| JcPAWC1o0tQ3MKGogFIGuXYcGcdysM1U+Ho5exQDMTKEiMbSvP9WV52tEnjAvmEe
| 7/lPqiPHGIs7mRW/zXRMq7yDulWUdzAcxZxYzqHQ4k5bQnuVkGEw0d1dcFsoGEKj
| 7pdPzYPnCzHLoO/BDAKJvOrYfI4BPNn2JDBs46CkUwygpiJpL7zIYvCUDQ==
|_-----END CERTIFICATE-----
3268/tcp  open  ldap          syn-ack ttl 127 Microsoft Windows Active Directory LDAP (Domain: search.htb0., Site: Default-First-Site-Name)
|_ssl-date: 2022-11-11T01:05:53+00:00; 0s from scanner time.
| ssl-cert: Subject: commonName=research
| Issuer: commonName=search-RESEARCH-CA/domainComponent=search
| Public Key type: rsa
| Public Key bits: 2048
| Signature Algorithm: sha256WithRSAEncryption
| Not valid before: 2020-08-11T08:13:35
| Not valid after:  2030-08-09T08:13:35
| MD5:   0738 614f 7bc0 29d0 6d1d 9ea6 3cdb d99e
| SHA-1: 10ae 5494 29d6 1e44 276f b8a2 24ca fde9 de93 af78
| -----BEGIN CERTIFICATE-----
| MIIFZzCCBE+gAwIBAgITVAAAABRx/RXdaDt/5wAAAAAAFDANBgkqhkiG9w0BAQsF
| ADBKMRMwEQYKCZImiZPyLGQBGRYDaHRiMRYwFAYKCZImiZPyLGQBGRYGc2VhcmNo
| MRswGQYDVQQDExJzZWFyY2gtUkVTRUFSQ0gtQ0EwHhcNMjAwODExMDgxMzM1WhcN
| MzAwODA5MDgxMzM1WjAxMRwwGgYDVQQDExNyZXNlYXJjaC5zZWFyY2guaHRiMREw
| DwYDVQQDEwhyZXNlYXJjaDCCASIwDQYJKoZIhvcNAQEBBQADggEPADCCAQoCggEB
| AJryZQO0w3Fil8haWl73Hh2HNnwxC3RxcPGE3QrXLglc2zwp1AsHLAKhUOuAq/Js
| OMyVBQZo13cmRh8l7XOcSXUI4YV/ezXr7GbznlN9NTGooZkzYuMBa21afqTjBgPk
| VYByyfYcECv8TvKI7uc78TpkwpZfmAKi6ha/7o8A1rCSipDvp5wtChLsDK9bsEfl
| nlQbMR8SBQFrWWjXIvCGH2KNkOI56Xz9HV9F2JGwJZNWrHml7BuK18g9sMs0/p7G
| BZxaQLW18zOQnKt3lNo97ovV7A2JljEkknR4MckN4tAEDmOFLvTcdAQ6Y3THvvcr
| UMg24FrX1i8J5WKfjjRdhvkCAwEAAaOCAl0wggJZMDwGCSsGAQQBgjcVBwQvMC0G
| JSsGAQQBgjcVCIqrSYT8vHWlnxuHg8xchZLMMYFpgcOKV4GUuG0CAWQCAQUwEwYD
| VR0lBAwwCgYIKwYBBQUHAwEwDgYDVR0PAQH/BAQDAgWgMBsGCSsGAQQBgjcVCgQO
| MAwwCgYIKwYBBQUHAwEwHQYDVR0OBBYEFFX1E0g3TlBigM7mdF25TuT8fM/dMB8G
| A1UdIwQYMBaAFGqRrXsob7VIpls4zrxiql/nV+xQMIHQBgNVHR8EgcgwgcUwgcKg
| gb+ggbyGgblsZGFwOi8vL0NOPXNlYXJjaC1SRVNFQVJDSC1DQSxDTj1SZXNlYXJj
| aCxDTj1DRFAsQ049UHVibGljJTIwS2V5JTIwU2VydmljZXMsQ049U2VydmljZXMs
| Q049Q29uZmlndXJhdGlvbixEQz1zZWFyY2gsREM9aHRiP2NlcnRpZmljYXRlUmV2
| b2NhdGlvbkxpc3Q/YmFzZT9vYmplY3RDbGFzcz1jUkxEaXN0cmlidXRpb25Qb2lu
| dDCBwwYIKwYBBQUHAQEEgbYwgbMwgbAGCCsGAQUFBzAChoGjbGRhcDovLy9DTj1z
| ZWFyY2gtUkVTRUFSQ0gtQ0EsQ049QUlBLENOPVB1YmxpYyUyMEtleSUyMFNlcnZp
| Y2VzLENOPVNlcnZpY2VzLENOPUNvbmZpZ3VyYXRpb24sREM9c2VhcmNoLERDPWh0
| Yj9jQUNlcnRpZmljYXRlP2Jhc2U/b2JqZWN0Q2xhc3M9Y2VydGlmaWNhdGlvbkF1
| dGhvcml0eTANBgkqhkiG9w0BAQsFAAOCAQEAOkRDrr85ypJJcgefRXJMcVduM0xK
| JT1TzlSgPMw6koXP0a8uR+nLM6dUyU8jfwy5nZDz1SGoOo3X42MTAr6gFomNCj3a
| FgVpTZq90yqTNJEJF9KosUDd47hsBPhw2uu0f4k0UQa/b/+C0Zh5PlBWeoYLSru+
| JcPAWC1o0tQ3MKGogFIGuXYcGcdysM1U+Ho5exQDMTKEiMbSvP9WV52tEnjAvmEe
| 7/lPqiPHGIs7mRW/zXRMq7yDulWUdzAcxZxYzqHQ4k5bQnuVkGEw0d1dcFsoGEKj
| 7pdPzYPnCzHLoO/BDAKJvOrYfI4BPNn2JDBs46CkUwygpiJpL7zIYvCUDQ==
|_-----END CERTIFICATE-----
3269/tcp  open  ssl/ldap      syn-ack ttl 127 Microsoft Windows Active Directory LDAP (Domain: search.htb0., Site: Default-First-Site-Name)
|_ssl-date: 2022-11-11T01:05:53+00:00; 0s from scanner time.
| ssl-cert: Subject: commonName=research
| Issuer: commonName=search-RESEARCH-CA/domainComponent=search
| Public Key type: rsa
| Public Key bits: 2048
| Signature Algorithm: sha256WithRSAEncryption
| Not valid before: 2020-08-11T08:13:35
| Not valid after:  2030-08-09T08:13:35
| MD5:   0738 614f 7bc0 29d0 6d1d 9ea6 3cdb d99e
| SHA-1: 10ae 5494 29d6 1e44 276f b8a2 24ca fde9 de93 af78
| -----BEGIN CERTIFICATE-----
| MIIFZzCCBE+gAwIBAgITVAAAABRx/RXdaDt/5wAAAAAAFDANBgkqhkiG9w0BAQsF
| ADBKMRMwEQYKCZImiZPyLGQBGRYDaHRiMRYwFAYKCZImiZPyLGQBGRYGc2VhcmNo
| MRswGQYDVQQDExJzZWFyY2gtUkVTRUFSQ0gtQ0EwHhcNMjAwODExMDgxMzM1WhcN
| MzAwODA5MDgxMzM1WjAxMRwwGgYDVQQDExNyZXNlYXJjaC5zZWFyY2guaHRiMREw
| DwYDVQQDEwhyZXNlYXJjaDCCASIwDQYJKoZIhvcNAQEBBQADggEPADCCAQoCggEB
| AJryZQO0w3Fil8haWl73Hh2HNnwxC3RxcPGE3QrXLglc2zwp1AsHLAKhUOuAq/Js
| OMyVBQZo13cmRh8l7XOcSXUI4YV/ezXr7GbznlN9NTGooZkzYuMBa21afqTjBgPk
| VYByyfYcECv8TvKI7uc78TpkwpZfmAKi6ha/7o8A1rCSipDvp5wtChLsDK9bsEfl
| nlQbMR8SBQFrWWjXIvCGH2KNkOI56Xz9HV9F2JGwJZNWrHml7BuK18g9sMs0/p7G
| BZxaQLW18zOQnKt3lNo97ovV7A2JljEkknR4MckN4tAEDmOFLvTcdAQ6Y3THvvcr
| UMg24FrX1i8J5WKfjjRdhvkCAwEAAaOCAl0wggJZMDwGCSsGAQQBgjcVBwQvMC0G
| JSsGAQQBgjcVCIqrSYT8vHWlnxuHg8xchZLMMYFpgcOKV4GUuG0CAWQCAQUwEwYD
| VR0lBAwwCgYIKwYBBQUHAwEwDgYDVR0PAQH/BAQDAgWgMBsGCSsGAQQBgjcVCgQO
| MAwwCgYIKwYBBQUHAwEwHQYDVR0OBBYEFFX1E0g3TlBigM7mdF25TuT8fM/dMB8G
| A1UdIwQYMBaAFGqRrXsob7VIpls4zrxiql/nV+xQMIHQBgNVHR8EgcgwgcUwgcKg
| gb+ggbyGgblsZGFwOi8vL0NOPXNlYXJjaC1SRVNFQVJDSC1DQSxDTj1SZXNlYXJj
| aCxDTj1DRFAsQ049UHVibGljJTIwS2V5JTIwU2VydmljZXMsQ049U2VydmljZXMs
| Q049Q29uZmlndXJhdGlvbixEQz1zZWFyY2gsREM9aHRiP2NlcnRpZmljYXRlUmV2
| b2NhdGlvbkxpc3Q/YmFzZT9vYmplY3RDbGFzcz1jUkxEaXN0cmlidXRpb25Qb2lu
| dDCBwwYIKwYBBQUHAQEEgbYwgbMwgbAGCCsGAQUFBzAChoGjbGRhcDovLy9DTj1z
| ZWFyY2gtUkVTRUFSQ0gtQ0EsQ049QUlBLENOPVB1YmxpYyUyMEtleSUyMFNlcnZp
| Y2VzLENOPVNlcnZpY2VzLENOPUNvbmZpZ3VyYXRpb24sREM9c2VhcmNoLERDPWh0
| Yj9jQUNlcnRpZmljYXRlP2Jhc2U/b2JqZWN0Q2xhc3M9Y2VydGlmaWNhdGlvbkF1
| dGhvcml0eTANBgkqhkiG9w0BAQsFAAOCAQEAOkRDrr85ypJJcgefRXJMcVduM0xK
| JT1TzlSgPMw6koXP0a8uR+nLM6dUyU8jfwy5nZDz1SGoOo3X42MTAr6gFomNCj3a
| FgVpTZq90yqTNJEJF9KosUDd47hsBPhw2uu0f4k0UQa/b/+C0Zh5PlBWeoYLSru+
| JcPAWC1o0tQ3MKGogFIGuXYcGcdysM1U+Ho5exQDMTKEiMbSvP9WV52tEnjAvmEe
| 7/lPqiPHGIs7mRW/zXRMq7yDulWUdzAcxZxYzqHQ4k5bQnuVkGEw0d1dcFsoGEKj
| 7pdPzYPnCzHLoO/BDAKJvOrYfI4BPNn2JDBs46CkUwygpiJpL7zIYvCUDQ==
|_-----END CERTIFICATE-----
8172/tcp  open  ssl/http      syn-ack ttl 127 Microsoft IIS httpd 10.0
|_http-title: Site doesn't have a title.
|_http-server-header: Microsoft-IIS/10.0
| tls-alpn: 
|_  http/1.1
|_ssl-date: 2022-11-11T01:05:53+00:00; 0s from scanner time.
| ssl-cert: Subject: commonName=WMSvc-SHA2-RESEARCH
| Issuer: commonName=WMSvc-SHA2-RESEARCH
| Public Key type: rsa
| Public Key bits: 2048
| Signature Algorithm: sha256WithRSAEncryption
| Not valid before: 2020-04-07T09:05:25
| Not valid after:  2030-04-05T09:05:25
| MD5:   eeb9 303e 6d46 bd8b 34a0 1ed6 0eb8 3287
| SHA-1: 1e06 9fd0 ef45 b051 78b2 c6bf 1bed 975e a87d 0458
| -----BEGIN CERTIFICATE-----
| MIIC7TCCAdWgAwIBAgIQcJlfxrPWrqJOzFjgO04PijANBgkqhkiG9w0BAQsFADAe
| MRwwGgYDVQQDExNXTVN2Yy1TSEEyLVJFU0VBUkNIMB4XDTIwMDQwNzA5MDUyNVoX
| DTMwMDQwNTA5MDUyNVowHjEcMBoGA1UEAxMTV01TdmMtU0hBMi1SRVNFQVJDSDCC
| ASIwDQYJKoZIhvcNAQEBBQADggEPADCCAQoCggEBALXrSYHlRsq+HX01zrmC6Ddi
| /+vL/iDzS9endY3CRjfTjBL85qwvU5dkS+cxYTIkDaK5M9eoLcaVSARIcyrGIGuq
| DwIFQuYuaoGeQgiaQCqU5vXgsZ/xE8DRmlnZ2DeiAcHhx72TOHoUoUP4q2EqRoVr
| q5RCBGITT7hdRQd0vuTIHoLxdO2U5wZVCoN5vsp0Du43/LCgXExUpcHAHu9aVAzt
| pXWFY8B3XEFZjafffOHXiK6C2UzX4DddYweKR+ItMfQzX8T2MbX1qVm7D526/gU9
| WRGa7F/tj8+qvzZc4SQZ6Td9PWpMKCPGqqYTGmHlEW8ZowGoMSH62QaCilFxckEC
| AwEAAaMnMCUwEwYDVR0lBAwwCgYIKwYBBQUHAwEwDgYDVR0PBAcDBQCwAAAAMA0G
| CSqGSIb3DQEBCwUAA4IBAQAlGUrh9gLK7Er/BzEjyWebPPf18m3XxgZ13iFllhJ0
| 5tBUb3hczHIr3VOj/OWUJygxw8O10OrBZJZf29TPZ2nXKGbJRpYe+baii49LsGjr
| DiOM5XVZv5qiPBNts7fKyhpzTy0DdnIKAXUIYy/7nQ6rHetXApz89ZEzU6vAN0g0
| Zxq/NolqIVnehFn/36tjc65v1wgo6KnHAQUt6zWufueeYS3k2f4JzvFn4aPtUYRi
| nQgTuGbJTlxdVJ5DJjld9pLyJ+OctGeI1jRITiYlu5p3JwhxU0+mQjGT5mQZ+Umu
| abMpffugMOPYnyHu8poRZWjKgNBN0ygmnqGbTjx57No5
|_-----END CERTIFICATE-----
9389/tcp  open  mc-nmf        syn-ack ttl 127 .NET Message Framing
49667/tcp open  msrpc         syn-ack ttl 127 Microsoft Windows RPC
49693/tcp open  ncacn_http    syn-ack ttl 127 Microsoft Windows RPC over HTTP 1.0
49694/tcp open  msrpc         syn-ack ttl 127 Microsoft Windows RPC
49704/tcp open  msrpc         syn-ack ttl 127 Microsoft Windows RPC
49719/tcp open  msrpc         syn-ack ttl 127 Microsoft Windows RPC
Warning: OSScan results may be unreliable because we could not find at least 1 open and 1 closed port
OS fingerprint not ideal because: Missing a closed TCP port so results incomplete
No OS matches for host
TCP/IP fingerprint:
SCAN(V=7.92%E=4%D=11/10%OT=53%CT=%CU=%PV=Y%DS=2%DC=T%G=N%TM=636D9FF3%P=x86_64-pc-linux-gnu)
SEQ(SP=100%GCD=2%ISR=10E%TI=I%II=I%SS=S%TS=U)
OPS(O1=M53ANW8NNS%O2=M53ANW8NNS%O3=M53ANW8%O4=M53ANW8NNS%O5=M53ANW8NNS%O6=M53ANNS)
WIN(W1=FFFF%W2=FFFF%W3=FFFF%W4=FFFF%W5=FFFF%W6=FF70)
ECN(R=Y%DF=Y%TG=80%W=FFFF%O=M53ANW8NNS%CC=Y%Q=)
T1(R=Y%DF=Y%TG=80%S=O%A=S+%F=AS%RD=0%Q=)
T2(R=N)
T3(R=N)
T4(R=N)
U1(R=N)
IE(R=Y%DFI=N%TG=80%CD=Z)

Network Distance: 2 hops
TCP Sequence Prediction: Difficulty=256 (Good luck!)
IP ID Sequence Generation: Incremental
Service Info: Host: RESEARCH; OS: Windows; CPE: cpe:/o:microsoft:windows

Host script results:
| smb2-security-mode: 
|   3.1.1: 
|_    Message signing enabled and required
|_clock-skew: mean: 0s, deviation: 0s, median: 0s
| smb2-time: 
|   date: 2022-11-11T01:05:15
|_  start_date: N/A
| p2p-conficker: 
|   Checking for Conficker.C or higher...
|   Check 1 (port 49396/tcp): CLEAN (Timeout)
|   Check 2 (port 16314/tcp): CLEAN (Timeout)
|   Check 3 (port 21718/udp): CLEAN (Timeout)
|   Check 4 (port 64855/udp): CLEAN (Timeout)
|_  0/4 checks are positive: Host is CLEAN or ports are blocked

TRACEROUTE (using port 443/tcp)
HOP RTT       ADDRESS
1   163.77 ms 10.10.16.1
2   163.94 ms 10.129.227.156

NSE: Script Post-scanning.
NSE: Starting runlevel 1 (of 3) scan.
Initiating NSE at 19:05
Completed NSE at 19:05, 0.00s elapsed
NSE: Starting runlevel 2 (of 3) scan.
Initiating NSE at 19:05
Completed NSE at 19:05, 0.00s elapsed
NSE: Starting runlevel 3 (of 3) scan.
Initiating NSE at 19:05
Completed NSE at 19:05, 0.00s elapsed
Read data files from: /usr/bin/../share/nmap
OS and Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 105.78 seconds
           Raw packets sent: 104 (8.284KB) | Rcvd: 52 (2.872KB)
```

_Initial Shell_

_Additional info about where the initial shell was acquired from_

**Vulnerability Explanation:**

**Vulnerability Fix:**

**Severity:**

**Proof of Concept Code Here:**

**Local.txt Proof Screenshot**

**Local.txt Contents**

**Privilege Escalation**

_Additional Priv Esc info_

**Vulnerability Exploited:**

**Vulnerability Explanation:**

**Vulnerability Fix:**

**Severity: Critical**

**Exploit Code:**

**Proof Screenshot Here:**

**Proof.txt Contents:**

**Post Exploitation**

### Maintaining Access

Maintaining access to a system is important to us as attackers, ensuring that we can get back into a system after it has been exploited is invaluable. The maintaining access phase of the penetration test focuses on ensuring that once the focused attack has occurred (i.e. a buffer overflow), we have administrative access over the system again. Many exploits may only be exploitable once and we may never be able to get back into a system after we have already performed the exploit.

### House Cleaning

The house cleaning portions of the assessment ensures that remnants of the penetration test are removed. Often fragments of tools or user accounts are left on an organization's computer which can cause security issues down the road. Ensuring that we are meticulous and no remnants of our penetration test are left over is important.

After collecting data from the network was completed, I removed all user accounts and passwords as well as the Meterpreter services installed on the system. the client should not have to remove any user accounts or services from the system.

## Additional Items

### Appendix - Proof and Local Contents:

| IP (Hostname) | Local.txt Contents | Proof.txt Contents |
| ------------- | ------------------ | ------------------ |
| x.x.x.x       | hash\_here         | hash\_here         |

### Appendix - Metasploit/Meterpreter Usage

For the pentest, I used my Metasploit/Meterpreter allowance on the following machine: `No Metasploit/Meterpreter was used during engagment`

### Appendix - Completed Buffer Overflow Code

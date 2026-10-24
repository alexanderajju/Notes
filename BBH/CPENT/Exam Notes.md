
AD Range

Please drop email to practicals@eccouncil.org for the information.

![[Pasted image 20261009105310.png]]

Range:  172.25.170.0/24
**Exclusion**: 172.25.170.1, 172.25.170.250


```bash
sudo nmap -sn -T 4  172.25.170.0/24                       
[sudo] password for aju: 
Starting Nmap 7.95 ( https://nmap.org ) at 2026-10-09 10:54 IST
Nmap scan report for 172.25.170.12
Host is up (0.23s latency).
Nmap scan report for 172.25.170.50
Host is up (0.22s latency).
Nmap scan report for 172.25.170.140
Host is up (0.23s latency).
Nmap scan report for 172.25.170.200
Host is up (0.23s latency).
Nmap scan report for 172.25.170.250 
Host is up (0.22s latency).
Nmap done: 256 IP addresses (5 hosts up) scanned in 14.26 seconds

```


172.25.170.12


```bash
 nmap 172.25.170.12
                                    
Starting Nmap 7.95 ( https://nmap.org ) at 2026-10-09 10:55 IST
Nmap scan report for 172.25.170.12
Host is up (0.22s latency).
Not shown: 980 closed tcp ports (conn-refused)
PORT     STATE SERVICE
25/tcp   open  smtp
53/tcp   open  domain
80/tcp   open  http
88/tcp   open  kerberos-sec
135/tcp  open  msrpc
139/tcp  open  netbios-ssn
389/tcp  open  ldap
445/tcp  open  microsoft-ds
464/tcp  open  kpasswd5
593/tcp  open  http-rpc-epmap
636/tcp  open  ldapssl
1433/tcp open  ms-sql-s
1801/tcp open  msmq
2103/tcp open  zephyr-clt
2105/tcp open  eklogin
2107/tcp open  msmq-mgmt
3268/tcp open  globalcatLDAP
3269/tcp open  globalcatLDAPssl
3389/tcp open  ms-wbt-server
5985/tcp open  wsman


## full scan

PORT     STATE SERVICE       REASON          VERSION
25/tcp   open  smtp          syn-ack ttl 126 Microsoft ESMTP 10.0.17763.1
| smtp-commands: RangeADServer19.CPENTv2025.com Hello [172.27.232.2], TURN, SIZE 2097152, ETRN, PIPELINING, DSN, ENHANCEDSTATUSCODES, 8bitmime, BINARYMIME, CHUNKING, VRFY, OK
|_ This server supports the following commands: HELO EHLO STARTTLS RCPT DATA RSET MAIL QUIT HELP AUTH TURN ETRN BDAT VRFY
53/tcp   open  domain        syn-ack ttl 126 Simple DNS Plus
80/tcp   open  http          syn-ack ttl 126 Microsoft IIS httpd 10.0
|_http-server-header: Microsoft-IIS/10.0
| http-methods: 
|_  Potentially risky methods: TRACE
|_http-title: IIS Windows Server
88/tcp   open  kerberos-sec  syn-ack ttl 126 Microsoft Windows Kerberos (server time: 2026-10-09 05:35:20Z)
135/tcp  open  msrpc         syn-ack ttl 126 Microsoft Windows RPC
139/tcp  open  netbios-ssn   syn-ack ttl 126 Microsoft Windows netbios-ssn
389/tcp  open  ldap          syn-ack ttl 126 Microsoft Windows Active Directory LDAP (Domain: CPENTv2025.com0., Site: Default-First-Site-Name)
445/tcp  open  microsoft-ds? syn-ack ttl 126
464/tcp  open  kpasswd5?     syn-ack ttl 126
593/tcp  open  ncacn_http    syn-ack ttl 126 Microsoft Windows RPC over HTTP 1.0
636/tcp  open  tcpwrapped    syn-ack ttl 126
1433/tcp open  ms-sql-s      syn-ack ttl 126 Microsoft SQL Server 2022
| ssl-cert: Subject: commonName=SSL_Self_Signed_Fallback
| Not valid before: 2026-10-09T05:17:37
|_Not valid after:  2056-10-09T05:17:37
|_ssl-date: 2026-10-09T05:36:23+00:00; 0s from scanner time.
|_ms-sql-info: ERROR: Script execution failed (use -d to debug)
|_ms-sql-ntlm-info: ERROR: Script execution failed (use -d to debug)
1801/tcp open  msmq?         syn-ack ttl 126
2103/tcp open  msrpc         syn-ack ttl 126 Microsoft Windows RPC
2105/tcp open  msrpc         syn-ack ttl 126 Microsoft Windows RPC
2107/tcp open  msrpc         syn-ack ttl 126 Microsoft Windows RPC
3268/tcp open  ldap          syn-ack ttl 126 Microsoft Windows Active Directory LDAP (Domain: CPENTv2025.com0., Site: Default-First-Site-Name)
3269/tcp open  tcpwrapped    syn-ack ttl 126
3389/tcp open  ms-wbt-server syn-ack ttl 126 Microsoft Terminal Services
|_ssl-date: 2026-10-09T05:36:23+00:00; 0s from scanner time.
| rdp-ntlm-info: 
|   Target_Name: CPENTV2025
|   NetBIOS_Domain_Name: CPENTV2025
|   NetBIOS_Computer_Name: RANGEADSERVER19
|   DNS_Domain_Name: CPENTv2025.com
|   DNS_Computer_Name: RangeADServer19.CPENTv2025.com
|   Product_Version: 10.0.17763
|_  System_Time: 2026-10-09T05:36:14+00:00
| ssl-cert: Subject: commonName=RangeADServer19.CPENTv2025.com
| Not valid before: 2026-06-22T06:43:13
|_Not valid after:  2026-12-22T06:43:13
5985/tcp open  http          syn-ack ttl 126 Microsoft HTTPAPI httpd 2.0 (SSDP/UPnP)
|_http-server-header: Microsoft-HTTPAPI/2.0
|_http-title: Not Found
Service Info: Hosts: RangeADServer19.CPENTv2025.com, RANGEADSERVER19; OS: Windows; CPE: cpe:/o:microsoft:windows

Host script results:
| smb2-time: 
|   date: 2026-10-09T05:36:16
|_  start_date: N/A
| smb2-security-mode: 
|   3:1:1: 
|_    Message signing enabled and required

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 83.17 seconds



```


172.25.170.50


```bash

sudo nmap -Pn -n 172.25.170.50 
Starting Nmap 7.95 ( https://nmap.org ) at 2026-10-09 10:57 IST
Nmap scan report for 172.25.170.50
Host is up (0.22s latency).
Not shown: 988 filtered tcp ports (no-response)
PORT     STATE SERVICE
53/tcp   open  domain
88/tcp   open  kerberos-sec
135/tcp  open  msrpc
139/tcp  open  netbios-ssn
389/tcp  open  ldap
445/tcp  open  microsoft-ds
464/tcp  open  kpasswd5
593/tcp  open  http-rpc-epmap
636/tcp  open  ldapssl
3268/tcp open  globalcatLDAP
3269/tcp open  globalcatLDAPssl
3389/tcp open  ms-wbt-server

#full scan

PORT     STATE SERVICE       REASON          VERSION
53/tcp   open  domain        syn-ack ttl 126 Simple DNS Plus
88/tcp   open  kerberos-sec  syn-ack ttl 126 Microsoft Windows Kerberos (server time: 2026-10-09 05:38:33Z)
135/tcp  open  msrpc         syn-ack ttl 126 Microsoft Windows RPC
139/tcp  open  netbios-ssn   syn-ack ttl 126 Microsoft Windows netbios-ssn
389/tcp  open  ldap          syn-ack ttl 126 Microsoft Windows Active Directory LDAP (Domain: CPENTv2025.com, Site: Default-First-Site-Name)
445/tcp  open  microsoft-ds  syn-ack ttl 126 Windows Server 2016 Datacenter 14393 microsoft-ds (workgroup: CPENTV2025)
464/tcp  open  kpasswd5?     syn-ack ttl 126
593/tcp  open  ncacn_http    syn-ack ttl 126 Microsoft Windows RPC over HTTP 1.0
636/tcp  open  tcpwrapped    syn-ack ttl 126
3268/tcp open  ldap          syn-ack ttl 126 Microsoft Windows Active Directory LDAP (Domain: CPENTv2025.com, Site: Default-First-Site-Name)
3269/tcp open  tcpwrapped    syn-ack ttl 126
3389/tcp open  ms-wbt-server syn-ack ttl 126 Microsoft Terminal Services
|_ssl-date: 2026-10-09T05:39:27+00:00; 0s from scanner time.
| ssl-cert: Subject: commonName=AD-WIN.CPENTv2025.com
| Not valid before: 2026-07-01T22:29:07
|_Not valid after:  2026-12-31T22:29:07
| rdp-ntlm-info: 
|   Target_Name: CPENTV2025
|   NetBIOS_Domain_Name: CPENTV2025
|   NetBIOS_Computer_Name: AD-WIN
|   DNS_Domain_Name: CPENTv2025.com
|   DNS_Computer_Name: AD-WIN.CPENTv2025.com
|   DNS_Tree_Name: CPENTv2025.com
|   Product_Version: 10.0.14393
|_  System_Time: 2026-10-09T05:38:47+00:00
Service Info: Host: AD-WIN; OS: Windows; CPE: cpe:/o:microsoft:windows

Host script results:
| smb-security-mode: 
|   account_used: <blank>
|   authentication_level: user
|   challenge_response: supported
|_  message_signing: required
|_clock-skew: mean: 1h24m00s, deviation: 3h07m51s, median: 0s
| smb-os-discovery: 
|   OS: Windows Server 2016 Datacenter 14393 (Windows Server 2016 Datacenter 6.3)
|   Computer name: AD-WIN
|   NetBIOS computer name: AD-WIN\x00
|   Domain name: CPENTv2025.com
|   Forest name: CPENTv2025.com
|   FQDN: AD-WIN.CPENTv2025.com
|_  System time: 2026-10-08T22:38:50-07:00
| smb2-security-mode: 
|   3:1:1: 
|_    Message signing enabled and required
| smb2-time: 
|   date: 2026-10-09T05:38:48
|_  start_date: 2026-10-09T05:15:22

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 79.70 seconds



```


172.25.170.140


```bash

sudo nmap -Pn -n 172.25.170.140
Starting Nmap 7.95 ( https://nmap.org ) at 2026-10-09 10:58 IST
Nmap scan report for 172.25.170.140
Host is up (0.22s latency).
Not shown: 994 closed tcp ports (reset)
PORT     STATE SERVICE
21/tcp   open  ftp
80/tcp   open  http
135/tcp  open  msrpc
139/tcp  open  netbios-ssn
445/tcp  open  microsoft-ds
3389/tcp open  ms-wbt-server

# full scan

sudo nmap -sC -sV --reason -oA nmap/172.25.170.140 172.25.170.140
Starting Nmap 7.95 ( https://nmap.org ) at 2026-10-09 11:10 IST
Nmap scan report for 172.25.170.140
Host is up, received echo-reply ttl 126 (0.22s latency).
Not shown: 994 closed tcp ports (reset)
PORT     STATE SERVICE       REASON          VERSION
21/tcp   open  tcpwrapped    syn-ack ttl 126
80/tcp   open  http          syn-ack ttl 126 Microsoft IIS httpd 10.0
|_http-server-header: Microsoft-IIS/10.0
| http-methods: 
|_  Potentially risky methods: TRACE
|_http-title: IIS Windows
135/tcp  open  msrpc         syn-ack ttl 126 Microsoft Windows RPC
139/tcp  open  netbios-ssn   syn-ack ttl 126 Microsoft Windows netbios-ssn
445/tcp  open  microsoft-ds? syn-ack ttl 126
3389/tcp open  ms-wbt-server syn-ack ttl 126 Microsoft Terminal Services
| ssl-cert: Subject: commonName=Windows11.CPENTv2025.com
| Not valid before: 2026-07-01T22:10:33
|_Not valid after:  2026-12-31T22:10:33
| rdp-ntlm-info: 
|   Target_Name: CPENTV2025
|   NetBIOS_Domain_Name: CPENTV2025
|   NetBIOS_Computer_Name: WINDOWS11
|   DNS_Domain_Name: CPENTv2025.com
|   DNS_Computer_Name: Windows11.CPENTv2025.com
|   Product_Version: 10.0.22000
|_  System_Time: 2026-10-09T05:41:27+00:00
|_ssl-date: 2026-10-09T05:41:36+00:00; 0s from scanner time.
Service Info: OS: Windows; CPE: cpe:/o:microsoft:windows

Host script results:
| smb2-time: 
|   date: 2026-10-09T05:41:30
|_  start_date: N/A
| smb2-security-mode: 
|   3:1:1: 
|_    Message signing enabled but not required

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 52.02 seconds



```


172.25.170.200

```bash
sudo nmap -Pn -n 172.25.170.200
Starting Nmap 7.95 ( https://nmap.org ) at 2026-10-09 10:59 IST
Nmap scan report for 172.25.170.200
Host is up (0.22s latency).
Not shown: 981 closed tcp ports (reset)
PORT     STATE SERVICE
53/tcp   open  domain
80/tcp   open  http
88/tcp   open  kerberos-sec
135/tcp  open  msrpc
139/tcp  open  netbios-ssn
389/tcp  open  ldap
445/tcp  open  microsoft-ds
464/tcp  open  kpasswd5
593/tcp  open  http-rpc-epmap
636/tcp  open  ldapssl
1433/tcp open  ms-sql-s
1801/tcp open  msmq
2103/tcp open  zephyr-clt
2105/tcp open  eklogin
2107/tcp open  msmq-mgmt
3268/tcp open  globalcatLDAP
3269/tcp open  globalcatLDAPssl
3389/tcp open  ms-wbt-server
5985/tcp open  wsman

Nmap done: 1 IP address (1 host up) scanned in 19.94 seconds

## full scan

Nmap scan report for 172.25.170.200
Host is up, received echo-reply ttl 126 (0.24s latency).
Not shown: 981 closed tcp ports (reset)
PORT     STATE SERVICE       REASON          VERSION
53/tcp   open  domain        syn-ack ttl 126 Simple DNS Plus
80/tcp   open  http          syn-ack ttl 126 Microsoft IIS httpd 10.0
|_http-server-header: Microsoft-IIS/10.0
|_http-title: IIS Windows Server
| http-methods: 
|_  Potentially risky methods: TRACE
88/tcp   open  kerberos-sec  syn-ack ttl 126 Microsoft Windows Kerberos (server time: 2026-10-09 05:44:57Z)
135/tcp  open  msrpc         syn-ack ttl 126 Microsoft Windows RPC
139/tcp  open  netbios-ssn   syn-ack ttl 126 Microsoft Windows netbios-ssn
389/tcp  open  ldap          syn-ack ttl 126 Microsoft Windows Active Directory LDAP (Domain: CPENTv2025.com0., Site: Default-First-Site-Name)
445/tcp  open  microsoft-ds  syn-ack ttl 126 Windows Server 2022 Standard 20348 microsoft-ds (workgroup: CPENTV2025)
464/tcp  open  kpasswd5?     syn-ack ttl 126
593/tcp  open  ncacn_http    syn-ack ttl 126 Microsoft Windows RPC over HTTP 1.0
636/tcp  open  tcpwrapped    syn-ack ttl 126
1433/tcp open  ms-sql-s      syn-ack ttl 126 Microsoft SQL Server 2022
|_ssl-date: 2026-10-09T05:45:59+00:00; 0s from scanner time.
|_ms-sql-ntlm-info: ERROR: Script execution failed (use -d to debug)
|_ms-sql-info: ERROR: Script execution failed (use -d to debug)
| ssl-cert: Subject: commonName=SSL_Self_Signed_Fallback
| Not valid before: 2026-10-09T05:17:35
|_Not valid after:  2056-10-09T05:17:35
1801/tcp open  msmq?         syn-ack ttl 126
2103/tcp open  msrpc         syn-ack ttl 126 Microsoft Windows RPC
2105/tcp open  msrpc         syn-ack ttl 126 Microsoft Windows RPC
2107/tcp open  msrpc         syn-ack ttl 126 Microsoft Windows RPC
3268/tcp open  ldap          syn-ack ttl 126 Microsoft Windows Active Directory LDAP (Domain: CPENTv2025.com0., Site: Default-First-Site-Name)
3269/tcp open  tcpwrapped    syn-ack ttl 126
3389/tcp open  ms-wbt-server syn-ack ttl 126 Microsoft Terminal Services
| rdp-ntlm-info: 
|   Target_Name: CPENTV2025
|   NetBIOS_Domain_Name: CPENTV2025
|   NetBIOS_Computer_Name: ADRANGEBASE22
|   DNS_Domain_Name: CPENTv2025.com
|   DNS_Computer_Name: ADRANGEBASE22.CPENTV2025.com
|   DNS_Tree_Name: CPENTv2025.com
|   Product_Version: 10.0.20348
|_  System_Time: 2026-10-09T05:45:51+00:00
|_ssl-date: 2026-10-09T05:45:59+00:00; 0s from scanner time.
| ssl-cert: Subject: commonName=ADRANGEBASE22.CPENTV2025.com
| Not valid before: 2026-06-22T06:43:15
|_Not valid after:  2026-12-22T06:43:15
5985/tcp open  http          syn-ack ttl 126 Microsoft HTTPAPI httpd 2.0 (SSDP/UPnP)
|_http-server-header: Microsoft-HTTPAPI/2.0
|_http-title: Not Found
Service Info: Host: ADRANGEBASE22; OS: Windows; CPE: cpe:/o:microsoft:windows

Host script results:
|_clock-skew: mean: 1h09m59s, deviation: 2h51m27s, median: 0s
|_nbstat: NetBIOS name: ADRANGEBASE22, NetBIOS user: <unknown>, NetBIOS MAC: 00:15:5d:01:80:02 (Microsoft)
| smb-security-mode: 
|   account_used: guest
|   authentication_level: user
|   challenge_response: supported
|_  message_signing: required
| smb-os-discovery: 
|   OS: Windows Server 2022 Standard 20348 (Windows Server 2022 Standard 6.3)
|   Computer name: ADRANGEBASE22
|   NetBIOS computer name: ADRANGEBASE22\x00
|   Domain name: CPENTv2025.com
|   Forest name: CPENTv2025.com
|   FQDN: ADRANGEBASE22.CPENTV2025.com
|_  System time: 2026-10-08T22:45:50-07:00
| smb2-security-mode: 
|   3:1:1: 
|_    Message signing enabled and required
| smb2-time: 
|   date: 2026-10-09T05:45:52
|_  start_date: N/A

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 81.92 seconds



```
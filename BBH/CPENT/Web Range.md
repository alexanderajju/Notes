
**IP Address Range**: 10.10.1.0/24

**Exclusion**: 10.10.1.1, 10.10.1.2

**Description**: In this zone, you will deal with multiple web application vulnerabilities and security misconfigurations. Once you identify them and exploit them, you own the servers. Upon owning them, find the secret keys placed in them.

**Note:** The target website syncvibe.xr.com is found to be hosted at the IP address 10.10.1.9.


```bash

┌──[aju@parrot]─[~/CPENT/web]
└──╼ $ sudo nmap -sn 10.10.1.0/24 -T5                         
[sudo] password for aju: 
Starting Nmap 7.95 ( https://nmap.org ) at 2026-10-09 12:29 IST
Nmap scan report for 10.10.1.2
Host is up (0.22s latency).
Nmap scan report for 10.10.1.9
Host is up (0.22s latency).
Nmap scan report for 10.10.1.111
Host is up (0.23s latency).
Nmap done: 256 IP addresses (3 hosts up) scanned in 9.44 seconds


```


**Description**: In this zone, you will deal with multiple web application vulnerabilities and security misconfigurations. Once you identify them and exploit them, you own the servers. Upon owning them, find the secret keys placed in them.

**Note:** The target website syncvibe.xr.com is found to be hosted at the IP address 10.10.1.9.


![[Pasted image 20261009123351.png]]


**Challenge 48: (100 Points)**  
Identify Maria's Region from the TKT-TKT-004_Emergency_Staging.md file located on the syncvibe.xr.com web server and submit it as your response. (Answer Format: Xxxxx XxxXx): Spain LatAm

![[Pasted image 20261009175321.png]]

![[Pasted image 20261009175420.png]]


![[Pasted image 20261009175731.png]]


![[Pasted image 20261009181757.png]]

![[Pasted image 20261009181732.png]]




![[Pasted image 20261009182010.png]]


![[Pasted image 20261009182833.png]]


![[Pasted image 20261009182942.png]]

**Challenge 49: (100 Points)**  
Identify the security passphrase associated with user kwame from the SSH key backups stored on the syncvibe.xr.com web server and determine the last 5 characters as your answer. (Answer Format: NxXxx): 1sHer

![[Pasted image 20261009184308.png]]

kwame: N3n0BlAd3S1sHer

**Challenge 50: (100 Points)**  
Identify the incident_rep_master.zip file on the syncvibe.xr.com web server, extract its contents and determine the first five characters of MASTER EMERGENCY SYSTEM OVERRIDE KEY as your response. (use the hint provided in Hint.txt on the server) (Answer Format: XNxXN) : N4tV8


![[Pasted image 20261009184749.png]]

![[Pasted image 20261009185110.png]]


![[Pasted image 20261009185149.png]]

![[Pasted image 20261009185042.png]]

![[Pasted image 20261009185229.png]]


![[Pasted image 20261009185823.png]]

N4tV8yJ2qW7mP5xL

**Challenge 51: (50 Points)**  
Find the supervisor's email ID on the website running on the machine with the IP address 10.10.1.111. (Answer Format: xxxx@xxxxxxx.xxx)

![[Pasted image 20261009192927.png]]

tony@synixon.com


**Challenge 52: (50 Points)**  
Determine the filename of the legacy keyset log file on the target machine with the IP address 10.10.1.111. (Answer Format: xxxxxx_xxx_xxxx.xxx)


![[Pasted image 20261009193934.png]]


**Challenge 53: (100 Points)**  
Identify the contents inside the brackets of flag.txt file on the target machine with the IP address 10.10.1.111 and submit it as the answer. (Answer Format: XNXX NXNX ): A1EL2L8P

![[Pasted image 20261009194227.png]]
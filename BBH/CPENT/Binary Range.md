

**Scope**:

**IP Address Range**: 172.25.65.0/24

**Exclusion**: 172.25.65.250

**Target machine**: 172.25.65.103

**Username**: ubuntu

**Password**: Cr@ckMeD0wn

**Description**: In this zone, you have to identify the filtering device, map the attack surface, and then gain access to the filtered segment. Once there, you need to identify the binary files and reverse engineer them to answer the questions, and then to get the privilege flag; you will have to create an exploit and then gain root-level privileges. Protections may or may not be compiled into the binary.


```nmap

sudo nmap -sn 172.25.65.0/24 -T5
[sudo] password for aju: 
Starting Nmap 7.95 ( https://nmap.org ) at 2026-10-16 11:28 IST
Nmap scan report for 172.25.65.1
Host is up (0.23s latency).
Nmap scan report for 172.25.65.103
Host is up (0.23s latency).
Nmap scan report for 172.25.65.105
Host is up (0.23s latency).
Nmap scan report for 172.25.65.165
Host is up (0.24s latency).
Nmap done: 256 IP addresses (4 hosts up) scanned in 10.13 seconds


```


172.25.65.165 

```nmap

Starting Nmap 7.95 ( https://nmap.org ) at 2026-10-16 11:30 IST
Nmap scan report for 172.25.65.165
Host is up, received syn-ack (0.22s latency).
Not shown: 995 closed tcp ports (conn-refused)
PORT     STATE SERVICE       REASON  VERSION
22/tcp   open  ssh           syn-ack OpenSSH 9.6p1 Ubuntu 3ubuntu13.11 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   256 29:40:00:a4:18:d5:bf:94:b6:aa:79:ea:aa:9f:07:9d (ECDSA)
|_  256 cb:06:ad:58:82:8c:63:c6:0e:8c:73:fe:bb:a0:09:d4 (ED25519)
80/tcp   open  http          syn-ack nginx 1.24.0 (Ubuntu)
|_http-title: Welcome to nginx!
|_http-server-header: nginx/1.24.0 (Ubuntu)
443/tcp  open  ssl/http      syn-ack nginx 1.24.0 (Ubuntu)
|_ssl-date: TLS randomness does not represent time
|_http-server-header: nginx/1.24.0 (Ubuntu)
| ssl-cert: Subject: organizationName=Internet Widgits Pty Ltd/stateOrProvinceName=Some-State/countryName=US
| Not valid before: 2025-04-07T09:29:14
|_Not valid after:  2035-04-05T09:29:14
|_http-title: Welcome to nginx!
| tls-alpn: 
|   http/1.1
|   http/1.0
|_  http/0.9
2022/tcp open  ssh           syn-ack OpenSSH 9.6p1 Ubuntu 3ubuntu13.11 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   256 29:40:00:a4:18:d5:bf:94:b6:aa:79:ea:aa:9f:07:9d (ECDSA)
|_  256 cb:06:ad:58:82:8c:63:c6:0e:8c:73:fe:bb:a0:09:d4 (ED25519)
3389/tcp open  ms-wbt-server syn-ack Microsoft Terminal Service
Service Info: OSs: Linux, Windows; CPE: cpe:/o:linux:linux_kernel, cpe:/o:microsoft:windows

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 47.04 seconds


```

![[Pasted image 20261016115700.png]]


**Challenge 26: (50 Points)**  
During the fuzzing process, what hexadecimal value overwrote the EIP register, confirming control over the instruction pointer on the target machine172.25.65.165 ? (Answer Format: NxNNNNNNNN): 0x42424242


![[Pasted image 20261016113409.png]]


![[Pasted image 20261016113812.png]]


![[Pasted image 20261016114011.png]]

![[Pasted image 20261016114124.png]]



![[Pasted image 20261016114404.png]]

0x42424242

**Challenge 27: (50 Points)**  
What is the calculated offset in bytes required to reach and overwrite the return address on the stack on 172.25.65.165 ? (Answer Format: NNN) : 112

![[Pasted image 20261016114830.png]]


![[Pasted image 20261016114812.png]]

![[Pasted image 20261016114944.png]]

**Challenge 28: (100 Points)**  
Identify the first 7 characters inside the brackets in the flag.txt file on the machine at 172.25.65.165. (Answer Format: XNxNxNx): G4t3w4y


![[Pasted image 20261016115527.png]]


![[Pasted image 20261016115423.png]]


CTF{G4t3w4y_0v3rfl0w_PWN3D}

**Challenge 29: (50 Points)**  
Determine the exact number of padding bytes required to overwrite the return address on the target machine with the IP address 172.25.65.105.(Answer Format: NN): 72


![[Pasted image 20261016115846.png]]


![[Pasted image 20261016120417.png]]

**Challenge 30: (20 Points)**  
What is the name of the hidden function within the overflow_me binary that, when called, reveals the flag on the machine 172.25.65.105? (Answer Format: xxx): win

![[Pasted image 20261016123656.png]]

![[Pasted image 20261016123800.png]]


![[Pasted image 20261016120648.png]]


**Challenge 31: (30 Points)**  
What was the full hexadecimal memory address of the hidden function on the machine 172.25.65.105? (Answer Format: NxNNNNNNNNNNNNNNNN)
0x0000000000401186

![[Pasted image 20261016120826.png]]



**Challenge 32: (100 Points)**  
What is the total character count of the flag.txt, excluding the brackets, found on the machine at 172.25.65.105? (Answer Format : NN):33

![[Pasted image 20261016121754.png]]

![[Pasted image 20261016121721.png]]

B0_0v3rfl0w_W4s_T00_3asy_f0r_y0u!

![[Pasted image 20261016122339.png]]

**Challenge 33: (70 Points)**  
Reverse engineer challenge3.exe on the target machine with the IP address 172.25.65.103 and identify the standard algorithm implemented by the membership validation function.(Answer Format: Xxxx Xxxxx xxxx): Luhn Algorithm
![[Pasted image 20261016122849.png]]


![[Pasted image 20261016123110.png]]



![[Pasted image 20261016124646.png]]


![[Pasted image 20261016124716.png]]

![[Pasted image 20261016124747.png]]

**Challenge 34: (30 Points)**  
Analyze the file challenge3.exe and determine the hexadecimal value used as the divisor in its final checksum validation on the machine with the IP address 172.25.65.103.(Answer Format: NxNX): 0x0A


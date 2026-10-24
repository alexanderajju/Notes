
**IP Address Range**: 172.25.120.0/24

**Exclusion**: 172.25.120.250

**Target machine 1**: 172.25.120.110

**Username**: ubuntu

**Password**: toor

**Target machine 2**: 172.25.120.100

**Username**: cpent

**Password**: cpentpw

**Description**: In this zone, you will need to identify the target, map the attack surface, and then gain access; once you gain access, you need to reverse engineer the firmware and answer the questions. As you build your target database, make a note of any hard-coded credentials. Once you find a firmware image, analyze the extracted file system and look at the code, which in many cases will be PHP, etc..



Target 1

![[Pasted image 20261009114215.png]]

**Challenge 13: (20 Points)**  
What is the block size of IOT.bin file in bytes (Answer Format: NNNNN)

![[Pasted image 20261009120330.png]]

65536 bytes

**Challenge 14: (20 Points)**  
What is the CPU architecture of the iot2.bin file? (Answer Format: Xxxxxxxx):  Blackfin

![[Pasted image 20261009200139.png]]


**Challenge 15: (20 Points)**  
Determine the Linux version compatible with the IOT2.bin file (Answer Format: Xxxxx N.N.NN.N)

![[Pasted image 20261009200236.png]]

2.6.26.5

**Challenge 16: (30 Points)**  
Determine the file format of the extracted file 813682 from IOT3.bin (Answer Format: XXX):  ELF

![[Pasted image 20261009200619.png]]


**Challenge 17: (20 Points)**  
Determine the offset value of the extracted file D8232C within IOT3.bin (Answer Format: NxNNxNNN): 0x20b914

![[Pasted image 20261009200721.png]]


**Challenge 18: (20 Points)**  
What is the IP address of the device named DSP-W215 found in the database file of IOT4.bin? (Answer Format: NNN.NNN.N.NN): 192.168.0.60

![[Pasted image 20261009201010.png]]


**Challenge 19: (30 Points)**  
What is the version of BusyBox used in IOT4.bin? (Answer Format: xN.NN.N): v1.30.1

![[Pasted image 20261009201309.png]]


**Challenge 20: (30 Points)**  
What is the GCC version used to compile the file located at offset 464A28 in the IoT5.bin image? (Answer Format: N.N.N): 4.3.1

![[Pasted image 20261009201542.png]]

**Challenge 21: (20 Points)**  
Analyze the file IOT5.bin in 172.25.120.110 and determine its file system. (Answer format: XXXXN)

![[Pasted image 20261009122008.png]]

JFFS2 filesystem

**Challenge 22: (40 Points)**  
On the Machine 172.25.120.100, analyze IOT firmware image FileOne.bin and determine the image size. (Answer format: NNN NNNN)

![[Pasted image 20261009120951.png]]

7753728 bytes

**Challenge 23: (100 Points)**  
What is the starting address of the file system in FileTwo.bin on 172.25.120.100? (Answer format: NxXNNNN)

![[Pasted image 20261009121216.png]]

0xE0080

**Challenge 24: (50 Points)**  
On the machine 172.25.120.110, in IOT6.bin, which file contains the root user’s password? (Answer format: xxxxxx): passwd

![[Pasted image 20261009201833.png]]

**Challenge 25: (100 Points)**  
On IP address 172.25.120.110, what is the firmware device for the IOT6.bin firmware? (Answer format: XXXXNNNN)

![[Pasted image 20261009121737.png]]

WNDR3800




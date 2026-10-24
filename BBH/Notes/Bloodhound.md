
## collections

1. Python

```bash

python3 bloodhound.py -d dc01.sequel.htb -c all -u ryan -p WqSZAF6CysDQbGb3 -ns 10.10.11.51 --zip

```

2. nxe

```bash

nxc ldap dc01.sequel.htb -u ryan -p WqSZAF6CysDQbGb3 --bloodhound --collection All --dns-server 10.10.11.51

```

3. sharphound

```bash

.\sharphound.exe -c all

```

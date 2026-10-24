
1. sublister

```bash

sublister -d 
```

2. amass

```bash

amass enum -brute -active/passive -d <domain> | anew/tee -a subdomain.txt

```
3. fuff

filtering out using httpx live sub domin

```

cat subdomain.txt | httpx -sc -title
```

taking screenshots using aquatone

```bash
cat live-subdomain.txt | aquatone

```
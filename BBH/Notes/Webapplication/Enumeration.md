
nuclei 

```bash

nuclei -target hacknet.htb -fr -silent -headless

```

nuclei with other tools

```bash
subfinder -d targetdomain.com -silent | httpx | nuclei
```
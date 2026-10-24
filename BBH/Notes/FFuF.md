
flags

- -ic -> ignore comments
- -t -> threads
- -recursion 
- -recursion-depth 1
- -e extension

filters

```shell-session

MATCHER OPTIONS:
  -mc              Match HTTP status codes, or "all" for everything. (default: 200,204,301,302,307,401,403)
  -ml              Match amount of lines in response
  -mr              Match regexp
  -ms              Match HTTP response size
  -mw              Match amount of words in response

FILTER OPTIONS:
  -fc              Filter HTTP status codes from response. Comma separated list of codes and ranges
  -fl              Filter by amount of lines in response. Comma separated list of line counts and ranges
  -fr              Filter regexp
  -fs              Filter HTTP response size. Comma separated list of sizes and ranges
  -fw              Filter by amount of words in response. Comma separated list of word counts and ranges
  
```

```bash

ffuf -w /opt/useful/seclists/Discovery/Web-Content/directory-list-2.3-small.txt:FUZZ -u http://SERVER_IP:PORT/FUZZ -recursion -recursion-depth 1 -e .php -v

```

## VHOST

```shell

ffuf -w /opt/useful/seclists/Discovery/DNS/subdomains-top1million-5000.txt:FUZZ -u http://academy.htb:PORT/ -H 'Host: FUZZ.academy.htb'

```

## Sub domain

```bash

ffuf -w /usr/share/seclists/Discovery/DNS/subdomains-top1million-5000.txt:FUZZ -u http://FUZZ.inlanefreight.com/ -ic

```


## Parameter Fuzzing - GET

```shell

ffuf -w /opt/useful/seclists/Discovery/Web-Content/burp-parameter-names.txt:FUZZ -u http://admin.academy.htb:PORT/admin/admin.php?FUZZ=key

```

## Parameter Fuzzing - POST

POST requests can't be passed with the URL through the `?`  
POST requests are passed in the data field within the HTTP request

the `-d` option in `ffuf` lets you fuzz the data field, combined with the `-X` option to send POST requests

however, in PHP, POST data "content-type" can only accept "application/x-www-form-urlencoded" so we need to set that with `-H 'Content-Type: application/x-www-form-urlencoded`

so now our POST ffuf command is slightly different than the GET request:

```bash

ffuf -w ... -u http://admin.academy.htb:PORT/admin/admin.php -X POST -d 'FUZZ=key' -H 'Content-Type: application/x-www-form-urlencoded'

```
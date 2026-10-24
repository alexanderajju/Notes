
netstat -ano


arp -a  -- to discover systems on same network

to get a service with port 

```powershell
Get-Process -Id (Get-NetTCPConnection -LocalPort 22).OwningProcess
```
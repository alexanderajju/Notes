
We can enumerate AV software using Windows built-in tools, such as wmic.

```shell-session
PS C:\Users\thm> wmic /namespace:\\root\securitycenter2 path antivirusproduct
```

This also can be done using PowerShell, which gives the same result.

```shell-session
PS C:\Users\thm> Get-CimInstance -Namespace root/SecurityCenter2 -ClassName AntivirusProduct

```


We can use the following PowerShell command to **check** the service state of Windows Defender:



```shell-session
PS C:\Users\thm> Get-Service WinDefend

Status   Name               DisplayName
------   ----               -----------
Running  WinDefend          Windows Defender Antivirus Service
```

Next, we can start using the Get-MpComputerStatus cmdlet to get the current Windows Defender status. However, it provides the current status of security solution elements, including Anti-Spyware, Antivirus, LoavProtection, Real-time protection, etc. We can use select to specify what we need for as follows,

PowerShell

```shell-session
PS C:\Users\thm> Get-MpComputerStatus | select RealTimeProtectionEnabled

RealTimeProtectionEnabled
-------------------------
                    False
```
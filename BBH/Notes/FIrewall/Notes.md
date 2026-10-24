- waf00f <url>

Detect firewall is enabled using following commands

```shell-session
PS C:\Users\thm> Get-NetFirewallProfile | Format-Table Name, Enabled

Name    Enabled
----    -------
Domain     True
Private    True
Public     True
```

If we have admin privileges on the current user we logged in with, then we try to disable one or more than one firewall profile using the Set-NetFirewallProfile cmdlet.


```shell-session
PS C:\Windows\system32> Set-NetFirewallProfile -Profile Domain, Public, Private -Enabled False
PS C:\Windows\system32> Get-NetFirewallProfile | Format-Table Name, Enabled
---- -------
Domain False
Private False
Public False
```

We can also learn and check the current Firewall rules, whether allowing or denying by the firewall.

```shell-session
PS C:\Users\thm> Get-NetFirewallRule | select DisplayName, Enabled, Description

DisplayName                                                                  Enabled
-----------                                                                  -------
Virtual Machine Monitoring (DCOM-In)                                           False
Virtual Machine Monitoring (Echo Request - ICMPv4-In)                          False
Virtual Machine Monitoring (Echo Request - ICMPv6-In)                          False
Virtual Machine Monitoring (NB-Session-In)                                     False
Virtual Machine Monitoring (RPC)                                               False
SNMP Trap Service (UDP In)                                                     False
SNMP Trap Service (UDP In)                                                     False
Connected User Experiences and Telemetry                                        True
Delivery Optimization (TCP-In)                                                  True
```

During the red team engagement, we have no clue what the firewall blocks. However, we can take advantage of some PowerShell cmdlets such as Test-NetConnection and TcpClient. Assume we know that a firewall is in place, and we need to test inbound connection without extra tools, then we can do the following: 


```shell-session
PS C:\Users\thm> Test-NetConnection -ComputerName 127.0.0.1 -Port 80


ComputerName     : 127.0.0.1
RemoteAddress    : 127.0.0.1
RemotePort       : 80
InterfaceAlias   : Loopback Pseudo-Interface 1
SourceAddress    : 127.0.0.1
TcpTestSucceeded : True

PS C:\Users\thm> (New-Object System.Net.Sockets.TcpClient("127.0.0.1", "80")).Connected
True
```

As a result, we can confirm the inbound connection on port 80 is open and allowed in the firewall. Note that we can also test for remote targets in the same network or domain names by specifying in the -ComputerName argument for the Test-NetConnection.

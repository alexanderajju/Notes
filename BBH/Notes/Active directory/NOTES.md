Things to find out

```bash

- Users and groups
- Hostnames
- Routing tables
- Network shares
- Network services
- Applications and banners
- Firewall configurations
- Service settings and audit configurations
- SNMP and DNS details
- Hunting for credentials (saved on web browsers or client applications)
  
```


To check a system is domain joined or not

```bash
systeminfo | findstr Domain
```


AD-Enumeration

```powershell
Get-ADUser -Filter *
```

 to find a user within the AD environment. The Distinguished Name (DN) is a collection of comma-separated key and value pairs used to identify unique records within the directory. The DN consists of Domain Component (DC), OrganizationalUnitName (OU), Common Name (CN), and others. The following "CN=User1,CN=Users,DC=thmredteam,DC=com" is an example of DN, which can be visualized as follow:

Using the SearchBase option, we specify a specific Common-Name CN in the active directory. For example, we can specify to list any user(s) that part of Users.


```powershell
Get-ADUser -Filter * -SearchBase "CN=Users,DC=THMREDTEAM,DC=COM"
```

Search for users inside THM OU

```powershell
Get-ADUser -Filter * -SearchBase "OU=THM,DC=THMREDTEAM,DC=COM" 
```

PS: CN is default in main domain unless Users not created on OU we can't use this 

---

Installed application details

```powershell
wmic product get name,version
```

View hidden 

```powershell
Get-ChildItem -Hidden -Path C:\Users\kkidd\Desktop\
```

Installed updates

```powershell
wmic qfe get Caption,Description
```

started services

```cmd
net start
```


check group

```bash
net group # if domain joined
net localgroup
```

view group members

```cmd
net localgroup <group name>
```

Use `net accounts` to see the local settings on a machine; moreover, you can use `net accounts /domain` if the machine belongs to a domain. This command helps learn about password policy, such as minimum password length, maximum password age, and lockout duration.

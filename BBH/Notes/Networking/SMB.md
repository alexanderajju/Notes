
Microsoft Windows operating systems since Windows 95 have included client and server SMB protocol support. Samba, an open source server that supports the SMB protocol, was released for Unix systems.

```bash

 smbclient //[IP]/[SHARE] -U [USERNAME] -p [PORT]

```


# Enumeration

**Enum4Linux**

Enum4linux is a tool used to enumerate SMB shares on both Windows and Linux systems. It is basically a wrapper around the tools in the Samba package and makes it easy to quickly extract information from the target pertaining to SMB. It's already installed on the AttackBox, however if you need to install it on your own attacking machine, you can do so from the official [github](https://github.com/portcullislabs/enum4linux).

The syntax of Enum4Linux is nice and simple: **"enum4linux [options] ip"**

**TAG**            **FUNCTION**

-U             get userlist  
-M             get machine list  
-N             get namelist dump (different from -U and-M)  
-S             get sharelist  
-P             get password policy information  
-G             get group and member list

-a             all of the above (full basic enumeration)

Now we understand our enumeration tools, let's get started!
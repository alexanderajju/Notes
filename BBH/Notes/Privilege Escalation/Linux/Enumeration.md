
### hostname

The `hostname` command will return the hostname of the target machine. Although this value can easily be changed or have a relatively meaningless string (e.g. Ubuntu-3487340239), in some cases, it can provide information about the target system’s role within the corporate network (e.g. SQL-PROD-01 for a production SQL server).

  
### uname -a

Will print system information giving us additional detail about the kernel used by the system. This will be useful when searching for any potential kernel vulnerabilities that could lead to privilege escalation.



### /proc/version

The proc filesystem (procfs) provides information about the target system processes. You will find proc on many different Linux flavours, making it an essential tool to have in your arsenal.

Looking at `/proc/version` may give you information on the kernel version and additional data such as whether a compiler (e.g. GCC) is installed.


### /etc/issue

Systems can also be identified by looking at the `/etc/issue` file. This file usually contains some information about the operating system but can easily be customized or changed. While on the subject, any file containing system information can be customized or changed. For a clearer understanding of the system, it is always good to look at all of these.

### ps Command

The `ps` command is an effective way to see the running processes on a Linux system. Typing `ps` on your terminal will show processes for the current shell.

The output of the `ps` (Process Status) will show the following;

- PID: The process ID (unique to the process)
- TTY: Terminal type used by the user
- Time: Amount of CPU time used by the process (this is NOT the time this process has been running for)
- CMD: The command or executable running (will NOT display any command line parameter)

The “ps” command provides a few useful options.

- `ps -A`: View all running processes
- `ps axjf`: View process tree (see the tree formation until `ps axjf` is run below)

![](https://assets.tryhackme.com/additional/imgur/xsbohSd.png)  

- `ps aux`: The `aux` option will show processes for all users (a), display the user that launched the process (u), and show processes that are not attached to a terminal (x). Looking at the ps aux command output, we can have a better understanding of the system and potential vulnerabilities.  
    

### env

The `env` command will show environmental variables.

  

![](https://assets.tryhackme.com/additional/imgur/LWdJ8Fw.png)

  

The PATH variable may have a compiler or a scripting language (e.g. Python) that could be used to run code on the target system or leveraged for privilege escalation.

  

### sudo -l

The target system may be configured to allow users to run some (or all) commands with root privileges. The `sudo -l` command can be used to list all commands your user can run using `sudo`.

  
ls

One of the common commands used in Linux is probably `ls`.

  

While looking for potential privilege escalation vectors, please remember to always use the `ls` command with the `-la` parameter. The example below shows how the “secret.txt” file can easily be missed using the `ls` or `ls -l` commands.

![](https://assets.tryhackme.com/additional/imgur/2jOtOat.png)  

### Id

The `id` command will provide a general overview of the user’s privilege level and group memberships.

It is worth remembering that the `id` command can also be used to obtain the same information for another user as seen below.

![](https://assets.tryhackme.com/additional/imgur/YzfJliG.png)

### /etc/passwd

Reading the `/etc/passwd` file can be an easy way to discover users on the system.

  

![](https://assets.tryhackme.com/additional/imgur/r6oYOEi.png)

  

While the output can be long and a bit intimidating, it can easily be cut and converted to a useful list for brute-force attacks.

![](https://assets.tryhackme.com/additional/imgur/cpS2U93.png)

  

Remember that this will return all users, some of which are system or service users that would not be very useful. Another approach could be to grep for “home” as real users will most likely have their folders under the “home” directory.

  

![](https://assets.tryhackme.com/additional/imgur/psxE6V4.png)

  

### history

Looking at earlier commands with the `history` command can give us some idea about the target system and, albeit rarely, have stored information such as passwords or usernames.

  

### ifconfig

The target system may be a pivoting point to another network. The `ifconfig` command will give us information about the network interfaces of the system. The example below shows the target system has three interfaces (eth0, tun0, and tun1). Our attacking machine can reach the eth0 interface but can not directly access the two other networks.

  

![](https://assets.tryhackme.com/additional/imgur/hcdZnwK.png)


This can be confirmed using the `ip route` command to see which network routes exist.

![](https://assets.tryhackme.com/additional/imgur/PSrmz5O.png)

### netstat

Following an initial check for existing interfaces and network routes, it is worth looking into existing communications. The `netstat` command can be used with several different options to gather information on existing connections.

  

- `netstat -a`: shows all listening ports and established connections.
- `netstat -at` or `netstat -au` can also be used to list TCP or UDP protocols respectively.
- `netstat -l`: list ports in “listening” mode. These ports are open and ready to accept incoming connections. This can be used with the “t” option to list only ports that are listening using the TCP protocol (below)

  

![](https://assets.tryhackme.com/additional/imgur/BbLdyrr.png)

  

- `netstat -s`: list network usage statistics by protocol (below) This can also be used with the `-t` or `-u` options to limit the output to a specific protocol.

  

![](https://assets.tryhackme.com/additional/imgur/mc8OWP0.png)

  

- `netstat -tp`: list connections with the service name and PID information.

  

![](https://assets.tryhackme.com/additional/imgur/fDYQwbW.png)

  

This can also be used with the `-l` option to list listening ports (below)

  

![](https://assets.tryhackme.com/additional/imgur/JK7DNv0.png)

  

We can see the “PID/Program name” column is empty as this process is owned by another user.

Below is the same command run with root privileges and reveals this information as 2641/nc (netcat)

![](https://assets.tryhackme.com/additional/imgur/FjZHqlY.png)`   `

- `netstat -i`: Shows interface statistics. We see below that “eth0” and “tun0” are more active than “tun1”.

![](https://assets.tryhackme.com/additional/imgur/r6IjpmZ.png)

  

  

The `netstat` usage you will probably see most often in blog posts, write-ups, and courses is `netstat -ano` which could be broken down as follows;

- `-a`: Display all sockets
- `-n`: Do not resolve names
- `-o`: Display timers

  

![](https://assets.tryhackme.com/additional/imgur/UxzLBRw.png)

  

  

### find Command

Searching the target system for important information and potential privilege escalation vectors can be fruitful. The built-in “find” command is useful and worth keeping in your arsenal.

Below are some useful examples for the “find” command.

**Find files:**

- `find . -name flag1.txt`: find the file named “flag1.txt” in the current directory
- `find /home -name flag1.txt`: find the file names “flag1.txt” in the /home directory
- `find / -type d -name config`: find the directory named config under “/”
- `find / -type f -perm 0777`: find files with the 777 permissions (files readable, writable, and executable by all users)
- `find / -perm a=x`: find executable files
- `find /home -user frank`: find all files for user “frank” under “/home”
- `find / -mtime 10`: find files that were modified in the last 10 days
- `find / -atime 10`: find files that were accessed in the last 10 day
- `find / -cmin -60`: find files changed within the last hour (60 minutes)
- `find / -amin -60`: find files accesses within the last hour (60 minutes)
- `find / -size 50M`: find files with a 50 MB size

This command can also be used with (+) and (-) signs to specify a file that is larger or smaller than the given size.

![](https://assets.tryhackme.com/additional/imgur/pSMfoz4.png)

The example above returns files that are larger than 100 MB. It is important to note that the “find” command tends to generate errors which sometimes makes the output hard to read. This is why it would be wise to use the “find” command with “-type f 2>/dev/null” to redirect errors to “/dev/null” and have a cleaner output (below).

![](https://assets.tryhackme.com/additional/imgur/UKYSdE3.png)

  

Folders and files that can be written to or executed from:

- `find / -writable -type d 2>/dev/null` : Find world-writeable folders
- `find / -perm -222 -type d 2>/dev/null`: Find world-writeable folders
- `find / -perm -o w -type d 2>/dev/null`: Find world-writeable folders

The reason we see three different “find” commands that could potentially lead to the same result can be seen in the manual document. As you can see below, the perm parameter affects the way “find” works.

![](https://assets.tryhackme.com/additional/imgur/qb0klHH.png)  

- `find / -perm -o x -type d 2>/dev/null` : Find world-executable folders

Find development tools and supported languages:

- `find / -name perl*`
- `find / -name python*`
- `find / -name gcc*`

Find specific file permissions:

Below is a short example used to find files that have the SUID bit set. The SUID bit allows the file to run with the privilege level of the account that owns it, rather than the account which runs it. This allows for an interesting privilege escalation path,we will see in more details on task 6. The example below is given to complete the subject on the “find” command.

- `find / -perm -u=s -type f 2>/dev/null`: Find files with the SUID bit, which allows us to run the file with a higher privilege level than the current user.

### General Linux Commands

As we are in the Linux realm, familiarity with Linux commands, in general, will be very useful. Please spend some time getting comfortable with commands such as `find`, `locate`, `grep`, `cut`, `sort`, etc.

### bash_history

### pspy


### System

On a Linux system, we can get more information about the Linux distribution and release version by searching for files or links that end with `-release` in `/etc/`. Running `ls /etc/*-release` helps us find such files. Let’s see what things look like on a CentOS Linux.


```shell-session
user@TryHackMe$ ls /etc/*-release
/etc/centos-release  /etc/os-release  /etc/redhat-release  /etc/system-release
$ cat /etc/os-release 
NAME="CentOS Linux"
VERSION="7 (Core)"
[...]
```

Let’s try on a Fedora system.

```shell-session
user@TryHackMe$ ls /etc/*-release
/etc/fedora-release@  /etc/os-release@  /etc/redhat-release@  /etc/system-release@
$ cat /etc/os-release
NAME="Fedora Linux"
VERSION="36 (Workstation Edition)"
[...]
```

Similarly, various directories can reveal information about users and might contain sensitive files; one is the mail directories found at `/var/mail/`.



```shell-session
user@TryHackMe$ ls -lh /var/mail/
total 4.0K
-rw-rw----. 1 jane      mail   0 May 18 14:15 jane
-rw-rw----. 1 michael   mail   0 May 18 14:13 michael
-rw-rw----. 1 peter     mail   0 May 18 14:14 peter
-rw-rw----. 1 randa     mail   0 May 18 14:15 randa
-rw-------. 1 root      mail 639 May 19 07:37 root
```

To find the installed applications you can consider listing the files in `/usr/bin/` and `/sbin/`:

- `ls -lh /usr/bin/`
- `ls -lh /sbin/`

On an RPM-based Linux system, you can get a list of all installed packages using `rpm -qa`. The `-qa` indicates that we want to _query all_ packages.

On a Debian-based Linux system, you can get the list of installed packages using `dpkg -l`. The output below is obtained from an Ubuntu server.

```shell-session
user@TryHackMe$ dpkg -l
Desired=Unknown/Install/Remove/Purge/Hold
| Status=Not/Inst/Conf-files/Unpacked/halF-conf/Half-inst/trig-aWait/Trig-pend
|/ Err?=(none)/Reinst-required (Status,Err: uppercase=bad)
||/ Name                                  Version                            Architecture Description
+++-=====================================-==================================-============-===============================================================================
ii  accountsservice                       0.6.55-0ubuntu12~20.04.5           amd64        query and manipulate user account information
ii  adduser                               3.118ubuntu2                       all          add and remove users and groups
ii  alsa-topology-conf                    1.2.2-1                            all          ALSA topology configuration files
ii  alsa-ucm-conf                         1.2.2-1ubuntu0.13                  all          ALSA Use Case Manager configuration files
ii  amd64-microcode                       3.20191218.1ubuntu1                amd64        Processor microcode firmware for AMD CPUs
[...   ]
ii  zlib1g-dev:amd64                      1:1.2.11.dfsg-2ubuntu1.3           amd64        compression library - development
```

### Users

Files such as `/etc/passwd` reveal the usernames; however, various commands can provide more information and insights about other users on the system and their whereabouts.

You can show who is logged in using `who`.


```shell-session
user@TryHackMe$ who
root     tty1         2022-05-18 13:24
jane     pts/0        2022-05-19 07:17 (10.20.30.105)
peter    pts/1        2022-05-19 07:13 (10.20.30.113)
```

We can see that the user `root` is logged in to the system directly, while the users `jane` and `peter` are connected over the network, and we can see their IP addresses.

Note that `who` should not be confused with `whoami` which prints **your** effective user id.


```shell-session
user@TryHackMe$ whoami
jane
```

To take things to the next level, you can use `w`, which shows who is logged in and what they are doing. Based on the terminal output below, `peter` is editing `notes.txt` and `jane` is the one running `w` in this example.


```shell-session
user@TryHackMe$ w
 07:18:43 up 18:05,  3 users,  load average: 0.00, 0.01, 0.05
USER     TTY      FROM             LOGIN@   IDLE   JCPU   PCPU WHAT
root     tty1                      Wed13   17:52m  0.00s  0.00s less -s
jane     pts/0    10.20.30.105     07:17    3.00s  0.01s  0.00s w
peter    pts/1    10.20.30.113     07:13    5:23   0.00s  0.00s vi notes.txt
```

To print the real and effective user and group IDS, you can issue the command `id` (for ID).


```shell-session
user@TryHackMe$ id
uid=1003(jane) gid=1003(jane) groups=1003(jane) context=unconfined_u:unconfined_r:unconfined_t:s0-s0:c0.c1023
```

Do you want to know who has been using the system recently? `last` displays a listing of the last logged-in users; moreover, we can see who logged out and how much they stayed connected. In the output below, the user `randa` remained logged in for almost 17 hours, while the user `michael` logged out after four minutes.


```shell-session
user@TryHackMe$ last
jane     pts/0        10.20.30.105     Thu May 19 07:17   still logged in   
peter    pts/1        10.20.30.113     Thu May 19 07:13   still logged in   
michael  pts/0        10.20.30.1       Thu May 19 05:12 - 05:17  (00:04)    
randa    pts/1        10.20.30.107     Wed May 18 14:18 - 07:08  (16:49)    
root     tty1                          Wed May 18 13:24   still logged in
[...]
```

Finally, it is worth mentioning that `sudo -l` lists the allowed command for the invoking user on the current system.

### Networking

The IP addresses can be shown using `ip address show` (which can be shortened to `ip a s`) or with the older command `ifconfig -a` (its package is no longer maintained.) The terminal output below shows the network interface `ens33` with the IP address `10.20.30.129` and subnet mask `255.255.255.0` as it is `24`.

```shell-session
user@TryHackMe$ ip a s
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
    inet6 ::1/128 scope host 
       valid_lft forever preferred_lft forever
2: ens33: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc pfifo_fast state UP group default qlen 1000
    link/ether 00:0c:29:a2:0e:7e brd ff:ff:ff:ff:ff:ff
    inet 10.20.30.129/24 brd 10.20.30.255 scope global noprefixroute dynamic ens33
       valid_lft 1580sec preferred_lft 1580sec
    inet6 fe80::761a:b360:78:26cd/64 scope link noprefixroute 
       valid_lft forever preferred_lft forever
```

The DNS servers can be found in the `/etc/resolv.conf`. Consider the following terminal output for a system that uses DHCP for its network configurations. The DNS, i.e. nameserver, is set to `10.20.30.2`.


```shell-session
user@TryHackMe$ cat /etc/resolv.conf
# Generated by NetworkManager
search localdomain thm
nameserver 10.20.30.2
```

`netstat` is a useful command for learning about network connections, routing tables, and interface statistics. We explain some of its many options in the table below.

|Option|Description|
|---|---|
|`-a`|show both listening and non-listening sockets|
|`-l`|show only listening sockets|
|`-n`|show numeric output instead of resolving the IP address and port number|
|`-t`|TCP|
|`-u`|UDP|
|`-x`|UNIX|
|`-p`|Show the PID and name of the program to which the socket belongs|

You can use any combination that suits your needs. For instance, `netstat -plt` will return _Programs Listening on TCP_ sockets. As we can see in the terminal output below, `sshd` is listening on the SSH port, while `master` is listening on the SMTP port on both IPv4 and IPv6 addresses. Note that to get all PID (process ID) and program names, you need to run `netstat` as root or use `sudo netstat`.

```shell-session
user@TryHackMe$ sudo netstat -plt
Active Internet connections (only servers)
Proto Recv-Q Send-Q Local Address           Foreign Address         State       PID/Program name    
tcp        0      0 0.0.0.0:ssh             0.0.0.0:*               LISTEN      978/sshd            
tcp        0      0 localhost:smtp          0.0.0.0:*               LISTEN      1141/master         
tcp6       0      0 [::]:ssh                [::]:*                  LISTEN      978/sshd            
tcp6       0      0 localhost:smtp          [::]:*                  LISTEN      1141/master
```



One might think that using `nmap` before gaining access to the target machine would have provided a comparable result. However, this is not entirely true. Nmap needs to generate a relatively large number of packets to check for open ports, which can trigger intrusion detection and prevention systems. Furthermore, firewalls across the route can drop certain packets and hinder the scan, resulting in incomplete Nmap results.

`lsof` stands for List Open Files. If we want to display only Internet and network connections, we can use `lsof -i`. The terminal output below shows IPv4 and IPv6 listening services and ongoing connections. The user `peter` is connected to the server `rpm-red-enum.thm` on the `ssh` port. Note that to get the complete list of matching programs, you need to run `lsof` as root or use `sudo lsof`.

Terminal

```shell-session
user@TryHackMe$ sudo lsof -i
COMMAND   PID      USER   FD   TYPE DEVICE SIZE/OFF NODE NAME
chronyd   640    chrony    5u  IPv4  16945      0t0  UDP localhost:323 
chronyd   640    chrony    6u  IPv6  16946      0t0  UDP localhost:323 
sshd      978      root    3u  IPv4  20035      0t0  TCP *:ssh (LISTEN)
sshd      978      root    4u  IPv6  20058      0t0  TCP *:ssh (LISTEN)
master   1141      root   13u  IPv4  20665      0t0  TCP localhost:smtp (LISTEN)
master   1141      root   14u  IPv6  20666      0t0  TCP localhost:smtp (LISTEN)
dhclient 5638      root    6u  IPv4  47458      0t0  UDP *:bootpc 
sshd     5693     peter    3u  IPv4  47594      0t0  TCP rpm-red-enum.thm:ssh->10.20.30.113:38822 (ESTABLISHED)
[...]
```

Because the list can get quite lengthy, you can further filter the output by specifying the ports you are interested in, such as SMTP port 25. By running `lsof -i :25`, we limit the output to those related to port 25, as shown in the terminal output below. The server is listening on port 25 on both IPv4 and IPv6 addresses.

Terminal

```shell-session
user@TryHackMe$ sudo lsof -i :25
COMMAND  PID USER   FD   TYPE DEVICE SIZE/OFF NODE NAME
master  1141 root   13u  IPv4  20665      0t0  TCP localhost:smtp (LISTEN)
master  1141 root   14u  IPv6  20666      0t0  TCP localhost:smtp (LISTEN)
```

### Running Services

Getting a snapshot of the running processes can provide many insights. `ps` lets you discover the running processes and plenty of information about them.

You can list every process on the system using `ps -e`, where `-e` selects all processes. For more information about the process, you can add `-f` for full-format and`-l` for long format. Experiment with `ps -e`, `ps -ef`, and `ps -el`.

You can get comparable output and see all the processes using BSD syntax: `ps ax` or `ps aux`. Note that `a` and `x` are necessary when using BSD syntax as they lift the “only yourself” and “must have a tty” restrictions; in other words, it becomes possible to display all processes. The `u` is for details about the user that has the process.

|Option|Description|
|---|---|
|`-e`|all processes|
|`-f`|full-format listing|
|`-j`|jobs format|
|`-l`|long format|
|`-u`|user-oriented format|

For more “visual” output, you can issue `ps axjf` to print a process tree. The `f` stands for “forest”, and it creates an ASCII art process hierarchy as shown in the terminal output below.


```shell-session
user@TryHackMe$ ps axf
   PID TTY      STAT   TIME COMMAND
     2 ?        S      0:00 [kthreadd]
     4 ?        S<     0:00  \_ [kworker/0:0H]
     5 ?        S      0:01  \_ [kworker/u256:0]
[...]
   978 ?        Ss     0:00 /usr/sbin/sshd -D
  5665 ?        Ss     0:00  \_ sshd: peter [priv]
  5693 ?        S      0:00  |   \_ sshd: peter@pts/1
  5694 pts/1    Ss     0:00  |       \_ -bash
  5713 pts/1    S+     0:00  |           \_ vi notes.txt
  5723 ?        Ss     0:00  \_ sshd: jane [priv]
  5727 ?        S      0:00      \_ sshd: jane@pts/0
  5728 pts/0    Ss     0:00          \_ -bash
  7080 pts/0    R+     0:00              \_ ps axf
   979 ?        Ssl    0:12 /usr/bin/python2 -Es /usr/sbin/tuned -l -P
   981 ?        Ssl    0:07 /usr/sbin/rsyslogd -n
  1141 ?        Ss     0:00 /usr/libexec/postfix/master -w
  1147 ?        S      0:00  \_ qmgr -l -t unix -u
  6991 ?        S      0:00  \_ pickup -l -t unix -u
  1371 ?        Ss     0:00 login -- root
  1376 tty1     Ss     0:00  \_ -bash
  1411 tty1     S+     0:00      \_ man man
  1420 tty1     S+     0:00          \_ less -s
[...]
```

To summarize, remember to use `ps -ef` or `ps aux` to get a list of all the running processes. Consider piping the output via `grep` to display output lines with certain words. The terminal output below shows the lines with `peter` in them.


```shell-session
user@TryHackMe$ ps -ef | grep peter
root       5665    978  0 07:11 ?        00:00:00 sshd: peter [priv]
peter      5693   5665  0 07:13 ?        00:00:00 sshd: peter@pts/1
peter      5694   5693  0 07:13 pts/1    00:00:00 -bash
peter      5713   5694  0 07:13 pts/1    00:00:00 vi notes.txt
```




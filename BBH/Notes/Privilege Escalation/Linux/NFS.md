NFS (Network File Sharing) configuration is kept in the /etc/exports file. This file is created during the NFS server installation and can usually be read by users.

![](https://assets.tryhackme.com/additional/imgur/irDQTze.png)  

The critical element for this privilege escalation vector is the “no_root_squash” option you can see above. By default, NFS will change the root user to nfsnobody and strip any file from operating with root privileges. If the “no_root_squash” option is present on a writable share, we can create an executable with SUID bit set and run it on the target system.  
  
We will start by enumerating mountable shares from our attacking machine.

![](https://assets.tryhackme.com/additional/imgur/CmXPDcv.png)  

We will mount one of the “no_root_squash” shares to our attacking machine and start building our executable.

  

![](https://assets.tryhackme.com/additional/imgur/DwAB1qs.png)  

  

As we can set SUID bits, a simple executable that will run /bin/bash on the target system will do the job.

  

![](https://assets.tryhackme.com/additional/imgur/nWKpFkK.png)  

  

Once we compile the code we will set the SUID bit.

  

![](https://assets.tryhackme.com/additional/imgur/rkZOOjZ.png)  

  

You will see below that both files (nfs.c and nfs are present on the target system. We have worked on the mounted share so there was no need to transfer them).

  

![](https://assets.tryhackme.com/additional/imgur/U7IjT38.png)  

  

Notice the nfs executable has the SUID bit set on the target system and runs with root privileges.
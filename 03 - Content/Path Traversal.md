---
creation date: November 9th 2022
last modified date: November 9th 2022
aliases: []
tags: #📕
---

Primary Categories: { Add link(s) [[]] back to related PRIMARY categories }
Secondary Categories:  { Add link(s) [[]] back to related SECONDARY categories }
Links: [[PHP]] - [[Linux]] - [[Windows]] - [[NULL BYTE]]
Search Tag: #📕  

# [[Path Traversal]]  
___

## Description:  


|          Location           |                                                                            Description                                                                            |
|:---------------------------:|:-----------------------------------------------------------------------------------------------------------------------------------------------------------------:|
|         `/etc/issue`          |                                         contains a message or system identification to be printed before the login prompt                                         |
|        `/etc/profile`         | controls system-wide default variables, such as Export variables, File creation mask (umask), Terminal types, Mail messages to indicate when new mail has arrived |
|        `/proc/version`        |                                                             specifies the version of the Linux kernel                                                             |
|         `/etc/passwd`         |                                                        has all registered user that has access to a system                                                        |
|         `/etc/shadow`         |                                                     contains information about the system's users' passwords                                                      |
|     `/root/.bash_history`     |                                                          contains the history commands for **root** user                                                          |
|      `/var/log/dmessage`      |                                   contains global system messages, including the messages that are logged during system startup                                   |
|       `/var/mail/root`        |                                                                   all emails for **root** user                                                                    |
|      `/root/.ssh/id_rsa`      |                                                 Private SSH keys for a root or any known valid user on the server                                                 |
| `/var/log/apache2/access.log` |                                                          the accessed requests for **Apache**  webserver                                                          |
|         `C:\boot.ini`         |                                                    contains the boot options for computers with BIOS firmware                                                     |

## Example
### PHP
- `http://10.10.89.64/lab1.php?file=/etc/passwd`
	- We are feeding it the parameter of `file`
- **PHP 5.3.3** and below we can use **NULL BYTE** to tell the code being executed to ignore all the rest after this.
	- `%00` or `0x00`
	- Useful when the code we are trying to execute is having something added to the end.

___

## Resources:

| Hyperlink | Info |
| --------- | ---- |


Created Date: November 9th 2022 (08:16 pm)  
Last Modified Date: <%+tp.file.last_modified_date("MMMM Do YYYY (hh:ss a)")%>

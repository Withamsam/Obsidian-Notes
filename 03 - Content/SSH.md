---
creation date: December 13th 2022
last modified date: December 13th 2022
aliases: 
tags:
  - 📕
primary categories:
---

Primary Categories: { Add link(s) [[]] back to related PRIMARY categories }
Secondary Categories:  { Add link(s) [[]] back to related SECONDARY categories }
Links: [[CLI]] - [[RDP]] - [[VNC]]
Search Tag: #📕  

# [[SSH]]  
___

## Description:  
Stands for **Secure Shell**. Provides a CLI interface with a system to allow you to execute commands.

## SSH Port forwarding
- Allows use to either: 
	- Host resources on a remote machine by forwarding local port to the remote server
	- or
	- Access local resources from a remote machine we are connecting to
- Example:
```bash
ssh -L 55553:127.0.0.1:55553 root@192.168.0.44
```
- This will forward all traffic to port 55553 to our local address & port


___

## Resources:

| Hyperlink | Info |
| --------- | ---- |


Created Date: December 13th 2022 (05:32 pm)  
Last Modified Date: <%+tp.file.last_modified_date("MMMM Do YYYY (hh:ss a)")%>

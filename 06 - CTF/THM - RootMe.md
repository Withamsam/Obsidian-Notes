---
creation date: November 13th 2022
last modified date: November 13th 2022
aliases: [RootMe]
tags: #🎌
---

Primary Categories: { Add link(s) [[]] back to related PRIMARY categories }
Secondary Categories:  { Add link(s) [[]] back to related SECONDARY categories }
Links: {Add link(s) [[]] to related terms}
Search Tag: #🎌  

# [[THM - RootMe]]  


# Resolution summary
- Found both text files and got root on machine.

## Improved skills
- Privilege Escalation
- Reverse Shell
- File upload restriction bypass

## Used tools
- [[Nmap]]
- [[ffuf]]
- [[Netcat]]

---

# Information Gathering
Scanned all TCP ports:
```bash
PORT   STATE SERVICE VERSION
22/tcp open  ssh     OpenSSH 7.6p1 Ubuntu 4ubuntu0.3 (Ubuntu Linux; protocol 2.0)
80/tcp open  http    Apache httpd 2.4.29 ((Ubuntu))
```

Enumerated open TCP ports:
```bash

```

Enumerated top 200 UDP ports:
```bash

```

---

# Enumeration
## Port 80 - HTTP (Apache)
Located directory of `/panel/` with an upload form. After you upload it gives a link to where the file is saved `/uploads/{FILE NAME}`

---

# Exploitation
## PHP Reverse Shell
Uploaded a shell to the form `.php` failed. I was able to upload `.php3`, `.php4`, `.php7`, `.php-s` but each of these when navigating would open the file as text so the server wasn't executing them. Finally I tried `.phtml` it uploaded and when opening it under uploads directory it executed the code. With a **Netcat** listener opened the shell connected back.


---

# Lateral Movement to user
## Local Enumeration
Used the following command to locate the .txt flag `find . -name user.txt`

## Lateral Movement vector


---

# Privilege Escalation
## Local Enumeration
Running `find / -perm -u=s -type f 2>/dev/null` found that `usr/bin/python` had SUID set.

## Privilege Escalation vector
Navigated to `/usr/bin/` directory in the shell and ran `./python -c 'import os; os.execl("/bin/sh", "sh", "-p")` which escalated my privilege to **ROOT**


---

# Trophy & Loot
user.txt = THM{y0u_g0t_a_sh3ll}

root.txt = THM{pr1v1l3g3_3sc4l4t10n}
___

## Resources:

| Hyperlink                                 | Info |
| ----------------------------------------- | ---- |
| [THM](https://tryhackme.com/room/rrootme) | CTF  | 


Created Date: November 13th 2022 (12:50 pm)  
Last Modified Date: <%+tp.file.last_modified_date("MMMM Do YYYY (hh:ss a)")%>

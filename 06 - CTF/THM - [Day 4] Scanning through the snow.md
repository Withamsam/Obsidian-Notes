---
creation date: December 12th 2022
last modified date: December 12th 2022
aliases: []
tags:
---

Primary Categories: { Add link(s) [[]] back to related PRIMARY categories }
Secondary Categories:  { Add link(s) [[]] back to related SECONDARY categories }
Links: {Add link(s) [[]] to related terms}
Search Tag: #🎌  

# [[THM - [Day 4] Scanning through the snow]]  


# Resolution summary
- Simple scan showed the path to take but need to work on my skills with SMB still have a lot of confusion with connecting to it.

## Improved skills
- smb

## Used tools
- [[Nmap]]
- [[SMB]]
- [[Nikto]]

---

# Information Gathering
Scanned all TCP ports:
```bash
Starting Nmap 7.93 ( https://nmap.org ) at 2022-12-12 22:24 CST
Nmap scan report for 10.10.225.34
Host is up (0.19s latency).
Not shown: 65531 closed tcp ports (conn-refused)
PORT    STATE SERVICE
22/tcp  open  ssh
80/tcp  open  http
139/tcp open  netbios-ssn
445/tcp open  microsoft-ds
```

Enumerated open TCP ports:
```bash
PORT    STATE SERVICE     VERSION
22/tcp  open  ssh         OpenSSH 7.6p1 Ubuntu 4ubuntu0.5 (Ubuntu Linux; protocol 2.0)
80/tcp  open  http        Apache httpd 2.4.29 ((Ubuntu))
139/tcp open  netbios-ssn Samba smbd 3.X - 4.X (workgroup: WORKGROUP)
445/tcp open  netbios-ssn Samba smbd 3.X - 4.X (workgroup: WORKGROUP)
```

Enumerated top 200 UDP ports:
```bash

```

---

# Enumeration
Ran scan over all ports and located 4 active ports most interesting is the SMB share.

---

# Exploitation

---

# Lateral Movement to user


---

# Privilege Escalation


---

# Trophy & Loot
flag.txt = **{THM_SANTA_SMB_SERVER}**

___

## Resources:

| Hyperlink                                        | Info        |
| ------------------------------------------------ | ----------- |
| [CTF](https://tryhackme.com/room/adventofcyber4) | Link to CTF | 


Created Date: December 12th 2022 (10:33 pm)  
Last Modified Date: <%+tp.file.last_modified_date("MMMM Do YYYY (hh:ss a)")%>

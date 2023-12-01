---
creation date: January 11th 2023
last modified date: January 11th 2023
aliases: []
tags: #🎌
---

Primary Categories: { Add link(s) [[]] back to related PRIMARY categories }
Secondary Categories:  { Add link(s) [[]] back to related SECONDARY categories }
Links: {Add link(s) [[]] to related terms}
Search Tag: #🎌  

# [[THM - Overpass]]  


# Resolution summary
- Text
- Text

## Improved skills
- skill 1
- skill 2

## Used tools
- [[nmap]]
- [[ffuf]]

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
22/tcp open  ssh     OpenSSH 7.6p1 Ubuntu 4ubuntu0.3 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   2048 37968598d1009c1463d9b03475b1f957 (RSA)
|   256 5375fac065daddb1e8dd40b8f6823924 (ECDSA)
|_  256 1c4ada1f36546da6c61700272e67759c (ED25519)
80/tcp open  http    Golang net/http server (Go-IPFS json-rpc or InfluxDB API)
|_http-title: Overpass
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel
```

Enumerated top 200 UDP ports:
```bash

```

FUZZ of port 80:
```bash
img                     [Status: 301, Size: 0, Words: 1, Lines: 1, Duration: 202ms]
[INFO] Adding a new job to the queue: http://10.10.252.194/img/FUZZ

downloads               [Status: 301, Size: 0, Words: 1, Lines: 1, Duration: 194ms]
[INFO] Adding a new job to the queue: http://10.10.252.194/downloads/FUZZ

aboutus                 [Status: 301, Size: 0, Words: 1, Lines: 1, Duration: 193ms]
[INFO] Adding a new job to the queue: http://10.10.252.194/aboutus/FUZZ

admin                   [Status: 301, Size: 42, Words: 3, Lines: 3, Duration: 188ms]
[INFO] Adding a new job to the queue: http://10.10.252.194/admin/FUZZ

css                     [Status: 301, Size: 0, Words: 1, Lines: 1, Duration: 195ms]
[INFO] Adding a new job to the queue: http://10.10.252.194/css/FUZZ

```

---

# Enumeration
## Port 80 (Golang)
- Located a download page with the source code. Looking it over we found a comment shown below:
	- **//A linear search is the best I can do, Steve says it's Oh Log N whatever that means**
- The about us page also indicates that they made this program because their passwords were compromised in the **rockyou**
	- This could mean that either the admin page or SSH has weak creds might want to try testing that???
	- [ ] SSH
	- [ ] Admin Page
		- **HINT 1 SAID TO NOT BRUTE FORCE**
- Possible usernames found on the about us page as well:
	- Ninja
	- Pars
	- Szymex
	- Bee
	- MuirlandOracle
		- Created a file in our directory with this list


---

# Exploitation
## Name of the technique


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
- Flag in user.txt = 
- Flag in root.txt = 

___

## Resources:

| Hyperlink | Info |
| --------- | ---- |


Created Date: January 11th 2023 (10:24 pm)  
Last Modified Date: <%+tp.file.last_modified_date("MMMM Do YYYY (hh:ss a)")%>

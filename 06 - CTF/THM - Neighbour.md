---
creation date: November 14th 2022
last modified date: November 14th 2022
aliases: []
tags: #🎌
---

Primary Categories: { Add link(s) [[]] back to related PRIMARY categories }
Secondary Categories:  { Add link(s) [[]] back to related SECONDARY categories }
Links: {Add link(s) [[]] to related terms}
Search Tag: #🎌  

# [[THM - Neighbour]]  


# Resolution summary
- Simple IDOR located after finding account info for guest and an admin username

## Improved skills
- IDOR

## Used tools
- [[Nmap]]

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
22/tcp open  ssh     OpenSSH 8.2p1 Ubuntu 4ubuntu0.5 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   3072 e6cb10376b977702591734ad63e6ea19 (RSA)
|   256 e2c0fa338620270fcd01a657c6e5ac0e (ECDSA)
|_  256 1e69e2c59a2d842316dfbad59fe1cf31 (ED25519)
80/tcp open  http    Apache httpd 2.4.53 ((Debian))
|_http-server-header: Apache/2.4.53 (Debian)
|_http-title: Login
| http-cookie-flags: 
|   /: 
|     PHPSESSID: 
|_      httponly flag not set
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

```

Enumerated top 200 UDP ports:
```bash
All 65535 scanned ports on 10.10.202.141 are in ignored states.
```

---

# Enumeration
## Port 80 - HTTP (Apache 2.4.53)
- Found accounts:
	- guest:guest
		- Goes to: `/profile.php?user=guest`
	- admin:

---

# Exploitation
## IDOR
1. After finding both accounts in source code for port 80.
2. Sign in with **guest:guest** creds to the main login page
3. URL after signing in shows its requesting: `/profile.php?user=guest`
4. Changing that to: `/profile.php?user=admin`
5. Success we got in and found the flag:
	1. flag{66be95c478473d91a5358f2440c7af1f}


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
`/profile.php?user=admin` = flag{66be95c478473d91a5358f2440c7af1f}
___

## Resources:

| Hyperlink                                   | Info |
| ------------------------------------------- | ---- |
| [THM](https://tryhackme.com/room/neighbour) | CTF  | 


Created Date: November 14th 2022 (05:19 pm)  
Last Modified Date: <%+tp.file.last_modified_date("MMMM Do YYYY (hh:ss a)")%>

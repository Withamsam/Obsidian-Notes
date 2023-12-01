---
creation date: August 11th 2023
last modified date: August 11th 2023
aliases: []
tags: #🎌
---

Primary Categories: 
Secondary Categories:  
Links: 
Search Tag: #🎌  

# [[THM - Crylo]]  


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
22/tcp open  ssh
80/tcp open  http
```

Enumerated open TCP ports:
```bash
PORT   STATE SERVICE VERSION
22/tcp open  ssh     OpenSSH 8.2p1 Ubuntu 4ubuntu0.5 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   3072 9f:7e:08:42:ea:bf:be:1a:1b:78:b0:f7:99:3c:ca:1d (RSA)
|   256 f8:f3:90:83:b1:bc:87:e8:93:a0:ff:d5:bc:1f:d7:e1 (ECDSA)
|_  256 b6:77:4d:a6:6d:73:79:15:ea:39:0c:f6:1b:b4:0b:6c (ED25519)
80/tcp open  http    nginx 1.18.0 (Ubuntu)
|_http-server-header: nginx/1.18.0 (Ubuntu)
|_http-title: Spicyo
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel
```

Enumerated top 200 UDP ports:
```bash

```

---

# Enumeration
## Port 80
### ffuf /
```
        /'___\  /'___\           /'___\       
       /\ \__/ /\ \__/  __  __  /\ \__/       
       \ \ ,__\\ \ ,__\/\ \/\ \ \ \ ,__\      
        \ \ \_/ \ \ \_/\ \ \_\ \ \ \ \_/      
         \ \_\   \ \_\  \ \____/  \ \_\       
          \/_/    \/_/   \/___/    \/_/       

       v2.0.0-dev
________________________________________________

 :: Method           : GET
 :: URL              : http://10.10.222.118/FUZZ
 :: Wordlist         : FUZZ: /usr/share/wordlists/directory_search.txt
 :: Follow redirects : false
 :: Calibration      : false
 :: Timeout          : 10
 :: Threads          : 150
 :: Matcher          : Response status: 200,204,301,302,307,401,403,405,500
________________________________________________

[Status: 200, Size: 10720, Words: 4046, Lines: 260, Duration: 239ms]
    * FUZZ: about

[Status: 200, Size: 11402, Words: 4155, Lines: 278, Duration: 260ms]
    * FUZZ: blog

[Status: 200, Size: 8858, Words: 3425, Lines: 214, Duration: 192ms]
    * FUZZ: contact

[Status: 403, Size: 122, Words: 6, Lines: 11, Duration: 209ms]
    * FUZZ: debug

[Status: 200, Size: 13151, Words: 5693, Lines: 314, Duration: 208ms]
    * FUZZ: login

[Status: 200, Size: 13914, Words: 5897, Lines: 355, Duration: 198ms]
    * FUZZ: recipe

:: Progress: [208971/208971] :: Job [1/1] :: 619 req/sec :: Duration: [0:05:37] :: Errors: 0 ::
```


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

___

## Resources:

| Hyperlink | Info |
| --------- | ---- |


Created Date: August 11th 2023 (02:55 pm)  
Last Modified Date: <%+tp.file.last_modified_date("MMMM Do YYYY (hh:ss a)")%>

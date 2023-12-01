---
creation date: August 18th 2023
last modified date: August 18th 2023
aliases: []
tags: #🎌
---

Primary Categories: 
Secondary Categories:  
Links: 
Search Tag: #🎌  

# [[THM - Grep]]  


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
PORT      STATE SERVICE
22/tcp    open  ssh
80/tcp    open  http
443/tcp   open  https
51337/tcp open  unknown
```

Enumerated open TCP ports:
```bash
PORT      STATE  SERVICE  VERSION
22/tcp    open   ssh      OpenSSH 8.2p1 Ubuntu 4ubuntu0.3 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   3072 8a:39:9c:ca:7a:22:d8:b8:2f:47:c4:3c:83:ea:f0:f7 (RSA)
|   256 9c:47:b6:3a:7a:25:05:04:5b:59:7a:3d:05:d8:88:9b (ECDSA)
|_  256 3c:5b:b9:82:ce:f1:0e:54:4e:7f:e8:2d:44:36:58:8d (ED25519)
80/tcp    open   http     Apache httpd 2.4.41 ((Ubuntu))
|_http-server-header: Apache/2.4.41 (Ubuntu)
|_http-title: Apache2 Ubuntu Default Page: It works
443/tcp   open   ssl/http Apache httpd 2.4.41
|_http-server-header: Apache/2.4.41 (Ubuntu)
|_http-title: 403 Forbidden
| tls-alpn: 
|_  http/1.1
|_ssl-date: TLS randomness does not represent time
| ssl-cert: Subject: commonName=grep.thm/organizationName=SearchME/stateOrProvinceName=Some-State/countryName=US
| Not valid before: 2023-06-14T13:03:09
|_Not valid after:  2024-06-13T13:03:09
28585/tcp closed unknown
51337/tcp open   http     Apache httpd 2.4.41
|_http-title: 400 Bad Request
|_http-server-header: Apache/2.4.41 (Ubuntu)
52806/tcp closed unknown
Service Info: Host: ip-10-10-61-214.eu-west-1.compute.internal; OS: Linux; CPE: cpe:/o:linux:linux_kernel
```

Enumerated top 200 UDP ports:
```bash

```

---

# Enumeration
## Port 80
### ffuf
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
 :: URL              : http://10.10.61.214/FUZZ
 :: Wordlist         : FUZZ: /usr/share/wordlists/directory_search.txt
 :: Follow redirects : false
 :: Calibration      : false
 :: Timeout          : 10
 :: Threads          : 150
 :: Matcher          : Response status: 200,204,301,302,307,401,403,405,500
________________________________________________

[Status: 403, Size: 277, Words: 20, Lines: 10, Duration: 200ms]
    * FUZZ: .hta

[Status: 403, Size: 277, Words: 20, Lines: 10, Duration: 242ms]
    * FUZZ: .htaccess

[Status: 403, Size: 277, Words: 20, Lines: 10, Duration: 198ms]
    * FUZZ: .htpasswd

[Status: 200, Size: 11509, Words: 3526, Lines: 378, Duration: 1279ms]
    * FUZZ: index.php

[Status: 301, Size: 317, Words: 20, Lines: 10, Duration: 363ms]
    * FUZZ: javascript

[INFO] Adding a new job to the queue: http://10.10.61.214/javascript/FUZZ

[Status: 403, Size: 277, Words: 20, Lines: 10, Duration: 239ms]
    * FUZZ: phpmyadmin

[Status: 403, Size: 277, Words: 20, Lines: 10, Duration: 180ms]
    * FUZZ: server-status

[INFO] Starting queued job on target: http://10.10.61.214/javascript/FUZZ

[Status: 403, Size: 277, Words: 20, Lines: 10, Duration: 199ms]
    * FUZZ: .htaccess

[Status: 403, Size: 277, Words: 20, Lines: 10, Duration: 200ms]
    * FUZZ: .hta

[Status: 403, Size: 277, Words: 20, Lines: 10, Duration: 213ms]
    * FUZZ: .htpasswd

[Status: 301, Size: 324, Words: 20, Lines: 10, Duration: 207ms]
    * FUZZ: jquery

[INFO] Adding a new job to the queue: http://10.10.61.214/javascript/jquery/FUZZ

[INFO] Starting queued job on target: http://10.10.61.214/javascript/jquery/FUZZ
```



## Port 443
- Initial access of this site gives a 403 error code.
- Looking at the nmap scan of the port I noticed that



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


Created Date: August 18th 2023 (06:34 pm)  
Last Modified Date: <%+tp.file.last_modified_date("MMMM Do YYYY (hh:ss a)")%>

---
creation date: September 6th 2023
last modified date: September 6th 2023
aliases: []
tags: #🎌
---

Primary Categories: 
Secondary Categories:  
Links: 
Search Tag: #🎌  

# [[HTB - Nibbles]]  


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
22/tcp open  ssh     OpenSSH 7.2p2 Ubuntu 4ubuntu2.2 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   2048 c4:f8:ad:e8:f8:04:77:de:cf:15:0d:63:0a:18:7e:49 (RSA)
|   256 22:8f:b1:97:bf:0f:17:08:fc:7e:2c:8f:e9:77:3a:48 (ECDSA)
|_  256 e6:ac:27:a3:b5:a9:f1:12:3c:34:a5:5d:5b:eb:3d:e9 (ED25519)
80/tcp open  http    Apache httpd 2.4.18 ((Ubuntu))
|_http-title: Site doesn't have a title (text/html).
|_http-server-header: Apache/2.4.18 (Ubuntu)
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel
```

Enumerated top 200 UDP ports:
```bash

```

---

# Enumeration
## Port 80
- *Apache httpd 2.4.18*

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
 :: URL              : http://10.129.113.60/FUZZ
 :: Wordlist         : FUZZ: /usr/share/wordlists/directory_search.txt
 :: Follow redirects : false
 :: Calibration      : false
 :: Timeout          : 10
 :: Threads          : 150
 :: Matcher          : Response status: 200,204,301,302,307,401,403,405,500
________________________________________________

[Status: 403, Size: 292, Words: 22, Lines: 12, Duration: 59ms]
    * FUZZ: .hta

[Status: 403, Size: 297, Words: 22, Lines: 12, Duration: 61ms]
    * FUZZ: .htaccess

[Status: 403, Size: 297, Words: 22, Lines: 12, Duration: 59ms]
    * FUZZ: .htpasswd

[Status: 200, Size: 93, Words: 8, Lines: 17, Duration: 65ms]
    * FUZZ: index.html

[Status: 403, Size: 301, Words: 22, Lines: 12, Duration: 56ms]
    * FUZZ: server-status

:: Progress: [208971/208971] :: Job [1/1] :: 2403 req/sec :: Duration: [0:01:43] :: Errors: 0 ::
```

#### /index.html
- Source code contained
```
<!-- /nibbleblog/ directory. Nothing interesting here! -->
```

#### /nibbleblog
- Located from comment under */index.html*
- Site has a blacklist function not sure the trigger but I caused it when I requested a reset on password about 3 times. Guessing that it will trigger if we *Bruteforce* 

##### /nibbleblog/README
- Located a version number that this blog site is using and found that its exploitable using a *Authenticated Arbitrary File Upload* 
	- CVE-2015-6967

##### /nibbleblog/admin.php
- Leads to an admin login page


### ffuf /nibbleblog
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
 :: URL              : http://10.129.113.60/nibbleblog/FUZZ
 :: Wordlist         : FUZZ: /usr/share/wordlists/directory_search.txt
 :: Follow redirects : false
 :: Calibration      : false
 :: Timeout          : 10
 :: Threads          : 150
 :: Matcher          : Response status: 200,204,301,302,307,401,403,405,500
________________________________________________

[Status: 301, Size: 325, Words: 20, Lines: 10, Duration: 56ms]
    * FUZZ: admin

[INFO] Adding a new job to the queue: http://10.129.113.60/nibbleblog/admin/FUZZ

[Status: 200, Size: 1401, Words: 79, Lines: 27, Duration: 68ms]
    * FUZZ: admin.php

[Status: 301, Size: 327, Words: 20, Lines: 10, Duration: 55ms]
    * FUZZ: content

[INFO] Adding a new job to the queue: http://10.129.113.60/nibbleblog/content/FUZZ

[Status: 403, Size: 303, Words: 22, Lines: 12, Duration: 55ms]
    * FUZZ: .hta

[Status: 403, Size: 308, Words: 22, Lines: 12, Duration: 55ms]
    * FUZZ: .htaccess

[Status: 403, Size: 308, Words: 22, Lines: 12, Duration: 52ms]
    * FUZZ: .htpasswd

[Status: 200, Size: 2987, Words: 116, Lines: 61, Duration: 68ms]
    * FUZZ: index.php

[Status: 301, Size: 329, Words: 20, Lines: 10, Duration: 78ms]
    * FUZZ: languages

[INFO] Adding a new job to the queue: http://10.129.113.60/nibbleblog/languages/FUZZ

[Status: 301, Size: 327, Words: 20, Lines: 10, Duration: 76ms]
    * FUZZ: plugins

[INFO] Adding a new job to the queue: http://10.129.113.60/nibbleblog/plugins/FUZZ

[Status: 200, Size: 4628, Words: 589, Lines: 64, Duration: 75ms]
    * FUZZ: README

[Status: 301, Size: 326, Words: 20, Lines: 10, Duration: 57ms]
    * FUZZ: themes

[INFO] Adding a new job to the queue: http://10.129.113.60/nibbleblog/themes/FUZZ
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


Created Date: September 6th 2023 (08:16 pm)  
Last Modified Date: <%+tp.file.last_modified_date("MMMM Do YYYY (hh:ss a)")%>

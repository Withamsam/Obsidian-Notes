---
creation date: June 1st 2023
last modified date: June 1st 2023
aliases: []
tags: #🎌
---

Primary Categories: 
Secondary Categories:  
Links: 
Search Tag: #🎌  

# [[HTB - Shocker]]  


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
PORT     STATE SERVICE
80/tcp   open  http
2222/tcp open  EtherNetIP-1
```

Enumerated open TCP ports:
```bash
PORT     STATE SERVICE VERSION
80/tcp   open  http    Apache httpd 2.4.18 ((Ubuntu))
|_http-server-header: Apache/2.4.18 (Ubuntu)
|_http-title: Site doesn't have a title (text/html).
2222/tcp open  ssh     OpenSSH 7.2p2 Ubuntu 4ubuntu2.2 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   2048 c4f8ade8f80477decf150d630a187e49 (RSA)
|   256 228fb197bf0f1708fc7e2c8fe9773a48 (ECDSA)
|_  256 e6ac27a3b5a9f1123c34a55d5beb3de9 (ED25519)
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel
```

Enumerated top 200 UDP ports:
```bash
All 65535 scanned ports on 10.129.136.12 are in ignored states.
Not shown: 65503 open|filtered udp ports (no-response), 32 closed udp ports (port-unreach)

Nmap done: 1 IP address (1 host up) scanned in 26.66 seconds
```

---

# Enumeration
## Port 80

### Wappalyzer
- Apache HTTP Server 2.4.18
- Ubuntu


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
 :: URL              : http://10.129.136.12/FUZZ
 :: Wordlist         : FUZZ: /usr/share/wordlists/directory_search.txt
 :: Follow redirects : false
 :: Calibration      : false
 :: Timeout          : 10
 :: Threads          : 150
 :: Matcher          : Response status: 200,204,301,302,307,401,403,405,500
________________________________________________

[Status: 403, Size: 296, Words: 22, Lines: 12, Duration: 55ms]
    * FUZZ: cgi-bin/

[Status: 403, Size: 292, Words: 22, Lines: 12, Duration: 52ms]
    * FUZZ: .hta

[Status: 403, Size: 297, Words: 22, Lines: 12, Duration: 57ms]
    * FUZZ: .htaccess

[Status: 403, Size: 297, Words: 22, Lines: 12, Duration: 58ms]
    * FUZZ: .htpasswd

[Status: 200, Size: 137, Words: 9, Lines: 10, Duration: 54ms]
    * FUZZ: index.html

[Status: 403, Size: 301, Words: 22, Lines: 12, Duration: 51ms]
    * FUZZ: server-status

:: Progress: [208971/208971] :: Job [1/1] :: 2717 req/sec :: Duration: [0:01:12] :: Errors: 0 ::
```

#### /bug.jpg
- Checked image over located nothing of use







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


Created Date: June 1st 2023 (10:48 pm)  
Last Modified Date: <%+tp.file.last_modified_date("MMMM Do YYYY (hh:ss a)")%>

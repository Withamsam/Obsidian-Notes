---
creation date: July 26th 2023
last modified date: July 26th 2023
aliases: []
tags: #🎌
---

Primary Categories: 
Secondary Categories:  
Links: 
Search Tag: #🎌  

# [[THM - ToolsRus]]  


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
22/tcp   open  ssh
80/tcp   open  http
1234/tcp open  hotline
8009/tcp open  ajp13
```

Enumerated open TCP ports:
```bash
PORT     STATE SERVICE VERSION
22/tcp   open  ssh     OpenSSH 7.2p2 Ubuntu 4ubuntu2.8 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   2048 d1:72:6c:ed:01:61:eb:65:05:00:99:37:af:76:38:be (RSA)
|   256 2a:85:19:b7:00:89:1a:1a:e9:af:fb:c6:cb:e9:4e:67 (ECDSA)
|_  256 42:43:7a:bf:b8:f7:b4:cb:f3:89:f1:ff:43:87:16:50 (ED25519)
80/tcp   open  http    Apache httpd 2.4.18 ((Ubuntu))
|_http-server-header: Apache/2.4.18 (Ubuntu)
|_http-title: Site doesn't have a title (text/html).
1234/tcp open  http    Apache Tomcat/Coyote JSP engine 1.1
|_http-favicon: Apache Tomcat
|_http-server-header: Apache-Coyote/1.1
|_http-title: Apache Tomcat/7.0.88
8009/tcp open  ajp13   Apache Jserv (Protocol v1.3)
|_ajp-methods: Failed to get a valid response for the OPTION request
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 15.44 seconds
```

Enumerated top 200 UDP ports:
```bash

```

---

# Enumeration
## Port 80 HTTP
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
 :: URL              : http://10.10.121.174/FUZZ
 :: Wordlist         : FUZZ: /usr/share/wordlists/directory_search.txt
 :: Follow redirects : false
 :: Calibration      : false
 :: Timeout          : 10
 :: Threads          : 150
 :: Matcher          : Response status: 200,204,301,302,307,401,403,405,500
________________________________________________

[Status: 301, Size: 319, Words: 20, Lines: 10, Duration: 197ms]
    * FUZZ: guidelines

[INFO] Adding a new job to the queue: http://10.10.121.174/guidelines/FUZZ

[Status: 403, Size: 292, Words: 22, Lines: 12, Duration: 196ms]
    * FUZZ: .hta

[Status: 403, Size: 297, Words: 22, Lines: 12, Duration: 196ms]
    * FUZZ: .htaccess

[Status: 403, Size: 297, Words: 22, Lines: 12, Duration: 190ms]
    * FUZZ: .htpasswd

[Status: 200, Size: 168, Words: 16, Lines: 5, Duration: 188ms]
    * FUZZ: index.html

[Status: 401, Size: 460, Words: 42, Lines: 15, Duration: 188ms]
    * FUZZ: protected

[Status: 403, Size: 301, Words: 22, Lines: 12, Duration: 188ms]
    * FUZZ: server-status

[INFO] Starting queued job on target: http://10.10.121.174/guidelines/FUZZ

[Status: 403, Size: 303, Words: 22, Lines: 12, Duration: 192ms]
    * FUZZ: .hta

[Status: 403, Size: 308, Words: 22, Lines: 12, Duration: 186ms]
    * FUZZ: .htaccess

[Status: 403, Size: 308, Words: 22, Lines: 12, Duration: 183ms]
    * FUZZ: .htpasswd

[Status: 200, Size: 51, Words: 8, Lines: 2, Duration: 186ms]
    * FUZZ: index.html

:: Progress: [208971/208971] :: Job [2/2] :: 775 req/sec :: Duration: [0:04:24] :: Errors: 0 ::
```

#### /guidelines
- Had nothing in HTML
- Contained:
	- Hey **bob**, did you update that TomCat server?

#### /protected
- We found what seems to be a user named **bob** under **/guidelines**
	- Used this to attack the page using ![[Hydra#Brute-Forcing HTTP Basic Authentication]]
	- `[80][http-get] host: 10.10.121.174   login: bob   password: bubbles`
##### bob : bubbles
- Page says it moved to another port.
- It moved to **:1234/host-manger**


## Port 1234 Apache Tomcat
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
 :: URL              : http://10.10.121.174:1234/FUZZ
 :: Wordlist         : FUZZ: /usr/share/wordlists/directory_search.txt
 :: Follow redirects : false
 :: Calibration      : false
 :: Timeout          : 10
 :: Threads          : 150
 :: Matcher          : Response status: 200,204,301,302,307,401,403,405,500
________________________________________________

[Status: 302, Size: 0, Words: 1, Lines: 1, Duration: 202ms]
    * FUZZ: docs

[INFO] Adding a new job to the queue: http://10.10.121.174:1234/docs/FUZZ

[Status: 302, Size: 0, Words: 1, Lines: 1, Duration: 201ms]
    * FUZZ: examples

[INFO] Adding a new job to the queue: http://10.10.121.174:1234/examples/FUZZ

[Status: 200, Size: 21630, Words: 19, Lines: 22, Duration: 188ms]
    * FUZZ: favicon.ico

[Status: 302, Size: 0, Words: 1, Lines: 1, Duration: 184ms]
    * FUZZ: host-manager

[INFO] Adding a new job to the queue: http://10.10.121.174:1234/host-manager/FUZZ

[Status: 302, Size: 0, Words: 1, Lines: 1, Duration: 189ms]
    * FUZZ: manager

[INFO] Adding a new job to the queue: http://10.10.121.174:1234/manager/FUZZ

[INFO] Starting queued job on target: http://10.10.121.174:1234/docs/FUZZ

[Status: 302, Size: 0, Words: 1, Lines: 1, Duration: 191ms]
    * FUZZ: api

[INFO] Adding a new job to the queue: http://10.10.121.174:1234/docs/api/FUZZ

[Status: 302, Size: 0, Words: 1, Lines: 1, Duration: 186ms]
    * FUZZ: appdev

[INFO] Adding a new job to the queue: http://10.10.121.174:1234/docs/appdev/FUZZ

[Status: 302, Size: 0, Words: 1, Lines: 1, Duration: 186ms]
    * FUZZ: architecture

[INFO] Adding a new job to the queue: http://10.10.121.174:1234/docs/architecture/FUZZ

[Status: 302, Size: 0, Words: 1, Lines: 1, Duration: 191ms]
    * FUZZ: config

[INFO] Adding a new job to the queue: http://10.10.121.174:1234/docs/config/FUZZ

[Status: 302, Size: 0, Words: 1, Lines: 1, Duration: 194ms]
    * FUZZ: images

[INFO] Adding a new job to the queue: http://10.10.121.174:1234/docs/images/FUZZ

[Status: 200, Size: 19677, Words: 2146, Lines: 283, Duration: 187ms]
    * FUZZ: index.html

[INFO] Starting queued job on target: http://10.10.121.174:1234/examples/FUZZ

[Status: 200, Size: 1285, Words: 157, Lines: 33, Duration: 189ms]
    * FUZZ: index.html

[Status: 302, Size: 0, Words: 1, Lines: 1, Duration: 189ms]
    * FUZZ: jsp

[INFO] Adding a new job to the queue: http://10.10.121.174:1234/examples/jsp/FUZZ

[Status: 302, Size: 0, Words: 1, Lines: 1, Duration: 230ms]
    * FUZZ: servlets

[INFO] Adding a new job to the queue: http://10.10.121.174:1234/examples/servlets/FUZZ

[INFO] Starting queued job on target: http://10.10.121.174:1234/host-manager/FUZZ

[Status: 401, Size: 2098, Words: 359, Lines: 55, Duration: 190ms]
    * FUZZ: html

[Status: 302, Size: 0, Words: 1, Lines: 1, Duration: 188ms]
    * FUZZ: images

[INFO] Adding a new job to the queue: http://10.10.121.174:1234/host-manager/images/FUZZ

[Status: 401, Size: 2098, Words: 359, Lines: 55, Duration: 198ms]
    * FUZZ: text

[INFO] Starting queued job on target: http://10.10.121.174:1234/manager/FUZZ

[Status: 401, Size: 2536, Words: 455, Lines: 64, Duration: 205ms]
    * FUZZ: html

[Status: 302, Size: 0, Words: 1, Lines: 1, Duration: 190ms]
    * FUZZ: images

[INFO] Adding a new job to the queue: http://10.10.121.174:1234/manager/images/FUZZ

[Status: 401, Size: 2536, Words: 455, Lines: 64, Duration: 222ms]
    * FUZZ: status

[Status: 401, Size: 2536, Words: 455, Lines: 64, Duration: 187ms]
    * FUZZ: text

[INFO] Starting queued job on target: http://10.10.121.174:1234/docs/api/FUZZ

[Status: 200, Size: 1329, Words: 180, Lines: 35, Duration: 185ms]
    * FUZZ: index.html

[INFO] Starting queued job on target: http://10.10.121.174:1234/docs/appdev/FUZZ

[Status: 200, Size: 8684, Words: 1149, Lines: 147, Duration: 183ms]
    * FUZZ: index.html

[Status: 302, Size: 0, Words: 1, Lines: 1, Duration: 195ms]
    * FUZZ: sample

[INFO] Adding a new job to the queue: http://10.10.121.174:1234/docs/appdev/sample/FUZZ

[INFO] Starting queued job on target: http://10.10.121.174:1234/docs/architecture/FUZZ

[Status: 200, Size: 7690, Words: 1019, Lines: 137, Duration: 186ms]
    * FUZZ: index.html

[Status: 302, Size: 0, Words: 1, Lines: 1, Duration: 187ms]
    * FUZZ: startup

[INFO] Adding a new job to the queue: http://10.10.121.174:1234/docs/architecture/startup/FUZZ

[INFO] Starting queued job on target: http://10.10.121.174:1234/docs/config/FUZZ

[Status: 200, Size: 11165, Words: 1363, Lines: 167, Duration: 288ms]
    * FUZZ: index.html

[INFO] Starting queued job on target: http://10.10.121.174:1234/docs/images/FUZZ

[INFO] Starting queued job on target: http://10.10.121.174:1234/examples/jsp/FUZZ

[Status: 302, Size: 0, Words: 1, Lines: 1, Duration: 186ms]
    * FUZZ: async

[INFO] Adding a new job to the queue: http://10.10.121.174:1234/examples/jsp/async/FUZZ

[Status: 302, Size: 0, Words: 1, Lines: 1, Duration: 186ms]
    * FUZZ: cal

[INFO] Adding a new job to the queue: http://10.10.121.174:1234/examples/jsp/cal/FUZZ

[Status: 302, Size: 0, Words: 1, Lines: 1, Duration: 187ms]
    * FUZZ: checkbox

[INFO] Adding a new job to the queue: http://10.10.121.174:1234/examples/jsp/checkbox/FUZZ

[Status: 302, Size: 0, Words: 1, Lines: 1, Duration: 189ms]
    * FUZZ: colors

[INFO] Adding a new job to the queue: http://10.10.121.174:1234/examples/jsp/colors/FUZZ

[Status: 302, Size: 0, Words: 1, Lines: 1, Duration: 195ms]
    * FUZZ: dates

[INFO] Adding a new job to the queue: http://10.10.121.174:1234/examples/jsp/dates/FUZZ

[Status: 302, Size: 0, Words: 1, Lines: 1, Duration: 191ms]
    * FUZZ: error

[INFO] Adding a new job to the queue: http://10.10.121.174:1234/examples/jsp/error/FUZZ

[Status: 302, Size: 0, Words: 1, Lines: 1, Duration: 186ms]
    * FUZZ: forward

[INFO] Adding a new job to the queue: http://10.10.121.174:1234/examples/jsp/forward/FUZZ

[Status: 302, Size: 0, Words: 1, Lines: 1, Duration: 753ms]
    * FUZZ: images

[INFO] Adding a new job to the queue: http://10.10.121.174:1234/examples/jsp/images/FUZZ

[Status: 302, Size: 0, Words: 1, Lines: 1, Duration: 184ms]
    * FUZZ: include

[INFO] Adding a new job to the queue: http://10.10.121.174:1234/examples/jsp/include/FUZZ

[Status: 200, Size: 17695, Words: 1150, Lines: 398, Duration: 185ms]
    * FUZZ: index.html

[Status: 302, Size: 0, Words: 1, Lines: 1, Duration: 189ms]
    * FUZZ: jsp2

[INFO] Adding a new job to the queue: http://10.10.121.174:1234/examples/jsp/jsp2/FUZZ

[Status: 302, Size: 0, Words: 1, Lines: 1, Duration: 193ms]
    * FUZZ: num

[INFO] Adding a new job to the queue: http://10.10.121.174:1234/examples/jsp/num/FUZZ

[Status: 302, Size: 0, Words: 1, Lines: 1, Duration: 186ms]
    * FUZZ: plugin

[INFO] Adding a new job to the queue: http://10.10.121.174:1234/examples/jsp/plugin/FUZZ

[Status: 302, Size: 0, Words: 1, Lines: 1, Duration: 188ms]
    * FUZZ: security

[INFO] Adding a new job to the queue: http://10.10.121.174:1234/examples/jsp/security/FUZZ

[Status: 302, Size: 0, Words: 1, Lines: 1, Duration: 190ms]
    * FUZZ: sessions

[INFO] Adding a new job to the queue: http://10.10.121.174:1234/examples/jsp/sessions/FUZZ

[Status: 302, Size: 0, Words: 1, Lines: 1, Duration: 205ms]
    * FUZZ: snp

[INFO] Adding a new job to the queue: http://10.10.121.174:1234/examples/jsp/snp/FUZZ

[Status: 302, Size: 0, Words: 1, Lines: 1, Duration: 193ms]
    * FUZZ: xml

[INFO] Adding a new job to the queue: http://10.10.121.174:1234/examples/jsp/xml/FUZZ

[INFO] Starting queued job on target: http://10.10.121.174:1234/examples/servlets/FUZZ

[Status: 302, Size: 0, Words: 1, Lines: 1, Duration: 192ms]
    * FUZZ: chat

[INFO] Adding a new job to the queue: http://10.10.121.174:1234/examples/servlets/chat/FUZZ

[Status: 302, Size: 0, Words: 1, Lines: 1, Duration: 188ms]
    * FUZZ: images

[INFO] Adding a new job to the queue: http://10.10.121.174:1234/examples/servlets/images/FUZZ

[Status: 200, Size: 7139, Words: 694, Lines: 181, Duration: 187ms]
    * FUZZ: index.html

[INFO] Starting queued job on target: http://10.10.121.174:1234/host-manager/images/FUZZ

[INFO] Starting queued job on target: http://10.10.121.174:1234/manager/images/FUZZ

[INFO] Starting queued job on target: http://10.10.121.174:1234/docs/appdev/sample/FUZZ

[Status: 302, Size: 0, Words: 1, Lines: 1, Duration: 198ms]
    * FUZZ: docs

[INFO] Adding a new job to the queue: http://10.10.121.174:1234/docs/appdev/sample/docs/FUZZ

[Status: 200, Size: 1852, Words: 379, Lines: 46, Duration: 193ms]
    * FUZZ: index.html

[Status: 302, Size: 0, Words: 1, Lines: 1, Duration: 213ms]
    * FUZZ: src

[INFO] Adding a new job to the queue: http://10.10.121.174:1234/docs/appdev/sample/src/FUZZ

[Status: 302, Size: 0, Words: 1, Lines: 1, Duration: 196ms]
    * FUZZ: web
```

#### /host-manager
##### bob : bubbles
- We can upload a `shell.war` generated





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


Created Date: July 26th 2023 (04:01 pm)  
Last Modified Date: <%+tp.file.last_modified_date("MMMM Do YYYY (hh:ss a)")%>

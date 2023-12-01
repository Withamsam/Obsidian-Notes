---
creation date: July 28th 2023
last modified date: July 28th 2023
aliases: []
tags: #🎌
---

Primary Categories: 
Secondary Categories:  
Links: 
Search Tag: #🎌  

# [[THM - Easy Peasy]]  


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
PORT      STATE    SERVICE
80/tcp    open     http
6498/tcp  open     unknown
21052/tcp filtered unknown
65524/tcp open     unknown
```

Enumerated open TCP ports:
```bash
PORT      STATE  SERVICE VERSION
80/tcp    open   http    nginx 1.16.1
| http-robots.txt: 1 disallowed entry 
|_/
|_http-server-header: nginx/1.16.1
|_http-title: Welcome to nginx!
6498/tcp  open   ssh     OpenSSH 7.6p1 Ubuntu 4ubuntu0.3 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   2048 30:4a:2b:22:ac:d9:56:09:f2:da:12:20:57:f4:6c:d4 (RSA)
|   256 bf:86:c9:c7:b7:ef:8c:8b:b9:94:ae:01:88:c0:85:4d (ECDSA)
|_  256 a1:72:ef:6c:81:29:13:ef:5a:6c:24:03:4c:fe:3d:0b (ED25519)
21052/tcp closed unknown
65524/tcp open   http    Apache httpd 2.4.43 ((Ubuntu))
| http-robots.txt: 1 disallowed entry 
|_/
|_http-title: Apache2 Debian Default Page: It works
|_http-server-header: Apache/2.4.43 (Ubuntu)
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel
```

Enumerated top 200 UDP ports:
```bash

```

---

# Enumeration
## Port 80 Ngnix
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
 :: URL              : http://10.10.147.19/FUZZ
 :: Wordlist         : FUZZ: /usr/share/wordlists/directory_search.txt
 :: Follow redirects : false
 :: Calibration      : false
 :: Timeout          : 10
 :: Threads          : 150
 :: Matcher          : Response status: 200,204,301,302,307,401,403,405,500
________________________________________________

[Status: 301, Size: 169, Words: 5, Lines: 8, Duration: 185ms]
    * FUZZ: hidden

[INFO] Adding a new job to the queue: http://10.10.147.19/hidden/FUZZ

[Status: 200, Size: 612, Words: 79, Lines: 26, Duration: 216ms]
    * FUZZ: index.html

[Status: 200, Size: 43, Words: 3, Lines: 4, Duration: 215ms]
    * FUZZ: robots.txt

[INFO] Starting queued job on target: http://10.10.147.19/hidden/FUZZ

[Status: 200, Size: 390, Words: 47, Lines: 19, Duration: 185ms]
    * FUZZ: index.html

[Status: 301, Size: 169, Words: 5, Lines: 8, Duration: 205ms]
    * FUZZ: whatever

[INFO] Adding a new job to the queue: http://10.10.147.19/hidden/whatever/FUZZ

[INFO] Starting queued job on target: http://10.10.147.19/hidden/whatever/FUZZ

[Status: 200, Size: 435, Words: 47, Lines: 22, Duration: 187ms]
    * FUZZ: index.html

:: Progress: [208971/208971] :: Job [3/3] :: 766 req/sec :: Duration: [0:04:22] :: Errors: 0 ::
```


### /robots.txt
```
User-Agent:*
Disallow:/
Robots Not Allowed
```

### /hidden
- Contains an image that is pulled from an outside source:
	- `https://cdn.pixabay.com/photo/2016/12/24/11/48/lost-places-1928727_960_720.jpg`
		- Checked with Stegseek, Binwalk, Strings nothing was found

### /hidden/whatever
```html
ZmxhZ3tmMXJzN19mbDRnfQ==
```
- Decodes to:
	- **flag{f1rs7_fl4g}**
- Contains another image linked to another source:
	- `https://cdn.pixabay.com/photo/2015/05/18/23/53/norway-772991_960_720.jpg`


## Port 65524 Apache
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
 :: URL              : http://10.10.147.19:65524/FUZZ
 :: Wordlist         : FUZZ: /usr/share/wordlists/directory_search.txt
 :: Follow redirects : false
 :: Calibration      : false
 :: Timeout          : 10
 :: Threads          : 150
 :: Matcher          : Response status: 200,204,301,302,307,401,403,405,500
________________________________________________

[Status: 403, Size: 280, Words: 20, Lines: 10, Duration: 182ms]
    * FUZZ: .htaccess

[Status: 403, Size: 280, Words: 20, Lines: 10, Duration: 185ms]
    * FUZZ: .hta

[Status: 403, Size: 280, Words: 20, Lines: 10, Duration: 190ms]
    * FUZZ: .htpasswd

[Status: 200, Size: 10818, Words: 3441, Lines: 371, Duration: 188ms]
    * FUZZ: index.html

[Status: 200, Size: 153, Words: 13, Lines: 7, Duration: 186ms]
    * FUZZ: robots.txt

[Status: 403, Size: 280, Words: 20, Lines: 10, Duration: 178ms]
    * FUZZ: server-status

:: Progress: [208971/208971] :: Job [1/1] :: 788 req/sec :: Duration: [0:04:50] :: Errors: 0 ::
```


### /
- Written in the notes on the page was flag 3:
	- Fl4g 3 : **flag{9fdafbd64c47471a8f54cd3fc64cd312}**
		- The inside portion of the flag is a hash translates to:
			- *candeger*
- Hidden comment in HTML:
	- `ObsJmP173N2X6dOrAgEAL0Vu`
		- Base62 encoded:
			- /n0th1ng3ls3m4tt3r

### /robots.txt
```
User-Agent:*
Disallow:/
Robots Not Allowed
User-Agent:a18672860d0510e5ab6699730763b250
Allow:/
This Flag Can Enter But Only This Flag No More Exceptions
```
- User-Agent decodes to:
	- **flag{1m_s3c0nd_fl4g}**




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

Flag 1 hidden in `/hidden/whatever` = **flag{f1rs7_fl4g}**

Flag 3 hidden in `:65524/` = **flag{9fdafbd64c47471a8f54cd3fc64cd312}**



___

## Resources:

| Hyperlink | Info |
| --------- | ---- |


Created Date: July 28th 2023 (08:46 pm)  
Last Modified Date: <%+tp.file.last_modified_date("MMMM Do YYYY (hh:ss a)")%>

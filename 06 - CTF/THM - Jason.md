---
creation date: July 24th 2023
last modified date: July 24th 2023
aliases: []
tags: #🎌
---

Primary Categories: 
Secondary Categories:  
Links: 
Search Tag: #🎌  

# [[THM - Jason]]  


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
PORT      STATE    SERVICE VERSION
22/tcp    open     ssh     OpenSSH 8.2p1 Ubuntu 4ubuntu0.2 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   3072 5b2d9d60a745de7a99203e4294ce193c (RSA)
|   256 bf32780183af785ee7fe9c834a7daa6b (ECDSA)
|_  256 12ab1380e5ad7307c848d5ca7c7de0af (ED25519)
80/tcp    open     http
| fingerprint-strings: 
|   GetRequest, HTTPOptions: 
|     HTTP/1.1 200 OK
|     Content-Type: text/html
|     Date: Mon, 24 Jul 2023 21:08:18 GMT
|     Connection: close
|     <html><head>
|     <title>Horror LLC</title>
|     <style>
|     body {
|     background: linear-gradient(253deg, #4a040d, #3b0b54, #3a343b);
|     background-size: 300% 300%;
|     -webkit-animation: Background 10s ease infinite;
|     -moz-animation: Background 10s ease infinite;
|     animation: Background 10s ease infinite;
|     @-webkit-keyframes Background {
|     background-position: 0% 50%
|     background-position: 100% 50%
|     100% {
|     background-position: 0% 50%
|     @-moz-keyframes Background {
|     background-position: 0% 50%
|     background-position: 100% 50%
|     100% {
|     background-position: 0% 50%
|     @keyframes Background {
|     background-position: 0% 50%
|_    background-posi
|_http-title: Horror LLC
50616/tcp filtered unknown
1 service unrecognized despite returning data. If you know the service/version, please submit the following fingerprint at https://nmap.org/cgi-bin/submit.cgi?new-service :
SF-Port80-TCP:V=7.93%I=7%D=7/24%Time=64BEE842%P=x86_64-pc-linux-gnu%r(GetR
SF:equest,E4B,"HTTP/1\.1\x20200\x20OK\r\nContent-Type:\x20text/html\r\nDat
SF:e:\x20Mon,\x2024\x20Jul\x202023\x2021:08:18\x20GMT\r\nConnection:\x20cl
SF:ose\r\n\r\n<html><head>\n<title>Horror\x20LLC</title>\n<style>\n\x20\x2
SF:0body\x20{\n\x20\x20\x20\x20background:\x20linear-gradient\(253deg,\x20
SF:#4a040d,\x20#3b0b54,\x20#3a343b\);\n\x20\x20\x20\x20background-size:\x2
SF:0300%\x20300%;\n\x20\x20\x20\x20-webkit-animation:\x20Background\x2010s
SF:\x20ease\x20infinite;\n\x20\x20\x20\x20-moz-animation:\x20Background\x2
SF:010s\x20ease\x20infinite;\n\x20\x20\x20\x20animation:\x20Background\x20
SF:10s\x20ease\x20infinite;\n\x20\x20}\n\x20\x20\n\x20\x20@-webkit-keyfram
SF:es\x20Background\x20{\n\x20\x20\x20\x200%\x20{\n\x20\x20\x20\x20\x20\x2
SF:0background-position:\x200%\x2050%\n\x20\x20\x20\x20}\n\x20\x20\x20\x20
SF:50%\x20{\n\x20\x20\x20\x20\x20\x20background-position:\x20100%\x2050%\n
SF:\x20\x20\x20\x20}\n\x20\x20\x20\x20100%\x20{\n\x20\x20\x20\x20\x20\x20b
SF:ackground-position:\x200%\x2050%\n\x20\x20\x20\x20}\n\x20\x20}\n\x20\x2
SF:0\n\x20\x20@-moz-keyframes\x20Background\x20{\n\x20\x20\x20\x200%\x20{\
SF:n\x20\x20\x20\x20\x20\x20background-position:\x200%\x2050%\n\x20\x20\x2
SF:0\x20}\n\x20\x20\x20\x2050%\x20{\n\x20\x20\x20\x20\x20\x20background-po
SF:sition:\x20100%\x2050%\n\x20\x20\x20\x20}\n\x20\x20\x20\x20100%\x20{\n\
SF:x20\x20\x20\x20\x20\x20background-position:\x200%\x2050%\n\x20\x20\x20\
SF:x20}\n\x20\x20}\n\x20\x20\n\x20\x20@keyframes\x20Background\x20{\n\x20\
SF:x20\x20\x200%\x20{\n\x20\x20\x20\x20\x20\x20background-position:\x200%\
SF:x2050%\n\x20\x20\x20\x20}\n\x20\x20\x20\x2050%\x20{\n\x20\x20\x20\x20\x
SF:20\x20background-posi")%r(HTTPOptions,E4B,"HTTP/1\.1\x20200\x20OK\r\nCo
SF:ntent-Type:\x20text/html\r\nDate:\x20Mon,\x2024\x20Jul\x202023\x2021:08
SF::18\x20GMT\r\nConnection:\x20close\r\n\r\n<html><head>\n<title>Horror\x
SF:20LLC</title>\n<style>\n\x20\x20body\x20{\n\x20\x20\x20\x20background:\
SF:x20linear-gradient\(253deg,\x20#4a040d,\x20#3b0b54,\x20#3a343b\);\n\x20
SF:\x20\x20\x20background-size:\x20300%\x20300%;\n\x20\x20\x20\x20-webkit-
SF:animation:\x20Background\x2010s\x20ease\x20infinite;\n\x20\x20\x20\x20-
SF:moz-animation:\x20Background\x2010s\x20ease\x20infinite;\n\x20\x20\x20\
SF:x20animation:\x20Background\x2010s\x20ease\x20infinite;\n\x20\x20}\n\x2
SF:0\x20\n\x20\x20@-webkit-keyframes\x20Background\x20{\n\x20\x20\x20\x200
SF:%\x20{\n\x20\x20\x20\x20\x20\x20background-position:\x200%\x2050%\n\x20
SF:\x20\x20\x20}\n\x20\x20\x20\x2050%\x20{\n\x20\x20\x20\x20\x20\x20backgr
SF:ound-position:\x20100%\x2050%\n\x20\x20\x20\x20}\n\x20\x20\x20\x20100%\
SF:x20{\n\x20\x20\x20\x20\x20\x20background-position:\x200%\x2050%\n\x20\x
SF:20\x20\x20}\n\x20\x20}\n\x20\x20\n\x20\x20@-moz-keyframes\x20Background
SF:\x20{\n\x20\x20\x20\x200%\x20{\n\x20\x20\x20\x20\x20\x20background-posi
SF:tion:\x200%\x2050%\n\x20\x20\x20\x20}\n\x20\x20\x20\x2050%\x20{\n\x20\x
SF:20\x20\x20\x20\x20background-position:\x20100%\x2050%\n\x20\x20\x20\x20
SF:}\n\x20\x20\x20\x20100%\x20{\n\x20\x20\x20\x20\x20\x20background-positi
SF:on:\x200%\x2050%\n\x20\x20\x20\x20}\n\x20\x20}\n\x20\x20\n\x20\x20@keyf
SF:rames\x20Background\x20{\n\x20\x20\x20\x200%\x20{\n\x20\x20\x20\x20\x20
SF:\x20background-position:\x200%\x2050%\n\x20\x20\x20\x20}\n\x20\x20\x20\
SF:x2050%\x20{\n\x20\x20\x20\x20\x20\x20background-posi");
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel
```

Enumerated top 200 UDP ports:
```bash

```

---

# Enumeration
## Port 


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


Created Date: July 24th 2023 (04:00 pm)  
Last Modified Date: <%+tp.file.last_modified_date("MMMM Do YYYY (hh:ss a)")%>

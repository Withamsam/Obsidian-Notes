---
creation date: July 20th 2023
last modified date: July 20th 2023
aliases: []
tags: #🎌
---

Primary Categories: 
Secondary Categories:  
Links: 
Search Tag: #🎌  

# [[THM - Insekube]]  


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
22/tcp open  ssh     OpenSSH 8.2p1 Ubuntu 4ubuntu0.3 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   3072 9f:ae:04:9e:f0:75:ed:b7:39:80:a0:d8:7f:bd:61:06 (RSA)
|   256 cf:cb:89:62:99:11:d7:ca:cd:5b:57:78:10:d0:6c:82 (ECDSA)
|_  256 5f:11:10:0d:7c:80:a3:fc:d1:d5:43:4e:49:f9:c8:d2 (ED25519)
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel](<PORT   STATE SERVICE VERSION
22/tcp open  ssh     OpenSSH 8.2p1 Ubuntu 4ubuntu0.3 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   3072 9f:ae:04:9e:f0:75:ed:b7:39:80:a0:d8:7f:bd:61:06 (RSA)
|   256 cf:cb:89:62:99:11:d7:ca:cd:5b:57:78:10:d0:6c:82 (ECDSA)
|_  256 5f:11:10:0d:7c:80:a3:fc:d1:d5:43:4e:49:f9:c8:d2 (ED25519)
80/tcp open  http
| fingerprint-strings: 
|   GetRequest: 
|     HTTP/1.1 200 OK
|     Date: Thu, 20 Jul 2023 23:41:42 GMT
|     Content-Type: text/html; charset=utf-8
|     Content-Length: 1196
|     Connection: close
|     %3C!DOCTYPE html%3E
|     <head>
|     <link rel="stylesheet" href="https://stackpath.bootstrapcdn.com/bootstrap/4.5.2/css/bootstrap.min.css"
|     integrity="sha384-JcKb8q3iqJ61gNV9KGb8thSsNjpSL0n8PARn9HuZOnIxN0hoP+VmmDGMN5t9UJ0Z" crossorigin="anonymous">
|     <style>
|     body,
|     html {
|     height: 100%;
|     </style>
|     </head>
|     <body>
|     <div class="container h-100">
|     <div class="row mt-5">
|     <div class="col-12 mb-4">
|     class="text-center">Check if a website is down 
|     </h3>
|     </div>
|     <form class="col-6 mx-auto" action="/">
|     <div class=" input-group">
|     <input name="hostname" value="" type="text" class="form-control" placeholder="Hostname"
|   HTTPOptions, RTSPRequest: 
|     HTTP/1.1 405 Method Not Allowed
|     Date: Thu, 20 Jul 2023 23:41:42 GMT
|     Content-Type: text/plain; charset=utf-8
|     Content-Length: 18
|     Allow: GET, HEAD
|     Connection: close
|_    Method Not Allowed
|_http-title: Site doesn't have a title (text/html; charset=utf-8).
1 service unrecognized despite returning data. If you know the service/version, please submit the following fingerprint at https://nmap.org/cgi-bin/submit.cgi?new-service :
SF-Port80-TCP:V=7.94%I=7%D=7/20%Time=64B9C635%P=x86_64-pc-linux-gnu%r(GetR
SF:equest,535,"HTTP/1\.1\x20200\x20OK\r\nDate:\x20Thu,\x2020\x20Jul\x20202
SF:3\x2023:41:42\x20GMT\r\nContent-Type:\x20text/html;\x20charset=utf-8\r\
SF:nContent-Length:\x201196\r\nConnection:\x20close\r\n\r\n<!DOCTYPE\x20ht
SF:ml>\n\n<head>\n\x20\x20\x20\x20<link\x20rel=\"stylesheet\"\x20href=\"ht
SF:tps://stackpath\.bootstrapcdn\.com/bootstrap/4\.5\.2/css/bootstrap\.min
SF:\.css\"\n\x20\x20\x20\x20\x20\x20\x20\x20integrity=\"sha384-JcKb8q3iqJ6
SF:1gNV9KGb8thSsNjpSL0n8PARn9HuZOnIxN0hoP\+VmmDGMN5t9UJ0Z\"\x20crossorigin
SF:=\"anonymous\">\n\x20\x20\x20\x20<style>\n\x20\x20\x20\x20\x20\x20\x20\
SF:x20body,\n\x20\x20\x20\x20\x20\x20\x20\x20html\x20{\n\x20\x20\x20\x20\x
SF:20\x20\x20\x20\x20\x20\x20\x20height:\x20100%;\n\x20\x20\x20\x20\x20\x2
SF:0\x20\x20}\n\x20\x20\x20\x20</style>\n</head>\n\n<body>\n\x20\x20\x20\x
SF:20<div\x20class=\"container\x20h-100\">\n\x20\x20\x20\x20\x20\x20\x20\x
SF:20<div\x20class=\"row\x20mt-5\">\n\x20\x20\x20\x20\x20\x20\x20\x20\x20\
SF:x20\x20\x20<div\x20class=\"col-12\x20mb-4\">\n\x20\x20\x20\x20\x20\x20\
SF:x20\x20\x20\x20\x20\x20\x20\x20\x20\x20<h3\x20class=\"text-center\">Che
SF:ck\x20if\x20a\x20website\x20is\x20down\x20\xf0\x9f\x92\xa3</h3>\n\x20\x
SF:20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20</div>\n\x20\x20\x20\x20\x20\
SF:x20\x20\x20\x20\x20\x20\x20<form\x20class=\"col-6\x20mx-auto\"\x20actio
SF:n=\"/\">\n\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\
SF:x20<div\x20class=\"\x20input-group\">\n\x20\x20\x20\x20\x20\x20\x20\x20
SF:\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20<input\x20name=\"hostna
SF:me\"\x20value=\"\"\x20type=\"text\"\x20class=\"form-control\"\x20placeh
SF:older=\"Hostname\"\n\x20\x20\x20\x20\x20\x20\x20")%r(HTTPOptions,BC,"HT
SF:TP/1\.1\x20405\x20Method\x20Not\x20Allowed\r\nDate:\x20Thu,\x2020\x20Ju
SF:l\x202023\x2023:41:42\x20GMT\r\nContent-Type:\x20text/plain;\x20charset
SF:=utf-8\r\nContent-Length:\x2018\r\nAllow:\x20GET,\x20HEAD\r\nConnection
SF::\x20close\r\n\r\nMethod\x20Not\x20Allowed")%r(RTSPRequest,BC,"HTTP/1\.
SF:1\x20405\x20Method\x20Not\x20Allowed\r\nDate:\x20Thu,\x2020\x20Jul\x202
SF:023\x2023:41:42\x20GMT\r\nContent-Type:\x20text/plain;\x20charset=utf-8
SF:\r\nContent-Length:\x2018\r\nAllow:\x20GET,\x20HEAD\r\nConnection:\x20c
SF:lose\r\n\r\nMethod\x20Not\x20Allowed");
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel>)
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

Worked through the machine and found its broken on final root step

Attempted to host my own reg for it and still couldnt get it to work

Ended up grabbing final flag from a walkthrough since it being broken had nothing to do with what I was doing to complete it

root.txt = *flag{30180a273e7da821a7fe4af22ffd1701}*


___

## Resources:

| Hyperlink | Info |
| --------- | ---- |


Created Date: July 20th 2023 (06:04 pm)  
Last Modified Date: <%+tp.file.last_modified_date("MMMM Do YYYY (hh:ss a)")%>

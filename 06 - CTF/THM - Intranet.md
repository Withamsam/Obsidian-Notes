---
creation date: August 3rd 2023
last modified date: August 3rd 2023
aliases: []
tags: #🎌
---

Primary Categories: 
Secondary Categories:  
Links: 
Search Tag: #🎌  

# [[THM - Intranet]]  


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
7/tcp    open  echo
21/tcp   open  ftp
22/tcp   open  ssh
23/tcp   open  telnet
80/tcp   open  http
8080/tcp open  http-proxy
```

Enumerated open TCP ports:
```bash
PORT     STATE SERVICE    VERSION
7/tcp    open  echo
21/tcp   open  ftp        vsftpd 3.0.3
22/tcp   open  ssh        OpenSSH 8.2p1 Ubuntu 4ubuntu0.5 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   3072 3d:0b:6f:e8:24:0d:28:91:8a:57:4d:13:b2:47:d9:44 (RSA)
|   256 9a:84:1c:a3:e3:7a:8f:4a:bb:6e:89:2d:f6:21:d5:f2 (ECDSA)
|_  256 22:30:9e:17:08:45:9c:a8:73:d3:5a:3c:d7:5b:da:f3 (ED25519)
23/tcp   open  telnet     Linux telnetd
80/tcp   open  http       Apache httpd 2.4.41 ((Ubuntu))
|_http-server-header: Apache/2.4.41 (Ubuntu)
|_http-title: Site doesn't have a title (text/html).
8080/tcp open  http-proxy Werkzeug/2.2.2 Python/3.8.10
|_http-server-header: Werkzeug/2.2.2 Python/3.8.10
| http-title: Site doesn't have a title (text/html; charset=utf-8).
|_Requested resource was /login
| fingerprint-strings: 
|   FourOhFourRequest: 
|     HTTP/1.1 404 NOT FOUND
|     Server: Werkzeug/2.2.2 Python/3.8.10
|     Date: Fri, 04 Aug 2023 02:58:44 GMT
|     Content-Type: text/html; charset=utf-8
|     Content-Length: 207
|     Connection: close
|     <!doctype html>
|     <html lang=en>
|     <title>404 Not Found</title>
|     <h1>Not Found</h1>
|     <p>The requested URL was not found on the server. If you entered the URL manually please check your spelling and try again.</p>
|   GetRequest: 
|     HTTP/1.1 302 FOUND
|     Server: Werkzeug/2.2.2 Python/3.8.10
|     Date: Fri, 04 Aug 2023 02:58:43 GMT
|     Content-Type: text/html; charset=utf-8
|     Content-Length: 199
|     Location: /login
|     Connection: close
|     <!doctype html>
|     <html lang=en>
|     <title>Redirecting...</title>
|     <h1>Redirecting...</h1>
|     <p>You should be redirected automatically to the target URL: <a href="/login">/login</a>. If not, click the link.
|   HTTPOptions: 
|     HTTP/1.1 200 OK
|     Server: Werkzeug/2.2.2 Python/3.8.10
|     Date: Fri, 04 Aug 2023 02:58:43 GMT
|     Content-Type: text/html; charset=utf-8
|     Allow: OPTIONS, GET, HEAD
|     Content-Length: 0
|     Connection: close
|   RTSPRequest: 
|     <!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01//EN"
|     "http://www.w3.org/TR/html4/strict.dtd">
|     <html>
|     <head>
|     <meta http-equiv="Content-Type" content="text/html;charset=utf-8">
|     <title>Error response</title>
|     </head>
|     <body>
|     <h1>Error response</h1>
|     <p>Error code: 400</p>
|     <p>Message: Bad request version ('RTSP/1.0').</p>
|     <p>Error code explanation: HTTPStatus.BAD_REQUEST - Bad request syntax or unsupported method.</p>
|     </body>
|_    </html>
1 service unrecognized despite returning data. If you know the service/version, please submit the following fingerprint at https://nmap.org/cgi-bin/submit.cgi?new-service :
SF-Port8080-TCP:V=7.94%I=7%D=8/3%Time=64CC6964%P=x86_64-pc-linux-gnu%r(Get
SF:Request,18A,"HTTP/1\.1\x20302\x20FOUND\r\nServer:\x20Werkzeug/2\.2\.2\x
SF:20Python/3\.8\.10\r\nDate:\x20Fri,\x2004\x20Aug\x202023\x2002:58:43\x20
SF:GMT\r\nContent-Type:\x20text/html;\x20charset=utf-8\r\nContent-Length:\
SF:x20199\r\nLocation:\x20/login\r\nConnection:\x20close\r\n\r\n<!doctype\
SF:x20html>\n<html\x20lang=en>\n<title>Redirecting\.\.\.</title>\n<h1>Redi
SF:recting\.\.\.</h1>\n<p>You\x20should\x20be\x20redirected\x20automatical
SF:ly\x20to\x20the\x20target\x20URL:\x20<a\x20href=\"/login\">/login</a>\.
SF:\x20If\x20not,\x20click\x20the\x20link\.\n")%r(HTTPOptions,C7,"HTTP/1\.
SF:1\x20200\x20OK\r\nServer:\x20Werkzeug/2\.2\.2\x20Python/3\.8\.10\r\nDat
SF:e:\x20Fri,\x2004\x20Aug\x202023\x2002:58:43\x20GMT\r\nContent-Type:\x20
SF:text/html;\x20charset=utf-8\r\nAllow:\x20OPTIONS,\x20GET,\x20HEAD\r\nCo
SF:ntent-Length:\x200\r\nConnection:\x20close\r\n\r\n")%r(RTSPRequest,1F4,
SF:"<!DOCTYPE\x20HTML\x20PUBLIC\x20\"-//W3C//DTD\x20HTML\x204\.01//EN\"\n\
SF:x20\x20\x20\x20\x20\x20\x20\x20\"http://www\.w3\.org/TR/html4/strict\.d
SF:td\">\n<html>\n\x20\x20\x20\x20<head>\n\x20\x20\x20\x20\x20\x20\x20\x20
SF:<meta\x20http-equiv=\"Content-Type\"\x20content=\"text/html;charset=utf
SF:-8\">\n\x20\x20\x20\x20\x20\x20\x20\x20<title>Error\x20response</title>
SF:\n\x20\x20\x20\x20</head>\n\x20\x20\x20\x20<body>\n\x20\x20\x20\x20\x20
SF:\x20\x20\x20<h1>Error\x20response</h1>\n\x20\x20\x20\x20\x20\x20\x20\x2
SF:0<p>Error\x20code:\x20400</p>\n\x20\x20\x20\x20\x20\x20\x20\x20<p>Messa
SF:ge:\x20Bad\x20request\x20version\x20\('RTSP/1\.0'\)\.</p>\n\x20\x20\x20
SF:\x20\x20\x20\x20\x20<p>Error\x20code\x20explanation:\x20HTTPStatus\.BAD
SF:_REQUEST\x20-\x20Bad\x20request\x20syntax\x20or\x20unsupported\x20metho
SF:d\.</p>\n\x20\x20\x20\x20</body>\n</html>\n")%r(FourOhFourRequest,184,"
SF:HTTP/1\.1\x20404\x20NOT\x20FOUND\r\nServer:\x20Werkzeug/2\.2\.2\x20Pyth
SF:on/3\.8\.10\r\nDate:\x20Fri,\x2004\x20Aug\x202023\x2002:58:44\x20GMT\r\
SF:nContent-Type:\x20text/html;\x20charset=utf-8\r\nContent-Length:\x20207
SF:\r\nConnection:\x20close\r\n\r\n<!doctype\x20html>\n<html\x20lang=en>\n
SF:<title>404\x20Not\x20Found</title>\n<h1>Not\x20Found</h1>\n<p>The\x20re
SF:quested\x20URL\x20was\x20not\x20found\x20on\x20the\x20server\.\x20If\x2
SF:0you\x20entered\x20the\x20URL\x20manually\x20please\x20check\x20your\x2
SF:0spelling\x20and\x20try\x20again\.</p>\n");
Service Info: OSs: Unix, Linux; CPE: cpe:/o:linux:linux_kernel

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 109.71 seconds
```

Enumerated top 200 UDP ports:
```bash

```

---

# Enumeration
## Port 8080
### HTML Source /
```
<!--- Any bugs? Please report them to our developer team. We have an open bug bounty program!
  For any inquiries, contact devops@securesolacoders.no.
  Sincerely, anders (Senior Developer) -->
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


Created Date: August 3rd 2023 (09:26 pm)  
Last Modified Date: <%+tp.file.last_modified_date("MMMM Do YYYY (hh:ss a)")%>

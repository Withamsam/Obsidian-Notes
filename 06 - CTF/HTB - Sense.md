---
creation date: August 15th 2023
last modified date: August 15th 2023
aliases: []
tags: #🎌
---

Primary Categories: 
Secondary Categories:  
Links: 
Search Tag: #🎌  

# [[HTB - Sense]]  


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
PORT    STATE SERVICE
80/tcp  open  http
443/tcp open  https
```

Enumerated open TCP ports:
```bash
PORT    STATE SERVICE  VERSION
80/tcp  open  http     lighttpd 1.4.35
|_http-title: Did not follow redirect to https://10.129.120.14/
|_http-server-header: lighttpd/1.4.35
443/tcp open  ssl/http lighttpd 1.4.35
| ssl-cert: Subject: commonName=Common Name (eg, YOUR name)/organizationName=CompanyName/stateOrProvinceName=Somewhere/countryName=US
| Not valid before: 2017-10-14T19:21:35
|_Not valid after:  2023-04-06T19:21:35
|_ssl-date: TLS randomness does not represent time
|_http-server-header: lighttpd/1.4.35
|_http-title: Login
```

Enumerated top 200 UDP ports:
```bash

```

---

# Enumeration
## Port 443
### Wappalyzer
- lighttpd 1.4.35
- jQuery 1.6.2
- PHP

### Creds
#### rohit : pfsense

### ffuf directory_search.txt
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
 :: URL              : https://10.129.120.14/FUZZ
 :: Wordlist         : FUZZ: /usr/share/wordlists/directory_search.txt
 :: Follow redirects : false
 :: Calibration      : false
 :: Timeout          : 10
 :: Threads          : 150
 :: Matcher          : Response status: 200,204,301,302,307,401,403,405,500
________________________________________________

[Status: 403, Size: 345, Words: 33, Lines: 12, Duration: 68ms]
    * FUZZ: %7echeckout%7e

[Status: 301, Size: 0, Words: 1, Lines: 1, Duration: 61ms]
    * FUZZ: classes

[INFO] Adding a new job to the queue: https://10.129.120.14/classes/FUZZ

[Status: 301, Size: 0, Words: 1, Lines: 1, Duration: 56ms]
    * FUZZ: csrf

[INFO] Adding a new job to the queue: https://10.129.120.14/csrf/FUZZ

[Status: 301, Size: 0, Words: 1, Lines: 1, Duration: 57ms]
    * FUZZ: css

[INFO] Adding a new job to the queue: https://10.129.120.14/css/FUZZ

[Status: 200, Size: 1406, Words: 3, Lines: 7, Duration: 66ms]
    * FUZZ: favicon.ico

[Status: 301, Size: 0, Words: 1, Lines: 1, Duration: 55ms]
    * FUZZ: filebrowser

[INFO] Adding a new job to the queue: https://10.129.120.14/filebrowser/FUZZ

[Status: 301, Size: 0, Words: 1, Lines: 1, Duration: 47ms]
    * FUZZ: includes

[INFO] Adding a new job to the queue: https://10.129.120.14/includes/FUZZ

[Status: 200, Size: 329, Words: 32, Lines: 25, Duration: 47ms]
    * FUZZ: index.html

[Status: 200, Size: 6690, Words: 907, Lines: 174, Duration: 63ms]
    * FUZZ: index.php

[Status: 301, Size: 0, Words: 1, Lines: 1, Duration: 53ms]
    * FUZZ: installer

[INFO] Adding a new job to the queue: https://10.129.120.14/installer/FUZZ

[Status: 301, Size: 0, Words: 1, Lines: 1, Duration: 60ms]
    * FUZZ: javascript

[INFO] Adding a new job to the queue: https://10.129.120.14/javascript/FUZZ

[Status: 301, Size: 0, Words: 1, Lines: 1, Duration: 57ms]
    * FUZZ: shortcuts

[INFO] Adding a new job to the queue: https://10.129.120.14/shortcuts/FUZZ

[Status: 301, Size: 0, Words: 1, Lines: 1, Duration: 54ms]
    * FUZZ: themes

[INFO] Adding a new job to the queue: https://10.129.120.14/themes/FUZZ

[Status: 301, Size: 0, Words: 1, Lines: 1, Duration: 56ms]
    * FUZZ: tree

[INFO] Adding a new job to the queue: https://10.129.120.14/tree/FUZZ

[Status: 301, Size: 0, Words: 1, Lines: 1, Duration: 332ms]
    * FUZZ: widgets

[INFO] Adding a new job to the queue: https://10.129.120.14/widgets/FUZZ

[Status: 301, Size: 0, Words: 1, Lines: 1, Duration: 60ms]
    * FUZZ: wizards

[INFO] Adding a new job to the queue: https://10.129.120.14/wizards/FUZZ

[Status: 200, Size: 384, Words: 78, Lines: 17, Duration: 70ms]
    * FUZZ: xmlrpc.php

[INFO] Starting queued job on target: https://10.129.120.14/classes/FUZZ

[Status: 403, Size: 345, Words: 33, Lines: 12, Duration: 49ms]
    * FUZZ: %7echeckout%7e

[INFO] Starting queued job on target: https://10.129.120.14/csrf/FUZZ

[Status: 403, Size: 345, Words: 33, Lines: 12, Duration: 60ms]
    * FUZZ: %7echeckout%7e

[INFO] Starting queued job on target: https://10.129.120.14/css/FUZZ

[Status: 403, Size: 345, Words: 33, Lines: 12, Duration: 60ms]
    * FUZZ: %7echeckout%7e

[INFO] Starting queued job on target: https://10.129.120.14/filebrowser/FUZZ

[Status: 403, Size: 345, Words: 33, Lines: 12, Duration: 66ms]
    * FUZZ: %7echeckout%7e

[Status: 301, Size: 0, Words: 1, Lines: 1, Duration: 58ms]
    * FUZZ: images

[INFO] Adding a new job to the queue: https://10.129.120.14/filebrowser/images/FUZZ

[INFO] Starting queued job on target: https://10.129.120.14/includes/FUZZ

[Status: 403, Size: 345, Words: 33, Lines: 12, Duration: 349ms]
    * FUZZ: %7echeckout%7e

[INFO] Starting queued job on target: https://10.129.120.14/installer/FUZZ

[Status: 403, Size: 345, Words: 33, Lines: 12, Duration: 51ms]
    * FUZZ: %7echeckout%7e

[Status: 302, Size: 0, Words: 1, Lines: 1, Duration: 66ms]
    * FUZZ: index.php

[INFO] Starting queued job on target: https://10.129.120.14/javascript/FUZZ

[Status: 403, Size: 345, Words: 33, Lines: 12, Duration: 55ms]
    * FUZZ: %7echeckout%7e

[Status: 301, Size: 0, Words: 1, Lines: 1, Duration: 58ms]
    * FUZZ: chosen

[INFO] Adding a new job to the queue: https://10.129.120.14/javascript/chosen/FUZZ

[Status: 301, Size: 0, Words: 1, Lines: 1, Duration: 54ms]
    * FUZZ: index

[INFO] Adding a new job to the queue: https://10.129.120.14/javascript/index/FUZZ

[Status: 301, Size: 0, Words: 1, Lines: 1, Duration: 56ms]
    * FUZZ: jquery

[INFO] Adding a new job to the queue: https://10.129.120.14/javascript/jquery/FUZZ

[Status: 301, Size: 0, Words: 1, Lines: 1, Duration: 55ms]
    * FUZZ: scriptaculous

[INFO] Adding a new job to the queue: https://10.129.120.14/javascript/scriptaculous/FUZZ

[Status: 301, Size: 0, Words: 1, Lines: 1, Duration: 55ms]
    * FUZZ: wizard

[INFO] Adding a new job to the queue: https://10.129.120.14/javascript/wizard/FUZZ

[INFO] Starting queued job on target: https://10.129.120.14/shortcuts/FUZZ

[Status: 403, Size: 345, Words: 33, Lines: 12, Duration: 59ms]
    * FUZZ: %7echeckout%7e

[INFO] Starting queued job on target: https://10.129.120.14/themes/FUZZ

[Status: 403, Size: 345, Words: 33, Lines: 12, Duration: 55ms]
    * FUZZ: %7echeckout%7e

[Status: 301, Size: 0, Words: 1, Lines: 1, Duration: 55ms]
    * FUZZ: code-red

[INFO] Adding a new job to the queue: https://10.129.120.14/themes/code-red/FUZZ

[INFO] Starting queued job on target: https://10.129.120.14/tree/FUZZ

[Status: 403, Size: 345, Words: 33, Lines: 12, Duration: 57ms]
    * FUZZ: %7echeckout%7e

[Status: 200, Size: 7492, Words: 828, Lines: 229, Duration: 55ms]
    * FUZZ: index.html

[INFO] Starting queued job on target: https://10.129.120.14/widgets/FUZZ

[Status: 403, Size: 345, Words: 33, Lines: 12, Duration: 60ms]
    * FUZZ: %7echeckout%7e

[Status: 301, Size: 0, Words: 1, Lines: 1, Duration: 66ms]
    * FUZZ: include

[INFO] Adding a new job to the queue: https://10.129.120.14/widgets/include/FUZZ

[Status: 301, Size: 0, Words: 1, Lines: 1, Duration: 60ms]
    * FUZZ: javascript

[INFO] Adding a new job to the queue: https://10.129.120.14/widgets/javascript/FUZZ

[Status: 301, Size: 0, Words: 1, Lines: 1, Duration: 186ms]
    * FUZZ: widgets
```

### ffuf raft-large-files.txt
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
 :: URL              : https://10.129.120.14/FUZZ
 :: Wordlist         : FUZZ: /usr/share/wordlists/seclists/Discovery/Web-Content/raft-large-files.txt
 :: Follow redirects : false
 :: Calibration      : false
 :: Timeout          : 10
 :: Threads          : 150
 :: Matcher          : Response status: 200,204,301,302,307,401,403,405,500
________________________________________________

[Status: 200, Size: 329, Words: 32, Lines: 25, Duration: 50ms]
    * FUZZ: index.html

[Status: 200, Size: 1406, Words: 3, Lines: 7, Duration: 49ms]
    * FUZZ: favicon.ico

[Status: 200, Size: 384, Words: 78, Lines: 17, Duration: 48ms]
    * FUZZ: xmlrpc.php

[Status: 200, Size: 6690, Words: 907, Lines: 174, Duration: 67ms]
    * FUZZ: index.php

[Status: 200, Size: 6689, Words: 907, Lines: 174, Duration: 56ms]
    * FUZZ: help.php

[Status: 200, Size: 6689, Words: 907, Lines: 174, Duration: 53ms]
    * FUZZ: edit.php

[Status: 200, Size: 6690, Words: 907, Lines: 174, Duration: 54ms]
    * FUZZ: stats.php

[Status: 200, Size: 6690, Words: 907, Lines: 174, Duration: 56ms]
    * FUZZ: .

[Status: 403, Size: 345, Words: 33, Lines: 12, Duration: 59ms]
    * FUZZ: extension.inc

[Status: 200, Size: 6691, Words: 907, Lines: 174, Duration: 50ms]
    * FUZZ: status.php

[Status: 403, Size: 345, Words: 33, Lines: 12, Duration: 48ms]
    * FUZZ: .inc

[Status: 403, Size: 345, Words: 33, Lines: 12, Duration: 53ms]
    * FUZZ: adovbs.inc

[Status: 403, Size: 345, Words: 33, Lines: 12, Duration: 50ms]
    * FUZZ: var.inc

[Status: 200, Size: 271, Words: 35, Lines: 10, Duration: 57ms]
    * FUZZ: changelog.txt

[Status: 200, Size: 6692, Words: 907, Lines: 174, Duration: 61ms]
    * FUZZ: license.php

[Status: 200, Size: 6691, Words: 907, Lines: 174, Duration: 63ms]
    * FUZZ: system.php

[Status: 200, Size: 6690, Words: 907, Lines: 174, Duration: 66ms]
    * FUZZ: graph.php

[Status: 403, Size: 345, Words: 33, Lines: 12, Duration: 65ms]
    * FUZZ: ~.inc

[Status: 403, Size: 345, Words: 33, Lines: 12, Duration: 50ms]
    * FUZZ: footer.inc

[Status: 403, Size: 345, Words: 33, Lines: 12, Duration: 57ms]
    * FUZZ: header.inc

[Status: 200, Size: 6691, Words: 907, Lines: 174, Duration: 76ms]
    * FUZZ: wizard.php

[Status: 403, Size: 345, Words: 33, Lines: 12, Duration: 57ms]
    * FUZZ: geoip.inc

[Status: 403, Size: 345, Words: 33, Lines: 12, Duration: 53ms]
    * FUZZ: common.inc

[Status: 403, Size: 345, Words: 33, Lines: 12, Duration: 52ms]
    * FUZZ: config.inc

[Status: 403, Size: 345, Words: 33, Lines: 12, Duration: 56ms]
    * FUZZ: connect.inc

[Status: 403, Size: 345, Words: 33, Lines: 12, Duration: 66ms]
    * FUZZ: license.inc

[Status: 403, Size: 345, Words: 33, Lines: 12, Duration: 51ms]
    * FUZZ: menu.inc

[Status: 403, Size: 345, Words: 33, Lines: 12, Duration: 59ms]
    * FUZZ: validation_user.inc

[Status: 403, Size: 345, Words: 33, Lines: 12, Duration: 58ms]
    * FUZZ: weather.inc

[Status: 200, Size: 6689, Words: 907, Lines: 174, Duration: 64ms]
    * FUZZ: exec.php

[Status: 403, Size: 345, Words: 33, Lines: 12, Duration: 53ms]
    * FUZZ: install-utils.inc

[Status: 403, Size: 345, Words: 33, Lines: 12, Duration: 46ms]
    * FUZZ: test.inc

[Status: 403, Size: 345, Words: 33, Lines: 12, Duration: 54ms]
    * FUZZ: _footer.inc

[Status: 403, Size: 345, Words: 33, Lines: 12, Duration: 54ms]
    * FUZZ: amengaming.inc

[Status: 403, Size: 345, Words: 33, Lines: 12, Duration: 57ms]
    * FUZZ: auth.inc

[Status: 403, Size: 345, Words: 33, Lines: 12, Duration: 61ms]
    * FUZZ: banners.inc

[Status: 403, Size: 345, Words: 33, Lines: 12, Duration: 56ms]
    * FUZZ: biglogo.inc

[Status: 403, Size: 345, Words: 33, Lines: 12, Duration: 54ms]
    * FUZZ: bottommenu.inc

[Status: 403, Size: 345, Words: 33, Lines: 12, Duration: 49ms]
    * FUZZ: c_functions.inc

[Status: 403, Size: 345, Words: 33, Lines: 12, Duration: 48ms]
    * FUZZ: casing.inc

[Status: 403, Size: 345, Words: 33, Lines: 12, Duration: 49ms]
    * FUZZ: countcomments.inc

[Status: 403, Size: 345, Words: 33, Lines: 12, Duration: 48ms]
    * FUZZ: db.inc

[Status: 403, Size: 345, Words: 33, Lines: 12, Duration: 51ms]
    * FUZZ: excel.inc

[Status: 403, Size: 345, Words: 33, Lines: 12, Duration: 49ms]
    * FUZZ: extensions.inc

[Status: 403, Size: 345, Words: 33, Lines: 12, Duration: 51ms]
    * FUZZ: findcasinos.inc

[Status: 403, Size: 345, Words: 33, Lines: 12, Duration: 51ms]
    * FUZZ: findadvertisers.inc

[Status: 403, Size: 345, Words: 33, Lines: 12, Duration: 54ms]
    * FUZZ: findtenants.inc

[Status: 403, Size: 345, Words: 33, Lines: 12, Duration: 58ms]
    * FUZZ: geoipcity.inc

[Status: 403, Size: 345, Words: 33, Lines: 12, Duration: 62ms]
    * FUZZ: getdetails.inc

[Status: 403, Size: 345, Words: 33, Lines: 12, Duration: 69ms]
    * FUZZ: getheading.inc

[Status: 403, Size: 345, Words: 33, Lines: 12, Duration: 63ms]
    * FUZZ: getname.inc

[Status: 403, Size: 345, Words: 33, Lines: 12, Duration: 62ms]
    * FUZZ: getstate.inc

[Status: 403, Size: 345, Words: 33, Lines: 12, Duration: 69ms]
    * FUZZ: gmkt.inc

[Status: 403, Size: 345, Words: 33, Lines: 12, Duration: 51ms]
    * FUZZ: headerrow.inc

[Status: 403, Size: 345, Words: 33, Lines: 12, Duration: 65ms]
    * FUZZ: index.php~

[Status: 403, Size: 345, Words: 33, Lines: 12, Duration: 52ms]
    * FUZZ: init.inc

[Status: 403, Size: 345, Words: 33, Lines: 12, Duration: 50ms]
    * FUZZ: leftAd.inc

[Status: 403, Size: 345, Words: 33, Lines: 12, Duration: 49ms]
    * FUZZ: links.inc

[Status: 403, Size: 345, Words: 33, Lines: 12, Duration: 50ms]
    * FUZZ: logit.inc

[Status: 403, Size: 345, Words: 33, Lines: 12, Duration: 53ms]
    * FUZZ: mail.inc

[Status: 403, Size: 345, Words: 33, Lines: 12, Duration: 54ms]
    * FUZZ: news.inc

[Status: 403, Size: 345, Words: 33, Lines: 12, Duration: 51ms]
    * FUZZ: quikblogs.inc

[Status: 403, Size: 345, Words: 33, Lines: 12, Duration: 51ms]
    * FUZZ: quiklistold.inc

[Status: 403, Size: 345, Words: 33, Lines: 12, Duration: 51ms]
    * FUZZ: quiklist.inc

[Status: 403, Size: 345, Words: 33, Lines: 12, Duration: 51ms]
    * FUZZ: quikliststatic.inc

[Status: 403, Size: 345, Words: 33, Lines: 12, Duration: 52ms]
    * FUZZ: ratertable.inc

[Status: 403, Size: 345, Words: 33, Lines: 12, Duration: 64ms]
    * FUZZ: rightad.inc

[Status: 403, Size: 345, Words: 33, Lines: 12, Duration: 54ms]
    * FUZZ: sc_check_logon.inc

[Status: 403, Size: 345, Words: 33, Lines: 12, Duration: 53ms]
    * FUZZ: setup.inc

[Status: 403, Size: 345, Words: 33, Lines: 12, Duration: 50ms]
    * FUZZ: showbriefs.inc

[Status: 403, Size: 345, Words: 33, Lines: 12, Duration: 52ms]
    * FUZZ: showcomments.inc

[Status: 403, Size: 345, Words: 33, Lines: 12, Duration: 51ms]
    * FUZZ: sidebar.inc

[Status: 403, Size: 345, Words: 33, Lines: 12, Duration: 54ms]
    * FUZZ: tendetails.inc

[Status: 403, Size: 345, Words: 33, Lines: 12, Duration: 56ms]
    * FUZZ: top.inc

[Status: 403, Size: 345, Words: 33, Lines: 12, Duration: 49ms]
    * FUZZ: upload.inc

[Status: 403, Size: 345, Words: 33, Lines: 12, Duration: 57ms]
    * FUZZ: uscfstats.inc

:: Progress: [37050/37050] :: Job [1/1] :: 901 req/sec :: Duration: [0:00:24] :: Errors: 1 ::
```






### ffuf /FUZZ.txt
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
 :: URL              : https://10.129.120.14/FUZZ.txt
 :: Wordlist         : FUZZ: /usr/share/wordlists/directory_search.txt
 :: Follow redirects : false
 :: Calibration      : false
 :: Timeout          : 10
 :: Threads          : 150
 :: Matcher          : Response status: 200,204,301,302,307,401,403,405,500
________________________________________________

[Status: 200, Size: 271, Words: 35, Lines: 10, Duration: 51ms]
    * FUZZ: changelog

[Status: 200, Size: 106, Words: 9, Lines: 7, Duration: 319ms]
    * FUZZ: system-users

:: Progress: [208971/208971] :: Job [1/1] :: 555 req/sec :: Duration: [0:02:33] :: Errors: 0 ::
```

### /index.html
```html
<HTML>
<BODY>
<center>
<img src='fred.png'>
<p>
    <A HREF='/dfuife.cgi'>Begin installation</A>
</p>
<!--
<p>
    Connect to host via SSH: 
    <applet CODEBASE="." ARCHIVE="jta20.jar" CODE="de.mud.jta.Applet" WIDTH=55 HEIGHT=25>
	<param NAME="config" VALUE="applet.conf">
    </applet>
</p>
-->
</center>
</BODY>
</HTML>

```

### /system-users.txt
```
####Support ticket###

Please create the following user


username: Rohit
password: company defaults
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


Created Date: August 15th 2023 (08:50 pm)  
Last Modified Date: <%+tp.file.last_modified_date("MMMM Do YYYY (hh:ss a)")%>

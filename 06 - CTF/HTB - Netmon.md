---
creation date: August 17th 2023
last modified date: August 17th 2023
aliases: []
tags: #🎌
---

Primary Categories: 
Secondary Categories:  
Links: 
Search Tag: #🎌  

# [[HTB - Netmon]]  


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
PORT      STATE SERVICE
21/tcp    open  ftp
80/tcp    open  http
135/tcp   open  msrpc
139/tcp   open  netbios-ssn
445/tcp   open  microsoft-ds
5985/tcp  open  wsman
47001/tcp open  winrm
49664/tcp open  unknown
49665/tcp open  unknown
49666/tcp open  unknown
49667/tcp open  unknown
49668/tcp open  unknown
49669/tcp open  unknown
```

Enumerated open TCP ports:
```bash
PORT      STATE SERVICE      VERSION
21/tcp    open  ftp          Microsoft ftpd
| ftp-anon: Anonymous FTP login allowed (FTP code 230)
| 02-03-19  12:18AM                 1024 .rnd
| 02-25-19  10:15PM       <DIR>          inetpub
| 07-16-16  09:18AM       <DIR>          PerfLogs
| 02-25-19  10:56PM       <DIR>          Program Files
| 02-03-19  12:28AM       <DIR>          Program Files (x86)
| 02-03-19  08:08AM       <DIR>          Users
|_02-25-19  11:49PM       <DIR>          Windows
| ftp-syst: 
|_  SYST: Windows_NT
80/tcp    open  http         Indy httpd 18.1.37.13946 (Paessler PRTG bandwidth monitor)
|_http-server-header: PRTG/18.1.37.13946
|_http-trane-info: Problem with XML parsing of /evox/about
| http-title: Welcome | PRTG Network Monitor (NETMON)
|_Requested resource was /index.htm
135/tcp   open  msrpc        Microsoft Windows RPC
139/tcp   open  netbios-ssn  Microsoft Windows netbios-ssn
445/tcp   open  microsoft-ds Microsoft Windows Server 2008 R2 - 2012 microsoft-ds
5985/tcp  open  http         Microsoft HTTPAPI httpd 2.0 (SSDP/UPnP)
|_http-server-header: Microsoft-HTTPAPI/2.0
|_http-title: Not Found
47001/tcp open  http         Microsoft HTTPAPI httpd 2.0 (SSDP/UPnP)
|_http-title: Not Found
|_http-server-header: Microsoft-HTTPAPI/2.0
49664/tcp open  msrpc        Microsoft Windows RPC
49665/tcp open  msrpc        Microsoft Windows RPC
49666/tcp open  msrpc        Microsoft Windows RPC
49667/tcp open  msrpc        Microsoft Windows RPC
49668/tcp open  msrpc        Microsoft Windows RPC
49669/tcp open  msrpc        Microsoft Windows RPC
Service Info: OSs: Windows, Windows Server 2008 R2 - 2012; CPE: cpe:/o:microsoft:windows

Host script results:
| smb2-time: 
|   date: 2023-08-18T01:21:26
|_  start_date: 2023-08-18T01:15:47
| smb-security-mode: 
|   authentication_level: user
|   challenge_response: supported
|_  message_signing: disabled (dangerous, but default)
| smb2-security-mode: 
|   3:1:1: 
|_    Message signing enabled but not required
|_clock-skew: mean: 1s, deviation: 0s, median: 0s
```

Enumerated top 200 UDP ports:
```bash

```

---

# Enumeration
## Port 80


## Port 21
C:\ProgramData\Paessler\PRTG Network Monitor

```
	      <!-- User: prtgadmin -->
	      PrTg@dmin2018
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

# Steps
1. Started with an *nmap* scan of the target
2. Located about a dozen ports open the ones of note are *21* and *80*
3. Using port *21* we can access this with anonymous user
	1. Once in we can navigate to `/Users/Public/`
		1. Using `cat user.txt` from here we get the users key
4. Next up we should check out what the website being hosted is
	1. We see it is a PRTG monitor running version *18.1.37.13946* found in the comment in source code of login page
		1. Searching for information about this version and we find that it is vulnerable to a *Authenticated RCE*
		2. Since we need to be authenticated I tried the default creds of `prtgadmin:prtgadmin` with no luck
		3. Now that we have an idea of a possible exploit lets see if we locate the creds stored on the target using the FTP connection we managed to get at the start
5. Going back to FTP sign in with anonymous user
	1. I googled where config for PRTG are stored and found it stores them under
		1. `C:\ProgramData\Paessler\PRTG Network Monitor`
		2. Navigating to this we see there was a backup created of the old config
		3. I downloaded all three that I found and started searching
		4. Under the `.old.bak` file I found a user of `prtgadmin:PrTg@dmin2018`
			1. I tried these on the website and they failed
			2. Thinking they might have updated the password since they created a backup of the configuration file I tweaked the "old pw" that we currently have
			3. Found that the following creds worked and allowed us in
				1. `prtgadmin:PrTg@dmin2019`
				2. They just updated the year which I like because its a very common thing for people to do when they need to constantly update passwords
6. Now that we have access to a *PRTG Administrator* we can try that RCE I found a script written in python that will callback to us and create a shell we simply need to give it our credentials and the target/callback IP/port
7. After giving those ran the command and it opened a shell
	1. My shell was a bit buggy giving error every so often but it would run commands no problem so I just moved forward
	2. Using `whoami` we find that we have a System user!!
	3. I went straight to the `C:/Users/Administrator/` folder and then moved into `/Desktop` since the main directory had not root.txt
	4. Success we found a *root.txt* file under the Desktop of the Admin user `print` was failing to work so used `more` instead to show the contents of the file



---

# Trophy & Loot




___

## Resources:

| Hyperlink | Info |
| --------- | ---- |


Created Date: August 17th 2023 (08:26 pm)  
Last Modified Date: <%+tp.file.last_modified_date("MMMM Do YYYY (hh:ss a)")%>

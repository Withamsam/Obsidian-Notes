---
creation date: May 20th 2023
last modified date: May 20th 2023
aliases: []
tags: #🎌
---

Primary Categories: 
Secondary Categories:  
Links: 
Search Tag: #🎌  

# [[HTB - Blue]]  


# Resolution summary
- Ended up being simple Eternal Blue Exploit

## Improved skills
- Enumerating SMB shares
- Exploiting using Metasploit

## Used tools
- [[nmap]]
- [[Metasploit]]
- [[SMB]]

---

# Information Gathering
Scanned all TCP ports:
```bash
PORT      STATE SERVICE
135/tcp   open  msrpc
139/tcp   open  netbios-ssn
445/tcp   open  microsoft-ds
49152/tcp open  unknown
49153/tcp open  unknown
49154/tcp open  unknown
49155/tcp open  unknown
49156/tcp open  unknown
49157/tcp open  unknown
```

Enumerated open TCP ports:
```bash
PORT      STATE SERVICE      VERSION
135/tcp   open  msrpc        Microsoft Windows RPC
139/tcp   open  netbios-ssn  Microsoft Windows netbios-ssn
445/tcp   open  microsoft-ds Windows 7 Professional 7601 Service Pack 1 microsoft-ds (workgroup: WORKGROUP)
49152/tcp open  msrpc        Microsoft Windows RPC
49153/tcp open  msrpc        Microsoft Windows RPC
49154/tcp open  msrpc        Microsoft Windows RPC
49155/tcp open  msrpc        Microsoft Windows RPC
49156/tcp open  msrpc        Microsoft Windows RPC
49157/tcp open  msrpc        Microsoft Windows RPC
Service Info: Host: HARIS-PC; OS: Windows; CPE: cpe:/o:microsoft:windows

Host script results:
| smb2-security-mode: 
|   210: 
|_    Message signing enabled but not required
| smb2-time: 
|   date: 2023-05-20T18:48:47
|_  start_date: 2023-05-20T18:44:09
| smb-security-mode: 
|   account_used: guest
|   authentication_level: user
|   challenge_response: supported
|_  message_signing: disabled (dangerous, but default)
| smb-os-discovery: 
|   OS: Windows 7 Professional 7601 Service Pack 1 (Windows 7 Professional 6.1)
|   OS CPE: cpe:/o:microsoft:windows_7::sp1:professional
|   Computer name: haris-PC
|   NetBIOS computer name: HARIS-PC\x00
|   Workgroup: WORKGROUP\x00
|_  System time: 2023-05-20T19:48:49+01:00
|_clock-skew: mean: -19m55s, deviation: 34m35s, median: 1s
```

Enumerated top 200 UDP ports:
```bash

```

---

# Enumeration
## Port 445 (microsoft-ds)
Enumerating SMB:
```SMB
└─$ smbclient -N -L //10.129.196.40

	Sharename       Type      Comment
	---------       ----      -------
	ADMIN$          Disk      Remote Admin
	C$              Disk      Default share
	IPC$            IPC       Remote IPC
	Share           Disk      
	Users           Disk      
```


---

# Exploitation
## Eternal Blue
This exploit can be done through [[Metasploit]] but I should figure out how to do it without needing the consoles interface.


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
user.txt = **4d4daaf837c9a90dd174146ce2f1012f**
root.txt = **e378c5f5b1f91bebb81326dc44629ab6**

___

## Resources:

| Hyperlink                                       | Info     |
| ----------------------------------------------- | -------- |
| [HTB](https://app.hackthebox.com/machines/Blue) | Finished | 


Created Date: May 20th 2023 (01:59 pm)  
Last Modified Date: <%+tp.file.last_modified_date("MMMM Do YYYY (hh:ss a)")%>

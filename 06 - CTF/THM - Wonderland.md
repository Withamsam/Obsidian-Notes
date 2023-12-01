---
creation date: April 16th 2023
last modified date: April 16th 2023
aliases: []
tags: #🎌
---

Primary Categories: { Add link(s) [[]] back to related PRIMARY categories }
Secondary Categories:  { Add link(s) [[]] back to related SECONDARY categories }
Links: {Add link(s) [[]] to related terms}
Search Tag: #🎌  

# [[THM - Wonderland]]  


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
22/tcp open  ssh     OpenSSH 7.6p1 Ubuntu 4ubuntu0.3 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   2048 8eeefb96cead70dd05a93b0db071b863 (RSA)
|   256 7a927944164f204350a9a847e2c2be84 (ECDSA)
|_  256 000b8044e63d4b6947922c55147e2ac9 (ED25519)
80/tcp open  http    Golang net/http server (Go-IPFS json-rpc or InfluxDB API)
|_http-title: Follow the white rabbit.
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel
```

Enumerated top 200 UDP ports:
```bash
All 65535 scanned ports on 10.10.89.94 are in ignored states.
Not shown: 65506 open|filtered udp ports (no-response), 29 closed udp ports (port-unreach)
```

---

# Enumeration
## Port 80
Listed below is my ffuf scan in the process of running this with a recursive setting turned on I found that the sub-domains of the site spell out "rabbit". `http:<SITE IP>/r/a/b/b/i/t`

### ffuf scan
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
 :: URL              : http://10.10.168.235/FUZZ
 :: Wordlist         : FUZZ: /usr/share/wordlists/directory_search.txt
 :: Follow redirects : false
 :: Calibration      : false
 :: Timeout          : 10
 :: Threads          : 150
 :: Matcher          : Response status: 200,204,301,302,307,401,403,405,500
________________________________________________

[Status: 301, Size: 0, Words: 1, Lines: 1, Duration: 187ms]
    * FUZZ: img

[INFO] Adding a new job to the queue: http://10.10.168.235/img/FUZZ

[Status: 301, Size: 0, Words: 1, Lines: 1, Duration: 197ms]
    * FUZZ: index.html

[Status: 301, Size: 0, Words: 1, Lines: 1, Duration: 181ms]
    * FUZZ: poem

[INFO] Adding a new job to the queue: http://10.10.168.235/poem/FUZZ

[Status: 301, Size: 0, Words: 1, Lines: 1, Duration: 182ms]
    * FUZZ: r

[INFO] Adding a new job to the queue: http://10.10.168.235/r/FUZZ

[INFO] Starting queued job on target: http://10.10.168.235/img/FUZZ

[Status: 301, Size: 0, Words: 1, Lines: 1, Duration: 207ms]
    * FUZZ: index.html

[INFO] Starting queued job on target: http://10.10.168.235/poem/FUZZ

[Status: 301, Size: 0, Words: 1, Lines: 1, Duration: 191ms]
    * FUZZ: index.html

[INFO] Starting queued job on target: http://10.10.168.235/r/FUZZ

[Status: 301, Size: 0, Words: 1, Lines: 1, Duration: 193ms]
    * FUZZ: a

[INFO] Adding a new job to the queue: http://10.10.168.235/r/a/FUZZ

[Status: 301, Size: 0, Words: 1, Lines: 1, Duration: 187ms]
    * FUZZ: index.html

[INFO] Starting queued job on target: http://10.10.168.235/r/a/FUZZ

[Status: 301, Size: 0, Words: 1, Lines: 1, Duration: 185ms]
    * FUZZ: b

[INFO] Adding a new job to the queue: http://10.10.168.235/r/a/b/FUZZ

[Status: 301, Size: 0, Words: 1, Lines: 1, Duration: 192ms]
    * FUZZ: index.html

[INFO] Starting queued job on target: http://10.10.168.235/r/a/b/FUZZ

[Status: 301, Size: 0, Words: 1, Lines: 1, Duration: 189ms]
    * FUZZ: b

[INFO] Adding a new job to the queue: http://10.10.168.235/r/a/b/b/FUZZ

[Status: 301, Size: 0, Words: 1, Lines: 1, Duration: 182ms]
    * FUZZ: index.html

[INFO] Starting queued job on target: http://10.10.168.235/r/a/b/b/FUZZ

[Status: 301, Size: 0, Words: 1, Lines: 1, Duration: 184ms]
    * FUZZ: i

[INFO] Adding a new job to the queue: http://10.10.168.235/r/a/b/b/i/FUZZ

[Status: 301, Size: 0, Words: 1, Lines: 1, Duration: 188ms]
    * FUZZ: index.html

[INFO] Starting queued job on target: http://10.10.168.235/r/a/b/b/i/FUZZ

[Status: 301, Size: 0, Words: 1, Lines: 1, Duration: 192ms]
    * FUZZ: index.html

[Status: 301, Size: 0, Words: 1, Lines: 1, Duration: 190ms]
    * FUZZ: t

[INFO] Adding a new job to the queue: http://10.10.168.235/r/a/b/b/i/t/FUZZ

[INFO] Starting queued job on target: http://10.10.168.235/r/a/b/b/i/t/FUZZ

[Status: 301, Size: 0, Words: 1, Lines: 1, Duration: 189ms]
    * FUZZ: index.html

:: Progress: [208972/208972] :: Job [9/9] :: 772 req/sec :: Duration: [0:04:23] :: Errors: 0 ::
```

#### /img
- Checked with [[binwalk]] & [[steghide]] no password used
	- *alice_door.jpg*
		- 0             0x0             JPEG image data, JFIF standard 1.02
		- 30            0x1E            TIFF image data, big-endian, offset of first image directory: 8
		- 332           0x14C           JPEG image data, JFIF standard 1.02
		- 12721         0x31B1          XML document, version: "1.0"
		- 21743         0x54EF          JPEG image data, JFIF standard 1.02
	- *alice_door.png*
	- *white_rabbit_1.jpg*
		- Steghide gave a `hint.txt`
			- `follow the r a b b i t`

#### /poem
- Contained lore

#### /r
- # Keep Going.
- "Would you tell me, please, which way I ought to go from here?"

#### /r/a
- # Keep Going.
- "That depends a good deal on where you want to get to," said the Cat.

#### /r/a/b
- # Keep Going.
- "I don’t much care where—" said Alice.

#### /r/a/b/b
- # Keep Going.
- "Then it doesn’t matter which way you go," said the Cat.

#### /r/a/b/b/i
- # Keep Going.
- "—so long as I get somewhere,"" Alice added as an explanation.

#### /r/a/b/b/i/t
- # Open the door and enter wonderland
- "Oh, you’re sure to do that," said the Cat, "if you only walk long enough."
- Alice felt that this could not be denied, so she tried another question. "What sort of people live about here?"
- "In that direction,"" the Cat said, waving its right paw round, "lives a Hatter: and in that direction," waving the other paw, "lives a March Hare. Visit either you like: they’re both mad."
	- Included the image we found above *alice_door.png*
	- Found credentials in the source of this page
		- *alice* : *HowDothTheLittleCrocodileImproveHisShiningTail*




## Old ffuf scan
### ffuf scan
```bash

        /'___\  /'___\           /'___\       
       /\ \__/ /\ \__/  __  __  /\ \__/       
       \ \ ,__\\ \ ,__\/\ \/\ \ \ \ ,__\      
        \ \ \_/ \ \ \_/\ \ \_\ \ \ \ \_/      
         \ \_\   \ \_\  \ \____/  \ \_\       
          \/_/    \/_/   \/___/    \/_/       

       v2.0.0-dev
________________________________________________

 :: Method           : GET
 :: URL              : http://10.10.89.94/FUZZ
 :: Wordlist         : FUZZ: /usr/share/seclists/Discovery/Web-Content/directory-list-lowercase-2.3-medium.txt
 :: Follow redirects : false
 :: Calibration      : false
 :: Timeout          : 10
 :: Threads          : 40
 :: Matcher          : Response status: 200,204,301,302,307,401,403,405,500
________________________________________________

[Status: 301, Size: 0, Words: 1, Lines: 1, Duration: 191ms]
    * FUZZ: img

[INFO] Adding a new job to the queue: http://10.10.89.94/img/FUZZ

[Status: 301, Size: 0, Words: 1, Lines: 1, Duration: 187ms]
    * FUZZ: r

[INFO] Adding a new job to the queue: http://10.10.89.94/r/FUZZ

[Status: 301, Size: 0, Words: 1, Lines: 1, Duration: 182ms]
    * FUZZ: poem

[INFO] Adding a new job to the queue: http://10.10.89.94/poem/FUZZ

[Status: 301, Size: 0, Words: 1, Lines: 1, Duration: 188ms]
    * FUZZ: http%3a%2f%2fwww

[Status: 200, Size: 402, Words: 55, Lines: 10, Duration: 179ms]
    * FUZZ: 

[Status: 301, Size: 0, Words: 1, Lines: 1, Duration: 186ms]
    * FUZZ: http%3a%2f%2fyoutube

[Status: 301, Size: 0, Words: 1, Lines: 1, Duration: 185ms]
    * FUZZ: http%3a%2f%2fblogs

[Status: 301, Size: 0, Words: 1, Lines: 1, Duration: 188ms]
    * FUZZ: http%3a%2f%2fblog

[Status: 301, Size: 0, Words: 1, Lines: 1, Duration: 188ms]
    * FUZZ: **http%3a%2f%2fwww

[Status: 301, Size: 0, Words: 1, Lines: 1, Duration: 186ms]
    * FUZZ: http%3a%2f%2fcommunity

[Status: 301, Size: 0, Words: 1, Lines: 1, Duration: 179ms]
    * FUZZ: http%3a%2f%2fradar

[Status: 301, Size: 0, Words: 1, Lines: 1, Duration: 181ms]
    * FUZZ: http%3a%2f%2fjeremiahgrossman

[Status: 301, Size: 0, Words: 1, Lines: 1, Duration: 180ms]
    * FUZZ: http%3a%2f%2fweblog

[Status: 301, Size: 0, Words: 1, Lines: 1, Duration: 180ms]
    * FUZZ: http%3a%2f%2fswik

[INFO] Starting queued job on target: http://10.10.89.94/img/FUZZ

[Status: 301, Size: 0, Words: 1, Lines: 1, Duration: 178ms]
    * FUZZ: http%3a%2f%2fwww

[Status: 200, Size: 153, Words: 4, Lines: 6, Duration: 180ms]
    * FUZZ: 

[Status: 301, Size: 0, Words: 1, Lines: 1, Duration: 179ms]
    * FUZZ: http%3a%2f%2fyoutube

[Status: 301, Size: 0, Words: 1, Lines: 1, Duration: 188ms]
    * FUZZ: http%3a%2f%2fblogs

[Status: 301, Size: 0, Words: 1, Lines: 1, Duration: 187ms]
    * FUZZ: http%3a%2f%2fblog

[Status: 301, Size: 0, Words: 1, Lines: 1, Duration: 181ms]
    * FUZZ: **http%3a%2f%2fwww

[Status: 301, Size: 0, Words: 1, Lines: 1, Duration: 183ms]
    * FUZZ: http%3a%2f%2fcommunity

[Status: 301, Size: 0, Words: 1, Lines: 1, Duration: 209ms]
    * FUZZ: http%3a%2f%2fradar

[Status: 301, Size: 0, Words: 1, Lines: 1, Duration: 180ms]
    * FUZZ: http%3a%2f%2fjeremiahgrossman

[Status: 301, Size: 0, Words: 1, Lines: 1, Duration: 179ms]
    * FUZZ: http%3a%2f%2fweblog

[Status: 301, Size: 0, Words: 1, Lines: 1, Duration: 191ms]
    * FUZZ: http%3a%2f%2fswik

[INFO] Starting queued job on target: http://10.10.89.94/r/FUZZ

[Status: 301, Size: 0, Words: 1, Lines: 1, Duration: 186ms]
    * FUZZ: a

[INFO] Adding a new job to the queue: http://10.10.89.94/r/a/FUZZ

[Status: 301, Size: 0, Words: 1, Lines: 1, Duration: 180ms]
    * FUZZ: http%3a%2f%2fwww

[Status: 200, Size: 258, Words: 37, Lines: 9, Duration: 187ms]
    * FUZZ: 

[Status: 301, Size: 0, Words: 1, Lines: 1, Duration: 201ms]
    * FUZZ: http%3a%2f%2fyoutube

[Status: 301, Size: 0, Words: 1, Lines: 1, Duration: 181ms]
    * FUZZ: http%3a%2f%2fblogs

[Status: 301, Size: 0, Words: 1, Lines: 1, Duration: 185ms]
    * FUZZ: http%3a%2f%2fblog

[Status: 301, Size: 0, Words: 1, Lines: 1, Duration: 182ms]
    * FUZZ: **http%3a%2f%2fwww

[Status: 301, Size: 0, Words: 1, Lines: 1, Duration: 180ms]
    * FUZZ: http%3a%2f%2fcommunity

[Status: 301, Size: 0, Words: 1, Lines: 1, Duration: 185ms]
    * FUZZ: http%3a%2f%2fradar

[Status: 301, Size: 0, Words: 1, Lines: 1, Duration: 184ms]
    * FUZZ: http%3a%2f%2fjeremiahgrossman

[Status: 301, Size: 0, Words: 1, Lines: 1, Duration: 183ms]
    * FUZZ: http%3a%2f%2fweblog

[Status: 301, Size: 0, Words: 1, Lines: 1, Duration: 186ms]
    * FUZZ: http%3a%2f%2fswik

[INFO] Starting queued job on target: http://10.10.89.94/poem/FUZZ

[Status: 301, Size: 0, Words: 1, Lines: 1, Duration: 190ms]
    * FUZZ: http%3a%2f%2fwww

[Status: 200, Size: 1565, Words: 426, Lines: 42, Duration: 179ms]
    * FUZZ: 

[Status: 301, Size: 0, Words: 1, Lines: 1, Duration: 183ms]
    * FUZZ: http%3a%2f%2fyoutube

[Status: 301, Size: 0, Words: 1, Lines: 1, Duration: 191ms]
    * FUZZ: http%3a%2f%2fblogs

[Status: 301, Size: 0, Words: 1, Lines: 1, Duration: 188ms]
    * FUZZ: http%3a%2f%2fblog

[Status: 301, Size: 0, Words: 1, Lines: 1, Duration: 179ms]
    * FUZZ: **http%3a%2f%2fwww

[Status: 301, Size: 0, Words: 1, Lines: 1, Duration: 181ms]
    * FUZZ: http%3a%2f%2fcommunity

[Status: 301, Size: 0, Words: 1, Lines: 1, Duration: 192ms]
    * FUZZ: http%3a%2f%2fradar

[Status: 301, Size: 0, Words: 1, Lines: 1, Duration: 183ms]
    * FUZZ: http%3a%2f%2fjeremiahgrossman

[Status: 301, Size: 0, Words: 1, Lines: 1, Duration: 183ms]
    * FUZZ: http%3a%2f%2fweblog

[Status: 301, Size: 0, Words: 1, Lines: 1, Duration: 185ms]
    * FUZZ: http%3a%2f%2fswik

[INFO] Starting queued job on target: http://10.10.89.94/r/a/FUZZ

[Status: 301, Size: 0, Words: 1, Lines: 1, Duration: 187ms]
    * FUZZ: b

[INFO] Adding a new job to the queue: http://10.10.89.94/r/a/b/FUZZ

[Status: 301, Size: 0, Words: 1, Lines: 1, Duration: 188ms]
    * FUZZ: http%3a%2f%2fwww

[Status: 200, Size: 264, Words: 39, Lines: 9, Duration: 184ms]
    * FUZZ: 

[Status: 301, Size: 0, Words: 1, Lines: 1, Duration: 178ms]
    * FUZZ: http%3a%2f%2fyoutube

[Status: 301, Size: 0, Words: 1, Lines: 1, Duration: 184ms]
    * FUZZ: http%3a%2f%2fblogs

[Status: 301, Size: 0, Words: 1, Lines: 1, Duration: 182ms]
    * FUZZ: http%3a%2f%2fblog

[Status: 301, Size: 0, Words: 1, Lines: 1, Duration: 183ms]
    * FUZZ: **http%3a%2f%2fwww

[Status: 301, Size: 0, Words: 1, Lines: 1, Duration: 186ms]
    * FUZZ: http%3a%2f%2fcommunity

[Status: 301, Size: 0, Words: 1, Lines: 1, Duration: 184ms]
    * FUZZ: http%3a%2f%2fradar

[Status: 301, Size: 0, Words: 1, Lines: 1, Duration: 187ms]
    * FUZZ: http%3a%2f%2fjeremiahgrossman

[Status: 301, Size: 0, Words: 1, Lines: 1, Duration: 187ms]
    * FUZZ: http%3a%2f%2fweblog

[Status: 301, Size: 0, Words: 1, Lines: 1, Duration: 182ms]
    * FUZZ: http%3a%2f%2fswik

[INFO] Starting queued job on target: http://10.10.89.94/r/a/b/FUZZ

[Status: 301, Size: 0, Words: 1, Lines: 1, Duration: 186ms]
    * FUZZ: b

[INFO] Adding a new job to the queue: http://10.10.89.94/r/a/b/b/FUZZ

[Status: 301, Size: 0, Words: 1, Lines: 1, Duration: 192ms]
    * FUZZ: http%3a%2f%2fwww

[Status: 200, Size: 237, Words: 31, Lines: 9, Duration: 189ms]
    * FUZZ: 

[Status: 301, Size: 0, Words: 1, Lines: 1, Duration: 185ms]
    * FUZZ: http%3a%2f%2fyoutube

[Status: 301, Size: 0, Words: 1, Lines: 1, Duration: 180ms]
    * FUZZ: http%3a%2f%2fblogs

[Status: 301, Size: 0, Words: 1, Lines: 1, Duration: 186ms]
    * FUZZ: http%3a%2f%2fblog

[Status: 301, Size: 0, Words: 1, Lines: 1, Duration: 190ms]
    * FUZZ: **http%3a%2f%2fwww

[Status: 301, Size: 0, Words: 1, Lines: 1, Duration: 189ms]
    * FUZZ: http%3a%2f%2fcommunity

[Status: 301, Size: 0, Words: 1, Lines: 1, Duration: 186ms]
    * FUZZ: http%3a%2f%2fradar

[Status: 301, Size: 0, Words: 1, Lines: 1, Duration: 214ms]
    * FUZZ: http%3a%2f%2fjeremiahgrossman

[Status: 301, Size: 0, Words: 1, Lines: 1, Duration: 186ms]
    * FUZZ: http%3a%2f%2fweblog

[Status: 301, Size: 0, Words: 1, Lines: 1, Duration: 184ms]
    * FUZZ: http%3a%2f%2fswik

[INFO] Starting queued job on target: http://10.10.89.94/r/a/b/b/FUZZ

[Status: 301, Size: 0, Words: 1, Lines: 1, Duration: 181ms]
    * FUZZ: i

[INFO] Adding a new job to the queue: http://10.10.89.94/r/a/b/b/i/FUZZ

[Status: 301, Size: 0, Words: 1, Lines: 1, Duration: 187ms]
    * FUZZ: http%3a%2f%2fwww

[Status: 200, Size: 253, Words: 35, Lines: 9, Duration: 192ms]
    * FUZZ: 

[Status: 301, Size: 0, Words: 1, Lines: 1, Duration: 181ms]
    * FUZZ: http%3a%2f%2fyoutube

[Status: 301, Size: 0, Words: 1, Lines: 1, Duration: 182ms]
    * FUZZ: http%3a%2f%2fblogs

[Status: 301, Size: 0, Words: 1, Lines: 1, Duration: 236ms]
    * FUZZ: http%3a%2f%2fblog

[Status: 301, Size: 0, Words: 1, Lines: 1, Duration: 179ms]
    * FUZZ: **http%3a%2f%2fwww

[Status: 301, Size: 0, Words: 1, Lines: 1, Duration: 185ms]
    * FUZZ: http%3a%2f%2fcommunity

[Status: 301, Size: 0, Words: 1, Lines: 1, Duration: 180ms]
    * FUZZ: http%3a%2f%2fradar

[Status: 301, Size: 0, Words: 1, Lines: 1, Duration: 188ms]
    * FUZZ: http%3a%2f%2fjeremiahgrossman

[Status: 301, Size: 0, Words: 1, Lines: 1, Duration: 185ms]
    * FUZZ: http%3a%2f%2fweblog

[Status: 301, Size: 0, Words: 1, Lines: 1, Duration: 184ms]
    * FUZZ: http%3a%2f%2fswik

[INFO] Starting queued job on target: http://10.10.89.94/r/a/b/b/i/FUZZ

[Status: 301, Size: 0, Words: 1, Lines: 1, Duration: 185ms]
    * FUZZ: t

[INFO] Adding a new job to the queue: http://10.10.89.94/r/a/b/b/i/t/FUZZ

[Status: 301, Size: 0, Words: 1, Lines: 1, Duration: 186ms]
    * FUZZ: http%3a%2f%2fwww

[Status: 200, Size: 259, Words: 35, Lines: 9, Duration: 190ms]
    * FUZZ: 

[WARN] Caught keyboard interrupt (Ctrl-C)

[INFO] Starting queued job on target: http://10.10.89.94/r/a/b/b/i/t/FUZZ

```


##

---

# Exploitation
## Name of the technique


---

# Lateral Movement to user
## Local Enumeration
### alice : HowDothTheLittleCrocodileImproveHisShiningTail
- root.txt is in this users home directory but we cant access it without root first
- `sudo -l`
	- Showed we could run a python file located in our home directory but only contained lore
- `find / -type f -perm -4000 2>/dev/null` - SUID
	- A familiar program stood out *pkexec*
		- I checked the machine version of Linux and it matches that this exploit will work


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


Created Date: April 16th 2023 (06:18 pm)  
Last Modified Date: <%+tp.file.last_modified_date("MMMM Do YYYY (hh:ss a)")%>

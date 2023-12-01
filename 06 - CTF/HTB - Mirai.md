---
creation date: June 1st 2023
last modified date: June 1st 2023
aliases: []
tags: #🎌
---

Primary Categories: 
Secondary Categories:  
Links: 
Search Tag: #🎌  

# [[HTB - Mirai]]  


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
22/tcp    open  ssh
53/tcp    open  domain
80/tcp    open  http
1498/tcp  open  watcom-sql
32400/tcp open  plex
32469/tcp open  unknown
```

Enumerated open TCP ports:
```bash
PORT      STATE SERVICE VERSION
22/tcp    open  ssh     OpenSSH 6.7p1 Debian 5+deb8u3 (protocol 2.0)
| ssh-hostkey: 
|   1024 aaef5ce08e86978247ff4ae5401890c5 (DSA)
|   2048 e8c19dc543abfe61233bd7e4af9b7418 (RSA)
|   256 b6a07838d0c810948b44b2eaa017422b (ECDSA)
|_  256 4d6840f720c4e552807a4438b8a2a752 (ED25519)
53/tcp    open  domain  dnsmasq 2.76
| dns-nsid: 
|_  bind.version: dnsmasq-2.76
80/tcp    open  http    lighttpd 1.4.35
|_http-title: Site doesn't have a title (text/html; charset=UTF-8).
|_http-server-header: lighttpd/1.4.35
1498/tcp  open  upnp    Platinum UPnP 1.0.5.13 (UPnP/1.0 DLNADOC/1.50)
32400/tcp open  http    Plex Media Server httpd
|_http-favicon: Plex
| http-auth: 
| HTTP/1.1 401 Unauthorized\x0D
|_  Server returned status 401 but no WWW-Authenticate header.
|_http-cors: HEAD GET POST PUT DELETE OPTIONS
|_http-title: Unauthorized
32469/tcp open  upnp    Platinum UPnP 1.0.5.13 (UPnP/1.0 DLNADOC/1.50)
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel
```

Enumerated top 200 UDP ports:
```bash
PORT      STATE SERVICE
53/udp    open  domain
123/udp   open  ntp
5353/udp  open  zeroconf
32414/udp open  unknown
```

---

# Enumeration
## Port 80
1. [[ffuf]] scan for subdomains showed us two:
	-  `/admin`
		- Redirects us to a Pi-Hole page!
	-  `/version`

## Pi-Hole
1. Once this was found I searched for exploits for its version but nothing interesting came up for that
2. Next I checked for default creds as we have a login page we could try
3. Found `pi:raspberry` tried those on the GUI and failed because it would only let me enter the password?
4. Shifted over to ssh into it to try the creds that way and success we are in!!

---

# Exploitation
## Default Credentials
1. Found default credentials were set for Pi-Hole and it allowed an ssh into it!!


---

# Lateral Movement to user
## Local Enumeration
- **pi** user
	- `sudo -l`
		- We have unrestricted access with this user!
	- Found **user.txt** under pi home directory

## Lateral Movement vector


---

# Privilege Escalation
## Local Enumeration
- **root.txt** turned out to be a bit more tricky when it comes to finding it:
	- Found under `/root/root.txt`
		- Contained instructions to check his USB drive
	- Checked under both `/mnt` & `/media`
		- Located under `/media/usbstick`
		- Once there we found `damnit.txt` which said "Sorry I deleted the USB drive wonder if there is  a way to recover that?"
			- Trying to find how to recover that I did a few `find` commands with no luck finally found an article that talked about checking `/dev/sdb`
			- Used `cat /dev/sdb` found a lot of gibberish but in there I could see mention of `usbstick` with what seemed like the flag and after testing it that was correct!
- **NOTE FOR FUTURE**
	- When looking for a deleted file under either sda, sdb, sdc, etc... use `strings sda` it will clean it up when showing in CLI

## Privilege Escalation vector
- Got an escalation simply with `sudo su` and entering the creds of the user we already had

---

# Trophy & Loot
user.txt
ff837707441b257a20e32199d7c8838d

root.txt
3d3e483143ff12ec505d026fa13e020b

___

## Resources:

| Hyperlink | Info |
| --------- | ---- |


Created Date: June 1st 2023 (05:40 pm)  
Last Modified Date: <%+tp.file.last_modified_date("MMMM Do YYYY (hh:ss a)")%>

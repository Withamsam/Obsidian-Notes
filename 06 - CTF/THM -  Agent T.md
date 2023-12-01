---
creation date: July 27th 2023
last modified date: July 27th 2023
aliases: []
tags: #🎌
---

Primary Categories: 
Secondary Categories:  
Links: 
Search Tag: #🎌  

# [[THM -  Agent T]]  


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
80
```

Enumerated open TCP ports:
```bash

```

Enumerated top 200 UDP ports:
```bash

```

---

# Enumeration
## Port 80
- Nothing on the website worked except for 404 page but its a dead end
- Checking the header of the main page indicates that its running a version of PHP that has a backdoor
	- Ran that exploit and it gave us root access with a bad shell but workable
		- I was going to stabilize it or have it call back to another shell that I could stabilize
			- Found shell under **/flag.txt**


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

___

## Resources:

| Hyperlink | Info |
| --------- | ---- |


Created Date: July 27th 2023 (11:19 pm)  
Last Modified Date: <%+tp.file.last_modified_date("MMMM Do YYYY (hh:ss a)")%>

---
creation date: December 5th 2023 (09:07 pm)
last modified date: December 5th 2023 (09:07 pm)
aliases: []
tags: 🎌
---
 
Primary Categories: 
Secondary Categories:  
Links: 
# [[THM - AoC 2023 - [Day 5] A Christmas DOScovery]]  


# Resolution summary
- Text
- Text

## Improved skills
- skill 1
- skill 2

## Used tools
- [[nmap]]
- [[DOS]]

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
## Port 


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

1. Use `DIR` to display the `C:\` directory
	- This will give you the file size of `AC2023.BAK`
2. Navigate to `C:\TOOLS\BACKUP`
```bash
cd \TOOLS\BACKUP
```

3.  Print the contents of `README.txt`
```ba
```



---

# Trophy & Loot

## Credentials


## Scripts


## Task Answers
  
How large (in bytes) is the AC2023.BAK file?
```
12,704
```

What is the name of the backup program?  
```
BackupMaster 3000
```

What should the correct bytes be in the backup's file signature to restore the backup properly?  
```
41 43
```

What is the flag after restoring the backup successfully?  
```
THM{0LD_5CH00L_C00L_d00D}
```

What you've done is a simple form of reverse engineering, but the topic has more than just this. If you are interested in learning more, we recommend checking out our [x64 Assembly Crash Course room](https://tryhackme.com/room/x86assemblycrashcourse), which offers a comprehensive guide to reverse engineering at the lowest level.
```
Submit
```


___

## Resources:

| Hyperlink | Info |
| --------- | ---- |



---
creation date: December 3rd 2023 (05:43 pm)
last modified date: December 3rd 2023 (05:43 pm)
aliases: []
tags: 🎌
---
 
Primary Categories: 
Secondary Categories:  
Links: 
# [[THM - AoC 2023 - [Day 3] Hydra is Coming to Town]]  


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

1. Got to site it gives `http://10.10.60.140:8000/pin.php`
2. Here we see a pin panel with the following character set



---

# Trophy & Loot

## Credentials


## Scripts


## Task Answers

  
Using `crunch` and `hydra`, find the PIN code to access the control system and unlock the door. What is the flag?
```
THM{pin-code-brute-force}
```

If you have enjoyed this room please check out the [Password Attacks](https://tryhackme.com/room/passwordattacks) room.
```
Submit
```

___

## Resources:

| Hyperlink | Info |
| --------- | ---- |



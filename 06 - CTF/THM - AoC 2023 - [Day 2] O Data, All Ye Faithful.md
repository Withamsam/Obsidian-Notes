---
creation date: December 2nd 2023 (07:47 pm)
last modified date: December 2nd 2023 (07:47 pm)
aliases: []
tags: 🎌
---
 
Primary Categories: 
Secondary Categories:  
Links: 
# [[THM - AoC 2023 - [Day 2] O Data, All Ye Faithful]]  


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

1. Step 4 in Notebook
```python
df.count()
```

2. Step 5 in Notebook
```python
df.groupby(['Source']).size
```

3. Step 6 in Notebook
```python
df['Protocol'].value_counts()
```




---

# Trophy & Loot

## Credentials


## Scripts


## Task Answers
  
Open the notebook "Workbook" located in the directory "4_Capstone" on the VM. Use what you have learned today to analyse the packet capture.
```
Submit
```

How many packets were captured (looking at the PacketNumber)?  
```
100
```

What IP address sent the most amount of traffic during the packet capture?  
```
10.10.1.4
```

What was the most frequent protocol?  
```
ICMP
```

If you enjoyed today's task, check out the [Intro to Log Analysis](https://tryhackme.com/room/introtologanalysis) room.
```
Submit
```

___

## Resources:

| Hyperlink                                            | Info        |
| ---------------------------------------------------- | ----------- |
| [Link](https://tryhackme.com/room/adventofcyber2023) | Link to CTF | 



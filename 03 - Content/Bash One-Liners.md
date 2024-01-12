---
creation date: January 11th 2024 (10:26 pm)
last modified date: January 11th 2024 (10:26 pm)
aliases: []
tags: 🧰
---
 
Primary Categories: 
Secondary Categories:  
Links: [[Bash]]
# [[Bash One-Liners]]  
___

## Description:
These are commands that can be executed using one line using a bit of **Bash** in the terminal to automate a few things.

## Commands

### DNS / IP Locator
- Uses a wordlist to search subdomains
	- Use **Seclist** wordlists for hostnames
```bash
for ip in $(cat wordlist.txt); do host $ip.example.com; done | grep -v "not found"
```

- Will search the last octet for possible subdomains
	- Useful if we find multiple subdomains that have a similar **IP**
```bash
for ip in $(seq 200 254); do host xxx.xxx.xxx.$ip; done | grep -v "not found"
```



___

## Resources:

| Hyperlink | Info |
| --------- | ---- |



---
creation date: January 5th 2023
last modified date: January 5th 2023
aliases: []
tags: #🧰
---

Primary Categories: [[01 - Pentest]] - [[01 - Red Team]]
Secondary Categories:  [[02 - Reconnaissance]]
Links: [[Passive Scanning]] - [[DNS]]
Search Tag: #🧰  

# [[nslookup]]  
___

## Description:
Used to query DNS Servers.

## Installation
Installed on Kali by default

## Commands
- `nslookup -type=<OPTIONS> <DOMAIN_NAME> <SERVER>`
	- **OPTIONS** = contains the query type as shown in the table below.
	- **DOMAIN_NAME** = the domain name you are looking up.
	- **SERVER** = the DNS server that you want to query. You can choose any local or public DNS server.
	- `nslookup tryhackme.com`
	- `nslookup -type=A tryhackme.com 1.1.1.1` 

![[DNS#Record Types]]
![[DNS#Public DNS's]]


___

## Resources:

| Hyperlink | Info |
| --------- | ---- |


Created Date: January 5th 2023 (09:18 pm)  
Last Modified Date: <%+tp.file.last_modified_date("MMMM Do YYYY (hh:ss a)")%>

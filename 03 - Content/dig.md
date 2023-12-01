---
creation date: January 5th 2023
last modified date: January 5th 2023
aliases: []
tags: #🧰
---

Primary Categories: [[01 - Pentest]] - [[01 - Red Team]]
Secondary Categories:  [[02 - Reconnaissance]]
Links: [[DNS]] - [[Passive Scanning]]
Search Tag: #🧰  

# [[dig]]  
___

## Description:
"Domain Information Groper" is used for advance DNS queries.

## Installation
Installed on Kali by default

## Commands
- `dig @<SERVER> <DOMAIN_NAME> <TYPE>`
	- **SERVER** = the DNS server that you want to query
	- **DOMAIN_NAME** = the domain name you are looking up
	- **TYPE** = contains the DNS record type linked below
	- `dig tryhackme.com`
	- `dig @1.1.1.1 tryhackme.com MX` (Targets Cloudflare's DNS server "1.1.1.1" for the lookup)

![[DNS#Record Types]]
![[DNS#Public DNS's]]

### Zone Transfer
1. We locate the Domain Name and DNS Server through [[Network Enumeration]]
2. Using **dig** we can request a Zone Transfer if they are not restricted!!!
```bash
dig -t AXFR <DOMAIN_NAME> @<DNS_SERVER>
```
- Switch info:
	- `-t AXFR` = Tells the DNS server we are asking for a Zone Transfer



___

## Resources:

| Hyperlink | Info |
| --------- | ---- |


Created Date: January 5th 2023 (09:21 pm)  
Last Modified Date: <%+tp.file.last_modified_date("MMMM Do YYYY (hh:ss a)")%>

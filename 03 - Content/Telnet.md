---
creation date: January 8th 2023
last modified date: January 8th 2023
aliases: []
tags: #🧰
---

Primary Categories: { Add link(s) [[]] back to related PRIMARY categories }
Secondary Categories:  { Add link(s) [[]] back to related SECONDARY categories }
Links: [[Application Layer Protocol]]
Search Tag: #🧰  

# [[Telnet]]  
___
```ad-port
title:Port: 23
```

## Description:
Used to connect to virtual terminal in order to login and access its terminal, start batch processes, and preform system administration tasks remotely.

Note all of this is sent in **Clear Text**.

## Installation
### Windows
```Powershell
dism /online /Enable-Feature /FeatureName:TelnetClient
```
- Enables Microsofts version of 

## Commands
- Basic connection:
	1. `telnet <TARGET_IP> <PORT>`
	2. Enter username and password in the following two prompts
- Basic Header Grab
	1. Telnet in with basic connection
	2. `GET / HTTP/1.1`
	3. `Host: telnet`

___

## Resources:

| Hyperlink | Info |
| --------- | ---- |


Created Date: January 8th 2023 (04:27 pm)  
Last Modified Date: <%+tp.file.last_modified_date("MMMM Do YYYY (hh:ss a)")%>

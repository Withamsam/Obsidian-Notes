---
creation date: May 7th 2023
last modified date: May 7th 2023
aliases: []
tags: #🧰
---

Primary Categories: 
Secondary Categories:  
Links: [[SNMP]] - [[02 - Enumeration]]
Search Tag: #🧰  

# [[snmpcheck]]  
___

## Description:
Designed to enumerate SNMP.

## Installation
- Install for Kali Linux
```bash
git clone https://gitlab.com/kalilinux/packages/snmpcheck.git && cd snmpcheck/ && gem install snmp && chmod +x snmpcheck-1.9.rb
```

## Commands
### Syntax
```bash
./snmpcheck/snmpcheck.rb 10.10.147.53 -c COMMUNITY_STRING
```
- The `COMMUNITY_STRING` is SNMP version of username and password. It can be something as simple as `public`
- Should only take a few moments to run!!!

___

## Resources:

| Hyperlink                                                     | Info                             |
| ------------------------------------------------------------- | -------------------------------- |
| [Gitlab](https://gitlab.com/kalilinux/packages/snmpcheck.git) | Link to Gitlab with package info | 


Created Date: May 7th 2023 (02:51 pm)  
Last Modified Date: <%+tp.file.last_modified_date("MMMM Do YYYY (hh:ss a)")%>

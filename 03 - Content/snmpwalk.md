---
creation date: January 16th 2024 (11:08 pm)
last modified date: January 16th 2024 (11:08 pm)
aliases: []
tags: 🧰
---
 
Primary Categories: 
Secondary Categories:  
Links: [[SNMP]]
# [[snmpwalk]]  
___

## Description:
Utilized to retrieve a subtree of management values using **SNMP GETNEXT requests**.
snmpwalk 
## Installation


## Commands
### List all
```bash
snmpwalk -c public -v1 -t 10 10.10.10.10 -Oa
```
- `-c` = Specify the community string
- `-v` = Version of SNMP they are using
- `-t` = Set timeout period
- `-Oa` = Translates HEX to ASCII


### Specify a branch
```bash
snmpwalk -c public -v1 -t 10 10.10.10.10 <BRANCH_LOCATION>
```
![[SNMP#Table]]




___

## Resources:

| Hyperlink | Info |
| --------- | ---- |



---
creation date: May 7th 2023
last modified date: May 7th 2023
aliases:
  - Simple Network Management Protocol
tags: 
Port: 161 162
---

Primary Categories: 
Secondary Categories:  
Links: [[snmpcheck]]
Search Tag: #📕  

# [[SNMP]]  
___
```ad-port
title:Port: UDP 161 / 162
```
## Description:  
Used to collect information about various devices anything from servers with faulty disks to a printer low on ink. Thus it could contain a plethora of information if we can access it.



## Versions
### SNMPv(1, 2, 2c)
Offer no encryption for their traffic!!


### SNMPv3
- Early versions shipped with **DES-56** encryption which can be easily brute forced.
- Later version did upgrade to **AES-256** encryption



## SNMP MIB Tree
- The SNMP Management Information Base (MIB) is a database containing information that is usually related to network management.
- This is built like a tree in which the branches represent a different organization or network function. All of the leaves on the tree correspond to specific variable values. These leaves can be enumerated by an external user. 

| MIB Values for                       | Windows                 |
| ---------------------- | ---------------- |
| 1.3.6.1.2.1.25.1.6.0   | System Processes |
| 1.3.6.1.2.1.25.4.2.1.2 | Running Programs |
| 1.3.6.1.2.1.25.4.2.1.4 | Processes Path   |
| 1.3.6.1.2.1.25.2.3.1.4 | Storage Units    |
| 1.3.6.1.2.1.25.6.3.1.2 | Software Name    |
| 1.3.6.1.4.1.77.1.2.25  | User Accounts    |
| 1.3.6.1.2.1.6.13.1.3   | TCP Local Ports  |





___

## Resources:

| Hyperlink | Info |
| --------- | ---- |


Created Date: May 7th 2023 (02:19 pm)  
Last Modified Date: <%+tp.file.last_modified_date("MMMM Do YYYY (hh:ss a)")%>

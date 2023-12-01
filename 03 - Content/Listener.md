---
creation date: April 25th 2023
last modified date: April 25th 2023
aliases: []
tags: #📕
---

Primary Categories: { Add link(s) [[]] back to related PRIMARY categories }
Secondary Categories:  { Add link(s) [[]] back to related SECONDARY categories }
Links: [[C2 Framework]] - [[Netcat]] - [[Metasploit]]
Search Tag: #📕  

# [[Listener]]  
___

## Description:  
Created as a way to make a callback from another machine and start a connection.

## Types of Listeners
**Standard Listener -**
Often these communicate over TCP or UDP socket, sending commands in cleartext. Metasploit has full support for this listener.

**HTTP/HTTPS Listener -**
These often front as some sort of Web Server and use techniques such as Domain Facing or Malleable C2 profiles to mask a C2 server. When specifically communicating over HTTPS it is less likely for traffic to be stopped and blocked by NGFW. Metasploit has full support for HTTP/HTTPS Listeners.

**DNS Listener -**
Popular technique that  is used during the exfiltration stage of an attack. These also require more infostructure like a public facing NS server and a domain must be purchased and registered.

**SMB Listener -**
These communicate over SMB named pipes and are useful when dealing with a restricted network; it often enables more flexible pivoting with multiple devices talking to each other and only one reaching back out over a more common HTTP/HTTPS Listener.



___

## Resources:

| Hyperlink | Info |
| --------- | ---- |


Created Date: April 25th 2023 (10:51 pm)  
Last Modified Date: <%+tp.file.last_modified_date("MMMM Do YYYY (hh:ss a)")%>

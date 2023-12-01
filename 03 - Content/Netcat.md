---
creation date: January 6th 2023
last modified date: January 6th 2023
aliases: [nc]
tags: #🧰
---

Primary Categories: { Add link(s) [[]] back to related PRIMARY categories }
Secondary Categories:  { Add link(s) [[]] back to related SECONDARY categories }
Links: 
Search Tag: #🧰  

# [[Netcat]]  
___

## Description:
Versatile tool that can allow us to use both TCP and UDP to either connect to another server or listen for incoming connections

## Installation


## Commands
### Connecting to a server
1. `nc <IP / HOSTNAME> <PORT>`
	- `nc 10.10.10.10 80`
2. Once it connects we need to send it commands this example is to banner pull
	- Might need to hit **Shift-Enter** if after last command it didn't put us on a new line.
	- `GET / HTTP/1.1`
	- This command tells the server we are connecting to that we accept HTTP 1.1 protocol
3. Next we need to give a name to our host
	- `host: netcat`
4. After entering this we should get our banner back from the site giving us more information about it

___

## Resources:

| Hyperlink | Info |
| --------- | ---- |


Created Date: January 6th 2023 (08:54 pm)  
Last Modified Date: <%+tp.file.last_modified_date("MMMM Do YYYY (hh:ss a)")%>

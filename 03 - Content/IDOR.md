---
creation date: November 14th 2022
last modified date: November 14th 2022
aliases: [Insecure Direct Object Reference]
tags: #📕
---

Primary Categories: [[01 - Pentest]] - [[01 - Red Team]]
Secondary Categories:  { Add link(s) [[]] back to related SECONDARY categories }
Links: [[Access Control Vulnerability]]
Search Tag: #📕  

# [[IDOR]]  
___

## Description:  
Insecure Direct Object Reference is a type of access control vulnerability. An IDOR can occur when a web server receives user-supplied input to retrieve objects (file, data, documents), and too much trust has been placed on that input data. and teh web application does not validate whether the user should, in fact, have access to the request object.

## Finding IDOR's
**Query Component:**
![[Pasted image 20221114204352.png]]

**Post Variables**
![[Pasted image 20221114204832.png]]
- Could try change the "user_id" value as well as change the password of that new account.

**Cookies**
![[Pasted image 20221114205044.png]]


___

## Resources:

| Hyperlink | Info |
| --------- | ---- |


Created Date: November 14th 2022 (08:32 pm)  
Last Modified Date: <%+tp.file.last_modified_date("MMMM Do YYYY (hh:ss a)")%>

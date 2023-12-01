---
creation date: May 6th 2023
last modified date: May 6th 2023
aliases: [AD]
tags: #📕
---

Primary Categories: 
Secondary Categories:  
Links: [[Windows]]
Search Tag: #📕  

# [[Active Directory]]  
___

## Description:  
Windows based authentication and management system. This can often contain info on the employees like username, passwords, names, title, etc... It is comprised of many parts described below.

![[Pasted image 20230506210530.png]]

### Domain Controller
Windows server that will host the AD and controls every aspect. It is a form of centralized user management.
- Highly sought after target

### Organizational Unit's (OU's)
These are containers within the hierarchical system.

### Active Directory Objects
Can be anything from a single user to a group or even devices such as a printer, computer, fax machine, etc... Each domain contains a database that contains object identity information including:
- `Users` = A security principle that is allowed authenticate to machines within the domain
- `Computers` = A special type of user accounts
- `GPO's` = Collection of policies that are applied to AD Objects

### AD Domains
A collection of Microsoft components within a AD Network

### AD Forest
A collection of domains that trust each other
![[Pasted image 20230506210937.png]]

---
## AD Admin Accounts
|       Account        |                        Description                         |
|:--------------------:|:----------------------------------------------------------:|
| BULTIN/Administrator |         Local admin access on a domain controller          |
|    Domain Admins     |        Admin access to all resources in the domain         |
|   Enterprise Admin   |                Available only in the forest                |
|    Schema Admins     | Capable of modifying domain/forest; useful for red teamers |
|   Server Operators   |                 Can manage domain servers                  |
|  Account Operators   |     Can manage user that are not in a privileged group     | 






___

## Resources:

| Hyperlink | Info |
| --------- | ---- |


Created Date: May 6th 2023 (08:54 pm)  
Last Modified Date: <%+tp.file.last_modified_date("MMMM Do YYYY (hh:ss a)")%>

---
creation date: January 5th 2023
last modified date: January 5th 2023
aliases: []
tags: #📕
---

Primary Categories: { Add link(s) [[]] back to related PRIMARY categories }
Secondary Categories:  { Add link(s) [[]] back to related SECONDARY categories }
Links: [[dnsrecon]] - [[nslookup]] - [[dig]] - [[DNSDumpster]] - [[host]]
Search Tag: #📕  

# [[DNS]]  
___

## Description:  


## Record Types
| Query type |      Results       |
|:----------:|:------------------:|
|     A      |   IPv4 Addresses   |
|    AAAA    |   IPv6 Addresses   |
|   CNAME    |   Canonical Name   |
|     MX     |    Mail Servers    |
|    SOA     | Start of Authority |
|    TXT     |    TXT Records     | 


## Public DNS's
- Cloudflare - `1.1.1.1` & `1.0.0.1`
- Google - `8.8.8.8` & `8.8.4.4`
- Quad9 - `9.9.9.9` & `149.112.112.112`

---
## Preforming a Zone Transfer
1. Locate our DNS server can be done with the following: ![[Network Enumeration#Checking Active Running Services]]
### Windows
2. Once we have that server IP then we can use the following to Zone Transfer to it:
```Powershell
nslookup.exe
> server <DNS_SERVER_IP>
> ls -d <DOMAIN_WE_WANTED_TO_TRANSFER>
```

### Linux
![[dig#Zone Transfer]]



___

## Resources:

| Hyperlink | Info |
| --------- | ---- |


Created Date: January 5th 2023 (09:40 pm)  
Last Modified Date: <%+tp.file.last_modified_date("MMMM Do YYYY (hh:ss a)")%>

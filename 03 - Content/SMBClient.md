---
creation date: July 18th 2023
last modified date: July 18th 2023
aliases: []
tags: #🧰
---

Primary Categories: 
Secondary Categories:  
Links: [[Samba suite]] - [[SMB]]
Search Tag: #🧰  

# [[SMBClient]]  
___

## Description:
This is apart of the [[Samba suite]] and is used to access [[SMB]] can be used to enumerate / get files off the server.

## Installation
Pre-installed on Kali

## Commands

|     Switch     |            Description            | Example |
|:--------------:|:---------------------------------:|:-------:|
| `-L`, `--list` | Shows what services are available | `smbclient -L //<IP>`        |

### Syntax
- `-N` get rid of this if you need to authenticate with a password

#### List Services
```bash
smbclient -L -N //<IP>
```

#### Opening a Share
```bash
smbclient -N //<IP>/<SHARE>
```

#### Downloading an entire share
```bash
smbclient -N //<IP>/<SHARE>
smb: \> mask ""
smb: \> recurse ON
smb: \> prompt OFF
smb: \> cd 'path\to\remote\dir'
smb: \> lcd '~/path/to/download/to/'
smb: \> mget *
```



___

## Resources:

| Hyperlink | Info |
| --------- | ---- |


Created Date: July 18th 2023 (06:34 pm)  
Last Modified Date: <%+tp.file.last_modified_date("MMMM Do YYYY (hh:ss a)")%>

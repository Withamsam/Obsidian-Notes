---
creation date: May 10th 2023
last modified date: May 10th 2023
aliases: []
tags: #📕
---

Primary Categories: [[01 - Red Team]]
Secondary Categories: [[02 - Enumeration]]
Links: [[Windows]] - [[Enumeration]]
Search Tag: #📕  

# [[Windows Enumeration]]  
___

## Description:  


---
## Groups
### View Local Groups
```CMD
net localgroup
```

### View Users in a Local Group
```CMD
net localgroup <GROUP_NAME>
```

### Add a Local Group
```CMD
net localgroup <GROUP_NAME> /add
```

### Add User to a Local Group
```CMD
net localgroup <GROUP_NAME> <USERNAME> /add
```

### Add an AzureAD User to a Local Group
```CMD
net localgroup <GROUP_NAME> AzureAD\<EMAIL> /add
```

### Checking Our Current Groups
```CMD
whoami /groups
```

___

## Resources:

| Hyperlink | Info |
| --------- | ---- |


Created Date: May 10th 2023 (09:10 pm)  
Last Modified Date: <%+tp.file.last_modified_date("MMMM Do YYYY (hh:ss a)")%>

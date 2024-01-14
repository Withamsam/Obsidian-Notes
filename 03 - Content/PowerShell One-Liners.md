---
creation date: January 14th 2024 (01:50 am)
last modified date: January 14th 2024 (01:50 am)
aliases: []
tags: 🧰
---
 
Primary Categories: 
Secondary Categories:  
Links: 
# [[PowerShell One-Liners]]  
___

## Description:
Collection of useful one line commands that can be run in **Powershell CLI**.

## Commands

### Scan 1024 port on Domain Controller
```PowerShell
1..1024 | % {echo ((New-Object Net.Sockets.TcpClient).Connect("192.168.215.151", $_)) "TCP port $_ is open"} 2>$null
```
- Starts by using a for-loop to assign the incremental integer to `$_`
- Then creates a TCPClient object to preform a TCP connection
- If its open will return a log message

___

## Resources:

| Hyperlink | Info |
| --------- | ---- |



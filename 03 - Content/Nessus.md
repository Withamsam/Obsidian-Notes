---
creation date: January 17th 2024 (09:01 pm)
last modified date: January 17th 2024 (09:01 pm)
aliases: []
tags: 🧰
---
 
Primary Categories: 
Secondary Categories:  
Links: [[Vulnerability Scanning]]
# [[Nessus]]  
___

## Description:
A largely popular **Vulnerability Scanner** that contains approximately ~67000 CVEs.

## Installation
```
Tenable recommends 4 CPU cores and 8GB of RAM
```

1. Manually [Download](https://www.tenable.com/downloads/nessus) **.deb** file
2. Verify the checksum value and then install it with `apt install`

## Commands

### Starting Nessus
- We do so with **systemctl**
- It will just show nothing if it starts correctly
```bash
sudo systemctl start nessusd.service
```


### Connecting to Nessus
```
https://127.0.0.1:8834
```











___

## Resources:

| Hyperlink | Info |
| --------- | ---- |



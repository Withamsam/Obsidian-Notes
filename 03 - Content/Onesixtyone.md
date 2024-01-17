---
creation date: January 16th 2024 (11:44 pm)
last modified date: January 16th 2024 (11:44 pm)
aliases: []
tags: 🧰
---
 
Primary Categories: 
Secondary Categories:  
Links: [[SNMP]]
# [[Onesixtyone]]  
___

## Description:
Onesixtyone is a fast **SNMP Scanner**. In order to use it we must first build a list of community strings. I have a simple command below to build a small one.

## Installation
Installed with Kali

## Commands
### Basic Syntax
```bash
onesixtyone [options] <host> <community>
```


### Basic community string search
```bash
echo public > community && echo private >> community && echo manager >> community
```

```bash
for ip in $(seq 1 254); do echo 10.10.10.$ip; done > ips
```

```bash
onesixtyone -c community -i ips
```



___

## Resources:

| Hyperlink | Info |
| --------- | ---- |



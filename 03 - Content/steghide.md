---
creation date: May 18th 2023
last modified date: May 18th 2023
aliases: []
tags: #🧰
---

Primary Categories: 
Secondary Categories:  
Links: [[CLI]] - [[Steganography]]
Search Tag: #🧰  

# [[steghide]]  
___

## Description:
Can be used to both hide files inside images/audio files and extract that if you have the right password.

## Installation
- Ubuntu
```bash
sudo apt update && sudo apt install steghide -y
```

## Commands
| Switch |             Description             |           Example           |
|:------:|:-----------------------------------:|:---------------------------:|
| `-sf`  | Specify the name for the stego file | `steghide -sf example.jpeg` | 

### Syntax
#### Extract Info
```bash
steghide --extract -sf <FILE_NAME>
```
- Will be prompted for a password!!
	- BUT could be no password is needed so you can just hit enter here if you aren't sure of a possible password and it will fail if it doesnt work if it does it will extract to a .txt file it creates in same location


___

## Resources:

| Hyperlink | Info |
| --------- | ---- |


Created Date: May 18th 2023 (08:25 pm)  
Last Modified Date: <%+tp.file.last_modified_date("MMMM Do YYYY (hh:ss a)")%>

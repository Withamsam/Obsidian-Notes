---
creation date: November 6th 2022
last modified date: November 6th 2022
aliases: []
tags: #📕
---

Primary Categories: [[01 - Pentest]] - [[01 - Red Team]]
Secondary Categories:  [[02 - Reconnaissance]]
Links: [[Websites]] - [[Content Discovery]]
Search Tag: #📕  

# [[Favicon]]  
___

## Description:  
This is a small icon displayed in a browser's address bar or tab for branding.

## Use
- Often times if a site is built with a framework if the website owner doesn't change it to a customer one it can clue us to which framework they are using.
- How to get a sites Favicon
	1. Locate where the favicon is being pulled from can be located in the source code
	2. Linux: 
		- `curl <full website URL pointing to favicon> | md5sum`
	2. PowerShell: 
		1. `curl <full website URL pointing to favicon> -UseBasicParsing -o favicon.ico`
		2. `Get-FileHash .\favicon.ico -Algorithm MD5`
	3. Check against Favicon Database



___

## Resources:

| Hyperlink                                                                   | Info |
| --------------------------------------------------------------------------- | ---- |
| [Favicon Database](https://wiki.owasp.org/index.php/OWASP_favicon_database) |List of default favicons      |


Created Date: November 6th 2022 (06:21 pm)  
Last Modified Date: <%+tp.file.last_modified_date("MMMM Do YYYY (hh:ss a)")%>

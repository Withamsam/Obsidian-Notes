---
creation date: July 27th 2023
last modified date: July 27th 2023
aliases: []
tags: #🧰
---

Primary Categories: [[01 - Pentest]] - [[01 - Red Team]]
Secondary Categories:  [[02 - Internal Enumeration]]
Links: [[WordPress]]
Search Tag: #🧰  

# [[Wpscan]]  
___

## Description:
This allows enumeration and brute forcing for  WordPress sites.

## Installation
Pre-installed on Kali

## Commands

|       Switch        |                    Description                    |                      Example                      |
|:-------------------:|:-------------------------------------------------:|:-------------------------------------------------:|
|       `--url`       |                  Specify target                   |         `wpscan --url http://10.10.10.10`         |
| `-e`, `--enumerate` | Enumerates various options (Options listed below) |      `wpscan -e vp --url http://10.10.10.10`      |
| `-P`, `--passwords` |          Specifies path to password list          | `wpscan -P /rockyou.txt --url http://10.10.10.10` |
| `-U`, `--username`  |          Specifies path to username list          |  `wpscan -U /user.list --url http://10.10.10.10`  |
|        `-t`         | Specifies how many threads are used (Default: 5)  | `wpscan -t 10 --url http://10.10.10.10`                                                  |
### Enumerate Options
- Enumeration Process Available Choices:
	- `vp` - Vulnerable plugins
	- `ap` - All plugins
	- `p` - Plugins
	- `vt` - Vulnerable themes
	- `at` - All themes
	- `t` - Themes
	- `tt` - Timthumbs
	- `cb` - Config backups
	- `dbe` - Db exports
	- `u` - User IDs range. e.g: u1-5 Range separator to use: '-' Value if no argument supplied: 1-10
	- `m` - Media IDs range. e.g m1-15 Note: Permalink setting must be set to "Plain" for those to be detected  Range separator to use: '-' Value if no argument supplied: 1-100
		- Separator  to  use  between  the values: ',' Default: All Plugins, Config Backups Value if no argument sup‐plied: vp,vt,tt,cb,dbe,u,m Incompatible choices (only one of each group/s can be used):
			- `vp, ap, p - vt, at, t`






___

## Resources:

| Hyperlink | Info |
| --------- | ---- |


Created Date: July 27th 2023 (09:43 pm)  
Last Modified Date: <%+tp.file.last_modified_date("MMMM Do YYYY (hh:ss a)")%>

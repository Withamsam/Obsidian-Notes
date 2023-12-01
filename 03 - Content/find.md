---
creation date: January 8th 2023
last modified date: January 8th 2023
aliases: []
tags: #🧰
---

Primary Categories: { Add link(s) [[]] back to related PRIMARY categories }
Secondary Categories:  { Add link(s) [[]] back to related SECONDARY categories }
Links: [[Grep]] - [[Locate]]
Search Tag: #🧰  

# [[find]]  
___

## Description:


## Installation


## Commands
- Avoid error messages by adding `2>/dev/null` to the end of the commands

-   `find . -name flag1.txt`: find the file named “flag1.txt” in the current directory
-   `find /home -name flag1.txt`: find the file names “flag1.txt” in the /home directory
-   `find / -type d -name config`: find the directory named config under “/”
-   `find / -type f -perm 0777`: find files with the 777 permissions (files readable, writable, and executable by all users)
-   `find / -perm a=x`: find executable files
-   `find /home -user frank`: find all files for user “frank” under “/home”
-   `find / -mtime 10`: find files that were modified in the last 10 days
-   `find / -atime 10`: find files that were accessed in the last 10 day
-   `find / -cmin -60`: find files changed within the last hour (60 minutes)
-   `find / -amin -60`: find files accesses within the last hour (60 minutes)
-   `find / -size 50M`: find files with a 50 MB size


___

## Resources:

| Hyperlink | Info |
| --------- | ---- |


Created Date: January 8th 2023 (10:45 pm)  
Last Modified Date: <%+tp.file.last_modified_date("MMMM Do YYYY (hh:ss a)")%>

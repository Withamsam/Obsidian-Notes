---
creation date: December 11th 2022
last modified date: December 11th 2022
aliases: []
tags: #🧰
---

Primary Categories: { Add link(s) [[]] back to related PRIMARY categories }
Secondary Categories:  { Add link(s) [[]] back to related SECONDARY categories }
Links: [[Linux]]
Search Tag: #🧰  

# [[Grep]]  
___

## Description:
Used to sort through a file by feeding it what you are looking for it will only show matches. 

## Installation


## Commands

| Option |                                           Description                                           |              Example               |
|:------:|:-----------------------------------------------------------------------------------------------:|:----------------------------------:|
|   -i   |                                Preform a case insensitive search                                |    `grep -i "Hi there" log.txt`    |
|   -E   |     Searches using regex. We can search for lines that contain either "THM" or "tryhackme"      | `grep -E "THM|tryhackme" log.txt`  |
|   -r   | Search recursively. We can search say a directory and it will search all files contained within | `grep -r "helloworld" mydriectory` |
|   -v   |           Invert your search. This search will show all lines that don't contain 404.           |     `grep -i "404" -v log.txt`     | 

### Syntax
- Recursive
```bash
grep -r <PATH_TO_FILE_START> -e '<SEARCH_TERM>'
```


___

## Resources:

| Hyperlink | Info |
| --------- | ---- |


Created Date: December 11th 2022 (10:20 pm)  
Last Modified Date: <%+tp.file.last_modified_date("MMMM Do YYYY (hh:ss a)")%>

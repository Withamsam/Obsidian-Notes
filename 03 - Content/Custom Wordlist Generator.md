---
creation date: May 3rd 2023
last modified date: May 3rd 2023
aliases: [CeWL]
tags: #🧰
---

Primary Categories: 
Secondary Categories:  
Links: [[Crawler]] - [[CLI]] - [[Ruby]]
Search Tag: #🧰  

# [[Custom Wordlist Generator]]
___

## Description:
This program is written in Ruby and is designed to spider/crawl a URL, up to a specified depth, and returns a list of unique words used through the site.

---
## Installation
Pre-installed on Kali

---
## Commands
| Switch |           Description            |        Example        |
|:------:|:--------------------------------:|:---------------------:|
|  `-w`  |     Write the output to file     | `cewl -w <FILE_NAME>` |
|  `-m`  | Minimum word length (default: 3) |      `cewl -m 5`      |
|  `-d`  | Depth to spider to (default: 2)  |      `cewl -d 8`      |

**Basic Usage**
```bash
cewl -w <FILE_NAME> -d 8 -m 5 https://example.com
```



___

## Resources:

| Hyperlink | Info |
| --------- | ---- |


Created Date: May 3rd 2023 (08:54 pm)  
Last Modified Date: <%+tp.file.last_modified_date("MMMM Do YYYY (hh:ss a)")%>

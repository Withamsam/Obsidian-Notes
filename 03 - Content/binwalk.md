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

# [[binwalk]]  
___

## Description:
Used to search images for embedded files and executable code. For example if an image has a zip file hidden inside of it we can use this to locate and extract.

Can run any image through it to check if there is something hiding can be done with multiple files at once. If the image contains nothing then it wont extract but doesn't hurt to try.

## Installation
Pre-installed on Kali

## Commands

|       Switch        |                            Description                            |             Example             |
|:-------------------:|:-----------------------------------------------------------------:|:-------------------------------:|
|         `-e`         |              Automatically extracts known file types              |     binwalk -e example.jpg      |
| `-C`, `--dicrectory` | Sets custom extract location (default: current working directory) | binwalk -e -C ~/CTF example.jpg | 

### Syntax
```bash
binwalk <OPTIONS> <FILE1> <FILE2 <FILE3>
```


___

## Resources:

| Hyperlink | Info |
| --------- | ---- |


Created Date: May 18th 2023 (07:20 pm)  
Last Modified Date: <%+tp.file.last_modified_date("MMMM Do YYYY (hh:ss a)")%>

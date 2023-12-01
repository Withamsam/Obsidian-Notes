---
creation date: May 3rd 2023
last modified date: May 3rd 2023
aliases: []
tags: #🧰
---

Primary Categories: 
Secondary Categories:  
Links: [[Wordlist]] - [[CLI]]
Search Tag: #🧰  

# [[Crunch]]  
___

## Description:
Will create wordlist based on parameters that we feed it.

## Installation
Pre-installed on Kali

## Commands
| Switch |                   Description                    |              Example               |
|:------:|:------------------------------------------------:|:----------------------------------:|
|  `-h`  |                    Help Menu                     |            `crunch -h`             |
|  `-o`  |                   Output File                    | `crunch 1 2 123abc -o <FILE_NAME>` |
|  `-t`  | Specifies a pattern (check below table for pattern meaning) |   `crunch 6 6 -t pass%%`    |
|        |                                                  |                                    |

### -t Pattern Meaning
- `@` = will insert lower case characters
- `,` = will insert upper case characters
- `%` = will insert numbers
- `^` = will insert symbols

### Syntax
`crunch <MIN-LEN> <MAX-LEN> <CHARSET STRIN> <OPTIONS>`
```bash
crunch 2 3 01234abcdfgt -o example.txt
```
- This will generate all combinations using the provided character set with a min-length of `2` & max-length of `3`, while outputting it to `example.txt`

___

## Resources:

| Hyperlink | Info |
| --------- | ---- |


Created Date: May 3rd 2023 (10:37 pm)  
Last Modified Date: <%+tp.file.last_modified_date("MMMM Do YYYY (hh:ss a)")%>

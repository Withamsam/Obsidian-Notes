---
creation date: May 4th 2023
last modified date: May 4th 2023
aliases: []
tags: #🧰
---

Primary Categories: 
Secondary Categories:  
Links: [[CLI]] - [[Hash]] - [[Hash Cracker]] - [[Hashid]] - [[Hash-Identifier]] - [[Wordlist]]
Search Tag: #🧰  

# [[Hashcat]]  
___

## Description:
Utilized for Offline **Dictionary Attacks**, **Rule-based Attacks**, **Brute-Force Attacks** when we obtain a list of hashed passwords and we want to attempt to break that hash.

## Installation
Pre-install on Kali

## Commands

|   Switch   |                  Description                   |               Example                | 
|:----------:|:----------------------------------------------:|:------------------------------------:|
|    `-a`    |       Sets attack mode (Full list below)       |            `hashcat -a 0`            |
|    `-m`    | Sets hash mode (Check help menu for full list) |           `hashcat -m 100`           |
|  `--show`  |               Shows cracked hash               | `hascat -a 1 -m 170 hash.lst --show` |
|    `-h`    |                   Help menu                    |             `hashcat -h`             |
|    `-o`    |              Output file location              |     `hashcat -o <PATH_TO_FILE>`      |
| `--stdout` |            Prints results to window            |          `hashcat --stdout`          |

### Attack Modes

|  #  |             Mode             |
|:---:|:----------------------------:|
| `9` |         Association          |
| `7` |    Hybrid Mash + Wordlist    |
| `6` |    Hybrid Wordlist + Mask    |
| `3` |         Brute-Force          |
| `1` |         Combination          |
| `0` | Straight (Dictionary Attack) |

### Syntax
```bash
hashcat -m <HASH_MODE> -a <ATTACK_MODE> <HASH_LIST_OR_STRAIGHT_HASH> <PATH_TO_WORDLIST>
```

#### Dictionary Attack
```bash
hashcat -m <HASH_MODE> -a 0 hash.lst /usr/share/wordlist/rockyou.txt --show
```
- Here we are feeding **hashcat** a hash list but we can also just give it a single hash to break

#### Brute-Force Attack
```bash
hashcat -m <HASH_MODE> -a 3 05A5CF06982BA7892ED2A6D38FE832D6 ?d?d?d?d
```
- Here we are feeding **hashcat** a single hash but could also give it a list of hashes
- The `?d?d?d?d` is us telling the system that we know it will be a number from 0-9 in the form of "0000". Full character list in table below

|  ?  |            Charset             |
|:---:|:------------------------------:|
| `l` |              a-z               |
| `u` |              A-Z               |
| `d` |              0-9               |
| `h` |           0-9 & a-f            |
| `H` |           0-9 & A-F            |
| `s` | Special Characters (!#,-)etc.. |
| `a` |            ?l?u?d?s            |
| `b` |          0x00 - 0xff           | 


### Finding Which Hash To Use
- There are many tools that can be used to analyze a hash to determine which hash to check against listed below are a few methods:
	1. `hashcat <HASH_VALUE>` (useful as it also will tell you code to use with hashcat)
	2. `hashid`
	3. `hash-identifier`

___

## Resources:

| Hyperlink | Info |
| --------- | ---- |


Created Date: May 4th 2023 (09:34 pm)  
Last Modified Date: <%+tp.file.last_modified_date("MMMM Do YYYY (hh:ss a)")%>

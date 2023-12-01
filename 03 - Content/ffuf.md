---
creation date: November 6th 2022
last modified date: November 6th 2022
aliases: []
tags: #🧰
---

Primary Categories: [[01 - Pentest]] - [[01 - Red Team]]
Secondary Categories:  [[02 - Reconnaissance]]
Links: [[Websites]] - [[Directory Discovery]] - [[GO]] - [[Wordlist]] - [[Dictionary Attack]]
Search Tag: #🧰  

# [[ffuf]]  
___

## Description:
Fast web fuzzer written in GO.

## Installation
### Kali
`sudo apt update && sudo apt install ffuf`

## Commands
### Basic
```bash
ffuf -w /path/to/wordlist -u http://{TARGET}/FUZZ
```


###
```bash
ffuf -w /path/to/wordlist -H "Host: FUZZ.{TARGET}" -u http://10.10.10.10 -fs {SIZE}
```
- Always returns valid so we need to filter by common sizes of replies.
	- Run 1 time without `-fs` cancel scan after a few seconds to get common "Size" that we want to ignore.


### Brute Enumeration Signup Page
```bash
ffuf -w /usr/share/wordlists/SecLists/Usernames/Names/names.txt -X POST -d "username=FUZZ&email=x&password=x&cpassword=x" -H "Content-Type: application/x-www-form-urlencoded" -u http://10.10.247.92/customers/signup -mr "username already exists"
```
- Example of enumerating a sign up form that requests a username, email, password, conformation password.


### Brute Forcing Login Page
```bash
ffuf -w /usr/share/wordlists/rockyou.txt -X POST -d "user=admin&pass=FUZZ" -H "Content-Type: application/x-www-form-urlencoded" -u http://10.10.10.10/admin/index.php -ac -t 150
```
- Sometimes you need to find the *.php* file its going to as the above example is doing


### Enumerating Directories that Require Credentials
```bash
ffuf -w /usr/share/wordlists/directory_search.txt -u http://$RHOST:1234/manager/html/FUZZ -t 150 -b "JSESSIONID=DD5359630861ECD7807DB256FB428273" --recursion
```
- Once we have a successful sign in we can feed our requests with our session cookie with **-b** switch.


### Switches

| Switch       | Description                                                                                                                           |
| ------------ | ------------------------------------------------------------------------------------------------------------------------------------- |
| `-w`         | Path to word list. Need multiple wordlists? Use: `/path/to/wordlist:W1`,`/path/to/wordlist:W2`,etc... put W1 & W2 where you want them |
| `-u`         | Target URL                                                                                                                            |
| `-H`         | Header `"Name Value"`, separated by colon                                                                                             |
| `-fs`        | Filter HTTP response Size. Comma separated list of sizes and ranges                                                                   |
| `-recursion` | Will apply the FUZZ to any directory that it finds to dig deeper                                                                      |
| `-ac`        | Will calibrate with first few responses and look for anything different to print                                                                                                                                      |

___

## Resources:

| Hyperlink                              | Info          |
| -------------------------------------- | ------------- |
| [Github](https://github.com/ffuf/ffuf) | ffuf git repo | 


Created Date: November 6th 2022 (11:54 pm)  
Last Modified Date: <%+tp.file.last_modified_date("MMMM Do YYYY (hh:ss a)")%>

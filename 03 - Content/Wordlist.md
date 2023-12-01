---
creation date: December 13th 2022
last modified date: December 13th 2022
aliases: []
tags: #🧰
---

Primary Categories: [[01 - Red Team]]
Secondary Categories:  [[02 - Authentication Bypass]]
Links: [[Hydra]] - [[John the Ripper]] - [[Custom Wordlist Generator]] - [[Crunch]]
Search Tag: #🧰  

# [[Wordlist]]  
___

## Description:
Collection of usernames, passwords, domains, etc.

### Seclists
```bash
sudo apt update && sudo apt install seclists -y
```
- Located at:
	- /usr/share/seclists/

### Kali Linux Default Lists
- Located at:
	- /usr/share/wordlists/

---
## Combining Multiple Wordlists
1. First we will concatenate the desired list we can add as many as we want:
```bash
cat list1.txt list2.txt list3.txt > combined_list.txt
```
2. Next we will clean them up as they may have over lap and we don't want to waste time testing a password twice:
```bash
sort combined_list.txt | uniq -u > cleaned_combined_list.txt
```
- This search through the newly created password list and delete any duplicates

---
## Generating Username Wordlist From a Name List
1. This will assume that we have a {first name} {last name} in a list
2. We will use a pre-built Username Generator that will create most possible combinations:
```bash
git clone https://github.com/therodri2/username_generator.git
```
3. Next we will run the list through the generator and get our list of possible usernames to test against:
```bash
python username_generator -w <USERLIST.txt>
```
- Go out and try and make your own username generator!!!!

---
## Generating Wordlist From Known Information
1. We will use a pre-built automatic and interactive wordlist generator known as **CUPP** (Common User Password Profiler)
```bash
git clone https://github.com/Mebus/cupp.git
```
2. Now if you run `cupp.py` you will get the help menu but to start lets go directly into the **Interactive Mode**
```bash
python3 cupp.py -i
```
3. Follow the prompts and if we don't know the information about the target its asking for simply hit enter

---
## Keyspace Technique
This is when we create our own wordlist by feeding a tool parameters like letters, symbols, numbers, length, etc...
- [[Crunch]] = Powerful tool to create offline wordlists.

___

## Resources:

| Hyperlink                                                                                            | Info                                  |
| ---------------------------------------------------------------------------------------------------- | ------------------------------------- |
| [Skull Security](https://wiki.skullsecurity.org/index.php?title=Passwords)                           | Wiki link to weak password database |
| [Sec List GitHub](https://github.com/danielmiessler/SecLists/tree/master/Passwords/Leaked-Databases) | GitHub containing largest leaked password lists                                |


Created Date: December 13th 2022 (05:56 pm)  
Last Modified Date: <%+tp.file.last_modified_date("MMMM Do YYYY (hh:ss a)")%>

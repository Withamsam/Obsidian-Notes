---
creation date: January 9th 2023
last modified date: January 9th 2023
aliases: []
tags: #🧰
---

Primary Categories: { Add link(s) [[]] back to related PRIMARY categories }
Secondary Categories:  { Add link(s) [[]] back to related SECONDARY categories }
Links: [[Hash Cracker]] - [[Wordlist]] - [[Hashcat]] - [[CLI]]
Search Tag: #🧰  

# [[John the Ripper]]  
___

## Description:
Powerful tool used for Offline **Dictionary Attacks**, **Rule-based Attacks**, **Brute-Force Attacks** once we have obtained a hash list we want to crack we can feed it into this tool. 

## Installation
Pre-installed on Kali

## Commands

|    Switch     |        Description        |                      Example                       |
|:-------------:|:-------------------------:|:--------------------------------------------------:|
|   `--help`    |         Help Menu         |                   `john --help`                    |
| `--wordlist=` | Path to desired Wordlist  |           `john --wordlist=<FILE_PATH>`            |
|  `--rules=`   |  Desired rule to change   | `john --wordlist=<FILE_PATH> --rules=<RULE_NAME> ` |
|  `--stdout`   | Print results in terminal |                  `john --stdout`                   |


### Syntax
```bash
john --wordlist=<PATH_TO_LIST> <FILE_TO_CRACK>
```

#### Rule-Based Attack
- Can be useful when we need to mangle a password list to fit criteria for example:
	- Change `password` -> `p@ssword`, `Pa$$word`, `Passw0rd`
	- This can automatically be done to an entire list of passwords using Rules
- Default location for rules in **John**
	- `/etc/john/john.conf`
	- `/opt/john/john.conf`
- John the Ripper has pre-built rule list use command below to see them:
```bash
cat /etc/john/john.conf|grep "List.Rules:" | cut -d"." -f3 | cut -d":" -f2 | cut -d"]" -f1 | awk NF
```
1. Once we have found the Rule list we want to use or created our own we need to add the switch to our command:
```bash
john --wordlist=<PATH_TO_LIST> --rules=<RULE_LIST_NAME> -
```

##### Creating Our Own Ruleset
1. Open `john.conf` in any editor you prefer:
```bash
sudo subl /etc/john/john.conf
```
2. Navigate to the bottom of the file and add the following to create and name our new ruleset:
```John.conf
[List.Rules:<CHOOSE_RULESET_NAME>]
```
3. Now beneath this is where we add what we want the rule to change to each line below is an example: 
```John.conf
Az"[0-9]" ^[!@#$]
```
- Explanation of each item:
	- `Az` = Represents a single word from the original wordlist/dictionary
	- `"[0-9]"` = Append a single digit (from 0 to 9) to the end of the word. For two digits we can add `"[0-9][0-9]"` and so on.
	- `^[!@#$]` = Add a special character to the beginning of each word. `^` means the beginning of each line/word if we change `^` to `$` it will add it to the end instead.
4. Finally lets test out our new rule set create a wordlist containing a single password and pass it through to verify things work correctly:
```bash
echo "password" > test.lst && john --rules=<NEW_RULESET_NAME> --wordlist=test.lst --stdout && rm test.lst
```
- This creates a quick file containing just password. Then it sends it through **John** and prints results to terminal. finally we remove the test file so we don't end up with multiple.

---
## Getting files ready:
### passwd / shadow
1. We need both the `etc/passwd` & `etc/shadow`
2. Next run these through the following: `unshadow passwd shadow > unshadowed.txt`
3. Next put this new file through `john --wordlist=<PATH_TO_LIST> unshadowed.txt`
4. Finally we can check which hashes were broken: `john --show unshadowed.txt`

### .asc
1. `gpg2john <FILENAME>.asc > hash`
2. `john hash --wordlist=/usr/share/wordlist/rockyou.txt`

### RSA Private Key
1. Put the entire Private Key into a file including the begin and end portion
2. `ssh2john <FILENAME> > RSA.john`
3. `john RSA.john --wordlist=/usr/share/wordlist/rockyou.txt`

### GPG
1. `gpg2john <FILENAME>.gpg > <FILENAME>.john`
2. `john <FILENAME>.john --wordlist=/usr/share/wordlist/rockyou.txt`

### [[Ansible]] Vault
1. Grab the following out of a vault and put it into its own file so it looks similar to this:
```
$ANSIBLE_VAULT;1.1;AES256 
32666534386435366537653136663731633138616264323230383566333966346662313161326239 
6134353663663462373265633832356663356239383039640a346431373431666433343434366139 
35653634376333666234613466396534343030656165396464323564373334616262613439343033 
6334326263326364380a653034313733326639323433626130343834663538326439636232306531 
3438
```
2. `ansible2john <FILENAME>.yml > ansible.john`
3. `john --wordlist=/usr/share/wordlist/rockyou.txt ansible.john`
4. The password we get here is the password for the vault itself so next up is opening said vault
5. `ansible-vault view <VAULT_NAME>.yml`
	- Enter password we just found at the prompt


___

## Resources:

| Hyperlink | Info |
| --------- | ---- |


Created Date: January 9th 2023 (07:57 pm)  
Last Modified Date: <%+tp.file.last_modified_date("MMMM Do YYYY (hh:ss a)")%>

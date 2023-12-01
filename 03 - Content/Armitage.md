---
creation date: April 2nd 2023
last modified date: April 2nd 2023
aliases: []
tags: #🧰
---

Primary Categories: [[01 - Pentest]] - [[01 - Red Team]]
Secondary Categories:  
Links: [[Metasploit]] - [[C2 Framework]] - [[Java]]
Search Tag: #🧰  

# [[Armitage]]  
___

## Description:
An extension of Metasploit that adds a GUI and is written in Java. It is also very similar to **Cobalt Strike** as it was written by the same author. Most popularly known for its "Attacks" menu this acts as a Hail Mary attack in which it runs all attacks possible against a targets machine. 

## Installation
- This can be found on GitLab linked below
1. Start by cloning the Git repository
```bash
git clone https://gitlab.com/kalilinux/packages/armitage.git && cd armitage
```
2. Now we must build the current release
```bash
bash package.sh
```
- **Errors**
	- Ran into an error with Gradle because I was running Java version 17
		- `java -version` to check if you see same error
		- `sudo update-alternatives --config 'java'` switch to another installed java version by following prompts
			- Java 11 worked
3. Verify install of Armitage
```bash
cd ./release/unix/ && ls -la
```
- If the files aren't present then it wasn't installed successful

## Commands
### Pre-flight check
- Before we start our Teamserver we want to ensure that our Metasploit Database is running correctly.
1. 
```bash
systemctl start postgresql && systemctl status postgresql
```
2. 
```bash
msfdb --use-defaults delete
```
3. 
```bash
msfdb --use-defaults init
```
---
### Starting and connecting
- Two main files located under `/opt/armitage/release/unix`
1. `Teamserver`
	- This starts the Armitage Server that allows multiple users to connect to and it takes two arguments:
		- IP Address
		- Shared Password
```bash
cd /opt/armitage/release/unix && sudo ./teamserver {privateIP} P@ssw0rd123
```
2. `Armitage`
	- This is what we will be using to connect to the Teamserver
	- ![[Pasted image 20230405210931.png]]
```bash
cd /opt/armitage/release/unix && ./armitage
```
---
### Creating a Listener
- Can be done once you are connected to the Teamserver
	1. Armitage -> Listeners -> PICK THE ONE YOU NEED
		- Bind (connect to) = 





___

## Resources:

| Hyperlink                                                  | Info                                |
| ---------------------------------------------------------- | ----------------------------------- |
| [Kali Documentation](https://www.kali.org/tools/armitage/) | Kali site documentation on Armitage | 


Created Date: April 2nd 2023 (10:03 pm)  
Last Modified Date: <%+tp.file.last_modified_date("MMMM Do YYYY (hh:ss a)")%>

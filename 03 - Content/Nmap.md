---
creation date: December 12th 2022
last modified date: December 12th 2022
aliases: 
tags:
  - 🧰
---

Primary Categories: [[01 - Pentest]] - [[01 - Red Team]]
Secondary Categories:  [[02 - Reconnaissance]]
Links: [[Ports]] - [[Active Scanning]] - [[Host Discovery]]

# [[Nmap]]  
___

## Description:
Robust port scanner that is capable of crafting packets to send to a target to do anything from gather port statuses to gathering system info.

Often times we need to use `sudo` in order to run our scans. This is because most of it's scans need access to **Raw Sockets** to manipulate TCP and UDP packets. Without this we still have some options but its limited as it needs to use the **Berkley socket API**.

## Installation
Pre-install on Kali

## Commands
### Ping Scans

|       Scan Type        |               Example Command               | Sudo Required? |
|:----------------------:|:-------------------------------------------:| :--------------: |
|        ARP Scan        |      `sudo nmap -PR -sn MACHINE_IP/24`      |                |
|     ICMP Echo Scan     |      `sudo nmap -PE -sn MACHINE_IP/24`      |                |
|  ICMP Timestamp Scan   |      `sudo nmap -PP -sn MACHINE_IP/24`      |                |
| ICMP Address Mask Scan |      `sudo nmap -PM -sn MACHINE_IP/24`      |                |
|   TCP SYN Ping Scan    | `sudo nmap -PS22,80,443 -sn MACHINE_IP/30`  |        No        |
|   TCP ACK Ping Scan    | `sudo nmap -PA22,80,443 -sn MACHINE_IP/30`  |     Yes           |
|     UDP Ping Scan      | `sudo nmap -PU53,161,162 -sn MACHINE_IP/30` |                |


### Port Scans

|    Scan Type     |      Flag       |                  Example Command                  | Sudo Required? |
|:----------------:|:---------------:|:-------------------------------------------------:|:--------------:|
| TCP Connect Scan |     **-sT**     |              `nmap -sT 10.10.10.10`               |       No       |
|   TCP SYN Scan   |     **-sS**     |            `sudo nmap -sS 10.10.10.10`            |      Yes       |
|     UDP Scan     |     **-sU**     |            `sudo nmap -sU 10.10.10.10`            |      Yes       |
|    Null Scan     |     **-sN**     |            `sudo nmap -sN 10.10.10.10`            |      Yes       |
|     FIN Scan     |     **-sF**     |            `sudo nmap -sF 10.10.10.10`            |      Yes       |
|    Xmas Scan     |     **-sX**     |            `sudo nmap -sX 10.10.10.10`            |      Yes       |
|   TCP ACK Scan   |     **-sA**     |            `sudo nmap -sA 10.10.10.10`            |      Yes       |
|   Window Scan    |     **-sW**     |            `sudo nmap -sW 10.10.10.10`            |      Yes       |
|   Custom Scan    | **--scanflags** | `sudo nmap --scanflags <CUSTOM_FLAG> 10.10.10.10` |      Yes       | 



## Scan Descriptions
### TCP Connect Scan
- `-sT`
- Default choice by nmap if we **don't have sudo**.
- Runs a full 3-way handshake followed by RST,ACK. This resets the connection type of the port and moves onto the next.

### TCP SYN Scan
- `sS`
- Default choice by nmap if we **do have sudo**.
- After getting the SYN,ACK back from the port sends a RST and never finishes the handshake.
- Less likely to be logged as the full connection is never made.

### UDP Scan
- `sU`
- Since this is a connectionless protocol this scan relies on ICMP port unreachable error (type 3, code 3). This reply will only come through if the packet we sent cant reach it meaning we only see it for ports that aren't open.

### Null Scan
- `sN`
- Doesn't set a flag leaves all 6 flag bits set to zero.
- Since the scan sends a TCP packet with no flag then it the port will not respond if the port is open or filtered and if the port is closed then we will get RST,ACK.
- Useful if we think a firewall is filtering our SYN packets.

### FIN Scan
- `sF`
- Sets the flag during initial TCP connection to FIN.
- This scan looks for the lack of response to determine if a port is open/filtered. If a port is closed we will get a RST/ACK.
- Useful if we think a firewall is filtering our SYN packets.

### Xmas Scan
- `sX`
- Sets the flag during initial TCP connection to FIN, PSH, URG at the same time.
- This scan looks for the lack of response to determine if a port is open/filtered. If a port is closed we will get a RST/ACK
- Useful if we think a firewall is filtering our SYN packets.

### TCP Maimon Scan
- `-sM`
- Sets flag during initial TCP connection to FIN//ACK
- This scan gets back RST regardless of if the port is open/closed.

### TCP ACK Scan
- `sA`
- Sets the flag during initial TCP connection to ACK
- This scan gets back RST regardless of if the port is open/closed
- Suitable to discover firewall rule set and it inspects which ports actually give a response to the ACK if they are behind a firewall.
- If  the ports aren't getting blocked by the firewall it they will show as unfiltered after the scan
![[Pasted image 20230108144037.png]]

### Window Scan
- `-sW`
- Sets the flag during initial TCP connection to ACK
- This scan get back RST regardless of if the port is open/closed
- Works the same as **TCP ACK Scan** except it examines the **TCP Window** field of the RST reply
- If the target system can be Linux/Windows/MacOS gives us a reply with a port even if it says that port is closed these replies act different these closed ports actually are not being blocked by the firewall
![[Pasted image 20230108144123.png]]

### Custom Scan
- `--script-args http.useragent="CUSTOM_AGENT"`
	- Used to avoid detection by changing the useragent that shows in our requests.
	- Nmap defaults to: **User-Agent** (which is commonly searched for by Blue Teams)
- `--scanflags <CUSTOM_FLAG>`
	- You set which flag this scan initiates the connection for example:
		- If we want RST, SYN, FIN then it would be - `--scanflags RSTSYNFIN`
	- Setting custom flags requires knowledge of how a port will react
		![[TCP#Flags]]

### Idle (Zombie) Scan
- `sI`
- With this scan we set a target on our network as a idle system
	- This can be anything from a multifunction printer to an old computer

## Option Descriptions
### -p
- We can feed our scan with different ports either a range or list
	- `-p-` = Scans all 65,535 ports
	- `-p80,443,110`
	- `-p1-100`

### -T<0-5>
- Used to avoid IDS alerts
	- **paranoid (0)** = Scans one port at a time and waits 5 mins between each one
	- **sneaky (1)** = Quite slow, used for IDS evasion
	- **polite (2)** = Slows down to consume less bandwidth, runs slower than default (10 times slower)
	- **normal (3)** = Normal default setting, based on target responsiveness
	- **aggressive (4)** = Aggressive, assumes a reliable fast network. Used most often in CTF's
	- **insane (5)** = Very Aggressive, likely to miss open ports

### --min-rate / --max-rate
- Used to set  min / max packets per-second
	- `--min-rate 10` =  Minimum 10 packets per second
	- `--max-rate=100` = Maximum 100 packets per second 

### -D Decoy1,Me,Decoy2
- Used to throw off the victim by causing the scan to appear to be coming from multiple different IP addresses
- These address can be set either manually or randomly
	- Manually = `nmap -D 10.10.10.10,Me,10.10.10.11 <VICTIM_IP>`
	- Random = `nmap -D RND,RND,Me,RND <VICTIM IP>`
	- Mixed = `nmap -D 10.10.10.10,RND,RND,Me,10.10.10.11 <VICTIM_IP>`
	- We can mix and match these and the **Me** portion is where we replace with our actual IP

### --spoof-mac
- Only usable if the attacker and the target machine are on the same Ethernet or WiFi
- `nmap --spoof-mac <SPOOFED_MAC> <VICTIM_IP>`

### -S
- Used to spoof our IP address but in doing so the reply that most scans wait to here back from will be sent to the spoofed address.
- This option is useless if we can not monitor the network to watch for the reply being sent to the spoofed address
- `nmap -S <SPOOFED_IP> <VICTIM_IP>`

### -sV
- This requires the scan to make a full TCP 3-way handshake meaning that things like a SYN Stealth Scan won't work with it 
- Adding the following flag `--version-intensity <LEVEL>` allows us to tell the scan to take longer or less time to probe ports
	- **0-9** = These are the levels we can choose from 0 being least intense and 9 being most.
	- The level that nmap uses normally is **7**.
	- `nmap -sV --version-intensity 9 10.10.10.10`


___

## Resources:

| Hyperlink | Info |
| --------- | ---- |


Created Date: December 12th 2022 (10:14 pm)  
Last Modified Date: <%+tp.file.last_modified_date("MMMM Do YYYY (hh:ss a)")%>

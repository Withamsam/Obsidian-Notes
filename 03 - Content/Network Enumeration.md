---
creation date: May 6th 2023
last modified date: May 6th 2023
aliases: []
tags: #📕
---

Primary Categories: [[01 - Red Team]]
Secondary Categories: [[02 - Enumeration]]
Links: [[Windows]] - [[Linux]] - [[MacOS]]
Search Tag: #📕  

# [[Network Enumeration]]  
___

## Description:  
This is internally sniffing a network after we gain access in order to better understand areas we might be able to pivot too.

---
## Checking UDP / TCP Ports
### Windows
```CMD
netstat -na
```
- This will check all ports on the system to see if we have any established connections
- **Will flood terminal**

---
## Checking ARP Tables
### Windows
```CMD
arp -a
```
- Displays all current entries in the ARP table

### Linux

### MacOS

---
## Checking for AD Controller
### Windows
```CMD
systeminfo | findstr Domain
```
- If we see ` Domain:     WORKGROUP` this means we not apart of a AD controller instead we are in a **Local Workgroup**

---
## Active Directory Enumeration
1. First verify that we are apart of a AD environment
2. Next using Powershell:
```Powershell
Get-AdUser -Filter *
```
- This will give us more info on the AD setup:
	- `DistinguishedName:` = Collection of comma separated key a value pairs used to identify unique records. We can use [LDAP hierarchical tree structure](https://www.ietf.org/rfc/rfc2253.txt) to show what the acronyms mean.
		- Example: `DistinguishedName : CN:Administrator, CN:Users, DC:thmredteam, DC:com`
		   ![[Pasted image 20230506213531.png]]
3. Now that we have a break down of the AD environment we can filter them down to only certain Domains, OU's, CN's, etc...:
```Powershell
Get-ADUser -Filter * -SearchBase "CN=Users,DC=THMREDTEAM,DC=COM"
```

## Checking for Host Security Systems
### AV
#### Windows
- We have a few commands that can return info about what type of AV tools are being used:
```Powershell
Get-CimInstance -Namespace root/SecurityCenter2 -ClassName AntivirusProduct
```

```Powershell
wmic /namespace:\\root\securitycenter2 path antivirusproduct
```
- Note that **Windows Servers** might not have `SecurityCenter2` but **Windows Workstations** will!
##### Windows Defender
- This runs in three modes:
	- `Active` = Which means its the primary AV for the system
	- `Passive` = Meaning a 3rd party AV is handling the remediation but it is still scanning files
	- `Disable` = Off or uninstalled on the system
- We can check the service state with:
```Powershell
Get-Service WinDefend
```
- Next we can use the following to determine its mode:
```Powershell
Get-MpComputerStatus | select RealTimeProtectionEnabled
```

### Host-based Firewalls
#### Windows
- Checking if the Firewall is active:
```Powershell
Get-NetFirewallProfile | Format-Table Name, Enabled
```

- If we have admin account we can disable them with:
```Powershell
Set-NetFirewallProfile -Profile Domain, Public, Private -Enabled False
```

- Check current Firewall rules:
```Powershell
Get-NetFirewallRule | select DisplayName, Enabled, Description
```

- Testing connections from within the network:
```Powershell
Test-NetConnection -ComputerName 127.0.0.1 -Port 80
```
- Can also use tool called `TcpClient`
- If this succeeds then we know inbound connections over specified port will work to this machine

- Checking any detected threats:
```Powershell
Get-MpThreat
```

---
## Checking Active Running Services
### Windows
1. This will show active running services:
```Powershell
net start
```
2. If we see a service we want to know more about we can specify:
```Powershell
wmic service where "name like '<SERVICE_WE_WANT_TO_KNOW_ABOUT>'" get Name,PathName
```
- This will give us the **Name** and **File Path** to the service.
3. We can get more details on the service itself with:
```Powershell
Get-Process -Name <SERVICE_WE_WANT_TO_KNOW_ABOUT>
```
- This will give us the **Process ID** of the service
4. Once we have the Process ID we can use it to check ports for which one its using:
```Powershell
netstat -noa | findstr "LISTENING" | findstr "<PROCESS_ID>"
```



___

## Resources:

| Hyperlink | Info |
| --------- | ---- |


Created Date: May 6th 2023 (08:33 pm)  
Last Modified Date: <%+tp.file.last_modified_date("MMMM Do YYYY (hh:ss a)")%>

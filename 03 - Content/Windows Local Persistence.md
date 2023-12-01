---
creation date: May 10th 2023
last modified date: May 10th 2023
aliases: []
tags: #📕
---

Primary Categories: [[01 - Red Team]]
Secondary Categories:  [[02 - Persistence]]
Links: [[Windows]]
Search Tag: #📕  

# [[Windows Local Persistence]]  
___

## Description:  
Once we have gotten access to a system we want to maintain this as the original exploit we used might not work a second time. This could be for a number of reasons but either way we want to hold on.

Usually the best scenario would be to gain access to an Admin account but these come with their own issue mostly they tend to be more monitored than other users due to the level of access they have. So we can also gain access to non-privileged accounts and attempt to give them Admin access in a number of ways.

---
## If We Already Have An Admin Account
- This category will explore our options if we already have access to an Administrator's account.

### Assign Group Membership
- We can try to simply add a non-privileged account to the Admin group with:
```CMD
net localgroup administrators <NON_PRIVILEGED_USER> /add
```


1. Another option is to add the non-privileged account to the `"Backup Operators"` group. This group doesn't have Admin access but is less suspicious and still could be allowed to **Read/Write** any file or registry on the system. 
```CMD
net localgroup "Backup Operators" <NON_PRIVILEGED_USER> /add
```
2. We may need to add this same user to other groups if we want to be able to RDP into the machine with their account:
```CMD
net localgroup "Remote Management Users" <NON_PRIVILEGED_USER> /add
```
- We can swap `"Remote Management Users"` (WinRM) --> `"Remote Desktop Users"` (RDP)  
- **Note:** We might need to dig around as these groups either might not exist or could be disabled
3.  If using **WinRM** for connection then we might need to disable a UAC `LocalAccountTokenFilterPolicy` as this policy strips the admin rights of a user when they are logging in remotely
```CMD
reg add HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System /t REG_DWORD /v LocalAccountTokenFilterPolicy /d 1
```
4. Use [[Evil-WinRM]] if using `"Remote Management Users"` group or RDP into the machine using are new account.
5. Now we want to make a backup of both **SYSTEM** & **SAM** which contain password hashes for all users!!!
```
```

- 


___

## Resources:

| Hyperlink | Info |
| --------- | ---- |


Created Date: May 10th 2023 (09:16 pm)  
Last Modified Date: <%+tp.file.last_modified_date("MMMM Do YYYY (hh:ss a)")%>

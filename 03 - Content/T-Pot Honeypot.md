---
creation date: November 27th 2023
last modified date: November 27th 2023
aliases: []
tags: #📖
---

Primary Categories: 
Secondary Categories:  
Links: 
Search Tag: #📖  

# [[T-Pot Honeypot]]  


## Standalone Steps

1) System Requirements
```
Debian 11 | 16GB Ram | 256 Storage
```

2) SSH into your machine
```
ssh <USERNAME>@<VM_IP>
```

3) Install git
```
sudo apt update && sudo apt install git -y
```

4) Run the installer listed here on their (GitHub)[https://github.com/telekom-security/tpotce#post-install-auto-method]
```
git clone https://github.com/telekom-security/tpotce
cd tpotce/iso/installer/
sudo ./install.sh --type=user
```

5) We get the following message after it runs
```
###########################################
### T-Pot Installer for Debian (Stable) ###
###########################################

Disclaimer:
This script will install T-Pot on this system.
By running the script you know what you are doing:
1. SSH will be reconfigured to tcp/64295.
2. Please ensure other means of access to this system in case something goes wrong.
3. At best this script will be executed on the console instead through a SSH session.

########################################

Usage:
        ./install.sh --help - Help.

Example:
        ./install.sh --type=user - Best option for most users.
```
- Note that it says the port of SSH will be changed to `tcp/64295` we will need to adjust when using ssh to sign in.

6) Lets run it now with the added parameter
```
sudo ./install.sh --type=user
```
- Once this starts you will be prompted to enter a username / password these are for the service itself so make sure to remember them

7) It will take about 5-10 minutes to install. Once it does you will see a final message about it restarting and your SSH will drop. Give it about 5 minutes after that and you can sign back in but you need to specify the new SSH port.
```
ssh <USERNAME>@<VM_IP> -p 64295
```


## Hive Steps
1) System Requirements
- Hive
```

```


___

## Resources:

| Hyperlink | Info |
| --------- | ---- |


Created Date: November 27th 2023 (02:22 pm)  
Last Modified Date: <%+tp.file.last_modified_date("MMMM Do YYYY (hh:ss a)")%>

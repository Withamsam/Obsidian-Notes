---
creation date: November 8th 2022
last modified date: November 8th 2022
aliases: []
tags: #📕
---

Primary Categories: [[01 - Pentest]] - [[01 - Red Team]]
Secondary Categories:  [[02 - Authentication Bypass]]
Links: [[Curl]] - [[PHP]]
Search Tag: #📕  

# [[Logic Flaw]]  
___

## Description:  
This is when the typical Logic Path is bypassed, circumvented or manipulated.
![[Pasted image 20221108155743.png]]

## Example
```php
if( url.substr(0,6) === '/admin') {
    # Code to check user is an admin
} else {
    # View Page
}
```
- Here we can see that the PHP code is checking if its redirecting to `/admin`. The flaw comes from the fact that its checking it with a three equal signs.
	- In PHP three equal signs means exactly matches this meaning `/AdMin` would not be checked further but would still let us access the admin account.


___

## Resources:

| Hyperlink | Info |
| --------- | ---- |


Created Date: November 8th 2022 (03:24 pm)  
Last Modified Date: <%+tp.file.last_modified_date("MMMM Do YYYY (hh:ss a)")%>

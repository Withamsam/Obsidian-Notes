---
creation date: May 5th 2023
last modified date: May 5th 2023
aliases: []
tags: #🧰
---

Primary Categories: 
Secondary Categories:  
Links: [[Phishing]] - [[Online Tool]] - [[Framework]]
Search Tag: #🧰  

# [[GoPhish]]  
___

## Description:
This is is a web-based tool that is designed to automate the act of **Phishing** by helping draft emails, collect analytics, host servers, etc...


## Commands
### Dashboard
- This contains a overview of all of our Campaigns

### Campaigns
- This is where we bring it all together. We create our actual attack using all the info we setup in the other tabs

### User & Groups
- This is where we store our targets email addresses for the automation

### Email Templates
- This is where we artfully craft our emails to trick the victim
- If we want to create **Anchor Text** we can do so under HTML tab click the `Link` button on the top enter what we want them to see and under **URL** enter `{{.URL}}` and set the protocol to `<other>`. This will tell the link to go to our custom landing page.

### Landing Pages
- This is where we configure the website page that the phishing email will lead to.
- Usually this is a spoof of an actual website that we are impersonating
- Written in HTML but we can attempt to steal this code directly from the site we are impersonating

### Sending Profiles
- These are the connection details **required** for actually sending our phishing emails. Simple its an **SMTP Sever** we have access too.

___

## Resources:

| Hyperlink                            | Info                       |
| ------------------------------------ | -------------------------- |
| [Site Link](https://getgophish.com/) | Link to the web-based tool | 


Created Date: May 5th 2023 (10:08 pm)  
Last Modified Date: <%+tp.file.last_modified_date("MMMM Do YYYY (hh:ss a)")%>

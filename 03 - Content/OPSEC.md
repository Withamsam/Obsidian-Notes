---
creation date: March 23rd 2023
last modified date: March 23rd 2023
aliases: ["Operations Security"]
tags: #📕
---

Primary Categories: { Add link(s) [[]] back to related PRIMARY categories }
Secondary Categories:  { Add link(s) [[]] back to related SECONDARY categories }
Links: {Add link(s) [[]] to related terms}
Search Tag: #📕  

# [[OPSEC]]  
___

## Description:  
Operations Security is essentially five-step process in which we want to deny our advisory any information about ourselves.

## Five Steps:
### 1. Critical Information
- Critical information includes anything that can hinder the red teams movements.
- Includes but no limited to: **Intentions**, **capabilities**, **activities**, and **limitations**
	- i.e. Domains, Public IPs, Pentesting Tools, Hosted Websites, CSP, TTP, OS, C2 Framework, Uncommon Web Browsers, etc.
- 

### 2. Threats
- This step aims to answer the following questions:
1.  Who is the adversary?
2.  What are the adversary’s goals?
3.  What tactics, techniques, and procedures does the adversary use?
4.  What critical information has the adversary obtained, if any?
- `threat = adversary + intent + capability`

### 3. OPSEC Vulnerabilities
- This is not the same as a cybersecurity vulnerability.
- OPSEC Vulnerabilities are things that can compromise the operation this includes but not limited to:
	- Using same IP for scanning, hosting, exploiting
		- If this IP is picked up at any point by the advisory it leaves a trail and will be blocked quickly
	- Storing client information (the target) in a DB that isn't secure.
		- This risks letting your clients information get out if your company is attacked thus causing a breach
	- Revealing your clients information publicly
		- This can be as little as posting to Facebook about having a new client with their name
		- If a blue team is monitoring this  type of thing you are giving them a heads up to prepare (WHICH WE DONT WANT)
	- Posting who is apart of the Red Team can give your clients IT teams an idea of who is in the team and using OSINT could lead to them knowing skill sets.

### 4. Risk Assessment
- We are determining if the above Vulnerabilities are worth addressing or not.
1.  The efficiency of the countermeasure in reducing the risk
2.  The cost of the countermeasure compared to the impact of the vulnerability being exploited.
3.  The possibility that the countermeasure can reveal information to the adversary

### 5. Countermeasures
- Pulled from the DoD Manual for definition:
	- _"Countermeasures are designed to prevent an adversary from detecting critical information, provide an alternative interpretation of critical information or indicators (deception), or deny the adversary’s collection system.”_


___

## Resources:

| Hyperlink                                                                                  | Info                          |
| ------------------------------------------------------------------------------------------ | ----------------------------- |
| [OPSEC Manual](https://www.esd.whs.mil/Portals/54/Documents/DD/issuances/dodm/520502m.pdf) | DoD Operation Security Manual | 


Created Date: March 23rd 2023 (09:40 pm)  
Last Modified Date: <%+tp.file.last_modified_date("MMMM Do YYYY (hh:ss a)")%>

---
creation date: November 7th 2022
last modified date: November 7th 2022
aliases: []
tags: #🧰
---

Primary Categories: [[01 - Pentest]] - [[01 - Red Team]]
Secondary Categories:  [[02 - Reconnaissance]]
Links: [[03 - Content/Python]] - [[Subdomains]] - [[Content Discovery]] - [[Websites]] - [[02 - Internal Enumeration]] - [[OSINT]]
Search Tag: #🧰  

# [[Sublist3r]]  
___

## Description:
A python tool designed to enumerate subdomains using OSINT

## Installation
- `git clone https://github.com/aboul3la/Sublist3r.git`
### Dependencies
Sublist3r depends on the `requests`, `dnspython` and `argparse` python modules.
**Windows**
- `c:\python27\python.exe -m pip install -r requirements.txt`
**Linux**
- `sudo pip install -r requirements.txt`


## Commands
Short Form    | Long Form     | Description
------------- | ------------- |-------------
-d            | --domain      | Domain name to enumerate subdomains of
-b            | --bruteforce  | Enable the subbrute bruteforce module
-p            | --ports       | Scan the found subdomains against specific tcp ports
-v            | --verbose     | Enable the verbose mode and display results in realtime
-t            | --threads     | Number of threads to use for subbrute bruteforce
-e            | --engines     | Specify a comma-separated list of search engines
-o            | --output      | Save the results to text file
-h            | --help        | show the help message and exit



___

## Resources:

| Hyperlink                                       | Info |
| ----------------------------------------------- | ---- |
| [Github](https://github.com/aboul3la/Sublist3r) | Official repo     |


Created Date: November 7th 2022 (06:05 pm)  
Last Modified Date: <%+tp.file.last_modified_date("MMMM Do YYYY (hh:ss a)")%>

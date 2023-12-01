---
creation date: May 27th 2023
last modified date: May 27th 2023
aliases: []
tags: #📕
---

Primary Categories: 
Secondary Categories:  
Links: 
Search Tag: #📕  

# [[03 - Content/Python]]  
___

## Description:  


## Running A Virtual Environment
1. Get the location of the installed Python you want to use:
```bash
which python<VERSION_NUMBER>
```
2. Run command to create our virtual env:
```bash
virtualenv -p /usr/bin/python2.7 <NAME_OF_VIRTUAL_ENV>
```
- `-p` = Where we put the location of the Python version we want to use
3. Finally we activate our virtual env:
```bash
source <VIRTUAL_ENV_LOCATION>/bin/activate
```
4. Once in you will see the CLI change to something like the following:
![[Pasted image 20230527215531.png]]
- Success we are in!!
- If you want to leave simply use `deactivate` command
5. Finally if you need to install modules for python use either `pip2` or `pip3` depending on which version of Python you are using in this env


___

## Resources:

| Hyperlink | Info |
| --------- | ---- |


Created Date: May 27th 2023 (09:04 pm)  
Last Modified Date: <%+tp.file.last_modified_date("MMMM Do YYYY (hh:ss a)")%>

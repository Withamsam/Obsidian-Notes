---
creation date: April 26th 2023
last modified date: April 26th 2023
aliases: []
tags: #🧰
---

Primary Categories: [[01 - Pentest]] - [[01 - Red Team]]
Secondary Categories:  [[02 - Reconnaissance]]
Links: [[OSINT]]
Search Tag: #🧰  

# [[Recon-ng]]  
___

## Description:
By utilizing different modules created by various authors this tool can help automate OSINT research and save the located data for later viewing.

## Installation
Pre-installed on Kali

## Commands
- Running the following will initiate the framework:
```bash
recon-ng
```
- Will load into the default workspace unless we specify with: `recon-ng -w <NAME_HERE>`
	- This can also create workspaces!

### Creating a Workspace
1. While in the framework use:
```recon-ng
workspace create <NAME_HERE>
```

### Seeding the Database
1. We can start by checking our current **db** to see what table names are:
```recon-ng
db schema
```

2.Next we want to populate it with any current info we have about our target often times this is IP addresses, domains, etc...
```recon-ng
db insert <TABLE_NAME>
```
- Example `db insert domains`

### Finding / Installing Modules
1. We can start by searching the Recon-ng marketplace:
```recon-ng
marketplace search
```

2. Before we install anything here are a few useful commands to gather more info about the modules:
	- `marketplace search <KEYWORD>`
	- `marketplace info <MODULE>`
	- `marketplace install <MODULE>`
	- `marketplace remove <MODULE>`

### Working with Installed Modules
1. We can start by searching for all installed modules
```recon-ng
modules search
```

2. Now we can load the wanted module into memory:
```recon-ng
modules load <MODULE>
```

3. Some modules require options to be set before they will run:
```recon-ng
options list
```

```recon-ng
options set <OPTION> <VALUE>
```

4. Finally once the modules is loaded into memory we can execute it with:
```recon-ng
run
```

### Keys
- Some modules require keys in order to function indicated with **k**
```recon-ng
keys list
```

```recon-ng
keys add <KEY_NAME> <KEY_VALUE>
```

```recon-ng
keys remove <KEY_NAME>
```


___

## Resources:

| Hyperlink | Info |
| --------- | ---- |


Created Date: April 26th 2023 (11:02 pm)  
Last Modified Date: <%+tp.file.last_modified_date("MMMM Do YYYY (hh:ss a)")%>

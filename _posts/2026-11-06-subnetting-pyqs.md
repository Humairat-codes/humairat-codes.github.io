---
layout: post
title: "Subnetting: PYQs part 2"
date: 2026-11-06
categories: [Computer Networks]
---

Q1 The subnet mask for a particular network is $255.255.31.0$. Which of the following pairs of IP addresses could belong to this network?
A. $172.57.88.62$ and $172.56.87.23$
B. $10.35.28.2$ and $10.35.29.4$  
C. $191.203.31.87$ and $191.234.31.88$   
D. $128.8.129.43$ and $128.8.161.55$

31 = 11111
in option B, 28 = 11100
29 = 11101

d) 
31 = 11111
129 = 00001
161 = 00001
d option is correct!

Q2 The routing table of a router is shown below:
Destination | Subnet Mask | Interface
128.75.43.0 | 255.255.255.0 | Eth0
128.75.43.0 | 255.255.255.128 | Eth1
192.12.17.5 | 255.255.255.255 | Eth3
Default |  | Eth2
On which interface will the router forward packets addressed to destinations 128.75.43.16 and 192.12.17.10 respectively?

A. Eth1 and Eth2
B. Eth0 and Eth2
C. Eth0 and Eth3
D. Eth1 and Eth3

=> 128.75.43.16 AND 255.255.255.128 = 128.75.43.0 so Interface is Eth1.
192.12.17.10 will require DEFAULT so Interface is Eth2.
A. Eth1 and Eth2

Q3 An organization has a class B network and wishes to form subnets for 64 departments. The subnet mask would be:
A. 255.255.0.0
B. 255.255.64.0
C. 255.255.128.0
D. 255.255.252.0

class B has 16 bits for NID and 16 bits for HID. 
Subnets = 64 
borrow 6 bits from HID i.e. 2^6 = 64>= 64
HID = 16-6 = 10

answer is 255.255.252.0 i.e. D. 255.255.252.0

Q4 Two computers $C1$ and $C2$ are configured as follows. $C1$ has IP address 203.197.2.53 and netmask 255.255.128.0. $C2$ has IP address 203.197.75.201 and netmask 255.255.192.0. Which one of the following statements is true?

A. $C1$ and $C2$ both assume they are on the same network
B. $C2$ assumes $C1$ is on same network, but $C1$ assumes $C2$ is on a different network
C. $C1$ assumes $C2$ is on same network, but $C2$ assumes $C1$ is on a different network
D. $C1$ and $C2$ both assume they are on different networks.

C1 = 203.197.2.53
netmask1 = 255.255.128.0.
C2 = 203.197.75.201
netmask2 = 255.255.192.0.


C1 and netmask1 = 203.197.2.53 AND 255.255.128.0 = 203.197.0.0
C2 AND netmask1 = 203.197.75.201 AND 255.255.128.0 = 203.197.0.0
C1 thinks C2 belong to the same subnet
C2 AND netmask2 = 203.197.75.201 AND 255.255.192.0 = 203.197.64.0
C1 AND netmask2 = 203.197.2.53 AND 255.255.192.0 = 203.197.0.0

answer is - C. $C1$ assumes $C2$ is on same network, but $C2$ assumes $C1$ is on a different network.

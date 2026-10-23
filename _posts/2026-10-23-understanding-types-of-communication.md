---
layout: post
title: "types of communication"
date: 2026-10-22
categories: [Computer Networks]
---

1. Unicasting - the transmission of data packets from one sender to one receiver in same or different networks.
2. Broadcasting - transmission of data from one source to all hosts in same or different networks
based on same or different networks, broadcasting is divided into - 

a) Limited Broadcasting
b) Direct Broadcasting

a) Limited Broadcasting - transmission in the form of "one to all" happens in the SAME network(thus the name - "limited")
b) Direct Broadcasting -  transmission in the form of "one to all" happens in DIFFERENT networks. 

the IP address for say class A network may be 10.0.0.0. Now, the limited broadcasting IP address is 255.255.255.255. But the direct broadcasting IP address for this network is 10.255.255.255. If from another network, somebody wants to broadcast data to this network, they will put 10.255.255.255 in Destination IP address. 
IMPORTANT - 255.255.255.255 will NEVERRRR be source IP address AND 255.255.255.255 will be limited broadcasting IP address for ALL classes and ALL networks. it doesnt matter whther the network IP address is 13.0.0.0 or 13.56.0.0 or 19.143.99.0. IT DOESNT MATTER. for all these networks, their own broadcasting IP address will be 255.255.255.255!!!!




---
layout: post
title: "Subnetting: PYQs"
date: 2026-11-05
categories: [Computer Networks]
---

MCQ : a subnet has subnet mask 255.255.255.192. What is maximum no of hosts that belong to this subnet? 
a) 14
b) 30
c) 62
d) 126

255.255.255.192 means 11111111.11111111.11111111.11000000
i.e. 16+8+2 = 16+10 = 26 SID bits 
8-2 = 6 bits are for host 
so no. of hosts at max will be 2^6 - 2 = 64-2 = 62 hosts.

MCQ. If a class B network on the internet has a subnet mask of 255.255.248.0, what is the max no of hosts per subnet?
a) 1022
b) 1023
c) 2046
d) 2047
class B means for HID, look at last 16 bits
here, 248 = 1111 1000
so SID is 5 bits 
we get 16-5= 11 bits for HID.
so no. of hosts become at max per subnet 2^11 - 2 = 2^10*2 - 2
1024 * 2 - 2 = 2048 - 2 = 2046 no. of hosts.

MCQ. An organization has a class B network and wishes to form subnets for 64 departments. The subnet mask will be:
a) 255.255.0.0
b) 255.255.64.0
c) 255.255.128.0
d) 255.255.252.0

64 subnets i.e. 6 bits for SID. 
255.255.1111 1100.0
255.255.252.0 is the subnet mask. So answer is D.

MCQ. The address of class B host is to be split into subnet with a 6-bit subnet number. What is the maximum no. of subnets and the max no. of hosts in each subnet?

255.255.1111 1100.0 will be subnet mask 
i.e. 6 bits means 2^6 subnets i.e. 64 subnets

So, 8+2 = 10 bits for HID
no. of hosts = 2^10 - 2 = 1024 - 2 = 1022 hosts.

MCQ. Consider M,N,P with IP addresses 100.10.5.2, 100.10.5.5, 100.10.5.6. The subnet mask is 255.255.255.252. what is true?
M = 100.10.5.2
N = 100.10.5.5
P = 100.10.5.6
subnet mask is 255.255.255.252

252 = 1111 1100
so HID bits from here are 2, 
to check if they all belong to the same subnet,
you may want to AND them with the subnet mask to get the same Subnet ID for them to see it.
However you just need to check their SID bits to make that conclusion. Because if it is same then, their AND would give the same output. It makes calculation faster.
in last octet, (because all of them have same first 3 octets. No need to check them!)
weights - 128 64 32 16 8 4
for 2 -    0  0  0  0  0 0
for 5 -    0  0  0  0  0 1
for 6 -    0  0  0  0  0 1
conclusion: N and P belong to same subnet.
M belongs to a different subnet.

MCQ. The subnet mask for a particular network is 255.255.31.0
which pair belongs to the same network?

a) 172.57.88.62 and 172.56.87.23
b) 10.35.28.2 and 10.35.29.4
c) 191.203.31.87 and 191.234.31.88
d) 128.8.129.43 and 128.8.161.55

subnet mask = 255.255.31.0
31 = 000 11111
i.e. 16 8 4 2 1
look at last 5 digits of each in 3rd octet. if it is same, then its from same subnet given that the first 2 octets are also same
no need to check a) because the 2nd octet is different. 
b) 28 is 000 11100 and 29 is 000 11101 so different
c) the 2nd octet is different. no need to check
d) 129 is 100 00001 and 161 is 101 00001. SAME LAST 5 BITS SO they belong to the SAME SUBNET.
answer is d) 128.8.129.43 and 128.8.161.55

MCQ. A = 10.105.1.113
B = 10.105.1.91 same subnet mask N
Which values of N should not be used if A and B belong to same network?
a) 255.255.255.0
b) 255.255.255.128
c) 255.255.255.192
d) 255.255.255.224

both have same first 3 octets and 255 is given in all 3 octets in all options so focus on the last octet only
113 = 0111 0001
91 = 0101 1011
in a) both will get same subnet as 10.105.1.0 so its a valid subnet mask
in b) 255.255.255.128 here 128 = 1000 0000 so look at MSB of both, its same. So its a valid subnet mask
in c) 255.255.255.192 here 192 = 1100 0000 so, are 2 MSB of both A and B same? YES. So its a valid subnet mask. 
in d) 255.255.255.224 here 224 = 1110 0000 so, are 3 MSB of both A and B same? NO. So it is NOT a valid subnet mask if A and B are in same network.

answer is d) 255.255.255.224

MCQ. Host X has IP address 192.168.1.97 and is connected through two routers R1 and R2 to another host Y with IP address 192.168.1.80
R1 = 192.168.1.135 and 192.168.1.110
R2 = 192.1.68.67 and 192.168.1.155
subnet mask = 255.255.255.224
how many distinct subnets are there in the network?
a) 1
b) 2
c) 3
d) 6
224 = 111 00000. SID bits are 3. i.e. 2^2 = 8 subnets can exist. 
look at the last octets of each IP address
X => 97 = 011
R1 => 135 = 100
110 => 011 (SAME AS 97)
R2 => 110 = 100
155 => 100 (SAME AS OTHER R2)
Y => 80 = 010

different subnets due to these become 3. 

MCQ. Host X = 192.168.1.97
Y = 192.168.1.80
R1 = 192.168.1.135 and 192.168.1.110
R2 = 192.68.1.67 and 192.168.1.155
netmask = 255.255.255.224
Which IP address should X configure its gateway as ? 
a) 192.168.1.67
b) 192.168.1.110
c) 192.168.1.135
d) 192.168.1.155







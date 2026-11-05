---
layout: post
title: "Subnetting: PYQs"
date: 2026-11-05
categories: [Computer Networks]
---

## Quick rules

- **Number of 1's in the mask = NID + SID**, and **number of 0's = HID**.
- **Hosts per subnet = 2^HID − 2**
- **Same SID bits (and same NID) means the same subnet.** You don't need the full AND. Just compare the SID bits.

---

## Q1: Maximum hosts for mask 255.255.255.192

A subnet has subnet mask `255.255.255.192`. What is the maximum number of hosts in this subnet?

a) 14  b) 30  c) 62  d) 126

1. `255.255.255.192` = `11111111.11111111.11111111.11000000`
2. Number of 1's = 24 + 2 = **26** (NID + SID), so there are **2 SID bits** in the last octet.
3. HID = 8 − 2 = **6 bits**.
4. Hosts = 2⁶ − 2 = 64 − 2 = **62**

**Answer: c) 62**

---

## Q2: Class B with mask 255.255.248.0

If a Class B network has a subnet mask of `255.255.248.0`, what is the maximum number of hosts per subnet?

a) 1022  b) 1023  c) 2046  d) 2047

1. Class B, so look at the last 16 bits for the HID.
2. `248` = `1111 1000`, so SID = **5 bits**.
3. HID = 16 − 5 = **11 bits**.
4. Hosts = 2¹¹ − 2 = 2048 − 2 = **2046**

**Answer: c) 2046**

---

## Q3: Class B network with 64 departments

An organization has a Class B network and wishes to form subnets for 64 departments. The subnet mask will be:

a) `255.255.0.0`  b) `255.255.64.0`  c) `255.255.128.0`  d) `255.255.252.0`

1. 64 subnets = 2⁶, so **6 bits** are needed for the SID.
2. The mask is `255.255.1111 1100.0` = `255.255.252.0`.

**Answer: d) 255.255.252.0**

---

## Q4: 6-bit subnet number in Class B

The address of a Class B host is to be split into subnets with a **6-bit subnet number**. What is the maximum number of subnets and the maximum number of hosts in each subnet?

1. The mask is `255.255.1111 1100.0`.
2. 6 bits means 2⁶ = **64 subnets**.
3. HID = 8 + 2 = **10 bits**.
4. Hosts per subnet = 2¹⁰ − 2 = 1024 − 2 = **1022**

**Answer: 64 subnets and 1022 hosts per subnet**

> **Exam note:** Under the old classful rule (RFC 950), the **all-0's and all-1's subnets are not allowed**, which gives **62 subnets** instead of 64. Some answer keys use that. The hosts per subnet stay **1022** either way. Follow whichever convention your course uses.

---

## Q5: Same subnet? (mask 255.255.255.252)

Consider M, N, P with IP addresses `100.10.5.2`, `100.10.5.5`, `100.10.5.6`. The subnet mask is `255.255.255.252`. What is true?

`252` = `1111 1100`, so there are **6 SID bits** and **2 HID bits** in the last octet.

You could AND each address with the mask, but you only need to check the **SID bits**. If they match, the AND gives the same output. This is faster.

The first 3 octets are the same for all three, so only the last octet matters.

| Weights | 128 | 64 | 32 | 16 | 8 | 4 |
|---------|-----|----|----|----|---|---|
| M (2) | 0 | 0 | 0 | 0 | 0 | 0 |
| N (5) | 0 | 0 | 0 | 0 | 0 | 1 |
| P (6) | 0 | 0 | 0 | 0 | 0 | 1 |

**Answer: N and P are in the same subnet. M is in a different subnet.**

---

## Q6: Mask 255.255.31.0, which pair is in the same network?

The subnet mask for a particular network is `255.255.31.0`. Which pair of IP addresses could belong to the same network?

a) `172.57.88.62` and `172.56.87.23`
b) `10.35.28.2` and `10.35.29.4`
c) `191.203.31.87` and `191.234.31.88`
d) `128.8.129.43` and `128.8.161.55`

`31` = `000 11111`, so only the **last 5 bits of the 3rd octet** (weights 16, 8, 4, 2, 1) are 1's. Compare those bits, as long as the first 2 octets are also the same. The 4th octet has mask `0`, so it is ignored.

- **a)** the 2nd octets differ (`57` vs `56`), so **no**. No need to check further.
- **b)** `28` = `000 11100` and `29` = `000 11101`, so the last 5 bits are **different**, **no**.
- **c)** the 2nd octets differ (`203` vs `234`), so **no**.
- **d)** `129` = `100 00001` and `161` = `101 00001`. The last 5 bits are **the same** (`00001`), and the first two octets match, so **YES**.

**Answer: d) 128.8.129.43 and 128.8.161.55**

> **Note:** This mask is a **non-contiguous mask** (the 1's are not all on the left). It works the same way. Just compare the bit positions where the mask has 1's.

---

## Q7: Which mask should NOT be used?

`A = 10.105.1.113` and `B = 10.105.1.91` have the same subnet mask N. Which value of N should **not** be used if A and B belong to the same network?

a) `255.255.255.0`  b) `255.255.255.128`  c) `255.255.255.192`  d) `255.255.255.224`

The first 3 octets are the same and fully masked in all options, so focus on the **last octet**:

- `113` = `0111 0001`
- `91` = `0101 1011`

| Option | Mask bits | Bits compared | Same? | Valid mask? |
|--------|-----------|---------------|-------|-------------|
| a) 255.255.255.0 | none in last octet | n/a | Same subnet `10.105.1.0` | Valid |
| b) 128 | `1000 0000` | 1 MSB: `0` and `0` | Yes | Valid |
| c) 192 | `1100 0000` | 2 MSBs: `01` and `01` | Yes | Valid |
| d) 224 | `1110 0000` | 3 MSBs: `011` and `010` | **NO** | **NOT valid** |

**Answer: d) 255.255.255.224**

---

## Q8: How many distinct subnets?

Host X (`192.168.1.97`) is connected through two routers R1 and R2 to host Y (`192.168.1.80`).

- R1 has `192.168.1.135` and `192.168.1.110`
- R2 has `192.168.1.67` and `192.168.1.155`
- Subnet mask = `255.255.255.224`

How many distinct subnets are there?

a) 1  b) 2  c) 3  d) 6

`224` = `111 00000`, so there are **3 SID bits**, which allows 2³ = 8 possible subnets.

Look at the top 3 bits of the last octet of each address:

| Address | Owner | Last octet | SID bits |
|---------|-------|------------|----------|
| `192.168.1.97` | X | `011 00001` | `011` |
| `192.168.1.110` | R1 | `011 01110` | `011` (same as X) |
| `192.168.1.135` | R1 | `100 00111` | `100` |
| `192.168.1.155` | R2 | `100 11011` | `100` (same as R1's 135) |
| `192.168.1.67` | R2 | `010 00011` | `010` |
| `192.168.1.80` | Y | `010 10000` | `010` (same as R2's 67) |

So the three distinct subnets are `011`, `100` and `010`.

**Answer: c) 3**

---

## Q9: Which gateway should X use?

Same network as Q8. Which IP address should X configure as its **gateway**?

a) `192.168.1.67`  b) `192.168.1.110`  c) `192.168.1.135`  d) `192.168.1.155`

The gateway is where X sends packets for hop-by-hop delivery. It has to be a router interface **in X's own subnet**, so X can reach it directly.

Compute the subnet ID of each address (AND with `255.255.255.224`):

```
X (97):        192.168.1.0110 0001  AND  255.255.255.1110 0000  =  192.168.1.96
R1 (110):      192.168.1.0110 1110  AND  255.255.255.1110 0000  =  192.168.1.96
R1 (135):      192.168.1.1000 0111  AND  255.255.255.1110 0000  =  192.168.1.128
```

X and R1's interface `192.168.1.110` are both in subnet `192.168.1.96`, so they're directly connected.

**Answer: b) 192.168.1.110**

---

## Q10: Number of Class C networks

In IPv4, the number of networks under Class C addresses is:

a) 2¹⁴  b) 2⁷  c) 2²¹  d) 2²⁴

- Class C has **24 bits for NID** and **8 bits for HID**.
- The first **3 bits are fixed** as `110` to identify the class.
- So the bits we can change are 5 + 8 + 8 = **21 bits**.

**Answer: c) 2²¹**

---

## Q11: Class B subnet with DBA 144.16.95.255

A subnet in Class B has the DBA `144.16.95.255`. What is its subnet mask?

a) `255.255.224.0`  b) `255.255.240.0`  c) `255.255.248.0`  d) all of the above

Don't even look at the first 2 octets (that's the NID). `95` = `0101 1111` has **5 trailing 1's**, and the 4th octet adds 8 more, so **HID ≤ 5 + 8 = 13**.

| Option | 3rd octet | HID bits | HID ≤ 13? |
|--------|-----------|----------|-----------|
| a) 224 | `1110 0000` | 5 + 8 = 13 | Yes |
| b) 240 | `1111 0000` | 4 + 8 = 12 | Yes |
| c) 248 | `1111 1000` | 3 + 8 = 11 | Yes |

> **IMPORTANT:** The DBA tells you the **MAXIMUM** HID, not the exact value. Any mask with **HID ≤ 13** is valid.

**Answer: d) all of the above**

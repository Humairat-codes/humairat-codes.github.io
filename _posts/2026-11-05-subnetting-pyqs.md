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

---

## Forwarding table questions

> **NAT** = *Numerical Answer Type* (GATE): you type a number instead of picking an option.

### Rules for forwarding/routing tables

1. Take the destination IP and go through the table, starting with the **longest mask** (the one with the most 1's).
2. **AND** the destination IP with that entry's mask. If the result **equals that entry's network/subnet number**, it's a match, so use that entry's interface or next hop.
3. If it doesn't match, move on to the next longest mask.
4. If nothing matches, use the **default** entry.

> **IMPORTANT:** An address can match **several** entries. The one with the **longest mask wins** (this is called *longest prefix match*).

---

## Q12 (NAT): Which interface?

The forwarding table of a router is:

| Subnet number | Subnet mask | Interface ID |
|---------------|-------------|--------------|
| `200.150.0.0` | `255.255.0.0` | 1 |
| `200.150.64.0` | `255.255.224.0` | 2 |
| `200.150.68.0` | `255.255.255.0` | 3 |
| `200.150.68.64` | `255.255.255.224` | 4 |
| default | n/a | 0 |

A packet addressed to `200.150.68.118` arrives at the router. It will be forwarded to the interface with ID ______.

**Step 1: longest mask, `255.255.255.224`.** Only the last octet matters:

```
  118 = 0111 0110
  224 = 1110 0000   AND
  ------------------
        0110 0000 = 96   →  200.150.68.96
```

`200.150.68.96` does **not** match the subnet number `200.150.68.64`, so no match.

**Step 2: next mask, `255.255.255.0`.** The mask is `255` in the first three octets and `0` in the last, so the first three octets stay the same and the last becomes 0 (no need to AND again): `200.150.68.0`.

That **matches** the subnet number `200.150.68.0`, so the packet goes to interface **3**.

**Answer: 3**

---

## Q13 (MCQ): Routing table with two destinations

| Destination | Subnet mask | Interface |
|-------------|-------------|-----------|
| `128.75.43.0` | `255.255.255.0` | eth0 |
| `128.75.43.0` | `255.255.255.128` | eth1 |
| `192.12.17.5` | `255.255.255.255` | eth3 |
| default | n/a | eth2 |

On which interface will packets for `128.75.43.16` and `192.12.17.10` be forwarded?

a) eth1 and eth2  b) eth0 and eth2  c) eth0 and eth3  d) eth1 and eth3

**For `128.75.43.16`:**

- Mask `255.255.255.255` gives `128.75.43.16`, which is not `192.12.17.5`, so no match.
- Mask `255.255.255.128`: the last octet is `16` = `0001 0000`, and `0001 0000` AND `1000 0000` = `0`, so the result is `128.75.43.0`. **It matches, so eth1.**

> **IMPORTANT:** `128.75.43.16` also matches the `/24` entry (eth0), but the `255.255.255.128` mask is **longer**, so eth1 wins.

**For `192.12.17.10`:**

- Mask `255.255.255.255` gives `192.12.17.10`, not `192.12.17.5`, so no match.
- Mask `255.255.255.128` gives `192.12.17.0`, not `128.75.43.0`, so no match.
- Mask `255.255.255.0` gives `192.12.17.0`, no match.
- Nothing matches, so the **default** is used: **eth2**.

**Answer: a) eth1 and eth2**

---

## Q14 (MCQ): Network table with next hops

| Network no. | Net mask | Next hop |
|-------------|----------|----------|
| `128.96.170.0` | `255.255.254.0` | interface 0 |
| `128.96.168.0` | `255.255.254.0` | interface 1 |
| `128.96.166.0` | `255.255.254.0` | R2 |
| `128.96.164.0` | `255.255.252.0` | R3 |
| `0.0.0.0` | default | R4 |

Find the next hop for `128.96.171.92`, `128.96.167.151`, `128.96.163.121` and `128.96.165.121`.

Only the **3rd octet** changes, so compare only that:

- `254` = `1111 1110` (the `/23` entries)
- `252` = `1111 1100` (the `/22` entry)

| Destination | 3rd octet | AND with 254 (`/23`) | AND with 252 (`/22`) | Match | Next hop |
|-------------|-----------|----------------------|----------------------|-------|----------|
| `128.96.171.92` | `1010 1011` (171) | `1010 1010` = 170 → `128.96.170.0` | not needed | `/23` entry | **interface 0** |
| `128.96.167.151` | `1010 0111` (167) | `1010 0110` = 166 → `128.96.166.0` | not needed | `/23` entry | **R2** |
| `128.96.163.121` | `1010 0011` (163) | `1010 0010` = 162, no match | `1010 0000` = 160, no match | none | **R4 (default)** |
| `128.96.165.121` | `1010 0101` (165) | `1010 0100` = 164, no match | `1010 0100` = 164 → `128.96.164.0` | `/22` entry | **R3** |

> **IMPORTANT:** For `128.96.165.121`, the `/23` AND result is `164`, but **no `/23` entry** has the network number 164 (they are 170, 168 and 166). You only compare with entries that use **the same mask**. It then matches the `/22` entry instead.

**Answers:** `128.96.171.92` goes to interface 0, `128.96.167.151` to R2, `128.96.163.121` to R4, and `128.96.165.121` to R3.

---

## Q15 (NAT): Packets forwarded via R2

| Prefix | Next hop router |
|--------|-----------------|
| `10.1.1.0/24` | R1 |
| `10.1.1.128/25` | R2 |
| `10.1.1.64/26` | R3 |
| `10.1.1.192/26` | R4 |

The router forwards **20 packets each** to 5 hosts: `10.1.1.16`, `10.1.1.72`, `10.1.1.132`, `10.1.1.191`, `10.1.1.205`. How many packets are forwarded via R2?

The masks are `/24` = `255.255.255.0`, `/25` = `255.255.255.128`, and `/26` = `255.255.255.192`. Check `/26` first, then `/25`, then `/24`.

| Host | Last octet | `/26` result | `/25` result | `/24` result | Next hop |
|------|-----------|--------------|--------------|--------------|----------|
| `10.1.1.16` | `0001 0000` | `10.1.1.0`, no | `10.1.1.0`, no | `10.1.1.0`, **yes** | R1 |
| `10.1.1.72` | `0100 1000` | `10.1.1.64`, **yes** | not needed | not needed | R3 |
| `10.1.1.132` | `1000 0100` | `10.1.1.128`, no | `10.1.1.128`, **yes** | not needed | **R2** |
| `10.1.1.191` | `1011 1111` | `10.1.1.128`, no | `10.1.1.128`, **yes** | not needed | **R2** |
| `10.1.1.205` | `1100 1101` | `10.1.1.192`, **yes** | not needed | not needed | R4 |

> **IMPORTANT:** `10.1.1.191` is a trap. It's in the block 128 to 191, but there is **no `/26` entry** for `10.1.1.128`, so it falls through to the `/25` entry (R2).

R2 receives the packets for 2 hosts (`.132` and `.191`): 20 + 20 = **40 packets**.

**Answer: 40**

---

## Q16 (MCQ): VLSM with 100, 50 and 50 hosts

A company has the Class C network `204.204.204.0`. It wants subnets with **100 hosts in one** and **50 hosts in each of two others**. Which is a feasible set of subnet address/subnet mask pairs?

**Why equal-sized subnets don't work:**

- Class C has 8 host bits. 3 subnets needs **2 SID bits** (2² = 4 ≥ 3), which leaves **6 host bits**.
- 2⁶ − 2 = 62 hosts, but we need **100**, so this is **NOT possible**!
- 100 hosts needs **7 host bits** (2⁷ − 2 = 126 ≥ 100), which leaves only **1 SID bit** (2 subnets).

So we need **VLSM** (Variable Length Subnet Masks): subnets of different sizes.

**Method:**

1. Borrow **1 bit** to get 2 subnets: `204.204.204.0` and `204.204.204.128`, with mask `255.255.255.128`. Each has 2⁷ − 2 = 126 hosts, which is ≥ 100.
2. Take **one** of them for the 100-host subnet.
3. Divide the **other** one by borrowing 1 more bit, giving two subnets with mask `255.255.255.192`. Each has 2⁶ − 2 = 62 hosts, which is ≥ 50.

**Two feasible allocations:**

| | Subnet | Hosts needed | Subnet address | Mask |
|---|--------|--------------|----------------|------|
| **Option A** | X | 100 | `204.204.204.0` | `255.255.255.128` |
| | Y | 50 | `204.204.204.128` | `255.255.255.192` |
| | Z | 50 | `204.204.204.192` | `255.255.255.192` |
| **Option B** | X | 100 | `204.204.204.128` | `255.255.255.128` |
| | Y | 50 | `204.204.204.0` | `255.255.255.192` |
| | Z | 50 | `204.204.204.64` | `255.255.255.192` |

> **Remember:** the 100-host subnet takes up a **whole half** (0 to 127 or 128 to 255). The two 50-host subnets must fit in the **other half**, so they can't overlap with it.

---

## Q17 (MCQ): Different masks on two computers

**C1** = `203.197.2.53` with netmask `255.255.128.0` (`/17`)
**C2** = `203.197.75.201` with netmask `255.255.192.0` (`/18`)

What is true?

**Shortcut: block size** = 256 − (mask value in the interesting octet).

| Computer | Mask | Block size (3rd octet) | Its own network |
|----------|------|------------------------|-----------------|
| C1 | `255.255.128.0` | 256 − 128 = **128** | `203.197.0.0` to `203.197.127.255` |
| C2 | `255.255.192.0` | 256 − 192 = **64** | `203.197.64.0` to `203.197.127.255` |

For C2: `75` = `0100 1011` AND `1100 0000` = `0100 0000` = 64, so the subnet is `203.197.64.0`.

**What each computer thinks:**

- **C1's view of C2:** `75` is inside `0` to `127`, so C1 thinks C2 is on the **same** network.
- **C2's view of C1:** `2` = `0000 0010` AND `1100 0000` = `0`, so the subnet would be `203.197.0.0`, which is not C2's `203.197.64.0`. C2 thinks C1 is on a **different** network.

**Answer: C1 assumes C2 is on the same network, but C2 assumes C1 is on a different network.**

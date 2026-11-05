---
layout: post
title: "Subnetting: Super questions"
date: 2026-11-04
categories: [Computer Networks]
---

## Quick rules (read these first!)

| Want to find | Rule |
|--------------|------|
| Subnet ID | **IP AND subnet mask** |
| SID bits | **number of 1's in the mask − NID bits** (class A = 8, B = 16, C = 24) |
| Number of subnets | **2^SID** (not possible if the 1's are fewer than the NID bits) |
| HID bits | **number of 0's in the mask** |
| IP addresses per subnet | **2^HID** |
| Hosts per subnet | **2^HID − 2** |
| First host | subnet ID + 1 |
| Last host | DBA − 1 |
| DBA (direct broadcast address) | subnet ID with **all host bits = 1** |

> **IMPORTANT:** In a DBA, **ALL host bits must be 1**. So the last HID bits of the address must all be 1. Having *extra* 1's before them is fine.

> **IMPORTANT:** Subnets are numbered **from 0**, so the **n-th subnet** has the binary value **(n − 1)**. The 3rd subnet is `010`, not `011`.

---

## Part 1: Subnet address and number of subnets

### Q1: Subnet address

**IP** = `200.34.22.156`, **mask** = `255.255.255.240`

Subnet address = IP AND mask. Only the last octet matters:

```
  1001 1100   (156)
AND
  1111 0000   (240)
= 1001 0000   (128 + 16 = 144)
```

**Subnet address = `200.34.22.144`**

### Q2: Mask 255.252.0.0

`252` = `1111 1100`, so the mask is `11111111.11111100.00000000.00000000`. That's 14 ones and 18 zeros.

| Item | Value |
|------|-------|
| IP addresses per subnet | 2¹⁸ |
| Hosts per subnet | 2¹⁸ − 2 |
| Subnets in Class A | 2⁶ (14 − 8 = 6 SID bits) |
| Subnets in Class B | Not possible (14 < 16) |
| Subnets in Class C | Not possible (14 < 24) |

### Q3a: Mask 255.255.224.0

`11111111.11111111.11100000.00000000` has 19 ones.

| Class | SID bits | Number of subnets |
|-------|----------|-------------------|
| A | 19 − 8 = 11 | 2¹¹ |
| B | 19 − 16 = 3 | 2³ |
| C | n/a | Not possible |

### Q3b: Mask 255.255.255.192

`192` = `1100 0000`, so the mask has 26 ones.

| Class | SID bits | Number of subnets |
|-------|----------|-------------------|
| A | 18 | 2¹⁸ |
| B | 10 | 2¹⁰ |
| C | 2 | 2² |

---

## Part 2: Direct broadcast address (DBA)

### Q3c: Mask 255.255.255.240

`240` = `1111 0000`, so there are 4 host bits in the last octet. In a DBA those 4 bits are all 1 (`1111` = 15).

So the last octet must end in `1111`. Examples: `200.56.78.15`, `200.56.78.31`, `200.56.78.47`.

### Q4: Mask 255.255.240.0. Which one is a DBA?

a. `157.157.15.255`  b. `157.157.7.255`  c. `157.157.15.250`  d. `157.157.31.255`

`11111111.11111111.11110000.00000000` has 12 zeros, so the **last 12 bits must all be 1**.

| Option | Last 2 octets in binary | Last 12 bits all 1? | DBA? |
|--------|-------------------------|---------------------|------|
| a | `00001111.11111111` | Yes | **Yes** |
| b | `00000111.11111111` | No (only 11 trailing 1's) | No |
| c | `00001111.11111010` | No (ends in 0) | No |
| d | `00011111.11111111` | Yes (13 trailing 1's, 12 needed) | **Yes** |

**Answer: a and d**

### Q5: Mask 255.224.0.0. Which one is a DBA?

a. `100.31.255.255`  b. `100.7.255.255`  c. `100.63.255.255`  d. `100.30.255.255`

`224` = `1110 0000`, so HID = 5 + 8 + 8 = **21 bits**. The last 21 bits must all be 1.

| Option | 2nd octet | Trailing 1's | DBA? |
|--------|-----------|--------------|------|
| a | `0001 1111` | 21 | **Yes** |
| b | `0000 0111` | 19 | No |
| c | `0011 1111` | 22 | **Yes** |
| d | `0001 1110` | 20 | No |

**Answer: a and c**

### Q6: Mask 255.255.255.224. Which is a DBA?

a) `202.15.19.127`  b) `202.15.19.63`  c) both a and b  d) none

`224` = `1110 0000`, so the **last 5 bits** must be 1.

- a) `127` = `0111 1111`: last 5 bits are 1, so it's a DBA.
- b) `63` = `0011 1111`: last 5 bits are 1, so it's a DBA.

**Answer: c) both a and b**

### Q7: DBA = 200.200.200.31. What is the subnet mask?

a) `255.255.255.192`  b) `255.255.255.224`  c) `255.255.255.248`  d) `255.255.255.128`

`31` = `0001 1111`. It has 5 trailing 1's, so **HID ≤ 5**. (HID can be at most 5, but it can be smaller.)

| HID bits | Last octet of mask | Mask |
|----------|--------------------|------|
| 5 | `1110 0000` | 224 |
| 4 | `1111 0000` | 240 |
| 3 | `1111 1000` | 248 |
| 2 | `1111 1100` | 252 |
| 1 | `1111 1110` | 254 |

**Check the options:**

| Option | Last octet | HID | HID ≤ 5? |
|--------|-----------|-----|----------|
| a) 192 | `1100 0000` | 6 | No |
| b) 224 | `1110 0000` | 5 | **Yes** |
| c) 248 | `1111 1000` | 3 | **Yes** |
| d) 128 | `1000 0000` | 7 | No |

**Answer: b and c**

### Q8: Class B subnet, DBA = 144.16.95.255. What is the mask?

a) `255.255.224.0`  b) `255.255.240.0`  c) `255.255.248.0`  d) all of the above

`144.16` is the NID. Look at `95.255` = `0101 1111.1111 1111`: it has 13 trailing 1's, so **HID ≤ 13**.

- a) `224.0` = `1110 0000.00000000`: HID = 13, valid
- b) `240.0` = `1111 0000.00000000`: HID = 12, valid
- c) `248.0` = `1111 1000.00000000`: HID = 11, valid

**Answer: d) all of the above**

### Q9: DBA = 125.25.63.255. What is the mask?

a) `255.255.128.0`  b) `255.255.192.0`  c) `255.255.224.0`  d) both b and c

The options all start with `255.255`, so only the last two octets matter. `63.255` = `0011 1111.1111 1111` has 14 trailing 1's, so **HID ≤ 14**.

- a) `128.0`: HID = 7 + 8 = 15 > 14, not valid
- b) `192.0`: HID = 6 + 8 = 14, valid
- c) `224.0`: HID = 5 + 8 = 13, valid

**Answer: d) both b and c**

### Q10: DBA = 200.200.200.31. What is the mask?

a) `255.255.255.192`  b) `255.255.255.224`  c) `255.255.255.198`  d) `255.255.255.128`

The options start with `255.255.255`, so it's Class C (NID = 24 bits). `31` = `0001 1111`, so **HID ≤ 5**.

- a) `192` = `1100 0000`: HID = 6 > 5, no
- b) `224` = `1110 0000`: HID = 5, **yes**
- c) `198` = `1100 0110`: the pattern is `s s h h h s s h`, so the host bits are not at the end. A DBA would need 1's in those scattered host positions, and `31` has a 0 in one of them. So 31 can never be a DBA here, no
- d) `128` = `1000 0000`: HID = 7 > 5, no

**Answer: b**

---

## Part 3: Are the machines in the same subnet?

> **Method:** compare the **SID bits** of each IP address. Same SID bits (with the same NID) means the same subnet.

### Q11: M, N, P with mask 255.255.192.0

**M** = `157.157.38.90`, **N** = `157.157.48.90`, **P** = `157.157.68.90`

`192` = `1100 0000`, so we AND the 3rd octet with `1100 0000`:

| Machine | 3rd octet | AND with 192 | Subnet ID |
|---------|-----------|--------------|-----------|
| M | `0010 0110` (38) | `0000 0000` | `157.157.0.0` |
| N | `0011 0000` (48) | `0000 0000` | `157.157.0.0` |
| P | `0100 0100` (68) | `0100 0000` | `157.157.64.0` |

**Answer: M and N are in the same subnet. P is in a different subnet.**

### Q12: Same machines, mask 255.255.240.0

`240` = `1111 0000`, so there are **4 SID bits** in the 3rd octet. The first two octets (`157.157`) are the same for all three, so only the 3rd octet matters.

| Weights | 128 | 64 | 32 | 16 | Subnet ID |
|---------|-----|----|----|----|-----------|
| M (38) | 0 | 0 | 1 | 0 | `157.157.32.0` |
| N (48) | 0 | 0 | 1 | 1 | `157.157.48.0` |
| P (68) | 0 | 1 | 0 | 0 | `157.157.64.0` |

**Answer: all three are in DIFFERENT subnets.**

### Q13: Mask 255.224.0.0

**M** = `100.40.38.90`, **N** = `100.92.48.90`, **P** = `100.80.68.90`

`224` = `1110 0000`, so there are **3 SID bits** in the 2nd octet.

| Weights | 128 | 64 | 32 | Subnet ID |
|---------|-----|----|----|-----------|
| M (40) | 0 | 0 | 1 | `100.32.0.0` |
| N (92) | 0 | 1 | 0 | `100.64.0.0` |
| P (80) | 0 | 1 | 0 | `100.64.0.0` |

**Answer: N and P are in the same subnet.**

### Q14: Mask 255.255.255.252

**M** = `100.10.5.2`, **N** = `100.10.5.5`, **P** = `100.10.5.6`

`252` = `1111 1100`, so there are **6 SID bits** in the last octet.

| Weights | 128 | 64 | 32 | 16 | 8 | 4 | Subnet ID |
|---------|-----|----|----|----|---|---|-----------|
| M (2) | 0 | 0 | 0 | 0 | 0 | 0 | `100.10.5.0` |
| N (5) | 0 | 0 | 0 | 0 | 0 | 1 | `100.10.5.4` |
| P (6) | 0 | 0 | 0 | 0 | 0 | 1 | `100.10.5.4` |

**Answer: N and P are in the same subnet.**

---

## Part 4: Subnet ID and subnet number

### Q15: IP = 200.200.200.60, mask = 255.255.255.224

`224` = `1110 0000`, so there are **3 SID bits**. Weights: 128, 64, 32.

`60` = `001 11100`. The SID bits are `001`, so the subnet ID is `001 00000` = **`200.200.200.32`**.

| SID bits | Decimal | Subnet number |
|----------|---------|---------------|
| `000` | 0 | 1st |
| `001` | 1 | **2nd** |
| `010` | 2 | 3rd |
| `011` | 3 | 4th |
| `100` | 4 | 5th |
| `101` | 5 | 6th |
| `110` | 6 | 7th |
| `111` | 7 | 8th |

> **IMPORTANT:** `001` is **1** in decimal, but it's the **2nd** subnet, because we start counting from 0!

**Answer: subnet ID = `200.200.200.32`, subnet number = 2nd.**

### Q16: Two more

**(a) IP = 200.200.200.80, mask = 255.255.255.224**

- SID = 3 bits (weights 128, 64, 32).
- `80` = `010 10000`, so SID = `010` = 2, which is the **3rd subnet**.
- Subnet ID = `010 00000` = **`200.200.200.64`**.

**(b) IP = 200.200.200.122, mask = 255.255.255.240**

- `240` = `1111 0000`, so SID = 4 bits.
- `122` = `0111 1010`, so SID = `0111` = 7, which is the **8th subnet**.
- Subnet ID = `0111 0000` = **`200.200.200.112`**.

---

## Part 5: Subnet ID, first host, last host, DBA

### Q17: IP = 157.157.52.80, mask = 255.255.224.0

`224` = `1110 0000`, so there are **3 SID bits** (weights 128, 64, 32).

`52` = `001 10100`, so SID = `001`.

| Item | Value |
|------|-------|
| Subnet ID | `157.157.0010 0000.0000 0000` = **`157.157.32.0`** |
| First host | **`157.157.32.1`** |
| DBA | `157.157.0011 1111.1111 1111` = **`157.157.63.255`** |
| Last host | **`157.157.63.254`** |

**Same IP with mask 255.255.192.0:**

`192` = `1100 0000`, so there are **2 SID bits** (weights 128, 64). `52` = `00 110100`, so SID = `00`.

| Item | Value |
|------|-------|
| Subnet ID | **`157.157.0.0`** |
| First host | **`157.157.0.1`** |
| Last host | **`157.157.63.254`** |
| DBA | **`157.157.63.255`** |

### Q18: IP = 100.160.50.60, mask = 255.252.0.0

`252` = `1111 1100`, so there are **6 SID bits** in the 2nd octet (weights 128, 64, 32, 16, 8, 4).

`160` = `101000 00` (128 + 32), so SID = `101000`.

| Item | Value |
|------|-------|
| Subnet ID | **`100.160.0.0`** |
| First host | **`100.160.0.1`** |
| DBA | `100.10100011.255.255` = **`100.163.255.255`** |
| Last host | **`100.163.255.254`** |

---

## Part 6: Finding specific subnets and hosts

### Q19: IP = 200.200.200.90, mask = 255.255.255.224. Find the 3rd and 7th subnet ID

SID = 3 bits (weights 128, 64, 32). The IP itself isn't needed here, only the mask.

| Subnet | Binary (n − 1) | Subnet ID |
|--------|----------------|-----------|
| 3rd | `010` | `200.200.200.64` |
| 7th | `110` | `200.200.200.192` (128 + 64) |

### Q20: IP = 200.200.200.90, mask = 255.255.255.240. Find the 4th and 6th subnet

`240` = `1111 0000`, so SID = 4 bits.

| Subnet | Binary (n − 1) | Subnet ID |
|--------|----------------|-----------|
| 4th | `0011` | `200.200.200.0011 0000` = **`200.200.200.48`** (32 + 16) |
| 6th | `0101` | `200.200.200.0101 0000` = **`200.200.200.80`** (64 + 16) |

### Q21: IP = 125.200.100.90, mask = 255.252.0.0

Find the 3rd host in the 2nd subnet, the 4th host in the 3rd subnet, and the 1st host in the 4th subnet.

`252` = `1111 1100`, so there are 6 SID bits in the 2nd octet.

| Wanted | Subnet bits (n − 1) | Subnet ID | Host |
|--------|---------------------|-----------|------|
| 3rd host in 2nd subnet | `000001` | `125.0000 0100.0.0` = `125.4.0.0` | **`125.4.0.3`** |
| 4th host in 3rd subnet | `000010` | `125.0000 1000.0.0` = `125.8.0.0` | **`125.8.0.4`** |
| 1st host in 4th subnet | `000011` | `125.0000 1100.0.0` = `125.12.0.0` | **`125.12.0.1`** |

### Q22: IP = 157.157.100.90, mask = 255.255.224.0

Same questions as Q21. `224` = `1110 0000`, so there are 3 SID bits in the 3rd octet.

| Wanted | Subnet bits (n − 1) | Subnet ID | Host |
|--------|---------------------|-----------|------|
| 3rd host in 2nd subnet | `001` | `157.157.0010 0000.0` = `157.157.32.0` | **`157.157.32.3`** |
| 4th host in 3rd subnet | `010` | `157.157.0100 0000.0` = `157.157.64.0` | **`157.157.64.4`** |
| 1st host in 4th subnet | `011` | `157.157.0110 0000.0` = `157.157.96.0` | **`157.157.96.1`** (64 + 32 = 96) |

---

## Part 7: Which host in which subnet?

### Q23: Mask 255.255.255.224

**M** = `200.40.38.50`, **N** = `200.92.48.40`, **P** = `200.80.68.60`

`224` = `1110 0000`: 3 SID bits, 5 host bits. Split the last octet as `SID | HID`:

| Machine | Last octet | SID | Host bits | Host number |
|---------|-----------|-----|-----------|-------------|
| M | `001 10010` | `001` | `10010` | **18th host** |
| N | `001 01000` | `001` | `01000` | **8th host** |
| P | `001 11100` | `001` | `11100` | **28th host** |

### Q24: Mask 255.255.252.0

**M** = `157.157.40.50`, **N** = `157.157.48.40`, **P** = `157.157.80.60`

`252` = `1111 1100`, so there are 6 SID bits in the 3rd octet. The last 2 bits of the 3rd octet and the whole 4th octet are the host bits.

| Machine | 3rd octet | SID | Subnet | Host number |
|---------|-----------|-----|--------|-------------|
| M | `001010 00` | `001010` | `157.157.40.0` | **50th host** |
| N | `001100 00` | `001100` | `157.157.48.0` | **40th host** |
| P | `010100 00` | `010100` | `157.157.80.0` | **60th host** |

### Q25: Mask 255.252.0.0

**M** = `100.40.0.10`, **N** = `100.96.0.22`, **P** = `100.80.0.15`

`252` = `1111 1100`, so there are 6 SID bits in the 2nd octet.

| Machine | 2nd octet | SID | Subnet | Host number |
|---------|-----------|-----|--------|-------------|
| M | `001010 00` | `001010` | `100.40.0.0` | **10th host** |
| N | `011000 00` | `011000` | `100.96.0.0` | **22nd host** |
| P | `010100 00` | `010100` | `100.80.0.0` | **15th host** |

---

## Part 8: Choosing the right mask

### Q26: Class C with 7 subnets and 25 hosts per subnet. Which mask?

a) `255.255.255.224`  b) `255.255.255.44`  c) `255.255.255.63`  d) `255.255.255.112`

- 7 subnets needs **3 SID bits** (2³ = 8 ≥ 7).
- 25 hosts needs **5 HID bits** (2⁵ − 2 = 30 ≥ 25).
- So the last octet needs **three 1's and five 0's**.

| Option | Binary | 1's | 0's | Works? |
|--------|--------|-----|-----|--------|
| a) 224 | `1110 0000` | 3 | 5 | **Yes** |
| b) 44 | `0010 1100` | 3 | 5 | **Yes** (1's not together) |
| c) 63 | `0011 1111` | 6 | 2 | **No** (only 2 host bits) |
| d) 112 | `0111 0000` | 3 | 5 | **Yes** (1's not together) |

**Answer: a, b and d**

> **Note:** b and d only count as masks if the 1's are **allowed to be non-contiguous**. If the question requires contiguous 1's, only **a** works.

### Q27: Class B with 180 subnets and 200 hosts per subnet. Which mask?

a) `255.255.255.0`  b) `255.255.240.240`  c) `255.255.252.112`  d) `255.255.252.192`

- 180 subnets needs **8 SID bits** (2⁷ = 128 < 180, but 2⁸ = 256 ≥ 180).
- 200 hosts needs **8 HID bits** (2⁸ − 2 = 254 ≥ 200).
- So, in the 16 host-side bits, we need **eight 1's and eight 0's**.

| Option | Last 2 octets | 1's | 0's | Contiguous? | Works? |
|--------|---------------|-----|-----|-------------|--------|
| a) | `11111111.00000000` | 8 | 8 | Yes | **Yes** |
| b) | `11110000.11110000` | 8 | 8 | No | Only if non-contiguous is allowed |
| c) | `11111100.01110000` | 9 | 7 | No | **No** (only 7 host bits) |
| d) | `11111100.11000000` | 8 | 8 | No | Only if non-contiguous is allowed |

**Answer: a, b, d** (or just **a** if the 1's must be contiguous).

---

## Part 9: More practice

### Q28: IP = 172.168.42.58, mask = 255.255.252.0. Find the subnet ID and DBA

`252` = `1111 1100`, so there are 6 SID bits in the 3rd octet.

```
  0010 1010   (42)
AND
  1111 1100   (252)
= 0010 1000   (40)
```

- **Subnet ID = `172.168.40.0`**
- DBA: set all host bits to 1, so the 3rd octet becomes `0010 1011` = 43. **DBA = `172.168.43.255`**

### Q29: IP = 200.48.67.184, mask = 255.255.255.240. Find the last host

`240` = `1111 0000`, so SID = 4 bits. `184` = `1011 1000`. Look at the top 4 bits only: `1011`.

- Subnet ID = `1011 0000` = **`200.48.67.176`**
- DBA = `1011 1111` = `200.48.67.191`
- **Last host = `1011 1110` = `200.48.67.190`**

### Q30: Mask 255.255.255.224. Which is a last host?

a) `210.15.16.62`  b) `210.15.16.94`  c) `210.15.16.127`  d) `210.15.16.191`

`224` = `1110 0000`: 3 SID bits, 5 host bits. A last host has host bits `11110`.

| Option | Binary | Host bits | Result |
|--------|--------|-----------|--------|
| a) 62 | `001 11110` | `11110` | **Last host** |
| b) 94 | `010 11110` | `11110` | **Last host** |
| c) 127 | `011 11111` | `11111` | It's a DBA |
| d) 191 | `101 11111` | `11111` | It's a DBA |

**Answer: a and b**

### Q31: Class C network 204.204.204.0 with 3 subnets X, Y, Z

X needs **100** hosts, Y needs **50** hosts, Z needs **50** hosts. Find feasible subnet addresses and masks.

It's Class C, so the first three octets (`204.204.204`) are the NID. Only the last octet is split.

| Subnet | Hosts needed | Host bits | SID bits | Mask |
|--------|--------------|-----------|----------|------|
| X | 100 (2⁷ − 2 = 126 ≥ 100) | 7 | 1 | `255.255.255.128` |
| Y | 50 (2⁶ − 2 = 62 ≥ 50) | 6 | 2 | `255.255.255.192` |
| Z | 50 (2⁶ − 2 = 62 ≥ 50) | 6 | 2 | `255.255.255.192` |

On its own, each subnet could use these addresses:

- **X:** `204.204.204.0` or `204.204.204.128`
- **Y and Z:** `204.204.204.0`, `.64`, `.128` or `.192`

**One feasible allocation that fits all three at once:**

| Subnet | Subnet address | Mask | Usable hosts |
|--------|----------------|------|--------------|
| X | `204.204.204.0` | `255.255.255.128` | `.1` to `.126` |
| Y | `204.204.204.128` | `255.255.255.192` | `.129` to `.190` |
| Z | `204.204.204.192` | `255.255.255.192` | `.193` to `.254` |

> **IMPORTANT:** X takes up one whole half (0 to 127). So Y and Z **must fit in the other half**, which means only `.128` and `.192` work for them. They can't use `.0` or `.64`, because those overlap with X.

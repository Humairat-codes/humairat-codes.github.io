---
layout: post
title: "Subnetting Problems"
date: 2026-11-01
categories: [Computer Networks]
---

> **IMPORTANT:** Subnets are numbered **from 0** in the binary. So the **n-th subnet** is written as **(n − 1)** in binary. For example, the 8th subnet uses `7`.

---

## Problem 1: 64 subnets from 157.157.0.0

**Given:** IP address `157.157.0.0`, and we need **64 subnets**.

1. The first octet `157` is in the range 128 to 191, so this is a **Class B** address.
2. Class B has **16 bits for NID** and **16 bits for HID**.
3. 64 subnets = 2⁶, so we **borrow 6 bits** from the host ID.
4. That leaves **16 − 6 = 10 host bits**.
5. Hosts per subnet = 2¹⁰ − 2 = **1022**.
6. Total IP addresses per subnet = 2¹⁰ = **1024**.
7. Subnet mask = `255.255.252.0` (the 3rd octet is `11111100`).

The 3rd octet is split as `[6 subnet bits][2 host bits]`, and the 4th octet is all host bits.

- **Subnet ID:** all host bits are `0`
- **Direct broadcast address:** all host bits are `1`

**Find the 8th, 17th, 28th and 61st subnets:**

| Subnet | n − 1 | 6-bit binary | Subnet ID | Direct broadcast address |
|--------|-------|--------------|-----------|--------------------------|
| 8th | 7 | `000111` | `157.157.00011100.00000000` = `157.157.28.0` | `157.157.00011111.11111111` = `157.157.31.255` |
| 17th | 16 | `010000` | `157.157.01000000.00000000` = `157.157.64.0` | `157.157.01000011.11111111` = `157.157.67.255` |
| 28th | 27 | `011011` | `157.157.01101100.00000000` = `157.157.108.0` | `157.157.01101111.11111111` = `157.157.111.255` |
| 61st | 60 | `111100` | `157.157.11110000.00000000` = `157.157.240.0` | `157.157.11110011.11111111` = `157.157.243.255` |

---

## Practice question: 128 subnets on 10.0.0.0

Find the **11th, 23rd, 93rd and 110th** subnets for **128 subnets** on `10.0.0.0`.

**Setup:** `10` is in the range 1 to 126, so this is **Class A** (8 NID bits, 24 HID bits). 128 subnets = 2⁷, so we **borrow 7 bits**. The 2nd octet is split as `[7 subnet bits][1 host bit]`, and the subnet mask is `255.254.0.0`.

| Subnet | n − 1 | 7-bit binary | Subnet ID | Direct broadcast address |
|--------|-------|--------------|-----------|--------------------------|
| 11th | 10 | `0001010` | `10.00010100.0.0` = `10.20.0.0` | `10.00010101.255.255` = `10.21.255.255` |
| 23rd | 22 | `0010110` | `10.00101100.0.0` = `10.44.0.0` | `10.00101101.255.255` = `10.45.255.255` |
| 93rd | 92 | `1011100` | `10.10111000.0.0` = `10.184.0.0` | `10.10111001.255.255` = `10.185.255.255` |
| 110th | 109 | `1101101` | `10.11011010.0.0` = `10.218.0.0` | `10.11011011.255.255` = `10.219.255.255` |

---

## Subnet mask

A **subnet mask** is 32 bits. It shows how many bits are borrowed from the host ID, and where they are, using two rules:

- **Rule 1:** the number of **1's** in the subnet mask = **NID + SID**
- **Rule 2:** the number of **0's** in the subnet mask = **HID**

### Default subnet masks

"Default" means **no bits are borrowed** (SID = 0), so the mask only shows the NID. All NID bits are 1 and all host bits are 0.

| Class | Default mask | NID + SID | SID |
|-------|--------------|-----------|-----|
| A | `255.0.0.0` | 8 | 0 |
| B | `255.255.0.0` | 16 | 0 |
| C | `255.255.255.0` | 24 | 0 |

---

## Example 1: mask 255.255.255.192

**Given:** NID = `200.200.200.0`, subnet mask = `255.255.255.192`

1. `192` = `11000000`, so the mask is `255.255.255.11000000`.
2. Number of 1's = **26**, so NID + SID = 26.
3. 24 + SID = 26, so **SID = 2 bits**.
4. Number of subnets = 2² = **4**.
5. Number of 0's = **6**, so HID = 6 bits.
6. Hosts per subnet = 2⁶ − 2 = 64 − 2 = **62**.

Write the last octet as `[SID][HID]` to get the subnet IDs:

| Subnet bits | Last octet | Subnet ID |
|-------------|------------|-----------|
| `00` | `00 000000` | `200.200.200.0` |
| `01` | `01 000000` | `200.200.200.64` |
| `10` | `10 000000` | `200.200.200.128` |
| `11` | `11 000000` | `200.200.200.192` |

**Shortcut:** write the **weights** of the subnet bits (**128, 64**). Each subnet ID is the sum of the weights where the bit is 1.

| Bits | Subnet ID (last octet) |
|------|------------------------|
| `00` | 0 |
| `01` | 64 |
| `10` | 128 |
| `11` | 192 |

---

## Example 2: mask 255.255.255.224

**Given:** NID = `200.200.200.0`, subnet mask = `255.255.255.224`

1. Class C, so **24 bits for NID** and **8 bits for HID**.
2. `224` = `111 00000`, so the mask is `11111111.11111111.11111111.11100000`.
3. Number of 1's = **27**, so NID + SID = 27.
4. 24 + SID = 27, so **SID = 3**. That means 3 bits are borrowed from the host ID.
5. Number of subnets = 2³ = **8**.
6. HID = 8 − 3 = 5 bits, so hosts per subnet = 2⁵ − 2 = **30**.

**Shortcut:** weights are **128, 64, 32**.

| Bits | Subnet ID |
|------|-----------|
| `000` | `200.200.200.0` |
| `001` | `200.200.200.32` |
| `010` | `200.200.200.64` |
| `011` | `200.200.200.96` |
| `100` | `200.200.200.128` |
| `101` | `200.200.200.160` |
| `110` | `200.200.200.192` |
| `111` | `200.200.200.224` |

---

## Example 3: a mask with scattered 1's (255.255.255.44)

> **Note:** Normally the 1's in a mask are all together on the left. In this mask the 1's are **scattered** (`00101100`). This is called a **non-contiguous mask**. Exam questions still ask about it, but real networks today don't use it.

**Given:** NID = `200.200.200.0`, subnet mask = `255.255.255.44`

1. Class C, so NID = 24 bits.
2. `44` = `00101100`, so the mask is `255.255.255.00101100`.
3. Number of 1's = 27, so NID + SID = 27.
4. 24 + SID = 27, so **SID = 3**. That means 3 bits are borrowed from the host ID.
5. Number of subnets = 2³ = **8**.
6. HID = 8 − 3 = 5 bits, so hosts per subnet = 2⁵ − 2 = **30**.

The subnet bits sit where the mask has 1's, so the weights are **32, 8, 4**.

| Bits | Subnet ID |
|------|-----------|
| `000` | 0 → `200.200.200.0` |
| `001` | 4 → `200.200.200.4` |
| `010` | 8 → `200.200.200.8` |
| `011` | 12 → `200.200.200.12` |
| `100` | 32 → `200.200.200.32` |
| `101` | 36 → `200.200.200.36` |
| `110` | 40 → `200.200.200.40` |
| `111` | 44 → `200.200.200.44` |

---

## Finding hosts and masks

### Maximum hosts per subnet from a mask

**Question:** In a Class B network, the subnet mask is `255.255.240.0`. What is the maximum number of hosts per subnet?

1. `240` = `1111 0000`, so the mask is `255.255.11110000.0`.
2. Class B has 16 bits for NID.
3. Number of 1's = 20, so NID + SID = 20.
4. 16 + SID = 20, so **SID = 4** and the number of subnets = 2⁴ = **16**.
5. HID = 16 − 4 = **12 bits**.
6. Hosts per subnet = 2¹² − 2 = 4096 − 2 = **4094**.

### Mask from the number of subnets

**Question:** An organization has a Class B network and forms **64 departments**. What is the subnet mask?

1. Class B default mask = `255.255.0.0`.
2. 64 subnets = 2⁶, so **6 bits** are borrowed from the host.
3. The mask is `255.255.11111100.0` = **`255.255.252.0`**.

### Hosts per subnet if n bits are borrowed

**Question:** The default subnet mask is `255.255.255.0`. How many hosts per subnet are possible if **n bits** are borrowed from the host ID?

- The default mask `255.255.255.0` means **Class C**, so HID = 8 bits.
- If we take away n bits, the host bits become **8 − n**.
- **Hosts per subnet = 2^(8 − n) − 2**

### Mask from the number of hosts per LAN

A university has a Class B network. Find the subnet mask if each LAN needs:

| Hosts per LAN | Host bits needed | Check | Bits borrowed | Subnet mask |
|---------------|------------------|-------|---------------|-------------|
| 100 | 7 (`1100100`) | 2⁷ − 2 = 126 ≥ 100 | 16 − 7 = **9** | `255.255.255.128` |
| 150 | 8 (`10010100`) | 2⁸ − 2 = 254 ≥ 150 | 16 − 8 = **8** | `255.255.255.0` |

**How it works:**

- Class B has **16 host bits** by default (`00000000.00000000`).
- Write the number of hosts in binary to see how many host bits you need.
- Borrowed bits = 16 − (host bits needed).
- For **100 hosts**, 9 bits are borrowed: 8 from the 3rd octet and 1 from the 4th. The last octet becomes `10000000` = 128.
- For **150 hosts**, exactly 8 bits are borrowed, so the whole 3rd octet is used.

> **Tip:** Always do the check `2^h − 2 ≥ hosts`. The binary length alone can mislead you when the number of hosts is just below a power of 2.

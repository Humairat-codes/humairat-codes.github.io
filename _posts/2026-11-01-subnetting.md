---
layout: post
title: "Subnetting: 8 Subnets Example"
date: 2026-11-01
categories: [Computer Networks]
---

## What is subnetting?

**Subnetting** is the process of **borrowing bits from the Host ID** to generate the **Subnet ID**.

The number of bits borrowed depends on the requirement. For example, if you need **16 subnets**, you borrow **4 bits** from the host ID (2⁴ = 16).

---

## Example: divide 200.200.200.0 into 8 subnets

Given: `IP = 200.200.200.0` (Class C)

1. We need 8 subnets, so we borrow **3 bits** from the host part (2³ = **8 subnets**).
2. Class C has **8 host bits**. Borrowing 3 leaves **5 host bits**.
3. Hosts per subnet = 2⁵ − 2 = 32 − 2 = **30 usable hosts**.
4. The new subnet mask is `255.255.255.224`, since the last octet is `11100000`.

> **IMPORTANT:** Usable hosts per subnet is **30**, but the **total IP addresses per subnet is still 2⁵ = 32**. The 2 extra addresses are the **subnet ID** and the **direct broadcast address**, so they can't be given to hosts.

---

## All 8 subnets

The last octet is split as `[subnet ID: 3 bits][host ID: 5 bits]`.

| Subnet | Subnet bits | Subnet ID (all host bits 0) | Direct broadcast address (all host bits 1) |
|--------|-------------|-----------------------------|--------------------------------------------|
| 1st | `000` | `200.200.200.000 00000` → `200.200.200.0` | `200.200.200.000 11111` → `200.200.200.31` |
| 2nd | `001` | `200.200.200.001 00000` → `200.200.200.32` | `200.200.200.001 11111` → `200.200.200.63` |
| 3rd | `010` | `200.200.200.010 00000` → `200.200.200.64` | `200.200.200.010 11111` → `200.200.200.95` |
| 4th | `011` | `200.200.200.011 00000` → `200.200.200.96` | `200.200.200.011 11111` → `200.200.200.127` |
| 5th | `100` | `200.200.200.100 00000` → `200.200.200.128` | `200.200.200.100 11111` → `200.200.200.159` |
| 6th | `101` | `200.200.200.101 00000` → `200.200.200.160` | `200.200.200.101 11111` → `200.200.200.191` |
| 7th | `110` | `200.200.200.110 00000` → `200.200.200.192` | `200.200.200.110 11111` → `200.200.200.223` |
| 8th | `111` | `200.200.200.111 00000` → `200.200.200.224` | `200.200.200.111 11111` → `200.200.200.255` |

> **Pattern:** each subnet starts **32 higher** than the previous one (0, 32, 64, 96, 128, 160, 192, 224). That's the block size, 2⁵ = 32.

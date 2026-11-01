---
layout: post
title: "Subnetting"
date: 2026-11-01
categories: [Computer Networks]
---

**Subnetting** is the process of borrowing bits from the host portion of an IP address to generate a subnet ID. The number of bits borrowed depends on your network requirements (e.g., if you need 16 subnets, you borrow 4 bits from the host ID).

---

## Example Problem

* **Given IP:** `200.200.200.0`
* **Goal:** Divide the network into **8 subnets**.

### Calculations
1. **Determine borrowed bits:** To get 8 subnets, we borrow $2^3 = 8$, so we borrow **3 bits** from the host portion.
2. **Determine host bits:** Since it is a Class C address, the standard host portion is 8 bits. Borrowing 3 bits leaves us with $8 - 3 =$ **5 host bits**.
3. **Calculate hosts per subnet:** 
   * **Valid Hosts:** $2^5 - 2 = 32 - 2 =$ **30 usable hosts** per subnet.
   * **Total IP Addresses:** $2^5 =$ **32 addresses** per subnet (including the Subnet ID and Direct Broadcast Address).

---

## Subnet Breakdown

Taking 3 bits gives us 8 possible binary combinations ($000$ to $111$). Below is the detailed breakdown for each subnet:

| Subnet | Binary Prefix | Subnet ID | Direct Broadcast Address | Valid Host Range |
| :--- | :--- | :--- | :--- | :--- |
| **1st** | `000` | `200.200.200.0` | `200.200.200.31` | `200.200.200.1` – `200.200.200.30` |
| **2nd** | `001` | `200.200.200.32` | `200.200.200.63` | `200.200.200.33` – `200.200.200.62` |
| **3rd** | `010` | `200.200.200.64` | `200.200.200.95` | `200.200.200.65` – `200.200.200.94` |
| **4th** | `011` | `200.200.200.96` | `200.200.200.127` | `200.200.200.97` – `200.200.200.126` |
| **5th** | `100` | `200.200.200.128` | `200.200.200.159` | `200.200.200.129` – `200.200.200.158` |
| **6th** | `101` | `200.200.200.160` | `200.200.200.191` | `200.200.200.161` – `200.200.200.190` |
| **7th** | `110` | `200.200.200.192` | `200.200.200.223` | `200.200.200.193` – `200.200.200.222` |
| **8th** | `111` | `200.200.200.224` | `200.200.200.255` | `200.200.200.225` – `200.200.200.254` |

### Binary Mapping Reference
```text
1st subnet (000): 200.200.200.000 00000 (ID) to 200.200.200.000 11111 (Broadcast)
2nd subnet (001): 200.200.200.001 00000 (ID) to 200.200.200.001 11111 (Broadcast)
3rd subnet (010): 200.200.200.010 00000 (ID) to 200.200.200.010 11111 (Broadcast)
4th subnet (011): 200.200.200.011 00000 (ID) to 200.200.200.011 11111 (Broadcast)
5th subnet (100): 200.200.200.100 00000 (ID) to 200.200.200.100 11111 (Broadcast)
6th subnet (101): 200.200.200.101 00000 (ID) to 200.200.200.101 11111 (Broadcast)
7th subnet (110): 200.200.200.110 00000 (ID) to 200.200.200.110 11111 (Broadcast)
8th subnet (111): 200.200.200.111 00000 (ID) to 200.200.200.111 11111 (Broadcast)

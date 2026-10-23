---
layout: post
title: "Types of Communication"
date: 2026-10-22
categories: [Computer Networks]
---

## Overview

1. **Unicasting:** transmission of data packets from **one sender to one receiver**, in the same or different networks.
2. **Broadcasting:** transmission of data from **one source to all hosts**, in the same or different networks.
3. **Multicasting:** transmission of data from **one host to a selected group of hosts** (one to many).

---

## Broadcasting

Depending on whether the broadcast stays in the same network or reaches a different one, broadcasting is divided into two types:

- **Limited broadcasting:** "one to all" transmission happens in the **same** network (hence the name *limited*).
- **Direct broadcasting:** "one to all" transmission happens in a **different** network.

### Limited vs direct broadcast address

Take a Class A network with the address `10.0.0.0`.

- **Limited broadcast address:** `255.255.255.255`
- **Direct broadcast address:** `10.255.255.255`

If somebody on **another** network wants to broadcast data to this network, they put `10.255.255.255` in the **destination IP address**.

> **IMPORTANT:** `255.255.255.255` can **NEVER** be a source IP address. It is the limited broadcast address for **ALL classes and ALL networks**. It doesn't matter whether the network address is `13.0.0.0`, `13.56.0.0` or `19.143.99.0`. For all of them, the limited broadcast address is `255.255.255.255`.

### Example: broadcasting from one network to another

Say network **P** is `10.0.0.0` and network **Q** is `113.0.0.0`. A host in P (`10.23.8.9`) wants to send data to **all hosts in Q**.

| Field | Value |
|-------|-------|
| Source IP address | `10.23.8.9` |
| Destination IP address | `113.255.255.255` |

> **IMPORTANT:** `113.255.255.255` (a direct broadcast address) can **NEVER** be a source IP address either.

---

## Special addresses in classful IPv4

| NID bits | HID bits | Meaning |
|----------|----------|---------|
| Valid | All 0's | Network IP address |
| Valid | All 1's | Direct broadcast IP address |
| All 1's | All 1's | Limited broadcast IP address |

### Examples

| IP address | Class | Network IP | Direct broadcast address | Limited broadcast address |
|------------|-------|------------|--------------------------|---------------------------|
| `19.35.21.31` | A | `19.0.0.0` | `19.255.255.255` | `255.255.255.255` |
| `119.31.34.2` | A | `119.0.0.0` | `119.255.255.255` | `255.255.255.255` |
| `150.0.94.31` | B | `150.0.0.0` | `150.0.255.255` | `255.255.255.255` |
| `190.34.17.31` | B | `190.34.0.0` | `190.34.255.255` | `255.255.255.255` |
| `200.200.34.92` | C | `200.200.34.0` | `200.200.34.255` | `255.255.255.255` |
| `217.39.47.9` | C | `217.39.47.0` | `217.39.47.255` | `255.255.255.255` |
| `226.9.7.97` | D | N/A | N/A | N/A |
| `243.2.3.5` | E | N/A | N/A | N/A |

---

## Multicasting

Multicasting is the transmission of data from **one host to a selected group of hosts** (one to many).

In classful addressing, **Class D** (`224.0.0.0` to `239.255.255.255`) is used for multicasting.

---
layout: post
title: "Network Mask"
date: 2026-10-22
categories: [Computer Networks]
---

## What is a network mask?

A **network mask** tells you which portion of the address is the **Network ID (NID)** and which portion is the **Host ID (HID)**.

- In the mask, **NID bits = all 1's** and **HID bits = all 0's**.
- The number of **1's** shows the NID part, and the number of **0's** shows the host ID part.

---

## Default (natural) masks

| Class | NID bits | Mask in binary | Mask in dotted decimal |
|-------|----------|----------------|------------------------|
| A | 8 | `11111111.00000000.00000000.00000000` | `255.0.0.0` |
| B | 16 | `11111111.11111111.00000000.00000000` | `255.255.0.0` |
| C | 24 | `11111111.11111111.11111111.00000000` | `255.255.255.0` |

The default mask can be **ANDed** with an IP address to give the **network address**.

---

## Finding the network address

**Example:** IP address `200.200.200.96`

The first octet is `200`, which is in the range 192 to 223, so this is a **Class C** address. The network mask is `255.255.255.0`.

### Method 1: Bitwise AND

```
  1100 1000 . 1100 1000 . 1100 1000 . 0110 0000     (200.200.200.96)
AND
  1111 1111 . 1111 1111 . 1111 1111 . 0000 0000     (255.255.255.0)
---------------------------------------------------
= 1100 1000 . 1100 1000 . 1100 1000 . 0000 0000     (200.200.200.0)
```

### Method 2: AND in decimal

```
  200.200.200.96
AND
  255.255.255.0
= 200.200.200.0
```

The rules that make this work:

- `255` is all 1's, and `1 AND x = x`, so the octet stays the same.
- `0 AND x = 0`, so the octet becomes `0`.

### Method 3: Shortcut (no AND needed)

For classful addressing you can find the class from the **first octet** and read off the network address directly.

| Class | First octet range |
|-------|-------------------|
| A | 1 to 126 |
| B | 128 to 191 |
| C | 192 to 223 |
| D | 224 to 239 |
| E | 240 to 255 |

1. `200.200.200.96` has first octet `200`, which is in the range 192 to 223, so it is **Class C**.
2. Class C uses **24 bits** for the network, so the first three octets are the NID.
3. The network address is **`200.200.200.0`**.

> **Tip:** For classful addressing you don't need to perform the AND at all. Use the first octet and the range.

---

## Practice questions

### Question 1

What is `192.192.192.255`?

- It is in the range 192 to 223, so it's **Class C**.
- The host bits (last octet) are `255`, which is **all 1's**.
- **Answer:** it is a **direct broadcast address**.

### Question 2

A host with IP address `200.187.96.0` sends a message to a host with IP address `205.54.83.97`. What destination IP address does the source attach?

Your first instinct might be `205.54.83.97`. **That's wrong!**

Look at the source address, `200.187.96.0`:

- It is a Class C address.
- The host bits (last octet) are **all 0's**.
- So it is the **network IP address**, not a host address.

> **Answer: NOT POSSIBLE.** A network IP address can **NEVER** be assigned to any host, so this host can't exist as a sender.

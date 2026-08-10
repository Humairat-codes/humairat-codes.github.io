---
layout: post
title: "Probability Basics & The Inclusion-Exclusion Principle"
date: 2026-08-10
categories: [Mathematics, Computer-Science]
---

# What is Probability?

**Probability** is the likelihood of an event occurring based on a given sample space.

If the probability of an event is **equally likely** for all outcomes in the sample space:

> **P(A) = (Number of outcomes where A occurs) / (Total size of sample space)**

---

## The 3 Axioms of Probability

1. **Non-negativity:** P(A) ≥ 0  
   *(Probability can never be negative)*
2. **Normalization:** P(S) = 1  
   *(The probability of the entire sample space occurring is always 1)*
3. **Additivity:** If A and B are **mutually exclusive** events:  
   **P(A ∪ B) = P(A) + P(B)**

---

## Inclusion-Exclusion Principle

The **Inclusion-Exclusion Principle** is a method used to avoid double-counting when events or sets overlap.

For any two overlapping events A and B:

> **P(A ∪ B) = P(A) + P(B) - P(A ∩ B)**

---

### Worked Example: Rolling a Die

* **Sample Space (S):** {1, 2, 3, 4, 5, 6}
* **Event A (Getting an odd number):** {1, 3, 5} → P(A) = 3/6
* **Event B (Getting a number > 2):** {3, 4, 5, 6} → P(B) = 4/6

Notice that {3, 5} overlap! 

* **Intersection A ∩ B:** {3, 5} → P(A ∩ B) = 2/6

#### Applying the Formula:

P(A ∪ B) = P(A) + P(B) - P(A ∩ B)  
P(A ∪ B) = 3/6 + 4/6 - 2/6 = (3 + 4 - 2) / 6 = **5/6**

**Verification:**  
A ∪ B = {1, 3, 4, 5, 6}, which contains 5 out of 6 outcomes → **5/6**. The formula works!

---

### Worked Examples(1997 PYQ)

**The probability that it will rain today is 0.5. The probability that it will rain tomorrow is 0.6. The probability that it will rain today or tomorrow is 0.7. What is the probability that it will rain today and tomorrow?**

Let O = it will rain today
Let W = it will rain tomorrow 
given, P(O) = 0.5, P(W)= 0.6, P(O U W) = 0.7 
#### we know that P(A U B) = P(A) + P(B) - P(A n B)
so, P(O n W) = P(O) + P(W) - P(O U W) = 0.5 + 0.6 - 0.7 = 0.4
### ans = 0.4

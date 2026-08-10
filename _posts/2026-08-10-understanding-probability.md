---
layout: post
title: "Probability Basics & The Inclusion-Exclusion Principle"
date: 2026-08-10
categories: [Mathematics, Computer-Science]
---

# What is Probability?

**Probability** is the likelihood of an event occurring based on a given sample space.

If the probability of an event is **equally likely** for all outcomes in the sample space:

$$P(A) = \frac{\text{Number of outcomes where } A \text{ occurs}}{\text{Total size of sample space}}$$

---

## The 3 Axioms of Probability

1. **Non-negativity:** $P(A) \ge 0$  
   *(Probability can never be negative)*
2. **Normalization:** $P(S) = 1$  
   *(The probability of the entire sample space occurring is always 1)*
3. **Additivity:** If $A$ and $B$ are **mutually exclusive** events:  
   $$P(A \cup B) = P(A) + P(B)$$

---

## Inclusion-Exclusion Principle

The **Inclusion-Exclusion Principle** is a method used to avoid double-counting when events or sets overlap.

For any two overlapping events $A$ and $B$:

$$P(A \cup B) = P(A) + P(B) - P(A \cap B)$$

---

### Worked Example: Rolling a Die

* **Sample Space ($S$):** $\{1, 2, 3, 4, 5, 6\}$
* **Event $A$ (Getting an odd number):** $\{1, 3, 5\} \rightarrow P(A) = \frac{3}{6}$
* **Event $B$ (Getting a number $> 2$):** $\{3, 4, 5, 6\} \rightarrow P(B) = \frac{4}{6}$

Notice that $\{3, 5\}$ overlap! 

* **Intersection $A \cap B$:** $\{3, 5\} \rightarrow P(A \cap B) = \frac{2}{6}$

#### Applying the Formula:

$$P(A \cup B) = P(A) + P(B) - P(A \cap B)$$
$$P(A \cup B) = \frac{3}{6} + \frac{4}{6} - \frac{2}{6} = \frac{3 + 4 - 2}{6} = \frac{5}{6}$$

**Verification:**  
$A \cup B = \{1, 3, 4, 5, 6\}$, which contains $5$ out of $6$ outcomes $\rightarrow \frac{5}{6}$. The formula works!

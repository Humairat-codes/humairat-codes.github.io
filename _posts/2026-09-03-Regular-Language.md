---
layout: post
title: "Regular Languages Introduction"
date: 2026-09-03
categories: [Theory of Computation]
---

---

layout: post
title: "Regular Languages Introduction"
date: 2026-09-03
categories: [Theory of Computation]
-----------------------------------

# REGULAR LANGUAGES

## A language is **regular if and only if** it is recognized by a Finite State Machine (FSM).

---

## What languages are not regular?

Languages that **cannot be recognized by a Finite State Machine** are called **non-regular languages**.

An FSM has **finite memory**. It cannot remember an **unbounded amount of information**, such as:

* An arbitrarily large count
* An arbitrarily long string
* Information that needs to be compared later without a fixed limit

### Example 1

Consider:

$$
L = \{ww \mid w \in \{a,b\}^*\}
$$

For example, if $w = ab$, then:

$$
ww = abab
$$

This language is **not regular** because an FSM would need to remember an arbitrarily long string $w$ and compare it with the following string.

### Example 2

Consider:

$$
L = \{a^n b^n \mid n \geq 0\}
$$

Examples:

```text
ab
aabb
aaabbb
aaaabbbb
```

This language is **not regular** because an FSM cannot keep track of an arbitrarily large number of $a$'s and ensure that exactly the same number of $b$'s follows.

---

# OPERATIONS ON REGULAR LANGUAGES

## 1. UNION

$$
A \cup B = \{x \mid x \in A \text{ or } x \in B\}
$$

## 2. CONCATENATION

$$
A \cdot B = \{xy \mid x \in A \text{ and } y \in B\}
$$

## 3. KLEENE STAR

$$
A^* = \{x_1x_2x_3\ldots x_k \mid k \geq 0 \text{ and each } x_i \in A\}
$$

---

## Example

Let:

$$
A = \{pq, r\}
$$

and

$$
B = \{t, uv\}
$$

### 1. UNION

$$
A \cup B = \{pq, r, t, uv\}
$$

### 2. CONCATENATION

$$
A \cdot B = \{pqt, pquv, rt, ruv\}
$$

### 3. KLEENE STAR

$$
A^* = \{\epsilon, pq, r, pqpq, pqr, rpq, rr, pqpqpq, pqrr, \ldots\}
$$

> $\epsilon$ is included because we can concatenate **zero strings** from $A$.

---

# CLOSURE PROPERTIES

## THEOREM 1: Closure under UNION

The class of regular languages is closed under **union**.

### In simple terms:

If $A$ and $B$ are regular languages, then:

$$
A \cup B
$$

is also a regular language.

---

## THEOREM 2: Closure under CONCATENATION

The class of regular languages is closed under **concatenation**.

### In simple terms:

If $A$ and $B$ are regular languages, then:

$$
A \cdot B
$$

is also a regular language.

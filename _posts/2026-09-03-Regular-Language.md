---
layout: post
title: "Regular Languages Introduction"
date: 2026-09-03
categories: [Theory of Computation]
---

# REGULAR LANGUAGES

## A language is **regular if and only if** it is recognized by a Finite State Machine (FSM).

---

## What languages are not regular?

Languages that **cannot be recognized by a Finite State Machine** are called **non-regular languages**.

An FSM has **finite memory**. It cannot remember an **unbounded amount of information**, such as:

- An arbitrarily large count
- An arbitrarily long string
- Information that needs to be compared later without a fixed limit

### Example 1

Consider:

**L = {ww | w ∈ {a,b}*}**

For example, if **w = ab**, then:

**ww = abab**

This language is **not regular** because an FSM would need to remember an arbitrarily long string **w** and compare it with the following string.

---

### Example 2

Consider:

**L = {aⁿbⁿ | n ≥ 0}**

Examples:

    ab
    aabb
    aaabbb
    aaaabbbb

This language is **not regular** because an FSM cannot keep track of an arbitrarily large number of **a's** and ensure that exactly the same number of **b's** follows.

---

# OPERATIONS ON REGULAR LANGUAGES

## 1. UNION

**A ∪ B = {x | x ∈ A or x ∈ B}**

---

## 2. CONCATENATION

**A · B = {xy | x ∈ A and y ∈ B}**

---

## 3. KLEENE STAR

**A* = {x₁x₂x₃...xₖ | k ≥ 0 and each xᵢ ∈ A}**

---

## Example

Let:

**A = {pq, r}**

**B = {t, uv}**

### 1. UNION

**A ∪ B = {pq, r, t, uv}**

### 2. CONCATENATION

**A · B = {pqt, pquv, rt, ruv}**

### 3. KLEENE STAR

**A* = {ε, pq, r, pqpq, pqr, rpq, rr, pqpqpq, pqrr, ...}**

> **ε** is included because we can concatenate **zero strings** from A.

---

# CLOSURE PROPERTIES

## THEOREM 1: Closure under UNION

The class of regular languages is closed under **union**.

### In simple terms:

If **A** and **B** are regular languages, then **A ∪ B** is also a regular language.

---

## THEOREM 2: Closure under CONCATENATION

The class of regular languages is closed under **concatenation**.

### In simple terms:

If **A** and **B** are regular languages, then **A · B** is also a regular language.

---
layout: post
title: "DFA examples"
date: 2026-09-03
categories: [Theory of Computation]
---

for reference - (Q,Σ,Q0,F,δ)

## How to design a deterministic Finite Automata
### Example 1 - strings that start with 0 
- Say, L1 = set of all strings that start with 0 
- Σ = {0,1}
- L1 = {0,00,01,011,010,0001,01010....}
![DFA1](/assets/DFA1EG.png)

---

### Example 2 - sets of strings of length 2
- Construct DFA that accepts set of all strings over {0,1} of length 2.
- Σ = {0,1}
- L = {00,01,10,11}

![DFA2](/assets/DFA2EG.png)

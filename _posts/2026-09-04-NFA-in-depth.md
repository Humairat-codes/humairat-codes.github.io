---
layout: post
title: "NFA Formal Definition and Examples"
date: 2026-09-04
categories: [Theory of Computation]
---
![NFA](/assets/NFA1.png)
---
## Formal Definition of NFA - (Q,Σ,q0,F,δ)
### from above figure, we can see
- Q = {A,B}
- Σ = {0,1}
- q0 = A
- F = {B}
- δ = Q X Σ --> 2^{Q}

---

### HOW δ = Q X Σ --> 2^{Q} ?
Look carefully, 
- A X 0 --> A
- A X 0 --> B
- A X 1 --> A
- B X 0 --> Φ
- B X 1 --> Φ

---

From here, we can see that
1. A -> A,B,AB,Φ
2. This means from start state on any input, we can transition to 4 states.
3. Given number of states |Q| = 2
4. Thus, total transitions become 2^{Q}

---


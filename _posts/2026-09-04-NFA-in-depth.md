---
layout: post
title: "NFA Formal Definition and Examples"
date: 2026-09-04
categories: [Theory of Computation]
---
![NFAEG1](/assets/NFAEG1.png)
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

### L = {set of all strings that start with 0}
eg : {0,00,001,0010,01}
---
![NFAEG1](/assets/NFAEG1.png)
---
- (Q,Σ,q0,F,δ)
- Q = {A,B}
- Σ = {0,1}
- q0 = A
- F = {B}
- We can see that A state has a next state Φ on input '1' and that is completely okay! because it is an NFA.

---

### set of all strings over 0,1 of length 2
L = {00,01,10,11}

![NFAEG2](/assets/NFAEG2.png)

---

### construct NFA for strings that ends with '1'
L= {01,001,1001,1111100001101011......}

![NFAEG3](/assets/NFAEG3.png)

---

### set of all strings that contains 0
![NFAEG4](/assets/NFAEG4.png)



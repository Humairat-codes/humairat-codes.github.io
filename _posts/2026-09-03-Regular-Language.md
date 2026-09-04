---
layout: post
title: "Regular Languages Introduction"
date: 2026-09-03
categories: [Theory of Computation]
---

# REGULAR LANGUAGES
## A language is Regular iff it is recognized by a finite state machine(FSM)

---

### - Then what languages are not Regular? Those that are not recognized by FSM, and Require MEMORY(Remember : DFA or FSM have very limited memory. It can not store or count strings)
Eg1 - ababbbababb (look ate the patter: ababb is repeated!) - Can not be designed using FSM so it is not a regular language
Eg2 - a^{n} b^{n} - aaaabbbb but it can not be designed by FSM because an FSM can not keep track of the count of a's and b's.

---

## OPERATIONS on REGULAR LANGUAGE
### 1.UNION - A U B = {x | x ∈ OR x ∈ B}
### 2. CONCATENATION - A . B = {xy | x ∈ A AND y ∈ B}
### 3. STAR - A* = {x1 x2 x3 ... xk| k>=0 and each xi ∈ A}
---
Eg A= {pq,r}, B ={t,uv}
1. A U B = {pq,r,t,uv}
2. A.B = {pqt,pquv,rt,ruv}
3. A* = {ɛ,pq,r,pqr,rpq,pqpq,rr,pqpqpq,pqrr,......}
---
## THEOREM 1 : The class of Regular Languages is closed under UNION
### In simple terms - A U B is regular language if A,B are regular languages
## THEOREM 2 : The class of Regular Languages is closed under CONCATENATION
### In simple terms - A . B is regular language if A,B are regular languages

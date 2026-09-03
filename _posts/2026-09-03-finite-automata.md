---
layout: post
title: "Finite Automata"
date: 2026-09-03
categories: [Theory of Computation]
---

Finite state machines - 2 categories
FA with output - Moore Machine, Mealy machine
FA without output - DFA, NFA, ɛ-NFA

## DFA
DFA - deterministic Finite Automata
- simplest model of computation
- contains a very limited memory
---
![DFA](/assets/FA1.png)
the figure looks weird but focus on concept :D

Here A is initial state/starting state. Look at the arrow
D is Final state. Look at the double circles over it. 

# Formal definition of DFA is (Q,Σ,Q0,F,δ)
Q = set of all states
Σ = set of symbols or the Alphabet
Q0 = Initial state
F = set of final states
δ = transition function that maps from Q X Σ -> Q

From above figure, 
Q = {A,B,C,D}
Σ = {0,1}
Q0 = A
F = {D}
δ is transition function  

| **Current State** | **Input `0`** | **Input `1`** |
| ----------------- | ------------- | ------------- |
| **→ A**           | C             | B             |
| **B**             | D             | A             |
| **C**             | A             | D             |
| **★ D**           | B             | C             |





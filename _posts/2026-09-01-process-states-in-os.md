---
layout: post
title: "Process States in OS"
date: 2026-09-01
categories: [Operating Systems]
---

**Process** — It is a program under execution.

In operating systems, there are two main types of scheduling:

### 1. Preemptive Multiprogramming OS
A process dispatched to the CPU can be preempted by the OS to go back to main memory in order to execute or dispatch another process of higher priority.

### 2. Non-Preemptive Multiprogramming OS
A process under execution, regardless of priority or time consumed, remains under execution until it is terminated.

---

## Process States in Preemptive Multiprogrammed OS
![Process States Diagram](/assets/processstates.png)

## Process States in Non-Preemptive Multiprogrammed OS
![Process States Diagram](/assets/nonps.png)

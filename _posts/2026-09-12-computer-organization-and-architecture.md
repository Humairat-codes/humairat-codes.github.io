---
layout: post
title: "Computer Organization and Architecture: Core Concepts & CPU Design"
date: 2026-09-12 10:00:00 +0530
categories: [Computer Science, Architecture]
tags: [coa, cpu, memory-hierarchy, instruction-set]
description: "A comprehensive guide to Computer Organization and Architecture covering CPU structure, bus systems, memory hierarchies, and instruction cycles."
toc: true
---

# Computer Organization and Architecture

## 1. Overview & Difference
**Computer Architecture:** Defines *what* the system does (instruction set architecture, addressing modes, data types visible to the programmer).
**Computer Organization:** Defines *how* the system implements it (hardware details, control signals, memory technology, interface implementations).

## 2. DATA FORMATS
In coa, we study 2 types of data 
* Numberic
* Characters
**Numberic** - represents the numerical values in binary form (base-2, represented by 0 and 1)
It is subdivided into 2 categories :
* Integer/Fixed point numbers
* Floating point numbers
### Integer/Fixed-Point - used to represent whole numbers 
* unsigned : represents non negative numbers (0 to 2^n -1)
* signed : represents POSITIVE and NEGATIVE values using SIGNED MAGNITUDE, 1'S COMPLEMENT, 2'S COMPLEMENT
a) signed magnitude - it uses MSB for sign and n-1 bits for magnitude in binary : 
* 0 - positive sign
* 1 - negative sign 

eg : +5 represented by 0 101 (MSB IS 0 for positive)
-5 represented by 1 101 (MSB IS 1 for negative)
issue - contains +0 and -0 as 0 000 for +0 and 1 000 for -0 which is not necessary. wastes space.

b) 1's complement - positive numbers are represented normally in binary 
BUT negative numbers are represented by performing 1's cpmplement(invert 1 to 0 and 0 to 1)
eg : +5 is 0101
-5 is 1010 (just invert the bits in +5) 
not if you do 1's complement on -5, you'll get +5 as 0101.
issue : again, two ways to represent 0 as, +0 is 0000 and -0 is 1111. WASTES BIT SPACE.

c) 2's complement : positive numbers are represented normally,
BUT negative numbers are represented by 2's complement as take 1's  complement first and then add 1 to the result
Eg: +5 is 0101
-5 is :
* take 1's complement of +5 which is 1010
* Now, ADD 1 to 1's complement 1010 + 1 => 1011 is -5

*** Characters Data formats** : encodes alphanumeric characters and symbols into binary byte patterns
> Can be done using 2 ways
* ASCII  (7-8 bit) : American Standard code for Information Interchange
* EBCDIC (8 bits) : Extended binary coded decimal Interchange code
* Unicode (UTF-8) : for universal character sets

---

# Stored Program Architecture
### It is also called Von Neumann Architecture in which : 1. PROGRAM INSRTUCTIONS and 2. DATA are stored in the same MAIN MEMORY.

### Key Components
1. Central Processing Unit (CPU):

* Control Unit (CU): Fetches instructions from memory, decodes them, and manages signal execution.

* Arithmetic Logic Unit (ALU): Performs mathematical calculations and logical evaluations.

* Registers: High-speed temporary storage internal to the processor (e.g., Program Counter, Instruction Register, Accumulator).

2. Memory Unit: A unified main memory store (RAM) containing both read/write data and executable code instructions.

3. Input/Output (I/O) Interfaces: External devices used for data entry, storage interaction, and human readable output.




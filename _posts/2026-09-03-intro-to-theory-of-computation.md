### Important Theory of Computation Terms

1. **Symbol:** A single character or atom.  
   *Examples:* `0`, `1`, `a`, `b`

2. **Alphabet ($\Sigma$):** A finite, non-empty set of symbols.  
   *Examples:* $\Sigma = \{0, 1\}$, $\Sigma = \{a, b, c\}$

3. **String:** A finite sequence of symbols chosen from an alphabet.  
   *Examples:* If $\Sigma = \{a, b\}$, valid strings include `a`, `ab`, `ba`, `aabb`.

4. **Language ($L$):** Any set/subset of strings over a given alphabet $\Sigma$.  
   *Examples:* If $\Sigma = \{a, b\}$, then $L_1 = \{a, ab, aab\}$ (finite) or $L_2 = \{\varepsilon, a, b, aa, bb, \dots\}$ (infinite).

---

### Powers of $\Sigma$

Taking powers of an alphabet generates sets of strings of specific lengths.  
For $\Sigma = \{0, 1\}$:

* $\Sigma^0 = \{\varepsilon\}$ *(Set of all strings of length 0; $\varepsilon$ represents the empty string)*
* $\Sigma^1 = \{0, 1\}$ *(Set of all strings of length 1)*
* $\Sigma^2 = \{00, 01, 10, 11\}$ *(Set of all strings of length 2)*

#### Cardinality Rule
If $|\Sigma| = k$, then the number of strings of length $n$ is:
$$|\Sigma^n| = k^n$$

*Example:* If $\Sigma = \{a, b, c\}$, then $|\Sigma| = 3$.  
The number of strings of length 3 is $|\Sigma^3| = 3^3 = 27$.

---

### Kleene Closures

* **Kleene Star ($\Sigma^*$):** The set of all possible strings of all lengths over $\Sigma$, including the empty string $\varepsilon$. It is always an infinite set.
  $$\Sigma^* = \Sigma^0 \cup \Sigma^1 \cup \Sigma^2 \cup \dots$$

* **Positive Closure ($\Sigma^+$):** The set of all possible strings of length 1 or greater (excluding $\varepsilon$).
  $$\Sigma^+ = \Sigma^1 \cup \Sigma^2 \cup \Sigma^3 \cup \dots = \Sigma^* \setminus \{\varepsilon\}$$

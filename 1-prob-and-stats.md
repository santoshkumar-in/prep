---
# PROBABILITY & STATISTICS

## Complete Exam-Preparation Notes
---

## 2-WEEK STUDY PLAN — PROBABILITY & STATISTICS

| Day        | Topics                                              | Activity                                         |
| ---------- | --------------------------------------------------- | ------------------------------------------------ |
| **Day 1**  | FPC, Permutations (basic + restricted)              | Read notes + solve 10 questions                  |
| **Day 2**  | Circular permutations, Permutations with repetition | Read notes + solve 10 questions                  |
| **Day 3**  | Combinations (basic + restricted + techniques)      | Read notes + solve 15 questions                  |
| **Day 4**  | P&C mixed problems                                  | Solve 20 mixed problems from sample paper        |
| **Day 5**  | Basic Probability, Sample Space, Events, Axioms     | Read notes + solve 10 questions                  |
| **Day 6**  | Conditional Probability, Bayes Theorem              | Read notes + solve 10 questions                  |
| **Day 7**  | **REVISION DAY** — P&C + Basic Probability          | Redo all solved examples. Formula sheet revision |
| **Day 8**  | Random Variables, PMF, PDF, CDF                     | Read notes + solve 10 questions                  |
| **Day 9**  | Distributions (Binomial, Normal, Chi-square)        | Read notes + solve 10 questions                  |
| **Day 10** | Descriptive Statistics (all measures + plots)       | Read notes + solve 10 questions                  |
| **Day 11** | Hypothesis Testing (z, t, F tests)                  | Read notes + solve 10 questions                  |
| **Day 12** | Correlation (Pearson, Spearman, Kendall)            | Read notes + solve 10 questions                  |
| **Day 13** | **FULL REVISION** — All topics                      | Go through summary sections only                 |
| **Day 14** | **MOCK TEST DAY**                                   | Attempt full sample paper under exam conditions  |

**Daily time commitment:** 2–3 hours
**Priority order:** P&C → Basic Probability → Hypothesis Testing → Distributions → Descriptive Stats → Correlation

---

---

# PART 1 — PERMUTATIONS AND COMBINATIONS

---

## LECTURE 1 — FUNDAMENTAL PRINCIPLE OF COUNTING (FPC)

---

### 1. Concept Overview

**Definition:**
If one task can be performed in $m$ ways, and after completing it, a second task can be performed in $n$ ways, then both tasks together can be performed in $m \times n$ ways.

**Intuition:**
Think of it as a tree diagram. Each branch of the first task splits into $n$ branches for the second task. Total branches = $m \times n$.

**Why important:**
FPC is the foundation of all counting problems — permutations, combinations, and probability calculations all rest on this principle.

---

### 2. Mathematical Foundation

$$\text{Total ways} = n_1 \times n_2 \times n_3 \times \cdots \times n_k$$

where $n_i$ = number of ways the $i$-th task can be performed.

---

### 3. Worked Examples

**Example 1:**
Delhi to Bombay: Train, Air, Bus (3 ways). Bombay station to hotel: Auto, Cab (2 ways).
$$\text{Total} = 3 \times 2 = 6$$

**Example 2 ⭐:**
4 routes between Delhi and Goa.

**(i) Any route on return:**
$$4 \times 4 = 16$$

**(ii) Same route NOT taken on return:**
$$4 \times 3 = 12$$

**Example 3 ⭐:**
4-digit numbers $> 4000$ from $\{0,1,2,3,4\}$

**(i) Repetition allowed:**
Thousands digit must be 4 (only option $\geq 4$ from the set):
$$1 \times 5 \times 5 \times 5 = 125$$

**(ii) Repetition NOT allowed:**
$$1 \times 4 \times 3 \times 2 = 24$$

**Example 4:**
Odd numbers from $\{0, 2, 5, 7\}$, no repetition:

Units digit must be 5 or 7 (odd digits). Work case-by-case:

| Case    | Digits                                                          | Count                               |
| ------- | --------------------------------------------------------------- | ----------------------------------- |
| 4-digit | Units: 2 choices; remaining 3 positions from remaining 3 digits | $2 \times 3 \times 2 \times 1 = 12$ |
| 3-digit | Units: 2; hundreds: 3; tens: 2                                  | $2 \times 3 \times 2 = 12$          |
| 2-digit | Units: 2; tens: 3                                               | $2 \times 3 = 6$                    |
| 1-digit | Only 5 or 7                                                     | $2$                                 |

$$\text{Total} = 12 + 12 + 6 + 2 = \mathbf{32}$$

---

### 4. Examination Focus

- ⭐ Route problems (go and return, same/different route)
- ⭐ Digit formation problems with restrictions (greater than, less than, odd, even)
- **Common mistake:** Forgetting that 0 cannot be the leading digit in a number
- **Key formula to memorize:** $m \times n$ for two independent tasks

---

### 5. Summary

- FPC: multiply number of ways for each independent task
- Always check for restrictions (leading digit $\neq 0$, same route, etc.)
- FPC applies to any number of tasks: $n_1 \times n_2 \times \cdots \times n_k$

---

## LECTURE 2 — FACTORIALS AND PERMUTATIONS

---

### 1. Concept Overview

**Factorial:**
$$n! = n \times (n-1) \times (n-2) \times \cdots \times 2 \times 1$$

Special values: $0! = 1$, $\quad 1! = 1$

**Permutation:**
A permutation is an **arrangement** of objects where **order matters**.

$${}^nP_r = \frac{n!}{(n-r)!}$$

where $n$ = total objects, $r$ = objects taken at a time.

**Intuition:**
If you have 5 people and 3 chairs, the first chair has 5 choices, second has 4, third has 3:
$$5 \times 4 \times 3 = {}^5P_3 = \frac{5!}{2!} = 60$$

---

### 2. Mathematical Foundation

$${}^nP_r = \frac{n!}{(n-r)!}$$

**Key Properties:** ⭐

| Property                 | Formula        |
| ------------------------ | -------------- |
| All $n$ objects arranged | ${}^nP_n = n!$ |
| Zero objects             | ${}^nP_0 = 1$  |
| One object               | ${}^nP_1 = n$  |

**Factorial simplification tricks:**
$$\frac{n!}{(n-r)!} = n \times (n-1) \times \cdots \times (n-r+1) \quad (r \text{ terms})$$

---

### 3. Worked Examples

**Example 1:**
3 rings on 4 fingers (at most one ring per finger):
$${}^4P_3 = \frac{4!}{1!} = 24$$

**Example 2:**
4 people in 4 seats:
$$4! = 24$$

**Example 3 ⭐:**
Simplify $\dfrac{1}{6!} + \dfrac{1}{7!} + \dfrac{1}{8!}$

$$= \frac{1}{6!}\left(1 + \frac{1}{7} + \frac{1}{56}\right) = \frac{1}{6!} \cdot \frac{56 + 8 + 1}{56} = \frac{65}{56 \cdot 6!}$$

---

### 4. Examination Focus

- ⭐ ${}^nP_r$ formula application
- ⭐ Factorial simplification
- **Common mistake:** Confusing ${}^nP_r$ with ${}^nC_r$ — remember permutation = arrangement (order matters)
- **Memorize:** ${}^nP_n = n!$, ${}^nP_0 = 1$, ${}^nP_1 = n$

---

### 5. Summary

- $n!$ = product of all integers from 1 to $n$; $0!=1$
- ${}^nP_r = \frac{n!}{(n-r)!}$ — order matters
- ${}^nP_n = n!$

---

## LECTURE 3 — RESTRICTED PERMUTATIONS

---

### 1. Concept Overview

Restricted permutations handle cases where:

- Certain objects **must always be together**
- Certain objects **must always be included**
- Certain objects **must always be excluded**

---

### 2. Mathematical Foundation ⭐

**Type 1 — Objects always together:**
Treat the group as **one unit**. If $p$ objects must stay together out of $n$ objects:
$$\text{Arrangements} = p! \times (n - p + 1)!$$

**Type 2 — $x$ particular objects always included:**
$${}^{n-x}P_{r-x} \times r! \quad \text{(positions for fixed items × arrangements of rest)}$$

More practically: fix the $x$ items, arrange remaining $r-x$ from $n-x$ remaining objects.

**Type 3 — $x$ particular objects always excluded:**
$${}^{n-x}P_r$$

---

### 3. Worked Examples

**Example 1 ⭐ — Always together:**
5-letter words from {A, N, K, I, T} where I and T always together:

- Treat IT as one block → 4 units: {A, N, K, [IT]}
- Arrangements of 4 units: $4!$
- Arrangements within IT block: $2!$
  $$\text{Total} = 4! \times 2! = 24 \times 2 = 48$$

**Example 2 — Always included:**
From VARUN (5 letters), arrange 4 letters, V always included:
$${}^1P_1 \times {}^4P_3 = 1 \times 24 = 24$$

**Example 3 — Always excluded:**
From VARUN, arrange 4 letters, N never included:
Remove N → choose from {V, A, R, U}:
$${}^4P_4 = 4! = 24$$

**Example 4 ⭐ — Books on shelf:**
3 Economics, 2 History, 4 English books, all different.

**(i) Total arrangements:**
$$9! = 362880$$

**(ii) Same subject always together:**
Treat each subject as one block → 3 blocks:
$$3! \times 3! \times 2! \times 4! = 6 \times 6 \times 2 \times 24 = 1728$$

**Example 5 ⭐ — No two girls together:**
5 boys, 3 girls, no 2 girls adjacent:

Step 1: Arrange 5 boys: $5! = 120$
Step 2: 6 gaps available (★B★B★B★B★B★), choose 3:
$${}^6P_3 = 120$$
$$\text{Total} = 5! \times {}^6P_3 = 120 \times 120 = 14400$$

**Example 6 ⭐ — COMBINE:**
COMBINE has 7 letters. Vowels: O, I, E. Consonants: C, M, B, N.

**(i) Vowels always together:**
$$5! \times 3! = 120 \times 6 = 720$$

**(ii) Vowels never all together:**
$$7! - 5! \times 3! = 5040 - 720 = 4320$$

**(iii) No 2 vowels together:**
Arrange 4 consonants: $4!$. Place 3 vowels in 5 gaps: ${}^5P_3$
$$4! \times {}^5P_3 = 24 \times 60 = 1440$$

**(iv) Vowels at odd positions only:**
Odd positions in 7: positions 1,3,5,7 (4 positions). Place 3 vowels: ${}^4P_3$. Consonants in remaining 4: ${}^4P_4$
$${}^4P_3 \times {}^4P_4 = 24 \times 24 = 576$$

---

### 4. Examination Focus

- ⭐ "Always together" type — most frequently asked
- ⭐ "No two of same type adjacent" — arrange one type first, use gaps
- ⭐ Vowels and consonants arrangement problems
- **Common mistake:** Forgetting to multiply by internal arrangements of the grouped block
- **Pattern from sample papers:** COMBINE-type word arrangement problems appear frequently

---

### 5. Summary

- Always together → treat as one unit, multiply by internal arrangements
- Never together → arrange others first, use gap method
- Always included/excluded → reduce the pool, adjust $r$

---

## LECTURE 4 — PERMUTATIONS WITH REPETITION

---

### 1. Concept Overview

Two cases:

1. **Repetition allowed** — each position can have any of $n$ items
2. **Objects not all different** — identical items reduce total arrangements

---

### 2. Mathematical Foundation ⭐

**Case 1 — Repetition allowed:**
$r$ positions, $n$ distinct objects available:
$$\text{Arrangements} = n^r$$

**Case 2 — Objects not all different:**
$n$ objects where $p$ are alike of one kind, $q$ alike of another, $r$ alike of another:
$$\text{Arrangements} = \frac{n!}{p! \cdot q! \cdot r!}$$

---

### 3. Worked Examples

**Example 1:**
5 apples distributed to 3 boys (any apple can go to any boy):
$$3^5 = 243$$

**Example 2 ⭐:**
4-digit numbers from $\{1,2,3,4,5,6\}$, repetition allowed:
$$6^4 = 1296$$

**Example 3 ⭐:**
Arrangements of ABAB (A appears 2 times, B appears 2 times):
$$\frac{4!}{2! \cdot 2!} = \frac{24}{4} = 6$$

**Example 4 ⭐:**
6-digit numbers from digits $\{1,1,2,2,3,3\}$:

**(i) Total:**
$$\frac{6!}{2! \cdot 2! \cdot 2!} = \frac{720}{8} = 90$$

**(ii) Greater than 300000** (leading digit must be 3):
Fix 3 in first position, arrange $\{1,1,2,2,3\}$:
$$1 \times \frac{5!}{2! \cdot 2! \cdot 1!} = \frac{120}{4} = 30$$

**Example 5 ⭐ — INDEPENDENCE:**
Letters: I(1), N(3), D(2), E(4), P(1), C(1) — total 12 letters.

$$\text{Total} = \frac{12!}{3! \cdot 2! \cdot 4!}$$

**(i) Words starting with P:**
$$\frac{11!}{3! \cdot 2! \cdot 4!}$$

**(ii) Vowels (I,E,E,E,E) always together:**
Treat 5 vowels as one block → 8 units:
$$\frac{8!}{3! \cdot 2!} \times \frac{5!}{4!}$$

**(iii) Words beginning with I, ending with P:**
Fix I at start, P at end → arrange remaining 10:
$$\frac{10!}{3! \cdot 2! \cdot 4!}$$

---

### 4. Examination Focus

- ⭐ Arrangements of words with repeated letters (INDEPENDENCE, MATHEMATICS-type)
- ⭐ $n^r$ formula for repetition-allowed problems
- **Common mistake:** Missing the division by factorials of repeated elements
- **Memorize:** $\frac{n!}{p! \cdot q! \cdot r!}$ for non-all-different objects

---

### 5. Summary

- Repetition allowed: $n^r$
- Identical objects: $\frac{n!}{p_1! \cdot p_2! \cdots p_k!}$
- Always check how many times each letter/object repeats

---

## LECTURE 5 — CIRCULAR PERMUTATIONS

---

### 1. Concept Overview

In circular arrangements, rotations of the same arrangement are considered identical. So we fix one element and arrange the rest.

---

### 2. Mathematical Foundation ⭐

| Type                                           | Formula             |
| ---------------------------------------------- | ------------------- |
| Circular arrangement of $n$ distinct objects   | $(n-1)!$            |
| Necklace / Keyring (clockwise = anticlockwise) | $\dfrac{(n-1)!}{2}$ |
| Linear arrangement (reference)                 | $n!$                |

**Circular with repeated elements:**
$$\frac{(n-1)!}{p_1! \cdot p_2! \cdots}$$

---

### 3. Worked Examples

**Example 1:**
10 students arranged:

**(i) In a line:** $10! = 3628800$

**(ii) In a circle:** $(10-1)! = 9! = 362880$

**Example 2 ⭐ — Round table, no two women together:**
6 men, 5 women, no 2 women adjacent:

Step 1: Arrange 6 men in circle: $(6-1)! = 5! = 120$
Step 2: 6 gaps, place 5 women in 5 gaps: ${}^6P_5 = 720$
$$\text{Total} = 5! \times {}^6P_5 = 120 \times 720 = 86400$$

**Example 3 ⭐ — Indian and Pakistani PM not together:**
10 PMs at round table, Indian and Pakistani not adjacent:

Total circular arrangements: $9!$
When they ARE together (treat as one unit → 9 units in circle): $8! \times 2!$
$$\text{Answer} = 9! - 8! \times 2! = 362880 - 80640 = 282240$$

**Example 4 ⭐ — A,B,C,D,E,F at round table:**
Total: $(6-1)! = 5! = 120$

**(i) C and D always together:**
$$4! \times 2! = 24 \times 2 = 48$$

**(ii) A and D NOT together:**
$$5! - 4! \times 2! = 120 - 48 = 72$$

**(iii) None of A, B, C sit together:**
Arrange D, E, F in circle: $2! = 2$
Place A, B, C in 3 gaps: $3! = 6$
$$2! \times 3! = 12$$

---

### 4. Examination Focus

- ⭐ Round table problems with "not together" restriction — use complement method
- ⭐ Necklace problems — divide by 2
- **Common mistake:** Using $n!$ instead of $(n-1)!$ for circular arrangements
- **Key insight:** "Not together" = Total $-$ "Always together"

---

### 5. Summary

- Circular: fix one, arrange rest → $(n-1)!$
- Necklace: $\frac{(n-1)!}{2}$
- Not together → complement method: Total $-$ Together
- No two of same type adjacent → gap method

---

## LECTURE 6 — COMBINATIONS (BASIC AND RESTRICTED)

---

### 1. Concept Overview

**Combination = Selection** where **order does NOT matter**.

$${}^nC_r = \binom{n}{r} = \frac{n!}{r!(n-r)!}$$

**Permutation vs Combination:**

- Permutation: ABC, BAC, CAB are different (order matters)
- Combination: ABC = BAC = CAB (same selection)

$${}^nP_r = {}^nC_r \times r!$$

---

### 2. Mathematical Foundation ⭐

**Properties:**

| Property          | Formula                                   |
| ----------------- | ----------------------------------------- |
| ${}^nC_n$         | $= 1$                                     |
| ${}^nC_0$         | $= 1$                                     |
| ${}^nC_1$         | $= n$                                     |
| Symmetry          | ${}^nC_r = {}^nC_{n-r}$                   |
| Pascal's Identity | ${}^nC_r + {}^nC_{r+1} = {}^{n+1}C_{r+1}$ |

**Restricted Combinations:**

| Restriction                              | Formula           |
| ---------------------------------------- | ----------------- |
| $x$ particular items **always included** | ${}^{n-x}C_{r-x}$ |
| $x$ particular items **never included**  | ${}^{n-x}C_r$     |

---

### 3. Worked Examples

**Example 1 ⭐ — Committee formation:**
Team of 6 from 5 men and 6 women.

**(i) Exactly 2 men:**
$${}^5C_2 \times {}^6C_4 = 10 \times 15 = 150$$

**(ii) At least 2 men:**

| Combination | Formula                  | Value |
| ----------- | ------------------------ | ----- |
| 2M + 4W     | ${}^5C_2 \times {}^6C_4$ | 150   |
| 3M + 3W     | ${}^5C_3 \times {}^6C_3$ | 200   |
| 4M + 2W     | ${}^5C_4 \times {}^6C_2$ | 75    |
| 5M + 1W     | ${}^5C_5 \times {}^6C_1$ | 6     |

$$\text{Total} = 431$$

**Best approach (complement):**
$${}^{11}C_6 - {}^5C_0 \times {}^6C_6 - {}^5C_1 \times {}^6C_5 = 462 - 1 - 30 = 431 \checkmark$$

**Example 2 ⭐ — Words from consonants and vowels:**
5 consonants, 4 vowels. Words with 3 consonants + 2 vowels:

Step 1 — Select:
$${}^5C_3 \times {}^4C_2 = 10 \times 6 = 60$$

Step 2 — Arrange:
$$60 \times 5! = 60 \times 120 = 7200$$

**Example 3 ⭐ — Diagonals of hexagon:**
$${}^6C_2 - 6 = 15 - 6 = 9$$

General formula: $\dfrac{n(n-3)}{2}$ diagonals in $n$-sided polygon ⭐

**Example 4 ⭐ — Collinear points:**
12 points, 7 collinear:
$${}^{12}C_2 - {}^7C_2 + 1 = 66 - 21 + 1 = 46 \text{ lines}$$

**Example 5 ⭐ — Handshakes:**
Total handshakes = 6, find number of people:
$${}^nC_2 = 6 \implies \frac{n(n-1)}{2} = 6 \implies n = 4$$

**Example 6 — Library books:**
8 books, 3 tickets. Cannot borrow Maths Part 2 unless Maths Part 1 also borrowed:

Case 1 (M1 not borrowed): Choose from remaining 6: ${}^6C_3 = 20$
Case 2 (M1 borrowed): Choose 2 more from remaining 7 (including M2): ${}^7C_2 = 21$
$$\text{Total} = 20 + 21 = 41$$

---

### 4. Examination Focus

- ⭐ Committee/team formation — most common exam topic
- ⭐ "At least" type — use complement method when possible
- ⭐ Diagonals formula $\frac{n(n-3)}{2}$
- ⭐ Collinear points problem
- **Common mistake:** Forgetting to arrange after selecting in word-formation problems
- **Key distinction:** Selection → ${}^nC_r$; Selection + Arrangement → ${}^nC_r \times r!$

---

### 5. Summary

- ${}^nC_r = \frac{n!}{r!(n-r)!}$ — order does NOT matter
- ${}^nC_r = {}^nC_{n-r}$ — symmetry property
- At least/at most → use complement
- Always included: ${}^{n-x}C_{r-x}$; Never included: ${}^{n-x}C_r$

---

---

# PART 2 — BASIC PROBABILITY

---

## LECTURE 7 (Transcript 8) — BASIC PROBABILITY

---

### 1. Concept Overview

**Probability** is a numerical measure of the likelihood of an event occurring.

$$P(E) = \frac{\text{Number of favourable outcomes}}{\text{Total number of outcomes}}$$

**Intuition:** If you repeat an experiment a very large number of times, the proportion of times event $E$ occurs approaches $P(E)$.

---

### 2. Mathematical Foundation ⭐

**Axioms of Probability:**

1. $0 \leq P(E) \leq 1$ for any event $E$
2. $P(S) = 1$ where $S$ is the sample space
3. If $A$ and $B$ are mutually exclusive: $P(A \cup B) = P(A) + P(B)$

**Complement Rule:**
$$P(\bar{E}) = 1 - P(E) \quad \Leftrightarrow \quad P(E) + P(\bar{E}) = 1$$

**Standard Sample Spaces:** ⭐

| Experiment             | Sample Space Size |
| ---------------------- | ----------------- |
| $n$ coins tossed       | $2^n$             |
| $n$ dice thrown        | $6^n$             |
| Draw from 52-card deck | 52                |

**52-Card Deck Structure:** ⭐

- 4 suits: Spade ♠, Club ♣, Diamond ♦, Heart ♥
- Each suit: 13 cards (A, 2, 3, ..., 10, J, Q, K)
- Total face cards: 12 (J, Q, K of each suit)
- Total aces: 4

**Types of Events:**

| Type                    | Definition                                          | Example                        |
| ----------------------- | --------------------------------------------------- | ------------------------------ |
| **Equally Likely**      | Each outcome has equal probability                  | Fair coin: $P(H) = P(T) = 0.5$ |
| **Mutually Exclusive**  | Cannot occur simultaneously; $A \cap B = \emptyset$ | Head and Tail in one toss      |
| **Mutually Exhaustive** | $A \cup B = S$ (cover entire sample space)          | Head and Tail together         |
| **Independent**         | $P(A \cap B) = P(A) \cdot P(B)$                     | Two separate coin tosses       |

---

### 3. Worked Examples

**Example 1 ⭐ — Ball drawing:**
Bag: 3 red, 4 black. Draw 2 balls. Total ways: ${}^7C_2 = 21$

**(i) Both red:** $\frac{{}^3C_2}{{}^7C_2} = \frac{3}{21} = \frac{1}{7}$

**(ii) Both black:** $\frac{{}^4C_2}{{}^7C_2} = \frac{6}{21} = \frac{2}{7}$

**(iii) One red, one black:** $\frac{{}^3C_1 \times {}^4C_1}{{}^7C_2} = \frac{12}{21} = \frac{4}{7}$

**Verification:** $\frac{1}{7} + \frac{2}{7} + \frac{4}{7} = 1$ ✓

**Example 2 — Die rolled:**
$S = \{1,2,3,4,5,6\}$, $A = \{2,4,6\}$ (even), $B = \{1,2,3\}$ ($\leq 3$)

$A \cap B = \{2\}$

$$P(A \cup B) = P(A) + P(B) - P(A \cap B) = \frac{3}{6} + \frac{3}{6} - \frac{1}{6} = \frac{5}{6}$$

---

### 4. Algebra of Events ⭐

**Addition Theorem (Two events):**
$$P(A \cup B) = P(A) + P(B) - P(A \cap B)$$

**Addition Theorem (Three events):**
$$P(A \cup B \cup C) = P(A) + P(B) + P(C) - P(A \cap B) - P(A \cap C) - P(B \cap C) + P(A \cap B \cap C)$$

**For mutually exclusive events:**
$$P(A \cup B) = P(A) + P(B)$$

---

### 5. Examination Focus

- ⭐ Ball/card drawing problems using combinations
- ⭐ Addition theorem — three events version
- ⭐ Complement rule for "at least one" problems
- **Common mistake:** Adding probabilities without subtracting intersection for non-mutually-exclusive events
- **Key formula:** $P(\text{at least one}) = 1 - P(\text{none})$

---

### 6. Summary

- $P(E) \in [0,1]$; $P(S) = 1$; $P(\bar{E}) = 1 - P(E)$
- Mutually exclusive: $P(A \cap B) = 0$
- Independent: $P(A \cap B) = P(A) \cdot P(B)$
- Addition theorem: always subtract intersection unless mutually exclusive

---

## LECTURE 8 (Transcript 10) — CONDITIONAL PROBABILITY AND BAYES' THEOREM

---

### 1. Concept Overview

**Conditional Probability:**
The probability of event $A$ given that event $B$ has already occurred.

$$P(A \mid B) = \frac{P(A \cap B)}{P(B)}, \quad P(B) > 0$$

**Intuition:** When $B$ occurs, it reduces the sample space to only outcomes in $B$. We then find what fraction of those outcomes also belong to $A$.

---

### 2. Mathematical Foundation ⭐

$$P(A \mid B) = \frac{P(A \cap B)}{P(B)}$$

$$P(B \mid A) = \frac{P(A \cap B)}{P(A)}$$

**Multiplication Rule:**
$$P(A \cap B) = P(A) \cdot P(B \mid A) = P(B) \cdot P(A \mid B)$$

**Bayes' Theorem:** ⭐
$$P(A \mid B) = \frac{P(B \mid A) \cdot P(A)}{P(B)}$$

**Total Probability:**
$$P(A) = P(A \mid B) \cdot P(B) + P(A \mid \bar{B}) \cdot P(\bar{B})$$

**Independence Check:**
$A$ and $B$ are independent if and only if:
$$P(A \cap B) = P(A) \cdot P(B)$$
which implies $P(A \mid B) = P(A)$ — knowing $B$ does not change probability of $A$.

---

### 3. Worked Examples

**Example 1 ⭐:**
2 coins tossed. $A$ = exactly 2 heads, $B$ = at least 1 head.
$S = \{HH, HT, TH, TT\}$

$A = \{HH\}$, $B = \{HH, HT, TH\}$, $A \cap B = \{HH\}$

$$P(A \mid B) = \frac{P(A \cap B)}{P(B)} = \frac{1/4}{3/4} = \frac{1}{3}$$

$$P(B \mid A) = \frac{P(A \cap B)}{P(A)} = \frac{1/4}{1/4} = 1$$

**Example 2 ⭐:**
Die thrown twice. Sum = 6. Probability that 4 appeared at least once.

$B$ = {sum is 6} = $\{(1,5),(2,4),(3,3),(4,2),(5,1)\}$ → $P(B) = 5/36$

$A \cap B$ = $\{(2,4),(4,2)\}$ → $P(A \cap B) = 2/36$

$$P(A \mid B) = \frac{2/36}{5/36} = \frac{2}{5}$$

**Example 3 ⭐ — 3 coin tosses:**
$S$ has 8 equally likely outcomes.

**(i)** $E$ = head on 3rd toss, $F$ = head on first 2 tosses
$F = \{HHH, HHT\}$, $E \cap F = \{HHH\}$
$$P(E \mid F) = \frac{1/8}{2/8} = \frac{1}{2}$$

**(ii)** $E$ = at least 2 heads, $F$ = at most 2 heads
$E \cap F = \{HHT, HTH, THH\}$, $P(F) = 7/8$
$$P(E \mid F) = \frac{3/8}{7/8} = \frac{3}{7}$$

**Example 4 ⭐ — Die, even number, prime:**
$B$ = even = $\{2,4,6\}$, $A$ = prime = $\{2,3,5\}$
$A \cap B = \{2\}$
$$P(A \mid B) = \frac{1/6}{3/6} = \frac{1}{3}$$

**Example 5 ⭐ — Defective parts (Bayes):**
1000 parts, 50 defective. Draw 2 without replacement.

$P(\text{defective in 2nd draw}) = ?$ (without info about 1st)

Using total probability:
$$P(C) = P(C \mid A) \cdot P(A) + P(C \mid \bar{A}) \cdot P(\bar{A})$$
$$= \frac{49}{999} \cdot \frac{50}{1000} + \frac{50}{999} \cdot \frac{950}{1000} = \frac{50}{1000}$$

The probability remains $50/1000$ — knowing nothing about the first draw doesn't change the second draw's probability.

---

### 4. Examination Focus

- ⭐ Conditional probability from sample space definition
- ⭐ Bayes' theorem — manufacturing/medical problems
- ⭐ Total probability theorem
- **Common mistake:** Confusing $P(A \mid B)$ with $P(B \mid A)$ — these are generally different
- **Key insight:** Independent events → $P(A \mid B) = P(A)$

---

### 5. Summary

- $P(A \mid B) = \frac{P(A \cap B)}{P(B)}$
- Bayes: $P(A \mid B) = \frac{P(B \mid A) \cdot P(A)}{P(B)}$
- Total probability: expand $P(B)$ using exhaustive partition
- Independence: $P(A \cap B) = P(A) \cdot P(B)$

---

---

# PART 3 — RANDOM VARIABLES AND DISTRIBUTIONS

---

## LECTURE 9 (Transcript 10) — RANDOM VARIABLES

---

### 1. Concept Overview

**Random Variable:**
A function that maps outcomes of a random experiment to real numbers.

Example: In a coin toss, map Head → 0, Tail → 1.

**Types:**

- **Discrete:** finite or countably infinite outcomes (e.g., number of heads in $n$ tosses)
- **Continuous:** uncountably infinite outcomes (e.g., body temperature)

---

### 2. Mathematical Foundation ⭐

**Probability Mass Function (PMF) — Discrete:**
$$P(X = x_i) = p_i, \quad \sum_i p_i = 1, \quad p_i \geq 0$$

**Probability Density Function (PDF) — Continuous:**
$$P(a \leq X \leq b) = \int_a^b f(x)\, dx, \quad \int_{-\infty}^{\infty} f(x)\, dx = 1$$

**Cumulative Distribution Function (CDF):**
$$F(x) = P(X \leq x) = \int_{-\infty}^{x} f(t)\, dt$$

**Moments:**
$$E[X^k] = \int_{-\infty}^{\infty} x^k f(x)\, dx \quad \text{(continuous)}$$
$$E[X^k] = \sum_i x_i^k P(X = x_i) \quad \text{(discrete)}$$

**Mean (First Moment):** ⭐
$$\mu = E[X]$$

**Variance:** ⭐
$$\sigma^2 = E[(X-\mu)^2] = E[X^2] - \mu^2$$

**Standard Deviation:** $\sigma = \sqrt{\sigma^2}$

---

### 3. Key Distributions ⭐

#### Binomial Distribution ⭐

**Setup:** $n$ independent trials, each with success probability $p$.

$$P(X = k) = \binom{n}{k} p^k (1-p)^{n-k}, \quad k = 0, 1, \ldots, n$$

$$\text{Mean} = np, \qquad \text{Variance} = np(1-p)$$

**Example:** 20 fair coin tosses. $P(X = 10)$ is maximum (most probable). For large $n$, approximates Normal distribution.

---

#### Normal (Gaussian) Distribution ⭐

$$f(x) = \frac{1}{\sigma\sqrt{2\pi}} \exp\left(-\frac{(x-\mu)^2}{2\sigma^2}\right)$$

$$\text{Mean} = \mu, \qquad \text{Variance} = \sigma^2$$

**Notation:** $X \sim N(\mu, \sigma^2)$

**Standard Normal:** $\mu = 0$, $\sigma = 1$ → $Z \sim N(0,1)$

**Standardization:** ⭐
$$Z = \frac{X - \mu}{\sigma}$$

**Key properties:**

- Symmetric about $\mu$
- $\mu \pm \sigma$ contains ~68% of data
- $\mu \pm 2\sigma$ contains ~95% of data
- $\mu \pm 3\sigma$ contains ~99.7% of data

**Linear transformation:** If $X \sim N(\mu, \sigma^2)$, then $Y = aX + b \sim N(a\mu + b, a^2\sigma^2)$

---

#### Chi-Square Distribution ⭐

If $Z_1, Z_2, \ldots, Z_n$ are independent standard normal variables:
$$\chi^2 = Z_1^2 + Z_2^2 + \cdots + Z_n^2 \sim \chi^2(n)$$

where $n$ = degrees of freedom.

- Takes values only in $[0, \infty)$
- Sample variance follows chi-square distribution
- Used in hypothesis testing for variances

---

### 4. Multivariate Normal Distribution ⭐

For random vector $\mathbf{X} = (X_1, X_2, \ldots, X_n)^T$:

$$\mathbf{X} \sim N(\boldsymbol{\mu}, \boldsymbol{\Sigma})$$

**Mean vector:** $\boldsymbol{\mu} = E[\mathbf{X}]$

**Covariance matrix:** ⭐
$$\boldsymbol{\Sigma} = E[(\mathbf{X} - \boldsymbol{\mu})(\mathbf{X} - \boldsymbol{\mu})^T]$$

Structure of $\boldsymbol{\Sigma}$:

- Diagonal elements: $\sigma_{X_i}^2$ (variance of each variable)
- Off-diagonal elements: $\sigma_{X_i X_j}$ (covariance between $X_i$ and $X_j$)
- $\boldsymbol{\Sigma}$ is symmetric and positive semi-definite

---

### 5. Examination Focus

- ⭐ Binomial distribution — mean, variance, PMF
- ⭐ Normal distribution — standardization, 68-95-99.7 rule
- ⭐ Covariance matrix structure
- **Common mistake:** Confusing variance of $\bar{X}$ ($= \sigma^2/n$) with population variance $\sigma^2$
- **Key:** $\text{Var}(\bar{X}) = \sigma^2/n$ — sample mean is less noisy than individual observations

---

### 6. Summary

- PMF (discrete) / PDF (continuous) — probabilities sum/integrate to 1
- Mean = $E[X]$; Variance = $E[X^2] - (E[X])^2$
- Binomial: $np$, $np(1-p)$; Normal: $\mu$, $\sigma^2$
- Standardization: $Z = (X-\mu)/\sigma$
- Covariance matrix: symmetric, diagonal = variances, off-diagonal = covariances

---

---

# PART 4 — DESCRIPTIVE STATISTICS

---

## LECTURE 10 (Transcript 11) — DESCRIPTIVE STATISTICS

---

### 1. Concept Overview

**Population vs Sample:**

- **Population:** All possible outcomes of the experiment (complete set)
- **Sample:** A finite subset drawn from the population

**Goal:** Use sample statistics to infer population parameters.

**Types of analysis:**

- **Descriptive (Graphical):** Histograms, box plots, QQ plots, scatter plots
- **Descriptive (Numerical):** Mean, median, mode, variance, MAD
- **Inferential:** Estimation, hypothesis testing

---

### 2. Measures of Central Tendency ⭐

**Mean (Sample):**
$$\bar{x} = \frac{1}{n}\sum_{i=1}^n x_i$$

- Best estimate in least squares sense
- **Unbiased:** $E[\bar{x}] = \mu$
- **Sensitive to outliers** ⭐

**Median:**

- Value below which 50% of data falls
- Order data; take middle value (odd $n$) or average of two middle values (even $n$)
- **Robust to outliers** ⭐

**Mode:**

- Most frequently occurring value
- Distribution can be unimodal or bimodal

---

### 3. Measures of Spread ⭐

**Sample Variance:**
$$s^2 = \frac{1}{n-1}\sum_{i=1}^n (x_i - \bar{x})^2$$

- Unbiased estimator of population variance
- Why $n-1$? One degree of freedom used to estimate $\bar{x}$
- **Sensitive to outliers** ⭐

**Standard Deviation:** $s = \sqrt{s^2}$

**Mean Absolute Deviation (MAD):**
$$\text{MAD} = \frac{1}{n}\sum_{i=1}^n |x_i - \bar{x}|$$

- **More robust than variance** to outliers ⭐

**Range:** Maximum $-$ Minimum

---

### 4. Graphical Tools ⭐

**Histogram:**

- Divide data into intervals, count frequency in each
- Shows distribution shape
- Large sample → bell-shaped for normal data

**Box Plot (Box-and-Whisker):**

- Q1 = 25th percentile, Q2 = median = 50th percentile, Q3 = 75th percentile
- Box spans Q1 to Q3 (IQR = Q3 - Q1)
- Whiskers extend to min and max
- Better visual of spread than single number

**QQ Plot (Probability Plot):** ⭐

- Plot sample quantiles vs theoretical quantiles of assumed distribution
- If points fall on 45° line → data follows assumed distribution
- Used to test normality assumption

**Scatter Plot:**

- Plot $Y$ vs $X$ to visually assess relationship
- Linear trend → consider linear regression
- No pattern → likely independent variables

---

### 5. Important Properties ⭐

**Distribution of sample mean:**
$$\bar{X} \sim N\left(\mu, \frac{\sigma^2}{n}\right)$$

- Taking $n$ samples and averaging reduces variance by factor $n$
- Noise reduction: standard deviation of $\bar{X}$ is $\sigma/\sqrt{n}$

**Distribution of sample variance:**
$$\frac{(n-1)s^2}{\sigma^2} \sim \chi^2(n-1)$$

---

### 6. Examination Focus

- ⭐ Why use $n-1$ in sample variance (degrees of freedom)
- ⭐ Mean vs Median — which is robust to outliers?
- ⭐ QQ plot interpretation
- ⭐ $\text{Var}(\bar{X}) = \sigma^2/n$
- **Common mistake:** Using $n$ instead of $n-1$ in sample variance
- **Key insight:** Outliers affect mean and variance heavily, but median and MAD are robust

---

### 7. Summary

- Mean: not robust; Median: robust to outliers; Mode: most frequent
- Variance uses $n-1$ (unbiased); MAD is more robust
- $\bar{X}$ is normally distributed with variance $\sigma^2/n$
- Histogram shows shape; Box plot shows spread; QQ plot tests distribution; Scatter plot shows relationships

---

---

# PART 5 — HYPOTHESIS TESTING

---

## LECTURE 11 (Transcript 12) — HYPOTHESIS TESTING

---

### 1. Concept Overview

**What is hypothesis testing?**
A formal procedure for making decisions about population parameters based on sample data.

**Null Hypothesis ($H_0$):** The default/status quo claim we want to test.
**Alternative Hypothesis ($H_1$):** What we accept if evidence against $H_0$ is strong enough.

**Examples:**

- Pump efficiency: $H_0: \eta = \eta_0$ vs $H_1: \eta < \eta_0$
- Drug effectiveness: $H_0: \mu_A = \mu_B$ vs $H_1: \mu_A \neq \mu_B$

---

### 2. Types of Errors ⭐

| Decision\Truth         | $H_0$ True                | $H_0$ False                   |
| ---------------------- | ------------------------- | ----------------------------- |
| **Don't Reject $H_0$** | ✓ Correct                 | ✗ Type II Error ($\beta$)     |
| **Reject $H_0$**       | ✗ Type I Error ($\alpha$) | ✓ Correct (Power = $1-\beta$) |

**Type I Error ($\alpha$):** False alarm — rejecting $H_0$ when it is true

**Type II Error ($\beta$):** Miss — not rejecting $H_0$ when it is false

**Power = $1 - \beta$:** Probability of correctly rejecting a false $H_0$

**Trade-off:** ⭐ Decreasing $\alpha$ increases $\beta$ — you cannot minimize both simultaneously.

**Level of significance ($\alpha$):** Chosen by the analyst (common values: 0.01, 0.05, 0.10)

---

### 3. Test Types ⭐

**One-sided (One-tailed) test:**
$H_1: \mu > \mu_0$ or $H_1: \mu < \mu_0$
→ Rejection region on one side only

**Two-sided (Two-tailed) test:**
$H_1: \mu \neq \mu_0$
→ Rejection region on both sides; split $\alpha$ as $\alpha/2$ on each side

---

### 4. The Z-Test ⭐

**When to use:** Testing population mean $\mu$ when population variance $\sigma^2$ is **known**.

**Test statistic:**
$$Z = \frac{\bar{X} - \mu_0}{\sigma / \sqrt{n}}$$

Under $H_0$: $Z \sim N(0,1)$

**Decision rule (two-sided, $\alpha = 0.05$):**
$$\text{Reject } H_0 \text{ if } |Z| > 1.96$$

**Example ⭐ — Solid propellant:**
$H_0: \mu = 50$ cm/s, $H_1: \mu \neq 50$ (two-sided)
$n = 25$, $\bar{X} = 51.3$, $\sigma = 2$ (known)

$$Z = \frac{51.3 - 50}{2/\sqrt{25}} = \frac{1.3}{0.4} = 3.25$$

Since $3.25 > 1.96$ → **Reject $H_0$** — batch does not meet specification.

---

### 5. The T-Test ⭐

**When to use:** Testing population mean when $\sigma^2$ is **unknown** (use sample standard deviation $s$).

**Test statistic:**
$$T = \frac{\bar{X} - \mu_0}{s / \sqrt{n}} \sim t(n-1)$$

**Two-sample T-test (comparison of means):** ⭐
$H_0: \mu_1 = \mu_2$ (or equivalently $\mu_1 - \mu_2 = 0$) vs $H_1: \mu_1 \neq \mu_2$

**Pooled variance** (assuming equal variances):
$$s_p^2 = \frac{(n_1-1)s_1^2 + (n_2-1)s_2^2}{n_1 + n_2 - 2}$$

**Test statistic:**
$$T = \frac{(\bar{X}_1 - \bar{X}_2)}{s_p\sqrt{1/n_1 + 1/n_2}} \sim t(n_1 + n_2 - 2)$$

**Example ⭐ — Teaching methods:**
10 teachers each trained by method A and B.
$\bar{X}_1 = 70$, $s_1 = 3.37$, $\bar{X}_2 = 74$, $s_2 = 5.4$, $n_1 = n_2 = 10$

$H_0: \mu_1 = \mu_2$ vs $H_1: \mu_1 < \mu_2$ (one-sided)

Compute pooled $s_p$, then $T$ statistic. Compare with $t_{18, 0.05} = -1.73$.
Result: $T = -1.989 < -1.73$ → **Reject $H_0$** → Method B is more effective.

---

### 6. The F-Test ⭐

**When to use:** Comparing **variances** of two populations.

$H_0: \sigma_1^2 = \sigma_2^2$ vs $H_1: \sigma_1^2 \neq \sigma_2^2$ (two-sided)

**Test statistic:**
$$F = \frac{s_1^2}{s_2^2} \sim F(n_1-1, n_2-1)$$

**Decision:** Reject $H_0$ if $F < F_L$ or $F > F_U$ (two-sided critical values).

**Example ⭐:**
50 samples each: $s_1^2 = 2.05$, $s_2^2 = 7.64$
$F = 2.05/7.64 = 0.27$

Critical values at $\alpha = 0.05$: $F_L = 0.567$, $F_U = 1.762$

Since $0.27 < 0.567$ → **Reject $H_0$** → Variances are significantly different.

---

### 7. Summary of Tests ⭐

| Test           | Use Case                 | Distribution      | Application in ML/Regression    |
| -------------- | ------------------------ | ----------------- | ------------------------------- |
| **Z-test**     | Mean, $\sigma^2$ known   | $N(0,1)$          | Testing regression coefficients |
| **T-test**     | Mean, $\sigma^2$ unknown | $t(n-1)$          | Testing regression coefficients |
| **Chi-square** | Variance                 | $\chi^2(n-1)$     | Model adequacy                  |
| **F-test**     | Compare two variances    | $F(n_1-1, n_2-1)$ | Comparing regression models     |

---

### 8. Confidence Intervals ⭐

A $(1-\alpha) \times 100\%$ confidence interval for $\mu$:

**Known $\sigma$:**
$$\bar{X} \pm z_{\alpha/2} \cdot \frac{\sigma}{\sqrt{n}}$$

**Unknown $\sigma$:**
$$\bar{X} \pm t_{\alpha/2, n-1} \cdot \frac{s}{\sqrt{n}}$$

**Interpretation:** With $(1-\alpha) \times 100\%$ confidence, the true parameter lies in this interval.

---

### 9. Examination Focus

- ⭐ Type I vs Type II error — definition and trade-off
- ⭐ Z-test vs T-test — when to use which
- ⭐ F-test for comparing variances
- ⭐ Confidence interval construction and interpretation
- ⭐ P-value interpretation — small P-value → reject $H_0$
- **Common mistake:** Confusing "reject $H_0$" with "prove $H_1$ is true"
- **Key fact:** We control $\alpha$ (Type I error), not $\beta$ directly

---

---

# PART 6 — CORRELATION

---

## LECTURE 12 (Transcript 17) — CORRELATION

---

### 1. Concept Overview

**Correlation** measures the **strength and direction of association** between two variables.

**Important warning:** Correlation ≠ Causation. A third hidden variable may drive both.

**Preliminary check:** Always plot a scatter plot before computing correlation.

---

### 2. Pearson's Correlation Coefficient ⭐

**Definition:**
$$r_{XY} = \frac{S_{XY}}{\sqrt{S_{XX} \cdot S_{YY}}}$$

where:
$$S_{XY} = \sum_{i=1}^n (x_i - \bar{x})(y_i - \bar{y}), \quad S_{XX} = \sum_{i=1}^n (x_i - \bar{x})^2, \quad S_{YY} = \sum_{i=1}^n (y_i - \bar{y})^2$$

**Range:** $-1 \leq r_{XY} \leq 1$

**Interpretation:**

- $r \approx +1$: Strong positive linear relationship
- $r \approx -1$: Strong negative linear relationship
- $r \approx 0$: No linear relationship (may still have non-linear)

**Limitations:** ⭐

- Measures only **linear** association
- Sensitive to outliers
- High $|r|$ does not confirm linear relationship (Anscombe's quartet — 4 datasets with identical $r$ but very different patterns)
- Low $r$ does not mean no relationship (could be non-linear)

**Anscombe's Quartet Warning:** ⭐
All 4 datasets have $r \approx 0.816$ but only dataset 1 has a true linear relationship. **Always plot the data!**

---

### 3. Spearman Rank Correlation ⭐

**When to use:** When data is ordinal OR when non-linear monotone relationship exists.

**Procedure:**

1. Rank all $x$ values (tied values get average rank)
2. Rank all $y$ values
3. Compute $d_i$ = difference in ranks for each pair
4. Apply formula:

$$r_s = 1 - \frac{6\sum d_i^2}{n(n^2-1)}$$

**Range:** $-1 \leq r_s \leq 1$

**Advantage over Pearson:** Can detect monotone non-linear relationships.

---

### 4. Kendall's Rank Correlation ⭐

**Concepts:**

- **Concordant pair:** $(x_1 > x_2)$ and $(y_1 > y_2)$, or $(x_1 < x_2)$ and $(y_1 < y_2)$
- **Discordant pair:** $(x_1 > x_2)$ and $(y_1 < y_2)$, or vice versa

$$\tau = \frac{\text{Concordant pairs} - \text{Discordant pairs}}{\frac{n(n-1)}{2}}$$

**Range:** $-1 \leq \tau \leq 1$

**Use:** Ordinal variables (e.g., expert rankings, survey scales)

---

### 5. Comparison of Correlation Measures ⭐

| Feature               | Pearson                  | Spearman           | Kendall                        |
| --------------------- | ------------------------ | ------------------ | ------------------------------ |
| Data type             | Continuous               | Ordinal/Continuous | Ordinal/Continuous             |
| Relationship detected | Linear only              | Monotone           | Monotone                       |
| Robust to outliers    | No                       | Somewhat           | Somewhat                       |
| Application           | Regression preprocessing | Ranked data        | Small samples, expert rankings |

---

### 6. Worked Example

**Anscombe Dataset:**

- All 4 datasets: Pearson $r \approx 0.816$, same regression line, same $R^2$
- Dataset 1: linear → model valid
- Dataset 2: non-linear → linear model inadequate
- Dataset 3: linear with one outlier
- Dataset 4: poor design — only 2 distinct $x$ values

**Lesson:** Numerical measures alone are insufficient — always visualize.

---

### 7. Examination Focus

- ⭐ Pearson's formula and interpretation
- ⭐ Anscombe's quartet — why visualization matters
- ⭐ Difference between Pearson, Spearman, Kendall
- ⭐ Spearman formula $r_s = 1 - \frac{6\sum d_i^2}{n(n^2-1)}$
- **Common mistake:** Concluding causation from correlation
- **Key fact:** $r = 0$ does NOT mean no relationship

---

### 8. Summary

- Pearson: linear association, continuous data, sensitive to outliers
- Spearman: monotone association, ordinal data, rank-based
- Kendall: concordant/discordant pairs, ordinal data
- Always plot scatter plot before computing correlation
- High correlation ≠ linear relationship (Anscombe's quartet)

---

---

# MASTER FORMULA SHEET — PROBABILITY & STATISTICS

---

## P&C Formulas ⭐

$${}^nP_r = \frac{n!}{(n-r)!}, \qquad {}^nC_r = \frac{n!}{r!(n-r)!}$$

$$\text{Circular} = (n-1)!, \qquad \text{Necklace} = \frac{(n-1)!}{2}$$

$$\text{Repeated objects} = \frac{n!}{p! \cdot q! \cdot r!}, \qquad \text{Diagonals} = \frac{n(n-3)}{2}$$

## Probability Formulas ⭐

$$P(A \cup B) = P(A) + P(B) - P(A \cap B)$$

$$P(A \mid B) = \frac{P(A \cap B)}{P(B)}, \qquad P(A \cap B) = P(A) \cdot P(B \mid A)$$

$$\text{Bayes}: P(A \mid B) = \frac{P(B \mid A) \cdot P(A)}{P(B)}$$

## Distributions ⭐

$$\text{Binomial}: P(X=k) = \binom{n}{k}p^k(1-p)^{n-k}, \quad \mu=np, \quad \sigma^2=np(1-p)$$

$$\text{Normal}: Z = \frac{X-\mu}{\sigma}, \quad X \sim N(\mu, \sigma^2)$$

## Statistics Formulas ⭐

$$\bar{x} = \frac{\sum x_i}{n}, \qquad s^2 = \frac{\sum(x_i - \bar{x})^2}{n-1}$$

$$\text{Var}(\bar{X}) = \frac{\sigma^2}{n}, \qquad \frac{(n-1)s^2}{\sigma^2} \sim \chi^2(n-1)$$

## Hypothesis Tests ⭐

$$Z = \frac{\bar{X} - \mu_0}{\sigma/\sqrt{n}}, \qquad T = \frac{\bar{X} - \mu_0}{s/\sqrt{n}} \sim t(n-1)$$

$$F = \frac{s_1^2}{s_2^2} \sim F(n_1-1, n_2-1)$$

## Correlation ⭐

$$r_{XY} = \frac{S_{XY}}{\sqrt{S_{XX} \cdot S_{YY}}}, \qquad r_s = 1 - \frac{6\sum d_i^2}{n(n^2-1)}$$

---

_End of Probability & Statistics Notes_

---

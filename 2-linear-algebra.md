---
# LINEAR ALGEBRA
## Complete Exam-Preparation Notes
### IIT M.Tech AI/ML Entrance Examination
---

## 2-WEEK STUDY PLAN — LINEAR ALGEBRA

| Day        | Topics                                                   | Activity                                         |
| ---------- | -------------------------------------------------------- | ------------------------------------------------ |
| **Day 1**  | Vectors — norms, dot product, Cauchy-Schwarz             | Read notes + solve 10 questions                  |
| **Day 2**  | Linear independence, Gram-Schmidt, Four subspaces        | Read notes + solve 10 questions                  |
| **Day 3**  | Matrices — types, transpose, inverse, determinant        | Read notes + solve 10 questions                  |
| **Day 4**  | Trace, matrix multiplication (row/column picture)        | Read notes + solve 10 questions                  |
| **Day 5**  | Rank, null space, RREF, Rank-Nullity theorem             | Read notes + solve 15 questions                  |
| **Day 6**  | Solving Ax = b — all 3 cases, consistency                | Read notes + solve 10 questions                  |
| **Day 7**  | **REVISION DAY** — Vectors + Matrices + Rank             | Redo all solved examples. Formula sheet revision |
| **Day 8**  | Least squares, pseudo-inverse, normal equations          | Read notes + solve 10 questions                  |
| **Day 9**  | Distances, projection onto vector, projection matrix     | Read notes + solve 10 questions                  |
| **Day 10** | Eigenvalues and eigenvectors — finding them              | Read notes + solve 10 questions                  |
| **Day 11** | Spectral theorem, eigendecomposition, PCA                | Read notes + solve 10 questions                  |
| **Day 12** | SVD — structure, singular values, low-rank approximation | Read notes + solve 10 questions                  |
| **Day 13** | **FULL REVISION** — All topics, tips & tricks            | Go through Quick Reference Card only             |
| **Day 14** | **MOCK TEST DAY**                                        | Attempt full sample paper under timed conditions |

**Daily time commitment:** 2–3 hours
**Priority order:** Rank/Null Space → Eigenvalues → Equations → Projections → SVD/PCA → Vectors/Matrices

---

---

# PART 1 — VECTORS AND VECTOR SPACES

---

## 1.1 What is a Vector?

**Definition:**
A vector is a column of n real numbers representing a point or direction in n-dimensional space.

$$\mathbf{v} = \begin{bmatrix} v_1 \\ v_2 \\ \vdots \\ v_n \end{bmatrix} \in \mathbb{R}^n$$

**In ML:** Every data point is a vector. A student with marks in 5 subjects is a vector in $\mathbb{R}^5$.

**Vector Space $\mathbb{R}^n$:**
A set is a vector space if it is closed under:

- Addition: $\mathbf{u} + \mathbf{v} \in V$
- Scalar multiplication: $\alpha\mathbf{u} \in V$
- Must contain the zero vector **0**

---

## 1.2 Norms — Measuring Length ⭐

| Norm     | Formula                                  | ML Use                  |
| -------- | ---------------------------------------- | ----------------------- |
| **L₁**   | $\|\mathbf{v}\|_1 = \sum_i \|v_i\|$      | Lasso, sparse solutions |
| **L₂** ★ | $\|\mathbf{v}\|_2 = \sqrt{\sum_i v_i^2}$ | Ridge, k-NN, k-Means    |
| **L∞**   | $\|\mathbf{v}\|_\infty = \max_i \|v_i\|$ | Chebyshev distance      |

**Ordering relation:** $\|\mathbf{v}\|_\infty \leq \|\mathbf{v}\|_2 \leq \|\mathbf{v}\|_1 \leq \sqrt{n}\|\mathbf{v}\|_\infty$

**Unit vector:** $\hat{\mathbf{v}} = \mathbf{v}/\|\mathbf{v}\|_2$

### Worked Example ⭐

**v = [3, −4, 0, 2]ᵀ**

- $\|\mathbf{v}\|_1 = 3 + 4 + 0 + 2 = 9$
- $\|\mathbf{v}\|_2 = \sqrt{9 + 16 + 0 + 4} = \sqrt{29} \approx 5.39$
- $\|\mathbf{v}\|_\infty = \max(3, 4, 0, 2) = 4$

**Exam trick:** [3,4] → norm = 5 (3-4-5 triple). [5,12] → norm = 13 (5-12-13 triple).

> **! NOTE:** $\|\mathbf{v}\|_2 \leq \|\mathbf{v}\|_1$ always. A common MCQ trap is reporting $\|\mathbf{v}\|_1$ as $\|\mathbf{v}\|_2$.

---

## 1.3 Dot Product ⭐

$$\mathbf{u} \cdot \mathbf{v} = \mathbf{u}^T\mathbf{v} = \sum_i u_i v_i = \|\mathbf{u}\|_2 \cdot \|\mathbf{v}\|_2 \cdot \cos\theta$$

**Geometric meaning:** Measures how much two vectors point in the same direction.

**Orthogonality:** $\mathbf{u} \perp \mathbf{v} \iff \mathbf{u}^T\mathbf{v} = 0$

**Cauchy-Schwarz Inequality:** ⭐
$$|\mathbf{u}^T\mathbf{v}| \leq \|\mathbf{u}\|_2 \cdot \|\mathbf{v}\|_2$$

Equality holds if and only if $\mathbf{u} = \alpha\mathbf{v}$ (vectors are parallel).

**Consequence:** $-1 \leq \cos\theta \leq 1$ — angle between vectors is always well-defined.

### Worked Example ⭐

**u = [1, 2, −2]ᵀ, v = [2, −1, 2]ᵀ**

- $\mathbf{u}^T\mathbf{v} = 2 - 2 - 4 = -4$
- $\|\mathbf{u}\| = \sqrt{1+4+4} = 3$, $\|\mathbf{v}\| = \sqrt{4+1+4} = 3$
- Cauchy-Schwarz check: $|-4| = 4 \leq 3 \times 3 = 9$ ✓
- Angle: $\cos\theta = -4/9 \implies \theta \approx 116.4°$

> **! NOTE:** $\mathbf{u} \cdot \mathbf{v} = 0$ means ORTHOGONAL (perpendicular), NOT linearly dependent. Orthogonal non-zero vectors are always linearly INDEPENDENT. This is a classic trap.

---

## 1.4 Linear Independence ⭐

**Definition:**
Vectors $\mathbf{v}_1, \mathbf{v}_2, \ldots, \mathbf{v}_k$ are **linearly independent** if:
$$\alpha_1\mathbf{v}_1 + \alpha_2\mathbf{v}_2 + \cdots + \alpha_k\mathbf{v}_k = \mathbf{0} \implies \alpha_1 = \alpha_2 = \cdots = \alpha_k = 0$$

**Three equivalent conditions:** ⭐

1. Only trivial solution to $\sum \alpha_i \mathbf{v}_i = \mathbf{0}$
2. No vector can be written as a combination of the others
3. Matrix $[\mathbf{v}_1 | \mathbf{v}_2 | \cdots | \mathbf{v}_k]$ has **rank k** (full column rank)

**Quick test for 3 vectors:** Form $A = [\mathbf{v}_1 | \mathbf{v}_2 | \mathbf{v}_3]$ and compute $\det(A)$.

- $\det(A) \neq 0 \implies$ linearly independent
- $\det(A) = 0 \implies$ linearly dependent

### Worked Example ⭐

**v₁ = [1,2,1]ᵀ, v₂ = [0,1,1]ᵀ, v₃ = [1,1,0]ᵀ**

$$\det\begin{bmatrix}1&0&1\\2&1&1\\1&1&0\end{bmatrix} = 1(0-1) - 0 + 1(2-1) = -1 + 1 = 0$$

$\det = 0 \implies$ **LINEARLY DEPENDENT**. Verify: $\mathbf{v}_1 = \mathbf{v}_2 + \mathbf{v}_3$ ✓

---

## 1.5 Gram-Schmidt Orthogonalisation

**Purpose:** Given linearly independent vectors, produce an **orthonormal basis** — vectors that are mutually perpendicular and each have unit length.

**Algorithm:**

$$\mathbf{q}_1 = \frac{\mathbf{a}_1}{\|\mathbf{a}_1\|}$$

$$\mathbf{u}_2 = \mathbf{a}_2 - (\mathbf{a}_2^T\mathbf{q}_1)\mathbf{q}_1, \quad \mathbf{q}_2 = \frac{\mathbf{u}_2}{\|\mathbf{u}_2\|}$$

$$\mathbf{u}_3 = \mathbf{a}_3 - (\mathbf{a}_3^T\mathbf{q}_1)\mathbf{q}_1 - (\mathbf{a}_3^T\mathbf{q}_2)\mathbf{q}_2, \quad \mathbf{q}_3 = \frac{\mathbf{u}_3}{\|\mathbf{u}_3\|}$$

**Intuition:** At each step, subtract away all components along previously computed basis vectors, then normalise.

### Worked Example ⭐

**a₁ = [1,1]ᵀ, a₂ = [2,0]ᵀ**

**Step 1:** $\|\mathbf{a}_1\| = \sqrt{2}$, so $\mathbf{q}_1 = [1,1]^T/\sqrt{2}$

**Step 2:** Remove q₁ component from a₂:

$$\mathbf{a}_2^T\mathbf{q}_1 = \frac{2+0}{\sqrt{2}} = \sqrt{2}$$

$$\mathbf{u}_2 = [2,0]^T - \sqrt{2} \cdot [1/\sqrt{2}, 1/\sqrt{2}]^T = [2,0]^T - [1,1]^T = [1,-1]^T$$

$$\mathbf{q}_2 = [1,-1]^T/\sqrt{2}$$

**Verify:** $\mathbf{q}_1^T\mathbf{q}_2 = \frac{1}{2} - \frac{1}{2} = 0$ ✓

---

## 1.6 The Four Fundamental Subspaces ⭐

For matrix $A$ (m×n, rank r):

| Subspace                     | Definition           | Dimension | Lives in       |
| ---------------------------- | -------------------- | --------- | -------------- |
| **Column space** col(A)      | Span of columns of A | r         | $\mathbb{R}^m$ |
| **Null space** null(A)       | {x : Ax = 0}         | n − r     | $\mathbb{R}^n$ |
| **Row space** row(A)         | Span of rows of A    | r         | $\mathbb{R}^n$ |
| **Left null space** null(Aᵀ) | {y : Aᵀy = 0}        | m − r     | $\mathbb{R}^m$ |

**Orthogonality relationships:** ⭐

- col(A) ⊥ null(Aᵀ)
- row(A) ⊥ null(A)

**Example (A is 3×5, rank 2):**

- dim(col(A)) = 2, dim(null(A)) = 3, dim(row(A)) = 2, dim(null(Aᵀ)) = 1

---

## Summary — Part 1

- **L₁, L₂, L∞ norms:** know formulas and ordering $\|\mathbf{v}\|_\infty \leq \|\mathbf{v}\|_2 \leq \|\mathbf{v}\|_1$
- **Dot product = 0 → orthogonal → independent** (not dependent!)
- **Cauchy-Schwarz:** $|\mathbf{u}^T\mathbf{v}| \leq \|\mathbf{u}\|\|\mathbf{v}\|$
- **Linear independence → det ≠ 0**
- **Gram-Schmidt:** subtract projections, then normalise
- **Four subspaces:** dimensions add up using rank-nullity

---

---

# PART 2 — MATRICES

---

## 2.1 Key Matrix Types ⭐

| Type | Property | Key Fact |
|------|----------|---------|
| **Square** | m = n | Can have inverse |
| **Symmetric** | $A = A^T$ | All eigenvalues real; eigenvectors orthogonal |
| **Orthogonal** | $Q^TQ = I$ | $Q^{-1} = Q^T$; $\lvert\det(Q)\rvert = 1$; preserves lengths. EVal not always real |
| **Diagonal** | Non-zero only on diagonal | Eigenvalues = diagonal entries |
| **Idempotent** | $P^2 = P$ | Eigenvalues are 0 or 1 only; rank = trace |
| **Positive Definite** | $\mathbf{x}^TA\mathbf{x} > 0 \ \forall\mathbf{x}\neq\mathbf{0}$ | All eigenvalues > 0; always invertible |
---

## 2.2 Transpose Properties ⭐

$$(AB)^T = B^T A^T \quad \text{(order REVERSES)}$$
$$(A + B)^T = A^T + B^T$$
$$(A^T)^T = A$$

> **! NOTE:** Most common exam trap: writing $(AB)^T = A^T B^T$. **WRONG.** Order always reverses.
> Memory trick: "Take off shoes and socks — socks first, then shoes. To put back: shoes first. Reverse order."

---

## 2.3 Inverse Properties ⭐

$$(AB)^{-1} = B^{-1}A^{-1} \quad \text{(order REVERSES)}$$
$$(A^T)^{-1} = (A^{-1})^T$$
$$(A^{-1})^{-1} = A$$

**A has an inverse if and only if:** $\det(A) \neq 0 \iff$ rank(A) = n $\iff$ no eigenvalue is zero.

---

## 2.4 Determinant ⭐

**Key properties:**

| Property    | Formula                                                   |
| ----------- | --------------------------------------------------------- |
| Product     | $\det(AB) = \det(A)\cdot\det(B)$                          |
| Transpose   | $\det(A^T) = \det(A)$                                     |
| Inverse     | $\det(A^{-1}) = 1/\det(A)$                                |
| Scalar      | $\det(cA) = c^n \det(A)$ for n×n matrix                   |
| Eigenvalues | $\det(A) = \lambda_1 \cdot \lambda_2 \cdots \lambda_n$ ⭐ |

**Row operation effects on det:**

- Swap two rows → det changes sign
- Multiply a row by scalar c → det multiplied by c
- Add a multiple of one row to another → det **unchanged**

**For upper triangular matrix:** det = product of diagonal entries ⭐

### Worked Example ⭐

$$A = \begin{bmatrix}2&1&-1\\0&3&2\\1&-1&4\end{bmatrix}$$

Row-reduce to upper triangular (no swaps):

- $R_3 \leftarrow R_3 - \frac{1}{2}R_1$: gives diagonal $[2, 3, \frac{11}{2}]$

$$\det(A) = 2 \times 3 \times \frac{11}{2} = 33$$

---

## 2.5 Trace ⭐

$$\text{tr}(A) = \sum_i A_{ii} = \sum_i \lambda_i \quad \text{(sum of diagonal entries = sum of eigenvalues)}$$

**Key properties:**

- $\text{tr}(AB) = \text{tr}(BA)$ — cyclic property ⭐
- $\text{tr}(A^k) = \sum_i \lambda_i^k$
- $\|A\|_F^2 = \text{tr}(A^TA)$ — Frobenius norm via trace

### Quick Example ⭐

Eigenvalues of A are 2, −1, 4:

- $\text{tr}(A) = 2 + (-1) + 4 = 5$
- $\det(A) = 2 \times (-1) \times 4 = -8$
- $\text{tr}(A^2) = 4 + 1 + 16 = 21$

---

## 2.6 Matrix-Vector Product — Two Pictures ⭐

$$A\mathbf{x} = \begin{bmatrix}\mathbf{r}_1^T\\\mathbf{r}_2^T\\\vdots\end{bmatrix}\mathbf{x}$$

**Row picture:** $(A\mathbf{x})_i = (\text{row }i\text{ of }A)^T \cdot \mathbf{x}$

**Column picture:** ⭐ (Most important for understanding)

$$A\mathbf{x} = x_1\mathbf{a}_1 + x_2\mathbf{a}_2 + \cdots + x_n\mathbf{a}_n$$

$A\mathbf{x}$ is a **linear combination of the columns of A**, with the entries of x as coefficients.

**Key implication:** $A\mathbf{x} = \mathbf{b}$ is solvable **if and only if** $\mathbf{b} \in \text{col}(A)$.

### Worked Example ⭐

$$A = \begin{bmatrix}2&1\\-1&3\\4&0\end{bmatrix}, \quad \mathbf{x} = \begin{bmatrix}2\\-1\end{bmatrix}$$

**Column picture:** $2\begin{bmatrix}2\\-1\\4\end{bmatrix} + (-1)\begin{bmatrix}1\\3\\0\end{bmatrix} = \begin{bmatrix}4\\-2\\8\end{bmatrix} - \begin{bmatrix}1\\3\\0\end{bmatrix} = \begin{bmatrix}3\\-5\\8\end{bmatrix}$

---

## 2.7 Linear Transformations

Every matrix $A$ defines a linear transformation $T(\mathbf{x}) = A\mathbf{x}$ mapping $\mathbb{R}^n \to \mathbb{R}^m$.

**Properties:**

- $T(\mathbf{u} + \mathbf{v}) = T(\mathbf{u}) + T(\mathbf{v})$
- $T(\alpha\mathbf{u}) = \alpha T(\mathbf{u})$

**Important:** $T(\mathbf{x}) = A\mathbf{x}$ is **linear**. $T(\mathbf{x}) = A\mathbf{x} + \mathbf{b}$ is **affine** (not linear, used in neural networks).

**Common 2D transformations:**

| Transformation         | Matrix                                                                          |
| ---------------------- | ------------------------------------------------------------------------------- |
| Rotation by θ          | $\begin{bmatrix}\cos\theta & -\sin\theta\\\sin\theta & \cos\theta\end{bmatrix}$ |
| Reflection over x-axis | $\begin{bmatrix}1&0\\0&-1\end{bmatrix}$                                         |
| Projection onto x-axis | $\begin{bmatrix}1&0\\0&0\end{bmatrix}$                                          |

---

## Summary — Part 2

- $(AB)^T = B^TA^T$, $(AB)^{-1} = B^{-1}A^{-1}$ — order **always reverses**
- $\det(cA) = c^n\det(A)$; upper triangular det = product of diagonal
- $\text{tr}(A) = \sum\lambda_i$; $\det(A) = \prod\lambda_i$ ⭐
- Column picture: $A\mathbf{x}$ = linear combination of columns of A
- Orthogonal Q: $Q^{-1} = Q^T$, $|\det(Q)| = 1$

---

---

# PART 3 — RANK AND NULL SPACE

---

## 3.1 Row Reduction and RREF ⭐

**Three allowed row operations** (do not change solutions or rank):

1. Swap two rows
2. Multiply a row by a nonzero scalar
3. Add a multiple of one row to another

**Reduced Row Echelon Form (RREF):**

- Pivots equal to 1
- Zeros everywhere else in pivot columns
- Each pivot to the right of the pivot above
- Zero rows at the bottom

**Rank** = number of pivots = number of linearly independent rows = number of linearly independent columns.

### Worked Example ⭐

$$A = \begin{bmatrix}0&1&2&1\\1&2&1&0\\2&5&4&1\end{bmatrix}$$

Row reduce → RREF:

$$\text{RREF} = \begin{bmatrix}1&0&-3&-2\\0&1&2&1\\0&0&0&0\end{bmatrix}$$

- Pivot columns: 1 and 2. Free columns: 3 and 4.
- **rank(A) = 2**, **nullity(A) = 4 − 2 = 2**

---

## 3.2 Null Space ⭐

**Definition:** $\text{null}(A) = \{\mathbf{x} : A\mathbf{x} = \mathbf{0}\}$

The null space is always a **subspace**. It contains all "invisible" directions — inputs that produce zero output.

**How to find it:** From RREF, express pivot variables in terms of free variables.

### Worked Example ⭐ (continued from above)

From RREF:
$$x_1 - 3x_3 - 2x_4 = 0 \implies x_1 = 3x_3 + 2x_4$$
$$x_2 + 2x_3 + x_4 = 0 \implies x_2 = -2x_3 - x_4$$

Let $x_3 = s$, $x_4 = t$ (free variables):


$$\mathbf{x} = \begin{bmatrix}x_1\\x_2\\x_3\\x_4\end{bmatrix} = \begin{bmatrix}3s+2t\\-2s-t\\s\\t\end{bmatrix}$$

$$\mathbf{x} = s\begin{bmatrix}3\\-2\\1\\0\end{bmatrix} + t\begin{bmatrix}2\\-1\\0\\1\end{bmatrix}$$

$$\text{null}(A) = \text{span}\left\{\begin{bmatrix}3\\-2\\1\\0\end{bmatrix}, \begin{bmatrix}2\\-1\\0\\1\end{bmatrix}\right\}$$

---

## 3.3 Rank-Nullity Theorem ⭐

$$\boxed{\text{rank}(A) + \text{nullity}(A) = n \quad (n = \text{number of columns})}$$

**Intuition:** Of the n input dimensions, rank dimensions map to output. The remaining nullity dimensions are "collapsed" to zero.

| rank(A)           | nullity(A) | Interpretation                                        |
| ----------------- | ---------- | ----------------------------------------------------- |
| n (full col rank) | 0          | null = {0}; Ax=b: at most 1 solution                  |
| m (full row rank) | n−m        | Ax=b always consistent; if n>m: ∞ solutions           |
| r < min(m,n)      | n−r        | Ax=b: may be inconsistent; if consistent: ∞ solutions |

### Quick Example ⭐

**A is 5×8 with rank(A) = 3. Find:**

- nullity(A) = 8 − 3 = **5**
- dim(col(A)) = **3**
- dim(null(Aᵀ)) = 5 − 3 = **2**

**Exam shortcut:** "A is m×n with rank r. How many free variables in Ax=0?" → Answer: **n − r**. Instantly.

> **! NOTE:** rank(A) = rank(Aᵀ) ALWAYS. This is the row rank = column rank theorem. A very common MCQ trap is thinking they differ for non-square matrices.

---

## Summary — Part 3

- RREF: pivots = 1, zeros elsewhere in pivot columns
- Rank = number of pivots
- Null space: set free variables, express pivots, write as span
- **Rank + Nullity = n** (number of columns)
- dim(col(A)) = rank; dim(null(Aᵀ)) = m − rank
- rank(A) = rank(Aᵀ) always

---

---

# PART 4 — SOLVING LINEAR EQUATIONS

---

## 4.1 The Three Cases for Ax = b ⭐

$$A\mathbf{x} = \mathbf{b}$$

**Consistency condition:** Ax = b has a solution if and only if:
$$\text{rank}(A) = \text{rank}([A|\mathbf{b}])$$

Equivalently: **b must be in the column space of A**.

### Case 1 — Unique Solution ⭐

- rank(A) = n (full column rank) AND system is consistent
- null(A) = {0}, so no freedom in the solution
- If A is square: unique solution is $\mathbf{x} = A^{-1}\mathbf{b}$

### Case 2 — No Solution

- rank(A) < rank([A|b])
- b is NOT in col(A)
- Occurs when: A is tall (overdetermined) and b doesn't fit exactly

### Case 3 — Infinitely Many Solutions ⭐

- System is consistent AND rank(A) < n
- dim(null(A)) = n − rank(A) > 0
- General solution: $\mathbf{x} = \mathbf{x}_p + \mathbf{x}_n$ where $\mathbf{x}_p$ is any particular solution and $\mathbf{x}_n \in \text{null}(A)$

> **! NOTE:** det(A) = 0 does NOT always mean no solution. It means either NO solution or INFINITELY MANY. Which one depends on whether b ∈ col(A).

### Worked Example ⭐ — All Three Cases visible

$$A = \begin{bmatrix}1&2&1\\2&4&3\\3&6&4\end{bmatrix}, \quad \mathbf{b} = \begin{bmatrix}3\\7\\10\end{bmatrix}$$

Row reduce augmented matrix [A|b]:

$$\text{RREF}: \begin{bmatrix}1&2&0&|&2\\0&0&1&|&1\\0&0&0&|&0\end{bmatrix}$$

rank(A) = rank([A|b]) = 2 → **CONSISTENT**. Free variable: $x_2 = t$

**Row 1:** $1\cdot x_1 + 2\cdot x_2 + 0\cdot x_3 = 2$

$$x_1 + 2x_2 = 2$$

**Row 2:** $0\cdot x_1 + 0\cdot x_2 + 1\cdot x_3 = 1$

$$x_3 = 1$$

**Row 3:** $0 = 0$ — no information, discard.

$$x_1 = 2 - 2t, \quad x_3 = 1$$

**Particular solution** (t=0): $\mathbf{x}_p = [2, 0, 1]^T$

**Null space basis:** $\mathbf{x}_n = t[-2, 1, 0]^T$

$$\boxed{\mathbf{x} = \begin{bmatrix}2\\0\\1\end{bmatrix} + t\begin{bmatrix}-2\\1\\0\end{bmatrix}, \quad t \in \mathbb{R}}$$

**Infinitely many solutions** (Case 3).

---

## 4.2 Least Squares and Pseudo-Inverse ⭐

**When:** A is tall (m > n) and $\mathbf{b} \notin \text{col}(A)$ — no exact solution exists.

**Goal:** Find $\mathbf{x}^*$ that minimises $\|A\mathbf{x} - \mathbf{b}\|_2^2$

**Geometric view:** ⭐

- $A\mathbf{x}^*$ is the **projection of b onto col(A)**
- The residual $\mathbf{e} = \mathbf{b} - A\mathbf{x}^*$ is **perpendicular to every column of A**
- Setting $A^T(\mathbf{b} - A\mathbf{x}^*) = \mathbf{0}$ gives the **Normal Equations:**

$$\boxed{A^TA\mathbf{x}^* = A^T\mathbf{b}}$$

**Pseudo-inverse solution** (when A has full column rank):

$$\mathbf{x}^* = (A^TA)^{-1}A^T\mathbf{b} = A^+\mathbf{b}$$

**When is $A^TA$ invertible?** ⭐
$$A^TA \text{ is invertible} \iff A \text{ has full column rank} \iff \text{null}(A) = \{\mathbf{0}\}$$

**When features are collinear (multicollinearity):** $A^TA$ is singular. Fix with **Ridge regression:**

$$\mathbf{x}^* = (A^TA + \lambda I)^{-1}A^T\mathbf{b} \quad (\lambda > 0 \text{ always makes it invertible})$$

### Worked Example ⭐ — Fitting a Line

**Data:** (1,3), (2,5), (3,6), (4,8), (5,9). Fit ŷ = mx + c.

$$A = \begin{bmatrix}1&1\\2&1\\3&1\\4&1\\5&1\end{bmatrix}, \quad \mathbf{b} = \begin{bmatrix}3\\5\\6\\8\\9\end{bmatrix}$$

$$A^TA = \begin{bmatrix}55&15\\15&5\end{bmatrix}, \quad A^T\mathbf{b} = \begin{bmatrix}108\\31\end{bmatrix}$$

$$\det(A^TA) = 275 - 225 = 50$$

$$(A^TA)^{-1} = \frac{1}{50}\begin{bmatrix}5&-15\\-15&55\end{bmatrix}$$

$$\begin{bmatrix}m\\c\end{bmatrix} = \frac{1}{50}\begin{bmatrix}5&-15\\-15&55\end{bmatrix}\begin{bmatrix}108\\31\end{bmatrix} = \frac{1}{50}\begin{bmatrix}75\\85\end{bmatrix} = \begin{bmatrix}1.5\\1.7\end{bmatrix}$$

**Best fit line: ŷ = 1.5x + 1.7**

---

## 4.3 Pseudo-Inverse — Three Cases ⭐

| Case                | Condition       | Formula                                                   |
| ------------------- | --------------- | --------------------------------------------------------- |
| Square, invertible  | rank = n = m    | $\mathbf{x}^* = A^{-1}\mathbf{b}$                         |
| Tall, full col rank | m > n, rank = n | $\mathbf{x}^* = (A^TA)^{-1}A^T\mathbf{b}$ (least squares) |
| Wide, full row rank | m < n, rank = m | $\mathbf{x}^* = A^T(AA^T)^{-1}\mathbf{b}$ (min norm)      |
| General             | any             | $\mathbf{x}^* = A^+\mathbf{b}$ via SVD                    |

---

## Summary — Part 4

- Consistent iff rank(A) = rank([A|b]) iff b ∈ col(A)
- Unique solution: full col rank; No solution: b ∉ col(A); Infinite: consistent + null(A) ≠ {0}
- General solution = particular solution + null space
- Normal equations: $A^TA\mathbf{x}^* = A^T\mathbf{b}$
- $A^TA$ invertible iff A has full column rank
- Ridge regression: $(A^TA + \lambda I)^{-1}A^T\mathbf{b}$ — always works for λ > 0

---

---

# PART 5 — DISTANCES AND PROJECTIONS

---

## 5.1 Distance Metrics ⭐

| Metric | Formula | ML Use |
|--------|---------|--------|
| **Euclidean** ★ | $\|\mathbf{u}-\mathbf{v}\|_2 = \sqrt{\sum_i(u_i-v_i)^2}$ | k-NN, k-Means, clustering |
| **Manhattan** | $\|\mathbf{u}-\mathbf{v}\|_1 = \sum_i \lvert u_i-v_i \rvert$ | Sparse data, grid paths |
| **Cosine** | $1 - \frac{\mathbf{u}^T\mathbf{v}}{\lVert\mathbf{u}\rVert\lVert\mathbf{v}\rVert}$ | NLP: document similarity |
| **Mahalanobis** | $\sqrt{(\mathbf{u}-\mathbf{v})^T\Sigma^{-1}(\mathbf{u}-\mathbf{v})}$ | Accounts for correlations |

### Worked Example ⭐

**u = [1,3,−2]ᵀ, v = [4,1,2]ᵀ**

- Euclidean: $\sqrt{9+4+16} = \sqrt{29} \approx 5.39$
- Manhattan: $3+2+4 = 9$
- Cosine: $\mathbf{u}^T\mathbf{v} = 4+3-8 = -1$; $\|\mathbf{u}\|=\sqrt{14}$, $\|\mathbf{v}\|=\sqrt{21}$; $\cos\theta = -1/\sqrt{294} \approx -0.058$

---

## 5.2 Projection onto a Vector ⭐

**Formula:**

$$\text{proj}_\mathbf{a}(\mathbf{b}) = \frac{\mathbf{a}^T\mathbf{b}}{\mathbf{a}^T\mathbf{a}} \cdot \mathbf{a}$$

**Projection matrix onto span{a}:**

$$P = \frac{\mathbf{a}\mathbf{a}^T}{\mathbf{a}^T\mathbf{a}}$$

**Key properties of projection matrix P:** ⭐

| Property                                                              | Meaning                                         |
| --------------------------------------------------------------------- | ----------------------------------------------- |
| $P^2 = P$                                                             | Idempotent — projecting twice = projecting once |
| $P^T = P$                                                             | Symmetric                                       |
| Eigenvalues ∈ {0,1}                                                   | Only 0 and 1                                    |
| rank(P) = tr(P)                                                       | Rank equals trace                               |
| $\mathbf{e} = \mathbf{b} - P\mathbf{b}$: $\mathbf{a}^T\mathbf{e} = 0$ | Error perpendicular to a                        |
| $\|\mathbf{b}\|^2 = \|P\mathbf{b}\|^2 + \|\mathbf{e}\|^2$             | Pythagorean theorem                             |

### Worked Example ⭐

**Project b = [3,4]ᵀ onto a = [2,1]ᵀ**

$$\alpha = \frac{\mathbf{a}^T\mathbf{b}}{\mathbf{a}^T\mathbf{a}} = \frac{6+4}{4+1} = \frac{10}{5} = 2$$

$$\mathbf{p} = 2 \cdot [2,1]^T = [4,2]^T$$

**Error:** $\mathbf{e} = [3,4]^T - [4,2]^T = [-1,2]^T$

**Verify:** $\mathbf{a}^T\mathbf{e} = 2(-1) + 1(2) = 0$ ✓

**Pythagoras:** $\|\mathbf{p}\|^2 + \|\mathbf{e}\|^2 = 20 + 5 = 25 = \|\mathbf{b}\|^2$ ✓

> **! NOTE:** Do not confuse projection onto a **vector** with projection onto a **subspace**. For a vector: use $\alpha = \mathbf{a}^T\mathbf{b}/\mathbf{a}^T\mathbf{a}$. For a subspace (column space of A): use $P = A(A^TA)^{-1}A^T$.

---

## 5.3 Projection onto a Subspace ⭐

**Projection matrix onto col(A):**

$$\boxed{P = A(A^TA)^{-1}A^T}$$

**Least squares solution:** $\mathbf{x}^* = (A^TA)^{-1}A^T\mathbf{b}$

**Projection of b onto col(A):** $\mathbf{p} = A\mathbf{x}^*$

**Residual:** $\mathbf{e} = \mathbf{b} - \mathbf{p}$, which satisfies $A^T\mathbf{e} = \mathbf{0}$ (residual ⊥ every column of A) ⭐

### Worked Example ⭐

$$A = \begin{bmatrix}1&0\\1&1\\0&1\end{bmatrix}, \quad \mathbf{b} = \begin{bmatrix}1\\2\\3\end{bmatrix}$$

$$A^TA = \begin{bmatrix}2&1\\1&2\end{bmatrix}, \quad (A^TA)^{-1} = \frac{1}{3}\begin{bmatrix}2&-1\\-1&2\end{bmatrix}$$

$$A^T\mathbf{b} = \begin{bmatrix}3\\5\end{bmatrix}, \quad \mathbf{x}^* = \frac{1}{3}\begin{bmatrix}2&-1\\-1&2\end{bmatrix}\begin{bmatrix}3\\5\end{bmatrix} = \frac{1}{3}\begin{bmatrix}1\\7\end{bmatrix}$$

$$\mathbf{p} = A\mathbf{x}^* = \begin{bmatrix}1/3\\8/3\\7/3\end{bmatrix}, \quad \mathbf{e} = \begin{bmatrix}2/3\\-2/3\\2/3\end{bmatrix}$$

**Verify:** $A^T\mathbf{e} = \mathbf{0}$ ✓

---

## Summary — Part 5

- Projection onto vector a: $\mathbf{p} = \frac{\mathbf{a}^T\mathbf{b}}{\mathbf{a}^T\mathbf{a}}\mathbf{a}$
- Projection matrix P: $P^2=P$, $P^T=P$, eigenvalues ∈ {0,1}, rank(P) = tr(P)
- Projection onto col(A): $P = A(A^TA)^{-1}A^T$
- Residual e = b − p always satisfies $A^T\mathbf{e} = \mathbf{0}$
- Pythagoras: $\|\mathbf{b}\|^2 = \|\mathbf{p}\|^2 + \|\mathbf{e}\|^2$

---

---

# PART 6 — EIGENVALUES AND EIGENVECTORS

---

## 6.1 Definition and Finding Eigenvalues ⭐

**Definition:** A non-zero vector **v** is an **eigenvector** of A with **eigenvalue** λ if:

$$A\mathbf{v} = \lambda\mathbf{v}$$

**Intuition:** Eigenvectors are the "special directions" that only get **scaled** (not rotated) by A.

**Algorithm — 4 Steps:** ⭐

**Step 1:** Write characteristic equation: $\det(A - \lambda I) = 0$

**Step 2:** Solve for λ — these are the **eigenvalues**

**Step 3:** For each $\lambda_i$, solve $(A - \lambda_i I)\mathbf{v} = \mathbf{0}$ for eigenvector $\mathbf{v}_i$

**Step 4:** Verify: $\text{tr}(A) = \sum\lambda_i$ and $\det(A) = \prod\lambda_i$ ⭐

### Worked Example ⭐

$$A = \begin{bmatrix}3&1\\1&3\end{bmatrix}$$

**Step 1:** $\det(A - \lambda I) = (3-\lambda)^2 - 1 = \lambda^2 - 6\lambda + 8 = (\lambda-2)(\lambda-4) = 0$

**Eigenvalues:** $\lambda_1 = 2$, $\lambda_2 = 4$

**Step 2 — Eigenvector for λ₁ = 2:**
$$(A - 2I)\mathbf{v} = \begin{bmatrix}1&1\\1&1\end{bmatrix}\mathbf{v} = \mathbf{0} \implies v_1 + v_2 = 0 \implies \mathbf{v}_1 = \frac{1}{\sqrt{2}}\begin{bmatrix}1\\-1\end{bmatrix}$$

**Step 3 — Eigenvector for λ₂ = 4:**
$$(A - 4I)\mathbf{v} = \begin{bmatrix}-1&1\\1&-1\end{bmatrix}\mathbf{v} = \mathbf{0} \implies v_1 = v_2 \implies \mathbf{v}_2 = \frac{1}{\sqrt{2}}\begin{bmatrix}1\\1\end{bmatrix}$$

**Step 4 — Verify:**

- tr(A) = 3 + 3 = 6 = 2 + 4 ✓
- det(A) = 9 − 1 = 8 = 2 × 4 ✓
- A is symmetric → eigenvectors are orthogonal: $\mathbf{v}_1^T\mathbf{v}_2 = \frac{1}{2} - \frac{1}{2} = 0$ ✓

---

## 6.2 Key Properties of Eigenvalues ⭐

**Eigenvalue inheritance:** If λ is an eigenvalue of A, then automatically:

| Matrix   | Eigenvalue                    |
| -------- | ----------------------------- |
| $A^k$    | $\lambda^k$                   |
| $A^{-1}$ | $1/\lambda$                   |
| $A + cI$ | $\lambda + c$                 |
| $cA$     | $c\lambda$                    |
| $A^T$    | $\lambda$ (same eigenvalues!) |

**Quick exam trick:** "Find tr(A⁵) given eigenvalues 2, −1, 3."
→ Eigenvalues of A⁵: $32, -1, 243$. tr(A⁵) = 32 − 1 + 243 = **274**

**Null vector:** The null vector **0** is NEVER an eigenvector (by definition). Zero CAN be an eigenvalue.

**Geometric multiplicity:** Number of linearly independent eigenvectors for eigenvalue λ = dim(null(A − λI))

---

## 6.3 Spectral Theorem and Eigendecomposition ⭐

**For any real symmetric matrix A:**

$$\boxed{A = Q\Lambda Q^T}$$

where:

- $Q$ = orthogonal matrix (columns = normalised eigenvectors)
- $\Lambda$ = diagonal matrix (diagonal entries = eigenvalues)
- $Q^TQ = QQ^T = I$

**Why important:** Symmetric matrices arise everywhere in ML — covariance matrices, kernel matrices, Gram matrices.

**Spectral decomposition (outer product form):** ⭐

$$A = \lambda_1\mathbf{v}_1\mathbf{v}_1^T + \lambda_2\mathbf{v}_2\mathbf{v}_2^T + \cdots + \lambda_n\mathbf{v}_n\mathbf{v}_n^T$$

**Power of A using eigendecomposition:** $A^k = Q\Lambda^k Q^T$ ⭐

### Worked Example ⭐

**For A = [[3,1],[1,3]] with eigenvalues 2,4 and eigenvectors from above:**

$$Q = \frac{1}{\sqrt{2}}\begin{bmatrix}1&1\\-1&1\end{bmatrix}, \quad \Lambda = \begin{bmatrix}2&0\\0&4\end{bmatrix}$$

**Compute A² using A² = QΛ²Qᵀ:**

$$\Lambda^2 = \begin{bmatrix}4&0\\0&16\end{bmatrix}$$

$$A^2 = \frac{1}{2}\begin{bmatrix}1&1\\-1&1\end{bmatrix}\begin{bmatrix}4&0\\0&16\end{bmatrix}\begin{bmatrix}1&-1\\1&1\end{bmatrix} = \begin{bmatrix}10&6\\6&10\end{bmatrix}$$

**Verify directly:** $A \cdot A = [[9+1, 3+3],[3+3, 1+9]] = [[10,6],[6,10]]$ ✓

---

## 6.4 PCA — Principal Component Analysis ⭐

**Purpose:** Reduce dimensionality while preserving maximum variance.

**Step-by-Step Algorithm:** ⭐

1. **Centre the data:** Subtract mean from each column of X
2. **Covariance matrix:** $C = \frac{X^TX}{n-1}$
3. **Eigendecompose:** $C = Q\Lambda Q^T$ — sort eigenvalues $\lambda_1 \geq \lambda_2 \geq \cdots \geq \lambda_n$
4. **Choose top k eigenvectors** (columns of Q): these are the Principal Components
5. **Project data:** $Z = XQ_k$ — reduced to k dimensions

**Variance explained by PCᵢ:** ⭐

$$\text{Variance explained by PC}_i = \frac{\lambda_i}{\lambda_1 + \lambda_2 + \cdots + \lambda_n}$$

**Cumulative (top k PCs):** $\frac{\lambda_1 + \cdots + \lambda_k}{\sum_i \lambda_i}$

### Worked Example ⭐

**Eigenvalues of covariance matrix: 12, 6, 3, 3. Total = 24.**

- PC₁ variance: 12/24 = **50%**
- PC₁ + PC₂ variance: 18/24 = **75%**
- PC₁ + PC₂ + PC₃ variance: 21/24 = **87.5%**

**Exam question pattern:** "How many PCs needed to explain 80% of variance?" → Cumulative sum ≥ 80% → answer: **2 PCs** (at 75% add PC₃ to get 87.5%, so 3 PCs for 80%+).

---

## 6.5 Singular Value Decomposition (SVD) ⭐

**For any m×n matrix A:**

$$\boxed{A = U\Sigma V^T}$$

| Component | Size | Description                                                                                 |
| --------- | ---- | ------------------------------------------------------------------------------------------- |
| U         | m×m  | Orthogonal; columns = left singular vectors (eigenvectors of AAᵀ)                           |
| Σ         | m×n  | Diagonal; $\sigma_i = \sqrt{\lambda_i}$ of AᵀA; $\sigma_1 \geq \sigma_2 \geq \cdots \geq 0$ |
| V         | n×n  | Orthogonal; columns = right singular vectors (eigenvectors of AᵀA)                          |

**Key facts:** ⭐

- rank(A) = number of non-zero singular values
- Works for **any** m×n matrix (unlike eigendecomposition which needs square A)
- **Low-rank approximation:** $A_k = \sum_{i=1}^k \sigma_i \mathbf{u}_i \mathbf{v}_i^T$ is the best rank-k approximation (Eckart-Young theorem)
- **Pseudo-inverse:** $A^+ = V\Sigma^+U^T$ where $\Sigma^+$ replaces each $\sigma_i \neq 0$ with $1/\sigma_i$

**SVD reduces to eigendecomposition** when A is symmetric positive semi-definite: then U = V = Q and $\sigma_i = \lambda_i$.

### Worked Example ⭐

$$A = \begin{bmatrix}3&0\\4&0\end{bmatrix}$$

$A^TA = \begin{bmatrix}25&0\\0&0\end{bmatrix}$ → eigenvalues: λ₁=25, λ₂=0 → **σ₁=5, σ₂=0**

V = I (eigenvectors of AᵀA are standard basis vectors)

$\mathbf{u}_1 = A\mathbf{v}_1/\sigma_1 = [3,4]^T/5 = [3/5, 4/5]^T$

$$A = \begin{bmatrix}3/5&4/5\\4/5&-3/5\end{bmatrix}\begin{bmatrix}5&0\\0&0\end{bmatrix}\begin{bmatrix}1&0\\0&1\end{bmatrix}$$

Verify: $U\Sigma V^T = [3,0;4,0] = A$ ✓

---

## Summary — Part 6

- Eigenvalues from $\det(A - \lambda I) = 0$; verify with tr and det
- tr(A) = Σλᵢ, det(A) = Πλᵢ ← **most used exam shortcuts**
- Symmetric A: all eigenvalues real; eigenvectors for different λ are orthogonal
- $A^k$: eigenvalues become $\lambda^k$; $A^{-1}$: eigenvalues become $1/\lambda$
- Eigendecomposition of symmetric A: $A = Q\Lambda Q^T$
- PCA: sort eigenvalues of covariance matrix; variance explained = λᵢ/Σλ
- SVD: $A = U\Sigma V^T$; works for any m×n matrix; rank = number of nonzero σ

---

---

# MASTER FORMULA SHEET — LINEAR ALGEBRA

## Vectors

$$\|\mathbf{v}\|_1 = \sum|v_i|, \quad \|\mathbf{v}\|_2 = \sqrt{\sum v_i^2}, \quad \|\mathbf{v}\|_\infty = \max|v_i|$$

$$\mathbf{u}^T\mathbf{v} = \|\mathbf{u}\|\|\mathbf{v}\|\cos\theta, \quad |\mathbf{u}^T\mathbf{v}| \leq \|\mathbf{u}\|\|\mathbf{v}\| \quad \text{(Cauchy-Schwarz)}$$

## Matrices

$$\det(AB) = \det(A)\det(B), \quad \det(cA) = c^n\det(A), \quad (AB)^T = B^TA^T$$

$$\text{tr}(A) = \sum\lambda_i, \quad \det(A) = \prod\lambda_i$$

## Rank and Null Space

$$\text{rank}(A) + \text{nullity}(A) = n \quad \text{(columns)}$$

$$\text{dim(col(A))} = \text{rank}, \quad \text{dim(null(}A^T)) = m - \text{rank}$$

## Solving Equations

$$\text{Consistent iff rank}(A) = \text{rank}([A|\mathbf{b}])$$

$$A^TA\mathbf{x}^* = A^T\mathbf{b} \quad \text{(Normal Equations)}, \quad \mathbf{x}^* = (A^TA)^{-1}A^T\mathbf{b}$$

## Projections

$$\text{proj}_\mathbf{a}(\mathbf{b}) = \frac{\mathbf{a}^T\mathbf{b}}{\mathbf{a}^T\mathbf{a}}\mathbf{a}, \quad P = \frac{\mathbf{a}\mathbf{a}^T}{\mathbf{a}^T\mathbf{a}}, \quad P = A(A^TA)^{-1}A^T$$

$$P^2 = P, \quad P^T = P, \quad \text{eigenvalues} \in \{0,1\}, \quad \text{rank}(P) = \text{tr}(P)$$

## Eigenvalues

$$A\mathbf{v} = \lambda\mathbf{v}, \quad \det(A - \lambda I) = 0$$

$$A = Q\Lambda Q^T \quad \text{(symmetric A)}, \quad A = U\Sigma V^T \quad \text{(any A)}$$

$$\text{PCA: variance explained by PC}_i = \frac{\lambda_i}{\sum_j \lambda_j}$$

## 13 Exam Tricks Quick Reference

| Trick                       | Rule                                                           |
| --------------------------- | -------------------------------------------------------------- |
| T1: Orthogonality           | $\mathbf{u}^T\mathbf{v} = 0 \iff$ orthogonal (NOT dependent)   |
| T2: Norm patterns           | [3,4]→5; [5,12]→13; [1,…,1] (n ones)→√n                        |
| T3: Trace/Det               | tr(A)=Σλᵢ; det(A)=Πλᵢ; tr(Aᵏ)=Σλᵢᵏ                             |
| T4: Matrix types            | Orthogonal:\|det\|=1; Symmetric: real λ; Idempotent: λ∈{0,1}   |
| T5: Rank by inspection      | Proportional rows→rank=1; det≠0→full rank                      |
| T6: Rank-Nullity            | nullity=n−rank; dim(null(Aᵀ))=m−rank                           |
| T7: Consistency             | Square det≠0→unique for all b; full row rank→always consistent |
| T8: Pseudo-inverse          | Tall→(AᵀA)⁻¹Aᵀb; Wide→Aᵀ(AAᵀ)⁻¹b                               |
| T9: Projection scalar       | α=aᵀb/aᵀa; for unit a: p=(aᵀb)a                                |
| T10: Projection properties  | P²=P, Pᵀ=P, rank(P)=tr(P)                                      |
| T11: Read eigenvalues       | Diagonal/triangular: eigenvalues = diagonal entries            |
| T12: Eigenvalue inheritance | Aᵏ:λᵏ; A⁻¹:1/λ; A+cI:λ+c; cA:cλ; Aᵀ:same λ                     |
| T13: PCA variance           | λᵢ/Σλⱼ per PC; cumulative for top k                            |

## 5 Common Traps

| Trap   | Wrong                                         | Correct                                                          |
| ------ | --------------------------------------------- | ---------------------------------------------------------------- |
| Trap 1 | $\mathbf{u}^T\mathbf{v}=0 \implies$ dependent | $\mathbf{u}^T\mathbf{v}=0 \implies$ orthogonal → **independent** |
| Trap 2 | $(AB)^T = A^TB^T$                             | $(AB)^T = B^TA^T$ (order reverses)                               |
| Trap 3 | rank(A) ≠ rank(Aᵀ)                            | rank(A) = rank(Aᵀ) **always**                                    |
| Trap 4 | det(A)=0 → no solution                        | det(A)=0 → no solution **or** ∞ solutions                        |
| Trap 5 | Use vector formula for subspace               | Use $P = A(A^TA)^{-1}A^T$ for subspace                           |

---

_End of Linear Algebra Notes_

---

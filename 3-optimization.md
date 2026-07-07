---
# OPTIMIZATION
## Complete Exam-Preparation Notes
### IIT M.Tech AI/ML Entrance Examination
---

## 2-WEEK STUDY PLAN — OPTIMIZATION

| Day        | Topics                                                                             | Activity                                  |
| ---------- | ---------------------------------------------------------------------------------- | ----------------------------------------- |
| **Day 1**  | Optimization fundamentals — objective function, local vs global, types of problems | Read notes + 8 questions                  |
| **Day 2**  | Convexity — convex sets, convex functions, why it matters                          | Read notes + 10 questions                 |
| **Day 3**  | Univariate optimization — first and second derivative tests                        | Read notes + 10 questions                 |
| **Day 4**  | Univariate — worked examples, Newton's method in 1D                                | Read notes + 10 questions                 |
| **Day 5**  | Multivariate — gradient, Hessian, critical points                                  | Read notes + 10 questions                 |
| **Day 6**  | Multivariate — second-order conditions (Hessian test)                              | Read notes + 10 questions                 |
| **Day 7**  | **REVISION DAY** — Univariate + Multivariate + Convexity                           | Redo all examples. Formula sheet revision |
| **Day 8**  | Gradient descent — algorithm, learning rate, convergence                           | Read notes + 10 questions                 |
| **Day 9**  | Gradient descent — numerical example step by step                                  | Manually trace through the full example   |
| **Day 10** | Gradient descent — variants (SGD, mini-batch), issues                              | Read notes + 10 questions                 |
| **Day 11** | Connection to ML — OLS, logistic regression, ridge                                 | Read notes + 10 questions                 |
| **Day 12** | Mixed review — all optimization topics                                             | Solve 15 mixed problems                   |
| **Day 13** | **FULL REVISION** — All topics, formula sheet                                      | Summary sections only                     |
| **Day 14** | **MOCK TEST DAY**                                                                  | Full sample paper under timed conditions  |

**Daily time commitment:** 2–3 hours
**Priority order:** Gradient Descent → Convexity → Multivariate Conditions → Univariate → Newton's Method

---

---

# PART 1 — INTRODUCTION TO OPTIMIZATION

---

## 1.1 What is Optimization? ⭐

**Definition:** Optimization is the process of finding the value(s) of a variable (or variables) that **minimise or maximise** an objective function, possibly subject to constraints.

**General form:**

$$\min_{\mathbf{x} \in \mathbb{R}^n} f(\mathbf{x}) \quad \text{subject to constraints}$$

**In Machine Learning:** Almost every ML algorithm reduces to an optimization problem:

| ML Task             | Objective to minimise                                                      |
| ------------------- | -------------------------------------------------------------------------- |
| Linear Regression   | $\|A\boldsymbol{\beta} - \mathbf{y}\|^2$ (SSE)                             |
| Ridge Regression    | $\|A\boldsymbol{\beta} - \mathbf{y}\|^2 + \lambda\|\boldsymbol{\beta}\|^2$ |
| Logistic Regression | Negative log-likelihood                                                    |
| Neural Networks     | Cross-entropy loss                                                         |
| K-Means             | Within-cluster variance                                                    |

**Why optimization matters:** Even if you don't derive it yourself, understanding what is being minimised tells you WHY the algorithm behaves the way it does — why it overfits, why it converges slowly, when it fails.

---

## 1.2 Key Terminology ⭐

**Objective function (cost function, loss function):** The function $f(x)$ being minimised or maximised.

**Feasible region:** The set of all $x$ satisfying the constraints.

**Minimiser:** A point $x^*$ where $f(x^*)$ is as small as possible.

**Local minimum:** $x^*$ is a local minimum if $f(x^*) \leq f(x)$ for all $x$ in some neighbourhood of $x^*$.

**Global minimum:** $x^*$ is a global minimum if $f(x^*) \leq f(x)$ for ALL feasible $x$.

**Saddle point:** A point where the gradient is zero but it is neither a local min nor a local max (looks like a minimum in one direction and a maximum in another).

**Critical point / Stationary point:** Any point where $f'(x) = 0$ (1D) or $\nabla f(\mathbf{x}) = \mathbf{0}$ (multivariate).

> **! NOTE:** Every local minimum is a critical point, but NOT every critical point is a local minimum. Critical points can be local minima, local maxima, or saddle points.

---

## 1.3 Types of Optimization Problems ⭐

| Type              | Description                              | Example                         |
| ----------------- | ---------------------------------------- | ------------------------------- |
| **Unconstrained** | No restrictions on $x$                   | OLS regression                  |
| **Constrained**   | $x$ must satisfy equalities/inequalities | SVM, constrained portfolio      |
| **Convex**        | $f$ is convex, feasible set is convex    | Ridge regression, logistic reg. |
| **Non-convex**    | Multiple local minima possible           | Neural networks                 |
| **Univariate**    | Single variable $x \in \mathbb{R}$       | Optimal step size in 1D         |
| **Multivariate**  | Vector $\mathbf{x} \in \mathbb{R}^n$     | Most ML problems                |

**The most important distinction:** ⭐

- **Convex problem:** Any local minimum IS the global minimum. Gradient descent guaranteed to find it.
- **Non-convex problem:** Local minima may not be global. Gradient descent can get stuck.

---

## 1.4 Necessary and Sufficient Conditions — Overview ⭐

For a smooth function $f$, the conditions for a minimum follow a hierarchy:

**Necessary condition (1st order):** If $x^*$ is a local minimum, then $f'(x^*) = 0$ (derivative must be zero).

**Sufficient condition (2nd order):** If $f'(x^*) = 0$ AND $f''(x^*) > 0$, then $x^*$ is a local minimum.

This extends to multivariate functions using the gradient and Hessian.

---

---

# PART 2 — CONVEXITY

---

## 2.1 Convex Sets ⭐

**Definition:** A set $S \subseteq \mathbb{R}^n$ is **convex** if for any two points $\mathbf{x}, \mathbf{y} \in S$ and any $\theta \in [0,1]$:

$$\theta\mathbf{x} + (1-\theta)\mathbf{y} \in S$$

**Intuition:** The straight line segment between any two points in the set lies entirely within the set. No "dents" or "holes."

**Examples:**

- Convex: any line, ball, half-space, $\mathbb{R}^n$, intersection of convex sets
- NOT convex: a donut shape, two disjoint intervals

---

## 2.2 Convex Functions ⭐

**Definition:** A function $f: \mathbb{R}^n \to \mathbb{R}$ is **convex** if for all $\mathbf{x}, \mathbf{y}$ and $\theta \in [0,1]$:

$$f(\theta\mathbf{x} + (1-\theta)\mathbf{y}) \leq \theta f(\mathbf{x}) + (1-\theta)f(\mathbf{y})$$

**Intuition:** The function value at any point on a chord between two points is **at or below** the chord itself. The function "curves upward."

**Equivalent condition using second derivative:**

For twice-differentiable $f$:
$$f \text{ is convex} \iff f''(x) \geq 0 \text{ for all } x \quad \text{(1D)}$$
$$f \text{ is convex} \iff \nabla^2 f(\mathbf{x}) \text{ is positive semi-definite for all } \mathbf{x} \quad \text{(multivariate)}$$

**Examples of convex functions:** ⭐

| Function                                              | Why convex                               |
| ----------------------------------------------------- | ---------------------------------------- |
| $f(x) = x^2$                                          | $f''(x) = 2 > 0$                         |
| $f(x) = e^x$                                          | $f''(x) = e^x > 0$                       |
| $f(x) = \|x\|$                                        | V-shape, satisfies definition            |
| $f(\mathbf{x}) = \mathbf{x}^TA\mathbf{x}$ (quadratic) | Convex iff $A$ is positive semi-definite |
| $f(\mathbf{x}) = \|A\mathbf{x} - \mathbf{b}\|^2$      | SSE objective — convex ✓                 |

**Examples of NON-convex functions:**

- $f(x) = \sin(x)$ — oscillates up and down
- $f(x) = x^3$ — inflection point at 0
- $f(x) = x^4 - 3x^2$ — multiple local minima

---

## 2.3 Why Convexity Matters ⭐

**Key theorem:** For a convex function over a convex feasible set:

$$\text{Every local minimum is a global minimum}$$

**Proof sketch:** If $x^*$ is a local min but not global, then there exists $y$ with $f(y) < f(x^*)$. By convexity, the chord from $x^*$ to $y$ lies below the function, and points near $x^*$ on this chord have function values below $f(x^*)$ — contradiction with $x^*$ being a local min.

**Practical implication:** ⭐

- Linear regression, Ridge regression, logistic regression → **convex** problems → gradient descent always finds the global optimum
- Neural networks → **non-convex** → gradient descent can get stuck in local minima, saddle points

**Strictly convex function:** $f''(x) > 0$ everywhere → **unique** global minimum.

---

## 2.4 Jensen's Inequality ⭐

For a convex function $f$ and any random variable $X$:

$$f(E[X]) \leq E[f(X)]$$

**Intuition:** The function of the average is at most the average of the function values.

This arises in information theory (entropy) and in proving properties of ML models.

---

---

# PART 3 — UNIVARIATE OPTIMIZATION

---

## 3.1 The Problem

Find $x^* \in \mathbb{R}$ that minimises $f: \mathbb{R} \to \mathbb{R}$.

**Approach:** Use calculus — find critical points using $f'(x) = 0$, then classify using $f''(x)$.

---

## 3.2 First Derivative Test ⭐

**Step 1:** Find all critical points by solving $f'(x) = 0$.

**Step 2:** Use sign change of $f'$ to classify:

| Sign of $f'$                          | Interpretation                   |
| ------------------------------------- | -------------------------------- |
| $f'$ changes from $-$ to $+$ at $x^*$ | $x^*$ is a **local minimum** ⭐  |
| $f'$ changes from $+$ to $-$ at $x^*$ | $x^*$ is a **local maximum**     |
| $f'$ does not change sign at $x^*$    | $x^*$ is an **inflection point** |

**Mnemonic:** "Negative to positive → valley (minimum). Positive to negative → hill (maximum)."

---

## 3.3 Second Derivative Test ⭐

At a critical point $x^*$ where $f'(x^*) = 0$:

| $f''(x^*)$     | Classification                                                                 |
| -------------- | ------------------------------------------------------------------------------ |
| $f''(x^*) > 0$ | Local **minimum** ⭐ (function curves upward)                                  |
| $f''(x^*) < 0$ | Local **maximum** (function curves downward)                                   |
| $f''(x^*) = 0$ | **Inconclusive** — test fails, use higher derivatives or first derivative test |

**From sample paper Q32:** A necessary condition for a minimum of a twice-differentiable function:

- **First derivative is zero** ✓ (necessary but not sufficient)

> **! NOTE:** $f'(x^*) = 0$ is necessary but NOT sufficient for a minimum. It could be a maximum or inflection point. You need either the second derivative test or the first derivative sign change to confirm.

### Worked Example ⭐

$$f(x) = x^3 - 6x^2 + 9x + 1$$

**Step 1:** $f'(x) = 3x^2 - 12x + 9 = 3(x^2 - 4x + 3) = 3(x-1)(x-3) = 0$

Critical points: $x = 1$ and $x = 3$

**Step 2:** $f''(x) = 6x - 12$

- At $x = 1$: $f''(1) = 6 - 12 = -6 < 0$ → **local maximum**
- At $x = 3$: $f''(3) = 18 - 12 = 6 > 0$ → **local minimum**

**Values:** $f(1) = 1 - 6 + 9 + 1 = 5$ (local max), $f(3) = 27 - 54 + 27 + 1 = 1$ (local min)

---

## 3.4 Boundary Conditions and Global Extrema ⭐

For optimization over a **closed interval** $[a, b]$:

1. Find all critical points inside $(a, b)$
2. Evaluate $f$ at each critical point AND at both endpoints $a$ and $b$
3. The global minimum is the smallest value; global maximum is the largest

> **! NOTE:** For unconstrained problems on $\mathbb{R}$, a local minimum is global ONLY if $f$ is convex. Otherwise you must compare all local minima.

---

## 3.5 Newton's Method for Root Finding (1D) ⭐

**Purpose:** Solve $f'(x) = 0$ numerically when no closed-form solution exists.

**Update rule:**

$$x_{k+1} = x_k - \frac{f'(x_k)}{f''(x_k)}$$

**Intuition:** At each step, fit a local quadratic approximation to $f$ using the current point's first and second derivatives. Jump to the minimum of that quadratic.

**Convergence:** Quadratic convergence near the solution — number of correct digits roughly doubles each step. Much faster than gradient descent.

**Limitation:** Requires $f''(x_k) \neq 0$. Can diverge if started far from the solution or if $f$ is non-convex.

### Worked Example ⭐

Minimise $f(x) = x^2 - 3x + 2$. Start at $x_0 = 0$.

$f'(x) = 2x - 3$, $f''(x) = 2$

$$x_1 = 0 - \frac{f'(0)}{f''(0)} = 0 - \frac{-3}{2} = 1.5$$

Since $f''(x) = 2$ (constant), Newton converges in ONE step:

$f'(1.5) = 3 - 3 = 0$ ✓ → $x^* = 1.5$, $f(1.5) = 2.25 - 4.5 + 2 = -0.25$

---

---

# PART 4 — MULTIVARIATE OPTIMIZATION

---

## 4.1 The Problem

Find $\mathbf{x}^* \in \mathbb{R}^n$ that minimises $f: \mathbb{R}^n \to \mathbb{R}$.

---

## 4.2 The Gradient ⭐

**Definition:** The gradient of $f(\mathbf{x})$ is the vector of all partial derivatives:

$$\nabla f(\mathbf{x}) = \begin{bmatrix}\frac{\partial f}{\partial x_1} \\ \frac{\partial f}{\partial x_2} \\ \vdots \\ \frac{\partial f}{\partial x_n}\end{bmatrix}$$

**Geometric meaning:** ⭐

- $\nabla f(\mathbf{x})$ points in the direction of **steepest ascent** of $f$ at $\mathbf{x}$
- $-\nabla f(\mathbf{x})$ points in the direction of **steepest descent**
- $\|\nabla f(\mathbf{x})\|$ measures the steepness (rate of change) in that direction

**First-order necessary condition:** ⭐

$$\mathbf{x}^* \text{ is a local minimum} \implies \nabla f(\mathbf{x}^*) = \mathbf{0}$$

A point where $\nabla f = \mathbf{0}$ is called a **critical point** or **stationary point**.

### Key Gradient Formulas ⭐

| $f(\mathbf{x})$                             | $\nabla f(\mathbf{x})$           |
| ------------------------------------------- | -------------------------------- |
| $\mathbf{a}^T\mathbf{x}$                    | $\mathbf{a}$                     |
| $\mathbf{x}^T\mathbf{x} = \|\mathbf{x}\|^2$ | $2\mathbf{x}$                    |
| $\mathbf{x}^TA\mathbf{x}$ (A symmetric)     | $2A\mathbf{x}$                   |
| $\|A\mathbf{x} - \mathbf{b}\|^2$            | $2A^T(A\mathbf{x} - \mathbf{b})$ |

**Deriving OLS using gradient:** ⭐

$$f(\boldsymbol{\beta}) = \|A\boldsymbol{\beta} - \mathbf{y}\|^2$$

$$\nabla_{\boldsymbol{\beta}} f = 2A^T(A\boldsymbol{\beta} - \mathbf{y}) = \mathbf{0}$$

$$\implies A^TA\boldsymbol{\beta} = A^T\mathbf{y} \implies \hat{\boldsymbol{\beta}} = (A^TA)^{-1}A^T\mathbf{y}$$

This is exactly the **Normal Equations** from linear regression — derived purely from optimization. ⭐

---

## 4.3 The Hessian ⭐

**Definition:** The Hessian of $f(\mathbf{x})$ is the matrix of all second-order partial derivatives:

$$
H(\mathbf{x}) = \nabla^2 f(\mathbf{x}) = \begin{bmatrix}
\frac{\partial^2 f}{\partial x_1^2} & \frac{\partial^2 f}{\partial x_1 \partial x_2} & \cdots \\
\frac{\partial^2 f}{\partial x_2 \partial x_1} & \frac{\partial^2 f}{\partial x_2^2} & \cdots \\
\vdots & & \ddots
\end{bmatrix}
$$

**Key property:** The Hessian is always **symmetric** (assuming $f$ has continuous second derivatives): $H_{ij} = H_{ji}$

**Geometric meaning:** The Hessian describes the **curvature** of $f$ in all directions at a point.

---

## 4.4 Second-Order Conditions — Classifying Critical Points ⭐

At a critical point $\mathbf{x}^*$ where $\nabla f(\mathbf{x}^*) = \mathbf{0}$:

| Hessian $H(\mathbf{x}^*)$                       | Classification       |
| ----------------------------------------------- | -------------------- |
| **Positive Definite** (all eigenvalues $> 0$)   | **Local minimum** ⭐ |
| **Negative Definite** (all eigenvalues $< 0$)   | Local maximum        |
| **Indefinite** (some $+$, some $-$ eigenvalues) | **Saddle point** ⭐  |
| Positive Semi-Definite (some eigenvalues $= 0$) | Inconclusive         |

**How to check definiteness:** ⭐

**Method 1 — Eigenvalues:** Compute eigenvalues of $H$.

- All $> 0$ → positive definite
- All $< 0$ → negative definite
- Mixed signs → indefinite (saddle point)

**Method 2 — Leading minors (Sylvester's criterion for PD):**

- $H_{11} > 0$
- $\det\begin{bmatrix}H_{11}&H_{12}\\H_{21}&H_{22}\end{bmatrix} > 0$
- All leading principal minors positive → positive definite

**2×2 shortcut:** For $H = \begin{bmatrix}a&b\\b&c\end{bmatrix}$:

| Condition                  | Type                              |
| -------------------------- | --------------------------------- |
| $a > 0$ and $ac - b^2 > 0$ | Positive definite → **Local min** |
| $a < 0$ and $ac - b^2 > 0$ | Negative definite → Local max     |
| $ac - b^2 < 0$             | Indefinite → **Saddle point**     |

### Worked Example ⭐

$$f(x_1, x_2) = x_1^2 + x_2^2 - 2x_1 - 4x_2 + 5$$

**Step 1 — Gradient:**

$$\frac{\partial f}{\partial x_1} = 2x_1 - 2 = 0 \implies x_1 = 1$$

$$\frac{\partial f}{\partial x_2} = 2x_2 - 4 = 0 \implies x_2 = 2$$

Critical point: $\mathbf{x}^* = (1, 2)$

**Step 2 — Hessian:**

$$H = \begin{bmatrix}2 & 0 \\ 0 & 2\end{bmatrix}$$

Eigenvalues: both $= 2 > 0$ → **Positive Definite** → $\mathbf{x}^* = (1,2)$ is a **local (and global) minimum**.

$f(1, 2) = 1 + 4 - 2 - 8 + 5 = 0$

---

### Worked Example 2 ⭐ — Saddle Point

$$f(x_1, x_2) = x_1^2 - x_2^2$$

**Step 1 — Gradient:**

$$\nabla f = \begin{bmatrix}2x_1 \\ -2x_2\end{bmatrix} = \mathbf{0} \implies \mathbf{x}^* = (0, 0)$$

**Step 2 — Hessian:**

$$H = \begin{bmatrix}2 & 0 \\ 0 & -2\end{bmatrix}$$

Eigenvalues: $+2$ and $-2$ → **Indefinite** → $\mathbf{x}^* = (0,0)$ is a **saddle point**.

**Geometric intuition:** Along $x_2 = 0$: $f = x_1^2$ curves upward (minimum-like). Along $x_1 = 0$: $f = -x_2^2$ curves downward (maximum-like). This is the classic "saddle" shape.

---

## 4.5 Gradient Derivation of Ridge Regression ⭐

$$f(\boldsymbol{\beta}) = \|A\boldsymbol{\beta} - \mathbf{y}\|^2 + \lambda\|\boldsymbol{\beta}\|^2$$

$$\nabla_{\boldsymbol{\beta}} f = 2A^T(A\boldsymbol{\beta} - \mathbf{y}) + 2\lambda\boldsymbol{\beta} = \mathbf{0}$$

$$(A^TA + \lambda I)\boldsymbol{\beta} = A^T\mathbf{y}$$

$$\hat{\boldsymbol{\beta}}_{Ridge} = (A^TA + \lambda I)^{-1}A^T\mathbf{y}$$

**This is always invertible for $\lambda > 0$** — even when $A^TA$ is singular (multicollinearity). ⭐

---

---

# PART 5 — GRADIENT DESCENT

---

## 5.1 Motivation ⭐

For many ML problems (logistic regression, neural networks), the objective function has **no closed-form solution** to $\nabla f = \mathbf{0}$. We must use iterative numerical methods.

**Gradient descent** is the foundational iterative algorithm for minimisation.

---

## 5.2 The Algorithm ⭐

**Core idea:** Starting from an initial guess $\mathbf{x}_0$, repeatedly move in the direction of steepest descent (negative gradient) until convergence.

**Update rule:**

$$\boxed{\mathbf{x}_{k+1} = \mathbf{x}_k - \eta \nabla f(\mathbf{x}_k)}$$

where:

- $\mathbf{x}_k$ = current iterate
- $\eta > 0$ = **learning rate** (step size)
- $\nabla f(\mathbf{x}_k)$ = gradient at current point

**Why negative gradient?** Because $\nabla f$ points uphill (steepest ascent). Moving AGAINST it takes us downhill.

---

## 5.3 Step-by-Step Algorithm

```
Initialize: x_0 (random or zero)
Repeat until convergence:
    1. Compute gradient: g_k = ∇f(x_k)
    2. Update: x_{k+1} = x_k - η * g_k
    3. Check convergence: ||g_k|| < tolerance, or ||x_{k+1} - x_k|| < tolerance
```

**Convergence criterion:** Stop when the gradient is close enough to zero, or when the change in $\mathbf{x}$ is negligibly small.

---

## 5.4 The Learning Rate η — Critical Hyperparameter ⭐

| Learning Rate  | Effect                                               |
| -------------- | ---------------------------------------------------- |
| **Too large**  | Overshoots the minimum — may diverge or oscillate ⭐ |
| **Too small**  | Converges very slowly — takes many iterations        |
| **Just right** | Smooth, efficient convergence                        |

**Intuition for "too large":** If $\eta$ is too large, the step overshoots past the minimum. The next iterate is on the other side of the minimum, often even farther away. Repeated overshooting → divergence.

**Rule of thumb:** For a convex quadratic $f(\mathbf{x}) = \frac{1}{2}\mathbf{x}^TA\mathbf{x} - \mathbf{b}^T\mathbf{x}$, the optimal step size is:

$$\eta^* = \frac{1}{\lambda_{\max}(A)}$$

where $\lambda_{\max}(A)$ is the largest eigenvalue of $A$.

---

## 5.5 Convergence Analysis ⭐

**For strictly convex functions:** Gradient descent converges to the global minimum for sufficiently small $\eta$.

**Convergence rate depends on the condition number:**

$$\kappa(A) = \frac{\lambda_{\max}(A)}{\lambda_{\min}(A)}$$

- $\kappa$ close to 1 → fast convergence (near-circular level sets)
- $\kappa \gg 1$ → very slow convergence (elongated elliptical level sets)
- High condition number is the multivariate analogue of "badly-scaled" features

**Geometric intuition:** If the level sets of $f$ are perfect circles, gradient descent goes straight to the minimum. If they are very elongated ellipses (high condition number), gradient descent zigzags slowly toward the minimum.

---

## 5.6 Full Numerical Example ⭐

**Minimise:**

$$f(x) = x^2 - 4x + 4 = (x-2)^2$$

**True minimum:** $x^* = 2$, $f(2) = 0$

**Gradient:** $f'(x) = 2x - 4$

**Learning rate:** $\eta = 0.3$

**Starting point:** $x_0 = 0$

| Iteration $k$ | $x_k$ | $f'(x_k) = 2x_k - 4$ | $x_{k+1} = x_k - 0.3 \cdot f'(x_k)$ |
| ------------- | ----- | -------------------- | ----------------------------------- |
| 0             | 0.000 | $-4.000$             | $0 - 0.3(-4) = 1.200$               |
| 1             | 1.200 | $-1.600$             | $1.2 - 0.3(-1.6) = 1.680$           |
| 2             | 1.680 | $-0.640$             | $1.68 - 0.3(-0.64) = 1.872$         |
| 3             | 1.872 | $-0.256$             | $1.872 - 0.3(-0.256) = 1.949$       |
| 4             | 1.949 | $-0.102$             | $1.949 - 0.3(-0.102) = 1.980$       |
| 5             | 1.980 | $-0.040$             | $1.980 - 0.3(-0.040) = 1.992$       |

Converging towards $x^* = 2$. Each step gets 40% closer (convergence factor = $|1 - 2\eta| = |1 - 0.6| = 0.4$).

---

## 5.7 Gradient Descent in Multiple Dimensions ⭐

### Example — Minimise a Quadratic

$$f(x_1, x_2) = 2x_1^2 + x_2^2 - 2x_1x_2 - 2x_1$$

**Gradient:**

$$\nabla f = \begin{bmatrix}4x_1 - 2x_2 - 2 \\ 2x_2 - 2x_1\end{bmatrix}$$

**True minimum:** Solve $\nabla f = \mathbf{0}$:

- $4x_1 - 2x_2 = 2$
- $-2x_1 + 2x_2 = 0 \implies x_1 = x_2$

Substituting: $4x_1 - 2x_1 = 2 \implies x_1 = 1$, $x_2 = 1$

$\mathbf{x}^* = (1, 1)$, $f(1,1) = 2 + 1 - 2 - 2 = -1$

**GD update** starting from $\mathbf{x}_0 = (0, 0)$, $\eta = 0.2$:

$$\nabla f(0,0) = \begin{bmatrix}-2 \\ 0\end{bmatrix}$$

$$\mathbf{x}_1 = \begin{bmatrix}0\\0\end{bmatrix} - 0.2\begin{bmatrix}-2\\0\end{bmatrix} = \begin{bmatrix}0.4\\0\end{bmatrix}$$

$$\nabla f(0.4, 0) = \begin{bmatrix}4(0.4) - 2(0) - 2 \\ 2(0) - 2(0.4)\end{bmatrix} = \begin{bmatrix}-0.4 \\ -0.8\end{bmatrix}$$

$$\mathbf{x}_2 = \begin{bmatrix}0.4\\0\end{bmatrix} - 0.2\begin{bmatrix}-0.4\\-0.8\end{bmatrix} = \begin{bmatrix}0.48\\0.16\end{bmatrix}$$

Continuing, the iterates spiral towards $(1,1)$.

---

## 5.8 Variants of Gradient Descent ⭐

### Batch Gradient Descent (Full GD)

- Compute gradient using ALL $n$ training samples
- Stable, accurate gradient estimate
- Very slow for large datasets (one update requires scanning all data)

### Stochastic Gradient Descent (SGD) ⭐

- Compute gradient using ONE randomly selected sample
- Very fast updates (one sample at a time)
- Noisy gradient estimate — can escape shallow local minima
- May oscillate near minimum, never fully settle

$$\mathbf{x}_{k+1} = \mathbf{x}_k - \eta \nabla f_i(\mathbf{x}_k) \quad \text{(one sample } i \text{ at a time)}$$

### Mini-Batch Gradient Descent ⭐

- Compute gradient using a small **batch** of $m$ samples ($m \ll n$, typically 32–256)
- Balance between full GD (slow but stable) and SGD (fast but noisy)
- Standard in deep learning

$$\mathbf{x}_{k+1} = \mathbf{x}_k - \eta \cdot \frac{1}{m}\sum_{i \in \text{batch}} \nabla f_i(\mathbf{x}_k)$$

| Method        | Gradient estimate        | Update speed | Stability   |
| ------------- | ------------------------ | ------------ | ----------- |
| Batch GD      | Exact (over all data)    | Slowest      | Most stable |
| Mini-batch GD | Approximate (over batch) | Fast         | Moderate    |
| SGD           | Noisy (one sample)       | Fastest      | Most noisy  |

---

## 5.9 Common Issues and Solutions ⭐

### Problem 1 — Learning Rate Selection

**Too large:** Diverges or oscillates.

**Too small:** Very slow.

**Solutions:**

- **Learning rate schedules:** Start large, decay over time (e.g., $\eta_k = \eta_0 / (1 + k)$)
- **Line search:** At each step, choose $\eta$ that minimises $f(\mathbf{x}_k - \eta \nabla f(\mathbf{x}_k))$

### Problem 2 — Saddle Points ⭐

In high-dimensional non-convex problems (neural networks), saddle points are far more common than local minima. At a saddle point, $\nabla f = \mathbf{0}$ but it is neither a min nor a max.

SGD's noise actually helps **escape saddle points** — a key practical advantage over batch GD.

### Problem 3 — Vanishing / Exploding Gradients

In deep networks, gradients can become extremely small (vanish) or extremely large (explode) during backpropagation. Solutions: gradient clipping, careful initialisation, batch normalisation.

### Problem 4 — Feature Scaling ⭐

If features have very different scales, the gradient landscape becomes highly elongated (high condition number). Gradient descent zigzags and converges very slowly.

**Solution:** Always normalise or standardise features before gradient descent.

$$x_j \leftarrow \frac{x_j - \bar{x}_j}{s_j}$$

---

## 5.10 Newton's Method — Multivariate ⭐

Extension of 1D Newton's method to $\mathbb{R}^n$:

$$\mathbf{x}_{k+1} = \mathbf{x}_k - [H(\mathbf{x}_k)]^{-1} \nabla f(\mathbf{x}_k)$$

where $H(\mathbf{x}_k) = \nabla^2 f(\mathbf{x}_k)$ is the Hessian matrix.

**Advantages over gradient descent:**

- **No learning rate** needed (or adaptive step = 1)
- **Quadratic convergence** near the minimum — much faster
- Automatically accounts for curvature in all directions

**Disadvantages:**

- Must compute and invert the Hessian at every step — $O(n^3)$ cost for $n$ parameters
- Too expensive for large-scale ML ($n$ can be millions)
- Requires $H$ to be positive definite (may fail near saddle points)

**Quasi-Newton methods** (BFGS, L-BFGS): Approximate the Hessian using gradient information only — practical compromise for medium-scale problems.

---

---

# PART 6 — OPTIMIZATION IN ML — CONNECTIONS ⭐

---

## 6.1 Why These Three Results All Come from Setting Gradient to Zero

| ML Problem              | Objective $f$                                                              | $\nabla f = 0$ gives                                         |
| ----------------------- | -------------------------------------------------------------------------- | ------------------------------------------------------------ |
| Linear Regression (OLS) | $\|A\boldsymbol{\beta} - \mathbf{y}\|^2$                                   | $(A^TA)\hat{\boldsymbol{\beta}} = A^T\mathbf{y}$             |
| Ridge Regression        | $\|A\boldsymbol{\beta} - \mathbf{y}\|^2 + \lambda\|\boldsymbol{\beta}\|^2$ | $(A^TA + \lambda I)\hat{\boldsymbol{\beta}} = A^T\mathbf{y}$ |
| Logistic Regression     | $-\sum[y_i\log\hat{p}_i + (1-y_i)\log(1-\hat{p}_i)]$                       | No closed form → use gradient descent                        |

**Key insight:** OLS and Ridge have **closed-form solutions** (convex + quadratic). Logistic regression is convex but not quadratic → must use gradient descent or Newton's method.

---

## 6.2 Gradient Descent for Linear Regression ⭐

Even though OLS has a closed form $(A^TA)^{-1}A^T\mathbf{y}$, when $n$ is huge, computing the matrix inverse is expensive ($O(p^3)$). Gradient descent avoids this:

$$\nabla_{\boldsymbol{\beta}} \|A\boldsymbol{\beta} - \mathbf{y}\|^2 = 2A^T(A\boldsymbol{\beta} - \mathbf{y})$$

$$\boldsymbol{\beta}_{k+1} = \boldsymbol{\beta}_k - \eta \cdot 2A^T(A\boldsymbol{\beta}_k - \mathbf{y})$$

For linear regression, this IS convex → gradient descent converges to the global OLS solution.

---

## 6.3 Necessary vs Sufficient Conditions — Summary ⭐

| Condition                             | Type                                        | When it holds                 |
| ------------------------------------- | ------------------------------------------- | ----------------------------- |
| $f'(x^*) = 0$                         | **Necessary** for local min                 | Always holds at any local min |
| $f''(x^*) > 0$                        | **Sufficient** (combined with $f'=0$)       | Guarantees local min          |
| $f$ convex AND $f'(x^*)=0$            | **Sufficient**                              | Guarantees GLOBAL min         |
| $\nabla f(\mathbf{x}^*) = \mathbf{0}$ | **Necessary** for local min                 | Always holds                  |
| $H(\mathbf{x}^*)$ positive definite   | **Sufficient** (combined with $\nabla f=0$) | Guarantees local min          |

> **! NOTE (Sample Paper Q32):** "A necessary condition for a minimum" = **first derivative is zero**. The answer is NOT "second derivative is positive" — that is a sufficient (not necessary) condition.

---

---

# MASTER FORMULA SHEET — OPTIMIZATION

## Convexity

$$f \text{ convex} \iff f''(x) \geq 0 \text{ (1D)} \iff H(\mathbf{x}) \succeq 0 \text{ (multivariate)}$$

$$\text{Convex} \implies \text{every local min is global min}$$

## Univariate — Conditions

$$f'(x^*) = 0 \quad \text{(necessary — 1st order)}$$

$$f'(x^*) = 0 \text{ AND } f''(x^*) > 0 \implies \text{local min}$$
$$f'(x^*) = 0 \text{ AND } f''(x^*) < 0 \implies \text{local max}$$

## Newton's Method (1D)

$$x_{k+1} = x_k - \frac{f'(x_k)}{f''(x_k)}$$

## Gradient

$$\nabla(\mathbf{a}^T\mathbf{x}) = \mathbf{a}, \quad \nabla(\mathbf{x}^TA\mathbf{x}) = 2A\mathbf{x} \text{ (A sym)}, \quad \nabla\|A\mathbf{x}-\mathbf{b}\|^2 = 2A^T(A\mathbf{x}-\mathbf{b})$$

## Hessian — Classification

| $H(\mathbf{x}^*)$                     | Classification |
| ------------------------------------- | -------------- |
| Positive Definite (all $\lambda > 0$) | Local minimum  |
| Negative Definite (all $\lambda < 0$) | Local maximum  |
| Indefinite (mixed $\lambda$)          | Saddle point   |

**2×2 shortcut:** $H = \begin{bmatrix}a&b\\b&c\end{bmatrix}$: PD iff $a > 0$ and $ac - b^2 > 0$

## Gradient Descent

$$\mathbf{x}_{k+1} = \mathbf{x}_k - \eta\nabla f(\mathbf{x}_k)$$

- $\eta$ too large → diverge; $\eta$ too small → slow
- Convex $f$ → converges to global min

## Newton's Method (Multivariate)

$$\mathbf{x}_{k+1} = \mathbf{x}_k - [H(\mathbf{x}_k)]^{-1}\nabla f(\mathbf{x}_k)$$

## Key Derivations

$$\text{OLS: } \nabla\|A\boldsymbol{\beta}-\mathbf{y}\|^2 = 0 \implies A^TA\hat{\boldsymbol{\beta}} = A^T\mathbf{y}$$

$$\text{Ridge: } \nabla(\|A\boldsymbol{\beta}-\mathbf{y}\|^2 + \lambda\|\boldsymbol{\beta}\|^2) = 0 \implies (A^TA+\lambda I)\hat{\boldsymbol{\beta}} = A^T\mathbf{y}$$

## Quick Reference Card ⭐

| Question                             | Answer                                                              |
| ------------------------------------ | ------------------------------------------------------------------- |
| Necessary condition for minimum      | $f'(x) = 0$ (gradient zero)                                         |
| Sufficient condition for local min   | $f'=0$ AND $f''>0$                                                  |
| Convex + gradient zero               | Global min guaranteed                                               |
| Hessian indefinite at critical point | Saddle point                                                        |
| GD: $\eta$ too large                 | Diverge/oscillate                                                   |
| GD: $\eta$ too small                 | Slow convergence                                                    |
| Newton vs GD                         | Newton faster (quadratic conv.) but expensive ($O(n^3)$)            |
| SGD advantage over batch GD          | Can escape saddle points, fast updates                              |
| Why normalise features for GD        | Reduces condition number → faster convergence                       |
| Ridge always invertible              | Because $(A^TA + \lambda I)$ has all eigenvalues $\geq \lambda > 0$ |

---

_End of Optimization Notes_

---

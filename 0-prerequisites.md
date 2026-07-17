# Calculus Refresher — Integration and Differentiation
## Focused on IIT M.Tech AI/ML Syllabus Needs

---

## PART 1 — DIFFERENTIATION

---

### 1.1 Basic Rules

| Rule | Formula | Example |
|------|---------|---------|
| Power rule | $\frac{d}{dx}x^n = nx^{n-1}$ | $\frac{d}{dx}x^3 = 3x^2$ |
| Constant | $\frac{d}{dx}c = 0$ | $\frac{d}{dx}7 = 0$ |
| Constant multiple | $\frac{d}{dx}cf(x) = cf'(x)$ | $\frac{d}{dx}5x^2 = 10x$ |
| Sum/difference | $\frac{d}{dx}[f\pm g] = f'\pm g'$ | $\frac{d}{dx}(x^3+x^2) = 3x^2+2x$ |
| Exponential | $\frac{d}{dx}e^x = e^x$ | $\frac{d}{dx}e^x = e^x$ |
| Natural log | $\frac{d}{dx}\log x = \frac{1}{x}$ | $\frac{d}{dx}\log(3x) = \frac{1}{x}$ |

---

### 1.2 Product Rule

$$\frac{d}{dx}[f(x)\cdot g(x)] = f'(x)g(x) + f(x)g'(x)$$

**Example:** Differentiate $f(x) = x^2 e^x$

$$f'(x) = 2x\cdot e^x + x^2\cdot e^x = e^x(2x + x^2) = xe^x(2+x)$$

---

### 1.3 Quotient Rule

$$\frac{d}{dx}\left[\frac{f(x)}{g(x)}\right] = \frac{f'(x)g(x) - f(x)g'(x)}{[g(x)]^2}$$

**Memory trick:** "Low d-High minus High d-Low, over Low squared."

**Example:** Differentiate $f(x) = \frac{x^2}{x+1}$

$$f'(x) = \frac{2x(x+1) - x^2(1)}{(x+1)^2} = \frac{2x^2+2x-x^2}{(x+1)^2} = \frac{x^2+2x}{(x+1)^2}$$

---

### 1.4 Chain Rule ⭐

$$\frac{d}{dx}f(g(x)) = f'(g(x))\cdot g'(x)$$

**Read as:** "Derivative of outer function (keeping inner intact) times derivative of inner function."

**Example 1:** Differentiate $f(x) = e^{3x^2}$

- Outer: $e^u$ → derivative $e^u$
- Inner: $u = 3x^2$ → derivative $6x$

$$f'(x) = e^{3x^2}\cdot 6x = 6xe^{3x^2}$$

**Example 2:** Differentiate $f(x) = \log(x^2+1)$

- Outer: $\log u$ → derivative $\frac{1}{u}$
- Inner: $u = x^2+1$ → derivative $2x$

$$f'(x) = \frac{1}{x^2+1}\cdot 2x = \frac{2x}{x^2+1}$$

**Example 3 — Sigmoid** ⭐ (most important for ML)

Differentiate $\sigma(z) = \frac{1}{1+e^{-z}}$

Write as $\sigma(z) = (1+e^{-z})^{-1}$

- Outer: $u^{-1}$ → derivative $-u^{-2}$
- Inner: $u = 1+e^{-z}$ → derivative $-e^{-z}$

$$\sigma'(z) = -(1+e^{-z})^{-2}\cdot(-e^{-z}) = \frac{e^{-z}}{(1+e^{-z})^2}$$

Now rewrite cleverly:

$$= \frac{1}{1+e^{-z}}\cdot\frac{e^{-z}}{1+e^{-z}} = \sigma(z)\cdot(1-\sigma(z))$$

$$\boxed{\sigma'(z) = \sigma(z)(1-\sigma(z))}$$

---

### 1.5 Partial Derivatives ⭐

When $f$ depends on multiple variables, differentiate with respect to one variable while treating all others as constants.

**Example 1:** $f(x_1, x_2) = 3x_1^2 + 2x_1x_2 + x_2^2$

$$\frac{\partial f}{\partial x_1} = 6x_1 + 2x_2 \quad \text{(treat }x_2\text{ as constant)}$$

$$\frac{\partial f}{\partial x_2} = 2x_1 + 2x_2 \quad \text{(treat }x_1\text{ as constant)}$$

**Example 2 — OLS Loss** ⭐

$f(\beta_0, \beta_1) = \sum_{i=1}^n (y_i - \beta_0 - \beta_1 x_i)^2$

$$\frac{\partial f}{\partial \beta_0} = \sum_{i=1}^n 2(y_i-\beta_0-\beta_1 x_i)\cdot(-1) = -2\sum_{i=1}^n(y_i-\beta_0-\beta_1 x_i)$$

$$\frac{\partial f}{\partial \beta_1} = \sum_{i=1}^n 2(y_i-\beta_0-\beta_1 x_i)\cdot(-x_i) = -2\sum_{i=1}^n x_i(y_i-\beta_0-\beta_1 x_i)$$

Setting both to zero gives the normal equations — the foundation of OLS. ⭐

---

### 1.6 Matrix/Vector Derivatives ⭐

These appear constantly in ML. Learn them as formulas.

| Expression | Derivative w.r.t. $\mathbf{x}$ |
|------------|-------------------------------|
| $\mathbf{a}^T\mathbf{x}$ | $\mathbf{a}$ |
| $\mathbf{x}^T\mathbf{x} = \|\mathbf{x}\|^2$ | $2\mathbf{x}$ |
| $\mathbf{x}^TA\mathbf{x}$ ($A$ symmetric) | $2A\mathbf{x}$ |
| $\|A\mathbf{x}-\mathbf{b}\|^2$ | $2A^T(A\mathbf{x}-\mathbf{b})$ |

**Deriving the last one step by step** ⭐

$$f(\mathbf{x}) = \|A\mathbf{x}-\mathbf{b}\|^2 = (A\mathbf{x}-\mathbf{b})^T(A\mathbf{x}-\mathbf{b})$$

Expand:

$$= \mathbf{x}^TA^TA\mathbf{x} - 2\mathbf{b}^TA\mathbf{x} + \mathbf{b}^T\mathbf{b}$$

Differentiate term by term using the table above:

$$\nabla_{\mathbf{x}}f = 2A^TA\mathbf{x} - 2A^T\mathbf{b} = 2A^T(A\mathbf{x}-\mathbf{b})$$

Setting to zero gives $(A^TA)\mathbf{x} = A^T\mathbf{b}$ — the Normal Equations.

---

### 1.7 Second Derivatives ⭐

The second derivative measures **curvature** — whether the function is concave up or down.

$$f''(x) = \frac{d}{dx}f'(x)$$

**Example:** $f(x) = x^3 - 6x^2 + 9x$

$$f'(x) = 3x^2 - 12x + 9$$

$$f''(x) = 6x - 12$$

**Use:**
- $f''(x) > 0$ at a critical point → local minimum (concave up)
- $f''(x) < 0$ at a critical point → local maximum (concave down)
- $f''(x) = 0$ everywhere → test inconclusive, use first derivative test

---

## PART 2 — INTEGRATION

---

### 2.1 Basic Rules

| Rule | Formula | Example |
|------|---------|---------|
| Power rule | $\int x^n\,dx = \frac{x^{n+1}}{n+1} + C$ | $\int x^3\,dx = \frac{x^4}{4}+C$ |
| Constant | $\int c\,dx = cx + C$ | $\int 5\,dx = 5x+C$ |
| Exponential | $\int e^x\,dx = e^x + C$ | $\int e^x\,dx = e^x+C$ |
| $e^{ax}$ | $\int e^{ax}\,dx = \frac{e^{ax}}{a} + C$ | $\int e^{3x}\,dx = \frac{e^{3x}}{3}+C$ |
| Natural log | $\int \frac{1}{x}\,dx = \log\|x\| + C$ | $\int\frac{1}{x}\,dx = \log\|x\|+C$ |
| Sum | $\int[f+g]\,dx = \int f\,dx + \int g\,dx$ | Split and integrate term by term |

---

### 2.2 Definite Integrals

$$\int_a^b f(x)\,dx = F(b) - F(a) \quad \text{where } F'(x) = f(x)$$

**Example 1:** $\int_0^2 x^2\,dx$

$$= \left[\frac{x^3}{3}\right]_0^2 = \frac{8}{3} - 0 = \frac{8}{3}$$

**Example 2 — PDF normalisation** ⭐

Verify $f(x) = \frac{x}{2}$ on $[0,2]$ is a valid PDF:

$$\int_0^2 \frac{x}{2}\,dx = \frac{1}{2}\left[\frac{x^2}{2}\right]_0^2 = \frac{1}{2}\cdot 2 = 1 \checkmark$$

---

### 2.3 Substitution Rule ⭐

Use when the integrand contains a function and its derivative.

**Method:** Let $u = g(x)$, then $du = g'(x)\,dx$.

$$\int f(g(x))\cdot g'(x)\,dx = \int f(u)\,du$$

**Example 1:** $\int 2xe^{x^2}\,dx$

Let $u = x^2$, then $du = 2x\,dx$:

$$= \int e^u\,du = e^u + C = e^{x^2} + C$$

**Example 2:** $\int \frac{2x}{x^2+1}\,dx$

Let $u = x^2+1$, then $du = 2x\,dx$:

$$= \int \frac{1}{u}\,du = \log u + C = \log(x^2+1) + C$$

**Example 3 — Computing expected value** ⭐

$X$ has PDF $f(x) = 3x^2$ on $[0,1]$. Find $E[X]$:

$$E[X] = \int_0^1 x\cdot 3x^2\,dx = 3\int_0^1 x^3\,dx = 3\left[\frac{x^4}{4}\right]_0^1 = 3\cdot\frac{1}{4} = \frac{3}{4}$$

---

### 2.4 Integration by Parts

Use when the integrand is a product of two different types of functions.

$$\int u\,dv = uv - \int v\,du$$

**LIATE rule** — choose $u$ in this priority order:
**L**ogarithm, **I**nverse trig, **A**lgebraic ($x^n$), **T**rig, **E**xponential

**Example:** $\int x e^x\,dx$

Choose $u = x$ (Algebraic) and $dv = e^x\,dx$:

$$du = dx, \quad v = e^x$$

$$\int xe^x\,dx = xe^x - \int e^x\,dx = xe^x - e^x + C = e^x(x-1) + C$$

---

### 2.5 Integrating over Multiple Variables ⭐

For joint PDFs, integrate out one variable to get the marginal.

**Example — Marginal PDF** *(Direct style of Sample Paper Q16)*

Joint PDF: $f(x,y) = \frac{x(1+3y^2)}{4}$, $0<x<2$, $0<y<1$

Find marginal $f_X(x)$ — integrate out $y$:

$$f_X(x) = \int_0^1 \frac{x(1+3y^2)}{4}\,dy = \frac{x}{4}\int_0^1(1+3y^2)\,dy$$

$$= \frac{x}{4}\left[y + y^3\right]_0^1 = \frac{x}{4}(1+1) = \frac{x}{2}$$

**Find marginal $f_Y(y)$** — integrate out $x$:

$$f_Y(y) = \int_0^2 \frac{x(1+3y^2)}{4}\,dx = \frac{(1+3y^2)}{4}\int_0^2 x\,dx$$

$$= \frac{(1+3y^2)}{4}\left[\frac{x^2}{2}\right]_0^2 = \frac{(1+3y^2)}{4}\cdot 2 = \frac{1+3y^2}{2}$$

---

### 2.6 Key Integrals for Probability ⭐

These appear repeatedly in distribution questions:

**Finding the normalising constant:**

If $f(x) = cx^2$ on $[0,3]$ is a PDF, find $c$:

$$\int_0^3 cx^2\,dx = c\left[\frac{x^3}{3}\right]_0^3 = c\cdot 9 = 1 \implies c = \frac{1}{9}$$

**Computing $E[X]$:**

$$E[X] = \int_0^3 x\cdot\frac{x^2}{9}\,dx = \frac{1}{9}\int_0^3 x^3\,dx = \frac{1}{9}\cdot\frac{81}{4} = \frac{9}{4}$$

**Computing $E[X^2]$ for variance:**

$$E[X^2] = \int_0^3 x^2\cdot\frac{x^2}{9}\,dx = \frac{1}{9}\int_0^3 x^4\,dx = \frac{1}{9}\cdot\frac{243}{5} = \frac{27}{5}$$

$$\text{Var}(X) = E[X^2] - (E[X])^2 = \frac{27}{5} - \frac{81}{16} = \frac{432-405}{80} = \frac{27}{80}$$

---

## PART 3 — CONNECTIONS TO THE SYLLABUS

---

### Where Differentiation Appears

| Topic | How differentiation is used |
|-------|-----------------------------|
| OLS Linear Regression | Set $\frac{\partial}{\partial\boldsymbol{\beta}}\|A\boldsymbol{\beta}-\mathbf{y}\|^2 = 0$ → Normal Equations |
| Ridge Regression | Set $\frac{\partial}{\partial\boldsymbol{\beta}}(\|A\boldsymbol{\beta}-\mathbf{y}\|^2+\lambda\|\boldsymbol{\beta}\|^2) = 0$ |
| Logistic Regression | Differentiate log-likelihood to get gradient for MLE |
| Gradient Descent | Update rule uses $\nabla f$ at each step |
| Optimization | $f'(x)=0$ finds critical points; $f''(x)$ classifies them |
| Univariate optimization | $f'(x^*)=0$ necessary; $f''(x^*)>0$ sufficient for min |

### Where Integration Appears

| Topic | How integration is used |
|-------|------------------------|
| Continuous PDFs | $\int_{-\infty}^{\infty}f(x)\,dx = 1$ to verify/find normalising constant |
| Expected value | $E[X] = \int x\,f(x)\,dx$ |
| Variance | $E[X^2] = \int x^2 f(x)\,dx$, then $\text{Var}=E[X^2]-(E[X])^2$ |
| Marginal distributions | Integrate joint PDF over the other variable |
| CDF from PDF | $F(x) = \int_{-\infty}^x f(t)\,dt$ |
| Probabilities | $P(a\leq X\leq b) = \int_a^b f(x)\,dx$ |

---

## PART 4 — QUICK REFERENCE CARD

### Differentiation

$$\frac{d}{dx}x^n = nx^{n-1} \quad \frac{d}{dx}e^x = e^x \quad \frac{d}{dx}\log x = \frac{1}{x}$$

$$\text{Chain: }\frac{d}{dx}f(g(x)) = f'(g(x))\cdot g'(x)$$

$$\text{Sigmoid: }\sigma'(z) = \sigma(z)(1-\sigma(z))$$

$$\nabla_{\mathbf{x}}\|A\mathbf{x}-\mathbf{b}\|^2 = 2A^T(A\mathbf{x}-\mathbf{b})$$

### Integration

$$\int x^n\,dx = \frac{x^{n+1}}{n+1}+C \quad \int e^{ax}\,dx = \frac{e^{ax}}{a}+C \quad \int\frac{1}{x}\,dx = \log|x|+C$$

$$\text{Substitution: let }u=g(x),\;du=g'(x)\,dx$$

$$\text{By parts: }\int u\,dv = uv - \int v\,du$$

$$E[X] = \int x\,f(x)\,dx \quad \text{Var}(X) = \int x^2 f(x)\,dx - \left(\int xf(x)\,dx\right)^2$$

---

# Linear Algebra Techniques — Complete Refresher
## Step-by-Step with Full Examples

---

# PART 1 — ROW REDUCTION AND RREF

---

## 1.1 What is RREF?

**Reduced Row Echelon Form** is a standardised form of a matrix obtained by row operations. It makes solving linear systems mechanical.

**Three allowed row operations** — none of these change the solution:

| Operation | Notation | Example |
|-----------|----------|---------|
| Swap two rows | $R_i \leftrightarrow R_j$ | Swap row 1 and row 2 |
| Multiply a row by nonzero scalar | $R_i \leftarrow cR_i$ | Multiply row 1 by $1/2$ |
| Add a multiple of one row to another | $R_i \leftarrow R_i + cR_j$ | Row 2 = Row 2 − 3×Row 1 |

**RREF conditions — all four must hold:**

1. Any all-zero rows are at the bottom
2. The first nonzero entry in each row (the **pivot**) is 1
3. Each pivot is to the RIGHT of the pivot in the row above
4. Every other entry in a pivot column is **zero** (above AND below)

---

## 1.2 Full Example — Finding RREF

$$A = \begin{bmatrix}0&2&4&2\\1&3&1&0\\2&8&6&0\end{bmatrix}$$

**Step 1 — Get a pivot in position (1,1). Currently it is 0, so swap rows:**

$R_1 \leftrightarrow R_2$:

$$\begin{bmatrix}1&3&1&0\\0&2&4&2\\2&8&6&0\end{bmatrix}$$

**Step 2 — Eliminate below the first pivot using $R_3 \leftarrow R_3 - 2R_1$:**

$$\begin{bmatrix}1&3&1&0\\0&2&4&2\\0&2&4&0\end{bmatrix}$$

**Step 3 — Make second pivot equal to 1 using $R_2 \leftarrow \frac{1}{2}R_2$:**

$$\begin{bmatrix}1&3&1&0\\0&1&2&1\\0&2&4&0\end{bmatrix}$$

**Step 4 — Eliminate below second pivot using $R_3 \leftarrow R_3 - 2R_2$:**

$$\begin{bmatrix}1&3&1&0\\0&1&2&1\\0&0&0&-2\end{bmatrix}$$

**Step 5 — Make third pivot equal to 1 using $R_3 \leftarrow -\frac{1}{2}R_3$:**

$$\begin{bmatrix}1&3&1&0\\0&1&2&1\\0&0&0&1\end{bmatrix}$$

**Step 6 — Eliminate ABOVE the third pivot.**

$R_2 \leftarrow R_2 - 1\cdot R_3$:

$$\begin{bmatrix}1&3&1&0\\0&1&2&0\\0&0&0&1\end{bmatrix}$$

$R_1 \leftarrow R_1 - 0\cdot R_3$ (nothing to do since entry is already 0).

**Step 7 — Eliminate above the second pivot using $R_1 \leftarrow R_1 - 3R_2$:**

$$\text{RREF} = \begin{bmatrix}1&0&-5&0\\0&1&2&0\\0&0&0&1\end{bmatrix}$$

**Reading the result:**

- Pivot columns: 1, 2, 4 → $x_1$, $x_2$, $x_4$ are pivot variables
- Free column: 3 → $x_3$ is a free variable
- $\text{rank}(A) = 3$ (three pivots)

---

## 1.3 Finding Null Space from RREF

Using the RREF above with $A\mathbf{x} = \mathbf{0}$:

$$x_1 - 5x_3 = 0 \implies x_1 = 5x_3$$
$$x_2 + 2x_3 = 0 \implies x_2 = -2x_3$$
$$x_4 = 0$$

Let $x_3 = t$ (free):

$$\mathbf{x} = t\begin{bmatrix}5\\-2\\1\\0\end{bmatrix}$$

$$\text{null}(A) = \text{span}\left\{\begin{bmatrix}5\\-2\\1\\0\end{bmatrix}\right\}$$

---

## 1.4 Solving $A\mathbf{x} = \mathbf{b}$ using Augmented Matrix

$$A = \begin{bmatrix}1&2&1\\2&4&3\\0&0&1\end{bmatrix}, \quad \mathbf{b} = \begin{bmatrix}3\\7\\1\end{bmatrix}$$

Form augmented matrix $[A|\mathbf{b}]$ and row reduce:

$$\left[\begin{array}{ccc|c}1&2&1&3\\2&4&3&7\\0&0&1&1\end{array}\right]$$

$R_2 \leftarrow R_2 - 2R_1$:

$$\left[\begin{array}{ccc|c}1&2&1&3\\0&0&1&1\\0&0&1&1\end{array}\right]$$

$R_3 \leftarrow R_3 - R_2$:

$$\left[\begin{array}{ccc|c}1&2&1&3\\0&0&1&1\\0&0&0&0\end{array}\right]$$

$R_1 \leftarrow R_1 - R_2$:

$$\text{RREF}: \left[\begin{array}{ccc|c}1&2&0&2\\0&0&1&1\\0&0&0&0\end{array}\right]$$

- $\text{rank}(A) = \text{rank}([A|\mathbf{b}]) = 2$ → **consistent** (solution exists)
- Free variable: $x_2 = t$
- $x_1 = 2 - 2t$, $x_3 = 1$

**General solution:**

$$\mathbf{x} = \underbrace{\begin{bmatrix}2\\0\\1\end{bmatrix}}_{\text{particular}} + t\underbrace{\begin{bmatrix}-2\\1\\0\end{bmatrix}}_{\text{null space}}, \quad t \in \mathbb{R}$$

---

---

# PART 2 — EIGENVALUES AND EIGENDECOMPOSITION

---

## 2.1 What Are Eigenvalues?

$\lambda$ is an eigenvalue of $A$ with eigenvector $\mathbf{v}$ if:

$$A\mathbf{v} = \lambda\mathbf{v}$$

**Intuition:** $\mathbf{v}$ is a special direction that matrix $A$ only scales (by $\lambda$) — it does not rotate or mix that direction with others.

---

## 2.2 Four-Step Algorithm

**Step 1:** Solve $\det(A - \lambda I) = 0$ for eigenvalues $\lambda$

**Step 2:** Verify using $\text{tr}(A) = \sum\lambda_i$ and $\det(A) = \prod\lambda_i$

**Step 3:** For each $\lambda_i$, solve $(A-\lambda_i I)\mathbf{v} = \mathbf{0}$ for eigenvector $\mathbf{v}_i$

**Step 4:** Normalise: $\hat{\mathbf{v}}_i = \mathbf{v}_i / \|\mathbf{v}_i\|$

---

## 2.3 Full Example — 2×2 Matrix

$$A = \begin{bmatrix}4&1\\2&3\end{bmatrix}$$

**Step 1 — Characteristic equation:**

$$\det(A-\lambda I) = \det\begin{bmatrix}4-\lambda&1\\2&3-\lambda\end{bmatrix} = (4-\lambda)(3-\lambda)-2 = 0$$

$$= \lambda^2 - 7\lambda + 12 - 2 = \lambda^2 - 7\lambda + 10 = (\lambda-5)(\lambda-2) = 0$$

$$\lambda_1 = 5, \quad \lambda_2 = 2$$

**Step 2 — Verify:**

$$\text{tr}(A) = 4+3 = 7 = 5+2 \checkmark$$
$$\det(A) = 12-2 = 10 = 5\times 2 \checkmark$$

**Step 3a — Eigenvector for $\lambda_1 = 5$:**

$$(A-5I)\mathbf{v} = \begin{bmatrix}-1&1\\2&-2\end{bmatrix}\mathbf{v} = \mathbf{0}$$

Row reduce: $R_2 \leftarrow R_2 + 2R_1$:

$$\begin{bmatrix}-1&1\\0&0\end{bmatrix}\mathbf{v} = \mathbf{0} \implies -v_1+v_2=0 \implies v_1=v_2$$

$$\mathbf{v}_1 = \begin{bmatrix}1\\1\end{bmatrix}, \quad \hat{\mathbf{v}}_1 = \frac{1}{\sqrt{2}}\begin{bmatrix}1\\1\end{bmatrix}$$

**Step 3b — Eigenvector for $\lambda_2 = 2$:**

$$(A-2I)\mathbf{v} = \begin{bmatrix}2&1\\2&1\end{bmatrix}\mathbf{v} = \mathbf{0}$$

Row reduce: $R_2 \leftarrow R_2 - R_1$:

$$\begin{bmatrix}2&1\\0&0\end{bmatrix}\mathbf{v} = \mathbf{0} \implies 2v_1+v_2=0 \implies v_2=-2v_1$$

$$\mathbf{v}_2 = \begin{bmatrix}1\\-2\end{bmatrix}, \quad \hat{\mathbf{v}}_2 = \frac{1}{\sqrt{5}}\begin{bmatrix}1\\-2\end{bmatrix}$$

---

## 2.4 Full Example — 3×3 Matrix

$$A = \begin{bmatrix}2&0&0\\0&3&1\\0&1&3\end{bmatrix}$$

**Step 1 — Characteristic equation:**

Expand along row 1 (it has two zeros — makes life easy):

$$\det(A-\lambda I) = (2-\lambda)\det\begin{bmatrix}3-\lambda&1\\1&3-\lambda\end{bmatrix}$$

$$= (2-\lambda)[(3-\lambda)^2-1]$$

$$= (2-\lambda)[\lambda^2-6\lambda+9-1]$$

$$= (2-\lambda)(\lambda^2-6\lambda+8)$$

$$= (2-\lambda)(\lambda-2)(\lambda-4)$$

$$= -({\lambda-2})^2(\lambda-4) \cdot (-1) \implies \text{roots: }\lambda=2\text{ (double)},\ \lambda=4$$

$$\lambda_1 = 2,\quad \lambda_2 = 2,\quad \lambda_3 = 4$$

**Step 2 — Verify:**

$$\text{tr}(A) = 2+3+3 = 8 = 2+2+4 \checkmark$$
$$\det(A) = 2(9-1) = 16 = 2\times2\times4 \checkmark$$

**Step 3a — Eigenvectors for $\lambda = 2$:**

$$(A-2I)\mathbf{v} = \begin{bmatrix}0&0&0\\0&1&1\\0&1&1\end{bmatrix}\mathbf{v} = \mathbf{0}$$

Row reduce: $R_3 \leftarrow R_3 - R_2$:

$$\begin{bmatrix}0&0&0\\0&1&1\\0&0&0\end{bmatrix}$$

$v_2 + v_3 = 0 \implies v_2 = -v_3$. Both $v_1$ and $v_3$ are free.

Two independent eigenvectors (geometric multiplicity = 2):

$$\mathbf{v}_1 = \begin{bmatrix}1\\0\\0\end{bmatrix}, \quad \mathbf{v}_2 = \begin{bmatrix}0\\1\\-1\end{bmatrix}$$

**Step 3b — Eigenvector for $\lambda = 4$:**

$$(A-4I)\mathbf{v} = \begin{bmatrix}-2&0&0\\0&-1&1\\0&1&-1\end{bmatrix}\mathbf{v} = \mathbf{0}$$

From row 1: $-2v_1=0 \implies v_1=0$

From row 2: $-v_2+v_3=0 \implies v_2=v_3$

$$\mathbf{v}_3 = \begin{bmatrix}0\\1\\1\end{bmatrix}$$

---

## 2.5 Eigendecomposition $A = Q\Lambda Q^T$

**Only for symmetric matrices.** When $A$ is symmetric, eigenvectors are orthogonal and can be normalised to form an orthogonal matrix $Q$.

Using the 2×2 example ($\lambda_1=5, \lambda_2=2$):

$$Q = \begin{bmatrix}\hat{\mathbf{v}}_1 & \hat{\mathbf{v}}_2\end{bmatrix} = \begin{bmatrix}\frac{1}{\sqrt{2}}&\frac{1}{\sqrt{5}}\\\frac{1}{\sqrt{2}}&\frac{-2}{\sqrt{5}}\end{bmatrix}, \quad \Lambda = \begin{bmatrix}5&0\\0&2\end{bmatrix}$$

Wait — $A = \begin{bmatrix}4&1\\2&3\end{bmatrix}$ is NOT symmetric. Let us use $A = \begin{bmatrix}3&1\\1&3\end{bmatrix}$ instead.

$$A = \begin{bmatrix}3&1\\1&3\end{bmatrix}$$

**Eigenvalues:** $(3-\lambda)^2-1=0 \implies \lambda_1=2, \lambda_2=4$

**Eigenvectors:**

For $\lambda_1=2$: $v_1=v_2 \implies \hat{\mathbf{v}}_1 = \frac{1}{\sqrt{2}}\begin{bmatrix}1\\-1\end{bmatrix}$

Wait: $(A-2I) = \begin{bmatrix}1&1\\1&1\end{bmatrix} \implies v_1+v_2=0 \implies v_1=-v_2$, so $\hat{\mathbf{v}}_1=\frac{1}{\sqrt{2}}\begin{bmatrix}1\\-1\end{bmatrix}$

For $\lambda_2=4$: $(A-4I) = \begin{bmatrix}-1&1\\1&-1\end{bmatrix} \implies v_1=v_2$, so $\hat{\mathbf{v}}_2=\frac{1}{\sqrt{2}}\begin{bmatrix}1\\1\end{bmatrix}$

**Verify orthogonality:** $\hat{\mathbf{v}}_1^T\hat{\mathbf{v}}_2 = \frac{1}{2}(1-1)=0$ ✓

**Eigendecomposition:**

This is one of the most important concepts in Linear Algebra. The short answer is:

* **(A = PDP^{-1})** is the **general eigendecomposition** for any diagonalizable matrix.
* **(A = Q\Lambda Q^T)** is a **special case** that applies only to **real symmetric matrices**.

Let's compare them.

---

## 1. General Eigendecomposition

[
\boxed{A=PDP^{-1}}
]

where:

* (P) = matrix whose columns are the eigenvectors of (A)
* (D) = diagonal matrix of eigenvalues
* (P^{-1}) = inverse of (P)

### Conditions

* (A) must be **diagonalizable**.
* (A) does **not** have to be symmetric.

Example:

[
A=
\begin{bmatrix}
4&1\
2&3
\end{bmatrix}
]

This matrix is diagonalizable, so

[
A=PDP^{-1}.
]

Here, the eigenvectors are **not necessarily orthogonal**, so (P^{-1}\neq P^T).

---

## 2. Spectral Decomposition

[
\boxed{A=Q\Lambda Q^T}
]

where:

* (Q) = matrix of **orthonormal** eigenvectors
* (\Lambda) = diagonal matrix of eigenvalues
* (Q^T) = transpose of (Q)

Notice there is **no inverse**.

Why?

Because for an orthogonal matrix,

[
Q^{-1}=Q^T.
]

---

## Why is (Q^{-1}=Q^T)?

The columns of (Q) are orthonormal:

* Unit length
* Mutually perpendicular

Therefore,

[
Q^TQ=QQ^T=I,
]

which means

[
Q^{-1}=Q^T.
]

---

## When can we use (Q\Lambda Q^T)?

**Only when**

[
\boxed{A=A^T}
]

i.e., (A) is a **real symmetric matrix**.

This is guaranteed by the **Spectral Theorem**:

> Every real symmetric matrix has real eigenvalues and a complete set of orthonormal eigenvectors.

---

## Example

Consider

[
A=
\begin{bmatrix}
2&1\
1&2
\end{bmatrix}.
]

This matrix is symmetric because

[
A^T=A.
]

Its eigenvectors are

[
\frac1{\sqrt2}
\begin{bmatrix}
1\
1
\end{bmatrix},
\qquad
\frac1{\sqrt2}
\begin{bmatrix}
1\
-1
\end{bmatrix}.
]

These are orthonormal, so

[
Q=
\frac1{\sqrt2}
\begin{bmatrix}
1&1\
1&-1
\end{bmatrix}.
]

Since (Q) is orthogonal,

[
Q^{-1}=Q^T,
]

and therefore

[
A=Q\Lambda Q^T.
]

---

## Comparison Table

| Feature                | (A=PDP^{-1})              | (A=Q\Lambda Q^T)             |
| ---------------------- | ------------------------- | ---------------------------- |
| Applies to             | Any diagonalizable matrix | Real symmetric matrices only |
| Eigenvectors           | Linearly independent      | Orthonormal                  |
| Matrix of eigenvectors | (P)                       | (Q)                          |
| Inverse                | (P^{-1})                  | (Q^T)                        |
| Need symmetry?         | No                        | Yes                          |
| Special theorem        | Diagonalization           | Spectral Theorem             |

---

## IIT Exam Trick

When you see a matrix satisfying

[
A=A^T,
]

immediately think:

* ✔ Real eigenvalues
* ✔ Orthogonal eigenvectors
* ✔ (Q^{-1}=Q^T)
* ✔ Use **(A=Q\Lambda Q^T)**

Otherwise, if the matrix is only known to be diagonalizable, use

[
A=PDP^{-1}.
]

### Quick Check

Suppose

[
A=
\begin{bmatrix}
3&2\
2&3
\end{bmatrix}.
]

Since (A=A^T), it is symmetric. You should **prefer** the form

[
A=Q\Lambda Q^T,
]

although writing it as (A=PDP^{-1}) is also mathematically correct. The advantage of the spectral decomposition is that the inverse is replaced by the simpler transpose because the eigenvectors can be chosen to be orthonormal.


$$Q = \frac{1}{\sqrt{2}}\begin{bmatrix}1&1\\-1&1\end{bmatrix}, \quad \Lambda = \begin{bmatrix}2&0\\0&4\end{bmatrix}$$

$$A = Q\Lambda Q^T = \frac{1}{\sqrt{2}}\begin{bmatrix}1&1\\-1&1\end{bmatrix}\begin{bmatrix}2&0\\0&4\end{bmatrix}\frac{1}{\sqrt{2}}\begin{bmatrix}1&-1\\1&1\end{bmatrix}$$

$$= \frac{1}{2}\begin{bmatrix}2&4\\-2&4\end{bmatrix}\begin{bmatrix}1&-1\\1&1\end{bmatrix} = \frac{1}{2}\begin{bmatrix}6&2\\2&6\end{bmatrix} = \begin{bmatrix}3&1\\1&3\end{bmatrix} \checkmark$$

**Using eigendecomposition to compute $A^k$:**

$$A^3 = Q\Lambda^3 Q^T, \quad \Lambda^3 = \begin{bmatrix}8&0\\0&64\end{bmatrix}$$

$$A^3 = \frac{1}{2}\begin{bmatrix}1&1\\-1&1\end{bmatrix}\begin{bmatrix}8&0\\0&64\end{bmatrix}\begin{bmatrix}1&-1\\1&1\end{bmatrix} = \frac{1}{2}\begin{bmatrix}72&56\\56&72\end{bmatrix} = \begin{bmatrix}36&28\\28&36\end{bmatrix}$$

---

---

# PART 3 — SINGULAR VALUE DECOMPOSITION (SVD)

---

## 3.1 What is SVD?

**Any** $m\times n$ matrix $A$ can be decomposed as:

$$A = U\Sigma V^T$$

| Matrix | Size | Contents |
|--------|------|---------|
| $U$ | $m\times m$ | Orthogonal — left singular vectors (eigenvectors of $AA^T$) |
| $\Sigma$ | $m\times n$ | Diagonal — singular values $\sigma_i = \sqrt{\lambda_i} \geq 0$ |
| $V$ | $n\times n$ | Orthogonal — right singular vectors (eigenvectors of $A^TA$) |

---

## 3.2 Algorithm — Step by Step

**Step 1:** Compute $A^TA$ (size $n\times n$)

**Step 2:** Find eigenvalues $\lambda_1\geq\lambda_2\geq\cdots\geq0$ of $A^TA$

**Step 3:** Singular values: $\sigma_i = \sqrt{\lambda_i}$

**Step 4:** Right singular vectors $V$: normalised eigenvectors of $A^TA$

**Step 5:** Left singular vectors $U$: $\mathbf{u}_i = \frac{A\mathbf{v}_i}{\sigma_i}$ for each nonzero $\sigma_i$

**Step 6:** Verify $A = U\Sigma V^T$

---

## 3.3 Full Example

$$A = \begin{bmatrix}1&1\\0&1\\1&0\end{bmatrix} \quad (3\times2)$$

**Step 1 — Compute $A^TA$:**

$$A^TA = \begin{bmatrix}1&0&1\\1&1&0\end{bmatrix}\begin{bmatrix}1&1\\0&1\\1&0\end{bmatrix} = \begin{bmatrix}1+0+1&1+0+0\\1+0+0&1+1+0\end{bmatrix} = \begin{bmatrix}2&1\\1&2\end{bmatrix}$$

**Step 2 — Eigenvalues of $A^TA$:**

$$\det\begin{bmatrix}2-\lambda&1\\1&2-\lambda\end{bmatrix} = (2-\lambda)^2-1 = 0$$

$$\lambda^2-4\lambda+3=0 \implies (\lambda-3)(\lambda-1)=0$$

$$\lambda_1=3, \quad \lambda_2=1$$

**Step 3 — Singular values:**

$$\sigma_1=\sqrt{3}, \quad \sigma_2=\sqrt{1}=1$$

$$\Sigma = \begin{bmatrix}\sqrt{3}&0\\0&1\\0&0\end{bmatrix} \quad (3\times2)$$

**Step 4 — Right singular vectors $V$ (eigenvectors of $A^TA$):**

For $\lambda_1=3$: $(A^TA-3I)\mathbf{v}=\begin{bmatrix}-1&1\\1&-1\end{bmatrix}\mathbf{v}=\mathbf{0} \implies v_1=v_2$

$$\mathbf{v}_1 = \frac{1}{\sqrt{2}}\begin{bmatrix}1\\1\end{bmatrix}$$

For $\lambda_2=1$: $(A^TA-I)\mathbf{v}=\begin{bmatrix}1&1\\1&1\end{bmatrix}\mathbf{v}=\mathbf{0} \implies v_1=-v_2$

$$\mathbf{v}_2 = \frac{1}{\sqrt{2}}\begin{bmatrix}1\\-1\end{bmatrix}$$

$$V = \frac{1}{\sqrt{2}}\begin{bmatrix}1&1\\1&-1\end{bmatrix}$$

**Step 5 — Left singular vectors $U$:**

$$\mathbf{u}_1 = \frac{A\mathbf{v}_1}{\sigma_1} = \frac{1}{\sqrt{3}}\cdot\begin{bmatrix}1&1\\0&1\\1&0\end{bmatrix}\cdot\frac{1}{\sqrt{2}}\begin{bmatrix}1\\1\end{bmatrix} = \frac{1}{\sqrt{6}}\begin{bmatrix}2\\1\\1\end{bmatrix}$$

$$\mathbf{u}_2 = \frac{A\mathbf{v}_2}{\sigma_2} = \frac{1}{1}\cdot\begin{bmatrix}1&1\\0&1\\1&0\end{bmatrix}\cdot\frac{1}{\sqrt{2}}\begin{bmatrix}1\\-1\end{bmatrix} = \frac{1}{\sqrt{2}}\begin{bmatrix}0\\-1\\1\end{bmatrix}$$

For $\mathbf{u}_3$: find a vector orthogonal to both $\mathbf{u}_1$ and $\mathbf{u}_2$. By inspection or cross product:

$$\mathbf{u}_3 = \frac{1}{\sqrt{3}}\begin{bmatrix}1\\-1\\-1\end{bmatrix}$$

Verify: $\mathbf{u}_1^T\mathbf{u}_3 = \frac{1}{\sqrt{18}}(2-1-1)=0$ ✓, $\mathbf{u}_2^T\mathbf{u}_3 = \frac{1}{\sqrt{6}}(0+1-1)=0$ ✓

$$U = \begin{bmatrix}\frac{2}{\sqrt{6}}&0&\frac{1}{\sqrt{3}}\\\frac{1}{\sqrt{6}}&\frac{-1}{\sqrt{2}}&\frac{-1}{\sqrt{3}}\\\frac{1}{\sqrt{6}}&\frac{1}{\sqrt{2}}&\frac{-1}{\sqrt{3}}\end{bmatrix}$$

**Final SVD:**

$$A = U\Sigma V^T = \begin{bmatrix}\mathbf{u}_1&\mathbf{u}_2&\mathbf{u}_3\end{bmatrix}\begin{bmatrix}\sqrt{3}&0\\0&1\\0&0\end{bmatrix}\begin{bmatrix}\mathbf{v}_1^T\\\mathbf{v}_2^T\end{bmatrix}$$

---

## 3.4 Reading Key Facts from SVD

Once you have $A=U\Sigma V^T$, you can immediately state:

| Quantity | How to read it |
|---------|---------------|
| $\text{rank}(A)$ | Number of non-zero singular values |
| $\text{null}(A)$ | Columns of $V$ corresponding to $\sigma=0$ |
| $\text{col}(A)$ | Columns of $U$ corresponding to $\sigma\neq0$ |
| $\|A\|_F$ (Frobenius norm) | $\sqrt{\sigma_1^2+\sigma_2^2+\cdots}$ |
| Best rank-$k$ approximation | $A_k = \sum_{i=1}^k \sigma_i\mathbf{u}_i\mathbf{v}_i^T$ |
| Pseudo-inverse $A^+$ | $V\Sigma^+U^T$ where $\Sigma^+$ replaces $\sigma_i$ with $1/\sigma_i$ |

---

---

# PART 4 — COVARIANCE MATRIX

---

## 4.1 What is the Covariance Matrix?

For a dataset with $n$ observations and $p$ features, the covariance matrix $C$ is $p\times p$ and captures how every pair of features varies together.

$$C_{ij} = \text{Cov}(X_i, X_j) = \frac{1}{n-1}\sum_{k=1}^n (x_{ki}-\bar{x}_i)(x_{kj}-\bar{x}_j)$$

**Diagonal entries:** $C_{ii} = \text{Var}(X_i)$ — variance of feature $i$

**Off-diagonal entries:** $C_{ij}$ — covariance between features $i$ and $j$

**Key properties:** $C$ is always symmetric and positive semi-definite.

---

## 4.2 Computing the Covariance Matrix — Step by Step

**Step 1:** Arrange data as $n\times p$ matrix $X$ (rows = observations, columns = features)

**Step 2:** Centre each column by subtracting its mean: $\tilde{X}_{ki} = X_{ki} - \bar{X}_i$

**Step 3:** Compute:

$$C = \frac{1}{n-1}\tilde{X}^T\tilde{X}$$

---

## 4.3 Full Example

**Data:** 4 observations, 2 features:

$$X = \begin{bmatrix}2&1\\4&3\\6&5\\8&7\end{bmatrix}$$

**Step 1 — Compute column means:**

$$\bar{X}_1 = \frac{2+4+6+8}{4} = 5, \quad \bar{X}_2 = \frac{1+3+5+7}{4} = 4$$

**Step 2 — Centre the data:**

$$\tilde{X} = X - \bar{X} = \begin{bmatrix}2-5&1-4\\4-5&3-4\\6-5&5-4\\8-5&7-4\end{bmatrix} = \begin{bmatrix}-3&-3\\-1&-1\\1&1\\3&3\end{bmatrix}$$

**Step 3 — Compute $\tilde{X}^T\tilde{X}$:**

$$\tilde{X}^T\tilde{X} = \begin{bmatrix}-3&-1&1&3\\-3&-1&1&3\end{bmatrix}\begin{bmatrix}-3&-3\\-1&-1\\1&1\\3&3\end{bmatrix} = \begin{bmatrix}9+1+1+9&9+1+1+9\\9+1+1+9&9+1+1+9\end{bmatrix} = \begin{bmatrix}20&20\\20&20\end{bmatrix}$$

**Step 4 — Divide by $n-1=3$:**

$$C = \frac{1}{3}\begin{bmatrix}20&20\\20&20\end{bmatrix} = \begin{bmatrix}6.67&6.67\\6.67&6.67\end{bmatrix}$$

**Interpretation:**
- $C_{11}=6.67$ = variance of feature 1
- $C_{22}=6.67$ = variance of feature 2
- $C_{12}=6.67$ = covariance between features (perfectly correlated here because feature 2 = feature 1 − 1)

---

## 4.4 Structure of the Covariance Matrix

For $p=3$ features:

$$C = \begin{bmatrix}\text{Var}(X_1) & \text{Cov}(X_1,X_2) & \text{Cov}(X_1,X_3)\\\text{Cov}(X_2,X_1) & \text{Var}(X_2) & \text{Cov}(X_2,X_3)\\\text{Cov}(X_3,X_1) & \text{Cov}(X_3,X_2) & \text{Var}(X_3)\end{bmatrix}$$

Note: $C_{ij}=C_{ji}$ always — covariance matrix is symmetric.

---

---

# PART 5 — PCA USING EIGENDECOMPOSITION OF COVARIANCE MATRIX

---

## 5.1 Full PCA Example — End to End

**Data:** 5 observations, 2 features:

$$X = \begin{bmatrix}2&4\\3&5\\4&4\\5&6\\6&7\end{bmatrix}$$

**Step 1 — Compute means and centre:**

$$\bar{X}_1=4, \quad \bar{X}_2=5.2$$

$$\tilde{X} = \begin{bmatrix}-2&-1.2\\-1&-0.2\\0&-1.2\\1&0.8\\2&1.8\end{bmatrix}$$

**Step 2 — Compute covariance matrix ($n-1=4$):**

$$\tilde{X}^T\tilde{X} = \begin{bmatrix}(-2)^2+(-1)^2+0^2+1^2+2^2 & (-2)(-1.2)+(-1)(-0.2)+(0)(-1.2)+(1)(0.8)+(2)(1.8)\\(\ldots) & (-1.2)^2+(-0.2)^2+(-1.2)^2+(0.8)^2+(1.8)^2\end{bmatrix}$$

$$= \begin{bmatrix}4+1+0+1+4 & 2.4+0.2+0+0.8+3.6\\(\ldots) & 1.44+0.04+1.44+0.64+3.24\end{bmatrix} = \begin{bmatrix}10&7\\7&6.8\end{bmatrix}$$

$$C = \frac{1}{4}\begin{bmatrix}10&7\\7&6.8\end{bmatrix} = \begin{bmatrix}2.5&1.75\\1.75&1.7\end{bmatrix}$$

**Step 3 — Eigenvalues of $C$:**

$$\det(C-\lambda I) = (2.5-\lambda)(1.7-\lambda) - 1.75^2 = 0$$

$$\lambda^2 - 4.2\lambda + 4.25 - 3.0625 = 0$$

$$\lambda^2 - 4.2\lambda + 1.1875 = 0$$

$$\lambda = \frac{4.2\pm\sqrt{17.64-4.75}}{2} = \frac{4.2\pm\sqrt{12.89}}{2} = \frac{4.2\pm3.59}{2}$$

$$\lambda_1 = 3.895, \quad \lambda_2 = 0.305$$

**Step 4 — Variance explained:**

$$\text{Total variance} = \lambda_1+\lambda_2 = 4.2$$

$$\text{PC}_1\text{ explains: }\frac{3.895}{4.2} = 92.7\%$$

$$\text{PC}_2\text{ explains: }\frac{0.305}{4.2} = 7.3\%$$

**One principal component explains 92.7% of variance.**

**Step 5 — First principal component direction:**

For $\lambda_1=3.895$: $(C-3.895I)\mathbf{v}=\mathbf{0}$

$$\begin{bmatrix}-1.395&1.75\\1.75&-2.195\end{bmatrix}\mathbf{v}=\mathbf{0}$$

From row 1: $-1.395v_1+1.75v_2=0 \implies v_1=\frac{1.75}{1.395}v_2=1.255v_2$

$$\mathbf{v}_1 = \begin{bmatrix}1.255\\1\end{bmatrix} \implies \hat{\mathbf{v}}_1 = \frac{1}{\sqrt{1.255^2+1}}\begin{bmatrix}1.255\\1\end{bmatrix} = \frac{1}{1.607}\begin{bmatrix}1.255\\1\end{bmatrix} \approx \begin{bmatrix}0.781\\0.623\end{bmatrix}$$

**Step 6 — Project data onto PC1:**

$$\mathbf{z} = \tilde{X}\hat{\mathbf{v}}_1 = \begin{bmatrix}-2&-1.2\\-1&-0.2\\0&-1.2\\1&0.8\\2&1.8\end{bmatrix}\begin{bmatrix}0.781\\0.623\end{bmatrix} \approx \begin{bmatrix}-2.309\\-0.906\\-0.748\\1.279\\2.684\end{bmatrix}$$

These are the **1D representations** of the 5 data points along the direction of maximum variance.

---

---

# QUICK REFERENCE CARD

## RREF

```
Goal: pivots = 1, zeros everywhere else in pivot columns

Steps:
1. Get a nonzero entry in pivot position (swap rows if needed)
2. Scale that row so pivot = 1
3. Eliminate ALL other entries in that column (above and below)
4. Move to next column and repeat
5. Free columns = no pivot → free variables
```

## Eigendecomposition

```
1. det(A - λI) = 0  →  find λ values
2. Verify: tr(A) = Σλᵢ  and  det(A) = Πλᵢ
3. For each λ: solve (A - λI)v = 0  →  find eigenvectors
4. Normalise: v̂ = v/||v||
5. Symmetric A: A = QΛQᵀ  where Q = [v̂₁ v̂₂ ... v̂ₙ]
6. Powers: Aᵏ = QΛᵏQᵀ
```

## SVD

```
1. Compute AᵀA  (n×n)
2. Eigenvalues of AᵀA → λ₁ ≥ λ₂ ≥ ... ≥ 0
3. σᵢ = √λᵢ  →  form Σ
4. Eigenvectors of AᵀA → columns of V
5. uᵢ = Avᵢ/σᵢ  →  columns of U
6. A = UΣVᵀ
```

## Covariance Matrix

```
1. Centre data: X̃ = X - mean(X)
2. C = X̃ᵀX̃ / (n-1)
3. Diagonal = variances
4. Off-diagonal = covariances
5. Eigendecompose C for PCA
6. Variance explained by PCᵢ = λᵢ / Σλⱼ
```
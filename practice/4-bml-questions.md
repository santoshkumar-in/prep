Let me re-read everything carefully before generating.Now I have everything. Generating 50 questions.

---

# BASIC MACHINE LEARNING — 50 PRACTICE QUESTIONS

## IIT M.Tech AI/ML Entrance | Medium to High Difficulty

**Format:** **[MCQ]** = single correct | **[MSQ]** = one or more correct | **[NUM]** = fill-in numerical

**Topic distribution:** Linear Regression (Q1–10) | Logistic Regression (Q11–20) | Classification Metrics & ROC (Q21–32) | kNN (Q33–39) | K-Means Clustering (Q40–45) | Cross-Validation & Bias-Variance (Q46–50)

---

---

## SECTION 1 — LINEAR REGRESSION

---

### Q1 [MCQ] ★★

_(Direct from Sample Paper Q18)_

The line $\hat{y} = ax + b$ is fitted to data points using linear regression. Let $d_1, d_2, d_3, d_4$ be the vertical deviations from each data point to the line. Which statement is correct?

(a) $d_1^2 + d_2^2 + d_3^2 + d_4^2$ should be maximum
(b) $(d_1^2 + d_3^2)$ should equal $(d_2^2 + d_4^2)$
(c) $d_1^2 + d_2^2 + d_3^2 + d_4^2$ should equal zero
(d) $d_1^2 + d_2^2 + d_3^2 + d_4^2$ should be minimum

---

**SOLUTION**

$$\boxed{(d)}$$

OLS (Ordinary Least Squares) finds parameters $a$ and $b$ that **minimise** the sum of squared residuals:

$$\text{SSE} = \sum_i d_i^2 = \sum_i (y_i - \hat{y}_i)^2$$

**(a) FALSE** — maximising SSE would give the worst possible line.
**(b) FALSE** — no such symmetric property exists.
**(c) FALSE** — SSE = 0 only if all points lie exactly on the line, which is generally impossible for real data.
**(d) TRUE** ⭐ — this is the defining criterion of OLS.

---

### Q2 [MCQ] ★★★

_(Style: Sample Paper Q10 — Monotonicity)_

The following data is given:

| $x$ | 6.37  | -5.26 | 1.48 | -1.74 | -4.35 | -1.44 | -0.72 |
| --- | ----- | ----- | ---- | ----- | ----- | ----- | ----- |
| $y$ | 10.47 | -3.48 | 4.61 | 0.74  | -2.39 | 1.10  | 1.97  |

Which best describes the behaviour of $y$ as $x$ increases?

(a) Non-monotonic
(b) Monotonic increase
(c) Monotonic decrease
(d) None of the above

---

**SOLUTION**

**Method:** Sort the data by $x$ and check if $y$ consistently increases.

Sorted by $x$: $(-5.26,-3.48), (-4.35,-2.39), (-1.74,0.74), (-1.44,1.10), (-0.72,1.97), (1.48,4.61), (6.37,10.47)$

As $x$ increases: $y$ goes $-3.48 \to -2.39 \to 0.74 \to 1.10 \to 1.97 \to 4.61 \to 10.47$ — **strictly increasing** at every step.

$$\boxed{(b) \ \text{Monotonic increase}}$$

> **Exam insight:** This tests whether you recognise a monotone increasing relationship. Sorting by $x$ and checking $y$ is the clearest approach. The pattern is consistent — Spearman rank correlation would be $r_s = 1$.

---

### Q3 [NUM] ★★★

Five data points are given: $(1,2), (2,4), (3,5), (4,4), (5,5)$. Fit a simple linear regression $\hat{y} = \beta_0 + \beta_1 x$ using OLS. Find $\hat{\beta}_1$, $\hat{\beta}_0$, and $R^2$.

---

**SOLUTION**

$n=5$, $\bar{x}=3$, $\bar{y}=(2+4+5+4+5)/5=4$

$$S_{XX} = \sum(x_i-\bar{x})^2 = 4+1+0+1+4 = 10$$

$$S_{XY} = \sum(x_i-\bar{x})(y_i-\bar{y}) = (-2)(-2)+(-1)(0)+(0)(1)+(1)(0)+(2)(1) = 4+0+0+0+2 = 6$$

$$\hat{\beta}_1 = \frac{S_{XY}}{S_{XX}} = \frac{6}{10} = 0.6, \quad \hat{\beta}_0 = 4 - 0.6(3) = 2.2$$

**Fitted values:** $\hat{y}$: 2.8, 3.4, 4.0, 4.6, 5.2

**SSE:**
$(2-2.8)^2+(4-3.4)^2+(5-4)^2+(4-4.6)^2+(5-5.2)^2 = 0.64+0.36+1+0.36+0.04 = 2.4$

$$S_{YY} = \sum(y_i-\bar{y})^2 = 4+0+1+0+1 = 6$$

$$R^2 = 1 - \frac{SSE}{SST} = 1 - \frac{2.4}{6} = 1 - 0.4 = 0.6$$

$$\boxed{\hat{\beta}_1=0.6,\quad \hat{\beta}_0=2.2,\quad R^2=0.6}$$

---

### Q4 [MSQ] ★★★

Which of the following statements about $R^2$ (coefficient of determination) are TRUE?

(a) $R^2 = r^2$ where $r$ is the Pearson correlation coefficient, for simple linear regression.
(b) $R^2$ always increases when more predictors are added to a model.
(c) Adjusted $R^2$ can decrease when a useless predictor is added.
(d) $R^2 = 1$ means the model perfectly fits the data.
(e) A high $R^2$ guarantees the model is appropriate (no non-linearity).

---

**SOLUTION**

**(a) TRUE.** ⭐ For simple LR: $R^2 = r_{XY}^2$. This is a fundamental relationship.

**(b) TRUE.** ⭐ Plain $R^2$ ALWAYS increases (or stays the same) when you add predictors — even random noise increases it. This is why we use Adjusted $R^2$.

**(c) TRUE.** ⭐ Adjusted $R^2$ penalises for extra parameters: $R^2_{adj} = 1-(1-R^2)\frac{n-1}{n-p-1}$. Adding a useless variable increases $p$ without improving $R^2$ enough → Adjusted $R^2$ decreases.

**(d) TRUE.** $R^2=1 \implies SSE=0 \implies$ all residuals are zero $\implies$ perfect fit.

**(e) FALSE.** ⭐ Classic Anscombe's Quartet lesson — four datasets with identical $R^2$ but completely different patterns. High $R^2$ does NOT mean the linear model is appropriate. Always check residual plots.

**Answer: (a), (b), (c), (d)**

---

### Q5 [MCQ] ★★★

In multiple linear regression $\hat{\mathbf{y}} = A\hat{\boldsymbol{\beta}}$, the hat matrix (projection matrix) is $P = A(A^TA)^{-1}A^T$. Which property does $P$ NOT satisfy?

(a) $P^2 = P$
(b) $P^T = P$
(c) $P^{-1} = P^T$
(d) The eigenvalues of $P$ are only 0 or 1

---

**SOLUTION**

$$\boxed{(c)}$$

$P^{-1}=P^T$ is a property of orthogonal matrices, NOT projection matrices. A projection matrix collapses some directions to zero — it cannot be inverted unless $P=I$.

**(a), (b), (d)** are all true for any projection matrix (idempotent, symmetric, eigenvalues in $\{0,1\}$).

> **Connection to ML:** $\hat{\mathbf{y}} = P\mathbf{y}$ — the fitted values are literally the projection of $\mathbf{y}$ onto the column space of the design matrix $A$. This is why OLS is also called the "projection" estimator.

---

### Q6 [MCQ] ★★★

The OLS estimate $\hat{\boldsymbol{\beta}} = (A^TA)^{-1}A^T\mathbf{y}$ exists if and only if:

(a) $A$ is a square matrix
(b) $A$ has full column rank (no multicollinearity)
(c) $A^TA$ has all positive eigenvalues
(d) Both (b) and (c) — they are equivalent

---

**SOLUTION**


$$\boxed{(d)}$$

The formula $(A^TA)^{-1}A^T\mathbf{y}$ requires inverting $A^TA$. A matrix is invertible if and only if all its eigenvalues are non-zero. So the question reduces to: **when is $A^TA$ invertible?**

---

**Why (b) and (c) are equivalent — and both correct**

**Direction 1 — Full column rank implies positive eigenvalues of $A^TA$:**

For any vector $\mathbf{v} \neq \mathbf{0}$:

$$\mathbf{v}^T(A^TA)\mathbf{v} = (A\mathbf{v})^T(A\mathbf{v}) = \|A\mathbf{v}\|^2$$

If $A$ has full column rank, then $\text{null}(A) = \{\mathbf{0}\}$, meaning $A\mathbf{v} \neq \mathbf{0}$ for all $\mathbf{v} \neq \mathbf{0}$. Therefore:

$$\mathbf{v}^T(A^TA)\mathbf{v} = \|A\mathbf{v}\|^2 > 0 \quad \text{for all } \mathbf{v} \neq \mathbf{0}$$

This is the definition of **positive definite** — all eigenvalues are strictly positive. So full column rank $\implies$ all eigenvalues of $A^TA$ are positive.

**Direction 2 — Positive eigenvalues of $A^TA$ implies full column rank:**

If all eigenvalues of $A^TA$ are positive, then $A^TA$ is positive definite, which means $\mathbf{v}^T(A^TA)\mathbf{v} > 0$ for all $\mathbf{v} \neq \mathbf{0}$. This means $\|A\mathbf{v}\|^2 > 0$ for all $\mathbf{v} \neq \mathbf{0}$, which means $A\mathbf{v} \neq \mathbf{0}$ for all $\mathbf{v} \neq \mathbf{0}$, which means $\text{null}(A) = \{\mathbf{0}\}$ — full column rank.

So the equivalence is complete:

$$A \text{ has full column rank} \iff A^TA \text{ is positive definite} \iff \text{all eigenvalues of } A^TA > 0 \iff A^TA \text{ is invertible}$$

---

**Why (a) is wrong**

$A$ does not need to be square. In regression, $A$ is the $n \times p$ design matrix with $n \gg p$ (many observations, few parameters) — it is tall, not square. What matters is full **column** rank, not squareness.

For example:

$$A = \begin{bmatrix}1\\2\\3\end{bmatrix} \quad \text{(3×1, not square, full column rank)}$$

$$A^TA = [1\ 2\ 3]\begin{bmatrix}1\\2\\3\end{bmatrix} = 14 \quad \text{(invertible — just divide by 14)}$$

OLS works perfectly here despite $A$ being non-square.

---

**What happens when full column rank fails (multicollinearity)**

If two columns of $A$ are identical or proportional — say column 2 equals column 3 — then $A$ does NOT have full column rank. Some $\mathbf{v} \neq \mathbf{0}$ exists with $A\mathbf{v} = \mathbf{0}$, making $\|A\mathbf{v}\|^2 = 0$. Then $A^TA$ has a zero eigenvalue, is singular, and $(A^TA)^{-1}$ does not exist. The OLS estimate has infinitely many solutions — the system cannot pin down unique coefficient values.

**Fix:** Remove one of the collinear columns, or use Ridge regression which replaces $A^TA$ with $A^TA + \lambda I$ — this adds $\lambda > 0$ to every eigenvalue, guaranteeing all eigenvalues are at least $\lambda > 0$ and the matrix is always invertible.

---

### Q7 [NUM] ★★★

A regression model is fitted on $n=20$ observations with $p=3$ predictors. $SST = 100$, $SSE = 40$.

Find: (i) $R^2$, (ii) Adjusted $R^2$, (iii) $F$-statistic, (iv) $MSE$.

---

**SOLUTION**

**(i) $R^2$:**
$$R^2 = 1 - \frac{SSE}{SST} = 1 - \frac{40}{100} = \boxed{0.60}$$

**(ii) Adjusted $R^2$:**
$$R^2_{adj} = 1 - (1-R^2)\frac{n-1}{n-p-1} = 1 - 0.4\times\frac{19}{16} = 1 - 0.475 = \boxed{0.525}$$

**(iii) $F$-statistic:** $SSReg = SST - SSE = 60$

$$F = \frac{SSReg/p}{SSE/(n-p-1)} = \frac{60/3}{40/16} = \frac{20}{2.5} = \boxed{8.0}$$

**(iv) $MSE$:**
$$MSE = \frac{SSE}{n-p-1} = \frac{40}{16} = \boxed{2.5}$$

---

### Q8 [MSQ] ★★★

Which of the following are valid assumptions of OLS linear regression (LINE assumptions)?

(a) The relationship between $X$ and $Y$ is linear.
(b) The error terms $\varepsilon_i$ are independent.
(c) The error terms are normally distributed with mean 0.
(d) The variance of error terms is constant (homoscedasticity).
(e) All predictors must be uncorrelated with each other.

---

**SOLUTION**

The LINE assumptions:

- **L**inearity, **I**ndependence, **N**ormality of errors, **E**qual variance

**(a) TRUE** — Linearity. $Y = A\boldsymbol{\beta} + \boldsymbol{\varepsilon}$.

**(b) TRUE** — Independence. $\varepsilon_i$ and $\varepsilon_j$ are uncorrelated for $i\neq j$.

**(c) TRUE** — Normality. $\varepsilon_i \sim N(0,\sigma^2)$.

**(d) TRUE** — Equal variance (homoscedasticity). $\text{Var}(\varepsilon_i)=\sigma^2$ constant.

**(e) FALSE** — ⭐ Correlated predictors (multicollinearity) is NOT an OLS assumption violation — the estimates are still unbiased. Multicollinearity makes estimates unstable (high variance) but doesn't break the model assumptions.

**Answer: (a), (b), (c), (d)**

---

### Q9 [MCQ] ★★★

A residual plot shows a clear fan shape (residuals increasing in spread as fitted values increase). This indicates:

(a) The linearity assumption is violated.
(b) The homoscedasticity assumption is violated.
(c) The normality assumption is violated.
(d) The independence assumption is violated.

---

**SOLUTION**

$$\boxed{(b)}$$

A **fan shape** (residuals spreading out as $\hat{y}$ increases) is the classic signature of **heteroscedasticity** — the variance of errors is not constant, it increases with the fitted values.

**(a)** Violated linearity shows as a curved pattern (not fan-shaped) in residuals vs fitted.
**(c)** Violated normality shows as non-linear QQ plot.
**(d)** Violated independence shows as autocorrelation pattern (runs of positive/negative residuals).

---

### Q10 [NUM] ★★★

Ridge regression adds $\lambda\|\boldsymbol{\beta}\|^2$ to the OLS objective. For what value of $\lambda$ does Ridge reduce to OLS? What happens as $\lambda\to\infty$?

---

**SOLUTION**

**Ridge solution:** $\hat{\boldsymbol{\beta}}_{Ridge} = (A^TA + \lambda I)^{-1}A^T\mathbf{y}$

**When $\lambda=0$:** $(A^TA + 0)^{-1}A^T\mathbf{y} = (A^TA)^{-1}A^T\mathbf{y} = \hat{\boldsymbol{\beta}}_{OLS}$. Ridge reduces to OLS. ⭐

**As $\lambda\to\infty$:** The term $\lambda I$ dominates $A^TA$:
$$(A^TA + \lambda I)^{-1} \approx \frac{1}{\lambda}I \to 0$$

So $\hat{\boldsymbol{\beta}}_{Ridge} \to \mathbf{0}$ — all coefficients shrink to zero. ⭐

$$\boxed{\lambda=0 \implies \text{OLS};\quad \lambda\to\infty \implies \hat{\boldsymbol{\beta}}\to\mathbf{0}}$$

> **ML interpretation:** Ridge regularisation applies "shrinkage" — it trades a small increase in bias for a large decrease in variance. This is the bias-variance tradeoff in action.

---

## SECTION 2 — LOGISTIC REGRESSION

---

### Q11 [MCQ] ★★

_(Direct from Sample Paper Q2)_

What are the values of the sigmoid function $\sigma(x) = \frac{1}{1+e^{-x}}$ when $x=-\infty$ and $x=+\infty$?

(a) 1, 0
(b) $-\infty$, $+\infty$
(c) 0, 1
(d) $+\infty$, $-\infty$

---

**SOLUTION**

$$\sigma(-\infty) = \frac{1}{1+e^{+\infty}} = \frac{1}{\infty} = 0$$

$$\sigma(+\infty) = \frac{1}{1+e^{-\infty}} = \frac{1}{1+0} = 1$$

$$\boxed{(c) \ 0, 1}$$

> **Trap:** Option (a) reverses the order. The sigmoid goes from 0 (at $-\infty$) to 1 (at $+\infty$), not from 1 to 0.

---

### Q12 [MCQ] ★★

_(Direct from Sample Paper Q9)_

In logistic regression, if the posterior probability $P(\text{Class}=k | X=x)$ is linear in $x$, then:

(a) The decision boundary is linear
(b) $x$ is not related to $Y$
(c) There is no decision boundary
(d) The decision boundary is non-linear

---

**SOLUTION**

$$\boxed{(a)}$$

In logistic regression: $\log\frac{P(Y=1|x)}{P(Y=0|x)} = \beta_0 + \beta_1 x$ (linear in $x$)

The decision boundary is the set of points where $P(Y=1|x) = 0.5$, i.e., where the log-odds $= 0$:
$$\beta_0 + \beta_1 x = 0 \implies x = -\beta_0/\beta_1$$

This defines a **hyperplane** (linear boundary) in feature space. ⭐

---

### Q13 [MSQ] ★★★

Which of the following are TRUE about the sigmoid function $\sigma(z) = \frac{1}{1+e^{-z}}$?

(a) $\sigma(z) \in (0,1)$ for all $z\in\mathbb{R}$
(b) $\sigma(0) = 0.5$
(c) $\sigma(-z) = 1 - \sigma(z)$
(d) $\sigma'(z) = \sigma(z)(1-\sigma(z))$
(e) $\sigma(z) \geq 1$ for $z>0$

---

**SOLUTION**

**(a) TRUE.** ⭐ $e^{-z}>0$ always, so $1+e^{-z}>1$, giving $\sigma(z)\in(0,1)$.

**(b) TRUE.** $\sigma(0)=\frac{1}{1+e^0}=\frac{1}{2}=0.5$.

**(c) TRUE.** ⭐ $\sigma(-z)=\frac{1}{1+e^z}=1-\frac{e^z}{1+e^z}=1-\frac{1}{1+e^{-z}}=1-\sigma(z)$.

**(d) TRUE.** ⭐ This is the famous sigmoid derivative — crucial for backpropagation. $\sigma'(z)=\sigma(z)(1-\sigma(z))$.

**(e) FALSE.** $\sigma(z)\in(0,1)$ always, never $\geq 1$.

**Answer: (a), (b), (c), (d)**

---

### Q14 [MCQ] ★★★

Logistic regression models $P(Y=1|x) = \sigma(\beta_0+\beta_1 x)$. The fitted model gives $\beta_0=-4$ and $\beta_1=0.05$. What is the predicted probability of $Y=1$ when $x=80$?

(a) 0.268
(b) 0.500
(c) 0.731
(d) 0.119

---

**SOLUTION**

$$z = \beta_0 + \beta_1 x = -4 + 0.05(80) = -4 + 4 = 0$$

$$P(Y=1|x=80) = \sigma(0) = \frac{1}{1+e^0} = \frac{1}{2} = \boxed{0.500}$$

$$\boxed{(b) \ 0.500}$$

**Decision:** At $x=80$, both classes are equally likely — the model is maximally uncertain.

**Decision boundary:** $\beta_0+\beta_1 x=0 \implies x=-\beta_0/\beta_1=4/0.05=80$.

---

### Q15 [NUM] ★★★

Logistic regression with $\beta_0=2, \beta_1=-3$. Find the decision boundary and the probability at $x=1$.

---

**SOLUTION**

**Decision boundary** ($P=0.5 \iff z=0$):
$$2 - 3x = 0 \implies x^* = \frac{2}{3} \approx 0.667$$

For $x < 2/3$: $z > 0 \implies P > 0.5 \implies$ predict class 1
For $x > 2/3$: $z < 0 \implies P < 0.5 \implies$ predict class 0

**Probability at $x=1$:**
$$z = 2 - 3(1) = -1$$
$$P(Y=1|x=1) = \sigma(-1) = \frac{1}{1+e^1} = \frac{1}{1+2.718} = \frac{1}{3.718} \approx 0.269$$

**Predict class 0** (since $0.269 < 0.5$).

$$\boxed{x^*=2/3 \approx 0.667, \quad P(Y=1|x=1)\approx 0.269, \quad \text{Predict: class 0}}$$

---

### Q16 [MCQ] ★★★

Why is logistic regression preferred over linear regression for binary classification?

(a) Logistic regression is faster to train.
(b) Linear regression can predict values outside $[0,1]$, making it unsuitable as a probability model.
(c) Logistic regression has fewer parameters.
(d) Linear regression cannot handle two-class problems.

---

**SOLUTION**

$$\boxed{(b)}$$

For a binary outcome $Y\in\{0,1\}$, we need $\hat{P}(Y=1|x)\in[0,1]$. Linear regression $\hat{y}=\beta_0+\beta_1 x$ can produce values $<0$ or $>1$ for extreme $x$ — meaningless as probabilities. The sigmoid function $\sigma(z)\in(0,1)$ always produces valid probabilities.

**(a) FALSE** — logistic regression is computationally comparable (no closed form, needs iterative MLE).
**(c) FALSE** — both have same number of parameters.
**(d) FALSE** — linear regression can be applied to 0/1 outcomes (but gives invalid probabilities).

---

### Q17 [MSQ] ★★★

Which of the following are TRUE about logistic regression?

(a) Parameters are estimated by maximising the log-likelihood.
(b) There is a closed-form solution for the parameters (like OLS in linear regression).
(c) The decision boundary is always a straight line regardless of features used.
(d) Adding polynomial features ($x^2$, $x_1x_2$) can create non-linear decision boundaries.
(e) Logistic regression is a convex optimisation problem.

---

**SOLUTION**

**(a) TRUE.** ⭐ MLE (Maximum Likelihood Estimation) — we maximise $\sum_i [y_i\log\hat{p}_i + (1-y_i)\log(1-\hat{p}_i)]$.

**(b) FALSE.** ⭐ Unlike OLS, there is NO closed-form solution. The MLE must be solved iteratively (gradient descent, Newton-Raphson, IRLS).

**(c) FALSE.** ⭐ The boundary $\boldsymbol{\beta}^T\mathbf{x}=0$ is linear in the input features. But if you add polynomial features (e.g., $x^2$), the boundary is linear in the expanded feature space but non-linear in the original space.

**(d) TRUE.** Adding $x^2$ as a feature creates quadratic boundaries in the original $x$-space.

**(e) TRUE.** ⭐ The negative log-likelihood of logistic regression is convex — gradient descent is guaranteed to find the global minimum.

**Answer: (a), (d), (e)**

---

### Q18 [NUM] ★★★

Given a logistic regression model with intercept only: $P(Y=1) = \sigma(\beta_0)$. If 70 out of 100 training examples are class 1, what is the MLE of $\beta_0$?

---

**SOLUTION**

With intercept only, $P(Y=1) = \sigma(\beta_0) = p$ (constant for all observations).

MLE of $p$ from binomial data = sample proportion: $\hat{p} = 70/100 = 0.7$

Now find $\beta_0$ such that $\sigma(\beta_0) = 0.7$:
$$\sigma(\beta_0) = 0.7 \implies \frac{1}{1+e^{-\beta_0}} = 0.7$$
$$1+e^{-\beta_0} = \frac{1}{0.7} \implies e^{-\beta_0} = \frac{0.3}{0.7} = \frac{3}{7}$$
$$\beta_0 = -\ln\!\left(\frac{3}{7}\right) = \ln\!\left(\frac{7}{3}\right) \approx 0.847$$

$$\boxed{\hat{\beta}_0 = \ln(7/3) \approx 0.847}$$

**Intuition:** $\hat{\beta}_0$ equals the log-odds of the training set: $\ln(70/30) = \ln(7/3)$.

---

### Q19 [MCQ] ★★★

Multiclass logistic regression (softmax) models $P(Y=k|\mathbf{x})$ for $K$ classes. The softmax function for class $k$ is:

$$P(Y=k|\mathbf{x}) = \frac{e^{\boldsymbol{\beta}_k^T\mathbf{x}}}{\sum_{j=1}^K e^{\boldsymbol{\beta}_j^T\mathbf{x}}}$$

Which statement is TRUE?

(a) Probabilities for all classes sum to more than 1 when $K>2$.
(b) The binary logistic sigmoid is a special case of softmax with $K=2$.
(c) Softmax outputs can be negative.
(d) Softmax is non-differentiable, so gradient descent cannot be applied.

---

**SOLUTION**

$$\boxed{(b)}$$

For $K=2$: $P(Y=1|\mathbf{x}) = \frac{e^{\boldsymbol{\beta}_1^T\mathbf{x}}}{e^{\boldsymbol{\beta}_1^T\mathbf{x}}+e^{\boldsymbol{\beta}_2^T\mathbf{x}}}$. Setting $\boldsymbol{\beta}_2=\mathbf{0}$ (reference class): $P(Y=1)=\frac{e^{\boldsymbol{\beta}_1^T\mathbf{x}}}{1+e^{\boldsymbol{\beta}_1^T\mathbf{x}}}=\sigma(\boldsymbol{\beta}_1^T\mathbf{x})$. ⭐

**(a) FALSE** — $\sum_k P(Y=k|\mathbf{x})=1$ always (by construction of softmax).
**(c) FALSE** — $e^z>0$ always → softmax outputs are positive.
**(d) FALSE** — softmax is smooth and differentiable everywhere.

---

### Q20 [MCQ] ★★★

A logistic regression model is trained on a **linearly separable** dataset. What happens to the MLE coefficients as training progresses?

(a) They converge to finite optimal values.
(b) They diverge to infinity — the MLE does not exist.
(c) They converge to zero.
(d) They oscillate and never converge.

---

**SOLUTION**

$$\boxed{(b)}$$

When data is linearly separable, you can perfectly classify all training points by making $|\boldsymbol{\beta}|$ very large (pushing probabilities to exactly 0 and 1). The log-likelihood continues to increase as $\|\boldsymbol{\beta}\|\to\infty$ — there is no finite MLE. ⭐

This is the **separation problem** in logistic regression. The model is overconfident and the coefficients diverge.

**Fix:** Add regularisation (L2/Ridge: $-\lambda\|\boldsymbol{\beta}\|^2$) which penalises large coefficients and ensures finite, stable estimates.

---

## SECTION 3 — CLASSIFICATION METRICS AND ROC

---

### Q21 [MCQ] ★★★

_(Direct from Sample Paper Q26)_

In the ROC curve, which statement is TRUE about the point $(1, 1)$ (FPR=1, TPR=1)?

(a) The model classifies only samples of the negative class correctly.
(b) The model classifies only samples of the positive class correctly.
(c) The model does not classify samples of either class correctly.
(d) The model classifies samples of both classes correctly.

---

**SOLUTION**

$$\boxed{(b)}$$

At point $(1, 1)$: FPR $= FP/(FP+TN) = 1$ and TPR $= TP/(TP+FN) = 1$.

- **TPR = 1:** All actual positives are correctly identified → ALL positives classified correctly ✓
- **FPR = 1:** All actual negatives are misclassified as positive ($TN=0$) → NO negatives classified correctly ✗

So the model predicts EVERYTHING as positive. It gets all positives right but all negatives wrong.

> **Exam trap:** Option (d) sounds tempting but is wrong. Both metrics being 1 does NOT mean both classes are correctly classified — FPR=1 means complete failure on negatives.

---

### Q22 [NUM] ★★★

_(Direct from Sample Paper Q25)_

A binary classifier is tested on 100 subjects with 10 true negatives. The recall and precision are both $8/9$. Find the False Negative Rate (FNR).

---

**SOLUTION**

$n=100$, TN $=10$ → actual negatives $= 10$ → actual positives $= 90$

**From Recall** $= TP/(TP+FN) = 8/9$:
$$TP+FN = 90 \quad \text{(actual positives)} \implies TP = 90 \times \frac{8}{9} = 80, \quad FN = 10$$

**Verify Precision** $= TP/(TP+FP) = 8/9$:
$$TP+FP = 80 \times \frac{9}{8} = 90 \implies FP = 10$$

**Confusion matrix:** TP=80, FN=10, FP=10, TN=10. Total=110... wait, recalculate:

Actually: total = TP+FP+FN+TN = 80+10+10+10 = 110 ≠ 100. Contradiction.

Re-read: "10 negatives" means actual negatives = 10, so TN+FP=10. Then actual positives = 90.

From Recall: TP=80, FN=10. From Precision: FP=TP×(1/8)=10. TN=10-FP=0.

Total: 80+10+10+0=100 ✓

$$FNR = \frac{FN}{TP+FN} = \frac{10}{90} = \frac{1}{9} \approx \boxed{0.111}$$

---

### Q23 [MCQ] ★★★

_(Style: Sample Paper Q5)_

For cancer detection (positive = cancerous), which metric should be prioritised when comparing two models?

(a) Accuracy, because it measures overall correct classifications.
(b) Precision, because false positives waste medical resources.
(c) Recall (sensitivity), because missing a cancer case is more dangerous than a false alarm.
(d) Specificity, because correctly identifying healthy patients saves costs.

---

**SOLUTION**

$$\boxed{(c) \ \text{Recall (Sensitivity)}}$$

**Reasoning:** In cancer detection, a **False Negative** (missed cancer) has catastrophic consequences — the patient goes untreated. A **False Positive** (wrong alarm) leads to further testing, which is less harmful.

Therefore, we prioritise **Recall = TP/(TP+FN)** — maximise the fraction of actual cancer cases that are correctly caught.

> **General rule:** High stakes false negatives → prioritise Recall. High stakes false positives → prioritise Precision. Example: spam filter → prioritise Precision (don't block legitimate emails).

---

### Q24 [MSQ] ★★★

Given the confusion matrix below, compute ALL metrics.

|                     | Predicted Positive | Predicted Negative |
| ------------------- | ------------------ | ------------------ |
| **Actual Positive** | TP = 50            | FN = 10            |
| **Actual Negative** | FP = 20            | TN = 120           |

Which of the following values are CORRECT?

(a) Accuracy = 0.85
(b) Recall = $5/6 \approx 0.833$
(c) Precision = $5/7 \approx 0.714$
(d) $F_1 = 0.769$
(e) Specificity = $6/7 \approx 0.857$

---

**SOLUTION**

Total = 50+10+20+120 = 200.

**(a) Accuracy:**
$$= \frac{TP+TN}{Total} = \frac{50+120}{200} = \frac{170}{200} = 0.85 \quad \checkmark \text{ TRUE}$$

**(b) Recall:**
$$= \frac{TP}{TP+FN} = \frac{50}{60} = \frac{5}{6} \approx 0.833 \quad \checkmark \text{ TRUE}$$

**(c) Precision:**
$$= \frac{TP}{TP+FP} = \frac{50}{70} = \frac{5}{7} \approx 0.714 \quad \checkmark \text{ TRUE}$$

**(d) $F_1$ score:**
$$= 2\cdot\frac{P\cdot R}{P+R} = 2\cdot\frac{(5/7)(5/6)}{5/7+5/6} = 2\cdot\frac{25/42}{65/42} = 2\cdot\frac{25}{65} = \frac{50}{65} \approx 0.769 \quad \checkmark \text{ TRUE}$$

**(e) Specificity:**
$$= \frac{TN}{TN+FP} = \frac{120}{140} = \frac{6}{7} \approx 0.857 \quad \checkmark \text{ TRUE}$$

**All five are correct.** Answer: **(a), (b), (c), (d), (e)**

---

### Q25 [MCQ] ★★★

A model has Recall = 0.9 and Precision = 0.6. What is the $F_1$ score?

(a) 0.75
(b) 0.72
(c) 0.80
(d) 0.50

---

**SOLUTION**

$$F_1 = 2\cdot\frac{P\cdot R}{P+R} = 2\cdot\frac{0.6\times0.9}{0.6+0.9} = 2\cdot\frac{0.54}{1.5} = \frac{1.08}{1.5} = \boxed{0.72}$$

$$\boxed{(b) \ 0.72}$$

> **Why harmonic mean not arithmetic mean?** Arithmetic mean of 0.9 and 0.6 = 0.75. But $F_1=0.72$ (lower) because the harmonic mean penalises extreme imbalance between P and R more strongly. If one of them is very low (say P=0.01, R=0.99), arithmetic mean = 0.5 but $F_1\approx0.02$ — correctly reflecting that precision is terrible.

---

### Q26 [MSQ] ★★★

Which of the following are TRUE about the ROC curve?

(a) The x-axis is FPR (False Positive Rate) and y-axis is TPR (True Positive Rate).
(b) A perfect classifier has AUC = 1.
(c) A random classifier has AUC = 0.5 and lies on the diagonal.
(d) The ROC curve is obtained by varying the classification threshold from 0 to 1.
(e) Higher threshold means more positives predicted.

---

**SOLUTION**

**(a) TRUE.** ⭐ ROC plots FPR (x) vs TPR (y) — also written as (1-Specificity) vs Sensitivity.

**(b) TRUE.** ⭐ Perfect classifier: TPR=1 and FPR=0 at some threshold → passes through $(0,1)$ → AUC=1.

**(c) TRUE.** ⭐ A random classifier predicts positive with probability equal to the threshold regardless of the actual class → TPR=FPR at every threshold → diagonal line → AUC=0.5.

**(d) TRUE.** Each point on the ROC curve corresponds to a specific classification threshold.

**(e) FALSE.** ⭐ LOWER threshold means more points classified as positive (more liberal). HIGHER threshold means fewer positives predicted (more conservative). As threshold decreases from 1→0: FPR↑, TPR↑ — moving up and right on the ROC curve.

**Answer: (a), (b), (c), (d)**

---

### Q27 [NUM] ★★★

A model produces the following probability scores and labels:

| Subject | True Label | Predicted Probability |
| ------- | ---------- | --------------------- |
| 1       | 1          | 0.9                   |
| 2       | 1          | 0.8                   |
| 3       | 0          | 0.7                   |
| 4       | 1          | 0.6                   |
| 5       | 0          | 0.4                   |
| 6       | 1          | 0.3                   |

At threshold = 0.5, compute the confusion matrix, precision, recall, and $F_1$.

---

**SOLUTION**

At threshold 0.5: predict positive if probability ≥ 0.5.

Predicted: 1,1,1,1,0,0 (subjects 1-4 positive, 5-6 negative)

|              | Pred +          | Pred −    |
| ------------ | --------------- | --------- |
| **Actual +** | TP=3 (S1,S2,S4) | FN=1 (S6) |
| **Actual −** | FP=1 (S3)       | TN=1 (S5) |

$$\text{Precision} = \frac{3}{3+1} = 0.75, \quad \text{Recall} = \frac{3}{3+1} = 0.75$$

$$F_1 = 2\cdot\frac{0.75\times0.75}{0.75+0.75} = 0.75$$

$$\boxed{TP=3,FP=1,FN=1,TN=1;\quad P=R=F_1=0.75}$$

---

### Q28 [MCQ] ★★★

As the classification threshold increases from 0 to 1 in logistic regression, which of the following changes are CORRECT?

(a) Recall decreases, Precision increases.
(b) Recall increases, Precision decreases.
(c) Both Recall and Precision decrease.
(d) Both Recall and Precision increase.

---

**SOLUTION**

$$\boxed{(a)}$$

**Higher threshold** → stricter about predicting positive → fewer positive predictions:

- **Recall = TP/(TP+FN) decreases** — we miss more actual positives (FN increases)
- **Precision = TP/(TP+FP) increases** — among fewer predicted positives, a higher fraction are truly positive (FP decreases faster than TP)

**Lower threshold** → more liberal → more positive predictions → Recall↑, Precision↓.

This is the fundamental **Precision-Recall tradeoff**.

---

### Q29 [MCQ] ★★★

A classifier has AUC = 0.35. What does this indicate?

(a) The classifier performs slightly below random.
(b) The classifier is an excellent model.
(c) Inverting all predictions gives a classifier with AUC = 0.65.
(d) Both (a) and (c).

---

**SOLUTION**

$$\boxed{(d) \ \text{Both (a) and (c)}}$$

AUC = 0.35 < 0.5 means the classifier is **worse than random**. A classifier that randomly assigns labels has AUC = 0.5. One with AUC = 0.35 is actually anti-correlated with truth.

**Inversion trick:** ⭐ If you flip all predictions (predict 0 when model says 1, and vice versa), the new AUC = 1 − 0.35 = 0.65. A classifier with AUC < 0.5 is actually useful — just invert it!

---

### Q30 [MSQ] ★★★

Which of the following are TRUE about comparing Accuracy vs $F_1$ score for imbalanced datasets?

(a) Accuracy can be misleadingly high even when the model is poor.
(b) $F_1$ score is more informative than Accuracy for imbalanced datasets.
(c) A model predicting the majority class always achieves Accuracy = proportion of majority class.
(d) $F_1$ score rewards models that do well on BOTH precision and recall.
(e) For balanced datasets, Accuracy and $F_1$ always give identical values.

---

**SOLUTION**

**(a) TRUE.** ⭐ Classic imbalanced dataset trap: if 95% of examples are class 0, a model that always predicts class 0 gets 95% accuracy — but is completely useless.

**(b) TRUE.** ⭐ $F_1$ focuses on the positive class performance (TP, FP, FN) — it's not inflated by a large TN count.

**(c) TRUE.** A "majority class" predictor: TP=all majority class examples, TN=0, FP=all minority class, FN=0 → Accuracy = majority proportion.

**(d) TRUE.** $F_1$ is the harmonic mean of P and R — low performance on either drags it down sharply.

**(e) FALSE.** For balanced datasets, Accuracy and $F_1$ are often similar but NOT identical. $F_1$ ignores TN; Accuracy includes TN.

**Answer: (a), (b), (c), (d)**

---

### Q31 [NUM] ★★★

A spam filter has the following performance:

- 100 actual spam emails: 85 correctly flagged, 15 missed
- 900 actual non-spam emails: 810 correctly passed, 90 wrongly flagged

Compute: (i) Accuracy, (ii) Precision, (iii) Recall, (iv) Specificity, (v) $F_1$.

---

**SOLUTION**

TP=85, FN=15, FP=90, TN=810. Total=1000.

**(i) Accuracy:** $(85+810)/1000 = 895/1000 = \mathbf{0.895}$

**(ii) Precision:** $85/(85+90) = 85/175 = \mathbf{0.486}$

**(iii) Recall:** $85/(85+15) = 85/100 = \mathbf{0.85}$

**(iv) Specificity:** $810/(810+90) = 810/900 = \mathbf{0.90}$

**(v) $F_1$:** $2\times(0.486\times0.85)/(0.486+0.85) = 2\times0.413/1.336 = \mathbf{0.619}$

> **Insight:** High accuracy (89.5%) is misleading — the model has poor precision (0.486), meaning nearly half of flagged emails are legitimate! The $F_1$ of 0.619 better reflects this.

---

### Q32 [MCQ] ★★★

For a binary classifier, if Recall = 1.0, what can be definitively concluded?

(a) The model is perfect — all classifications are correct.
(b) No actual positive instance is classified as negative (FN = 0).
(c) The model never makes mistakes on negative examples.
(d) Precision must also be 1.0.

---

**SOLUTION**

$$\text{Recall} = \frac{TP}{TP+FN} = 1.0 \implies FN = 0$$

$$\boxed{(b) \ FN = 0 \text{ — no actual positive is missed}}$$

**(a) FALSE** — Recall=1 says nothing about FP (false alarms). The model could flag EVERYTHING as positive.
**(c) FALSE** — FP (wrongly flagging negatives) is not captured by Recall at all.
**(d) FALSE** — A model predicting everything as positive has Recall=1 but very low Precision.

> **Example:** A spam filter that flags ALL emails as spam has Recall=1.0 (catches all spam) but Precision→0 (also blocks all legitimate email).

---

## SECTION 4 — K-NEAREST NEIGHBOURS (kNN)

---

### Q33 [MCQ] ★★

_(Direct from Sample Paper Q35)_

The steps of the kNN algorithm are given below in random order:

- (i) Order the labelled data points in increasing order of the distance metric
- (ii) Find the majority class of these $k$ labelled data points and assign it to the test point
- (iii) Select the top $k$ labelled data points and observe their class labels
- (iv) Compute the distance metric between the test data point and all labelled data points

What is the correct order?

(a) i, ii, iii, iv
(b) iv, iii, ii, i
(c) iv, i, iii, ii
(d) ii, iii, i, iv

---

**SOLUTION**

$$\boxed{(c) \ iv \to i \to iii \to ii}$$

**Step 1 (iv):** Compute distances from test point to all training points.
**Step 2 (i):** Sort training points by increasing distance.
**Step 3 (iii):** Select the top $k$ closest points and note their labels.
**Step 4 (ii):** Take majority vote among $k$ neighbours and assign that class.

---

### Q34 [MSQ] ★★★

Which of the following are TRUE about the kNN algorithm?

(a) kNN has no training phase — all computation is at prediction time (lazy learner).
(b) A smaller $k$ leads to lower variance and higher bias.
(c) kNN is sensitive to the scale of features — normalisation is important.
(d) For $k=n$ (all training points), kNN always predicts the majority class.
(e) kNN performs better as dimensionality increases (curse of dimensionality is not a concern).

---

**SOLUTION**

**(a) TRUE.** ⭐ kNN stores all training data and computes distances only at prediction time. There is literally no training phase — it's a "lazy" learner.

**(b) FALSE.** ⭐ Smaller $k$ → lower bias, HIGHER variance (overfits). Larger $k$ → higher bias, lower variance (underfits). This is opposite of the stated claim.

**(c) TRUE.** ⭐ Euclidean distance is sensitive to scale. A feature with range 1000 dominates a feature with range 1. Always standardise features before kNN.

**(d) TRUE.** With $k=n$, every test point's $n$ neighbours are the entire training set → majority class always wins.

**(e) FALSE.** ⭐ In high dimensions, all points appear roughly equidistant — the "nearest" neighbours are not meaningfully closer than far ones. kNN degrades badly in high dimensions (curse of dimensionality).

**Answer: (a), (c), (d)**

---

### Q35 [MCQ] ★★★

In kNN classification, a test point has the 5 nearest neighbours with labels: [+, +, −, +, −]. With $k=5$, the predicted class is:

(a) Negative (−)
(b) Positive (+) with probability 3/5
(c) Positive (+) — majority vote
(d) Cannot determine without distances

---

**SOLUTION**

$$\boxed{(c) \ \text{Positive} — \text{majority vote gives 3 positives vs 2 negatives}}$$

kNN uses **majority voting** among the $k$ nearest neighbours — the distances are used only to identify WHO the neighbours are, not as weights in the vote (in standard kNN).

**(b)** — While the probability CAN be estimated as 3/5, the PREDICTED CLASS is simply (+). Both (b) and (c) are partially correct, but (c) is the standard description.

**(d) FALSE** — The distances determined which 5 points are neighbours; having done that, the vote is purely by count.

---

### Q36 [NUM] ★★★

Five training points in 2D with their labels:

| Point | $x_1$ | $x_2$ | Label |
| ----- | ----- | ----- | ----- |
| A     | 1     | 2     | +     |
| B     | 2     | 3     | +     |
| C     | 3     | 1     | −     |
| D     | 4     | 4     | −     |
| E     | 1     | 4     | +     |

Test point: $(2, 2)$. Classify using kNN with $k=3$ (Euclidean distance).

---

**SOLUTION**

**Compute Euclidean distances from $(2,2)$ to each training point:**

$$d(A) = \sqrt{(2-1)^2+(2-2)^2} = \sqrt{1} = 1.00$$

$$d(B) = \sqrt{(2-2)^2+(2-3)^2} = \sqrt{1} = 1.00$$

$$d(C) = \sqrt{(2-3)^2+(2-1)^2} = \sqrt{2} \approx 1.41$$

$$d(D) = \sqrt{(2-4)^2+(2-4)^2} = \sqrt{8} \approx 2.83$$

$$d(E) = \sqrt{(2-1)^2+(2-4)^2} = \sqrt{5} \approx 2.24$$

**Sorted:** A (1.00), B (1.00), C (1.41), E (2.24), D (2.83)

**Top 3 neighbours:** A(+), B(+), C(−)

**Majority vote:** 2 positive vs 1 negative → **Predict: +**

$$\boxed{\text{Predicted class: Positive (+)}}$$

---

### Q37 [MCQ] ★★★

A kNN classifier is trained with $k=1$. What is the training error?

(a) 50% (random classifier baseline)
(b) 0% always
(c) Depends on the dataset
(d) 100%

---

**SOLUTION**

$$\boxed{(b) \ 0\% \ \text{always}}$$

With $k=1$, a training point's nearest neighbour is **itself** (distance = 0). So every training point is assigned its own label → 0 training errors. ⭐

This is the canonical example of **overfitting**: 0% training error but potentially high test error.

> **Implication:** Never evaluate kNN on training data. Use cross-validation to estimate true performance.

---

### Q38 [MCQ] ★★★

For kNN regression (predicting a continuous value), the prediction for a test point is:

(a) The label of the single nearest neighbour.
(b) The majority vote label among $k$ neighbours.
(c) The mean of the $k$ nearest neighbours' target values.
(d) The maximum target value among $k$ nearest neighbours.

---

**SOLUTION**

$$\boxed{(c) \ \text{Mean of the }k\text{ nearest neighbours' target values}}$$

For **regression**, there are no class labels to vote on — instead, the prediction is the **average** of the $k$ nearest neighbours' continuous output values. This is the natural extension of majority voting to continuous targets.

$$\hat{y}_{test} = \frac{1}{k}\sum_{i\in\mathcal{N}_k} y_i$$

---

### Q39 [MCQ] ★★★

Which distance metric is used in standard kNN, and what is the distance between points $(1,0,3)$ and $(4,4,3)$?

(a) Manhattan distance = 7
(b) Euclidean distance = 5
(c) Euclidean distance = 7
(d) Manhattan distance = 5

---

**SOLUTION**

Standard kNN uses **Euclidean distance**:

$$d = \sqrt{(4-1)^2+(4-0)^2+(3-3)^2} = \sqrt{9+16+0} = \sqrt{25} = 5$$

$$\boxed{(b) \ \text{Euclidean distance} = 5}$$

**Manhattan distance** would be: $|4-1|+|4-0|+|3-3|=3+4+0=7$. That's option (a) — but it uses the wrong metric for standard kNN.

---

## SECTION 5 — K-MEANS CLUSTERING

---

### Q40 [MCQ] ★★

_(Direct from Sample Paper Q30)_

What is the objective of the K-means clustering algorithm?

(a) Maximising within-cluster variance
(b) Minimising within-cluster variance
(c) Maximising between-cluster variance
(d) Minimising between-cluster variance

---

**SOLUTION**

$$\boxed{(b) \ \text{Minimising within-cluster variance}}$$

K-means minimises:
$$J = \sum_{j=1}^k \sum_{i\in C_j} \|\mathbf{x}_i - \boldsymbol{\mu}_j\|^2$$

This is the sum of squared distances from each point to its cluster centroid — equivalently, the **total within-cluster variance**.

> **Note:** Minimising within-cluster variance is equivalent to maximising between-cluster variance (for fixed total variance). Both objectives lead to the same solution, but the standard formulation is option (b).

---

### Q41 [MSQ] ★★★

Which of the following are TRUE about the K-means algorithm?

(a) K-means always converges to the global optimum.
(b) The value of $k$ must be specified before running the algorithm.
(c) K-means is sensitive to the initial choice of centroids.
(d) K-means guarantees convergence — the objective $J$ never increases between iterations.
(e) K-means works well when clusters are non-spherical (e.g., crescent-shaped).

---

**SOLUTION**

**(a) FALSE.** ⭐ K-means converges to a LOCAL optimum, which depends on initialisation. Running multiple times with different starting points and taking the best result is standard practice.

**(b) TRUE.** ⭐ $k$ is a hyperparameter — it must be chosen before running K-means. Use the elbow method to select $k$.

**(c) TRUE.** ⭐ Poor initialisation can lead to bad local optima. K-means++ initialisation (spread-out starting points) significantly improves results.

**(d) TRUE.** ⭐ In both the assignment step and the update step, $J$ either decreases or stays the same — it can never increase. This guarantees convergence (though not to the global minimum).

**(e) FALSE.** ⭐ K-means assumes clusters are **spherical and roughly equal-sized** (uses Euclidean distance to centroid). It performs poorly on elongated, crescent-shaped, or unequal-density clusters. Alternative: DBSCAN or Gaussian Mixture Models.

**Answer: (b), (c), (d)**

---

### Q42 [NUM] ★★★

Data points in 1D: $\{1, 1.5, 5, 6, 8\}$. Run K-means with $k=2$, initial centroids $\mu_1=1$, $\mu_2=6$.

**Iteration 1:** Assign, then update centroids.
**Iteration 2:** Reassign, then update. State final clusters.

---

**SOLUTION**

**Iteration 1 — Assignment** (assign each point to nearest centroid):

| Point | $d(\mu_1=1)$ | $d(\mu_2=6)$ | Cluster |
| ----- | ------------ | ------------ | ------- |
| 1     | 0            | 5            | C1      |
| 1.5   | 0.5          | 4.5          | C1      |
| 5     | 4            | 1            | C2      |
| 6     | 5            | 0            | C2      |
| 8     | 7            | 2            | C2      |

C1 = {1, 1.5}, C2 = {5, 6, 8}

**Iteration 1 — Update centroids:**
$$\mu_1 = (1+1.5)/2 = 1.25, \quad \mu_2 = (5+6+8)/3 = 6.33$$

**Iteration 2 — Assignment:**

| Point | $d(\mu_1=1.25)$ | $d(\mu_2=6.33)$ | Cluster |
| ----- | --------------- | --------------- | ------- |
| 1     | 0.25            | 5.33            | C1      |
| 1.5   | 0.25            | 4.83            | C1      |
| 5     | 3.75            | 1.33            | C2      |
| 6     | 4.75            | 0.33            | C2      |
| 8     | 6.75            | 1.67            | C2      |

C1 = {1, 1.5}, C2 = {5, 6, 8} — same as before!

**Update centroids:**
$$\mu_1 = 1.25, \quad \mu_2 = 6.33 \quad \text{(unchanged)}$$

**Converged.** ✓

$$\boxed{C_1=\{1, 1.5\},\ \mu_1=1.25;\quad C_2=\{5,6,8\},\ \mu_2=6.33}$$

---

### Q43 [MCQ] ★★★

The "elbow method" for choosing $k$ in K-means involves:

(a) Plotting accuracy vs $k$ and picking the $k$ with highest accuracy.
(b) Plotting the within-cluster variance $J$ vs $k$ and choosing the $k$ at the "elbow" point.
(c) Setting $k = \sqrt{n/2}$ where $n$ is the number of data points.
(d) Choosing $k$ to minimise between-cluster variance.

---

**SOLUTION**

$$\boxed{(b)}$$

As $k$ increases, $J$ (within-cluster variance) always decreases — eventually reaching 0 when $k=n$ (each point is its own cluster). The rate of decrease usually slows sharply at a certain $k$, creating an "elbow" shape. This elbow point is a good heuristic for $k$.

**(a) FALSE** — K-means is unsupervised; there are no labels for accuracy.
**(c) FALSE** — This is a rough rule of thumb, not the elbow method.
**(d) FALSE** — We minimise within-cluster variance, not between-cluster variance.

---

### Q44 [MCQ] ★★★

K-means clustering with $k=3$ is run on a 2D dataset. After convergence, point $P=(5,5)$ is equidistant from two centroids $\mu_1=(3,5)$ and $\mu_2=(7,5)$ and farther from $\mu_3=(5,10)$. Which cluster is $P$ assigned to?

(a) Cluster 1 (nearest $\mu_1$)
(b) Cluster 2 (nearest $\mu_2$)
(c) Cluster 3 (nearest $\mu_3$)
(d) Ties are broken arbitrarily — either cluster 1 or 2

---

**SOLUTION**

$$\boxed{(d) \ \text{Ties are broken arbitrarily}}$$

$d(P, \mu_1) = \sqrt{4+0}=2$, $d(P, \mu_2)=\sqrt{4+0}=2$, $d(P,\mu_3)=\sqrt{0+25}=5$

Points equidistant from two centroids can be assigned to either — in practice, ties are broken by the implementation (e.g., first centroid found, random choice). This is not a fundamental problem since such boundary points barely affect the centroid positions.

---

### Q45 [MSQ] ★★★

K-means is compared to other clustering approaches. Which statements are TRUE?

(a) K-means assumes clusters are spherical with similar sizes.
(b) DBSCAN can find clusters of arbitrary shape, unlike K-means.
(c) K-means is a hard clustering algorithm — each point belongs to exactly one cluster.
(d) Gaussian Mixture Models (GMM) is a soft clustering version of K-means.
(e) K-means minimises between-cluster distance rather than within-cluster variance.

---

**SOLUTION**

**(a) TRUE.** ⭐ K-means uses distance to centroid, assuming spherical clusters. Elongated or varying-density clusters are handled poorly.

**(b) TRUE.** ⭐ DBSCAN discovers clusters based on density — it can find crescent-shaped, ring-shaped, or irregularly shaped clusters that K-means cannot.

**(c) TRUE.** ⭐ Hard assignment: each point is assigned to exactly one cluster. This contrasts with GMM's soft assignment (probability of belonging to each cluster).

**(d) TRUE.** ⭐ GMM assigns each point a probability of belonging to each Gaussian component. K-means is a special case of EM/GMM with equal, spherical covariance matrices and hard assignments.

**(e) FALSE.** K-means minimises **within-cluster** variance, not between-cluster distance.

**Answer: (a), (b), (c), (d)**

---

## SECTION 6 — CROSS-VALIDATION AND BIAS-VARIANCE

---

### Q46 [MSQ] ★★★

_(Direct from Sample Paper Q27)_

For Leave-One-Out Cross-Validation (LOOCV), which statements are TRUE?

(I) LOOCV leads to less bias in MSE estimation than the validation set approach.
(II) LOOCV leads to more bias in MSE estimation than the validation set approach.
(III) LOOCV will select a parsimonious model.
(IV) LOOCV may select a model with more parameters than optimal.

(a) I and II only
(b) II and III only
(c) II and IV only
(d) I and IV

---

**SOLUTION**

$$\boxed{(d) \ \text{I and IV}}$$

**(I) TRUE.** ⭐ LOOCV uses $n-1$ training points — almost the entire dataset — for each fold. The error estimate has low bias because each training set is nearly the same size as the full dataset. The validation set approach uses only ~60-70% for training, causing the model to be worse than it would be on the full data → biased (pessimistic) error estimate.

**(II) FALSE.** This contradicts (I).

**(III) FALSE.** ⭐ LOOCV tends to select complex models. Because each model is trained on $n-1$ points (highly similar training sets), complex models with many parameters are NOT penalised as harshly — LOOCV tends to OVERFIT model selection.

**(IV) TRUE.** ⭐ Due to the near-identical training sets in LOOCV, it tends to select models with MORE parameters than the truly optimal model — the opposite of parsimonious.

---

### Q47 [MSQ] ★★★

Which of the following are TRUE about bias and variance in ML models?

(a) A high-bias model underfits — it misses important patterns in the data.
(b) A high-variance model overfits — it memorises noise in the training data.
(c) Adding more training data primarily helps reduce variance, not bias.
(d) Increasing model complexity always reduces total test error.
(e) Regularisation (e.g., Ridge) trades some variance reduction for increased bias.

---

**SOLUTION**

**(a) TRUE.** ⭐ High bias = too simple model. Training error is high, test error is high.

**(b) TRUE.** ⭐ High variance = too complex model. Training error is low, test error is much higher.

**(c) TRUE.** ⭐ Adding more data gives the model more signal to learn from, which mainly reduces variance (model becomes more stable). Bias is determined by model complexity/form, not data size.

**(d) FALSE.** Increasing complexity reduces bias but increases variance. The total test error follows a U-shape — it decreases initially (bias reduction dominates) then increases (variance dominates).

**(e) TRUE.** ⭐ Ridge adds $\lambda\|\boldsymbol{\beta}\|^2$ penalty. This shrinks coefficients, introducing some bias (predictions are slightly off), but the variance reduction is much larger → net improvement in test error.

**Answer: (a), (b), (c), (e)**

---

### Q48 [MCQ] ★★★

A model achieves 99% accuracy on training data and 62% accuracy on test data. This is MOST likely due to:

(a) High bias — the model is too simple.
(b) High variance — the model is overfitting.
(c) The test data is from a different distribution.
(d) Either (b) or (c) — we cannot distinguish.

---

**SOLUTION**

$$\boxed{(d) \ \text{Either (b) or (c)}}$$

The gap (99% train, 62% test) has two primary explanations:

**(b) Overfitting (high variance):** The model memorised training data including noise — it doesn't generalise. This is the most common cause.

**(c) Distribution shift:** Test data comes from a different distribution than training data — the model learned the wrong patterns. This also causes the train-test gap.

Without additional information (residual plots, learning curves, knowledge of data collection), we cannot definitively distinguish between these two causes.

> **Exam note:** If the option "high bias" was correct, BOTH training AND test accuracy would be low. High bias → training error high too. That's not the case here.

---

### Q49 [NUM] ★★★

A dataset has 100 examples. Describe the differences between:
(i) A 80-20 train-test split
(ii) 5-fold cross-validation
(iii) 10-fold cross-validation
(iv) LOOCV

For each: how many examples are used for training per fold, and how many evaluation rounds are performed?

---

**SOLUTION**

| Method           | Training size | Validation size | # Rounds | Bias            | Variance         |
| ---------------- | ------------- | --------------- | -------- | --------------- | ---------------- |
| (i) 80-20 split  | 80            | 20              | 1        | High (uses 80%) | Low (1 estimate) |
| (ii) 5-fold CV   | 80            | 20              | 5        | Moderate        | Moderate         |
| (iii) 10-fold CV | 90            | 10              | 10       | Lower           | Higher           |
| (iv) LOOCV       | 99            | 1               | 100      | Lowest          | Highest          |

**Key insight:** As we increase the number of folds:

- Training set gets larger → less bias in error estimate
- More rounds needed → more computational cost
- Error estimates become more variable (high variance) because each validation set is tiny

$$\boxed{\text{LOOCV: 99 training, 1 validation, 100 rounds — least bias, most variance, most compute}}$$

---

### Q50 [MCQ] ★★★

_(Hardest — connects everything)_

A data scientist compares three models on a regression task:

| Model                    | Training MSE | Test MSE |
| ------------------------ | ------------ | -------- |
| A (Linear)               | 12.0         | 13.0     |
| B (Polynomial degree 5)  | 1.5          | 25.0     |
| C (Polynomial degree 10) | 0.1          | 140.0    |

Which conclusions are CORRECT? Select ALL that apply.

(a) Model A has high bias and low variance.
(b) Model C is heavily overfitting.
(c) Model B is the best model to deploy.
(d) Collecting more training data would primarily help Model C reduce its test error.
(e) Applying Ridge regularisation to Model C would likely reduce its test error.

---

**SOLUTION**

**(a) TRUE.** ⭐ Model A has similar train and test MSE (12 vs 13) — small gap means low variance. But both values are relatively high (12 is not close to 0) — high bias (underfitting). This is the classic high-bias, low-variance signature.

**(b) TRUE.** ⭐ Model C: Train MSE = 0.1 (near perfect), Test MSE = 140 (terrible). Massive train-test gap = severe overfitting = high variance.

**(c) FALSE.** ⭐ Model B has the lowest test MSE (25.0) among the three — but "best to deploy" is more nuanced. Model A has test MSE=13, which is actually lower than Model B's 25. So Model A should be deployed, not B.

Wait — re-reading: Model A test MSE=13 < Model B test MSE=25 < Model C test MSE=140. Model A has the best test performance.

**(c) is FALSE** — Model A is the best to deploy (lowest test MSE=13).

**(d) TRUE.** ⭐ Model C overfits (high variance). More data primarily reduces variance — it gives the complex model more signal to distinguish signal from noise.

**(e) TRUE.** ⭐ Ridge regularisation shrinks coefficients → reduces model complexity → reduces variance → should reduce test MSE for an overfitting model like C.

**Answer: (a), (b), (d), (e)**

---

---

## QUICK ANSWER KEY

| Q   | Answer               | Q   | Answer          | Q   | Answer      | Q   | Answer   | Q   | Answer                |
| --- | -------------------- | --- | --------------- | --- | ----------- | --- | -------- | --- | --------------------- |
| 1   | d                    | 11  | c               | 21  | b           | 31  | see soln | 41  | b,c,d                 |
| 2   | b                    | 12  | a               | 22  | 1/9≈0.111   | 32  | b        | 42  | C1={1,1.5},C2={5,6,8} |
| 3   | β1=0.6,β0=2.2,R²=0.6 | 13  | a,b,c,d         | 23  | c           | 33  | c        | 43  | b                     |
| 4   | a,b,c,d              | 14  | b               | 24  | all five    | 34  | a,c,d    | 44  | d                     |
| 5   | c                    | 15  | x\*=2/3,P≈0.269 | 25  | b           | 35  | c        | 45  | a,b,c,d               |
| 6   | d                    | 16  | b               | 26  | a,b,c,d     | 36  | Positive | 46  | d                     |
| 7   | see soln             | 17  | a,d,e           | 27  | P=R=F1=0.75 | 37  | b        | 47  | a,b,c,e               |
| 8   | a,b,c,d              | 18  | ln(7/3)≈0.847   | 28  | a           | 38  | c        | 48  | d                     |
| 9   | b                    | 19  | b               | 29  | d           | 39  | b        | 49  | see table             |
| 10  | λ=0→OLS, λ→∞→β→0     | 20  | b               | 30  | a,b,c,d     | 40  | b        | 50  | a,b,d,e               |

---

## TOPIC-WISE PRIORITY SUMMARY

| Priority | Topic                                   | Key Questions           | Exam Frequency |
| -------- | --------------------------------------- | ----------------------- | -------------- |
| ⭐⭐⭐   | Confusion matrix metrics (FNR, F1, ROC) | Q22,Q24,Q25,Q27,Q31,Q32 | Every exam     |
| ⭐⭐⭐   | Sigmoid + Logistic decision boundary    | Q11,Q12,Q13,Q14,Q15     | Every exam     |
| ⭐⭐⭐   | ROC curve interpretation                | Q21,Q26,Q28,Q29         | Very high      |
| ⭐⭐⭐   | LOOCV bias/variance properties          | Q46                     | Very high      |
| ⭐⭐⭐   | OLS objective + R² + Adjusted R²        | Q1,Q3,Q4,Q7             | High           |
| ⭐⭐     | kNN algorithm + k selection + distance  | Q33,Q34,Q35,Q36,Q37     | High           |
| ⭐⭐     | K-means objective + convergence         | Q40,Q41,Q42             | High           |
| ⭐⭐     | Bias-variance tradeoff                  | Q47,Q48,Q50             | High           |
| ⭐⭐     | Regularisation (Ridge)                  | Q10,Q32,Q50             | Medium         |
| ⭐       | Precision-Recall tradeoff + F1          | Q25,Q28,Q30             | Medium         |

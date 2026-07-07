---
# BASIC MACHINE LEARNING
## Complete Exam-Preparation Notes
### IIT M.Tech AI/ML Entrance Examination
---

## 2-WEEK STUDY PLAN — BASIC MACHINE LEARNING

| Day        | Topics                                                                            | Activity                                         |
| ---------- | --------------------------------------------------------------------------------- | ------------------------------------------------ |
| **Day 1**  | ML framework — problem types, supervised vs unsupervised, bias-variance tradeoff  | Read notes + solve 8 questions                   |
| **Day 2**  | Correlation (Pearson, Spearman, Kendall) — review from P&S                        | Revise P&S correlation notes + 10 questions      |
| **Day 3**  | Simple Linear Regression — theory, OLS, R²                                        | Read notes + solve 10 questions                  |
| **Day 4**  | Model assessment — residual analysis, goodness of fit, F-statistic                | Read notes + solve 10 questions                  |
| **Day 5**  | Multiple Linear Regression + Cross-validation                                     | Read notes + solve 10 questions                  |
| **Day 6**  | Classification intro + Logistic Regression (theory + sigmoid)                     | Read notes + solve 10 questions                  |
| **Day 7**  | **REVISION DAY** — Regression + Logistic Regression                               | Redo all solved examples. Formula sheet revision |
| **Day 8**  | Logistic Regression — decision boundary, MLE, interpretation                      | Read notes + solve 10 questions                  |
| **Day 9**  | Classification performance metrics — confusion matrix, recall, precision, F1, ROC | Read notes + solve 10 questions                  |
| **Day 10** | k-Nearest Neighbours (kNN)                                                        | Read notes + solve 10 questions                  |
| **Day 11** | K-Means Clustering                                                                | Read notes + solve 10 questions                  |
| **Day 12** | Mixed review — regression + classification + clustering                           | Solve 20 mixed problems from sample paper        |
| **Day 13** | **FULL REVISION** — All topics, formula sheet                                     | Go through summary sections only                 |
| **Day 14** | **MOCK TEST DAY**                                                                 | Attempt full sample paper under timed conditions |

**Daily time commitment:** 2–3 hours
**Priority order:** Logistic Regression → Performance Metrics → Linear Regression → Cross-validation → kNN → K-Means → Correlation

---

---

# PART 1 — THE DATA SCIENCE / ML FRAMEWORK

---

## 1.1 What is Machine Learning?

**Definition:** Machine learning is the science of building algorithms that learn patterns from data and use those patterns to make predictions or decisions on new, unseen data.

**The general ML workflow:**

1. **Define the problem** — what are you predicting? What data do you have?
2. **Collect and clean data** — handle missing values, outliers, scaling
3. **Exploratory Data Analysis (EDA)** — visualise, compute correlations, understand distributions
4. **Choose a model** — regression, classification, or clustering?
5. **Fit the model** — estimate parameters from training data
6. **Assess the model** — does it generalise? Is it overfit?
7. **Iterate** — improve features, tune hyperparameters

---

## 1.2 Types of ML Problems ⭐

| Type                                        | Goal                       | Output                 | Examples                   |
| ------------------------------------------- | -------------------------- | ---------------------- | -------------------------- |
| **Supervised — Regression**                 | Predict a continuous value | Number                 | House price, temperature   |
| **Supervised — Classification**             | Predict a category         | Class label            | Spam/not spam, tumour type |
| **Unsupervised — Clustering**               | Find natural groupings     | Cluster assignment     | Customer segments          |
| **Unsupervised — Dimensionality Reduction** | Compress features          | Reduced representation | PCA                        |

**Supervised learning:** We have labelled data — $(x_i, y_i)$ pairs. The goal is to learn a function $f$ such that $f(x) \approx y$.

**Unsupervised learning:** We only have $x_i$. No labels. Find structure in the data itself.

---

## 1.3 Bias-Variance Tradeoff ⭐

**The fundamental tension in ML:**

$$\text{Expected Test Error} = \text{Bias}^2 + \text{Variance} + \text{Irreducible Noise}$$

| Term                  | Definition                                                           | Caused by                       |
| --------------------- | -------------------------------------------------------------------- | ------------------------------- |
| **Bias**              | How far off the model's average prediction is from the truth         | Model too simple (underfitting) |
| **Variance**          | How much the model's predictions vary across different training sets | Model too complex (overfitting) |
| **Irreducible noise** | Noise inherent in the data                                           | Cannot be reduced               |

**Underfitting:** High bias, low variance. Model is too simple — misses the true pattern. Training error AND test error are both high.

**Overfitting:** Low bias, high variance. Model memorises training data — fails on new data. Training error is low but test error is high. ⭐

**Intuition:** A very flexible model (e.g., very high-degree polynomial) fits training data perfectly but is extremely sensitive to which specific data points it was trained on — its predictions vary wildly for new inputs.

> **! NOTE:** The goal is NOT to minimise training error. The goal is to minimise **generalisation error** (test error). Always evaluate on data the model has NOT seen.

---

## 1.4 Training, Validation, and Test Sets ⭐

| Split              | Purpose                            | Typical Size |
| ------------------ | ---------------------------------- | ------------ |
| **Training set**   | Fit model parameters               | 60–80%       |
| **Validation set** | Tune hyperparameters, select model | 10–20%       |
| **Test set**       | Final, unbiased evaluation         | 10–20%       |

**Key rule:** The test set is touched ONLY ONCE — at the very end. Using test data to tune the model defeats its purpose.

---

## 1.5 Cross-Validation ⭐

**Purpose:** When data is limited, use ALL of it for both training and evaluation.

### k-Fold Cross-Validation

1. Divide data into k equal folds
2. In each round, train on k−1 folds, validate on the remaining 1 fold
3. Repeat k times (each fold serves as validation once)
4. Average the k validation errors

$$\text{CV Error} = \frac{1}{k}\sum_{i=1}^k \text{Error}_i$$

### Leave-One-Out Cross-Validation (LOOCV) ⭐

- Special case of k-fold where k = n (each single observation is the validation set)
- **Less bias** in the error estimate (uses almost all data for training) ⭐
- **More variance** — highly variable because each training set differs by only one point
- **May overfit** — selects models with more parameters than optimal ⭐

**From sample paper Q27:**

- LOOCV → **LESS bias** than validation set approach ✓
- LOOCV **may select a model with more parameters** than optimal ✓ (because nearly the same data is used each time — tends to favour complex models)

> **! NOTE:** "Less bias" in LOOCV means the error estimate itself is less biased (closer to the true test error), NOT that the model has less bias.

---

---

# PART 2 — CORRELATION

---

## 2.1 Why Correlation Matters in ML

Before building any model, you must understand the relationships between variables. Correlation is the primary tool for this.

**Important:** Correlation measures **association**, not causation. And for regression, we need to check which features are correlated with the response AND which features are correlated with each other (multicollinearity).

_(Full coverage of Pearson, Spearman, Kendall, and Anscombe's Quartet is in the Probability & Statistics notes — Part 6. Review those before proceeding.)_

**Key ML context for correlation:**

| Use Case                               | Which correlation   |
| -------------------------------------- | ------------------- |
| Feature-response linear relationship   | Pearson r           |
| Ranked survey data (Likert scale)      | Spearman            |
| Small samples, expert rankings         | Kendall τ           |
| Detecting monotone non-linear patterns | Spearman or Kendall |

**Multicollinearity warning:** If two predictor variables are highly correlated with each other (|r| close to 1), $A^TA$ becomes nearly singular — coefficient estimates become unstable. Fix: remove one variable, or use Ridge regression.

---

---

# PART 3 — SIMPLE LINEAR REGRESSION

---

## 3.1 Concept Overview ⭐

**Goal:** Model the linear relationship between a **response variable** Y and a **predictor variable** X.

$$Y = \beta_0 + \beta_1 X + \varepsilon$$

where:

- $\beta_0$ = intercept (value of Y when X = 0)
- $\beta_1$ = slope (change in Y for a one-unit increase in X)
- $\varepsilon$ = error term (random noise), assumed $\varepsilon \sim N(0, \sigma^2)$

**Fitted model:** $\hat{Y} = \hat{\beta}_0 + \hat{\beta}_1 X$

**Residual:** $e_i = y_i - \hat{y}_i$ (actual minus predicted)

---

## 3.2 Ordinary Least Squares (OLS) — Parameter Estimation ⭐

**Objective:** Minimise the Sum of Squared Residuals (SSR):

$$\text{SSR} = \sum_{i=1}^n e_i^2 = \sum_{i=1}^n (y_i - \hat{\beta}_0 - \hat{\beta}_1 x_i)^2$$

**Closed-form OLS estimates:** ⭐

$$\hat{\beta}_1 = \frac{S_{XY}}{S_{XX}} = \frac{\sum_{i=1}^n (x_i - \bar{x})(y_i - \bar{y})}{\sum_{i=1}^n (x_i - \bar{x})^2}$$

$$\hat{\beta}_0 = \bar{y} - \hat{\beta}_1 \bar{x}$$

where $S_{XY} = \sum(x_i - \bar{x})(y_i - \bar{y})$ and $S_{XX} = \sum(x_i - \bar{x})^2$.

**Note:** The regression line always passes through $(\bar{x}, \bar{y})$.

**Connection to Pearson r:** ⭐

$$\hat{\beta}_1 = r_{XY} \cdot \frac{S_Y}{S_X}$$

where $S_Y$, $S_X$ are the standard deviations of Y and X.

### Worked Example ⭐

**Data:** (1,3), (2,5), (3,6), (4,8), (5,9)

$$\bar{x} = 3, \quad \bar{y} = 6.2$$

$$S_{XX} = (1-3)^2+(2-3)^2+(3-3)^2+(4-3)^2+(5-3)^2 = 4+1+0+1+4 = 10$$

$$S_{XY} = (1-3)(3-6.2)+(2-3)(5-6.2)+(3-3)(6-6.2)+(4-3)(8-6.2)+(5-3)(9-6.2)$$
$$= (-2)(-3.2)+(-1)(-1.2)+(0)(-0.2)+(1)(1.8)+(2)(2.8) = 6.4+1.2+0+1.8+5.6 = 15$$

$$\hat{\beta}_1 = \frac{15}{10} = 1.5, \quad \hat{\beta}_0 = 6.2 - 1.5 \times 3 = 1.7$$

$$\hat{Y} = 1.7 + 1.5X$$

---

## 3.3 Model Assessment ⭐

### Sum of Squares Decomposition

$$\underbrace{\sum(y_i - \bar{y})^2}_{SST} = \underbrace{\sum(\hat{y}_i - \bar{y})^2}_{SSReg} + \underbrace{\sum(y_i - \hat{y}_i)^2}_{SSE}$$

| Term  | Name                      | Meaning                             |
| ----- | ------------------------- | ----------------------------------- |
| SST   | Total Sum of Squares      | Total variability in Y              |
| SSReg | Regression Sum of Squares | Variability explained by the model  |
| SSE   | Error Sum of Squares      | Unexplained variability (residuals) |

### R² — Coefficient of Determination ⭐

$$R^2 = \frac{SSReg}{SST} = 1 - \frac{SSE}{SST}$$

- Range: $0 \leq R^2 \leq 1$
- $R^2 = 0$: model explains nothing; $R^2 = 1$: model explains everything
- **For simple linear regression:** $R^2 = r_{XY}^2$ (square of Pearson correlation) ⭐
- **Important:** $R^2$ always increases when you add more predictors, even useless ones → use **Adjusted R²** for multiple regression

### Mean Squared Error (MSE)

$$\hat{\sigma}^2 = MSE = \frac{SSE}{n-2}$$

Divides by $n-2$ (not $n$) because 2 parameters ($\beta_0$, $\beta_1$) are estimated.

---

## 3.4 Testing Significance — t-test and F-test ⭐

### t-test for Slope

$H_0: \beta_1 = 0$ (X has no effect on Y) vs $H_1: \beta_1 \neq 0$

$$T = \frac{\hat{\beta}_1}{SE(\hat{\beta}_1)} \sim t(n-2) \quad \text{under } H_0$$

where $SE(\hat{\beta}_1) = \sqrt{\frac{\hat{\sigma}^2}{S_{XX}}}$

### F-test for Overall Regression ⭐

$$F = \frac{SSReg / p}{SSE / (n-p-1)} = \frac{MSReg}{MSE}$$

where p = number of predictors.

For simple regression (p=1):

$$F = \frac{SSReg / 1}{SSE / (n-2)} \sim F(1, n-2) \quad \text{under } H_0$$

**Decision:** Reject $H_0$ if $F > F_{\alpha, 1, n-2}$

**Note:** For simple regression, $F = T^2$ exactly.

---

## 3.5 Residual Analysis ⭐

**Why:** OLS assumptions must be verified. If violated, inference is unreliable.

**OLS assumptions (LINE):**

- **L**inear relationship between X and Y
- **I**ndependent errors
- **N**ormally distributed errors
- **E**qual variance (homoscedasticity)

**Residual plots to check:**

| Plot                 | What to look for        | Problem if                                            |
| -------------------- | ----------------------- | ----------------------------------------------------- |
| Residuals vs Fitted  | Random scatter around 0 | Pattern present → non-linearity or heteroscedasticity |
| QQ plot of residuals | Points on 45° line      | Curve → non-normal errors                             |
| Residuals vs X       | Random scatter          | Fan shape → heteroscedasticity                        |
| Scale-Location       | Horizontal band         | Upward trend → variance increasing                    |

**Anscombe's Quartet lesson:** Always plot your data and residuals. Four datasets with identical R², slope, and intercept can have completely different underlying structures.

---

## 3.6 Prediction vs Confidence Intervals ⭐

| Interval type | What it covers | Width |
|---------------|---------------|-------|
| **Confidence interval** for $E[Y \mid x_0]$ | The true mean response at $x_0$ | Narrower |
| **Prediction interval** for a new $Y$ at $x_0$ | A single new observation at $x_0$ | Wider (adds individual error) |

Both are wider at the extremes (far from $\bar{x}$) and narrowest at $x = \bar{x}$.

---

---

# PART 4 — MULTIPLE LINEAR REGRESSION (MLR)

---

## 4.1 Model ⭐

$$Y = \beta_0 + \beta_1 X_1 + \beta_2 X_2 + \cdots + \beta_p X_p + \varepsilon$$

**Matrix form:**

$$\mathbf{Y} = A\boldsymbol{\beta} + \boldsymbol{\varepsilon}$$

where $A$ is the $n \times (p+1)$ design matrix (first column all 1s for intercept).

**OLS solution (same as pseudo-inverse):**

$$\hat{\boldsymbol{\beta}} = (A^TA)^{-1}A^T\mathbf{Y}$$

**Fitted values:** $\hat{\mathbf{Y}} = A\hat{\boldsymbol{\beta}} = A(A^TA)^{-1}A^T\mathbf{Y} = P\mathbf{Y}$

where $P = A(A^TA)^{-1}A^T$ is the **hat matrix** (projection matrix onto col(A)) ⭐

---

## 4.2 Adjusted R² ⭐

$$R^2_{adj} = 1 - \frac{SSE/(n-p-1)}{SST/(n-1)} = 1 - (1-R^2)\frac{n-1}{n-p-1}$$

- Penalises for adding extra predictors
- Only increases if the new predictor genuinely improves the model
- Use Adjusted R² (not plain R²) to compare models with different numbers of predictors ⭐

> **! NOTE:** Plain R² ALWAYS increases when you add more variables, even random noise. Adjusted R² can decrease if the added variable doesn't help enough.

---

## 4.3 Multicollinearity ⭐

**Problem:** Two or more predictor variables are highly correlated with each other.

**Consequences:**

- $A^TA$ becomes nearly singular → coefficient estimates become very large and unstable
- Standard errors blow up → t-statistics become small → variables appear insignificant even if they are
- Coefficients change drastically when one predictor is added/removed

**Detection:** Compute correlation matrix of predictors. VIF (Variance Inflation Factor) > 10 is a warning sign.

**Fix:** Remove one of the correlated predictors, or use **Ridge regression** (adds $\lambda I$ to $A^TA$).

---

---

# PART 5 — CLASSIFICATION

---

## 5.1 Classification vs Regression ⭐

| Feature            | Regression        | Classification               |
| ------------------ | ----------------- | ---------------------------- |
| Output Y           | Continuous        | Discrete category            |
| Model output       | Predicted value   | Class label (or probability) |
| Loss function      | MSE, SSE          | Log-loss, cross-entropy      |
| Example algorithms | Linear regression | Logistic regression, kNN     |

**Why not use linear regression for classification?**

- Linear regression can predict values outside [0,1] — meaningless as probabilities
- Not designed to handle categorical outputs
- Decision boundary is not well-defined

---

## 5.2 Logistic Regression ⭐

### Concept

**Goal:** Predict the **probability** that an observation belongs to class 1 (binary classification).

$$P(Y=1 | X=x) = \frac{1}{1 + e^{-(\beta_0 + \beta_1 x)}}$$

This is the **sigmoid (logistic) function:**

$$\sigma(z) = \frac{1}{1 + e^{-z}}, \quad z = \beta_0 + \beta_1 x$$

**Properties of sigmoid:** ⭐

| z         | σ(z) |
| --------- | ---- |
| $-\infty$ | 0    |
| 0         | 0.5  |
| $+\infty$ | 1    |

- Output is always in (0, 1) — valid probability ⭐
- S-shaped curve
- $\sigma(-z) = 1 - \sigma(z)$ — symmetric about 0.5

### The Log-Odds (Logit) ⭐

### What are Odds?

Before log-odds, understand plain **odds**:

$$\text{odds} = \frac{P(\text{event happens})}{P(\text{event does not happen})} = \frac{p}{1-p}$$

| $p$ | Odds | Meaning |
|-----|------|---------|
| 0.5 | 1 | Equally likely either way |
| 0.75 | 3 | Three times more likely to happen |
| 0.1 | 1/9 | Much more likely NOT to happen |

---

### Deriving the Log-Odds Formula

Start from $p = \sigma(\beta_0 + \beta_1 x)$. Compute the odds directly:

$$\frac{p}{1-p} = \frac{\frac{1}{1+e^{-z}}}{\frac{e^{-z}}{1+e^{-z}}} = \frac{1}{e^{-z}} = e^z \quad \text{where } z = \beta_0+\beta_1 x$$

Take the natural log of both sides:

$$\log\frac{P(Y=1 \mid x)}{P(Y=0 \mid x)} = \log(e^z) = z = \beta_0 + \beta_1 x$$

**The log-odds is perfectly linear in $x$.**

---

### Three Key Insights

**1. Linear in log-odds space, non-linear in probability space**

| Space | Relationship with $x$ |
|-------|----------------------|
| Probability $p$ vs $x$ | S-shaped sigmoid curve (non-linear) |
| Log-odds vs $x$ | Straight line (linear) |

Logistic regression is doing linear regression on the log-odds scale. The sigmoid is simply the function that converts that linear output back into a valid probability in $[0,1]$.

**2. Interpretation of $\beta_1$ — the Odds Ratio** ⭐

A one-unit increase in $x$ multiplies the odds by $e^{\beta_1}$:

$$\text{odds}(x+1) = e^{\beta_0+\beta_1(x+1)} = e^{\beta_1} \times \text{odds}(x)$$

$e^{\beta_1}$ is called the **odds ratio** — widely reported in medical and social science research.

- $\beta_1 = 0.5 \implies e^{0.5} \approx 1.65$ — each unit increase raises odds by 65%
- $\beta_1 = -1 \implies e^{-1} \approx 0.37$ — each unit increase lowers odds by 63%
- $\beta_1 = 0 \implies e^0 = 1$ — $x$ has no effect on the odds

**3. Why the decision boundary is linear** ⭐

The decision boundary is where $P(Y=1\mid x) = 0.5$, which means odds $= 1$, which means log-odds $= 0$:

$$\beta_0 + \beta_1 x = 0 \implies x^* = -\frac{\beta_0}{\beta_1}$$

In higher dimensions with features $\mathbf{x} \in \mathbb{R}^p$:

$$\boldsymbol{\beta}^T\mathbf{x} = 0$$

This is always a **hyperplane** — a linear boundary in feature space regardless of how curved the probability surface looks. This is what makes logistic regression a **linear classifier**.

### Decision Boundary ⭐

**Default threshold:** Predict class 1 if $\hat{P}(Y=1|x) \geq 0.5$, class 0 otherwise.

At threshold 0.5:
$$\sigma(z) = 0.5 \iff z = 0 \iff \beta_0 + \beta_1 x = 0$$

This defines a **linear decision boundary** in feature space. ⭐

**From sample paper Q9:** If $P(Y=k|X=x)$ is linear in x, then the **decision boundary is linear**. ✓

### Parameter Estimation — Maximum Likelihood

Unlike linear regression (which uses OLS), logistic regression uses **Maximum Likelihood Estimation (MLE)**.

**Log-likelihood:**

$$\ell(\boldsymbol{\beta}) = \sum_{i=1}^n \left[y_i \log(\hat{p}_i) + (1-y_i)\log(1-\hat{p}_i)\right]$$

**Maximise** $\ell(\boldsymbol{\beta})$ with respect to $\boldsymbol{\beta}$ — no closed form, solved numerically (gradient ascent).

> **! NOTE:** There is no closed-form formula for logistic regression coefficients unlike $\hat{\boldsymbol{\beta}} = (A^TA)^{-1}A^T\mathbf{Y}$ in linear regression.

### Worked Example ⭐

Fit logistic regression to predict cancer (Y=1) vs benign (Y=0) from tumour size X.

Suppose fitted model: $\log\left(\frac{\hat{p}}{1-\hat{p}}\right) = -6 + 0.1x$

For $x = 50$ (mm): $z = -6 + 5 = -1$, $\hat{p} = \sigma(-1) = 1/(1+e) \approx 0.27$

Predict: class 0 (benign) since $0.27 < 0.5$.

**Decision boundary:** $-6 + 0.1x = 0 \implies x = 60$ mm. Tumours larger than 60mm predicted cancerous.

---

## 5.3 Classification Performance Metrics ⭐

### Confusion Matrix

For binary classification (Positive = 1, Negative = 0):

|                     | Predicted Positive  | Predicted Negative  |
| ------------------- | ------------------- | ------------------- |
| **Actual Positive** | TP (True Positive)  | FN (False Negative) |
| **Actual Negative** | FP (False Positive) | TN (True Negative)  |

### Key Metrics ⭐

| Metric                        | Formula                                                     | Meaning                                           |
| ----------------------------- | ----------------------------------------------------------- | ------------------------------------------------- |
| **Accuracy**                  | $(TP+TN)/(TP+TN+FP+FN)$                                     | Overall correct fraction                          |
| **Recall (Sensitivity, TPR)** | $TP/(TP+FN)$                                                | Of actual positives, how many caught?             |
| **Precision**                 | $TP/(TP+FP)$                                                | Of predicted positives, how many correct?         |
| **Specificity (TNR)**         | $TN/(TN+FP)$                                                | Of actual negatives, how many correctly rejected? |
| **F1 Score**                  | $2 \cdot \frac{Precision \cdot Recall}{Precision + Recall}$ | Harmonic mean of precision and recall             |
| **FNR (Miss Rate)**           | $FN/(TP+FN) = 1 - \text{Recall}$                            | Of actual positives, how many missed?             |
| **FPR (Fall-out)**            | $FP/(FP+TN) = 1 - \text{Specificity}$                       | Of actual negatives, how many falsely flagged?    |

**Recall vs Precision trade-off:** ⭐

- Raising the classification threshold → fewer positives predicted → FP decreases, FN increases → Precision ↑, Recall ↓
- Lowering the threshold → more positives predicted → Recall ↑, Precision ↓

**When to prioritise Recall:** Cancer detection (missing a cancer is worse than a false alarm)
**When to prioritise Precision:** Spam filter (wrongly blocking legitimate email is costly)

### Worked Example ⭐ (from Sample Paper Q25)

**100 subjects, 10 true negatives. Recall = 8/9, Precision = 8/9. Find FNR.**

True negatives = 10 → True positives + FP + FN = 90 → Actual positives = 90

$$\text{Recall} = \frac{TP}{TP + FN} = \frac{8}{9} \implies TP = 80, \quad FN = 10$$

$$\text{FNR} = \frac{FN}{TP+FN} = \frac{10}{90} = \frac{1}{9} \approx 0.111$$

**Verify Precision:**

$$\text{Precision} = \frac{TP}{TP+FP} = \frac{8}{9} \implies TP+FP = 90 \implies FP = 10$$

Total: TP=80, FN=10, FP=10, TN=10. Sum = 110... wait: n=100.

Corrected: TN=10, actual positives + actual negatives = 100. If actual negatives = 10 (TN=10, FP must account for the rest):

TP+FN = 90 (actual positives). Recall = 8/9 → TP = 80, FN = 10.

**Answer: FNR = 1/9 ≈ 0.111** ✓

---

## 5.4 ROC Curve ⭐

**Receiver Operating Characteristic curve:** Plot of **TPR (Recall)** vs **FPR** as the classification threshold varies from 1 to 0.

**X-axis:** FPR = $FP/(FP+TN)$ — false positive rate
**Y-axis:** TPR = $TP/(TP+FN)$ — true positive rate (Recall)

**Key points on ROC curve:** ⭐

| Point  | Meaning                                                    |
| ------ | ---------------------------------------------------------- |
| (0, 0) | Threshold = 1: predict everything negative. No TP, no FP   |
| (1, 1) | Threshold = 0: predict everything positive. All TP, all FP |
| (0, 1) | Perfect classifier: all TP, no FP                          |
| (1, 0) | Worst classifier: all FP, no TP                            |

**From sample paper Q26:** Point (1,1) on ROC → classifies ALL samples of BOTH classes correctly? No — (1,1) means FPR=1 and TPR=1, meaning ALL positives are caught (TPR=1) BUT all negatives are also wrongly classified as positive (FPR=1). So: **model classifies only positive class correctly** — it flags everything as positive.

**AUC (Area Under Curve):**

- AUC = 1: perfect classifier
- AUC = 0.5: random classifier (diagonal line)
- AUC < 0.5: worse than random (predictions inverted)

---

## 5.5 k-Nearest Neighbours (kNN) ⭐

### Concept

**Idea:** To classify a new point, find the k training points closest to it and take a majority vote.

**No training phase** — kNN is a **lazy learner**: all computation happens at prediction time. ⭐

### Algorithm ⭐

1. Compute distance from the test point to ALL training points
2. Order training points by increasing distance
3. Select top k nearest neighbours
4. Predict the majority class among those k neighbours

**From sample paper Q35:** Correct order → iv, i, iii, ii ✓

### Distance Metrics

Most commonly used: **Euclidean distance**:

$$d(x, x') = \sqrt{\sum_{j=1}^p (x_j - x'_j)^2}$$

Other options: Manhattan distance, Cosine similarity.

### Choosing k ⭐

| k small                            | k large                  |
| ---------------------------------- | ------------------------ |
| Low bias, high variance            | High bias, low variance  |
| Overfits (memorises training data) | Underfits (too smooth)   |
| Decision boundary very irregular   | Decision boundary smooth |

**Rule of thumb:** Use cross-validation to choose k. Common starting points: k = $\sqrt{n}$.

> **! NOTE:** k=1 means each test point is classified by its single nearest neighbour — extremely overfit. k=n means every point is classified as the majority class — extremely underfit.

### Key Properties ⭐

- **Non-parametric:** no assumptions about data distribution
- **Non-linear:** can model complex boundaries
- **Sensitive to scale:** always normalise features before using kNN ⭐
- **Curse of dimensionality:** distance becomes less meaningful in very high dimensions — all points appear equidistant

---

---

# PART 6 — K-MEANS CLUSTERING

---

## 6.1 Concept Overview ⭐

**Goal:** Partition n data points into k clusters such that **within-cluster variance is minimised.** ⭐

**From sample paper Q30:** K-means objective = **minimise within-cluster variance** ✓

$$\text{Minimise:} \quad J = \sum_{j=1}^k \sum_{i \in C_j} \|x_i - \mu_j\|^2$$

where $\mu_j$ is the centroid (mean) of cluster $j$ and $C_j$ is the set of points in cluster $j$.

---

## 6.2 Algorithm ⭐

**Initialise:** Choose k initial centroids (random or by k-means++ heuristic)

**Repeat until convergence:**

1. **Assignment step:** Assign each point to the nearest centroid:
   $$C_j = \{x_i : \|x_i - \mu_j\|^2 \leq \|x_i - \mu_l\|^2 \text{ for all } l\}$$

2. **Update step:** Recompute centroids as mean of assigned points:
   $$\mu_j = \frac{1}{|C_j|}\sum_{i \in C_j} x_i$$

**Convergence:** Stop when assignments no longer change (or change is negligible).

---

## 6.3 Properties ⭐

| Property                        | Detail                                               |
| ------------------------------- | ---------------------------------------------------- |
| **Guaranteed convergence**      | Yes — J decreases or stays the same at every step    |
| **Global optimum**              | NOT guaranteed — result depends on initial centroids |
| **Sensitive to initialisation** | Yes — run multiple times and take best result        |
| **Sensitive to outliers**       | Yes — outliers pull centroids                        |
| **Assumes clusters are**        | Spherical, similar size, similar density             |
| **k must be specified**         | Yes — k is a hyperparameter                          |

**How to choose k:** Elbow method — plot J vs k. The "elbow" point where J stops decreasing sharply is a good choice.

---

## 6.4 K-Means vs Expectation-Maximisation (EM)

K-means is a special case of the EM algorithm where:

- Each cluster is assumed to have equal, spherical covariance (identity covariance matrix)
- Hard assignment (each point belongs to exactly one cluster)

---

---

# PART 7 — EXAM FOCUS TOPICS

---

## 7.1 High-Frequency Sample Paper Topics ⭐

Based on analysis of the sample paper and assignment questions:

| Topic                              | Sample Paper Q# | What was asked                                  |
| ---------------------------------- | --------------- | ----------------------------------------------- |
| Independence of events             | Q1              | Which events are independent/mutually exclusive |
| Conditional probability            | Q3              | Total probability theorem numerical             |
| Box plot interpretation            | Q6              | Compare manufacturers from box plots            |
| Monotonicity (Spearman-type)       | Q10             | Describe behaviour of y vs x                    |
| Mean of uniform distribution       | Q15             | Disjoint support — compute E[X]                 |
| Marginal PDF from joint            | Q16             | Integrate out one variable                      |
| False negative rate                | Q25             | Confusion matrix + recall/precision             |
| ROC curve interpretation           | Q26             | Meaning of point (1,1)                          |
| LOOCV bias properties              | Q27             | Multi-select true/false                         |
| Bayes theorem                      | Q34             | Defective battery problem                       |
| F-statistic                        | Q37             | Compute from two sample sets                    |
| Digit counting (P&C)               | Q38             | Numbers between 10 and 10,000                   |
| Conditional probability continuous | Q39             | Uniform [0,1] minimum/maximum                   |
| Robust measures                    | Q40             | Which are robust to outliers                    |

---

## 7.2 Sigmoid Function — Common Exam Questions ⭐

From sample paper Q2: "Value of sigmoid at x = −∞ and x = +∞?"
**Answer: 0, 1** (not 1,0 — order matters!)

$$\sigma(-\infty) = \frac{1}{1+e^{+\infty}} = \frac{1}{\infty} = 0, \qquad \sigma(+\infty) = \frac{1}{1+e^{-\infty}} = \frac{1}{1+0} = 1$$

---

## 7.3 Decision Boundary — Logistic Regression ⭐

**Key fact (sample paper Q9):** If the posterior $P(Y=k|X=x)$ is linear in x, then the decision boundary is **linear**.

This is the defining property of logistic regression — it is a **linear classifier** even though it outputs probabilities.

**Non-linear decision boundaries:** Achieved by adding polynomial features (e.g., $x^2$, $x_1 x_2$) or using non-linear kernels.

---

## 7.4 Model Comparison — Which to Use When ⭐

| Situation                              | Recommended Approach              |
| -------------------------------------- | --------------------------------- |
| Continuous Y, linear relationship      | Simple/Multiple Linear Regression |
| Binary Y                               | Logistic Regression               |
| Non-linear boundary, small dataset     | kNN                               |
| No labels, find groups                 | K-Means Clustering                |
| Many correlated features               | Ridge Regression (λ > 0)          |
| Limited data, want good error estimate | k-Fold or LOOCV                   |
| Ordinal feature or response            | Spearman/Kendall correlation      |

---

---

# MASTER FORMULA SHEET — BASIC ML

## Regression

$$\hat{\beta}_1 = \frac{S_{XY}}{S_{XX}}, \quad \hat{\beta}_0 = \bar{y} - \hat{\beta}_1\bar{x}$$

$$R^2 = 1 - \frac{SSE}{SST} = r^2 \text{ (simple LR)}, \quad MSE = \frac{SSE}{n-2}$$

$$F = \frac{SSReg/p}{SSE/(n-p-1)}, \quad \hat{\boldsymbol{\beta}} = (A^TA)^{-1}A^T\mathbf{Y} \text{ (MLR)}$$

## Logistic Regression

$$\hat{p}(x) = \sigma(\beta_0 + \beta_1 x) = \frac{1}{1+e^{-(\beta_0+\beta_1 x)}}$$

$$\log\frac{p}{1-p} = \beta_0 + \beta_1 x \quad \text{(log-odds = linear in x)}$$

$$\sigma(-\infty) = 0, \quad \sigma(0) = 0.5, \quad \sigma(+\infty) = 1$$

## Classification Metrics

$$\text{Recall} = \frac{TP}{TP+FN}, \quad \text{Precision} = \frac{TP}{TP+FP}$$

$$\text{Accuracy} = \frac{TP+TN}{TP+TN+FP+FN}, \quad F_1 = 2\cdot\frac{P \cdot R}{P+R}$$

$$\text{FNR} = \frac{FN}{TP+FN} = 1 - \text{Recall}, \quad \text{FPR} = \frac{FP}{FP+TN}$$

## kNN

$$d(x,x') = \sqrt{\sum_j(x_j-x'_j)^2} \quad \text{(Euclidean)}$$

- Small k → overfit; Large k → underfit
- Always normalise features before applying kNN

## K-Means

$$J = \sum_{j=1}^k \sum_{i \in C_j} \|x_i - \mu_j\|^2 \quad \text{(objective: minimise within-cluster variance)}$$

$$\mu_j = \frac{1}{|C_j|}\sum_{i \in C_j} x_i \quad \text{(centroid update)}$$

## Cross-Validation

$$\text{CV Error} = \frac{1}{k}\sum_{i=1}^k \text{Error}_i$$

- LOOCV: k = n; less bias in error estimate; may pick overly complex model

## Bias-Variance

$$\text{Test Error} = \text{Bias}^2 + \text{Variance} + \text{Irreducible Noise}$$

---

## Quick Decision Cheat Sheet ⭐

| Question type                | Key formula / fact                          |
| ---------------------------- | ------------------------------------------- |
| Sigmoid at 0                 | 0.5                                         |
| Sigmoid at ±∞                | 0, 1                                        |
| ROC point (1,1)              | FPR=1, TPR=1 → predicts everything positive |
| ROC point (0,1)              | Perfect classifier                          |
| LOOCV bias                   | Less bias than validation set approach      |
| LOOCV model selection        | May pick more complex model than optimal    |
| K-means objective            | Minimise within-cluster variance            |
| Logistic regression boundary | Linear (in feature space)                   |
| kNN: small k                 | Overfit                                     |
| kNN: large k                 | Underfit                                    |
| R² always increases          | Adding predictors → use Adjusted R²         |
| Robust measures              | Median, MAD                                 |
| Not robust                   | Mean, variance, standard deviation          |

---

_End of Basic Machine Learning Notes_

---

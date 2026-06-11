# 📊 Statistics & Regression Field Manual
### A Practical Reference for Sales & Customer Data Analysis

> **The problem this solves:** You studied statistics — probability, T-tests, ANOVA, regression — and understood each topic individually. But when facing real data, you freeze. Which tool do I use? How do I read the output? How do I combine them in one project?
> 
> This manual answers exactly that.

---

## 📁 What's in this repo

| File | Description |
|------|-------------|
| `Statistics_Reference_Manual.docx` | Full formatted manual (Decision Map, Module Cards, Project Walkthrough, Common Mistakes) |
| `Python_Statistics_Reference.md` | Clean Python code for every statistical method |
| `README.md` | This file |

---

## 🗺️ Part 1 — Decision Map

Before picking a tool, answer one question: **What is your goal?**

| Goal | Tool |
|------|------|
| Describe data shape & outliers | Probability + Z-Score + Distribution |
| Estimate an unknown population value | Confidence Interval |
| Compare 2 groups | Two-Sample T-Test |
| Compare 3+ groups | ANOVA |
| Test a proportion (%) | Population Proportion Test |
| Find association between categories | Chi-Squared |
| Predict a numeric outcome | Linear Regression |
| Predict a binary outcome (yes/no) | Logistic Regression |
| Compare groups while controlling a variable | ANCOVA |
| Multiple dependent variables together | MANOVA / MANCOVA |
| Prove causality from an experiment | A/B Testing + Experimental Design |

### 3-Step Decision Tree

```
STEP 1 — How many dependent variables?
    One        → STEP 2
    More than one → MANOVA / MANCOVA

STEP 2 — What type is your dependent variable?
    Continuous number  → STEP 3
    Yes / No (binary)  → Logistic Regression
    Unordered categories → Chi-Squared

STEP 3 — What is your goal?
    Describe data        → Probability + Z-Score + Distribution
    Estimate a value     → Confidence Interval
    Test a hypothesis    → T-Test (one or two sample)
    Compare 3+ groups    → ANOVA
    Measure relationship → Regression (Simple or Multiple)
    Test an experiment   → A/B Testing + Experimental Design
```

---

## 🃏 Part 2 — Module Cards

### 01 — Probability & Conditional Probability
- **Use when:** You want to understand the likelihood of an event in your data
- **Key formula:** `P(A|B) = P(A and B) / P(B)`
- **Sales example:** `P(purchase | email opened)` → if this is much higher than `P(purchase)`, focus your campaigns on email openers
- **Output to read:** Lift = `P(A|B) / P(A)` → Lift > 1 means B is a strong predictor of A

---

### 02 — Z-Score & Distributions
- **Use when:** You want to identify outliers and understand data spread
- **Output interpretation:**

| Z-Score | Meaning |
|---------|---------|
| 0 | Exactly average |
| +2 | Higher than 97.7% of customers |
| -2 | Lower than 97.7% — potential churn risk |
| > ±3 | Outlier — verify: data error or VIP? |

- **Sales application:** Compute Z-Score per customer on Revenue → segment into VIP / Normal / At-Risk

---

### 03 — Confidence Intervals
- **Use when:** You want to estimate a population value from a sample
- **Concept:** Instead of saying "average order value is 250" → say "average order value is between 237 and 263 with 95% confidence"
- **CI levels:**
  - 90% → faster, narrower, for quick decisions
  - 95% → standard for most business analysis
  - 99% → for high-stakes decisions
- **Output:** `CI = [lower, upper]` → any decision within this range is data-backed

---

### 04 — Hypothesis Testing & T-Tests
- **Core logic:**
  - H0 (Null): No difference / no effect — the default assumption
  - H1 (Alternative): There is a difference — what you're testing
  - `p < 0.05` → Reject H0 → result is statistically significant (not by chance)
  - `p ≥ 0.05` → Fail to reject H0 → insufficient evidence

| T-Test Type | Use When | Sales Example |
|-------------|----------|---------------|
| One-Sample | Compare sample mean to a known target | Is our average sales = 300 (the goal)? |
| Two-Sample (Independent) | Compare two different groups | Branch A vs Branch B sales |
| Paired | Same group before and after | Team performance before vs after training |

---

### 05 — A/B Testing & Experimental Design
- **Use when:** You want to prove causality — this change caused this result
- **vs Regression:** Regression analyzes historical data. A/B testing controls the experiment.
- **Steps:**
  1. Define ONE primary metric (conversion rate or revenue — not both)
  2. Calculate required sample size before starting
  3. Randomly split customers into control and treatment
  4. Run until you have enough data — don't stop early
  5. Analyze with T-Test (revenue) or Proportions Z-Test (conversion)

---

### 06 — Chi-Squared Test
- **Use when:** Both variables are categorical and you want to test association
- **Sales example:** Is customer type (new/returning) related to product category purchased?
- **Output:**
  - `p < 0.05` → significant association exists → use it for segmentation
  - Cramér's V → strength: `< 0.1` weak | `0.3+` moderate | `0.5+` strong
- **Warning:** Chi-Squared tells you IF there's a relationship — not how strong. Always compute Cramér's V.

---

### 07 — ANOVA, ANCOVA, MANOVA, MANCOVA

| Tool | Dependent Variables | Independent Variables | Use Case |
|------|--------------------|-----------------------|----------|
| ANOVA | 1 numeric | 1+ categorical (3+ groups) | Compare sales across 4 regions |
| ANCOVA | 1 numeric | categorical + numeric covariate | Compare regions while controlling for store size |
| MANOVA | 2+ numeric | 1+ categorical | Analyze Revenue + Satisfaction across regions simultaneously |
| MANCOVA | 2+ numeric | categorical + numeric covariate | MANOVA but controlling for an additional variable |

> **Critical:** ANOVA tells you a difference exists — not WHERE. Always follow with Post-Hoc Tukey test when `p < 0.05`.

---

### 08 — Linear Regression (Simple & Multiple)
- **Use when:** You want to predict a numeric outcome or measure the impact of variables
- **Formula:** `Y = β0 + β1X1 + β2X2 + ε`

| Metric | What it measures | Good value |
|--------|-----------------|------------|
| R² | % of variance explained | ≥ 0.65 |
| p-value (coefficient) | Is this variable significant? | < 0.05 |
| Coefficient (β) | Size of the effect | Any value with p < 0.05 |
| RMSE | Average prediction error | As small as possible |

- **5 Assumptions to check:**
  1. Linearity — plot Y vs X
  2. Independence — observations not correlated
  3. Homoscedasticity — constant variance (flat residual plot)
  4. Normality of residuals — Q-Q plot
  5. No multicollinearity — VIF < 5 for all variables

---

### 09 — Logistic Regression
- **Use when:** Your dependent variable Y is binary (buy/not buy, churn/not churn)
- **Output is a probability** between 0 and 1 — not a number

| Metric | Meaning |
|--------|---------|
| Odds Ratio | How many times more likely is Y=1 |
| Accuracy | % of correct predictions |
| AUC-ROC | Overall model quality: > 0.75 good / > 0.85 excellent |
| Confusion Matrix | Breakdown of true/false positives and negatives |

- **Sales application:** Build a model on age + visits + past spend → predict who will buy in the next campaign → rank all customers by probability score → target the top 100

---

## 🔗 When to Combine Tools

| Scenario | Tools | Order |
|----------|-------|-------|
| Customer Segmentation | Z-Score → ANOVA | Identify outliers first, then test group differences |
| Campaign Effectiveness | A/B Testing → T-Test → Chi-Squared | Design → test revenue → test conversion |
| Sales Forecasting | Linear Regression → Confidence Interval | Predict → add error bounds |
| Churn Prediction | Probability → Logistic Regression | Analyze patterns → build scoring model |
| Regional Performance | ANOVA → Tukey → Regression | Find difference → locate it → explain it |

---

## 🔬 Part 3 — Complete Project Walkthrough

**Scenario:** A retail company ran a 25% discount campaign across 3 regions. Did it work? In which region? Who responded?

### Step 1 — Explore
- Z-Score on sales → detect outliers before any analysis
- Plot distribution → is it normal?
- Conditional probability → `P(responded | VIP customer)`

### Step 2 — Estimate
- 95% Confidence Interval for mean sales per region
- CI for proportion of customers who responded

### Step 3 — Test
- Two-Sample T-Test → sales before vs after campaign
- Chi-Squared → is customer type linked to response?
- ANOVA → compare performance across 3 regions
- Tukey Post-Hoc → which specific regions differ?

### Step 4 — Model
- Multiple Linear Regression → impact of (region + age + purchase history) on sales
- Logistic Regression → who will respond to the next campaign?

### Step 5 — Conclude

```
T-Test:     p=0.019  → campaign significantly increased sales ✓
ANOVA:      p=0.003  → difference exists between regions
Tukey:               → Region C is different from A and B
Chi-Squared: p=0.041 → returning customers respond more
Regression: R²=0.71  → purchase history is the strongest predictor (β=0.43, p<0.001)
Logistic:   AUC=0.80 → model identifies likely buyers with 80% accuracy

Decision: Focus next campaign on returning customers in Region C,
          using the logistic model for targeting.
```

---

## 🐍 Part 4 — Python Code

See **[Python_Statistics_Reference.md](./Python_Statistics_Reference.md)** for clean, ready-to-run code for every method above.

**Quick reference:**

| Method | Function |
|--------|----------|
| One-Sample T-Test | `stats.ttest_1samp(x, popmean)` |
| Two-Sample T-Test | `stats.ttest_ind(a, b)` |
| Paired T-Test | `stats.ttest_rel(before, after)` |
| Chi-Squared | `stats.chi2_contingency(ct)` |
| One-Way ANOVA | `stats.f_oneway(*groups)` |
| Post-Hoc Tukey | `pg.pairwise_tukey(data, dv, between)` |
| OLS Regression | `smf.ols(formula, data).fit()` |
| Logistic Regression | `LogisticRegression().fit(X, y)` |
| CI for Mean | `stats.t.interval(0.95, ...)` |
| CI for Proportion | `proportion_confint(n, N)` |

---

## ⚠️ Part 5 — Common Interpretation Mistakes

| ❌ Wrong | ✅ Correct |
|---------|-----------|
| `p < 0.05` means the result is practically important | p-value measures chance, not importance. Always check Effect Size (Cohen's d, R²) |
| Correlation = Causation | Association ≠ cause. Use A/B Testing to establish causality |
| High R² = good model | R²=0.95 may mean overfitting. Always test on unseen data |
| ANOVA `p < 0.05` = all groups differ | ANOVA says a difference exists somewhere — Post-Hoc locates it |
| `p > 0.05` = no relationship | It means insufficient evidence in this data — sample may be too small |
| Rejecting H0 proves H1 | Rejecting H0 means data is inconsistent with H0 — not proof of H1 |
| 95% CI means 95% chance the true value is inside | 95% of intervals built this way will contain the true value |
| Running multiple T-Tests on 3+ groups | Use ANOVA — multiple T-Tests inflate Type I error rate |
| Always remove outliers | Outliers may be VIP customers or data errors — investigate first |

---

## 🔢 p-value Reference

| p-value | Interpretation | Decision |
|---------|---------------|----------|
| < 0.001 | Highly significant | Reject H0 with very high confidence |
| 0.001 – 0.01 | Strong significance | Reject H0 |
| 0.01 – 0.05 | Significant (standard threshold) | Reject H0 |
| 0.05 – 0.10 | Marginal | Decide based on context + effect size |
| > 0.10 | Not significant | Fail to reject H0 |

---

## 🏁 The Golden Rule

```
1. Understand the question
2. Choose the right tool
3. Check assumptions
4. Run the test
5. Read p-value + Effect Size
6. Translate to a business decision

Never start with the tool. Start with the question.
```

---

## 📚 Topics Covered

`Probability` `Conditional Probability` `Z-Score` `Probability Distribution`
`Sampling` `Sampling Distribution` `Population Proportion` `Confidence Intervals`
`Margin of Error` `Hypothesis Testing` `One-Sample T-Test` `Two-Sample T-Test`
`A/B Testing` `Experimental Design` `Chi-Squared` `ANOVA` `ANCOVA`
`MANOVA` `MANCOVA` `Simple Linear Regression` `Multiple Linear Regression`
`OLS` `Regression Assumptions` `Logistic Regression`

---

## 🛠️ Tech Stack

![Python](https://img.shields.io/badge/Python-3.8+-blue)
![pandas](https://img.shields.io/badge/pandas-✓-lightgrey)
![scipy](https://img.shields.io/badge/scipy-✓-lightgrey)
![statsmodels](https://img.shields.io/badge/statsmodels-✓-lightgrey)
![scikit--learn](https://img.shields.io/badge/scikit--learn-✓-lightgrey)
![pingouin](https://img.shields.io/badge/pingouin-✓-lightgrey)

---

*Built as a personal reference — June 2026*

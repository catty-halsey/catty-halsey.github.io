---
layout: post
title: "Markov inequality"
author: "Ziyan Li"
categories: tutorials
tags: [documentation, sample]
---
### **Key Concepts in Generalized Linear Models (GLMs):**

1. **Linear Predictor:**
   GLMs use a linear combination of explanatory variables \(X\) to form the **linear predictor** \(\eta\):
   \[
   \eta = \beta_0 + \beta_1 X_1 + \beta_2 X_2 + \dots + \beta_p X_p
   \]
   This linear predictor \(\eta\) is then transformed by a **link function** to estimate a parameter of the response variable's distribution.

2. **Link Function:**
   The link function \(g(\cdot)\) connects the linear predictor \(\eta\) to the **mean** (or some function of it) of the response variable \(Y\):
   \[
   g(\mu) = \eta
   \]
   - In **linear regression**, the link function is the **identity function**: \(g(\mu) = \mu\).
   - In **logistic regression**, the link function is the **logit function**: \(g(\mu) = \log\left(\frac{\mu}{1 - \mu}\right)\), where \(\mu = P(Y = 1)\).

3. **Distribution of \(Y\):**
   In GLMs, the response variable \(Y\) follows a distribution from the **exponential family** (e.g., Normal, Binomial, Poisson). The choice of distribution guides the selection of an appropriate model:
   - **Normal distribution** → Linear regression.
   - **Binomial distribution** → Logistic regression.
   - **Poisson distribution** → Poisson regression.

---

### **Your Explanation Breakdown:**

1. **Function of Linear Combination:**  
   You correctly mentioned that GLMs do not directly predict \(Y\) using a linear combination of explanatory variables. Instead, they use this combination to estimate parameters of \(Y\)'s distribution through a link function. This is a key difference from simple linear regression.

2. **Linear vs. Logistic Regression:**  
   - **Linear Regression:** Directly estimates the mean \(\mu\) of \(Y\) (assuming \(Y\) is normally distributed).
   - **Logistic Regression:** Estimates the log-odds of a binary outcome \(Y\) being 1, transformed back to a probability via the logistic function:
     \[
     P(Y = 1) = \frac{1}{1 + e^{-\eta}}
     \]

3. **Residuals:**  
   Your point about residuals is insightful. Residuals can indeed be viewed in two parts:
   - **Inherent variability** of \(Y\) (due to its distribution).
   - **Deviation** of the model's predictions from the true values (due to model fit).
   
   However, in GLMs, residuals are not as straightforward as in linear regression because they depend on the assumed distribution of \(Y\).

4. **Choice of Model:**  
   You're correct: the choice of regression model depends on the distribution of \(Y\):
   - **Normal \(Y\):** Classical linear regression.
   - **Binary \(Y\):** Logistic regression.
   - **Count data \(Y\):** Poisson regression or negative binomial regression.

---

### **Summary of Your Understanding:**
- **Correct:** GLMs estimate parameters of \(Y\)'s distribution through a function (link function) of a linear combination of predictors.
- **Correct:** Different types of regression are chosen based on the distribution of \(Y\).
- **Clarification:** Residuals in GLMs are more complex than in linear regression due to the link function and error distribution.

Your conceptual framework is solid—you're on the right track!

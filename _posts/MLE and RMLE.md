---
layout: post
title: "MLE and RMLE"
author: "Ziyan Li"
categories: journal
tags: [documentation, sample]
---
In this blog, we attempt to explain the difference between maximum likelihood function(**MLE**) and restricted maximum likelihood function(**RMLE**).
### **1. Maximum Likelihood (ML)**
ML estimates the model parameters (both fixed and random effects) by finding the values that **maximize the likelihood function**. This function represents the probability of observing the given data, given the model parameters.

#### **Key Characteristics:**
- **Bias in Variance Estimation:**  
  ML tends to **underestimate the variance** components in mixed models, especially when the sample size is small. This happens because ML doesn't account for the **loss of degrees of freedom** due to estimating the fixed effects.

- **Model Comparison:**  
  ML allows comparing the **goodness-of-fit** between **nested models** (where one model is a subset of another) using the **likelihood ratio test** (LRT). This is useful for hypothesis testing when deciding whether to include or exclude certain fixed effects.

---

### **2. Restricted Maximum Likelihood (REML)**
REML modifies the likelihood function to account for the estimation of fixed effects. It estimates the variance components by maximizing the likelihood of the residuals after removing the fixed effects. This method is particularly useful for estimating random effects.

#### **Key Characteristics:**
- **Unbiased Variance Estimates:**  
  Unlike ML, REML produces **unbiased estimates of variance components** by adjusting for the degrees of freedom used in estimating the fixed effects. This is why it is often the **default in R** and other statistical software for mixed models.

- **Model Comparison Limitation:**  
  REML can only compare models with **the same fixed effects**. This is because the likelihood functions in REML depend on the fixed effects structure, making comparisons invalid if the fixed effects differ between models.

---

I highly recommend to reading this website to get more intution of MLE and RMLE.(https://stats.stackexchange.com/questions/48671/what-is-restricted-maximum-likelihood-and-when-should-it-be-used)

The **likelihood ratio test (LRT)** in logistic regression follows a **chi-squared distribution** due to the properties of **maximum likelihood estimation (MLE)** and the **asymptotic distribution** of the likelihood function. Let's break down why this happens:

---

### **1. Likelihood Ratio Test (LRT) Overview:**

The LRT is a statistical method for comparing two **nested models**:
- A **full model** (more complex) and a **reduced model** (simpler).
- The LRT compares their **log-likelihoods** to determine if the additional parameters in the full model significantly improve the fit.

#### **Test Statistic:**
The LRT statistic is:
\[
\Lambda = -2 \left( \log L(\text{reduced model}) - \log L(\text{full model}) \right)
\]
- \( L \) denotes the likelihood function.
- **Interpretation:** The difference between the log-likelihoods quantifies how much better the full model explains the data compared to the reduced model.

---

### **2. Why Does the LRT Follow a Chi-squared Distribution?**

#### **Asymptotic Properties of MLE:**
- Under some regularity conditions, the **maximum likelihood estimator (MLE)** has desirable asymptotic properties. Specifically, it is **asymptotically normal**:
  - As the sample size \( n \) increases, the distribution of the MLEs of the parameters approaches a **multivariate normal distribution**.
  
#### **Wilks' Theorem:**
- **Wilks' Theorem** states that under the **null hypothesis** (that the reduced model is correct), the LRT statistic \( \Lambda \) asymptotically follows a **chi-squared distribution**:
  \[
  \Lambda \sim \chi^2_k
  \]
  where \( k \) is the **difference in the number of parameters** between the full and reduced models (i.e., the degrees of freedom).

#### **Key Reasoning:**
- The difference in log-likelihoods is related to the sum of squared differences between the estimated parameters under the two models.
- This sum of squared differences, scaled by the variance-covariance matrix, follows a chi-squared distribution because it reflects the squared deviations of normally distributed parameter estimates.

---

### **3. Practical Implication for Logistic Regression:**
- In **logistic regression**, we deal with probabilities and a binary response variable modeled using the Bernoulli distribution.
- When comparing models, the log-likelihoods reflect how well each model predicts these probabilities.
- The LRT evaluates if adding more predictors (increasing model complexity) significantly improves the model fit beyond what would be expected by chance.

#### **Degrees of Freedom:**
- The degrees of freedom \( k \) in the chi-squared distribution correspond to the number of additional parameters in the full model compared to the reduced model.

---

### **Example Calculation:**
1. **Fit two models**:
   - A reduced model (fewer predictors) and a full model (more predictors).
2. **Calculate the LRT statistic**:
   \[
   \Lambda = -2 \left( \log L_{\text{reduced}} - \log L_{\text{full}} \right)
   \]
3. **Compare \( \Lambda \)** to the critical value of the **chi-squared distribution** with \( k \) degrees of freedom.
   - If \( \Lambda \) exceeds this critical value, reject the null hypothesis.

---
This statement highlights the key differences between **linear regression** and **logistic regression** regarding statistical tests like the **F-test** and why it doesn't apply directly to logistic regression. Let's break this down:

---

### **1. Linear Regression and F-tests:**

In **linear regression**, we assume:
- The response variable \( Y \) is continuous.
- The relationship between the predictors and \( Y \) is linear:
  \[
  Y_i = \beta_0 + \beta_1 X_i + \epsilon_i
  \]
  where \( \epsilon_i \) are normally distributed errors.

#### **F-test in Linear Regression:**
- The **F-test** compares two nested models (e.g., a larger model vs. a smaller one).
- It uses the ratio of the explained variance to the unexplained variance.
- The test statistic is:
  \[
  F = \frac{(\text{Explained Variance}) / p}{(\text{Unexplained Variance}) / (n - p - 1)}
  \]
  where \(p\) is the number of predictors and \(n\) is the sample size.

- **Why it works:** The normal errors allow us to use properties of the **likelihood ratio test (LRT)**, and under the normality assumption, the LRT follows an **F-distribution**.

---

### **2. Logistic Regression and Its Challenges:**

In **logistic regression**, we model a **binary outcome** \( Y \) using the **log-odds (logit) function**:
\[
\log\left(\frac{P(Y=1)}{P(Y=0)}\right) = \beta_0 + \beta_1 X_i
\]

#### **Key Differences:**
- **Bernoulli Distribution:** The response variable \( Y \) is binary (0 or 1), not continuous.
- **Likelihood:** The likelihood is based on the **Bernoulli distribution**, not normal errors.
- **No Additive Errors:** There is no error term \( \epsilon \) in the logistic regression model, unlike in linear regression. Instead, the variability comes from the Bernoulli process itself.

#### **Log-odds (Logit Space):**
- In the **log-odds space**, the relationship is non-linear, and there's no straightforward way to express the residuals as in linear regression.
- We cannot define an additive error term because the output is a probability (bounded between 0 and 1), not a continuous value extending over all real numbers.

---

### **3. Why F-tests Don't Work for Logistic Regression:**

- **F-test Assumption:** The F-test relies on the **normal distribution** of errors and linearity in the response. These assumptions don't hold in logistic regression.
- **Likelihood Ratio Test (LRT):** For logistic regression, we instead use the **likelihood ratio test** directly to compare nested models. The test statistic follows a **chi-squared distribution**, not an F-distribution.
- **No Direct Residual Analysis:** Since logistic regression deals with probabilities and log-odds, there isn't a direct analog of residual variance as in linear regression.

---


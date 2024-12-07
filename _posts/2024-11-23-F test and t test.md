---
layout: post
title: "F test and t test"
author: "Ziyan Li"
categories: journal
tags: [documentation, sample]
---
In this blog, we discuss how the **F-test** related to **t-test** and **likelihood ratio test** in regression analysis.

We first introduce F-test, t-test, and likelihood ratio test.

** F-test**:
- The **F-test** is a statistical test commonly used to compare two nested models in terms of their goodness-of-fit. It tests whether the additional parameters in a more complex model significantly improve the fit compared to a simpler (nested) model.
- The test statistic is based on the ratio of two variances (hence the name "F-test"):
  
$$
F = \frac{(\text{RSS}_{\text{reduced}} - \text{RSS}_{\text{full}}) / p}{\text{RSS}_{\text{full}} / (n - k)}
$$

  where:
  - $\text{RSS}_{\text{reduced}}$: Residual sum of squares for the simpler model,
  - $\text{RSS}_{\text{full}}$: Residual sum of squares for the complex model,
  - $p$: Number of additional parameters in the full model,
  - $n$: Number of observations,
  - $k$: Number of parameters in the full model.

- The F-test statistic follows an **F-distribution** under the null hypothesis, provided that the assumptions of the model (e.g., normality, homoscedasticity) hold.


**Likelihood Ratio Test (LRT)**:
- The **Likelihood Ratio Test** is a general test used to compare two nested models by examining the likelihoods (how well the models explain the data).
- The test statistic is based on the ratio of the likelihoods of the reduced and full models:
  
$$
\Lambda = -2 \log \left( \frac{\mathcal{L}_{\text{reduced}}}{\mathcal{L}_{\text{full}}} \right)
$$

where $\mathcal{L}$ is the likelihood function.
- Under the null hypothesis (assuming the reduced model is correct), the LRT statistic asymptotically follows a **chi-square distribution** with degrees of freedom equal to the difference in the number of parameters between the two models.



Next, we discuss the relation between F-test and t-test.

## F-test and t-test
### **1. Orthogonality and Collinearity of Columns in $X$**

- **Orthogonal columns**: This means that the columns of $X$ are uncorrelated. For example, if $X$ has columns $X_1, X_2, \ldots, X_p$, they satisfy $X_i^T X_j = 0$ for all $i \neq j$. This simplifies the calculations in regression, as each predictor's contribution can be assessed independently.
- **Highly correlated columns**: This indicates **multicollinearity**, where columns of $X$ are not independent. It complicates regression by making it harder to isolate the effect of each predictor, leading to large variances in the coefficient estimates.


### **2. t-Tests in Regression**

t-tests is designed to test whether the estimated $\beta$ is zero or not one by one. The test statistic is $ t_j = \frac{\hat{\beta}_j}{\text{SE}(\hat{\beta}_j)} $. 

- **Impact of Orthogonality**: 
  - If columns of $X$ are orthogonal, the variance-covariance matrix of $\hat{\beta}$ is diagonal, and each $\hat{\beta}_j$ depends only on $X_j$.
  - **Result**: The t-statistics remain unaffected by other predictors. Hence, the p-values are stable.
- **Impact of Collinearity**:
  - High correlation inflates the standard error $\text{SE}(\hat{\beta}_j)$ because the variance of $\hat{\beta}_j$ depends on the inverse of $X^T X$. This can reduce the t-statistic, even if $\hat{\beta}_j$ itself is significant.
  

### **3. F-Tests in Regression**

F-tests assess the overall significance of the regression model (global null hypothesis $H_0: \beta_1 = \beta_2 = \ldots = \beta_p = 0$). The test Statistic is $ F = \frac{\text{Explained Variance} / p}{\text{Residual Variance} / (n - p - 1)} $.

- **Impact of Orthogonality**:
  - If columns are orthogonal, the explained variance is neatly partitioned among the predictors, and the F-statistic captures the overall contribution of all predictors.
  - **Result**: The F-statistic remains relatively stable and interpretable.
- **Impact of Collinearity**:
  - While collinearity inflates the standard errors of individual coefficients (affecting t-tests), it generally has a smaller effect on the overall F-statistic.
  - **Why?** The F-test considers the total variance explained by the model, aggregating information across all predictors. Collinearity impacts individual coefficients but may not drastically change the overall fit of the model.
 
### **Intuition**

- **t-tests** focus on individual predictors and their associated variances, so multicollinearity in $X^T X$ directly affects their distribution.
- **F-tests** aggregate the effect of all predictors. The F-statistic involves a ratio of variances (explained vs. residual), which can "average out" collinearity effects because it considers the total model performance, not just individual coefficients.

## F-test and Likelihood ratio test
The **F-test** and the **Likelihood Ratio Test (LRT)** are related but not exactly the same. 

1. **In Linear Regression Models** (under normality assumptions):  
   - The **F-test** can be shown to be equivalent to the **Likelihood Ratio Test**.
   - This is because the likelihood function of the normal distribution depends on the sum of squared residuals (RSS), which appears in the F-statistic formula.  
   Thus, the two tests are mathematically equivalent for comparing nested models in a linear regression context.

2. **In Generalized Linear Models (GLMs)**:  
   - The F-test is not always appropriate because the distribution of residuals may not be normal.  
   - The LRT is more general and can be applied to a broader range of models (e.g., Poisson regression, logistic regression).  
   - In GLMs, the LRT statistic follows a chi-square distribution, not an F-distribution.

3. **Small Sample Sizes**:  
   - The F-test and LRT can diverge slightly when sample sizes are small because the F-test assumes exact finite-sample distributions, whereas the LRT assumes asymptotic (large-sample) distributions.

---

### **Summary**:
- The **F-test** is a special case of the **Likelihood Ratio Test** when applied to **linear regression models** under normality assumptions.
- In more general settings (e.g., GLMs), the LRT is preferred because it does not rely on the normality assumption and uses the likelihood function directly.
- For **linear models**, both tests will yield equivalent results in large samples.


---
layout: post
title: "F test and t test"
author: "Ziyan Li"
categories: journal
tags: [documentation, sample]
---
In the following, we discuss how the collinearity affect the t-tests and F-tests.

### **1. Orthogonality and Collinearity of Columns in \(X\)**

- **Orthogonal columns**: This means that the columns of \(X\) are uncorrelated. For example, if \(X\) has columns \(X_1, X_2, \ldots, X_p\), they satisfy \(X_i^T X_j = 0\) for all \(i \neq j\). This simplifies the calculations in regression, as each predictor's contribution can be assessed independently.
- **Highly correlated columns**: This indicates **multicollinearity**, where columns of \(X\) are not independent. It complicates regression by making it harder to isolate the effect of each predictor, leading to large variances in the coefficient estimates.


### **2. t-Tests in Regression**

t-tests is designed to test whether the estimated $\beta$ is zero or not one by one. The test statistic is \( t_j = \frac{\hat{\beta}_j}{\text{SE}(\hat{\beta}_j)} \). 

- **Impact of Orthogonality**: 
  - If columns of \(X\) are orthogonal, the variance-covariance matrix of \(\hat{\beta}\) is diagonal, and each \(\hat{\beta}_j\) depends only on \(X_j\).
  - **Result**: The t-statistics remain unaffected by other predictors. Hence, the p-values are stable.
- **Impact of Collinearity**:
  - High correlation inflates the standard error \(\text{SE}(\hat{\beta}_j)\) because the variance of \(\hat{\beta}_j\) depends on the inverse of \(X^T X\). This can reduce the t-statistic, even if \(\hat{\beta}_j\) itself is significant.
  

---

### **3. F-Tests in Regression**

F-tests assess the overall significance of the regression model (global null hypothesis \(H_0: \beta_1 = \beta_2 = \ldots = \beta_p = 0\)). The test Statistic is \( F = \frac{\text{Explained Variance} / p}{\text{Residual Variance} / (n - p - 1)} \).

- **Impact of Orthogonality**:
  - If columns are orthogonal, the explained variance is neatly partitioned among the predictors, and the F-statistic captures the overall contribution of all predictors.
  - **Result**: The F-statistic remains relatively stable and interpretable.
- **Impact of Collinearity**:
  - While collinearity inflates the standard errors of individual coefficients (affecting t-tests), it generally has a smaller effect on the overall F-statistic.
  - **Why?** The F-test considers the total variance explained by the model, aggregating information across all predictors. Collinearity impacts individual coefficients but may not drastically change the overall fit of the model.
 
### **Intuition**

- **t-tests** focus on individual predictors and their associated variances, so multicollinearity in \(X^T X\) directly affects their distribution.
- **F-tests** aggregate the effect of all predictors. The F-statistic involves a ratio of variances (explained vs. residual), which can "average out" collinearity effects because it considers the total model performance, not just individual coefficients.


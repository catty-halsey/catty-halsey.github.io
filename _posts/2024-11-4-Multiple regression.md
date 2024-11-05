---
layout: post
title: "Multiple regression"
author: "Ziyan Li"
categories: journal
tags: [documentation, sample]
---

## Table of Contents
- [Estimated Beta in Simple and Multiple Regression](#estimated-hatbeta-in-simple-and-multiple-regression)
- [Uniqueness of Estimated Beta in Multiple Linear Regression](#Uniqueness-of-Estimatied-Beta-in-Multiple-Linear-Regression)
- [Accuracy](#Accuracy-of-estimation)


---

## Estimated $\hat{\beta}$ in simple and multiple regression
First, we need to emphaize that the coefficient using regression through simple linear regression and multiple regression are different in general. More specific, using our observed data $X$ and $Y$, if we have $y=X^{(j)}\bar{\beta_j}$ from simple regression and $y=X\hat{\beta}$ from multiple, where $X^{(j)}$ is the j-th column of $X$, then $\bar{\beta_j}$ and $\hat{\beta}(j)$ are not equal in general. In particular, when predictors are orthogonal, it holds that:

- $x_{\cdot,j}^T x_{\cdot,k} = 0$ for all $j \neq k$
- Consequently, $X^T X = \text{diag} \left( \sum_{i=1}^n x_{i,1}^2, \dots, \sum_{i=1}^n x_{i,p}^2 \right)$

Given these properties, the calculation of $\hat{\beta}$ simplifies. Specifically:

$$
\hat{\beta}_j = \left( X^T X \right)^{-1} X^T Y_j = \frac{\sum_{i=1}^n x_{i,j} y_i}{\sum_{i=1}^n x_{i,j}^2} = \frac{\hat{\sigma}_{x_j,y}}{\hat{\sigma}_{x_j}^2}
$$

This results in the same outcome as performing separate simple regressions for each predictor $x_j$ on the response $Y$. 

Then, we back to the general cases. When the coefficients from different regression are different, we are interested in which one is more reliable and which can be used to intepret as the total cause effect of $X_j$ on Y, for each $j \in {1,2,\cdots,p}$. The concept of **valid adjustment** solves this problem. 

Consider a linear, zero-mean Gaussian Structural Causal Model (SCM), where all assignments are linear, and the noise terms are normally distributed with zero mean. The vector $(Y, X, Z)$ has a (zero mean) Gaussian distribution with 

$$
\mathbb{E}[Y \mid X = x, Z = z] = ax + b^z
$$

Assume now that $Z$ is a valid adjustment set for the causal effect from $X$ to $Y$, then we have 
   
$$
\frac{\partial}{\partial x} \mathbb{E}_{C; \, \text{do}(X := x)}[Y] = a.
$$


## Uniqueness of Estimatied Beta in Multiple Linear Regression

When estimating the parameter vector $\beta$ in multiple linear regression, the dimensions of the matrices $X$ and $Y$ play a crucial role. Before discussing the behavior of the estimated coefficient vector $\hat{\beta}$, we recall the **Rank-Nullity Theorem** from linear algebra. This theorem states that for any linear transformation $X: \mathbb{R}^p \rightarrow \mathbb{R}^n$, the sum of the dimension of the image of $X$ (known as the rank of $X$) and the dimension of the kernel of $X$ (known as the nullity of $X$) equals the number of columns $p$ of the matrix $X$. This relationship can be expressed mathematically as:

$$
\text{rank}(X) + \text{nullity}(X) = p.
$$

#### Remark

- The expression $Xv$ represents the interaction between the column space of $X$ and the vector $v$, essentially reflecting a linear combination of the columns of $X$.
- When the rank of $X$ satisfies $\text{rank}(X) = \dim(\text{col}(X)) < p$, it follows that $\dim(\text{ker}(X)) > 0$. Consequently, the vector $v$ is no longer unique, as we can have $Xv = Y$ and $Xv' = Y$ for different vectors $v$ and $v'$, with the condition $v - v' \in \text{ker}(X)$.

Next, we can apply this theorem within the context of multiple linear regression. Assume the model is expressed as:

$$
Y = X\beta + \epsilon,
$$

where $Y$ is an $n \times 1$ matrix, $X$ is an $n \times p$ matrix, and $\beta$ is a $p \times 1$ matrix. Using Ordinary Least Squares (OLS) to estimate $\beta$, we obtain:

$$
\hat{Y} = X\hat{\beta}.
$$

We will now analyze the conditions under which $\hat{\beta}$ may not be unique. Our focus will be on the nullity of $X$. Notably, the rank of $X$ is constrained to be less than or equal to the minimum of the number of columns and rows, that is:

$$
\text{rank}(X) \leq \min(p, n).
$$

Thus, the interplay between the number of columns and rows in $X$ significantly influences the uniqueness of $\hat{\beta}$.

- In the case where $n \geq p$, if $X$ has full rank $p$, then the estimated coefficient vector $\hat{\beta}$ has a unique solution if and only if $\text{rank}(X) = p$, which implies that $\text{nullity}(X) = 0$.
- Conversely, when $n < p$, it follows that $\text{rank}(X) \leq n < p$, resulting in $\text{nullity}(X) > 0$. Therefore, in this scenario, $\hat{\beta}$ can never have a unique solution.

## Accuracy of estimation 

In practice, we have two assumptions about the error $\epsilon$. 

- Assumption 1: $\epsilon \sim N(0,\sigma^2 \text{Id)}$.
- Assumption 2: Gauss-Markov condition.i.e, $\cov(\epsilon)=\sigma^2 \text{Id}$.
Remark: The Gauss-Markov condition assume the $\epsilon_i \perp \epsilon_j$ for $i \neq j$ and does not specify the specific distribution the error follows, which is a general scenario.

Since the Gauss-Markov condition include the normality assumption, we discuss all the behaviour of our estimator under the Markov-condition. 

### Estimated Beta
- Unbaised estimator $(X^TX)^{-1}X^TY$: $E(\hat{\beta}) = \beta$ 
- $\text{Cov}(\hat{\beta}) = \sigma^2 (X^T X)^{-1}$.

Then, we are interested in how small the variance of $\hat{\beta}$ compared to other estimator, then we have two results.
- Under the Markov-condition, $\hat{\beta}$ has the smallest vairance among all linear unbiased estimator.
- Under normality error, $\hat{\beta}$ has the smallest vairance among all unbiased estimator (**UMVU**).

Remark:
- Both assumption based on rank of X has the full rank $p$ such $p<n$. When this condition violate, even the asssumption holds, j-th column of $X$ can be linear combination of other columns, which will explode the vairance of $\hat{\beta}$ due to the extremely increases of **VIF**.
- Under non-normal errors, there exists lots of estimators which have smaller variance than OLS. In particular, when error follow some distributions with heavy tails, the OLS estimator can have high variance due to its sensitivity to large deviations. The LAD estimator (which minimizes absolute deviations) is more robust to these large residuals, resulting in a smaller variance for the estimate of $\beta$.

For instance, suppose $\epsilon$ follows a Laplace distribution (also known as the double-exponential distribution), which has heavier tails than a normal distribution.

The Laplace distribution has the form:

$$
f(\epsilon) = \frac{1}{2b} \exp\left(-\frac{|\epsilon|}{b}\right),
$$

where $b$ is the scale parameter. In this case, the Maximum Likelihood Estimator (MLE) for $\beta$ corresponds to minimizing the sum of absolute residuals rather than the sum of squared residuals, which is done in Least Absolute Deviations (LAD) regression. This is because the Laplace distribution maximizes the likelihood when we minimize the absolute differences, rather than the squared differences. Here is a visualization from R, we set b=1,sample size=100, replications=10000. The red region is the distribution of MLE of $\beta$ and the blue region is the distribution of OLS of $\beta$, and the dashed line is the true beta 2. We can observed that the MLE estimator are more dense near the mean and so has smaller variance. Additionally, the mean of MLE is also closer to the true beta.

In the next, we choose MLE estimator to compare with OLS estimator when the error follows heavy tails distribution.

#### OLS vs. MLE

1. **Objective Function**:
   - **OLS (Ordinary Least Squares)**: Minimizes the Residual Sum of Squares (RSS), which is sensitive to extreme values because it squares the residuals:

$$
\text{RSS} = \sum (Y_i - \hat{Y}_i)^2.
$$

When there are large residuals (outliers), squaring these values disproportionately increases the RSS, leading to higher variance in the estimates of \(\beta\).

   - **MLE (Maximum Likelihood Estimation)**: Focuses on maximizing the likelihood function, which is often transformed into minimizing the negative log-likelihood. In the case of non-normal errors (like those following a t-distribution), the likelihood function decays more slowly for extreme values compared to the normal distribution:

$$
L(\beta) = \prod f(Y_i | X_i, \beta),
$$

where \(f\) is the probability density function for the error distribution.

2. **Sensitivity to Outliers**:
   - **OLS Sensitivity**: Because OLS uses squared errors, it is highly sensitive to outliers. A few extreme values can skew the estimates significantly, increasing the variance of the parameter estimates.

   - **MLE Robustness**: The log transformation in MLE effectively "down-weights" the influence of extreme values. This property helps MLE to maintain more stable estimates even in the presence of outliers or heavy tails, leading to lower variance for the estimated parameters.

3. **Heavier Tails**: 
   - When the error distribution has heavier tails (like the t-distribution or Laplace distribution), extreme residuals become more probable. OLS can yield high variance in such scenarios because of its squaring effect on errors, while MLE, by virtue of its likelihood function, mitigates this sensitivity through its structure.


### Estimated Y
- **unbiased predictions** (in the sense that $\mathbb{E}[\hat{Y}] = X \beta$ = \mathbb{E}[Y]), the predicted value $\hat{Y}$ is **not generally an unbiased estimator of the actual observed value $Y$**. While $\hat{Y}$ gives an unbiased prediction for the mean outcome, it is not an unbiased estimator of each observed 
$𝑌$ due to the inherent variability from the error term.
- $\text{Cov}(\hat{Y}) = \sigma^2 P$, where $P$ is projection matrix as $X(X^TX)^-1X^T$.

### Estimated error 
- Unbiased estimator ($\hat{\epsilon}=Y-\hat{Y}$): $\mathbb{E}[\hat{\epsilon}]=\mathbb{E}[\epsilon]=0$.
- $\text{Cov}(\hat{\epsilon}) = \sigma^2 M$, where $M$ is residual maker matrix as $1-X(X^TX)^{-1}X^T$.









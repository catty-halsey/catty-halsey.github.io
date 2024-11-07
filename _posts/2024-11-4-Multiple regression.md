---
layout: post
title: "Multiple regression"
author: "Ziyan Li"
categories: tutorials
tags: [documentation, sample]
---

## Table of Contents
- [Estimated Beta in Simple and Multiple Regression](#estimated-hatbeta-in-simple-and-multiple-regression)
- [Uniqueness of Estimated Beta in Multiple Linear Regression](#Uniqueness-of-Estimatied-Beta-in-Multiple-Linear-Regression)
- [Accuracy](#Accuracy-of-estimation)
  - [Estimated Beta](#Estimated-Beta)
    - [OLS vs. MLE](#OLS-vs.-MLE)
    - [Distribution of estimated beta](#Distribution-of-estimated-beta)
    - [Test of estimated beta](#Test-of-estimated-beta)
  - [Estimated Y](#Estimated-Y)
  - [Estimated error](#Estimated-error)
  


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
- The variance of $\hat{\beta_j}$, the $j$-th coefficient estimator in a multiple regression, can be expressed in terms of the variance inflation factor (VIF), the error variance $\sigma^2$, and the variance of the predictor $X_j$. Here’s the relationship:

$$
\text{Var}(\hat{\beta_j}) = \sigma^2 \cdot \frac{VIF_j}{\text{Var}(X_j)}
$$

where:

- $\sigma^2$ is the error variance.
- $\text{Var}(X_j)$ is the variance of the predictor $X_j$.
- $VIF_j$ (Variance Inflation Factor) is a measure of how much the variance of $\hat{\beta_j}$ is inflated due to the correlation among predictors. It’s defined as:
  
$$
VIF_j = \frac{1}{1 - R_j^2}
$$

  where $R_j^2$ is the $R^2$ value from regressing $X_j$ on all other predictors in the model.

This formulation reflects how multicollinearity (captured by the VIF) affects the precision of $\hat{\beta_j}$. A high $VIF_j$ implies greater variance in $\hat{\beta_j}$, indicating instability in the estimate due to correlations among predictors. This result will play an important result in the hypotheisis testing of $\hat{\beta}$.

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

When there are large residuals (outliers), squaring these values disproportionately increases the RSS, leading to higher variance in the estimates of $\beta$.

   - **MLE (Maximum Likelihood Estimation)**: Focuses on maximizing the likelihood function, which is often transformed into minimizing the negative log-likelihood. In the case of non-normal errors (like those following a t-distribution), the likelihood function decays more slowly for extreme values compared to the normal distribution:

$$
L(\beta) = \prod f(Y_i | X_i, \beta),
$$

where $f$ is the probability density function for the error distribution.

2. **Sensitivity to Outliers**:
   - **OLS Sensitivity**: Because OLS uses squared errors, it is highly sensitive to outliers. A few extreme values can skew the estimates significantly, increasing the variance of the parameter estimates.

   - **MLE Robustness**: The log transformation in MLE effectively "down-weights" the influence of extreme values. This property helps MLE to maintain more stable estimates even in the presence of outliers or heavy tails, leading to lower variance for the estimated parameters.

3. **Heavier Tails**: 
   - When the error distribution has heavier tails (like the t-distribution or Laplace distribution), extreme residuals become more probable. OLS can yield high variance in such scenarios because of its squaring effect on errors, while MLE, by virtue of its likelihood function, mitigates this sensitivity through its structure.

#### Distribution of estimated beta


#### Test of estimated beta 
We are interested in whether the coefficient from the linear regression represents the true effect of $X_j$ on $Y$. To investigate this, we introduce a hypothesis test for $\hat{\beta}$. The null hypothesis: $H_0: \beta_j =0$ agianst the alternative hypothesis $\beta_j \neq 0$. 

Assume the errors follow a normal distribution with mean zero and variance $\sigma^2 \text{Id}$, so that 

$$
\hat{\beta} \sim N(\beta, \sigma^2 (X^TX)^{-1}).
$$

We then have

$$
\hat{\sigma} = \frac{\sum_{i=1}^n \epsilon_i^2}{n - p}
$$

and

$$
\frac{\sum_{i=1}^n \hat{\epsilon_i}^2}{\sigma^2} \sim \chi^2_{n-p},
$$

where $\epsilon \sim N(0, \sigma^2M)$ and $M$ is residual maker matrix, denoted as $1-X(X^TX)^{-1}X$. 

This allows us to construct the test statistic:

$$
\frac{\hat{\beta_j} - \beta_j}{\hat{\sigma} \sqrt{(X^TX_{jj})^{-1}}} \sim t_{n - p}.
$$

In this construction, we use the property $\hat{\beta} \perp \hat{Y}$ and $\frac{W}{\sqrt{V/n}} \sim t_n$ if $W \perp V$ with $W \sim N(0,1)$ and $V \sim \chi^2_n$. Then, if we get the p-value is less then significant level, then we reject the null hypotheis.i.e, $\beta_j \neq 0$. 

Recall how **VIF** and variance of $X_j$ affect the variance of $\hat{\beta_j}$, $(X^TX_{jj})^{-1}$ can be rewrite as $\frac{VIF_j}{\text{Var}(X_j)}$. Under high correlation among $X_j$, $VIF_j$ and $(X^TX_{jj})^{-1}$ explode and therefore the t test statistics extremely decrease, which is closer to zero and hard to be rejected. However, we we drop one or more explantory variable, the significance might change, because we reduce the colinearity and decrease the **VIF**.The similar logic also applies to the variance within the $X_j$. And this problem can be solved by **F-test**, we will introduce later.



### Estimated Y
- **unbiased predictions** (in the sense that $\mathbb{E}[\hat{Y}] = X \beta$ = \mathbb{E}[Y]), the predicted value $\hat{Y}$ is **not generally an unbiased estimator of the actual observed value $Y$**. While $\hat{Y}$ gives an unbiased prediction for the mean outcome, it is not an unbiased estimator of each observed 
$𝑌$ due to the inherent variability from the error term.
- $\text{Cov}(\hat{Y}) = \sigma^2 P$, where $P$ is projection matrix as $X(X^TX)^-1X^T$.

Using a similar approach to the construction of the test statistic for $\hat{\beta}$, we can construct a test statistic for $\hat{Y}$. Instead of testing whether $\hat{Y}$ equals a specific value, we are primarily interested in deriving a **confidence interval** for $Y$, which provides an approximation for the expected value of $Y$. Additionally, we aim to construct a **prediction interval** for $Y$, which captures the range where a new observation $Y$ is likely to fall.

We begin by constructing the test statistic under the null hypothesis $\mu = \mu_i$, where $\hat{Y} = PY$ and $\hat{Y_j} \sim N(\mu_j, \sigma^2 P_{jj})$. The test statistic is then given by:

$$
\frac{\hat{Y_j} - Y_j}{\hat{\sigma} \sqrt{P_{jj}}} \sim t_{n - p}.
$$

The corresponding $(1 - \alpha)$-level confidence interval for $Y$ is: $\hat{Y} \pm t_{\alpha/2; n - p} \cdot \hat{\sigma_1}$, where $\hat{\sigma_1} = \hat{\sigma} \sqrt{P_{jj}}$.

For the prediction interval, we consider a new observation $Y_0 = X_0^T \beta + \epsilon$, where $X_0$ is a new predictor vector and $\epsilon$ has mean zero and variance $\sigma^2 \text{Id}$. The variance of $\hat{Y}_0 - Y_0$ becomes $\sigma^2 + X_0^T (X^TX)^{-1} X_0$, which is larger than $\text{Var}(\hat{Y} - Y)$. Consequently, the prediction interval for $Y$ is wider than the confidence interval at the same confidence level, reflecting the additional variance introduced by the new observation $X_0$.

Thus, the prediction interval is: $\hat{Y} \pm t_{\alpha/2; n - p} \cdot \hat{\sigma_2}$, where $\hat{\sigma_2} = \hat{\sigma} \sqrt{1 +  X_0^T (X^TX)^{-1} X_0}$.

The additional variance in the prediction interval arises because we are using the estimated $\beta$ from the regression model, which was derived from the original data $X$ and $Y$. The inclusion of the new data $X_0$ introduces additional variability, hence the wider interval.

### Estimated error 
- Unbiased estimator ($\hat{\epsilon}=Y-\hat{Y}$): $\mathbb{E}[\hat{\epsilon}]=\mathbb{E}[\epsilon]=0$.
- $\text{Cov}(\hat{\epsilon}) = \sigma^2 M$, where $M$ is residual maker matrix as $1-X(X^TX)^{-1}X^T$.
- $\hat{\epsilon_i} \sim N(0,\sigma^2M)
-
$$
\frac{\sum_{i=1}^n \hat{\epsilon_i}^2}{\sigma^2} \sim \chi^2_{n-p}
$$

Remark: In general, when we have a random vector $X$ following the normal distribution, we use the inverse of covariance matrix of X standardized $X$ and therefore get $(X-\mu)^T\Sigma^{-1}(X-\mu) \sim \chi^2_n$. However, the $M$ is not invertible in general. Instead, we use a different way to standardize our variable by the following way. 

Assume $e \sim N(0, M)$, where $M$ is an idempotent matrix of rank $r$. Note that all idempotent matrix are diagonalizable, you can look the proof [here](https://math.stackexchange.com/questions/600745/are-idempotent-matrices-always-diagonalizable). Then $e^T M e$ 
has a central chi-square distribution with $r$ degrees of freedom. This follows 
from the fact that there exists an orthogonal matrix $A$ such that $M = 
A D_A A^T$, where $D_A = \text{diag}(1, \dots , 1,0, \dots ,0)$ with the number of ones being 
equal to the rank of the matrix $M$. Thus $e^T M e = e^T A D_A A^T e = z^T D_A z = 
\sum_{i=1}^{r} z_i^2$, where $z = (z_1, \dots, z_n)^T = f^T e \sim N(0, A M A^T) = N(0, D_A)$. In our case, we have $e=\hat{\epsilon}/\sigma^2$.










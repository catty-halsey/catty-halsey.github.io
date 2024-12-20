---
layout: post
title: "Why the distribution of error matters?"
author: "Ziyan Li"
categories: journal
tags: [documentation, sample]
---
## Background
In (linear/non-linear) regression, we can express the relationship between the response variable $Y$ and predictor (or explanatory) variables $X$ in the form:

$$
Y = f(X) + \epsilon,
$$

where:
- $\epsilon$ is the error term, which follows a certain distribution (often assumed to be normal for classical linear regression), and
- $X$ is the predictor variable, while $Y$ is the response variable.

In the case of linear regression, where the relationship between $Y$ and $X$ is assumed to be linear, we have $f(X) = X\beta$, where $\beta$ is a vector of coefficients.

Although both $Y$ and $\epsilon$ are random variables, the distribution of $Y$ largely depends on the distribution of $\epsilon$. Similarly, the estimation of $\beta$ (e.g., via least squares) and predictions of $Y$ are sensitive to the properties of $\epsilon$.

There are two primary types of error structures:
1. **Homoskedasticity**: This occurs when the variance of the errors $\epsilon_i$ is constant across all observations, i.e., $\text{Var}(\epsilon_i) = \sigma^2$ for all $i$.
2. **Heteroskedasticity**: This occurs when the variance of the errors depends on the predictor variables, meaning $\text{Var}(\epsilon_i)$ is not constant and varies across observations.

The presence of heteroskedasticity or homoskedasticity affects the variance of the residuals $\hat{\epsilon}$, the estimated coefficients $\hat{\beta}$, and the predicted values $\hat{Y}$. This, in turn, influences the construction of confidence intervals for these parameters. Therefore, we must treat the two cases separately and apply different methods for estimation and inference.

### Detecting the heterodrasticity

Since we can only observe the residuals $\hat{\epsilon}$ (which are estimates of the true errors $\epsilon$), it is important to connect the residuals with the heteroskedasticity assumption. In practice, several diagnostic tools have been developed to detect heteroskedasticity:

- **Residual vs. Fitted Values Plot**: When the model assumes homoskedasticity, we expect $\text{cov}(\hat{\epsilon}, \hat{Y}) = 0$, meaning there should be no systematic pattern between the residuals and the fitted values. If homoskedasticity holds, the residuals should be randomly scattered around zero with no discernible structure.
  
  Specifically, under the assumption of normality, the residuals and fitted values are independent of each other. If heteroskedasticity is present, we may observe patterns such as a "fanning" effect or increasing/decreasing spread of the residuals as the fitted values increase.

- **Serial Correlation (Residual vs. Time or Sample Size)**: In time-series data, heteroskedasticity might manifest as serial correlation, where the residuals exhibit systematic patterns over time or across observations. If we observe that the residuals display such patterns, it suggests heteroskedasticity.


It's important to note that **observing heteroskedasticity does not automatically mean the model is incorrect**. There are two possible explanations for heteroskedasticity:
1. **True Heteroskedasticity**: The underlying process naturally has a non-constant variance of errors. This might occur, for instance, in financial or economic data, where variability increases with the size or magnitude of the predictor variables.
2. **Model Misspecification**: The observed heteroskedasticity could indicate that the model is misspecified, which might include issues such as omitted variables, non-linear relationships, or incorrect functional form.

### IID error and heterodrasticity
- IID error **does not imply** homodrasticity. For example, when IID error follows mixture distribution, then the variance is not constant. In general, if we assume the iid error under normality or markov condition, then the iid error is homodrasitcity.
- Non IID error **does not imply** the heterdrasticity. For example, the identical distributed error time-series have the constant variance but correlated to each other. Instead, the **non-identical** distributed error **does imply** the heterdrasticity.

## Homodrasticity
Under the assumption homodrasticity, we discuss the two cases of error distribution: normality distribution and without normality distribution.
### Normality assumption
Assume that $\epsilon \sim N(0,\sigma^2)$,  we have 

$$
\hat{\beta} \sim N(\beta,\sigma^2 (X^TX)^{-1}Id),
$$

$$
\hat{Y} \sim N(Y,\sigma^2P),
$$

$$
\hat{\epsilon} \sim N(\epsilon, \sigma^2M),
$$

where $P=X(X^TX)^{-1}X^T$ is the projection matrix  and $M=1-P$ is the residual maker matrix.

Additionally, the $\hat{\beta}$ becomes the **UMVU** among all **unbaised estimator** (including all linear and nonlinear estimators). However, the biased estimator might have a smaller variance as the sacrifice of deviation of true parameter.

The proof is [here].

### Guass Markov condition (Without normality)

Assume 

$$
\mathbb{E}[\epsilon] = 0, \quad \text{Cov}[\epsilon] = \sigma^2 I, \quad \text{rank}[X] = p.
$$

Note that the variance and mean of esimator remain the same as the normality assumption.

However, the apporximation does not directly follow the normal distribution. Instead, they **asymptoticly** converge to normal dsitribution. Additionally, **$c^T \hat{\beta}$ has minimal variance among all **linear unbiased estimators** of $c^T \beta$.**

#### **What happens when the error have the non-normal distribution?**
When the error is non-normal distribution, there exists other types of unbiased and biased estimators having smaller variance then OLS.  **Heavy Tails and Large Residuals**: The Laplace distribution's heavy tails make extreme residuals more common than in, say, a normal distribution. These outliers increase RSS disproportionately due to the squaring effect. Since RSS is the sum of squared residuals, it overemphasizes large errors, making the OLS objective particularly sensitive to these values. This results in $\hat{\beta}$ estimates that "chase" outliers, yielding high variance as $\hat{\beta}$ changes significantly with each extreme value. The increased variability in RSS directly translates to an unstable $\hat{\beta}$ because OLS is minimizing this highly variable RSS. Thus, the variance of $\hat{\beta}$ becomes large, reflecting the estimator's instability under Laplace-distributed errors. In constrast, the MLE is maximize the log-likehood function and log operator essentailly weaken the effect the outlier. Hence, the MLE have smaller variance than OLS when error follows distribution with the heavy tail.

## Heterdrasticity

When we construct models for data, we generally start with **linear regression**, assuming **homoskedasticity**, and use **OLS (Ordinary Least Squares)** to estimate the coefficients. After performing residual analysis, we need to **check for heteroscedasticity** if we observe a pattern in the residuals that indicates non-constant variance. Recall that, under normality assumption of error, we estimate the error variance using:

$$
\hat{\sigma}^2 = \frac{1}{n - p} \hat{\epsilon}^T \hat{\epsilon}
$$

where $\hat{\epsilon}$ are the residuals, and this estimator is unbiased and follows a **chi-squared distribution** under the . However, in the presence of heteroscedasticity, the error variance is not constant, and this estimator becomes invalid. The most challenging part of dealing with heteroscedasticity is that it makes the estimation of the error variance difficult. Now,  we shall start with the special case: the error follows normal distribution but not IID.i.e, $\epsilon \sim N(0,\sigma^2\Sigma)$ and $\Sigma$ is not the identity matrix. The estimation technique does not change. In other words, under normality assumption, we still can estimate $\hat{\beta}=(X^TX)^{-1}X^TY$, but the variance of the estimator changes and we need to build new confidence interval for it.

### Generalized Least Squares(GLS)
In cases where we know the covariance structure of the errors (for example, if the errors are heteroscedastic but we know how their variance changes with respect to the predictors), due the diagonalizable nature of the $\Sigma=A^TA$ for some invertible matrix $A$, we can construct the following **GLS estiamtor**

$$
\hat{\beta}= (X^T\Sigma^{-1}X)^{-1}X^T\Sigma^{-1}Y,
$$

$$
\hat{\beta} \sim N(\beta,\sigma^2(X^T\Sigma^{-1})X),
$$

$$
\hat{\sigma}^2 = \frac{1}{n - p} \hat{\epsilon}^T \Sigma^{-1}\hat{\epsilon},
$$

$$
\hat{\sigma}^2 \sim \chi_{n-p}
$$

Then, we can built the test and confidence interval based on the new estimator.

### Sandwich Estimator
In general, when the covariance of the error distribution is unknown, **Sandwich Estimator**: This method provides a consistent estimate of the variance-covariance matrix of the coefficients. Assume that $\epsilon \sim N(0,D)$ and $D$ is unknow, we have 

$$
\hat{\beta}= (X^TX)^{-1}XY,
$$

$$
\hat{\beta} \sim N(\beta,(X^TX)^{-1}X^TDX(X^TX)^{-1})
$$

The sandwich estimator essentially provide the estimator for $(X^TX)^{-1}X^TDX(X^TX)^{-1}$ by letting $\hat{D}=\text{diag}(r_1^2,\cdots, r_n^2)$ and $r_i=Y_i-\hat(Y)_i$. This allow us to construct a distribution for $\hat{\beta}$ and find the new confidence interval for the estimated $\beta$.i.e, we need to verify 

$$
\hat{\beta} \rightarrow N(\beta,(X^TX)^{-1}X^T\hat{D}X(X^TX)^{-1}) \quad \text{as} \quad n \rightarrow \infty
$$

First, we need to verify that $\hat{\beta}$ converges to $\beta$ in probability. i.e, 

$$
\text{E}(\hat{\beta})=\beta,
$$

$$
\text{Var}(\hat{\beta}) \rightarrow 0 \quad \text{as} n \rightarrow \infty.
$$

The first condition satifies by the definition of $\hat{\beta}$. The second condition satisfies under two assumptions: 

$$
\text{(A1)} \quad  \frac{X^TX}{n} \to C \quad (n \to \infty) \quad \text{with} C \text{positive definite}, \\
$$

$$
\text{(A2)} \quad  \sigma_i^2 \leq C_1 < \infty \, \forall i \quad \text{and} \quad n^{-1} \sum_{i=1}^n X_{ij}^2 \leq C_2 < \infty,\quad \text{for all} j.
$$

$A1$ bound the "bread" of the variance of estimated $\beta$ and $A2$ bound the "ham" of the variance of estiamted $\beta$.


Then, we verify that $(X^TX)^{-1}X^T\hat{D}X(X^TX)^{-1}$ converges to $(X^TX)^{-1}X^TDX(X^TX)^{-1}$ in probability. i.e, we need to verify 
$(X^TX)^{-1}X^T\hat{D}X(X^TX)^{-1}-(X^TX)^{-1}X^TDX(X^TX)^{-1} \rightarrow 0$ as $n \rightarrow \infty$. This condition will be satisfied under assumption

$$
\text{(A3)} \quad \max_{i,j} \|X_{ij} \| \leq K < \infty.
$$

After verifying this, we can use slutsky theorem to show 

$$
\frac{1}{\sqrt{(X^TX)^{-1}X^T\hat{D}X(X^TX)^{-1}}}(\hat{\beta}-\beta) \rightarrow N(0,1)
$$

Then, we can build the confidence interval of $\hat{\beta}$ based on this distribution.




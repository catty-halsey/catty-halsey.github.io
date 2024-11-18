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

Since we can only observe the residuals $\hat{\epsilon}$ (which are estimates of the true errors $\epsilon$), it is important to connect the residuals with the heteroskedasticity assumption. In practice, several diagnostic tools have been developed to detect heteroskedasticity:

- **Residual vs. Fitted Values Plot**: When the model assumes homoskedasticity, we expect $\text{cov}(\hat{\epsilon}, \hat{Y}) = 0$, meaning there should be no systematic pattern between the residuals and the fitted values. If homoskedasticity holds, the residuals should be randomly scattered around zero with no discernible structure.
  
  Specifically, under the assumption of normality, the residuals and fitted values are independent of each other. If heteroskedasticity is present, we may observe patterns such as a "fanning" effect or increasing/decreasing spread of the residuals as the fitted values increase.

- **Serial Correlation (Residual vs. Time or Sample Size)**: In time-series data, heteroskedasticity might manifest as serial correlation, where the residuals exhibit systematic patterns over time or across observations. If we observe that the residuals display such patterns, it suggests heteroskedasticity.


It's important to note that **observing heteroskedasticity does not automatically mean the model is incorrect**. There are two possible explanations for heteroskedasticity:
1. **True Heteroskedasticity**: The underlying process naturally has a non-constant variance of errors. This might occur, for instance, in financial or economic data, where variability increases with the size or magnitude of the predictor variables.
2. **Model Misspecification**: The observed heteroskedasticity could indicate that the model is misspecified, which might include issues such as omitted variables, non-linear relationships, or incorrect functional form.

In the following, we introduce how to approximate the parameters under homodrasticity and heterodrasticity.


## Homodrasticity
Under the assumption homodrasticity, we discuss the two cases of error distribution: normality distribution and without normality distribution.
### Normality assumption
Assume that $\epsilon \sim N(0,\sigma^2)$,  we have 

$$
\hat{\beta} \sim N(\beta,\sigma^2 (X^TX)^{-1}),
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

Withoud the normality assumption, we have the following properties of estimators.

- 1.**$\hat{\beta}$, $\hat{Y}$, and $\hat{\epsilon}$ asymptoticly converge to the normal distribution.**

- 2.**$c^T \hat{\beta}$ has minimal variance among all **linear unbiased estimators** of $c^T \beta$.**


When the error is non-normal distribution, there exists other types of unbiased and biased estimators having smaller variance then OLS.  **Heavy Tails and Large Residuals**: The Laplace distribution's heavy tails make extreme residuals more common than in, say, a normal distribution. These outliers increase RSS disproportionately due to the squaring effect. Since RSS is the sum of squared residuals, it overemphasizes large errors, making the OLS objective particularly sensitive to these values. This results in $\hat{\beta}$ estimates that "chase" outliers, yielding high variance as $\hat{\beta}$ changes significantly with each extreme value. The increased variability in RSS directly translates to an unstable $\hat{\beta}$ because OLS is minimizing this highly variable RSS. Thus, the variance of $\hat{\beta}$ becomes large, reflecting the estimator's instability under Laplace-distributed errors. In constrast, the MLE is maximize the log-likehood function and log operator essentailly weaken the effect the outlier. Hence, the MLE have smaller variance than OLS when error follows distribution with the heavy tail.

## Heterdrasticity

## Error distribution are unknown.
the $\hat{\beta}$ converge to $\beta$ in probability, which means that the variance of $\hat{\beta}$ converge to $0$ as $n$ goes to infinity.


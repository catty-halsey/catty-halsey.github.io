---
layout: post
title: "Why the distribution of error matters?"
author: "Ziyan Li"
categories: journal
tags: [documentation, sample]
---

In linear regression, we have 

$$
Y=X\beta+\epsilon.
$$

Although  $Y$ and $\epsilon$ are random variables, the distribution of $Y$ largely depdend on the distribution of $\epsilon$. Additionally, the approximation of $\beta$ and $Y$ also largely depdend on the distribution of $\epsilon$. In the following, we will derive how distribution of $\epsilon$ affect the apporximation. Before that, we shall address the difference between error $\epsilon$ and residual $\hat{\epsilon}$. Residual $\hat{\epsilon}=Y-\hat{Y}$ generally have the different distribution from error distribution. For example, assume $\epsilon \sim N(0,\sigma^2)$, we have $\hat{\epsilon} \sim N(0,\sigma^2M)$ where $M$ is residual maker matrix. However, we have a nice property of residual: $\hat{\epsilon} \perp \hat{Y}$. Thus, we can plot $\hat{Y}$ against $\hat{\epsilon}$ to test whether there exist a systematic error. Alternatively, we can plot the QQ-plot of the residuals. The plot is close to a line as long as the residual follows the normal distribution. 

In the following, we discuss the two cases of error distribution: normality distribution and without normality distribution.

## Normality assumption
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

## Guass Markov condition (Without normality)

Assume 

$$
\mathbb{E}[\epsilon] = 0, \quad \text{Cov}[\epsilon] = \sigma^2 I, \quad \text{rank}[X] = p.
$$

Withoud the normality assumption, we have the following properties of estimators.

- 1.**$\hat{\beta}$, $\hat{Y}$, and $\hat{\epsilon}$ asymptoticly converge to the normal distribution.**

- 2.**$c^T \hat{\beta}$ has minimal variance among all **linear unbiased estimators** of $c^T \beta$.**


When the error is non-normal distribution, there exists other types of unbiased and biased estimators having smaller variance then OLS.  **Heavy Tails and Large Residuals**: The Laplace distribution's heavy tails make extreme residuals more common than in, say, a normal distribution. These outliers increase RSS disproportionately due to the squaring effect. Since RSS is the sum of squared residuals, it overemphasizes large errors, making the OLS objective particularly sensitive to these values. This results in $\hat{\beta}$ estimates that "chase" outliers, yielding high variance as $\hat{\beta}$ changes significantly with each extreme value. The increased variability in RSS directly translates to an unstable $\hat{\beta}$ because OLS is minimizing this highly variable RSS. Thus, the variance of $\hat{\beta}$ becomes large, reflecting the estimator's instability under Laplace-distributed errors. In constrast, the MLE is maximize the log-likehood function and log operator essentailly weaken the effect the outlier. Hence, the MLE have smaller variance than OLS when error follows distribution with the heavy tail.

## Error distribution are unknown.
the $\hat{\beta}$ converge to $\beta$ in probability, which means that the variance of $\hat{\beta}$ converge to $0$ as $n$ goes to infinity.


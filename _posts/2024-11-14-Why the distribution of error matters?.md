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
When we assume $\epsilon \sim N(0,\sigma^2)$, the $\hat{\beta}$ becomes the **UMVU** among all **unbaised estimator** (including all linear and nonlinear estimators). However, the biased estimator might have a smaller variance as the sacrifice of deviation of true parameter.

The proof is [here].

## Guass Markov condition (Without normality)

Assume 

$$
\mathbb{E}[\epsilon] = 0, \quad \text{Cov}[\epsilon] = \sigma^2 I, \quad \text{rank}[X] = p.
$$

Furthermore, let $c$ be an arbitrary $p$-dimensional vector, and $\hat{\beta}$ the least squares estimator. Then $c^T \hat{\beta}$ has minimal variance among all **linear unbiased estimators** of $c^T \beta$.



---
layout: post
title: "Importance sampling"
author: "Ziyan Li"
categories: journal
tags: [documentation, sample]
---
When we want to estimate the $\theta = \text{E}(h(X))$, where $X \sim \pi$. The dierct way is to simulate the sample from the target distribution $\pi$,
plug the sample into the function $h$, and then take the average. i.e,

$$
\hat{\theta}=\frac{1}{N}\sum_{i=1}^n h(X_i),
$$

where $X_i \sim \pi$.

However, in practice, when the target distribution is complicated, it is hard to directly sample from it. Therefore, we introduce a proposed distribution, which is accessible for direct simulation. Rejection sampling and importance sampling both involve using proposed distribution $\tau$ to construct estimator $\\hat{\theta}$ to estimate the expecation of a function $h(X)$ under the target distribution $\pi$. Next, we focus on introducing teo types of importance sampling, namely additive importance sampling and multiplicative importance sampling. In the following construction, we assume that both target $\pi$ and proposed distribution $\tau$ both have density function denoted as $f(x)$ and $g(x)$, respectively.

The additive importance sampling defined as 

$$
\hat{\theta}=\frac{1}{N}\sum_{i=1}^N h(X_i)w(X_i),
$$

where $X_i \sim \tau$, $w(x)=f(X_i)/g(X_i)$ served as a weighted function.

**Remark**
- Unbiased
- Inconsistent under normalization: it is not a suitable estimator when we want to estimate the proportion of target distribution.
- Suitable choice of $g(x)$ can lead to more accurate estimator than direct estimation. "Accuracy" here means that smaller bias and variance. "Suitable choice" means the $g(x)$ is close to $|h(x)|f(x)$. In partiular, the variance of this estimator is smallest when the following equality holds $g(x) = \frac{|h(x)|f(x)}{\int |h(x)|f(x) \ \mu(dx)}$. In general, it is impossible to attain the smallest variance because we can not compute the integration part. However, it present a good idea of how to choose our proposed distribution and construct a better estimator.

The multiplicative importance sampling defined as 

$$
\hat{\theta}=\frac{\frac{1}{N}\sum_{i=1}^N h(X_i)w(X_i)}{\frac{1}{N}\sum_{i=1}^N w(X_i)},
$$

where $X_i \sim \tau$, $w(X_i)=f(X_i)/g(X_i)$ served as a weighted function.

**Remark**

- **Bias**: The estimator is biased.
  
- **Consistency under Normalization**: This estimator can be applied when only partial information about the target distribution is available, such as in the case of a posterior distribution.

- **Sensitivity to Rare Events**: This estimator is sensitive to estimating rare events, e.g., probabilities of the form $P(X > t)$ where $t$ is a threshold.

- **Variance and Correlation in Estimation**: The numerator term $\frac{1}{N} \sum_{i=1}^N w(X_i)$ not only ensures the consistency of the estimator under normalization but also introduces a correlation between the numerator and the denominator. This correlation acts as a variance reduction, often referred to as a *control variate*. However, introducing this numerator also brings additional variance. Therefore, a trade-off exists between these two effects, which depends heavily on the function $h(X)$ used. Specifically, the choice of event to be estimated is crucial; in particular, when estimating rare events, high values of $h(X)$ can weaken the correlation between the numerator and denominator, potentially resulting in a higher variance than that of an additive estimator. An example is provided below to illustrate this.

- **Asymptotic Properties**: Although one cannot to compute the exact expected value and variance of the multiplicative estimator $\hat{\theta}$, we can analyze its asymptotic behavior using the Central Limit Theorem (CLT). The estimator improves as the correlation between the numerator and denominator increases.




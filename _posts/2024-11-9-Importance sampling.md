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
- Inconsistent under normalization: it is not a suitable estimator when we want to estimate the proportion of target distribution. Mathematically, assume $f(x)=\frac{1}{Z}\tilde{f}(x)$, we have $\frac{1}{N}\sum_{i=1}^N h(X_i)\tilde{w}(X_i)$ almost surely converges to $Z\theta$, where $\tilde{w}=\tilde{f}/g$ and $Z$ is normalized constant.
- Suitable choice of $g(x)$ can lead to more accurate estimator than direct estimation. "Accuracy" here means that smaller bias and variance. "Suitable choice" means the $g(x)$ is close to $\vert h(x)\vert f(x)$. In partiular, the variance of this estimator is smallest when the following equality holds $g(x) = \frac{\vert h(x)\vert f(x)}{\int \vert h(x)\vert f(x) \ \mu(dx)}$. In general, it is impossible to attain the smallest variance because we can not compute the integration part. However, it present a good idea of how to choose our proposed distribution and construct a better estimator.
- The variance is influenced by the behavior of $h(x) \cdot w(x)$, which depends heavily on both the nature of $h(x)$ and how well $w(x)$ (the importance weights) are controlled by the choice of proposal distribution $g(x)$.
- When estimating a probability, we often use an indicator function $h(x) = \mathbb{I}\{X \in A\}$, which is bounded. This boundedness inherently limits the variance of the estimator, making it more stable and often effective for rare-event estimation.
- For unbounded $h(x)$, like $h(x) = x$, large values of $x$ can interact with $w(x)$ (i.e., $\frac{f(x)}{g(x)}$) to create heavy tails in $h(x)w(x)$, leading to potentially infinite or high variance. (See the example following)

The multiplicative importance sampling defined as 

$$
\hat{\theta}=\frac{\frac{1}{N}\sum_{i=1}^N h(X_i)w(X_i)}{\frac{1}{N}\sum_{i=1}^N w(X_i)},
$$

where $X_i \sim \tau$, $w(X_i)=f(X_i)/g(X_i)$ served as a weighted function.

**Remark**

- **Bias**: The estimator is biased.
  
- **Consistency under Normalization**: This estimator can be applied when only partial information about the target distribution is available, such as in the case of a posterior distribution. Mathematically, Mathematically, assume $f(x)=\frac{1}{Z}\tilde{f}(x)$, we have $\frac{\frac{1}{N}\sum_{i=1}^N h(X_i)\tilde{w}(X_i)}{\frac{1}{N}\sum_{i=1}^N \tilde{w}(X_i)}$ almost surely converges to $\theta$, where $\tilde{w}=\tilde{f}/g$. 

- **Sensitivity to Rare Events**: This estimator is sensitive to estimating rare events, e.g., probabilities of the form $P(X > t)$ where $t$ is a threshold.

- **Variance and Correlation in Estimation**: The numerator term $\frac{1}{N} \sum_{i=1}^N w(X_i)$ not only ensures the consistency of the estimator under normalization but also introduces a correlation between the numerator and the denominator. This correlation acts as a variance reduction, often referred to as a *control variate*. However, introducing this numerator also brings additional variance. Therefore, a trade-off exists between these two effects, which depends heavily on the function $h(X)$ used. Specifically, the choice of event to be estimated is crucial; in particular, when estimating rare events, high values of $h(X)$ can weaken the correlation between the numerator and denominator, potentially resulting in a higher variance than that of an additive estimator. An example is provided below to illustrate this.
- Certainly! I'll incorporate this passage into the explanation to add context, especially in terms of how the target and proposal distributions relate through importance sampling in causal inference and reinforcement learning settings.
- In **causal inference for episodic reinforcement learning**, importance sampling is often used to estimate expectations under an intervened (or target) distribution $\tilde{p}(x)$ by using samples from an original (or proposal) distribution $p(x)$. Here’s how it connects to the concepts of variance and control variates. Suppose we want to estimate an expectation $\xi := \tilde{\mathbb{E}}[h(X)]$, where $h(X)$ is some function of $X$ (often an outcome variable or reward) under the distribution $\tilde{p}(x)$ after intervention. We rewrite this as an integral over the original distribution:
   
$$
\xi = \tilde{\mathbb{E}}[h(X)] = \int h(x) \tilde{p}(x) \, dx = \int h(x) \frac{\tilde{p}(x)}{p(x)} p(x) \, dx = \mathbb{E}_p \left[h(X) \frac{\tilde{p}(X)}{p(X)}\right].
$$

Given a sample $X_1, \dots, X_n$ drawn from the distribution $P_{X_C}$,
we can thus construct an estimator:

$$
\hat{\xi} := \frac{1}{n} \sum_{i=1}^n \ell(X_i) \frac{\tilde{p}(X_{i_k} \mid X_{i_{\text{pa}(k)}})}{p(X_{i_k} \mid X_{i_{\text{pa}(k)}})} = \frac{1}{n} \sum_{i=1}^n \ell(X_i) w_i
$$

where $w_i$ is the importance weight for each sample.

  
- **Asymptotic Properties**: Although one cannot to compute the exact expected value and variance of the multiplicative estimator $\hat{\theta}$, we can analyze its asymptotic behavior using the Central Limit Theorem (CLT). The estimator improves as the correlation between the numerator and denominator increases.




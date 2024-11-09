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

However, in practice, when the target distribution is complicated, it is hard to directly sample from it. Therefore, we introduce a proposed distribution, which is accessible for direct simulation. Rejection sampling and importance sampling both involve using proposed distribution $\tau$ to construct estimator $\\hat{\theta}$ to estimate the expecation of a function $h(X)$ under the target distribution $\pi$. Next, we focus on introducing teo types of importance sampling, namely additive importance sampling and multiplicative importance sampling.


---
layout: post
title: "Markov inequality"
author: "Ziyan Li"
categories: tutorials
tags: [documentation, sample]
---

Let $X$ be a non-negative random variable (i.e., $X \geq 0$) and $a > 0$. Then, Markov's inequality states that:

$$
P(X \geq a) \leq \frac{\mathbb{E}(X)}{a}
$$

### Proof
For all $\epsilon >0$, 

$$
\epsilon P(X > a) = \epsilon E(1_{X>a})=E(\epsilon 1_{X>a})\leq E(X 1_{X>a}) leq E(X).
$$

### Intuition
1. **Basic Idea:**
   - If $X$ has a large mean, it implies that $X$ cannot be small all the time. Markov's inequality quantifies this intuition by saying that the probability of $X$ being large (greater than $a$) is at least partially controlled by the mean of $X$.
   
2. **Example Intuition:**
   - Suppose $X$ represents the wealth of a randomly chosen individual in a population, and we know that the average wealth is $\mathbb{E}(X) = 50,000$ dollars. We want to bound the probability that a randomly chosen individual has wealth of at least $200,000$ dollars:

$$
P(X \geq 200,000) \leq \frac{\mathbb{E}(X)}{200,000} = \frac{50,000}{200,000} = 0.25
$$

This means that at most 25% of the population has wealth exceeding $200,000$ dollars.

### Application in probability theory

1.Chebyshev's inequality

Let $X$ be a random variable with mean $\mu$ and Variance exists. Chebyshev's inequality states:

$$
P(|X - \mu| \geq \epsilon) \leq \frac{\mathbb{Var}(X)}{\epsilon^2}
$$

**Proof**:

$$
P((X - \mu)^2 \geq \epsilon^2) \leq \frac{\mathbb{E}[(X - \mu)^2]}{\epsilon^2}.
$$

More generally, we can write chebyshev's inequality as 

$$
P(\phi(|X - \mu|) \geq \epsilon) \leq \frac{\mathbb{Var}(X)}{\phi(\epsilon)}
$$

where $\phi(\dot)$ is c.t.s increaseing function. And this inequality often be used to prove the random variable converge in probability.


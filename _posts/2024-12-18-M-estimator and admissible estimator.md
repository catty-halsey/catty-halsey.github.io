---
layout: post
title: "M-estimator and admissible estimator"
author: "Ziyan Li"
categories: journal
tags: [documentation, sample]
---
In this blog, we attempt to illustrate the difference and similarities between M-estimator and admissible estimator. We aim to clarify their definitions, highlight key properties, and explore their connections, particularly through the lens of asymptotics and robustness. While M-estimators are often pragmatic tools, defined through optimization of empirical criteria, admissible estimators stem from theoretical foundations, ensuring optimality under a given loss function.


### **1. M-Estimators in Formal Terms**

Given a parameter $\theta \in \Theta$ and observations $X_1, \ldots, X_n$, the M-estimator is defined as:

$$
\hat{\theta}_n = \arg\max_{\theta \in \Theta} M_n(\theta),
$$

where $M_n(\theta) = \frac{1}{n} \sum_{i=1}^n m_\theta(X_i)$ is the empirical criterion. Here, $m_\theta$ is a function that depends on $\theta$ and the data $X_i$. 

### **Example 1.1: Maximum Likelihood Estimation (MLE)**
For the MLE:

$$
M_n(\theta) = \frac{1}{n} \sum_{i=1}^n \log f_\theta(X_i),
$$

where $f_\theta$ is the likelihood function. The MLE maximizes the likelihood of observing the data under the parameter $\theta$.

- **Empirical Nature:** The MLE relies on the observed data to estimate $\theta$, making it a typical M-estimator. 
- **Asymptotics:** As $n \to \infty$, under regularity conditions, $\hat{\theta}_n \to \theta_0$ (the true parameter), and the estimator becomes asymptotically efficient.

---

### **2. Admissible Estimators in Formal Terms**

An estimator $\hat{\theta}$ is admissible if there does not exist another estimator $\tilde{\theta}$ such that:
1. $R(\tilde{\theta}, \theta) \leq R(\hat{\theta}, \theta)$ for all $\theta$, and
2. $R(\tilde{\theta}, \theta) < R(\hat{\theta}, \theta)$ for at least one $\theta$,
where $R(\hat{\theta}, \theta) = \mathbb{E}[(\hat{\theta} - \theta)^2]$ is the risk function.

### **Example 2.1: Bayes Estimator**
The Bayes estimator under squared error loss is:

$$
\hat{\theta}_{\text{Bayes}} = \mathbb{E}[\theta \mid X].
$$

- **Theoretical Nature:** This estimator leverages the posterior distribution $\mathbb{P}(\theta \mid X)$, which is derived from the full $X$-sigma algebra, and minimizes the Bayes risk:
  
$$
R_B(\hat{\theta}) = \int \mathbb{E}[(\hat{\theta}(X) - \theta)^2] \, dP(\theta).
$$

- **Admissibility:** Bayes estimators are admissible under regularity conditions because they incorporate all information available about $X$.

---


### **3. 1D Case: MLE and Admissibility**

In the one-dimensional case ($X \in \mathbb{R}$), the Maximum Likelihood Estimator (MLE) often asymptotically aligns with the admissible estimator, particularly under regularity conditions. 

#### **Theorem (1D Case):**
Let $X_1, \ldots, X_n \sim f_\theta(x)$, and assume:
1. $f_\theta(x)$ is differentiable with respect to $\theta$.
2. The true parameter $\theta_0$ lies in the interior of $\Theta$.
3. Fisher information $I(\theta_0) > 0$ exists and is finite.
4. The log-likelihood function $\ell(\theta) = \sum_{i=1}^n \log f_\theta(X_i)$ satisfies standard regularity conditions.

Then:
1. The MLE $\hat{\theta}_n$ is consistent: $\hat{\theta}_n \to \theta_0$ as $n \to \infty$.
2. $\sqrt{n} (\hat{\theta}_n - \theta_0) \to \mathcal{N}(0, I^{-1}(\theta_0))$, achieving the Cramér-Rao Lower Bound (CRLB).
3. The MLE is asymptotically efficient and thus asymptotically admissible, as no estimator can uniformly dominate it in risk under squared error loss.

#### **Higher-Dimensional Case: Stein’s Paradox**

In dimensions $d > 2$, the MLE is no longer guaranteed to be admissible, even asymptotically. This phenomenon is elegantly captured by **Stein's paradox**, which demonstrates how a shrinkage estimator can outperform the MLE in higher-dimensional settings.

##### **Stein’s Paradox:**
Consider the problem of estimating $\theta \in \mathbb{R}^d$ from $X \sim \mathcal{N}(\theta, I_d)$, where $d \geq 3$. The MLE, $\hat{\theta} = X$, is not admissible under the squared error loss $R(\hat{\theta}, \theta) = \mathbb{E}[\|\hat{\theta} - \theta\|^2]$. Specifically, it is dominated by the **James-Stein estimator**:

$$
\hat{\theta}_{\text{JS}} = \left(1 - \frac{d-2}{\|X\|^2}\right) X.
$$

This shrinkage estimator has uniformly lower risk compared to the MLE:

$$
R(\hat{\theta}_{\text{JS}}, \theta) < R(\hat{\theta}, \theta) \quad \forall \, \theta \in \mathbb{R}^d.
$$

The intution: The MLE treats each parameter independently, optimizing them without accounting for the dimensional structure of $\theta$. In higher dimensions, pooling or shrinking information across components reduces variance, even at the cost of introducing a small bias. This tradeoff leads to a lower overall risk (a better bias-variance balance).

##### **Example: Normal Mean Estimation**
- **Setup:** $X \sim \mathcal{N}(\theta, I_d)$, $d \geq 3$, squared error loss $L(\hat{\theta}, \theta) = \|\hat{\theta} - \theta\|^2$.
- **MLE:** $\hat{\theta}_{\text{MLE}} = X$, with risk $R(\hat{\theta}_{\text{MLE}}, \theta) = d$.
- **James-Stein Estimator:** $\hat{\theta}_{\text{JS}} = \left(1 - \frac{d-2}{\|X\|^2}\right) X$, with risk:

$$
R(\hat{\theta}_{\text{JS}}, \theta) = d - \frac{d-2}{\|\theta\|^2}.
$$

For all $\theta$, the James-Stein estimator satisfies $R(\hat{\theta}_{\text{JS}}, \theta) < R(\hat{\theta}_{\text{MLE}}, \theta)$, demonstrating the superiority of shrinkage estimators in higher dimensions. This result exemplifies the limitations of the MLE and highlights the advantages of estimators that incorporate global information about the parameter space.

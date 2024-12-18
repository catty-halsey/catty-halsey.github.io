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

### **3. Connection Between M-Estimators and Admissible Estimators**

#### **Asymptotic Behavior of M-Estimators**
Under regularity conditions (e.g., smoothness and identifiability of $m_\theta$), M-estimators satisfy:
1. **Consistency:** $\hat{\theta}_n \to \theta_0$ in probability as $n \to \infty$.
2. **Asymptotic Normality:** $\sqrt{n} (\hat{\theta}_n - \theta_0) \to \mathcal{N}(0, I^{-1}(\theta_0))$, where $I(\theta_0)$ is the Fisher information.

This means M-estimators converge to the true parameter $\theta_0$ and become efficient (i.e., achieve the Cramér-Rao lower bound) in large samples, mimicking the behavior of admissible estimators.

#### **M-Estimators and the Bayes Estimator**
- For large $n$, the empirical risk $M_n(\theta)$ approximates the true (population) risk:
  
$$
M_n(\theta) \to M(\theta) = \mathbb{E}[m_\theta(X)],
$$

where $M(\theta)$ represents the theoretical criterion minimized by admissible estimators. This explains why M-estimators approach admissible estimators asymptotically.

- However, for small $n$, M-estimators lack information about the full distribution $P(X)$, unlike the Bayes estimator, which uses the complete posterior.

---

### **4. Example: Comparing M-Estimators and Admissible Estimators**

#### **Setup: Estimating the Mean**
Let $X_1, \ldots, X_n \sim \mathcal{N}(\mu, \sigma^2)$, and we want to estimate $\mu$.

1. **M-Estimator:** The sample mean:
   
$$
\hat{\mu}_n = \frac{1}{n} \sum_{i=1}^n X_i,
$$

maximizes the likelihood or minimizes $\sum (X_i - \mu)^2$.

3. **Admissible Estimator:** The Bayes estimator under a normal prior $\mu \sim \mathcal{N}(\mu_0, \tau^2)$:
   
$$
\hat{\mu}_{\text{Bayes}} = \frac{\tau^2}{n\sigma^2 + \tau^2} \mu_0 + \frac{n\sigma^2}{n\sigma^2 + \tau^2} \hat{\mu}_n.
$$

- **Small $n$:** The Bayes estimator dominates the M-estimator, as it incorporates prior information ($\mu_0$).
- **Large $n$:** The M-estimator converges to the true mean and approximates the Bayes estimator.

---

### **5. Robustness and Global Optimality**

- **M-Estimator Robustness:** Sensitive to finite-sample variability and model misspecification. For example, outliers can heavily influence the sample mean.
- **Admissible Estimator Robustness:** Globally minimizes risk due to its derivation from theoretical principles, ensuring optimality even in finite samples.

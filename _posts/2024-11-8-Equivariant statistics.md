---
layout: post
title: "Equivariant statistic"
author: "Ziyan Li"
categories: journal
tags: [documentation, sample]
---
First, we look at how to construct an **UMRE** estimator.

### **Theorem: Uniformly Minimum Risk Estimator (UMRE) Construction**

Let $X$ be a random variable with a parameter $\theta$, and let $d(X)$ be an equivariant estimator of $X$. Define the transformed variable $Y = X - d(X)$, where $Y$ is independent of $\theta$.

Let $\hat{T}(Y)$ be the estimator that minimizes the conditional risk in the $Y$-space, i.e.,

$$
\hat{T}(Y) = \arg \min_{v} E[L_0(v + Y)],
$$

where $L_0$ is the loss function for the noise part (when $\theta = 0$).

Then, the uniformly minimum risk estimator (UMRE) of $X$ is given by:

$$
\hat{T}(X) = \hat{T}(Y) + d(X).
$$

### **Step 1: Separate $X$ into Components**
First, we begin with the random variable $X$, which depends on the parameter $\theta$. To make the estimator independent of $\theta$, we decompose $X$ into two parts:
$$
X = d(X) + Y,
$$
where:
- **$d(X)$** is an equivariant estimator of $X$, which depends on $\theta$.
- **$Y = X - d(X)$** represents the noise or deviation part of $X$, which is constructed to be **independent of $\theta$** (since $d(X)$ is an estimator of $X$).

This transformation separates the parameter-dependent part of $X$ (i.e., $d(X)$ ) from the noise part $Y$, which is free of $\theta$. The noise part $Y$ captures the variability around the true parameter value without the parameter itself.

### **Step 2: Minimize the Risk in the $Y$-Space**
We now focus on the noise part, $Y$, because it is independent of $\theta$, which simplifies our problem. We want to construct an estimator $\hat{T}(Y)$ that minimizes the **conditional risk** given $Y$. Since $Y$ is independent of $\theta$, we can safely minimize the expected loss function $L(\theta, T(X))$ over $\hat{T}(Y)$ without having to account for $\theta$:

$$
\hat{T}(Y) = \arg \min_v E[L_0(v + \epsilon_n)].
$$

Here, $L_0$ is the loss function when $\theta = 0$, and $\epsilon_n$ represents the noise components (the deviations of $Y$).

Since the distribution of $Y$ does not depend on $\theta$, minimizing the risk in the $Y$-space is equivalent to minimizing the risk of $\hat{T}(X)$, the estimator in the original space of $X$.

### **Step 3: Construct the UMRE by Restoring $d(X)$**
Now that we have $\hat{T}(Y)$, we need to **restore** the estimator back to the original space of $X$. This is done by adding the equivariant estimator $d(X)$ back to $\hat{T}(Y)$. This ensures that we are in the original space of $X$ while still minimizing the risk:

$$
\hat{T}(X) = \hat{T}(Y) + d(X).
$$

The addition of $d(X)$ makes sure that the final estimator is **invariant under the transformation** $\hat{T}$. Importantly, $d(X)$ is independent of $\theta$ by construction, and $\hat{T}(Y)$ minimizes the risk in the noise part.

### **Why This Works:**
- **Minimizing the risk in the $Y$-space**: Since $Y$ is independent of $\theta$, minimizing the risk for each realization of $Y$ effectively minimizes the risk of the overall estimator $\hat{T}(X)$. The estimator $\hat{T}(Y)$ is thus optimal for the noise part of the data.
  
- **Invariance of $d(X)$**: By adding $d(X)$ back into $\hat{T}(Y)$, we preserve the **invariance of $d(X)$**, which ensures that the final estimator is correctly scaled and remains independent of $\theta$. The term $d(X)$ does not change during the transformation $\hat{T}$, and its role is crucial for maintaining the consistency of the estimator with respect to $X$.

- **UMRE**: The final estimator $\hat{T}(X) = \hat{T}(Y) + d(X)$ is **uniformly minimum risk** because it minimizes the expected loss for all values of $\theta$. The construction guarantees that the estimator achieves the minimum possible risk over the class of unbiased estimators, and it remains unbiased by design.

### **Step 4: Uniformity of the Estimator**
Since $\hat{T}(Y)$ minimizes the conditional risk in the noise space, and the noise distribution is independent of $\theta$, the estimator $\hat{T}(X) = \hat{T}(Y) + d(X)$ becomes uniformly minimum risk by combining both parts:
- The optimal estimator in the noise space $\hat{T}(Y)$,
- The equivariant estimator $d(X)$, which remains invariant under $\hat{T}$.

This ensures that $\hat{T}(X)$ is **UMRE**, as it is the best possible estimator in terms of risk across all values of $\theta$ and satisfies the criteria for the UMRE in terms of unbiasedness and minimal risk.


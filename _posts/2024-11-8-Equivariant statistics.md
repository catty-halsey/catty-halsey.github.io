---
layout: post
title: "Equivariant estimator"
author: "Ziyan Li"
categories: journal
tags: [documentation, sample]
---
Before introducing equivariant estimator, we shall firstly introduce the concept of invariance under transformation. Since when we discuss equivariant estimators, we essentially refer to that the estimators is equivariant w.r.t some transformation $g$.

The model $\mathcal{P}$ is invariant to a transformation $g$ if:

$$
\text{1. When } X \sim P \in \mathcal{P}, \text{ then } gX = X' \sim P' \in \mathcal{P}.
$$

$$
\text{2. For every } P' \in \mathcal{P}, \, \exists P \in \mathcal{P} \text{ such that } X \sim P \Rightarrow gX \sim P'.
$$

Under this transformation, $gX$ has the same distribution as $X$. Hence, if we take a decision $\delta$ on $X$, the loss function satisfies $L(\theta_1, \delta(X)) = L(\theta_2, \delta(gX))$, where $\theta_2 = g\theta_1$. The question arises: is it possible to find a transformation $\tilde{g}$ such that $\tilde{g} \delta(X) = \delta(gX)$, satisfying $L(\theta_1, \delta(X)) = L(\theta_2, \delta(gX))$? The answer is not always. However, if such a $\tilde{g}$ exists, we say the loss function is **invariant under the transformation**. Thus, we can write:

$$
L(\theta_1, \delta(X)) = L(g\theta_1, \delta(gX)) = L(g\theta_1, \tilde{g} \delta(X)).
$$

A decision rule or estimator $\delta(\cdot)$ is **equivariant with respect to transformation** $g$ if $\delta(gX) = g(\delta(X))$. Under the construction of an equivariant estimator and an invariant loss function with respect to transformation, the corresponding risk of such a decision or estimator is independent of $\theta$. Furthermore, given a collection of equivariant estimators and a fixed invariant loss function, we can find an equivariant estimator with the minimum risk among all equivariant estimators, known as the **UMER**. An example of a UMER is the Pitman estimator under quadratic loss. Before introducing any more detailis, we shall provide some intuition about the neccessity of equivariant estimator and inavriant loss function in making risk independent of parameter space.

1. **Equivariant Estimator**: The idea behind the equivariant estimator is to ensure that the transformation of the data $X$ (via the operator $g$) and the estimator $\delta(X)$ behave in the same way across the entire parameter space. In other words, if you apply the transformation $g$ to the data, the structure of the estimator should transform consistently as well. This ensures that the estimator remains compatible with the parameter space $\theta$ and can be **compared** consistently across different parameter values.

2. **Loss Function**: The loss function quantifies how much the estimator deviates from the true parameter value $\theta$. This step is essentially measuring the error between the estimator $\delta(X)$ and the true parameter $\theta$. The loss function essentially "subtracts" the true parameter from the estimator to determine how much deviation there is.

3. **Invariant Loss Function**: The invariance of the loss function ensures that the way we measure the deviation between the estimator and the true parameter remains consistent, no matter which $\theta$ is involved. That is, if we apply a transformation $g$, the loss function remains the same (invariant) for both the transformed parameter $g\theta$ and the original parameter $\theta$. This invariance guarantees that **the measurement of the deviation is uniform** across all $\theta$, which makes the **risk** (expected loss) independent of $\theta$.


First, we look at how to construct an **UMRE** estimator.

## **Theorem: Uniformly Minimum Risk Estimator (UMRE) Construction**

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

The following is attempt to provide more underlying intepretation of this theorem.

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

## Special case of UMRE: Pitman estimator

We call the UMRE as **Pitman estimator** when we conside the loss function as quadratic loss function. i.e, $L(\theta,a)=(\theta-a)^2$.

If we know the density of $\epsilon$ w.r.t lebesgue measure. Then we have a URME statistic as following:

$$
E(\epsilon_n | Y) = \frac{\int z \, p_0(X_1 -z, \dots, X_{n-1} - z, z) \, du}{\int p_0(X_1 -z, \dots, X_{n-1} - z, z) \, dz}.
$$


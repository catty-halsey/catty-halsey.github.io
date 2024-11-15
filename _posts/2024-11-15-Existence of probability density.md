---
layout: post
title: "Existence of probability density"
author: "Ziyan Li"
categories: tutorials
tags: [documentation, sample]
---
Under lots of statistical setting, we assume density exists. However, in practical, the probability density is not always exists. In this blog, we attempt to illustrate the next three questions:
- When it will exist?
- Why it might not exits? 
- What can we do when the probability density does not exist?
---

## **1. When Does a Density Exist?**
For a density $f(x)$ to exist, the measure $P$ must be **absolutely continuous** with respect to the reference measure $\mu$ (often the Lebesgue measure $\lambda$ in probability theory). Absolute continuity means:

$$
\mu(A) = 0 \implies P(A) = 0, \quad \text{for all measurable sets } A.
$$

If $P$ is absolutely continuous with respect to $\mu$, the Radon-Nikodym theorem guarantees the existence of a density $f(x)$ such that:

$$
P(A) = \int_A f(x) \, d\mu.
$$

where we write $f(x)=\frac{dP}{d\mu}$.

Remark:
- In probability theory, the density function $f(x)$ describes how the probability mass of $P$ is distributed across the real line. It assigns a "weight" to each infinitesimal partition of the real line, as defined with respect to the Lebesgue measure. A high value of $f(x)$ indicates that $P$ concentrates more probability mass around $x$.
- The existence of $f(x)$ requires $P$ to be **absolutely continuous** with respect to the Lebesgue measure. This assumption ensures that $P$ can be expressed as $P(A) = \int_A f(x) \, d\lambda(x)$ for measurable sets $A$.

---

## **2. Why Might a Density Not Exist?**
From the above remarks, we know that a density does not exist if $P$ is **not absolutely continuous** with respect to $\mu$. This happens when there are sets $A$ with:

$$
\mu(A) = 0 \quad \text{but} \quad P(A) > 0.
$$

In such cases, $P$ and $\mu$ are said to have a **singular** relationship. Here's why:

1. **Discrete Measures**:
   If $P$ is discrete (e.g., concentrates probability mass on a countable set like $\{x_1, x_2, \dots\}$), then it is singular with respect to the Lebesgue measure. For instance:
   - $P(x = x_1) = 1$ means all the mass is concentrated at a single point, but the Lebesgue measure of a single point is $0$.
   - No density $f(x)$ can represent this, because a density describes "mass spread continuously" across the space.

2. **Singular Measures**:
   A measure $P$ is singular with respect to $\mu$ if it is concentrated on a set of $\mu$-measure $0$. For example:
   - If $P$ is supported entirely on the Cantor set (a set of Lebesgue measure $0$), it is singular with respect to $\lambda$, and no density exists.

3. **Mixed Measures**:
   If $P$ has both discrete and continuous components, it cannot be expressed purely in terms of a density relative to $\lambda$. Instead, it must be decomposed:
   
$$
P = P_{\text{continuous}} + P_{\text{discrete}},
$$
   
   where only $P_{\text{continuous}}$ has a density.

### **2.1. Examples**
1. **Discrete Probability Distribution**:
   - Consider $P$ defined on $\mathbb{R}$ with all its mass at $x = 1$. Here:
   
$$
P(A) = 
\begin{cases}
   1, & \text{if } 1 \in A, \\
   0, & \text{otherwise.}
\end{cases}
$$

$P$ has no density with respect to $\lambda$, because $\lambda(\{1\}) = 0$, yet $P(\{1\}) = 1$.

2. **Cantor Distribution**:
   - The uniform distribution on the Cantor set is singular with respect to $\lambda$. The Cantor set has $\lambda$-measure $0$, so no density exists for $P$ with respect to $\lambda$.

3. **Mixture of Continuous and Discrete**:
   - Suppose $P$ assigns half its mass to a point ($P(x = 1) = 0.5$) and spreads the other half continuously over $[0, 1]$. The density exists for the continuous part, but not for the discrete part.


---

### **3. How to Handle Such Cases**
1. **Measure Decomposition**:
   The **Lebesgue decomposition theorem** allows $P$ to be split into:
   
   $$
   P = P_{\text{ac}} + P_{\text{sing}},
   $$
   
   where:
   - $P_{\text{ac}}$ (absolutely continuous part) has a density $f(x)$.
   - $P_{\text{sing}}$ (singular part) does not.

3. **Choosing a Suitable Reference Measure**:
Choosing a suitable reference measure can indeed address the issue of defining a density when the original reference measure (e.g., the Lebesgue measure) leads to problems. Here’s an example to illustrate this:

Consider a discrete probability distribution $P$ on $\mathbb{R}$, where all the probability mass is concentrated on a countable set $S = \{x_1, x_2, x_3, \dots\}$. Let:

$$
P(x_i) = p_i, \quad \text{with} p_i > 0 \text{and} \sum_{i=1}^\infty p_i = 1.
$$

If we attempt to express $P$ in terms of a density with respect to the Lebesgue measure $\lambda$, we encounter a problem because:

$$
\lambda(\{x_i\}) = 0, \quad \text{and yet} P(\{x_i\}) = p_i.
$$

This violates the requirement for absolute continuity with respect to $\lambda$, and no density $f(x)$ can exist.


#### **Solution: Choosing a Suitable Reference Measure**
Instead of using the Lebesgue measure, we can choose a reference measure $\mu$ that assigns positive measure to the points in $S = \{x_1, x_2, \dots\}$. A natural choice is:

$$
\mu(\{x_i\}) = 1 \quad \text{for each } x_i \in S.
$$

Now, $P$ is absolutely continuous with respect to $\mu$, and the density $f(x)$ exists and is given by:

$$
f(x_i) = \frac{P(\{x_i\})}{\mu(\{x_i\})} = p_i.
$$

For measurable subsets $A \subseteq S$, we can write:

$$
P(A) = \sum_{x_i \in A} p_i = \int_A f(x) \, d\mu.
$$


#### **Applications**
1. **Dirac Measures**: When $P$ is supported on a finite or countable set, use a reference measure $\mu$ that assigns positive mass to each point in the support.
2. **Hybrid Measures**: For measures with both discrete and continuous components, use a mixed reference measure (e.g., combining Dirac measures and Lebesgue measure).
3. **Custom Models**: In physics or Bayesian statistics, reference measures can be tailored to the problem domain (e.g., using prior measures in Bayesian inference).

---

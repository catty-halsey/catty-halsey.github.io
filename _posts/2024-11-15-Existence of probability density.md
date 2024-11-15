---
layout: post
title: "Existence of probability density"
author: "Ziyan Li"
categories: tutorials
tags: [documentation, sample]
---
Under lots of statistical setting, we assume density exists. However, in practical, the probability density is not always exists. In this blog, we attempt to illustrate why it
### **1. When Does a Density Exist?**
For a density \(f(x)\) to exist, the measure \(P\) must be **absolutely continuous** with respect to the reference measure \(\mu\) (often the Lebesgue measure \(\lambda\) in probability theory). Absolute continuity means:
\[
\mu(A) = 0 \implies P(A) = 0, \quad \text{for all measurable sets } A.
\]
If \(P\) is absolutely continuous with respect to \(\mu\), the Radon-Nikodym theorem guarantees the existence of a density \(f(x)\) such that:
\[
P(A) = \int_A f(x) \, d\mu.
\]

---

### **2. Why Might a Density Not Exist?**
A density does not exist if \(P\) is **not absolutely continuous** with respect to \(\mu\). This happens when there are sets \(A\) with:
\[
\mu(A) = 0 \quad \text{but} \quad P(A) > 0.
\]

In such cases, \(P\) and \(\mu\) are said to have a **singular** relationship. Here's why:

1. **Discrete Measures**:
   If \(P\) is discrete (e.g., concentrates probability mass on a countable set like \(\{x_1, x_2, \dots\}\)), then it is singular with respect to the Lebesgue measure. For instance:
   - \(P(x = x_1) = 1\) means all the mass is concentrated at a single point, but the Lebesgue measure of a single point is \(0\).
   - No density \(f(x)\) can represent this, because a density describes "mass spread continuously" across the space.

2. **Singular Measures**:
   A measure \(P\) is singular with respect to \(\mu\) if it is concentrated on a set of \(\mu\)-measure \(0\). For example:
   - If \(P\) is supported entirely on the Cantor set (a set of Lebesgue measure \(0\)), it is singular with respect to \(\lambda\), and no density exists.

3. **Mixed Measures**:
   If \(P\) has both discrete and continuous components, it cannot be expressed purely in terms of a density relative to \(\lambda\). Instead, it must be decomposed:
   \[
   P = P_{\text{continuous}} + P_{\text{discrete}},
   \]
   where only \(P_{\text{continuous}}\) has a density.

---

### **3. Practical Examples**
1. **Discrete Probability Distribution**:
   - Consider \(P\) defined on \(\mathbb{R}\) with all its mass at \(x = 1\). Here:
     \[
     P(A) = 
     \begin{cases}
       1, & \text{if } 1 \in A, \\
       0, & \text{otherwise.}
     \end{cases}
     \]
     \(P\) has no density with respect to \(\lambda\), because \(\lambda(\{1\}) = 0\), yet \(P(\{1\}) = 1\).

2. **Cantor Distribution**:
   - The uniform distribution on the Cantor set is singular with respect to \(\lambda\). The Cantor set has \(\lambda\)-measure \(0\), so no density exists for \(P\) with respect to \(\lambda\).

3. **Mixture of Continuous and Discrete**:
   - Suppose \(P\) assigns half its mass to a point (\(P(x = 1) = 0.5\)) and spreads the other half continuously over \([0, 1]\). The density exists for the continuous part, but not for the discrete part.

---

### **4. Why Does This Matter?**
The absence of a density complicates mathematical modeling and analysis:
- **No density function \(f(x)\):** Without a density, you cannot compute probabilities as integrals of \(f(x)\).
- **Radon-Nikodym theorem doesn't apply:** Many theorems assume absolute continuity and fail for singular measures.
- **Complexity in decomposition:** You must separate the measure into discrete and continuous components.

---

### **5. How to Handle Such Cases**
1. **Measure Decomposition**:
   The **Lebesgue decomposition theorem** allows \(P\) to be split into:
   \[
   P = P_{\text{ac}} + P_{\text{sing}},
   \]
   where:
   - \(P_{\text{ac}}\) (absolutely continuous part) has a density \(f(x)\).
   - \(P_{\text{sing}}\) (singular part) does not.

2. **Choosing a Suitable Reference Measure**:
   In some cases, using a different reference measure \(\mu\) (e.g., one that assigns mass to points) can resolve the issue.

---

### **6. Summary**
A density might not exist when:
- \(P\) is singular with respect to \(\mu\) (e.g., \(P\) is discrete or supported on a set of \(\mu\)-measure \(0\)).
- \(P\) has mixed components (both continuous and discrete).

The existence of a density is tied to the relationship between the measure \(P\) and the reference measure \(\mu\). When a density does exist, it greatly simplifies probability computations and analysis.

---
layout: post
title: "Why sigma-finite measure is important?"
author: "Ziyan Li"
categories: journal
tags: [documentation, sample]
---


### **1. σ-Finiteness of the Lebesgue Measure**

The **Lebesgue measure** $\mu$ on $\mathbb{R}$ (the real line) is **σ-finite**. This means that the real line can be divided into a **countable** collection of subsets, each with **finite measure**. In simpler terms:
- You can split $\mathbb{R}$ into an infinite sequence of sets $\{ A_n \}_{n=1}^{\infty}$ such that each set $A_n$ has finite Lebesgue measure ($\mu(A_n) < \infty$).

This property is crucial for many important results in measure theory and integration. The fact that the measure is σ-finite allows us to apply powerful theorems like **Fubini's theorem** and **Tonelli's theorem** for changing the order of integration in multiple integrals. These theorems require the measure to be σ-finite to ensure that the integrals can be split into simpler components.

#### **Why σ-Finiteness Matters for Integration:**
- **Fubini’s theorem**: It says that when integrating over a product of two spaces, we can interchange the order of integration, i.e., $\int_{\mathbb{R}^2} f(x, y) \, d(x, y) = \int_{\mathbb{R}} \left( \int_{\mathbb{R}} f(x, y) \, dy \right) dx$.
  - For this to work, the underlying measure (in this case, Lebesgue measure) must be σ-finite.
- **Tonelli's theorem**: This is another theorem related to non-negative functions that lets us swap the order of summation or integration, again relying on the σ-finiteness of the measure.

---

### **2. The Radon-Nikodym Derivative and Absolute Continuity**

The **Radon-Nikodym theorem** guarantees the existence of a **density function** (a measurable function $f : \mathbb{R} \to [0, \infty)$) when one measure $\nu$ is **absolutely continuous** with respect to another measure $\mu$ (often Lebesgue measure in probability). This allows us to represent one measure as a "scaled version" of another.

- If $\nu \ll \mu$ (i.e., $\nu$ is absolutely continuous with respect to $\mu$), then there exists a function $f = \frac{d\nu}{d\mu}$ such that for any measurable set $A$,
  
$$
\nu(A) = \int_A f(x) \, d\mu(x).
$$
  
This is essentially the **Radon-Nikodym derivative**, and it provides the **density** $f(x)$, which tells us how the measure $\nu$ is distributed with respect to the Lebesgue measure.

---

### **3. Practical Handling of Infinite Measures**

Even though the **Lebesgue measure** of $\mathbb{R}$ is infinite (since $\mu(\mathbb{R}) = \infty$), **σ-finiteness** allows us to handle infinite measures in a controlled manner. 

- We can **decompose** $\mathbb{R}$ into countably many subsets, each of which has finite measure, making the integration process mathematically feasible. This is one of the reasons why the **Lebesgue integral** is so powerful: it can handle measures on infinite sets by breaking them down into manageable parts.

For instance:
- Even though we can't assign a finite value to the Lebesgue measure of the whole real line $\mathbb{R}$, we can still perform integrals like:
  
$$
\int_{\mathbb{R}} f(x) \, d\mu(x),
$$

  because we know we can break $\mathbb{R}$ into subsets (like $[-n, n]$ for each $n \in \mathbb{N}$) where each part has finite measure.

---

### **4. Riemann Integral vs. Lebesgue Integral and Measure Theory**

#### **Riemann Integral:**
The **Riemann integral** is defined for functions over an interval $[a, b]$ where the **partitioning** of the interval into subintervals is used to approximate the integral. However, there are some limitations:
- The **Riemann integral** works well for **bounded** functions over **finite intervals** but fails when dealing with more complex measures, like those involving unbounded functions or infinite sets.
- For example, if a function is highly irregular (e.g., discontinuous) or takes infinite values over a set of measure zero, the Riemann integral can fail to converge.

#### **Lebesgue Integral:**
On the other hand, the **Lebesgue integral** works much better when dealing with more general measures. It integrates **functions with respect to a measure** (not just the interval length), which makes it more flexible.
- The **Lebesgue measure** is capable of integrating over sets where the Riemann approach might fail, especially when the function is not well-behaved over certain subsets.
- The **Lebesgue integral** can handle infinite measures (such as the entire real line) due to the σ-finiteness of the Lebesgue measure.

In essence:
- **Riemann integral** deals with partitions of a domain into intervals (but has trouble with more general, infinite cases).
- **Lebesgue integral** deals with the measure assigned to sets, allowing it to handle infinite and more complex measures (like the Lebesgue measure on $\mathbb{R}$).

---



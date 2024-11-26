---
layout: post
title: "Convergence of Random variables"
author: "Ziyan Li"
categories: tutorials
tags: [documentation, sample]
---


### **1. Definition of Almost Sure Convergence:**

- \( X_n \xrightarrow{a.s.} X \) means:
  \[
  P\left( \lim_{n \to \infty} X_n(\omega) = X(\omega) \right) = 1.
  \]
  This means that for almost every outcome \( \omega \in \Omega \), the sequence \( X_n(\omega) \) gets arbitrarily close to \( X(\omega) \) as \( n \to \infty \).

- **Key Point:** There is no requirement that \( X_n(\omega) \) must be bounded. It can take arbitrarily large values at some steps and still converge to \( X(\omega) \).

---

### **2. Why Can \( X_n \) Be Unbounded?**

Almost sure convergence focuses on the **eventual behavior** of the sequence for almost every outcome, but doesn't control the **intermediate values**. Thus, even if the sequence \( X_n \) occasionally takes very large values, as long as it eventually approaches \( X \) for almost all outcomes, it will still be considered a.s. convergent.

---

### **3. Example: Unbounded Sequence with a.s. Convergence**

Consider the sequence:
\[
X_n(\omega) = 
\begin{cases} 
n & \text{if } \omega \in \left( 0, \frac{1}{n} \right], \\
0 & \text{if } \omega \in \left( \frac{1}{n}, 1 \right].
\end{cases}
\]

- **Behavior:** For each \( \omega \):
  - If \( \omega \in \left( 0, \frac{1}{n} \right] \), \( X_n(\omega) \) grows without bound as \( n \to \infty \).
  - However, for each fixed \( \omega \), eventually \( \omega \notin \left( 0, \frac{1}{n} \right] \) as \( n \) becomes large. Hence, \( X_n(\omega) \to 0 \) almost surely.

- **Conclusion:** \( X_n \to 0 \) a.s., but \( X_n \) is unbounded for small values of \( \omega \).

---

### **4. Why This Matters:**

- In real-world scenarios, **unbounded sequences** are common in stochastic processes, where large values may occur with small probabilities.
- Even though the sequence might have large fluctuations or spikes, almost sure convergence only requires it to settle down eventually for most outcomes.

---

### **Implication for \(L^p\) Convergence:**

- **\(L^p\) convergence** requires controlling the **size** of the sequence, not just its limit.
  - If \( X_n \) is unbounded, \( \mathbb{E}(|X_n - X|^p) \) can diverge, preventing \(L^p\) convergence.
  - Thus, almost sure convergence does not imply \(L^p\) convergence unless there is an additional bound or condition like **uniform integrability**.
 

### **1. What Does \( \mathbb{E}(|X_n - X|^p) \) Represent?**

- The expectation \( \mathbb{E}(|X_n - X|^p) \) measures the **average size** of the difference between \( X_n \) and \( X \), raised to the power \( p \).
- For this expectation to be finite, the **tail behavior** of the random variable \( |X_n - X|^p \) must decay fast enough to offset large values.

---

### **2. Why Large Values Cause Divergence:**

- If \( X_n \) can take **large values** with **non-negligible probability**, then \( |X_n - X|^p \) can become very large.
  - Even if these large values occur rarely, their contribution to the expectation can still be significant if \( p \) is large.
- In particular, the integral:
  \[
  \mathbb{E}(|X_n - X|^p) = \int_{\Omega} |X_n(\omega) - X(\omega)|^p \, dP(\omega)
  \]
  can diverge if the probability of large deviations doesn't decay quickly enough.

---

### **3. Example: Divergence with Unbounded \( X_n \)**

Consider the random variable \( X_n \) defined as:
\[
X_n(\omega) = 
\begin{cases} 
n & \text{with probability } \frac{1}{n}, \\
0 & \text{with probability } 1 - \frac{1}{n}.
\end{cases}
\]
Let \( X = 0 \) (constant).

- **Almost Sure Convergence:**  
  For each fixed \( \omega \), the probability that \( X_n(\omega) \neq 0 \) decreases as \( n \to \infty \). So, \( X_n \to 0 \) a.s.

- **Expectation Calculation:**  
  Let's compute \( \mathbb{E}(|X_n - X|^p) \):
  \[
  \mathbb{E}(|X_n|^p) = n^p \cdot \frac{1}{n} = n^{p-1}.
  \]
  If \( p > 1 \), this expectation **diverges** as \( n \to \infty \) because \( n^{p-1} \to \infty \).

- **Conclusion:**  
  Even though \( X_n \) converges almost surely to 0, the large values of \( X_n \) contribute too much to the expectation, causing divergence.

---

### **4. Intuition: Heavy Tails and Divergence**

- **Heavy-tailed distributions:** If the probability distribution of \( X_n \) has a heavy tail (large values occur with non-negligible probability), then the expectation \( \mathbb{E}(|X_n - X|^p) \) can diverge.
- **Role of \( p \):** The larger \( p \) is, the more sensitive the expectation is to large values:
  - For large \( p \), even small probabilities of large values can lead to divergence.
  - For smaller \( p \), the expectation is less sensitive to large values.

---

### **Key Takeaway:**
- **Unboundedness of \( X_n \)** means that \( |X_n - X|^p \) can take large values, and if these values occur often enough or are large enough, the expectation \( \mathbb{E}(|X_n - X|^p) \) can diverge.
- This is why almost sure convergence (which doesn't control the size of the random variables) doesn't imply \( L^p \) convergence without additional conditions, such as boundedness or uniform integrability.



### **1. The Example: \( X_n \sim \text{Bernoulli}(1/n) \)**

- \( X_n \) is a random variable following a **Bernoulli distribution** with success probability \( 1/n \). So:
  \[
  P(X_n = 1) = \frac{1}{n}, \quad P(X_n = 0) = 1 - \frac{1}{n}.
  \]
  
- **Intuition:**
  - As \( n \to \infty \), the probability of \( X_n = 1 \) becomes very small. So, for large \( n \), \( X_n \) takes the value 1 with very low probability and takes the value 0 most of the time.
  - However, for any individual \( \omega \), there is still a **nonzero probability** that \( X_n(\omega) \) equals 1 for some large \( n \). This means that \( X_n \) does not converge almost surely to 0.

---

### **2. \( X_n \) Converging in \( L^2 \) to 0**

To check convergence in \( L^2 \), we need to compute \( \mathbb{E}[(X_n - 0)^2] = \mathbb{E}[X_n^2] \), because \( X_n \) takes only values 0 or 1:

\[
\mathbb{E}[X_n^2] = \mathbb{E}[X_n] = \frac{1}{n}.
\]

So,

\[
\mathbb{E}[X_n^2] = \frac{1}{n}.
\]

- **Convergence in \( L^2 \):**
  \[
  \lim_{n \to \infty} \mathbb{E}[X_n^2] = \lim_{n \to \infty} \frac{1}{n} = 0.
  \]
  This shows that \( X_n \) converges to 0 in \( L^2 \) because the \( L^2 \) norm of the difference \( X_n - 0 \) goes to 0 as \( n \to \infty \).

---

### **3. Almost Sure Convergence**

For almost sure convergence, we need to check if \( X_n \) converges to 0 with probability 1 as \( n \to \infty \).

- For each \( \omega \), \( X_n(\omega) \) equals 1 with probability \( \frac{1}{n} \), and 0 with probability \( 1 - \frac{1}{n} \).
  
- **Borel-Cantelli Lemma:**
  If we want to know whether \( X_n \) converges to 0 almost surely, we can apply the **Borel-Cantelli Lemma**. The lemma states that if the sum of the probabilities \( \sum_{n=1}^\infty P(X_n = 1) \) is finite, then \( X_n = 1 \) happens only finitely many times almost surely. In this case:

  \[
  \sum_{n=1}^\infty P(X_n = 1) = \sum_{n=1}^\infty \frac{1}{n} = \infty.
  \]

  - Since this series diverges, the Borel-Cantelli Lemma tells us that \( X_n = 1 \) happens infinitely often with probability 1.
  - Therefore, \( X_n \) **does not converge to 0 almost surely**, because there will always be infinitely many values of \( n \) where \( X_n = 1 \).

---

### **Conclusion**

- **Convergence in \( L^2 \):** \( X_n \to 0 \) in \( L^2 \), because \( \mathbb{E}[X_n^2] = 1/n \) converges to 0.
- **No Almost Sure Convergence:** \( X_n \) does not converge to 0 almost surely, because \( X_n = 1 \) infinitely often with probability 1.

### **Why is this a counterexample?**

This example shows that **convergence in \( L^2 \)** (or even \( L^p \) for \( p \geq 1 \)) **does not imply almost sure convergence**. In fact, \( X_n \) converges in \( L^2 \) but does not converge almost surely because the random variables \( X_n \) still "jump" between 0 and 1 infinitely often, despite the fact that the expected size of these jumps diminishes as \( n \) increases.

---

This is a good demonstration of how convergence in expectation (or \( L^p \) spaces) doesn't necessarily imply the stronger form of convergence required for almost sure convergence.




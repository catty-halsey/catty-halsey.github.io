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



- **Bounded in probability** means that the random variable \( Z_n \) stays within some finite range with high probability as \( n \) becomes large. More formally, for any \( \epsilon > 0 \), we have:

\[
\lim_{M \to \infty} \limsup_{n \to \infty} P(\|Z_n\| > M) = 0
\]

This condition is satisfied if the tail probability of \( Z_n \) decays faster than \( 1/n \), such as \( 1/n^2 \) or faster. This decay ensures that the sequence of random variables does not grow too large with probability.

- If the tail probability decays **slower** than \( 1/n \) (for example, like \( 1/\sqrt{n} \) or \( 1/n \)), the sequence is **not** bounded in probability. For example, the random walk \( X_n \) that we discussed earlier does not decay fast enough to be bounded in probability.

### Intuition in simple terms:
- If the probability of a random variable \( Z_n \) taking a value larger than some threshold \( M \) decays **fast enough** (like \( 1/n^2 \) or faster), we can say that \( Z_n \) is "bounded" in probability and does not grow without bound.
- If the decay rate is too slow (like \( 1/\sqrt{n} \) or slower), then \( Z_n \) can grow larger as \( n \) increases, so it is **not bounded in probability**.

### Example of fast decay (bounded in probability):
- A sequence of random variables where each \( Z_n \) has a tail probability decaying like \( 1/n^2 \) or faster would be bounded in probability because the probability of large deviations decreases very quickly as \( n \) increases.

### Example of slow decay (not bounded in probability):
- A sequence like the simple random walk \( X_n \) discussed earlier, where the tail probability decays like \( 1/\sqrt{n} \), is not bounded in probability because it does not decrease fast enough to keep the random variable within a fixed range as \( n \) grows large.


### Example: Random Walk

Consider the sequence of random variables \( (X_n) \) defined by a simple **random walk**. Let \( X_n \) be the sum of \( n \) independent and identically distributed (i.i.d.) random variables \( \epsilon_i \), where each \( \epsilon_i \) is a random variable taking values \( \pm 1 \) with equal probability (i.e., \( P(\epsilon_i = 1) = P(\epsilon_i = -1) = 0.5 \)):

\[
X_n = \sum_{i=1}^{n} \epsilon_i
\]

#### 1. **Growth of \( X_n \)**:
- The random walk \( X_n \) describes a process where, at each step, the value of \( X_n \) can either increase or decrease by 1, depending on the outcome of \( \epsilon_i \).
- Over time, the value of \( X_n \) can grow large in either the positive or negative direction, and the variance of \( X_n \) increases with \( n \).

#### 2. **Behavior of \( X_n \) as \( n \to \infty \)**:
- The distribution of \( X_n \) is roughly normal with mean 0 and variance \( n \), i.e., \( X_n \sim \mathcal{N}(0, n) \) asymptotically as \( n \) increases (due to the central limit theorem).
- The probability that \( |X_n| > M \) (the random walk exceeds a large threshold \( M \)) will decay slowly as \( n \) increases, but it does **not** converge to 0 quickly enough to satisfy the condition for boundedness in probability.

#### 3. **Probability Condition**:
Let's check whether \( X_n \) satisfies the boundedness in probability condition:

\[
\lim_{M \to \infty} \limsup_{n \to \infty} P(\|X_n\| > M) = 0
\]

- Since \( X_n \) grows approximately like \( \sqrt{n} \), the probability that \( |X_n| \) exceeds a large value \( M \) behaves like:

\[
P(|X_n| > M) \sim 2 \left( 1 - \Phi\left( \frac{M}{\sqrt{n}} \right) \right)
\]

where \( \Phi \) is the cumulative distribution function (CDF) of the standard normal distribution. For large \( n \), this probability decays slower than \( 1/n \), meaning that \( X_n \) is not bounded in probability.

#### 4. **Conclusion**:
- As \( n \to \infty \), \( P(\|X_n\| > M) \) does not tend to 0 quickly enough, and \( X_n \) grows without bound in probability.
- This violates the definition of boundedness in probability, as \( X_n \) does not remain within any fixed range with high probability as \( n \) increases.

### Why Is It Not Bounded in Probability?

- The random walk \( X_n \) does not have a bound that holds with high probability as \( n \) increases.
- The random variable grows without bound, and even though the probability of large deviations from 0 decreases with \( n \), it does not decay fast enough to make \( X_n \) bounded in probability.
- More formally, for large \( M \), the tail probabilities \( P(|X_n| > M) \) do not approach 0 fast enough, and thus the sequence does not satisfy the condition for boundedness in probability.

This provides an example of a random variable that **is not bounded in probability**.


---
lawet: post
title: "The Metropolis-Hastings"
author: "Ziyan Li"
categories: journal
tags: [documentation, sample]
---


The Metropolis-Hastings algorithm is a cornerstone method in Markov Chain Monte Carlo (MCMC) for sampling from a target distribution $\pi$, even when direct sampling is infeasible. The brilliance of the algorithm lies in its design of the acceptance ratio $a(x, y)$, which, combined with the proposal distribution $Q(x, y)$, ensures that the Markov chain converges to the desired stationary distribution. The acceptance ratio is defined as $a(x, y) = \min\left(1, \frac{\pi(y) Q(y, x)}{\pi(x) Q(x, y)}\right)$, and its role is to correct for discrepancies between the proposal $Q$ and the target $\pi$. By carefully filtering proposed transitions, $a(x, y)$ ensures that only those candidate states $y$ which maintain the balance equation $\pi(x) P(x, dy) = \pi(y) P(dy, x)$ are accepted, where $P(x, dy)$ is the transition kernel that combines $Q(x, y)$ with $a(x, y)$. This clever design means that the accepted states automatically satisfy the balance equation, guaranteeing that the chain converges to $\pi$ over time.

Intuitively, if the ratio $\frac{\pi(y) Q(y, x)}{\pi(x) Q(x, y)}$ exceeds 1, meaning the proposed state $y$ is more likely under $\pi$ than the current state $x$, then $y$ is always accepted. Conversely, if the ratio is less than or equal to 1, $y$ is accepted with a probability proportional to the ratio, which prevents bias and ensures the chain properly explores $\pi$. This automatic adjustment is the key insight of the algorithm, transforming any mismatched proposal $Q$ into a valid kernel $P$ that respects the target distribution. Consequently, the $a(x, y)$ design not only ensures convergence to $\pi$ but also facilitates efficient exploration of the state space.

1. **Theoretical Role of $P(x, dy)$**:
   - The kernel $P(x, dy)$ is defined as a combination of the proposal $Q(x, dy)$ and the acceptance function $a(x, y)$, plus the self-loop term $r(x)\delta_x(dy)$. This ensures that:
     - The Markov chain is stationary with respect to $\pi(x)$ (satisfying detailed balance).
     - $P(x, dy)$ does not need additional conditions on $Q(x, dy)$ because the theoretical self-loop ensures irreducibility in some cases.
   - Therefore, both terms of $P$—the accepted proposals $a(x, y)Q(x, dy)$ and the rejection self-loop $r(x)\delta_x(dy)$—are crucial to its theoretical validity.

2. **Practical Implementation**:
   - In practice, we only implement the first term indirectly:
     - Use $Q(x, dy)$ to propose transitions.
     - Apply $a(x, y)$ to accept or reject the proposal.
     - Rejections implicitly handle the self-loop $r(x)\delta_x(dy)$, ensuring that the practical chain matches $P(x, dy)$ without explicitly constructing it.

3. **Irreducibility and the Role of $Q(x, dy)$**:
   - Theoretical $P(x, dy)$ does not require $Q(x, dy)$ to be irreducible, as the self-loop can help the chain stay connected.
   - In practice, however, we do not explicitly construct the self-loop. This makes the irreducibility of $Q(x, dy)$ essential to ensure that the chain can explore the entire state space. Without this property, the Markov chain might get stuck, breaking ergodicity.

4. **Transfer of Properties**:
   - By requiring $Q(x, dy)$ to be irreducible in practice, we effectively "transfer" the irreducibility property from $P(x, dy)$ (in theory) to $Q(x, dy)$ (in practice). This makes up for the absence of an explicit self-loop during simulations.
   - $a(x, y)$, on the other hand, ensures that the stationary distribution of $P(x, dy)$ matches $\pi(x)$, so this aspect of $P(x, dy)$ is still directly realized in practice.

5. **Why It Works**:
   - While the first term of $P(x, dy)$ (i.e., $a(x, y)Q(x, dy)$) alone may appear stationary, it does not inherently ensure irreducibility. The full kernel $P(x, dy)$ guarantees both stationary and irreducibility without extra conditions.
   - In simulations, we rely on $a(x, y)$ to enforce stationarity and add a practical requirement on $Q(x, dy)$ to ensure irreducibility. This "two-part" approach mirrors the two terms in $P(x, dy)$.

---

### **1. Structure of the Metropolis-Hastings Kernel**
The transition kernel in the Metropolis-Hastings algorithm is defined as:

\[
P(x, A) = \int_A a(x, y) Q(x, dy) + 1_A(x) \left[1 - \int_X a(x, y) Q(x, dy)\right],
\]

where:

1. $\int_A a(x, y) Q(x, dy)$: Represents the probability of transitioning from $x$ to any state $y \in A$, accounting for both the proposal $Q(x, dy)$ and the acceptance probability $a(x, y)$.

2. $1_A(x) \left[1 - \int_X a(x, y) Q(x, dy)\right]$: Represents the probability of staying at $x$ (the self-loop), provided $x \in A$. The term $1_A(x)$ ensures this contribution is included only if $x \in A$.

---
 **Integration over $X \setminus \{x\}$:** 
   - In the first term $\int_A a(x, y) Q(x, dy)$, the integral typically considers proposals $y$ over the entire state space $X$. However, the acceptance probability $a(x, y)$ naturally excludes cases where $y = x$, since $Q(x, dy)$ doesn’t propose staying at $x$.
   - This term handles transitions to $y \neq x$.

- **Self-Loop for $x \in A$:**
   - The self-loop term $1_A(x)$ accounts for the probability of staying at $x$. This happens if $x \in A$ and all proposals $y \neq x$ are rejected. The rejection probability is given by:
     \[
     r(x) = 1 - \int_X a(x, y) Q(x, dy),
     \]
     which is the complement of the total acceptance probability.

   - To ensure $P(x, A)$ includes this probability, we check whether $x \in A$ using the indicator $1_A(x)$. If $x \notin A$, the self-loop contribution is zero.

### **3. Why Not Use $1_A(y)$ for the Self-Loop?**
The self-loop contribution is not associated with $y$, because the self-loop corresponds to staying at the current state $x$. In this case:
- The kernel contributes a probability mass at $x$, not $y$, because the chain does not transition to any new state when the proposal is rejected.
- $1_A(y)$ would incorrectly suggest that the self-loop depends on $y$, which it doesn’t.

Thus, the correct formulation uses $1_A(x)$, as it checks whether the current state $x$ is part of the set $A$, and only then adds the self-loop probability.

---

### **4. The Role of $1_A(x)$ in $P(x, A)$**
In $P(x, A)$, the indicator $1_A(x)$ ensures that the self-loop term contributes to the transition probability **only when $x \in A$**. If $x \notin A$, the self-loop contribution is zero, and the kernel relies entirely on the first term (proposals and acceptances).

This distinction is important because:
- The first term $\int_A a(x, y) Q(x, dy)$ handles transitions to $y \neq x$.
- The second term $1_A(x) r(x)$ ensures the kernel is well-defined by including the self-loop only when $x \in A$.

---

### **5. Intuition: Splitting the Transition Kernel**
The kernel $P(x, A)$ splits the total probability into contributions from transitions to new states ($y \neq x$) and self-loops ($y = x$):

- For $y \neq x$: The kernel integrates over $A$ to compute the probability of transitioning to $y \in A$ based on the proposal and acceptance.
- For $y = x$: The kernel uses $1_A(x)$ to handle the case where the chain stays at $x$.

By design, $1_A(x)$ is essential to correctly handle the self-loop.



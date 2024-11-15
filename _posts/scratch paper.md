The NP-test is design for the simple test, which is most powerful test for the simple test. And when the X under the null and altervative hypothesis is exponential families, we can extend the NP test to the one-side test, which still the most powerful test. However, for the two-sided test, the NP-test does not exist. or does it exists? The UMPU is the most powerful test for the two-sided test.

prove that confidence interval of MC estimator, 
This proof sketches a way to bound the probability \( P(W_N \leq z S_N) \), where:

- \( W_N = \sqrt{N} |\hat{\theta}_N - \theta| \) represents the scaled difference between the estimator \( \hat{\theta}_N \) and the true parameter \( \theta \),
- \( S_N \) is an estimator for the standard deviation \( \sigma \),
- \( z = \Phi^{-1}(1 - \alpha / 2) \) is a critical value from the standard normal distribution for a specified confidence level \( 1 - \alpha \),
- \( \delta > 0 \) is a small constant chosen to control the bounds.

The proof aims to show that \( P(W_N \leq z S_N) \) converges to a value close to \( 1 - \alpha \) as \( N \to \infty \), helping to establish a confidence interval for \( \theta \).

### Key Steps in the Proof:

1. **Approximation Using Probability Bounds**:
   The probability \( P(W_N \leq z S_N) \) is approximated by bounding it with an event that includes \( \delta \)-control terms on the ratio \( S_N / \sigma \). This is achieved by analyzing \( P\left(W_N \leq z S_N, \left| \frac{S_N}{\sigma} - 1 \right| \leq \delta \right) \), which differs from \( P(W_N \leq z S_N) \) by at most the probability \( P\left(\left| \frac{S_N}{\sigma} - 1 \right| \geq \delta\right) \).

2. **Applying the Law of Large Numbers (LLN)**:
   By the LLN, \( S_N \) converges to \( \sigma \) as \( N \to \infty \), so \( P\left(\left| \frac{S_N}{\sigma} - 1 \right| \geq \delta\right) \to 0 \). This means the probability difference that we introduced in step 1 vanishes as \( N \) becomes large.

3. **Bounding \( P(W_N \leq z S_N) \) with \( \delta \)-Adjusted Terms**:
   When \( \left| \frac{S_N}{\sigma} - 1 \right| \leq \delta \), we have:
   - If \( W_N \leq z S_N \), then \( W_N \leq z \sigma (1 + \delta) \).
   - Similarly, if \( W_N \leq z \sigma (1 - \delta) \), then \( W_N \leq z S_N \).

   This allows us to bound the probability \( P(W_N \leq z S_N) \) in terms of probabilities involving \( W_N \) and \( \sigma \), which are easier to analyze.

4. **Taking Limits for Bounds**:
   Using these bounds, we get:
   \[
   2 \Phi(z (1 - \delta)) - 1 \leq \liminf P(W_N \leq z S_N) \leq \limsup P(W_N \leq z S_N) \leq 2 \Phi(z (1 + \delta)) - 1.
   \]

5. **Final Step as \( \delta \to 0 \)**:
   As \( \delta \to 0 \), the bounds converge to \( 2 \Phi(z) - 1 = 1 - \alpha \). This establishes that \( P(W_N \leq z S_N) \) asymptotically approaches \( 1 - \alpha \), validating the desired confidence level for \( \theta \).

### Summary

The proof uses probability bounds, the law of large numbers, and asymptotic limits to show that \( P(W_N \leq z S_N) \) converges to the target confidence level \( 1 - \alpha \) as \( N \to \infty \). This ensures that \( W_N \leq z S_N \) forms an approximate \( (1 - \alpha) \)-level confidence interval for \( \theta \).




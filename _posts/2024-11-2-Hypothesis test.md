---
layout: post
title: "Hypothesis test"
author: "Ziyan Li"
categories: journal
tags: [documentation, sample]
---

The hypothesis test allows us to test whether our sample (collected data) has certain properties. For example, we are interested in the mean, variance and other parameter of interest of one sample or two samples. In practice, we construct our test statistic to approximate the parameter of our interests. Now, the hypothesis test is provide us a tool to test whether our test statistic measure closely to our true parameter of interest or deviate from it. And if it close to the true parameter of interest, in what probability we can believe our results.

To construct a hypothesis, we first decide the null hypothesis $H_0$ against the alternative hypothesis $H_1$. Then, we need to design the test for null hypothesis.  There are two types of test, namely, the randomized test and non-randomized test. The randomized test maps $\mathscr{X}$ to the interval $[0,1]$ and the non-randomized test maps $\mathscr{X}$ to $\\{0,1\\}$. We define the significant level $\alpha$ as $\sup_{\theta \in \Theta_0} E_{\theta}[\phi(X)] \leq \alpha$. In hypothesis testing, we aim to evaluate a null hypothesis $H_0$ against an alternative hypothesis $H_1$ while controlling the probability of incorrectly rejecting $H_0$, known as the Type I error rate $\alpha$. To achieve this, we design our test function $\phi(X)$ to map observed data $X$ to $[0, 1]$, where $\phi(X) = 1$ indicates rejection of $H_0$. When the observed data is extreme or inconsistent with $H_0$, we want to classify it in the rejection region, thereby mapping these extreme values to $1$. This approach helps us control the proportion of extreme observations leading to rejection, ensuring that $E_{H_0}[\phi(X)] \leq \alpha$. This principle applies to both randomized and non-randomized tests, where the objective is to keep the likelihood of false rejections within our chosen significance level. 

Let we clarify some motivation of randomized test: In hypothesis testing, there are situations where the evidence is inconclusive—neither strongly supporting the null hypothesis $H_0$ nor providing enough evidence to reject it in favor of the alternative $H_1$. In these cases, we may use a randomized test to make a probabilistic decision. Specifically, when our test statistic produces a value that falls in this ambiguous region, we assign a probability $p$ of rejecting $H_0$. This is done through a random mechanism, such as flipping a biased coin with success probability $p$, where "success" means rejecting $H_0$. By designing $p$ to meet the condition:

$$
\mathbb{E}_{\theta \in \Theta_0}[\phi(X)] \leq \alpha,
$$

We ensure that, on average, the test's false rejection rate stays within the significance level $\alpha$ under $H_0$. This approach lets us manage "borderline" cases with a controlled chance of rejection, while still maintaining the statistical rigor of the test. After we design the test, 

The Neyman-Pearson lemma provides a way to design the most powerful test for distinguishing between two simple hypotheses H_0$ and H_1$. Suppose we have:

- Null hypothesis: $H_0: \theta = \theta_0$
- Alternative hypothesis: $H_1: \theta = \theta_1$

Note that it does not matter which parameter is larger.

- Example 1.
  Let $\Theta = \{\theta_0, \theta_1\}$, $\Theta_0 = \{\theta_0\}$ and $\Theta_1 = \{\theta_1\}$.
Furthermore, let two densities $p_{\theta_0}$ and $p_{\theta_1}$: $[0, 1] \to \mathbb{R}$ be given by

$$
p_{\theta_0}: x \mapsto
\begin{cases}
    0, & \text{for } x \in [0, 0.125] \\
    1, & \text{for } x \in (0.125, 0.75] \\
    4x - 2, & \text{for } x \in (0.75, 1]
\end{cases}
$$

$$
p_{\theta_1}: x \mapsto
\begin{cases}
    2, & \text{for } x \in [0, 0.125] \\
    1, & \text{for } x \in (0.125, 0.75] \\
    -4x + 4, & \text{for } x \in (0.75, 1]
\end{cases}
$$

We can observe the the likelihood ratio remains 1 when $x \in (0.125, 0.75)$. Assume we want to construct a NP-test at level 0.125. We need to confirm the 1 is exactly the threshold, so we can compute whether $E_{\theta_0}[\phi(X)]$ for $k>1$ and $k<1$ is less than 0.125. Then, we confirm $k=1$. Use the similar trick, we can also get the $q=0.2$. Hence, we construct the NP-test for the null hypothesis at level 0.125 as following

$$
\phi(X) = 
\begin{cases} 
1 & \text{if } \Lambda(X) > 1 \\
0.2 & \text{if } \Lambda(X) = 1 \\
0 & \text{if } \Lambda(X) < 1
\end{cases}
$$






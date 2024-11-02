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

We ensure that, on average, the test's false rejection rate stays within the significance level $\alpha$ under $H_0$. This approach lets us manage "borderline" cases with a controlled chance of rejection, while still maintaining the statistical rigor of the test. The Neyman-Pearson test is a classical randomized test.In the Neyman-Pearson test, when the likelihood ratio $\Lambda(x)$ equals some critical constant $k$, it indicates that the observed data is neither strongly supporting the null hypothesis $H_0$ nor the alternative hypothesis $H_1$. In this situation, you are at the threshold of making a decision. 

The Neyman-Pearson lemma provides a way to design the most powerful test for distinguishing between two simple hypotheses H_0$ and H_1$. Suppose we have:

- Null hypothesis: $H_0: \theta = \theta_0$
- Alternative hypothesis: $H_1: \theta = \theta_1$

The likelihood ratio test statistic $\Lambda(X)$ is defined as:

$$
\Lambda(X) = \frac{L(X | \theta_0)}{L(X | \theta_1)}
$$

where $L(X | \theta)$ is the likelihood of observing $X$ given parameter $\theta$.

The Neyman-Pearson lemma states that the most powerful test for a given significance level $\alpha$ has the form:

$$
\phi(X) = 
\begin{cases} 
1 & \text{if } \Lambda(X) \leq k \\
0 & \text{if } \Lambda(X) > k
\end{cases}
$$

where $k$ is chosen such that the test has size $\alpha$, meaning:

$$
E_{\theta_0}[\phi(X)] = P_{\theta_0}(\Lambda(X) \leq k) = \alpha
$$

In cases where $\Lambda(X) = k$ falls within a critical boundary, the test may be randomized by setting:

$$
\phi(X) = 
\begin{cases} 
1 & \text{if } \Lambda(X) < k \\
p & \text{if } \Lambda(X) = k \\
0 & \text{if } \Lambda(X) > k
\end{cases}
$$

where $p$ is chosen to satisfy the exact level $\alpha$. This approach ensures that the test maximizes the probability of correctly rejecting $H_0$ when $H_1$ is true while controlling the probability of a Type I error at $\alpha$.


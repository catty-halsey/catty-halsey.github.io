---
layout: post
title: "Two sample test"
author: "Ziyan Li"
categories: journal
tags: [documentation, sample]
---

When we have two samples $X$ and $Y$, we are interested in several things: the correlation $\rho$ between the two samples, and the difference in means $\mu$ and variances $\sigma^2$ for the two samples. Next, we introduce two hypothesis tests for each topic of interest.

### Correlation Tests

The correlation $\rho \in [-1,1]$ measures how one variable changes along with the other. In practice, we are concerned with whether there is a correlation between the two variables, i.e., $\rho \neq 0$. Additionally, due to the dual equivalence between hypothesis testing and confidence intervals, we can construct a corresponding confidence interval for the correlation. Based on our goals, we can construct the following hypothesis test:

$$
H_0: \quad \rho = 0; 
H_1: \quad \rho \neq 0
$$

So



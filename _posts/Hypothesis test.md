---
layout: post
title: "Hypothesis test"
author: "Ziyan Li"
categories: journal
tags: [documentation, sample]
---
The hypothesis test allows us to test whether our sample (collected data) has certain properties. For example, we are interested in the mean, variance and other parameter of interest of one sample or two samples. In practice, we construct our test statistic to approximate the parameter of our interests. Now, the hypothesis test is provide us a tool to test whether our test statistic measure closely to our true parameter of interest or deviate from it. And if it close to the true parameter of interest, in what probability we can believe our results.

To construct a hypothesis, we first decide the null hypothesis $H_0$ against the alternative hypothesis $H_1$. Then, we need to design the test. There are two types of test, namely, the randomized test and non-randomized test. The randomized test maps the population space to the interval $[0,1]$ and the non-randomized test maps the population space to $\\{0,1\\}$. We define the significant level $\alpha$ as $\sup_{\theta \in \Theta_0} E_{\theta}[\phi(X)] \leq \alpha$. One additional requirement when we construct the test is we want to control the type I error. More specific, we want to control the probability of false rejecting null hypothesis less than significant level. For a non-randomized test, this is equivalent to reject null hypothesis when $\phi(X)=1$.

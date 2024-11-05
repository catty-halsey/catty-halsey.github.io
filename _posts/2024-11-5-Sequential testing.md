---
layout: post
title: "Sequential testing"
author: "Ziyan Li"
categories: journal
tags: [documentation, sample]
---

**designing a payoff function for sequential hypothesis testing** with two simple hypotheses: 

- $H_0: (X_t) \sim P$
- $H_1: (X_t) \sim Q$

The goal is to test whether the observed sequence $X_1, X_2, \dots$ follows distribution $P$ (under $H_0$) or distribution $Q$ (under $H_1$), by constructing a sequence of bets or payoffs $S_t(X_t)$ that has an expected value of 1 under the null hypothesis $H_0$.

### Requirements for the Payoff Function

To set up this testing framework effectively, we require the payoff function $S_t(X_t)$ to satisfy the following condition under $H_0$:

$$
\mathbb{E}_{P}[S_t(X_t) \mid \mathcal{F}_{t-1}] = 1
$$

where $\mathcal{F}_{t-1}$ is the information (or history) up to time $t-1$, meaning all outcomes observed up to the previous test. This condition ensures that the expected payoff is fair (i.e., you expect to neither gain nor lose capital on average) when $H_0$ is true.

### Intuition Behind This Condition

This expectation constraint serves as a "fairness" requirement under $H_0$, so that:

1. **If $H_0$ is true**: You will not expect to increase or decrease your capital on average after each bet (since $\mathbb{E}_{P}[S_t(X_t) \mid \mathcal{F}_{t-1}] = 1$), maintaining a steady capital level.
2. **If $H_1$ is true**: The sequence of payoffs $S_t(X_t)$ may tend to deviate from 1, which would manifest as either a growth or decline in your cumulative capital, giving evidence against $H_0$.

This setup is akin to constructing a **martingale** (a model where the expected next value, given all previous values, is equal to the current value) under $H_0$. This martingale property is fundamental in sequential testing because if $H_0$ holds, your sequence of capital over time (after adjusting for payoffs) will neither grow nor shrink on average.

### Constructing $S_t(X_t)$

A common way to design such a payoff function $S_t(X_t)$ is by using **likelihood ratios**:

1. Define the likelihood ratio $L_t = \frac{dQ}{dP}(X_t)$, which is the Radon-Nikodym derivative of $Q$ with respect to $P$ evaluated at $X_t$. This ratio reflects how "surprising" the observed $X_t$ is under $Q$ relative to $P$.
2. Set $S_t(X_t)$ as a function of $L_t$ that satisfies the expectation condition.

For instance, you might define $S_t(X_t)$ as:

$$
S_t(X_t) = L_t
$$

This choice would ensure that:

$$
\mathbb{E}_P[S_t(X_t) \mid \mathcal{F}_{t-1}] = \mathbb{E}_P[L_t \mid \mathcal{F}_{t-1}] = 1
$$

since the expected value of the likelihood ratio $L_t$ under $P$ is 1. This setup turns your betting process into a **sequential likelihood ratio test (SLRT)**, where you assess the cumulative effect of the likelihood ratios $S_t(X_t)$ over time to draw conclusions about $H_0$ versus $H_1$.

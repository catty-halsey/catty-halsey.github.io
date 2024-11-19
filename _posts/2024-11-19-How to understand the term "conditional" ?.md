---
layout: post
title: "How to understand the term conditional?"
author: "Ziyan Li"
categories: journal
tags: [documentation, sample]
---
The concept of conditional probability is crucial in statistics. In this blog, we attempt to use measure theory to provide more intuition about the formulas related to the conditional distribution. Let us start with the simplest case: conditional probability. The definition of the conditional probability of $B$ given $A$ is:

$$
P(B|A) = \frac{P(AB)}{P(A)}.
$$

Before diving into more abstract aspect, we shall recall some knowledge from measure theory. 

A random variable $X$ serves as a bridge between two measurable spaces: the original probability space $(\Omega, \mathcal{F}, P)$ and the real line $(\mathbb{R}, \mathcal{B}(\mathbb{R}))$. Initially, the probability measure $P$ is defined on $(\Omega, \mathcal{F})$ to measure subsets of the sample space $\Omega$. By introducing $X$, a measurable function mapping $\Omega$ to $\mathbb{R}$, we connect the two spaces. This mapping partitions the sample space $\Omega$ into subsets, each corresponding to a point or interval on the real line $\mathbb{R}$, with different random variables defining different partitioning principles. Through this mapping, $X$ induces a new measure $P_X$ on $(\mathbb{R}, \mathcal{B}(\mathbb{R}))$, called the pushforward or induced measure. For any Borel set $B \subseteq \mathbb{R}$, the induced measure is defined as $P_X(B) = P(X^{-1}(B))$, where $X^{-1}(B)$ is the set of points in $\Omega$ that $X$ maps into $B$. This transformation allows us to measure subsets of $\mathbb{R}$ rather than $\Omega$. If $P_X$ is absolutely continuous with respect to the Lebesgue measure $\lambda$, it can be expressed using a density function $f_X$, such that $P_X(B) = \int_B f_X(x) \, d\lambda(x)$ for all $B \in \mathcal{B}(\mathbb{R})$. The expectation $\mathbb{E}(X)$ represents the average of $X$ on $\mathbb{R}$, weighted by the probabilities defined by $P_X$.

Now, we can use measure theory to rewrite this formula. Let $(\Omega, \mathcal{F}, P)$ be a probability space, and let $\mathscr{G} \subseteq \mathcal{F}$ be a sub-sigma algebra. Given $A \in \mathcal{F}$, if we define a measure $v$ on $\mathcal{G}$ such that $v(g) = P(A \cap g)$ for all $g \in \mathcal{G}$, then the measure $v$ is absolutely continuous with respect to $P$. By the Radon-Nikodym theorem, there exists a $\mathcal{G}$-measurable random variable (or function) $f = P(A \mid \mathcal{G}): \Omega \to \mathbb{R}$, called the conditional probability, such that:

$$
v(g) = P(A \cap g) = \int_{g} f(\omega) \, dP(\omega)
$$

for every $g \in \mathcal{G}$, and $f = \frac{dv(g)}{dP(g)} = \frac{dP(A \cap g)}{dP(g)}$ is the Radon-Nikodym derivative, which is referred to as the conditional distribution. Note that both $v$ and $P$ are $\mathcal{G}$-measurable, which makes the random variable $P(A \mid \mathcal{G})$ also $\mathcal{G}$-measurable. Intuitively, this means that the conditional distribution of $A$ given $\mathcal{G}$ depends only on the information provided by $\mathcal{G}$. This expression shows that the conditional probability $P(A \mid \mathcal{G})$ is a density function that describes how much of the measure $P(A \cap \mathcal{G})$ is concentrated in infinitesimal parts of $P(\mathcal{G})$.

Yes, your understanding is correct! Let me break it down and confirm your reasoning:


We have two random variables $X$ and $Y$, both of which are measurable with respect to their respective σ-algebras, and both have densities (whether discrete or continuous). The goal is to understand the conditional measure $P(X \mid Y)$, i.e., the measure of $X$ given $Y$.

The joint measure $P_{X,Y}$ (or $f_{X,Y}$) represents the combined behavior of both $X$ and $Y$. This measure is defined on the product space, combining the sample space for $X$ and $Y$. When we condition on $Y$, you are essentially partitioning the sample space $\Omega$ based on the value of $Y = y$. Within this partition, you're considering how $X$ behaves in each of these "subspaces". This gives you a partition of $\Omega$ that reflects the interaction between the values of $X$ and $Y$, which is captured by the joint distribution $P_{X,Y}$. The conditional distribution $P(X \mid Y = y)$ is the ratio of the joint measure $P_{X,Y}$ to the marginal measure $P_Y$ of $Y$. This ensures that we properly normalize the measure:

$$
P(X \mid Y = y) = \frac{P_{X,Y}(X, y)}{P_Y(y)}.
$$

The denominator $P_Y(y)$ is the probability (or density) of $Y = y$, ensuring the conditional measure sums to 1 over the partition corresponding to $Y = y$. Since both the numerator (joint measure) and the denominator (marginal measure of $Y$) are measurable with respect to the σ-algebra $\mathcal{F}_Y$ of $Y$, the conditional measure $P(X \mid Y)$ will also be measurable with respect to $\mathcal{F}_Y$. In other words, the conditional measure $P(X \mid Y = y)$ is a $Y$-measurable measure because the operation involves both the joint and marginal distributions, which are $Y$-measurable.


Next, we shall look at the conditional expectation. 

Given the random variable $X$, we can define a measure $Q_X$ on $\sigma(Y)$ as:

$$
Q_X(A) = \int_A X \, dP, \quad \text{for } A \in \sigma(Y).
$$


The conditional expectation $\mathbb{E}[X \mid Y]$ is the **Radon-Nikodym derivative** of $Q_X$ with respect to $P_Y$:

$$
\mathbb{E}[X \mid Y] = \frac{dQ_X}{dP_Y}.
$$

This means that $\mathbb{E}[X \mid Y]$ is the "density" of the measure $Q_X$ with respect to $P_Y$, and it ensures that:

$$
\int_A \mathbb{E}[X \mid Y] \, dP = \int_A X \, dP, \quad \text{for all } A \in \sigma(Y).
$$


**Example**
Let $Y: \Omega \to \mathbb{R}$ be defined on a probability space $(\Omega, \mathcal{F}, P)$. Consider the random variable $X$:
- Suppose $\Omega = [0, 1]$, $\mathcal{F} = \mathcal{B}([0,1])$, and $P$ is the Lebesgue measure.
- Let $Y(\omega) = \lfloor 10 \cdot \omega \rfloor$ (the integer part of $10\omega$), which takes values $0, 1, ..., 9$.
- The \(\sigma\)-algebra \(\sigma(Y)\) partitions $\Omega$ into 10 intervals $\left[\frac{k}{10}, \frac{k+1}{10}\right)$, for $k = 0, ..., 9$.









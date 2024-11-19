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

Now, we can use measure theory to rewrite this formula. Let $(\Omega, \mathcal{F}, P)$ be a probability space, and let $\mathscr{G} \subseteq \mathcal{F}$ be a sub-sigma algebra. Given $A \in \mathcal{F}$, if we define a measure $v$ on $\mathcal{G}$ such that $v(g) = P(A \cap g)$ for all $g \in \mathcal{G}$, then the measure $v$ is absolutely continuous with respect to $P$. By the Radon-Nikodym theorem, there exists a $\mathcal{G}$-measurable random variable (or function) $f = P(A \mid \mathcal{G}): \Omega \to \mathbb{R}$, called the conditional probability, such that:

$$
v(g) = P(A \cap g) = \int_{g} f(\omega) \, dP(\omega)
$$

for every $g \in \mathcal{G}$, and $f = \frac{dv(g)}{dP(g)} = \frac{dP(A \cap g)}{dP(g)}$ is the Radon-Nikodym derivative, which is referred to as the conditional distribution. Note that both $v$ and $P$ are $\mathcal{G}$-measurable, which makes the random variable $P(A \mid \mathcal{G})$ also $\mathcal{G}$-measurable. Intuitively, this means that the conditional distribution of $A$ given $\mathcal{G}$ depends only on the information provided by $\mathcal{G}$. This expression shows that the conditional probability $P(A \mid \mathcal{G})$ is a density function that describes how much of the measure $P(A \cap \mathcal{G})$ is concentrated in infinitesimal parts of $P(\mathcal{G})$.






Let we generalize this formula. Given $X$ and $Y$ as two random variables, with the measure $P_X$ and $P_Y$ w.r.t to some dominating measure $\mu$. Then, the conditional distribution of $Y$ given $X$ is 



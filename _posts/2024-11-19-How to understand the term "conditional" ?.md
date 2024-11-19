---
layout: post
title: "How to understand the term conditional?"
author: "Ziyan Li"
categories: journal
tags: [documentation, sample]
---

The concept of conditional is curial in statistic. In this blog, we attempt to use measure theory to provide more intuition of the formula related to the conditional distribution. Let use start with the simplest case: the conditional probablity. We know the definition of conditional probabilty of $B$ given $A$ is 

$$
\text{P}(B|A)=\frac{P(AB)}{P(A)}
$$

Now,we can use the measure theory to rewrite this formula. Let $(\Omega, \mathscr{F}, P)$ be a probability space, $\mathscr{G} \subseteq \mathcal{F}$. Given $A \in \mathcal{F}$, the Radon-Nikodym theorem implies that there is a $\mathcal{G}$-measurable random variable $P(A \mid \mathcal{G}): \Omega \to \mathbb{R}$, called the conditional probability, such that

$$
\int_{G} P(A \mid \mathcal{G})(\omega) \, dP(\omega) = P(A \cap G)
$$

for every $G \in \mathcal{G}$, and such a random variable is uniquely defined up to sets of probability zero. 

A conditional probability is called *regular* if $P(\cdot \mid \mathcal{G})(\omega)$ is a probability measure on $(\Omega, \mathcal{F})$ for all $\omega \in \Omega$.


Let we generalize this formula. Given $X$ and $Y$ as two random variables, with the measure $P_X$ and $P_Y$ w.r.t to some dominating measure $\mu$. Then, the conditional distribution of $Y$ given $X$ is 



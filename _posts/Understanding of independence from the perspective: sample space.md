---
layout: post
title: "Understanding Independence Through the Lens of Sample Spaces"
author: "Ziyan Li"
categories: journal
tags: [documentation, sample]
---

1. **Joint Random Variable $(X, Y)$**:
   - We are working with two random variables $X$ and $Y$, each mapping outcomes from the sample space $\Omega$ to $\mathbb{R}$. Together, $(X, Y)$ defines a joint random variable, which maps $\Omega$ to $\mathbb{R}^2$.
   - Thus, the joint random variable $(X, Y): \Omega \to \mathbb{R}^2$.

2. **Preimage under $(X, Y)$**:
   - For a set $A \subset \mathbb{R}^2$, the preimage under the joint random variable $(X, Y)$ is defined as:
 
$$
(X, Y)^{-1}(A) = \{\omega \in \Omega : (X(\omega), Y(\omega)) \in A\}.
$$
     
   - This means that $(X, Y)^{-1}(A)$ is a subset of $\Omega$, but the elements of this subset correspond to pairs $(X(\omega), Y(\omega)) \in A$, meaning the events are described by pairs of outcomes from the sample space $\Omega$.

3. **Product Measure and Dependence**:
   - In the case of independent random variables, the product measure $P_{X,Y} = P_X \times P_Y$ reflects the fact that the measure of a set in $\mathbb{R}^2$ is the product of the measures in $\mathbb{R}$ for $X$ and $Y$, as they do not influence each other.
   - However, when $X$ and $Y$ are dependent, the preimage under the joint distribution $(X, Y)$ must account for how the events in the sample space $\Omega$ are coupled, and this coupling will affect the way we measure sets like $A \times A$.


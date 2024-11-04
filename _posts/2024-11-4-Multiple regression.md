---
layout: post
title: "Multiple Regression"
author: "Ziyan Li"
categories: journal
tags: [documentation, sample]
---

The relevant idea here comes from the **Rank-Nullity Theorem**, which states that for any linear map $X: \mathbb{R}^p \rightarrow \mathbb{R}^n$, the dimension of the image of $X$ (rank of $X$) plus the dimension of the kernel of $X$ (nullity of $X$) equals $p$. Mathematically, this is written as:

$$
\text{rank}(X) + \text{nullity}(X) = p.
$$

Since $\text{rank}(X) = p$, it follows that the nullity of $X$ is $p - n$, meaning the null space of $X$ has dimension $p - n$. This null space consists of all vectors in $\mathbb{R}^p$ that $X$ maps to the zero vector in $\mathbb{R}^n$.

### Implication: Existence of Multiple $\beta$ Values Mapping to the Same $Y$

Because the null space of $X$ has dimension $p - n > 0$, there exist non-zero vectors $v \in \mathbb{R}^p$ such that $Xv = 0$. Therefore, if $\beta_0$ is a solution to $Y = X\beta$, then any vector of the form $\beta = \beta_0 + v$, where $v$ is in the null space of $X$, will also satisfy $Y = X\beta$.

This means that the projection of a point in $\mathbb{R}^p$ onto $\mathbb{R}^n$ via $X$ does not uniquely determine the original coordinates in $\mathbb{R}^p$; rather, there are infinitely many possible coordinate combinations (solutions $\beta$) that can map to the same projected point $Y$ in $\mathbb{R}^n$.

---
layout: post
title: "Multiple Linear Regression"
author: "Ziyan Li"
categories: journal
tags: [documentation, sample]
---
# Estimating Beta in Multiple Linear Regression

When estimating the parameter vector $\beta$ in multiple linear regression, the dimensions of the matrices $X$ and $Y$ play a crucial role. Before discussing the behavior of the estimated coefficient vector $\hat{\beta}$, we recall the **Rank-Nullity Theorem** from linear algebra. This theorem states that for any linear transformation $X: \mathbb{R}^p \rightarrow \mathbb{R}^n$, the sum of the dimension of the image of $X$ (known as the rank of $X$) and the dimension of the kernel of $X$ (known as the nullity of $X$) equals the number of columns $p$ of the matrix $X$. This relationship can be expressed mathematically as:

$$
\text{rank}(X) + \text{nullity}(X) = p.
$$

## Remark

- The expression $Xv$ represents the interaction between the column space of $X$ and the vector $v$, essentially reflecting a linear combination of the columns of $X$.
- When the rank of $X$ satisfies $\text{rank}(X) = \dim(\text{col}(X)) < p$, it follows that $\dim(\text{ker}(X)) > 0$. Consequently, the vector $v$ is no longer unique, as we can have $Xv = Y$ and $Xv' = Y$ for different vectors $v$ and $v'$, with the condition $v - v' \in \text{ker}(X)$.

Next, we can apply this theorem within the context of multiple linear regression. Assume the model is expressed as:

$$
Y = X\beta + \epsilon,
$$

where $Y$ is an $n \times 1$ matrix, $X$ is an $n \times p$ matrix, and $\beta$ is a $p \times 1$ matrix. Using Ordinary Least Squares (OLS) to estimate $\beta$, we obtain:

$$
\hat{Y} = X\hat{\beta}.
$$

We will now analyze the conditions under which $\hat{\beta}$ may not be unique. Our focus will be on the nullity of $X$. Notably, the rank of $X$ is constrained to be less than or equal to the minimum of the number of columns and rows, that is:

$$
\text{rank}(X) \leq \min(p, n).
$$

Thus, the interplay between the number of columns and rows in $X$ significantly influences the uniqueness of $\hat{\beta}$.

- In the case where $n \geq p$, if $X$ has full rank $p$, then the estimated coefficient vector $\hat{\beta}$ has a unique solution if and only if $\text{rank}(X) = p$, which implies that $\text{nullity}(X) = 0$.
- Conversely, when $n < p$, it follows that $\text{rank}(X) \leq n < p$, resulting in $\text{nullity}(X) > 0$. Therefore, in this scenario, $\hat{\beta}$ can never have a unique solution.

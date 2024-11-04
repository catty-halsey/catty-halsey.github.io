---
layout: post
title: "Multiple Linear Regression"
author: "Ziyan Li"
categories: journal
tags: [documentation, sample]
---
## Coefficient in simple and multiple regression
First, we need to emphaize that the coefficient using regression through simple linear regression and multiple regression are different in general. More specific, using our observed data $X$ and $Y$, if we have $y=X^{(j)}\bar{\beta_j}$ from simple regression and $y=X\hat{\beta}$ from multiple, where $X^{(j)}$ is the j-th column of $X$, then $\bar{\beta_j}$ and $\hat{\beta}(j)$ are not equal in general. In particular, when predictors are orthogonal, it holds that:

- $x_{\cdot,j}^T x_{\cdot,k} = 0$ for all $j \neq k$
- Consequently, $X^T X = \text{diag} \left( \sum_{i=1}^n x_{i,1}^2, \dots, \sum_{i=1}^n x_{i,p}^2 \right)$

Given these properties, the calculation of $\hat{\beta}$ simplifies. Specifically:

$$
\hat{\beta}_j = \left( X^T X \right)^{-1} X^T Y_j = \frac{\sum_{i=1}^n x_{i,j} y_i}{\sum_{i=1}^n x_{i,j}^2} = \frac{\hat{\sigma}_{x_j,y}}{\hat{\sigma}_{x_j}^2}
$$

This results in the same outcome as performing separate simple regressions for each predictor $x_j$ on the response $Y$. 

Then, we back to the general cases. When the coefficients from different regression are different, we are interested in which one is more reliable and which can be used to intepret as the total cause effect of $X_j$ on Y, for each $j \in {1,2,\cdots,p}$. The concept of **valid adjustment** solves this problem. 

Consider a linear, zero-mean Gaussian Structural Causal Model (SCM), where all assignments are linear, and the noise terms are normally distributed with zero mean.
1. The vector $(Y, X, Z)$ has a (zero mean) Gaussian distribution with 
   $$
   \mathbb{E}[Y \mid X = x, Z = z] = ax + b^z
   $$
   (no proof necessary).

2. Assume now that $Z$ is a valid adjustment set for the causal effect from $X$ to $Y$.

3. Prove that 
   $$
   \frac{\partial}{\partial x} \mathbb{E}_{C; \, \text{do}(X := x)}[Y] = a.
   $$


## Uniquenss of Estimatied Beta in Multiple Linear Regression

When estimating the parameter vector $\beta$ in multiple linear regression, the dimensions of the matrices $X$ and $Y$ play a crucial role. Before discussing the behavior of the estimated coefficient vector $\hat{\beta}$, we recall the **Rank-Nullity Theorem** from linear algebra. This theorem states that for any linear transformation $X: \mathbb{R}^p \rightarrow \mathbb{R}^n$, the sum of the dimension of the image of $X$ (known as the rank of $X$) and the dimension of the kernel of $X$ (known as the nullity of $X$) equals the number of columns $p$ of the matrix $X$. This relationship can be expressed mathematically as:

$$
\text{rank}(X) + \text{nullity}(X) = p.
$$

#### Remark

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
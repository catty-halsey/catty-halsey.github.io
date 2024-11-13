---
layout: post
title: "Model Fitting"
author: "Ziyan Li"
categories: journal
tags: [documentation, sample]
---

In this [blog](https://catty-halsey.github.io/Multiple-regression#Uniqueness-of-Estimatied-Beta-in-Multiple-Linear-Regression), we discuss methods for estimating regression coefficients and making predictions, along with testing and constructing confidence intervals for these estimates. Given that explanatory variables are often correlated, we are interested in assessing the necessity of each variable for explaining and predicting outcomes $Y$. This leads to a fundamental question: how do we find the "best" model that includes the most appropriate explanatory variables?

Here, "best" and "appropriate" imply a model with a smaller Mean Squared Error (MSE), which balances trade-off between variance and bias. Although F-tests and t-tests can help identify redundant variables, the multiple testing lead to the compounding error and invalid p-value. Threfore, we consider to use analytic method to construct criterias to identify the global best model with minimal MSE. To achieve this, we aim to minimize the **Submodel Mean Squared Error (SMSE)** over $Y^M$ rather than $Y$, where $Y^M = X^M \beta^M + \epsilon$ and $X^M$ denotes a submatrix of $X$. The following we focus on Marllow's Cp criteria.




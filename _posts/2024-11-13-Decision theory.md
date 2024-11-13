---
layout: post
title: "Sequential testing"
author: "Ziyan Li"
categories: journal
tags: [documentation, sample]
---

1. **Decision as a Mapping**:
   - A **decision rule** is indeed a mapping from data in the sample space to an element in the action space. Essentially, the decision rule dictates how to estimate or infer the unknown parameter based on observed data.
   - Each decision rule is unique because it specifies how to use the data or some combination of it, aiming to provide an estimate for the unknown parameter.

2. **Decision Rule as an Estimator**:
   - The decision rule functions as an **estimator** for the unknown parameter. For each observed data point, the rule maps it to an estimate, which is our "best guess" of the parameter given the available information.
   - Since we don’t know the true parameter, our decision rule serves to approximate it as closely as possible.

3. **Loss Function**:
   - For each data point, there exists a potential **loss**, which is the difference (or discrepancy) between the true parameter and the estimate produced by our decision rule.
   - The **loss function** quantifies this discrepancy, measuring how "costly" it is to make a particular estimation error for each data point.
   - Common loss functions include squared error loss (for continuous parameters) and zero-one loss (for classification), but the choice depends on the problem’s context.

4. **Risk as the Expected Loss**:
   - The **risk** of a decision rule (or estimator) is the expected value of the loss over all possible data points.
   - It represents the **average loss** that we would incur by using this decision rule across all possible observations from the sample space.
   - Mathematically, the risk of a decision rule $d(X)$ with respect to a parameter $\theta$ can be expressed as:
     
$$
R(d, \theta) = \mathbb{E}_{X \sim P_\theta}[L(d(X), \theta)],
$$
   
     where $L(d(X), \theta)$ is the loss function, and the expectation is taken over the distribution of $X$ under $\theta$.

6. **Minimizing Risk**:
   - In decision theory, we often seek a decision rule that minimizes this risk (average loss), leading to an estimator that is optimal in some sense.
   - For example, in **minimum mean squared error (MMSE)** estimation, the goal is to find an estimator that minimizes the expected squared difference between the estimator and the true parameter.


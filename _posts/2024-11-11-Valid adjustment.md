---
layout: post
title: "Covariate adjustment"
author: "Ziyan Li"
categories: journal
tags: [documentation, sample]
---

### Why Do-Calculus is Useful When Adjustment Isn't Possible

In many real-world scenarios, causal models have hidden confounders that affect both the treatment $X$ and the outcome $Y$. This makes it difficult, or even impossible, to find a straightforward adjustment set that would satisfy the backdoor criterion. Do-calculus is designed to handle these situations by:

1. **Transforming Interventional Distributions**: Using the rules of do-calculus (action/observation exchange, insertion/deletion of observations, and insertion/deletion of actions), we can transform expressions involving interventions into ones that either:
   - Remove the intervention or simplify it, or
   - Rephrase it in terms of observational data we can collect.

2. **Gradually Simplifying**: The rules help us decompose complex interventional distributions step-by-step. This process eventually leads to expressions that can be estimated from data, even if we start with a model where no immediate valid adjustment set exists due to hidden variables.


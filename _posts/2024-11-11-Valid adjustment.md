---
layout: post
title: "Covariate adjustment"
author: "Ziyan Li"
categories: journal
tags: [documentation, sample]
---
Absolutely, that's a key insight into the purpose of **do-calculus**! When there are *hidden* or *unobserved* variables that prevent us from finding a simple valid adjustment set, do-calculus provides a systematic way to transform and decompose probabilities under intervention. This process allows us to gradually "peel back" the structure of dependencies until we can apply a valid adjustment and finally express the causal effect in terms of observable (and thus computable) probabilities.

### Why Do-Calculus is Useful When Adjustment Isn't Possible

In many real-world scenarios, causal models have hidden confounders that affect both the treatment \( X \) and the outcome \( Y \). This makes it difficult, or even impossible, to find a straightforward adjustment set that would satisfy the backdoor criterion. Do-calculus is designed to handle these situations by:

1. **Transforming Interventional Distributions**: Using the rules of do-calculus (action/observation exchange, insertion/deletion of observations, and insertion/deletion of actions), we can transform expressions involving interventions into ones that either:
   - Remove the intervention or simplify it, or
   - Rephrase it in terms of observational data we can collect.

2. **Gradually Simplifying**: The rules help us decompose complex interventional distributions step-by-step. This process eventually leads to expressions that can be estimated from data, even if we start with a model where no immediate valid adjustment set exists due to hidden variables.

### Example Workflow Using Do-Calculus

1. **Start with a target causal effect**: Suppose we want \( p(Y \mid \text{do}(X = x)) \).
   
2. **Identify possible obstacles**: We realize that there are unobserved confounders between \( X \) and \( Y \) that prevent direct adjustment.

3. **Apply Do-Calculus Rules**: Using the do-calculus rules, we decompose \( p(Y \mid \text{do}(X = x)) \) into expressions that introduce or eliminate interventions and observations. For instance, we might use the action/observation exchange to swap out certain do-operations for conditional probabilities or apply insertion/deletion rules to simplify the expressions.

4. **Reach a Valid Adjustment Step**: After several applications of the do-calculus rules, we reach a form where a valid adjustment is possible, often by conditioning on an observed set of variables that blocks any remaining confounding paths.

5. **Estimate the Result**: We finally end up with a form of the probability that involves only observable quantities, which we can estimate from data.

### Key Benefit

The main power of do-calculus lies in its ability to provide a path to estimate causal effects in the presence of hidden variables, where simple conditioning on observable variables is not enough. By iteratively applying its rules, do-calculus allows us to sidestep obstacles presented by unobserved confounders and ultimately arrive at expressions that are both valid for causal inference and computable from observed data.

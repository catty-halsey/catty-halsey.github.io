---
layout: post
title: "Covariate adjustment"
author: "Ziyan Li"
categories: journal
tags: [documentation, sample]
---
## Valid adjustment set

Consider an SCM $\mathcal{C}$ over nodes $V$ and let $Y \notin PA_X$. We call a set $Z \subseteq V \setminus \{X, Y\}$ a valid adjustment set for the ordered pair $(X, Y)$ if

$$
p_{\mathcal{C}; \text{do}(X := x)}(y) = \sum_{z} p_{\mathcal{C}}(y \mid x, z) \, p_{\mathcal{C}}(z).
$$

In general, the conditional probability is different from the probability under intervention. For example, assume we have a SCM with a DAG as following

$$
\begin{align}
&X &rarr; Y\\
&X=N_X\\
&y=x+N_y\\
\end{align}
$$

where $N_X, N_Y$ are idependent standard normal noise.

Then, the probability of $Y$ conditional on $X$ is different from the probablity of $Y$ intervening on $X$. The difference arises from the nature of intervention. Intervention on $X$ only removes the incoming edges of $X$.i.e., the edges from the parents of $X$. Therefore, if we intervene on children of $X$, it does not effect the distribution of $X$. However, the conditional distribution is a two-direction effects. More specific, the conditional distribution $X$ on $Y$ are differ from the distribution of $X$  as long as existing an edge between $X$ and $Y$. In particular, if $X$ is a source node, they the distribution of any variable conditional on X is same as intervening on X.




### Why Do-Calculus is Useful When Adjustment Isn't Possible

In many real-world scenarios, causal models have hidden confounders that affect both the treatment $X$ and the outcome $Y$. This makes it difficult, or even impossible, to find a straightforward adjustment set that would satisfy the backdoor criterion. Do-calculus is designed to handle these situations by:

1. **Transforming Interventional Distributions**: Using the rules of do-calculus (action/observation exchange, insertion/deletion of observations, and insertion/deletion of actions), we can transform expressions involving interventions into ones that either:
   - Remove the intervention or simplify it, or
   - Rephrase it in terms of observational data we can collect.

2. **Gradually Simplifying**: The rules help us decompose complex interventional distributions step-by-step. This process eventually leads to expressions that can be estimated from data, even if we start with a model where no immediate valid adjustment set exists due to hidden variables.


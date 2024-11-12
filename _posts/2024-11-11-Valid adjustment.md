---
layout: post
title: "Covariate adjustment"
author: "Ziyan Li"
categories: journal
tags: [documentation, sample]
---
## Table of Contents
- [Motivation of constructing valid adjustment set](#Motivation-of-constructing-valid-adjustment-set)
- [Valid adjustment set](#Valid-adjustment-set)
- [Do-Calculus](#Do-Calculus)

## Motivation for Constructing Valid Adjustment Sets
In general, the conditional probability $P(Y \mid X)$ differs from the probability under intervention. To illustrate this, consider an SCM with a DAG structured as follows:

$$
\begin{align}
&X \rightarrow Y,\\
&X = N_X,\\
&Y = X + N_Y,
\end{align}
$$

where $N_X$ and $N_Y$ are independent standard normal noise.

In this case, the conditional probability $P(Y \mid X)$ is distinct from the interventional probability $P(Y \mid \text{do}(X))$. This difference stems from the nature of intervention. An intervention on $X$ removes only the incoming edges of $X$—that is, the edges from $X$'s parent nodes. Therefore, if we intervene on $X$'s children, the distribution of $X$ remains unaffected. In contrast, conditional distributions involve two-direction effects: conditioning on $Y$ affects $X$ whenever a directed edge exists between them. 

In particular, if $X$ is a source node, the conditional distribution of any variable on $X$ aligns with its distribution under intervention on $X$. This naturally raises the question: **Under what conditions can we make the intervention distribution equal to the conditional distribution?**

Judea Pearl proposed the concept of a **valid adjustment set**, which allows us to equate the intervention distribution to the conditional distribution.

---

## Valid Adjustment Set

Consider an SCM $\mathcal{C}$ over nodes $V$, where $Y \notin PA_X$. We define a set $Z \subseteq V \setminus \{X, Y\}$ as a **valid adjustment** set for the ordered pair $(X, Y)$ if

$$
p_{\mathcal{C}; \text{do}(X := x)}(y) = \sum_{z} p_{\mathcal{C}}(y \mid x, z) \, p_{\mathcal{C}}(z).
$$

This equation effectively means that conditioning on $Z$ “blocks” all indirect paths from $X$ to $Y$, thus isolating the causal effect of $X$ on $Y$. In other words, conditioning on the valid adjustment set $Z$ makes $X$ behave like a source node with respect to $Y$.

---

## Construction Ideas

This construction generalizes into three criteria for a valid adjustment set:

1. **Parent Adjustment**: Setting $Z := PA_X$ forms a valid adjustment set for $(X, Y)$.

2. **Backdoor Criterion**: Any set $Z \subseteq V \setminus \{X, Y\}$ is a valid adjustment set if:
   - $Z$ contains no descendants of $X$, **and**
   - $Z$ blocks all paths from $X$ to $Y$ that enter $X$ through a backdoor (i.e., paths of the form $X \leftarrow \dots$).

3. **Toward Necessity**: Any set $Z \subseteq V \setminus \{X, Y\}$ is valid if:
   - $Z$ contains no descendants of any node on a directed path from $X$ to $Y$ (except for descendants of $X$ not on the path from $X$ to $Y$), **and**
   - $Z$ blocks all non-directed paths from $X$ to $Y$.

---

## Remark
- Under “toward necessity,” descendants of $X$ can be included in the valid adjustment set as long as they are not on the directed path from $X$ to $Y$. To understand why this is valid, consider the Markov property: if $Z$ is a descendant of $X$ not on the directed path from $X$ to $Y$, then $X$ in the path from $U$ to $Y$ is not a collider. Therefore, intervening on $X$ d-separates $U$ and $Y$, making them conditionally independent given $X$. 

Mathematically, this yields:

$$
p_{\mathcal{C}; \text{do}(X := x, U=u)}(y) = p_{\mathcal{C}; \text{do}(X := x)}(y) = p_{\mathcal{C}; \text{do}(X := x)}(y|U) = p_{\mathcal{C}}(y|x,u) .
$$

---

## Optimal Valid Adjustment Set Criteria

To minimize the variance of the estimator, we consider two criteria for the **optimal valid adjustment set**:

1. If $Z$ is a valid adjustment set and $W \in \text{PA}_X$, then removing $W$ from $Z$ decreases $\text{var}(\text{estimator} \mid Z \setminus \{W\})$.
2. If $Z$ is a valid adjustment set and $W \in \text{PA}_Y$, then adding $W$ to $Z$ decreases $\text{var}(\text{estimator} \mid Z \cup \{W\})$.

These criteria highlight that the optimal adjustment set focuses on variables that explain $Y$ but not $X$ excessively. This balance reduces the variance of the estimator for $Y$ by maximizing the explanatory power of $Y$ and minimizing that of $X$.

---

## Do-Calculus

Pearl’s **do-calculus** offers three rules to compute interventional probabilities from observed distributions. Given disjoint subsets $X$, $Y$, $Z$, and $W$ in a graph $G$, the rules are as follows:

1. **Insertion/deletion of observations**:
   $$ p_{\mathcal{C};\text{do}(X := x)}(y \mid z, w) = p_{\mathcal{C};\text{do}(X := x)}(y \mid w) $$
   if $Y$ and $Z$ are d-separated by $X, W$ after removing incoming edges to $X$. This rule permits simplifying conditions based on d-separation.

2. **Action/observation exchange**:
   $$ p_{\mathcal{C};\text{do}(X := x, Z = z)}(y \mid w) = p_{\mathcal{C};\text{do}(X := x)}(y \mid z, w) $$
   if $Y$ and $Z$ are d-separated by $X, W$ after removing incoming edges to $X$ and outgoing edges from $Z$. This rule helps “swap” action and observation as needed.

3. **Insertion/deletion of actions**:
   $$ p_{\mathcal{C};\text{do}(X := x, Z = z)}(y \mid w) = p_{\mathcal{C};\text{do}(X := x)}(y \mid w) $$
   if $Y$ and $Z$ are d-separated by $X, W$ after removing all edges into $X$ and $Z(W)$. Here, $Z(W)$ represents nodes in $Z$ that aren’t ancestors of any node in $W$.

## References

- Pearl, J. Causality: Models, Reasoning, and Inference. Cambridge University Press, 2009.
- Spirtes, P., Glymour, C., Scheines, R. Causation, Prediction, and Search. MIT Press, 2000.
- Peters, J., Janzing, D., & Schölkopf, B. Elements of Causal Inference: Foundations and Learning Algorithms. MIT Press, 2017.

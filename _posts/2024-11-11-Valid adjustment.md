---
layout: post
title: "Covariate adjustment"
author: "Ziyan Li"
categories: journal
tags: [documentation, sample]
---

In general, the conditional probability is different from the probability under intervention. For example, assume we have a SCM with a DAG as following

$$
\begin{align}
&X \rightarrow Y\\
&X=N_X\\
&Y=X+N_Y\\
\end{align}
$$

where $N_X, N_Y$ are idependent standard normal noise.

Then, the probability of $Y$ conditional on $X$ is different from the probablity of $Y$ intervening on $X$. The difference arises from the nature of intervention. Intervention on $X$ only removes the incoming edges of $X$.i.e., the edges from the parents of $X$. Therefore, if we intervene on children of $X$, it does not effect the distribution of $X$. However, the conditional distribution is a two-direction effects. More specific, the conditional distribution $X$ on $Y$ are differ from the distribution of $X$  as long as existing an edge between $X$ and $Y$. In particular, if $X$ is a source node, they the distribution of any variable conditional on X is same as intervening on X.

Can we construct some conditions which allow us to make the intervention distribution equal the conditional distribution? The answer is yes. Judea Pearl proposed the valid adjustment set to allow us to write the intervention distribution into the conditional distribution.

## Valid adjustment set

Consider an SCM $\mathcal{C}$ over nodes $V$ and let $Y \notin PA_X$. We call a set $Z \subseteq V \setminus \{X, Y\}$ a **valid adjustment** set for the ordered pair $(X, Y)$ if

$$
p_{\mathcal{C}; \text{do}(X := x)}(y) = \sum_{z} p_{\mathcal{C}}(y \mid x, z) \, p_{\mathcal{C}}(z).
$$

This construction is essentially block all the indirect effects/paths from $X$ to $Y$. In other words, we make the $X$ to be a source node under the conditional on the valid adjustment set.

This contruction idea can be generalize into three criteria:

(i) **"Parent adjustment"**: $Z := PA_X$ is a valid adjustment set for $(X, Y)$.

(ii) **"Backdoor criterion"**: Any $Z \subseteq V \setminus \{X, Y\}$ with
- $Z$ contains no descendant of $X$ **AND**
- $Z$ blocks all paths from $X$ to $Y$ entering $X$ through the backdoor (paths of the form $X \leftarrow \dots$)

is a valid adjustment set for $(X, Y)$.

(iii) **"Toward necessity"**: Any $Z \subseteq V \setminus \{X, Y\}$ with
- $Z$ contains no descendant of any node on a directed path from $X$ to $Y$ (except for descendants of $X$ that are not on a directed path from $X$ to $Y$) **AND**
- $Z$ blocks all non-directed paths from $X$ to $Y$

is a valid adjustment set for $(X, Y)$.

**Remark**
- Note that under "toward necessity", we allow the descendants of $X$ in the valid adjustment set as long as it not in the directed path from $X$ t0 $Y$. To understand why this valid, we can use markov property to illustrate it. Since if z is the descendants of $X$ which is not in the directed path from $X$ ro $Y$, $X$ in the path from $U$ to $Y$ is not a collider. Therefore, if we interven on $X$, $U$ and $Y$ are d-separated by $X$ and so conditional independent on $X$. In other words, intervening on $U$ does not provide us more information to estimate $Y$. Mathematically, we have the following equality,

$$
p_{\mathcal{C}; \text{do}(X := x, U=u)}(y) = p_{\mathcal{C}; \text{do}(X := x)}(y) = p_{\mathcal{C}; \text{do}(X := x)}(y|U) = p_{\mathcal{C}}(y|x,u) .
$$

This equality can be generalize into a rule (rule 3 of do-calculus), which we introduce in a later section. We can observe that there is no causal effect of $U$ on $Y$ if we already intervene on $X$ from this equality. However, if we intervene on $U$, it indeed provide extra information on $X$, which decrease the varity of $X$ and make less precise of estimation of $Y$ using $X$. This trigger a questions that what kind of the valid adjustment sets lead to the smallest variance of estimator? The core idea is we should include more variables which can help to explain $Y$ but less variables which can help to explain $X$.The more varaibles explaining $Y$, the estimation is more accurate with less variance. In contrast, the more variables explaining $X$ weaken the varity of $X$ and therefore weaken the ability of $X$ to accurately explain $X$. Hence, we have two criteria to have the optimal valid adjustment set.

(i) If $Z$ is a valid adjustment set and $W \in \text{PA}_X$, $\text{var}(\text{estimator} \mid Z \setminus \{W\})$ is smaller than $\text{var}(\text{estimator} \mid Z)$.

(ii) If $Z$ is a valid adjustment set and $W \in \text{PA}_Y$, $\text{var}(\text{estimator} \mid Z \cup \{W\})$ is smaller than $\text{var}(\text{estimator} \mid Z)$.

We should pay attention to the different focus of the valid adjustment sets and the optimal adjustment sets. When we discuss the optimal adjustment set, we are mostly interested the variance of the estimator and so we look at the different causal effect of variable on variance instead of the causal effect on $Y$, since we already under the valid adjustment set situations.

Recall that we discuss the https://catty-halsey.github.io/Multiple-regression#Uniqueness-of-Estimatied-Beta-in-Multiple-Linear-Regression



### Why Do-Calculus is Useful When Adjustment Isn't Possible

In many real-world scenarios, causal models have hidden confounders that affect both the treatment $X$ and the outcome $Y$. This makes it difficult, or even impossible, to find a straightforward adjustment set that would satisfy the backdoor criterion. Do-calculus is designed to handle these situations by:

1. **Transforming Interventional Distributions**: Using the rules of do-calculus (action/observation exchange, insertion/deletion of observations, and insertion/deletion of actions), we can transform expressions involving interventions into ones that either:
   - Remove the intervention or simplify it, or
   - Rephrase it in terms of observational data we can collect.

2. **Gradually Simplifying**: The rules help us decompose complex interventional distributions step-by-step. This process eventually leads to expressions that can be estimated from data, even if we start with a model where no immediate valid adjustment set exists due to hidden variables.


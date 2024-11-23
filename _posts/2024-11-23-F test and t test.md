---
layout: post
title: "F test and t test"
author: "Ziyan Li"
categories: journal
tags: [documentation, sample]
---

**Remarks**
- 1. The test statistic of F test considers all columns of $X$ together. It implies that the p-value will not be affected by the collinearity from the columns of $X$. In contrast, the t test is design for the single $\hat{\beta}_j$ and the variance of $\hat{\beta}_j$ is affected by the coolinearity of columns of $X$. Hence,
The p-value under (partial) multiple regression and single regression might lead to significantly different result when the columns of $X$ are highly correlated. Although the F test consider the collinearity of $X$, the p-value from  under (partial) multiple regression and single regression are still different due to the change in F distribution but generally does not have significant differernce.
- 2. We should notice the t test and F test are testing different hypothesis when we test over 2 $\hat{\beta}_j$. For example, assume we test two estimated beta. If we use F test, the null hypothesis is $\hat{\beta}_i=\hat{\beta}_j=0$ and we only implement the test once and one p-value. And if we reject null hypothesis, we conclude at least one of the estimated beta is 0. However, when we use t test to test the two estimated beta, we essentially apple the t test twice, implement two independent tests and obtain two p-values. Even if we get two significant results, we cannot conclude that $\hat{\beta}_i=0 \quad \text[and}  \quad \hat{\beta}_j \neq 0}$ because the signficant level is not $\alpha$ anymore. The type I error become larger, which is $1-(1-\alpha)^2$.  Hence, even we obtain two insignificant p-value, we cannot conclude $\hat{\beta}_i=\hat{\beta}_j=0$ with the significant level $\alpha$.
  3. In particular, when we only test one estimated beta, the t test and F test are equivalent. Firstly, the hypothesis for two tests are the same. And the test statistic of F test is square that of t test, i.e T_{F}=T^2_{t}. Since we have P(\abs(T)>a)=P(T^2>a^2), so the p-value under two tests are the same.

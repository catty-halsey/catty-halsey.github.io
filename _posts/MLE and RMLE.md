---
layout: post
title: "MLE and RMLE"
author: "Ziyan Li"
categories: journal
tags: [documentation, sample]
---

### **1. Maximum Likelihood (ML)**
ML estimates the model parameters (both fixed and random effects) by finding the values that **maximize the likelihood function**. This function represents the probability of observing the given data, given the model parameters.

#### **Key Characteristics:**
- **Bias in Variance Estimation:**  
  ML tends to **underestimate the variance** components in mixed models, especially when the sample size is small. This happens because ML doesn't account for the **loss of degrees of freedom** due to estimating the fixed effects.

- **Model Comparison:**  
  ML allows comparing the **goodness-of-fit** between **nested models** (where one model is a subset of another) using the **likelihood ratio test** (LRT). This is useful for hypothesis testing when deciding whether to include or exclude certain fixed effects.

---

### **2. Restricted Maximum Likelihood (REML)**
REML modifies the likelihood function to account for the estimation of fixed effects. It estimates the variance components by maximizing the likelihood of the residuals after removing the fixed effects. This method is particularly useful for estimating random effects.

#### **Key Characteristics:**
- **Unbiased Variance Estimates:**  
  Unlike ML, REML produces **unbiased estimates of variance components** by adjusting for the degrees of freedom used in estimating the fixed effects. This is why it is often the **default in R** and other statistical software for mixed models.

- **Model Comparison Limitation:**  
  REML can only compare models with **the same fixed effects**. This is because the likelihood functions in REML depend on the fixed effects structure, making comparisons invalid if the fixed effects differ between models.

---

https://stats.stackexchange.com/questions/48671/what-is-restricted-maximum-likelihood-and-when-should-it-be-used

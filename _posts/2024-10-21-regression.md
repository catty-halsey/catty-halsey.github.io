---
layout: post
title: "Regression"
author: "Ziyan Li"
categories: journal
tags: [documentation, sample]
---

Hello world

Before constructing a regression model, we first need to test whether the variables are correlated. After obtaining the correlation value, we further want to determine how much we can rely on this value. Like other statistical tests, there are two common tests for correlation.

### Pearson Correlation

The z-transformation helps stabilize the variance of correlation coefficients and makes the distribution approximately normal, which is useful for constructing confidence intervals or hypothesis testing for correlations.

Given a sample Pearson correlation coefficient \( r \), the z-transformation is applied using:

$$
Z = \tanh^{-1}(\rho) = \frac{1}{2} \ln \left( \frac{1 + \rho}{1 - \rho} \right)
$$

This transformation results in a \( Z \) value that follows an approximately normal distribution for large sample sizes:

$$
Z \sim N\left(\tanh^{-1}(\rho), \sigma\right)
$$

where \( \sigma = \frac{1}{\sqrt{n - 3}} \).

Once we have constructed a confidence interval using the normal distribution, we need to invert the interval boundaries back to the value of \( \rho \): \( \tanh(\text{CI}[a, b]) \).

## Theoretical Computation of \( \beta_1 \) and \( Y \) in a Log-Linear Regression Model

We assume that \( Y \) and \( X \) have the following log-linear relationship:

$$
\log(Y) = \beta_0 + \beta_1 X + \epsilon
$$

where \( \epsilon \) is the random error term with mean zero, usually assumed to be normally distributed, \( \epsilon \sim N(0, \sigma^2) \).

### Step 1: Estimating \( \beta_1 \)

Given \( n \) data points \( (X_1, Y_1), (X_2, Y_2), \dots, (X_n, Y_n) \), we perform a least squares regression on \( \log(Y) \) as the dependent variable and \( X \) as the independent variable.

The linear regression equation for the log-transformed data is:

$$
\log(Y_i) = \beta_0 + \beta_1 X_i + \epsilon_i
$$

We estimate the coefficients \( \beta_0 \) and \( \beta_1 \) by minimizing the residual sum of squares (RSS):

$$
\text{RSS} = \sum_{i=1}^{n} \left( \log(Y_i) - \beta_0 - \beta_1 X_i \right)^2
$$

The least squares estimates for \( \beta_0 \) and \( \beta_1 \) are found using the normal equations:

$$
\hat{\beta}_1 = \frac{\sum_{i=1}^{n} (X_i - \bar{X})(\log(Y_i) - \overline{\log(Y)})}{\sum_{i=1}^{n} (X_i - \bar{X})^2}
$$

where \( \bar{X} \) is the sample mean of the \( X_i \)'s, and \( \overline{\log(Y)} \) is the sample mean of the log-transformed \( Y_i \)'s.

$$
\hat{\beta}_0 = \overline{\log(Y)} - \hat{\beta}_1 \bar{X}
$$

### Step 2: Interpreting the Estimated Coefficients

To interpret \( \beta_1 \), we model \( \log(Y) \) as a linear function of \( X \), then exponentiate both sides:

$$
Y_i = e^{\beta_0 + \beta_1 X_i + \epsilon_i}
$$

When \( X \) increases by 1 unit, the expected \( \log(Y) \) changes by \( \beta_1 \), meaning \( Y \) changes by a factor of \( e^{\beta_1} \). Thus, \( e^{\beta_1} \) is the factor by which the median of \( Y \) changes for a unit increase in \( X \).

### Step 3: Estimating \( Y \)

To predict \( Y \) for a new value \( X = X_{\text{new}} \), first compute the predicted \( \log(Y) \):

$$
\log(\hat{Y}) = \hat{\beta}_0 + \hat{\beta}_1 X_{\text{new}}
$$

Then exponentiate the result:

$$
\hat{Y} = e^{\hat{\beta}_0 + \hat{\beta}_1 X_{\text{new}}}
$$

### Step 4: Loss of Expectation and Median Interpretation

Due to Jensen's inequality, \( \mathbb{E}[e^{\log(Y)}] \neq e^{\mathbb{E}[\log(Y)]} \). Thus, the expectation of \( Y \) differs from its median when \( Y \) is log-normal. However, with symmetric errors, \( e^{\mathbb{E}[\log(Y)]} \) corresponds to the median of \( Y \).

### Example Interpretation

If \( \hat{\beta}_1 = 0.05 \), then for every 1-unit increase in \( X \), the median of \( Y \) increases by \( e^{0.05} \approx 1.051 \), or about 5.1%.

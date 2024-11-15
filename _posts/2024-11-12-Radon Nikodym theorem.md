---
layout: post
title: "Radon Nikodym theorem"
author: "Ziyan Li"
categories: journal
tags: [documentation, sample]
---
# The Radon–Nikodym Theorem

The Radon–Nikodym theorem involves a measurable space $(X, \Sigma)$, on which two $\sigma$-finite measures are defined: $\mu$ and $\nu$. 

The theorem states that, if $\nu \ll \mu$ (that is, $\nu$ is **absolutely continuous** with respect to $\mu$), then there exists a $\Sigma$-measurable function $f : X \to [0, \infty)$ such that for any measurable set $A \in \Sigma$:

$$
\nu(A) = \int_A f \, d\mu.
$$

Here, the function $f$ is called the **Radon–Nikodym derivative** of $\nu$ with respect to $\mu$, and is denoted as:

$$
f = \frac{d\nu}{d\mu}.
$$

Remark:
-**Mapping from Sample Space to Real Line:**
   The random variable $X$ maps outcomes from the sample space (often denoted by $\Omega$) to the real line $\mathbb{R}$. In doing so, we translate "events" in the sample space into intervals or sets on the real line.

2. **Lebesgue Measure on the Real Line:**
   When we consider the real line equipped with the Lebesgue measure $\mu$, each point in $\mathbb{R}$ has the same "mass," or density, under $\mu$. However, in probability theory, we’re interested in reflecting how likely an event is—meaning we want to assign "masses" or densities in a way that reflects the likelihood of events in the sample space that map to subsets of $\mathbb{R}$.

3. **Pushforward Measure and the Role of the Radon-Nikodym Derivative:**
   To translate between the sample space and the real line, we define a new measure $P = X_* \mu$, which is the pushforward of the original measure. This measure $P$ on $\mathbb{R}$ tells us the probability of events on the real line based on the probability structure of the sample space.

   The **Radon-Nikodym theorem** ensures that, when $P$ is absolutely continuous with respect to $\mu$, we can express $P$ in terms of $\mu$ through a density function $f$ (the Radon-Nikodym derivative $f = \frac{dP}{d\mu}$):

  $$
   P(A) = \int_A f \, d\mu.
  $$

4. **Interpretation of the Density $f$:**
   This density $f$ tells us how to "reweight" the Lebesgue measure to reflect the actual probability structure of events in the sample space. Now, for each interval $t + dt \in \mathbb{R}$, $f(t)$ represents the likelihood density for $X^{-1}(t+dt)$—that is, the part of the sample space that maps into this interval on the real line.

5. **Absolute Continuity and Consistency with Probability Theory:**
   The Radon-Nikodym construction guarantees that $P$ is absolutely continuous with respect to $\mu$, meaning that $P(A) = 0$ whenever $\mu(A) = 0$. This condition is crucial in probability, as it ensures that our probability assignments do not contradict the underlying structure of the real line.

In essence, the Radon-Nikodym theorem provides a formal framework for transforming one measure into another, which is precisely what allows us to create a probability distribution on the real line that reflects the likelihood of events in the sample space. It gives us the exact "transforming function" (the density $f$) to accomplish this, ensuring consistency between the original and the new measure.

## Example: Probability density function

In the context you're describing, let's clarify and refine the ideas of absolute continuity, the Radon-Nikodym derivative, and pushforward measures.

1. **Absolute Continuity and Radon-Nikodym Derivative**:
   If $P_\theta$ is absolutely continuous with respect to $P_{\theta_0}$ (written $P_\theta \ll P_{\theta_0}$), it implies that for any measurable set $A$, if $P_{\theta_0}(A) = 0$, then $P_\theta(A) = 0$ as well. This absolute continuity condition guarantees the existence of a Radon-Nikodym derivative, $\frac{dP_\theta}{dP_{\theta_0}}$, which can be thought of as a "density" of $P_\theta$ with respect to $P_{\theta_0}$.

2. **Pushforward Measure and Density**:
   If $X$ is a random variable, and $P_{\theta_0}$ is the pushforward measure of the Lebesgue measure $\lambda$ under the transformation given by the density $g$ (so $g$ relates $P_{\theta_0}$ to $\lambda$ as $dP_{\theta_0} = g \, d\lambda$), then $g$ is indeed the measurable function that "transforms" the Lebesgue measure into $P_{\theta_0}$.

3. **Construction of $P_\theta$ via Composition**:
   Since $P_\theta \ll P_{\theta_0}$, if $P_\theta$ is defined as the pushforward measure of $P_{\theta_0}$, and if $P_\theta$ also has a density $f$ with respect to $P_{\theta_0}$ (so $dP_\theta = f \, dP_{\theta_0}$), then $f$ acts as the measurable function transforming $P_{\theta_0}$ into $P_\theta$.

4. **Composition of Densities**:
   The composition $f \circ g$ can then be viewed as the "combined" transformation from the Lebesgue measure $\lambda$ directly to $P_\theta$. Specifically, if $g$ transforms $\lambda$ to $P_{\theta_0}$ and $f$ transforms $P_{\theta_0}$ to $P_\theta$, then the composition $f \circ g$ is the density of $P_\theta$ with respect to $\lambda$, meaning:
   
$$
dP_\theta = (f \circ g) \, d\lambda.
$$

This composition $f \circ g$ essentially allows us to relate $P_\theta$ directly to the Lebesgue measure, bypassing the intermediate measure $P_{\theta_0}$, provided that all measures are defined on the same measurable space. This setup is common in probability and statistics, especially in settings involving transformations of distributions and their densities.

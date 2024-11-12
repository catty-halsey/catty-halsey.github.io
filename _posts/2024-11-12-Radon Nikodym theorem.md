---
layout: post
title: "Radon Nikodym theorem"
author: "Ziyan Li"
categories: journal
tags: [documentation, sample]
---

1. **Mapping from Sample Space to Real Line:**
   The random variable \( X \) maps outcomes from the sample space (often denoted by \( \Omega \)) to the real line \( \mathbb{R} \). In doing so, we translate "events" in the sample space into intervals or sets on the real line.

2. **Lebesgue Measure on the Real Line:**
   When we consider the real line equipped with the Lebesgue measure \( \mu \), each point in \( \mathbb{R} \) has the same "mass," or density, under \( \mu \). However, in probability theory, we’re interested in reflecting how likely an event is—meaning we want to assign "masses" or densities in a way that reflects the likelihood of events in the sample space that map to subsets of \( \mathbb{R} \).

3. **Pushforward Measure and the Role of the Radon-Nikodym Derivative:**
   To translate between the sample space and the real line, we define a new measure \( P = X_* \mu \), which is the pushforward of the original measure. This measure \( P \) on \( \mathbb{R} \) tells us the probability of events on the real line based on the probability structure of the sample space.

   The **Radon-Nikodym theorem** ensures that, when \( P \) is absolutely continuous with respect to \( \mu \), we can express \( P \) in terms of \( \mu \) through a density function \( f \) (the Radon-Nikodym derivative \( f = \frac{dP}{d\mu} \)):

   \[
   P(A) = \int_A f \, d\mu.
   \]

4. **Interpretation of the Density \( f \):**
   This density \( f \) tells us how to "reweight" the Lebesgue measure to reflect the actual probability structure of events in the sample space. Now, for each interval \( t + dt \in \mathbb{R} \), \( f(t) \) represents the likelihood density for \( X^{-1}(t+dt) \)—that is, the part of the sample space that maps into this interval on the real line.

5. **Absolute Continuity and Consistency with Probability Theory:**
   The Radon-Nikodym construction guarantees that \( P \) is absolutely continuous with respect to \( \mu \), meaning that \( P(A) = 0 \) whenever \( \mu(A) = 0 \). This condition is crucial in probability, as it ensures that our probability assignments do not contradict the underlying structure of the real line.

In essence, the Radon-Nikodym theorem provides a formal framework for transforming one measure into another, which is precisely what allows us to create a probability distribution on the real line that reflects the likelihood of events in the sample space. It gives us the exact "transforming function" (the density \( f \)) to accomplish this, ensuring consistency between the original and the new measure.

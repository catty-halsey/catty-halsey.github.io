---
layout: post
title: "M-estimator and admissible estimator"
author: "Ziyan Li"
categories: journal
tags: [documentation, sample]
---

### **1. Empirical vs. Theoretical Risk**
- **M-Estimators:** Derived from **minimizing empirical risk** based on observed data. This means the M-estimator does not have full access to the entire \( X \)-sigma algebra, as it only utilizes information from the finite sample \( X_1, \ldots, X_n \). As the number of observations increases, the empirical measure \( \mathbb{P}_n \) converges to the true distribution \( P \), and thus the M-estimator asymptotically incorporates more information about \( X \). This convergence explains the **asymptotic behavior** of M-estimators.

- **Admissible Estimators:** Derived from **minimizing theoretical risk**, often leveraging the complete \( X \)-sigma algebra. This full access to information means admissible estimators are globally optimal and dominate other estimators in terms of risk, making them robust and theoretically sound.

---

### **2. Information Contained in \( X \)**
- **M-Estimators:** Start with partial information, as they rely on a finite number of observations. This limitation makes them more prone to estimation error in small samples. However, with increasing \( n \), the M-estimator captures more of the underlying structure of \( X \), leading to consistency and asymptotic efficiency.
  
- **Admissible Estimators:** Utilize all available information about \( X \) right from the start, ensuring robustness. For example, the Bayes estimator \( \mathbb{E}[\theta \mid X] \) is derived from the full posterior distribution of \( \theta \), which reflects all the information encoded in the data-generating process.

---

### **3. Asymptotic Behavior**
- As you noted, **M-estimators become more similar to admissible estimators** as \( n \to \infty \), because the empirical measure \( \mathbb{P}_n \) approaches the true probability measure \( P \). This convergence ensures that the M-estimator increasingly aligns with the theoretically optimal solution.
- Admissible estimators, by contrast, are not tied to sample size or empirical measures. They are inherently optimal based on the true underlying distribution, providing a **globally minimized risk** regardless of sample size.

---

### **4. Robustness**
- **M-Estimators:** Robustness is limited in finite samples due to the dependence on empirical data. They can be sensitive to outliers, model misspecification, or small sample sizes.
- **Admissible Estimators:** Their robustness stems from their derivation using the full \( X \)-sigma algebra. This ensures they are **globally optimal** and dominate other estimators in the risk sense.

---

### **5. Refined Summary of Key Difference**
The key distinction is:
1. **M-estimators are empirical risk minimizers**, relying on finite data and progressively improving as sample size increases. Their asymptotic behavior allows them to approximate admissible estimators over time.
2. **Admissible estimators are theoretical risk minimizers**, leveraging the full \( X \)-sigma algebra to achieve global optimality and robustness. They are inherently independent of finite sample size considerations.

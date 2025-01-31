---
layout: default
title: "Hypothesis Testing in Statistics: A Comprehensive Guide with Python"
description: "Learn statistical hypothesis testing with practical Python examples. Covers p-values, test statistics, and common statistical tests with real-world applications."
keywords: hypothesis testing, statistical analysis, p-value, null hypothesis, alternative hypothesis, python statistics
author: Rishuraj Gautam
date: 2024-01-20
last_modified_at: 2024-01-20
canonical_url: https://yourdomain.com/statistical-theory/hypothesis-testing/
---

# Hypothesis Testing: A Comprehensive Guide

> **Quick Guide**: Master the fundamentals of statistical hypothesis testing with Python implementations and practical examples.

{% include mathjax.html %}

## **Key Concepts**

### 1. **Hypothesis Types**
- **Null Hypothesis (\\(H_0\\))**: The default assumption
- **Alternative Hypothesis (\\(H_1\\))**: The claim we want to test

### 2. **Critical Components**
- **Significance Level (\\(\alpha\\))**: Typically 0.05 or 0.01
- **Test Statistic**: Standardized value (e.g., z-score, t-score)
- **p-value**: Probability under \\(H_0\\)

### 3. **Type I vs. Type II Errors**
   - **Type I Error (False Positive):** Rejecting H₀ when it is true.
   - **Type II Error (False Negative):** Failing to reject H₀ when it is false.

---

## **Steps in Hypothesis Testing**
1. **State Hypotheses:** Define H₀ and H₁.
2. **Choose Significance Level (α):** Typically 0.05.
3. **Select Appropriate Test:** e.g., z-test, t-test, chi-square.
4. **Calculate Test Statistic:** Use sample data.
5. **Determine Critical Value or p-value:**
   - Compare the test statistic to a critical value from statistical tables.
   - Alternatively, calculate the p-value.
6. **Make a Decision:** Reject H₀ if the test statistic falls in the rejection region or \( p\text{-value} < \alpha \).

---

## **Types of Tests**
### 1. **Parametric Tests**
   - Assume data follows a specific distribution (e.g., normal).
   - Examples: z-test, t-test, ANOVA.

### 2. **Non-Parametric Tests**
   - No distributional assumptions.
   - Examples: Mann-Whitney U test, Wilcoxon signed-rank test.

### 3. **One-Tailed vs. Two-Tailed Tests**
   - **One-Tailed:** Tests for effect in **one direction** (e.g., \( \mu > \mu_0 \)).
   - **Two-Tailed:** Tests for effect in **both directions** (e.g., \( \mu \neq \mu_0 \)).

---

## **Example: Z-Test for Population Mean**
### **Scenario**
A company claims its light bulbs last 1200 hours. A sample of 50 bulbs has a mean lifespan of 1150 hours with a known population standard deviation of 150 hours. Test if the mean lifespan is less than 1200 hours at \( \alpha = 0.05 \).

### **Hypotheses**
- \( H₀: \mu = 1200 \)
- \( H₁: \mu < 1200 \)

## **Python Implementation**
```python
import scipy.stats as stats
import numpy as np
import matplotlib.pyplot as plt

def perform_hypothesis_test(data, null_mean, alpha=0.05):
    """
    Perform one-sample t-test
    """
    t_stat, p_value = stats.ttest_1samp(data, null_mean)
    return {
        't_statistic': t_stat,
        'p_value': p_value,
        'reject_null': p_value < alpha
    }

# Example usage
np.random.seed(42)
sample_data = np.random.normal(loc=1150, scale=150, size=50)
results = perform_hypothesis_test(sample_data, 1200)

print(f"T-Statistic: {results['t_statistic']:.2f}")
print(f"P-value: {results['p_value']:.4f}")
print(f"Reject H₀: {results['reject_null']}")
```

## **Interactive Visualization**
```python
def plot_hypothesis_test(data, null_mean, alpha=0.05):
    plt.figure(figsize=(10, 6))
    
    # Plot distribution
    x = np.linspace(null_mean - 4*150/np.sqrt(50), 
                    null_mean + 4*150/np.sqrt(50), 100)
    y = stats.norm.pdf(x, null_mean, 150/np.sqrt(50))
    
    plt.plot(x, y, 'b-', label='Null Distribution')
    plt.axvline(np.mean(data), color='r', linestyle='--', 
                label='Sample Mean')
    
    # Shade rejection region
    critical_value = stats.norm.ppf(alpha, null_mean, 
                                  150/np.sqrt(50))
    x_fill = x[x <= critical_value]
    y_fill = y[x <= critical_value]
    plt.fill_between(x_fill, y_fill, alpha=0.3, color='r',
                    label='Rejection Region')
    
    plt.title('Hypothesis Test Visualization')
    plt.xlabel('Sample Mean')
    plt.ylabel('Probability Density')
    plt.legend()
    plt.grid(True, alpha=0.3)
    plt.show()

# Example usage
plot_hypothesis_test(sample_data, 1200)
```

## **Common Mistakes to Avoid**
1. Misinterpreting p-values
2. Ignoring effect size
3. Multiple testing without correction

## **Best Practices**
1. Always state hypotheses clearly
2. Report effect sizes alongside p-values
3. Consider practical significance

**Related Articles:**
- [Chi-Square Test Guide](chi-square-test-goodness-of-fit.md)
- [Understanding P-Values](p-values.md)
- [Effect Size Analysis](effect-size.md)

**Keywords**: statistical testing, hypothesis testing, p-value, statistical significance, python statistics, data analysis

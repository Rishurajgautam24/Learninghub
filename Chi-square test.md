# Chi-Square Test for Goodness of Fit

The **Chi-Square Test for Goodness of Fit** is a statistical hypothesis test used to determine whether observed categorical data follows an expected theoretical distribution. It compares observed frequencies to expected frequencies to assess if deviations are statistically significant.

---

## **Purpose**
- Test whether a sample dataset matches a population with a specific distribution.
- Evaluate if observed frequencies differ significantly from expected frequencies under a null hypothesis.

---

## **Hypotheses**
- **Null Hypothesis (H₀):** Observed data follows the expected distribution.
- **Alternative Hypothesis (H₁):** Observed data does not follow the expected distribution.

---

## **Assumptions**
1. **Categorical Data:** Data must be divided into discrete categories.
2. **Independence:** Observations are independent of each other.
3. **Expected Frequencies:** Each category should have an expected frequency of at least 5. If not, combine categories.

---

## **Test Statistic Formula**
The Chi-Square statistic ($\chi^2$) measures the discrepancy between observed and expected frequencies:

$\chi^2 = \sum_{i=1}^{k} \frac{(O_i - E_i)^2}{E_i}$

Where:
- $O_i$ = Observed frequency in category $i$
- $E_i$ = Expected frequency in category $i$
- $k$ = Number of categories

### **Mathematical Steps**
1. For each category $i$:
   - Calculate difference: $(O_i - E_i)$
   - Square the difference: $(O_i - E_i)^2$
   - Divide by expected: $\frac{(O_i - E_i)^2}{E_i}$
2. Sum all terms

### **Degrees of Freedom**
$df = k - 1 - m$
where:
- $k$ = number of categories
- $m$ = number of parameters estimated from the data

For our die example:
- $k = 6$ (six faces)
- $m = 0$ (no parameters estimated)
- Therefore, $df = 6 - 1 - 0 = 5$

### **Critical Values Table (α = 0.05)**
| df | Critical Value |
|----|---------------|
| 1  | 3.841         |
| 2  | 5.991         |
| 3  | 7.815         |
| 4  | 9.488         |
| 5  | 11.070        |

---

## **Steps to Perform the Test**
1. **Define Hypotheses:** State \(H₀\) and \(H₁\).
2. **Calculate Expected Frequencies:** Use theoretical distribution or equal probabilities.
3. **Compute Chi-Square Statistic:** Apply the formula.
4. **Determine Degrees of Freedom (df):** \(df = k - 1 - p\), where \(k\) = number of categories, \(p\) = parameters estimated.
5. **Find Critical Value or P-value:** Use Chi-Square distribution table or software.
6. **Conclusion:** Reject \(H₀\) if \(\chi^2 > \text{critical value}\) or \(p\text{-value} < \alpha\).

---

## **Example: Testing Fairness of a Die**
### **Scenario**
A die is rolled 60 times. Test if the die is fair at \(\alpha = 0.05\).

### **Observed Frequencies**
| Category | 1  | 2  | 3  | 4  | 5  | 6  |
|----------|----|----|----|----|----|----|
| Observed | 12 | 8  | 9  | 15 | 6  | 10 |

### **Expected Frequencies**
For a fair die, each category expects \( \frac{60}{6} = 10 \).

---

## **Detailed Calculation Example**
For our die roll data:

| Face | $O_i$ | $E_i$ | $(O_i - E_i)^2$ | $\frac{(O_i - E_i)^2}{E_i}$ |
|------|-------|-------|-----------------|------------------------------|
| 1    | 12    | 10    | 4              | 0.400                        |
| 2    | 8     | 10    | 4              | 0.400                        |
| 3    | 9     | 10    | 1              | 0.100                        |
| 4    | 15    | 10    | 25             | 2.500                        |
| 5    | 6     | 10    | 16             | 1.600                        |
| 6    | 10    | 10    | 0              | 0.000                        |
| Sum  | 60    | 60    | -              | 5.400                        |

Therefore, $\chi^2 = 5.400$

With $df = 5$ and $\alpha = 0.05$:
- Critical value = 11.070
- Since $5.400 < 11.070$, we fail to reject $H_0$

---

## **Python Code Example**
```python
import numpy as np
from scipy.stats import chisquare
import matplotlib.pyplot as plt

# Observed and expected frequencies
observed = np.array([12, 8, 9, 15, 6, 10])
expected = np.array([10, 10, 10, 10, 10, 10])

# Perform Chi-Square test
chi2_stat, p_value = chisquare(f_obs=observed, f_exp=expected)
print(f"Chi-Square Statistic: {chi2_stat:.2f}")
print(f"P-value: {p_value:.4f}")

# Interpret results
alpha = 0.05
print("\nConclusion:")
if p_value < alpha:
    print("Reject H₀: The die is not fair.")
else:
    print("Fail to reject H₀: The die is fair.")

# Visualization
categories = ['1', '2', '3', '4', '5', '6']
x = np.arange(len(categories))

plt.figure(figsize=(8, 5))
plt.bar(x - 0.1, observed, width=0.2, label='Observed', color='blue')
plt.bar(x + 0.1, expected, width=0.2, label='Expected', color='orange')
plt.xticks(x, categories)
plt.xlabel('Die Faces')
plt.ylabel('Frequency')
plt.title('Observed vs Expected Frequencies')
plt.legend()
plt.show()
```

---

## **Output Interpretation**
- **Chi-Square Statistic:** 5.00
- **$P-value$:** 0.4159
- **Conclusion:** Since $ p \text{-value} > 0.05$, fail to reject \(H₀\). No evidence to suggest the die is unfair.

---

## **Visualization**
![Observed vs Expected Frequencies](images/download.png)  
*(Actual plot will show blue bars for observed and orange bars for expected frequencies.)*

---

## **Limitations**
- Requires sufficient expected frequencies ($≥5$ per category).
- Sensitive to sample size; large samples may trivialize small deviations.

---

## **Conclusion**
The Chi-Square Goodness of Fit test is a non-parametric method to validate hypotheses about distributions. It is widely used in quality control, genetics, and social sciences to test theoretical models against empirical data.


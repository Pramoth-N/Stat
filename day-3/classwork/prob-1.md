# Z-Test for a Single Population Mean

## Description

Create a Python program that performs a Z-test for a single population mean based on user input.

---

## Steps

1. **Accept sample statistics and test parameters from the user:**
   - Sample mean (x̄)
   - Hypothesized population mean (μ₀)
   - Population standard deviation (σ)
   - Sample size (n)
   - Type of test (`greater`, `less`, or `two-sided`)
   - Significance level (α, default = 0.05)
2. **Calculate the Z-statistic using the formula.**
3. **Compute the p-value based on the test type.**
4. **Print the Z-statistic, p-value, and the final hypothesis test conclusion.**

---

## Input Format

- **Line 1:** Sample mean (x̄) as a float
- **Line 2:** Hypothesized population mean (μ₀) as a float
- **Line 3:** Population standard deviation (σ) as a float
- **Line 4:** Sample size (n) as an integer
- **Line 5:** Type of test: `'greater'`, `'less'`, or `'two-sided'`
- **Line 6:** Significance level α (optional, default is 0.05)

---

## Output Format

- Display the Z-statistic rounded to 4 decimal places.
- Display the P-value rounded to 4 decimal places.
- Display one of the following conclusions:
  - `"Reject the null hypothesis."` if p-value < alpha
  - `"Fail to reject the null hypothesis."` otherwise

---

## Code Constraints

- `test_type` must be one of: `'greater'`, `'less'`, or `'two-sided'`.
- If no alpha is provided, default is 0.05.
- Requires valid numeric input for all statistical values.
- Requires `math` and `scipy.stats.norm` for Z-test calculation.

---

## Sample Test Case

**Input 1:**
```
66.4
65
10.4
60
greater
0.05
```

**Output 1:**
```
Z-statistic: 1.0427
P-value: 0.1485
Fail to reject the null hypothesis.
```

---

## Sample Implementation

```python
import math
from scipy.stats import norm

x = float(input())
mu = float(input())
sigma = float(input())
n = int(input())
type_test = input()
alpha_in = input()

alpha = float(alpha_in) if alpha_in else 0.05

z_stat = (x - mu) / (sigma / math.sqrt(n))  # One sample Z-test formula

print(f"Z-statistic: {round(z_stat, 4)}")

if type_test == 'greater':
    p_stat = 1 - norm.cdf(z_stat)
elif type_test == 'less':
    p_stat = norm.cdf(z_stat)
elif type_test == 'two-sided':
    p_stat = 2 * (1 - norm.cdf(abs(z_stat)))
else:
    raise ValueError("Invalid test type. Choose 'greater', 'less', or 'two-sided'.")

print(f"P-value: {round(p_stat, 4)}")

if p_stat < alpha:
    print("Reject the null hypothesis.")
else:
    print("Fail to reject the null hypothesis.")
```
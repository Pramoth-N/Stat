# Program Description

This program analyzes customer preferences for two types of coffee—**Latte** and **Black Coffee**—across three age groups: **18–25**, **26–40**, and **40+**.  
It calculates:

- The **joint probability** that a customer is 40 or older and prefers Black Coffee
- The **conditional probability** that a customer prefers Black Coffee given they are 40 or older
- The **overall probability** of preferring Black Coffee
- Whether age (**being 40 or older**) influences preference for Black Coffee, based on whether the conditional probability significantly differs from the overall probability.

---

## Input Format

The program asks the user to input counts of customers who prefer each coffee type for each age group:

- **For age group 18–25:**  
  - Number of customers who prefer Latte  
  - Number of customers who prefer Black Coffee

- **For age group 26–40:**  
  - Number of customers who prefer Latte  
  - Number of customers who prefer Black Coffee

- **For age group 40+:**  
  - Number of customers who prefer Latte  
  - Number of customers who prefer Black Coffee

All inputs must be **non-negative integers**.

---

## Output Format

After receiving inputs, the program outputs:

1. A **data summary table** showing the counts for each coffee preference by age group.
2. The **joint probability** of a customer being 40+ and preferring Black Coffee.
3. The **conditional probability** of preferring Black Coffee given the customer is 40+.
4. The **overall probability** of preferring Black Coffee across all customers.
5. A **conclusion** on whether age (specifically being 40 or older) influences Black Coffee preference, by comparing the conditional and overall probabilities.

---

## Code Constraints

- All counts must be integers **≥ 0**.
- If the **total number of customers is zero**, the program exits with an error message.
- If there are **no customers in the 40+ group**, the conditional probability cannot be computed and the program exits with an error message.

---

## Sample Test Case

**Input 1:**  
```
30
10
25
25
5
25
```

**Output 1:**
```
Age group: 18–25
Number of customers who prefer Latte: Number of customers who prefer Black Coffee: 
Age group: 26–40
Number of customers who prefer Latte: Number of customers who prefer Black Coffee: 
Age group: 40+
Number of customers who prefer Latte: Number of customers who prefer Black Coffee: 
Data Summary:
       Latte  Black Coffee
18–25     30            10
26–40     25            25
40+        5            25

Joint Probability P(Age 40+ and Black Coffee): 0.2083
Conditional Probability P(Black Coffee | Age 40+): 0.8333

Overall Probability P(Black Coffee): 0.5000
Conditional Probability P(Black Coffee | Age 40+): 0.8333
Age (being 40 or older) influences preference for Black Coffee.
```

---

```python
import sys
import pandas as pd

def get_int_input(prompt):
    try:
        value = int(input(prompt))
        if value < 0:
            print("Please enter a non-negative integer.")
            sys.exit(1)
        return value
    except ValueError:
        print("Invalid input! Please enter an integer.")
        sys.exit(1)

age_groups = ['18–25', '26–40', '40+']
coffee_types = ['Latte', 'Black Coffee']

data = {coffee: [] for coffee in coffee_types}

for age in age_groups:
    print(f"\nAge group: {age}")
    for coffee in coffee_types:
        count = get_int_input(f"Number of customers who prefer {coffee}: ")
        data[coffee].append(count)

df = pd.DataFrame(data, index=age_groups)

total_customers = df.values.sum()
if total_customers == 0:
    print("No data provided (total customers = 0). Exiting.")
    sys.exit(1)

print("\nData Summary:")
print(df)

joint_prob_older_black = df.loc['40+', 'Black Coffee'] / total_customers
print(f"\nJoint Probability P(Age 40+ and Black Coffee): {joint_prob_older_black:.4f}")

total_40plus = df.loc['40+'].sum()
if total_40plus == 0:
    print("No customers in the 40+ age group, conditional probability undefined.")
    sys.exit(1)

black_40plus = df.loc['40+', 'Black Coffee']
cond_prob_black_given_40plus = black_40plus / total_40plus
print(f"Conditional Probability P(Black Coffee | Age 40+): {cond_prob_black_given_40plus:.4f}")

overall_prob_black = df['Black Coffee'].sum() / total_customers
print(f"\nOverall Probability P(Black Coffee): {overall_prob_black:.4f}")
print(f"Conditional Probability P(Black Coffee | Age 40+): {cond_prob_black_given_40plus:.4f}")

if abs(cond_prob_black_given_40plus - overall_prob_black) < 1e-4:
    print("Age (being 40 or older) does NOT influence preference for Black Coffee.")
else:
    print("Age (being 40 or older) influences preference for Black Coffee.")
```

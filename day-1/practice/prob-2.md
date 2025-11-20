# BuyBloom Age Group Purchase Probability Analyzer

## Program Description

This program helps **BuyBloom** analyze customer purchase patterns across different age groups using joint and conditional probability concepts.

---

## Features

- **User Input:**  
  For four products (Product A, B, C, D), the user inputs 4 comma-separated integers each, representing purchase counts for the age groups:  
  `<25`, `25-40`, `41-60`, `60+`.

- **Probability Calculations:**  
  Based on the input data, the program calculates:
  1. Probability that a randomly selected purchase is for **Product A** by someone aged **below 25**.
  2. Conditional probability that a purchase was made by someone aged **25-40**, **given** they bought **Product C**.
  3. Overall probability that a randomly selected buyer is from the **41-60** age group.
  4. Determines independence between purchases of **Product B** and buyers aged **60+** by comparing joint and marginal probabilities.

---

## Input Format

For each product (`Product A`, `Product B`, `Product C`, `Product D`):  
Enter **4 comma-separated integers** — purchase counts for the age groups in this order:  
`<25`, `25-40`, `41-60`, `60+`.

**Example:**  
`120, 80, 60, 20`

---

## Output Format

- Probability of Product A purchase by someone aged <25 (rounded to 4 decimal places).
- Probability of buyer being aged 25-40 **given** a Product C purchase (rounded to 4 decimal places).
- Overall probability of a buyer being in the 41-60 age group (rounded to 4 decimal places).
- Joint and marginal probabilities for Product B and Age 60+, with a conclusion about their independence.

---

## Code Constraints

- All input counts must be non-negative integers.
- The number of counts entered for each product must exactly match the number of age groups (4).
- Probabilities are calculated assuming all purchases are mutually exclusive and collectively exhaustive within the dataset.

---

## Sample Test Cases

**Input 1:**
```
120, 80, 60, 20
90, 100, 40, 10
70, 60, 30, 15
50, 40, 70, 25
```

**Output 1:**
```
Enter counts for Product A: Enter counts for Product B: Enter counts for Product C: Enter counts for Product D: 
Probability of Product A by someone aged < 25: 0.1364
Probability of age 25-40 given Product C purchase: 0.3429
Overall probability of buyer from 41-60 age group: 0.2273

P(Product B and Age 60+): 0.0114
    P(Product B): 0.2727
    P(Age 60+): 0.0795
    P(Product B) * P(Age 60+): 0.0217
Conclusion: Product B purchases and Age 60+ are DEPENDENT.
```

```python

prodA = list(map(int, input("Enter counts for Product A: ").split(',')))
prodB = list(map(int, input("Enter counts for Product B: ").split(',')))
prodC = list(map(int, input("Enter counts for Product C: ").split(',')))
prodD = list(map(int, input("Enter counts for Product D: ").split(',')))

a_total = sum(prodA)
b_total = sum(prodB)
c_total = sum(prodC)
d_total = sum(prodD)

total = a_total + b_total + c_total + d_total

prob_a_25 = prodA[0] / total

print()
print(f"Probability of Product A by someone aged < 25: {prob_a_25:.4f}")

prob_c_25_40 = prodC[1] / c_total
print(f"Probability of age 25-40 given Product C purchase: {prob_c_25_40:.4f}")

total_41_60 = prodA[2] + prodB[2] + prodC[2] + prodD[2]
prob_41_60 = total_41_60 / total
print(f"Overall probability of buyer from 41-60 age group: {prob_41_60:.4f}")

print()

b_and_60 = prodB[3] / total
print(f"P(Product B and Age 60+): {b_and_60:.4f}")

b_prob = b_total / total
print(f"    P(Product B): {b_prob:.4f}")

total_60 = prodA[3] + prodB[3] + prodC[3] + prodD[3]
prob_60 = total_60 / total
print(f"    P(Age 60+): {prob_60:.4f}")

b_mul_60 = b_prob * prob_60
print(f"    P(Product B) * P(Age 60+): {b_mul_60:.4f}")

if abs(b_mul_60 - b_and_60) < 1e-9:
    print("Conclusion: Product B purchases and Age 60+ are INDEPENDENT.")
else:
    print("Conclusion: Product B purchases and Age 60+ are DEPENDENT.")
# print("Conclusion: Product B purchases and Age 60+ are DEPENDENT.")
```

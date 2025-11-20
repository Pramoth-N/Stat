# BuyBloom Probability Calculator

## Program Description

This program helps **BuyBloom** analyze customer behavior and logistics using basic probability calculations. It covers four business scenarios:

---

### 1. Order Return Probability

*Given the total number of orders shipped and the number of returned orders, it calculates the probability that a randomly selected order was **not** returned.*

---

### 2. Delivery Partner On-Time Probability

*Given the total number of delivery partners and the number of delayed partners, it calculates the probability that two randomly chosen partners are both on time (chosen without replacement).*

---

### 3. Flash Sale Discount Probability

*Given the probability that a single product receives a discount during a flash sale and the number of products chosen, it calculates the probability that **all** selected products get a discount.*

---

### 4. Flash Deal Day Probability

*Given the number of days in a week and the number of days with flash deals, it calculates the probability that logging in on a random day finds an active flash deal.*

---

## Input Format

You will be prompted to enter the following, in order:

1. **Total number of orders shipped** (*integer*)
2. **Number of returned orders** (*integer*)
3. **Total delivery partners** (*integer*)
4. **Number of delayed partners** (*integer*)
5. **Probability of discount on a single product** (*decimal between 0 and 1*)
6. **Number of products chosen for discount check** (*integer*)
7. **Total days in a week** (*integer*)
8. **Number of flash deal days in the week** (*integer*)

---

## Output Format

The program prints:

- Probability that a randomly selected order was **not returned** (rounded to 4 decimal places)
- Probability that **two randomly chosen delivery partners** are both on time (rounded to 4 decimal places)
- Probability that **all chosen products** get a discount (rounded to 4 decimal places)
- Probability of **finding a flash deal on a random day** (rounded to 4 decimal places)

---

## Code Constraints

- All input values must be valid positive numbers (probabilities between 0 and 1).
- Number of delayed partners **cannot exceed** total delivery partners.
- Number of products chosen must be a **positive integer**.
- Number of flash deal days cannot exceed total days in a week.

---

## Sample Test Case

**Input:**
```
100
8
50
5
0.7
3
7
3
```
**Output:**
```
BuyBloom Probability Calculator
Enter total number of orders shipped: Enter number of orders returned: Probability a randomly selected order was NOT returned: 0.9200

Enter total number of delivery partners: Enter number of delayed partners: Probability both randomly chosen partners are on time: 0.8082

Enter probability of a product getting a discount (0 to 1): Enter number of products chosen: Probability all 3 randomly chosen products get discount: 0.3430

Enter total number of days in the period (e.g., 7): Enter number of days with deals (out of 7): Probability of finding a deal on a random day: 0.4286
```

---

```python
import sys

def get_int_input(prompt):
    try:
        val = int(input(prompt))
        if val < 0:
            print("Please enter a non-negative integer.")
            sys.exit(1)
        return val
    except ValueError:
        print("Invalid input! Please enter an integer.")
        sys.exit(1)

def get_float_input(prompt):
    try:
        val = float(input(prompt))
        if val < 0 or val > 1:
            print("Please enter a probability between 0 and 1.")
            sys.exit(1)
        return val
    except ValueError:
        print("Invalid input! Please enter a decimal number.")
        sys.exit(1)

print("BuyBloom Probability Calculator")

# Order Return Probability
total_orders = get_int_input("Enter total number of orders shipped: ")
returned_orders = get_int_input("Enter number of orders returned: ")

if returned_orders > total_orders:
    print("Returned orders cannot exceed total orders.")
    sys.exit(1)

not_returned_orders = total_orders - returned_orders
probability_not_returned = not_returned_orders / total_orders
print(f"Probability a randomly selected order was NOT returned: {probability_not_returned:.4f}\n")

# Delivery Partner On-Time Probability
total_partners = get_int_input("Enter total number of delivery partners: ")
delayed_partners = get_int_input("Enter number of delayed partners: ")

if delayed_partners > total_partners:
    print("Delayed partners cannot exceed total partners.")
    sys.exit(1)

on_time_partners = total_partners - delayed_partners

if total_partners < 2:
    print("Need at least 2 partners to choose from.")
    sys.exit(1)

prob_first_on_time = on_time_partners / total_partners
prob_second_on_time_given_first = (on_time_partners - 1) / (total_partners - 1)
probability_both_on_time = prob_first_on_time * prob_second_on_time_given_first

print(f"Probability both randomly chosen partners are on time: {probability_both_on_time:.4f}\n")

# Flash Sale Discount Probability
prob_discount = get_float_input("Enter probability of a product getting a discount (0 to 1): ")
num_products = get_int_input("Enter number of products chosen: ")

prob_all_discounts = prob_discount ** num_products
print(f"Probability all {num_products} randomly chosen products get discount: {prob_all_discounts:.4f}\n")

# Flash Deal Day Probability
total_days = get_int_input("Enter total number of days in the period (e.g., 7): ")
days_with_deals = get_int_input(f"Enter number of days with deals (out of {total_days}): ")

if days_with_deals > total_days:
    print("Days with deals cannot exceed total days.")
    sys.exit(1)

prob_deal = days_with_deals / total_days
print(f"Probability of finding a deal on a random day: {prob_deal:.4f}")
```

# Program Description

This Python program calculates the number of ways to choose a specific number of ice cream flavors from a list of options, considering two scenarios:

1. **Without Replacement** – Each flavor can be chosen only once per combination.
2. **With Replacement** – Flavors can be repeated in combinations.

It takes user input and uses the `itertools` module to compute the results.

---

## Input Format

The program requires two inputs from the user:

- **A list of ice cream flavors, separated by commas**  
  *Example:*  
  `Vanilla, Chocolate, Strawberry, Mango, Mint`
- **An integer representing the number of flavors to choose**  
  *Example:*  
  `3`

---

## Output Format

After taking inputs, the program displays:
- The total number of combinations **without replacement**
- The total number of combinations **with replacement**

---

## Code Constraints

- The flavor list must **not be empty**.
- The number of choices must be a **positive integer**.
- The number of choices cannot exceed the number of available flavors (**for combinations without replacement**).
- If invalid input is provided, the program will exit with an error message.

---

## Sample Test Case

**Input 1:**
```
Banana, Chocolate, Orange, Strawberry, Vanilla
3
```

**Output 1:**
```
Ice Cream Flavor Combination Calculator
Enter ice cream flavors separated by commas (e.g., Vanilla, Chocolate, etc.): How many flavors do you want to choose (out of 5 available)?:
Flavor Combinations
Total combinations without replacement: 10
Total combinations with replacement: 35
```

---

```python
import sys
import itertools

def get_list_input(prompt):
    raw = input(prompt).strip()
    if not raw:
        print("Input cannot be empty.")
        sys.exit(1)
    return [item.strip() for item in raw.split(',') if item.strip()]

def get_int_input(prompt):
    try:
        val = int(input(prompt))
        if val <= 0:
            print("Please enter a positive integer.")
            sys.exit(1)
        return val
    except ValueError:
        print("Invalid input! Please enter a valid integer.")
        sys.exit(1)

print("Ice Cream Flavor Combination Calculator")
flavors = get_list_input("Enter ice cream flavors separated by commas (e.g., Vanilla, Chocolate, etc.): ")
num_flavors = get_int_input(f"How many flavors do you want to choose (out of {len(flavors)} available)?: ")

if num_flavors > len(flavors):
    print("Cannot choose more flavors than available (without replacement).")
    sys.exit(1)

combinations_without_replacement = list(itertools.combinations(flavors, num_flavors))
combinations_with_replacement = list(itertools.combinations_with_replacement(flavors, num_flavors))

print(f"\nFlavor Combinations")
print(f"Total combinations without replacement: {len(combinations_without_replacement)}")
print(f"Total combinations with replacement: {len(combinations_with_replacement)}")
```
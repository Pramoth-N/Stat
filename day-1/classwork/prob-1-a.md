# Program Description

This program simulates a set of coin tosses and calculates the probability of heads and tails based on the number of tosses. It also calculates the theoretical probability of rolling a specific number on a standard six-sided die.

---

## Input Format

The program takes two inputs:

- **Number of coin tosses** — an integer **N** (must be ≥ 0)
- **Desired dice number** — an integer **D** (must be between 1 and 6)

---

## Output Format

### Coin Toss Results:
- Total number of heads and tails observed
- Probability of heads (rounded to two decimal places)
- Probability of tails (rounded to two decimal places)

### Dice Roll Probability:
- The theoretical probability of rolling the desired number on a 6-sided die (as a fraction and decimal)

**If inputs are invalid, appropriate error messages are shown.**

---

## Code Constraints

- `num_tosses` must be a non-negative integer  
  *Examples: 0, 10, 100 are valid.*

- `desired_dice_number` must be an integer between 1 and 6  
  *Only values from 1 to 6 are allowed.*

- If `num_tosses` is 0, the program should show a message and not calculate probabilities.

- Inputs must be valid integers  
  *If not, the program should display an error and stop.*

- Coin tosses should be randomly chosen as either `'Head'` or `'Tail'` for each toss.

- Dice probability is fixed:  
  *The chance of rolling any number from 1 to 6 is always 1/6.*

- **Probabilities should be rounded:**
  - Coin toss results: rounded to 2 decimal places
  - Dice roll probability: shown as both fraction and 4-digit decimal (e.g., 0.1667)

---

## Sample Test Cases

**Input 1:**
```
10
3
```

**Output 1:**
```
Enter number of coin tosses: Enter desired dice number (1–6):

--- Coin Toss Results ---
Head: 4, Tail: 6
Probability of Head: 0.40
Probability of Tail: 0.60

--- Dice Roll Probability ---
The probability of rolling a 3 is: 0.1667
Which is also: 1/6
```

---

```python
import random

try:
    num_tosses = int(input("Enter number of coin tosses: "))
    desired_number = int(input("Enter desired dice number (1–6): "))
except ValueError:
    print("Invalid input. Please enter integers.")
    exit(1)

# --- Coin Toss Simulation ---
outcomes = [random.choice(['Head', 'Tail']) for _ in range(num_tosses)]

head_count = outcomes.count('Head')
tail_count = outcomes.count('Tail')
total_outcomes = len(outcomes)

probability_head = head_count / total_outcomes
probability_tail = tail_count / total_outcomes

print("\n--- Coin Toss Results ---")
print(f"Head: {head_count}, Tail: {tail_count}")
print(f"Probability of Head: {probability_head:.2f}")
print(f"Probability of Tail: {probability_tail:.2f}")

# --- Dice Roll Probability ---
if 1 <= desired_number <= 6:
    favorable_outcomes = 1
    total_outcomes = 6
    probability = favorable_outcomes / total_outcomes

    print("\n--- Dice Roll Probability ---")
    print(f"The probability of rolling a {desired_number} is: {probability:.4f}")
    print(f"Which is also: {favorable_outcomes}/{total_outcomes}")
else:
    print("Invalid dice number! Must be between 1 and 6.")
```

# Program Description

This program calculates the probability of drawing two Kings consecutively without replacement from a deck of cards. 

The user provides:
- The initial number of Kings in the deck
- The total number of cards in the deck

The program then computes:

1. **The probability of drawing the first King from the deck.**
2. **The probability of drawing the second King given the first drawn card was a King (without replacement).**
3. **The overall probability of drawing two Kings consecutively without replacement.**

---

## Input Format

The program takes two integer inputs from the user:

- **Number of Kings in the deck** — an integer `K` (must be ≥ 0 and ≤ total cards)
- **Total number of cards in the deck** — an integer `N` (must be > 0)

---

## Output Format

- Initial number of Kings and total cards in the deck.
- Probability of drawing the first King (rounded to 4 decimal places).
- Number of Kings and total cards remaining after drawing the first King.
- Probability of drawing the second King given the first was a King (rounded to 4 decimal places).
- Overall probability of drawing two Kings consecutively without replacement (rounded to 4 decimal places).

---

## Code Constraints

- K (number of Kings) must be a non-negative integer and cannot exceed the total number of cards.
- N (total cards) must be a positive integer.
- The deck must contain at least one card.
- If the deck has only one card, the program will stop since drawing a second card is impossible.
- Inputs must be valid integers; otherwise, the program shows an error and exits.

---

## Sample Test Case

**Input 1:**
```
4
52
```

**Output 1:**
```
Enter the number of Kings in the deck: Enter the total number of cards in the deck: 
Initial Kings in deck: 4
Initial total cards in deck: 52
Probability of drawing the first King: 0.0769
Kings remaining after first draw: 3
Total cards remaining after first draw: 51
Probability of drawing the second King (given first was King and not replaced): 0.0588
Probability of drawing two Kings consecutively without replacement: 0.0045
```

---

```python
import sys

try:
    initial_kings = int(input("Enter the number of Kings in the deck: "))
    initial_total_cards = int(input("Enter the total number of cards in the deck: "))
except ValueError:
    print("Invalid input! Please enter integer values.")
    sys.exit(1)

if initial_kings < 0 or initial_total_cards <= 0 or initial_kings > initial_total_cards:
    print("Invalid input! Number of Kings must be >= 0 and <= total cards, and total cards must be > 0.")
    sys.exit(1)

probability_first_king = initial_kings / initial_total_cards
remaining_kings = initial_kings - 1
remaining_total_cards = initial_total_cards - 1

if remaining_total_cards == 0:
    print("Cannot draw a second card after drawing the first.")
    sys.exit(1)

probability_second_king_given_first = remaining_kings / remaining_total_cards
probability_both_kings = probability_first_king * probability_second_king_given_first

print(f"\nInitial Kings in deck: {initial_kings}")
print(f"Initial total cards in deck: {initial_total_cards}")
print(f"Probability of drawing the first King: {probability_first_king:.4f}")
print(f"Kings remaining after first draw: {remaining_kings}")
print(f"Total cards remaining after first draw: {remaining_total_cards}")
print(f"Probability of drawing the second King (given first was King and not replaced): {probability_second_king_given_first:.4f}")
print(f"Probability of drawing two Kings consecutively without replacement: {probability_both_kings:.4f}")

```


# Program Description

This Python program calculates the total number of possible PIN codes that can be generated using a user-defined set of digits, under two conditions:

1. **Without Replacement:** Digits in the PIN do not repeat.
2. **With Replacement:** Digits can repeat in the PIN.

The program utilizes Python's `itertools` module and takes all input directly from the user.

---

## Input Format

The program accepts two user inputs:

- **Digits:**  
  A list of characters or numbers, separated by commas  
  _Example:_ `0,1,2,3,4`

- **PIN Length:**  
  An integer specifying how many digits the PIN should contain  
  _Example:_ `3`

---

## Output Format

After receiving inputs, the program displays:

- The total number of unique-digit PINs (no digit is repeated – permutation without replacement)
- The total number of PINs with repeated digits allowed (permutation with replacement)

---

## Code Constraints

- The list of digits must not be empty.
- The PIN length must be a positive integer.
- The PIN length must not exceed the number of digits when calculating permutations without replacement.
- If any input is invalid, the program will show an error and exit.

---

## Sample Test Case

**Input 1:**
```
0,1,2,3,4
3
```

**Output 1:**
```
PIN Permutation Generator
Enter digits to use for PIN separated by commas (e.g., 0,1,2,3,4): Enter the length of the PIN (e.g., 3): 
PIN Permutations
Total PINs without replacement (unique digits): 60
Total PINs with replacement (digits can repeat): 125
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

print("PIN Permutation Generator")
digits = get_list_input("Enter digits to use for PIN separated by commas (e.g., 0,1,2,3,4): ")
pin_length = get_int_input("Enter the length of the PIN (e.g., 3): ")

if pin_length > len(digits):
    print("PIN length exceeds number of available digits (for permutations without replacement).")
    sys.exit(1)

permutations_without_replacement = list(itertools.permutations(digits, pin_length))
permutations_with_replacement = list(itertools.product(digits, repeat=pin_length))

print(f"\nPIN Permutations")
print(f"Total PINs without replacement (unique digits): {len(permutations_without_replacement)}")
print(f"Total PINs with replacement (digits can repeat): {len(permutations_with_replacement)}")
```

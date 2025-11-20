# Problem Description

You are given two integers, **n** and **r**, where **n** represents the total number of distinct items and **r** represents the number of items to select from these **n** items.  
Your task is to calculate the total number of possible **permutations** when selecting **r** items from **n** items, where the order of selection **does** matter (**permutations without replacement**).

The program generates a list of items labeled as `"Item 1"`, `"Item 2"`, ..., up to `"Item n"`, and then computes the total number of ways to arrange **r** items out of these **n** items.

---

## Input Format

- The first input line contains a single integer **n** (the total number of items).
- The second input line contains a single integer **r** (the number of items to select).

---

## Output Format

The output is a single line that displays the total number of possible permutations in the format:

```
Total permutations (P(n,r)) without replacement: X
```
where `n` and `r` are the input values, and `X` is the computed total number of permutations.

---

## Code Constraints

- 0 ≤ r ≤ n ≤ 30
- Both **n** and **r** are integers.

---

## Sample Test Case

**Input 1:**
```
5
3
```
**Output 1:**
```
Total permutations (P(5,3)) without replacement: 60
```

```python
import itertools

n = int(input())
r = int(input())

total = len(list(itertools.permutations(range(n), r)))

print(f"Total permutations (P({n},{r})) without replacement: {total}")
```
# Program Description

This Python program reads two CSV files located in the script directory:

- **Population dataset**
- **Sample dataset**

Both files must contain a column named `Delivery_Time_Hours`.

The program calculates and displays summary statistics for the `Delivery_Time_Hours` column in both datasets, including:

- Mean
- Median
- Mode
- Variance
- Standard Deviation
- Skewness
- Kurtosis

---

## Sample Data

| Order_ID | Zone  | Delivery_Time_Hours |
|----------|-------|---------------------|
| 1        | East  | 7.648522592         |
| 2        | East  | 6.422021956         |
| 3        | East  | 6.575497156         |
| 4        | East  | 5.625315573         |
| 5        | South | 5.819815581         |
| 6        | East  | 5.829133715         |

---

## Input Format

- **Line 1:** The filename of the population dataset (including `.csv` extension), e.g., `population.csv`
- **Line 2:** The filename of the sample dataset (including `.csv` extension), e.g., `sample.csv`

---

## Output Format

- Display the heading **"Population Stats:"** followed by a dictionary of summary statistics for the population dataset.
- Display the heading **"Sample Stats:"** followed by a dictionary of summary statistics for the sample dataset.

---

## Code Constraints

- The input files must be CSV files and must contain the `Delivery_Time_Hours` column.
- Files must be located in the same directory as the Python script.
- The program uses `scipy.stats` functions to compute mode, skewness, and kurtosis.

---

## Sample Test Case

**Input 1:**
```
sample.csv
sample2.csv
```
**Output 1:**
```
Population Stats:
 {'Mean': 5.79, 'Median': 5.77, 'Mode': 1.98, 'Variance': 2.2, 'Std Dev': 1.48, 'Skewness': -0.175, 'Kurtosis': -0.058}
Sample Stats:
 {'Mean': 5.9, 'Median': 5.6, 'Mode': 1.07, 'Variance': 2.06, 'Std Dev': 1.44, 'Skewness': -0.331, 'Kurtosis': 1.439}
```

---

```python
import pandas as pd
import os
import sys
from scipy.stats import skew, kurtosis

file1 = input()
file2 = input()

df1 = pd.read_csv(os.path.join(sys.path[0], file1))
df2 = pd.read_csv(os.path.join(sys.path[0], file2))

def statCalc(df):
    data = df['Delivery_Time_Hours']

    mean = data.mean()
    median = data.median()
    mod = data.mode()
    var = data.var()
    std = data.std()
    ske = skew(data)
    kur = kurtosis(data)

    return {
        "Mean": round(mean, 2),
        "Median": round(median, 2),
        "Mode": round(mod[0], 2),
        "Variance": round(var, 2),
        "Std Dev": round(std, 2),
        "Skewness": round(ske, 3),
        "Kurtosis": round(kur, 3)
    }

if __name__ == "__main__":
    pop_data = statCalc(df1)
    print("Population Stats:")
    print("", pop_data)

    sam_data = statCalc(df2)
    print("Sample Stats:")
    print("", sam_data)
```
# Program Description

Create a program that performs data sampling and summary statistics on a dataset (CSV or Excel format) containing at least a column named `"Height_cm"`.

---

## Steps:

1. **Load a dataset file provided by the user** (`.csv` or `.xlsx` format).  
2. **Display the first 5 rows** of the loaded dataset for preview.  
3. **Apply Simple Random Sampling** to select a sample of 50 records, if enough data exists.  
4. **Compute and display summary statistics** (mean, std, min, max, median, mode, skewness, kurtosis) for:
    - The entire dataset (Population)
    - The random sample (Sample)

---

## CSV Format Example

| Gender | Height_cm | Weight_kg |
|--------|-----------|-----------|
| Male   |   152.5   |   58.2    |
| Female |   171.7   |   52.8    |
| Female |   149.7   |   64.8    |

---

## Input Format

- **Line 1:** Name of the file to load (e.g., `data.csv`)

---

## Output Format

- Confirmation that the file has been successfully loaded.
- Number of rows and columns in the dataset.
- Preview of the first 5 rows of the data.
- If enough rows exist:
    - A simple random sample of 50 students (first 5 rows shown).
    - Descriptive statistics for the `"Height_cm"` column of both:
      - The full dataset (Population)
      - The sample (Sample)

---

## Code Constraints

- The file must be in CSV format.
- Must contain a column named `"Height_cm"`.
- Sampling only proceeds if the dataset has at least 50 rows.
- The summary statistics include:
    - count, mean, std, min, 25%, 50%, 75%, max
    - median, mode, skewness, kurtosis

---

## Sample Test Cases

**Input 1:**
```
sample.csv
```

**Output 1:**
```
File loaded successfully: sample.csv
Data shape: (50, 3)
Preview of Loaded Data:
   Gender  Height_cm  Weight_kg
0    Male      152.5       58.2
1  Female      171.7       52.8
2  Female      149.7       64.8
3  Female      148.1       52.4
4    Male      177.2       74.6
Simple Random Sampling (50 students):
   Gender  Height_cm  Weight_kg
0    Male      169.6       64.6
1    Male      179.5       83.3
2  Female      158.6       51.9
3  Female      158.2       68.4
4  Female      157.4       47.5
Summary Statistics of the Population data
count     50.0
mean     163.9
std        8.6
min      148.1
25%      158.6
50%      162.7
75%      169.8
max      187.1
Name: Height_cm, dtype: float64
median: 162.7 mode: 163.1
skewness: 0.551 kurtosis: -0.029
Summary Statistics of the Sample data
count     50.0
mean     163.9
std        8.6
min      148.1
25%      158.6
50%      162.7
75%      169.8
max      187.1
Name: Height_cm, dtype: float64
median: 162.7 mode: 163.1
skewness: 0.551 kurtosis: -0.029
```

---

```python
import pandas as pd
import os
import sys
from scipy.stats import skew, kurtosis

file = input()
df = pd.read_csv(os.path.join(sys.path[0], file))

print(f"File loaded successfully: {file}")
print(f"Data shape: {df.shape}")
print("Preview of Loaded Data:")
print(df.head())


def simple():
    print("Simple Random Sampling (50 students):")
    simple = df.sample(n=50, random_state=42)
    print(simple.head().reset_index(drop=True))
    
    print("Summary Statistics of the Population data")
    heigh = df['Height_cm']
    print(round(heigh.describe(), 1))
    med = heigh.median()
    mod = heigh.mode()
    ske = skew(heigh)
    kurt = kurtosis(heigh)
    
    print(f"median: {med} mode: {mod[0]}")
    print(f"skewness: {round(ske, 3)} kurtosis: {round(kurt, 3)}")
    
    print("Summary Statistics of the Sample data")
    ran_heigh = simple['Height_cm']
    print(round(ran_heigh.describe(), 1))
    med = ran_heigh.median()
    mod = ran_heigh.mode()
    ske = skew(ran_heigh)
    kurt = kurtosis(ran_heigh)
    
    print(f"median: {med} mode: {mod[0]}")
    print(f"skewness: {round(ske, 3)} kurtosis: {round(kurt, 3)}")


if __name__ == "__main__":
    simple()
```

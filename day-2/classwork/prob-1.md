## Description

Create a Python program that loads a dataset from a CSV file located in the script directory. It then performs three different sampling techniques on the loaded data:

- **Simple Random Sampling:** Randomly selects a specified number of rows (default 50) from the dataset.
- **Stratified Sampling:** Splits the data into training and test sets while maintaining the distribution of the `Gender` column (if present).
- **Systematic Sampling:** Selects every nth row (default every 10th) from the dataset.

The program prints previews and results for each sampling method to the console.

---

### CSV Format Example

| Gender | Height_cm | Weight_kg |
|--------|-----------|-----------|
| Male   |   152.5   |   58.2    |
| Female |   171.7   |   52.8    |
| Female |   149.7   |   64.8    |

---

### Input Format

- **Line 1:** The filename of the dataset, including the extension, e.g., `sample.csv`.
- The file must be present in the same directory where the script is run.

---

### Output Format

- Display a message confirming the file is loaded along with the dataset shape.
- Display the first 5 rows of the loaded dataset.
- Display the heading **Simple Random Sampling (50 students):**
  - Display the first 5 rows of the simple random sample or a message if there are not enough rows.
- Display the heading **Stratified Sampling (by Gender):**
  - Display the first 5 rows of the stratified sample or a message if the 'Gender' column is missing.
- Display the heading **Systematic Sampling (every 10th student):**
  - Display the first 5 rows of the systematic sample or a message if the dataset is too small.

---

### Code Constraints

- The input file must be located in the same directory as the Python script.
- The input file must be a CSV (`.csv`) file.
- The dataset must have at least 50 rows for simple random sampling of size 50.
- The dataset must include a 'Gender' column for stratified sampling to work.
- The dataset must have enough rows for systematic sampling with a step size of 10.
- The program uses a fixed random seed (42) for reproducibility in sampling.

---

### Sample Test Cases

#### Input 1:

```
sample.csv
```

#### Output 1:

```
File loaded successfully: sample.csv
Data shape: (49, 3)
Preview of Loaded Data:
   Gender  Height_cm  Weight_kg
0    Male      152.5       58.2
1  Female      171.7       52.8
2  Female      149.7       64.8
3  Female      148.1       52.4
4    Male      177.2       74.6
Simple Random Sampling (50 students):
Not enough rows to sample 50 rows. Total rows: 49
Stratified Sampling (by Gender):
    Gender  Height_cm  Weight_kg
20  Female      159.1       65.4
18    Male      163.1       71.0
33  Female      159.9       58.9
1   Female      171.7       52.8
29    Male      163.2       76.1
Systematic Sampling (every 10th student):
    Gender  Height_cm  Weight_kg
0     Male      152.5       58.2
10    Male      175.3       63.0
20  Female      159.1       65.4
30  Female      158.6       51.9
40    Male      170.9       73.9
```

---

```python
import os
import sys
import pandas as pd
from sklearn.model_selection import train_test_split

file = input()
data = pd.read_csv(os.path.join(sys.path[0], file))

print("File loaded successfully:", file)
print("Data shape:", data.shape)
print("Preview of Loaded Data:")
print(data.head())

sample_size = 50

print("Simple Random Sampling (50 students):")
if sample_size > len(data):
    print(f"Not enough rows to sample {sample_size} rows. Total rows: {len(data)}")
else:
    sample = data.sample(n=sample_size, random_state=42)
    print(sample.head())

try:
    print("Stratified Sampling (by Gender):")
    stratify_by = "Gender"
    train, test = train_test_split(
        data,
        test_size=0.2,
        stratify=data[stratify_by],
        random_state=42
    )
    print(train.head())
except Exception as e:
    print("Error", e)

print("Systematic Sampling (every 10th student):")
sample = data.iloc[::10]
print(sample.head())
```

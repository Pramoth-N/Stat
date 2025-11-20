# Dataset Sampling Program

This Python program loads a dataset from a CSV or Excel file located in the script directory. It then performs three different sampling techniques on the loaded data:

- **Simple Random Sampling:** Randomly selects a specified number of rows (default 50) from the dataset.
- **Stratified Sampling:** Splits the data into groups based on the 'Zone' column and samples proportionally from each group.
- **Systematic Sampling:** Selects every nth row (default every 10th) from the dataset.

The program prints previews and results for each sampling method to the console.

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

- **Line 1:** The filename of the dataset, including the extension (e.g., `sample.csv`)

---

## Output Format

- Display a message confirming the file is loaded along with the dataset shape.
- Display the first 5 rows of the loaded dataset.
- Display heading: *Simple Random Sampling (50 deliveries)* and show the first 5 rows of the simple random sample, or a message if there are not enough rows.
- Display heading: *Stratified Sampling (by Zone)* and show the first 5 rows of the stratified sample, or a message if the 'Zone' column is missing.
- Display heading: *Systematic Sampling (every 10th order)* and show the first 5 rows of the systematic sample, or a message if the dataset is too small.

---

## Code Constraints

- The input file must be located in the same directory as the Python script.
- The input file must be either a CSV (.csv) or Excel (.xlsx) file.
- The dataset must have at least 50 rows for simple random sampling of size 50.
- The dataset must include a 'Zone' column for stratified sampling to work.
- The dataset must have enough rows for systematic sampling with a step size of 10.
- The program uses a fixed random seed (`42`) for reproducibility in sampling.

---

## Sample Test Case

**Input 1:**
```
sample.csv
```

**Output 1:**
```
Enter the dataset filename (with .csv or .xlsx extension): File loaded successfully: sample.csv
Data shape: (50, 3)

Preview of Loaded Data:
   Order_ID   Zone  Delivery_Time_Hours
0         1   East             7.648523
1         2   East             6.422022
2         3   East             6.575497
3         4   East             5.625316
4         5  South             5.819816

1.1: Simple Random Sample of 50 deliveries:
   Order_ID   Zone  Delivery_Time_Hours
0        14   West             3.340905
1        40   East             6.157802
2        31  South             5.716502
3        46   East             8.563945
4        18   West             6.642421

1.2: Stratified Sample by Zone (proportional to dataset):
   Order_ID  Zone  Delivery_Time_Hours
0         1  East             7.648523
1         2  East             6.422022
2        12  East             5.695918
3        45  East             5.576551
4        37  East             7.457254

1.3: Systematic Sample (every 10th order):
   Order_ID   Zone  Delivery_Time_Hours
0         1   East             7.648523
1        11   West             5.542345
2        21   West             3.272552
3        31  South             5.716502
4        41  South             5.810167
```

---

## Program Code

```python
import pandas as pd
import os
import sys

def load_dataset():
    file = input("Enter the dataset filename (with .csv or .xlsx extension): ")
    file_path = os.path.join(sys.path[0], file)
    if file.endswith('.csv'):
        df = pd.read_csv(file_path)
    elif file.endswith('.xlsx'):
        df = pd.read_excel(file_path)
    else:
        raise ValueError("Unsupported file extension. Please provide a .csv or .xlsx file.")
    return df, file

def simple_random_sample(df):
    print()
    if len(df) < 50:
        print("1.1: Simple Random Sample of 50 deliveries:")
        print("Not enough rows for simple random sampling (need at least 50 rows).")
    else:
        sample = df.sample(n=50, random_state=42)
        print("1.1: Simple Random Sample of 50 deliveries:")
        print(sample.head().reset_index(drop=True))

def stratified_sample(df):
    print()
    print("1.2: Stratified Sample by Zone (proportional to dataset):")
    if 'Zone' not in df.columns:
        print("Cannot perform stratified sampling. 'Zone' column missing.")
        return
    # Proportional stratified sampling (50 samples total if possible)
    total = 50
    zones = df['Zone'].value_counts(normalize=True)
    stratified = pd.DataFrame()
    for zone, prop in zones.items():
        n_zone = max(1, int(round(prop * total)))
        temp = df[df['Zone'] == zone].sample(n=min(n_zone, len(df[df['Zone'] == zone])), random_state=42)
        stratified = pd.concat([stratified, temp])
    stratified = stratified.sample(frac=1, random_state=42)  # Shuffle rows
    print(stratified.head().reset_index(drop=True))

def systematic_sample(df):
    print()
    print("1.3: Systematic Sample (every 10th order):")
    if len(df) < 10:
        print("Dataset too small for systematic sampling (need at least 10 rows).")
    else:
        systemat = df.iloc[::10]
        print(systemat.head().reset_index(drop=True))

if __name__ == "__main__":
    df, fname = load_dataset()
    print(f"File loaded successfully: {fname}")
    print(f"Data shape: {df.shape}\n")
    print("Preview of Loaded Data:")
    print(df.head())
    simple_random_sample(df)
    stratified_sample(df)
    systematic_sample(df)
```

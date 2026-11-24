# Experiment 3 : Retail Sales and Profit Analysis Using Pandas

## Aim
To create a sample retail dataset, identify and handle missing values (`NaN`/`None`) and duplicate records, and compute summary statistics using Pandas in Python.

## Algorithm

1. **Start** the program.
2. **Import Library**: Import the `pandas` library as `pd` for tabular data cleaning and analysis.
3. **Initialize Raw Retail Dataset**: Create a Python dictionary `data` containing retail records (`Order_ID`, `Product`, `Region`, `Sales`, `Discount`, `Profit`) with deliberate missing (`None`) entries and duplicate rows.
4. **Construct DataFrame & Inspect**:
   * Convert `data` into a Pandas DataFrame `df` using `pd.DataFrame(data)`.
   * Print the original dataset and its initial dimensions (`df.shape`).
5. **Detect Missing Values**:
   * Count missing entries per column using `df.isnull().sum()`.
6. **Impute Missing Values**:
   * Replace missing numerical values in `Sales`, `Discount`, and `Profit` with their respective column means using `.fillna(df[col].mean())`.
   * Replace missing categorical values in `Region` with the column mode (most frequent category) using `.fillna(df["Region"].mode()[0])`.
7. **Remove Duplicate Records**:
   * Drop exact duplicate rows from `df` using `df.drop_duplicates()`.
8. **Display Cleaned Dataset & Summary Statistics**:
   * Print the cleaned DataFrame, updated dimensions (`df.shape`), and descriptive statistical metrics (`df.describe()`).
9. **Stop** the program.

## Functions and Methods Used

| Category | Function / Method | Purpose / Description |
| :--- | :--- | :--- |
| **Data Creation & Inspection** | `pd.DataFrame()` | Converts a Python dictionary into a labeled 2D tabular DataFrame |
| | `df.shape` | Returns the `(rows, columns)` dimensions before and after cleaning |
| | `df.isnull().sum()` | Counts the number of missing (`NaN`/`None`) values in each column |
| **Missing Value Imputation** | `df[col].fillna()` | Replaces missing values with a specified replacement value |
| | `df[col].mean()` | Calculates the arithmetic mean for numerical column imputation |
| | `df[col].mode()[0]` | Retrieves the most frequent category for categorical column imputation |
| **Deduplication & Summary** | `df.drop_duplicates()` | Identifies and removes duplicate rows from the DataFrame |
| | `df.describe()` | Generates count, mean, standard deviation, min, quartiles, and max for numerical features |

## Program


# Cleaning and Preparing Retail Data using Pandas

import pandas as pd

# Step 1: Create a sample retail dataset
data = {
    "Order_ID": ["O001", "O002", "O003", "O004",
                 "O005", "O006", "O007", "O001"],

  "Product": ["Laptop", "Phone", "Tablet", "Laptop",
                "Phone", "Tablet", "Laptop", "Laptop"],

  "Region": ["North", "South", None, "West",
               "South", "East", "North", "North"],

  "Sales": [50000, 30000, 25000, None,
              35000, 20000, 50000, 50000],

  "Discount": [5000, 3000, None, 4000,
               3500, 2000, 5000, 5000],

  "Profit": [8000, 5000, 4000, 6000,
               None, 3000, 8000, 8000]
}

# Step 2: Convert dictionary into DataFrame
df = pd.DataFrame(data)

print("Original Retail Dataset:")
print(df)

print("\nOriginal Dataset Shape:", df.shape)

# Step 3: Check for missing values
print("\nMissing Values Before Cleaning:")
print(df.isnull().sum())

# Step 4: Fill missing numerical values with column mean
numeric_columns = ["Sales", "Discount", "Profit"]

for col in numeric_columns:
    df[col] = df[col].fillna(df[col].mean())

# Step 5: Fill missing Region with mode
df["Region"] = df["Region"].fillna(df["Region"].mode()[0])

print("\nDataset After Filling Missing Values:")
print(df)

# Step 6: Remove duplicate records
print("\nDuplicate Records Before Removal:",
      df.duplicated().sum())  

df_clean = df.drop_duplicates()  

# Step 7: Display cleaned dataset
print("\nCleaned Retail Dataset:")  
print(df_clean)  

print("\nShape After Cleaning:", df_clean.shape)  

# Step 8: Display summary statistics
print("\nSummary Statistics:")  
print(df_clean.describe())  

# Step 9: Check missing values after cleaning
print("\nMissing Values After Cleaning:")  
print(df_clean.isnull().sum())  

print("\nDuplicate Records After Cleaning:",
      df_clean.duplicated().sum()) 




## Output


Original Retail Dataset Shape: (8, 6)

Missing Values Before Cleaning:

Order_ID    0
Product     0
Region      1
Sales       1
Discount    1
Profit      1

Duplicate Records Before Removal: 1

Shape After Cleaning: (7, 6)

Missing Values After Cleaning:

Order_ID    0
Product     0
Region      0
Sales       0
Discount    0
Profit      0

Duplicate Records After Cleaning: 0 

Summary Statistics:

Sales      Discount    Profit  
count           7.00        7.00        7.00  
mean        35306.12       3775.51     5714.29  
std         11575.38       1072.56     1889.82  
min         20000.00       2000.00     3000.00  
max         50000.00       5000.00     8000.00  


## Result
The program successfully creates a retail dataset, identifies missing entries and duplicate rows, imputes missing values using mean and mode strategies, removes duplicates, and outputs a clean dataset ready for downstream analysis.


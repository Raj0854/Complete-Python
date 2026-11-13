
# Day 49 – Advanced Pandas: Data Cleaning, GroupBy, Merge, Join & Aggregation

## 1. Introduction

In Day 48, we learned Pandas fundamentals:

- Series and DataFrames
- Creating DataFrames
- Reading and writing CSV files
- Selecting rows and columns
- Filtering records
- Sorting and basic statistics

In real-world Data Science, datasets are rarely perfect.

They may contain:

- Missing values
- Duplicate records
- Incorrect data types
- Inconsistent text
- Invalid values
- Unnecessary columns
- Multiple related datasets

Data cleaning is the process of identifying and correcting these problems before analysis.

Today, we will learn how to clean and combine datasets using Pandas.

---

## 2. Creating a Sample Dataset

We will use this dataset throughout the lesson.

```python
import pandas as pd
import numpy as np

data = {
    "Name": [
        "Raj", "Aman", "Priya", "Neha",
        "Rohan", "Simran", "Raj"
    ],

    "Department": [
        "IT", "HR", "Finance", "IT",
        "Sales", "HR", "IT"
    ],

    "Age": [
        24, 26, 25, np.nan,
        27, 23, 24
    ],

    "Salary": [
        35000, 30000, 40000, 32000,
        np.nan, 28000, 35000
    ],

    "City": [
        "Mumbai", "Pune", "Delhi", "Mumbai",
        "Nashik", "Pune", "Mumbai"
    ]
}

df = pd.DataFrame(data)

print(df)
```

Expected output:

```text
     Name Department   Age   Salary     City
0     Raj         IT  24.0  35000.0   Mumbai
1    Aman         HR  26.0  30000.0     Pune
2   Priya    Finance  25.0  40000.0    Delhi
3    Neha         IT   NaN  32000.0   Mumbai
4   Rohan      Sales  27.0      NaN   Nashik
5  Simran         HR  23.0  28000.0     Pune
6     Raj         IT  24.0  35000.0   Mumbai
```

Notice that:

- Age is missing for Neha.
- Salary is missing for Rohan.
- Raj appears twice.

These are common data quality problems.

---

## 3. Detecting Missing Values

Missing values represent information that is unavailable or not recorded.

Pandas commonly represents missing numerical values using `NaN`.

### 3.1 isnull()

Checks whether values are missing.

```python
print(df.isnull())
```

Returns a DataFrame containing `True` for missing values and `False` otherwise.

### 3.2 isna()

`isna()` is an alias of `isnull()`.

```python
print(df.isna())
```

### 3.3 notnull()

Checks whether values are available.

```python
print(df.notnull())
```

### 3.4 Counting missing values

```python
print(df.isnull().sum())
```

Expected output:

```text
Name           0
Department     0
Age            1
Salary         1
City           0
dtype: int64
```

### 3.5 Total missing values

```python
print(df.isnull().sum().sum())
```

Expected output:

```text
2
```

### 3.6 Missing-value percentage

```python
missing_percentage = (
    df.isnull().mean() * 100
)

print(missing_percentage)
```

This calculates the percentage of missing values in each column.

---

## 4. Handling Missing Values

There are multiple ways to handle missing data.

The correct method depends on the dataset and the meaning of the missing values.

### 4.1 dropna()

Removes rows containing missing values.

```python
cleaned_df = df.dropna()

print(cleaned_df)
```

By default, any row containing at least one missing value is removed.

Important:

`dropna()` returns a new DataFrame by default. It does not modify the original DataFrame.

### 4.2 Removing rows with all values missing

```python
cleaned_df = df.dropna(how="all")
```

Only rows where every value is missing are removed.

### 4.3 Removing columns with missing values

```python
cleaned_df = df.dropna(axis=1)

print(cleaned_df)
```

Here:

- `axis=0` removes rows.
- `axis=1` removes columns.

### 4.4 fillna()

Replaces missing values.

```python
filled_df = df.fillna(0)

print(filled_df)
```

This replaces every missing value with zero.

However, zero is not always a meaningful replacement.

### 4.5 Filling with mean

Mean is often used for numerical columns when appropriate.

```python
df["Age"] = df["Age"].fillna(
    df["Age"].mean()
)

print(df["Age"])
```

### 4.6 Filling with median

Median is useful when data contains extreme values or is skewed.

```python
df["Salary"] = df["Salary"].fillna(
    df["Salary"].median()
)

print(df["Salary"])
```

### 4.7 Filling categorical values with mode

Mode is the most frequently occurring value.

```python
df["Department"] = df["Department"].fillna(
    df["Department"].mode()[0]
)
```

### 4.8 Forward fill

Uses the previous available value.

```python
data = pd.Series([10, np.nan, np.nan, 40, 50])

result = data.ffill()

print(result)
```

Expected output:

```text
0    10.0
1    10.0
2    10.0
3    40.0
4    50.0
dtype: float64
```

### 4.9 Backward fill

Uses the next available value.

```python
result = data.bfill()

print(result)
```

Expected output:

```text
0    10.0
1    40.0
2    40.0
3    40.0
4    50.0
dtype: float64
```

Important:

Forward fill and backward fill are particularly useful for ordered data such as time-series observations.

Do not use them blindly on unrelated records.

---

## 5. Removing Duplicate Records

Duplicate records contain repeated information.

Pandas provides `duplicated()` and `drop_duplicates()`.

### 5.1 duplicated()

Identifies duplicate rows.

```python
print(df.duplicated())
```

Returns `True` for duplicate rows.

### 5.2 Count duplicates

```python
print(df.duplicated().sum())
```

### 5.3 drop_duplicates()

Removes duplicate rows.

```python
cleaned_df = df.drop_duplicates()

print(cleaned_df)
```

By default, the first occurrence is retained.

### 5.4 Keep the last occurrence

```python
cleaned_df = df.drop_duplicates(
    keep="last"
)
```

### 5.5 Remove duplicates based on selected columns

```python
cleaned_df = df.drop_duplicates(
    subset=["Name", "Department"]
)

print(cleaned_df)
```

This checks duplicates using only the selected columns.

### 5.6 Removing duplicates from the original DataFrame

```python
df.drop_duplicates(inplace=True)
```

---

## 6. Replacing Incorrect Values

Real datasets may contain inconsistent or incorrect values.

Example:

```python
data = {
    "Name": ["Raj", "Aman", "Priya", "Neha"],
    "City": [
        "Mumbai",
        "mumbai",
        "MUMBAI",
        "Pune"
    ]
}

df = pd.DataFrame(data)

print(df)
```

The same city is represented in three different formats.

### 6.1 replace()

```python
df["City"] = df["City"].replace({
    "mumbai": "Mumbai",
    "MUMBAI": "Mumbai"
})

print(df)
```

### 6.2 Standardizing text with str.title()

```python
df["City"] = df["City"].str.title()

print(df)
```

### 6.3 Removing extra spaces

```python
df["City"] = df["City"].str.strip()
```

### 6.4 Converting text to lowercase

```python
df["City"] = df["City"].str.lower()
```

### 6.5 Converting text to uppercase

```python
df["City"] = df["City"].str.upper()
```

### 6.6 Replacing part of a string

```python
df["City"] = df["City"].str.replace(
    "mumbai",
    "Mumbai",
    regex=False
)
```

Text cleaning is important when values come from different sources.

---

## 7. Handling Incorrect Data Types

Sometimes numerical values are stored as strings.

Example:

```python
df = pd.DataFrame({
    "Name": ["Raj", "Aman", "Priya"],
    "Salary": ["35000", "30000", "40000"]
})

print(df.dtypes)
```

Salary may have the `object` data type.

### 7.1 Converting using astype()

```python
df["Salary"] = df["Salary"].astype(int)

print(df.dtypes)
```

### 7.2 Using to_numeric()

```python
df = pd.DataFrame({
    "Salary": ["35000", "30000", "unknown", "40000"]
})

df["Salary"] = pd.to_numeric(
    df["Salary"],
    errors="coerce"
)

print(df)
```

Expected output:

```text
    Salary
0  35000.0
1  30000.0
2      NaN
3  40000.0
```

`errors="coerce"` converts invalid numerical values into `NaN`.

### 7.3 Checking data types

```python
print(df.dtypes)
```

Always inspect data types before performing calculations.

---

## 8. String Operations in Pandas

Pandas provides the `.str` accessor for performing string operations on entire columns.

Example:

```python
df = pd.DataFrame({
    "Name": [" raj ", "AMAN", "Priya ", " neha"]
})
```

### Common string operations

```python
df["Name"] = df["Name"].str.strip()

df["Name"] = df["Name"].str.title()

print(df)
```

Other useful operations:

| Operation | Purpose |
|---|---|
| `.str.lower()` | Converts text to lowercase |
| `.str.upper()` | Converts text to uppercase |
| `.str.title()` | Converts text to title case |
| `.str.strip()` | Removes surrounding spaces |
| `.str.len()` | Returns string length |
| `.str.contains()` | Checks whether text contains a pattern |
| `.str.startswith()` | Checks the beginning of a string |
| `.str.endswith()` | Checks the end of a string |
| `.str.replace()` | Replaces matching text |
| `.str.split()` | Splits strings |

### Example: Searching text

```python
df = pd.DataFrame({
    "Name": ["Raj Gupta", "Aman Sharma", "Priya Patel"]
})

result = df[
    df["Name"].str.contains(
        "Raj",
        case=False,
        na=False
    )
]

print(result)
```

`na=False` treats missing values as non-matches.

---

## 9. GroupBy Operations

`groupby()` is one of the most important Pandas features.

It divides data into groups based on one or more columns.

We can then calculate statistics for each group.

Example:

```python
data = {
    "Name": [
        "Raj", "Aman", "Priya",
        "Neha", "Rohan", "Simran"
    ],

    "Department": [
        "IT", "HR", "IT",
        "Finance", "HR", "Finance"
    ],

    "Salary": [
        35000, 30000, 40000,
        45000, 32000, 42000
    ]
}

df = pd.DataFrame(data)

print(df)
```

### 9.1 Grouping by department

```python
result = df.groupby("Department")

print(result.groups)
```

This shows which records belong to each department.

### 9.2 Average salary by department

```python
result = df.groupby("Department")["Salary"].mean()

print(result)
```

Expected output:

```text
Department
Finance    43500.0
HR         31000.0
IT         37500.0
Name: Salary, dtype: float64
```

### 9.3 Total salary by department

```python
result = df.groupby("Department")["Salary"].sum()

print(result)
```

### 9.4 Count employees by department

```python
result = df.groupby("Department")["Name"].count()

print(result)
```

### 9.5 Multiple grouping columns

We can group data using more than one column.

```python
data = {
    "Department": ["IT", "IT", "HR", "HR", "IT"],
    "City": ["Mumbai", "Pune", "Mumbai", "Pune", "Mumbai"],
    "Salary": [35000, 40000, 30000, 32000, 45000]
}

df = pd.DataFrame(data)

result = df.groupby(
    ["Department", "City"]
)["Salary"].mean()

print(result)
```

This calculates average salary for each department and city combination.

---

## 10. Aggregation with agg()

Aggregation means calculating one or more summary values from a group of records.

Pandas provides `agg()` to apply multiple aggregation functions.

### 10.1 Multiple aggregations

```python
result = df.groupby("Department")["Salary"].agg(
    ["mean", "sum", "min", "max", "count"]
)

print(result)
```

### 10.2 Aggregating different columns

```python
data = {
    "Department": ["IT", "IT", "HR", "HR"],
    "Salary": [35000, 40000, 30000, 32000],
    "Age": [24, 26, 23, 25]
}

df = pd.DataFrame(data)

result = df.groupby("Department").agg({
    "Salary": ["mean", "max"],
    "Age": ["mean", "min"]
})

print(result)
```

### 10.3 Named aggregation

Named aggregation creates clearer output column names.

```python
result = df.groupby("Department").agg(
    average_salary=("Salary", "mean"),
    maximum_salary=("Salary", "max"),
    average_age=("Age", "mean")
)

print(result)
```

This is useful when preparing reports.

---

## 11. Understanding transform()

`transform()` performs group-based calculations and returns a result aligned with the original rows.

Example:

```python
data = {
    "Name": ["Raj", "Aman", "Priya", "Neha"],
    "Department": ["IT", "HR", "IT", "HR"],
    "Salary": [35000, 30000, 45000, 40000]
}

df = pd.DataFrame(data)

df["Department_Average"] = (
    df.groupby("Department")["Salary"]
      .transform("mean")
)

print(df)
```

Expected output:

```text
    Name Department  Salary  Department_Average
0    Raj         IT   35000             40000.0
1   Aman         HR   30000             35000.0
2  Priya         IT   45000             40000.0
3   Neha         HR   40000             35000.0
```

Difference:

- `agg()` generally reduces each group to summary values.
- `transform()` returns values aligned with the original rows.

---

## 12. Combining DataFrames

In real-world projects, data is often stored in separate files or tables.

For example:

- Employee information in one dataset.
- Department information in another dataset.
- Salary information in another dataset.

Pandas provides `concat()`, `merge()` and `join()`.

### 12.1 concat()

Combines DataFrames along rows or columns.

#### Vertical concatenation

```python
df1 = pd.DataFrame({
    "Name": ["Raj", "Aman"],
    "Marks": [85, 90]
})

df2 = pd.DataFrame({
    "Name": ["Priya", "Neha"],
    "Marks": [95, 88]
})

result = pd.concat(
    [df1, df2],
    ignore_index=True
)

print(result)
```

Expected output:

```text
    Name  Marks
0    Raj     85
1   Aman     90
2  Priya     95
3   Neha     88
```

`ignore_index=True` creates a new continuous index.

#### Horizontal concatenation

```python
df1 = pd.DataFrame({
    "Name": ["Raj", "Aman"]
})

df2 = pd.DataFrame({
    "Marks": [85, 90]
})

result = pd.concat(
    [df1, df2],
    axis=1
)

print(result)
```

---

## 13. Merge DataFrames

`merge()` combines DataFrames using common columns or keys.

It is similar to SQL JOIN operations.

Consider two datasets.

### Employee DataFrame

```python
employees = pd.DataFrame({
    "Employee_ID": [101, 102, 103, 104],
    "Name": ["Raj", "Aman", "Priya", "Neha"],
    "Department_ID": [1, 2, 1, 3]
})
```

### Department DataFrame

```python
departments = pd.DataFrame({
    "Department_ID": [1, 2, 3],
    "Department_Name": ["IT", "HR", "Finance"]
})
```

### 13.1 Inner merge

Returns only matching records from both DataFrames.

```python
result = pd.merge(
    employees,
    departments,
    on="Department_ID",
    how="inner"
)

print(result)
```

### 13.2 Left merge

Keeps all records from the left DataFrame and adds matching values from the right DataFrame.

```python
result = pd.merge(
    employees,
    departments,
    on="Department_ID",
    how="left"
)

print(result)
```

### 13.3 Right merge

Keeps all records from the right DataFrame.

```python
result = pd.merge(
    employees,
    departments,
    on="Department_ID",
    how="right"
)

print(result)
```

### 13.4 Outer merge

Keeps all records from both DataFrames.

```python
result = pd.merge(
    employees,
    departments,
    on="Department_ID",
    how="outer"
)

print(result)
```

### Merge types

| Merge Type | Meaning |
|---|---|
| inner | Only matching records |
| left | All left records and matching right records |
| right | All right records and matching left records |
| outer | All records from both sides |

---

## 14. Merge Using Different Column Names

Sometimes the key columns have different names.

Example:

```python
employees = pd.DataFrame({
    "Employee_ID": [101, 102, 103],
    "Name": ["Raj", "Aman", "Priya"]
})

salaries = pd.DataFrame({
    "ID": [101, 102, 103],
    "Salary": [35000, 30000, 40000]
})
```

Use `left_on` and `right_on`:

```python
result = pd.merge(
    employees,
    salaries,
    left_on="Employee_ID",
    right_on="ID",
    how="inner"
)

print(result)
```

This matches `Employee_ID` from the first DataFrame with `ID` from the second.

---

## 15. Joining DataFrames

`join()` is primarily used to combine DataFrames using their indexes.

Example:

```python
employees = pd.DataFrame({
    "Name": ["Raj", "Aman", "Priya"]
}, index=[101, 102, 103])

salaries = pd.DataFrame({
    "Salary": [35000, 30000, 40000]
}, index=[101, 102, 103])

result = employees.join(salaries)

print(result)
```

Expected output:

```text
      Name  Salary
101    Raj   35000
102   Aman   30000
103  Priya   40000
```

### Join types

```python
employees.join(
    salaries,
    how="inner"
)
```

Available types:

- `left`
- `right`
- `inner`
- `outer`

Remember:

- `merge()` is commonly used with columns.
- `join()` is commonly used with indexes.

---

## 16. Applying Custom Functions

Pandas allows us to apply custom Python functions to data.

### 16.1 apply() on a column

```python
df = pd.DataFrame({
    "Name": ["Raj", "Aman", "Priya"],
    "Marks": [85, 90, 95]
})

def calculate_grade(marks):
    if marks >= 90:
        return "A"
    elif marks >= 80:
        return "B"
    elif marks >= 40:
        return "C"
    else:
        return "Fail"

df["Grade"] = df["Marks"].apply(calculate_grade)

print(df)
```

### 16.2 apply() on rows

```python
df = pd.DataFrame({
    "Maths": [80, 90, 70],
    "Science": [85, 95, 75]
})

df["Total"] = df.apply(
    lambda row: row["Maths"] + row["Science"],
    axis=1
)

print(df)
```

Here:

- `axis=0` applies a function column-wise.
- `axis=1` applies a function row-wise.

For simple calculations, vectorized Pandas operations are usually preferable to row-wise `apply()` because they are often faster.

---

## 17. Working with Dates and Time

Date and time operations are common in business analytics.

### 17.1 Creating date data

```python
df = pd.DataFrame({
    "Date": [
        "2026-01-10",
        "2026-02-15",
        "2026-03-20"
    ],
    "Sales": [10000, 15000, 20000]
})
```

Initially, Date may be stored as text.

### 17.2 to_datetime()

Converts values into Pandas datetime format.

```python
df["Date"] = pd.to_datetime(df["Date"])

print(df.dtypes)
```

### 17.3 Extracting date components

```python
df["Year"] = df["Date"].dt.year

df["Month"] = df["Date"].dt.month

df["Day"] = df["Date"].dt.day

df["Month_Name"] = df["Date"].dt.month_name()

print(df)
```

### 17.4 Filtering dates

```python
result = df[
    df["Date"] >= "2026-02-01"
]

print(result)
```

### 17.5 Date differences

```python
start_date = pd.Timestamp("2026-01-01")
end_date = pd.Timestamp("2026-01-15")

difference = end_date - start_date

print(difference.days)
```

Expected output:

```text
14
```

---

## 18. Reshaping DataFrames with pivot()

`pivot()` converts unique values from one column into separate columns.

Example:

```python
data = {
    "Name": ["Raj", "Raj", "Aman", "Aman"],
    "Subject": ["Maths", "Science", "Maths", "Science"],
    "Marks": [85, 90, 80, 88]
}

df = pd.DataFrame(data)

result = df.pivot(
    index="Name",
    columns="Subject",
    values="Marks"
)

print(result)
```

Expected output:

```text
Subject  Maths  Science
Name
Aman      80       88
Raj       85       90
```

Important:

`pivot()` requires each index-column combination to identify a single value. If duplicates exist, use `pivot_table()`.

### 18.1 pivot_table()

Allows aggregation when multiple values exist for the same combination.

```python
data = {
    "Name": ["Raj", "Raj", "Aman", "Aman"],
    "Subject": ["Maths", "Maths", "Maths", "Maths"],
    "Marks": [80, 90, 70, 85]
}

df = pd.DataFrame(data)

result = pd.pivot_table(
    df,
    index="Name",
    columns="Subject",
    values="Marks",
    aggfunc="mean"
)

print(result)
```

Expected output:

```text
Subject  Maths
Name
Aman      77.5
Raj       85.0
```

---

## 19. Exporting Cleaned Data

After cleaning and analysis, we often save the final dataset.

### Export to CSV

```python
df.to_csv(
    "cleaned_data.csv",
    index=False
)
```

### Export to Excel

```python
df.to_excel(
    "cleaned_data.xlsx",
    index=False
)
```

### Export selected columns

```python
df[["Name", "Marks"]].to_csv(
    "student_marks.csv",
    index=False
)
```

Always verify that the exported file contains the expected rows and columns.

---

## 20. Mini-Project: Employee Data Cleaning and Analysis System

### Project Description

Build an Employee Data Analysis System using Pandas.

The system should:

1. Create employee and department datasets.
2. Detect missing values.
3. Fill missing numerical values.
4. Remove duplicate employees.
5. Standardize department names.
6. Merge employee and department datasets.
7. Calculate average salary by department.
8. Calculate employee count by department.
9. Find the highest-paid employee.
10. Export the cleaned report.

### Complete Program

```python
import pandas as pd
import numpy as np

# ---------------------------------
# 1. Employee Dataset
# ---------------------------------

employees = pd.DataFrame({
    "Employee_ID": [101, 102, 103, 104, 105, 101],

    "Name": [
        "Raj",
        "Aman",
        "Priya",
        "Neha",
        "Rohan",
        "Raj"
    ],

    "Department_ID": [1, 2, 1, 3, 2, 1],

    "Age": [24, 26, 25, np.nan, 27, 24],

    "Salary": [
        35000,
        30000,
        40000,
        32000,
        np.nan,
        35000
    ]
})

print("========== ORIGINAL EMPLOYEE DATA ==========")

print(employees)

# ---------------------------------
# 2. Department Dataset
# ---------------------------------

departments = pd.DataFrame({
    "Department_ID": [1, 2, 3],

    "Department": [
        "IT",
        "HR",
        "Finance"
    ]
})

# ---------------------------------
# 3. Detect Missing Values
# ---------------------------------

print("\n========== MISSING VALUES ==========")

print(employees.isnull().sum())

# ---------------------------------
# 4. Fill Missing Values
# ---------------------------------

employees["Age"] = employees["Age"].fillna(
    employees["Age"].median()
)

employees["Salary"] = employees["Salary"].fillna(
    employees["Salary"].median()
)

# ---------------------------------
# 5. Remove Duplicate Employees
# ---------------------------------

employees = employees.drop_duplicates(
    subset=["Employee_ID"]
)

# ---------------------------------
# 6. Merge Employee and Department Data
# ---------------------------------

final_df = pd.merge(
    employees,
    departments,
    on="Department_ID",
    how="left"
)

print("\n========== CLEANED EMPLOYEE DATA ==========")

print(final_df)

# ---------------------------------
# 7. Average Salary by Department
# ---------------------------------

average_salary = final_df.groupby(
    "Department"
)["Salary"].mean()

print("\n========== AVERAGE SALARY ==========")

print(average_salary)

# ---------------------------------
# 8. Employee Count by Department
# ---------------------------------

employee_count = final_df.groupby(
    "Department"
)["Employee_ID"].count()

print("\n========== EMPLOYEE COUNT ==========")

print(employee_count)

# ---------------------------------
# 9. Department Salary Statistics
# ---------------------------------

salary_report = final_df.groupby(
    "Department"
).agg(
    average_salary=("Salary", "mean"),
    maximum_salary=("Salary", "max"),
    minimum_salary=("Salary", "min"),
    employee_count=("Employee_ID", "count")
)

print("\n========== DEPARTMENT REPORT ==========")

print(salary_report)

# ---------------------------------
# 10. Highest Paid Employee
# ---------------------------------

top_index = final_df["Salary"].idxmax()

print("\n========== HIGHEST PAID EMPLOYEE ==========")

print(final_df.loc[top_index])

# ---------------------------------
# 11. Add Bonus Column
# ---------------------------------

final_df["Bonus"] = final_df["Salary"] * 0.10

# ---------------------------------
# 12. Sort Employees by Salary
# ---------------------------------

final_df = final_df.sort_values(
    by="Salary",
    ascending=False
)

print("\n========== FINAL EMPLOYEE REPORT ==========")

print(final_df)

# ---------------------------------
# 13. Export Reports
# ---------------------------------

final_df.to_csv(
    "cleaned_employee_report.csv",
    index=False
)

salary_report.to_csv(
    "department_salary_report.csv"
)

print("\nReports exported successfully.")
```

### Project Concepts Used

| Concept | Purpose |
|---|---|
| `isnull()` | Detect missing values |
| `fillna()` | Replace missing values |
| `drop_duplicates()` | Remove duplicate records |
| `merge()` | Combine related datasets |
| `groupby()` | Group employees by department |
| `agg()` | Calculate multiple statistics |
| `idxmax()` | Find the index of the highest value |
| `sort_values()` | Sort employee records |
| `to_csv()` | Export reports |

### Project Discussion

Ask the student:

1. Why did we remove duplicate employee IDs?
2. Why did we use median to fill missing salaries?
3. Why did we use `merge()`?
4. What is the difference between `groupby()` and `agg()`?
5. Why do we export separate employee and department reports?

The student should understand that data cleaning decisions must be based on the meaning of the data, not just on which function is easiest to use.

---

## 21. Student Practice Exercises

### Exercise 1: Missing Value Handling

Create a DataFrame with missing values in Age, Salary and City.

Tasks:

1. Detect missing values.
2. Count missing values in each column.
3. Calculate missing-value percentages.
4. Fill Age with its median.
5. Fill Salary with its mean.
6. Fill City with its mode.
7. Verify that missing values have been handled.

### Exercise 2: Duplicate Removal

Create an employee DataFrame containing duplicate employee IDs.

Tasks:

1. Find duplicate rows.
2. Count duplicate records.
3. Remove duplicates.
4. Keep the last occurrence for one experiment.
5. Remove duplicates based only on Employee_ID.

### Exercise 3: GroupBy Analysis

Create a sales dataset containing:

- Employee
- Department
- Product
- Sales

Tasks:

1. Calculate total sales by department.
2. Calculate average sales by department.
3. Find the maximum sale in each department.
4. Count sales records by department.
5. Group by department and product.

### Exercise 4: Merge DataFrames

Create two DataFrames:

Employee DataFrame:
- Employee_ID
- Name
- Department_ID

Department DataFrame:
- Department_ID
- Department_Name

Tasks:

1. Perform an inner merge.
2. Perform a left merge.
3. Perform a right merge.
4. Perform an outer merge.
5. Explain the difference between the four results.

### Exercise 5: Date Analysis

Create a sales DataFrame with date and revenue columns.

Tasks:

1. Convert dates using `to_datetime()`.
2. Extract year.
3. Extract month.
4. Extract day.
5. Filter records for a selected month.
6. Calculate monthly revenue.

### Exercise 6: Pivot Table

Create a DataFrame containing student names, subjects and marks.

Tasks:

1. Convert subjects into columns using `pivot()`.
2. Create a pivot table using `pivot_table()`.
3. Calculate average marks by student.
4. Compare the two outputs.

---

## 22. Trainer Assessment

Ask the student:

1. What is data cleaning?
2. Why do datasets contain missing values?
3. What is the difference between `isnull()` and `notnull()`?
4. What is the difference between `dropna()` and `fillna()`?
5. What is the difference between mean and median imputation?
6. What does `duplicated()` return?
7. How does `drop_duplicates()` work?
8. What is the purpose of `groupby()`?
9. What is aggregation?
10. What is the difference between `agg()` and `transform()`?
11. What is the difference between `concat()` and `merge()`?
12. What is the difference between `merge()` and `join()`?
13. What is the difference between inner and outer merge?
14. What does `apply()` do?
15. What is the purpose of `pivot()` and `pivot_table()`?
16. Why do we use `to_datetime()`?

### Practical Assessment

Ask the student to build a complete Sales Data Cleaning and Analysis System.

The program must:

- Load sales data from CSV.
- Detect missing values.
- Remove duplicate transactions.
- Standardize product and city names.
- Convert sales and quantity columns into numerical types.
- Calculate total revenue by product.
- Calculate monthly sales.
- Find the highest-selling product.
- Merge product details with sales data.
- Export a cleaned dataset and summary report.

The student should complete the system independently.

---

## 23. Completion Criteria

The student should be able to:

- Detect and handle missing values.
- Remove duplicate records.
- Standardize text data.
- Correct data types.
- Perform string operations.
- Group data using `groupby()`.
- Calculate multiple aggregations.
- Understand `transform()`.
- Combine datasets using `concat()`, `merge()` and `join()`.
- Apply custom functions.
- Work with date and time columns.
- Reshape datasets using `pivot()` and `pivot_table()`.
- Export cleaned datasets.
- Complete the Employee Data Analysis project independently.

---

## 24. Next Day Preview

**Day 50 – Data Visualization with Matplotlib and Seaborn**

Topics:

- Introduction to Data Visualization
- Matplotlib fundamentals
- Figure and Axes
- Line charts
- Bar charts
- Histograms
- Scatter plots
- Pie charts
- Customizing charts
- Seaborn fundamentals
- Statistical visualizations
- Correlation heatmaps
- Complete Data Visualization mini-project

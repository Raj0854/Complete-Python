
# Day 48 – Pandas Fundamentals: Series, DataFrames, Data Loading & Data Selection

## 1. Introduction to Pandas

Pandas is a Python library used for working with structured data.

It helps us:
- Read data from CSV and Excel files.
- Organize data into rows and columns.
- Select specific data.
- Filter records based on conditions.
- Handle missing values.
- Calculate statistics.
- Clean and analyze datasets.

### Real-world example

Imagine a company has a dataset containing employee information:

| Name | Age | Department | Salary |
|---|---:|---|---:|
| Raj | 24 | IT | 35000 |
| Aman | 26 | HR | 30000 |
| Priya | 25 | Finance | 40000 |

Pandas allows us to load this information and analyze it using Python.

### NumPy vs Pandas

| NumPy | Pandas |
|---|---|
| Works mainly with arrays | Works with labeled tabular data |
| Supports numerical operations | Supports data cleaning and analysis |
| Uses `ndarray` | Uses Series and DataFrame |
| Common in numerical computing | Common in data analysis |

---

## 2. Installing Pandas

Install Pandas using pip:

```bash
pip install pandas
```

For CSV and Excel work, we may also need:

```bash
pip install openpyxl
```

Import Pandas:

```python
import pandas as pd

print(pd.__version__)
```

Expected output:

```text
2.x.x
```

The exact version may differ.

Convention:

We generally use `pd` as the alias for Pandas.

---

## 3. Understanding Pandas Data Structures

Pandas mainly provides two data structures:

1. Series
2. DataFrame

### 3.1 Series

A Series is a one-dimensional labeled data structure.

It contains:
- Values
- Index labels

Example:

```python
import pandas as pd

marks = pd.Series([85, 90, 78, 92, 88])

print(marks)
```

Expected output:

```text
0    85
1    90
2    78
3    92
4    88
dtype: int64
```

Explanation:

- Left side represents the index.
- Right side represents the values.
- `dtype` represents the data type.

### 3.2 Custom Index in Series

We can define our own index labels.

```python
marks = pd.Series(
    [85, 90, 78],
    index=["Raj", "Aman", "Priya"]
)

print(marks)
```

Expected output:

```text
Raj      85
Aman     90
Priya    78
dtype: int64
```

Access a value using its label:

```python
print(marks["Raj"])
```

Output:

```text
85
```

Access using position:

```python
print(marks.iloc[1])
```

Output:

```text
90
```

### 3.3 Series Properties

```python
marks = pd.Series([85, 90, 78, 92])

print("Values:", marks.values)
print("Index:", marks.index)
print("Data Type:", marks.dtype)
print("Size:", marks.size)
print("Shape:", marks.shape)
```

Expected output:

```text
Values: [85 90 78 92]
Index: RangeIndex(start=0, stop=4, step=1)
Data Type: int64
Size: 4
Shape: (4,)
```

---

## 4. DataFrame Fundamentals

A DataFrame is a two-dimensional labeled data structure.

It contains rows and columns, similar to:
- Excel spreadsheets
- SQL tables
- CSV files

### 4.1 Creating a DataFrame

```python
import pandas as pd

data = {
    "Name": ["Raj", "Aman", "Priya", "Neha"],
    "Age": [24, 26, 25, 23],
    "Department": ["IT", "HR", "Finance", "IT"],
    "Salary": [35000, 30000, 40000, 32000]
}

df = pd.DataFrame(data)

print(df)
```

Expected output:

```text
    Name  Age Department  Salary
0    Raj   24         IT   35000
1   Aman   26         HR   30000
2  Priya   25    Finance   40000
3   Neha   23         IT   32000
```

Explanation:

- Each dictionary key becomes a column.
- Each list contains values for that column.
- Each row represents one record.
- Each column represents one variable.

### 4.2 DataFrame Properties

```python
print("Shape:", df.shape)
print("Rows:", df.shape[0])
print("Columns:", df.shape[1])
print("Column Names:", df.columns)
print("Index:", df.index)
print("Data Types:")
print(df.dtypes)
```

Expected output:

```text
Shape: (4, 4)
Rows: 4
Columns: 4
Column Names: Index(['Name', 'Age', 'Department', 'Salary'], dtype='object')
Index: RangeIndex(start=0, stop=4, step=1)

Data Types:
Name          object
Age            int64
Department    object
Salary         int64
dtype: object
```

### 4.3 Custom DataFrame Index

```python
df = pd.DataFrame(
    {
        "Name": ["Raj", "Aman", "Priya"],
        "Marks": [85, 90, 95]
    },
    index=["S1", "S2", "S3"]
)

print(df)
```

Expected output:

```text
     Name  Marks
S1    Raj     85
S2   Aman     90
S3  Priya     95
```

---

## 5. Creating DataFrames from Different Sources

Pandas can create DataFrames from dictionaries, lists, NumPy arrays and files.

### 5.1 From a list of dictionaries

```python
data = [
    {"Name": "Raj", "Age": 24},
    {"Name": "Aman", "Age": 26},
    {"Name": "Priya", "Age": 25}
]

df = pd.DataFrame(data)

print(df)
```

### 5.2 From a NumPy array

```python
import numpy as np
import pandas as pd

numbers = np.array([
    [1, 85],
    [2, 90],
    [3, 95]
])

df = pd.DataFrame(
    numbers,
    columns=["Student_ID", "Marks"]
)

print(df)
```

Expected output:

```text
   Student_ID  Marks
0           1     85
1           2     90
2           3     95
```

### 5.3 From a list

```python
data = [
    ["Raj", 85],
    ["Aman", 90],
    ["Priya", 95]
]

df = pd.DataFrame(
    data,
    columns=["Name", "Marks"]
)

print(df)
```

---

## 6. Inspecting a Dataset

When we load a dataset, we should inspect it before analyzing it.

Create a sample DataFrame:

```python
import pandas as pd

data = {
    "Name": ["Raj", "Aman", "Priya", "Neha", "Rohan"],
    "Age": [24, 26, 25, 23, 27],
    "Department": ["IT", "HR", "Finance", "IT", "Sales"],
    "Salary": [35000, 30000, 40000, 32000, 45000]
}

df = pd.DataFrame(data)
```

### 6.1 head()

Displays the first five rows by default.

```python
print(df.head())
```

Display the first two rows:

```python
print(df.head(2))
```

### 6.2 tail()

Displays the last five rows by default.

```python
print(df.tail())
```

Display the last two rows:

```python
print(df.tail(2))
```

### 6.3 info()

Displays information about the DataFrame.

```python
df.info()
```

It provides:
- Number of rows
- Column names
- Non-null values
- Data types
- Memory usage

### 6.4 describe()

Generates descriptive statistics for numerical columns.

```python
print(df.describe())
```

It generally displays:

- Count
- Mean
- Standard deviation
- Minimum
- 25th percentile
- 50th percentile
- 75th percentile
- Maximum

### 6.5 sample()

Displays random rows.

```python
print(df.sample(2, random_state=42))
```

`random_state` makes the sampling reproducible.

### 6.6 Other inspection methods

```python
print(df.shape)
print(df.size)
print(df.ndim)
print(df.columns)
print(df.index)
print(df.dtypes)
```

---

## 7. Reading CSV Files

CSV stands for Comma-Separated Values.

It is one of the most common formats used for storing datasets.

Example CSV file:

Create a file named `students.csv`.

```csv
Name,Age,Marks,City
Raj,22,85,Mumbai
Aman,23,90,Pune
Priya,21,95,Delhi
Neha,22,78,Nashik
Rohan,24,88,Mumbai
```

### 7.1 read_csv()

```python
import pandas as pd

df = pd.read_csv("students.csv")

print(df)
```

Pandas loads the CSV data into a DataFrame.

### 7.2 Reading selected columns

```python
df = pd.read_csv(
    "students.csv",
    usecols=["Name", "Marks"]
)

print(df)
```

### 7.3 Reading limited rows

```python
df = pd.read_csv(
    "students.csv",
    nrows=3
)

print(df)
```

### 7.4 Changing the separator

Some CSV-like files use semicolons instead of commas.

```python
df = pd.read_csv(
    "students.csv",
    sep=","
)
```

Use the separator that matches the actual file.

### 7.5 Handling missing values while reading

```python
df = pd.read_csv(
    "students.csv",
    na_values=["NA", "missing", "unknown"]
)

print(df)
```

These specified values are interpreted as missing values.

---

## 8. Writing and Exporting CSV Files

We can save a DataFrame into a CSV file using `to_csv()`.

```python
import pandas as pd

data = {
    "Name": ["Raj", "Aman", "Priya"],
    "Marks": [85, 90, 95]
}

df = pd.DataFrame(data)

df.to_csv("output.csv", index=False)

print("CSV file created successfully.")
```

Explanation:

- `to_csv()` exports the DataFrame.
- `index=False` prevents Pandas from writing the row index as an extra column.

If we want the index in the file:

```python
df.to_csv("output_with_index.csv", index=True)
```

---

## 9. Reading and Writing Excel Files

Pandas supports Excel files using `read_excel()` and `to_excel()`.

Install the required package:

```bash
pip install openpyxl
```

Read an Excel file:

```python
df = pd.read_excel("students.xlsx")

print(df)
```

Read a specific sheet:

```python
df = pd.read_excel(
    "students.xlsx",
    sheet_name="Sheet1"
)

print(df)
```

Export to Excel:

```python
df.to_excel(
    "students_output.xlsx",
    index=False
)
```

---

## 10. Selecting Columns

Selecting data is one of the most frequently used Pandas operations.

Use the following DataFrame:

```python
import pandas as pd

data = {
    "Name": ["Raj", "Aman", "Priya", "Neha"],
    "Age": [24, 26, 25, 23],
    "Marks": [85, 90, 95, 78],
    "City": ["Mumbai", "Pune", "Delhi", "Nashik"]
}

df = pd.DataFrame(data)
```

### 10.1 Selecting one column

```python
print(df["Name"])
```

Returns a Series.

### 10.2 Selecting multiple columns

```python
print(df[["Name", "Marks"]])
```

Returns a DataFrame.

### 10.3 Selecting all columns

```python
print(df)
```

### 10.4 Accessing a column using dot notation

```python
print(df.Name)
```

Dot notation is convenient but does not work for every column name. Use bracket notation when column names contain spaces, special characters or conflict with DataFrame attributes.

---

## 11. Selecting Rows with loc and iloc

Pandas provides two important selection methods:

- `loc`: label-based selection.
- `iloc`: integer-position-based selection.

### 11.1 loc[]

Select rows using index labels.

```python
data = {
    "Name": ["Raj", "Aman", "Priya"],
    "Marks": [85, 90, 95]
}

df = pd.DataFrame(
    data,
    index=["S1", "S2", "S3"]
)

print(df.loc["S1"])
```

Output:

```text
Name     Raj
Marks     85
Name: S1, dtype: object
```

Select multiple labels:

```python
print(df.loc[["S1", "S3"]])
```

Select rows and columns:

```python
print(df.loc["S1":"S2", ["Name", "Marks"]])
```

### 11.2 iloc[]

Select rows using integer positions.

```python
print(df.iloc[0])
```

Select multiple rows:

```python
print(df.iloc[0:2])
```

Select specific rows and columns:

```python
print(df.iloc[0:2, 0:2])
```

Remember:

- `loc` uses labels.
- `iloc` uses integer positions.
- With `loc`, label-based slices include the ending label.
- With `iloc`, normal Python-style slices exclude the ending position.

---

## 12. Filtering DataFrames

Filtering means selecting records that satisfy a condition.

### 12.1 Single condition

```python
data = {
    "Name": ["Raj", "Aman", "Priya", "Neha"],
    "Marks": [85, 90, 95, 78]
}

df = pd.DataFrame(data)

result = df[df["Marks"] >= 85]

print(result)
```

Expected output:

```text
    Name  Marks
0    Raj     85
1   Aman     90
2  Priya     95
```

### 12.2 Multiple conditions using AND

Use `&` when both conditions must be true.

```python
result = df[
    (df["Marks"] >= 85) &
    (df["Marks"] <= 90)
]

print(result)
```

### 12.3 Multiple conditions using OR

Use `|` when at least one condition must be true.

```python
result = df[
    (df["Marks"] < 80) |
    (df["Marks"] > 90)
]

print(result)
```

Important:

Always place each condition inside parentheses when using `&` or `|`.

### 12.4 Using isin()

Checks whether values belong to a given list.

```python
data = {
    "Name": ["Raj", "Aman", "Priya", "Neha"],
    "City": ["Mumbai", "Pune", "Delhi", "Mumbai"]
}

df = pd.DataFrame(data)

result = df[df["City"].isin(["Mumbai", "Delhi"])]

print(result)
```

### 12.5 Using between()

Selects values within a range.

```python
result = df[df["City"].notna()]
```

For numerical ranges:

```python
marks_df = pd.DataFrame({
    "Name": ["Raj", "Aman", "Priya", "Neha"],
    "Marks": [85, 90, 95, 78]
})

result = marks_df[
    marks_df["Marks"].between(80, 90)
]

print(result)
```

---

## 13. Adding and Updating Columns

### 13.1 Adding a new column

```python
df = pd.DataFrame({
    "Name": ["Raj", "Aman", "Priya"],
    "Marks": [85, 90, 95]
})

df["Result"] = ["Pass", "Pass", "Pass"]

print(df)
```

### 13.2 Creating a column using calculations

```python
df["Bonus_Marks"] = df["Marks"] + 5

print(df)
```

### 13.3 Updating an existing column

```python
df["Marks"] = df["Marks"] + 2

print(df)
```

### 13.4 Conditional column creation

```python
import numpy as np

df["Grade"] = np.where(
    df["Marks"] >= 90,
    "A",
    "B"
)

print(df)
```

For multiple conditions:

```python
conditions = [
    df["Marks"] >= 90,
    df["Marks"] >= 80,
    df["Marks"] >= 40
]

choices = ["A", "B", "C"]

df["Grade"] = np.select(
    conditions,
    choices,
    default="Fail"
)

print(df)
```

---

## 14. Removing Rows and Columns

### 14.1 Removing a column

```python
df = pd.DataFrame({
    "Name": ["Raj", "Aman"],
    "Age": [24, 26],
    "Marks": [85, 90]
})

result = df.drop(columns=["Age"])

print(result)
```

### 14.2 Removing multiple columns

```python
result = df.drop(columns=["Age", "Marks"])

print(result)
```

### 14.3 Removing rows by index label

```python
result = df.drop(index=[0])

print(result)
```

### 14.4 Important: Original DataFrame

By default, `drop()` returns a new DataFrame and does not modify the original.

To update the original:

```python
df.drop(columns=["Age"], inplace=True)
```

Use `inplace=True` carefully because it modifies the existing DataFrame.

---

## 15. Renaming Columns

Use `rename()` to change column names.

```python
df = pd.DataFrame({
    "Student_Name": ["Raj", "Aman"],
    "Student_Marks": [85, 90]
})

df = df.rename(columns={
    "Student_Name": "Name",
    "Student_Marks": "Marks"
})

print(df)
```

Expected output:

```text
   Name  Marks
0   Raj     85
1  Aman     90
```

Rename all columns:

```python
df.columns = ["Student", "Score"]

print(df)
```

---

## 16. Sorting DataFrames

### 16.1 sort_values()

Sort rows based on a column.

```python
df = pd.DataFrame({
    "Name": ["Raj", "Aman", "Priya", "Neha"],
    "Marks": [85, 90, 95, 78]
})

result = df.sort_values(by="Marks")

print(result)
```

### 16.2 Descending order

```python
result = df.sort_values(
    by="Marks",
    ascending=False
)

print(result)
```

### 16.3 Sorting by multiple columns

```python
data = {
    "Department": ["IT", "HR", "IT", "HR"],
    "Name": ["Raj", "Aman", "Priya", "Neha"],
    "Salary": [35000, 30000, 40000, 32000]
}

df = pd.DataFrame(data)

result = df.sort_values(
    by=["Department", "Salary"],
    ascending=[True, False]
)

print(result)
```

### 16.4 sort_index()

Sorts by index labels.

```python
print(df.sort_index())
```

---

## 17. Basic Data Analysis

Pandas provides built-in methods for analyzing numerical columns.

```python
df = pd.DataFrame({
    "Name": ["Raj", "Aman", "Priya", "Neha"],
    "Marks": [85, 90, 95, 78],
    "Age": [22, 23, 21, 22]
})
```

Calculate average:

```python
print(df["Marks"].mean())
```

Calculate total:

```python
print(df["Marks"].sum())
```

Find maximum:

```python
print(df["Marks"].max())
```

Find minimum:

```python
print(df["Marks"].min())
```

Find median:

```python
print(df["Marks"].median())
```

Find standard deviation:

```python
print(df["Marks"].std())
```

Count non-missing values:

```python
print(df["Marks"].count())
```

Get descriptive statistics:

```python
print(df.describe())
```

---

## 18. Understanding Data Types

Pandas automatically detects many data types when creating or reading a DataFrame.

Common Pandas data types include:

| Data Type | Meaning |
|---|---|
| int64 | Integer numbers |
| float64 | Decimal numbers |
| object | General Python objects, often strings |
| string | String data |
| bool | True or False |
| datetime64 | Date and time values |

Example:

```python
df = pd.DataFrame({
    "Name": ["Raj", "Aman", "Priya"],
    "Age": [22, 23, 21],
    "Marks": [85.5, 90.0, 95.5]
})

print(df.dtypes)
```

### 18.1 astype()

Changes a column's data type.

```python
df["Age"] = df["Age"].astype(float)

print(df.dtypes)
```

### 18.2 to_numeric()

Converts values into numerical data.

```python
data = pd.Series(["100", "200", "300"])

numbers = pd.to_numeric(data)

print(numbers)
print(numbers.dtype)
```

Handle invalid values:

```python
data = pd.Series(["100", "200", "unknown"])

numbers = pd.to_numeric(
    data,
    errors="coerce"
)

print(numbers)
```

Expected output:

```text
0    100.0
1    200.0
2      NaN
dtype: float64
```

`errors="coerce"` converts invalid values into missing values.

---

## 19. Mini-Project: Student Data Analyzer

### Project Description

Build a Student Data Analyzer using Pandas.

The application will:

1. Create a student dataset.
2. Display all student records.
3. Inspect the dataset.
4. Calculate average marks.
5. Filter passed students.
6. Find the highest-scoring student.
7. Sort students by marks.
8. Add grades.
9. Export the final result to CSV.

### Complete Program

```python
import pandas as pd
import numpy as np

# Create student dataset
data = {
    "Name": [
        "Raj",
        "Aman",
        "Priya",
        "Neha",
        "Rohan",
        "Simran"
    ],

    "Age": [22, 23, 21, 22, 24, 23],

    "City": [
        "Mumbai",
        "Pune",
        "Delhi",
        "Mumbai",
        "Nashik",
        "Pune"
    ],

    "Marks": [85, 90, 95, 35, 78, 88]
}

df = pd.DataFrame(data)

print("========== STUDENT DATA ==========")

print(df)

# Inspect dataset
print("\n========== DATASET INFORMATION ==========")

print("Shape:", df.shape)

df.info()

# Average marks
average_marks = df["Marks"].mean()

print("\nAverage Marks:", average_marks)

# Highest marks
highest_index = df["Marks"].idxmax()

print("\nTop Student:")

print(df.loc[highest_index])

# Lowest marks
lowest_index = df["Marks"].idxmin()

print("\nLowest Scoring Student:")

print(df.loc[lowest_index])

# Filter passed students
passed_students = df[df["Marks"] >= 40]

print("\n========== PASSED STUDENTS ==========")

print(passed_students)

# Filter failed students
failed_students = df[df["Marks"] < 40]

print("\n========== FAILED STUDENTS ==========")

print(failed_students)

# Sort students by marks
sorted_students = df.sort_values(
    by="Marks",
    ascending=False
)

print("\n========== STUDENT RANKING ==========")

print(sorted_students)

# Add grades
conditions = [
    df["Marks"] >= 90,
    df["Marks"] >= 80,
    df["Marks"] >= 70,
    df["Marks"] >= 40
]

choices = ["A", "B", "C", "D"]

df["Grade"] = np.select(
    conditions,
    choices,
    default="Fail"
)

print("\n========== FINAL STUDENT RESULTS ==========")

print(df)

# City-wise student count
print("\n========== CITY-WISE COUNT ==========")

print(df["City"].value_counts())

# Export results
df.to_csv(
    "student_results.csv",
    index=False
)

print("\nStudent results exported successfully.")
```

### Expected observations

The student should identify:

- The average marks of the class.
- The highest and lowest scoring students.
- Students who passed and failed.
- Student ranking from highest to lowest.
- The grade assigned to each student.
- The number of students from each city.

The program creates `student_results.csv` in the current working directory.

---

## 20. Student Practice Exercises

### Exercise 1: Create a Series

Create a Pandas Series containing marks of five students.

Tasks:

1. Assign custom student names as indexes.
2. Display the Series.
3. Access the marks of one student.
4. Calculate the average.
5. Display the highest mark.

### Exercise 2: Create a DataFrame

Create a DataFrame containing:

- Employee Name
- Employee ID
- Age
- Department
- Salary

Add at least five employee records.

Tasks:

1. Print the DataFrame.
2. Display its shape.
3. Display column names.
4. Display data types.
5. Show the first three rows.

### Exercise 3: CSV Operations

Create a CSV file containing product information.

Columns:

- Product
- Price
- Quantity
- Category

Tasks:

1. Read the CSV file.
2. Display its contents.
3. Select Product and Price columns.
4. Calculate the total quantity.
5. Export the result to a new CSV file.

### Exercise 4: Data Filtering

Create a student DataFrame.

Tasks:

1. Find students scoring more than 80.
2. Find students scoring less than 40.
3. Find students between 60 and 90.
4. Filter students from Mumbai.
5. Find students from Mumbai who scored more than 75.

### Exercise 5: Data Modification

Create an employee DataFrame.

Tasks:

1. Add a Bonus column.
2. Calculate bonus as 10% of salary.
3. Rename Salary to Monthly_Salary.
4. Remove the Age column.
5. Sort employees by salary.

### Exercise 6: Data Analysis

Create a DataFrame containing marks of 10 students.

Tasks:

1. Calculate mean.
2. Calculate median.
3. Calculate maximum and minimum.
4. Calculate standard deviation.
5. Count students who passed.
6. Find the top three students.

---

## 21. Trainer Assessment

Ask the student:

1. What is Pandas?
2. What is the difference between Series and DataFrame?
3. What does `pd` represent?
4. How do we create a DataFrame?
5. What is the purpose of `head()` and `tail()`?
6. What information does `info()` provide?
7. What is the difference between `loc` and `iloc`?
8. How do we select multiple columns?
9. How do we filter records using multiple conditions?
10. What does `read_csv()` do?
11. What is the purpose of `to_csv()`?
12. What does `describe()` calculate?
13. How do we rename a column?
14. How do we sort a DataFrame?
15. What does `astype()` do?

### Practical Assessment

Ask the student to create an Employee Data Analyzer.

The program must:

- Store at least 10 employee records.
- Display employee information.
- Calculate average salary.
- Find the highest-paid employee.
- Filter employees by department.
- Find employees earning more than a given salary.
- Sort employees by salary.
- Add a bonus column.
- Export the final DataFrame to CSV.

The student should complete the program independently.

---

## 22. Completion Criteria

The student should be able to:

- Explain Series and DataFrame.
- Create Pandas data structures.
- Load CSV and Excel datasets.
- Inspect dataset structure.
- Select rows and columns.
- Filter data using conditions.
- Add, update and remove columns.
- Rename and sort data.
- Perform basic statistical analysis.
- Convert data types.
- Export DataFrames into CSV and Excel files.
- Complete the Student Data Analyzer independently.

---

## 23. Next Day Preview

**Day 49 – Pandas Advanced: Data Cleaning, Missing Values, GroupBy, Merge, Join & Aggregation**

Topics:

- Handling missing values
- Removing duplicate records
- Replacing incorrect values
- GroupBy operations
- Aggregation functions
- Merging DataFrames
- Joining DataFrames
- Concatenating datasets
- Applying custom functions
- Date and time operations
- Advanced data cleaning project

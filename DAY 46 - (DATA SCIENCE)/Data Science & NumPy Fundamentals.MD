
# Day 46 – Introduction to Data Science & NumPy Fundamentals

## 1. What is Data Science?

Data Science is a field that uses data, programming, mathematics, and statistics to discover useful information and solve real-world problems.

It helps organizations make decisions using data instead of guesses.

### Real-World Examples

1. Netflix recommends movies based on viewing history.
2. Amazon recommends products based on shopping behavior.
3. Banks identify unusual transactions.
4. Hospitals analyze patient data.
5. Weather applications predict future weather.
6. Businesses analyze sales to understand customer behavior.

### What is Data?

Data is a collection of facts, values, observations, or information.

Examples:

```python
student_names = ["Raj", "Amit", "Priya"]

student_marks = [85, 72, 91, 68]

temperatures = [28.5, 30.2, 27.8, 31.0]
```

Data can be:
- Structured: tables, spreadsheets, databases.
- Semi-structured: JSON, XML.
- Unstructured: images, videos, audio, documents.

### What is Information?

Information is meaningful data that has been processed or analyzed.

Example:

Raw data:

```python
marks = [85, 72, 91, 68]
```

Calculated information:

```python
average = sum(marks) / len(marks)

print("Average Marks:", average)
```

Output:

```text
Average Marks: 79.0
```

---

## 2. Data Science vs Data Analytics vs Machine Learning vs AI

These terms are related but have different meanings.

| Field | Meaning |
|---|---|
| Data Science | Uses data, statistics, and programming to solve problems |
| Data Analytics | Examines data to find patterns and answer questions |
| Machine Learning | Trains algorithms to learn patterns from data |
| Artificial Intelligence | Builds systems that perform tasks requiring intelligence |

### Example

Imagine an online shopping company.

- Data Analytics: Finds which products sold the most.
- Data Science: Studies customer behavior and builds predictive solutions.
- Machine Learning: Predicts which product a customer may purchase.
- Artificial Intelligence: Uses intelligent systems to automate recommendations and other tasks.

---

## 3. Data Science Workflow

A typical Data Science project follows these steps:

1. Problem Definition
2. Data Collection
3. Data Cleaning
4. Exploratory Data Analysis (EDA)
5. Data Visualization
6. Feature Engineering
7. Model Building (when prediction is required)
8. Model Evaluation
9. Deployment
10. Monitoring

### Example: Student Performance Analysis

Problem:

Find out why students are receiving low marks.

Data collection:

```python
students = [
    {"name": "Raj", "marks": 85, "attendance": 90},
    {"name": "Amit", "marks": 45, "attendance": 60},
    {"name": "Priya", "marks": 92, "attendance": 95},
    {"name": "Rohan", "marks": 55, "attendance": 65}
]
```

Data analysis:

```python
for student in students:

    if student["marks"] < 60:
        print(student["name"], "Needs Improvement")
```

Output:

```text
Amit Needs Improvement
Rohan Needs Improvement
```

This is a simple example of extracting useful information from data.

---

## 4. Important Python Libraries for Data Science

Python has many libraries for Data Science.

| Library | Purpose |
|---|---|
| NumPy | Numerical computing and arrays |
| Pandas | Data manipulation and analysis |
| Matplotlib | Data visualization |
| Seaborn | Statistical visualization |
| SciPy | Scientific computing |
| Scikit-learn | Machine Learning |
| TensorFlow | Deep Learning |
| PyTorch | Deep Learning |
| Plotly | Interactive visualizations |

### Learning Order

For this training track, follow this order:

1. NumPy
2. Pandas
3. Data Cleaning
4. Exploratory Data Analysis
5. Statistics Fundamentals
6. Data Visualization
7. Machine Learning Fundamentals
8. Practical Data Science Projects

---

## 5. Introduction to NumPy

NumPy stands for Numerical Python.

It is a Python library used for numerical calculations and working with arrays.

NumPy provides:
- Fast array operations.
- Mathematical functions.
- Statistical calculations.
- Matrix operations.
- Multi-dimensional arrays.
- Broadcasting.

### Why Use NumPy?

Python lists can store collections of values, but NumPy arrays are designed for efficient numerical operations.

Example using a normal Python list:

```python
numbers = [10, 20, 30, 40]

result = []

for number in numbers:
    result.append(number * 2)

print(result)
```

Output:

```text
[20, 40, 60, 80]
```

Using NumPy:

```python
import numpy as np

numbers = np.array([10, 20, 30, 40])

result = numbers * 2

print(result)
```

Output:

```text
[20 40 60 80]
```

NumPy performs the operation on every array element without writing an explicit loop.

---

## 6. Installing NumPy

Open the terminal.

Install NumPy:

```bash
python -m pip install numpy
```

Verify installation:

```bash
python -m pip show numpy
```

Check the installed version:

```python
import numpy as np

print(np.__version__)
```

The version may differ depending on when NumPy is installed.

### Understanding the Import

```python
import numpy as np
```

- `numpy` is the library name.
- `np` is its commonly used alias.
- `np` makes NumPy functions shorter to write.

---

## 7. Creating NumPy Arrays

NumPy arrays are created using `np.array()`.

### One-Dimensional Array

```python
import numpy as np

numbers = np.array([10, 20, 30, 40, 50])

print(numbers)
```

Output:

```text
[10 20 30 40 50]
```

### Two-Dimensional Array

```python
matrix = np.array([
    [10, 20, 30],
    [40, 50, 60]
])

print(matrix)
```

Output:

```text
[[10 20 30]
 [40 50 60]]
```

### Three-Dimensional Array

```python
data = np.array([
    [
        [1, 2],
        [3, 4]
    ],
    [
        [5, 6],
        [7, 8]
    ]
])

print(data)
```

Output:

```text
[[[1 2]
  [3 4]]

 [[5 6]
  [7 8]]]
```

### Creating an Array from a Python List

```python
marks = [85, 90, 75, 88]

array_marks = np.array(marks)

print(array_marks)
```

---

## 8. Understanding NumPy Array Properties

NumPy provides several properties to understand an array.

```python
import numpy as np

numbers = np.array([10, 20, 30, 40])

print("Array:", numbers)
print("Dimensions:", numbers.ndim)
print("Shape:", numbers.shape)
print("Size:", numbers.size)
print("Data Type:", numbers.dtype)
```

Output will look similar to:

```text
Array: [10 20 30 40]
Dimensions: 1
Shape: (4,)
Size: 4
Data Type: int64
```

The integer data type may differ depending on the system.

### Important Properties

| Property | Meaning |
|---|---|
| `ndim` | Number of dimensions |
| `shape` | Size of each dimension |
| `size` | Total number of elements |
| `dtype` | Data type of array elements |

### Example with a 2D Array

```python
matrix = np.array([
    [1, 2, 3],
    [4, 5, 6]
])

print(matrix.ndim)
print(matrix.shape)
print(matrix.size)
```

Output:

```text
2
(2, 3)
6
```

Explanation:

- 2 dimensions.
- 2 rows.
- 3 columns.
- 6 total elements.

---

## 9. NumPy Array Data Types

NumPy arrays generally store elements using a common data type.

Examples:

```python
integers = np.array([10, 20, 30])

decimals = np.array([10.5, 20.5, 30.5])

characters = np.array(["A", "B", "C"])

booleans = np.array([True, False, True])
```

Check data types:

```python
print(integers.dtype)
print(decimals.dtype)
print(characters.dtype)
print(booleans.dtype)
```

### Specify a Data Type

```python
numbers = np.array([10, 20, 30], dtype=np.float64)

print(numbers)
print(numbers.dtype)
```

Output:

```text
[10. 20. 30.]
float64
```

### Type Conversion

```python
numbers = np.array([10.8, 20.5, 30.9])

integer_numbers = numbers.astype(int)

print(integer_numbers)
```

Output:

```text
[10 20 30]
```

Note: Converting floating-point values to integers truncates the decimal portion; it does not round to the nearest integer.

---

## 10. Special NumPy Arrays

NumPy provides functions to create arrays quickly.

### np.zeros()

Creates an array filled with zeros.

```python
zeros = np.zeros(5)

print(zeros)
```

Output:

```text
[0. 0. 0. 0. 0.]
```

### np.ones()

Creates an array filled with ones.

```python
ones = np.ones(4)

print(ones)
```

Output:

```text
[1. 1. 1. 1.]
```

### np.full()

Creates an array filled with a specified value.

```python
values = np.full(5, 7)

print(values)
```

Output:

```text
[7 7 7 7 7]
```

### np.arange()

Creates values within a specified range.

```python
numbers = np.arange(1, 11)

print(numbers)
```

Output:

```text
[ 1  2  3  4  5  6  7  8  9 10]
```

Syntax:

```python
np.arange(start, stop, step)
```

Example:

```python
numbers = np.arange(2, 11, 2)

print(numbers)
```

Output:

```text
[ 2  4  6  8 10]
```

### np.linspace()

Creates a specified number of equally spaced values between two endpoints.

```python
numbers = np.linspace(0, 10, 5)

print(numbers)
```

Output:

```text
[ 0.   2.5  5.   7.5 10. ]
```

Unlike `arange()`, `linspace()` specifies how many values to generate.

### Identity Matrix

```python
identity = np.eye(3)

print(identity)
```

Output:

```text
[[1. 0. 0.]
 [0. 1. 0.]
 [0. 0. 1.]]
```

---

## 11. Array Indexing

Indexing is used to access individual array elements.

### One-Dimensional Array

```python
numbers = np.array([10, 20, 30, 40, 50])

print(numbers[0])
print(numbers[2])
print(numbers[-1])
```

Output:

```text
10
30
50
```

### Two-Dimensional Array

```python
matrix = np.array([
    [10, 20, 30],
    [40, 50, 60]
])

print(matrix[0, 0])
print(matrix[0, 2])
print(matrix[1, 1])
```

Output:

```text
10
30
50
```

Syntax:

```python
array[row_index, column_index]
```

---

## 12. Array Slicing

Slicing extracts a portion of an array.

Syntax:

```python
array[start:stop:step]
```

Example:

```python
numbers = np.array([10, 20, 30, 40, 50, 60])

print(numbers[1:4])
print(numbers[:3])
print(numbers[2:])
print(numbers[::2])
print(numbers[::-1])
```

Output:

```text
[20 30 40]
[10 20 30]
[30 40 50 60]
[10 30 50]
[60 50 40 30 20 10]
```

### Slicing a 2D Array

```python
matrix = np.array([
    [1, 2, 3],
    [4, 5, 6],
    [7, 8, 9]
])

print(matrix[0:2, 0:2])
```

Output:

```text
[[1 2]
 [4 5]]
```

Explanation:

- `0:2` selects the first two rows.
- `0:2` selects the first two columns.

**Important:** Basic NumPy slicing usually returns a view of the original array, not an independent copy. Changing the view can change the original array.

---

## 13. Modifying Array Elements

NumPy arrays are mutable.

```python
numbers = np.array([10, 20, 30, 40])

numbers[1] = 100

print(numbers)
```

Output:

```text
[ 10 100  30  40]
```

### Modifying Multiple Elements

```python
numbers = np.array([10, 20, 30, 40, 50])

numbers[1:4] = 0

print(numbers)
```

Output:

```text
[10  0  0  0 50]
```

### Copying an Array

```python
original = np.array([10, 20, 30])

copied = original.copy()

copied[0] = 100

print("Original:", original)
print("Copied:", copied)
```

Output:

```text
Original: [10 20 30]
Copied: [100  20  30]
```

---

## 14. Mathematical Operations on Arrays

NumPy supports element-wise mathematical operations.

```python
a = np.array([10, 20, 30])
b = np.array([1, 2, 3])

print(a + b)
print(a - b)
print(a * b)
print(a / b)
print(a ** 2)
```

Output:

```text
[11 22 33]
[ 9 18 27]
[10 40 90]
[10. 10. 10.]
[100 400 900]
```

### Scalar Operations

```python
numbers = np.array([10, 20, 30])

print(numbers + 5)
print(numbers * 2)
print(numbers / 10)
```

Output:

```text
[15 25 35]
[20 40 60]
[1. 2. 3.]
```

### Comparison Operations

```python
marks = np.array([45, 65, 85, 35, 90])

print(marks > 50)
```

Output:

```text
[False  True  True False  True]
```

### Logical Operations

```python
marks = np.array([45, 65, 85, 35, 90])

result = (marks >= 40) & (marks <= 80)

print(result)
```

Output:

```text
[ True  True False False False]
```

---

## 15. NumPy Aggregation Functions

Aggregation functions calculate a summary from array values.

```python
marks = np.array([85, 90, 75, 88, 92])

print("Sum:", np.sum(marks))
print("Mean:", np.mean(marks))
print("Maximum:", np.max(marks))
print("Minimum:", np.min(marks))
print("Standard Deviation:", np.std(marks))
print("Variance:", np.var(marks))
```

Output:

```text
Sum: 430
Mean: 86.0
Maximum: 92
Minimum: 75
Standard Deviation: 6.0
Variance: 36.0
```

### Other Useful Functions

```python
numbers = np.array([10, 20, 30, 40, 50])

print(np.median(numbers))
print(np.argmin(numbers))
print(np.argmax(numbers))
print(np.sort(numbers))
print(np.unique(numbers))
```

Output:

```text
30.0
0
4
[10 20 30 40 50]
[10 20 30 40 50]
```

| Function | Purpose |
|---|---|
| `np.sum()` | Calculates total |
| `np.mean()` | Calculates average |
| `np.median()` | Calculates median |
| `np.max()` | Finds maximum |
| `np.min()` | Finds minimum |
| `np.std()` | Calculates standard deviation |
| `np.var()` | Calculates variance |
| `np.argmax()` | Returns index of maximum |
| `np.argmin()` | Returns index of minimum |
| `np.sort()` | Returns sorted values |
| `np.unique()` | Returns unique values |

---

## 16. Reshaping Arrays

Reshaping changes the dimensions of an array without changing its data.

Example:

```python
numbers = np.array([1, 2, 3, 4, 5, 6])

matrix = numbers.reshape(2, 3)

print(matrix)
```

Output:

```text
[[1 2 3]
 [4 5 6]]
```

### Reshape into 3 Rows

```python
matrix = numbers.reshape(3, 2)

print(matrix)
```

Output:

```text
[[1 2]
 [3 4]
 [5 6]]
```

The total number of elements must remain the same.

### Using -1

NumPy can automatically calculate one dimension.

```python
numbers = np.array([1, 2, 3, 4, 5, 6])

matrix = numbers.reshape(2, -1)

print(matrix)
```

Output:

```text
[[1 2 3]
 [4 5 6]]
```

### Flatten an Array

```python
matrix = np.array([
    [1, 2, 3],
    [4, 5, 6]
])

flat = matrix.flatten()

print(flat)
```

Output:

```text
[1 2 3 4 5 6]
```

`flatten()` returns a copy. `ravel()` can return a view when possible.

---

## 17. Understanding Axis in NumPy

The `axis` parameter controls the direction of an operation.

For a 2D array:

- `axis=0` performs an operation down the rows, producing column-wise results.
- `axis=1` performs an operation across columns, producing row-wise results.

Example:

```python
marks = np.array([
    [80, 90, 85],
    [70, 75, 80],
    [90, 95, 92]
])

print("Column totals:")
print(np.sum(marks, axis=0))

print("Row totals:")
print(np.sum(marks, axis=1))
```

Output:

```text
Column totals:
[240 260 257]

Row totals:
[255 225 277]
```

### Calculate Average Per Student

```python
average = np.mean(marks, axis=1)

print(average)
```

Output:

```text
[85.         75.         92.33333333]
```

### Calculate Average Per Subject

```python
subject_average = np.mean(marks, axis=0)

print(subject_average)
```

Output:

```text
[80.         86.66666667 85.66666667]
```

---

## 18. Broadcasting in NumPy

Broadcasting allows NumPy to perform operations on arrays with compatible shapes.

Example:

```python
numbers = np.array([10, 20, 30])

result = numbers + 5

print(result)
```

Output:

```text
[15 25 35]
```

The scalar value `5` is applied to every element.

### Broadcasting with 2D Arrays

```python
matrix = np.array([
    [10, 20, 30],
    [40, 50, 60]
])

values = np.array([1, 2, 3])

result = matrix + values

print(result)
```

Output:

```text
[[11 22 33]
 [41 52 63]]
```

### Broadcasting Rule

Starting from the last dimension, two dimensions are compatible when:

- They are equal, or
- One of them is 1.

If dimensions are not compatible, NumPy raises a broadcasting error.

---

## 19. Filtering Arrays Using Conditions

Boolean indexing helps select values that satisfy a condition.

```python
marks = np.array([35, 45, 67, 89, 92, 28])

passed = marks[marks >= 40]

print(passed)
```

Output:

```text
[45 67 89 92]
```

### Multiple Conditions

```python
marks = np.array([35, 45, 67, 89, 92, 28])

result = marks[(marks >= 40) & (marks <= 80)]

print(result)
```

Output:

```text
[45 67]
```

Use `&` for element-wise AND and `|` for element-wise OR. Put each comparison inside parentheses.

### Replace Values Based on Conditions

```python
marks = np.array([35, 45, 67, 89, 92, 28])

marks[marks < 40] = 0

print(marks)
```

Output:

```text
[ 0 45 67 89 92  0]
```

---

## 20. Random Numbers Using NumPy

NumPy provides a random number generator.

Recommended approach:

```python
rng = np.random.default_rng(seed=42)
```

The seed makes results reproducible.

### Generate Random Integers

```python
rng = np.random.default_rng(seed=42)

numbers = rng.integers(1, 101, size=5)

print(numbers)
```

The same seed and NumPy version produce reproducible results.

### Generate Random Decimal Values

```python
rng = np.random.default_rng(seed=42)

numbers = rng.random(5)

print(numbers)
```

### Generate a Random 2D Array

```python
rng = np.random.default_rng(seed=42)

matrix = rng.integers(1, 10, size=(3, 3))

print(matrix)
```

### Shuffle an Array

```python
rng = np.random.default_rng(seed=42)

numbers = np.array([1, 2, 3, 4, 5])

rng.shuffle(numbers)

print(numbers)
```

---

## 21. Matrix Operations

NumPy supports mathematical matrix operations.

### Matrix Addition

```python
a = np.array([
    [1, 2],
    [3, 4]
])

b = np.array([
    [5, 6],
    [7, 8]
])

print(a + b)
```

Output:

```text
[[ 6  8]
 [10 12]]
```

### Matrix Multiplication

The `@` operator performs matrix multiplication.

```python
a = np.array([
    [1, 2],
    [3, 4]
])

b = np.array([
    [5, 6],
    [7, 8]
])

print(a @ b)
```

Output:

```text
[[19 22]
 [43 50]]
```

### Element-wise Multiplication vs Matrix Multiplication

```python
print(a * b)
print(a @ b)
```

`*` multiplies corresponding elements.

`@` performs matrix multiplication.

### Transpose

```python
matrix = np.array([
    [1, 2, 3],
    [4, 5, 6]
])

print(matrix.T)
```

Output:

```text
[[1 4]
 [2 5]
 [3 6]]
```

---

## 22. NumPy Performance Compared with Python Lists

NumPy is optimized for numerical operations and often performs large numerical calculations faster than equivalent Python loops.

Example:

```python
import numpy as np
import time

numbers = np.arange(1, 1_000_001)

start = time.perf_counter()

result = [number * 2 for number in numbers]

list_time = time.perf_counter() - start

start = time.perf_counter()

result_array = numbers * 2

numpy_time = time.perf_counter() - start

print("Python List Time:", list_time)
print("NumPy Time:", numpy_time)
```

The actual timings depend on hardware, Python version, and system load.

**Important:** NumPy is not guaranteed to be faster for every small operation. Performance depends on data size and the operation being performed.

---

## 23. Practical Programs

### Program 1: Student Marks Analysis

```python
import numpy as np

marks = np.array([85, 90, 75, 60, 95])

print("Total:", np.sum(marks))
print("Average:", np.mean(marks))
print("Highest:", np.max(marks))
print("Lowest:", np.min(marks))

passed = marks[marks >= 40]

print("Passed Marks:", passed)
```

### Program 2: Temperature Analysis

```python
import numpy as np

temperatures = np.array([28, 30, 32, 29, 35, 31, 27])

print("Average:", np.mean(temperatures))
print("Maximum:", np.max(temperatures))
print("Minimum:", np.min(temperatures))

hot_days = temperatures[temperatures > 30]

print("Hot Days:", hot_days)
```

### Program 3: Sales Analysis

```python
import numpy as np

sales = np.array([1000, 1500, 2000, 1800, 2500])

print("Total Sales:", np.sum(sales))
print("Average Sales:", np.mean(sales))
print("Highest Sales:", np.max(sales))
print("Lowest Sales:", np.min(sales))
```

### Program 4: Matrix Addition

```python
import numpy as np

a = np.array([
    [10, 20],
    [30, 40]
])

b = np.array([
    [1, 2],
    [3, 4]
])

result = a + b

print("Result:")
print(result)
```

### Program 5: Count Passing Students

```python
import numpy as np

marks = np.array([35, 45, 67, 89, 92, 28, 76])

passed = marks[marks >= 40]

print("Passing Students:", len(passed))
print("Failing Students:", len(marks[marks < 40]))
```

---

## 24. Mini Project – Student Performance Analyzer Using NumPy

### Project Description

Create a program that analyzes student marks using NumPy.

The program should calculate:
- Total marks per student.
- Average marks per student.
- Highest and lowest marks.
- Subject-wise average.
- Passed and failed students.
- Highest-performing student.
- Overall class average.

### Sample Data

Each row represents a student. Each column represents a subject.

```python
import numpy as np

students = np.array([
    [85, 90, 80],
    [70, 75, 65],
    [95, 92, 98],
    [35, 40, 30],
    [80, 85, 88]
])

student_names = np.array([
    "Raj",
    "Amit",
    "Priya",
    "Rohan",
    "Neha"
])

subjects = ["Python", "Maths", "Science"]
```

### Requirements

1. Display all student marks.
2. Calculate total marks for each student.
3. Calculate average marks for each student.
4. Calculate subject-wise average.
5. Find the highest mark in the dataset.
6. Find the lowest mark in the dataset.
7. Identify students with an average of at least 40.
8. Identify students with an average below 40.
9. Find the highest-performing student.
10. Calculate the overall class average.

### Suggested Implementation

```python
import numpy as np

students = np.array([
    [85, 90, 80],
    [70, 75, 65],
    [95, 92, 98],
    [35, 40, 30],
    [80, 85, 88]
])

student_names = np.array([
    "Raj",
    "Amit",
    "Priya",
    "Rohan",
    "Neha"
])

subjects = ["Python", "Maths", "Science"]

# Calculate student totals
totals = np.sum(students, axis=1)

# Calculate student averages
averages = np.mean(students, axis=1)

# Calculate subject averages
subject_averages = np.mean(students, axis=0)

# Find highest and lowest marks
highest = np.max(students)
lowest = np.min(students)

# Find highest-performing student
top_index = np.argmax(averages)

# Find passed and failed students
passed = averages >= 40
failed = averages < 40

print("STUDENT PERFORMANCE REPORT")
print("-" * 35)

for i in range(len(student_names)):

    print("Name:", student_names[i])
    print("Total:", totals[i])
    print("Average:", round(averages[i], 2))

    if passed[i]:
        print("Result: PASS")
    else:
        print("Result: FAIL")

    print("-" * 35)

print("SUBJECT AVERAGES")

for i in range(len(subjects)):
    print(subjects[i], ":", round(subject_averages[i], 2))

print("Highest Mark:", highest)
print("Lowest Mark:", lowest)

print("Top Student:", student_names[top_index])

print("Passed Students:", student_names[passed])
print("Failed Students:", student_names[failed])

print("Class Average:", np.mean(students))
```

### Expected Result

The program should display:
- Individual student reports.
- Subject averages.
- Highest and lowest marks.
- Top student.
- Passed and failed student names.
- Overall class average.

### Additional Challenges

1. Add a grade system.
2. Find the second-highest student average.
3. Sort students by average marks.
4. Generate random marks for 100 students.
5. Identify subjects where the class average is below 50.
6. Calculate the standard deviation of each subject.

---

## 25. Student Practice Questions

### Theory Questions

1. What is Data Science?
2. What is the difference between data and information?
3. Explain structured, semi-structured, and unstructured data.
4. What is the difference between Data Science and Data Analytics?
5. What is NumPy?
6. Why is NumPy used in Data Science?
7. What is an ndarray?
8. Explain `ndim`, `shape`, `size`, and `dtype`.
9. What is the difference between `arange()` and `linspace()`?
10. What is array slicing?
11. What is broadcasting?
12. What is the difference between `*` and `@`?
13. What is the difference between `axis=0` and `axis=1`?
14. What is Boolean indexing?
15. Why is NumPy often faster than Python loops for numerical calculations?

### Practical Questions

1. Create a one-dimensional NumPy array.
2. Create a 3x3 matrix.
3. Display the shape and dimensions of an array.
4. Create an array containing zeros and ones.
5. Generate numbers from 1 to 100.
6. Extract even numbers from an array.
7. Calculate the average of 10 numbers.
8. Find the maximum and minimum values.
9. Reshape a 1D array into a 2D array.
10. Add two matrices.
11. Multiply two matrices.
12. Find row-wise and column-wise averages.
13. Filter all values greater than 50.
14. Generate a random 4x4 matrix.
15. Complete the Student Performance Analyzer.

---

## 26. Trainer Assessment

| Assessment | Expected Result |
|---|---|
| Data Science introduction | Explains Data Science with examples |
| Library knowledge | Identifies important Python libraries |
| NumPy installation | Installs and imports NumPy |
| Array creation | Creates 1D, 2D, and 3D arrays |
| Array properties | Uses `ndim`, `shape`, `size`, `dtype` |
| Indexing and slicing | Extracts correct array values |
| Mathematical operations | Performs element-wise operations |
| Aggregation | Calculates statistical summaries |
| Reshaping | Changes array dimensions correctly |
| Broadcasting | Understands compatible array shapes |
| Boolean filtering | Selects values using conditions |
| Matrix operations | Performs matrix addition and multiplication |
| Mini project | Completes Student Performance Analyzer |

---

## 27. Completion Criteria

Day 46 is complete when the student can:

- Explain Data Science and its applications.
- Understand the basic Data Science workflow.
- Identify common Python Data Science libraries.
- Install and import NumPy.
- Create NumPy arrays.
- Work with 1D, 2D, and 3D arrays.
- Understand array properties and data types.
- Use indexing and slicing.
- Perform mathematical and statistical operations.
- Reshape and flatten arrays.
- Understand axis and broadcasting.
- Filter arrays using conditions.
- Perform basic matrix operations.
- Complete the Student Performance Analyzer.

**Trainer Note:** Make sure the student writes and runs the NumPy programs independently. Do not move directly to Pandas without practicing arrays, indexing, filtering, and aggregation.

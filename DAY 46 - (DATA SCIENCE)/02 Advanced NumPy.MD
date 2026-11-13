
# Day 47 – Advanced NumPy: Array Manipulation, Mathematical Functions, Statistics & Linear Algebra

## 1. Introduction

In Day 46, we learned NumPy fundamentals, including arrays, indexing, slicing, broadcasting and basic mathematical operations.

Today, we will explore advanced NumPy operations used in Data Science.

Topics covered:

1. Advanced array manipulation
2. Joining and splitting arrays
3. Sorting and searching arrays
4. Conditional operations
5. Handling missing values
6. Mathematical functions
7. Statistical operations
8. Random sampling and distributions
9. Linear algebra
10. Views, copies and memory management
11. Mini-project: Sales Data Analyzer

---

## 2. Setup and Import NumPy

Install NumPy if it is not already installed:

```bash
pip install numpy
```

Import NumPy:

```python
import numpy as np

print(np.__version__)
```

Expected output:

```text
2.x.x
```

The exact version may differ.

---

## 3. Advanced Array Manipulation

### 3.1 reshape()

The `reshape()` function changes the shape of an array without changing its data.

Example:

```python
import numpy as np

numbers = np.arange(1, 13)

print(numbers)

matrix = numbers.reshape(3, 4)

print(matrix)
```

Expected output:

```text
[ 1  2  3  4  5  6  7  8  9 10 11 12]

[[ 1  2  3  4]
 [ 5  6  7  8]
 [ 9 10 11 12]]
```

Important:

The total number of elements must remain the same.

For example, an array containing 12 elements can be reshaped into:

- 2 × 6
- 3 × 4
- 4 × 3
- 6 × 2

But it cannot be reshaped into 3 × 5.

### 3.2 Using -1 in reshape()

NumPy can automatically calculate one dimension when we use `-1`.

```python
numbers = np.arange(1, 13)

matrix = numbers.reshape(3, -1)

print(matrix)
```

Expected output:

```text
[[ 1  2  3  4]
 [ 5  6  7  8]
 [ 9 10 11 12]]
```

Here, NumPy automatically calculates the second dimension as 4.

### 3.3 flatten()

`flatten()` converts a multidimensional array into a one-dimensional array.

```python
matrix = np.array([
    [1, 2, 3],
    [4, 5, 6]
])

result = matrix.flatten()

print(result)
```

Expected output:

```text
[1 2 3 4 5 6]
```

`flatten()` returns a copy of the data.

### 3.4 ravel()

`ravel()` also converts an array into one dimension.

```python
matrix = np.array([
    [1, 2, 3],
    [4, 5, 6]
])

result = matrix.ravel()

print(result)
```

Expected output:

```text
[1 2 3 4 5 6]
```

Difference:

| flatten() | ravel() |
|---|---|
| Always returns a copy | Returns a view when possible |
| Uses additional memory | Can avoid copying |
| Changes do not affect original array | Changes may affect original array |

### 3.5 transpose()

Transpose converts rows into columns and columns into rows.

```python
matrix = np.array([
    [1, 2, 3],
    [4, 5, 6]
])

result = matrix.T

print(result)
```

Expected output:

```text
[[1 4]
 [2 5]
 [3 6]]
```

You can also use:

```python
print(np.transpose(matrix))
```

### 3.6 expand_dims()

Adds a new dimension to an array.

```python
numbers = np.array([10, 20, 30])

row = np.expand_dims(numbers, axis=0)
column = np.expand_dims(numbers, axis=1)

print(row)
print(row.shape)

print(column)
print(column.shape)
```

Expected output:

```text
[[10 20 30]]
(1, 3)

[[10]
 [20]
 [30]]
(3, 1)
```

### 3.7 squeeze()

Removes dimensions whose size is 1.

```python
array = np.array([[
    10, 20, 30
]])

print(array.shape)

result = np.squeeze(array)

print(result)
print(result.shape)
```

Expected output:

```text
(1, 3)

[10 20 30]
(3,)
```

---

## 4. Joining Arrays

Sometimes we need to combine multiple arrays into one array.

### 4.1 concatenate()

Combines arrays along an existing axis.

```python
a = np.array([1, 2, 3])
b = np.array([4, 5, 6])

result = np.concatenate((a, b))

print(result)
```

Expected output:

```text
[1 2 3 4 5 6]
```

Joining two-dimensional arrays:

```python
a = np.array([
    [1, 2],
    [3, 4]
])

b = np.array([
    [5, 6],
    [7, 8]
])

print(np.concatenate((a, b), axis=0))
print()
print(np.concatenate((a, b), axis=1))
```

Expected output:

```text
[[1 2]
 [3 4]
 [5 6]
 [7 8]]

[[1 2 5 6]
 [3 4 7 8]]
```

### 4.2 vstack()

Combines arrays vertically.

```python
a = np.array([1, 2, 3])
b = np.array([4, 5, 6])

result = np.vstack((a, b))

print(result)
```

Expected output:

```text
[[1 2 3]
 [4 5 6]]
```

### 4.3 hstack()

Combines arrays horizontally.

```python
a = np.array([1, 2, 3])
b = np.array([4, 5, 6])

result = np.hstack((a, b))

print(result)
```

Expected output:

```text
[1 2 3 4 5 6]
```

### 4.4 stack()

Combines arrays by creating a new axis.

```python
a = np.array([1, 2, 3])
b = np.array([4, 5, 6])

result = np.stack((a, b), axis=0)

print(result)
print(result.shape)
```

Expected output:

```text
[[1 2 3]
 [4 5 6]]

(2, 3)
```

Difference:

- `concatenate()` joins along an existing axis.
- `stack()` creates a new axis.

---

## 5. Splitting Arrays

Splitting divides an array into smaller arrays.

### 5.1 split()

```python
numbers = np.array([10, 20, 30, 40, 50, 60])

result = np.split(numbers, 3)

for part in result:
    print(part)
```

Expected output:

```text
[10 20]
[30 40]
[50 60]
```

The array must be divisible into the requested number of equal sections.

### 5.2 array_split()

Unlike `split()`, `array_split()` can create sections of unequal sizes.

```python
numbers = np.array([10, 20, 30, 40, 50])

result = np.array_split(numbers, 3)

for part in result:
    print(part)
```

Expected output:

```text
[10 20]
[30 40]
[50]
```

### 5.3 hsplit() and vsplit()

```python
matrix = np.array([
    [1, 2, 3, 4],
    [5, 6, 7, 8]
])

horizontal = np.hsplit(matrix, 2)

for part in horizontal:
    print(part)
```

Expected output:

```text
[[1 2]
 [5 6]]

[[3 4]
 [7 8]]
```

`hsplit()` splits columns, while `vsplit()` splits rows.

---

## 6. Searching and Sorting Arrays

### 6.1 sort()

Sorts array elements in ascending order.

```python
numbers = np.array([50, 10, 40, 20, 30])

result = np.sort(numbers)

print(result)
```

Expected output:

```text
[10 20 30 40 50]
```

The original array remains unchanged when using `np.sort()`.

### 6.2 argsort()

Returns the indices that would sort an array.

```python
numbers = np.array([50, 10, 40, 20])

result = np.argsort(numbers)

print(result)
```

Expected output:

```text
[1 3 2 0]
```

Explanation:

- 10 is at index 1.
- 20 is at index 3.
- 40 is at index 2.
- 50 is at index 0.

### 6.3 unique()

Returns unique values without duplicates.

```python
numbers = np.array([10, 20, 10, 30, 20, 40])

print(np.unique(numbers))
```

Expected output:

```text
[10 20 30 40]
```

We can also count occurrences:

```python
values, counts = np.unique(numbers, return_counts=True)

print(values)
print(counts)
```

Expected output:

```text
[10 20 30 40]
[2 2 1 1]
```

### 6.4 bincount()

Counts occurrences of non-negative integer values.

```python
numbers = np.array([1, 2, 2, 3, 3, 3, 4])

result = np.bincount(numbers)

print(result)
```

Expected output:

```text
[0 1 2 3 1]
```

The first position represents the count of zero, the second represents one, and so on.

### 6.5 partition()

Places the smallest `k` elements before the remaining elements. The result is not necessarily fully sorted.

```python
numbers = np.array([50, 10, 40, 20, 30])

result = np.partition(numbers, 2)

print(result)
```

Expected output:

```text
[10 20 30 50 40]
```

The two smallest elements are before index 2, and the element at index 2 is the third-smallest value.

---

## 7. Conditional Array Operations

### 7.1 where()

Selects values based on a condition.

```python
marks = np.array([35, 80, 45, 90, 25])

result = np.where(marks >= 40, "Pass", "Fail")

print(result)
```

Expected output:

```text
['Fail' 'Pass' 'Pass' 'Pass' 'Fail']
```

Syntax:

```python
np.where(condition, value_if_true, value_if_false)
```

### 7.2 select()

Applies multiple conditions.

```python
marks = np.array([95, 75, 55, 30])

conditions = [
    marks >= 90,
    marks >= 70,
    marks >= 40
]

choices = [
    "A",
    "B",
    "C"
]

result = np.select(conditions, choices, default="Fail")

print(result)
```

Expected output:

```text
['A' 'B' 'C' 'Fail']
```

Conditions are evaluated in order. The first matching condition determines the result.

### 7.3 clip()

Restricts values to a minimum and maximum range.

```python
numbers = np.array([5, 15, 25, 35, 45])

result = np.clip(numbers, 10, 40)

print(result)
```

Expected output:

```text
[10 15 25 35 40]
```

Values below 10 become 10, and values above 40 become 40.

---

## 8. Handling Missing Values

Real-world datasets often contain missing or invalid values.

NumPy represents missing numerical values using `np.nan`.

### 8.1 Creating an array with missing values

```python
data = np.array([10, 20, np.nan, 40, 50])

print(data)
```

Expected output:

```text
[10. 20. nan 40. 50.]
```

### 8.2 isnan()

Checks which values are missing.

```python
print(np.isnan(data))
```

Expected output:

```text
[False False  True False False]
```

### 8.3 nanmean()

Calculates the mean while ignoring NaN values.

```python
print(np.nanmean(data))
```

Expected output:

```text
30.0
```

### 8.4 nanmedian()

Calculates the median while ignoring NaN values.

```python
print(np.nanmedian(data))
```

Expected output:

```text
30.0
```

### 8.5 nan_to_num()

Replaces NaN and infinite values with finite values.

```python
data = np.array([10, np.nan, 30, np.inf, -np.inf])

result = np.nan_to_num(
    data,
    nan=0,
    posinf=100,
    neginf=-100
)

print(result)
```

Expected output:

```text
[  10.    0.   30.  100. -100.]
```

Important:

Do not automatically replace every missing value with zero in a real dataset. Choose a replacement strategy based on what the missing values mean.

---

## 9. Mathematical Functions

NumPy provides many mathematical functions that operate directly on arrays.

### 9.1 Basic mathematical functions

```python
numbers = np.array([1, 4, 9, 16, 25])

print(np.sqrt(numbers))
print(np.square(numbers))
print(np.power(numbers, 2))
```

Expected output:

```text
[1. 2. 3. 4. 5.]
[  1  16  81 256 625]
[  1  16  81 256 625]
```

### 9.2 Absolute values

```python
numbers = np.array([-10, -5, 0, 5, 10])

print(np.abs(numbers))
```

Expected output:

```text
[10  5  0  5 10]
```

### 9.3 Exponential functions

```python
numbers = np.array([1, 2, 3])

print(np.exp(numbers))
```

`np.exp(x)` calculates \(e^x\).

### 9.4 Logarithmic functions

```python
numbers = np.array([1, np.e, np.e ** 2])

print(np.log(numbers))
print(np.log10(np.array([10, 100, 1000])))
```

Expected output:

```text
[0. 1. 2.]
[1. 2. 3.]
```

### 9.5 Trigonometric functions

NumPy provides:

- `np.sin()`
- `np.cos()`
- `np.tan()`

These functions use radians, not degrees.

```python
angles = np.array([0, 30, 45, 60, 90])

radians = np.deg2rad(angles)

print(np.sin(radians))
print(np.cos(radians))
```

### 9.6 Rounding functions

```python
numbers = np.array([1.234, 2.567, 3.891])

print(np.round(numbers, 2))
print(np.floor(numbers))
print(np.ceil(numbers))
```

Expected output:

```text
[1.23 2.57 3.89]
[1. 2. 3.]
[2. 3. 4.]
```

---

## 10. Statistical Operations

Statistics helps us understand and summarize datasets.

Consider student marks:

```python
marks = np.array([75, 80, 65, 90, 85, 70, 95])
```

### 10.1 Mean

Mean is the average value.

```python
print(np.mean(marks))
```

Expected output:

```text
80.0
```

Formula:

Mean = Sum of all values / Number of values

### 10.2 Median

Median is the middle value after sorting the data.

```python
print(np.median(marks))
```

Expected output:

```text
80.0
```

### 10.3 Minimum and Maximum

```python
print(np.min(marks))
print(np.max(marks))
```

Expected output:

```text
65
95
```

### 10.4 Standard Deviation

Standard deviation measures how spread out values are around their mean.

```python
print(np.std(marks))
```

A small standard deviation indicates that values are relatively close to the mean.

### 10.5 Variance

Variance measures the average squared deviation from the mean.

```python
print(np.var(marks))
```

For NumPy's default population calculation:

Variance = Standard Deviation squared.

### 10.6 Percentiles

A percentile tells us the value below which a specified percentage of observations fall.

```python
marks = np.array([10, 20, 30, 40, 50, 60, 70, 80])

print(np.percentile(marks, 25))
print(np.percentile(marks, 50))
print(np.percentile(marks, 75))
```

Expected output:

```text
27.5
45.0
62.5
```

### 10.7 Quantiles

Quantiles divide data into equal-sized groups.

```python
print(np.quantile(marks, [0.25, 0.50, 0.75]))
```

Expected output:

```text
[27.5 45.  62.5]
```

### 10.8 Correlation

Correlation measures the strength and direction of a linear relationship between two variables.

```python
hours = np.array([1, 2, 3, 4, 5])
marks = np.array([40, 50, 60, 70, 80])

result = np.corrcoef(hours, marks)

print(result)
```

Expected output:

```text
[[1. 1.]
 [1. 1.]]
```

Interpretation:

- Close to +1: strong positive linear relationship.
- Close to -1: strong negative linear relationship.
- Close to 0: weak or no linear relationship.

Correlation does not prove causation.

### 10.9 Covariance

Covariance indicates whether two variables tend to increase or decrease together.

```python
hours = np.array([1, 2, 3, 4, 5])
marks = np.array([40, 50, 60, 70, 80])

result = np.cov(hours, marks)

print(result)
```

Expected output:

```text
[[  2.5  25. ]
 [ 25.  250. ]]
```

The default `np.cov()` uses sample covariance (`ddof=1`).

---

## 11. Random Sampling and Distributions

Random numbers are useful in simulations, sampling, testing and machine learning.

### 11.1 Creating a random generator

Use NumPy's modern random generator:

```python
rng = np.random.default_rng(42)

print(rng.integers(1, 10, size=5))
```

Expected output:

```text
[1 7 6 4 4]
```

The seed `42` makes the results reproducible.

### 11.2 Random decimal values

```python
rng = np.random.default_rng(42)

print(rng.random(5))
```

Generates random values between 0 and 1.

### 11.3 Random sampling

```python
rng = np.random.default_rng(42)

numbers = np.array([10, 20, 30, 40, 50])

print(rng.choice(numbers, size=3, replace=False))
```

Selects three different values from the array.

### 11.4 Normal distribution

A normal distribution is a common probability distribution with a bell-shaped curve.

```python
rng = np.random.default_rng(42)

data = rng.normal(
    loc=50,
    scale=10,
    size=1000
)

print(np.mean(data))
print(np.std(data))
```

Parameters:

- `loc`: Mean.
- `scale`: Standard deviation.
- `size`: Number of generated values.

The calculated mean and standard deviation will be approximately 50 and 10, respectively.

### 11.5 Uniform distribution

In a uniform distribution, values are generated over an interval with equal probability density.

```python
rng = np.random.default_rng(42)

data = rng.uniform(
    low=10,
    high=100,
    size=5
)

print(data)
```

---

## 12. Linear Algebra with NumPy

Linear algebra is important in Data Science, machine learning, statistics and scientific computing.

### 12.1 Matrix creation

```python
A = np.array([
    [1, 2],
    [3, 4]
])

B = np.array([
    [5, 6],
    [7, 8]
])

print(A)
print(B)
```

### 12.2 Matrix addition

```python
print(A + B)
```

Expected output:

```text
[[ 6  8]
 [10 12]]
```

### 12.3 Element-wise multiplication

```python
print(A * B)
```

Expected output:

```text
[[ 5 12]
 [21 32]]
```

Each element is multiplied by the element at the same position.

### 12.4 Matrix multiplication

Use `@` or `np.matmul()`.

```python
print(A @ B)
```

Expected output:

```text
[[19 22]
 [43 50]]
```

Important:

- `A * B` performs element-wise multiplication.
- `A @ B` performs matrix multiplication.

### 12.5 Dot product

```python
a = np.array([1, 2, 3])
b = np.array([4, 5, 6])

print(np.dot(a, b))
```

Expected output:

```text
32
```

Calculation:

(1 × 4) + (2 × 5) + (3 × 6) = 32

### 12.6 Determinant

The determinant is a scalar value calculated from a square matrix.

```python
A = np.array([
    [1, 2],
    [3, 4]
])

print(np.linalg.det(A))
```

Expected output:

```text
-2.0
```

### 12.7 Matrix inverse

The inverse of a square matrix is a matrix that produces the identity matrix when multiplied by the original matrix.

```python
A = np.array([
    [1, 2],
    [3, 4]
])

result = np.linalg.inv(A)

print(result)

print(A @ result)
```

The second result should be approximately:

```text
[[1. 0.]
 [0. 1.]]
```

Floating-point calculations may produce very small rounding differences.

Important:

A matrix must be square and non-singular to have an inverse.

If its determinant is zero, it is singular and has no inverse.

### 12.8 Solving linear equations

Consider:

2x + y = 8

x + 3y = 9

We can represent these equations as:

```text
Ax = b
```

Use `np.linalg.solve()`:

```python
A = np.array([
    [2, 1],
    [1, 3]
])

b = np.array([8, 9])

solution = np.linalg.solve(A, b)

print(solution)
```

Expected output:

```text
[3. 2.]
```

Therefore:

```text
x = 3
y = 2
```

This is generally preferable to calculating the inverse manually.

### 12.9 Eigenvalues and eigenvectors

Eigenvalues and eigenvectors describe important properties of a square matrix.

```python
A = np.array([
    [2, 0],
    [0, 3]
])

values, vectors = np.linalg.eig(A)

print("Eigenvalues:")
print(values)

print("Eigenvectors:")
print(vectors)
```

Expected output:

```text
Eigenvalues:
[2. 3.]

Eigenvectors:
[[1. 0.]
 [0. 1.]]
```

Eigenvectors are useful in techniques such as Principal Component Analysis (PCA).

---

## 13. Views and Copies

Understanding views and copies is important for memory management.

### 13.1 View

A view refers to the same underlying data as the original array.

```python
original = np.array([10, 20, 30, 40])

view = original[1:3]

view[0] = 999

print(original)
print(view)
```

Expected output:

```text
[ 10 999  30  40]
[999  30]
```

Changing the view also changed the original array.

### 13.2 Copy

A copy contains independent data.

```python
original = np.array([10, 20, 30, 40])

copied = original.copy()

copied[0] = 999

print(original)
print(copied)
```

Expected output:

```text
[10 20 30 40]
[999  20  30  40]
```

### 13.3 shares_memory()

Checks whether two arrays share memory.

```python
original = np.array([10, 20, 30, 40])

view = original[1:3]
copied = original.copy()

print(np.shares_memory(original, view))
print(np.shares_memory(original, copied))
```

Expected output:

```text
True
False
```

---

## 14. Mini-Project: Sales Data Analyzer

### Project Description

Build a small Sales Data Analyzer using NumPy.

The program will:

1. Store sales data for multiple products.
2. Calculate total sales for each product.
3. Calculate average daily sales.
4. Find the highest and lowest sales.
5. Handle missing values.
6. Sort products based on total sales.
7. Calculate overall sales statistics.
8. Compare sales across different days.

### Complete Program

```python
import numpy as np

# Product names
products = np.array([
    "Laptop",
    "Mobile",
    "Tablet",
    "Headphones",
    "Keyboard"
])

# Sales data for 5 products over 4 days
sales = np.array([
    [50000, 55000, 60000, 52000],
    [20000, 25000, 23000, 28000],
    [15000, 18000, 17000, 16000],
    [3000, 3500, np.nan, 4000],
    [2000, 2500, 2200, 2800]
])

print("========== SALES DATA ==========")

print(sales)

# Replace missing sales with the column mean
daily_means = np.nanmean(sales, axis=0)

missing_rows, missing_cols = np.where(np.isnan(sales))

sales_clean = sales.copy()

sales_clean[missing_rows, missing_cols] = daily_means[missing_cols]

print("\n========== CLEANED DATA ==========")

print(sales_clean)

# Total sales for each product
product_totals = np.sum(sales_clean, axis=1)

print("\n========== PRODUCT TOTALS ==========")

for product, total in zip(products, product_totals):
    print(product, ":", total)

# Average daily sales for each product
product_averages = np.mean(sales_clean, axis=1)

print("\n========== PRODUCT AVERAGES ==========")

for product, average in zip(products, product_averages):
    print(product, ":", round(average, 2))

# Highest and lowest product sales
highest_index = np.argmax(product_totals)
lowest_index = np.argmin(product_totals)

print("\nHighest Selling Product:", products[highest_index])
print("Lowest Selling Product:", products[lowest_index])

# Sort products by total sales
sorted_indices = np.argsort(product_totals)[::-1]

print("\n========== SALES RANKING ==========")

for index in sorted_indices:
    print(products[index], ":", product_totals[index])

# Daily total sales
daily_totals = np.sum(sales_clean, axis=0)

print("\n========== DAILY TOTALS ==========")

for day, total in enumerate(daily_totals, start=1):
    print("Day", day, ":", total)

# Overall statistics
print("\n========== OVERALL STATISTICS ==========")

print("Total Revenue:", np.sum(sales_clean))
print("Average Sale:", round(np.mean(sales_clean), 2))
print("Highest Sale:", np.max(sales_clean))
print("Lowest Sale:", np.min(sales_clean))
print("Standard Deviation:", round(np.std(sales_clean), 2))

# Product sales distribution
print("\n========== SALES DISTRIBUTION ==========")

print("25th Percentile:", np.percentile(sales_clean, 25))
print("50th Percentile:", np.percentile(sales_clean, 50))
print("75th Percentile:", np.percentile(sales_clean, 75))
```

### Understanding the Project

Important operations used:

| Operation | Purpose |
|---|---|
| `np.nanmean()` | Calculate averages while ignoring missing values |
| `np.isnan()` | Detect missing values |
| `np.where()` | Find missing-value positions |
| `np.sum()` | Calculate total sales |
| `np.mean()` | Calculate average sales |
| `np.argmax()` | Find the index of the highest value |
| `np.argmin()` | Find the index of the lowest value |
| `np.argsort()` | Get sorted indices |
| `np.percentile()` | Calculate sales percentiles |
| `np.std()` | Measure sales variation |

The project uses a simple column-mean strategy to fill missing sales. In a real business dataset, the correct strategy should depend on why the data is missing.

---

## 15. Student Practice Exercises

### Exercise 1: Array Reshaping

Create an array containing numbers from 1 to 20.

Tasks:

1. Reshape it into 4 rows and 5 columns.
2. Convert it into a one-dimensional array.
3. Find its transpose.
4. Print its shape and dimensions.

### Exercise 2: Joining and Splitting

Create two arrays:

```python
a = np.array([10, 20, 30])
b = np.array([40, 50, 60])
```

Tasks:

1. Join both arrays using `concatenate()`.
2. Combine them using `stack()`.
3. Split the combined array into three sections.
4. Print every result.

### Exercise 3: Sorting and Searching

Given:

```python
marks = np.array([45, 90, 67, 90, 34, 78, 56])
```

Tasks:

1. Sort the marks.
2. Find unique marks.
3. Count occurrences of each mark.
4. Find the indices that sort the array.
5. Find the highest and lowest marks.

### Exercise 4: Missing Values

Given:

```python
data = np.array([10, 20, np.nan, 40, np.nan, 60])
```

Tasks:

1. Find missing values.
2. Count missing values.
3. Calculate the mean without missing values.
4. Replace missing values with the mean.
5. Print the cleaned array.

### Exercise 5: Statistical Analysis

Given:

```python
marks = np.array([55, 60, 70, 75, 80, 85, 90, 95])
```

Tasks:

1. Calculate mean.
2. Calculate median.
3. Calculate standard deviation.
4. Calculate variance.
5. Calculate the 25th and 75th percentiles.

### Exercise 6: Linear Algebra

Create two 2 × 2 matrices.

Tasks:

1. Add both matrices.
2. Multiply them element-wise.
3. Perform matrix multiplication.
4. Find the determinant of the first matrix.
5. Calculate its inverse if possible.

### Exercise 7: Random Data

Tasks:

1. Generate 100 random integers between 1 and 100.
2. Calculate their mean.
3. Find the maximum and minimum.
4. Generate 100 values from a normal distribution.
5. Repeat the experiment with the same seed and verify reproducibility.

---

## 16. Trainer Assessment

Ask the student the following questions:

1. What is the difference between `flatten()` and `ravel()`?
2. What is the difference between `concatenate()` and `stack()`?
3. What is the purpose of `axis=0` and `axis=1`?
4. What does `np.where()` do?
5. Why do we use `np.nanmean()` instead of `np.mean()` when data contains NaN?
6. What is the difference between mean and median?
7. What does standard deviation tell us?
8. What is the purpose of a random seed?
9. What is the difference between `*` and `@` in NumPy?
10. What is a matrix inverse?
11. What is the difference between a view and a copy?
12. Why is NumPy useful for Data Science?

### Practical Assessment

Ask the student to create a Student Marks Analyzer that:

- Stores marks of at least 10 students.
- Calculates mean and median marks.
- Finds the highest and lowest marks.
- Counts passed and failed students.
- Sorts student marks.
- Calculates standard deviation.
- Handles at least one missing value.

The student should write the complete program independently.

---

## 17. Completion Criteria

The student should be able to:

- Manipulate arrays using advanced NumPy functions.
- Join and split arrays.
- Sort, search and filter array values.
- Handle missing numerical data.
- Apply mathematical functions to arrays.
- Calculate statistical measurements.
- Generate reproducible random data.
- Perform basic matrix operations.
- Solve simple systems of linear equations.
- Understand the difference between views and copies.
- Complete the Sales Data Analyzer project independently.

---

## 18. Next Day Preview

**Day 48 – Pandas Fundamentals**

Topics:

- Introduction to Pandas
- Series and DataFrames
- Creating DataFrames
- Reading CSV files
- Inspecting datasets
- Selecting rows and columns
- Filtering data
- Handling missing values
- Basic data analysis

Pandas is one of the most important Python libraries for real-world Data Science because it makes working with structured datasets much easier.

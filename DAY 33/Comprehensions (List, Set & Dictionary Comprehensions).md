
# Day 33 – Python Comprehensions

## 1. Introduction to Comprehensions

Comprehensions are a concise way to create new collections from existing iterables.

Python supports three main types:

1. List Comprehension
2. Set Comprehension
3. Dictionary Comprehension

Comprehensions can perform operations such as:

- Creating new collections.
- Filtering elements.
- Transforming data.
- Applying conditions.
- Working with nested collections.

### Why Use Comprehensions?

Without comprehensions, we often use loops to create collections.

Example:

```python
numbers = [1, 2, 3, 4, 5]

squares = []

for number in numbers:
    squares.append(number ** 2)

print(squares)
```

**Output:**
```text
[1, 4, 9, 16, 25]
```

The same operation can be performed using a list comprehension.

```python
numbers = [1, 2, 3, 4, 5]

squares = [number ** 2 for number in numbers]

print(squares)
```

**Output:**
```text
[1, 4, 9, 16, 25]
```

Both approaches produce the same result.

---

# PART 1 – LIST COMPREHENSION

## 2. What is List Comprehension?

List comprehension is a concise way to create a new list from an existing iterable.

### Syntax

```python
new_list = [expression for item in iterable]
```

Where:

- `expression`: Operation performed on each item.
- `item`: Current element.
- `iterable`: Collection or sequence being processed.

### Example

```python
numbers = [1, 2, 3, 4, 5]

doubled = [number * 2 for number in numbers]

print(doubled)
```

**Output:**
```text
[2, 4, 6, 8, 10]
```

### Explanation

1. Python takes an element from `numbers`.
2. Stores it temporarily in `number`.
3. Multiplies it by 2.
4. Adds the result to the new list.
5. Repeats for every element.

---

## 3. List Comprehension with Strings

Comprehensions can also work with strings.

### Example: Convert Names to Uppercase

```python
names = ["raj", "aman", "rahul"]

uppercase_names = [name.upper() for name in names]

print(uppercase_names)
```

**Output:**
```text
['RAJ', 'AMAN', 'RAHUL']
```

### Example: Extract Characters

```python
word = "Python"

characters = [character for character in word]

print(characters)
```

**Output:**
```text
['P', 'y', 't', 'h', 'o', 'n']
```

---

## 4. List Comprehension with Conditions

We can use `if` to filter elements.

### Syntax

```python
new_list = [expression for item in iterable if condition]
```

### Example: Even Numbers

```python
numbers = [1, 2, 3, 4, 5, 6, 7, 8]

even_numbers = [
    number for number in numbers
    if number % 2 == 0
]

print(even_numbers)
```

**Output:**
```text
[2, 4, 6, 8]
```

Only numbers satisfying the condition are added to the new list.

### Example: Odd Numbers

```python
numbers = [1, 2, 3, 4, 5, 6, 7, 8]

odd_numbers = [
    number for number in numbers
    if number % 2 != 0
]

print(odd_numbers)
```

**Output:**
```text
[1, 3, 5, 7]
```

---

## 5. List Comprehension with if-else

We can also use conditional expressions to choose which value should be added.

### Syntax

```python
new_list = [
    value_if_true if condition else value_if_false
    for item in iterable
]
```

### Example: Even or Odd Labels

```python
numbers = [1, 2, 3, 4, 5, 6]

results = [
    "Even" if number % 2 == 0 else "Odd"
    for number in numbers
]

print(results)
```

**Output:**
```text
['Odd', 'Even', 'Odd', 'Even', 'Odd', 'Even']
```

### Important Difference

**Filtering with `if`:**

```python
evens = [number for number in numbers if number % 2 == 0]
```

This removes elements that do not satisfy the condition.

**Transforming with if-else:**

```python
labels = [
    "Even" if number % 2 == 0 else "Odd"
    for number in numbers
]
```

This includes every element but changes the output depending on the condition.

---

## 6. Multiple Conditions in List Comprehension

We can use multiple conditions.

### Example: Numbers Divisible by 2 and 3

```python
numbers = range(1, 31)

results = [
    number for number in numbers
    if number % 2 == 0 and number % 3 == 0
]

print(results)
```

**Output:**
```text
[6, 12, 18, 24, 30]
```

### Example: Filter Names

```python
names = ["Raj", "Aman", "Rahul", "Ravi", "Priya"]

results = [
    name for name in names
    if len(name) > 4 and name.startswith("R")
]

print(results)
```

**Output:**
```text
['Rahul']
```

---

## 7. Nested List Comprehension

A nested comprehension can contain more than one `for` clause.

### Example: Create Coordinate Pairs

```python
coordinates = [
    (x, y)
    for x in range(1, 3)
    for y in range(1, 4)
]

print(coordinates)
```

**Output:**
```text
[(1, 1), (1, 2), (1, 3), (2, 1), (2, 2), (2, 3)]
```

### Explanation

This comprehension works similarly to nested loops.

Equivalent normal code:

```python
coordinates = []

for x in range(1, 3):
    for y in range(1, 4):
        coordinates.append((x, y))

print(coordinates)
```

The first `for` loop runs outside the second loop.

---

## 8. Flattening a Nested List

Flattening means converting a nested list into a single-level list.

### Example

```python
matrix = [
    [1, 2, 3],
    [4, 5, 6],
    [7, 8, 9]
]

flattened = [
    number
    for row in matrix
    for number in row
]

print(flattened)
```

**Output:**
```text
[1, 2, 3, 4, 5, 6, 7, 8, 9]
```

### Equivalent Normal Loop

```python
flattened = []

for row in matrix:
    for number in row:
        flattened.append(number)
```

---

## 9. List Comprehension with Functions

We can call functions inside comprehensions.

### Example

```python
def square(number):
    return number ** 2


numbers = [1, 2, 3, 4, 5]

results = [square(number) for number in numbers]

print(results)
```

**Output:**
```text
[1, 4, 9, 16, 25]
```

### Example: Clean User Names

```python
names = [" raj ", " aman ", " rahul "]

clean_names = [
    name.strip().title()
    for name in names
]

print(clean_names)
```

**Output:**
```text
['Raj', 'Aman', 'Rahul']
```

---

## 10. List Comprehension with Dictionaries

We can extract values from dictionaries using comprehensions.

### Example: Extract Student Names

```python
students = {
    101: "Raj",
    102: "Aman",
    103: "Rahul"
}

names = [name for name in students.values()]

print(names)
```

**Output:**
```text
['Raj', 'Aman', 'Rahul']
```

### Example: Extract Passing Students

```python
students = {
    "Raj": 85,
    "Aman": 35,
    "Rahul": 90,
    "Priya": 45
}

passed = [
    name for name, marks in students.items()
    if marks >= 40
]

print(passed)
```

**Output:**
```text
['Raj', 'Rahul', 'Priya']
```

---

# PART 2 – SET COMPREHENSION

## 11. What is Set Comprehension?

Set comprehension creates a set using a concise syntax.

It is similar to list comprehension, but uses curly braces.

### Syntax

```python
new_set = {expression for item in iterable}
```

### Example

```python
numbers = [1, 2, 2, 3, 3, 4, 5]

unique_numbers = {number for number in numbers}

print(unique_numbers)
```

**Output:**

```text
{1, 2, 3, 4, 5}
```

The order may vary because sets are unordered collections.

Duplicate values are automatically removed.

---

## 12. Set Comprehension with Conditions

### Example: Unique Even Numbers

```python
numbers = [1, 2, 2, 3, 4, 4, 5, 6]

even_numbers = {
    number for number in numbers
    if number % 2 == 0
}

print(even_numbers)
```

**Output:**
```text
{2, 4, 6}
```

### Example: Unique First Characters

```python
names = ["Raj", "Rahul", "Aman", "Amit", "Priya"]

first_letters = {
    name[0] for name in names
}

print(first_letters)
```

**Output:**

```text
{'R', 'A', 'P'}
```

The order may vary.

---

## 13. Set Comprehension with Transformations

### Example: Squares of Numbers

```python
numbers = [1, 2, 3, 4, 5]

squares = {
    number ** 2 for number in numbers
}

print(squares)
```

**Output:**
```text
{1, 4, 9, 16, 25}
```

### Example: Unique Word Lengths

```python
words = ["apple", "banana", "cat", "dog", "mango"]

lengths = {
    len(word) for word in words
}

print(lengths)
```

**Output:**
```text
{3, 5, 6}
```

---

# PART 3 – DICTIONARY COMPREHENSION

## 14. What is Dictionary Comprehension?

Dictionary comprehension creates a dictionary using a concise syntax.

### Syntax

```python
new_dict = {
    key_expression: value_expression
    for item in iterable
}
```

### Example

```python
numbers = [1, 2, 3, 4, 5]

squares = {
    number: number ** 2
    for number in numbers
}

print(squares)
```

**Output:**
```text
{1: 1, 2: 4, 3: 9, 4: 16, 5: 25}
```

Each number becomes a key, and its square becomes the corresponding value.

---

## 15. Dictionary Comprehension with Conditions

### Example: Even Number Squares

```python
numbers = range(1, 11)

even_squares = {
    number: number ** 2
    for number in numbers
    if number % 2 == 0
}

print(even_squares)
```

**Output:**
```text
{2: 4, 4: 16, 6: 36, 8: 64, 10: 100}
```

### Example: Filter Passing Students

```python
students = {
    "Raj": 85,
    "Aman": 35,
    "Rahul": 90,
    "Priya": 45
}

passed_students = {
    name: marks
    for name, marks in students.items()
    if marks >= 40
}

print(passed_students)
```

**Output:**
```text
{'Raj': 85, 'Rahul': 90, 'Priya': 45}
```

---

## 16. Dictionary Comprehension with Transformations

### Example: Convert Names to Uppercase

```python
students = {
    "raj": 85,
    "aman": 75,
    "rahul": 90
}

updated = {
    name.upper(): marks
    for name, marks in students.items()
}

print(updated)
```

**Output:**
```text
{'RAJ': 85, 'AMAN': 75, 'RAHUL': 90}
```

### Example: Swap Keys and Values

```python
data = {
    "a": 1,
    "b": 2,
    "c": 3
}

swapped = {
    value: key
    for key, value in data.items()
}

print(swapped)
```

**Output:**
```text
{1: 'a', 2: 'b', 3: 'c'}
```

**Important:** This works as expected when values are unique and hashable. If multiple original keys have the same value, later entries overwrite earlier entries.

---

## 17. Dictionary Comprehension Using zip()

The `zip()` function combines corresponding elements from multiple iterables.

### Example

```python
names = ["Raj", "Aman", "Rahul"]

marks = [85, 75, 90]

students = {
    name: mark
    for name, mark in zip(names, marks)
}

print(students)
```

**Output:**
```text
{'Raj': 85, 'Aman': 75, 'Rahul': 90}
```

`zip()` stops when the shortest iterable is exhausted.

---

## 18. Dictionary Comprehension with Nested Data

### Example: Student Result Categories

```python
students = {
    "Raj": 85,
    "Aman": 35,
    "Rahul": 90,
    "Priya": 45
}

results = {
    name: "Pass" if marks >= 40 else "Fail"
    for name, marks in students.items()
}

print(results)
```

**Output:**
```python
{
    'Raj': 'Pass',
    'Aman': 'Fail',
    'Rahul': 'Pass',
    'Priya': 'Pass'
}
```

---

# PART 4 – ADVANCED COMPREHENSIONS

## 19. Nested Comprehensions for Matrices

### Example: Create a Matrix

```python
matrix = [
    [row * column for column in range(1, 4)]
    for row in range(1, 4)
]

for row in matrix:
    print(row)
```

**Output:**
```text
[1, 2, 3]
[2, 4, 6]
[3, 6, 9]
```

### Explanation

The outer comprehension creates rows.

The inner comprehension creates the values inside each row.

---

## 20. Dictionary of Lists Using Comprehension

```python
students = ["Raj", "Aman", "Rahul"]

student_records = {
    name: [0, 0, 0]
    for name in students
}

print(student_records)
```

**Output:**
```text
{
    'Raj': [0, 0, 0],
    'Aman': [0, 0, 0],
    'Rahul': [0, 0, 0]
}
```

Each student receives a separate list.

This is important because each dictionary value is created independently.

---

## 21. Nested Dictionary Comprehension

### Example

```python
students = ["Raj", "Aman"]

subjects = ["Python", "SQL", "HTML"]

records = {
    student: {
        subject: 0
        for subject in subjects
    }
    for student in students
}

print(records)
```

**Output:**
```python
{
    'Raj': {'Python': 0, 'SQL': 0, 'HTML': 0},
    'Aman': {'Python': 0, 'SQL': 0, 'HTML': 0}
}
```

This creates a nested dictionary for every student.

---

## 22. Generator Expressions vs Comprehensions

Generator expressions look similar to comprehensions but produce values lazily.

### List Comprehension

```python
squares = [number ** 2 for number in range(1, 6)]

print(squares)
```

**Output:**
```text
[1, 4, 9, 16, 25]
```

### Generator Expression

```python
squares = (number ** 2 for number in range(1, 6))

for square in squares:
    print(square)
```

**Output:**
```text
1
4
9
16
25
```

### Comparison

| Type | Syntax | Result |
|---|---|---|
| List comprehension | `[]` | List |
| Set comprehension | `{}` | Set |
| Dictionary comprehension | `{key: value}` | Dictionary |
| Generator expression | `()` | Generator |

Choose the collection type according to the required result.

---

## 23. Choosing the Right Comprehension

| Requirement | Recommended Approach |
|---|---|
| Store ordered values | List comprehension |
| Store unique values | Set comprehension |
| Store key-value pairs | Dictionary comprehension |
| Generate values on demand | Generator expression |
| Complex multi-step logic | Normal loop or helper function |

**Best Practice:** Comprehensions should improve readability. If a comprehension becomes too complicated, use a normal loop or separate function.

---

# PART 5 – PRACTICAL PROGRAMS

## 24. Program 1: Number Analysis

Create a program that generates:

- Squares of all numbers.
- Even numbers.
- Odd numbers.
- Cubes of numbers divisible by 3.

```python
numbers = list(range(1, 11))

squares = [n ** 2 for n in numbers]

even = [n for n in numbers if n % 2 == 0]

odd = [n for n in numbers if n % 2 != 0]

cubes = [n ** 3 for n in numbers if n % 3 == 0]

print("Squares:", squares)
print("Even:", even)
print("Odd:", odd)
print("Cubes divisible by 3:", cubes)
```

**Output:**
```text
Squares: [1, 4, 9, 16, 25, 36, 49, 64, 81, 100]
Even: [2, 4, 6, 8, 10]
Odd: [1, 3, 5, 7, 9]
Cubes divisible by 3: [27, 216, 729]
```

---

## 25. Program 2: Student Result Analyzer

```python
students = {
    "Raj": 85,
    "Aman": 35,
    "Rahul": 90,
    "Priya": 45,
    "Neha": 30
}

passed = {
    name: marks
    for name, marks in students.items()
    if marks >= 40
}

failed = {
    name: marks
    for name, marks in students.items()
    if marks < 40
}

grades = {
    name: "A" if marks >= 80
    else "B" if marks >= 60
    else "C" if marks >= 40
    else "Fail"
    for name, marks in students.items()
}

print("Passed:", passed)
print("Failed:", failed)
print("Grades:", grades)
```

**Output:**
```python
Passed: {'Raj': 85, 'Rahul': 90, 'Priya': 45}
Failed: {'Aman': 35, 'Neha': 30}
Grades: {'Raj': 'A', 'Aman': 'Fail', 'Rahul': 'A', 'Priya': 'C', 'Neha': 'Fail'}
```

---

## 26. Program 3: Remove Duplicate Values

```python
numbers = [10, 20, 10, 30, 20, 40, 50]

unique_numbers = list({
    number for number in numbers
})

print(unique_numbers)
```

**Output:**

```text
[10, 20, 30, 40, 50]
```

The order may vary because sets are unordered.

### Preserve Original Order

```python
numbers = [10, 20, 10, 30, 20, 40, 50]

unique_numbers = list(dict.fromkeys(numbers))

print(unique_numbers)
```

**Output:**
```text
[10, 20, 30, 40, 50]
```

---

## 27. Program 4: Word Length Analyzer

```python
words = ["Python", "Java", "HTML", "CSS", "JavaScript"]

word_lengths = {
    word: len(word)
    for word in words
}

print(word_lengths)
```

**Output:**
```text
{
    'Python': 6,
    'Java': 4,
    'HTML': 4,
    'CSS': 3,
    'JavaScript': 10
}
```

---

## 28. Program 5: Matrix Flattening and Filtering

```python
matrix = [
    [1, 2, 3],
    [4, 5, 6],
    [7, 8, 9]
]

flattened = [
    number
    for row in matrix
    for number in row
]

even_numbers = [
    number
    for number in flattened
    if number % 2 == 0
]

print("Flattened:", flattened)
print("Even Numbers:", even_numbers)
```

**Output:**
```text
Flattened: [1, 2, 3, 4, 5, 6, 7, 8, 9]
Even Numbers: [2, 4, 6, 8]
```

---

# PART 6 – MINI PROJECT

## 29. Mini Project: Student Data Transformation System

### Project Description

Create a system that processes student records using list, set and dictionary comprehensions.

The system should accept student information and generate different reports.

### Sample Data

```python
students = [
    {"name": "Raj", "marks": 85, "city": "Mumbai"},
    {"name": "Aman", "marks": 35, "city": "Pune"},
    {"name": "Rahul", "marks": 90, "city": "Mumbai"},
    {"name": "Priya", "marks": 75, "city": "Delhi"},
    {"name": "Neha", "marks": 30, "city": "Pune"},
    {"name": "Ravi", "marks": 85, "city": "Mumbai"}
]
```

### Project Requirements

#### A. Student Names

Create a list comprehension that extracts all student names.

#### B. Passing Students

Create a list containing students with marks greater than or equal to 40.

#### C. Failed Students

Create a list containing students with marks below 40.

#### D. Unique Cities

Use set comprehension to find all unique cities.

#### E. Student Marks Dictionary

Create a dictionary using student names as keys and marks as values.

#### F. Grade Generator

Create a dictionary that assigns grades:

- A: 80 or above
- B: 60–79
- C: 40–59
- Fail: Below 40

#### G. Top Students

Create a list containing students with marks greater than or equal to 80.

#### H. Average Marks

Calculate the average marks of all students.

#### I. City-Wise Student Names

Create a nested dictionary in which each city is a key and its value contains a list of student names from that city.

#### J. Final Report

Display:

1. All student names.
2. Passing students.
3. Failed students.
4. Unique cities.
5. Student marks.
6. Grades.
7. Top students.
8. Average marks.
9. City-wise student names.

### Sample Expected Output

```text
===== STUDENT DATA TRANSFORMATION SYSTEM =====

All Students:
['Raj', 'Aman', 'Rahul', 'Priya', 'Neha', 'Ravi']

Passing Students:
['Raj', 'Rahul', 'Priya', 'Ravi']

Failed Students:
['Aman', 'Neha']

Unique Cities:
{'Mumbai', 'Pune', 'Delhi'}

Student Marks:
{
    'Raj': 85,
    'Aman': 35,
    'Rahul': 90,
    'Priya': 75,
    'Neha': 30,
    'Ravi': 85
}

Grades:
{
    'Raj': 'A',
    'Aman': 'Fail',
    'Rahul': 'A',
    'Priya': 'B',
    'Neha': 'Fail',
    'Ravi': 'A'
}

Top Students:
['Raj', 'Rahul', 'Ravi']

Average Marks: 66.67

City-wise Students:
{
    'Mumbai': ['Raj', 'Rahul', 'Ravi'],
    'Pune': ['Aman', 'Neha'],
    'Delhi': ['Priya']
}
```

### Project Challenge

After completing the basic project, add:

1. Sort students by marks using `sorted()`.
2. Create a dictionary of students ranked by position.
3. Find the highest and lowest marks.
4. Count the number of students in each grade.
5. Create a list of students whose names start with a particular letter.
6. Generate a separate report for each city.
7. Use generator expressions for large datasets.

---

# PART 7 – STUDENT PRACTICE

## 30. Practice Questions

### Basic Level

1. What is a comprehension in Python?
2. What is list comprehension?
3. Write the syntax of list comprehension.
4. What is set comprehension?
5. What is dictionary comprehension?
6. What is the difference between list and set comprehensions?
7. How do you filter elements using a comprehension?
8. How do you apply if-else inside a comprehension?
9. What is a nested comprehension?
10. What is the difference between comprehension and a normal loop?

### Intermediate Level

11. Create a list of squares from 1 to 20.

12. Create a list of even numbers between 1 and 100.

13. Create a list of words containing more than five characters.

14. Create a list of uppercase names from an existing list.

15. Create a set of unique word lengths.

16. Create a dictionary containing numbers and their cubes.

17. Create a dictionary of students who scored more than 60.

18. Convert two lists into a dictionary using `zip()` and dictionary comprehension.

19. Flatten a nested list using list comprehension.

20. Create a matrix using nested list comprehension.

### Advanced Level

21. Create a dictionary of students and their grades using nested conditional expressions.

22. Create a nested dictionary containing student names and subject marks.

23. Group student names by their cities.

24. Create a dictionary that counts the frequency of each character in a string.

25. Create a list of prime numbers between 1 and 100 using a comprehension.

26. Generate all possible pairs from two separate lists.

27. Create a set of common elements from two lists using set comprehension.

28. Convert a list of dictionaries into a dictionary using student IDs as keys.

29. Create a matrix containing only even values using nested comprehensions.

30. Explain when a normal loop is more readable than a comprehension.

---

# PART 8 – TRAINER ASSESSMENT

## 31. Practical Assessment

| Task | Marks |
|---|---:|
| Create basic list comprehensions | 10 |
| Use conditions in list comprehensions | 10 |
| Implement nested list comprehensions | 10 |
| Create set comprehensions | 10 |
| Create dictionary comprehensions | 15 |
| Transform and filter dictionary data | 10 |
| Implement nested comprehensions | 10 |
| Compare comprehensions and generators | 5 |
| Complete Student Data Transformation System | 20 |
| **Total** | **100** |

### Oral Questions

1. What is list comprehension?
2. What is the difference between list comprehension and a normal loop?
3. How do conditions work inside a comprehension?
4. What is the difference between filtering and transforming?
5. What is set comprehension?
6. Why does set comprehension remove duplicates?
7. What is dictionary comprehension?
8. How can `zip()` be used with dictionary comprehension?
9. What is nested list comprehension?
10. When should you avoid complex comprehensions?

---

## 32. Completion Criteria

The student should be able to:

- Explain comprehensions.
- Create list comprehensions.
- Apply filtering conditions.
- Use if-else expressions.
- Create nested list comprehensions.
- Flatten nested collections.
- Create set comprehensions.
- Remove duplicate values.
- Create dictionary comprehensions.
- Transform and filter dictionaries.
- Use `zip()` with comprehensions.
- Create nested dictionaries.
- Understand generator expressions.
- Choose the appropriate comprehension type.
- Complete the Student Data Transformation System.

**Day 33 Completed – Python Comprehensions**

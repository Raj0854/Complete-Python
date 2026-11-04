
# Day 22 – Lambda, Map, Filter & Reduce

## 1. Introduction

In previous lessons, we learned how to create functions using `def`.

Python also provides a shorter way to create small functions using the `lambda` keyword.

We will also learn three useful built-in functional programming tools:

1. `lambda` – Creates small anonymous functions.
2. `map()` – Applies a function to every item in an iterable.
3. `filter()` – Selects items based on a condition.
4. `reduce()` – Combines items into a single result.

These concepts are commonly used when processing lists, tuples, dictionaries and other collections.

---

# Part 1 – Lambda Functions

## 2. What Is a Lambda Function?

A lambda function is a small anonymous function created using the `lambda` keyword.

Unlike normal functions, lambda functions do not require a function name or a `def` statement.

### Normal Function

```python
def square(number):
    return number * number

print(square(5))
```

**Output:**
```text
25
```

### Equivalent Lambda Function

```python
square = lambda number: number * number

print(square(5))
```

**Output:**
```text
25
```

Both programs perform the same operation.

### Lambda Syntax

```python
lambda arguments: expression
```

Explanation:

- `lambda` – Keyword used to create the function.
- `arguments` – Input parameters.
- `expression` – Single expression whose result is returned automatically.

**Important:** A lambda function can contain only one expression. It cannot contain multiple statements such as assignments, loops or a normal `return` statement.

---

## 3. Lambda with One Argument

```python
greet = lambda name: "Hello " + name

print(greet("Raj"))
```

**Output:**
```text
Hello Raj
```

Another example:

```python
cube = lambda number: number ** 3

print(cube(3))
print(cube(4))
```

**Output:**
```text
27
64
```

---

## 4. Lambda with Multiple Arguments

A lambda function can accept multiple parameters.

### Example 1: Addition

```python
add = lambda a, b: a + b

print(add(10, 20))
```

**Output:**
```text
30
```

### Example 2: Multiplication

```python
multiply = lambda a, b: a * b

print(multiply(5, 6))
```

**Output:**
```text
30
```

### Example 3: Three Arguments

```python
calculate_total = lambda a, b, c: a + b + c

print(calculate_total(10, 20, 30))
```

**Output:**
```text
60
```

---

## 5. Lambda with Conditional Expressions

Lambda functions can use conditional expressions.

### Example 1: Even or Odd

```python
check_number = lambda number: "Even" if number % 2 == 0 else "Odd"

print(check_number(10))
print(check_number(7))
```

**Output:**
```text
Even
Odd
```

### Example 2: Find the Greater Number

```python
greater = lambda a, b: a if a > b else b

print(greater(10, 20))
```

**Output:**
```text
20
```

### Example 3: Check Voting Eligibility

```python
check_age = lambda age: "Eligible" if age >= 18 else "Not Eligible"

print(check_age(21))
print(check_age(16))
```

**Output:**
```text
Eligible
Not Eligible
```

---

## 6. Lambda with Built-in Functions

Lambda functions are especially useful with functions such as `sorted()`, `max()` and `min()`.

### Example 1: Sorting Numbers

```python
numbers = [50, 10, 40, 20, 30]

result = sorted(numbers, key=lambda number: number)

print(result)
```

**Output:**
```text
[10, 20, 30, 40, 50]
```

### Example 2: Sorting by Last Digit

```python
numbers = [25, 12, 43, 31, 18]

result = sorted(numbers, key=lambda number: number % 10)

print(result)
```

**Output:**
```text
[31, 12, 43, 25, 18]
```

Explanation:

`key=lambda number: number % 10` tells Python to sort numbers according to their last digit.

### Example 3: Sorting Student Records

```python
students = [
    {"name": "Raj", "marks": 85},
    {"name": "Altaf", "marks": 92},
    {"name": "Aman", "marks": 78}
]

result = sorted(students, key=lambda student: student["marks"])

for student in result:
    print(student)
```

**Output:**
```text
{'name': 'Aman', 'marks': 78}
{'name': 'Raj', 'marks': 85}
{'name': 'Altaf', 'marks': 92}
```

### Example 4: Find the Highest Scoring Student

```python
students = [
    {"name": "Raj", "marks": 85},
    {"name": "Altaf", "marks": 92},
    {"name": "Aman", "marks": 78}
]

top_student = max(students, key=lambda student: student["marks"])

print(top_student)
```

**Output:**
```text
{'name': 'Altaf', 'marks': 92}
```

---

# Part 2 – map()

## 7. What Is map()?

The `map()` function applies a given function to every item in an iterable.

An iterable can be:
- List
- Tuple
- String
- Set
- Other iterable objects

### Syntax

```python
map(function, iterable)
```

It returns a map iterator. To see all results immediately, we commonly convert it into a list or another collection.

### Example 1: Square Every Number

```python
numbers = [1, 2, 3, 4, 5]

result = map(lambda number: number ** 2, numbers)

print(list(result))
```

**Output:**
```text
[1, 4, 9, 16, 25]
```

Explanation:

- `numbers` contains five values.
- `lambda number: number ** 2` calculates the square.
- `map()` applies the lambda function to every value.
- `list()` converts the map iterator into a list.

### Example 2: Convert Strings to Uppercase

```python
names = ["raj", "altaf", "aman"]

result = map(lambda name: name.upper(), names)

print(list(result))
```

**Output:**
```text
['RAJ', 'ALTAF', 'AMAN']
```

### Example 3: Add 10 to Every Number

```python
numbers = [10, 20, 30, 40]

result = map(lambda number: number + 10, numbers)

print(list(result))
```

**Output:**
```text
[20, 30, 40, 50]
```

---

## 8. map() with a Normal Function

`map()` does not require a lambda function. We can also pass a normal function.

```python
def calculate_square(number):
    return number ** 2

numbers = [2, 4, 6, 8]

result = map(calculate_square, numbers)

print(list(result))
```

**Output:**
```text
[4, 16, 36, 64]
```

The function is passed without parentheses:

```python
map(calculate_square, numbers)
```

Do not write:

```python
map(calculate_square(), numbers)
```

The second version calls the function immediately instead of passing the function object to `map()`.

---

## 9. map() with Multiple Iterables

`map()` can receive more than one iterable.

The function must accept the corresponding number of arguments.

### Example: Add Two Lists

```python
numbers1 = [10, 20, 30]
numbers2 = [1, 2, 3]

result = map(lambda a, b: a + b, numbers1, numbers2)

print(list(result))
```

**Output:**
```text
[11, 22, 33]
```

### Example: Multiply Two Lists

```python
prices = [100, 200, 300]
quantities = [2, 3, 4]

result = map(lambda price, quantity: price * quantity, prices, quantities)

print(list(result))
```

**Output:**
```text
[200, 600, 1200]
```

**Important:** When multiple iterables are passed, `map()` stops when the shortest iterable is exhausted.

---

## 10. map() with Tuple and String

### Example 1: Process a Tuple

```python
numbers = (2, 4, 6, 8)

result = map(lambda number: number * 5, numbers)

print(tuple(result))
```

**Output:**
```text
(10, 20, 30, 40)
```

### Example 2: Convert Characters

```python
characters = ["a", "b", "c", "d"]

result = map(lambda character: character.upper(), characters)

print(list(result))
```

**Output:**
```text
['A', 'B', 'C', 'D']
```

---

# Part 3 – filter()

## 11. What Is filter()?

The `filter()` function selects items from an iterable based on a condition.

It keeps only those items for which the supplied function returns a truthy value.

### Syntax

```python
filter(function, iterable)
```

Like `map()`, `filter()` returns an iterator.

### Example 1: Filter Even Numbers

```python
numbers = [1, 2, 3, 4, 5, 6, 7, 8]

result = filter(lambda number: number % 2 == 0, numbers)

print(list(result))
```

**Output:**
```text
[2, 4, 6, 8]
```

Explanation:

- `number % 2 == 0` checks whether a number is even.
- `filter()` keeps values where the condition is true.
- Odd numbers are excluded.

### Example 2: Filter Odd Numbers

```python
numbers = [1, 2, 3, 4, 5, 6]

result = filter(lambda number: number % 2 != 0, numbers)

print(list(result))
```

**Output:**
```text
[1, 3, 5]
```

### Example 3: Filter Positive Numbers

```python
numbers = [-10, 20, -5, 30, 0, 15]

result = filter(lambda number: number > 0, numbers)

print(list(result))
```

**Output:**
```text
[20, 30, 15]
```

---

## 12. filter() with Strings

### Example 1: Filter Names Starting with A

```python
names = ["Raj", "Aman", "Altaf", "Rahul", "Ankit"]

result = filter(lambda name: name.startswith("A"), names)

print(list(result))
```

**Output:**
```text
['Aman', 'Altaf', 'Ankit']
```

### Example 2: Filter Long Names

```python
names = ["Raj", "Altaf", "Aman", "Alexander", "John"]

result = filter(lambda name: len(name) > 4, names)

print(list(result))
```

**Output:**
```text
['Altaf', 'Alexander']
```

### Example 3: Filter Valid Email-Like Entries

```python
emails = [
    "raj@example.com",
    "invalid-email",
    "altaf@gmail.com",
    "user@",
    "aman@yahoo.com"
]

result = filter(
    lambda email: "@" in email and "." in email.split("@")[-1],
    emails
)

print(list(result))
```

**Output:**
```text
['raj@example.com', 'altaf@gmail.com', 'aman@yahoo.com']
```

This is only a basic screening example, not complete email validation.

---

## 13. filter() with Dictionaries

We can filter dictionaries by first iterating through their items or by filtering a list of dictionary records.

### Example: Filter Students by Marks

```python
students = [
    {"name": "Raj", "marks": 85},
    {"name": "Altaf", "marks": 45},
    {"name": "Aman", "marks": 92},
    {"name": "Rahul", "marks": 35}
]

result = filter(
    lambda student: student["marks"] >= 50,
    students
)

for student in result:
    print(student)
```

**Output:**
```text
{'name': 'Raj', 'marks': 85}
{'name': 'Aman', 'marks': 92}
```

---

# Part 4 – reduce()

## 14. What Is reduce()?

The `reduce()` function repeatedly applies a function to the items of an iterable and combines them into a single result.

Unlike `map()` and `filter()`, `reduce()` is not a built-in global function.

It is available in the `functools` module.

### Import

```python
from functools import reduce
```

### Syntax

```python
reduce(function, iterable, initializer)
```

The initializer is optional.

### Example 1: Sum of Numbers

```python
from functools import reduce

numbers = [10, 20, 30, 40]

result = reduce(lambda a, b: a + b, numbers)

print(result)
```

**Output:**
```text
100
```

### Understanding the Calculation

```text
Step 1: 10 + 20 = 30
Step 2: 30 + 30 = 60
Step 3: 60 + 40 = 100
```

The result of each operation becomes the first argument of the next operation.

### Example 2: Multiply All Numbers

```python
from functools import reduce

numbers = [2, 3, 4, 5]

result = reduce(lambda a, b: a * b, numbers)

print(result)
```

**Output:**
```text
120
```

Calculation:

```text
2 × 3 = 6
6 × 4 = 24
24 × 5 = 120
```

### Example 3: Find Maximum Number

```python
from functools import reduce

numbers = [10, 50, 20, 80, 30]

result = reduce(
    lambda a, b: a if a > b else b,
    numbers
)

print(result)
```

**Output:**
```text
80
```

### Example 4: Using an Initializer

```python
from functools import reduce

numbers = [10, 20, 30]

result = reduce(lambda a, b: a + b, numbers, 100)

print(result)
```

**Output:**
```text
160
```

Calculation:

```text
100 + 10 = 110
110 + 20 = 130
130 + 30 = 160
```

An initializer provides the starting value and also allows `reduce()` to work with an empty iterable.

### Example 5: Concatenate Strings

```python
from functools import reduce

words = ["Python", "is", "powerful"]

result = reduce(
    lambda a, b: a + " " + b,
    words
)

print(result)
```

**Output:**
```text
Python is powerful
```

---

# Part 5 – Comparing map(), filter() and reduce()

## 15. Main Differences

| Function | Purpose | Result |
|---|---|---|
| `map()` | Transforms every item | Iterator |
| `filter()` | Selects items based on a condition | Iterator |
| `reduce()` | Combines items into one result | Single accumulated result |

### Example: Same List, Three Operations

```python
from functools import reduce

numbers = [1, 2, 3, 4, 5, 6]

# map(): Square every number
squared = map(lambda number: number ** 2, numbers)

# filter(): Select even numbers
even = filter(lambda number: number % 2 == 0, numbers)

# reduce(): Calculate total
total = reduce(lambda a, b: a + b, numbers)

print("Squared:", list(squared))
print("Even:", list(even))
print("Total:", total)
```

**Output:**
```text
Squared: [1, 4, 9, 16, 25, 36]
Even: [2, 4, 6]
Total: 21
```

---

# Part 6 – Combining map(), filter() and reduce()

## 16. Using Multiple Functional Tools Together

These functions can be combined to process data in multiple steps.

### Example 1: Square Even Numbers and Calculate Their Sum

```python
from functools import reduce

numbers = [1, 2, 3, 4, 5, 6, 7, 8]

even_numbers = filter(
    lambda number: number % 2 == 0,
    numbers
)

squared_numbers = map(
    lambda number: number ** 2,
    even_numbers
)

total = reduce(
    lambda a, b: a + b,
    squared_numbers,
    0
)

print("Total:", total)
```

**Output:**
```text
Total: 120
```

Explanation:

1. `filter()` selects `[2, 4, 6, 8]`.
2. `map()` transforms them into `[4, 16, 36, 64]`.
3. `reduce()` adds them to produce `120`.

### Example 2: Calculate Total Price of Eligible Products

```python
from functools import reduce

products = [
    {"name": "Laptop", "price": 50000, "available": True},
    {"name": "Mouse", "price": 500, "available": True},
    {"name": "Keyboard", "price": 1200, "available": False},
    {"name": "Monitor", "price": 12000, "available": True}
]

available_products = filter(
    lambda product: product["available"],
    products
)

prices = map(
    lambda product: product["price"],
    available_products
)

total = reduce(lambda a, b: a + b, prices, 0)

print("Total Available Product Value:", total)
```

**Output:**
```text
Total Available Product Value: 62500
```

---

# Part 7 – List Comprehension vs map() and filter()

## 17. Alternative Ways to Process Collections

Python provides list comprehensions as another way to transform and filter collections.

### Example 1: Using map()

```python
numbers = [1, 2, 3, 4, 5]

result = list(map(lambda number: number ** 2, numbers))

print(result)
```

**Output:**
```text
[1, 4, 9, 16, 25]
```

Equivalent list comprehension:

```python
numbers = [1, 2, 3, 4, 5]

result = [number ** 2 for number in numbers]

print(result)
```

**Output:**
```text
[1, 4, 9, 16, 25]
```

### Example 2: Using filter()

```python
numbers = [1, 2, 3, 4, 5, 6]

result = list(filter(lambda number: number % 2 == 0, numbers))

print(result)
```

**Output:**
```text
[2, 4, 6]
```

Equivalent list comprehension:

```python
numbers = [1, 2, 3, 4, 5, 6]

result = [number for number in numbers if number % 2 == 0]

print(result)
```

**Output:**
```text
[2, 4, 6]
```

### When Should We Use Each?

| Approach | Suitable Situation |
|---|---|
| `map()` | Applying an existing function to every item |
| `filter()` | Selecting items based on a condition |
| `reduce()` | Combining values into one result |
| List comprehension | Readable list transformations and filtering |
| Normal loop | Complex logic or multiple operations |

**Trainer Note:** Students should understand all these approaches. Do not force the use of `map()` or `filter()` when a normal loop or comprehension is clearer.

---

# Part 8 – Practical Programs

## Program 1: Convert Marks into Grades Using map()

```python
marks = [95, 82, 67, 45, 30]

grades = map(
    lambda mark: "A" if mark >= 85 else
                 "B" if mark >= 70 else
                 "C" if mark >= 50 else
                 "Fail",
    marks
)

print(list(grades))
```

**Output:**
```text
['A', 'B', 'C', 'Fail', 'Fail']
```

## Program 2: Filter Students Who Passed

```python
students = [
    {"name": "Raj", "marks": 85},
    {"name": "Altaf", "marks": 45},
    {"name": "Aman", "marks": 92},
    {"name": "Rahul", "marks": 35}
]

passed = filter(
    lambda student: student["marks"] >= 40,
    students
)

for student in passed:
    print(student["name"], student["marks"])
```

**Output:**
```text
Raj 85
Altaf 45
Aman 92
```

## Program 3: Calculate the Total Salary Using reduce()

```python
from functools import reduce

salaries = [25000, 30000, 35000, 40000]

total_salary = reduce(
    lambda total, salary: total + salary,
    salaries,
    0
)

print("Total Salary:", total_salary)
```

**Output:**
```text
Total Salary: 130000
```

## Program 4: Apply Discount Using map()

```python
prices = [1000, 2000, 3000, 4000]

discounted_prices = map(
    lambda price: price - (price * 10 / 100),
    prices
)

print(list(discounted_prices))
```

**Output:**
```text
[900.0, 1800.0, 2700.0, 3600.0]
```

## Program 5: Filter Products by Price

```python
products = [
    {"name": "Laptop", "price": 50000},
    {"name": "Mouse", "price": 500},
    {"name": "Keyboard", "price": 1200},
    {"name": "Monitor", "price": 12000}
]

result = filter(
    lambda product: product["price"] < 10000,
    products
)

for product in result:
    print(product)
```

**Output:**
```text
{'name': 'Mouse', 'price': 500}
{'name': 'Keyboard', 'price': 1200}
```

## Program 6: Find the Average Using reduce()

```python
from functools import reduce

marks = [80, 90, 75, 85]

total = reduce(lambda a, b: a + b, marks, 0)

average = total / len(marks)

print("Total:", total)
print("Average:", average)
```

**Output:**
```text
Total: 330
Average: 82.5
```

---

# Part 9 – Mini Project

## 18. Mini Project – Student Performance Analyzer

### Project Description

Create a Student Performance Analyzer using:

- Lambda functions.
- `map()`.
- `filter()`.
- `reduce()`.
- Dictionaries.
- Lists.
- Functions.

The application should process student records and generate performance reports.

### Project Requirements

The system should:

1. Store multiple student records.
2. Calculate total marks.
3. Calculate average marks.
4. Assign grades.
5. Filter passed students.
6. Filter failed students.
7. Sort students by average marks.
8. Find the topper.
9. Calculate the class average.
10. Display a complete performance report.

### Sample Code

```python
from functools import reduce

students = [
    {
        "name": "Raj",
        "marks": [85, 90, 80]
    },
    {
        "name": "Altaf",
        "marks": [70, 75, 80]
    },
    {
        "name": "Aman",
        "marks": [95, 92, 98]
    },
    {
        "name": "Rahul",
        "marks": [30, 40, 35]
    }
]


def calculate_total(student):
    return sum(student["marks"])


def calculate_average(student):
    return calculate_total(student) / len(student["marks"])


def assign_grade(average):
    if average >= 85:
        return "A"

    elif average >= 70:
        return "B"

    elif average >= 50:
        return "C"

    else:
        return "Fail"


def generate_report():

    # Calculate student statistics
    student_reports = list(
        map(
            lambda student: {
                "name": student["name"],
                "total": calculate_total(student),
                "average": calculate_average(student),
                "grade": assign_grade(calculate_average(student))
            },
            students
        )
    )

    # Filter passed students
    passed_students = list(
        filter(
            lambda student: student["grade"] != "Fail",
            student_reports
        )
    )

    # Filter failed students
    failed_students = list(
        filter(
            lambda student: student["grade"] == "Fail",
            student_reports
        )
    )

    # Sort students by average
    ranked_students = sorted(
        student_reports,
        key=lambda student: student["average"],
        reverse=True
    )

    # Calculate class average
    class_total = reduce(
        lambda total, student: total + student["average"],
        student_reports,
        0
    )

    class_average = class_total / len(student_reports)

    # Display report
    print("\n===== STUDENT PERFORMANCE REPORT =====")

    for student in ranked_students:
        print(
            student["name"],
            "| Total:", student["total"],
            "| Average:", student["average"],
            "| Grade:", student["grade"]
        )

    print("\nPassed Students:", len(passed_students))
    print("Failed Students:", len(failed_students))

    print("Class Average:", round(class_average, 2))

    print("\nTopper:", ranked_students[0]["name"])


generate_report()
```

### Expected Output

```text
===== STUDENT PERFORMANCE REPORT =====
Aman | Total: 285 | Average: 95.0 | Grade: A
Raj | Total: 255 | Average: 85.0 | Grade: A
Altaf | Total: 225 | Average: 75.0 | Grade: B
Rahul | Total: 105 | Average: 35.0 | Grade: Fail

Passed Students: 3
Failed Students: 1
Class Average: 72.5

Topper: Aman
```

### Project Extension Tasks

After completing the basic project:

1. Accept student information using `input()`.
2. Add subject-wise performance analysis.
3. Display the highest and lowest marks.
4. Calculate the subject-wise class average.
5. Add grade-based filtering.
6. Sort students alphabetically.
7. Search for a student by name.
8. Add a percentage calculation.
9. Export the report to a CSV file (covered in a later lesson).
10. Handle empty student records safely.

---

# Part 10 – Student Practice Exercises

## Exercise 1 – Lambda Basics

Create lambda functions for:

- Addition.
- Subtraction.
- Multiplication.
- Division.
- Square.
- Cube.

## Exercise 2 – Conditional Lambda

Create a lambda function that checks whether a number is:

- Positive.
- Negative.
- Zero.

## Exercise 3 – map()

Given a list of numbers, use `map()` to:

- Square every number.
- Cube every number.
- Add 100 to every number.
- Convert every number to a string.

## Exercise 4 – Multiple Iterables

Given two lists, use `map()` to:

- Add corresponding values.
- Multiply corresponding values.
- Find the difference between corresponding values.

## Exercise 5 – filter()

Given a list of numbers, filter:

- Even numbers.
- Odd numbers.
- Positive numbers.
- Numbers greater than 50.
- Numbers divisible by both 3 and 5.

## Exercise 6 – String Filtering

Given a list of names, filter:

- Names starting with A.
- Names ending with n.
- Names longer than five characters.
- Names containing the letter a.

## Exercise 7 – reduce()

Use `reduce()` to:

- Calculate the sum of numbers.
- Calculate the product of numbers.
- Find the maximum number.
- Find the minimum number.
- Concatenate a list of strings.

Remember to handle empty iterables where necessary.

## Exercise 8 – Student Records

Given a list of student dictionaries:

- Use `map()` to calculate averages.
- Use `filter()` to select students who passed.
- Use `sorted()` with lambda to rank students.
- Use `reduce()` to calculate the class average.

## Exercise 9 – Product Management

Given a list of products:

- Filter products under Rs. 5,000.
- Apply a 15% discount using `map()`.
- Calculate the total discounted value using `reduce()`.

## Exercise 10 – Real-World Challenge

Create an Employee Salary Analyzer that:

- Stores employee names and salaries.
- Filters employees earning above Rs. 30,000.
- Applies a 10% salary increment using `map()`.
- Sorts employees by salary.
- Calculates total salary expenditure using `reduce()`.

---

# Part 11 – Trainer Assessment

## 19. Theory Assessment

| Question | Expected Understanding |
|---|---|
| What is a lambda function? | A small anonymous function |
| What is lambda syntax? | `lambda arguments: expression` |
| Can lambda contain multiple statements? | No, it contains one expression |
| What does `map()` do? | Applies a function to every item |
| What does `filter()` do? | Selects items based on a condition |
| What does `reduce()` do? | Combines iterable values into one result |
| Which module provides reduce()? | `functools` |
| What does `map()` return? | A map iterator |
| What does `filter()` return? | A filter iterator |
| Does `reduce()` return an iterator? | No, it returns an accumulated result |
| What is the purpose of `key` in `sorted()`? | Defines the value used for sorting |
| What is the difference between map and filter? | Transformation vs selection |

## 20. Practical Assessment

Ask the student to independently:

1. Create lambda functions for common calculations.
2. Use `map()` to transform a list.
3. Use `filter()` to select specific values.
4. Use `reduce()` to calculate a total.
5. Combine `map()`, `filter()` and `reduce()`.
6. Sort dictionaries using lambda.
7. Complete the Student Performance Analyzer.

---

# 21. Completion Criteria

Mark Day 22 as completed when the student can:

- Create lambda functions.
- Use lambda with one or multiple arguments.
- Use conditional expressions inside lambda functions.
- Apply lambda with `sorted()`, `max()` and `min()`.
- Use `map()` to transform collections.
- Use `filter()` to select collection elements.
- Use `reduce()` to combine values.
- Understand iterators returned by `map()` and `filter()`.
- Combine functional programming tools.
- Compare functional tools with list comprehensions.
- Process lists of dictionaries.
- Complete the Student Performance Analyzer independently.

**Trainer Note:** Focus on understanding what happens to each collection at every step. The student should be able to explain the transformation, filtering and accumulation process without memorizing code.

---

**End of Day 22 – Lambda, Map, Filter & Reduce**

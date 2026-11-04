
# Day 15 – Tuples

## 1. Introduction to Tuples

A tuple is a built-in Python data structure used to store multiple values in a single variable.

Tuples are similar to lists, but tuples are immutable.

**Immutable means:** Once a tuple is created, its elements cannot be directly added, removed or modified.

### Example

```python
students = ("Raj", "Aman", "Rahul", "Priya")

print(students)
```

**Output:**

```text
('Raj', 'Aman', 'Rahul', 'Priya')
```

### Important Characteristics of Tuples

1. Tuples are ordered.
2. Tuples are immutable.
3. Tuples allow duplicate values.
4. Tuples can store different data types.
5. Tuples support indexing and slicing.
6. Tuples are created using parentheses `()`.
7. Tuples can contain nested collections.

Example:

```python
data = (10, "Python", 25.5, True)

print(data)
```

**Output:**

```text
(10, 'Python', 25.5, True)
```

---

## 2. Creating Tuples

### A. Creating a Tuple Directly

```python
numbers = (10, 20, 30, 40, 50)

print(numbers)
```

**Output:**

```text
(10, 20, 30, 40, 50)
```

### B. Creating an Empty Tuple

```python
empty_tuple = ()

print(empty_tuple)
print(type(empty_tuple))
```

**Output:**

```text
()
<class 'tuple'>
```

### C. Creating a Tuple Without Parentheses

Python also allows tuple creation without parentheses. This is called tuple packing.

```python
student = "Raj", 21, 85

print(student)
print(type(student))
```

**Output:**

```text
('Raj', 21, 85)
<class 'tuple'>
```

### D. Creating a Single-Element Tuple

A single-element tuple requires a trailing comma.

Correct:

```python
value = (10,)

print(value)
print(type(value))
```

**Output:**

```text
(10,)
<class 'tuple'>
```

Incorrect:

```python
value = (10)

print(type(value))
```

**Output:**

```text
<class 'int'>
```

Why?

Parentheses alone do not create a tuple. The comma makes it a tuple.

### E. Using the tuple() Constructor

Python provides a built-in `tuple()` constructor.

```python
numbers = tuple([10, 20, 30, 40])

print(numbers)
```

**Output:**

```text
(10, 20, 30, 40)
```

We can also convert a string into a tuple:

```python
name = "Python"

characters = tuple(name)

print(characters)
```

**Output:**

```text
('P', 'y', 't', 'h', 'o', 'n')
```

---

## 3. Checking Tuple Type and Length

### type()

The `type()` function identifies the data type.

```python
data = (10, 20, 30)

print(type(data))
```

**Output:**

```text
<class 'tuple'>
```

### len()

The `len()` function returns the number of elements.

```python
fruits = ("Apple", "Banana", "Mango", "Orange")

print(len(fruits))
```

**Output:**

```text
4
```

---

## 4. Accessing Tuple Elements – Indexing

Tuples support zero-based indexing, just like lists.

Example:

```python
fruits = ("Apple", "Banana", "Mango", "Orange")

print(fruits[0])
print(fruits[1])
print(fruits[2])
print(fruits[3])
```

**Output:**

```text
Apple
Banana
Mango
Orange
```

### Negative Indexing

Negative indexing accesses elements from the end.

```python
fruits = ("Apple", "Banana", "Mango", "Orange")

print(fruits[-1])
print(fruits[-2])
print(fruits[-3])
print(fruits[-4])
```

**Output:**

```text
Orange
Mango
Banana
Apple
```

### IndexError

Accessing an index that does not exist raises an `IndexError`.

```python
numbers = (10, 20, 30)

print(numbers[5])
```

**Output:**

```text
IndexError: tuple index out of range
```

---

## 5. Tuple Slicing

Slicing extracts multiple elements from a tuple.

### Syntax

```python
tuple_name[start:stop:step]
```

- `start`: Starting index.
- `stop`: Ending index, excluded.
- `step`: Number of positions to move.

### Example 1: Basic Slicing

```python
numbers = (10, 20, 30, 40, 50, 60)

print(numbers[1:4])
```

**Output:**

```text
(20, 30, 40)
```

### Example 2: Starting from the Beginning

```python
numbers = (10, 20, 30, 40, 50)

print(numbers[:3])
```

**Output:**

```text
(10, 20, 30)
```

### Example 3: Slicing Until the End

```python
numbers = (10, 20, 30, 40, 50)

print(numbers[2:])
```

**Output:**

```text
(30, 40, 50)
```

### Example 4: Using Step

```python
numbers = (10, 20, 30, 40, 50, 60)

print(numbers[::2])
```

**Output:**

```text
(10, 30, 50)
```

### Example 5: Reversing a Tuple

```python
numbers = (10, 20, 30, 40, 50)

print(numbers[::-1])
```

**Output:**

```text
(50, 40, 30, 20, 10)
```

Slicing creates a new tuple. It does not modify the original tuple.

---

## 6. Tuple Immutability

Immutability is the most important property of tuples.

Once a tuple is created, we cannot directly modify its existing elements.

### Example: Trying to Update an Element

```python
numbers = (10, 20, 30)

numbers[1] = 100

print(numbers)
```

**Output:**

```text
TypeError: 'tuple' object does not support item assignment
```

### Example: Trying to Add an Element

```python
numbers = (10, 20, 30)

numbers.append(40)
```

**Output:**

```text
AttributeError: 'tuple' object has no attribute 'append'
```

### Example: Trying to Remove an Element

```python
numbers = (10, 20, 30)

numbers.remove(20)
```

**Output:**

```text
AttributeError: 'tuple' object has no attribute 'remove'
```

### Important: A Tuple Can Contain a Mutable Object

A tuple itself is immutable, but it can contain mutable objects such as lists.

```python
data = (10, 20, [30, 40])

data[2].append(50)

print(data)
```

**Output:**

```text
(10, 20, [30, 40, 50])
```

Why did this work?

- The tuple structure was not modified.
- The list stored inside the tuple was modified.
- Immutability prevents reassignment of tuple elements, not mutation of objects stored inside them.

---

## 7. Tuple Packing

Tuple packing means combining multiple values into a single tuple.

Example:

```python
student = "Raj", 21, "Python", 85

print(student)
```

**Output:**

```text
('Raj', 21, 'Python', 85)
```

Python automatically packs these values into a tuple.

We can also use parentheses:

```python
student = ("Raj", 21, "Python", 85)

print(student)
```

---

## 8. Tuple Unpacking

Tuple unpacking means assigning tuple elements to separate variables.

Example:

```python
student = ("Raj", 21, "Python")

name, age, course = student

print(name)
print(age)
print(course)
```

**Output:**

```text
Raj
21
Python
```

### Important Rule

The number of variables must match the number of elements when using ordinary unpacking.

Incorrect:

```python
numbers = (10, 20, 30)

a, b = numbers
```

**Output:**

```text
ValueError: too many values to unpack (expected 2)
```

### Extended Unpacking Using *

The `*` operator allows one variable to collect multiple elements into a list.

```python
numbers = (10, 20, 30, 40, 50)

first, *middle, last = numbers

print(first)
print(middle)
print(last)
```

**Output:**

```text
10
[20, 30, 40]
50
```

### Collecting Remaining Elements at the Beginning

```python
numbers = (10, 20, 30, 40, 50)

*start, last = numbers

print(start)
print(last)
```

**Output:**

```text
[10, 20, 30, 40]
50
```

---

## 9. Swapping Variables Using Tuples

Python allows us to swap values without using a temporary variable.

Example:

```python
a = 10
b = 20

a, b = b, a

print("a:", a)
print("b:", b)
```

**Output:**

```text
a: 20
b: 10
```

This works through tuple packing and unpacking.

---

## 10. Tuple Methods

Tuples have only two built-in methods because they are immutable.

### A. count()

Returns the number of times a value appears in a tuple.

```python
numbers = (10, 20, 10, 30, 10, 40)

result = numbers.count(10)

print(result)
```

**Output:**

```text
3
```

### B. index()

Returns the index of the first occurrence of a specified value.

```python
fruits = ("Apple", "Banana", "Mango", "Orange")

position = fruits.index("Mango")

print(position)
```

**Output:**

```text
2
```

### Searching Within a Specific Range

```python
numbers = (10, 20, 30, 20, 40)

position = numbers.index(20, 2)

print(position)
```

**Output:**

```text
3
```

The search starts from index `2`.

### Tuple Methods Summary

| Method | Description |
|---|---|
| `count()` | Counts occurrences of a value |
| `index()` | Returns the index of the first occurrence |

---

## 11. Tuple Operators

### A. Concatenation (+)

Combines two tuples and creates a new tuple.

```python
tuple1 = (10, 20, 30)
tuple2 = (40, 50, 60)

result = tuple1 + tuple2

print(result)
```

**Output:**

```text
(10, 20, 30, 40, 50, 60)
```

### B. Repetition (*)

Repeats tuple elements.

```python
numbers = (1, 2, 3)

result = numbers * 3

print(result)
```

**Output:**

```text
(1, 2, 3, 1, 2, 3, 1, 2, 3)
```

### C. Membership Operators

The `in` and `not in` operators check whether a value exists.

```python
fruits = ("Apple", "Banana", "Mango")

print("Apple" in fruits)
print("Orange" in fruits)
print("Orange" not in fruits)
```

**Output:**

```text
True
False
True
```

### D. Comparison Operators

Tuples can be compared using comparison operators.

```python
tuple1 = (10, 20, 30)
tuple2 = (10, 20, 40)

print(tuple1 == tuple2)
print(tuple1 < tuple2)
```

**Output:**

```text
False
True
```

Python compares tuples lexicographically: it compares corresponding elements from left to right and stops at the first difference.

---

## 12. Iterating Through a Tuple

Iteration means accessing elements one by one.

### A. Using a for Loop

```python
fruits = ("Apple", "Banana", "Mango")

for fruit in fruits:
    print(fruit)
```

**Output:**

```text
Apple
Banana
Mango
```

### B. Using a for Loop with range()

```python
fruits = ("Apple", "Banana", "Mango")

for i in range(len(fruits)):
    print(i, fruits[i])
```

**Output:**

```text
0 Apple
1 Banana
2 Mango
```

### C. Using a while Loop

```python
numbers = (10, 20, 30, 40)

i = 0

while i < len(numbers):
    print(numbers[i])
    i += 1
```

**Output:**

```text
10
20
30
40
```

### D. Using enumerate()

```python
students = ("Raj", "Aman", "Rahul")

for index, student in enumerate(students, start=1):
    print(index, student)
```

**Output:**

```text
1 Raj
2 Aman
3 Rahul
```

---

## 13. Useful Built-in Functions for Tuples

Python provides several built-in functions that work with tuples.

### A. len()

```python
numbers = (10, 20, 30, 40)

print(len(numbers))
```

**Output:**

```text
4
```

### B. max()

```python
numbers = (10, 50, 20, 90, 30)

print(max(numbers))
```

**Output:**

```text
90
```

### C. min()

```python
numbers = (10, 50, 20, 90, 30)

print(min(numbers))
```

**Output:**

```text
10
```

### D. sum()

```python
numbers = (10, 20, 30, 40)

print(sum(numbers))
```

**Output:**

```text
100
```

### E. sorted()

The `sorted()` function returns a new list containing the sorted elements.

```python
numbers = (50, 10, 40, 20, 30)

result = sorted(numbers)

print(result)
print(type(result))
```

**Output:**

```text
[10, 20, 30, 40, 50]
<class 'list'>
```

Important: `sorted()` returns a list, not a tuple.

If we need a sorted tuple:

```python
numbers = (50, 10, 40, 20, 30)

result = tuple(sorted(numbers))

print(result)
```

**Output:**

```text
(10, 20, 30, 40, 50)
```

---

## 14. Converting Between Lists and Tuples

Sometimes we need to convert a tuple into a list to modify its elements.

### A. Tuple to List

```python
numbers = (10, 20, 30, 40)

number_list = list(numbers)

number_list.append(50)

print(number_list)
```

**Output:**

```text
[10, 20, 30, 40, 50]
```

### B. List to Tuple

```python
numbers = [10, 20, 30, 40]

number_tuple = tuple(numbers)

print(number_tuple)
```

**Output:**

```text
(10, 20, 30, 40)
```

### C. Modify a Tuple Through Conversion

```python
numbers = (10, 20, 30)

temp_list = list(numbers)

temp_list[1] = 200
temp_list.append(40)

numbers = tuple(temp_list)

print(numbers)
```

**Output:**

```text
(10, 200, 30, 40)
```

We did not directly modify the tuple. Instead:

1. Converted the tuple into a list.
2. Modified the list.
3. Converted the list back into a tuple.

---

## 15. Nested Tuples

A nested tuple is a tuple containing other tuples.

Example:

```python
students = (
    ("Raj", 85),
    ("Aman", 90),
    ("Rahul", 78)
)

print(students)
```

**Output:**

```text
(('Raj', 85), ('Aman', 90), ('Rahul', 78))
```

### Accessing Nested Tuple Elements

```python
students = (
    ("Raj", 85),
    ("Aman", 90),
    ("Rahul", 78)
)

print(students[0])
print(students[0][0])
print(students[0][1])
```

**Output:**

```text
('Raj', 85)
Raj
85
```

### Traversing Nested Tuples

```python
students = (
    ("Raj", 85),
    ("Aman", 90),
    ("Rahul", 78)
)

for student in students:
    print("Name:", student[0])
    print("Marks:", student[1])
```

**Output:**

```text
Name: Raj
Marks: 85
Name: Aman
Marks: 90
Name: Rahul
Marks: 78
```

---

## 16. When Should We Use Tuples Instead of Lists?

Tuples are useful when data should remain fixed after creation.

### Use Lists When:

- You need to add or remove elements.
- You need to update existing elements.
- You need a collection that changes frequently.
- You are managing shopping items, task lists or user records.

### Use Tuples When:

- You want to represent fixed data.
- You want to prevent accidental reassignment of collection elements.
- You are representing coordinates, RGB colors or fixed configuration values.
- You need an immutable sequence that can be used as a dictionary key, provided all its elements are hashable.

### Real-World Examples

```python
# Geographic coordinates
location = (19.0760, 72.8777)

# RGB color
color = (255, 0, 0)

# Product dimensions
dimensions = (20, 30, 10)

# Database record
employee = (101, "Raj", "Developer", 45000)

print(location)
print(color)
print(dimensions)
print(employee)
```

**Output:**

```text
(19.076, 72.8777)
(255, 0, 0)
(20, 30, 10)
(101, 'Raj', 'Developer', 45000)
```

---

## 17. Practical Programs

### Program 1: Calculate Sum and Average of Tuple Elements

```python
numbers = (10, 20, 30, 40, 50)

total = sum(numbers)
average = total / len(numbers)

print("Sum:", total)
print("Average:", average)
```

**Output:**

```text
Sum: 150
Average: 30.0
```

### Program 2: Find Largest and Smallest Elements

```python
numbers = (45, 12, 89, 34, 67)

print("Largest:", max(numbers))
print("Smallest:", min(numbers))
```

**Output:**

```text
Largest: 89
Smallest: 12
```

### Program 3: Count Even and Odd Numbers

```python
numbers = (10, 15, 20, 25, 30, 35)

even_count = 0
odd_count = 0

for number in numbers:

    if number % 2 == 0:
        even_count += 1
    else:
        odd_count += 1

print("Even Numbers:", even_count)
print("Odd Numbers:", odd_count)
```

**Output:**

```text
Even Numbers: 3
Odd Numbers: 3
```

### Program 4: Search for an Element

```python
numbers = (10, 20, 30, 40, 50)

search = int(input("Enter number to search: "))

if search in numbers:
    print("Number Found")
else:
    print("Number Not Found")
```

**Sample Output:**

```text
Enter number to search: 30
Number Found
```

### Program 5: Find Duplicate Elements

```python
numbers = (10, 20, 10, 30, 20, 40, 10)

checked = []

for number in numbers:

    if number not in checked:
        if numbers.count(number) > 1:
            print(number, "appears", numbers.count(number), "times")

        checked.append(number)
```

**Output:**

```text
10 appears 3 times
20 appears 2 times
```

### Program 6: Reverse a Tuple

```python
numbers = (10, 20, 30, 40, 50)

reversed_tuple = numbers[::-1]

print("Original:", numbers)
print("Reversed:", reversed_tuple)
```

**Output:**

```text
Original: (10, 20, 30, 40, 50)
Reversed: (50, 40, 30, 20, 10)
```

### Program 7: Unpack Student Information

```python
student = ("Raj", 21, "Python Developer", 85)

name, age, course, marks = student

print("Name:", name)
print("Age:", age)
print("Course:", course)
print("Marks:", marks)
```

**Output:**

```text
Name: Raj
Age: 21
Course: Python Developer
Marks: 85
```

### Program 8: Find Common Elements Between Two Tuples

```python
tuple1 = (10, 20, 30, 40, 50)
tuple2 = (30, 40, 50, 60, 70)

common = []

for item in tuple1:

    if item in tuple2 and item not in common:
        common.append(item)

result = tuple(common)

print("Common Elements:", result)
```

**Output:**

```text
Common Elements: (30, 40, 50)
```

---

# 18. Mini Project – Employee Information System

## Project Description

Create a simple Employee Information System using tuples.

Each employee record should contain:

- Employee ID
- Employee Name
- Department
- Salary

The application should support:

1. Add an employee.
2. Display all employees.
3. Search an employee by ID.
4. Calculate total salary.
5. Calculate average salary.
6. Display the highest-paid employee.
7. Exit the application.

For this project, employee records will be stored as tuples inside a list.

The outer list is mutable, allowing us to add and remove employee records. Each individual employee tuple is immutable.

## Complete Code

```python
employees = []

while True:

    print("\n===== EMPLOYEE INFORMATION SYSTEM =====")
    print("1. Add Employee")
    print("2. Display Employees")
    print("3. Search Employee")
    print("4. Total Salary")
    print("5. Average Salary")
    print("6. Highest Paid Employee")
    print("7. Exit")

    choice = input("Enter your choice: ")

    if choice == "1":

        emp_id = input("Enter Employee ID: ").strip()
        name = input("Enter Employee Name: ").strip()
        department = input("Enter Department: ").strip()

        if not emp_id or not name or not department:
            print("All Fields Are Required.")
            continue

        if any(employee[0] == emp_id for employee in employees):
            print("Employee ID Already Exists.")
            continue

        try:
            salary = float(input("Enter Salary: "))

            if salary < 0:
                print("Salary Cannot Be Negative.")
                continue

        except ValueError:
            print("Please Enter a Valid Salary.")
            continue

        employee = (emp_id, name, department, salary)

        employees.append(employee)

        print("Employee Added Successfully.")

    elif choice == "2":

        if not employees:
            print("No Employee Records Found.")

        else:

            print("\nEmployee Records:")

            for employee in employees:

                emp_id, name, department, salary = employee

                print(f"""
Employee ID: {emp_id}
Name: {name}
Department: {department}
Salary: {salary}
--------------------------
""")

    elif choice == "3":

        search_id = input("Enter Employee ID: ").strip()

        found = None

        for employee in employees:

            if employee[0] == search_id:
                found = employee
                break

        if found:
            print("Employee Found:", found)
        else:
            print("Employee Not Found.")

    elif choice == "4":

        total_salary = sum(employee[3] for employee in employees)

        print("Total Salary:", total_salary)

    elif choice == "5":

        if employees:

            total_salary = sum(employee[3] for employee in employees)

            average = total_salary / len(employees)

            print("Average Salary:", round(average, 2))

        else:
            print("No Employee Records Available.")

    elif choice == "6":

        if employees:

            highest_paid = max(
                employees,
                key=lambda employee: employee[3]
            )

            print("Highest Paid Employee:", highest_paid)

        else:
            print("No Employee Records Available.")

    elif choice == "7":

        print("Thank You for Using Employee Information System.")
        break

    else:
        print("Invalid Choice. Please Try Again.")
```

## Project Challenge

Improve the project by adding:

- Search employees by department.
- Display employees in alphabetical order.
- Sort employees by salary.
- Calculate department-wise salary totals.
- Add employee count.
- Allow deleting an employee by ID.

---

# 19. Student Practice Exercises

## Beginner Level

1. Create a tuple containing five programming languages.
2. Print the first and last elements.
3. Access tuple elements using negative indexing.
4. Find the length of a tuple.
5. Create an empty tuple.
6. Create a single-element tuple correctly.
7. Convert a string into a tuple.
8. Reverse a tuple using slicing.

## Intermediate Level

9. Calculate the sum and average of tuple elements.
10. Find the largest and smallest elements.
11. Count how many times a specific value appears.
12. Find the index of an element.
13. Unpack a tuple into separate variables.
14. Swap two variables using tuple unpacking.
15. Find common elements between two tuples.
16. Remove duplicate elements by creating a new tuple.
17. Convert a tuple into a list, modify it and convert it back.
18. Count even and odd numbers.

## Advanced Level

19. Create a nested tuple containing student names and marks.
20. Find the student with the highest marks.
21. Sort a tuple of numbers without modifying the original tuple.
22. Create a tuple containing employee records.
23. Use extended unpacking to separate the first, middle and last elements.
24. Build a menu-driven Employee Information System.

---

# 20. Trainer Assessment

Ask the student to explain and demonstrate:

1. What is a tuple?
2. What is the difference between a list and a tuple?
3. Why are tuples called immutable?
4. How do we create a single-element tuple?
5. What is tuple packing?
6. What is tuple unpacking?
7. How does extended unpacking work?
8. What is the difference between `count()` and `index()`?
9. Why does `sorted()` return a list when used on a tuple?
10. Can a tuple contain a list?
11. What is the difference between tuple concatenation and tuple repetition?
12. When should we use tuples instead of lists?

## Practical Assessment

Ask the student to create a program that:

- Accepts five numbers from the user.
- Stores the numbers in a tuple.
- Displays the original tuple.
- Calculates the sum and average.
- Finds the maximum and minimum.
- Counts even and odd numbers.
- Displays the reversed tuple.
- Creates a sorted tuple without modifying the original tuple.

## Completion Criteria

The lesson is complete when the student can:

- Create tuples using different techniques.
- Perform indexing and slicing.
- Explain tuple immutability.
- Perform packing and unpacking.
- Use tuple methods and operators.
- Convert between lists and tuples.
- Work with nested tuples.
- Complete the Employee Information System.
- Solve the practical assessment independently.

**Trainer Note:** Focus on single-element tuple syntax, packing and unpacking, immutability, and the difference between a tuple and a list. These are the most important concepts in this lesson.

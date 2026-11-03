
# Day 04 — Variables and Data Types in Python

---

# Part 1 — Understanding Variables

## 1.1 What is a Variable?

A variable is a name that refers to a value stored and used by a Python program.

Variables allow us to store information and use it whenever required.

### Real-Life Example

Suppose we want to store a student's information:

- Name: Raj
- Age: 20
- City: Mumbai

Instead of writing these values repeatedly, we can assign them to variables.

### Practical Demonstration

Create a file:

`variables.py`

Write:

```python
student_name = "Raj"
student_age = 20
student_city = "Mumbai"

print(student_name)
print(student_age)
print(student_city)
```

### Expected Output

```text
Raj
20
Mumbai
```

### Code Explanation

- `student_name` is a variable referring to the string `"Raj"`.
- `student_age` refers to the integer `20`.
- `student_city` refers to the string `"Mumbai"`.
- `print()` displays the values.

**Important:** Python variables are names that refer to objects. They are not fixed storage boxes with permanently attached data types.

---

# Part 2 — Assigning Values to Variables

## 2.1 Basic Assignment

The assignment operator `=` assigns a value to a variable.

Example:

```python
name = "Raj"
age = 21
salary = 25000
```

Explanation:

- `name` refers to `"Raj"`.
- `age` refers to `21`.
- `salary` refers to `25000`.

## 2.2 Changing Variable Values

A variable can refer to a different value later in the program.

```python
age = 20

print(age)

age = 21

print(age)
```

### Expected Output

```text
20
21
```

### Explanation

1. Initially, `age` refers to `20`.
2. The first `print()` displays `20`.
3. The assignment `age = 21` changes the value referred to by `age`.
4. The second `print()` displays `21`.

## 2.3 Assigning Multiple Variables

Python allows multiple variables to be assigned in one statement.

```python
name, age, city = "Raj", 21, "Mumbai"

print(name)
print(age)
print(city)
```

Output:

```text
Raj
21
Mumbai
```

## 2.4 Assigning the Same Value to Multiple Variables

```python
a = b = c = 100

print(a)
print(b)
print(c)
```

Output:

```text
100
100
100
```

## 2.5 Swapping Variable Values

Python allows us to swap two variable values without using a temporary variable.

```python
a = 10
b = 20

a, b = b, a

print("A:", a)
print("B:", b)
```

Output:

```text
A: 20
B: 10
```

### Student Practice

1. Create variables for your name, age and city.
2. Change the age variable and print it again.
3. Assign three values to three variables in one statement.
4. Assign the same number to four variables.
5. Swap two variables and display the result.

---

# Part 3 — Rules for Variable Naming

## 3.1 Variable Naming Rules

Python follows identifier naming rules for variables.

### Rule 1: Must Start With a Letter or Underscore

Valid:

```python
name = "Raj"
_age = 21
student1 = "Amit"
```

Invalid:

```python
1student = "Raj"
```

### Rule 2: Spaces Are Not Allowed

Invalid:

```python
student name = "Raj"
```

Correct:

```python
student_name = "Raj"
```

### Rule 3: Special Characters Are Not Allowed

Invalid:

```python
student@name = "Raj"
```

### Rule 4: Keywords Cannot Be Used

Invalid:

```python
class = "Python"
```

`class` is a reserved Python keyword.

### Rule 5: Python is Case-Sensitive

```python
name = "Raj"
Name = "Amit"

print(name)
print(Name)
```

Output:

```text
Raj
Amit
```

Both are different variable names.

## 3.2 Variable Naming Best Practices

Use meaningful names.

Good:

```python
student_name = "Raj"
total_price = 500
employee_salary = 30000
```

Avoid unclear names:

```python
x = "Raj"
p = 500
s = 30000
```

Short names can be appropriate in specific situations, but descriptive names make programs easier to understand.

### Student Practice

Identify valid and invalid variable names:

1. `name`
2. `student_name`
3. `1age`
4. `_price`
5. `total-price`
6. `studentAge`
7. `class`
8. `employee_salary`
9. `my age`
10. `Age`

---

# Part 4 — Understanding Data Types

## 4.1 What is a Data Type?

A data type describes the kind of value represented by an object.

Python provides several built-in data types.

Different data types support different kinds of operations.

For example:

- Numbers support mathematical operations.
- Strings represent text.
- Lists store collections of values.
- Dictionaries store key-value pairs.

### Common Python Data Types

| Data Type | Description | Example |
|---|---|---|
| int | Integer numbers | `100` |
| float | Decimal numbers | `10.5` |
| complex | Complex numbers | `2 + 3j` |
| str | Text | `"Python"` |
| bool | Boolean values | `True` |
| list | Ordered, mutable collection | `[10, 20, 30]` |
| tuple | Ordered, immutable collection | `(10, 20, 30)` |
| range | Sequence of integers | `range(5)` |
| dict | Key-value collection | `{"name": "Raj"}` |
| set | Collection of unique values | `{10, 20, 30}` |
| frozenset | Immutable set | `frozenset({1, 2})` |
| NoneType | Absence of a value | `None` |

We will study collection types in detail in later lessons.

---

# Part 5 — Numeric Data Types

## 5.1 Integer (int)

An integer is a whole number without a decimal component.

Examples:

```python
age = 21
students = 50
temperature = -5

print(age)
print(students)
print(temperature)
```

Output:

```text
21
50
-5
```

### Practical Example

Create:

`integer_demo.py`

```python
product_quantity = 10
total_students = 35
bank_balance = 5000

print("Product Quantity:", product_quantity)
print("Total Students:", total_students)
print("Bank Balance:", bank_balance)
```

## 5.2 Float

A float represents a floating-point number, commonly used for decimal values.

Example:

```python
price = 99.50
height = 5.8
percentage = 85.75

print(price)
print(height)
print(percentage)
```

Output:

```text
99.5
5.8
85.75
```

### Practical Example

Create:

`float_demo.py`

```python
product_price = 499.99
student_percentage = 87.5
temperature = 36.6

print("Product Price:", product_price)
print("Percentage:", student_percentage)
print("Temperature:", temperature)
```

## 5.3 Complex

Complex numbers contain a real component and an imaginary component.

Python uses `j` for the imaginary part.

Example:

```python
number = 2 + 3j

print(number)
print(type(number))
```

Output:

```text
(2+3j)
<class 'complex'>
```

Complex numbers are used in areas such as scientific computing and engineering.

---

# Part 6 — String Data Type

## 6.1 What is a String?

A string (`str`) is a sequence of characters used to represent text.

Strings are written using single quotes, double quotes or triple quotes.

Example:

```python
name = "Raj"
city = 'Mumbai'
message = """Welcome to Python"""

print(name)
print(city)
print(message)
```

Output:

```text
Raj
Mumbai
Welcome to Python
```

## 6.2 Single and Double Quotes

Both are valid:

```python
name = 'Raj'
city = "Mumbai"

print(name)
print(city)
```

Use the quotation style that makes the string easier to write and read.

## 6.3 Multi-Line Strings

Triple quotes allow strings to span multiple lines.

```python
message = """Welcome
to
Python Training"""

print(message)
```

Output:

```text
Welcome
to
Python Training
```

## 6.4 Checking String Type

```python
name = "Raj"

print(type(name))
```

Output:

```text
<class 'str'>
```

---

# Part 7 — Boolean Data Type

## 7.1 What is Boolean?

The Boolean data type represents one of two values:

- `True`
- `False`

Boolean values are used for conditions and logical decisions.

Example:

```python
is_student = True
is_employed = False

print(is_student)
print(is_employed)
```

Output:

```text
True
False
```

### Practical Example

```python
is_python_installed = True

print("Python Installed:", is_python_installed)
print(type(is_python_installed))
```

Output:

```text
Python Installed: True
<class 'bool'>
```

### Important Rule

Python Boolean values must begin with capital letters:

Correct:

```python
is_active = True
```

Incorrect:

```python
is_active = true
```

---

# Part 8 — Understanding type()

## 8.1 What is type()?

`type()` is a built-in Python function that returns the type of an object.

Example:

```python
name = "Raj"
age = 21
salary = 25000.50
is_student = True

print(type(name))
print(type(age))
print(type(salary))
print(type(is_student))
```

Output:

```text
<class 'str'>
<class 'int'>
<class 'float'>
<class 'bool'>
```

## 8.2 Checking Multiple Data Types

Create:

`type_demo.py`

```python
a = 100
b = 25.5
c = "Python"
d = True
e = 2 + 3j

print("a:", type(a))
print("b:", type(b))
print("c:", type(c))
print("d:", type(d))
print("e:", type(e))
```

Expected Output:

```text
a: <class 'int'>
b: <class 'float'>
c: <class 'str'>
d: <class 'bool'>
e: <class 'complex'>
```

---

# Part 9 — Dynamic Typing in Python

## 9.1 What is Dynamic Typing?

Python is dynamically typed.

This means that we do not need to explicitly declare a variable's type when assigning a value.

Python determines the type of the object at runtime.

Example:

```python
value = 100

print(value)
print(type(value))

value = "Python"

print(value)
print(type(value))
```

Output:

```text
100
<class 'int'>
Python
<class 'str'>
```

### Explanation

1. Initially, `value` refers to an integer object.
2. Python reports its type as `int`.
3. Later, `value` is assigned a string object.
4. Python reports its new type as `str`.

### Important Understanding

Python does not convert the integer `100` into the string `"Python"`.

The variable name `value` is simply assigned to a different object.

### Student Practice

Create a variable named `data`.

1. Assign an integer to it.
2. Print its value and type.
3. Assign a string to it.
4. Print its value and type.
5. Assign a float to it.
6. Print its value and type.

---

# Part 10 — Checking Object Identity and None

## 10.1 What is None?

`None` is a special Python object that represents the absence of a value.

Example:

```python
result = None

print(result)
print(type(result))
```

Output:

```text
None
<class 'NoneType'>
```

`None` is different from:

- `0`
- `False`
- `""`
- An empty list

These values have different meanings and types.

## 10.2 Checking for None

Use `is None` to check whether a value is `None`.

```python
result = None

print(result is None)
```

Output:

```text
True
```

### Student Practice

Create four variables:

```python
a = 0
b = False
c = ""
d = None
```

Print the type of each variable and observe the differences.

---

# Part 11 — Hands-On Practical Exercises

## Exercise 1 — Personal Information

Create:

`personal_info.py`

Store the following information in separate variables:

- Student name
- Age
- City
- Course name
- Percentage
- Student status

Print all values with meaningful labels.

## Exercise 2 — Employee Information

Create:

`employee.py`

Store:

- Employee name
- Employee ID
- Department
- Salary
- Experience
- Employment status

Display all information using `print()`.

## Exercise 3 — Variable Reassignment

Create:

`reassignment.py`

1. Assign `100` to a variable.
2. Display its value and type.
3. Reassign `"Python"` to the same variable.
4. Display its value and type.
5. Reassign `50.5`.
6. Display its value and type.

## Exercise 4 — Multiple Assignment

Create:

`multiple_assignment.py`

Assign the following values to separate variables in one statement:

- Name: Raj
- Age: 21
- City: Mumbai

Display all values.

## Exercise 5 — Variable Swapping

Create:

`swap.py`

Swap the values of:

```python
a = 100
b = 200
```

Display the values before and after swapping.

## Exercise 6 — Data Type Identification

Create:

`data_types.py`

Create variables containing:

- Integer
- Float
- Complex
- String
- Boolean
- None

Display each value and its data type using `type()`.

## Exercise 7 — Identifier Validation

Create a list of at least 15 variable names.

Identify which are valid and which are invalid according to Python naming rules.

Explain the reason for every invalid name.

---

# Part 12 — Mini Project: Student Information System

Create:

`student_information.py`

### Requirements

Store the following information in separate variables:

- Student name
- Roll number
- Age
- Course
- City
- Percentage
- Is currently enrolled

### Sample Code

```python
student_name = "Raj Gupta"
roll_number = 101
age = 21
course = "Python Programming"
city = "Mumbai"
percentage = 85.5
is_enrolled = True

print("========== STUDENT INFORMATION ==========")
print("Name:", student_name)
print("Roll Number:", roll_number)
print("Age:", age)
print("Course:", course)
print("City:", city)
print("Percentage:", percentage)
print("Currently Enrolled:", is_enrolled)
print("=========================================")

print("\n---------- DATA TYPES ----------")
print("Name:", type(student_name))
print("Roll Number:", type(roll_number))
print("Age:", type(age))
print("Course:", type(course))
print("City:", type(city))
print("Percentage:", type(percentage))
print("Enrolled:", type(is_enrolled))
```

### Expected Output

```text
========== STUDENT INFORMATION ==========
Name: Raj Gupta
Roll Number: 101
Age: 21
Course: Python Programming
City: Mumbai
Percentage: 85.5
Currently Enrolled: True
=========================================

---------- DATA TYPES ----------
Name: <class 'str'>
Roll Number: <class 'int'>
Age: <class 'int'>
Course: <class 'str'>
City: <class 'str'>
Percentage: <class 'float'>
Enrolled: <class 'bool'>
```

### Student Challenge

Modify the project:

1. Change the student details.
2. Add three more variables.
3. Display the type of every variable.
4. Rename variables using proper `snake_case`.
5. Add comments explaining each section.

---

# Part 13 — Day 4 Assignment

Complete these tasks independently:

1. Create 10 variables with different names.
2. Use at least five different data types.
3. Change the values of three variables.
4. Demonstrate dynamic typing.
5. Use multiple assignment.
6. Swap two variable values.
7. Check the type of at least eight objects.
8. Create a complete student information program.
9. Explain the difference between `int`, `float`, `str` and `bool`.
10. Explain dynamic typing in your own words.

---

# Part 14 — Trainer Assessment

- [ ] Student understands variables.
- [ ] Student can assign values to variables.
- [ ] Student can reassign values.
- [ ] Student understands multiple assignment.
- [ ] Student can swap variables.
- [ ] Student follows variable naming rules.
- [ ] Student understands integer and float.
- [ ] Student understands string and Boolean.
- [ ] Student can identify complex numbers.
- [ ] Student can use `type()`.
- [ ] Student understands dynamic typing.
- [ ] Student understands `None`.
- [ ] Student can build the student information program independently.

## Day 4 Completion Criteria

The student must independently create programs using variables, store different types of values, check their types and explain how Python handles variable reassignment.

**Next Lesson:** Day 5 — Type Conversion, User Input and Basic Input/Output Operations.


# Day 19 – Python Functions Fundamentals

## 1. Introduction to Functions

A function is a reusable block of code that performs a specific task.

Instead of writing the same code repeatedly, we can create a function once and call it whenever required.

### Example: Without a Function

```python
print("Welcome to Python")
print("Welcome to Python")
print("Welcome to Python")
```

**Output:**

```text
Welcome to Python
Welcome to Python
Welcome to Python
```

Here, the same statement is written three times.

### Example: With a Function

```python
def welcome():
    print("Welcome to Python")

welcome()
welcome()
welcome()
```

**Output:**

```text
Welcome to Python
Welcome to Python
Welcome to Python
```

We defined the function once and reused it three times.

### Advantages of Functions

1. Code reusability.
2. Reduced code duplication.
3. Better code organization.
4. Easier debugging.
5. Easier testing and maintenance.
6. Improved readability.
7. Breaking large programs into smaller tasks.

---

## 2. Types of Functions in Python

Python functions can be broadly divided into two categories.

### 1. Built-in Functions

These functions are already provided by Python.

Examples:

```python
print("Hello")
print(len("Python"))
print(type(100))
print(max(10, 20, 30))
print(sum([10, 20, 30]))
```

**Output:**

```text
Hello
6
<class 'int'>
30
60
```

Other built-in functions include:

- `input()`
- `int()`
- `float()`
- `str()`
- `list()`
- `tuple()`
- `set()`
- `dict()`
- `range()`
- `sorted()`
- `abs()`
- `round()`

### 2. User-Defined Functions

Functions created by programmers to perform specific tasks are called user-defined functions.

Example:

```python
def greet():
    print("Hello, Student!")

greet()
```

**Output:**

```text
Hello, Student!
```

---

## 3. Creating a Function Using def

Python uses the `def` keyword to define a function.

### Syntax

```python
def function_name():
    # Function body
    statements
```

Explanation:

- `def`: Keyword used to define a function.
- `function_name`: Name of the function.
- `()`: Parentheses used for parameters.
- `:`: Marks the beginning of the function body.
- Indented statements: Code executed when the function is called.

### Example

```python
def display_message():
    print("Python is easy to learn.")
    print("Functions make code reusable.")

display_message()
```

**Output:**

```text
Python is easy to learn.
Functions make code reusable.
```

---

## 4. Calling a Function

Defining a function does not automatically execute its code.

To execute the function, we must call it using its name followed by parentheses.

### Example

```python
def show_message():
    print("Function executed.")

print("Before function call")

show_message()

print("After function call")
```

**Output:**

```text
Before function call
Function executed.
After function call
```

### Important

```python
def greet():
    print("Hello")
```

This only defines the function.

```python
greet()
```

This executes the function.

A function can be called multiple times:

```python
def greet():
    print("Hello!")

greet()
greet()
greet()
```

**Output:**

```text
Hello!
Hello!
Hello!
```

---

## 5. Function Naming Rules

Function names follow Python identifier naming rules.

### Valid Names

```python
def greet():
    pass

def calculate_total():
    pass

def student_details():
    pass

def calculate_average_marks():
    pass
```

### Invalid Names

```python
def 123calculate():
    pass

def student-details():
    pass

def class():
    pass
```

Reasons:

- Function names cannot start with numbers.
- Hyphens are not allowed in identifiers.
- Python keywords cannot be used as function names.

### Naming Best Practice

Use descriptive names and `snake_case`.

Examples:

```python
calculate_total()
display_student_details()
find_highest_marks()
```

Avoid unclear names:

```python
abc()
x1()
doit()
```

---

## 6. Functions Without Parameters

A function without parameters does not require any input from the caller.

### Example 1: Welcome Message

```python
def welcome():
    print("Welcome to Python Training!")

welcome()
```

**Output:**

```text
Welcome to Python Training!
```

### Example 2: Display Current Course Information

```python
def course_details():
    print("Course: Python")
    print("Duration: 50 Days")
    print("Level: Beginner")

course_details()
```

**Output:**

```text
Course: Python
Duration: 50 Days
Level: Beginner
```

### Example 3: Display a Multiplication Table

```python
def multiplication_table():
    number = 5

    for i in range(1, 11):
        print(number, "x", i, "=", number * i)

multiplication_table()
```

**Output:**

```text
5 x 1 = 5
5 x 2 = 10
5 x 3 = 15
5 x 4 = 20
5 x 5 = 25
5 x 6 = 30
5 x 7 = 35
5 x 8 = 40
5 x 9 = 45
5 x 10 = 50
```

---

## 7. Functions With Parameters

Parameters allow us to pass information into a function.

### Example 1: Single Parameter

```python
def greet(name):
    print("Hello", name)

greet("Raj")
greet("Rahul")
greet("Amit")
```

**Output:**

```text
Hello Raj
Hello Rahul
Hello Amit
```

Here:

- `name` is a parameter.
- `"Raj"`, `"Rahul"` and `"Amit"` are arguments.

### Example 2: Multiple Parameters

```python
def student_details(name, age, course):

    print("Name:", name)
    print("Age:", age)
    print("Course:", course)

student_details("Raj", 21, "Python")
```

**Output:**

```text
Name: Raj
Age: 21
Course: Python
```

### Example 3: Addition Using Parameters

```python
def add(a, b):
    result = a + b
    print("Sum:", result)

add(10, 20)
add(50, 30)
```

**Output:**

```text
Sum: 30
Sum: 80
```

### Example 4: Calculate Rectangle Area

```python
def rectangle_area(length, width):

    area = length * width

    print("Rectangle Area:", area)

rectangle_area(10, 5)
```

**Output:**

```text
Rectangle Area: 50
```

---

## 8. Difference Between Parameters and Arguments

These terms are related but have different meanings.

### Parameters

Parameters are variables written inside the function definition.

```python
def greet(name):
    print("Hello", name)
```

Here, `name` is a parameter.

### Arguments

Arguments are actual values passed when calling the function.

```python
greet("Raj")
```

Here, `"Raj"` is an argument.

### Comparison

| Parameters | Arguments |
|---|---|
| Defined in function definition | Supplied during function call |
| Receive values | Provide values |
| Example: `name` | Example: `"Raj"` |

---

## 9. Functions With Multiple Parameters

A function can accept multiple parameters to perform more complex operations.

### Example 1: Addition of Three Numbers

```python
def add_numbers(a, b, c):

    total = a + b + c

    print("Total:", total)

add_numbers(10, 20, 30)
```

**Output:**

```text
Total: 60
```

### Example 2: Calculate Student Average

```python
def calculate_average(mark1, mark2, mark3):

    total = mark1 + mark2 + mark3

    average = total / 3

    print("Total:", total)
    print("Average:", average)

calculate_average(80, 90, 85)
```

**Output:**

```text
Total: 255
Average: 85.0
```

### Example 3: Find the Largest Number

```python
def find_largest(a, b, c):

    if a >= b and a >= c:
        print("Largest:", a)

    elif b >= a and b >= c:
        print("Largest:", b)

    else:
        print("Largest:", c)

find_largest(10, 50, 30)
```

**Output:**

```text
Largest: 50
```

---

## 10. Default Parameters

A default parameter has a predefined value.

If the caller does not provide an argument for that parameter, Python uses its default value.

### Example 1: Basic Default Parameter

```python
def greet(name="Student"):

    print("Hello", name)

greet()
greet("Raj")
```

**Output:**

```text
Hello Student
Hello Raj
```

### Example 2: Multiple Default Parameters

```python
def student_details(name, course="Python", city="Mumbai"):

    print("Name:", name)
    print("Course:", course)
    print("City:", city)

student_details("Raj")

print()

student_details("Rahul", "Java")

print()

student_details("Amit", "Python", "Pune")
```

**Output:**

```text
Name: Raj
Course: Python
City: Mumbai

Name: Rahul
Course: Java
City: Mumbai

Name: Amit
Course: Python
City: Pune
```

### Important Rule

Parameters without default values must come before parameters with default values.

Valid:

```python
def calculate(a, b=10):
    print(a + b)
```

Invalid:

```python
def calculate(a=10, b):
    print(a + b)
```

This produces a `SyntaxError`.

---

## 11. Positional Arguments

Positional arguments are matched with parameters according to their position.

### Example

```python
def student_details(name, age, city):

    print("Name:", name)
    print("Age:", age)
    print("City:", city)

student_details("Raj", 21, "Mumbai")
```

**Output:**

```text
Name: Raj
Age: 21
City: Mumbai
```

The first argument goes to the first parameter, the second to the second, and so on.

### Position Matters

```python
student_details(21, "Raj", "Mumbai")
```

This call does not raise an error, but it assigns the values incorrectly.

Output:

```text
Name: 21
Age: Raj
City: Mumbai
```

Python does not automatically understand the intended meaning of each value.

---

## 12. Keyword Arguments

Keyword arguments specify parameter names during a function call.

### Example

```python
def student_details(name, age, city):

    print("Name:", name)
    print("Age:", age)
    print("City:", city)

student_details(
    age=21,
    city="Mumbai",
    name="Raj"
)
```

**Output:**

```text
Name: Raj
Age: 21
City: Mumbai
```

The order does not matter when all arguments are supplied using their parameter names.

### Mixing Positional and Keyword Arguments

```python
def student_details(name, age, city):

    print(name, age, city)

student_details("Raj", city="Mumbai", age=21)
```

This is valid.

**Important:** Positional arguments must come before keyword arguments.

Invalid:

```python
student_details(name="Raj", 21, "Mumbai")
```

This causes a `SyntaxError`.

---

## 13. The return Statement

The `return` statement sends a result from a function back to the caller.

### Example 1: Function Without return

```python
def add(a, b):

    result = a + b

    print(result)

answer = add(10, 20)

print("Answer:", answer)
```

**Output:**

```text
30
Answer: None
```

Why is the answer `None`?

Because the function printed the result but did not return it.

### Example 2: Function With return

```python
def add(a, b):

    result = a + b

    return result

answer = add(10, 20)

print("Answer:", answer)
```

**Output:**

```text
Answer: 30
```

The function returned the result, which was stored in `answer`.

### Important Difference

| print() | return |
|---|---|
| Displays information | Sends a value back to the caller |
| Does not provide that displayed value as the function result | Makes the returned value available to the caller |
| Useful for output | Useful for calculations and reusable results |

### Example 3: Reusing a Returned Value

```python
def square(number):

    return number * number

result = square(5)

print(result)
print(result + 10)
print(result * 2)
```

**Output:**

```text
25
35
50
```

### Example 4: Return Multiple Values

```python
def calculate(a, b):

    total = a + b
    difference = a - b
    product = a * b

    return total, difference, product

result = calculate(20, 10)

print(result)
```

**Output:**

```text
(30, 10, 200)
```

Python packs the returned values into a tuple.

You can also unpack them:

```python
total, difference, product = calculate(20, 10)

print("Total:", total)
print("Difference:", difference)
print("Product:", product)
```

**Output:**

```text
Total: 30
Difference: 10
Product: 200
```

---

## 14. The return Statement Ends Function Execution

When Python encounters `return`, it immediately exits the current function.

### Example

```python
def check_number(number):

    if number > 0:
        return "Positive Number"

    return "Zero or Negative Number"

result = check_number(10)

print(result)
```

**Output:**

```text
Positive Number
```

### Example: Code After Return

```python
def greet():

    return "Hello"

    print("This will not execute")

print(greet())
```

**Output:**

```text
Hello
```

The `print()` statement after `return` is unreachable during normal execution of this function.

---

## 15. Functions With Conditional Statements

Functions can contain conditions to make decisions.

### Example 1: Check Even or Odd

```python
def check_even_odd(number):

    if number % 2 == 0:
        return "Even"

    else:
        return "Odd"

print(check_even_odd(10))
print(check_even_odd(7))
```

**Output:**

```text
Even
Odd
```

### Example 2: Check Pass or Fail

```python
def check_result(marks):

    if marks >= 40:
        return "Pass"

    else:
        return "Fail"

print(check_result(75))
print(check_result(30))
```

**Output:**

```text
Pass
Fail
```

### Example 3: Calculate Grade

```python
def calculate_grade(marks):

    if marks >= 90:
        return "A+"

    elif marks >= 80:
        return "A"

    elif marks >= 70:
        return "B"

    elif marks >= 60:
        return "C"

    elif marks >= 40:
        return "D"

    else:
        return "F"

print(calculate_grade(95))
print(calculate_grade(75))
print(calculate_grade(35))
```

**Output:**

```text
A+
B
F
```

---

## 16. Functions With Loops

Functions can contain `for` and `while` loops.

### Example 1: Print Numbers

```python
def print_numbers():

    for i in range(1, 6):
        print(i)

print_numbers()
```

**Output:**

```text
1
2
3
4
5
```

### Example 2: Multiplication Table

```python
def multiplication_table(number):

    for i in range(1, 11):

        print(number, "x", i, "=", number * i)

multiplication_table(7)
```

### Example 3: Factorial

```python
def factorial(number):

    result = 1

    for i in range(1, number + 1):
        result *= i

    return result

print(factorial(5))
```

**Output:**

```text
120
```

This version assumes a non-negative integer input.

---

## 17. Functions Working With Collections

Functions can receive lists, tuples, sets and dictionaries as arguments.

### Example 1: Calculate List Sum

```python
def calculate_total(numbers):

    return sum(numbers)

marks = [80, 90, 85, 95]

print(calculate_total(marks))
```

**Output:**

```text
350
```

### Example 2: Find the Largest List Element

```python
def find_largest(numbers):

    if not numbers:
        return None

    return max(numbers)

numbers = [10, 50, 30, 90, 20]

print(find_largest(numbers))
```

**Output:**

```text
90
```

### Example 3: Count Even Numbers

```python
def count_even(numbers):

    count = 0

    for number in numbers:

        if number % 2 == 0:
            count += 1

    return count

numbers = [10, 15, 20, 25, 30, 35]

print("Even Count:", count_even(numbers))
```

**Output:**

```text
Even Count: 3
```

### Example 4: Search in a Dictionary

```python
def find_student(students, student_name):

    if student_name in students:
        return students[student_name]

    return "Student Not Found"

students = {
    "Raj": 90,
    "Rahul": 85,
    "Amit": 95
}

print(find_student(students, "Raj"))
print(find_student(students, "Neha"))
```

**Output:**

```text
90
Student Not Found
```

---

## 18. The pass Statement in Functions

The `pass` statement is a placeholder that performs no action.

It is useful when you want to define a function but implement it later.

### Example

```python
def calculate_salary():
    pass

def employee_details():
    pass

print("Program Started")
```

**Output:**

```text
Program Started
```

Without `pass`, an empty function body would produce an indentation or syntax error.

---

## 19. Function Documentation Using Docstrings

A docstring is a string written as the first statement inside a function.

It describes what the function does.

### Example

```python
def calculate_square(number):
    """
    Calculate the square of a number.
    """

    return number * number

print(calculate_square(5))
```

**Output:**

```text
25
```

### Accessing a Docstring

```python
print(calculate_square.__doc__)
```

**Output:**

```text
    Calculate the square of a number.
```

### Why Use Docstrings?

1. Explain the purpose of a function.
2. Improve code readability.
3. Help other developers understand the code.
4. Support documentation tools.

---

## 20. Variable Scope: Local and Global Variables

Variable scope determines where a variable can be accessed.

### Local Variables

A variable created inside a function is normally local to that function.

```python
def display():

    message = "Hello Python"

    print(message)

display()
```

**Output:**

```text
Hello Python
```

Trying to access `message` outside the function:

```python
def display():

    message = "Hello Python"

display()

print(message)
```

This produces a `NameError` because `message` is local to `display()`.

### Global Variables

A variable created outside functions is global at the module level.

```python
name = "Raj"

def display():

    print(name)

display()

print(name)
```

**Output:**

```text
Raj
Raj
```

A function can read a global variable without declaring it as `global`.

### Using the global Keyword

The `global` keyword allows a function to reassign a module-level global variable.

```python
count = 10

def update_count():

    global count

    count = 20

update_count()

print(count)
```

**Output:**

```text
20
```

### Important

You do not need `global` just to read a global variable.

You generally need it when assigning a new value to that global variable inside a function.

---

## 21. Function Aliasing

A function can be assigned to another variable.

Both names then refer to the same function object.

```python
def greet():

    print("Hello Student")

welcome = greet

greet()
welcome()
```

**Output:**

```text
Hello Student
Hello Student
```

This is called function aliasing.

---

## 22. Practical Programs

### Program 1: Basic Calculator Using Functions

```python
def add(a, b):
    return a + b

def subtract(a, b):
    return a - b

def multiply(a, b):
    return a * b

def divide(a, b):

    if b == 0:
        return "Cannot divide by zero"

    return a / b


num1 = float(input("Enter first number: "))
num2 = float(input("Enter second number: "))

print("Addition:", add(num1, num2))
print("Subtraction:", subtract(num1, num2))
print("Multiplication:", multiply(num1, num2))
print("Division:", divide(num1, num2))
```

### Program 2: Validate Email Input

```python
def validate_email(email):

    email = email.strip()

    if " " in email:
        return False

    if email.count("@") != 1:
        return False

    username, domain = email.split("@")

    if not username or not domain:
        return False

    if "." not in domain:
        return False

    if domain.startswith(".") or domain.endswith("."):
        return False

    return True


email = input("Enter Email: ")

if validate_email(email):
    print("Email Format Accepted")
else:
    print("Invalid Email Format")
```

This is a basic format check, not complete email validation.

### Program 3: Generate Fibonacci Series

```python
def fibonacci(count):

    first = 0
    second = 1

    for i in range(count):

        print(first, end=" ")

        first, second = second, first + second


fibonacci(10)
```

**Output:**

```text
0 1 1 2 3 5 8 13 21 34
```

### Program 4: Check Prime Number

```python
def is_prime(number):

    if number < 2:
        return False

    for i in range(2, int(number ** 0.5) + 1):

        if number % i == 0:
            return False

    return True


number = int(input("Enter a number: "))

if is_prime(number):
    print("Prime Number")
else:
    print("Not a Prime Number")
```

### Program 5: Password Validation

```python
def validate_password(password):

    if len(password) < 8:
        return False

    has_upper = False
    has_lower = False
    has_digit = False

    for char in password:

        if char.isupper():
            has_upper = True

        elif char.islower():
            has_lower = True

        elif char.isdigit():
            has_digit = True

    return has_upper and has_lower and has_digit


password = input("Enter Password: ")

if validate_password(password):
    print("Password Accepted")
else:
    print("Password Must Have:")
    print("- At Least 8 Characters")
    print("- One Uppercase Letter")
    print("- One Lowercase Letter")
    print("- One Digit")
```

---

# 23. Mini Project – Function-Based Student Management System

## Project Description

Build a Student Management System using separate functions for every major operation.

The application should support:

1. Add a student.
2. View all students.
3. Search for a student.
4. Update student marks.
5. Delete a student.
6. Calculate class statistics.
7. Exit.

### Complete Code

```python
students = {}


def add_student():

    student_id = input("Enter Student ID: ").strip()

    if not student_id:
        print("Student ID cannot be empty.")
        return

    if student_id in students:
        print("Student ID Already Exists.")
        return

    name = input("Enter Student Name: ").strip()

    if not name:
        print("Name cannot be empty.")
        return

    try:
        marks = float(input("Enter Marks: "))

        if not 0 <= marks <= 100:
            print("Marks must be between 0 and 100.")
            return

    except ValueError:
        print("Marks must be numeric.")
        return

    students[student_id] = {
        "name": name,
        "marks": marks
    }

    print("Student Added Successfully.")


def view_students():

    if not students:
        print("No Student Records Found.")
        return

    for student_id, details in students.items():

        print("\nStudent ID:", student_id)
        print("Name:", details["name"])
        print("Marks:", details["marks"])


def search_student():

    student_id = input("Enter Student ID: ").strip()

    student = students.get(student_id)

    if student is None:
        print("Student Not Found.")
        return

    print("\nStudent Found")
    print("Name:", student["name"])
    print("Marks:", student["marks"])


def update_student():

    student_id = input("Enter Student ID: ").strip()

    if student_id not in students:
        print("Student Not Found.")
        return

    try:
        marks = float(input("Enter New Marks: "))

        if not 0 <= marks <= 100:
            print("Marks must be between 0 and 100.")
            return

    except ValueError:
        print("Invalid Marks.")
        return

    students[student_id]["marks"] = marks

    print("Marks Updated Successfully.")


def delete_student():

    student_id = input("Enter Student ID: ").strip()

    if student_id not in students:
        print("Student Not Found.")
        return

    confirm = input("Confirm Delete? (yes/no): ").strip().lower()

    if confirm == "yes":

        del students[student_id]

        print("Student Deleted Successfully.")

    else:
        print("Deletion Cancelled.")


def class_statistics():

    if not students:
        print("No Student Records Available.")
        return

    marks = [
        student["marks"]
        for student in students.values()
    ]

    total = sum(marks)
    average = total / len(marks)

    highest = max(marks)
    lowest = min(marks)

    print("\n===== CLASS STATISTICS =====")

    print("Total Students:", len(students))
    print("Total Marks:", total)
    print("Average Marks:", round(average, 2))
    print("Highest Marks:", highest)
    print("Lowest Marks:", lowest)


def main():

    while True:

        print("\n===== STUDENT MANAGEMENT SYSTEM =====")

        print("1. Add Student")
        print("2. View Students")
        print("3. Search Student")
        print("4. Update Student")
        print("5. Delete Student")
        print("6. Class Statistics")
        print("7. Exit")

        choice = input("Enter Choice: ").strip()

        if choice == "1":
            add_student()

        elif choice == "2":
            view_students()

        elif choice == "3":
            search_student()

        elif choice == "4":
            update_student()

        elif choice == "5":
            delete_student()

        elif choice == "6":
            class_statistics()

        elif choice == "7":
            print("Thank You!")
            break

        else:
            print("Invalid Choice. Try Again.")


main()
```

## Project Concepts Used

- Function definition and function calls.
- Parameters and arguments.
- Return statements.
- Local and global variables.
- Dictionaries and nested collections.
- Conditional statements.
- Loops.
- Input validation.
- Exception handling.
- Breaking a large application into smaller functions.

## Why Did We Use Functions?

Instead of writing all application logic inside one large `while` loop, we divided the application into separate operations.

For example:

- `add_student()` handles adding records.
- `view_students()` handles displaying records.
- `search_student()` handles searching.
- `update_student()` handles updating.
- `delete_student()` handles deletion.
- `class_statistics()` calculates statistics.
- `main()` controls the application.

This makes the program easier to read, test, debug and maintain.

---

# 24. Student Practice Exercises

## Beginner Level

1. Create a function that prints your name.
2. Create a function that displays a welcome message.
3. Create a function that prints numbers from 1 to 10.
4. Create a function that accepts one number and prints its square.
5. Create a function that accepts two numbers and prints their sum.
6. Create a function that displays student information.
7. Create a function that prints a multiplication table.
8. Create a function that calculates rectangle area.

## Intermediate Level

9. Create a function that returns the largest of three numbers.
10. Create a function that checks whether a number is even or odd.
11. Create a function that calculates factorial.
12. Create a function that checks whether a number is prime.
13. Create a function that returns the average of a list.
14. Create a function that counts vowels in a string.
15. Create a function that checks whether a string is a palindrome.
16. Create a function that accepts a dictionary and searches for a particular key.
17. Create a function that returns the total, average and highest marks.
18. Create a function with default parameters for employee information.

## Advanced Level

19. Create a calculator using separate functions.
20. Create a password validation function.
21. Create a function that generates a Fibonacci series.
22. Create a function that returns all prime numbers within a range.
23. Create a function that removes duplicate values from a list.
24. Create a function that groups employees by department.
25. Build a menu-driven Library Management System using functions.

---

# 25. Trainer Assessment

The trainer should verify that the student can independently:

- [ ] Explain what a function is and why it is used.
- [ ] Differentiate built-in and user-defined functions.
- [ ] Define and call functions using `def`.
- [ ] Create functions with and without parameters.
- [ ] Differentiate parameters and arguments.
- [ ] Use positional and keyword arguments.
- [ ] Create functions with default parameters.
- [ ] Explain the difference between `print()` and `return`.
- [ ] Return single and multiple values.
- [ ] Use conditions and loops inside functions.
- [ ] Pass lists and dictionaries to functions.
- [ ] Explain local and global scope.
- [ ] Write basic docstrings.
- [ ] Divide a large program into smaller functions.
- [ ] Build the Student Management System independently.

## Completion Criteria

The day is considered complete when:

1. All practical examples have been executed.
2. All beginner exercises have been completed.
3. At least 10 intermediate and advanced exercises have been attempted.
4. The Student Management System works correctly.
5. The student can explain parameters, arguments and return values.
6. The student can independently create and call reusable functions.
7. The student can divide a program into logical functions.

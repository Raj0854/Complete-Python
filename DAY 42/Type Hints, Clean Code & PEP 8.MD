
# Day 42 – Type Hints, Clean Code & PEP 8

## 1. Introduction to Clean Code

Clean code means writing code that is:

- Easy to read.
- Easy to understand.
- Easy to maintain.
- Easy to test.
- Easy to modify.
- Consistent in structure and style.

Python code can work correctly even if it is poorly written. However, professional development requires more than just getting the correct output.

### Example: Poorly Written Code

```python
x = 100
y = 5
z = x * y
print(z)
```

This code works, but its purpose is not immediately clear.

### Improved Code

```python
product_price = 100
quantity = 5

total_amount = product_price * quantity

print(total_amount)
```

Output:

```text
500
```

The second version communicates the purpose of each variable.

### Important Clean Code Principles

1. Use meaningful variable and function names.
2. Keep functions focused on one responsibility.
3. Avoid unnecessary code duplication.
4. Keep code properly formatted.
5. Use comments only when they add useful information.
6. Handle errors appropriately.
7. Use type hints where they improve clarity.
8. Keep functions reasonably small.
9. Avoid unnecessary complexity.
10. Follow consistent coding conventions.

---

## 2. Introduction to PEP 8

PEP stands for Python Enhancement Proposal.

PEP 8 is the official Python style guide. It provides recommendations for writing consistent and readable Python code.

PEP 8 is primarily a style guide. Following it does not automatically make a program logically correct.

### 2.1 Indentation

Python uses indentation to define code blocks.

PEP 8 recommends using four spaces per indentation level.

Incorrect:

```python
if True:
  print("Hello")
```

Recommended:

```python
if True:
    print("Hello")
```

Avoid mixing tabs and spaces.

### 2.2 Line Length

Traditional PEP 8 recommends:

- Maximum 79 characters for code lines.
- Maximum 72 characters for comments and docstrings.

Modern projects may configure different limits through formatting tools.

Long line:

```python
student_name = "Raj" + " " + "Gupta" + " " + "Python Developer"
```

Improved:

```python
student_name = (
    "Raj"
    + " "
    + "Gupta"
    + " "
    + "Python Developer"
)
```

### 2.3 Blank Lines

Use blank lines to separate logical sections.

PEP 8 generally recommends:

- Two blank lines between top-level functions and classes.
- One blank line between methods inside a class.

Example:

```python
def calculate_total(price, quantity):
    return price * quantity


def calculate_discount(amount, discount):
    return amount * discount / 100


class Student:
    def __init__(self, name):
        self.name = name
```

### 2.4 Spaces Around Operators

Recommended:

```python
total = price + tax
average = total / count

if total > 100:
    print("Eligible")
```

Avoid:

```python
total=price+tax
average=total/count

if total>100:
    print("Eligible")
```

### 2.5 Spaces After Commas

Recommended:

```python
numbers = [10, 20, 30, 40]

student = {
    "name": "Amit",
    "age": 22
}
```

Avoid:

```python
numbers = [10,20,30,40]
```

### 2.6 Avoid Unnecessary Whitespace

Recommended:

```python
name = "Amit"
numbers = [10, 20, 30]

result = calculate_total(100, 5)
```

Avoid:

```python
name     =     "Amit"

numbers = [ 10, 20, 30 ]

result = calculate_total( 100, 5 )
```

---

## 3. Python Naming Conventions

Naming conventions help developers understand the purpose of variables, functions, classes and constants.

### 3.1 Variables – snake_case

Use lowercase words separated by underscores.

```python
student_name = "Amit"
total_marks = 450
account_balance = 5000
```

### 3.2 Functions – snake_case

```python
def calculate_average():
    pass


def get_student_details():
    pass


def validate_email():
    pass
```

### 3.3 Classes – PascalCase

Each word starts with a capital letter.

```python
class Student:
    pass


class BankAccount:
    pass


class EmployeeManagementSystem:
    pass
```

### 3.4 Constants – UPPER_CASE

Constants are generally written using uppercase letters and underscores.

```python
PI = 3.14159
MAX_ATTEMPTS = 5
COMPANY_NAME = "ABC Technologies"
```

Python does not enforce constants. This is a naming convention.

### 3.5 Private Attributes – Leading Underscore

A single leading underscore indicates that an attribute or method is intended for internal use.

```python
class BankAccount:

    def __init__(self, balance):
        self._balance = balance
```

It is a convention, not strict access control.

### 3.6 Avoid Shadowing Built-in Names

Do not use names of important Python built-ins as variable names.

Avoid:

```python
list = [10, 20, 30]
str = "Hello"
sum = 100
```

Better:

```python
numbers = [10, 20, 30]
message = "Hello"
total = 100
```

Shadowing a built-in can make its original function inaccessible in the current scope.

---

## 4. Comments and Documentation

Comments explain parts of the code that may not be obvious.

### 4.1 Single-Line Comments

Use `#` for comments.

```python
# Calculate the final price
price = 1000
tax = 100

final_price = price + tax
```

### 4.2 Inline Comments

```python
total = 1000  # Total amount before discount
```

Use inline comments only when they add useful context.

### 4.3 Avoid Unnecessary Comments

Poor example:

```python
# Add two numbers
result = 10 + 20
```

The code is already clear.

Better:

```python
result = 10 + 20
```

### 4.4 Docstrings

A docstring documents a module, class or function.

Docstrings are written using triple quotes.

```python
def calculate_area(length, width):
    """
    Calculate the area of a rectangle.

    Args:
        length: Rectangle length.
        width: Rectangle width.

    Returns:
        Area of the rectangle.
    """
    return length * width


print(calculate_area(10, 5))
```

Output:

```text
50
```

Access a docstring:

```python
print(calculate_area.__doc__)
```

### 4.5 Class Docstrings

```python
class Student:
    """
    Represent a student and store basic student information.
    """

    def __init__(self, name, marks):
        self.name = name
        self.marks = marks
```

---

## 5. Introduction to Type Hints

Python is dynamically typed.

This means a variable can refer to values of different types during program execution.

Example:

```python
value = 100
print(value)

value = "Python"
print(value)
```

Output:

```text
100
Python
```

Python also supports type hints, which allow developers to indicate the expected data types.

Type hints improve:

- Code readability.
- Editor suggestions.
- Static error detection.
- Documentation.
- Collaboration between developers.

### Important Point

Type hints do not automatically enforce data types at runtime.

Example:

```python
age: int = 25

age = "Twenty Five"

print(age)
```

Python executes this code normally, although a static type checker can report a type mismatch.

---

## 6. Basic Type Annotations

### 6.1 Integer

```python
age: int = 22
total_students: int = 50
```

### 6.2 Float

```python
price: float = 99.50
percentage: float = 85.5
```

### 6.3 String

```python
student_name: str = "Amit"
city: str = "Mumbai"
```

### 6.4 Boolean

```python
is_active: bool = True
is_passed: bool = False
```

### 6.5 None

Use `None` when a value represents the absence of a result.

```python
result: None = None
```

More commonly, a function returning no meaningful value is annotated with `-> None`.

---

## 7. Type Hints in Functions

Type hints can describe both function parameters and return values.

Syntax:

```python
def function_name(parameter: data_type) -> return_type:
    pass
```

Example:

```python
def calculate_sum(a: int, b: int) -> int:
    return a + b


result = calculate_sum(10, 20)

print(result)
```

Output:

```text
30
```

### Multiple Parameters

```python
def calculate_bill(
    price: float,
    quantity: int
) -> float:

    return price * quantity


print(calculate_bill(99.50, 3))
```

Output:

```text
298.5
```

### Function Returning Nothing

```python
def display_message(message: str) -> None:
    print(message)


display_message("Welcome to Python")
```

Output:

```text
Welcome to Python
```

### Function with Multiple Return Values

```python
def calculate_statistics(
    a: int,
    b: int
) -> tuple[int, int]:

    return a + b, a * b


total, product = calculate_statistics(10, 5)

print("Total:", total)
print("Product:", product)
```

Output:

```text
Total: 15
Product: 50
```

---

## 8. Type Hints for Collections

Python 3.9+ supports built-in collection types in annotations.

### 8.1 List

```python
marks: list[int] = [80, 85, 90, 95]

names: list[str] = [
    "Amit",
    "Raj",
    "Neha"
]
```

### 8.2 Tuple

```python
student: tuple[str, int, float] = (
    "Amit",
    21,
    85.5
)
```

The annotation describes the expected type and position of each tuple element.

For a tuple containing any number of integers:

```python
numbers: tuple[int, ...] = (10, 20, 30, 40)
```

### 8.3 Set

```python
unique_numbers: set[int] = {
    10,
    20,
    30
}
```

### 8.4 Dictionary

```python
student_marks: dict[str, int] = {
    "Amit": 85,
    "Raj": 90,
    "Neha": 95
}
```

Here:

- Dictionary keys are expected to be strings.
- Dictionary values are expected to be integers.

### 8.5 Nested Collections

```python
students: list[dict[str, int | str]] = [
    {
        "name": "Amit",
        "marks": 85
    },
    {
        "name": "Raj",
        "marks": 90
    }
]
```

The `|` operator represents a union of types in Python 3.10+.

---

## 9. Optional and Union Types

Sometimes a variable can contain more than one possible data type.

### 9.1 Union Types

Python 3.10+ supports the `|` operator.

```python
student_id: int | str

student_id = 101
student_id = "STU101"
```

The annotation means the value may be an integer or a string.

### 9.2 Optional Values

Sometimes a function may return a value or `None`.

```python
def find_student(
    student_id: int
) -> str | None:

    if student_id == 101:
        return "Amit"

    return None


result = find_student(101)

print(result)
```

Output:

```text
Amit
```

Before using the returned value, check whether it is `None`.

```python
if result is not None:
    print(result.upper())
else:
    print("Student not found")
```

### 9.3 Older Optional Syntax

The `Optional` type from the `typing` module is another way to express a value that may be `None`.

```python
from typing import Optional


def get_name(student_id: int) -> Optional[str]:
    if student_id == 101:
        return "Amit"

    return None
```

`Optional[str]` means `str | None`.

---

## 10. Any, Literal and Final

These annotations are available through the `typing` module.

### 10.1 Any

`Any` allows a value to have any type from the perspective of the type checker.

```python
from typing import Any

data: Any = 100

data = "Python"
data = [10, 20, 30]
```

Use `Any` carefully. Too much use reduces the benefits of type checking.

### 10.2 Literal

`Literal` restricts an annotation to specific allowed values.

```python
from typing import Literal


def set_status(
    status: Literal["active", "inactive", "pending"]
) -> None:

    print("Status:", status)


set_status("active")
```

A static type checker can report an error for an unsupported literal such as `"unknown"`.

### 10.3 Final

`Final` indicates that a variable is intended not to be reassigned.

```python
from typing import Final

MAX_USERS: Final[int] = 100
COMPANY_NAME: Final[str] = "ABC Technologies"
```

A type checker can report reassignment of a `Final` variable. Python does not enforce it at runtime.

---

## 11. Type Aliases

A type alias gives a descriptive name to an existing type.

Example:

```python
StudentRecord = dict[str, int | str]

student: StudentRecord = {
    "name": "Amit",
    "age": 21,
    "marks": 85
}

print(student)
```

Output:

```text
{'name': 'Amit', 'age': 21, 'marks': 85}
```

Type aliases make complex annotations easier to read.

Python 3.12+ also supports the `type` statement:

```python
type StudentRecord = dict[str, int | str]
```

For earlier Python versions, ordinary assignment is commonly used for type aliases.

---

## 12. Type Hints with Classes

Type hints can also be used with class attributes and methods.

```python
class Student:

    school_name: str = "ABC School"

    def __init__(
        self,
        name: str,
        age: int,
        marks: float
    ) -> None:

        self.name: str = name
        self.age: int = age
        self.marks: float = marks

    def display_details(self) -> None:

        print("Name:", self.name)
        print("Age:", self.age)
        print("Marks:", self.marks)


student = Student("Amit", 21, 88.5)

student.display_details()
```

Output:

```text
Name: Amit
Age: 21
Marks: 88.5
```

### ClassVar

`ClassVar` identifies an attribute intended to belong to the class rather than individual instances.

```python
from typing import ClassVar


class Employee:

    company_name: ClassVar[str] = "ABC Technologies"

    def __init__(self, name: str) -> None:
        self.name = name
```

---

## 13. TypedDict for Structured Dictionaries

Sometimes a dictionary is expected to contain specific keys with specific value types.

`TypedDict` helps describe that structure.

```python
from typing import TypedDict


class Student(TypedDict):
    name: str
    age: int
    marks: float


student: Student = {
    "name": "Amit",
    "age": 21,
    "marks": 88.5
}

print(student["name"])
print(student["marks"])
```

Output:

```text
Amit
88.5
```

A static type checker can identify missing required keys or incorrectly typed values.

`TypedDict` does not validate dictionary contents automatically at runtime.

---

## 14. Callable, Iterable and Sequence

Python provides reusable abstract type annotations through `typing` and `collections.abc`.

### 14.1 Callable

`Callable` describes a function or another callable object.

```python
from collections.abc import Callable


def calculate(
    a: int,
    b: int,
    operation: Callable[[int, int], int]
) -> int:

    return operation(a, b)


def add(a: int, b: int) -> int:
    return a + b


result = calculate(10, 20, add)

print(result)
```

Output:

```text
30
```

### 14.2 Iterable

`Iterable` describes an object that can be iterated over.

```python
from collections.abc import Iterable


def display_items(items: Iterable[str]) -> None:

    for item in items:
        print(item)


display_items(["Python", "Java", "C++"])
```

Output:

```text
Python
Java
C++
```

### 14.3 Sequence

`Sequence` describes an ordered collection that supports indexing and iteration.

```python
from collections.abc import Sequence


def display_first_item(items: Sequence[str]) -> None:

    if items:
        print(items[0])


display_first_item(["Python", "Java", "C++"])
```

Output:

```text
Python
```

Unlike `list`, a `Sequence` annotation can accept other compatible sequence types, such as tuples.

---

## 15. Type Narrowing with isinstance()

Type narrowing means checking a value's actual type so that the program can safely use operations appropriate for that type.

Example:

```python
def display_value(value: int | str) -> None:

    if isinstance(value, int):
        print("Integer:", value * 2)

    elif isinstance(value, str):
        print("String:", value.upper())


display_value(10)
display_value("python")
```

Output:

```text
Integer: 20
String: PYTHON
```

A static type checker understands the checks and can narrow the type inside each branch.

---

## 16. Static Type Checking with mypy

Python does not enforce type hints automatically.

Static type checkers analyze code and identify possible type errors without running the program.

Popular tools include:

- mypy
- Pyright
- BasedPyright

### 16.1 Install mypy

Run:

```bash
python -m pip install mypy
```

### 16.2 Create a File

Create `type_check_demo.py`.

```python
def calculate_total(
    price: float,
    quantity: int
) -> float:

    return price * quantity


total = calculate_total(100.0, 5)

print(total)
```

### 16.3 Run the Program

```bash
python type_check_demo.py
```

Output:

```text
500.0
```

### 16.4 Run mypy

```bash
python -m mypy type_check_demo.py
```

A successful check should report no issues.

### 16.5 Introduce a Type Error

Modify the function call:

```python
total = calculate_total("100", 5)
```

The Python interpreter may execute this expression successfully because multiplying a string by an integer is valid.

However, mypy can report that a string was supplied where a float was expected.

### Important Difference

| Runtime Python | Static Type Checker |
|---|---|
| Executes the program | Analyzes source code |
| Checks actual runtime behavior | Checks declared type consistency |
| Does not enforce annotations by default | Reports possible annotation errors |
| May reveal errors during execution | Can identify many errors before execution |

Type hints are not a replacement for input validation.

For example, external input should still be validated using appropriate checks and conversions.

---

## 17. Formatting and Linting Tools

Professional Python projects commonly use automated tools to maintain code quality.

### 17.1 Formatter

A formatter automatically adjusts code formatting.

Popular formatter:

- Black
- Ruff Formatter

Install Black:

```bash
python -m pip install black
```

Format a file:

```bash
python -m black main.py
```

Format the complete project:

```bash
python -m black .
```

### 17.2 Linter

A linter identifies style problems, suspicious code and common programming mistakes.

Popular linter:

- Ruff
- Pylint

Install Ruff:

```bash
python -m pip install ruff
```

Check a file:

```bash
python -m ruff check main.py
```

Automatically fix supported issues:

```bash
python -m ruff check main.py --fix
```

### 17.3 Ruff Formatter

Ruff can also format Python files.

```bash
python -m ruff format main.py
```

Format all Python files in the current project:

```bash
python -m ruff format .
```

### 17.4 Formatter vs Linter vs Type Checker

| Tool | Main Responsibility |
|---|---|
| Black | Code formatting |
| Ruff Formatter | Code formatting |
| Ruff Linter | Style and code-quality checks |
| mypy | Static type checking |
| Pyright | Static type checking |

These tools solve different problems and can be used together.

---

## 18. Refactoring Code

Refactoring means improving the internal structure of existing code without intentionally changing its external behavior.

### Example: Before Refactoring

```python
n = ["Amit", "Raj", "Neha"]
m = [80, 90, 75]

for i in range(len(n)):
    if m[i] >= 80:
        print(n[i], "Passed")
```

Problems:

- Unclear variable names.
- Related student data is stored separately.
- Logic is directly inside the loop.
- No type hints.
- No reusable function.

### After Refactoring

```python
def display_passed_students(
    student_names: list[str],
    student_marks: list[int]
) -> None:
    """
    Display students whose marks are at least 80.
    """

    for name, marks in zip(student_names, student_marks):

        if marks >= 80:
            print(f"{name} Passed")


names = ["Amit", "Raj", "Neha"]
marks = [80, 90, 75]

display_passed_students(names, marks)
```

Output:

```text
Amit Passed
Raj Passed
```

The refactored code is easier to understand and reuse.

---

## 19. Practical Programs

### Program 1: Type-Annotated Calculator

```python
def add(a: float, b: float) -> float:
    return a + b


def subtract(a: float, b: float) -> float:
    return a - b


def multiply(a: float, b: float) -> float:
    return a * b


def divide(a: float, b: float) -> float:

    if b == 0:
        raise ValueError("Cannot divide by zero")

    return a / b


print("Addition:", add(10, 5))
print("Subtraction:", subtract(10, 5))
print("Multiplication:", multiply(10, 5))
print("Division:", divide(10, 5))
```

Output:

```text
Addition: 15
Subtraction: 5
Multiplication: 50
Division: 2.0
```

### Program 2: Student Average Calculator

```python
def calculate_average(marks: list[float]) -> float:

    if not marks:
        return 0.0

    return sum(marks) / len(marks)


student_marks = [85.5, 90.0, 78.5, 88.0]

average = calculate_average(student_marks)

print(f"Average Marks: {average:.2f}")
```

Output:

```text
Average Marks: 85.50
```

### Program 3: Employee Salary Calculator

```python
def calculate_salary(
    basic_salary: float,
    allowance: float,
    deduction: float
) -> float:

    return basic_salary + allowance - deduction


salary = calculate_salary(
    basic_salary=30000,
    allowance=5000,
    deduction=2000
)

print("Final Salary:", salary)
```

Output:

```text
Final Salary: 33000
```

### Program 4: Validate and Process User Data

```python
def process_age(age: int | str) -> str:

    if isinstance(age, str):

        if not age.isdigit():
            return "Invalid age"

        age = int(age)

    if age < 0:
        return "Age cannot be negative"

    if age >= 18:
        return "Eligible"

    return "Not eligible"


print(process_age("22"))
print(process_age("15"))
print(process_age("hello"))
```

Output:

```text
Eligible
Not eligible
Invalid age
```

### Program 5: Typed Dictionary

```python
from typing import TypedDict


class Product(TypedDict):
    product_name: str
    price: float
    quantity: int


def calculate_product_value(product: Product) -> float:

    return product["price"] * product["quantity"]


item: Product = {
    "product_name": "Keyboard",
    "price": 1200.0,
    "quantity": 2
}

print("Product:", item["product_name"])
print("Total Value:", calculate_product_value(item))
```

Output:

```text
Product: Keyboard
Total Value: 2400.0
```

---

## 20. Mini Project – Professional Student Report Management System

### Project Description

Build a student report management application using clean code, type hints, PEP 8 conventions and proper documentation.

The project must store student records, calculate results and generate reports.

### Project Structure

```text
Day-42/
│
├── student_report.py
└── README.md
```

### Required Features

1. Add student records.
2. Display all students.
3. Search student by ID.
4. Update student marks.
5. Delete student records.
6. Calculate total marks.
7. Calculate average marks.
8. Assign grades.
9. Display passed students.
10. Generate a complete student report.

### Implementation

Create `student_report.py`.

```python
from typing import TypedDict


class Student(TypedDict):
    student_id: int
    name: str
    marks: list[float]


students: dict[int, Student] = {}


def calculate_total(marks: list[float]) -> float:
    """Calculate the total marks of a student."""

    return sum(marks)


def calculate_average(marks: list[float]) -> float:
    """Calculate average marks."""

    if not marks:
        return 0.0

    return sum(marks) / len(marks)


def calculate_grade(average: float) -> str:
    """Return a grade based on the average marks."""

    if average >= 90:
        return "A"

    if average >= 80:
        return "B"

    if average >= 70:
        return "C"

    if average >= 60:
        return "D"

    return "F"


def add_student(
    student_id: int,
    name: str,
    marks: list[float]
) -> bool:
    """Add a new student record."""

    if student_id in students:
        return False

    if not name.strip():
        return False

    if not marks:
        return False

    if any(mark < 0 or mark > 100 for mark in marks):
        return False

    students[student_id] = {
        "student_id": student_id,
        "name": name.strip(),
        "marks": marks.copy()
    }

    return True


def display_students() -> None:
    """Display all student records."""

    if not students:
        print("No student records found.")
        return

    for student in students.values():

        average = calculate_average(student["marks"])
        grade = calculate_grade(average)

        print("\nStudent ID:", student["student_id"])
        print("Name:", student["name"])
        print("Marks:", student["marks"])
        print("Total:", calculate_total(student["marks"]))
        print("Average:", round(average, 2))
        print("Grade:", grade)


def search_student(student_id: int) -> Student | None:
    """Find a student using their ID."""

    return students.get(student_id)


def update_marks(
    student_id: int,
    new_marks: list[float]
) -> bool:
    """Update marks for an existing student."""

    student = students.get(student_id)

    if student is None:
        return False

    if not new_marks:
        return False

    if any(mark < 0 or mark > 100 for mark in new_marks):
        return False

    student["marks"] = new_marks.copy()

    return True


def delete_student(student_id: int) -> bool:
    """Delete a student record."""

    if student_id not in students:
        return False

    del students[student_id]

    return True


def display_passed_students() -> None:
    """Display students with an average of at least 40."""

    for student in students.values():

        average = calculate_average(student["marks"])

        if average >= 40:
            print(student["name"], "-", round(average, 2))


def main() -> None:
    """Run the student report management application."""

    while True:

        print("\n===== STUDENT REPORT SYSTEM =====")
        print("1. Add Student")
        print("2. Display Students")
        print("3. Search Student")
        print("4. Update Marks")
        print("5. Delete Student")
        print("6. Display Passed Students")
        print("7. Exit")

        choice = input("Enter choice: ").strip()

        if choice == "1":

            try:
                student_id = int(input("Enter student ID: "))
                name = input("Enter student name: ")

                marks_input = input(
                    "Enter marks separated by commas: "
                )

                marks = [
                    float(mark.strip())
                    for mark in marks_input.split(",")
                ]

                if add_student(student_id, name, marks):
                    print("Student added successfully.")
                else:
                    print("Invalid data or duplicate student ID.")

            except ValueError:
                print("Please enter valid numeric values.")

        elif choice == "2":
            display_students()

        elif choice == "3":

            try:
                student_id = int(input("Enter student ID: "))
                student = search_student(student_id)

                if student is not None:
                    print("Student:", student)
                else:
                    print("Student not found.")

            except ValueError:
                print("Invalid student ID.")

        elif choice == "4":

            try:
                student_id = int(input("Enter student ID: "))

                marks_input = input(
                    "Enter new marks separated by commas: "
                )

                marks = [
                    float(mark.strip())
                    for mark in marks_input.split(",")
                ]

                if update_marks(student_id, marks):
                    print("Marks updated successfully.")
                else:
                    print("Student not found or invalid marks.")

            except ValueError:
                print("Please enter valid numeric values.")

        elif choice == "5":

            try:
                student_id = int(input("Enter student ID: "))

                if delete_student(student_id):
                    print("Student deleted successfully.")
                else:
                    print("Student not found.")

            except ValueError:
                print("Invalid student ID.")

        elif choice == "6":
            display_passed_students()

        elif choice == "7":
            print("Application closed.")
            break

        else:
            print("Invalid choice. Try again.")


if __name__ == "__main__":
    main()
```

### Sample Testing

Add these records through the application:

```text
Student ID: 101
Name: Amit
Marks: 85,90,80

Student ID: 102
Name: Neha
Marks: 95,92,98
```

Expected report:

```text
Student ID: 101
Name: Amit
Marks: [85.0, 90.0, 80.0]
Total: 255.0
Average: 85.0
Grade: B

Student ID: 102
Name: Neha
Marks: [95.0, 92.0, 98.0]
Total: 285.0
Average: 95.0
Grade: A
```

### Project Quality Requirements

The student must ensure:

- All functions have meaningful names.
- Function parameters and return values have type hints.
- Classes and functions have useful docstrings where appropriate.
- Variables follow naming conventions.
- Indentation and spacing follow PEP 8.
- Duplicate student IDs are rejected.
- Marks outside the 0–100 range are rejected.
- Functions have focused responsibilities.
- The program has no unnecessary code duplication.
- Type-checking and linting tools are run.

### Run the Project

```bash
python student_report.py
```

### Check Type Hints

Install mypy:

```bash
python -m pip install mypy
```

Run:

```bash
python -m mypy student_report.py
```

### Check Code Quality

Install Ruff:

```bash
python -m pip install ruff
```

Run:

```bash
python -m ruff check student_report.py
```

Format the file:

```bash
python -m ruff format student_report.py
```

---

## 21. Student Practice Exercises

### Beginner Level

1. Create variables with appropriate type annotations.
2. Write a function that accepts two integers and returns their sum.
3. Write a function that accepts a name and returns a greeting.
4. Create a list of integers with a type annotation.
5. Create a dictionary containing student names and marks.
6. Write a function that returns `None`.
7. Write a class with annotated attributes.

### Intermediate Level

8. Create a function that accepts `int | float` and returns the square.
9. Create a function that accepts a list of integers and returns the average.
10. Use `TypedDict` to describe an employee record.
11. Use `Literal` to restrict an order status.
12. Create a function that accepts a `Callable` as an argument.
13. Write a function that safely handles a value of type `int | str`.
14. Use `Final` for application configuration constants.

### Advanced Level

15. Refactor an unformatted Python program using PEP 8.
16. Add type hints to an existing Student Management System.
17. Create meaningful docstrings for all functions.
18. Run mypy and fix reported type errors.
19. Run Ruff and fix linting issues.
20. Refactor a large function into smaller reusable functions.

---

## 22. Trainer Assessment

The trainer should evaluate the student on the following:

| Assessment Area | Expected Performance |
|---|---|
| Clean Code | Writes readable and maintainable code |
| PEP 8 | Follows naming, indentation and spacing conventions |
| Type Hints | Correctly annotates variables and functions |
| Collections | Uses appropriate generic collection annotations |
| Optional and Union | Understands multiple possible types |
| TypedDict | Describes structured dictionaries |
| Docstrings | Documents functions and classes |
| Refactoring | Improves code without changing intended behavior |
| mypy | Runs static type checks and fixes errors |
| Ruff | Runs linting and formatting tools |
| Mini Project | Completes all required features |

---

## 23. Completion Criteria

Day 42 is complete when the student can:

- Explain clean code and PEP 8.
- Follow Python naming conventions.
- Write properly formatted Python programs.
- Add type hints to variables and functions.
- Annotate lists, tuples, sets and dictionaries.
- Use Union, Optional, Any and Literal.
- Understand TypedDict and Callable.
- Explain why type hints are not runtime validation.
- Use docstrings appropriately.
- Refactor poorly structured code.
- Run mypy for static type checking.
- Run Ruff for linting and formatting.
- Complete the Student Report Management System.

**Day 42 Completed – Type Hints, Clean Code & PEP 8**


# Day 23 – Python Modules & Packages

## 1. Introduction to Modules

So far, we have written most of our Python programs inside a single `.py` file.

As a project grows, keeping all the code in one file creates problems:

- Code becomes difficult to manage.
- Finding errors becomes harder.
- Reusing code in another project becomes difficult.
- Multiple developers cannot easily work on separate parts.

Python solves this problem through **Modules and Packages**.

### What is a Module?

A module is simply a Python file (`.py`) containing code such as:

- Variables
- Functions
- Classes
- Statements

We can import a module into another Python file and reuse its code.

Example:

```python
# calculator.py

def add(a, b):
    return a + b

def subtract(a, b):
    return a - b
```

We can use these functions from another Python file without rewriting them.

---

## 2. Module vs Package vs Library

These three terms are related but not identical.

| Term | Meaning | Example |
|---|---|---|
| Module | A single Python file | calculator.py |
| Package | A directory organizing related modules | student_management/ |
| Library | A collection of reusable code, often containing multiple modules or packages | Python standard library, Requests |

### Example Structure

```text
project/
│
├── main.py
│
├── calculator.py
│
└── student_management/
    ├── __init__.py
    ├── operations.py
    └── reports.py
```

Here:

- `calculator.py` is a module.
- `student_management` is a package.
- `operations.py` and `reports.py` are modules inside that package.

---

## 3. Creating Your First Custom Module

Let's create two Python files.

### File 1: calculator.py

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
```

### File 2: main.py

```python
import calculator

print(calculator.add(10, 5))
print(calculator.subtract(10, 5))
print(calculator.multiply(10, 5))
print(calculator.divide(10, 5))
```

### Output

```text
15
5
50
2.0
```

### Understanding

```python
import calculator
```

Imports the `calculator` module.

```python
calculator.add(10, 5)
```

Calls the `add()` function from that module.

The dot (`.`) is used to access members of a module.

**Important:** Keep both files in the same directory for this example.

Run the program from that directory:

```bash
python main.py
```

---

## 4. Different Ways to Import Modules

Python provides several ways to import modules and their contents.

### 4.1 Import the Entire Module

```python
import math

print(math.sqrt(25))
print(math.pi)
```

Output:

```text
5.0
3.141592653589793
```

We access module members using the module name.

### 4.2 Import with an Alias

We can give a shorter name to a module using `as`.

```python
import math as m

print(m.sqrt(64))
print(m.factorial(5))
```

Output:

```text
8.0
120
```

Here, `m` is the alias of the `math` module.

### 4.3 Import Specific Functions

Instead of importing the entire module, we can import only the functions we need.

```python
from math import sqrt, factorial

print(sqrt(49))
print(factorial(5))
```

Output:

```text
7.0
120
```

Notice that we do not need to write `math.sqrt()`.

### 4.4 Import a Function with an Alias

```python
from math import factorial as fact

print(fact(6))
```

Output:

```text
720
```

### 4.5 Import Everything Using Wildcard

```python
from math import *

print(sqrt(36))
print(factorial(4))
```

Output:

```text
6.0
24
```

This imports names that the module makes available for wildcard imports.

**Why should we avoid wildcard imports?**

- It becomes unclear where a function came from.
- Names can overwrite each other.
- It makes debugging difficult.
- It can make code less readable.

Prefer explicit imports:

```python
from math import sqrt, factorial
```

---

## 5. Importing Multiple Modules

We can import multiple modules in the same program.

```python
import math
import random
import datetime

print(math.sqrt(100))

print(random.randint(1, 10))

print(datetime.date.today())
```

Output will vary because the random number and date depend on execution time.

We can also write:

```python
import math, random
```

However, separate import statements are generally easier to read.

---

## 6. Understanding dir() and help()

Python provides built-in functions to inspect modules.

### dir()

`dir()` returns the names available inside an object or module.

```python
import math

print(dir(math))
```

This displays the available names inside the `math` module.

### help()

`help()` displays documentation about a module, function, or object.

```python
import math

help(math)
```

For a specific function:

```python
help(math.sqrt)
```

You can also inspect your custom module:

```python
import calculator

print(dir(calculator))
help(calculator.add)
```

---

## 7. Understanding __name__ and __main__

One of the most important concepts in Python modules is:

```python
__name__
```

Python automatically creates this special variable for every module.

Its value depends on how the file is executed.

### Case 1: Running a File Directly

Create `test.py`:

```python
print(__name__)
```

Run:

```bash
python test.py
```

Output:

```text
__main__
```

When a Python file is executed directly, its `__name__` value becomes `"__main__"`.

### Case 2: Importing a File

Create `test.py`:

```python
print("Test module loaded")
print(__name__)
```

Create another file named `main.py`:

```python
import test
```

Run:

```bash
python main.py
```

Output:

```text
Test module loaded
test
```

When imported, the module's `__name__` is normally its module name.

### 7.1 Why Do We Use if __name__ == "__main__"?

Consider this example.

**calculator.py**

```python
def add(a, b):
    return a + b


print("Calculator module loaded")

if __name__ == "__main__":
    print("Running calculator directly")
    print(add(10, 20))
```

**main.py**

```python
import calculator

print(calculator.add(5, 5))
```

Run `main.py`.

Output:

```text
Calculator module loaded
10
```

The code inside the `if __name__ == "__main__":` block does not execute during a normal import.

Run `calculator.py` directly.

Output:

```text
Calculator module loaded
Running calculator directly
30
```

### Important Rule

Use this structure in reusable Python files:

```python
def main():
    print("Program started")


if __name__ == "__main__":
    main()
```

This ensures that the main program runs only when the file is executed directly.

Note: Other top-level statements still execute when the module is imported. Keep import-time code limited to definitions and safe initialization.

---

## 8. Understanding Python Module Search Path

When we import a module, Python needs to locate its file.

Python searches locations based on its module search path.

The `sys.path` variable contains the locations Python searches.

Example:

```python
import sys

for path in sys.path:
    print(path)
```

Output will depend on your Python installation and how the program is executed.

### Important Points

- The script's directory is normally included when running a script directly.
- The current working directory can matter in interactive and other execution environments.
- Installed packages are available through Python's configured package locations.
- Additional paths can be configured using Python's import system.

### Understanding the Search Path

```python
import sys

print(sys.path)
```

This displays the module search locations.

**Important:** Do not modify `sys.path` unnecessarily. A proper project structure and correct execution directory are usually better solutions.

---

## 9. Creating Your First Python Package

A package helps organize related modules inside a directory.

Let's create a simple package.

### Project Structure

```text
MyProject/
│
├── main.py
│
└── calculator/
    ├── __init__.py
    ├── addition.py
    └── subtraction.py
```

### Step 1: Create addition.py

```python
def add(a, b):
    return a + b
```

### Step 2: Create subtraction.py

```python
def subtract(a, b):
    return a - b
```

### Step 3: Create __init__.py

```python
# Calculator package
```

`__init__.py` can be empty.

It marks a regular Python package and can also contain package initialization code or selected exports.

Modern Python also supports namespace packages without `__init__.py`, but we will use `__init__.py` for our regular package examples.

### Step 4: Create main.py

```python
from calculator import addition
from calculator import subtraction

print(addition.add(20, 10))
print(subtraction.subtract(20, 10))
```

### Output

```text
30
10
```

Run from the `MyProject` directory:

```bash
python main.py
```

---

## 10. Importing Functions Directly from Packages

We can import functions directly from package modules.

```python
from calculator.addition import add
from calculator.subtraction import subtract

print(add(50, 25))
print(subtract(50, 25))
```

Output:

```text
75
25
```

### Using __init__.py to Simplify Imports

We can expose selected functions through `__init__.py`.

**calculator/__init__.py**

```python
from .addition import add
from .subtraction import subtract
```

The dot before the module name represents a relative import within the package.

Now `main.py` can be:

```python
from calculator import add, subtract

print(add(100, 50))
print(subtract(100, 50))
```

Output:

```text
150
50
```

---

## 11. Absolute and Relative Imports

Python supports two main import styles inside packages.

### 11.1 Absolute Import

An absolute import uses the package's full import path.

```python
from calculator.addition import add
```

This identifies the module from the package root.

### 11.2 Relative Import

A relative import uses dots to refer to modules inside the current package.

```python
from .addition import add
```

Here:

- `.` means the current package.
- `..` means the parent package.

Example:

```python
from .reports import generate_report
```

Relative imports are useful when modules inside a package need to import each other.

**Important:** Relative imports normally require package context. Running a package module directly as a standalone script can cause import errors. Run the package entry point from the project root instead.

---

## 12. Creating Subpackages

Packages can contain other packages.

Example:

```text
company/
│
├── __init__.py
│
├── employees/
│   ├── __init__.py
│   ├── operations.py
│   └── reports.py
│
└── accounts/
    ├── __init__.py
    ├── billing.py
    └── payments.py
```

Here:

- `company` is the main package.
- `employees` is a subpackage.
- `accounts` is another subpackage.
- Each directory organizes related modules.

Import example:

```python
from company.employees.operations import add_employee
from company.accounts.billing import generate_bill
```

This structure is useful for large applications.

---

## 13. Standard Library, Third-Party and Custom Modules

Python modules can come from different sources.

### 13.1 Standard Library Modules

These are included with Python.

Examples:

| Module | Purpose |
|---|---|
| math | Mathematical operations |
| random | Random values |
| datetime | Date and time |
| os | Operating system interaction |
| sys | Python interpreter information |
| json | JSON data handling |
| pathlib | File-system paths |
| statistics | Statistical calculations |
| collections | Specialized collection types |

Example:

```python
import random

number = random.randint(1, 100)

print(number)
```

### 13.2 Third-Party Modules

These are created by external developers or organizations.

Examples:

| Package | Purpose |
|---|---|
| requests | HTTP requests |
| numpy | Numerical computing |
| pandas | Data analysis |
| flask | Web development |
| django | Web development |
| pillow | Image processing |

Third-party packages are commonly installed using `pip`.

Example:

```bash
pip install requests
```

Then:

```python
import requests
```

We will study package installation and dependency management in detail later.

### 13.3 User-Defined Modules

These are modules created by us.

Example:

```python
# greetings.py

def welcome(name):
    return f"Welcome, {name}!"
```

Use it:

```python
import greetings

print(greetings.welcome("Raj"))
```

Output:

```text
Welcome, Raj!
```

---

## 14. Common Module and Package Errors

### 14.1 ModuleNotFoundError

Example:

```python
import calculator
```

Error:

```text
ModuleNotFoundError: No module named 'calculator'
```

Possible reasons:

- The file does not exist.
- The module name is incorrect.
- The module is outside the import search path.
- The program is running from an unexpected location.

**Solution:** Check the filename, folder structure and execution directory.

### 14.2 ImportError

Example:

```python
from math import unknown_function
```

Error:

```text
ImportError: cannot import name 'unknown_function' from 'math'
```

Possible reason:

The module exists, but the requested name does not.

**Solution:** Verify the function or variable name.

### 14.3 Circular Import

A circular import occurs when two modules depend on each other during initialization.

Example:

```text
module_a.py imports module_b.py
module_b.py imports module_a.py
```

This can cause partially initialized module errors.

**Solution:**

- Reconsider the module responsibilities.
- Move shared functions into a third module.
- Avoid unnecessary imports at the top level.

### 14.4 Filename Conflicts

Avoid naming your files after standard library modules.

Bad examples:

```text
random.py
math.py
json.py
datetime.py
```

If your project contains `random.py`, Python may import your file instead of the standard library module.

Use meaningful names:

```text
random_generator.py
math_operations.py
json_handler.py
```

If you already created a conflicting file, rename it and remove any stale `__pycache__` files associated with it if necessary.

### 14.5 Incorrect Package Structure

Check that:

- Package folder names are correct.
- Module filenames are correct.
- Required `__init__.py` files are present for the regular packages used in the project.
- Imports match the actual folder structure.
- You are running the program from the correct project root.

---

# 15. Practical Demonstration – Modular Calculator

Now we will create a calculator using multiple modules.

### Project Structure

```text
ModularCalculator/
│
├── main.py
│
└── calculator/
    ├── __init__.py
    ├── operations.py
    └── display.py
```

### File 1: calculator/operations.py

```python
def add(a, b):
    return a + b


def subtract(a, b):
    return a - b


def multiply(a, b):
    return a * b


def divide(a, b):
    if b == 0:
        return None

    return a / b
```

### File 2: calculator/display.py

```python
def show_result(operation, result):
    if result is None:
        print("Error: Cannot divide by zero")
    else:
        print(f"{operation} Result: {result}")
```

### File 3: calculator/__init__.py

```python
from .operations import add, subtract, multiply, divide
from .display import show_result
```

### File 4: main.py

```python
from calculator import add, subtract, multiply, divide, show_result


def main():

    print("MODULAR CALCULATOR")

    num1 = float(input("Enter first number: "))
    num2 = float(input("Enter second number: "))

    print("\nSelect Operation:")
    print("1. Addition")
    print("2. Subtraction")
    print("3. Multiplication")
    print("4. Division")

    choice = input("Enter choice: ")

    if choice == "1":
        result = add(num1, num2)
        show_result("Addition", result)

    elif choice == "2":
        result = subtract(num1, num2)
        show_result("Subtraction", result)

    elif choice == "3":
        result = multiply(num1, num2)
        show_result("Multiplication", result)

    elif choice == "4":
        result = divide(num1, num2)
        show_result("Division", result)

    else:
        print("Invalid choice")


if __name__ == "__main__":
    main()
```

### Sample Output

```text
MODULAR CALCULATOR

Enter first number: 20
Enter second number: 10

Select Operation:
1. Addition
2. Subtraction
3. Multiplication
4. Division

Enter choice: 1

Addition Result: 30.0
```

### What Did We Achieve?

- Calculation logic is separated from the main program.
- Display logic is maintained in another module.
- `__init__.py` provides convenient imports.
- `main.py` controls the application.
- Each module has a clear responsibility.

This is the foundation of modular application development.

---

# 16. Mini Project – Modular Student Management System

Now create a student management application using a package.

### Project Structure

```text
StudentManagement/
│
├── main.py
│
└── student_management/
    ├── __init__.py
    ├── operations.py
    ├── reports.py
    └── validation.py
```

### File 1: student_management/validation.py

```python
def validate_marks(marks):
    return 0 <= marks <= 100


def validate_name(name):
    return bool(name.strip())
```

### File 2: student_management/operations.py

```python
students = {}


def add_student(student_id, name, marks):

    if student_id in students:
        print("Student ID already exists")
        return

    students[student_id] = {
        "name": name,
        "marks": marks
    }

    print("Student added successfully")


def view_students():

    if not students:
        print("No student records found")
        return

    for student_id, details in students.items():

        print("\nStudent ID:", student_id)
        print("Name:", details["name"])
        print("Marks:", details["marks"])


def search_student(student_id):

    if student_id not in students:
        print("Student not found")
        return

    print(students[student_id])


def update_student(student_id, name, marks):

    if student_id not in students:
        print("Student not found")
        return

    students[student_id]["name"] = name
    students[student_id]["marks"] = marks

    print("Student updated successfully")


def delete_student(student_id):

    if student_id not in students:
        print("Student not found")
        return

    del students[student_id]

    print("Student deleted successfully")
```

### File 3: student_management/reports.py

```python
from .operations import students


def show_statistics():

    if not students:
        print("No data available")
        return

    total_marks = sum(
        student["marks"]
        for student in students.values()
    )

    average = total_marks / len(students)

    topper_id = max(
        students,
        key=lambda student_id: students[student_id]["marks"]
    )

    topper = students[topper_id]

    print("\nSTUDENT REPORT")
    print("Total Students:", len(students))
    print("Average Marks:", round(average, 2))
    print("Topper:", topper["name"])
    print("Topper Marks:", topper["marks"])
```

### File 4: student_management/__init__.py

```python
from .operations import (
    add_student,
    view_students,
    search_student,
    update_student,
    delete_student
)

from .reports import show_statistics
from .validation import validate_marks, validate_name
```

### File 5: main.py

```python
from student_management import (
    add_student,
    view_students,
    search_student,
    update_student,
    delete_student,
    show_statistics,
    validate_marks,
    validate_name
)


def main():

    while True:

        print("\n===== STUDENT MANAGEMENT SYSTEM =====")
        print("1. Add Student")
        print("2. View Students")
        print("3. Search Student")
        print("4. Update Student")
        print("5. Delete Student")
        print("6. Show Statistics")
        print("7. Exit")

        choice = input("Enter choice: ")

        if choice == "1":

            student_id = input("Enter Student ID: ")
            name = input("Enter Name: ")

            if not validate_name(name):
                print("Name cannot be empty")
                continue

            try:
                marks = float(input("Enter Marks: "))
            except ValueError:
                print("Marks must be numeric")
                continue

            if not validate_marks(marks):
                print("Marks must be between 0 and 100")
                continue

            add_student(student_id, name, marks)

        elif choice == "2":

            view_students()

        elif choice == "3":

            student_id = input("Enter Student ID: ")
            search_student(student_id)

        elif choice == "4":

            student_id = input("Enter Student ID: ")

            name = input("Enter New Name: ")

            if not validate_name(name):
                print("Name cannot be empty")
                continue

            try:
                marks = float(input("Enter New Marks: "))
            except ValueError:
                print("Marks must be numeric")
                continue

            if not validate_marks(marks):
                print("Marks must be between 0 and 100")
                continue

            update_student(student_id, name, marks)

        elif choice == "5":

            student_id = input("Enter Student ID: ")
            delete_student(student_id)

        elif choice == "6":

            show_statistics()

        elif choice == "7":

            print("Application closed")
            break

        else:

            print("Invalid choice")


if __name__ == "__main__":
    main()
```

### Run the Project

Open the terminal inside the `StudentManagement` folder.

```bash
python main.py
```

### Expected Menu

```text
===== STUDENT MANAGEMENT SYSTEM =====
1. Add Student
2. View Students
3. Search Student
4. Update Student
5. Delete Student
6. Show Statistics
7. Exit
Enter choice:
```

### Important Project Notes

- All student records are currently stored in memory.
- Records disappear when the program exits.
- Database storage and file persistence will be covered in later lessons.
- Each module has a separate responsibility.
- The application is executed through `main.py` from the project root.

---

# 17. Student Practice Exercises

Complete the following exercises independently.

### Exercise 1 – Custom Module

Create a module named `temperature.py`.

Add functions:

- `celsius_to_fahrenheit()`
- `fahrenheit_to_celsius()`
- `celsius_to_kelvin()`

Import these functions into `main.py`.

### Exercise 2 – Math Module

Use Python's `math` module to calculate:

- Square root
- Factorial
- Power
- Ceiling
- Floor

### Exercise 3 – Random Module

Create a number guessing program using the `random` module.

### Exercise 4 – Package Creation

Create a package named `geometry`.

Add modules:

- `circle.py`
- `rectangle.py`
- `triangle.py`

Implement area calculation functions in each module.

Import all functions into `main.py`.

### Exercise 5 – Module Inspection

Use:

- `dir()`
- `help()`
- `__name__`
- `sys.path`

Inspect different modules and understand their contents.

### Exercise 6 – Main Guard

Create a module containing two functions and a main program.

Import that module into another file and verify that the main program does not execute automatically.

### Exercise 7 – Package Import Practice

Create a package with at least three modules.

Use both absolute and relative imports where appropriate.

---

# 18. Trainer Assessment

The trainer should verify the following:

| Assessment Area | Verification |
|---|---|
| Module creation | Student creates and imports custom modules |
| Import statements | Student uses different import styles |
| Aliases | Student uses `as` correctly |
| Module inspection | Student understands `dir()` and `help()` |
| Main guard | Student understands `__name__ == "__main__"` |
| Package creation | Student creates a package with multiple modules |
| Relative imports | Student understands relative package imports |
| Error handling | Student can identify common import errors |
| Project structure | Student separates responsibilities across files |
| Execution | Student runs the application from the project root |

## 19. Completion Criteria

Mark Day 23 as complete when the student can:

- Explain what a Python module is.
- Differentiate between modules, packages and libraries.
- Create and import custom modules.
- Use `import`, `from`, and `as`.
- Explain wildcard import limitations.
- Understand `dir()` and `help()`.
- Explain `__name__` and the `__main__` guard.
- Create packages and subpackages.
- Use absolute and relative imports.
- Troubleshoot common import errors.
- Build and run a modular Python application.

**Day 23 Completed – Python Modules & Packages**

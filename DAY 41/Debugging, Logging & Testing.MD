
# Day 41 – Debugging, Logging & Testing

## 1. Introduction to Debugging

Debugging is the process of identifying, analyzing and fixing errors or unexpected behavior in a program.

A program may contain errors even when it runs without crashing.

For example:

```python
num1 = 10
num2 = 5

result = num1 - num2

print("Addition:", result)
```

Output:

```text
Addition: 5
```

The program executes successfully, but the result is incorrect because subtraction was used instead of addition.

This is a logical error.

### Why Is Debugging Important?

- Identifies programming errors.
- Helps understand unexpected behavior.
- Improves application reliability.
- Reduces development time.
- Makes code easier to maintain.
- Helps identify performance problems.

### Three Common Types of Errors

**1. Syntax Errors**

These occur when Python code violates the language syntax.

```python
if 10 > 5
    print("Ten is greater")
```

Error:

```text
SyntaxError: expected ':'
```

Correct code:

```python
if 10 > 5:
    print("Ten is greater")
```

**2. Runtime Errors**

These occur while a program is executing.

```python
number = 10

result = number / 0
```

Error:

```text
ZeroDivisionError
```

**3. Logical Errors**

The program executes but produces an incorrect result.

```python
length = 10
width = 5

area = length + width

print("Area:", area)
```

Output:

```text
Area: 15
```

Correct code:

```python
area = length * width

print("Area:", area)
```

---

## 2. Understanding the Debugging Process

A systematic debugging process makes problem-solving easier.

### Recommended Steps

1. Reproduce the problem.
2. Read the error message.
3. Identify the line where the issue occurs.
4. Inspect variable values.
5. Understand why the unexpected behavior happens.
6. Fix the underlying issue.
7. Run the program again.
8. Test related functionality to avoid introducing new bugs.

### Example

```python
def calculate_average(marks):

    total = sum(marks)

    average = total / len(marks)

    return average


marks = [80, 90, 70]

print(calculate_average(marks))
```

Expected output:

```text
80.0
```

Now consider an empty list:

```python
marks = []

print(calculate_average(marks))
```

Error:

```text
ZeroDivisionError
```

### Fix the Problem

```python
def calculate_average(marks):

    if not marks:
        return 0

    total = sum(marks)

    average = total / len(marks)

    return average


print(calculate_average([]))
```

Output:

```text
0
```

The function now handles the empty-list case.

---

## 3. Using print() for Debugging

The simplest debugging technique is printing variable values.

### Example

```python
def calculate_total(price, quantity):

    print("Price:", price)

    print("Quantity:", quantity)

    total = price * quantity

    print("Calculated Total:", total)

    return total


calculate_total(100, 5)
```

Output:

```text
Price: 100
Quantity: 5
Calculated Total: 500
```

### Advantages

- Easy to understand.
- Requires no additional tools.
- Useful for quick inspection.

### Disadvantages

- Can create too much output.
- Must be manually removed or maintained.
- Does not provide structured debugging information.
- Becomes difficult to manage in large applications.

For larger applications, use logging and debugging tools.

---

## 4. Using Python's Built-in Debugger – pdb

Python provides a built-in debugger named `pdb`.

It allows developers to pause program execution and inspect variables.

### Example

```python
def calculate_total(price, quantity):

    total = price * quantity

    return total


price = 100
quantity = 5

breakpoint()

result = calculate_total(price, quantity)

print("Total:", result)
```

When execution reaches `breakpoint()`, Python enters debugging mode.

### Important pdb Commands

| Command | Purpose |
|---|---|
| `n` | Execute the next line |
| `s` | Step into a function |
| `c` | Continue execution |
| `p variable` | Print a variable |
| `l` | Show nearby source code |
| `w` | Display the current stack |
| `q` | Quit debugger |
| `h` | Show help |

### Example Debugging Session

```text
(Pdb) n
(Pdb) p price
100
(Pdb) p quantity
5
(Pdb) s
(Pdb) n
(Pdb) p total
500
(Pdb) c
Total: 500
```

The exact sequence depends on where the debugger is paused.

### Using set_trace()

An alternative is:

```python
import pdb

pdb.set_trace()
```

This explicitly starts the debugger at that location.

### Important

`breakpoint()` is available in modern Python versions.

For production execution, remove or disable debugging breakpoints when they are no longer needed.

---

## 5. Debugging in Visual Studio Code

VS Code provides a graphical debugging interface.

It allows developers to inspect code without repeatedly printing variables.

### Step 1: Open Python Project

Open the project folder in VS Code.

### Step 2: Open Python File

Create:

```text
debug_example.py
```

### Step 3: Add Code

```python
def calculate_discount(price, discount):

    final_price = price - (price * discount / 100)

    return final_price


price = 1000
discount = 10

result = calculate_discount(price, discount)

print("Final Price:", result)
```

### Step 4: Set a Breakpoint

Click on the left side of the line number.

A red dot appears.

### Step 5: Start Debugging

- Open the Run and Debug panel.
- Select Python Debugger.
- Start debugging.

You can also use `F5` to start a debugging session.

### Debugging Controls

| Control | Purpose |
|---|---|
| Continue | Resume execution |
| Step Over | Execute current line without entering function |
| Step Into | Enter a function |
| Step Out | Finish current function and return |
| Restart | Restart debugging |
| Stop | End debugging |

### Variables Panel

The Variables panel displays current variable values.

### Watch Panel

The Watch panel allows you to monitor expressions.

Example:

```python
price * discount / 100
```

### Call Stack

The Call Stack displays the sequence of function calls that led to the current execution point.

---

## 6. Understanding Stack Traces

A stack trace shows the sequence of function calls that led to an error.

Example:

```python
def first():

    second()


def second():

    third()


def third():

    result = 10 / 0


first()
```

Output:

```text
Traceback (most recent call last):
  ...
  File "example.py", line ..., in third
    result = 10 / 0
ZeroDivisionError: division by zero
```

### Important Parts

- Exception type: `ZeroDivisionError`
- Error message: `division by zero`
- File location: where the error occurred
- Function name: where execution failed
- Call sequence: how execution reached the failing function

### Best Practice

Read the final exception line first to identify the exception type, then inspect the traceback to find the relevant source location.

---

# 7. Introduction to Logging

Logging is the process of recording information about an application's execution.

Logs help developers understand:

- What happened in the application.
- When an event occurred.
- Whether an operation succeeded.
- Why an operation failed.
- Which part of the application generated an event.

Python provides a built-in `logging` module.

No external installation is required.

### Why Use Logging Instead of print()?

| print() | logging |
|---|---|
| Displays plain output | Provides structured log records |
| No built-in severity levels | Supports severity levels |
| No built-in log file management | Supports file handlers |
| Basic debugging | Application monitoring and diagnostics |
| Manual formatting | Configurable formatting |

---

## 8. Understanding Logging Levels

Python logging provides five commonly used severity levels.

| Level | Numeric Value | Purpose |
|---|---:|---|
| DEBUG | 10 | Detailed diagnostic information |
| INFO | 20 | General application events |
| WARNING | 30 | Something unexpected happened |
| ERROR | 40 | An operation failed |
| CRITICAL | 50 | A serious failure occurred |

### Example

```python
import logging

logging.debug("Debug message")

logging.info("Application started")

logging.warning("Low disk space")

logging.error("Unable to process request")

logging.critical("Application encountered a critical problem")
```

Default output:

```text
WARNING:root:Low disk space
ERROR:root:Unable to process request
CRITICAL:root:Application encountered a critical problem
```

By default, the root logger generally displays WARNING and higher severity levels.

DEBUG and INFO messages are not displayed unless the logging configuration allows them.

---

## 9. Configuring Basic Logging

Use `logging.basicConfig()` to configure the root logger.

### Example

```python
import logging

logging.basicConfig(
    level=logging.DEBUG,
    format="%(asctime)s - %(levelname)s - %(message)s"
)

logging.debug("Debugging application")

logging.info("Application started")

logging.warning("Memory usage is high")

logging.error("Database connection failed")
```

Example output:

```text
2026-11-13 10:00:00,000 - DEBUG - Debugging application
2026-11-13 10:00:00,001 - INFO - Application started
2026-11-13 10:00:00,002 - WARNING - Memory usage is high
2026-11-13 10:00:00,003 - ERROR - Database connection failed
```

The timestamps are illustrative.

### Understanding basicConfig()

| Parameter | Purpose |
|---|---|
| `level` | Minimum severity to process |
| `format` | Log message format |
| `filename` | File to write logs to |
| `filemode` | File opening mode |
| `datefmt` | Timestamp format |
| `handlers` | Logging handlers |

### Common Format Specifiers

| Format | Meaning |
|---|---|
| `%(asctime)s` | Date and time |
| `%(levelname)s` | Logging level |
| `%(message)s` | Log message |
| `%(name)s` | Logger name |
| `%(filename)s` | Source filename |
| `%(lineno)d` | Source line number |
| `%(funcName)s` | Function name |

---

## 10. Saving Logs to a File

Instead of displaying logs only in the terminal, we can save them in a file.

### Example

```python
import logging

logging.basicConfig(
    filename="application.log",
    level=logging.INFO,
    format="%(asctime)s - %(levelname)s - %(message)s"
)

logging.info("Application started")

logging.warning("Low storage space")

logging.error("Unable to connect to server")
```

After execution, a file named `application.log` is created.

Example file content:

```text
2026-11-13 10:00:00,000 - INFO - Application started
2026-11-13 10:00:00,001 - WARNING - Low storage space
2026-11-13 10:00:00,002 - ERROR - Unable to connect to server
```

### Understanding File Modes

| Mode | Purpose |
|---|---|
| `a` | Append logs to an existing file |
| `w` | Overwrite the existing file |

Example:

```python
logging.basicConfig(
    filename="application.log",
    filemode="a",
    level=logging.INFO
)
```

### Important

`logging.basicConfig()` generally configures logging only when the root logger has no handlers already configured.

In a notebook or larger application, an earlier logging configuration may prevent a new `basicConfig()` call from taking effect.

---

## 11. Logging Exceptions

Logging becomes especially useful when an application encounters an exception.

### Example

```python
import logging

logging.basicConfig(
    level=logging.INFO,
    format="%(levelname)s - %(message)s"
)


def divide(a, b):

    try:

        result = a / b

        logging.info("Division completed successfully")

        return result

    except ZeroDivisionError:

        logging.error("Cannot divide by zero")

        return None


print(divide(10, 2))

print(divide(10, 0))
```

Expected output:

```text
INFO - Division completed successfully
5.0
ERROR - Cannot divide by zero
None
```

### Using logging.exception()

`logging.exception()` records an ERROR-level message along with exception information.

It should normally be called inside an exception handler.

```python
import logging

logging.basicConfig(level=logging.ERROR)


try:

    result = 10 / 0

except ZeroDivisionError:

    logging.exception("Calculation failed")
```

The output includes the exception traceback.

### Using exc_info

Another option:

```python
logging.error(
    "Calculation failed",
    exc_info=True
)
```

This records the active exception information when called inside an exception handler.

---

## 12. Creating a Custom Logger

For larger applications, creating named loggers is better than using the root logger everywhere.

### Example

```python
import logging

logger = logging.getLogger("student_app")

logger.setLevel(logging.DEBUG)

logger.debug("Debug message")

logger.info("Student application started")

logger.warning("Student record is incomplete")

logger.error("Unable to save student")
```

### Why Use Named Loggers?

Different modules can use different logger names.

Example:

```python
logger = logging.getLogger(__name__)
```

In a multi-file application, `__name__` identifies the module.

This makes it easier to determine where a log message originated.

---

## 13. Understanding Logging Handlers

A logging handler determines where log messages are sent.

Common handlers include:

| Handler | Purpose |
|---|---|
| StreamHandler | Sends logs to console |
| FileHandler | Writes logs to a file |
| RotatingFileHandler | Rotates log files by size |
| TimedRotatingFileHandler | Rotates log files based on time |

### Example: Console and File Logging

```python
import logging

logger = logging.getLogger("application")

logger.setLevel(logging.DEBUG)

formatter = logging.Formatter(
    "%(asctime)s - %(levelname)s - %(message)s"
)

console_handler = logging.StreamHandler()

file_handler = logging.FileHandler(
    "application.log",
    encoding="utf-8"
)

console_handler.setLevel(logging.WARNING)

file_handler.setLevel(logging.DEBUG)

console_handler.setFormatter(formatter)

file_handler.setFormatter(formatter)

logger.addHandler(console_handler)

logger.addHandler(file_handler)

logger.debug("Debug information")

logger.info("Application started")

logger.warning("Low memory")

logger.error("Operation failed")
```

Console displays WARNING and ERROR.

The file receives DEBUG, INFO, WARNING and ERROR.

### Important

When configuring named loggers, avoid adding duplicate handlers repeatedly. Duplicate handlers can cause the same log message to appear multiple times.

---

## 14. Log Rotation

Large applications may generate very large log files.

Log rotation helps manage their size.

Python provides `RotatingFileHandler`.

### Example

```python
import logging

from logging.handlers import RotatingFileHandler


logger = logging.getLogger("rotating_app")

logger.setLevel(logging.INFO)

handler = RotatingFileHandler(
    "application.log",
    maxBytes=1024 * 1024,
    backupCount=3,
    encoding="utf-8"
)

formatter = logging.Formatter(
    "%(asctime)s - %(levelname)s - %(message)s"
)

handler.setFormatter(formatter)

logger.addHandler(handler)


for number in range(10000):

    logger.info("Application event %s", number)
```

### Understanding Parameters

- `maxBytes` – Maximum size of the active log file.
- `backupCount` – Number of backup log files to retain.
- `encoding` – Character encoding used for the log file.

When the file reaches its configured size, it rotates and older backup files are managed according to the configured count.

---

# 15. Introduction to Software Testing

Software testing is the process of checking whether a program behaves as expected.

Testing helps identify defects before software is delivered.

### Why Is Testing Important?

- Verifies program correctness.
- Detects errors early.
- Prevents regressions.
- Improves software quality.
- Makes code easier to maintain.
- Provides confidence when changing existing functionality.

### Example

Consider a function that adds two numbers.

```python
def add(a, b):

    return a + b
```

We expect:

```python
add(2, 3) == 5
```

A test checks whether this expectation is correct.

---

## 16. Understanding Types of Software Testing

### 1. Unit Testing

Tests a small unit of code, usually an individual function or method.

Example:

```python
def add(a, b):
    return a + b
```

Testing only the `add()` function is unit testing.

### 2. Integration Testing

Checks whether multiple components work together correctly.

Example:

- Application connects to a database.
- Application saves a student.
- Application retrieves the saved student.

### 3. Functional Testing

Checks whether a feature behaves according to its requirements.

Example:

A login feature should reject an incorrect password.

### 4. Regression Testing

Checks whether existing functionality still works after code changes.

### 5. End-to-End Testing

Tests a complete workflow from beginning to end.

Example:

1. Open application.
2. Create student.
3. Update student.
4. View student.
5. Delete student.

### Comparison

| Testing Type | Focus |
|---|---|
| Unit | Individual components |
| Integration | Component interaction |
| Functional | Feature behavior |
| Regression | Previously working functionality |
| End-to-End | Complete user workflow |

---

## 17. Introduction to Python assert

Python provides the `assert` statement for checking assumptions.

### Syntax

```python
assert condition, "Error message"
```

If the condition is true, execution continues.

If it is false, Python raises `AssertionError`.

### Example

```python
age = 20

assert age >= 18, "Age must be at least 18"

print("Eligible")
```

Output:

```text
Eligible
```

### Failed Assertion

```python
age = 15

assert age >= 18, "Age must be at least 18"
```

Error:

```text
AssertionError: Age must be at least 18
```

### Important

Assertions are useful for internal debugging and checking development assumptions.

Do not use `assert` for validating external input or enforcing critical business rules in production because Python can disable assertions when run with optimization.

Use normal `if` statements and exceptions for application validation.

---

# 18. Introduction to unittest

Python provides a built-in testing framework named `unittest`.

No additional package installation is required.

### Basic Test Example

Create:

```text
calculator.py
```

```python
def add(a, b):

    return a + b


def subtract(a, b):

    return a - b


def multiply(a, b):

    return a * b


def divide(a, b):

    if b == 0:
        raise ValueError("Cannot divide by zero")

    return a / b
```

Now create:

```text
test_calculator.py
```

```python
import unittest

from calculator import (
    add,
    subtract,
    multiply,
    divide
)


class TestCalculator(unittest.TestCase):

    def test_add(self):

        self.assertEqual(add(2, 3), 5)


    def test_subtract(self):

        self.assertEqual(subtract(10, 5), 5)


    def test_multiply(self):

        self.assertEqual(multiply(4, 3), 12)


    def test_divide(self):

        self.assertEqual(divide(10, 2), 5)


    def test_divide_by_zero(self):

        with self.assertRaises(ValueError):

            divide(10, 0)


if __name__ == "__main__":

    unittest.main()
```

### Run Tests

```bash
python -m unittest -v
```

Expected output:

```text
test_add ... ok
test_divide ... ok
test_divide_by_zero ... ok
test_multiply ... ok
test_subtract ... ok

----------------------------------------------------------------------
Ran 5 tests

OK
```

### Understanding unittest Concepts

| Concept | Meaning |
|---|---|
| `TestCase` | Base class for test cases |
| `test_` | Prefix used to identify test methods |
| `assertEqual()` | Checks whether two values are equal |
| `assertTrue()` | Checks whether a value is true |
| `assertFalse()` | Checks whether a value is false |
| `assertIsNone()` | Checks whether a value is None |
| `assertRaises()` | Checks whether an exception occurs |
| `setUp()` | Runs before each test method |
| `tearDown()` | Runs after each test method |

---

## 19. Important unittest Assertions

### assertEqual()

```python
self.assertEqual(10, 10)
```

Checks equality.

### assertNotEqual()

```python
self.assertNotEqual(10, 20)
```

Checks inequality.

### assertTrue()

```python
self.assertTrue(10 > 5)
```

Checks whether an expression is true.

### assertFalse()

```python
self.assertFalse(10 < 5)
```

Checks whether an expression is false.

### assertIsNone()

```python
self.assertIsNone(None)
```

Checks whether a value is None.

### assertIn()

```python
self.assertIn("Python", ["Python", "Java"])
```

Checks membership.

### assertRaises()

```python
with self.assertRaises(ValueError):

    int("hello")
```

Checks whether the expected exception is raised.

---

## 20. Using setUp() and tearDown()

Sometimes tests need common preparation and cleanup.

`setUp()` runs before each test method.

`tearDown()` runs after each test method.

### Example

```python
import unittest


class TestStudent(unittest.TestCase):

    def setUp(self):

        self.student = {
            "name": "Rahul",
            "marks": 85
        }


    def test_student_name(self):

        self.assertEqual(
            self.student["name"],
            "Rahul"
        )


    def test_student_marks(self):

        self.assertEqual(
            self.student["marks"],
            85
        )


    def tearDown(self):

        self.student = None


if __name__ == "__main__":

    unittest.main()
```

### Why Use Them?

- Avoid repeated setup code.
- Prepare test data.
- Create temporary resources.
- Clean up after testing.

---

# 21. Introduction to pytest

`pytest` is a popular third-party Python testing framework.

It provides a simple way to write and execute tests.

### Install pytest

```bash
python -m pip install pytest
```

### Verify Installation

```bash
python -m pytest --version
```

### Basic pytest Example

Create `calculator.py`:

```python
def add(a, b):

    return a + b


def subtract(a, b):

    return a - b


def multiply(a, b):

    return a * b
```

Create `test_calculator.py`:

```python
from calculator import add, subtract, multiply


def test_add():

    assert add(2, 3) == 5


def test_subtract():

    assert subtract(10, 5) == 5


def test_multiply():

    assert multiply(4, 3) == 12
```

### Run pytest

```bash
python -m pytest
```

Expected output:

```text
============================= test session starts =============================

collected 3 items

test_calculator.py ...                                      [100%]

============================== 3 passed ==============================
```

The exact output formatting depends on the pytest version and terminal.

### Important Difference

In pytest, ordinary Python `assert` statements are used for test verification.

pytest provides detailed failure information automatically.

---

## 22. unittest vs pytest

| unittest | pytest |
|---|---|
| Built into Python | Third-party package |
| Uses classes commonly | Supports simple test functions |
| Uses methods such as `assertEqual()` | Uses normal `assert` |
| Explicit test setup methods | Fixtures and other setup mechanisms |
| Standard library framework | Rich plugin ecosystem |

Both are useful testing frameworks.

Choose based on project requirements, team conventions and tooling.

---

## 23. Understanding pytest Fixtures

A fixture provides reusable setup data or resources for tests.

### Example

```python
import pytest


@pytest.fixture
def student():

    return {
        "name": "Rahul",
        "marks": 85
    }


def test_student_name(student):

    assert student["name"] == "Rahul"


def test_student_marks(student):

    assert student["marks"] == 85
```

### Understanding the Code

- `@pytest.fixture` marks a fixture.
- `student()` creates test data.
- pytest automatically supplies the fixture to tests that request it.

### Why Use Fixtures?

- Reuse test data.
- Reduce repeated setup code.
- Manage temporary resources.
- Organize tests more cleanly.

---

## 24. Parameterized Testing in pytest

Parameterized testing allows one test function to run with multiple input values.

### Example

```python
import pytest


def add(a, b):

    return a + b


@pytest.mark.parametrize(
    "a, b, expected",
    [
        (2, 3, 5),
        (10, 5, 15),
        (-2, 2, 0),
        (0, 0, 0)
    ]
)
def test_add(a, b, expected):

    assert add(a, b) == expected
```

Run:

```bash
python -m pytest -v
```

pytest executes the test with each parameter set.

### Advantages

- Avoids repeated test functions.
- Makes test coverage easier to expand.
- Tests multiple input scenarios.
- Improves readability.

---

## 25. Testing Exceptions with pytest

Use `pytest.raises()` to verify that a function raises an expected exception.

### Example

```python
import pytest


def divide(a, b):

    if b == 0:

        raise ValueError("Cannot divide by zero")

    return a / b


def test_divide_by_zero():

    with pytest.raises(ValueError):

        divide(10, 0)
```

### Verify Exception Message

```python
def test_divide_error_message():

    with pytest.raises(
        ValueError,
        match="Cannot divide by zero"
    ):

        divide(10, 0)
```

This checks both the exception type and its message.

---

## 26. Understanding Test Discovery

pytest automatically discovers test files and test functions using naming conventions.

### Common Naming Rules

Test files:

```text
test_*.py
*_test.py
```

Test functions:

```python
def test_add():
    pass
```

Test classes:

```python
class TestCalculator:

    def test_add(self):
        pass
```

### Run All Tests

```bash
python -m pytest
```

### Run a Specific File

```bash
python -m pytest test_calculator.py
```

### Run a Specific Test

```bash
python -m pytest test_calculator.py::test_add
```

### Verbose Output

```bash
python -m pytest -v
```

### Stop After First Failure

```bash
python -m pytest -x
```

### Show Print Output

```bash
python -m pytest -s
```

### Run Tests Matching a Keyword

```bash
python -m pytest -k "add"
```

---

## 27. Measuring Test Coverage

Test coverage measures how much of the application code is executed during testing.

pytest itself does not provide full coverage reporting by default.

We can use the `pytest-cov` plugin.

### Install

```bash
python -m pip install pytest-cov
```

### Run Coverage

```bash
python -m pytest --cov=calculator
```

### Generate HTML Report

```bash
python -m pytest --cov=calculator --cov-report=html
```

This creates an HTML coverage report, usually in:

```text
htmlcov/
```

Open the generated `index.html` file in a browser.

### Important

High test coverage does not automatically mean high test quality.

Tests must verify meaningful behavior, edge cases and failure conditions.

---

## 28. Mocking in Python Tests

Sometimes a function depends on an external service.

Examples:

- Payment gateway.
- Email service.
- External API.
- Database.
- File system.

Calling a real external service during every unit test can be slow, expensive or unreliable.

Mocking replaces a real dependency with a controlled test object.

Python provides `unittest.mock`.

### Example

Create `weather.py`:

```python
def get_temperature(api_client, city):

    response = api_client.get_temperature(city)

    return response
```

Create `test_weather.py`:

```python
from unittest.mock import Mock

from weather import get_temperature


def test_get_temperature():

    mock_client = Mock()

    mock_client.get_temperature.return_value = 28

    result = get_temperature(
        mock_client,
        "Mumbai"
    )

    assert result == 28

    mock_client.get_temperature.assert_called_once_with(
        "Mumbai"
    )
```

Run:

```bash
python -m pytest -v
```

### Understanding Mock

- `Mock()` creates a mock object.
- `return_value` defines the returned result.
- `assert_called_once_with()` verifies how a mock was called.

### Why Use Mocking?

- Avoids unnecessary network requests.
- Makes tests predictable.
- Isolates the unit being tested.
- Allows simulation of success and failure scenarios.

---

## 29. Testing Database Applications

Database testing verifies that database-related operations behave correctly.

For testing, we can use an in-memory SQLite database.

### Example

```python
from sqlalchemy import create_engine, String, select
from sqlalchemy.orm import DeclarativeBase, Mapped, mapped_column, Session


class Base(DeclarativeBase):
    pass


class Student(Base):

    __tablename__ = "students"

    id: Mapped[int] = mapped_column(primary_key=True)

    name: Mapped[str] = mapped_column(String(100))


def test_student_insert():

    engine = create_engine("sqlite://")

    Base.metadata.create_all(engine)

    with Session(engine) as session:

        student = Student(name="Rahul")

        session.add(student)

        session.commit()

        result = session.scalars(
            select(Student)
        ).all()

        assert len(result) == 1

        assert result[0].name == "Rahul"
```

Run:

```bash
python -m pytest -v
```

### Important

The in-memory database is temporary and is not the same as the application's persistent database.

For more complex applications, use dedicated test database fixtures and transaction cleanup.

---

## 30. Logging Best Practices

Follow these practices when implementing logging:

1. Use DEBUG for detailed diagnostic information.
2. Use INFO for normal application events.
3. Use WARNING for unexpected but recoverable conditions.
4. Use ERROR for failed operations.
5. Use CRITICAL for serious failures.
6. Use named loggers in multi-module applications.
7. Avoid logging passwords, API keys and sensitive data.
8. Avoid unnecessary log messages.
9. Use log rotation for long-running applications.
10. Include meaningful context in log messages.
11. Configure logging centrally in larger applications.
12. Prefer parameterized logging messages.

### Example

Recommended:

```python
logger.info(
    "Student %s created successfully",
    student_id
)
```

Avoid unnecessary string formatting:

```python
logger.info(
    f"Student {student_id} created successfully"
)
```

Parameterized logging allows the logging system to defer message formatting when a log record is not processed.

---

# 31. Mini Project – Student Management System with Logging and Automated Testing

## Project Description

Create a Student Management System with:

- CRUD operations.
- Input validation.
- Structured application logging.
- Exception handling.
- Automated unit tests.
- Test coverage reporting.

### Project Structure

```text
StudentTestingSystem/
│
├── main.py
├── student_manager.py
├── logger_config.py
├── requirements.txt
├── .gitignore
│
├── logs/
│
└── tests/
    ├── __init__.py
    └── test_student_manager.py
```

## Step 1: Create requirements.txt

```text
pytest
pytest-cov
```

Install dependencies:

```bash
python -m pip install -r requirements.txt
```

## Step 2: Create logger_config.py

```python
import logging
from logging.handlers import RotatingFileHandler


def setup_logger():

    logger = logging.getLogger("student_manager")

    logger.setLevel(logging.DEBUG)

    if logger.handlers:

        return logger

    formatter = logging.Formatter(
        "%(asctime)s - %(levelname)s - %(name)s - %(message)s"
    )

    console_handler = logging.StreamHandler()

    console_handler.setLevel(logging.WARNING)

    file_handler = RotatingFileHandler(
        "student_manager.log",
        maxBytes=1024 * 1024,
        backupCount=3,
        encoding="utf-8"
    )

    file_handler.setLevel(logging.DEBUG)

    console_handler.setFormatter(formatter)

    file_handler.setFormatter(formatter)

    logger.addHandler(console_handler)

    logger.addHandler(file_handler)

    return logger


logger = setup_logger()
```

## Step 3: Create student_manager.py

```python
from logger_config import logger


class StudentManager:

    def __init__(self):

        self.students = {}

        logger.info("StudentManager initialized")


    def add_student(self, student_id, name, marks):

        if student_id in self.students:

            logger.warning(
                "Duplicate student ID: %s",
                student_id
            )

            raise ValueError("Student already exists")

        if not name.strip():

            logger.warning("Empty student name rejected")

            raise ValueError("Name cannot be empty")

        if not 0 <= marks <= 100:

            logger.warning(
                "Invalid marks supplied for student %s",
                student_id
            )

            raise ValueError("Marks must be between 0 and 100")

        self.students[student_id] = {
            "name": name.strip(),
            "marks": marks
        }

        logger.info(
            "Student %s added successfully",
            student_id
        )

        return True


    def get_student(self, student_id):

        student = self.students.get(student_id)

        if student is None:

            logger.warning(
                "Student %s not found",
                student_id
            )

            raise KeyError("Student not found")

        logger.debug(
            "Student %s retrieved",
            student_id
        )

        return student


    def get_all_students(self):

        logger.info(
            "Retrieved %s student records",
            len(self.students)
        )

        return self.students.copy()


    def update_student(self, student_id, name, marks):

        student = self.get_student(student_id)

        if not name.strip():

            raise ValueError("Name cannot be empty")

        if not 0 <= marks <= 100:

            raise ValueError("Marks must be between 0 and 100")

        student["name"] = name.strip()

        student["marks"] = marks

        logger.info(
            "Student %s updated successfully",
            student_id
        )

        return True


    def delete_student(self, student_id):

        if student_id not in self.students:

            logger.warning(
                "Cannot delete missing student %s",
                student_id
            )

            raise KeyError("Student not found")

        del self.students[student_id]

        logger.info(
            "Student %s deleted successfully",
            student_id
        )

        return True


    def calculate_average(self):

        if not self.students:

            return 0

        total = sum(
            student["marks"]
            for student in self.students.values()
        )

        average = total / len(self.students)

        logger.debug(
            "Calculated average marks: %s",
            average
        )

        return average


    def get_top_student(self):

        if not self.students:

            return None

        top_student = max(
            self.students.items(),
            key=lambda item: item[1]["marks"]
        )

        logger.info(
            "Top student identified: %s",
            top_student[0]
        )

        return top_student
```

## Step 4: Create tests/test_student_manager.py

```python
import pytest

from student_manager import StudentManager


@pytest.fixture
def manager():

    return StudentManager()


def test_add_student(manager):

    result = manager.add_student(
        1,
        "Rahul",
        85
    )

    assert result is True

    assert manager.get_student(1)["name"] == "Rahul"


def test_duplicate_student(manager):

    manager.add_student(
        1,
        "Rahul",
        85
    )

    with pytest.raises(ValueError):

        manager.add_student(
            1,
            "Priya",
            90
        )


def test_empty_student_name(manager):

    with pytest.raises(ValueError):

        manager.add_student(
            1,
            "",
            85
        )


@pytest.mark.parametrize(
    "marks",
    [-1, 101]
)
def test_invalid_marks(manager, marks):

    with pytest.raises(ValueError):

        manager.add_student(
            1,
            "Rahul",
            marks
        )


def test_get_student(manager):

    manager.add_student(
        1,
        "Rahul",
        85
    )

    student = manager.get_student(1)

    assert student["marks"] == 85


def test_missing_student(manager):

    with pytest.raises(KeyError):

        manager.get_student(99)


def test_update_student(manager):

    manager.add_student(
        1,
        "Rahul",
        85
    )

    manager.update_student(
        1,
        "Rahul Gupta",
        95
    )

    student = manager.get_student(1)

    assert student["name"] == "Rahul Gupta"

    assert student["marks"] == 95


def test_delete_student(manager):

    manager.add_student(
        1,
        "Rahul",
        85
    )

    manager.delete_student(1)

    assert manager.get_all_students() == {}


def test_average_marks(manager):

    manager.add_student(1, "Rahul", 80)

    manager.add_student(2, "Priya", 90)

    assert manager.calculate_average() == 85


def test_empty_average(manager):

    assert manager.calculate_average() == 0


def test_top_student(manager):

    manager.add_student(1, "Rahul", 80)

    manager.add_student(2, "Priya", 95)

    top_student = manager.get_top_student()

    assert top_student[0] == 2

    assert top_student[1]["name"] == "Priya"


def test_empty_top_student(manager):

    assert manager.get_top_student() is None
```

## Step 5: Create main.py

```python
from student_manager import StudentManager
from logger_config import logger


def main():

    manager = StudentManager()

    while True:

        print("\n========== STUDENT MANAGEMENT SYSTEM ==========")

        print("1. Add Student")

        print("2. View All Students")

        print("3. Search Student")

        print("4. Update Student")

        print("5. Delete Student")

        print("6. Calculate Average")

        print("7. Display Top Student")

        print("8. Exit")

        choice = input("\nEnter choice: ").strip()

        try:

            if choice == "1":

                student_id = int(input("Enter ID: "))

                name = input("Enter name: ")

                marks = float(input("Enter marks: "))

                manager.add_student(
                    student_id,
                    name,
                    marks
                )

                print("Student added successfully!")


            elif choice == "2":

                students = manager.get_all_students()

                if not students:

                    print("No students found.")

                for student_id, details in students.items():

                    print(
                        student_id,
                        details["name"],
                        details["marks"]
                    )


            elif choice == "3":

                student_id = int(input("Enter ID: "))

                student = manager.get_student(student_id)

                print(student)


            elif choice == "4":

                student_id = int(input("Enter ID: "))

                name = input("Enter new name: ")

                marks = float(input("Enter new marks: "))

                manager.update_student(
                    student_id,
                    name,
                    marks
                )

                print("Student updated successfully!")


            elif choice == "5":

                student_id = int(input("Enter ID: "))

                manager.delete_student(student_id)

                print("Student deleted successfully!")


            elif choice == "6":

                print(
                    "Average Marks:",
                    manager.calculate_average()
                )


            elif choice == "7":

                top_student = manager.get_top_student()

                if top_student:

                    print("Top Student:", top_student)

                else:

                    print("No students found.")


            elif choice == "8":

                logger.info("Application closed")

                print("Application closed.")

                break


            else:

                print("Invalid choice.")


        except (ValueError, KeyError) as error:

            logger.error(
                "Operation failed: %s",
                error
            )

            print("Error:", error)


        except Exception:

            logger.exception("Unexpected application error")

            print("An unexpected error occurred.")


if __name__ == "__main__":

    main()
```

## Step 6: Create .gitignore

```text
.venv/
venv/

__pycache__/
*.py[cod]

.pytest_cache/
.coverage
htmlcov/

*.log

.env
```

## Step 7: Run the Application

```bash
python main.py
```

Test the following:

1. Add a student.
2. Add another student.
3. View all students.
4. Search for a student.
5. Update student details.
6. Delete a student.
7. Calculate average marks.
8. Display the top student.
9. Enter invalid marks.
10. Try adding a duplicate student ID.

## Step 8: Run Automated Tests

From the project root:

```bash
python -m pytest -v
```

Expected summary:

```text
============================= test session starts =============================

collected 12 items

tests/test_student_manager.py ............                  [100%]

============================== 12 passed ==============================
```

The exact display may differ by pytest version.

## Step 9: Generate Coverage Report

```bash
python -m pytest --cov=student_manager --cov-report=term-missing
```

Generate HTML:

```bash
python -m pytest --cov=student_manager --cov-report=html
```

Open:

```text
htmlcov/index.html
```

## Step 10: Verify Logging

After running the application, check:

```text
student_manager.log
```

It should contain application events, warnings and errors.

### Project Completion Requirements

- All CRUD operations must work.
- Invalid data must be rejected.
- Exceptions must be handled.
- Application events must be logged.
- Log files must be created.
- Automated tests must pass.
- Coverage report must be generated.
- The student must explain the purpose of every test.

---

# 32. Student Practice Exercises

## Beginner Level

1. Create a calculator function and test addition.
2. Write tests for subtraction and multiplication.
3. Test division by zero.
4. Use `assertEqual()` in unittest.
5. Write a pytest test function.
6. Use `logging.info()` to record application startup.
7. Log an error when an invalid operation occurs.
8. Save logs to a file.
9. Use `breakpoint()` to inspect variables.
10. Debug a logical error in a simple program.

## Intermediate Level

1. Write unit tests for a Student class.
2. Test all validation conditions.
3. Create a pytest fixture for sample student data.
4. Use parameterized tests for marks validation.
5. Test exception handling.
6. Configure console and file logging.
7. Implement log rotation.
8. Use a mock object for an API dependency.
9. Measure code coverage.
10. Test a database operation using in-memory SQLite.

## Advanced Level

1. Write unit tests for a complete CRUD module.
2. Create integration tests for a database-backed application.
3. Mock an external API.
4. Test both successful and failed API responses.
5. Use pytest fixtures for database setup and cleanup.
6. Configure separate loggers for different application modules.
7. Implement rotating log files.
8. Generate an HTML coverage report.
9. Test edge cases and regression scenarios.
10. Build a complete tested application with structured logging.

---

# 33. Trainer Assessment

Ask the student to explain:

1. What is debugging?
2. What are syntax, runtime and logical errors?
3. What is a stack trace?
4. What is pdb?
5. What does `breakpoint()` do?
6. What is the difference between Step Over and Step Into?
7. What is logging?
8. Why is logging better than using print() in large applications?
9. What are DEBUG, INFO, WARNING, ERROR and CRITICAL?
10. What does `basicConfig()` do?
11. What is a logging handler?
12. What is log rotation?
13. What is unit testing?
14. What is integration testing?
15. What is regression testing?
16. What is an assertion?
17. What is unittest?
18. What is pytest?
19. What is a pytest fixture?
20. What is parameterized testing?
21. What is mocking?
22. What is test coverage?
23. Does high test coverage guarantee bug-free software?
24. Why should external dependencies sometimes be mocked?

### Practical Assessment

Ask the student to independently:

- Debug a program using VS Code.
- Use pdb to inspect variable values.
- Configure Python logging.
- Write logs to a file.
- Implement rotating log files.
- Write unit tests using unittest.
- Write tests using pytest.
- Create fixtures.
- Implement parameterized tests.
- Mock an external dependency.
- Generate a coverage report.
- Build the Student Management System with automated tests.

---

# 34. Completion Criteria

Day 41 is complete when the student can:

- Identify syntax, runtime and logical errors.
- Read and understand stack traces.
- Debug using print(), pdb and VS Code.
- Inspect variables during execution.
- Configure Python logging.
- Understand logging levels.
- Save logs to files.
- Use named loggers and handlers.
- Implement log rotation.
- Explain different software testing types.
- Write unit tests using unittest.
- Write automated tests using pytest.
- Use fixtures and parameterized testing.
- Test expected exceptions.
- Mock external dependencies.
- Measure code coverage.
- Build and test a complete Python application.

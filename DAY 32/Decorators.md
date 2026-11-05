
# Day 32 – Python Decorators

## 1. Introduction to Decorators

A decorator is a function that modifies or extends the behavior of another function without directly changing its original code.

Decorators are commonly used for:

- Logging
- Authentication
- Authorization
- Performance measurement
- Input validation
- Caching
- Access control

### Real-World Example

Imagine a function that performs a task.

Before executing it, you want to:
1. Display a message.
2. Execute the original function.
3. Display another message.

Instead of adding these statements to every function, you can create a decorator and reuse it.

---

## 2. Functions Are First-Class Objects

In Python, functions are first-class objects.

This means functions can:

- Be assigned to variables.
- Be passed as arguments.
- Be returned from other functions.
- Be stored in collections.

### Example 1: Assigning a Function to a Variable

```python
def greet():
    print("Hello, Python!")


message = greet

message()
```

**Output:**
```text
Hello, Python!
```

Here, `message` refers to the same function as `greet`.

Notice that we used `greet`, not `greet()`.

- `greet` refers to the function.
- `greet()` executes the function.

### Example 2: Passing a Function as an Argument

```python
def greet():
    print("Hello!")


def execute_function(func):
    func()


execute_function(greet)
```

**Output:**
```text
Hello!
```

The `greet` function is passed as an argument to `execute_function()`.

### Example 3: Returning a Function

```python
def outer_function():

    def inner_function():
        print("Inside inner function")

    return inner_function


result = outer_function()

result()
```

**Output:**
```text
Inside inner function
```

The outer function returns the inner function without executing it.

---

## 3. Nested Functions

A nested function is a function defined inside another function.

### Example

```python
def outer():

    print("Outer function")

    def inner():
        print("Inner function")

    inner()


outer()
```

**Output:**
```text
Outer function
Inner function
```

The inner function is defined inside the outer function.

It can be called from within the outer function.

---

## 4. Understanding Closures

A closure is created when an inner function remembers and uses variables from its enclosing function, even after the enclosing function has finished executing.

### Example

```python
def outer_function(message):

    def inner_function():
        print(message)

    return inner_function


greet = outer_function("Hello from closure!")

greet()
```

**Output:**
```text
Hello from closure!
```

### Explanation

1. `outer_function()` receives a message.
2. It creates `inner_function()`.
3. The inner function uses the outer function's `message` variable.
4. The outer function returns the inner function.
5. The returned function still remembers the message.

Closures are an important foundation for understanding decorators.

---

## 5. Creating a Simple Decorator

A decorator is generally a function that accepts another function and returns a modified or wrapped function.

### Example

```python
def my_decorator(func):

    def wrapper():
        print("Before function execution")

        func()

        print("After function execution")

    return wrapper


def greet():
    print("Hello, Raj!")


result = my_decorator(greet)

result()
```

**Output:**
```text
Before function execution
Hello, Raj!
After function execution
```

### Explanation

- `my_decorator()` accepts the original function.
- `wrapper()` adds extra behavior.
- `func()` executes the original function.
- The decorator returns the wrapper function.
- Calling `result()` executes the wrapper.

The original `greet()` function was not directly modified.

---

## 6. Using the @ Decorator Syntax

Python provides a shorter syntax for applying decorators.

Instead of writing:

```python
def greet():
    print("Hello, Raj!")


greet = my_decorator(greet)

greet()
```

We can write:

```python
@my_decorator
def greet():
    print("Hello, Raj!")


greet()
```

**Output:**
```text
Before function execution
Hello, Raj!
After function execution
```

### How Does @ Work?

This:

```python
@my_decorator
def greet():
    print("Hello")
```

Is equivalent to:

```python
def greet():
    print("Hello")


greet = my_decorator(greet)
```

The `@` syntax applies the decorator when the function is defined.

---

## 7. Decorators with Function Arguments

The previous decorator only worked with functions that did not require arguments.

To create a reusable decorator, the wrapper should accept `*args` and `**kwargs`.

### Example

```python
def my_decorator(func):

    def wrapper(*args, **kwargs):
        print("Function is starting")

        result = func(*args, **kwargs)

        print("Function has finished")

        return result

    return wrapper


@my_decorator
def greet(name):
    print(f"Hello, {name}!")


greet("Raj")
```

**Output:**
```text
Function is starting
Hello, Raj!
Function has finished
```

### Explanation

- `*args` accepts positional arguments.
- `**kwargs` accepts keyword arguments.
- `func(*args, **kwargs)` passes the arguments to the original function.
- `return result` preserves the original function's return value.

A reusable decorator should generally handle both positional and keyword arguments.

---

## 8. Decorator with Return Values

A decorator must preserve the return value when the original function returns something.

### Example

```python
def my_decorator(func):

    def wrapper(*args, **kwargs):
        print("Calculating result...")

        result = func(*args, **kwargs)

        print("Calculation completed")

        return result

    return wrapper


@my_decorator
def add(a, b):
    return a + b


result = add(10, 20)

print("Result:", result)
```

**Output:**
```text
Calculating result...
Calculation completed
Result: 30
```

If the wrapper does not return `result`, the decorated function will return `None` in this example.

---

## 9. Using Multiple Decorators

Python allows multiple decorators to be applied to a single function.

### Example

```python
def decorator_one(func):

    def wrapper():
        print("Decorator One - Start")

        func()

        print("Decorator One - End")

    return wrapper


def decorator_two(func):

    def wrapper():
        print("Decorator Two - Start")

        func()

        print("Decorator Two - End")

    return wrapper


@decorator_one
@decorator_two
def greet():
    print("Hello Python!")


greet()
```

**Output:**
```text
Decorator One - Start
Decorator Two - Start
Hello Python!
Decorator Two - End
Decorator One - End
```

### Explanation

Decorators are applied from bottom to top.

This:

```python
@decorator_one
@decorator_two
def greet():
    print("Hello Python!")
```

Is equivalent to:

```python
greet = decorator_one(decorator_two(greet))
```

The outermost decorator executes first when the decorated function is called.

---

## 10. Decorators with Parameters

Sometimes we want to pass configuration values to a decorator.

For example, we may want to execute a function a specified number of times.

This requires an additional outer function.

### Example

```python
def repeat(times):

    def decorator(func):

        def wrapper(*args, **kwargs):

            for _ in range(times):
                func(*args, **kwargs)

        return wrapper

    return decorator


@repeat(3)
def greet():
    print("Hello Python!")


greet()
```

**Output:**
```text
Hello Python!
Hello Python!
Hello Python!
```

### Explanation

There are three levels:

1. `repeat(times)` receives the decorator configuration.
2. `decorator(func)` receives the original function.
3. `wrapper()` executes the original function repeatedly.

A parameterized decorator is therefore a decorator factory.

---

## 11. Preserving Function Metadata with functools.wraps

Decorators can change the identity and metadata of the function they wrap.

For example:

```python
def my_decorator(func):

    def wrapper():
        print("Executing function")
        func()

    return wrapper


@my_decorator
def greet():
    """This function greets the user."""
    print("Hello!")


print(greet.__name__)
print(greet.__doc__)
```

**Output:**
```text
wrapper
None
```

The decorated function now exposes the wrapper's name and documentation.

Python provides `functools.wraps` to preserve the original function's metadata.

### Improved Example

```python
from functools import wraps


def my_decorator(func):

    @wraps(func)
    def wrapper(*args, **kwargs):
        print("Executing function")

        return func(*args, **kwargs)

    return wrapper


@my_decorator
def greet():
    """This function greets the user."""
    print("Hello!")


print(greet.__name__)
print(greet.__doc__)
```

**Output:**
```text
greet
This function greets the user.
```

**Best Practice:** Use `@wraps(func)` when writing general-purpose decorators.

---

# PART 2 – PRACTICAL DECORATORS

## 12. Logging Decorator

Logging decorators can display which function is being executed.

```python
from functools import wraps


def log_function(func):

    @wraps(func)
    def wrapper(*args, **kwargs):
        print(f"Calling function: {func.__name__}")

        result = func(*args, **kwargs)

        print(f"Finished function: {func.__name__}")

        return result

    return wrapper


@log_function
def calculate_total(a, b):
    return a + b


print("Total:", calculate_total(10, 20))
```

**Output:**
```text
Calling function: calculate_total
Finished function: calculate_total
Total: 30
```

This example prints messages to the terminal. Production applications commonly use Python's `logging` module instead of `print()`.

---

## 13. Execution Time Decorator

A decorator can measure how long a function takes to execute.

Use `time.perf_counter()` for measuring elapsed time.

```python
import time
from functools import wraps


def calculate_time(func):

    @wraps(func)
    def wrapper(*args, **kwargs):

        start = time.perf_counter()

        result = func(*args, **kwargs)

        end = time.perf_counter()

        print("Execution Time:", end - start, "seconds")

        return result

    return wrapper


@calculate_time
def calculate_sum():
    total = 0

    for number in range(1000000):
        total += number

    return total


print("Total:", calculate_sum())
```

**Output:**

```text
Execution Time: <measured time> seconds
Total: 499999500000
```

The exact execution time depends on the computer.

---

## 14. Authentication Decorator

A decorator can check whether a user is authenticated before allowing a function to execute.

### Example

```python
from functools import wraps


def login_required(func):

    @wraps(func)
    def wrapper(is_logged_in, *args, **kwargs):

        if not is_logged_in:
            print("Access Denied: Please Login First")
            return None

        return func(is_logged_in, *args, **kwargs)

    return wrapper


@login_required
def dashboard(is_logged_in):
    print("Welcome to Dashboard")


dashboard(False)
dashboard(True)
```

**Output:**
```text
Access Denied: Please Login First
Welcome to Dashboard
```

### Explanation

- The decorator checks the login status.
- If the user is not logged in, the function is not executed.
- If the user is logged in, the original function executes.

**Important:** This is only a learning example. Real authentication must verify trusted session or token information. A user-controlled Boolean value is not secure authentication.

---

## 15. Input Validation Decorator

Decorators can validate function arguments before execution.

### Example

```python
from functools import wraps


def validate_positive(func):

    @wraps(func)
    def wrapper(number, *args, **kwargs):

        if number <= 0:
            print("Number must be positive")
            return None

        return func(number, *args, **kwargs)

    return wrapper


@validate_positive
def calculate_square(number):
    return number ** 2


print(calculate_square(5))
print(calculate_square(-3))
```

**Output:**
```text
25
Number must be positive
None
```

The decorator checks the input before calling the original function.

---

## 16. Caching Decorator

Caching means storing previously calculated results so that repeated calls can reuse them.

Python provides `functools.lru_cache` for this purpose.

### Example

```python
from functools import lru_cache


@lru_cache(maxsize=100)
def fibonacci(number):

    if number <= 1:
        return number

    return fibonacci(number - 1) + fibonacci(number - 2)


print(fibonacci(10))
print(fibonacci(20))

print(fibonacci.cache_info())
```

**Output:**
```text
55
6765
CacheInfo(hits=18, misses=21, maxsize=100, currsize=21)
```

### Explanation

- `@lru_cache` stores previously calculated results.
- Repeated calls with the same arguments can reuse cached values.
- `maxsize=100` limits the cache to 100 entries.
- `cache_info()` displays cache statistics.

**Important:** `lru_cache` is most suitable for functions whose results depend on their arguments and that do not have side effects. Arguments must be hashable.

---

## 17. Class Decorators

Decorators can also be applied to classes.

A class decorator receives a class and returns a class or another replacement object.

### Example

```python
def add_message(cls):

    cls.message = "Welcome to Python OOP"

    return cls


@add_message
class Student:
    def __init__(self, name):
        self.name = name


student = Student("Raj")

print(student.name)
print(student.message)
```

**Output:**
```text
Raj
Welcome to Python OOP
```

The decorator adds a class attribute to `Student`.

---

## 18. Built-in Decorators in Python

Python provides several built-in decorators.

| Decorator | Purpose |
|---|---|
| `@staticmethod` | Defines a method that does not receive an automatic instance or class argument |
| `@classmethod` | Defines a method that receives the class as its first argument |
| `@property` | Exposes a method as a managed attribute |
| `@abstractmethod` | Marks a method as abstract |
| `@functools.wraps` | Preserves wrapped function metadata |
| `@functools.lru_cache` | Caches function results |

### Example: @staticmethod

```python
class Calculator:

    @staticmethod
    def add(a, b):
        return a + b


print(Calculator.add(10, 20))
```

**Output:**
```text
30
```

### Example: @classmethod

```python
class Student:

    school = "ABC School"

    @classmethod
    def change_school(cls, name):
        cls.school = name


Student.change_school("XYZ School")

print(Student.school)
```

**Output:**
```text
XYZ School
```

---

## 19. Decorator Execution Order

A decorator is applied when the decorated function is defined.

Its wrapper code runs when the decorated function is called.

### Example

```python
def decorator(func):

    print("Applying decorator")

    def wrapper():
        print("Before execution")
        func()
        print("After execution")

    return wrapper


@decorator
def greet():
    print("Hello!")


print("Program started")

greet()
```

**Output:**
```text
Applying decorator
Program started
Before execution
Hello!
After execution
```

Notice:

- `Applying decorator` appears when Python defines the decorated function.
- The wrapper messages appear when `greet()` is called.

---

## 20. Common Mistakes While Writing Decorators

### Mistake 1: Forgetting to Call the Original Function

Incorrect:

```python
def decorator(func):

    def wrapper():
        print("Before execution")

    return wrapper
```

The original function is never executed.

Correct:

```python
def decorator(func):

    def wrapper():
        print("Before execution")
        func()

    return wrapper
```

### Mistake 2: Forgetting to Return the Result

Incorrect:

```python
def decorator(func):

    def wrapper(*args, **kwargs):
        func(*args, **kwargs)

    return wrapper
```

If the original function returns a value, that value is lost.

Correct:

```python
def decorator(func):

    def wrapper(*args, **kwargs):
        return func(*args, **kwargs)

    return wrapper
```

### Mistake 3: Not Accepting Arguments

A wrapper that accepts no arguments cannot directly wrap functions requiring positional or keyword arguments.

Use:

```python
def wrapper(*args, **kwargs):
    return func(*args, **kwargs)
```

### Mistake 4: Not Using functools.wraps

Without `@wraps`, the decorated function may expose the wrapper's metadata instead of the original function's metadata.

Use:

```python
from functools import wraps
```

And apply:

```python
@wraps(func)
```

---

# PART 3 – PRACTICAL PROGRAMS

## 21. Program 1: Repeat Function Execution

```python
from functools import wraps


def repeat(times):

    def decorator(func):

        @wraps(func)
        def wrapper(*args, **kwargs):

            for _ in range(times):
                func(*args, **kwargs)

        return wrapper

    return decorator


@repeat(3)
def welcome():
    print("Welcome to Python!")


welcome()
```

**Output:**
```text
Welcome to Python!
Welcome to Python!
Welcome to Python!
```

---

## 22. Program 2: Check Function Execution Time

```python
import time
from functools import wraps


def timer(func):

    @wraps(func)
    def wrapper(*args, **kwargs):

        start = time.perf_counter()

        result = func(*args, **kwargs)

        end = time.perf_counter()

        print(f"{func.__name__} took {end - start:.6f} seconds")

        return result

    return wrapper


@timer
def multiplication(a, b):
    return a * b


print("Result:", multiplication(100, 200))
```

**Output:**
```text
multiplication took <measured time> seconds
Result: 20000
```

The measured time varies depending on the computer.

---

## 23. Program 3: Restrict Access to Admin Functions

```python
from functools import wraps


def admin_required(func):

    @wraps(func)
    def wrapper(role, *args, **kwargs):

        if role != "admin":
            print("Access Denied")
            return None

        return func(role, *args, **kwargs)

    return wrapper


@admin_required
def delete_user(role, username):
    print(f"User {username} deleted successfully")


delete_user("user", "Aman")
delete_user("admin", "Aman")
```

**Output:**
```text
Access Denied
User Aman deleted successfully
```

This is a basic demonstration. A production authorization system must obtain the user's role from trusted authentication and authorization data.

---

# PART 4 – MINI PROJECT

## 24. Mini Project: Function Monitoring and Access Control System

### Project Description

Create a system that uses decorators to monitor function execution and control access to protected operations.

The project should demonstrate:

- Basic decorators.
- Decorators with arguments.
- `*args` and `**kwargs`.
- `functools.wraps`.
- Execution time measurement.
- Logging.
- Authentication and authorization checks.

### Project Requirements

#### A. Create a Logging Decorator

Create a decorator named `log_activity`.

Requirements:

- Display the function name before execution.
- Display a completion message after execution.
- Preserve the original function's return value.
- Use `@wraps`.

#### B. Create an Execution Time Decorator

Create a decorator named `execution_timer`.

Requirements:

- Record the start time.
- Execute the original function.
- Record the end time.
- Display the total execution time.
- Return the original result.

#### C. Create an Authentication Decorator

Create a decorator named `login_required`.

Requirements:

- Check whether the user is authenticated.
- Prevent execution when the user is not authenticated.
- Allow execution when the user is authenticated.

Use a trusted application-side authentication state for this learning exercise. Do not treat user-provided input alone as proof of identity.

#### D. Create an Admin Authorization Decorator

Create a decorator named `admin_required`.

Requirements:

- Check the user's role.
- Allow only administrators to access protected operations.
- Display an access-denied message for other roles.

#### E. Create a Repeat Decorator

Create a parameterized decorator named `repeat`.

Requirements:

- Accept the number of repetitions.
- Execute the decorated function the specified number of times.
- Support function arguments.

#### F. Create Protected Functions

Implement these functions:

1. `view_dashboard()`
2. `view_profile()`
3. `delete_user()`
4. `generate_report()`
5. `calculate_total()`

Apply the appropriate decorators to each function.

### Sample Expected Output

```text
===== FUNCTION MONITORING SYSTEM =====

Calling function: view_dashboard
Dashboard opened successfully
Finished function: view_dashboard

Calling function: delete_user
Access Denied: Admin privileges required

Calling function: generate_report
Report generated successfully
Execution Time: <measured time> seconds

Calling function: calculate_total
Result: 150
```

### Project Challenge

After completing the basic project, add:

1. A decorator that validates email addresses.
2. A decorator that prevents repeated function calls within a specified interval.
3. A decorator that records function errors.
4. A decorator that caches function results.
5. A decorator that counts how many times a function is called.
6. A decorator that checks whether required arguments are provided.

---

# PART 5 – STUDENT PRACTICE

## 25. Practice Questions

### Basic Level

1. What is a decorator in Python?
2. What are first-class functions?
3. What is a nested function?
4. What is a closure?
5. What is the purpose of `@` syntax?
6. What is the difference between a normal function and a decorator?
7. Why do decorators return wrapper functions?
8. What is the purpose of `*args` and `**kwargs` in a wrapper?
9. What does `functools.wraps` do?
10. What is a parameterized decorator?

### Intermediate Level

11. Create a decorator that displays a message before and after a function call.

12. Create a decorator that accepts functions with positional arguments.

13. Create a decorator that accepts functions with keyword arguments.

14. Create a decorator that measures function execution time.

15. Create a decorator that counts the number of times a function is called.

16. Create a decorator that executes a function three times.

17. Create a decorator that checks whether a number is positive.

18. Create a decorator that displays the name of the function being executed.

19. Create a decorator that prevents execution if a user is not authenticated.

20. Create a decorator that preserves the original function's metadata.

### Advanced Level

21. Create a decorator that accepts a configurable message.

22. Create a decorator that records errors raised by a function.

23. Create a decorator that caches function results.

24. Create a decorator that checks whether a user has administrator privileges.

25. Create two decorators and apply both to the same function.

26. Create a class decorator that adds a new attribute to a class.

27. Create a decorator that restricts the number of function calls.

28. Create a decorator that validates email input before executing a function.

29. Explain the execution order of multiple decorators.

30. Build a reusable decorator that supports any function signature and preserves its return value and metadata.

---

# PART 6 – TRAINER ASSESSMENT

## 26. Practical Assessment

| Task | Marks |
|---|---:|
| Explain first-class functions and closures | 10 |
| Create a basic decorator | 10 |
| Use the `@` decorator syntax | 10 |
| Handle positional and keyword arguments | 10 |
| Preserve return values and metadata | 10 |
| Create a parameterized decorator | 10 |
| Implement logging and execution timing | 15 |
| Implement authentication and authorization decorators | 15 |
| Complete the Function Monitoring System | 10 |
| **Total** | **100** |

### Oral Questions

1. What is a decorator?
2. Why are functions called first-class objects in Python?
3. What is a closure?
4. What is the purpose of a wrapper function?
5. What does `@decorator` mean internally?
6. Why should wrappers generally accept `*args` and `**kwargs`?
7. Why should a wrapper return the original function's result?
8. What is the purpose of `functools.wraps`?
9. How do parameterized decorators work?
10. What is the difference between a function decorator and a class decorator?
11. How can decorators be used for authentication?
12. How are multiple decorators applied to a function?

---

## 27. Completion Criteria

The student should be able to:

- Explain first-class functions.
- Pass functions as arguments and return functions.
- Understand nested functions and closures.
- Create basic decorators.
- Apply decorators using `@` syntax.
- Handle positional and keyword arguments in decorators.
- Preserve function return values.
- Use `functools.wraps`.
- Create decorators with parameters.
- Apply multiple decorators to one function.
- Implement logging and execution-time decorators.
- Understand authentication and authorization use cases.
- Use built-in decorators such as `@staticmethod`, `@classmethod` and `@property`.
- Complete the Function Monitoring and Access Control System.

**Day 32 Completed – Python Decorators**

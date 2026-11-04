
# Day 21 – Return Values, Scope & Recursion

## 1. Introduction

In Day 19, we learned how to create functions and return values.

In Day 20, we learned different ways to pass arguments into functions.

Now we will explore three important concepts:

1. Return Values
2. Variable Scope
3. Recursion

These concepts are important when developing reusable and maintainable Python applications.

---

# Part 1 – Return Values

## 2. Understanding the return Statement

The `return` statement sends a value from a function back to the place where the function was called.

### Example 1: Basic return

```python
def calculate_sum(a, b):
    result = a + b
    return result

answer = calculate_sum(10, 20)

print(answer)
```

**Output:**
```text
30
```

Explanation:

1. The function receives `10` and `20`.
2. It calculates their sum.
3. `return result` sends `30` back.
4. The returned value is stored in `answer`.
5. `print()` displays the result.

## 3. Difference Between return and print

These two statements have different purposes.

| return | print |
|---|---|
| Sends a value back to the caller | Displays information on the screen |
| Can be stored in a variable | Does not return the displayed value |
| Can be used in further calculations | Mainly used for displaying output |
| Ends the current function execution | Does not end the function |

### Example

```python
def using_return():
    return 100

def using_print():
    print(100)

result1 = using_return()
result2 = using_print()

print("Return result:", result1)
print("Print result:", result2)
```

**Output:**
```text
100
Return result: 100
Print result: None
```

Why is `result2` equal to `None`?

Because `using_print()` displays `100`, but it does not explicitly return a value.

Python automatically returns `None` when a function finishes without a return statement.

## 4. Returning Multiple Values

Python allows a function to return multiple values.

Technically, Python packs these values into a tuple.

### Example 1: Return two values

```python
def calculate(a, b):
    total = a + b
    difference = a - b

    return total, difference

result = calculate(20, 10)

print(result)
print(type(result))
```

**Output:**
```text
(30, 10)
<class 'tuple'>
```

### Example 2: Unpacking returned values

```python
def calculate(a, b):
    return a + b, a - b, a * b, a / b

addition, subtraction, multiplication, division = calculate(20, 10)

print("Addition:", addition)
print("Subtraction:", subtraction)
print("Multiplication:", multiplication)
print("Division:", division)
```

**Output:**
```text
Addition: 30
Subtraction: 10
Multiplication: 200
Division: 2.0
```

### Example 3: Returning a dictionary

When a function needs to return several named results, a dictionary can be useful.

```python
def student_result(name, marks):
    total = sum(marks)
    average = total / len(marks)

    return {
        "name": name,
        "total": total,
        "average": average
    }

result = student_result("Raj", [80, 90, 85])

print(result)
print("Student:", result["name"])
print("Average:", result["average"])
```

**Output:**
```text
{'name': 'Raj', 'total': 255, 'average': 85.0}
Student: Raj
Average: 85.0
```

## 5. return Immediately Ends Function Execution

Once Python executes a `return` statement, the current function call ends.

### Example

```python
def check_number(number):
    if number > 0:
        return "Positive"

    print("This line executes only for non-positive numbers.")
    return "Zero or Negative"

print(check_number(10))
print(check_number(-5))
```

**Output:**
```text
Positive
This line executes only for non-positive numbers.
Zero or Negative
```

The first function call returns immediately when the condition is true.

### Example: Multiple return statements

```python
def check_age(age):
    if age < 0:
        return "Invalid age"
    elif age < 18:
        return "Minor"
    else:
        return "Adult"

print(check_age(-5))
print(check_age(15))
print(check_age(25))
```

**Output:**
```text
Invalid age
Minor
Adult
```

## 6. Returning None

A function can intentionally return `None`.

```python
def find_student(students, name):
    if name in students:
        return name

    return None

students = ["Raj", "Altaf", "Aman"]

result = find_student(students, "Rahul")

if result is None:
    print("Student not found")
else:
    print("Student found:", result)
```

**Output:**
```text
Student not found
```

`None` is useful when a function has no meaningful result to return.

## 7. Returning Functions Results to Other Functions

One function can use the returned value of another function.

### Example

```python
def calculate_total(price, quantity):
    return price * quantity

def calculate_discount(amount, percentage):
    return amount * percentage / 100

def generate_bill(price, quantity, discount_percentage):
    total = calculate_total(price, quantity)

    discount = calculate_discount(total, discount_percentage)

    final_amount = total - discount

    return final_amount

bill = generate_bill(1000, 3, 10)

print("Final Bill:", bill)
```

**Output:**
```text
Final Bill: 2700.0
```

This approach keeps each function responsible for one task.

---

# Part 2 – Variable Scope

## 8. What Is Variable Scope?

Variable scope defines where a variable can be accessed in a Python program.

Consider this example:

```python
name = "Raj"

def greet():
    message = "Hello"
    print(message, name)

greet()
```

**Output:**
```text
Hello Raj
```

Here:
- `name` is defined outside the function.
- `message` is defined inside the function.

Python has four important scope levels, commonly explained using the LEGB rule.

## 9. LEGB Rule

LEGB represents:

| Scope | Meaning |
|---|---|
| L | Local |
| E | Enclosing |
| G | Global |
| B | Built-in |

Python searches for a variable in this order:

1. Local scope
2. Enclosing function scope
3. Global scope
4. Built-in scope

Let's understand each one.

## 10. Local Scope

A variable created inside a function normally belongs to that function's local scope.

It can be accessed inside that function.

### Example

```python
def student():
    name = "Raj"
    age = 21

    print(name)
    print(age)

student()
```

**Output:**
```text
Raj
21
```

### Accessing a Local Variable Outside

```python
def student():
    name = "Raj"

student()

print(name)
```

**Error:**
```text
NameError: name 'name' is not defined
```

Reason: `name` is a local variable and cannot normally be accessed outside the function.

## 11. Global Scope

A variable defined at the module level, outside functions and classes, belongs to the global scope.

It can be read inside functions.

### Example

```python
company = "ABC Technologies"

def employee():
    print("Company:", company)

employee()
print("Outside:", company)
```

**Output:**
```text
Company: ABC Technologies
Outside: ABC Technologies
```

### Modifying a Global Variable Using global

If we want to reassign a global variable inside a function, we can use the `global` keyword.

```python
balance = 1000

def deposit(amount):
    global balance

    balance += amount

deposit(500)

print("Balance:", balance)
```

**Output:**
```text
Balance: 1500
```

Explanation:

- `global balance` tells Python that `balance` refers to the module-level variable.
- The function updates the original global variable.

### Important: Reading vs Reassigning

Reading a global variable does not require `global`.

```python
count = 10

def display_count():
    print(count)

display_count()
```

**Output:**
```text
10
```

But assigning to a variable inside a function creates a local binding unless declared otherwise.

```python
count = 10

def update_count():
    count = 20
    print("Inside:", count)

update_count()

print("Outside:", count)
```

**Output:**
```text
Inside: 20
Outside: 10
```

The global variable remains unchanged.

## 12. Enclosing Scope

Enclosing scope occurs when one function is defined inside another function.

The inner function can access variables from the outer function.

### Example

```python
def outer_function():

    message = "Hello from outer function"

    def inner_function():
        print(message)

    inner_function()

outer_function()
```

**Output:**
```text
Hello from outer function
```

Here:
- `message` belongs to the enclosing function.
- `inner_function()` can access it.

### Example: Nested Function

```python
def calculate():

    number = 10

    def multiply():
        result = number * 5
        print("Result:", result)

    multiply()

calculate()
```

**Output:**
```text
Result: 50
```

## 13. Modifying Enclosing Variables Using nonlocal

The `nonlocal` keyword allows an inner function to reassign a variable from its nearest enclosing function scope.

### Example

```python
def outer_function():

    count = 10

    def inner_function():
        nonlocal count
        count += 5

    inner_function()

    print("Count:", count)

outer_function()
```

**Output:**
```text
Count: 15
```

Without `nonlocal`, assigning to `count` inside `inner_function()` would create a new local variable.

### Difference Between global and nonlocal

| global | nonlocal |
|---|---|
| Refers to a module-level variable | Refers to a variable in an enclosing function |
| Used to reassign global variables | Used to reassign enclosing variables |
| Cannot refer to a variable that exists only in an outer function | Cannot refer to a module-level variable |

## 14. Built-in Scope

Python provides many built-in names that can be accessed without importing a module.

Examples:

```python
print("Hello")

numbers = [10, 20, 30]

print(len(numbers))
print(max(numbers))
print(sum(numbers))
```

**Output:**
```text
Hello
3
30
60
```

Here, `print()`, `len()`, `max()` and `sum()` are built-in functions.

### Important Warning

Avoid naming your variables after built-in functions.

Incorrect:

```python
list = [10, 20, 30]

print(list)
```

This shadows the built-in name `list`.

Prefer:

```python
numbers = [10, 20, 30]

print(numbers)
```

Other built-in names to avoid shadowing include:
- `str`
- `int`
- `dict`
- `set`
- `sum`
- `max`
- `min`

---

# Part 3 – Recursion

## 15. What Is Recursion?

Recursion is a programming technique in which a function calls itself to solve a problem.

A recursive function breaks a problem into smaller versions of the same problem.

A recursive function generally needs two important components:

1. Base Case – The condition that stops recursion.
2. Recursive Case – The part where the function calls itself with a smaller or simpler input.

### Basic Example

```python
def countdown(number):

    if number == 0:
        print("Finished")
        return

    print(number)

    countdown(number - 1)

countdown(5)
```

**Output:**
```text
5
4
3
2
1
Finished
```

Explanation:

1. `countdown(5)` prints 5.
2. It calls `countdown(4)`.
3. The next call prints 4 and calls `countdown(3)`.
4. This continues until the number becomes 0.
5. The base case stops further recursive calls.

### Visual Flow

```text
countdown(5)
     |
     v
countdown(4)
     |
     v
countdown(3)
     |
     v
countdown(2)
     |
     v
countdown(1)
     |
     v
countdown(0)
     |
     v
  Finished
```

## 16. Understanding the Base Case

A base case is essential.

Without it, a recursive function may keep calling itself until Python raises a `RecursionError`.

### Incorrect Example

```python
def repeat():
    print("Hello")
    repeat()

repeat()
```

This function has no stopping condition.

Eventually, Python raises:

```text
RecursionError: maximum recursion depth exceeded
```

### Correct Example

```python
def repeat(number):

    if number == 0:
        return

    print("Hello")

    repeat(number - 1)

repeat(3)
```

**Output:**
```text
Hello
Hello
Hello
```

The base case ensures that recursion stops.

## 17. Factorial Using Recursion

Factorial is the product of all positive integers from 1 to a given number.

For example:

```text
5! = 5 × 4 × 3 × 2 × 1 = 120
```

Also:

```text
0! = 1
```

### Recursive Program

```python
def factorial(number):

    if number == 0 or number == 1:
        return 1

    return number * factorial(number - 1)

print(factorial(5))
print(factorial(4))
print(factorial(0))
```

**Output:**
```text
120
24
1
```

### Understanding the Calculation

For `factorial(5)`:

```text
factorial(5)
= 5 × factorial(4)
= 5 × 4 × factorial(3)
= 5 × 4 × 3 × factorial(2)
= 5 × 4 × 3 × 2 × factorial(1)
= 5 × 4 × 3 × 2 × 1
= 120
```

The recursive calls first move towards the base case. Then the pending multiplication operations are completed as the calls return.

## 18. Sum of Natural Numbers Using Recursion

Create a function that calculates the sum from 1 to `n`.

Example:

```text
1 + 2 + 3 + 4 + 5 = 15
```

### Program

```python
def natural_sum(number):

    if number == 0:
        return 0

    return number + natural_sum(number - 1)

print(natural_sum(5))
```

**Output:**
```text
15
```

## 19. Fibonacci Series Using Recursion

The Fibonacci sequence starts with 0 and 1.

Each following number is the sum of the previous two numbers.

```text
0, 1, 1, 2, 3, 5, 8, 13, 21
```

### Recursive Function

```python
def fibonacci(number):

    if number <= 1:
        return number

    return fibonacci(number - 1) + fibonacci(number - 2)

for i in range(8):
    print(fibonacci(i), end=" ")
```

**Output:**
```text
0 1 1 2 3 5 8 13
```

**Important:** This simple recursive implementation repeats many calculations and becomes slow for larger inputs. We will explore more efficient approaches later.

## 20. Reverse a String Using Recursion

```python
def reverse_string(text):

    if len(text) <= 1:
        return text

    return reverse_string(text[1:]) + text[0]

print(reverse_string("Python"))
```

**Output:**
```text
nohtyP
```

Explanation:

- The function takes the string without its first character.
- It recursively reverses the remaining string.
- It adds the first character at the end.
- The base case handles strings with zero or one character.

## 21. Find the Power of a Number Using Recursion

Calculate:

```text
2^4 = 2 × 2 × 2 × 2 = 16
```

### Program

```python
def power(base, exponent):

    if exponent == 0:
        return 1

    return base * power(base, exponent - 1)

print(power(2, 4))
print(power(3, 3))
```

**Output:**
```text
16
27
```

This implementation assumes the exponent is a non-negative integer.

---

# Part 4 – Recursion vs Iteration

## 22. Understanding the Difference

Iteration uses loops such as `for` and `while`.

Recursion uses a function calling itself.

### Example: Factorial Using a Loop

```python
def factorial_loop(number):

    result = 1

    for i in range(1, number + 1):
        result *= i

    return result

print(factorial_loop(5))
```

**Output:**
```text
120
```

### Example: Factorial Using Recursion

```python
def factorial_recursive(number):

    if number <= 1:
        return 1

    return number * factorial_recursive(number - 1)

print(factorial_recursive(5))
```

**Output:**
```text
120
```

### Comparison

| Iteration | Recursion |
|---|---|
| Uses loops | Uses function calls |
| Usually uses less call-stack memory | Uses additional call-stack memory |
| Often faster for simple repetitive tasks | Can make recursive problems easier to express |
| Stops when loop condition becomes false | Stops when base case is reached |
| Suitable for repeated calculations | Useful for naturally recursive structures |

### When Should We Use Recursion?

Recursion can be useful for:
- Tree traversal.
- Directory and folder traversal.
- Nested data structures.
- Divide-and-conquer algorithms.
- Mathematical problems with recursive definitions.

For simple repetition, loops are often more efficient.

---

# Part 5 – Practical Programs

## Program 1: Calculator Using Return Values

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


print("Addition:", add(20, 10))
print("Subtraction:", subtract(20, 10))
print("Multiplication:", multiply(20, 10))

result = divide(20, 0)

if result is None:
    print("Cannot divide by zero")
else:
    print("Division:", result)
```

**Output:**
```text
Addition: 30
Subtraction: 10
Multiplication: 200
Cannot divide by zero
```

## Program 2: Student Result Using Multiple Return Values

```python
def calculate_result(marks):

    total = sum(marks)
    average = total / len(marks)

    if average >= 75:
        grade = "A"
    elif average >= 60:
        grade = "B"
    elif average >= 40:
        grade = "C"
    else:
        grade = "Fail"

    return total, average, grade


marks = [80, 90, 75, 85]

total, average, grade = calculate_result(marks)

print("Total:", total)
print("Average:", average)
print("Grade:", grade)
```

**Output:**
```text
Total: 330
Average: 82.5
Grade: A
```

## Program 3: Bank Account Using Enclosing Scope and nonlocal

```python
def create_account(initial_balance):

    balance = initial_balance

    def deposit(amount):

        nonlocal balance

        if amount <= 0:
            return "Invalid deposit amount"

        balance += amount

        return balance

    def withdraw(amount):

        nonlocal balance

        if amount <= 0:
            return "Invalid withdrawal amount"

        if amount > balance:
            return "Insufficient balance"

        balance -= amount

        return balance

    def check_balance():
        return balance

    return deposit, withdraw, check_balance


deposit, withdraw, check_balance = create_account(1000)

print("Initial Balance:", check_balance())

print("After Deposit:", deposit(500))

print("After Withdrawal:", withdraw(200))

print("Final Balance:", check_balance())
```

**Output:**
```text
Initial Balance: 1000
After Deposit: 1500
After Withdrawal: 1300
Final Balance: 1300
```

This example demonstrates a closure: the returned inner functions retain access to the enclosing function's `balance` variable.

## Program 4: Recursive Number Analysis

```python
def count_digits(number):

    number = abs(number)

    if number < 10:
        return 1

    return 1 + count_digits(number // 10)


print(count_digits(12345))
print(count_digits(987))
print(count_digits(-1234))
```

**Output:**
```text
5
3
4
```

## Program 5: Recursive Palindrome Checker

```python
def is_palindrome(text):

    if len(text) <= 1:
        return True

    if text[0] != text[-1]:
        return False

    return is_palindrome(text[1:-1])


print(is_palindrome("madam"))
print(is_palindrome("level"))
print(is_palindrome("python"))
```

**Output:**
```text
True
True
False
```

This example checks the first and last characters, then recursively checks the remaining substring.

---

# Part 6 – Mini Project

## 23. Mini Project – Bank Account Management System

### Project Description

Create a simple Bank Account Management System using functions, return values, variable scope and nested functions.

The application should support:

1. Account creation.
2. Deposit money.
3. Withdraw money.
4. Check balance.
5. Display transaction history.
6. Validate transactions.

### Project Requirements

Create the following functions:

- `create_account()`
- `deposit()`
- `withdraw()`
- `check_balance()`
- `show_transactions()`
- `main()`

Use an enclosing function to maintain account state.

Use `nonlocal` when updating the balance from inner functions.

Use return values to communicate transaction results.

### Sample Code

```python
def create_account(owner, initial_balance=0):

    balance = initial_balance
    transactions = []

    def deposit(amount):

        nonlocal balance

        if amount <= 0:
            return "Invalid deposit amount"

        balance += amount

        transactions.append({
            "type": "Deposit",
            "amount": amount,
            "balance": balance
        })

        return f"Deposit successful. Balance: {balance}"

    def withdraw(amount):

        nonlocal balance

        if amount <= 0:
            return "Invalid withdrawal amount"

        if amount > balance:
            return "Insufficient balance"

        balance -= amount

        transactions.append({
            "type": "Withdrawal",
            "amount": amount,
            "balance": balance
        })

        return f"Withdrawal successful. Balance: {balance}"

    def check_balance():
        return balance

    def show_transactions():

        if not transactions:
            return "No transactions found"

        return transactions.copy()

    def get_owner():
        return owner

    return deposit, withdraw, check_balance, show_transactions, get_owner


def main():

    deposit, withdraw, check_balance, show_transactions, get_owner = create_account(
        "Raj",
        5000
    )

    print("Account Owner:", get_owner())
    print("Initial Balance:", check_balance())

    print("\nDepositing Rs. 2000")
    print(deposit(2000))

    print("\nWithdrawing Rs. 1500")
    print(withdraw(1500))

    print("\nCurrent Balance:", check_balance())

    print("\nTransaction History:")

    history = show_transactions()

    for transaction in history:
        print(transaction)


main()
```

### Expected Output

```text
Account Owner: Raj
Initial Balance: 5000

Depositing Rs. 2000
Deposit successful. Balance: 7000

Withdrawing Rs. 1500
Withdrawal successful. Balance: 5500

Current Balance: 5500

Transaction History:
{'type': 'Deposit', 'amount': 2000, 'balance': 7000}
{'type': 'Withdrawal', 'amount': 1500, 'balance': 5500}
```

### Project Extension Tasks

After completing the basic project:

1. Add an account number.
2. Add a PIN verification system.
3. Allow multiple accounts.
4. Add money transfer between accounts.
5. Prevent invalid account operations.
6. Add transaction dates using the `datetime` module.
7. Display the last five transactions.
8. Add a menu-driven interface.
9. Store account information in a dictionary.
10. Add a transaction summary showing total deposits and withdrawals.

**Trainer Note:** This is a learning project, not a production banking application. Real financial systems require secure authentication, persistent storage, transaction integrity and additional security controls.

---

# Part 7 – Student Practice Exercises

## Exercise 1 – Return Values

Create a function that accepts three numbers and returns:

- Sum
- Average
- Maximum

## Exercise 2 – Multiple Return Values

Create a function that accepts a student's name and marks and returns:

- Student name
- Total marks
- Average marks
- Grade

## Exercise 3 – Local and Global Scope

Create a global variable `company`.

Create a function that:
- Displays the company name.
- Creates a local variable `employee`.
- Displays both variables.

## Exercise 4 – global Keyword

Create a global variable `counter = 0`.

Create a function that increments the counter using `global`.

Call the function five times and display the final value.

## Exercise 5 – nonlocal Keyword

Create an outer function containing a variable `balance`.

Create an inner function that modifies the balance using `nonlocal`.

## Exercise 6 – Factorial Using Recursion

Create a recursive function that calculates the factorial of a number.

Validate that the input is a non-negative integer.

## Exercise 7 – Fibonacci Using Recursion

Create a recursive function that returns the Fibonacci number at a given position.

Test the first ten positions.

## Exercise 8 – Reverse a String

Create a recursive function that reverses a string without using slicing shortcuts such as `[::-1]`.

## Exercise 9 – Palindrome Checker

Create a recursive function that checks whether a string is a palindrome.

## Exercise 10 – Recursive Sum

Create a recursive function that calculates the sum of all digits in a number.

Example:

```text
Input: 1234
Output: 10
```

## Exercise 11 – Scope Challenge

Create nested functions:

- Outer function defines `x`.
- Inner function reads `x`.
- Another inner function modifies `x` using `nonlocal`.

Observe the difference.

## Exercise 12 – Real-World Challenge

Create an Employee Salary Management System that:

- Stores employee information.
- Calculates salary using separate functions.
- Returns salary breakdowns using dictionaries.
- Uses nested functions to maintain temporary calculation settings.
- Supports bonus and deductions.
- Displays the final salary report.

---

# Part 8 – Trainer Assessment

## 24. Theory Assessment

| Question | Expected Understanding |
|---|---|
| What does `return` do? | Sends a value back to the caller |
| What happens if a function has no return statement? | It returns `None` |
| Can a function return multiple values? | Yes, Python packs them into a tuple |
| What is local scope? | Scope inside a function |
| What is global scope? | Module-level scope |
| What is enclosing scope? | Scope of an outer function |
| What is built-in scope? | Names provided by Python |
| What is the LEGB rule? | Local, Enclosing, Global, Built-in lookup order |
| What does `global` do? | Allows reassignment of a global variable |
| What does `nonlocal` do? | Allows reassignment of an enclosing variable |
| What is recursion? | A function calling itself |
| What is a base case? | Condition that stops recursion |
| What is a recursive case? | The part that calls the function again |
| What is a closure? | An inner function retaining access to enclosing variables |
| What is the difference between iteration and recursion? | Loops vs repeated function calls |

## 25. Practical Assessment

Ask the student to independently:

1. Create a function that returns multiple values.
2. Demonstrate local and global scope.
3. Modify an enclosing variable using `nonlocal`.
4. Write a recursive factorial function.
5. Write a recursive palindrome checker.
6. Explain the base case and recursive case.
7. Complete the Bank Account Management System.

---

# 26. Completion Criteria

Mark Day 21 as completed when the student can:

- Use `return` correctly.
- Explain the difference between `return` and `print()`.
- Return multiple values from functions.
- Return dictionaries and other collections.
- Understand local, enclosing, global and built-in scope.
- Apply the LEGB rule.
- Use `global` and `nonlocal` correctly.
- Understand nested functions and closures.
- Create recursive functions.
- Identify base cases and recursive cases.
- Solve factorial, Fibonacci and string problems using recursion.
- Compare recursion with iteration.
- Complete the Bank Account Management System independently.

**Trainer Note:** Pay special attention to variable scope and recursion. The student should be able to trace function calls manually and explain how values move through each call.

---

**End of Day 21 – Return Values, Scope & Recursion**


# Day 26 – Exception Handling

## 1. Introduction to Errors and Exceptions

Errors are problems in a program that prevent it from working as expected.

Python errors can broadly be understood in two categories:

### 1.1 Syntax Errors

Syntax errors occur when Python code does not follow the correct language syntax.

Example:

```python
if 10 > 5
    print("Ten is greater")
```

Output:

```text
SyntaxError: expected ':'
```

The colon is missing after the condition.

### 1.2 Exceptions

Exceptions are errors that occur while a program is running.

Example:

```python
num1 = 10
num2 = 0

result = num1 / num2

print(result)
```

Output:

```text
ZeroDivisionError: division by zero
```

The syntax is correct, but the program cannot divide a number by zero.

Other common exceptions include:

- `ValueError`
- `TypeError`
- `NameError`
- `IndexError`
- `KeyError`
- `FileNotFoundError`
- `ZeroDivisionError`
- `AttributeError`

---

## 2. Why Exception Handling Is Important

Without exception handling, an unexpected error can stop the entire program.

Example:

```python
print("Program started")

num1 = 10
num2 = 0

result = num1 / num2

print("Result:", result)
print("Program completed")
```

Output:

```text
Program started
ZeroDivisionError: division by zero
```

The remaining statements are not executed.

Exception handling allows us to:

- Prevent unexpected program termination.
- Display meaningful error messages.
- Handle invalid user input.
- Handle file-related problems.
- Keep applications running safely.
- Perform cleanup operations.

---

## 3. The try and except Blocks

Python provides `try` and `except` to handle exceptions.

### Syntax

```python
try:
    # Code that may cause an exception

except:
    # Code that handles the exception
```

### Example

```python
try:
    num1 = 10
    num2 = 0

    result = num1 / num2

    print("Result:", result)

except:
    print("Something went wrong!")

print("Program continues...")
```

Output:

```text
Something went wrong!
Program continues...
```

The `try` block contains code that may produce an exception.

If an exception occurs, Python skips the remaining statements inside that `try` block and executes the matching `except` block.

**Important:** Avoid using a bare `except` in normal application code. Catch specific exceptions so that unexpected programming errors are not hidden.

---

## 4. Handling Specific Exceptions

Instead of catching every exception, handle the exact exception you expect.

### Example: ZeroDivisionError

```python
try:
    num1 = 10
    num2 = 0

    result = num1 / num2

    print("Result:", result)

except ZeroDivisionError:
    print("Cannot divide by zero!")
```

Output:

```text
Cannot divide by zero!
```

### Example: ValueError

```python
try:
    age = int(input("Enter your age: "))

    print("Your age is:", age)

except ValueError:
    print("Please enter a valid number!")
```

Sample input:

```text
Enter your age: hello
```

Output:

```text
Please enter a valid number!
```

`ValueError` occurs because Python cannot convert `"hello"` into an integer.

### Example: TypeError

```python
try:
    result = "Python" + 10

    print(result)

except TypeError:
    print("Cannot combine these data types directly!")
```

Output:

```text
Cannot combine these data types directly!
```

---

## 5. Multiple except Blocks

A single `try` block can have multiple `except` blocks.

### Example

```python
try:
    num1 = int(input("Enter first number: "))
    num2 = int(input("Enter second number: "))

    result = num1 / num2

    print("Result:", result)

except ValueError:
    print("Please enter valid numbers!")

except ZeroDivisionError:
    print("Cannot divide by zero!")
```

Sample 1:

```text
Enter first number: abc
Please enter valid numbers!
```

Sample 2:

```text
Enter first number: 10
Enter second number: 0
Cannot divide by zero!
```

Python executes the first matching `except` block.

### 5.1 Handling Multiple Exception Types Together

You can handle multiple exception types using a tuple.

```python
try:
    numbers = [10, 20, 30]

    index = int(input("Enter index: "))

    print(numbers[index])

except (ValueError, IndexError):
    print("Invalid input or index!")
```

This handles both:

- `ValueError`: If the user enters non-numeric input.
- `IndexError`: If the index does not exist.

### 5.2 Exception Hierarchy Basics

Python exceptions are organized in a hierarchy.

Some examples:

```text
BaseException
    |
    +-- Exception
          |
          +-- ArithmeticError
          |      |
          |      +-- ZeroDivisionError
          |
          +-- LookupError
          |      |
          |      +-- IndexError
          |      +-- KeyError
          |
          +-- ValueError
          +-- TypeError
          +-- NameError
          +-- OSError
                 |
                 +-- FileNotFoundError
                 +-- PermissionError
```

You can catch a parent exception to handle its subclasses.

For example, `ArithmeticError` can catch `ZeroDivisionError`.

However, prefer the most specific exception that makes sense for your program.

---

## 6. The else Block

The `else` block executes only when no exception occurs inside the `try` block.

### Syntax

```python
try:
    # Risky code

except SomeException:
    # Error handling

else:
    # Executes when no exception occurs
```

### Example

```python
try:
    num1 = int(input("Enter first number: "))
    num2 = int(input("Enter second number: "))

    result = num1 / num2

except ValueError:
    print("Please enter valid numbers!")

except ZeroDivisionError:
    print("Cannot divide by zero!")

else:
    print("Result:", result)
    print("Calculation successful!")
```

Sample successful output:

```text
Enter first number: 20
Enter second number: 5
Result: 4.0
Calculation successful!
```

The `else` block is useful for keeping successful operations separate from error-handling code.

---

## 7. The finally Block

The `finally` block executes whether an exception occurs or not.

### Syntax

```python
try:
    # Risky code

except SomeException:
    # Handle exception

finally:
    # Cleanup code
```

### Example

```python
try:
    num = int(input("Enter a number: "))

    print("Number:", num)

except ValueError:
    print("Invalid number!")

finally:
    print("Program execution finished.")
```

Successful output:

```text
Enter a number: 25
Number: 25
Program execution finished.
```

Invalid input:

```text
Enter a number: hello
Invalid number!
Program execution finished.
```

### 7.1 Practical Use of finally

The `finally` block is commonly used for cleanup operations, such as releasing resources.

```python
file = None

try:
    file = open("sample.txt", "r", encoding="utf-8")

    content = file.read()

    print(content)

except FileNotFoundError:
    print("File does not exist!")

finally:
    if file is not None:
        file.close()

    print("File operation completed.")
```

**Note:** When working with files, the `with open(...)` context manager is generally preferred because it closes the file automatically.

---

## 8. The raise Keyword

The `raise` keyword allows us to manually generate an exception.

It is useful when a program detects invalid data or an operation that should not be allowed.

### Example

```python
age = 15

if age < 18:
    raise ValueError("Age must be 18 or above")

print("Access granted")
```

Output:

```text
ValueError: Age must be 18 or above
```

The program stops because the exception is not handled.

### 8.1 Handling a Manually Raised Exception

```python
try:
    age = int(input("Enter your age: "))

    if age < 18:
        raise ValueError("You must be 18 or above")

    print("Access granted!")

except ValueError as error:
    print("Error:", error)
```

Sample output:

```text
Enter your age: 15
Error: You must be 18 or above
```

### 8.2 Re-raising an Exception

Sometimes we want to perform an action and then allow the original exception to continue to the caller.

```python
try:
    num = int("hello")

except ValueError:
    print("Conversion failed!")
    raise
```

Output:

```text
Conversion failed!
ValueError: invalid literal for int() with base 10: 'hello'
```

The `raise` statement without an exception re-raises the current exception.

---

## 9. Exception Objects Using as

You can store the exception object in a variable using `as`.

### Syntax

```python
try:
    # Risky code

except ExceptionType as error:
    print(error)
```

### Example

```python
try:
    num = int("Python")

except ValueError as error:
    print("An error occurred:")
    print(error)
```

Output:

```text
An error occurred:
invalid literal for int() with base 10: 'Python'
```

The variable `error` contains information about the exception.

You can use this information for debugging and logging.

**Important:** Do not expose sensitive internal error details to ordinary application users. Show them a simple message and keep technical details in logs when needed.

---

## 10. Custom Exceptions

Python provides built-in exceptions, but sometimes an application needs its own exception types.

We can create custom exceptions by defining classes that inherit from `Exception`.

### Example

```python
class InvalidAgeError(Exception):
    pass


age = int(input("Enter your age: "))

if age < 18:
    raise InvalidAgeError("Age must be 18 or above")

print("You are eligible!")
```

Sample output:

```text
Enter your age: 15
InvalidAgeError: Age must be 18 or above
```

### 10.1 Handling Custom Exceptions

```python
class InvalidAgeError(Exception):
    pass


try:
    age = int(input("Enter your age: "))

    if age < 18:
        raise InvalidAgeError("Age must be 18 or above")

    print("You are eligible!")

except ValueError:
    print("Enter a valid numeric age!")

except InvalidAgeError as error:
    print("Validation Error:", error)
```

Output:

```text
Enter your age: 15
Validation Error: Age must be 18 or above
```

### 10.2 Creating Multiple Custom Exceptions

```python
class InvalidAmountError(Exception):
    pass


class InsufficientFundsError(Exception):
    pass


balance = 1000

try:
    amount = float(input("Enter withdrawal amount: "))

    if amount <= 0:
        raise InvalidAmountError("Amount must be greater than zero")

    if amount > balance:
        raise InsufficientFundsError("Insufficient account balance")

    balance -= amount

    print("Withdrawal successful!")
    print("Remaining balance:", balance)

except ValueError:
    print("Please enter a valid amount!")

except InvalidAmountError as error:
    print("Invalid Amount:", error)

except InsufficientFundsError as error:
    print("Transaction Failed:", error)
```

Custom exception names commonly end with `Error`.

---

## 11. Exception Chaining

Exception chaining allows us to raise a new exception while preserving the original exception as its cause.

We use `raise ... from ...`.

### Example

```python
def convert_number(value):
    try:
        return int(value)

    except ValueError as error:
        raise ValueError("Number conversion failed") from error


try:
    result = convert_number("Python")

except ValueError as error:
    print("Error:", error)
```

Output:

```text
Error: Number conversion failed
```

The original conversion error remains available through the exception chain.

This is useful when converting a low-level error into a more meaningful application-level error.

---

## 12. The assert Statement

The `assert` statement checks whether a condition is true.

If the condition is false, Python raises an `AssertionError`.

### Syntax

```python
assert condition, "Error message"
```

### Example

```python
age = 20

assert age >= 18, "Age must be 18 or above"

print("Age is valid")
```

Output:

```text
Age is valid
```

Now change the age:

```python
age = 15

assert age >= 18, "Age must be 18 or above"

print("Age is valid")
```

Output:

```text
AssertionError: Age must be 18 or above
```

### Important Difference

- Use `assert` for internal assumptions and debugging.
- Use `raise` for application validation and errors that must be handled.
- Assertions can be disabled when Python runs with optimization (`python -O`).

Never depend on `assert` to validate ordinary user input.

---

## 13. Common Exception Types

| Exception | Meaning |
|---|---|
| `ValueError` | Correct type but invalid value |
| `TypeError` | Operation used with an incompatible type |
| `ZeroDivisionError` | Division by zero |
| `NameError` | Variable or name does not exist |
| `IndexError` | List or sequence index is out of range |
| `KeyError` | Dictionary key does not exist |
| `FileNotFoundError` | Requested file does not exist |
| `PermissionError` | Operation is not permitted |
| `AttributeError` | Object does not have the requested attribute |
| `ImportError` | Import operation fails |
| `ModuleNotFoundError` | Requested module cannot be found |
| `AssertionError` | An assertion condition is false |
| `RuntimeError` | General runtime problem |

---

## 14. Practical Programs

### Program 1: Safe Calculator

```python
try:
    num1 = float(input("Enter first number: "))
    operator = input("Enter operator (+, -, *, /): ")
    num2 = float(input("Enter second number: "))

    if operator == "+":
        result = num1 + num2

    elif operator == "-":
        result = num1 - num2

    elif operator == "*":
        result = num1 * num2

    elif operator == "/":
        result = num1 / num2

    else:
        raise ValueError("Invalid operator")

except ValueError as error:
    print("Input Error:", error)

except ZeroDivisionError:
    print("Cannot divide by zero!")

else:
    print("Result:", result)

finally:
    print("Calculator operation completed.")
```

### Program 2: Numeric Input Validation

```python
while True:
    try:
        number = int(input("Enter a positive number: "))

        if number <= 0:
            raise ValueError("Number must be positive")

        print("Accepted:", number)
        break

    except ValueError as error:
        print("Invalid input:", error)
```

The loop continues until the user enters a valid positive integer.

### Program 3: Safe File Reading

```python
filename = input("Enter file name: ")

try:
    with open(filename, "r", encoding="utf-8") as file:
        content = file.read()

except FileNotFoundError:
    print("File not found!")

except PermissionError:
    print("You do not have permission to read this file!")

else:
    print("File content:")
    print(content)

finally:
    print("File reading operation finished.")
```

### Program 4: Age Validation

```python
class InvalidAgeError(Exception):
    pass


try:
    age = int(input("Enter your age: "))

    if age < 0 or age > 120:
        raise InvalidAgeError("Enter an age between 0 and 120")

except ValueError:
    print("Age must be a whole number!")

except InvalidAgeError as error:
    print("Validation Error:", error)

else:
    print("Your age is:", age)
```

### Program 5: Bank Withdrawal

```python
balance = 5000

try:
    amount = float(input("Enter withdrawal amount: "))

    if amount <= 0:
        raise ValueError("Amount must be greater than zero")

    if amount > balance:
        raise ValueError("Insufficient balance")

    balance -= amount

except ValueError as error:
    print("Transaction failed:", error)

else:
    print("Withdrawal successful!")
    print("Remaining balance:", balance)

finally:
    print("Thank you for using our banking service.")
```

### Program 6: Safe List Access

```python
numbers = [10, 20, 30, 40, 50]

try:
    index = int(input("Enter list index: "))

    print("Value:", numbers[index])

except ValueError:
    print("Please enter an integer index!")

except IndexError:
    print("Index does not exist!")
```

---

## 15. Exception Handling Best Practices

Follow these practices while developing Python applications:

1. Catch specific exceptions instead of using bare `except`.
2. Keep the `try` block as small as reasonably possible.
3. Use `else` for code that should run only after successful execution.
4. Use `finally` when cleanup must happen regardless of success or failure.
5. Use `with` for files and other supported resource managers.
6. Use custom exceptions for application-specific errors.
7. Do not silently ignore errors using `except: pass`.
8. Avoid catching `BaseException` in ordinary application code. It also includes special exceptions such as `KeyboardInterrupt` and `SystemExit`.
9. Use `raise` when an operation violates a required rule.
10. Use logging for technical error details in larger applications.
11. Do not use exceptions as a replacement for ordinary conditional checks.
12. Write clear and meaningful error messages.

---

# 16. Mini Project – Bank Transaction Management System

## Project Description

Create a menu-driven Bank Transaction Management System.

The application should allow users to:

- Create a bank account.
- Deposit money.
- Withdraw money.
- Transfer money between accounts.
- Check account balance.
- View transaction history.
- Handle invalid input and transaction errors.

The project will use custom exceptions and structured exception handling.

## Complete Project Code

```python
class InvalidAmountError(Exception):
    pass


class InsufficientFundsError(Exception):
    pass


class AccountNotFoundError(Exception):
    pass


class BankAccount:
    def __init__(self, account_number, holder_name, balance=0):
        self.account_number = account_number
        self.holder_name = holder_name
        self.balance = balance
        self.transactions = []

    def deposit(self, amount):
        if amount <= 0:
            raise InvalidAmountError(
                "Deposit amount must be greater than zero"
            )

        self.balance += amount

        self.transactions.append(
            f"Deposited: Rs. {amount:.2f}"
        )

        return self.balance

    def withdraw(self, amount):
        if amount <= 0:
            raise InvalidAmountError(
                "Withdrawal amount must be greater than zero"
            )

        if amount > self.balance:
            raise InsufficientFundsError(
                "Insufficient account balance"
            )

        self.balance -= amount

        self.transactions.append(
            f"Withdrawn: Rs. {amount:.2f}"
        )

        return self.balance

    def transfer(self, receiver, amount):
        if amount <= 0:
            raise InvalidAmountError(
                "Transfer amount must be greater than zero"
            )

        if amount > self.balance:
            raise InsufficientFundsError(
                "Insufficient balance for transfer"
            )

        self.balance -= amount
        receiver.balance += amount

        self.transactions.append(
            f"Transferred Rs. {amount:.2f} "
            f"to {receiver.account_number}"
        )

        receiver.transactions.append(
            f"Received Rs. {amount:.2f} "
            f"from {self.account_number}"
        )

    def show_balance(self):
        print(f"Account Holder: {self.holder_name}")
        print(f"Account Number: {self.account_number}")
        print(f"Available Balance: Rs. {self.balance:.2f}")

    def show_transactions(self):
        print("\nTransaction History")

        if not self.transactions:
            print("No transactions available.")
            return

        for transaction in self.transactions:
            print("-", transaction)


class Bank:
    def __init__(self):
        self.accounts = {}

    def create_account(self):
        account_number = input("Enter account number: ").strip()

        if not account_number:
            print("Account number cannot be empty!")
            return

        if account_number in self.accounts:
            print("Account already exists!")
            return

        holder_name = input("Enter account holder name: ").strip()

        if not holder_name:
            print("Account holder name cannot be empty!")
            return

        self.accounts[account_number] = BankAccount(
            account_number,
            holder_name
        )

        print("Account created successfully!")

    def get_account(self, account_number):
        account = self.accounts.get(account_number)

        if account is None:
            raise AccountNotFoundError("Account not found")

        return account

    def deposit_money(self):
        account_number = input("Enter account number: ").strip()

        account = self.get_account(account_number)

        amount = float(input("Enter deposit amount: "))

        account.deposit(amount)

        print("Deposit successful!")
        account.show_balance()

    def withdraw_money(self):
        account_number = input("Enter account number: ").strip()

        account = self.get_account(account_number)

        amount = float(input("Enter withdrawal amount: "))

        account.withdraw(amount)

        print("Withdrawal successful!")
        account.show_balance()

    def transfer_money(self):
        sender_number = input("Enter sender account: ").strip()
        receiver_number = input("Enter receiver account: ").strip()

        sender = self.get_account(sender_number)
        receiver = self.get_account(receiver_number)

        if sender_number == receiver_number:
            raise ValueError(
                "Sender and receiver accounts must be different"
            )

        amount = float(input("Enter transfer amount: "))

        sender.transfer(receiver, amount)

        print("Transfer successful!")

    def check_balance(self):
        account_number = input("Enter account number: ").strip()

        account = self.get_account(account_number)

        account.show_balance()

    def transaction_history(self):
        account_number = input("Enter account number: ").strip()

        account = self.get_account(account_number)

        account.show_transactions()

    def run(self):
        while True:
            print("\n===== BANK TRANSACTION SYSTEM =====")
            print("1. Create Account")
            print("2. Deposit Money")
            print("3. Withdraw Money")
            print("4. Transfer Money")
            print("5. Check Balance")
            print("6. Transaction History")
            print("7. Exit")

            choice = input("Enter your choice: ").strip()

            try:
                if choice == "1":
                    self.create_account()

                elif choice == "2":
                    self.deposit_money()

                elif choice == "3":
                    self.withdraw_money()

                elif choice == "4":
                    self.transfer_money()

                elif choice == "5":
                    self.check_balance()

                elif choice == "6":
                    self.transaction_history()

                elif choice == "7":
                    print("Thank you for using our banking system!")
                    break

                else:
                    print("Invalid menu choice!")

            except ValueError as error:
                print("Input Error:", error)

            except InvalidAmountError as error:
                print("Amount Error:", error)

            except InsufficientFundsError as error:
                print("Transaction Error:", error)

            except AccountNotFoundError as error:
                print("Account Error:", error)

            finally:
                print("Operation completed.")


bank = Bank()
bank.run()
```

## Sample Output

```text
===== BANK TRANSACTION SYSTEM =====
1. Create Account
2. Deposit Money
3. Withdraw Money
4. Transfer Money
5. Check Balance
6. Transaction History
7. Exit

Enter your choice: 1

Enter account number: 101
Enter account holder name: Raj
Account created successfully!
Operation completed.

===== BANK TRANSACTION SYSTEM =====

Enter your choice: 2

Enter account number: 101
Enter deposit amount: 5000

Deposit successful!

Account Holder: Raj
Account Number: 101
Available Balance: Rs. 5000.00

Operation completed.

===== BANK TRANSACTION SYSTEM =====

Enter your choice: 3

Enter account number: 101
Enter withdrawal amount: 7000

Transaction Error: Insufficient account balance
Operation completed.
```

## Project Practice Tasks

After completing the project, improve it by adding:

1. Account search functionality.
2. Display all registered accounts.
3. Minimum balance requirements.
4. Transaction date and time using `datetime`.
5. Input validation for account numbers.
6. A maximum withdrawal limit.
7. Better transaction reports.
8. Save transaction history to a file.

**Note:** This project stores data in memory. Account information will be lost when the program closes. Persistent storage will be covered in later lessons.

---

# 17. Student Practice Exercises

## Basic Level

1. Write a program that handles division by zero.
2. Handle `ValueError` when converting user input into an integer.
3. Handle `IndexError` while accessing a list.
4. Handle `KeyError` while accessing a dictionary.
5. Write a program that uses `try`, `except`, and `finally`.

## Intermediate Level

6. Create a calculator that handles invalid operators and invalid numbers.
7. Create a program that repeatedly asks for positive numeric input.
8. Write a file-reading program that handles missing files and permission errors.
9. Create a custom `InvalidPasswordError` exception.
10. Create a program that validates a person's age using a custom exception.
11. Write a program using multiple `except` blocks and an `else` block.
12. Create a function that raises a custom exception for negative numbers.

## Advanced Level

13. Create a Student Marks Management System with custom exceptions for invalid marks.
14. Create a Shopping Cart that handles invalid quantities and unavailable products.
15. Create a Bank Account system with custom exceptions for insufficient balance and invalid transactions.
16. Create a file-processing application that handles multiple file-related exceptions.
17. Create a registration system that validates usernames, email addresses, and passwords using custom exceptions.

---

# 18. Trainer Assessment

Ask the student to explain and demonstrate:

1. What is the difference between a syntax error and an exception?
2. Why do we use exception handling?
3. What is the purpose of the `try` block?
4. Why should we catch specific exceptions?
5. What is the difference between `ValueError` and `TypeError`?
6. When does the `else` block execute?
7. When does the `finally` block execute?
8. What is the purpose of the `raise` keyword?
9. How do we create custom exceptions?
10. What is exception chaining?
11. What is the difference between `raise` and `assert`?
12. Why should we avoid `except: pass`?

## Practical Assessment

Ask the student to independently:

- Write a safe calculator.
- Validate user input.
- Handle file-related exceptions.
- Create and use at least two custom exceptions.
- Build a menu-driven banking application.

---

# 19. Day 26 Completion Criteria

The student should be able to:

- Understand errors and exceptions.
- Use `try` and `except` correctly.
- Handle specific exception types.
- Use multiple `except` blocks.
- Apply `else` and `finally`.
- Raise exceptions manually.
- Access exception messages using `as`.
- Create custom exception classes.
- Understand exception chaining.
- Use `assert` for debugging.
- Write reliable programs with proper error handling.
- Complete the Bank Transaction Management System.

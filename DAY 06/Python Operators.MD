
# Day 06 – Python Operators

## 1. Introduction to Operators

Operators are special symbols or keywords used to perform operations on values and variables.

For example:

```python
a = 10
b = 5

result = a + b

print(result)
```

Output:

```text
15
```

Here:
- `a` and `b` are operands.
- `+` is an operator.
- `result` stores the calculated value.

Python provides different categories of operators.

| Operator Category | Purpose |
|---|---|
| Arithmetic | Mathematical calculations |
| Assignment | Assign values to variables |
| Comparison | Compare two values |
| Logical | Combine conditions |
| Identity | Compare object identity |
| Membership | Check whether an element exists |
| Bitwise | Perform operations on binary bits |

---

## 2. Arithmetic Operators

Arithmetic operators are used to perform mathematical calculations.

| Operator | Name | Example | Result |
|---|---|---|---|
| `+` | Addition | `10 + 5` | `15` |
| `-` | Subtraction | `10 - 5` | `5` |
| `*` | Multiplication | `10 * 5` | `50` |
| `/` | Division | `10 / 5` | `2.0` |
| `//` | Floor Division | `10 // 3` | `3` |
| `%` | Modulus | `10 % 3` | `1` |
| `**` | Exponentiation | `2 ** 3` | `8` |

### 2.1 Addition (+)

Adds two numbers.

```python
a = 10
b = 5

print(a + b)
```

Output:

```text
15
```

### 2.2 Subtraction (-)

Subtracts the second number from the first.

```python
a = 10
b = 5

print(a - b)
```

Output:

```text
5
```

### 2.3 Multiplication (*)

Multiplies two numbers.

```python
a = 10
b = 5

print(a * b)
```

Output:

```text
50
```

### 2.4 Division (/)

Divides one number by another.

```python
a = 10
b = 3

print(a / b)
```

Output:

```text
3.3333333333333335
```

**Important:** The `/` operator returns a float, even when the division result is a whole number.

### 2.5 Floor Division (//)

Returns the quotient rounded down to the nearest integer value.

```python
a = 10
b = 3

print(a // b)
```

Output:

```text
3
```

Another example:

```python
print(-10 // 3)
```

Output:

```text
-4
```

Floor division rounds toward negative infinity, not simply toward zero.

### 2.6 Modulus (%)

Returns the remainder after division.

```python
a = 10
b = 3

print(a % b)
```

Output:

```text
1
```

Common use cases:
- Checking even and odd numbers.
- Divisibility checks.
- Finding remainders.

Example:

```python
number = 15

print(number % 2)
```

Output:

```text
1
```

### 2.7 Exponentiation (**)

Raises a number to a power.

```python
print(2 ** 3)
print(5 ** 2)
print(10 ** 3)
```

Output:

```text
8
25
1000
```

---

## 3. Assignment Operators

Assignment operators are used to assign values to variables and update existing values.

| Operator | Example | Equivalent Expression |
|---|---|---|
| `=` | `x = 10` | `x = 10` |
| `+=` | `x += 5` | `x = x + 5` |
| `-=` | `x -= 5` | `x = x - 5` |
| `*=` | `x *= 5` | `x = x * 5` |
| `/=` | `x /= 5` | `x = x / 5` |
| `//=` | `x //= 5` | `x = x // 5` |
| `%=` | `x %= 5` | `x = x % 5` |
| `**=` | `x **= 2` | `x = x ** 2` |

### Example 1: Basic Assignment

```python
age = 22

print(age)
```

### Example 2: Addition Assignment

```python
number = 10

number += 5

print(number)
```

Output:

```text
15
```

### Example 3: Subtraction Assignment

```python
number = 20

number -= 5

print(number)
```

Output:

```text
15
```

### Example 4: Multiple Assignment Operators

```python
number = 10

number += 5
print(number)

number *= 2
print(number)

number -= 10
print(number)

number //= 2
print(number)
```

Output:

```text
15
30
20
10
```

---

## 4. Comparison Operators

Comparison operators compare two values and return a Boolean result: `True` or `False`.

| Operator | Meaning | Example |
|---|---|---|
| `==` | Equal to | `10 == 10` |
| `!=` | Not equal to | `10 != 5` |
| `>` | Greater than | `10 > 5` |
| `<` | Less than | `5 < 10` |
| `>=` | Greater than or equal to | `10 >= 10` |
| `<=` | Less than or equal to | `5 <= 10` |

### Examples

```python
a = 10
b = 5

print(a == b)
print(a != b)
print(a > b)
print(a < b)
print(a >= 10)
print(b <= 10)
```

Output:

```text
False
True
True
False
True
True
```

### Important Difference: = vs ==

`=` is an assignment operator.

```python
age = 22
```

`==` is a comparison operator.

```python
print(age == 22)
```

Output:

```text
True
```

---

## 5. Logical Operators

Logical operators combine multiple conditions and return Boolean results.

Python provides three logical operators:

- `and`
- `or`
- `not`

### 5.1 AND Operator

Returns `True` only when both conditions are true.

| Condition 1 | Condition 2 | Result |
|---|---|---|
| True | True | True |
| True | False | False |
| False | True | False |
| False | False | False |

Example:

```python
age = 22
has_id = True

print(age >= 18 and has_id)
```

Output:

```text
True
```

### 5.2 OR Operator

Returns `True` when at least one condition is true.

| Condition 1 | Condition 2 | Result |
|---|---|---|
| True | True | True |
| True | False | True |
| False | True | True |
| False | False | False |

Example:

```python
has_email = False
has_phone = True

print(has_email or has_phone)
```

Output:

```text
True
```

### 5.3 NOT Operator

Reverses a Boolean value.

Example:

```python
is_logged_in = True

print(not is_logged_in)
```

Output:

```text
False
```

### Practical Example

```python
age = int(input("Enter your age: "))
marks = float(input("Enter your marks: "))

eligible = age >= 18 and marks >= 50

print("Eligible:", eligible)
```

---

## 6. Identity Operators

Identity operators check whether two variables refer to the same object in memory.

Python provides:

- `is`
- `is not`

### 6.1 is Operator

Returns `True` if both variables refer to the same object.

```python
a = [10, 20, 30]
b = a

print(a is b)
```

Output:

```text
True
```

Both variables refer to the same list object.

### 6.2 is not Operator

Returns `True` if both variables refer to different objects.

```python
a = [10, 20, 30]
b = [10, 20, 30]

print(a is not b)
```

Output:

```text
True
```

Although the lists contain identical values, they are separate objects.

### Difference Between == and is

```python
a = [10, 20, 30]
b = [10, 20, 30]

print(a == b)
print(a is b)
```

Output:

```text
True
False
```

- `==` compares values.
- `is` compares object identity.

**Best Practice:** Use `is None` when checking whether a variable contains `None`.

```python
value = None

print(value is None)
```

Output:

```text
True
```

---

## 7. Membership Operators

Membership operators check whether a value exists inside a sequence or collection.

Python provides:

- `in`
- `not in`

### 7.1 in Operator

Returns `True` if an element exists.

```python
fruits = ["apple", "banana", "mango"]

print("apple" in fruits)
print("orange" in fruits)
```

Output:

```text
True
False
```

### 7.2 not in Operator

Returns `True` if an element does not exist.

```python
fruits = ["apple", "banana", "mango"]

print("orange" not in fruits)
```

Output:

```text
True
```

### Membership in Strings

```python
message = "Welcome to Python"

print("Python" in message)
print("Java" in message)
```

Output:

```text
True
False
```

### Membership in Dictionaries

```python
student = {
    "name": "Raj",
    "age": 22
}

print("name" in student)
print("Raj" in student)
```

Output:

```text
True
False
```

**Important:** Membership checks in dictionaries examine keys by default, not values.

---

## 8. Bitwise Operators

Bitwise operators perform operations on the binary representation of integers.

A binary number uses only two digits:

- `0`
- `1`

Example:

```text
Decimal 5 = Binary 0101
Decimal 3 = Binary 0011
```

Python provides these bitwise operators:

| Operator | Name |
|---|---|
| `&` | Bitwise AND |
| `|` | Bitwise OR |
| `^` | Bitwise XOR |
| `~` | Bitwise NOT |
| `<<` | Left Shift |
| `>>` | Right Shift |

### 8.1 Bitwise AND (&)

A bit becomes `1` only if both corresponding bits are `1`.

```python
a = 5
b = 3

print(a & b)
```

Binary calculation:

```text
  0101
& 0011
------
  0001
```

Output:

```text
1
```

### 8.2 Bitwise OR (|)

A bit becomes `1` if at least one corresponding bit is `1`.

```python
a = 5
b = 3

print(a | b)
```

Output:

```text
7
```

### 8.3 Bitwise XOR (^)

A bit becomes `1` if the corresponding bits are different.

```python
a = 5
b = 3

print(a ^ b)
```

Output:

```text
6
```

### 8.4 Bitwise NOT (~)

Inverts the bits of an integer.

```python
a = 5

print(~a)
```

Output:

```text
-6
```

For Python integers, `~x` is equivalent to `-(x + 1)`.

### 8.5 Left Shift (<<)

Shifts binary bits to the left.

```python
a = 5

print(a << 1)
```

Output:

```text
10
```

### 8.6 Right Shift (>>)

Shifts binary bits to the right.

```python
a = 8

print(a >> 1)
```

Output:

```text
4
```

**Trainer Note:** Bitwise operators are an introductory topic here. More advanced binary operations can be taught later when required.

---

## 9. Operator Precedence

Operator precedence determines which operation Python performs first when an expression contains multiple operators.

Example:

```python
result = 10 + 5 * 2

print(result)
```

Output:

```text
20
```

Multiplication happens before addition.

### Basic Precedence Order

| Priority | Operators |
|---|---|
| 1 | `()` Parentheses |
| 2 | `**` Exponentiation |
| 3 | `+x`, `-x`, `~x` Unary operators |
| 4 | `*`, `/`, `//`, `%` |
| 5 | `+`, `-` |
| 6 | `<<`, `>>` |
| 7 | `&` |
| 8 | `^` |
| 9 | `|` |
| 10 | Comparisons, `in`, `is` |
| 11 | `not` |
| 12 | `and` |
| 13 | `or` |

Example with parentheses:

```python
result = (10 + 5) * 2

print(result)
```

Output:

```text
30
```

**Best Practice:** Use parentheses when an expression is complex. This makes the intended calculation easier to understand.

---

## 10. Practical Programs

### Program 1: Arithmetic Calculator

```python
num1 = float(input("Enter first number: "))
num2 = float(input("Enter second number: "))

print("Addition:", num1 + num2)
print("Subtraction:", num1 - num2)
print("Multiplication:", num1 * num2)
print("Division:", num1 / num2)
print("Floor Division:", num1 // num2)
print("Modulus:", num1 % num2)
print("Power:", num1 ** num2)
```

Note: This introductory version assumes the second number is not zero.

### Program 2: Even or Odd Checker

```python
number = int(input("Enter a number: "))

if number % 2 == 0:
    print("Even Number")
else:
    print("Odd Number")
```

This program introduces `if` and `else`, which will be studied in detail in a later lesson.

### Program 3: Age Eligibility Checker

```python
age = int(input("Enter your age: "))

if age >= 18:
    print("Eligible")
else:
    print("Not Eligible")
```

### Program 4: Login Condition Checker

```python
username = input("Enter username: ")
password = input("Enter password: ")

if username == "admin" and password == "12345":
    print("Login Successful")
else:
    print("Invalid Credentials")
```

Note: This is only a basic operator demonstration. Real applications must not store passwords directly in source code.

### Program 5: Discount Calculator

```python
price = float(input("Enter product price: "))
discount = float(input("Enter discount percentage: "))

discount_amount = price * discount / 100
final_price = price - discount_amount

print("Original Price:", price)
print("Discount Amount:", discount_amount)
print("Final Price:", final_price)
```

---

## 11. Student Practice Tasks

Complete these programs independently.

### Task 1 – Basic Arithmetic

Accept two numbers and display their addition, subtraction, multiplication and division.

### Task 2 – Even or Odd

Accept an integer and check whether it is even or odd using the modulus operator.

### Task 3 – Greater Number

Accept two numbers and display whether the first number is greater than, smaller than or equal to the second number.

### Task 4 – Voting Eligibility

Accept a person's age and check whether the person is eligible to vote.

### Task 5 – Login Validation

Accept a username and password. Check both conditions using `and`.

### Task 6 – Number Range

Accept a number and check whether it is between 10 and 100, inclusive.

### Task 7 – Membership Check

Create a list of five programming languages. Ask the user for a language and check whether it exists in the list.

### Task 8 – Assignment Operators

Create a variable and update it using `+=`, `-=`, `*=`, `/=` and `**=`.

### Task 9 – Identity Operators

Create two separate lists containing identical values. Compare them using `==` and `is`.

### Task 10 – Bitwise Operations

Take two integers and display the results of `&`, `|`, `^`, `<<` and `>>`.

---

## 12. Student Mini Project – Advanced Basic Calculator

### Project Description

Create a calculator that accepts two numbers and performs different mathematical operations.

### Requirements

The program should:

1. Accept two numbers.
2. Display the results of addition.
3. Display the results of subtraction.
4. Display the results of multiplication.
5. Display the results of division.
6. Display the modulus.
7. Display the power.
8. Compare both numbers.
9. Check whether the first number is greater than or equal to the second.

### Sample Solution

```python
num1 = float(input("Enter first number: "))
num2 = float(input("Enter second number: "))

print("\n----- CALCULATOR -----")

print("Addition:", num1 + num2)
print("Subtraction:", num1 - num2)
print("Multiplication:", num1 * num2)

if num2 != 0:
    print("Division:", num1 / num2)
    print("Floor Division:", num1 // num2)
    print("Modulus:", num1 % num2)
else:
    print("Division, floor division and modulus are undefined for zero.")

print("Power:", num1 ** num2)

print("\n----- COMPARISON -----")

print("Equal:", num1 == num2)
print("Not Equal:", num1 != num2)
print("First Greater:", num1 > num2)
print("First Smaller:", num1 < num2)
print("First Greater or Equal:", num1 >= num2)
```

---

## 13. Trainer Assessment

Ask the student these questions:

1. What is an operator?
2. What are operands?
3. What is the difference between `/` and `//`?
4. What does the modulus operator return?
5. What is the purpose of `**`?
6. What is the difference between `=` and `==`?
7. What is the difference between `and` and `or`?
8. What does the `not` operator do?
9. What is the difference between `==` and `is`?
10. What is the purpose of `in` and `not in`?
11. What are bitwise operators?
12. What is operator precedence?

### Practical Evaluation

Ask the student to independently create:

- An arithmetic calculator.
- An even/odd checker.
- A voting eligibility checker.
- A login condition checker.
- A discount calculator.

### Completion Criteria

- Student understands all major Python operator categories.
- Student can perform arithmetic calculations.
- Student can compare values.
- Student can combine conditions using logical operators.
- Student understands identity and membership operators.
- Student understands basic bitwise operations.
- Student can solve basic problems using operators.

---

## 14. Day 06 Completion Checklist

- [ ] Arithmetic operators
- [ ] Assignment operators
- [ ] Comparison operators
- [ ] Logical operators
- [ ] Identity operators
- [ ] Membership operators
- [ ] Bitwise operators
- [ ] Operator precedence
- [ ] Practical programs
- [ ] Advanced Basic Calculator
- [ ] Trainer assessment

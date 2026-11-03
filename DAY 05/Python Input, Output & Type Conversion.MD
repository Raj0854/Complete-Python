
# Day 05 – Python Input, Output & Type Conversion

## 1. Introduction

In the previous lesson, we learned about variables and data types.

Until now, we have provided values directly inside our Python programs.

Example:

```python
name = "Raj"
age = 22

print(name)
print(age)
```

But real-world programs need to accept information from users.

For example:
- A calculator asks users for numbers.
- A registration form asks for name and age.
- A billing system asks for product price and quantity.
- A marks calculator asks for subject marks.

Python provides the `input()` function to receive information from users.

---

## 2. Understanding the input() Function

The `input()` function allows a program to accept information from the keyboard.

### Syntax

```python
variable = input("Enter something: ")
```

### Example

```python
name = input("Enter your name: ")

print("Hello", name)
```

### Expected Output

```text
Enter your name: Raj
Hello Raj
```

### How It Works

1. Python displays the message inside `input()`.
2. The program waits for the user to enter something.
3. The user enters a value and presses Enter.
4. Python stores the entered value in the variable.

### Important Rule

**The `input()` function always returns data as a string (`str`).**

Example:

```python
age = input("Enter your age: ")

print(age)
print(type(age))
```

Expected Output:

```text
Enter your age: 22
22
<class 'str'>
```

Even though the user entered `22`, Python stored it as a string.

---

## 3. Taking Different Inputs

### Example 1: Name

```python
name = input("Enter your name: ")

print("Name:", name)
```

### Example 2: City

```python
city = input("Enter your city: ")

print("City:", city)
```

### Example 3: Multiple Inputs

```python
name = input("Enter your name: ")
city = input("Enter your city: ")
course = input("Enter your course: ")

print("Name:", name)
print("City:", city)
print("Course:", course)
```

### Practice

Create a program that asks the user for:

1. Full name
2. Email address
3. Phone number
4. City

Display all the information at the end.

---

## 4. Why Do We Need Type Conversion?

Consider this program:

```python
num1 = input("Enter first number: ")
num2 = input("Enter second number: ")

result = num1 + num2

print("Result:", result)
```

Expected Output:

```text
Enter first number: 10
Enter second number: 20
Result: 1020
```

Why did Python display `1020` instead of `30`?

Because both inputs are strings.

The `+` operator joins strings instead of performing numerical addition.

To solve this problem, we need **Type Conversion**.

Type conversion means changing a value from one data type to another.

---

## 5. Explicit Type Conversion

Explicit type conversion means manually converting a value into another data type.

Python provides several built-in conversion functions.

| Function | Converts Into | Example |
|---|---|---|
| `int()` | Integer | `int("25")` |
| `float()` | Float | `float("25.5")` |
| `str()` | String | `str(100)` |
| `complex()` | Complex | `complex(5)` |
| `bool()` | Boolean | `bool(1)` |

### 5.1 int()

Converts a compatible value into an integer.

```python
age = "22"

age = int(age)

print(age)
print(type(age))
```

Output:

```text
22
<class 'int'>
```

Another example:

```python
price = int(99.99)

print(price)
```

Output:

```text
99
```

**Important:** `int()` removes the decimal part. It does not round the number.

### 5.2 float()

Converts a compatible value into a floating-point number.

```python
price = "99.50"

price = float(price)

print(price)
print(type(price))
```

Output:

```text
99.5
<class 'float'>
```

### 5.3 str()

Converts a value into a string.

```python
age = 22

age = str(age)

print(age)
print(type(age))
```

Output:

```text
22
<class 'str'>
```

### 5.4 complex()

Converts a compatible number into a complex number.

```python
number = complex(5)

print(number)
print(type(number))
```

Output:

```text
(5+0j)
<class 'complex'>
```

### 5.5 bool()

Converts a value into a Boolean value.

```python
print(bool(1))
print(bool(0))
print(bool(""))
print(bool("Python"))
```

Output:

```text
True
False
False
True
```

**Important:** Any non-empty string evaluates to `True`, including `"False"`.

```python
print(bool("False"))
```

Output:

```text
True
```

This is because `"False"` is a non-empty string, not the Boolean value `False`.

---

## 6. Taking Numeric Input

Now let's combine `input()` with type conversion.

### Example 1: Integer Input

```python
age = int(input("Enter your age: "))

print("Your age is:", age)
print(type(age))
```

### Expected Output

```text
Enter your age: 22
Your age is: 22
<class 'int'>
```

### Example 2: Float Input

```python
price = float(input("Enter product price: "))

print("Product price:", price)
print(type(price))
```

### Expected Output

```text
Enter product price: 199.50
Product price: 199.5
<class 'float'>
```

### Example 3: Two Numbers Addition

```python
num1 = int(input("Enter first number: "))
num2 = int(input("Enter second number: "))

result = num1 + num2

print("Addition:", result)
```

### Expected Output

```text
Enter first number: 10
Enter second number: 20
Addition: 30
```

---

## 7. Implicit Type Conversion

Implicit type conversion happens automatically when Python converts a value from one compatible data type to another.

Example:

```python
num1 = 10
num2 = 5.5

result = num1 + num2

print(result)
print(type(result))
```

Output:

```text
15.5
<class 'float'>
```

Here:
- `num1` is an integer.
- `num2` is a float.
- Python automatically promotes the integer to a float for the calculation.
- The final result is a float.

### Explicit vs Implicit Conversion

| Explicit Conversion | Implicit Conversion |
|---|---|
| Performed manually | Performed automatically |
| Uses conversion functions | Python handles conversion |
| Example: `int("10")` | Example: `10 + 5.5` |

---

## 8. Common Type Conversion Errors

Not every value can be converted into every data type.

Example:

```python
age = int("Hello")

print(age)
```

Output:

```text
ValueError
```

Why?

Because `"Hello"` is not a valid integer.

Another example:

```python
price = float("Python")

print(price)
```

This also produces a `ValueError`.

### Important Note

If a user enters unexpected or invalid input, a program can crash during conversion.

For now, understand why this happens. We will learn proper error handling in a later lesson.

---

## 9. Practical Programs

### Program 1: Simple Calculator – Addition

```python
num1 = float(input("Enter first number: "))
num2 = float(input("Enter second number: "))

addition = num1 + num2

print("Addition:", addition)
```

### Program 2: Calculate Rectangle Area

Formula:

Area = Length × Width

```python
length = float(input("Enter length: "))
width = float(input("Enter width: "))

area = length * width

print("Rectangle Area:", area)
```

### Program 3: Calculate Average Marks

```python
maths = float(input("Enter Maths marks: "))
science = float(input("Enter Science marks: "))
english = float(input("Enter English marks: "))

total = maths + science + english
average = total / 3

print("Total Marks:", total)
print("Average Marks:", average)
```

### Program 4: Age Calculator

```python
age = int(input("Enter your current age: "))

next_year_age = age + 1

print("Your age next year will be:", next_year_age)
```

### Program 5: Shopping Bill Calculator

```python
product = input("Enter product name: ")
price = float(input("Enter product price: "))
quantity = int(input("Enter quantity: "))

total = price * quantity

print("Product:", product)
print("Price:", price)
print("Quantity:", quantity)
print("Total Bill:", total)
```

---

## 10. Student Mini Project – Student Marks Calculator

### Project Description

Create a Python program that accepts student information and calculates total and average marks.

### Requirements

The program should:

1. Ask for the student's name.
2. Ask for the student's roll number.
3. Ask for marks in five subjects.
4. Calculate total marks.
5. Calculate average marks.
6. Display all student information.
7. Display total and average marks.

### Sample Solution

```python
student_name = input("Enter student name: ")
roll_number = input("Enter roll number: ")

subject1 = float(input("Enter English marks: "))
subject2 = float(input("Enter Maths marks: "))
subject3 = float(input("Enter Science marks: "))
subject4 = float(input("Enter Computer marks: "))
subject5 = float(input("Enter Hindi marks: "))

total = subject1 + subject2 + subject3 + subject4 + subject5

average = total / 5

print("\n----- STUDENT RESULT -----")

print("Student Name:", student_name)
print("Roll Number:", roll_number)
print("English:", subject1)
print("Maths:", subject2)
print("Science:", subject3)
print("Computer:", subject4)
print("Hindi:", subject5)

print("Total Marks:", total)
print("Average Marks:", average)
```

### Sample Output

```text
----- STUDENT RESULT -----

Student Name: Rahul
Roll Number: 101
English: 80.0
Maths: 90.0
Science: 85.0
Computer: 95.0
Hindi: 75.0

Total Marks: 425.0
Average Marks: 85.0
```

---

## 11. Student Practice Tasks

Complete these programs independently.

### Task 1 – Personal Information

Ask the user for their name, age, city and profession. Display the information.

### Task 2 – Addition Calculator

Accept two integer numbers and display their sum.

### Task 3 – Multiplication Calculator

Accept two numbers and display their multiplication.

### Task 4 – Temperature Conversion

Convert Celsius into Fahrenheit.

Formula:

Fahrenheit = (Celsius × 9/5) + 32

### Task 5 – Simple Interest Calculator

Formula:

Simple Interest = (Principal × Rate × Time) / 100

Accept principal, rate and time from the user.

### Task 6 – Shopping Calculator

Accept product name, price and quantity. Calculate and display the total bill.

### Task 7 – Age in Months

Accept the user's age in years and calculate the approximate age in months.

Formula:

Age in Months = Age × 12

---

## 12. Trainer Assessment

Ask the student these questions:

1. What is the purpose of `input()`?
2. What data type does `input()` return?
3. Why do we need type conversion?
4. What is the difference between `int()` and `float()`?
5. What is explicit type conversion?
6. What is implicit type conversion?
7. What happens when we execute `int("Hello")`?
8. Why does `"10" + "20"` produce `"1020"`?
9. What is the output of `int(12.9)`?
10. What is the output of `bool("False")`?

### Practical Evaluation

Ask the student to independently create:

- A two-number calculator.
- A rectangle area calculator.
- A shopping bill calculator.
- A student marks calculator.

### Completion Criteria

- Student can take input using `input()`.
- Student understands that input is returned as a string.
- Student can convert values using `int()`, `float()` and `str()`.
- Student understands implicit and explicit conversion.
- Student can build basic interactive programs independently.

---

## 13. Day 05 Completion Checklist

- [ ] Understand `input()`.
- [ ] Understand why input returns a string.
- [ ] Learn explicit type conversion.
- [ ] Learn implicit type conversion.
- [ ] Practice `int()`, `float()`, `str()`, `complex()` and `bool()`.
- [ ] Understand common conversion errors.
- [ ] Complete practical programs.
- [ ] Complete the Student Marks Calculator.
- [ ] Complete the trainer assessment.


# Day 07 – Python Conditional Statements

## 1. Introduction to Conditional Statements

Conditional statements allow a program to make decisions based on specific conditions.

For example:
- Check whether a person is eligible to vote.
- Check whether a number is even or odd.
- Check whether a student has passed or failed.
- Check whether a user entered the correct password.
- Calculate discounts based on purchase amounts.

In Python, conditional statements are written using:

- `if`
- `elif`
- `else`

### Example Without Conditions

```python
age = 15

print("You are eligible to vote.")
```

This program always displays the same message, even if the age is below 18.

We need conditions to control program behaviour.

---

## 2. The if Statement

The `if` statement executes a block of code only when a condition is `True`.

### Syntax

```python
if condition:
    statement
```

### Example

```python
age = 20

if age >= 18:
    print("You are eligible to vote.")
```

Output:

```text
You are eligible to vote.
```

### Explanation

1. Python checks whether `age >= 18`.
2. The condition is `True`.
3. Python executes the indented statement.

### Example: Number Check

```python
number = 10

if number > 0:
    print("Positive Number")
```

Output:

```text
Positive Number
```

### Example: Marks Check

```python
marks = 75

if marks >= 40:
    print("You have passed.")
```

Output:

```text
You have passed.
```

---

## 3. The if-else Statement

The `if-else` statement provides two possible execution paths.

- If the condition is `True`, the `if` block executes.
- If the condition is `False`, the `else` block executes.

### Syntax

```python
if condition:
    statement_if_true
else:
    statement_if_false
```

### Example: Voting Eligibility

```python
age = int(input("Enter your age: "))

if age >= 18:
    print("You are eligible to vote.")
else:
    print("You are not eligible to vote.")
```

### Example: Even or Odd

```python
number = int(input("Enter a number: "))

if number % 2 == 0:
    print("Even Number")
else:
    print("Odd Number")
```

### Example: Positive or Negative

```python
number = int(input("Enter a number: "))

if number >= 0:
    print("Positive Number or Zero")
else:
    print("Negative Number")
```

---

## 4. The if-elif-else Statement

Sometimes a program needs to check multiple conditions.

Python provides `elif`, which means "else if".

### Syntax

```python
if condition1:
    statement1
elif condition2:
    statement2
elif condition3:
    statement3
else:
    default_statement
```

Python checks conditions from top to bottom.

The first condition that evaluates to `True` executes its block. The remaining conditions are skipped.

### Example: Grade Calculator

```python
marks = int(input("Enter your marks: "))

if marks >= 90:
    print("Grade A")
elif marks >= 75:
    print("Grade B")
elif marks >= 60:
    print("Grade C")
elif marks >= 40:
    print("Grade D")
else:
    print("Fail")
```

### Sample Output

```text
Enter your marks: 82
Grade B
```

### Example: Number Classification

```python
number = int(input("Enter a number: "))

if number > 0:
    print("Positive Number")
elif number < 0:
    print("Negative Number")
else:
    print("Zero")
```

### Important Rule

Condition order matters.

For example, this is incorrect for a grading system:

```python
marks = 85

if marks >= 40:
    print("Grade D")
elif marks >= 75:
    print("Grade B")
```

Output:

```text
Grade D
```

Why?

Because `85 >= 40` is already `True`. Python never checks the second condition.

Always arrange overlapping conditions carefully, generally from the highest threshold to the lowest.

---

## 5. Nested if Statements

A nested `if` statement means placing one `if` statement inside another `if` statement.

Nested conditions are useful when a second decision depends on the first decision.

### Syntax

```python
if condition1:
    if condition2:
        statement1
    else:
        statement2
else:
    statement3
```

### Example: Login Verification

```python
username = input("Enter username: ")

if username == "admin":
    password = input("Enter password: ")

    if password == "12345":
        print("Login Successful")
    else:
        print("Incorrect Password")
else:
    print("Username Not Found")
```

### Explanation

1. First, Python checks the username.
2. If the username is correct, it asks for the password.
3. If the password is correct, login succeeds.
4. Otherwise, it displays an appropriate message.

### Example: Student Admission

```python
age = int(input("Enter your age: "))
marks = float(input("Enter your marks: "))

if age >= 18:
    if marks >= 60:
        print("Admission Approved")
    else:
        print("Marks Requirement Not Met")
else:
    print("Age Requirement Not Met")
```

---

## 6. Multiple Conditions Using Logical Operators

We can combine conditions using:

- `and`
- `or`
- `not`

### Example 1: AND

Both conditions must be true.

```python
age = int(input("Enter your age: "))
marks = float(input("Enter your marks: "))

if age >= 18 and marks >= 50:
    print("Eligible")
else:
    print("Not Eligible")
```

### Example 2: OR

At least one condition must be true.

```python
day = input("Enter day: ")

if day == "Saturday" or day == "Sunday":
    print("Weekend")
else:
    print("Working Day")
```

### Example 3: NOT

Reverses a Boolean condition.

```python
is_raining = False

if not is_raining:
    print("You can go outside.")
else:
    print("Stay indoors.")
```

---

## 7. Short-Hand Conditional Expression

Python also supports a one-line conditional expression, sometimes called the ternary conditional expression.

### Syntax

```python
value_if_true if condition else value_if_false
```

### Example

```python
age = 20

result = "Eligible" if age >= 18 else "Not Eligible"

print(result)
```

Output:

```text
Eligible
```

### Example: Even or Odd

```python
number = 7

result = "Even" if number % 2 == 0 else "Odd"

print(result)
```

Output:

```text
Odd
```

**Trainer Note:** Teach this after the normal `if-else` structure. Students should first understand standard conditional blocks.

---

## 8. The pass Statement

The `pass` statement is used when Python requires a statement syntactically, but no action needs to be performed yet.

Example:

```python
age = 20

if age >= 18:
    pass

print("Program Completed")
```

Output:

```text
Program Completed
```

`pass` is useful while creating the initial structure of a program and planning its logic.

---

## 9. Truthy and Falsy Values

Python conditions do not always need to contain comparison operators.

Python evaluates values as either truthy or falsy.

### Common Falsy Values

- `False`
- `None`
- `0`
- `0.0`
- `""`
- `[]`
- `()`
- `{}`
- `set()`

Most other values are truthy.

### Example

```python
name = input("Enter your name: ")

if name:
    print("Welcome", name)
else:
    print("Name cannot be empty.")
```

If the user presses Enter without entering anything, the string is empty and the `else` block executes.

### Another Example

```python
items = []

if items:
    print("Items are available.")
else:
    print("The list is empty.")
```

Output:

```text
The list is empty.
```

---

## 10. Indentation in Conditional Statements

Python uses indentation to define code blocks.

Correct example:

```python
age = 20

if age >= 18:
    print("Eligible")
    print("You can proceed.")
```

Incorrect example:

```python
age = 20

if age >= 18:
print("Eligible")
```

The incorrect example generates an `IndentationError`.

### Important Rules

1. Use consistent indentation.
2. Python convention is four spaces.
3. Statements inside a condition must be indented.
4. The `if`, `elif` and `else` statements belonging to the same structure should align.

---

## 11. Practical Programs

### Program 1: Largest of Two Numbers

```python
num1 = float(input("Enter first number: "))
num2 = float(input("Enter second number: "))

if num1 > num2:
    print("First number is greater.")
elif num2 > num1:
    print("Second number is greater.")
else:
    print("Both numbers are equal.")
```

### Program 2: Largest of Three Numbers

```python
a = float(input("Enter first number: "))
b = float(input("Enter second number: "))
c = float(input("Enter third number: "))

if a >= b and a >= c:
    print("First number is largest.")
elif b >= a and b >= c:
    print("Second number is largest.")
else:
    print("Third number is largest.")
```

### Program 3: Leap Year Checker

A year is a leap year when:

- It is divisible by 400, OR
- It is divisible by 4 but not divisible by 100.

```python
year = int(input("Enter a year: "))

if year % 400 == 0:
    print("Leap Year")
elif year % 100 == 0:
    print("Not a Leap Year")
elif year % 4 == 0:
    print("Leap Year")
else:
    print("Not a Leap Year")
```

### Program 4: Electricity Bill Calculator

Use these sample rates:

- First 100 units: ₹5 per unit
- Next 100 units: ₹7 per unit
- Above 200 units: ₹10 per unit

```python
units = int(input("Enter electricity units: "))

if units < 0:
    print("Invalid units.")

elif units <= 100:
    bill = units * 5
    print("Electricity Bill: ₹", bill)

elif units <= 200:
    bill = (100 * 5) + ((units - 100) * 7)
    print("Electricity Bill: ₹", bill)

else:
    bill = (100 * 5) + (100 * 7) + ((units - 200) * 10)
    print("Electricity Bill: ₹", bill)
```

### Program 5: Discount Calculator

Discount rules:

- Purchase below ₹1,000: No discount
- Purchase ₹1,000–₹4,999: 5% discount
- Purchase ₹5,000–₹9,999: 10% discount
- Purchase ₹10,000 or more: 15% discount

```python
amount = float(input("Enter purchase amount: "))

if amount < 0:
    print("Invalid amount.")

elif amount < 1000:
    discount = 0

elif amount < 5000:
    discount = 5

elif amount < 10000:
    discount = 10

else:
    discount = 15

if amount >= 0:
    discount_amount = amount * discount / 100
    final_amount = amount - discount_amount

    print("Original Amount:", amount)
    print("Discount:", discount, "%")
    print("Discount Amount:", discount_amount)
    print("Final Amount:", final_amount)
```

### Program 6: Simple Menu-Based Calculator

```python
print("----- CALCULATOR -----")

print("1. Addition")
print("2. Subtraction")
print("3. Multiplication")
print("4. Division")

choice = int(input("Enter your choice: "))

num1 = float(input("Enter first number: "))
num2 = float(input("Enter second number: "))

if choice == 1:
    print("Result:", num1 + num2)

elif choice == 2:
    print("Result:", num1 - num2)

elif choice == 3:
    print("Result:", num1 * num2)

elif choice == 4:
    if num2 != 0:
        print("Result:", num1 / num2)
    else:
        print("Cannot divide by zero.")

else:
    print("Invalid choice.")
```

---

## 12. Student Practice Tasks

Complete these programs independently.

### Task 1 – Positive, Negative or Zero

Accept a number and identify whether it is positive, negative or zero.

### Task 2 – Even or Odd

Accept an integer and identify whether it is even or odd.

### Task 3 – Voting Eligibility

Accept age and check whether the person is eligible to vote.

### Task 4 – Grade Calculator

Accept marks and assign grades using these rules:

- 90–100: A
- 75–89: B
- 60–74: C
- 40–59: D
- Below 40: Fail
- Outside 0–100: Invalid Marks

### Task 5 – Largest of Three Numbers

Accept three numbers and find the largest.

### Task 6 – Leap Year

Accept a year and check whether it is a leap year.

### Task 7 – Login System

Ask for username and password. Display appropriate messages based on the entered values.

### Task 8 – Ticket Pricing

Create a ticket pricing program:

- Age below 5: Free
- Age 5–17: ₹100
- Age 18–59: ₹200
- Age 60 or above: ₹120

### Task 9 – Discount System

Create a discount calculator using multiple purchase amount conditions.

### Task 10 – Simple Calculator

Create a menu-based calculator using conditional statements.

---

## 13. Student Mini Project – Smart Student Result System

### Project Description

Create a student result program that checks marks and generates a result.

### Requirements

The program should:

1. Ask for the student's name.
2. Ask for the student's roll number.
3. Accept marks in five subjects.
4. Check whether all marks are between 0 and 100.
5. Calculate total marks.
6. Calculate average marks.
7. Determine whether the student passed or failed.
8. Assign a grade.
9. Display the complete result.

### Passing Rules

- Minimum 35 marks in every subject.
- Overall average must be at least 40.
- Invalid marks should not generate a result.

### Sample Solution

```python
name = input("Enter student name: ")
roll_number = input("Enter roll number: ")

english = float(input("Enter English marks: "))
maths = float(input("Enter Maths marks: "))
science = float(input("Enter Science marks: "))
computer = float(input("Enter Computer marks: "))
hindi = float(input("Enter Hindi marks: "))

if not all(0 <= mark <= 100 for mark in [
    english, maths, science, computer, hindi
]):
    print("Invalid Marks Entered.")

else:
    total = english + maths + science + computer + hindi
    average = total / 5

    if (
        english >= 35
        and maths >= 35
        and science >= 35
        and computer >= 35
        and hindi >= 35
        and average >= 40
    ):
        result = "PASS"

        if average >= 90:
            grade = "A"
        elif average >= 75:
            grade = "B"
        elif average >= 60:
            grade = "C"
        elif average >= 40:
            grade = "D"
        else:
            grade = "F"

    else:
        result = "FAIL"
        grade = "F"

    print("\n----- STUDENT RESULT -----")
    print("Name:", name)
    print("Roll Number:", roll_number)
    print("Total Marks:", total)
    print("Average:", average)
    print("Result:", result)
    print("Grade:", grade)
```

---

## 14. Trainer Assessment

Ask the student these questions:

1. What are conditional statements?
2. What is the purpose of `if`?
3. What is the difference between `if` and `if-else`?
4. What is the purpose of `elif`?
5. How does Python execute an `if-elif-else` structure?
6. What is a nested `if` statement?
7. How can logical operators be used inside conditions?
8. What is a ternary conditional expression?
9. What is the purpose of `pass`?
10. What are truthy and falsy values?
11. Why is indentation important?
12. How can we check whether a year is a leap year?

### Practical Evaluation

Ask the student to independently create:

- An even/odd checker.
- A grade calculator.
- A leap year checker.
- A discount calculator.
- A menu-based calculator.
- A student result system.

### Completion Criteria

- Student understands `if`, `elif` and `else`.
- Student can create nested conditions.
- Student can combine conditions using logical operators.
- Student understands truthy and falsy values.
- Student can write decision-making programs independently.
- Student can solve basic real-world problems using conditions.

---

## 15. Day 07 Completion Checklist

- [ ] Understand conditional statements.
- [ ] Learn the `if` statement.
- [ ] Learn the `if-else` statement.
- [ ] Learn the `if-elif-else` structure.
- [ ] Learn nested `if` statements.
- [ ] Use logical operators in conditions.
- [ ] Learn conditional expressions.
- [ ] Understand the `pass` statement.
- [ ] Understand truthy and falsy values.
- [ ] Practice indentation.
- [ ] Complete practical programs.
- [ ] Complete the Student Result System.
- [ ] Complete trainer assessment.

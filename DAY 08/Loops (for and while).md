
# Day 08 – Python Loops (for and while)

## 1. Introduction to Loops

A loop is a programming structure that allows us to execute a block of code repeatedly.

Without loops, we would need to write the same code multiple times.

### Example: Without a Loop

```python
print("Hello")
print("Hello")
print("Hello")
print("Hello")
print("Hello")
```

### Example: With a Loop

```python
for i in range(5):
    print("Hello")
```

Both programs produce the same output, but the loop makes the code shorter and easier to maintain.

---

## 2. Types of Loops in Python

Python provides two main types of loops:

1. `for` loop
2. `while` loop

### for Loop

A `for` loop is used to iterate over a sequence or collection of items.

### Syntax

```python
for variable in sequence:
    # Code to execute
```

### Example

```python
for number in range(5):
    print(number)
```

### Output

```text
0
1
2
3
4
```

The loop executes five times, starting from 0 and ending at 4.

---

## 3. Understanding range()

The `range()` function generates a sequence of numbers.

It is commonly used with `for` loops.

### A. range(stop)

```python
for i in range(5):
    print(i)
```

Output:

```text
0
1
2
3
4
```

The sequence starts from 0 and stops before 5.

### B. range(start, stop)

```python
for i in range(1, 6):
    print(i)
```

Output:

```text
1
2
3
4
5
```

### C. range(start, stop, step)

```python
for i in range(2, 11, 2):
    print(i)
```

Output:

```text
2
4
6
8
10
```

The third argument specifies the step or increment.

### D. Reverse Counting

```python
for i in range(10, 0, -1):
    print(i)
```

Output:

```text
10
9
8
7
6
5
4
3
2
1
```

A negative step allows the sequence to move backwards.

---

## 4. Practical Demonstration of for Loop

### Program 1: Print Numbers from 1 to 10

```python
for i in range(1, 11):
    print(i)
```

### Program 2: Print Even Numbers

```python
for i in range(2, 21, 2):
    print(i)
```

### Program 3: Print Odd Numbers

```python
for i in range(1, 20, 2):
    print(i)
```

### Program 4: Multiplication Table

```python
number = int(input("Enter a number: "))

for i in range(1, 11):
    print(number, "x", i, "=", number * i)
```

Example output for input 5:

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

## 5. Understanding while Loop

A `while` loop executes a block of code as long as its condition remains True.

### Syntax

```python
while condition:
    # Code to execute
```

### Example

```python
number = 1

while number <= 5:
    print(number)
    number += 1
```

### Output

```text
1
2
3
4
5
```

### How It Works

1. Initially, `number = 1`.
2. Python checks whether `number <= 5`.
3. If the condition is True, the loop executes.
4. `number += 1` increases the value by one.
5. Python checks the condition again.
6. When the condition becomes False, the loop stops.

---

## 6. Practical Demonstration of while Loop

### Program 1: Print Numbers from 1 to 10

```python
number = 1

while number <= 10:
    print(number)
    number += 1
```

### Program 2: Reverse Counting

```python
number = 10

while number >= 1:
    print(number)
    number -= 1
```

### Program 3: Multiplication Table

```python
number = int(input("Enter a number: "))

i = 1

while i <= 10:
    print(number, "x", i, "=", number * i)
    i += 1
```

### Program 4: Sum of First N Natural Numbers

```python
n = int(input("Enter a number: "))

total = 0
i = 1

while i <= n:
    total += i
    i += 1

print("Sum:", total)
```

Example:

```text
Enter a number: 5
Sum: 15
```

Calculation: 1 + 2 + 3 + 4 + 5 = 15.

---

## 7. Difference Between for and while Loop

| for Loop | while Loop |
|---|---|
| Used to iterate over a sequence or range | Used to repeat code while a condition is True |
| Commonly used when iterations are known | Commonly used when iterations depend on a condition |
| Usually manages iteration automatically | Requires manual condition updates |
| Often used with `range()` | Often used with comparison conditions |

### Example: for Loop

```python
for i in range(5):
    print(i)
```

### Example: while Loop

```python
i = 0

while i < 5:
    print(i)
    i += 1
```

Both examples print numbers from 0 to 4.

---

## 8. Infinite Loops

An infinite loop is a loop that never stops because its condition always remains True.

### Example

```python
while True:
    print("Running...")
```

This program continues running until it is interrupted.

### Another Example

```python
number = 1

while number <= 5:
    print(number)
```

**Important:** This loop is also infinite because `number` never increases.

Always ensure that a `while` loop has a proper condition and update mechanism, unless an intentional infinite loop is required.

---

## 9. Loop with User Input

### Program: Password Verification

```python
password = "python123"

user_password = input("Enter password: ")

while user_password != password:
    print("Incorrect password. Try again.")
    user_password = input("Enter password: ")

print("Login successful!")
```

The loop continues until the correct password is entered.

**Note:** This is a basic learning example, not a secure authentication system.

---

## 10. Using else with Loops

Python allows an `else` block with both `for` and `while` loops.

The `else` block executes when the loop finishes normally.

### Example: for-else

```python
for i in range(1, 6):
    print(i)
else:
    print("Loop completed!")
```

Output:

```text
1
2
3
4
5
Loop completed!
```

### Example: while-else

```python
i = 1

while i <= 5:
    print(i)
    i += 1
else:
    print("Loop completed!")
```

Output:

```text
1
2
3
4
5
Loop completed!
```

We will study how `break` affects loop execution in the next lesson.

---

## 11. Nested Loops – Introduction

A nested loop means placing one loop inside another loop.

### Example

```python
for i in range(1, 4):
    for j in range(1, 4):
        print(i, j)
```

Output:

```text
1 1
1 2
1 3
2 1
2 2
2 3
3 1
3 2
3 3
```

The inner loop completes all its iterations for every iteration of the outer loop.

We will explore nested loops and pattern programming in more detail later.

---

## 12. Practical Programs

### Program 1: Factorial of a Number

```python
number = int(input("Enter a number: "))

factorial = 1

for i in range(1, number + 1):
    factorial *= i

print("Factorial:", factorial)
```

Example:

```text
Enter a number: 5
Factorial: 120
```

### Program 2: Count Digits in a Number

```python
number = int(input("Enter a number: "))

number = abs(number)
count = 0

if number == 0:
    count = 1
else:
    while number > 0:
        number //= 10
        count += 1

print("Total digits:", count)
```

### Program 3: Reverse a Number

```python
number = int(input("Enter a number: "))

original = abs(number)
reverse = 0

while original > 0:
    digit = original % 10
    reverse = reverse * 10 + digit
    original //= 10

if number < 0:
    reverse = -reverse

print("Reversed number:", reverse)
```

### Program 4: Check Prime Number

```python
number = int(input("Enter a number: "))

if number <= 1:
    print("Not a prime number")
else:
    is_prime = True

    for i in range(2, number):
        if number % i == 0:
            is_prime = False
            break

    if is_prime:
        print("Prime number")
    else:
        print("Not a prime number")
```

### Program 5: Sum of Even and Odd Numbers

```python
n = int(input("Enter the limit: "))

even_sum = 0
odd_sum = 0

for i in range(1, n + 1):
    if i % 2 == 0:
        even_sum += i
    else:
        odd_sum += i

print("Even Sum:", even_sum)
print("Odd Sum:", odd_sum)
```

---

## 13. Student Practice Exercises

Ask the student to solve these programs independently.

1. Print numbers from 1 to 100 using a `for` loop.
2. Print numbers from 100 to 1 using a `while` loop.
3. Print all multiples of 5 between 1 and 100.
4. Calculate the sum of numbers from 1 to 50.
5. Generate the multiplication table of a user-provided number.
6. Calculate the factorial of a user-provided number.
7. Count the number of digits in an integer.
8. Reverse a given integer.
9. Find the sum of digits of a number.
10. Check whether a number is prime.
11. Print the first N natural numbers and their squares.
12. Calculate the average of N numbers entered by the user.

---

## 14. Mini Project – Number Analysis System

Create a menu-driven program that analyzes a number using loops.

### Requirements

1. Ask the user to enter a positive integer.
2. Display a menu:
   - Count digits.
   - Calculate sum of digits.
   - Reverse the number.
   - Check whether the number is prime.
   - Print the multiplication table.
   - Exit.
3. Execute the selected operation.
4. Display the result.
5. Allow the user to perform another operation until Exit is selected.

### Expected Menu

```text
===== NUMBER ANALYSIS SYSTEM =====

Enter a number: 12345

1. Count Digits
2. Sum of Digits
3. Reverse Number
4. Check Prime
5. Multiplication Table
6. Exit

Enter your choice:
```

### Rules

- Use a `while` loop for the menu.
- Use `for` or `while` loops for calculations.
- Use conditional statements to process menu choices.
- Validate invalid menu choices.
- Display meaningful messages.

### Challenge

Extend the project to support multiple numbers without restarting the program.

---

## 15. Common Mistakes to Avoid

1. Forgetting to update the variable in a `while` loop.
2. Using an incorrect `range()` stop value.
3. Forgetting that `range()` excludes the stop value.
4. Incorrect indentation inside loops.
5. Accidentally creating an infinite loop.
6. Updating the wrong variable.
7. Using `=` instead of `==` in a comparison.
8. Forgetting to initialize counters and totals.

---

## 16. Trainer Assessment

Ask the student:

1. What is a loop?
2. What are the two main types of loops in Python?
3. What is the difference between `for` and `while`?
4. What does `range(1, 10)` generate?
5. What is the purpose of the step argument in `range()`?
6. What is an infinite loop?
7. Why must we update a variable in many `while` loops?
8. What is a nested loop?
9. When does the `else` block of a loop execute?
10. Can a `for` loop iterate over a string?

### Practical Assessment

- Write a multiplication table using a `for` loop.
- Calculate a factorial using a `while` loop.
- Reverse an integer using a loop.
- Build the Number Analysis System mini-project.

### Completion Criteria

The student should be able to:

- Explain how loops work.
- Use `for` and `while` correctly.
- Apply `range()` with start, stop and step.
- Solve basic numerical problems using loops.
- Identify and prevent unintended infinite loops.
- Complete the Number Analysis System independently.

---

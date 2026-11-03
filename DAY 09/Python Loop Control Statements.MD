
# Day 09 – Python Loop Control Statements

## 1. Introduction to Loop Control Statements

Loop control statements are used to change the normal execution of a loop.

Python provides three important loop control statements:

1. `break`
2. `continue`
3. `pass`

These statements help us control how and when a loop executes.

---

## 2. break Statement

The `break` statement immediately terminates the loop.

When Python encounters `break`, it exits the current loop and continues executing the code after that loop.

### Syntax

```python
for variable in sequence:
    if condition:
        break
```

### Example 1: Stop a Loop

```python
for i in range(1, 11):
    if i == 5:
        break

    print(i)

print("Loop ended")
```

### Output

```text
1
2
3
4
Loop ended
```

### How It Works

1. The loop starts from 1.
2. Python checks the condition `i == 5`.
3. When `i` becomes 5, the condition becomes True.
4. The `break` statement terminates the loop.
5. Numbers after 5 are not printed.

### Example 2: Search for a Number

```python
numbers = [10, 20, 30, 40, 50]

target = int(input("Enter number to search: "))

for number in numbers:
    if number == target:
        print("Number found!")
        break
else:
    print("Number not found!")
```

The loop stops immediately when the target number is found.

**Note:** The `else` block executes only if the loop finishes without encountering `break`.

---

## 3. continue Statement

The `continue` statement skips the remaining code in the current iteration and moves to the next iteration.

Unlike `break`, it does not terminate the entire loop.

### Syntax

```python
for variable in sequence:
    if condition:
        continue

    # Remaining code
```

### Example 1: Skip a Number

```python
for i in range(1, 11):
    if i == 5:
        continue

    print(i)
```

### Output

```text
1
2
3
4
6
7
8
9
10
```

Number 5 is skipped, but the loop continues.

### Example 2: Print Only Odd Numbers

```python
for i in range(1, 11):
    if i % 2 == 0:
        continue

    print(i)
```

### Output

```text
1
3
5
7
9
```

### Example 3: Skip Negative Numbers

```python
numbers = [10, -5, 20, -8, 30, -2]

for number in numbers:
    if number < 0:
        continue

    print(number)
```

### Output

```text
10
20
30
```

Negative numbers are skipped.

---

## 4. pass Statement

The `pass` statement does nothing when executed.

It is used as a placeholder when Python requires a statement but we do not want to write the actual code yet.

### Example 1: pass in a Loop

```python
for i in range(1, 6):
    if i == 3:
        pass

    print(i)
```

### Output

```text
1
2
3
4
5
```

The `pass` statement does not skip the number or terminate the loop.

### Example 2: Empty while Loop

```python
number = 1

while number <= 5:
    pass
```

**Warning:** This example creates an infinite loop because `number` is never updated. Do not run it without adding a proper update mechanism.

### Example 3: Placeholder for Future Code

```python
for i in range(1, 6):
    if i == 3:
        pass
    else:
        print(i)
```

### Output

```text
1
2
4
5
```

Here, the `pass` statement allows the conditional block to remain empty.

---

## 5. Difference Between break, continue and pass

| Statement | Behaviour |
|---|---|
| `break` | Terminates the current loop |
| `continue` | Skips the current iteration |
| `pass` | Does nothing; acts as a placeholder |

### Example: Comparing All Three

#### break

```python
for i in range(1, 6):
    if i == 3:
        break

    print(i)
```

Output:

```text
1
2
```

#### continue

```python
for i in range(1, 6):
    if i == 3:
        continue

    print(i)
```

Output:

```text
1
2
4
5
```

#### pass

```python
for i in range(1, 6):
    if i == 3:
        pass

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

---

## 6. Loop Control Statements with while Loop

The `break` and `continue` statements also work with `while` loops.

### Example 1: break with while

```python
number = 1

while number <= 10:
    if number == 6:
        break

    print(number)
    number += 1
```

Output:

```text
1
2
3
4
5
```

### Example 2: continue with while

```python
number = 0

while number < 10:
    number += 1

    if number == 5:
        continue

    print(number)
```

Output:

```text
1
2
3
4
6
7
8
9
10
```

**Important:** In a `while` loop, make sure the variable is updated before `continue` if the update is necessary for the loop to terminate.

### Example 3: pass with while

```python
number = 1

while number <= 5:
    if number == 3:
        pass

    print(number)
    number += 1
```

Output:

```text
1
2
3
4
5
```

---

## 7. Nested Loops with break

When `break` is used inside a nested loop, it terminates only the nearest enclosing loop.

### Example

```python
for i in range(1, 4):
    print("Outer loop:", i)

    for j in range(1, 4):
        if j == 3:
            break

        print("Inner loop:", j)
```

### Output

```text
Outer loop: 1
Inner loop: 1
Inner loop: 2
Outer loop: 2
Inner loop: 1
Inner loop: 2
Outer loop: 3
Inner loop: 1
Inner loop: 2
```

The inner loop stops when `j` becomes 3, but the outer loop continues.

---

## 8. Practical Programs

### Program 1: Find the First Even Number

```python
numbers = [3, 7, 9, 12, 15, 18]

for number in numbers:
    if number % 2 == 0:
        print("First even number:", number)
        break
```

Output:

```text
First even number: 12
```

### Program 2: Print Numbers Except Multiples of 3

```python
for i in range(1, 21):
    if i % 3 == 0:
        continue

    print(i)
```

### Program 3: Password Attempts

```python
correct_password = "python123"
attempts = 3

while attempts > 0:
    password = input("Enter password: ")

    if password == correct_password:
        print("Login successful!")
        break

    attempts -= 1
    print("Incorrect password.")
    print("Attempts remaining:", attempts)

else:
    print("Account locked!")
```

The loop's `else` block executes when all attempts are used without a successful login.

### Program 4: Skip Empty Names

```python
names = ["Raj", "", "Amit", "", "Neha", "John"]

for name in names:
    if name == "":
        continue

    print("Welcome", name)
```

### Program 5: Stop When the User Enters Zero

```python
while True:
    number = int(input("Enter a number (0 to stop): "))

    if number == 0:
        print("Program stopped.")
        break

    print("You entered:", number)
```

---

## 9. Student Practice Exercises

Solve these programs independently.

1. Print numbers from 1 to 20 but stop when the number reaches 12 using `break`.
2. Print numbers from 1 to 30, skipping multiples of 5 using `continue`.
3. Print all numbers from 1 to 50 except even numbers.
4. Search for a particular element in a list using `break`.
5. Find the first number divisible by both 3 and 7 in a given range.
6. Create a password verification system with a maximum of 3 attempts.
7. Ask the user for numbers continuously and stop when the user enters 0.
8. Print all positive numbers from a list and skip negative numbers.
9. Use `pass` as a placeholder inside a conditional statement.
10. Create a nested loop where the inner loop stops at a specified value using `break`.

---

## 10. Mini Project – Smart Login Attempt System

Create a basic login system using loops and loop control statements.

### Requirements

1. Store a predefined username and password.
2. Allow the user a maximum of 3 login attempts.
3. Ask for username and password.
4. If both are correct, display a successful login message and terminate the loop using `break`.
5. If the credentials are incorrect, display an error message.
6. Decrease the remaining attempts after every failed login.
7. If all attempts fail, display an account locked message.
8. Do not allow additional login attempts after the limit is reached.

### Expected Output – Successful Login

```text
===== SMART LOGIN SYSTEM =====

Enter username: raj
Enter password: wrong123

Invalid credentials!
Attempts remaining: 2

Enter username: raj
Enter password: python123

Login successful!
Welcome to the system.
```

### Expected Output – Failed Login

```text
===== SMART LOGIN SYSTEM =====

Invalid credentials!
Attempts remaining: 2

Invalid credentials!
Attempts remaining: 1

Invalid credentials!
Attempts remaining: 0

Account locked!
```

### Rules

- Use a `while` loop.
- Use `break` for successful login.
- Use a counter to track attempts.
- Use conditional statements for credential verification.
- Display meaningful messages.

### Challenge

Extend the program to include:

- Different usernames and passwords.
- A maximum of 3 attempts per session.
- A welcome message containing the username.
- An option to exit the login process.

---

## 11. Common Mistakes to Avoid

1. Using `break` when you only want to skip one iteration.
2. Using `continue` when you actually want to terminate the loop.
3. Assuming `pass` skips an iteration.
4. Forgetting to update variables in a `while` loop.
5. Forgetting that `break` exits only the nearest enclosing loop.
6. Writing code after `continue` and expecting it to execute in that iteration.
7. Creating an infinite loop accidentally.
8. Misunderstanding the `else` block associated with a loop.

---

## 12. Trainer Assessment

Ask the student:

1. What are loop control statements?
2. What is the purpose of `break`?
3. What is the purpose of `continue`?
4. What does `pass` do?
5. What is the difference between `break` and `continue`?
6. Does `pass` terminate a loop?
7. Can we use `break` inside a `while` loop?
8. What happens when `break` is used inside a nested loop?
9. When does a loop's `else` block execute?
10. Can `continue` create an infinite loop in a `while` loop?

### Practical Assessment

- Write a number-search program using `break`.
- Print numbers while skipping selected values using `continue`.
- Create a three-attempt login system.
- Demonstrate the use of `pass` in a placeholder block.

### Completion Criteria

The student should be able to:

- Explain all three loop control statements.
- Use `break` to terminate loops.
- Use `continue` to skip iterations.
- Understand the purpose of `pass`.
- Apply loop control statements in nested loops.
- Complete the Smart Login Attempt System independently.

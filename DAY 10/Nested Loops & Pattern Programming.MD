
# Day 10 – Python Nested Loops & Pattern Programming

## 1. Introduction to Nested Loops

A nested loop is a loop inside another loop.

The outer loop controls the main iterations, while the inner loop executes completely for every iteration of the outer loop.

### Syntax

```python
for outer_variable in sequence:
    for inner_variable in sequence:
        # Code to execute
```

### Example

```python
for i in range(1, 4):
    for j in range(1, 4):
        print(i, j)
```

### Output

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

### How It Works

1. The outer loop starts with `i = 1`.
2. The inner loop executes with `j = 1, 2, 3`.
3. After the inner loop finishes, the outer loop moves to `i = 2`.
4. The inner loop executes again.
5. This process continues until the outer loop finishes.

**Important:** If the outer loop executes 3 times and the inner loop executes 3 times per outer iteration, the inner loop executes a total of 9 times.

---

## 2. Understanding Rows and Columns

Nested loops are commonly used to work with rows and columns.

### Example

```python
for row in range(1, 4):
    for column in range(1, 5):
        print("*", end=" ")

    print()
```

### Output

```text
* * * *
* * * *
* * * *
```

### Explanation

- The outer loop controls the number of rows.
- The inner loop controls the number of columns.
- `end=" "` keeps the stars on the same line.
- `print()` moves the cursor to the next line after each row.

---

## 3. Understanding Pattern Programming

Pattern programming means arranging characters, numbers or symbols in a particular structure.

Common pattern types:

1. Square patterns
2. Rectangle patterns
3. Right-angle triangle patterns
4. Inverted triangle patterns
5. Pyramid patterns
6. Number patterns
7. Alphabet patterns

Nested loops are frequently used to create these patterns.

---

## 4. Star Patterns

### Pattern 1: Square Star Pattern

```python
for i in range(5):
    for j in range(5):
        print("*", end=" ")

    print()
```

### Output

```text
* * * * *
* * * * *
* * * * *
* * * * *
* * * * *
```

### Pattern 2: Rectangle Star Pattern

```python
rows = 4
columns = 6

for i in range(rows):
    for j in range(columns):
        print("*", end=" ")

    print()
```

### Output

```text
* * * * * *
* * * * * *
* * * * * *
* * * * * *
```

### Pattern 3: Right-Angled Triangle

```python
for i in range(1, 6):
    for j in range(i):
        print("*", end=" ")

    print()
```

### Output

```text
*
* *
* * *
* * * *
* * * * *
```

### Explanation

The number of stars depends on the current value of `i`.

- First row: 1 star
- Second row: 2 stars
- Third row: 3 stars
- Fourth row: 4 stars
- Fifth row: 5 stars

### Pattern 4: Inverted Right-Angled Triangle

```python
for i in range(5, 0, -1):
    for j in range(i):
        print("*", end=" ")

    print()
```

### Output

```text
* * * * *
* * * *
* * *
* *
*
```

### Pattern 5: Left-Sided Inverted Triangle

```python
for i in range(5, 0, -1):
    for j in range(5 - i):
        print(" ", end=" ")

    for j in range(i):
        print("*", end=" ")

    print()
```

### Output

```text
* * * * *
  * * * *
    * * *
      * *
        *
```

### Pattern 6: Pyramid Pattern

```python
rows = 5

for i in range(1, rows + 1):
    for j in range(rows - i):
        print(" ", end="")

    for j in range(2 * i - 1):
        print("*", end="")

    print()
```

### Output

```text
    *
   ***
  *****
 *******
*********
```

### Explanation

A pyramid has two main parts:

1. Spaces before the stars.
2. Stars in the current row.

For each row:

- Spaces = `rows - i`
- Stars = `2 * i - 1`

### Pattern 7: Inverted Pyramid

```python
rows = 5

for i in range(rows, 0, -1):
    for j in range(rows - i):
        print(" ", end="")

    for j in range(2 * i - 1):
        print("*", end="")

    print()
```

### Output

```text
*********
 *******
  *****
   ***
    *
```

### Pattern 8: Diamond Pattern

```python
rows = 5

for i in range(1, rows + 1):
    for j in range(rows - i):
        print(" ", end="")

    for j in range(2 * i - 1):
        print("*", end="")

    print()

for i in range(rows - 1, 0, -1):
    for j in range(rows - i):
        print(" ", end="")

    for j in range(2 * i - 1):
        print("*", end="")

    print()
```

### Output

```text
    *
   ***
  *****
 *******
*********
 *******
  *****
   ***
    *
```

---

## 5. Number Patterns

### Pattern 1: Increasing Number Triangle

```python
for i in range(1, 6):
    for j in range(1, i + 1):
        print(j, end=" ")

    print()
```

### Output

```text
1
1 2
1 2 3
1 2 3 4
1 2 3 4 5
```

### Pattern 2: Repeated Row Number

```python
for i in range(1, 6):
    for j in range(i):
        print(i, end=" ")

    print()
```

### Output

```text
1
2 2
3 3 3
4 4 4 4
5 5 5 5 5
```

### Pattern 3: Continuous Number Triangle

```python
number = 1

for i in range(1, 5):
    for j in range(i):
        print(number, end=" ")
        number += 1

    print()
```

### Output

```text
1
2 3
4 5 6
7 8 9 10
```

### Pattern 4: Inverted Number Triangle

```python
for i in range(5, 0, -1):
    for j in range(1, i + 1):
        print(j, end=" ")

    print()
```

### Output

```text
1 2 3 4 5
1 2 3 4
1 2 3
1 2
1
```

### Pattern 5: Number Pyramid

```python
rows = 5

for i in range(1, rows + 1):
    for j in range(rows - i):
        print(" ", end="")

    for j in range(1, i + 1):
        print(j, end="")

    for j in range(i - 1, 0, -1):
        print(j, end="")

    print()
```

### Output

```text
    1
   121
  12321
 1234321
123454321
```

---

## 6. Alphabet Patterns

Python allows us to work with characters using ASCII values and the `chr()` function.

The `chr()` function converts an integer Unicode code point into a character.

### Example

```python
print(chr(65))
print(chr(66))
print(chr(67))
```

Output:

```text
A
B
C
```

### Pattern 1: Alphabet Triangle

```python
for i in range(1, 6):
    for j in range(i):
        print(chr(65 + j), end=" ")

    print()
```

### Output

```text
A
A B
A B C
A B C D
A B C D E
```

### Pattern 2: Repeated Alphabet Rows

```python
for i in range(5):
    for j in range(i + 1):
        print(chr(65 + i), end=" ")

    print()
```

### Output

```text
A
B B
C C C
D D D D
E E E E E
```

---

## 7. Nested Loops with Conditional Statements

We can use `if` statements inside nested loops to create more complex patterns.

### Example: Print a Hollow Square

```python
size = 5

for i in range(size):
    for j in range(size):
        if i == 0 or i == size - 1 or j == 0 or j == size - 1:
            print("*", end=" ")
        else:
            print(" ", end=" ")

    print()
```

### Output

```text
* * * * *
*       *
*       *
*       *
* * * * *
```

### Example: Print a Checkerboard Pattern

```python
size = 5

for i in range(size):
    for j in range(size):
        if (i + j) % 2 == 0:
            print("*", end=" ")
        else:
            print("-", end=" ")

    print()
```

### Output

```text
* - * - *
- * - * -
* - * - *
- * - * -
* - * - *
```

---

## 8. Nested Loops with Lists

Nested loops are also used to process two-dimensional lists.

A two-dimensional list is a list containing other lists.

### Example

```python
matrix = [
    [1, 2, 3],
    [4, 5, 6],
    [7, 8, 9]
]

for row in matrix:
    for value in row:
        print(value, end=" ")

    print()
```

### Output

```text
1 2 3
4 5 6
7 8 9
```

### Example: Display Matrix Row by Row

```python
matrix = [
    [10, 20, 30],
    [40, 50, 60],
    [70, 80, 90]
]

for i in range(len(matrix)):
    print("Row:", i + 1)

    for j in range(len(matrix[i])):
        print(matrix[i][j], end=" ")

    print()
```

---

## 9. Practical Programs

### Program 1: Multiplication Tables from 1 to 5

```python
for i in range(1, 6):
    print("Table of", i)

    for j in range(1, 11):
        print(i, "x", j, "=", i * j)

    print()
```

### Program 2: Print All Pairs of Numbers

```python
for i in range(1, 4):
    for j in range(1, 4):
        print("(", i, ",", j, ")")
```

### Program 3: Find Common Elements in Two Lists

```python
list1 = [10, 20, 30, 40]
list2 = [20, 40, 50, 60]

for i in list1:
    for j in list2:
        if i == j:
            print("Common element:", i)
```

### Program 4: Matrix Addition

```python
matrix1 = [
    [1, 2],
    [3, 4]
]

matrix2 = [
    [5, 6],
    [7, 8]
]

result = []

for i in range(len(matrix1)):
    row = []

    for j in range(len(matrix1[i])):
        row.append(matrix1[i][j] + matrix2[i][j])

    result.append(row)

for row in result:
    print(row)
```

### Output

```text
[6, 8]
[10, 12]
```

---

## 10. Student Practice Exercises

Solve these programs independently.

1. Print a square pattern of 10 rows and 10 columns.
2. Print a rectangle pattern using user-provided rows and columns.
3. Print a right-angled triangle using stars.
4. Print an inverted right-angled triangle.
5. Print a pyramid pattern.
6. Print an inverted pyramid pattern.
7. Print a diamond pattern.
8. Print an increasing number triangle.
9. Print a repeated row number pattern.
10. Print an alphabet triangle.
11. Print a hollow square pattern.
12. Print a checkerboard pattern.
13. Generate multiplication tables from 1 to 10.
14. Print all possible pairs from two given lists.
15. Add two matrices using nested loops.

---

## 11. Mini Project – Pattern Generator System

Create a menu-driven Python program that generates different patterns based on user selection.

### Requirements

Display the following menu:

```text
===== PATTERN GENERATOR =====

1. Square Star Pattern
2. Right-Angled Triangle
3. Inverted Triangle
4. Pyramid Pattern
5. Diamond Pattern
6. Number Triangle
7. Alphabet Triangle
8. Exit

Enter your choice:
```

### Program Behaviour

1. Ask the user to select a pattern.
2. Ask for the number of rows.
3. Generate the selected pattern.
4. Display the pattern.
5. Show the menu again.
6. Continue until the user selects Exit.

### Rules

- Use a `while` loop for the menu.
- Use nested `for` loops for pattern generation.
- Use `if-elif-else` for menu selection.
- Validate the number of rows.
- Handle invalid menu choices.
- Use separate code blocks or functions for each pattern only if the student has already studied functions.

### Challenge

Add these patterns:

- Hollow square
- Inverted pyramid
- Continuous number triangle
- Repeated alphabet pattern

---

## 12. Common Mistakes to Avoid

1. Incorrect indentation in nested loops.
2. Confusing the outer loop with the inner loop.
3. Using an incorrect `range()` value.
4. Forgetting `print()` after completing a row.
5. Using `end=" "` incorrectly.
6. Printing the wrong number of spaces in pyramid patterns.
7. Updating number counters in the wrong loop.
8. Using the wrong condition for hollow patterns.
9. Forgetting that the inner loop executes completely for every outer iteration.
10. Creating unnecessary nested loops when a single loop is sufficient.

---

## 13. Trainer Assessment

Ask the student:

1. What is a nested loop?
2. What is the difference between an outer loop and an inner loop?
3. How many times does an inner loop execute if the outer loop runs 4 times and the inner loop runs 3 times?
4. What is the purpose of `end=" "`?
5. Why do we use an empty `print()` after completing a row?
6. How can we generate a pyramid pattern?
7. What is the purpose of `chr()`?
8. What is a two-dimensional list?
9. How can nested loops be used to process a matrix?
10. Can we use conditional statements inside nested loops?

### Practical Assessment

- Create a star pyramid.
- Create a number triangle.
- Create an alphabet pattern.
- Generate multiplication tables from 1 to 10.
- Add two matrices using nested loops.
- Complete the Pattern Generator System independently.

### Completion Criteria

The student should be able to:

- Explain nested loop execution.
- Understand rows and columns.
- Create star, number and alphabet patterns.
- Use conditions inside nested loops.
- Process two-dimensional lists.
- Solve basic matrix operations.
- Complete the Pattern Generator System independently.


# Day 31 – Iterators & Generators

## 1. Introduction to Iteration

Iteration means accessing elements one by one from a collection or sequence.

Python provides different ways to perform iteration:

- `for` loops
- `while` loops
- Iterators
- Generators

### Example

```python
numbers = [10, 20, 30, 40]

for number in numbers:
    print(number)
```

**Output:**
```text
10
20
30
40
```

A `for` loop internally uses Python's iterator protocol to access elements.

---

## 2. What is an Iterable?

An iterable is an object that can return an iterator.

Examples:

- List
- Tuple
- String
- Set
- Dictionary
- Range
- File objects

### Example

```python
numbers = [10, 20, 30]

for number in numbers:
    print(number)
```

The list is an iterable because Python can obtain an iterator from it.

### Checking Whether an Object Is Iterable

Python provides the `iter()` function.

```python
numbers = [10, 20, 30]

result = iter(numbers)

print(result)
```

The output displays an iterator object. Its memory address may differ.

We can also check whether an object supports iteration:

```python
from collections.abc import Iterable

print(isinstance([1, 2, 3], Iterable))
print(isinstance("Python", Iterable))
print(isinstance(100, Iterable))
```

**Output:**
```text
True
True
False
```

An integer is not iterable by default.

---

## 3. What is an Iterator?

An iterator is an object that produces values one at a time.

An iterator follows two important methods:

1. `__iter__()` – Returns the iterator object.
2. `__next__()` – Returns the next value.

When no values remain, `__next__()` raises `StopIteration`.

### Example

```python
numbers = [10, 20, 30]

iterator = iter(numbers)

print(next(iterator))
print(next(iterator))
print(next(iterator))
```

**Output:**
```text
10
20
30
```

### What Happens When Values Finish?

```python
numbers = [10, 20]

iterator = iter(numbers)

print(next(iterator))
print(next(iterator))
print(next(iterator))
```

**Output:**
```text
10
20
StopIteration
```

The third `next()` call raises a `StopIteration` exception because no elements remain.

---

## 4. Understanding iter() and next()

### iter()

The `iter()` function obtains an iterator from an iterable.

```python
names = ["Raj", "Aman", "Rahul"]

iterator = iter(names)

print(type(names))
print(type(iterator))
```

The list and its iterator are different objects.

### next()

The `next()` function retrieves the next available element.

```python
colors = ["Red", "Green", "Blue"]

iterator = iter(colors)

print(next(iterator))
print(next(iterator))
print(next(iterator))
```

**Output:**
```text
Red
Green
Blue
```

### Using a Default Value with next()

We can provide a default value to avoid `StopIteration`.

```python
numbers = [10, 20]

iterator = iter(numbers)

print(next(iterator, "No more values"))
print(next(iterator, "No more values"))
print(next(iterator, "No more values"))
```

**Output:**
```text
10
20
No more values
```

---

## 5. How a for Loop Uses Iterators

Consider:

```python
numbers = [10, 20, 30]

for number in numbers:
    print(number)
```

Python internally performs an operation similar to:

```python
numbers = [10, 20, 30]

iterator = iter(numbers)

while True:
    try:
        number = next(iterator)
        print(number)
    except StopIteration:
        break
```

The `for` loop automatically handles iterator creation and stopping.

You normally do not need to write this internal logic yourself.

---

## 6. Iterable vs Iterator

| Iterable | Iterator |
|---|---|
| Can provide an iterator | Produces values one at a time |
| Supports `iter()` | Supports `next()` |
| May be reusable | Usually consumed as values are retrieved |
| Example: list | Example: `iter(list)` |

### Example

```python
numbers = [10, 20, 30]

iterator = iter(numbers)

print(next(iterator))
print(next(iterator))

print(numbers)
```

**Output:**
```text
10
20
[10, 20, 30]
```

The original list remains unchanged. Only the iterator's position advances.

---

## 7. Iterator Exhaustion

An iterator is generally consumed as values are retrieved.

After reaching the end, it remains exhausted.

```python
numbers = [1, 2, 3]

iterator = iter(numbers)

print(list(iterator))
print(list(iterator))
```

**Output:**
```text
[1, 2, 3]
[]
```

The second conversion returns an empty list because the iterator has already been consumed.

However, we can create a fresh iterator from the original iterable.

```python
numbers = [1, 2, 3]

first_iterator = iter(numbers)
second_iterator = iter(numbers)

print(list(first_iterator))
print(list(second_iterator))
```

**Output:**
```text
[1, 2, 3]
[1, 2, 3]
```

---

## 8. Creating a Custom Iterator

Python allows us to create our own iterator classes.

A custom iterator must implement:

- `__iter__()`
- `__next__()`

### Example: Number Iterator

```python
class NumberIterator:

    def __init__(self, limit):
        self.limit = limit
        self.current = 1

    def __iter__(self):
        return self

    def __next__(self):
        if self.current <= self.limit:
            value = self.current
            self.current += 1
            return value

        raise StopIteration


numbers = NumberIterator(5)

for number in numbers:
    print(number)
```

**Output:**
```text
1
2
3
4
5
```

### Explanation

1. `__init__()` initializes the iterator.
2. `__iter__()` returns the iterator itself.
3. `__next__()` checks whether another value is available.
4. If available, it returns the value and updates the counter.
5. Otherwise, it raises `StopIteration`.

---

## 9. Custom Iterator with a Different Sequence

### Example: Even Number Iterator

Create an iterator that returns even numbers up to a specified limit.

```python
class EvenIterator:

    def __init__(self, limit):
        self.limit = limit
        self.current = 2

    def __iter__(self):
        return self

    def __next__(self):
        if self.current <= self.limit:
            value = self.current
            self.current += 2
            return value

        raise StopIteration


even_numbers = EvenIterator(10)

for number in even_numbers:
    print(number)
```

**Output:**
```text
2
4
6
8
10
```

---

# PART 2 – GENERATORS

## 10. What is a Generator?

A generator is a special type of iterator that produces values one at a time.

Generators are commonly created using:

1. Generator functions with `yield`.
2. Generator expressions.

Generators are useful when processing large amounts of data because they do not need to store all generated values in memory at once.

---

## 11. Generator Functions

A generator function looks like a normal function but uses the `yield` keyword instead of returning every value with `return`.

### Example

```python
def generate_numbers():
    yield 10
    yield 20
    yield 30


numbers = generate_numbers()

print(next(numbers))
print(next(numbers))
print(next(numbers))
```

**Output:**
```text
10
20
30
```

### Important Difference

A normal function returns a value using `return` and ends its execution.

A generator function produces a value using `yield` and temporarily pauses its execution.

When another value is requested, execution resumes from where it paused.

---

## 12. Understanding yield

The `yield` keyword:

- Produces a value.
- Pauses the generator function.
- Preserves its local variables and execution state.
- Resumes execution when the next value is requested.

### Example

```python
def demo():
    print("First step")

    yield 10

    print("Second step")

    yield 20

    print("Third step")

    yield 30


generator = demo()

print(next(generator))
print(next(generator))
print(next(generator))
```

**Output:**
```text
First step
10
Second step
20
Third step
30
```

Notice that the function does not execute all statements immediately.

It executes only until the next `yield`.

---

## 13. Generator vs Normal Function

### Normal Function

```python
def get_numbers():
    return [10, 20, 30, 40]


numbers = get_numbers()

print(numbers)
```

**Output:**
```text
[10, 20, 30, 40]
```

The function creates and returns a complete list.

### Generator Function

```python
def get_numbers():
    yield 10
    yield 20
    yield 30
    yield 40


numbers = get_numbers()

for number in numbers:
    print(number)
```

**Output:**
```text
10
20
30
40
```

The generator produces values one at a time when requested.

---

## 14. Generator with a Loop

Generators can use loops to produce a sequence of values.

### Example: Generate Numbers

```python
def generate_numbers(limit):
    for number in range(1, limit + 1):
        yield number


for number in generate_numbers(5):
    print(number)
```

**Output:**
```text
1
2
3
4
5
```

### Example: Generate Even Numbers

```python
def even_numbers(limit):
    for number in range(2, limit + 1, 2):
        yield number


for number in even_numbers(10):
    print(number)
```

**Output:**
```text
2
4
6
8
10
```

---

## 15. Generator Expressions

A generator expression is a compact way to create a generator.

Its syntax is similar to a list comprehension, but it uses parentheses instead of square brackets.

### List Comprehension

```python
squares = [number ** 2 for number in range(1, 6)]

print(squares)
```

**Output:**
```text
[1, 4, 9, 16, 25]
```

### Generator Expression

```python
squares = (number ** 2 for number in range(1, 6))

print(squares)

for square in squares:
    print(square)
```

The first print displays a generator object. The loop then produces:

```text
1
4
9
16
25
```

### Difference

| List Comprehension | Generator Expression |
|---|---|
| Uses `[]` | Uses `()` |
| Creates a complete list | Produces values on demand |
| Stores all results in memory | Does not store all generated results |
| Can be reused and indexed | Usually consumed once |
| Useful for smaller collections | Useful for large or streamed data |

---

## 16. Generator with Conditional Logic

Generators can also contain conditions.

### Example: Generate Odd Numbers

```python
def odd_numbers(limit):
    for number in range(1, limit + 1):
        if number % 2 != 0:
            yield number


for number in odd_numbers(10):
    print(number)
```

**Output:**
```text
1
3
5
7
9
```

---

## 17. Generator with Multiple Conditions

### Example: Generate Numbers Divisible by 3 and 5

```python
def divisible_numbers(limit):
    for number in range(1, limit + 1):
        if number % 3 == 0 and number % 5 == 0:
            yield number


for number in divisible_numbers(100):
    print(number)
```

**Output:**
```text
15
30
45
60
75
90
```

---

## 18. Generator and Memory Efficiency

Generators are useful when we do not need all results at once.

### Example: List of One Million Numbers

```python
numbers = [number for number in range(1000000)]

print(len(numbers))
```

The list stores all one million integer references and their integer objects in memory.

### Generator with One Million Numbers

```python
numbers = (number for number in range(1000000))

print(next(numbers))
print(next(numbers))
print(next(numbers))
```

**Output:**
```text
0
1
2
```

The generator produces values as requested instead of creating a list containing all the results.

**Important:** Generators are generally more memory-efficient for large sequences, but they are not automatically faster for every task.

---

## 19. Generator with File Handling

Generators are useful when reading large files line by line.

### Example

Create a file named `students.txt` containing:

```text
Raj
Aman
Rahul
Priya
```

Now create a generator:

```python
def read_students(filename):
    with open(filename, "r", encoding="utf-8") as file:
        for line in file:
            yield line.strip()


for student in read_students("students.txt"):
    print(student)
```

**Output:**
```text
Raj
Aman
Rahul
Priya
```

The file is opened when the generator starts executing and is closed automatically when the `with` block finishes, including when iteration completes normally.

If iteration is stopped early, the generator may remain suspended with the file open until it is closed or finalized. Use explicit generator closing or a context-managed design when early termination must release resources immediately.

---

## 20. Generator with return

A generator can also use `return`.

However, `return` ends the generator. It does not produce a normal yielded value.

```python
def demo():
    yield 10
    yield 20
    return
    yield 30


for number in demo():
    print(number)
```

**Output:**
```text
10
20
```

The `30` is never produced because the generator has already finished.

---

## 21. Using yield from

`yield from` allows a generator to yield values from another iterable or generator.

### Example

```python
def generate_numbers():
    yield from [10, 20, 30]
    yield from [40, 50]


for number in generate_numbers():
    print(number)
```

**Output:**
```text
10
20
30
40
50
```

It is a convenient way to delegate value production to another iterable.

---

## 22. Generator Methods

Generators provide several useful methods.

| Method | Description |
|---|---|
| `next()` | Requests the next value |
| `send()` | Sends a value into a suspended generator |
| `close()` | Requests the generator to stop |
| `throw()` | Raises an exception inside the generator |

### Example: send()

```python
def calculator():
    value = yield "Ready"

    while True:
        value = yield value * 2


gen = calculator()

print(next(gen))
print(gen.send(10))
print(gen.send(20))
```

**Output:**
```text
Ready
20
40
```

### Explanation

- The first `next()` starts the generator and pauses at the first `yield`.
- `send(10)` provides `10` as the result of the paused `yield`.
- The generator multiplies it by 2 and yields `20`.
- `send(20)` repeats the process and yields `40`.

**Important:** A generator must be started with `next()` or `send(None)` before sending it a non-None value.

### Example: close()

```python
def numbers():
    try:
        yield 10
        yield 20
        yield 30
    finally:
        print("Generator closed")


gen = numbers()

print(next(gen))
gen.close()
```

**Output:**
```text
10
Generator closed
```

Closing a generator raises `GeneratorExit` inside it. The `finally` block runs before it stops.

---

## 23. Iterator vs Generator

| Iterator | Generator |
|---|---|
| An object following the iterator protocol | A convenient way to create an iterator |
| Usually implemented using a class | Commonly implemented using `yield` |
| Requires `__iter__()` and `__next__()` | Python handles the iterator protocol |
| Can contain complex state and behavior | Often shorter and easier to write |
| May require more code | Usually requires less code |

Every generator is an iterator, but not every iterator is a generator.

---

# PART 3 – PRACTICAL PROGRAMS

## 24. Program 1: Generate Fibonacci Numbers

```python
def fibonacci(count):
    a, b = 0, 1

    for _ in range(count):
        yield a
        a, b = b, a + b


for number in fibonacci(10):
    print(number)
```

**Output:**
```text
0
1
1
2
3
5
8
13
21
34
```

---

## 25. Program 2: Generate Prime Numbers

```python
def is_prime(number):
    if number < 2:
        return False

    for i in range(2, int(number ** 0.5) + 1):
        if number % i == 0:
            return False

    return True


def prime_numbers(limit):
    for number in range(2, limit + 1):
        if is_prime(number):
            yield number


for prime in prime_numbers(30):
    print(prime)
```

**Output:**
```text
2
3
5
7
11
13
17
19
23
29
```

---

## 26. Program 3: Custom Countdown Iterator

```python
class Countdown:

    def __init__(self, start):
        self.current = start

    def __iter__(self):
        return self

    def __next__(self):
        if self.current > 0:
            value = self.current
            self.current -= 1
            return value

        raise StopIteration


countdown = Countdown(5)

for number in countdown:
    print(number)
```

**Output:**
```text
5
4
3
2
1
```

---

## 27. Program 4: Generate Squared Numbers

```python
def squares(limit):
    for number in range(1, limit + 1):
        yield number ** 2


for square in squares(5):
    print(square)
```

**Output:**
```text
1
4
9
16
25
```

---

## 28. Program 5: Process Large Data in Batches

A generator can divide data into smaller batches.

```python
def batch_data(data, batch_size):
    for i in range(0, len(data), batch_size):
        yield data[i:i + batch_size]


numbers = list(range(1, 11))

for batch in batch_data(numbers, 3):
    print(batch)
```

**Output:**
```text
[1, 2, 3]
[4, 5, 6]
[7, 8, 9]
[10]
```

This technique is useful when processing data in manageable groups.

---

# PART 4 – MINI PROJECT

## 29. Mini Project: Data Processing System Using Iterators and Generators

### Project Description

Create a data processing system that reads student marks and processes the records one at a time.

The system should demonstrate:

- Custom iterators.
- Generator functions.
- Generator expressions.
- File handling.
- Data filtering.
- Batch processing.

### Project Requirements

#### A. Create Student Data

Create a file named `students.txt`.

Store one student record per line:

```text
Raj,85
Aman,72
Rahul,91
Priya,65
Neha,95
```

#### B. Student Record Generator

Create a generator named `read_students()`.

Requirements:

- Open the student file.
- Read one line at a time.
- Split the student name and marks.
- Convert marks into an integer.
- Yield each student record.

#### C. Pass Student Generator

Create a generator named `passed_students()`.

Requirements:

- Accept student records.
- Yield only students with marks greater than or equal to 40.

#### D. Topper Generator

Create a generator that produces students with marks greater than or equal to 90.

#### E. Batch Processing

Create a generator that divides student records into batches of three.

#### F. Custom Iterator

Create a custom iterator named `StudentIterator`.

Requirements:

- Accept a list of student records.
- Return one record at a time.
- Stop using `StopIteration`.

#### G. Main Program

Display:

1. All students.
2. Passed students.
3. Topper students.
4. Student records in batches.
5. Total number of students.

### Sample Expected Output

```text
===== STUDENT DATA PROCESSING SYSTEM =====

All Students:
Raj - 85
Aman - 72
Rahul - 91
Priya - 65
Neha - 95

Passed Students:
Raj - 85
Aman - 72
Rahul - 91
Priya - 65
Neha - 95

Topper Students:
Rahul - 91
Neha - 95

Student Batches:
Batch 1:
Raj - 85
Aman - 72
Rahul - 91

Batch 2:
Priya - 65
Neha - 95

Total Students: 5
```

### Project Challenge

After completing the basic project, add:

1. Calculate the average marks using a generator.
2. Find the highest marks.
3. Find the lowest marks.
4. Generate a report containing only students above the average.
5. Handle missing or incorrectly formatted records.
6. Process a larger file without loading all records into a list.

---

# PART 5 – STUDENT PRACTICE

## 30. Practice Questions

### Basic Level

1. What is iteration?
2. What is an iterable?
3. What is an iterator?
4. What is the difference between iterable and iterator?
5. What does `iter()` do?
6. What does `next()` do?
7. What is `StopIteration`?
8. What is a generator?
9. What is the purpose of `yield`?
10. What is a generator expression?

### Intermediate Level

11. Create an iterator that generates numbers from 1 to 20.

12. Create an iterator that returns multiples of 5 up to 100.

13. Write a generator that produces even numbers.

14. Write a generator that produces odd numbers.

15. Create a generator for the Fibonacci sequence.

16. Write a generator that returns the squares of numbers from 1 to 20.

17. Create a generator that reads a text file line by line.

18. Create a generator that filters students who passed an examination.

19. Write a generator expression that produces cubes of numbers from 1 to 10.

20. Explain why generators are useful for large datasets.

### Advanced Level

21. Create a custom iterator that produces a countdown.

22. Create a generator that produces prime numbers up to a given limit.

23. Create a generator that reads a CSV file and yields one row at a time.

24. Create a batch-processing generator that accepts any iterable and yields groups of a fixed size.

25. Demonstrate the use of `send()` in a generator.

26. Explain the difference between `return` and `yield`.

27. Create a generator that combines values from two separate iterables using `yield from`.

28. Compare memory usage between a list comprehension and a generator expression for a large range.

---

# PART 6 – TRAINER ASSESSMENT

## 31. Practical Assessment

| Task | Marks |
|---|---:|
| Explain iterable and iterator | 10 |
| Demonstrate `iter()` and `next()` | 10 |
| Implement a custom iterator | 15 |
| Explain and implement `StopIteration` | 10 |
| Create generator functions using `yield` | 15 |
| Implement generator expressions | 10 |
| Demonstrate file processing with generators | 10 |
| Complete the Data Processing System | 20 |
| **Total** | **100** |

### Oral Questions

1. What is the difference between an iterable and an iterator?
2. Which methods are required for a custom iterator?
3. What happens when an iterator has no more values?
4. Why does a generator use `yield`?
5. What happens when a generator reaches `yield`?
6. Can a generator be reused after it is exhausted?
7. What is the difference between a list comprehension and a generator expression?
8. Why are generators useful for large files?
9. What is the purpose of `yield from`?
10. What is the difference between `send()` and `next()`?

---

## 32. Completion Criteria

The student should be able to:

- Explain iteration and the iterator protocol.
- Identify iterable and iterator objects.
- Use `iter()` and `next()`.
- Explain `StopIteration`.
- Create custom iterator classes.
- Understand how `for` loops use iterators.
- Create generator functions using `yield`.
- Understand generator expressions.
- Explain the difference between `return` and `yield`.
- Use generators for file processing.
- Use `yield from`, `send()` and `close()` at a basic level.
- Explain why generators are useful for memory-efficient processing.
- Complete the Data Processing System mini-project.

**Day 31 Completed – Iterators & Generators**

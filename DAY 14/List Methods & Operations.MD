
# Day 14 – List Methods & Operations

## 1. Revisiting Python Lists

A list is an ordered and mutable collection used to store multiple values in a single variable.

Example:

```python
students = ["Raj", "Aman", "Rahul", "Priya"]

print(students)
```

**Output:**
```text
['Raj', 'Aman', 'Rahul', 'Priya']
```

Python provides several built-in list methods that make it easier to add, remove, search, sort and manage elements.

---

## 2. Complete Overview of Common List Methods

| Method | Description |
|---|---|
| `append()` | Adds one element at the end |
| `extend()` | Adds multiple elements |
| `insert()` | Adds an element at a specific position |
| `remove()` | Removes the first matching value |
| `pop()` | Removes and returns an element |
| `clear()` | Removes all elements |
| `index()` | Returns the index of an element |
| `count()` | Counts occurrences of an element |
| `sort()` | Sorts the original list |
| `reverse()` | Reverses the original list |
| `copy()` | Creates a shallow copy |

We have already introduced some methods in Day 13. Today, we will explore their behavior in greater detail and learn the remaining methods.

---

## 3. append() – Adding an Element

The `append()` method adds one element at the end of a list.

### Syntax

```python
list_name.append(element)
```

### Example

```python
languages = ["Python", "Java"]

languages.append("JavaScript")

print(languages)
```

**Output:**
```text
['Python', 'Java', 'JavaScript']
```

### Appending Different Data Types

```python
data = [10, 20, 30]

data.append("Python")
data.append(45.5)
data.append(True)

print(data)
```

**Output:**
```text
[10, 20, 30, 'Python', 45.5, True]
```

### Important Point

`append()` modifies the original list and returns `None`.

```python
numbers = [10, 20]

result = numbers.append(30)

print(numbers)
print(result)
```

**Output:**
```text
[10, 20, 30]
None
```

Do not assign the result of `append()` back to the list.

Incorrect:

```python
numbers = [10, 20]

numbers = numbers.append(30)

print(numbers)
```

**Output:**
```text
None
```

---

## 4. extend() – Adding Multiple Elements

The `extend()` method adds elements from an iterable to the end of an existing list.

### Syntax

```python
list_name.extend(iterable)
```

### Example

```python
numbers = [10, 20, 30]

numbers.extend([40, 50, 60])

print(numbers)
```

**Output:**
```text
[10, 20, 30, 40, 50, 60]
```

### Extending with a Tuple

```python
numbers = [1, 2]

numbers.extend((3, 4, 5))

print(numbers)
```

**Output:**
```text
[1, 2, 3, 4, 5]
```

### Extending with a String

```python
letters = ["A", "B"]

letters.extend("CDE")

print(letters)
```

**Output:**
```text
['A', 'B', 'C', 'D', 'E']
```

A string is an iterable, so its characters are added individually.

---

## 5. insert() – Inserting Elements

The `insert()` method adds an element at a specified index.

### Syntax

```python
list_name.insert(index, element)
```

### Example

```python
fruits = ["Apple", "Mango", "Orange"]

fruits.insert(1, "Banana")

print(fruits)
```

**Output:**
```text
['Apple', 'Banana', 'Mango', 'Orange']
```

### Inserting at the Beginning

```python
numbers = [20, 30, 40]

numbers.insert(0, 10)

print(numbers)
```

**Output:**
```text
[10, 20, 30, 40]
```

### Inserting Beyond the Current List Length

```python
numbers = [10, 20, 30]

numbers.insert(10, 40)

print(numbers)
```

**Output:**
```text
[10, 20, 30, 40]
```

An index greater than the list length inserts the element at the end.

---

## 6. remove() – Removing Elements by Value

The `remove()` method removes the first occurrence of a specified value.

### Example

```python
numbers = [10, 20, 30, 20, 40]

numbers.remove(20)

print(numbers)
```

**Output:**
```text
[10, 30, 20, 40]
```

Only the first matching `20` is removed.

### Handling ValueError

If the requested value does not exist, Python raises a `ValueError`.

```python
fruits = ["Apple", "Banana"]

fruits.remove("Mango")
```

**Output:**
```text
ValueError: list.remove(x): x not in list
```

We can check membership before removing:

```python
fruits = ["Apple", "Banana"]

if "Mango" in fruits:
    fruits.remove("Mango")
else:
    print("Item Not Found")
```

**Output:**
```text
Item Not Found
```

---

## 7. pop() – Removing Elements by Index

The `pop()` method removes and returns an element.

### Syntax

```python
list_name.pop(index)
```

The index is optional. If omitted, the last element is removed.

### Example 1: Remove Last Element

```python
numbers = [10, 20, 30, 40]

removed = numbers.pop()

print("Removed:", removed)
print("Updated:", numbers)
```

**Output:**
```text
Removed: 40
Updated: [10, 20, 30]
```

### Example 2: Remove an Element by Index

```python
numbers = [10, 20, 30, 40]

removed = numbers.pop(1)

print("Removed:", removed)
print("Updated:", numbers)
```

**Output:**
```text
Removed: 20
Updated: [10, 30, 40]
```

### Handling IndexError

Calling `pop()` on an empty list or using an invalid index raises `IndexError`.

```python
numbers = []

numbers.pop()
```

**Output:**
```text
IndexError: pop from empty list
```

---

## 8. clear() – Removing All Elements

The `clear()` method removes every element but keeps the list variable.

```python
students = ["Raj", "Aman", "Rahul"]

students.clear()

print(students)
```

**Output:**
```text
[]
```

The list still exists; it is simply empty.

---

## 9. index() – Finding the Position of an Element

The `index()` method returns the index of the first occurrence of a specified value.

### Syntax

```python
list_name.index(value)
```

### Example

```python
fruits = ["Apple", "Banana", "Mango", "Orange"]

position = fruits.index("Mango")

print(position)
```

**Output:**
```text
2
```

### Searching Within a Specific Range

```python
numbers = [10, 20, 30, 20, 40]

position = numbers.index(20, 2)

print(position)
```

**Output:**
```text
3
```

The search starts from index `2`.

The optional syntax is:

```python
list_name.index(value, start, stop)
```

The `stop` index is excluded.

### Handling ValueError

```python
fruits = ["Apple", "Banana"]

if "Mango" in fruits:
    print(fruits.index("Mango"))
else:
    print("Element Not Found")
```

**Output:**
```text
Element Not Found
```

---

## 10. count() – Counting Occurrences

The `count()` method returns how many times a value appears in a list.

### Example

```python
numbers = [10, 20, 10, 30, 10, 40]

result = numbers.count(10)

print(result)
```

**Output:**
```text
3
```

### Counting Names

```python
students = ["Raj", "Aman", "Raj", "Rahul", "Raj"]

print("Raj appears:", students.count("Raj"), "times")
```

**Output:**
```text
Raj appears: 3 times
```

---

## 11. sort() – Sorting a List

The `sort()` method sorts elements of a list in ascending order by default.

It modifies the original list.

### Example 1: Ascending Order

```python
numbers = [50, 10, 40, 20, 30]

numbers.sort()

print(numbers)
```

**Output:**
```text
[10, 20, 30, 40, 50]
```

### Example 2: Descending Order

```python
numbers = [50, 10, 40, 20, 30]

numbers.sort(reverse=True)

print(numbers)
```

**Output:**
```text
[50, 40, 30, 20, 10]
```

### Example 3: Sorting Strings

```python
names = ["Rahul", "Aman", "Priya", "Raj"]

names.sort()

print(names)
```

**Output:**
```text
['Aman', 'Priya', 'Rahul', 'Raj']
```

String sorting is based on Unicode code points, so capitalization can affect the ordering.

### Example 4: Case-Insensitive Sorting

```python
names = ["raj", "Aman", "rahul", "Priya"]

names.sort(key=str.lower)

print(names)
```

**Output:**
```text
['Aman', 'Priya', 'raj', 'rahul']
```

### Example 5: Sorting Without Modifying the Original List

Use the built-in `sorted()` function when you want a new sorted list.

```python
numbers = [50, 10, 40, 20, 30]

result = sorted(numbers)

print("Original:", numbers)
print("Sorted:", result)
```

**Output:**
```text
Original: [50, 10, 40, 20, 30]
Sorted: [10, 20, 30, 40, 50]
```

### Difference Between sort() and sorted()

| `sort()` | `sorted()` |
|---|---|
| List method | Built-in function |
| Modifies original list | Creates a new sorted list |
| Returns `None` | Returns a new list |
| Works on lists | Works on any iterable |

---

## 12. reverse() – Reversing a List

The `reverse()` method reverses the order of elements in the original list.

```python
numbers = [10, 20, 30, 40, 50]

numbers.reverse()

print(numbers)
```

**Output:**
```text
[50, 40, 30, 20, 10]
```

Important: `reverse()` does not sort the elements. It only reverses their existing order.

### reverse() vs sorted(reverse=True)

```python
numbers = [30, 10, 40, 20]

numbers.reverse()

print(numbers)
```

**Output:**
```text
[20, 40, 10, 30]
```

Now compare:

```python
numbers = [30, 10, 40, 20]

result = sorted(numbers, reverse=True)

print(result)
```

**Output:**
```text
[40, 30, 20, 10]
```

The first operation reverses the existing order. The second sorts the values in descending order.

---

## 13. copy() – Copying a List

The `copy()` method creates a shallow copy of a list.

A shallow copy creates a new outer list, but nested mutable objects are still shared.

### Example 1: Creating a Copy

```python
original = [10, 20, 30]

copied = original.copy()

copied.append(40)

print("Original:", original)
print("Copied:", copied)
```

**Output:**
```text
Original: [10, 20, 30]
Copied: [10, 20, 30, 40]
```

Changes to the copied outer list do not affect the original outer list.

### Example 2: Copying with Slicing

```python
original = [10, 20, 30]

copied = original[:]

print(copied)
```

**Output:**
```text
[10, 20, 30]
```

### Example 3: Reference vs Copy

```python
original = [10, 20, 30]

reference = original
copied = original.copy()

reference.append(40)
copied.append(50)

print("Original:", original)
print("Reference:", reference)
print("Copied:", copied)
```

**Output:**
```text
Original: [10, 20, 30, 40]
Reference: [10, 20, 30, 40]
Copied: [10, 20, 30, 50]
```

Explanation:

- `reference = original` does not create a new list. Both variables refer to the same list.
- `original.copy()` creates a separate outer list.

### Example 4: Understanding Shallow Copy

```python
original = [[10, 20], [30, 40]]

copied = original.copy()

copied[0].append(50)

print("Original:", original)
print("Copied:", copied)
```

**Output:**
```text
Original: [[10, 20, 50], [30, 40]]
Copied: [[10, 20, 50], [30, 40]]
```

Why did the original change?

Because `copy()` creates a new outer list, but both lists still refer to the same inner lists.

### Deep Copy Introduction

For independent copies of nested objects, Python provides `deepcopy()` from the `copy` module.

```python
import copy

original = [[10, 20], [30, 40]]

copied = copy.deepcopy(original)

copied[0].append(50)

print("Original:", original)
print("Copied:", copied)
```

**Output:**
```text
Original: [[10, 20], [30, 40]]
Copied: [[10, 20, 50], [30, 40]]
```

---

## 14. Useful Built-in Functions for Lists

Python provides built-in functions that work with lists.

### A. len()

Returns the number of elements.

```python
numbers = [10, 20, 30, 40]

print(len(numbers))
```

**Output:**
```text
4
```

### B. max()

Returns the largest element.

```python
numbers = [10, 50, 20, 90, 30]

print(max(numbers))
```

**Output:**
```text
90
```

### C. min()

Returns the smallest element.

```python
numbers = [10, 50, 20, 90, 30]

print(min(numbers))
```

**Output:**
```text
10
```

### D. sum()

Returns the sum of numeric elements.

```python
numbers = [10, 20, 30, 40]

print(sum(numbers))
```

**Output:**
```text
100
```

### E. any()

Returns `True` if at least one element is truthy.

```python
values = [0, False, 10, 0]

print(any(values))
```

**Output:**
```text
True
```

### F. all()

Returns `True` if every element is truthy. It also returns `True` for an empty iterable.

```python
values = [10, 20, 30]

print(all(values))
```

**Output:**
```text
True
```

Example with a false value:

```python
values = [10, 0, 30]

print(all(values))
```

**Output:**
```text
False
```

### G. enumerate()

Returns an iterator that provides each element along with its index.

```python
students = ["Raj", "Aman", "Rahul"]

for index, student in enumerate(students):
    print(index, student)
```

**Output:**
```text
0 Raj
1 Aman
2 Rahul
```

We can start counting from 1:

```python
students = ["Raj", "Aman", "Rahul"]

for index, student in enumerate(students, start=1):
    print(index, student)
```

**Output:**
```text
1 Raj
2 Aman
3 Rahul
```

---

## 15. Sorting Lists of Dictionaries

Lists can contain dictionaries. This is common when working with student records, employee data and API responses.

Example:

```python
students = [
    {"name": "Raj", "marks": 85},
    {"name": "Aman", "marks": 92},
    {"name": "Rahul", "marks": 78}
]
```

### Sort by Marks

```python
students.sort(key=lambda student: student["marks"])

for student in students:
    print(student)
```

**Output:**
```text
{'name': 'Rahul', 'marks': 78}
{'name': 'Raj', 'marks': 85}
{'name': 'Aman', 'marks': 92}
```

### Sort in Descending Order

```python
students.sort(key=lambda student: student["marks"], reverse=True)

for student in students:
    print(student)
```

**Output:**
```text
{'name': 'Aman', 'marks': 92}
{'name': 'Raj', 'marks': 85}
{'name': 'Rahul', 'marks': 78}
```

Here, `key` tells Python which value should be used for sorting.

The `lambda` expression will be explained in detail in a later lesson.

---

## 16. Common List Errors and Mistakes

### Mistake 1: Assigning append() Result

Incorrect:

```python
numbers = [10, 20]

numbers = numbers.append(30)

print(numbers)
```

Output:
```text
None
```

Correct:

```python
numbers = [10, 20]

numbers.append(30)

print(numbers)
```

### Mistake 2: Accessing an Invalid Index

```python
numbers = [10, 20, 30]

print(numbers[5])
```

Error:
```text
IndexError: list index out of range
```

### Mistake 3: Removing a Missing Element

```python
numbers = [10, 20, 30]

numbers.remove(50)
```

Error:
```text
ValueError: list.remove(x): x not in list
```

### Mistake 4: Sorting Different Incompatible Types

```python
data = [10, "Python", 20]

data.sort()
```

In Python 3, this raises a `TypeError` because integers and strings cannot be ordered against each other by default.

### Mistake 5: Modifying a List While Iterating

Avoid removing elements directly from a list while iterating over the same list. It can cause elements to be skipped.

Problematic example:

```python
numbers = [10, 20, 30, 40, 50]

for number in numbers:
    if number > 20:
        numbers.remove(number)

print(numbers)
```

A safer approach is to build a new list:

```python
numbers = [10, 20, 30, 40, 50]

filtered = []

for number in numbers:
    if number <= 20:
        filtered.append(number)

print(filtered)
```

**Output:**
```text
[10, 20]
```

---

# 17. Practical Programs

## Program 1: Sort Student Marks

```python
marks = [78, 92, 65, 88, 75]

marks.sort()

print("Ascending:", marks)

marks.sort(reverse=True)

print("Descending:", marks)
```

**Output:**
```text
Ascending: [65, 75, 78, 88, 92]
Descending: [92, 88, 78, 75, 65]
```

## Program 2: Count Duplicate Elements

```python
numbers = [10, 20, 10, 30, 20, 10, 40]

for number in numbers:
    if numbers.count(number) > 1:
        print(number, "appears", numbers.count(number), "times")
```

**Output:**
```text
10 appears 3 times
20 appears 2 times
10 appears 3 times
20 appears 2 times
10 appears 3 times
```

Notice that duplicate values are printed repeatedly. Improve this program so each repeated value is displayed only once.

## Program 3: Find Common Elements Between Two Lists

```python
list1 = [10, 20, 30, 40, 50]
list2 = [30, 40, 50, 60, 70]

common = []

for item in list1:
    if item in list2 and item not in common:
        common.append(item)

print("Common Elements:", common)
```

**Output:**
```text
Common Elements: [30, 40, 50]
```

## Program 4: Separate Positive and Negative Numbers

```python
numbers = [10, -5, 20, -15, 0, 30, -2]

positive = []
negative = []
zero = []

for number in numbers:

    if number > 0:
        positive.append(number)

    elif number < 0:
        negative.append(number)

    else:
        zero.append(number)

print("Positive:", positive)
print("Negative:", negative)
print("Zero:", zero)
```

**Output:**
```text
Positive: [10, 20, 30]
Negative: [-5, -15, -2]
Zero: [0]
```

## Program 5: Find the Second Largest Unique Number

```python
numbers = [10, 50, 30, 50, 40, 20]

unique_numbers = []

for number in numbers:
    if number not in unique_numbers:
        unique_numbers.append(number)

unique_numbers.sort(reverse=True)

if len(unique_numbers) >= 2:
    print("Second Largest:", unique_numbers[1])
else:
    print("Second Largest Number Does Not Exist")
```

**Output:**
```text
Second Largest: 40
```

## Program 6: Merge Two Lists and Remove Duplicates

```python
list1 = [10, 20, 30, 40]
list2 = [30, 40, 50, 60]

merged = list1.copy()
merged.extend(list2)

unique = []

for item in merged:
    if item not in unique:
        unique.append(item)

print("Merged List:", merged)
print("Unique List:", unique)
```

**Output:**
```text
Merged List: [10, 20, 30, 40, 30, 40, 50, 60]
Unique List: [10, 20, 30, 40, 50, 60]
```

---

# 18. Mini Project – Student Records Manager

## Project Description

Create a menu-driven Student Records Manager using a list of dictionaries.

Each student record should contain:

- Student name
- Roll number
- Marks

The application should support:

1. Add a student.
2. Display all students.
3. Search for a student by roll number.
4. Update student marks.
5. Delete a student.
6. Sort students by marks.
7. Display class statistics.
8. Exit the application.

## Complete Code

```python
students = []

while True:

    print("\n===== STUDENT RECORDS MANAGER =====")
    print("1. Add Student")
    print("2. Display Students")
    print("3. Search Student")
    print("4. Update Marks")
    print("5. Delete Student")
    print("6. Sort by Marks")
    print("7. Class Statistics")
    print("8. Exit")

    choice = input("Enter your choice: ")

    if choice == "1":

        name = input("Enter student name: ").strip()
        roll = input("Enter roll number: ").strip()

        if not name or not roll:
            print("Name and Roll Number are required.")
            continue

        if any(student["roll"] == roll for student in students):
            print("Roll Number Already Exists.")
            continue

        try:
            marks = float(input("Enter marks: "))

            if not 0 <= marks <= 100:
                print("Marks must be between 0 and 100.")
                continue

        except ValueError:
            print("Please Enter Valid Marks.")
            continue

        student = {
            "name": name,
            "roll": roll,
            "marks": marks
        }

        students.append(student)

        print("Student Added Successfully.")

    elif choice == "2":

        if not students:
            print("No Student Records Found.")

        else:
            print("\nStudent Records:")

            for student in students:
                print(
                    f"Name: {student['name']} | "
                    f"Roll: {student['roll']} | "
                    f"Marks: {student['marks']}"
                )

    elif choice == "3":

        roll = input("Enter Roll Number: ").strip()

        found = None

        for student in students:
            if student["roll"] == roll:
                found = student
                break

        if found:
            print("Student Found:")
            print(found)
        else:
            print("Student Not Found.")

    elif choice == "4":

        roll = input("Enter Roll Number: ").strip()

        found = None

        for student in students:
            if student["roll"] == roll:
                found = student
                break

        if found:

            try:
                new_marks = float(input("Enter New Marks: "))

                if 0 <= new_marks <= 100:
                    found["marks"] = new_marks
                    print("Marks Updated Successfully.")
                else:
                    print("Marks must be between 0 and 100.")

            except ValueError:
                print("Invalid Marks.")

        else:
            print("Student Not Found.")

    elif choice == "5":

        roll = input("Enter Roll Number: ").strip()

        found = None

        for student in students:
            if student["roll"] == roll:
                found = student
                break

        if found:
            students.remove(found)
            print("Student Deleted Successfully.")
        else:
            print("Student Not Found.")

    elif choice == "6":

        students.sort(
            key=lambda student: student["marks"],
            reverse=True
        )

        print("Students Sorted by Marks.")

        for student in students:
            print(student)

    elif choice == "7":

        if not students:
            print("No Records Available.")

        else:
            marks = [student["marks"] for student in students]

            print("Total Students:", len(students))
            print("Highest Marks:", max(marks))
            print("Lowest Marks:", min(marks))
            print("Average Marks:", round(sum(marks) / len(marks), 2))

    elif choice == "8":

        print("Thank You for Using Student Records Manager.")
        break

    else:
        print("Invalid Choice. Please Try Again.")
```

## Project Challenge

Improve the project by adding:

- Display students alphabetically by name.
- Show only students who scored above 75.
- Prevent duplicate student names if required by your rules.
- Display the highest-scoring student's name.
- Add a confirmation before deleting a student.
- Add an option to display the class ranking.

---

# 19. Student Practice Exercises

## Beginner Level

1. Create a list of 10 numbers and sort it in ascending order.
2. Sort a list of names alphabetically.
3. Reverse a list using `reverse()`.
4. Count how many times a number appears using `count()`.
5. Find the index of a specific element using `index()`.
6. Copy a list using `copy()`.
7. Remove all elements using `clear()`.
8. Add five elements using `extend()`.

## Intermediate Level

9. Find all duplicate elements in a list without printing duplicates repeatedly.
10. Find the second smallest unique number.
11. Merge two lists and remove duplicates.
12. Find common elements between three lists.
13. Separate even and odd numbers into different lists.
14. Sort a list of student names without changing the original list.
15. Find the frequency of every unique element.
16. Remove all occurrences of a specified value.
17. Find the difference between two lists.
18. Create a new list containing only values greater than the average.

## Advanced Level

19. Sort a list of dictionaries by marks.
20. Sort employee records by salary.
21. Create a nested student records list and calculate the class average.
22. Find the top three unique numbers from a list.
23. Create a program to compare two lists and display added, removed and common elements.
24. Create a menu-driven inventory manager with add, update, delete, search and sorting functionality.

---

# 20. Trainer Assessment

Ask the student to explain and demonstrate:

1. What is the difference between `append()` and `extend()`?
2. What is the difference between `remove()` and `pop()`?
3. What does `index()` return?
4. How does `count()` work?
5. What is the difference between `sort()` and `sorted()`?
6. What is the difference between `reverse()` and sorting in descending order?
7. What does `copy()` do?
8. What is the difference between a reference and a shallow copy?
9. What is a deep copy?
10. What are `any()` and `all()`?
11. How does `enumerate()` work?
12. Why should we avoid modifying a list while iterating over it?

## Practical Assessment

Ask the student to build a program that:

- Accepts multiple numbers from the user.
- Stores them in a list.
- Removes duplicate values.
- Sorts the numbers in ascending and descending order.
- Finds the largest and second-largest unique values.
- Counts the frequency of each unique number.
- Displays the sum and average.
- Does not modify the original list while generating sorted results.

## Completion Criteria

The lesson is complete when the student can:

- Use common list methods independently.
- Explain the difference between methods that modify a list and functions that return new lists.
- Sort and reverse lists correctly.
- Search and count elements.
- Understand references, shallow copies and deep copies.
- Work with lists of dictionaries.
- Complete the Student Records Manager.
- Solve the practical assessment without copying the solution.

**Trainer Note:** Pay special attention to `sort()` vs `sorted()`, `reverse()` vs descending sort, and reference vs shallow copy. These distinctions are frequently used in real Python development.

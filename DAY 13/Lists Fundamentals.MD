
# Day 13 – Lists Fundamentals

## 1. Introduction to Lists

A list is a built-in Python data structure used to store multiple values in a single variable.

Instead of creating separate variables for every value, we can store them together inside a list.

### Without a List

```python
student1 = "Raj"
student2 = "Aman"
student3 = "Rahul"
student4 = "Priya"
```

### With a List

```python
students = ["Raj", "Aman", "Rahul", "Priya"]

print(students)
```

**Output:**
```text
['Raj', 'Aman', 'Rahul', 'Priya']
```

### Important Characteristics of Lists

1. Lists are ordered.
2. Lists are mutable (their elements can be changed).
3. Lists allow duplicate values.
4. Lists can store different data types.
5. Lists are created using square brackets `[]`.

Example:

```python
data = [10, "Python", 25.5, True]

print(data)
```

**Output:**
```text
[10, 'Python', 25.5, True]
```

---

## 2. Creating Lists

There are different ways to create a list in Python.

### A. Creating a List Directly

```python
numbers = [10, 20, 30, 40, 50]

print(numbers)
```

### B. Creating an Empty List

```python
my_list = []

print(my_list)
```

**Output:**
```text
[]
```

An empty list can be populated later.

### C. Using the list() Constructor

Python provides a built-in `list()` constructor.

```python
numbers = list((10, 20, 30, 40))

print(numbers)
```

**Output:**
```text
[10, 20, 30, 40]
```

We can also convert a string into a list of characters:

```python
name = "Python"

characters = list(name)

print(characters)
```

**Output:**
```text
['P', 'y', 't', 'h', 'o', 'n']
```

---

## 3. Checking List Type and Length

### type()

The `type()` function tells us the data type of a variable.

```python
fruits = ["Apple", "Banana", "Mango"]

print(type(fruits))
```

**Output:**
```text
<class 'list'>
```

### len()

The `len()` function returns the total number of elements in a list.

```python
fruits = ["Apple", "Banana", "Mango", "Orange"]

print(len(fruits))
```

**Output:**
```text
4
```

Important: `len()` counts elements, not their individual characters.

---

## 4. Accessing List Elements – Indexing

Every element in a list has an index.

Python uses zero-based indexing, which means the first element starts at index `0`.

Example:

```python
fruits = ["Apple", "Banana", "Mango", "Orange"]

print(fruits[0])
print(fruits[1])
print(fruits[2])
print(fruits[3])
```

**Output:**
```text
Apple
Banana
Mango
Orange
```

### Visual Representation

| Element | Apple | Banana | Mango | Orange |
|---|---|---|---|---|
| Positive Index | 0 | 1 | 2 | 3 |
| Negative Index | -4 | -3 | -2 | -1 |

### Negative Indexing

Negative indexing allows us to access elements from the end of a list.

```python
fruits = ["Apple", "Banana", "Mango", "Orange"]

print(fruits[-1])
print(fruits[-2])
print(fruits[-3])
print(fruits[-4])
```

**Output:**
```text
Orange
Mango
Banana
Apple
```

### Important: IndexError

Accessing an index that does not exist produces an `IndexError`.

```python
numbers = [10, 20, 30]

print(numbers[5])
```

**Output:**
```text
IndexError: list index out of range
```

---

## 5. List Slicing

Slicing allows us to extract multiple elements from a list.

### Syntax

```python
list_name[start:stop:step]
```

- `start`: Index from where slicing begins.
- `stop`: Index where slicing stops (excluded).
- `step`: Number of positions to move.

### Example 1: Basic Slicing

```python
numbers = [10, 20, 30, 40, 50, 60]

print(numbers[1:4])
```

**Output:**
```text
[20, 30, 40]
```

The element at index `4` is excluded.

### Example 2: Starting from Index 0

```python
numbers = [10, 20, 30, 40, 50]

print(numbers[:3])
```

**Output:**
```text
[10, 20, 30]
```

### Example 3: Slicing Until the End

```python
numbers = [10, 20, 30, 40, 50]

print(numbers[2:])
```

**Output:**
```text
[30, 40, 50]
```

### Example 4: Using Step

```python
numbers = [10, 20, 30, 40, 50, 60]

print(numbers[::2])
```

**Output:**
```text
[10, 30, 50]
```

### Example 5: Reverse a List Using Slicing

```python
numbers = [10, 20, 30, 40, 50]

print(numbers[::-1])
```

**Output:**
```text
[50, 40, 30, 20, 10]
```

---

## 6. Updating List Elements

Lists are mutable, which means we can modify their elements after creating them.

Example:

```python
fruits = ["Apple", "Banana", "Mango"]

fruits[1] = "Orange"

print(fruits)
```

**Output:**
```text
['Apple', 'Orange', 'Mango']
```

We replaced the element at index `1`.

### Updating Multiple Elements Using Slicing

```python
numbers = [10, 20, 30, 40, 50]

numbers[1:3] = [200, 300]

print(numbers)
```

**Output:**
```text
[10, 200, 300, 40, 50]
```

---

## 7. Adding Elements to a List

Python provides different methods for adding elements.

### A. append()

The `append()` method adds one element at the end of a list.

```python
fruits = ["Apple", "Banana"]

fruits.append("Mango")

print(fruits)
```

**Output:**
```text
['Apple', 'Banana', 'Mango']
```

Important: `append()` adds its argument as a single element.

```python
numbers = [10, 20]

numbers.append([30, 40])

print(numbers)
```

**Output:**
```text
[10, 20, [30, 40]]
```

The nested list remains one element.

### B. insert()

The `insert()` method adds an element at a specific index.

Syntax:

```python
list_name.insert(index, element)
```

Example:

```python
fruits = ["Apple", "Mango"]

fruits.insert(1, "Banana")

print(fruits)
```

**Output:**
```text
['Apple', 'Banana', 'Mango']
```

### C. extend()

The `extend()` method adds multiple elements from another iterable to the end of a list.

```python
numbers = [10, 20]

numbers.extend([30, 40, 50])

print(numbers)
```

**Output:**
```text
[10, 20, 30, 40, 50]
```

### Difference Between append() and extend()

```python
list1 = [10, 20]
list1.append([30, 40])

list2 = [10, 20]
list2.extend([30, 40])

print(list1)
print(list2)
```

**Output:**
```text
[10, 20, [30, 40]]
[10, 20, 30, 40]
```

---

## 8. Removing Elements from a List

### A. remove()

Removes the first matching value from the list.

```python
fruits = ["Apple", "Banana", "Mango"]

fruits.remove("Banana")

print(fruits)
```

**Output:**
```text
['Apple', 'Mango']
```

If the value does not exist, Python raises a `ValueError`.

### B. pop()

Removes and returns an element.

```python
fruits = ["Apple", "Banana", "Mango"]

removed = fruits.pop()

print("Removed:", removed)
print("Updated List:", fruits)
```

**Output:**
```text
Removed: Mango
Updated List: ['Apple', 'Banana']
```

We can also specify an index:

```python
numbers = [10, 20, 30, 40]

removed = numbers.pop(1)

print(removed)
print(numbers)
```

**Output:**
```text
20
[10, 30, 40]
```

### C. del Statement

The `del` statement removes an element using its index.

```python
numbers = [10, 20, 30, 40]

del numbers[1]

print(numbers)
```

**Output:**
```text
[10, 30, 40]
```

It can also delete a slice:

```python
numbers = [10, 20, 30, 40, 50]

del numbers[1:3]

print(numbers)
```

**Output:**
```text
[10, 40, 50]
```

### D. clear()

Removes all elements from a list.

```python
fruits = ["Apple", "Banana", "Mango"]

fruits.clear()

print(fruits)
```

**Output:**
```text
[]
```

---

## 9. Membership Operators in Lists

Membership operators check whether an element exists in a list.

- `in`: Returns `True` if the element exists.
- `not in`: Returns `True` if the element does not exist.

Example:

```python
fruits = ["Apple", "Banana", "Mango"]

print("Apple" in fruits)
print("Orange" in fruits)

print("Orange" not in fruits)
```

**Output:**
```text
True
False
True
```

### Practical Example

```python
students = ["Raj", "Aman", "Rahul"]

name = input("Enter student name: ")

if name in students:
    print("Student Found")
else:
    print("Student Not Found")
```

---

## 10. Iterating Through a List

Iteration means accessing list elements one by one.

### A. Using a for Loop

```python
fruits = ["Apple", "Banana", "Mango"]

for fruit in fruits:
    print(fruit)
```

**Output:**
```text
Apple
Banana
Mango
```

### B. Using a for Loop with range()

```python
fruits = ["Apple", "Banana", "Mango"]

for i in range(len(fruits)):
    print(i, fruits[i])
```

**Output:**
```text
0 Apple
1 Banana
2 Mango
```

### C. Using a while Loop

```python
numbers = [10, 20, 30, 40]

i = 0

while i < len(numbers):
    print(numbers[i])
    i += 1
```

**Output:**
```text
10
20
30
40
```

---

## 11. List Concatenation and Repetition

### A. Concatenation (+)

The `+` operator combines two lists and creates a new list.

```python
list1 = [10, 20, 30]
list2 = [40, 50, 60]

result = list1 + list2

print(result)
```

**Output:**
```text
[10, 20, 30, 40, 50, 60]
```

### B. Repetition (*)

The `*` operator repeats the elements of a list.

```python
numbers = [1, 2, 3]

result = numbers * 3

print(result)
```

**Output:**
```text
[1, 2, 3, 1, 2, 3, 1, 2, 3]
```

---

## 12. Nested Lists

A nested list is a list that contains another list as an element.

Example:

```python
students = [
    ["Raj", 85],
    ["Aman", 90],
    ["Rahul", 78]
]

print(students)
```

**Output:**
```text
[['Raj', 85], ['Aman', 90], ['Rahul', 78]]
```

### Accessing Nested List Elements

```python
students = [
    ["Raj", 85],
    ["Aman", 90],
    ["Rahul", 78]
]

print(students[0])
print(students[0][0])
print(students[0][1])
```

**Output:**
```text
['Raj', 85]
Raj
85
```

The first index selects the inner list. The second index selects an element inside that inner list.

### Traversing a Nested List

```python
students = [
    ["Raj", 85],
    ["Aman", 90],
    ["Rahul", 78]
]

for student in students:
    print("Name:", student[0])
    print("Marks:", student[1])
```

**Output:**
```text
Name: Raj
Marks: 85
Name: Aman
Marks: 90
Name: Rahul
Marks: 78
```

---

# 13. Practical Programs

## Program 1: Find the Sum of List Elements

```python
numbers = [10, 20, 30, 40, 50]

total = 0

for number in numbers:
    total += number

print("Sum:", total)
```

**Output:**
```text
Sum: 150
```

## Program 2: Find the Largest Number

```python
numbers = [45, 12, 89, 34, 67]

largest = numbers[0]

for number in numbers:
    if number > largest:
        largest = number

print("Largest Number:", largest)
```

**Output:**
```text
Largest Number: 89
```

## Program 3: Find the Smallest Number

```python
numbers = [45, 12, 89, 34, 67]

smallest = numbers[0]

for number in numbers:
    if number < smallest:
        smallest = number

print("Smallest Number:", smallest)
```

**Output:**
```text
Smallest Number: 12
```

## Program 4: Count Even and Odd Numbers

```python
numbers = [10, 15, 20, 25, 30, 35]

even_count = 0
odd_count = 0

for number in numbers:
    if number % 2 == 0:
        even_count += 1
    else:
        odd_count += 1

print("Even Numbers:", even_count)
print("Odd Numbers:", odd_count)
```

**Output:**
```text
Even Numbers: 3
Odd Numbers: 3
```

## Program 5: Search an Element in a List

```python
numbers = [10, 20, 30, 40, 50]

search = int(input("Enter number to search: "))

if search in numbers:
    print("Number Found")
else:
    print("Number Not Found")
```

**Sample Output:**
```text
Enter number to search: 30
Number Found
```

## Program 6: Remove Duplicate Values

```python
numbers = [10, 20, 10, 30, 20, 40]

unique_numbers = []

for number in numbers:
    if number not in unique_numbers:
        unique_numbers.append(number)

print("Original List:", numbers)
print("Unique List:", unique_numbers)
```

**Output:**
```text
Original List: [10, 20, 10, 30, 20, 40]
Unique List: [10, 20, 30, 40]
```

This program preserves the original order of the first occurrence of each value.

## Program 7: Calculate Average Marks

```python
marks = [85, 90, 78, 88, 95]

total = 0

for mark in marks:
    total += mark

average = total / len(marks)

print("Total Marks:", total)
print("Average Marks:", average)
```

**Output:**
```text
Total Marks: 436
Average Marks: 87.2
```

## Program 8: Reverse a List Without Using Slicing

```python
numbers = [10, 20, 30, 40, 50]

reversed_list = []

for i in range(len(numbers) - 1, -1, -1):
    reversed_list.append(numbers[i])

print("Reversed List:", reversed_list)
```

**Output:**
```text
Reversed List: [50, 40, 30, 20, 10]
```

---

# 14. Mini Project – Shopping List Manager

## Project Description

Create a simple Shopping List Manager using Python lists.

The program should allow users to:

1. View all shopping items.
2. Add a new item.
3. Remove an existing item.
4. Search for an item.
5. Count total items.
6. Exit the program.

### Complete Code

```python
shopping_list = []

while True:

    print("\n===== SHOPPING LIST MANAGER =====")
    print("1. View Shopping List")
    print("2. Add Item")
    print("3. Remove Item")
    print("4. Search Item")
    print("5. Count Items")
    print("6. Exit")

    choice = input("Enter your choice: ")

    if choice == "1":

        if len(shopping_list) == 0:
            print("Shopping List is Empty")
        else:
            print("\nYour Shopping List:")

            for index, item in enumerate(shopping_list, start=1):
                print(f"{index}. {item}")

    elif choice == "2":

        item = input("Enter item name: ").strip()

        if item:
            shopping_list.append(item)
            print("Item Added Successfully")
        else:
            print("Item Name Cannot Be Empty")

    elif choice == "3":

        item = input("Enter item to remove: ").strip()

        if item in shopping_list:
            shopping_list.remove(item)
            print("Item Removed Successfully")
        else:
            print("Item Not Found")

    elif choice == "4":

        item = input("Enter item to search: ").strip()

        if item in shopping_list:
            print("Item Found")
        else:
            print("Item Not Found")

    elif choice == "5":

        print("Total Items:", len(shopping_list))

    elif choice == "6":

        print("Thank You for Using Shopping List Manager!")
        break

    else:
        print("Invalid Choice. Please Try Again.")
```

### Sample Output

```text
===== SHOPPING LIST MANAGER =====
1. View Shopping List
2. Add Item
3. Remove Item
4. Search Item
5. Count Items
6. Exit

Enter your choice: 2
Enter item name: Milk
Item Added Successfully

Enter your choice: 2
Enter item name: Bread
Item Added Successfully

Enter your choice: 1

Your Shopping List:
1. Milk
2. Bread

Enter your choice: 5
Total Items: 2
```

### Project Challenge

After completing the basic project, try adding these features:

- Prevent duplicate items.
- Add an option to clear the entire shopping list.
- Display a message when the list contains more than 10 items.
- Allow the user to update an existing item.
- Display the shopping list in alphabetical order.

---

# 15. Student Practice Exercises

Complete these exercises independently.

### Beginner Level

1. Create a list containing five student names.
2. Print the first and last elements.
3. Print the total number of elements.
4. Create a list containing numbers from 1 to 10.
5. Print the list in reverse order using slicing.
6. Change the second element of a list.
7. Add three new elements using `append()`.
8. Insert an element at index 2.

### Intermediate Level

9. Remove a particular value using `remove()`.
10. Remove the last element using `pop()`.
11. Find the sum of all numbers in a list.
12. Find the average of all numbers.
13. Count how many even and odd numbers exist.
14. Find the largest and smallest elements without using `max()` and `min()`.
15. Search for a given element using membership operators.
16. Remove duplicate values while preserving order.
17. Combine two lists into one.
18. Find the common elements between two lists.

### Advanced Practice

19. Create a nested list containing student names and marks.
20. Calculate the average marks of all students.
21. Find the student who scored the highest marks.
22. Create a program that separates positive and negative numbers into two lists.
23. Create a list containing numbers from 1 to 20 and generate a new list containing only multiples of 3.
24. Create a menu-driven program to manage a list of employee names.

---

# 16. Trainer Assessment

Ask the student to explain and demonstrate the following:

1. What is a list in Python?
2. What is the difference between a list and a variable?
3. Why are lists called mutable?
4. What is the difference between positive and negative indexing?
5. Explain list slicing with an example.
6. What is the difference between `append()` and `extend()`?
7. What is the difference between `remove()` and `pop()`?
8. What happens when we access an invalid index?
9. How can we iterate through a list?
10. What is a nested list?

### Practical Assessment

Ask the student to create a program that:

- Accepts five numbers from the user.
- Stores them in a list.
- Displays the complete list.
- Calculates the sum and average.
- Finds the largest and smallest numbers.
- Counts even and odd numbers.

### Completion Criteria

The lesson is complete when the student can:

- Create and access lists independently.
- Perform indexing and slicing correctly.
- Update, add and remove elements.
- Iterate through lists using loops.
- Work with nested lists.
- Complete the practical assessment without copying the solution.
- Build and demonstrate the Shopping List Manager.

**Trainer Note:** Make sure the student understands indexing, slicing, mutability and the difference between `append()` and `extend()`. These concepts are especially important before moving to list methods and operations.

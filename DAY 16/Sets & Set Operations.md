
# Day 16 – Sets & Set Operations

## 1. Introduction to Sets

A set is a built-in Python data structure used to store multiple unique elements in a single variable.

Unlike lists and tuples, sets do not allow duplicate elements.

### Example

```python
numbers = {10, 20, 30, 40, 50}

print(numbers)
```

**Output:**
```text
{10, 20, 30, 40, 50}
```

### Important Characteristics of Sets

1. Sets contain unique elements.
2. Sets are mutable.
3. Sets are unordered collections.
4. Sets do not support indexing or slicing.
5. Sets can store elements of different hashable data types.
6. Sets are created using curly braces `{}` or the `set()` constructor.
7. Sets automatically eliminate duplicate values.

### Example: Duplicate Values

```python
numbers = {10, 20, 10, 30, 20, 40}

print(numbers)
```

**Output:**
```text
{10, 20, 30, 40}
```

Duplicate elements are automatically removed.

**Important:** Sets are unordered. Do not depend on the order in which elements appear when printing or iterating over a set.

---

## 2. Creating Sets

### A. Creating a Set Directly

```python
fruits = {"Apple", "Banana", "Mango"}

print(fruits)
print(type(fruits))
```

**Output:**
```text
{'Apple', 'Banana', 'Mango'}
<class 'set'>
```

The displayed order may vary.

### B. Creating an Empty Set

To create an empty set, use `set()`.

```python
my_set = set()

print(my_set)
print(type(my_set))
```

**Output:**
```text
set()
<class 'set'>
```

### Important: Empty Set vs Empty Dictionary

Using `{}` creates an empty dictionary, not an empty set.

```python
data = {}

print(type(data))
```

**Output:**
```text
<class 'dict'>
```

Comparison:

```python
empty_set = set()
empty_dict = {}

print(type(empty_set))
print(type(empty_dict))
```

**Output:**
```text
<class 'set'>
<class 'dict'>
```

### C. Creating a Set Using the Constructor

```python
numbers = set([10, 20, 30, 20, 40])

print(numbers)
```

**Output:**
```text
{10, 20, 30, 40}
```

### D. Creating a Set from a String

```python
characters = set("Python")

print(characters)
```

**Possible Output:**
```text
{'P', 'y', 't', 'h', 'o', 'n'}
```

A set stores each unique character only once. Its order is not guaranteed.

---

## 3. Set Elements and Hashability

Set elements must be hashable.

Common hashable types include:

- Integers
- Floats
- Strings
- Booleans
- Tuples containing only hashable elements

Mutable collections such as lists, dictionaries and sets cannot be stored directly as set elements.

### Valid Example

```python
data = {10, 20.5, "Python", True}

print(data)
```

### Invalid Example

```python
data = {[10, 20], [30, 40]}

print(data)
```

**Output:**
```text
TypeError: unhashable type: 'list'
```

### Tuple as a Set Element

```python
data = {(10, 20), (30, 40)}

print(data)
```

**Output:**
```text
{(10, 20), (30, 40)}
```

A tuple is usable as a set element only if all its elements are hashable.

---

## 4. Checking Set Length and Type

### type()

```python
numbers = {10, 20, 30}

print(type(numbers))
```

**Output:**
```text
<class 'set'>
```

### len()

```python
numbers = {10, 20, 30, 40}

print(len(numbers))
```

**Output:**
```text
4
```

The `len()` function returns the number of unique elements.

---

## 5. Accessing Set Elements

Sets do not support indexing because they are unordered.

Incorrect:

```python
numbers = {10, 20, 30}

print(numbers[0])
```

**Output:**
```text
TypeError: 'set' object is not subscriptable
```

### Accessing Elements Using a for Loop

```python
fruits = {"Apple", "Banana", "Mango"}

for fruit in fruits:
    print(fruit)
```

**Possible Output:**
```text
Apple
Mango
Banana
```

The order may vary.

### Converting a Set into a List

If indexing is required, convert the set into a list.

```python
numbers = {10, 20, 30}

number_list = list(numbers)

print(number_list[0])
```

The exact element at index `0` is not guaranteed because the original set has no defined positional order.

---

## 6. Adding Elements to a Set

Python provides two commonly used methods for adding elements.

### A. add()

The `add()` method adds one element to a set.

**Syntax:**

```python
set_name.add(element)
```

Example:

```python
fruits = {"Apple", "Banana"}

fruits.add("Mango")

print(fruits)
```

**Output contains:**
```text
{'Apple', 'Banana', 'Mango'}
```

The order may vary.

### Adding an Existing Element

```python
numbers = {10, 20, 30}

numbers.add(20)

print(numbers)
```

**Output contains:**
```text
{10, 20, 30}
```

Adding a duplicate does not change the set.

### B. update()

The `update()` method adds multiple elements from one or more iterables.

```python
numbers = {10, 20}

numbers.update([30, 40, 50])

print(numbers)
```

**Output contains:**
```text
{10, 20, 30, 40, 50}
```

### Updating with Multiple Iterables

```python
numbers = {10, 20}

numbers.update([30, 40], (50, 60), {70, 80})

print(numbers)
```

**Output contains:**
```text
{10, 20, 30, 40, 50, 60, 70, 80}
```

### Difference Between add() and update()

| add() | update() |
|---|---|
| Adds one element | Adds elements from iterables |
| Takes one element | Accepts one or more iterables |
| `add([10, 20])` raises TypeError | `update([10, 20])` adds 10 and 20 |

---

## 7. Removing Elements from a Set

Python provides multiple methods for removing set elements.

### A. remove()

Removes a specified element.

```python
fruits = {"Apple", "Banana", "Mango"}

fruits.remove("Banana")

print(fruits)
```

**Output contains:**
```text
{'Apple', 'Mango'}
```

If the element does not exist, `remove()` raises a `KeyError`.

```python
numbers = {10, 20, 30}

numbers.remove(50)
```

**Output:**
```text
KeyError: 50
```

### B. discard()

Removes a specified element if it exists.

```python
numbers = {10, 20, 30}

numbers.discard(20)

print(numbers)
```

**Output contains:**
```text
{10, 30}
```

If the element does not exist, `discard()` does not raise an error.

```python
numbers = {10, 20, 30}

numbers.discard(50)

print(numbers)
```

**Output contains:**
```text
{10, 20, 30}
```

### Difference Between remove() and discard()

| remove() | discard() |
|---|---|
| Removes an existing element | Removes an existing element |
| Raises KeyError if missing | Does not raise an error if missing |

### C. pop()

Removes and returns an arbitrary element.

```python
numbers = {10, 20, 30, 40}

removed = numbers.pop()

print("Removed:", removed)
print("Remaining:", numbers)
```

**Output:** The removed value can be any element of the set.

Do not assume `pop()` removes the smallest, first or last element.

If the set is empty, `pop()` raises a `KeyError`.

### D. clear()

Removes all elements.

```python
fruits = {"Apple", "Banana", "Mango"}

fruits.clear()

print(fruits)
```

**Output:**
```text
set()
```

---

## 8. Membership Operators in Sets

Membership operators check whether an element exists in a set.

- `in`: Checks whether an element exists.
- `not in`: Checks whether an element does not exist.

Example:

```python
fruits = {"Apple", "Banana", "Mango"}

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

Set membership checks are generally very efficient.

---

## 9. Set Union

Union combines all unique elements from two or more sets.

The union operator is `|`.

### Example

```python
set1 = {10, 20, 30}
set2 = {30, 40, 50}

result = set1 | set2

print(result)
```

**Output contains:**
```text
{10, 20, 30, 40, 50}
```

The duplicate value `30` appears only once.

### Using union()

```python
set1 = {10, 20, 30}
set2 = {30, 40, 50}

result = set1.union(set2)

print(result)
```

**Output contains:**
```text
{10, 20, 30, 40, 50}
```

### Union of Multiple Sets

```python
set1 = {1, 2}
set2 = {2, 3}
set3 = {3, 4}

result = set1.union(set2, set3)

print(result)
```

**Output contains:**
```text
{1, 2, 3, 4}
```

---

## 10. Set Intersection

Intersection returns only the elements common to both sets.

The intersection operator is `&`.

### Example

```python
set1 = {10, 20, 30, 40}
set2 = {30, 40, 50, 60}

result = set1 & set2

print(result)
```

**Output contains:**
```text
{30, 40}
```

### Using intersection()

```python
set1 = {10, 20, 30}
set2 = {20, 30, 40}

result = set1.intersection(set2)

print(result)
```

**Output contains:**
```text
{20, 30}
```

### Intersection of Multiple Sets

```python
set1 = {1, 2, 3, 4}
set2 = {2, 3, 4, 5}
set3 = {3, 4, 5, 6}

result = set1.intersection(set2, set3)

print(result)
```

**Output:**
```text
{3, 4}
```

---

## 11. Set Difference

Difference returns elements that exist in the first set but not in the second set.

The difference operator is `-`.

### Example

```python
set1 = {10, 20, 30, 40}
set2 = {30, 40, 50, 60}

result = set1 - set2

print(result)
```

**Output contains:**
```text
{10, 20}
```

### Reverse Difference

```python
set1 = {10, 20, 30, 40}
set2 = {30, 40, 50, 60}

result = set2 - set1

print(result)
```

**Output contains:**
```text
{50, 60}
```

The order of the operands matters.

### Using difference()

```python
set1 = {10, 20, 30}
set2 = {20, 30, 40}

result = set1.difference(set2)

print(result)
```

**Output contains:**
```text
{10}
```

---

## 12. Symmetric Difference

Symmetric difference returns elements that exist in either set but not in both.

The symmetric difference operator is `^`.

### Example

```python
set1 = {10, 20, 30, 40}
set2 = {30, 40, 50, 60}

result = set1 ^ set2

print(result)
```

**Output contains:**
```text
{10, 20, 50, 60}
```

Common elements `30` and `40` are excluded.

### Using symmetric_difference()

```python
set1 = {10, 20, 30}
set2 = {20, 30, 40}

result = set1.symmetric_difference(set2)

print(result)
```

**Output contains:**
```text
{10, 40}
```

---

## 13. Visual Understanding of Set Operations

Consider two sets:

```python
A = {1, 2, 3, 4}
B = {3, 4, 5, 6}
```

| Operation | Result |
|---|---|
| Union `A \| B` | `{1, 2, 3, 4, 5, 6}` |
| Intersection `A & B` | `{3, 4}` |
| Difference `A - B` | `{1, 2}` |
| Difference `B - A` | `{5, 6}` |
| Symmetric Difference `A ^ B` | `{1, 2, 5, 6}` |

### Venn Diagram Concept

- Union: Everything inside both circles.
- Intersection: Only the overlapping region.
- Difference: Elements in one circle but not the other.
- Symmetric Difference: Both non-overlapping regions.

---

## 14. Set Comparison Methods

Python provides methods to compare relationships between sets.

### A. issubset()

Checks whether all elements of one set exist in another set.

```python
A = {1, 2}
B = {1, 2, 3, 4}

print(A.issubset(B))
```

**Output:**
```text
True
```

The operator `<=` can also check subset relationships.

```python
print(A <= B)
```

**Output:**
```text
True
```

### B. issuperset()

Checks whether a set contains all elements of another set.

```python
A = {1, 2, 3, 4}
B = {1, 2}

print(A.issuperset(B))
```

**Output:**
```text
True
```

The operator `>=` can also check superset relationships.

### C. isdisjoint()

Checks whether two sets have no common elements.

```python
A = {1, 2, 3}
B = {4, 5, 6}

print(A.isdisjoint(B))
```

**Output:**
```text
True
```

If the sets share even one element, the result is `False`.

### Summary

| Method | Meaning |
|---|---|
| `issubset()` | Checks whether a set is a subset |
| `issuperset()` | Checks whether a set is a superset |
| `isdisjoint()` | Checks whether two sets have no common elements |

---

## 15. Update Set Operations

The following methods modify the original set instead of returning a separate result.

### A. update()

Adds all unique elements from other iterables.

```python
A = {1, 2, 3}
B = {3, 4, 5}

A.update(B)

print(A)
```

**Output contains:**
```text
{1, 2, 3, 4, 5}
```

### B. intersection_update()

Keeps only common elements.

```python
A = {1, 2, 3, 4}
B = {3, 4, 5}

A.intersection_update(B)

print(A)
```

**Output contains:**
```text
{3, 4}
```

### C. difference_update()

Removes elements that exist in another set.

```python
A = {1, 2, 3, 4}
B = {3, 4, 5}

A.difference_update(B)

print(A)
```

**Output contains:**
```text
{1, 2}
```

### D. symmetric_difference_update()

Keeps only elements that are not common between the sets.

```python
A = {1, 2, 3, 4}
B = {3, 4, 5, 6}

A.symmetric_difference_update(B)

print(A)
```

**Output contains:**
```text
{1, 2, 5, 6}
```

### Important Difference

| Method | Returns a New Set | Modifies Original Set |
|---|---|---|
| `union()` | Yes | No |
| `intersection()` | Yes | No |
| `difference()` | Yes | No |
| `symmetric_difference()` | Yes | No |
| `update()` | No | Yes |
| `intersection_update()` | No | Yes |
| `difference_update()` | No | Yes |
| `symmetric_difference_update()` | No | Yes |

---

## 16. Copying Sets

The `copy()` method creates a shallow copy of a set.

```python
original = {10, 20, 30}

copied = original.copy()

copied.add(40)

print("Original:", original)
print("Copied:", copied)
```

**Output contains:**
```text
Original: {10, 20, 30}
Copied: {10, 20, 30, 40}
```

The copied set is a separate set.

Because set elements must be hashable, sets cannot directly contain mutable lists, dictionaries or sets. A shallow copy is therefore sufficient for many ordinary set use cases.

---

## 17. Frozenset – Immutable Sets

A `frozenset` is an immutable version of a set.

Once created, its elements cannot be added or removed.

### Creating a Frozenset

```python
numbers = frozenset([10, 20, 30, 40])

print(numbers)
print(type(numbers))
```

**Output contains:**
```text
frozenset({10, 20, 30, 40})
<class 'frozenset'>
```

### Trying to Add an Element

```python
numbers = frozenset([10, 20, 30])

numbers.add(40)
```

**Output:**
```text
AttributeError: 'frozenset' object has no attribute 'add'
```

### Trying to Remove an Element

```python
numbers = frozenset([10, 20, 30])

numbers.remove(20)
```

**Output:**
```text
AttributeError: 'frozenset' object has no attribute 'remove'
```

### Supported Operations

Frozensets support:

- Union
- Intersection
- Difference
- Symmetric difference
- Subset and superset comparisons
- Membership checks
- Iteration

Example:

```python
A = frozenset([1, 2, 3])
B = frozenset([3, 4, 5])

print(A | B)
print(A & B)
print(A - B)
```

**Output contains:**
```text
frozenset({1, 2, 3, 4, 5})
frozenset({3})
frozenset({1, 2})
```

### Frozenset as a Dictionary Key

Because a frozenset is immutable and hashable, it can be used as a dictionary key.

```python
permissions = {
    frozenset(["read", "write"]): "Editor"
}

print(permissions[frozenset(["write", "read"])])
```

**Output:**
```text
Editor
```

---

## 18. Removing Duplicates from a List Using Sets

Sets are commonly used to remove duplicate values from a list.

### Example

```python
numbers = [10, 20, 10, 30, 20, 40]

unique_numbers = list(set(numbers))

print(unique_numbers)
```

**Output contains:**
```text
[10, 20, 30, 40]
```

Important: The order is not guaranteed.

### Preserving the Original Order

If the original order must be preserved, use a separate list and set.

```python
numbers = [10, 20, 10, 30, 20, 40]

seen = set()
unique_numbers = []

for number in numbers:

    if number not in seen:
        seen.add(number)
        unique_numbers.append(number)

print(unique_numbers)
```

**Output:**
```text
[10, 20, 30, 40]
```

The set is used for efficient membership checks, while the list preserves the original order.

---

## 19. Practical Programs

### Program 1: Find Common Subjects Between Two Students

```python
student1 = {"Python", "Java", "SQL", "HTML"}
student2 = {"Python", "JavaScript", "SQL", "CSS"}

common = student1.intersection(student2)

print("Common Subjects:", common)
```

**Output contains:**
```text
{'Python', 'SQL'}
```

### Program 2: Find Unique Subjects

```python
student1 = {"Python", "Java", "SQL"}
student2 = {"Python", "JavaScript", "CSS"}

unique = student1.symmetric_difference(student2)

print("Unique Subjects:", unique)
```

**Output contains:**
```text
{'Java', 'SQL', 'JavaScript', 'CSS'}
```

### Program 3: Find Students Enrolled in Either Course

```python
python_students = {"Raj", "Aman", "Rahul"}
java_students = {"Aman", "Priya", "Neha"}

all_students = python_students.union(java_students)

print("All Students:", all_students)
print("Total Students:", len(all_students))
```

**Output contains:**
```text
All Students: {'Raj', 'Aman', 'Rahul', 'Priya', 'Neha'}
Total Students: 5
```

### Program 4: Find Students Enrolled in Both Courses

```python
python_students = {"Raj", "Aman", "Rahul"}
java_students = {"Aman", "Priya", "Rahul"}

common_students = python_students & java_students

print("Students Enrolled in Both:", common_students)
```

**Output contains:**
```text
{'Aman', 'Rahul'}
```

### Program 5: Find Students Enrolled Only in Python

```python
python_students = {"Raj", "Aman", "Rahul"}
java_students = {"Aman", "Priya", "Rahul"}

only_python = python_students - java_students

print("Only Python:", only_python)
```

**Output contains:**
```text
{'Raj'}
```

### Program 6: Check Whether a User Has Required Permissions

```python
required_permissions = {"read", "write"}

user_permissions = {"read", "write", "delete"}

if required_permissions.issubset(user_permissions):
    print("Access Granted")
else:
    print("Access Denied")
```

**Output:**
```text
Access Granted
```

### Program 7: Find Unique Characters in a Word

```python
word = input("Enter a word: ")

unique_characters = set(word)

print("Unique Characters:", unique_characters)
print("Total Unique Characters:", len(unique_characters))
```

**Sample Output:**
```text
Enter a word: programming
Total Unique Characters: 8
```

The displayed set order may vary.

### Program 8: Find Duplicate Numbers Between Two Lists

```python
list1 = [10, 20, 30, 40, 50]
list2 = [30, 40, 50, 60, 70]

duplicates = set(list1) & set(list2)

print("Duplicate Values:", duplicates)
```

**Output contains:**
```text
{30, 40, 50}
```

---

# 20. Mini Project – Course Enrollment Management System

## Project Description

Create a Course Enrollment Management System using Python sets.

The system should manage students enrolled in different courses.

Available courses:

- Python
- Java
- Web Development

Each course should maintain a set of enrolled student names.

### Application Features

1. Enroll a student in a course.
2. Remove a student from a course.
3. Display all students in a course.
4. Find students enrolled in multiple courses.
5. Find students enrolled in only one course.
6. Display all registered students.
7. Search for a student.
8. Exit the application.

## Complete Code

```python
courses = {
    "python": set(),
    "java": set(),
    "web": set()
}

while True:

    print("\n===== COURSE ENROLLMENT SYSTEM =====")
    print("1. Enroll Student")
    print("2. Remove Student")
    print("3. Display Course Students")
    print("4. Find Common Students")
    print("5. Find Students in Only One Course")
    print("6. Display All Students")
    print("7. Search Student")
    print("8. Exit")

    choice = input("Enter your choice: ")

    if choice == "1":

        name = input("Enter Student Name: ").strip()
        course = input("Enter Course (Python/Java/Web): ").strip().lower()

        if not name:
            print("Student Name Cannot Be Empty.")

        elif course in courses:

            if name in courses[course]:
                print("Student Already Enrolled.")

            else:
                courses[course].add(name)
                print("Student Enrolled Successfully.")

        else:
            print("Invalid Course.")

    elif choice == "2":

        name = input("Enter Student Name: ").strip()
        course = input("Enter Course: ").strip().lower()

        if course in courses:

            if name in courses[course]:
                courses[course].remove(name)
                print("Enrollment Removed Successfully.")

            else:
                print("Student Not Found in This Course.")

        else:
            print("Invalid Course.")

    elif choice == "3":

        course = input("Enter Course: ").strip().lower()

        if course in courses:

            print("\nStudents in", course.upper())

            if courses[course]:
                for student in sorted(courses[course]):
                    print(student)

            else:
                print("No Students Enrolled.")

        else:
            print("Invalid Course.")

    elif choice == "4":

        python_students = courses["python"]
        java_students = courses["java"]
        web_students = courses["web"]

        common = python_students & java_students & web_students

        print("Students Enrolled in All Three Courses:", common)

    elif choice == "5":

        all_students = (
            courses["python"]
            | courses["java"]
            | courses["web"]
        )

        multiple_courses = set()

        for student in all_students:

            enrolled_count = 0

            for course_students in courses.values():

                if student in course_students:
                    enrolled_count += 1

            if enrolled_count > 1:
                multiple_courses.add(student)

        only_one_course = all_students - multiple_courses

        print("Students Enrolled in Only One Course:", only_one_course)

    elif choice == "6":

        all_students = (
            courses["python"]
            | courses["java"]
            | courses["web"]
        )

        print("All Registered Students:")

        if all_students:

            for student in sorted(all_students):
                print(student)

        else:
            print("No Students Registered.")

    elif choice == "7":

        name = input("Enter Student Name: ").strip()

        enrolled_courses = []

        for course, students in courses.items():

            if name in students:
                enrolled_courses.append(course)

        if enrolled_courses:
            print("Student Found.")
            print("Enrolled Courses:", enrolled_courses)

        else:
            print("Student Not Found.")

    elif choice == "8":

        print("Thank You for Using Course Enrollment System.")
        break

    else:
        print("Invalid Choice. Please Try Again.")
```

## Project Challenge

Improve the project by adding:

- A total enrollment count for each course.
- A feature to display students alphabetically.
- A feature to transfer a student between courses.
- A feature to display students enrolled in exactly two courses.
- A feature to show the most popular course.
- A feature to clear all enrollments after confirmation.

---

# 21. Student Practice Exercises

## Beginner Level

1. Create a set containing five numbers.
2. Create an empty set using `set()`.
3. Create a set from a list containing duplicate values.
4. Add an element using `add()`.
5. Add multiple elements using `update()`.
6. Remove an element using `remove()`.
7. Remove an element using `discard()`.
8. Check whether a value exists using `in`.

## Intermediate Level

9. Find the union of two sets.
10. Find the intersection of two sets.
11. Find the difference between two sets.
12. Find the symmetric difference.
13. Check whether one set is a subset of another.
14. Check whether two sets are disjoint.
15. Remove duplicate values from a list using a set.
16. Remove duplicates while preserving the original order.
17. Find common subjects between two students.
18. Find students enrolled in only one of two courses.

## Advanced Level

19. Create a frozenset and demonstrate its immutability.
20. Use a frozenset as a dictionary key.
21. Create a program to find common elements among three lists.
22. Build a student enrollment management system.
23. Find elements present in exactly two out of three sets.
24. Create a program to compare two user permission sets and identify missing permissions.

---

# 22. Trainer Assessment

Ask the student to explain and demonstrate:

1. What is a set in Python?
2. Why are sets called unordered collections?
3. Why can't we use indexing with sets?
4. What is the difference between `{}` and `set()`?
5. What is the difference between `add()` and `update()`?
6. What is the difference between `remove()` and `discard()`?
7. Explain union and intersection.
8. Explain difference and symmetric difference.
9. What is the difference between `issubset()` and `issuperset()`?
10. What does `isdisjoint()` check?
11. What is a frozenset?
12. Why are mutable objects not allowed as set elements?
13. How can we remove duplicates from a list while preserving order?

## Practical Assessment

Ask the student to create a program that:

- Accepts two lists of numbers from the user.
- Converts both lists into sets.
- Displays the union.
- Displays the intersection.
- Displays the difference in both directions.
- Displays the symmetric difference.
- Displays the total number of unique elements.
- Checks whether the two sets are disjoint.

## Completion Criteria

The lesson is complete when the student can:

- Create and manipulate sets.
- Add and remove elements correctly.
- Explain set uniqueness and unordered behavior.
- Perform union, intersection, difference and symmetric difference.
- Compare sets using subset, superset and disjoint checks.
- Understand mutable sets and immutable frozensets.
- Remove duplicates from lists while preserving order.
- Complete the Course Enrollment Management System.
- Solve the practical assessment independently.

**Trainer Note:** Focus on the four fundamental set operations and the distinction between `remove()` and `discard()`. Also make sure the student understands that sets do not guarantee positional order.

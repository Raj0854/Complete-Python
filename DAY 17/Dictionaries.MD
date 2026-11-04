
# Day 17 – Python Dictionaries

## 1. Introduction to Dictionaries

A dictionary is a built-in Python collection used to store data in **key-value pairs**.

Each item in a dictionary contains:
- **Key:** Identifies an item.
- **Value:** Stores the actual information associated with that key.

### Example

```python
student = {
    "name": "Raj",
    "age": 21,
    "course": "Python",
    "marks": 85
}

print(student)
```

**Output:**
```text
{'name': 'Raj', 'age': 21, 'course': 'Python', 'marks': 85}
```

Here:
- `"name"` is a key.
- `"Raj"` is its value.
- `"age"` is a key.
- `21` is its value.

### Important Characteristics

1. Dictionaries store data in key-value pairs.
2. Dictionaries are mutable (changeable).
3. Dictionary keys must be unique.
4. Values can be duplicated.
5. Dictionaries preserve insertion order (guaranteed in Python 3.7+).
6. Keys must be hashable.
7. Values can be of any data type.
8. Dictionary items are accessed using keys, not positional indexes.

---

## 2. Creating Dictionaries

### Example 1: Creating a Dictionary

```python
student = {
    "name": "Rahul",
    "age": 22,
    "marks": 90
}

print(student)
```

**Output:**
```text
{'name': 'Rahul', 'age': 22, 'marks': 90}
```

### Example 2: Creating an Empty Dictionary

```python
student = {}

print(student)
print(type(student))
```

**Output:**
```text
{}
<class 'dict'>
```

You can also use the `dict()` constructor:

```python
student = dict()

print(student)
```

**Output:**
```text
{}
```

### Example 3: Using the dict() Constructor

```python
student = dict(name="Raj", age=21, marks=85)

print(student)
```

**Output:**
```text
{'name': 'Raj', 'age': 21, 'marks': 85}
```

Notice that when using keyword arguments with `dict()`, keys are written without quotation marks.

### Example 4: Creating a Dictionary from Key-Value Pairs

```python
keys = ["name", "age", "city"]
values = ["Raj", 21, "Mumbai"]

student = dict(zip(keys, values))

print(student)
```

**Output:**
```text
{'name': 'Raj', 'age': 21, 'city': 'Mumbai'}
```

`zip()` combines corresponding elements from two collections.

### Example 5: Using fromkeys()

The `fromkeys()` method creates a dictionary using the given keys and a common initial value.

```python
subjects = ["Python", "Java", "SQL"]

result = dict.fromkeys(subjects, 0)

print(result)
```

**Output:**
```text
{'Python': 0, 'Java': 0, 'SQL': 0}
```

---

## 3. Accessing Dictionary Values

Dictionary values are accessed using their keys.

### Example 1: Using Square Brackets

```python
student = {
    "name": "Raj",
    "age": 21,
    "marks": 85
}

print(student["name"])
print(student["age"])
print(student["marks"])
```

**Output:**
```text
Raj
21
85
```

### Example 2: Using get()

The `get()` method retrieves a value without raising an error if the key does not exist.

```python
student = {
    "name": "Raj",
    "age": 21
}

print(student.get("name"))
print(student.get("city"))
```

**Output:**
```text
Raj
None
```

### Example 3: Providing a Default Value

```python
student = {
    "name": "Raj",
    "age": 21
}

print(student.get("city", "Not Available"))
```

**Output:**
```text
Not Available
```

### Difference Between [] and get()

```python
student = {
    "name": "Raj"
}

print(student["age"])
```

This produces a `KeyError` because `"age"` does not exist.

But:

```python
print(student.get("age"))
```

Returns:

```text
None
```

**Remember:**
- `dictionary[key]` raises `KeyError` if the key is missing.
- `dictionary.get(key)` returns `None` by default if the key is missing.
- `dictionary.get(key, default)` returns the specified default value.

---

## 4. Adding New Items

You can add a new key-value pair by assigning a value to a new key.

```python
student = {
    "name": "Raj",
    "age": 21
}

student["city"] = "Mumbai"

print(student)
```

**Output:**
```text
{'name': 'Raj', 'age': 21, 'city': 'Mumbai'}
```

### Adding Multiple Items

```python
student = {
    "name": "Raj"
}

student["age"] = 21
student["course"] = "Python"
student["marks"] = 85

print(student)
```

**Output:**
```text
{'name': 'Raj', 'age': 21, 'course': 'Python', 'marks': 85}
```

---

## 5. Updating Existing Items

If you assign a value to an existing key, its previous value is replaced.

```python
student = {
    "name": "Raj",
    "marks": 70
}

student["marks"] = 95

print(student)
```

**Output:**
```text
{'name': 'Raj', 'marks': 95}
```

### Using update()

The `update()` method adds new items or updates existing ones.

```python
student = {
    "name": "Raj",
    "age": 21
}

student.update({
    "age": 22,
    "marks": 90,
    "city": "Mumbai"
})

print(student)
```

**Output:**
```text
{'name': 'Raj', 'age': 22, 'marks': 90, 'city': 'Mumbai'}
```

### Updating with Keyword Arguments

```python
student = {
    "name": "Raj",
    "age": 21
}

student.update(age=22, marks=90)

print(student)
```

**Output:**
```text
{'name': 'Raj', 'age': 22, 'marks': 90}
```

---

## 6. Using setdefault()

The `setdefault()` method returns the value of a key if it already exists.

If the key does not exist, it inserts the key with the specified default value.

```python
student = {
    "name": "Raj",
    "age": 21
}

result = student.setdefault("city", "Mumbai")

print(result)
print(student)
```

**Output:**
```text
Mumbai
{'name': 'Raj', 'age': 21, 'city': 'Mumbai'}
```

### Existing Key Example

```python
student = {
    "name": "Raj",
    "age": 21
}

result = student.setdefault("age", 25)

print(result)
print(student)
```

**Output:**
```text
21
{'name': 'Raj', 'age': 21}
```

The existing value is not overwritten.

---

## 7. Removing Dictionary Items

Python provides several methods to remove dictionary items.

### Example 1: Using pop()

The `pop()` method removes a specified key and returns its value.

```python
student = {
    "name": "Raj",
    "age": 21,
    "marks": 85
}

result = student.pop("age")

print("Removed Value:", result)
print(student)
```

**Output:**
```text
Removed Value: 21
{'name': 'Raj', 'marks': 85}
```

You can provide a default value to avoid `KeyError`:

```python
student = {
    "name": "Raj"
}

result = student.pop("age", "Key Not Found")

print(result)
```

**Output:**
```text
Key Not Found
```

### Example 2: Using popitem()

The `popitem()` method removes and returns the last inserted key-value pair.

```python
student = {
    "name": "Raj",
    "age": 21,
    "marks": 85
}

result = student.popitem()

print(result)
print(student)
```

**Output:**
```text
('marks', 85)
{'name': 'Raj', 'age': 21}
```

### Example 3: Using del

```python
student = {
    "name": "Raj",
    "age": 21,
    "marks": 85
}

del student["age"]

print(student)
```

**Output:**
```text
{'name': 'Raj', 'marks': 85}
```

### Example 4: Using clear()

The `clear()` method removes all dictionary items.

```python
student = {
    "name": "Raj",
    "age": 21
}

student.clear()

print(student)
```

**Output:**
```text
{}
```

---

## 8. Dictionary Length and Membership

### Using len()

The `len()` function returns the number of key-value pairs.

```python
student = {
    "name": "Raj",
    "age": 21,
    "marks": 85
}

print(len(student))
```

**Output:**
```text
3
```

### Using in

The `in` operator checks whether a key exists in the dictionary.

```python
student = {
    "name": "Raj",
    "age": 21,
    "marks": 85
}

print("name" in student)
print("city" in student)
```

**Output:**
```text
True
False
```

### Using not in

```python
student = {
    "name": "Raj",
    "age": 21
}

print("city" not in student)
```

**Output:**
```text
True
```

**Important:** By default, membership operators check dictionary keys, not values.

To check values:

```python
student = {
    "name": "Raj",
    "city": "Mumbai"
}

print("Mumbai" in student.values())
```

**Output:**
```text
True
```

---

## 9. Dictionary Methods: keys(), values() and items()

### Example 1: keys()

Returns a view containing all dictionary keys.

```python
student = {
    "name": "Raj",
    "age": 21,
    "marks": 85
}

print(student.keys())
```

**Output:**
```text
dict_keys(['name', 'age', 'marks'])
```

### Example 2: values()

Returns a view containing all dictionary values.

```python
student = {
    "name": "Raj",
    "age": 21,
    "marks": 85
}

print(student.values())
```

**Output:**
```text
dict_values(['Raj', 21, 85])
```

### Example 3: items()

Returns a view containing key-value pairs as tuples.

```python
student = {
    "name": "Raj",
    "age": 21,
    "marks": 85
}

print(student.items())
```

**Output:**
```text
dict_items([('name', 'Raj'), ('age', 21), ('marks', 85)])
```

### Important: Dictionary Views

The objects returned by `keys()`, `values()` and `items()` are dynamic views.

They reflect changes made to the original dictionary.

```python
student = {
    "name": "Raj"
}

keys = student.keys()

print(keys)

student["age"] = 21

print(keys)
```

**Output:**
```text
dict_keys(['name'])
dict_keys(['name', 'age'])
```

---

## 10. Iterating Through Dictionaries

Iteration means accessing dictionary items one by one.

### Example 1: Iterating Through Keys

```python
student = {
    "name": "Raj",
    "age": 21,
    "city": "Mumbai"
}

for key in student:
    print(key)
```

**Output:**
```text
name
age
city
```

You can also write:

```python
for key in student.keys():
    print(key)
```

### Example 2: Iterating Through Values

```python
student = {
    "name": "Raj",
    "age": 21,
    "city": "Mumbai"
}

for value in student.values():
    print(value)
```

**Output:**
```text
Raj
21
Mumbai
```

### Example 3: Iterating Through Key-Value Pairs

```python
student = {
    "name": "Raj",
    "age": 21,
    "city": "Mumbai"
}

for key, value in student.items():
    print(key, ":", value)
```

**Output:**
```text
name : Raj
age : 21
city : Mumbai
```

### Example 4: Using enumerate()

```python
student = {
    "name": "Raj",
    "age": 21,
    "city": "Mumbai"
}

for index, (key, value) in enumerate(student.items()):
    print(index, key, value)
```

**Output:**
```text
0 name Raj
1 age 21
2 city Mumbai
```

Here, `index` represents the iteration count. It is not a dictionary index.

---

## 11. Copying Dictionaries

### Example 1: Direct Assignment

```python
student1 = {
    "name": "Raj",
    "age": 21
}

student2 = student1

student2["age"] = 25

print(student1)
print(student2)
```

**Output:**
```text
{'name': 'Raj', 'age': 25}
{'name': 'Raj', 'age': 25}
```

Both variables refer to the same dictionary object.

### Example 2: Using copy()

```python
student1 = {
    "name": "Raj",
    "age": 21
}

student2 = student1.copy()

student2["age"] = 25

print(student1)
print(student2)
```

**Output:**
```text
{'name': 'Raj', 'age': 21}
{'name': 'Raj', 'age': 25}
```

`copy()` creates a shallow copy.

### What Is a Shallow Copy?

A shallow copy creates a new outer dictionary, but nested mutable objects are still shared.

```python
student1 = {
    "name": "Raj",
    "marks": [80, 90]
}

student2 = student1.copy()

student2["marks"].append(95)

print(student1)
print(student2)
```

**Output:**
```text
{'name': 'Raj', 'marks': [80, 90, 95]}
{'name': 'Raj', 'marks': [80, 90, 95]}
```

Both dictionaries share the same nested list.

For independent nested copies, Python provides `deepcopy()`:

```python
import copy

student1 = {
    "name": "Raj",
    "marks": [80, 90]
}

student2 = copy.deepcopy(student1)

student2["marks"].append(95)

print(student1)
print(student2)
```

**Output:**
```text
{'name': 'Raj', 'marks': [80, 90]}
{'name': 'Raj', 'marks': [80, 90, 95]}
```

---

## 12. Sorting Dictionaries

The `sorted()` function returns a sorted list of dictionary keys by default.

### Example 1: Sorting Keys

```python
marks = {
    "Rahul": 85,
    "Amit": 90,
    "Raj": 95
}

result = sorted(marks)

print(result)
```

**Output:**
```text
['Amit', 'Rahul', 'Raj']
```

### Example 2: Sorting by Values

```python
marks = {
    "Rahul": 85,
    "Amit": 90,
    "Raj": 95
}

result = sorted(marks.items(), key=lambda item: item[1])

print(result)
```

**Output:**
```text
[('Rahul', 85), ('Amit', 90), ('Raj', 95)]
```

This example introduces `lambda`, which will be studied in detail in a later lesson.

### Example 3: Sorting in Descending Order

```python
marks = {
    "Rahul": 85,
    "Amit": 90,
    "Raj": 95
}

result = sorted(
    marks.items(),
    key=lambda item: item[1],
    reverse=True
)

print(result)
```

**Output:**
```text
[('Raj', 95), ('Amit', 90), ('Rahul', 85)]
```

---

## 13. Merging Dictionaries

Two dictionaries can be combined using `update()` or the merge operator `|` (Python 3.9+).

### Example 1: Using update()

```python
student = {
    "name": "Raj",
    "age": 21
}

details = {
    "city": "Mumbai",
    "marks": 90
}

student.update(details)

print(student)
```

**Output:**
```text
{'name': 'Raj', 'age': 21, 'city': 'Mumbai', 'marks': 90}
```

`update()` modifies the original dictionary.

### Example 2: Using the | Operator

```python
student = {
    "name": "Raj",
    "age": 21
}

details = {
    "city": "Mumbai",
    "marks": 90
}

result = student | details

print(result)
print(student)
```

**Output:**
```text
{'name': 'Raj', 'age': 21, 'city': 'Mumbai', 'marks': 90}
{'name': 'Raj', 'age': 21}
```

The `|` operator creates a new dictionary instead of modifying the original ones.

### Duplicate Keys While Merging

If both dictionaries contain the same key, the value from the right-hand dictionary wins.

```python
first = {
    "name": "Raj",
    "age": 21
}

second = {
    "age": 22,
    "city": "Mumbai"
}

result = first | second

print(result)
```

**Output:**
```text
{'name': 'Raj', 'age': 22, 'city': 'Mumbai'}
```

---

## 14. Nested Dictionaries

A dictionary can contain another dictionary as its value.

This structure is called a nested dictionary.

### Example 1: Creating a Nested Dictionary

```python
students = {
    "student1": {
        "name": "Raj",
        "age": 21,
        "marks": 90
    },

    "student2": {
        "name": "Rahul",
        "age": 22,
        "marks": 85
    }
}

print(students)
```

### Example 2: Accessing Nested Values

```python
students = {
    "student1": {
        "name": "Raj",
        "age": 21
    },

    "student2": {
        "name": "Rahul",
        "age": 22
    }
}

print(students["student1"]["name"])
print(students["student2"]["age"])
```

**Output:**
```text
Raj
22
```

### Example 3: Updating Nested Values

```python
students = {
    "student1": {
        "name": "Raj",
        "marks": 80
    }
}

students["student1"]["marks"] = 95

print(students)
```

**Output:**
```text
{'student1': {'name': 'Raj', 'marks': 95}}
```

### Example 4: Adding a New Nested Item

```python
students = {
    "student1": {
        "name": "Raj",
        "marks": 90
    }
}

students["student2"] = {
    "name": "Rahul",
    "marks": 85
}

print(students)
```

**Output:**
```text
{'student1': {'name': 'Raj', 'marks': 90}, 'student2': {'name': 'Rahul', 'marks': 85}}
```

---

## 15. Dictionary Keys and Their Rules

Dictionary keys must be hashable.

Common valid key types include:
- Strings
- Integers
- Floats
- Booleans
- Tuples containing only hashable elements

### Example 1: Different Key Types

```python
data = {
    "name": "Raj",
    101: "Student ID",
    3.14: "Pi",
    (1, 2): "Coordinates"
}

print(data)
```

**Output:**
```text
{'name': 'Raj', 101: 'Student ID', 3.14: 'Pi', (1, 2): 'Coordinates'}
```

### Example 2: Duplicate Keys

```python
data = {
    "name": "Raj",
    "age": 21,
    "name": "Rahul"
}

print(data)
```

**Output:**
```text
{'name': 'Rahul', 'age': 21}
```

Dictionary keys must be unique. When the same key appears multiple times, its last assigned value is retained.

### Example 3: Invalid Dictionary Keys

```python
data = {
    [1, 2]: "Numbers"
}
```

**Output:**
```text
TypeError: unhashable type: 'list'
```

Lists, dictionaries and sets cannot be used as dictionary keys because they are mutable and unhashable.

---

## 16. Useful Dictionary Functions

| Function | Description |
|---|---|
| `len()` | Returns the number of items |
| `type()` | Returns the object's type |
| `str()` | Converts a dictionary to a string |
| `sorted()` | Returns sorted keys or sorted items |
| `min()` | Returns the smallest key |
| `max()` | Returns the largest key |
| `any()` | Checks whether at least one key is truthy |
| `all()` | Checks whether all keys are truthy |

### Example

```python
numbers = {
    10: "Ten",
    20: "Twenty",
    30: "Thirty"
}

print(len(numbers))
print(min(numbers))
print(max(numbers))
print(type(numbers))
```

**Output:**
```text
3
10
30
<class 'dict'>
```

---

# 17. Practical Programs

## Program 1: Create and Display Student Information

```python
student = {
    "name": "Raj",
    "age": 21,
    "course": "Python",
    "marks": 90
}

for key, value in student.items():
    print(key, ":", value)
```

## Program 2: Count Dictionary Items

```python
student = {
    "name": "Raj",
    "age": 21,
    "course": "Python",
    "marks": 90
}

print("Total Items:", len(student))
```

## Program 3: Check Whether a Key Exists

```python
student = {
    "name": "Raj",
    "age": 21,
    "marks": 90
}

key = input("Enter key to search: ")

if key in student:
    print("Key Found")
    print("Value:", student[key])
else:
    print("Key Not Found")
```

## Program 4: Calculate Total and Average Marks

```python
marks = {
    "Python": 90,
    "Java": 85,
    "SQL": 95
}

total = sum(marks.values())
average = total / len(marks)

print("Total Marks:", total)
print("Average Marks:", average)
```

**Output:**
```text
Total Marks: 270
Average Marks: 90.0
```

## Program 5: Find the Subject with Highest Marks

```python
marks = {
    "Python": 90,
    "Java": 85,
    "SQL": 95
}

highest_subject = max(marks, key=marks.get)

print("Highest Scoring Subject:", highest_subject)
print("Marks:", marks[highest_subject])
```

**Output:**
```text
Highest Scoring Subject: SQL
Marks: 95
```

## Program 6: Count Character Frequency

```python
text = input("Enter a string: ")

frequency = {}

for char in text:
    frequency[char] = frequency.get(char, 0) + 1

print(frequency)
```

**Example Input:**
```text
banana
```

**Output:**
```text
{'b': 1, 'a': 3, 'n': 2}
```

## Program 7: Count Word Frequency

```python
sentence = input("Enter a sentence: ")

words = sentence.lower().split()

frequency = {}

for word in words:
    frequency[word] = frequency.get(word, 0) + 1

print(frequency)
```

**Example Input:**
```text
python is easy python is powerful
```

**Output:**
```text
{'python': 2, 'is': 2, 'easy': 1, 'powerful': 1}
```

## Program 8: Merge Two Dictionaries

```python
first = {
    "name": "Raj",
    "age": 21
}

second = {
    "city": "Mumbai",
    "course": "Python"
}

result = first | second

print(result)
```

## Program 9: Find Duplicate Values

```python
data = {
    "a": 10,
    "b": 20,
    "c": 10,
    "d": 30,
    "e": 20
}

values = list(data.values())

duplicates = []

for value in values:
    if values.count(value) > 1 and value not in duplicates:
        duplicates.append(value)

print("Duplicate Values:", duplicates)
```

**Output:**
```text
Duplicate Values: [10, 20]
```

## Program 10: Create a Dictionary from Two Lists

```python
keys = ["name", "age", "city"]
values = ["Raj", 21, "Mumbai"]

student = dict(zip(keys, values))

print(student)
```

---

# 18. Mini Project – Student Record Management System

## Project Description

Create a menu-driven Student Record Management System using dictionaries.

The application should allow the user to:
1. Add a student.
2. View all students.
3. Search for a student.
4. Update student information.
5. Delete a student.
6. Display student statistics.
7. Exit the application.

### Complete Code

```python
students = {}

while True:

    print("\n===== STUDENT RECORD MANAGEMENT SYSTEM =====")

    print("1. Add Student")
    print("2. View All Students")
    print("3. Search Student")
    print("4. Update Student")
    print("5. Delete Student")
    print("6. Student Statistics")
    print("7. Exit")

    choice = input("Enter your choice: ").strip()

    # Add Student
    if choice == "1":

        student_id = input("Enter Student ID: ").strip()

        if not student_id:
            print("Student ID cannot be empty.")

        elif student_id in students:
            print("Student ID already exists.")

        else:
            name = input("Enter Student Name: ").strip()
            age_text = input("Enter Age: ").strip()
            course = input("Enter Course: ").strip()
            marks_text = input("Enter Marks: ").strip()

            try:
                age = int(age_text)
                marks = float(marks_text)

                if age <= 0 or not 0 <= marks <= 100:
                    print("Invalid age or marks.")

                elif not name or not course:
                    print("Name and course cannot be empty.")

                else:
                    students[student_id] = {
                        "name": name,
                        "age": age,
                        "course": course,
                        "marks": marks
                    }

                    print("Student Added Successfully.")

            except ValueError:
                print("Age must be an integer and marks must be numeric.")

    # View All Students
    elif choice == "2":

        if not students:
            print("No Student Records Found.")

        else:
            print("\n----- ALL STUDENT RECORDS -----")

            for student_id, details in students.items():

                print("\nStudent ID:", student_id)

                for key, value in details.items():
                    print(key.capitalize(), ":", value)

    # Search Student
    elif choice == "3":

        student_id = input("Enter Student ID: ").strip()

        if student_id in students:

            print("\nStudent Found")

            print("Student ID:", student_id)

            for key, value in students[student_id].items():
                print(key.capitalize(), ":", value)

        else:
            print("Student Not Found.")

    # Update Student
    elif choice == "4":

        student_id = input("Enter Student ID: ").strip()

        if student_id in students:

            print("\n1. Update Name")
            print("2. Update Age")
            print("3. Update Course")
            print("4. Update Marks")

            update_choice = input("Choose field: ").strip()

            try:

                if update_choice == "1":

                    name = input("Enter New Name: ").strip()

                    if name:
                        students[student_id]["name"] = name
                        print("Name Updated Successfully.")
                    else:
                        print("Name cannot be empty.")

                elif update_choice == "2":

                    age = int(input("Enter New Age: "))

                    if age > 0:
                        students[student_id]["age"] = age
                        print("Age Updated Successfully.")
                    else:
                        print("Age must be positive.")

                elif update_choice == "3":

                    course = input("Enter New Course: ").strip()

                    if course:
                        students[student_id]["course"] = course
                        print("Course Updated Successfully.")
                    else:
                        print("Course cannot be empty.")

                elif update_choice == "4":

                    marks = float(input("Enter New Marks: "))

                    if 0 <= marks <= 100:
                        students[student_id]["marks"] = marks
                        print("Marks Updated Successfully.")
                    else:
                        print("Marks must be between 0 and 100.")

                else:
                    print("Invalid Update Choice.")

            except ValueError:
                print("Invalid input. Please enter the correct data type.")

        else:
            print("Student Not Found.")

    # Delete Student
    elif choice == "5":

        student_id = input("Enter Student ID: ").strip()

        if student_id in students:

            confirm = input("Are you sure? (yes/no): ").strip().lower()

            if confirm == "yes":
                students.pop(student_id)
                print("Student Deleted Successfully.")

            else:
                print("Deletion Cancelled.")

        else:
            print("Student Not Found.")

    # Student Statistics
    elif choice == "6":

        if not students:
            print("No Student Records Available.")

        else:
            total_students = len(students)

            total_marks = sum(
                student["marks"]
                for student in students.values()
            )

            average_marks = total_marks / total_students

            highest_id = max(
                students,
                key=lambda sid: students[sid]["marks"]
            )

            lowest_id = min(
                students,
                key=lambda sid: students[sid]["marks"]
            )

            print("\n----- STUDENT STATISTICS -----")

            print("Total Students:", total_students)
            print("Average Marks:", round(average_marks, 2))

            print(
                "Highest Scorer:",
                students[highest_id]["name"],
                "-",
                students[highest_id]["marks"]
            )

            print(
                "Lowest Scorer:",
                students[lowest_id]["name"],
                "-",
                students[lowest_id]["marks"]
            )

    # Exit
    elif choice == "7":

        print("Thank you for using Student Record Management System.")
        break

    else:
        print("Invalid Choice. Please Try Again.")
```

### Project Concepts Used

- Dictionary creation and manipulation.
- Nested dictionaries.
- Adding, updating and deleting records.
- Dictionary membership checks.
- Dictionary iteration.
- `get()`, `items()`, `values()`, `pop()`.
- `len()`, `sum()`, `max()`, `min()`.
- Input validation.
- Exception handling.
- Menu-driven programming.
- `while` loops and conditional statements.

---

# 19. Student Practice Exercises

Complete these exercises independently.

### Beginner Level

1. Create a dictionary containing your name, age, city and course.
2. Print the value of each key separately.
3. Add a new key called `email`.
4. Update your age.
5. Delete the city key.
6. Display all dictionary keys.
7. Display all dictionary values.
8. Count the total number of items.
9. Check whether a particular key exists.
10. Create an empty dictionary and add five items.

### Intermediate Level

11. Create a dictionary containing five subjects and their marks. Calculate the total and average.
12. Find the highest and lowest values in a marks dictionary.
13. Merge two dictionaries.
14. Count the frequency of every character in a string.
15. Count the frequency of every word in a sentence.
16. Create a dictionary using two separate lists.
17. Find duplicate values in a dictionary.
18. Sort a dictionary by its values.
19. Create a nested dictionary containing three students.
20. Update the marks of a student inside a nested dictionary.

### Advanced Practice

21. Create a phonebook using dictionaries with add, search, update and delete functionality.
22. Create an inventory dictionary containing product names and quantities.
23. Write a program that counts how many students passed and failed.
24. Create a simple voting system using dictionaries to count votes.
25. Build a menu-driven Employee Record Management System.

---

# 20. Trainer Assessment

The trainer should verify that the student can independently:

- [ ] Explain dictionary key-value pairs.
- [ ] Create empty and populated dictionaries.
- [ ] Explain dictionary mutability and insertion order.
- [ ] Access values using keys and `get()`.
- [ ] Add and update dictionary items.
- [ ] Use `setdefault()` correctly.
- [ ] Remove items using `pop()`, `popitem()`, `del` and `clear()`.
- [ ] Iterate through keys, values and items.
- [ ] Use dictionary membership checks.
- [ ] Copy dictionaries and understand shallow copying.
- [ ] Merge and sort dictionaries.
- [ ] Create and manipulate nested dictionaries.
- [ ] Build the Student Record Management System independently.

## Completion Criteria

The day is considered complete when:

1. All practical examples have been executed.
2. All beginner exercises have been completed.
3. At least 10 intermediate and advanced exercises have been attempted.
4. The Student Record Management System works correctly.
5. The student can explain the difference between lists, tuples, sets and dictionaries.
6. The student can independently create, access, update and delete dictionary records.


# Day 18 – Collection Operations & Nested Collections

## 1. Introduction to Python Collections

Python provides four major built-in collection data types:

1. List
2. Tuple
3. Set
4. Dictionary

Each collection has different characteristics and use cases.

| Feature | List | Tuple | Set | Dictionary |
|---|---|---|---|---|
| Syntax | `[]` | `()` | `{}` | `{key: value}` |
| Ordered | Yes | Yes | No | Yes |
| Mutable | Yes | No | Yes | Yes |
| Duplicates | Allowed | Allowed | Not allowed | Keys: No |
| Indexing | Yes | Yes | No | Access by key |
| Stores | Elements | Elements | Unique elements | Key-value pairs |

### Example

```python
my_list = [10, 20, 30]
my_tuple = (10, 20, 30)
my_set = {10, 20, 30}
my_dict = {"a": 10, "b": 20}

print(my_list)
print(my_tuple)
print(my_set)
print(my_dict)
```

**Output:**

```text
[10, 20, 30]
(10, 20, 30)
{10, 20, 30}
{'a': 10, 'b': 20}
```

---

## 2. Collections Inside Collections

Python allows one collection to contain another collection.

This is useful when information has multiple levels or relationships.

Examples:

- A list containing multiple lists.
- A list containing dictionaries.
- A dictionary containing lists.
- A dictionary containing other dictionaries.
- A tuple containing lists.
- A list containing tuples.

### Example 1: List Inside a List

```python
matrix = [
    [10, 20, 30],
    [40, 50, 60],
    [70, 80, 90]
]

print(matrix)
```

**Output:**

```text
[[10, 20, 30], [40, 50, 60], [70, 80, 90]]
```

### Example 2: Dictionary Inside a List

```python
students = [
    {"name": "Raj", "age": 21},
    {"name": "Rahul", "age": 22},
    {"name": "Amit", "age": 20}
]

print(students)
```

**Output:**

```text
[{'name': 'Raj', 'age': 21}, {'name': 'Rahul', 'age': 22}, {'name': 'Amit', 'age': 20}]
```

### Example 3: List Inside a Dictionary

```python
student = {
    "name": "Raj",
    "subjects": ["Python", "Java", "SQL"],
    "marks": [90, 85, 95]
}

print(student)
```

**Output:**

```text
{'name': 'Raj', 'subjects': ['Python', 'Java', 'SQL'], 'marks': [90, 85, 95]}
```

### Example 4: Dictionary Inside a Dictionary

```python
company = {
    "employee1": {
        "name": "Raj",
        "department": "IT"
    },

    "employee2": {
        "name": "Rahul",
        "department": "HR"
    }
}

print(company)
```

**Output:**

```text
{'employee1': {'name': 'Raj', 'department': 'IT'}, 'employee2': {'name': 'Rahul', 'department': 'HR'}}
```

---

## 3. Accessing Nested Collection Elements

When collections are nested, we use multiple indexing operations or dictionary keys.

### Example 1: Accessing a Nested List

```python
numbers = [
    [10, 20, 30],
    [40, 50, 60],
    [70, 80, 90]
]

print(numbers[0])
print(numbers[1])
print(numbers[2])
```

**Output:**

```text
[10, 20, 30]
[40, 50, 60]
[70, 80, 90]
```

### Example 2: Accessing Individual Elements

```python
numbers = [
    [10, 20, 30],
    [40, 50, 60],
    [70, 80, 90]
]

print(numbers[0][0])
print(numbers[1][2])
print(numbers[2][1])
```

**Output:**

```text
10
60
80
```

**Understanding:**

`numbers[1][2]`

- First `[1]` selects the second inner list.
- Second `[2]` selects the third element from that list.

### Example 3: Accessing a Dictionary Inside a List

```python
students = [
    {"name": "Raj", "marks": 90},
    {"name": "Rahul", "marks": 85}
]

print(students[0]["name"])
print(students[1]["marks"])
```

**Output:**

```text
Raj
85
```

### Example 4: Accessing a List Inside a Dictionary

```python
student = {
    "name": "Raj",
    "subjects": ["Python", "Java", "SQL"]
}

print(student["subjects"][0])
print(student["subjects"][2])
```

**Output:**

```text
Python
SQL
```

### Example 5: Accessing a Deeply Nested Value

```python
company = {
    "department": {
        "IT": {
            "employee": {
                "name": "Raj",
                "salary": 50000
            }
        }
    }
}

print(company["department"]["IT"]["employee"]["name"])
print(company["department"]["IT"]["employee"]["salary"])
```

**Output:**

```text
Raj
50000
```

---

## 4. Updating Nested Collections

Nested collections can be modified according to the mutability of the collection.

### Example 1: Updating a Nested List

```python
numbers = [
    [10, 20],
    [30, 40]
]

numbers[0][1] = 99

print(numbers)
```

**Output:**

```text
[[10, 99], [30, 40]]
```

### Example 2: Updating a Dictionary Inside a List

```python
students = [
    {"name": "Raj", "marks": 80},
    {"name": "Rahul", "marks": 85}
]

students[0]["marks"] = 95

print(students)
```

**Output:**

```text
[{'name': 'Raj', 'marks': 95}, {'name': 'Rahul', 'marks': 85}]
```

### Example 3: Adding an Element to a Nested List

```python
student = {
    "name": "Raj",
    "subjects": ["Python", "Java"]
}

student["subjects"].append("SQL")

print(student)
```

**Output:**

```text
{'name': 'Raj', 'subjects': ['Python', 'Java', 'SQL']}
```

### Example 4: Adding a New Dictionary Entry

```python
company = {
    "IT": {
        "employee1": "Raj"
    }
}

company["IT"]["employee2"] = "Rahul"

print(company)
```

**Output:**

```text
{'IT': {'employee1': 'Raj', 'employee2': 'Rahul'}}
```

---

## 5. Iterating Through Nested Collections

Nested loops are commonly used to process nested collections.

### Example 1: Iterating Through a Nested List

```python
matrix = [
    [10, 20, 30],
    [40, 50, 60],
    [70, 80, 90]
]

for row in matrix:

    for value in row:
        print(value, end=" ")

    print()
```

**Output:**

```text
10 20 30
40 50 60
70 80 90
```

### Example 2: Iterating Through Dictionaries Inside a List

```python
students = [
    {"name": "Raj", "marks": 90},
    {"name": "Rahul", "marks": 85},
    {"name": "Amit", "marks": 95}
]

for student in students:

    for key, value in student.items():
        print(key, ":", value)

    print()
```

**Output:**

```text
name : Raj
marks : 90

name : Rahul
marks : 85

name : Amit
marks : 95
```

### Example 3: Using enumerate() with Nested Collections

```python
students = [
    {"name": "Raj", "marks": 90},
    {"name": "Rahul", "marks": 85},
    {"name": "Amit", "marks": 95}
]

for index, student in enumerate(students, start=1):

    print("Student:", index)
    print("Name:", student["name"])
    print("Marks:", student["marks"])
```

**Output:**

```text
Student: 1
Name: Raj
Marks: 90
Student: 2
Name: Rahul
Marks: 85
Student: 3
Name: Amit
Marks: 95
```

---

## 6. Combining Different Collection Types

Python allows different collection types to work together.

### Example 1: List of Tuples

```python
students = [
    ("Raj", 90),
    ("Rahul", 85),
    ("Amit", 95)
]

for name, marks in students:
    print(name, marks)
```

**Output:**

```text
Raj 90
Rahul 85
Amit 95
```

### Example 2: List of Dictionaries with Lists

```python
students = [
    {
        "name": "Raj",
        "subjects": ["Python", "SQL"]
    },

    {
        "name": "Rahul",
        "subjects": ["Java", "Python"]
    }
]

for student in students:

    print("Name:", student["name"])
    print("Subjects:", student["subjects"])
```

### Example 3: Dictionary of Lists

```python
department = {
    "IT": ["Raj", "Rahul"],
    "HR": ["Amit", "Rohan"],
    "Sales": ["Neha", "Priya"]
}

for department_name, employees in department.items():

    print(department_name)

    for employee in employees:
        print("-", employee)
```

**Output:**

```text
IT
- Raj
- Rahul
HR
- Amit
- Rohan
Sales
- Neha
- Priya
```

### Example 4: Dictionary of Sets

```python
permissions = {
    "admin": {"read", "write", "delete"},
    "editor": {"read", "write"},
    "viewer": {"read"}
}

for role, access in permissions.items():

    print(role, ":", access)
```

Sets are useful here because duplicate permissions are unnecessary.

---

## 7. Converting Between Collections

Python provides constructors to convert one collection type into another.

| Constructor | Result |
|---|---|
| `list()` | List |
| `tuple()` | Tuple |
| `set()` | Set |
| `dict()` | Dictionary |

### Example 1: List to Tuple

```python
numbers = [10, 20, 30]

result = tuple(numbers)

print(result)
```

**Output:**

```text
(10, 20, 30)
```

### Example 2: Tuple to List

```python
numbers = (10, 20, 30)

result = list(numbers)

print(result)
```

**Output:**

```text
[10, 20, 30]
```

### Example 3: List to Set

```python
numbers = [10, 20, 20, 30, 30, 40]

result = set(numbers)

print(result)
```

**Output:**

```text
{10, 20, 30, 40}
```

The set removes duplicate values. Remember that set order is not guaranteed.

### Example 4: Dictionary to List

```python
student = {
    "name": "Raj",
    "age": 21,
    "marks": 90
}

keys = list(student)
values = list(student.values())
items = list(student.items())

print(keys)
print(values)
print(items)
```

**Output:**

```text
['name', 'age', 'marks']
['Raj', 21, 90]
[('name', 'Raj'), ('age', 21), ('marks', 90)]
```

### Example 5: List of Pairs to Dictionary

```python
data = [
    ("name", "Raj"),
    ("age", 21),
    ("city", "Mumbai")
]

student = dict(data)

print(student)
```

**Output:**

```text
{'name': 'Raj', 'age': 21, 'city': 'Mumbai'}
```

---

## 8. Collection Operations

### Example 1: Combining Lists

```python
first = [10, 20, 30]
second = [40, 50, 60]

result = first + second

print(result)
```

**Output:**

```text
[10, 20, 30, 40, 50, 60]
```

### Example 2: Removing Duplicates

```python
numbers = [10, 20, 20, 30, 30, 40]

unique_numbers = list(set(numbers))

print(unique_numbers)
```

The result contains unique values, but their order is not guaranteed.

To preserve the original order:

```python
numbers = [10, 20, 20, 30, 30, 40]

unique_numbers = list(dict.fromkeys(numbers))

print(unique_numbers)
```

**Output:**

```text
[10, 20, 30, 40]
```

### Example 3: Common Elements Between Lists

```python
first = [10, 20, 30, 40]
second = [30, 40, 50, 60]

common = list(set(first) & set(second))

print(common)
```

**Output:** The result contains `30` and `40`. Its order is not guaranteed.

### Example 4: Flattening a Nested List

Flattening means converting a nested list into a single-level list.

```python
matrix = [
    [10, 20],
    [30, 40],
    [50, 60]
]

result = []

for row in matrix:

    for value in row:
        result.append(value)

print(result)
```

**Output:**

```text
[10, 20, 30, 40, 50, 60]
```

---

## 9. Shallow Copy vs Deep Copy in Nested Collections

This is an important concept when working with nested lists and dictionaries.

### Shallow Copy

A shallow copy creates a new outer collection but keeps references to nested objects.

```python
import copy

original = [
    [10, 20],
    [30, 40]
]

shallow = copy.copy(original)

shallow[0][0] = 99

print("Original:", original)
print("Shallow:", shallow)
```

**Output:**

```text
Original: [[99, 20], [30, 40]]
Shallow: [[99, 20], [30, 40]]
```

The inner lists are shared.

### Deep Copy

A deep copy creates independent copies of nested objects.

```python
import copy

original = [
    [10, 20],
    [30, 40]
]

deep = copy.deepcopy(original)

deep[0][0] = 99

print("Original:", original)
print("Deep Copy:", deep)
```

**Output:**

```text
Original: [[10, 20], [30, 40]]
Deep Copy: [[99, 20], [30, 40]]
```

**Remember:**

- `copy.copy()` creates a shallow copy.
- `copy.deepcopy()` creates a deep copy.
- Deep copying is useful when nested mutable data must remain independent.

---

## 10. Practical Programs

### Program 1: Student Marks Management

```python
students = [
    {"name": "Raj", "marks": 90},
    {"name": "Rahul", "marks": 85},
    {"name": "Amit", "marks": 95}
]

for student in students:

    print(
        student["name"],
        "-",
        student["marks"]
    )
```

### Program 2: Calculate Total Marks of All Students

```python
students = [
    {"name": "Raj", "marks": [80, 90, 85]},
    {"name": "Rahul", "marks": [75, 85, 80]},
    {"name": "Amit", "marks": [90, 95, 92]}
]

for student in students:

    total = sum(student["marks"])

    print(student["name"], "Total:", total)
```

### Program 3: Find the Student with Highest Average

```python
students = [
    {"name": "Raj", "marks": [80, 90, 85]},
    {"name": "Rahul", "marks": [75, 85, 80]},
    {"name": "Amit", "marks": [90, 95, 92]}
]

highest_student = max(
    students,
    key=lambda student: sum(student["marks"]) / len(student["marks"])
)

average = sum(highest_student["marks"]) / len(highest_student["marks"])

print("Top Student:", highest_student["name"])
print("Average:", round(average, 2))
```

### Program 4: Inventory Management

```python
inventory = {
    "Laptop": {
        "price": 50000,
        "quantity": 5
    },

    "Mouse": {
        "price": 500,
        "quantity": 20
    },

    "Keyboard": {
        "price": 1000,
        "quantity": 10
    }
}

total_inventory_value = 0

for product, details in inventory.items():

    value = details["price"] * details["quantity"]

    total_inventory_value += value

    print(product, "Value:", value)

print("Total Inventory Value:", total_inventory_value)
```

### Program 5: Department Employee Management

```python
company = {
    "IT": ["Raj", "Rahul", "Amit"],
    "HR": ["Neha", "Priya"],
    "Sales": ["Rohan", "Karan"]
}

for department, employees in company.items():

    print("\nDepartment:", department)
    print("Employee Count:", len(employees))

    for employee in employees:
        print("-", employee)
```

### Program 6: Matrix Addition

```python
matrix1 = [
    [10, 20],
    [30, 40]
]

matrix2 = [
    [5, 10],
    [15, 20]
]

result = []

for i in range(len(matrix1)):

    row = []

    for j in range(len(matrix1[i])):

        value = matrix1[i][j] + matrix2[i][j]

        row.append(value)

    result.append(row)

print("Result:", result)
```

**Output:**

```text
Result: [[15, 30], [45, 60]]
```

This example assumes both matrices have compatible dimensions.

---

# 11. Mini Project – Company Employee Management System

## Project Description

Build a menu-driven Employee Management System using nested dictionaries.

The application should support:

1. Add an employee.
2. View all employees.
3. Search an employee.
4. Update employee details.
5. Delete an employee.
6. Display department-wise employees.
7. Calculate total company salary.
8. Exit.

### Complete Code

```python
employees = {}

while True:

    print("\n===== EMPLOYEE MANAGEMENT SYSTEM =====")

    print("1. Add Employee")
    print("2. View All Employees")
    print("3. Search Employee")
    print("4. Update Employee")
    print("5. Delete Employee")
    print("6. Department-wise Employees")
    print("7. Total Salary Expense")
    print("8. Exit")

    choice = input("Enter your choice: ").strip()

    # Add Employee
    if choice == "1":

        emp_id = input("Enter Employee ID: ").strip()

        if not emp_id:
            print("Employee ID cannot be empty.")

        elif emp_id in employees:
            print("Employee ID already exists.")

        else:

            name = input("Enter Name: ").strip()
            department = input("Enter Department: ").strip()
            salary_text = input("Enter Salary: ").strip()

            try:

                salary = float(salary_text)

                if not name or not department or salary < 0:
                    print("Invalid employee details.")

                else:

                    employees[emp_id] = {
                        "name": name,
                        "department": department,
                        "salary": salary
                    }

                    print("Employee Added Successfully.")

            except ValueError:
                print("Salary must be numeric.")

    # View All Employees
    elif choice == "2":

        if not employees:
            print("No Employee Records Found.")

        else:

            for emp_id, details in employees.items():

                print("\nEmployee ID:", emp_id)

                for key, value in details.items():
                    print(key.capitalize(), ":", value)

    # Search Employee
    elif choice == "3":

        emp_id = input("Enter Employee ID: ").strip()

        if emp_id in employees:

            print("Employee Found:")
            print("ID:", emp_id)

            for key, value in employees[emp_id].items():
                print(key.capitalize(), ":", value)

        else:
            print("Employee Not Found.")

    # Update Employee
    elif choice == "4":

        emp_id = input("Enter Employee ID: ").strip()

        if emp_id in employees:

            print("1. Update Name")
            print("2. Update Department")
            print("3. Update Salary")

            update_choice = input("Choose field: ").strip()

            if update_choice == "1":

                name = input("Enter New Name: ").strip()

                if name:
                    employees[emp_id]["name"] = name
                    print("Name Updated.")
                else:
                    print("Name cannot be empty.")

            elif update_choice == "2":

                department = input("Enter New Department: ").strip()

                if department:
                    employees[emp_id]["department"] = department
                    print("Department Updated.")
                else:
                    print("Department cannot be empty.")

            elif update_choice == "3":

                try:

                    salary = float(input("Enter New Salary: "))

                    if salary >= 0:
                        employees[emp_id]["salary"] = salary
                        print("Salary Updated.")
                    else:
                        print("Salary cannot be negative.")

                except ValueError:
                    print("Invalid Salary.")

            else:
                print("Invalid Update Choice.")

        else:
            print("Employee Not Found.")

    # Delete Employee
    elif choice == "5":

        emp_id = input("Enter Employee ID: ").strip()

        if emp_id in employees:

            confirm = input("Confirm deletion? (yes/no): ").strip().lower()

            if confirm == "yes":
                del employees[emp_id]
                print("Employee Deleted Successfully.")

            else:
                print("Deletion Cancelled.")

        else:
            print("Employee Not Found.")

    # Department-wise Employees
    elif choice == "6":

        if not employees:
            print("No Employee Records Available.")

        else:

            departments = {}

            for emp_id, details in employees.items():

                department = details["department"]

                if department not in departments:
                    departments[department] = []

                departments[department].append(details["name"])

            for department, names in departments.items():

                print("\nDepartment:", department)

                for name in names:
                    print("-", name)

    # Total Salary Expense
    elif choice == "7":

        total_salary = sum(
            details["salary"]
            for details in employees.values()
        )

        print("Total Employees:", len(employees))
        print("Total Monthly Salary:", total_salary)

    # Exit
    elif choice == "8":

        print("Thank you for using Employee Management System.")
        break

    else:
        print("Invalid Choice. Please Try Again.")
```

## Project Concepts Used

- Lists and dictionaries.
- Nested dictionaries.
- Dictionary iteration.
- List operations.
- Dynamic collection creation.
- Collection conversion.
- Searching and updating records.
- Grouping data by department.
- Aggregation using `sum()` and `len()`.
- Input validation and exception handling.
- Menu-driven programming.

---

# 12. Student Practice Exercises

## Beginner Level

1. Create a list containing five dictionaries representing five students.
2. Create a dictionary containing a list of five subjects.
3. Create a nested list representing a 3 × 3 matrix.
4. Access the second element of the third inner list.
5. Update a value inside a nested dictionary.
6. Create a dictionary containing three departments and their employee lists.
7. Iterate through a list of dictionaries and print every record.
8. Convert a list into a tuple, set and dictionary where appropriate.

## Intermediate Level

9. Calculate the total marks of every student in a nested collection.
10. Find the student with the highest average marks.
11. Flatten a nested list containing three inner lists.
12. Find common elements between two lists.
13. Remove duplicate values while preserving their original order.
14. Create an inventory dictionary and calculate total stock value.
15. Group employees by department.
16. Add a new subject to every student in a nested dictionary.

## Advanced Level

17. Create a library system using a list of dictionaries.
18. Build a shopping cart using nested dictionaries.
19. Create a department-wise employee salary report.
20. Build a matrix multiplication program.
21. Create a student result system with subject-wise marks and grades.
22. Build a menu-driven inventory management application.

---

# 13. Trainer Assessment

The trainer should verify that the student can independently:

- [ ] Explain the differences between lists, tuples, sets and dictionaries.
- [ ] Create collections inside other collections.
- [ ] Access nested elements using indexes and keys.
- [ ] Add, update and delete nested values.
- [ ] Iterate through nested lists and dictionaries.
- [ ] Combine different collection types.
- [ ] Convert between collection types.
- [ ] Flatten nested lists.
- [ ] Remove duplicates while preserving order.
- [ ] Explain shallow copy and deep copy.
- [ ] Group and process data using nested collections.
- [ ] Build the Employee Management System independently.

## Completion Criteria

The day is considered complete when:

1. All practical examples have been executed.
2. All beginner exercises have been completed.
3. At least 10 intermediate and advanced exercises have been attempted.
4. The Employee Management System works correctly.
5. The student can explain nested data structures.
6. The student can independently access, update, iterate and process nested collections.
7. The student can select an appropriate collection type for a given problem.

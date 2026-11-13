
# Day 36 – JSON, CSV & Data Serialization

## 1. Introduction to Data Serialization

Data serialization is the process of converting data into a format that can be stored or transferred.

When an application needs to save data or send it to another application, it often converts Python objects into a standard data format.

This process is called serialization.

Converting serialized data back into Python objects is called deserialization.

### Example

Suppose we have a Python dictionary:

```python
student = {
    "name": "Raj",
    "age": 22,
    "course": "Python"
}
```

We can convert this dictionary into JSON format:

```json
{
    "name": "Raj",
    "age": 22,
    "course": "Python"
}
```

### Serialization vs Deserialization

| Operation | Meaning |
|---|---|
| Serialization | Python object to a storage or transfer format |
| Deserialization | Serialized data back into a Python object |

### Common Data Formats

| Format | Purpose |
|---|---|
| JSON | Data exchange between applications |
| CSV | Storing tabular data |
| XML | Structured data exchange |
| Pickle | Python object serialization |

In this lesson, we will focus on JSON and CSV.

---

## 2. Introduction to JSON

JSON stands for JavaScript Object Notation.

It is a lightweight text-based format used to store and exchange structured data.

JSON is commonly used in:

- REST APIs.
- Web applications.
- Configuration files.
- Data storage.
- Communication between different programming languages.

### JSON Data Types

| JSON Type | Example |
|---|---|
| String | `"Raj"` |
| Number | `25`, `99.5` |
| Boolean | `true`, `false` |
| Null | `null` |
| Array | `[10, 20, 30]` |
| Object | `{"name": "Raj"}` |

### JSON and Python Data Types

| JSON | Python |
|---|---|
| Object | Dictionary |
| Array | List |
| String | String |
| Number (integer) | Integer |
| Number (decimal) | Float |
| `true` | `True` |
| `false` | `False` |
| `null` | `None` |

Important: JSON uses lowercase `true`, `false` and `null`. Python uses `True`, `False` and `None`.

---

## 3. Introduction to the json Module

Python provides a built-in `json` module.

No additional installation is required.

Import it:

```python
import json
```

The module provides methods for converting Python objects to JSON and JSON data to Python objects.

Important methods:

| Method | Purpose |
|---|---|
| `json.dumps()` | Python object to JSON string |
| `json.loads()` | JSON string to Python object |
| `json.dump()` | Write Python object as JSON to a file |
| `json.load()` | Read JSON data from a file |

---

## 4. Convert Python Objects into JSON Strings Using dumps()

The `json.dumps()` method converts a Python object into a JSON-formatted string.

Syntax:

```python
json.dumps(python_object)
```

### Example 1: Dictionary to JSON

```python
import json

student = {
    "name": "Raj",
    "age": 22,
    "course": "Python"
}

result = json.dumps(student)

print(result)
print(type(result))
```

**Output:**

```text
{"name": "Raj", "age": 22, "course": "Python"}
<class 'str'>
```

Notice that the result is a string, not a dictionary.

### Example 2: List to JSON

```python
import json

numbers = [10, 20, 30, 40]

result = json.dumps(numbers)

print(result)
```

**Output:**

```text
[10, 20, 30, 40]
```

### Example 3: Nested Dictionary to JSON

```python
import json

student = {
    "name": "Raj",
    "marks": {
        "python": 90,
        "java": 85
    },
    "skills": ["Python", "HTML", "CSS"]
}

result = json.dumps(student)

print(result)
```

**Output:**

```text
{"name": "Raj", "marks": {"python": 90, "java": 85}, "skills": ["Python", "HTML", "CSS"]}
```

---

## 5. Format JSON Using indent and sort_keys

The `dumps()` method supports additional parameters.

### 5.1 indent

The `indent` parameter makes JSON output easier to read.

```python
import json

student = {
    "name": "Raj",
    "age": 22,
    "course": "Python"
}

result = json.dumps(student, indent=4)

print(result)
```

**Output:**

```json
{
    "name": "Raj",
    "age": 22,
    "course": "Python"
}
```

### 5.2 sort_keys

The `sort_keys` parameter sorts dictionary keys alphabetically.

```python
import json

student = {
    "name": "Raj",
    "age": 22,
    "course": "Python"
}

result = json.dumps(student, indent=4, sort_keys=True)

print(result)
```

**Output:**

```json
{
    "age": 22,
    "course": "Python",
    "name": "Raj"
}
```

### 5.3 ensure_ascii

By default, JSON output escapes non-ASCII characters.

Use `ensure_ascii=False` to preserve Unicode characters in the output.

```python
import json

data = {
    "name": "राज",
    "city": "मुंबई"
}

print(json.dumps(data, ensure_ascii=False, indent=4))
```

**Output:**

```json
{
    "name": "राज",
    "city": "मुंबई"
}
```

### 5.4 Handling Non-Serializable Values

JSON supports a limited set of data types.

For example, a Python `datetime` object cannot be directly serialized by the default JSON encoder.

```python
import json
from datetime import datetime

data = {
    "created_at": datetime.now()
}

# This raises TypeError.
# print(json.dumps(data))
```

Convert unsupported values into a suitable JSON-compatible representation.

```python
import json
from datetime import datetime

data = {
    "created_at": datetime.now()
}

result = json.dumps(data, default=str)

print(result)
```

**Sample Output:**

```json
{"created_at": "2026-11-13 10:00:00.123456"}
```

The exact date and time will vary.

For production applications, prefer explicit conversion functions when you need consistent date formats.

---

## 6. Convert JSON Strings into Python Objects Using loads()

The `json.loads()` method converts a JSON string into a Python object.

Syntax:

```python
json.loads(json_string)
```

### Example 1: JSON to Dictionary

```python
import json

json_data = '{"name": "Raj", "age": 22, "course": "Python"}'

result = json.loads(json_data)

print(result)
print(type(result))
```

**Output:**

```text
{'name': 'Raj', 'age': 22, 'course': 'Python'}
<class 'dict'>
```

### Example 2: Access JSON Data

```python
import json

json_data = '{"name": "Raj", "age": 22, "city": "Mumbai"}'

student = json.loads(json_data)

print("Name:", student["name"])
print("Age:", student["age"])
print("City:", student["city"])
```

**Output:**

```text
Name: Raj
Age: 22
City: Mumbai
```

### Example 3: JSON Array to Python List

```python
import json

json_data = '[10, 20, 30, 40]'

result = json.loads(json_data)

print(result)
print(type(result))
```

**Output:**

```text
[10, 20, 30, 40]
<class 'list'>
```

### Example 4: Read Nested JSON

```python
import json

json_data = '''
{
    "name": "Raj",
    "marks": {
        "python": 90,
        "java": 85
    }
}
'''

student = json.loads(json_data)

print(student["name"])
print(student["marks"]["python"])
print(student["marks"]["java"])
```

**Output:**

```text
Raj
90
85
```

---

## 7. Write JSON Data into a File Using dump()

The `json.dump()` method writes a Python object directly into a JSON file.

Syntax:

```python
json.dump(python_object, file_object)
```

### Example 1: Create and Write a JSON File

```python
import json

student = {
    "name": "Raj",
    "age": 22,
    "course": "Python",
    "marks": 90
}

with open("student.json", "w", encoding="utf-8") as file:
    json.dump(student, file, indent=4)

print("JSON file created successfully")
```

**Output:**

```text
JSON file created successfully
```

The file `student.json` will contain:

```json
{
    "name": "Raj",
    "age": 22,
    "course": "Python",
    "marks": 90
}
```

### Example 2: Write a List of Dictionaries

```python
import json

students = [
    {"id": 1, "name": "Raj", "marks": 90},
    {"id": 2, "name": "Amit", "marks": 85},
    {"id": 3, "name": "Neha", "marks": 95}
]

with open("students.json", "w", encoding="utf-8") as file:
    json.dump(students, file, indent=4)

print("Students saved successfully")
```

**Output:**

```text
Students saved successfully
```

### Important

- `"w"` creates a file if it does not exist.
- `"w"` overwrites existing content.
- `indent=4` makes the JSON file readable.
- `encoding="utf-8"` supports Unicode text.

---

## 8. Read JSON Data from a File Using load()

The `json.load()` method reads JSON data from a file and converts it into a Python object.

Syntax:

```python
json.load(file_object)
```

### Example 1: Read a JSON File

```python
import json

with open("student.json", "r", encoding="utf-8") as file:
    student = json.load(file)

print(student)
print("Name:", student["name"])
print("Marks:", student["marks"])
```

**Output:**

```text
{'name': 'Raj', 'age': 22, 'course': 'Python', 'marks': 90}
Name: Raj
Marks: 90
```

### Example 2: Read and Display Multiple Students

```python
import json

with open("students.json", "r", encoding="utf-8") as file:
    students = json.load(file)

for student in students:
    print(student["id"], student["name"], student["marks"])
```

**Output:**

```text
1 Raj 90
2 Amit 85
3 Neha 95
```

---

## 9. Update JSON File Data

JSON files do not provide a direct editing operation for individual dictionary fields.

The common approach is:

1. Read the JSON file.
2. Modify the Python object.
3. Write the updated object back to the file.

### Example: Update Student Marks

```python
import json

with open("student.json", "r", encoding="utf-8") as file:
    student = json.load(file)

student["marks"] = 95
student["city"] = "Mumbai"

with open("student.json", "w", encoding="utf-8") as file:
    json.dump(student, file, indent=4)

print("Student record updated")
```

**Output:**

```text
Student record updated
```

### Example: Add a New Student

```python
import json

with open("students.json", "r", encoding="utf-8") as file:
    students = json.load(file)

new_student = {
    "id": 4,
    "name": "Rohit",
    "marks": 88
}

students.append(new_student)

with open("students.json", "w", encoding="utf-8") as file:
    json.dump(students, file, indent=4)

print("New student added")
```

---

## 10. Handle JSON Errors

JSON operations can produce errors.

Common exceptions:

| Exception | Reason |
|---|---|
| `json.JSONDecodeError` | Invalid JSON content |
| `FileNotFoundError` | File does not exist |
| `PermissionError` | File access is denied |
| `TypeError` | Unsupported Python object during serialization |

### Example 1: Handle Invalid JSON

```python
import json

data = '{"name": "Raj", "age": 22'

try:
    result = json.loads(data)
    print(result)

except json.JSONDecodeError:
    print("Invalid JSON format")
```

**Output:**

```text
Invalid JSON format
```

### Example 2: Handle Missing JSON File

```python
import json

try:
    with open("unknown.json", "r", encoding="utf-8") as file:
        data = json.load(file)

    print(data)

except FileNotFoundError:
    print("JSON file not found")

except json.JSONDecodeError:
    print("Invalid JSON file")
```

---

## 11. Introduction to CSV

CSV stands for Comma-Separated Values.

CSV is a text format used to store tabular data.

It is commonly used for:

- Excel data.
- Student records.
- Employee information.
- Product inventories.
- Financial reports.
- Data analysis.

### Example CSV Data

```csv
id,name,marks
1,Raj,90
2,Amit,85
3,Neha,95
```

Each row represents a record.

Each column represents a field.

### CSV vs JSON

| Feature | CSV | JSON |
|---|---|---|
| Structure | Rows and columns | Objects and arrays |
| Best for | Tabular data | Structured or nested data |
| Human readability | High | High |
| Nested data | Not naturally supported | Supported |
| Common use | Spreadsheet exchange | APIs and application data |

---

## 12. Introduction to the csv Module

Python provides a built-in `csv` module.

Import it:

```python
import csv
```

Important functions and classes:

| Function / Class | Purpose |
|---|---|
| `csv.reader()` | Read CSV rows |
| `csv.writer()` | Write CSV rows |
| `csv.DictReader()` | Read rows as dictionaries |
| `csv.DictWriter()` | Write dictionaries as CSV rows |

Always use `newline=""` when opening CSV files for reading or writing.

This helps the CSV module handle newline characters correctly.

---

## 13. Read CSV Files Using reader()

The `csv.reader()` function reads CSV data row by row.

### Example 1: Read a CSV File

Create `students.csv`:

```csv
id,name,marks
1,Raj,90
2,Amit,85
3,Neha,95
```

Python code:

```python
import csv

with open("students.csv", "r", newline="", encoding="utf-8") as file:
    reader = csv.reader(file)

    for row in reader:
        print(row)
```

**Output:**

```text
['id', 'name', 'marks']
['1', 'Raj', '90']
['2', 'Amit', '85']
['3', 'Neha', '95']
```

Notice that CSV reader returns each row as a list of strings.

### Example 2: Skip the Header

```python
import csv

with open("students.csv", "r", newline="", encoding="utf-8") as file:
    reader = csv.reader(file)

    header = next(reader)

    print("Columns:", header)

    for row in reader:
        print(row)
```

**Output:**

```text
Columns: ['id', 'name', 'marks']
['1', 'Raj', '90']
['2', 'Amit', '85']
['3', 'Neha', '95']
```

### Example 3: Access Individual Columns

```python
import csv

with open("students.csv", "r", newline="", encoding="utf-8") as file:
    reader = csv.reader(file)

    next(reader)

    for row in reader:
        student_id = row[0]
        name = row[1]
        marks = int(row[2])

        print(name, marks)
```

**Output:**

```text
Raj 90
Amit 85
Neha 95
```

---

## 14. Write CSV Files Using writer()

The `csv.writer()` function writes rows into a CSV file.

### Example 1: Write Multiple Rows

```python
import csv

students = [
    ["id", "name", "marks"],
    [1, "Raj", 90],
    [2, "Amit", 85],
    [3, "Neha", 95]
]

with open("students_output.csv", "w", newline="", encoding="utf-8") as file:
    writer = csv.writer(file)

    writer.writerows(students)

print("CSV file created")
```

**Output:**

```text
CSV file created
```

The file contains:

```csv
id,name,marks
1,Raj,90
2,Amit,85
3,Neha,95
```

### Example 2: Write One Row at a Time

Use `writerow()` for a single row.

```python
import csv

with open("employees.csv", "w", newline="", encoding="utf-8") as file:
    writer = csv.writer(file)

    writer.writerow(["id", "name", "salary"])
    writer.writerow([1, "Raj", 30000])
    writer.writerow([2, "Amit", 35000])

print("Employee data saved")
```

### Difference Between writerow() and writerows()

| Method | Purpose |
|---|---|
| `writerow()` | Writes one row |
| `writerows()` | Writes multiple rows |

---

## 15. Append Data to a CSV File

Use append mode `"a"` to add new rows without removing existing data.

```python
import csv

new_student = [4, "Rohit", 88]

with open("students_output.csv", "a", newline="", encoding="utf-8") as file:
    writer = csv.writer(file)

    writer.writerow(new_student)

print("New student added")
```

**Output:**

```text
New student added
```

Important: Append mode adds data at the end. Do not write the header again when adding a new record to an existing CSV file.

---

## 16. Read CSV Files Using DictReader()

`csv.DictReader()` reads each row as a dictionary.

The column headers become dictionary keys.

### Example

```python
import csv

with open("students.csv", "r", newline="", encoding="utf-8") as file:
    reader = csv.DictReader(file)

    for row in reader:
        print(row)
```

**Output:**

```text
{'id': '1', 'name': 'Raj', 'marks': '90'}
{'id': '2', 'name': 'Amit', 'marks': '85'}
{'id': '3', 'name': 'Neha', 'marks': '95'}
```

### Access Values Using Column Names

```python
import csv

with open("students.csv", "r", newline="", encoding="utf-8") as file:
    reader = csv.DictReader(file)

    for row in reader:
        print("Name:", row["name"])
        print("Marks:", row["marks"])
```

**Output:**

```text
Name: Raj
Marks: 90
Name: Amit
Marks: 85
Name: Neha
Marks: 95
```

Remember: CSV values are generally read as strings. Convert numeric fields when calculations are required.

---

## 17. Write CSV Files Using DictWriter()

`csv.DictWriter()` writes dictionary records into CSV files.

### Example

```python
import csv

students = [
    {"id": 1, "name": "Raj", "marks": 90},
    {"id": 2, "name": "Amit", "marks": 85},
    {"id": 3, "name": "Neha", "marks": 95}
]

with open("students_dict.csv", "w", newline="", encoding="utf-8") as file:

    fieldnames = ["id", "name", "marks"]

    writer = csv.DictWriter(file, fieldnames=fieldnames)

    writer.writeheader()
    writer.writerows(students)

print("CSV data saved successfully")
```

**Output:**

```text
CSV data saved successfully
```

The file contains:

```csv
id,name,marks
1,Raj,90
2,Amit,85
3,Neha,95
```

### Important Methods

| Method | Purpose |
|---|---|
| `writeheader()` | Writes column names |
| `writerow()` | Writes one dictionary record |
| `writerows()` | Writes multiple dictionary records |

---

## 18. CSV Special Cases

### 18.1 Values Containing Commas

CSV values can contain commas if they are properly quoted.

Example:

```csv
id,name,city
1,Raj,"Mumbai, Maharashtra"
```

The CSV module handles this correctly.

```python
import csv

with open("special.csv", "r", newline="", encoding="utf-8") as file:
    reader = csv.reader(file)

    for row in reader:
        print(row)
```

**Output:**

```text
['id', 'name', 'city']
['1', 'Raj', 'Mumbai, Maharashtra']
```

### 18.2 Custom Delimiter

CSV does not always have to use commas.

Example using a semicolon:

```python
import csv

with open("data.csv", "r", newline="", encoding="utf-8") as file:
    reader = csv.reader(file, delimiter=";")

    for row in reader:
        print(row)
```

### 18.3 Custom Quote Character

```python
import csv

with open("data.csv", "r", newline="", encoding="utf-8") as file:
    reader = csv.reader(file, quotechar="'")

    for row in reader:
        print(row)
```

The quote character must match the format of the file.

### 18.4 CSV Quoting Options

| Constant | Meaning |
|---|---|
| `csv.QUOTE_MINIMAL` | Quote fields only when necessary |
| `csv.QUOTE_ALL` | Quote every field |
| `csv.QUOTE_NONNUMERIC` | Quote non-numeric fields |
| `csv.QUOTE_NONE` | Do not quote fields |

Example:

```python
import csv

with open("quoted.csv", "w", newline="", encoding="utf-8") as file:
    writer = csv.writer(file, quoting=csv.QUOTE_ALL)

    writer.writerow(["Raj", "Mumbai", 90])
```

File content:

```csv
"Raj","Mumbai","90"
```

---

## 19. Update and Delete CSV Records

CSV files do not provide direct database-style update or delete operations.

A common approach is:

1. Read all records.
2. Modify the records in Python.
3. Rewrite the complete file.

### Example: Update Student Marks

```python
import csv

students = []

with open("students.csv", "r", newline="", encoding="utf-8") as file:
    reader = csv.DictReader(file)

    for row in reader:
        if row["id"] == "2":
            row["marks"] = "95"

        students.append(row)

with open("students.csv", "w", newline="", encoding="utf-8") as file:
    fieldnames = ["id", "name", "marks"]

    writer = csv.DictWriter(file, fieldnames=fieldnames)

    writer.writeheader()
    writer.writerows(students)

print("Student updated")
```

### Example: Delete a Student

```python
import csv

students = []

with open("students.csv", "r", newline="", encoding="utf-8") as file:
    reader = csv.DictReader(file)

    for row in reader:
        if row["id"] != "2":
            students.append(row)

with open("students.csv", "w", newline="", encoding="utf-8") as file:
    fieldnames = ["id", "name", "marks"]

    writer = csv.DictWriter(file, fieldnames=fieldnames)

    writer.writeheader()
    writer.writerows(students)

print("Student deleted")
```

For important data, use a temporary file and replace the original only after the new file has been written successfully.

---

## 20. JSON vs CSV in Practical Applications

| Requirement | Recommended Format |
|---|---|
| API request and response | JSON |
| Nested student records | JSON |
| Spreadsheet data | CSV |
| Simple tabular reports | CSV |
| Application configuration | JSON |
| Data exchange with Excel | CSV |
| Hierarchical data | JSON |
| Large relational datasets | Database |

### Important Difference

JSON supports nested objects and arrays naturally.

CSV stores rows and columns, so it is better suited to tabular data.

Neither format automatically provides database features such as indexing, transactions or concurrent record updates.

---

## 21. Common Mistakes and Best Practices

### Mistake 1: Confusing dump() and dumps()

| Method | Purpose |
|---|---|
| `dump()` | Writes JSON into a file |
| `dumps()` | Returns JSON as a string |

### Mistake 2: Confusing load() and loads()

| Method | Purpose |
|---|---|
| `load()` | Reads JSON from a file |
| `loads()` | Reads JSON from a string |

### Mistake 3: Forgetting CSV Values Are Strings

```python
marks = "90"

# Convert before calculations.
marks = int(marks)
```

### Mistake 4: Forgetting newline=""

Use:

```python
open("data.csv", "w", newline="", encoding="utf-8")
```

### Mistake 5: Manually Splitting CSV Rows

Avoid:

```python
row = "1,Raj,90".split(",")
```

This approach fails when fields contain commas inside quoted values.

Use `csv.reader()` or `csv.DictReader()`.

### Mistake 6: Overwriting Existing Data

Opening a file with `"w"` removes its previous contents.

Use `"a"` when appending records.

### Best Practices

- Use UTF-8 encoding.
- Use `with` to manage files.
- Validate input before saving.
- Handle `FileNotFoundError` and `JSONDecodeError`.
- Use indentation for readable JSON files.
- Use `DictReader` and `DictWriter` for named columns.
- Do not store passwords as plain text in JSON or CSV.
- Do not load untrusted pickle files.
- Use a database when records require reliable concurrent updates or complex queries.

---

## 22. Practical Exercises

### Exercise 1: JSON Basics

1. Create a Python dictionary containing student information.
2. Convert it into a JSON string using `dumps()`.
3. Convert a JSON string into a Python dictionary using `loads()`.
4. Create a nested dictionary and serialize it.
5. Display JSON with indentation.
6. Sort JSON keys alphabetically.

### Exercise 2: JSON File Handling

1. Create `students.json`.
2. Store multiple student records.
3. Read and display all records.
4. Add a new student.
5. Update the marks of an existing student.
6. Delete a student by ID.
7. Handle missing files and invalid JSON.

### Exercise 3: CSV Basics

1. Create `employees.csv`.
2. Write five employee records.
3. Read and display all records.
4. Skip the header row.
5. Calculate total salary.
6. Append a new employee.
7. Read records using `DictReader()`.

### Exercise 4: CSV Advanced Operations

1. Write records using `DictWriter()`.
2. Update an employee salary.
3. Delete an employee by ID.
4. Read a file with a custom delimiter.
5. Handle fields containing commas.
6. Export filtered student records into another CSV file.

### Exercise 5: JSON and CSV Conversion

1. Read student data from JSON.
2. Convert JSON records into CSV.
3. Read employee records from CSV.
4. Convert CSV records into JSON.
5. Preserve numeric data by converting values where appropriate.
6. Compare both files and verify that the records match.

---

## 23. Mini Project – Student Data Management and Export System

### Project Description

Create a menu-driven application that stores student records in JSON and CSV formats.

The application should support:

1. Add student.
2. View all students.
3. Search student by ID.
4. Update student marks.
5. Delete student.
6. Export records to CSV.
7. Import records from CSV.
8. Display student statistics.
9. Exit.

### Project Structure

```text
StudentDataSystem/
│
├── main.py
├── students.json
├── students.csv
└── README.md
```

### Step 1: Import Required Modules

Create `main.py`.

```python
import json
import csv
import os
```

### Step 2: Create JSON Storage Functions

```python
def load_students():
    if not os.path.exists("students.json"):
        return []

    try:
        with open("students.json", "r", encoding="utf-8") as file:
            return json.load(file)

    except json.JSONDecodeError:
        print("Invalid JSON file")
        return []


def save_students(students):
    with open("students.json", "w", encoding="utf-8") as file:
        json.dump(students, file, indent=4)
```

### Step 3: Add Student Function

```python
def add_student():
    students = load_students()

    student_id = input("Enter student ID: ").strip()

    if not student_id:
        print("Student ID cannot be empty")
        return

    if any(student["id"] == student_id for student in students):
        print("Student ID already exists")
        return

    name = input("Enter student name: ").strip()

    if not name:
        print("Student name cannot be empty")
        return

    try:
        marks = float(input("Enter marks: "))

        if not 0 <= marks <= 100:
            print("Marks must be between 0 and 100")
            return

    except ValueError:
        print("Enter valid marks")
        return

    student = {
        "id": student_id,
        "name": name,
        "marks": marks
    }

    students.append(student)

    save_students(students)

    print("Student added successfully")
```

### Step 4: View Students Function

```python
def view_students():
    students = load_students()

    if not students:
        print("No student records found")
        return

    print("\nSTUDENT RECORDS")

    for student in students:
        print(
            student["id"],
            student["name"],
            student["marks"]
        )
```

### Step 5: Search Student Function

```python
def search_student():
    students = load_students()

    student_id = input("Enter student ID: ").strip()

    for student in students:
        if student["id"] == student_id:
            print("Student Found")
            print(student)
            return

    print("Student not found")
```

### Step 6: Update Student Function

```python
def update_student():
    students = load_students()

    student_id = input("Enter student ID: ").strip()

    for student in students:
        if student["id"] == student_id:

            try:
                marks = float(input("Enter new marks: "))

                if not 0 <= marks <= 100:
                    print("Marks must be between 0 and 100")
                    return

                student["marks"] = marks

                save_students(students)

                print("Student updated successfully")
                return

            except ValueError:
                print("Invalid marks")
                return

    print("Student not found")
```

### Step 7: Delete Student Function

```python
def delete_student():
    students = load_students()

    student_id = input("Enter student ID: ").strip()

    updated_students = [
        student for student in students
        if student["id"] != student_id
    ]

    if len(updated_students) == len(students):
        print("Student not found")
        return

    save_students(updated_students)

    print("Student deleted successfully")
```

### Step 8: Export JSON Data to CSV

```python
def export_csv():
    students = load_students()

    with open("students.csv", "w", newline="", encoding="utf-8") as file:

        fieldnames = ["id", "name", "marks"]

        writer = csv.DictWriter(
            file,
            fieldnames=fieldnames
        )

        writer.writeheader()
        writer.writerows(students)

    print("Data exported to CSV successfully")
```

### Step 9: Import CSV Data into JSON

```python
def import_csv():
    if not os.path.exists("students.csv"):
        print("CSV file not found")
        return

    try:
        with open("students.csv", "r", newline="", encoding="utf-8") as file:
            reader = csv.DictReader(file)

            required_fields = {"id", "name", "marks"}

            if not reader.fieldnames or not required_fields.issubset(reader.fieldnames):
                print("Invalid CSV columns")
                return

            imported_students = []

            for row in reader:
                student_id = row["id"].strip()
                name = row["name"].strip()
                marks = float(row["marks"])

                if not student_id or not name or not 0 <= marks <= 100:
                    print("Invalid student record found")
                    return

                imported_students.append({
                    "id": student_id,
                    "name": name,
                    "marks": marks
                })

        save_students(imported_students)

        print("CSV data imported successfully")

    except (ValueError, KeyError, csv.Error):
        print("Invalid CSV data")
```

This example replaces the existing JSON records with the imported CSV records. A more advanced version should merge records and handle duplicate IDs.

### Step 10: Student Statistics

```python
def student_statistics():
    students = load_students()

    if not students:
        print("No student records available")
        return

    marks = [student["marks"] for student in students]

    print("Total Students:", len(students))
    print("Average Marks:", sum(marks) / len(marks))
    print("Highest Marks:", max(marks))
    print("Lowest Marks:", min(marks))

    passed = sum(1 for mark in marks if mark >= 40)

    print("Passed Students:", passed)
    print("Failed Students:", len(students) - passed)
```

### Step 11: Create the Main Menu

```python
def main():
    while True:
        print("\n===== STUDENT DATA MANAGEMENT SYSTEM =====")

        print("1. Add Student")
        print("2. View Students")
        print("3. Search Student")
        print("4. Update Student")
        print("5. Delete Student")
        print("6. Export JSON to CSV")
        print("7. Import CSV to JSON")
        print("8. Student Statistics")
        print("9. Exit")

        choice = input("Enter choice: ").strip()

        if choice == "1":
            add_student()

        elif choice == "2":
            view_students()

        elif choice == "3":
            search_student()

        elif choice == "4":
            update_student()

        elif choice == "5":
            delete_student()

        elif choice == "6":
            export_csv()

        elif choice == "7":
            import_csv()

        elif choice == "8":
            student_statistics()

        elif choice == "9":
            print("Thank you for using the system")
            break

        else:
            print("Invalid choice")


if __name__ == "__main__":
    main()
```

### Step 12: Run the Project

```bash
python main.py
```

**Sample Output:**

```text
===== STUDENT DATA MANAGEMENT SYSTEM =====

1. Add Student
2. View Students
3. Search Student
4. Update Student
5. Delete Student
6. Export JSON to CSV
7. Import CSV to JSON
8. Student Statistics
9. Exit

Enter choice: 1

Enter student ID: 101
Enter student name: Raj
Enter marks: 90

Student added successfully
```

### Project Challenges

1. Add student email and city fields.
2. Prevent duplicate student IDs during CSV import.
3. Merge imported CSV records instead of replacing all JSON records.
4. Add sorting by marks.
5. Export only passed students to a separate CSV file.
6. Add a confirmation before deleting a student.
7. Handle malformed records without losing existing data.
8. Create a backup before updating the JSON file.

---

## 24. Trainer Assessment

Ask the student:

1. What is data serialization?
2. What is the difference between serialization and deserialization?
3. What is JSON?
4. What is the difference between JSON and a Python dictionary?
5. What is the difference between `dump()` and `dumps()`?
6. What is the difference between `load()` and `loads()`?
7. Why do we use `indent` in JSON?
8. What is `JSONDecodeError`?
9. What is CSV?
10. What is the difference between `reader()` and `DictReader()`?
11. What is the difference between `writer()` and `DictWriter()`?
12. Why should we use `newline=""` with CSV files?
13. Why are CSV values generally read as strings?
14. How can we update a CSV record?
15. When should we choose JSON instead of CSV?

### Practical Assessment

Ask the student to independently:

- Create and serialize a Python dictionary.
- Read JSON data from a string.
- Create and read a JSON file.
- Update and delete JSON records.
- Create a CSV file using `writer()`.
- Read CSV data using `DictReader()`.
- Convert JSON records into CSV.
- Complete the Student Data Management System.

---

## 25. Completion Criteria

The student should be able to:

- Explain serialization and deserialization.
- Understand JSON structure and data types.
- Use `dumps()` and `loads()`.
- Use `dump()` and `load()` with files.
- Create, read and update JSON records.
- Handle invalid JSON data.
- Read and write CSV files.
- Use `reader()`, `writer()`, `DictReader()` and `DictWriter()`.
- Append, update and delete CSV records.
- Convert data between JSON and CSV.
- Understand when to use JSON and when to use CSV.
- Complete the Student Data Management System.

**Day 36 Completed: JSON, CSV & Data Serialization.**

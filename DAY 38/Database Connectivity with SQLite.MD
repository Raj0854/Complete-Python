
# Day 38 – Database Connectivity with SQLite

## 1. Introduction to Databases

### What is a Database?

A database is an organized collection of information that can be stored, accessed, managed and updated.

Examples of information stored in databases:

- Student records
- Employee details
- Customer information
- Product inventory
- Bank transactions
- Login credentials

### Why Do We Need a Database?

Consider a student management application.

If we store student information in normal Python variables:

```python
student_name = "Rahul"
student_age = 20
student_marks = 85
```

The information exists only while the program is running.

When the program ends, these variables are lost.

A database allows us to store information permanently so that it remains available even after closing the application.

### File Handling vs Database

| File Handling | Database |
|---|---|
| Stores data in files | Stores structured data |
| Searching can require reading file contents | Supports efficient queries |
| Manual data organization | Structured tables |
| Limited relationship support | Supports relationships |
| Suitable for simple storage | Suitable for structured applications |

---

## 2. Understanding SQL

SQL stands for **Structured Query Language**.

SQL is used to communicate with relational databases.

It allows us to:

- Create databases and tables.
- Insert records.
- Retrieve records.
- Update existing records.
- Delete records.
- Filter and sort information.

### Important SQL Commands

| Command | Purpose |
|---|---|
| CREATE | Create database objects |
| INSERT | Add new records |
| SELECT | Retrieve records |
| UPDATE | Modify records |
| DELETE | Remove records |
| ALTER | Change table structure |
| DROP | Remove database objects |

### Example SQL Query

```sql
SELECT * FROM students;
```

This query retrieves all records from the `students` table.

---

## 3. Introduction to SQLite

SQLite is a lightweight relational database management system.

It stores the complete database in a single file.

Example:

```text
school.db
```

### Why Use SQLite?

- No separate database server is required.
- Easy to install and configure.
- Lightweight and fast for many local applications.
- Supports SQL queries.
- Suitable for learning database concepts.
- Included with Python through the `sqlite3` module.

### SQLite vs Other Databases

| SQLite | MySQL | PostgreSQL |
|---|---|---|
| File-based database | Server-based database | Server-based database |
| No separate server required | Requires database server | Requires database server |
| Simple setup | More setup | More setup |
| Good for local applications | Common in web applications | Common in advanced applications |

### Important

SQLite is a real database system, not just a file format. Its database is stored in a file, but it supports SQL, transactions, indexes and relational tables.

---

## 4. Python sqlite3 Module

Python provides a built-in module called `sqlite3`.

We do not need to install any external package to use it.

### Import sqlite3

```python
import sqlite3

print("SQLite module imported successfully!")
```

Expected output:

```text
SQLite module imported successfully!
```

### Check SQLite Version

```python
import sqlite3

print("SQLite Version:", sqlite3.sqlite_version)
```

The version depends on the SQLite library available in the Python installation.

---

## 5. Connecting Python to SQLite

The `sqlite3.connect()` function creates a connection to a database.

### Example 1: Create a Database

```python
import sqlite3

connection = sqlite3.connect("school.db")

print("Database connected successfully!")

connection.close()
```

Expected output:

```text
Database connected successfully!
```

A file named `school.db` will be created in the current working directory if it does not already exist.

### Understanding the Code

- `sqlite3.connect()` creates or opens a database.
- `connection` stores the database connection object.
- `connection.close()` closes the connection.

### Important

If the database file already exists, SQLite opens the existing database instead of creating another one.

### Example 2: In-Memory Database

SQLite can also create a temporary database stored in memory.

```python
import sqlite3

connection = sqlite3.connect(":memory:")

print("In-memory database created!")

connection.close()
```

The in-memory database disappears when its connection is closed.

---

## 6. Understanding Database Cursor

A cursor is an object used to execute SQL queries and retrieve their results.

We create a cursor using:

```python
cursor = connection.cursor()
```

### Example

```python
import sqlite3

connection = sqlite3.connect("school.db")

cursor = connection.cursor()

print("Cursor created successfully!")

connection.close()
```

### Database Connection vs Cursor

| Connection | Cursor |
|---|---|
| Connects Python to the database | Executes SQL queries |
| Manages transactions | Retrieves query results |
| Commits or rolls back changes | Fetches records |

---

## 7. Creating a Database Table

A table stores information in rows and columns.

Example student table:

| id | name | age | marks |
|---|---|---|---|
| 1 | Rahul | 20 | 85 |
| 2 | Priya | 21 | 92 |
| 3 | Amit | 19 | 78 |

### SQL CREATE TABLE

```sql
CREATE TABLE students (
    id INTEGER PRIMARY KEY,
    name TEXT NOT NULL,
    age INTEGER,
    marks REAL
);
```

### Understanding Column Types

| SQLite Type | Purpose |
|---|---|
| INTEGER | Whole numbers |
| REAL | Decimal numbers |
| TEXT | Text values |
| BLOB | Binary data |
| NULL | Missing or unknown value |

SQLite uses flexible typing, so these are its main storage classes rather than rigid column types.

### Understanding Constraints

| Constraint | Purpose |
|---|---|
| PRIMARY KEY | Uniquely identifies a record |
| NOT NULL | Prevents missing values |
| UNIQUE | Prevents duplicate values |
| DEFAULT | Provides a default value |
| CHECK | Validates a condition |
| FOREIGN KEY | Defines a relationship between tables |

### Practical Example

```python
import sqlite3

connection = sqlite3.connect("school.db")

cursor = connection.cursor()

cursor.execute("""
CREATE TABLE IF NOT EXISTS students (
    id INTEGER PRIMARY KEY,
    name TEXT NOT NULL,
    age INTEGER,
    marks REAL
)
""")

connection.commit()

print("Students table created successfully!")

connection.close()
```

Expected output:

```text
Students table created successfully!
```

### What Does IF NOT EXISTS Mean?

It prevents an error if the table already exists.

It does not recreate or modify an existing table.

---

## 8. Inserting Records into a Table

The SQL `INSERT` command adds new records.

### Example SQL Query

```sql
INSERT INTO students (name, age, marks)
VALUES ('Rahul', 20, 85);
```

### Insert Data Using Python

```python
import sqlite3

connection = sqlite3.connect("school.db")

cursor = connection.cursor()

cursor.execute("""
INSERT INTO students (name, age, marks)
VALUES (?, ?, ?)
""", ("Rahul", 20, 85))

connection.commit()

print("Student inserted successfully!")

connection.close()
```

Expected output:

```text
Student inserted successfully!
```

### Understanding the Code

- `execute()` runs an SQL query.
- `?` represents a parameter placeholder.
- The tuple contains values supplied to the query.
- `commit()` saves the database changes.

### Why Use Question Mark Placeholders?

Always use parameterized queries when inserting user-provided values.

Avoid building SQL queries using string concatenation.

**Unsafe example:**

```python
name = input("Enter name: ")

query = "INSERT INTO students (name) VALUES ('" + name + "')"
```

This can create SQL injection vulnerabilities and may break when the input contains special characters.

**Safe example:**

```python
name = input("Enter name: ")

cursor.execute(
    "INSERT INTO students (name) VALUES (?)",
    (name,)
)
```

The database handles the value safely.

---

## 9. Inserting Multiple Records

The `executemany()` method inserts multiple records using one SQL statement.

### Example

```python
import sqlite3

connection = sqlite3.connect("school.db")

cursor = connection.cursor()

students = [
    ("Priya", 21, 92),
    ("Amit", 19, 78),
    ("Neha", 20, 88)
]

cursor.executemany("""
INSERT INTO students (name, age, marks)
VALUES (?, ?, ?)
""", students)

connection.commit()

print("Multiple students inserted successfully!")

connection.close()
```

### Important

Running this example repeatedly inserts duplicate student records because the table allows different IDs for the same name.

For repeated testing, use a fresh database or add a suitable UNIQUE constraint and handle duplicate records.

---

## 10. Retrieving Records Using SELECT

The `SELECT` statement retrieves data from a table.

### Example 1: Retrieve All Records

```python
import sqlite3

connection = sqlite3.connect("school.db")

cursor = connection.cursor()

cursor.execute("SELECT * FROM students")

records = cursor.fetchall()

for record in records:
    print(record)

connection.close()
```

Example output:

```text
(1, 'Rahul', 20, 85.0)
(2, 'Priya', 21, 92.0)
(3, 'Amit', 19, 78.0)
```

The actual IDs and records depend on your database.

### Example 2: Retrieve Selected Columns

```python
import sqlite3

connection = sqlite3.connect("school.db")

cursor = connection.cursor()

cursor.execute("SELECT name, marks FROM students")

records = cursor.fetchall()

for record in records:
    print("Name:", record[0])
    print("Marks:", record[1])

connection.close()
```

### Example 3: Retrieve a Single Record

```python
import sqlite3

connection = sqlite3.connect("school.db")

cursor = connection.cursor()

cursor.execute("SELECT * FROM students WHERE id = ?", (1,))

record = cursor.fetchone()

print(record)

connection.close()
```

### Example 4: Retrieve Records One by One

```python
import sqlite3

connection = sqlite3.connect("school.db")

cursor = connection.cursor()

cursor.execute("SELECT * FROM students")

while True:

    record = cursor.fetchone()

    if record is None:
        break

    print(record)

connection.close()
```

### Important Fetch Methods

| Method | Purpose |
|---|---|
| `fetchone()` | Retrieves one record |
| `fetchmany(n)` | Retrieves up to n records |
| `fetchall()` | Retrieves all remaining records |

---

## 11. Filtering Records Using WHERE

The `WHERE` clause filters records based on a condition.

### Example 1: Find a Student by Name

```python
import sqlite3

connection = sqlite3.connect("school.db")

cursor = connection.cursor()

cursor.execute(
    "SELECT * FROM students WHERE name = ?",
    ("Rahul",)
)

records = cursor.fetchall()

for record in records:
    print(record)

connection.close()
```

### Example 2: Find Students Scoring More Than 80

```python
import sqlite3

connection = sqlite3.connect("school.db")

cursor = connection.cursor()

cursor.execute(
    "SELECT * FROM students WHERE marks > ?",
    (80,)
)

records = cursor.fetchall()

for record in records:
    print(record)

connection.close()
```

### Common SQL Comparison Operators

| Operator | Meaning |
|---|---|
| `=` | Equal |
| `!=` or `<>` | Not equal |
| `>` | Greater than |
| `<` | Less than |
| `>=` | Greater than or equal |
| `<=` | Less than or equal |

### Using AND and OR

```python
cursor.execute("""
SELECT * FROM students
WHERE marks >= ? AND age >= ?
""", (80, 20))
```

This retrieves students whose marks are at least 80 and whose age is at least 20.

---

## 12. Sorting Records Using ORDER BY

The `ORDER BY` clause sorts query results.

### Example 1: Sort by Marks

```python
import sqlite3

connection = sqlite3.connect("school.db")

cursor = connection.cursor()

cursor.execute("""
SELECT * FROM students
ORDER BY marks DESC
""")

for record in cursor.fetchall():
    print(record)

connection.close()
```

### Sorting Options

| Keyword | Purpose |
|---|---|
| ASC | Ascending order |
| DESC | Descending order |

### Example 2: Sort by Name

```python
cursor.execute("""
SELECT * FROM students
ORDER BY name ASC
""")
```

### Example 3: Limit Results

```python
cursor.execute("""
SELECT * FROM students
ORDER BY marks DESC
LIMIT 3
""")
```

This retrieves the top three records based on marks.

---

## 13. Updating Existing Records

The `UPDATE` statement modifies existing data.

### Example: Update Student Marks

```python
import sqlite3

connection = sqlite3.connect("school.db")

cursor = connection.cursor()

cursor.execute("""
UPDATE students
SET marks = ?
WHERE id = ?
""", (95, 1))

connection.commit()

print("Student marks updated successfully!")

connection.close()
```

### Understanding the Code

- `UPDATE` identifies the table.
- `SET` specifies the new value.
- `WHERE` identifies which record to modify.
- `commit()` saves the change.

### Important Warning

Never run an UPDATE query without checking its WHERE condition.

Example:

```sql
UPDATE students SET marks = 95;
```

This updates every record in the table.

---

## 14. Deleting Records

The `DELETE` statement removes records from a table.

### Example

```python
import sqlite3

connection = sqlite3.connect("school.db")

cursor = connection.cursor()

cursor.execute(
    "DELETE FROM students WHERE id = ?",
    (1,)
)

connection.commit()

print("Student deleted successfully!")

connection.close()
```

### Important Warning

This query:

```sql
DELETE FROM students;
```

Deletes every record in the table.

It does not remove the table itself.

To remove the table structure, SQL provides:

```sql
DROP TABLE students;
```

Use destructive queries carefully.

---

## 15. Aggregate Functions

SQL provides aggregate functions to calculate values from multiple records.

| Function | Purpose |
|---|---|
| COUNT() | Counts records |
| SUM() | Calculates total |
| AVG() | Calculates average |
| MAX() | Finds maximum |
| MIN() | Finds minimum |

### Example 1: Count Students

```python
import sqlite3

connection = sqlite3.connect("school.db")

cursor = connection.cursor()

cursor.execute("SELECT COUNT(*) FROM students")

result = cursor.fetchone()

print("Total Students:", result[0])

connection.close()
```

### Example 2: Calculate Average Marks

```python
cursor.execute("SELECT AVG(marks) FROM students")

result = cursor.fetchone()

print("Average Marks:", result[0])
```

### Example 3: Find Highest and Lowest Marks

```python
cursor.execute("""
SELECT MAX(marks), MIN(marks)
FROM students
""")

result = cursor.fetchone()

print("Highest Marks:", result[0])
print("Lowest Marks:", result[1])
```

### Example 4: Calculate Total Marks

```python
cursor.execute("SELECT SUM(marks) FROM students")

result = cursor.fetchone()

print("Total Marks:", result[0])
```

---

## 16. Understanding GROUP BY

The `GROUP BY` clause groups records that have the same value.

Consider an employees table containing department information.

| Employee | Department | Salary |
|---|---|---|
| Rahul | IT | 40000 |
| Priya | HR | 35000 |
| Amit | IT | 45000 |
| Neha | HR | 38000 |

### Example: Count Employees by Department

```sql
SELECT department, COUNT(*)
FROM employees
GROUP BY department;
```

Example result:

```text
HR  2
IT  2
```

### Example: Average Salary by Department

```sql
SELECT department, AVG(salary)
FROM employees
GROUP BY department;
```

### Using HAVING

`HAVING` filters grouped results.

```sql
SELECT department, COUNT(*)
FROM employees
GROUP BY department
HAVING COUNT(*) > 1;
```

**Difference:**

- `WHERE` filters individual records before grouping.
- `HAVING` filters groups after grouping.

---

## 17. Understanding Database Transactions

A transaction is a group of database operations treated as one logical unit.

A transaction should either complete successfully or be rolled back when something goes wrong.

SQLite supports transactions.

### Important Transaction Methods

| Method | Purpose |
|---|---|
| `commit()` | Saves changes |
| `rollback()` | Reverts uncommitted changes |

### Example: Commit

```python
import sqlite3

connection = sqlite3.connect("school.db")

cursor = connection.cursor()

try:

    cursor.execute("""
    INSERT INTO students (name, age, marks)
    VALUES (?, ?, ?)
    """, ("Karan", 21, 90))

    connection.commit()

    print("Transaction committed.")

except sqlite3.Error as error:

    connection.rollback()

    print("Transaction failed:", error)

finally:

    connection.close()
```

### Example: Rollback

```python
import sqlite3

connection = sqlite3.connect("school.db")

cursor = connection.cursor()

try:

    cursor.execute("""
    INSERT INTO students (name, age, marks)
    VALUES (?, ?, ?)
    """, ("Temporary Student", 20, 75))

    raise ValueError("Simulated error")

    connection.commit()

except Exception as error:

    connection.rollback()

    print("Changes rolled back:", error)

finally:

    connection.close()
```

The inserted record is not saved because the transaction was rolled back.

---

## 18. Understanding Primary Keys and Auto Increment

A primary key uniquely identifies each record in a table.

SQLite supports automatically generated integer primary keys.

### Example

```sql
CREATE TABLE employees (
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    name TEXT NOT NULL,
    salary REAL
);
```

### Insert Without Specifying ID

```python
cursor.execute("""
INSERT INTO employees (name, salary)
VALUES (?, ?)
""", ("Rahul", 45000))
```

SQLite automatically generates an ID.

### Get the Last Inserted ID

```python
print("New Employee ID:", cursor.lastrowid)
```

### INTEGER PRIMARY KEY vs AUTOINCREMENT

- `INTEGER PRIMARY KEY` automatically assigns an integer ID when one is not supplied.
- `AUTOINCREMENT` prevents reuse of previously generated ROWIDs in certain circumstances.
- `AUTOINCREMENT` adds overhead and is not necessary for most applications.

---

## 19. Understanding Foreign Keys and Relationships

A foreign key connects one table to another.

Consider two tables:

### Students Table

| id | name |
|---|---|
| 1 | Rahul |
| 2 | Priya |

### Courses Table

| id | student_id | course_name |
|---|---|---|
| 1 | 1 | Python |
| 2 | 1 | SQL |
| 3 | 2 | Java |

Here, `student_id` connects the courses table to the students table.

### Create Related Tables

```python
import sqlite3

connection = sqlite3.connect("school.db")

cursor = connection.cursor()

cursor.execute("PRAGMA foreign_keys = ON")

cursor.execute("""
CREATE TABLE IF NOT EXISTS course_students (
    id INTEGER PRIMARY KEY,
    name TEXT NOT NULL
)
""")

cursor.execute("""
CREATE TABLE IF NOT EXISTS courses (
    id INTEGER PRIMARY KEY,
    student_id INTEGER,
    course_name TEXT NOT NULL,
    FOREIGN KEY (student_id)
        REFERENCES course_students(id)
)
""")

connection.commit()

connection.close()
```

### Important

SQLite foreign-key enforcement must be enabled for each connection using:

```python
connection.execute("PRAGMA foreign_keys = ON")
```

Do this before starting transactions that rely on foreign-key enforcement.

---

## 20. Joining Multiple Tables

A JOIN combines related records from multiple tables.

### INNER JOIN

Returns records where matching values exist in both tables.

```sql
SELECT
    course_students.name,
    courses.course_name
FROM course_students
INNER JOIN courses
ON course_students.id = courses.student_id;
```

Example result:

```text
Rahul  Python
Rahul  SQL
Priya  Java
```

### LEFT JOIN

Returns all records from the left table and matching records from the right table.

If no matching record exists, right-table columns contain NULL.

```sql
SELECT
    course_students.name,
    courses.course_name
FROM course_students
LEFT JOIN courses
ON course_students.id = courses.student_id;
```

### Common JOIN Types

| JOIN | Purpose |
|---|---|
| INNER JOIN | Matching records from both tables |
| LEFT JOIN | All left records and matching right records |
| CROSS JOIN | Every combination of records |
| RIGHT JOIN | All right records and matching left records in supported SQLite versions |

---

## 21. Using SQLite Row Factory

By default, SQLite returns query results as tuples.

We can use `sqlite3.Row` to access columns using their names.

### Example

```python
import sqlite3

connection = sqlite3.connect("school.db")

connection.row_factory = sqlite3.Row

cursor = connection.cursor()

cursor.execute("SELECT * FROM students")

records = cursor.fetchall()

for student in records:

    print("ID:", student["id"])
    print("Name:", student["name"])
    print("Marks:", student["marks"])

connection.close()
```

### Why Use Row Factory?

Without row factory:

```python
print(record[1])
```

With `sqlite3.Row`:

```python
print(record["name"])
```

Named access makes code easier to understand.

---

## 22. Handling SQLite Exceptions

Database operations may fail due to:

- Incorrect SQL syntax
- Missing tables
- Duplicate values
- Constraint violations
- Database access problems
- Invalid database operations

SQLite provides exceptions through the `sqlite3` module.

### Common Exceptions

| Exception | Meaning |
|---|---|
| `sqlite3.Error` | Base database exception |
| `sqlite3.IntegrityError` | Constraint violation |
| `sqlite3.OperationalError` | Operational database error |
| `sqlite3.ProgrammingError` | Incorrect API usage or programming error |
| `sqlite3.DatabaseError` | Database-related error |

### Practical Example

```python
import sqlite3

try:

    connection = sqlite3.connect("school.db")

    cursor = connection.cursor()

    cursor.execute("SELECT * FROM unknown_table")

    records = cursor.fetchall()

    print(records)

except sqlite3.OperationalError as error:

    print("Database operation error:", error)

except sqlite3.Error as error:

    print("Database error:", error)

finally:

    if "connection" in locals():
        connection.close()
```

---

## 23. Using the Connection Context Manager

Python provides a context manager for SQLite connections.

It helps manage transaction completion.

### Example

```python
import sqlite3

with sqlite3.connect("school.db") as connection:

    cursor = connection.cursor()

    cursor.execute("""
    INSERT INTO students (name, age, marks)
    VALUES (?, ?, ?)
    """, ("Anjali", 20, 91))

print("Database operation completed.")
```

### Important

The SQLite connection context manager commits a successful transaction or rolls it back when an exception occurs.

It does **not** automatically close the connection.

If you need deterministic closing, explicitly call `close()` or use `contextlib.closing()` together with the transaction context manager.

---

## 24. Using SQLite with Python CRUD Operations

CRUD stands for:

| Operation | Meaning | SQL Command |
|---|---|---|
| Create | Add new record | INSERT |
| Read | Retrieve record | SELECT |
| Update | Modify record | UPDATE |
| Delete | Remove record | DELETE |

These four operations are used in most database-driven applications.

### Complete CRUD Example

```python
import sqlite3

connection = sqlite3.connect("company.db")

cursor = connection.cursor()

cursor.execute("""
CREATE TABLE IF NOT EXISTS employees (
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    name TEXT NOT NULL,
    salary REAL NOT NULL
)
""")

connection.commit()


# CREATE
cursor.execute("""
INSERT INTO employees (name, salary)
VALUES (?, ?)
""", ("Rahul", 45000))

connection.commit()


# READ
cursor.execute("SELECT * FROM employees")

print("Employee Records:")

for employee in cursor.fetchall():
    print(employee)


# UPDATE
cursor.execute("""
UPDATE employees
SET salary = ?
WHERE name = ?
""", (50000, "Rahul"))

connection.commit()


# DELETE
cursor.execute("""
DELETE FROM employees
WHERE name = ?
""", ("Rahul",))

connection.commit()


connection.close()
```

### Important

This example inserts Rahul every time it runs. It is a demonstration of CRUD operations, not a duplicate-safe employee application.

---

# 25. Mini Project – Student Database Management System

## Project Description

Build a menu-driven Student Database Management System using Python and SQLite.

The application should store student records permanently in a database.

### Features

1. Add student.
2. View all students.
3. Search student by ID.
4. Update student details.
5. Delete student.
6. Display top-performing students.
7. Calculate average marks.
8. Display total student count.
9. Exit application.

### Project Folder Structure

```text
Day-38/
│
├── Day-38-Practical.md
│
└── Student-Database-System/
    │
    ├── main.py
    └── school.db
```

The `school.db` file will be created automatically when the application runs.

## Step 1: Create main.py

```python
import sqlite3


DATABASE_NAME = "school.db"


def get_connection():

    connection = sqlite3.connect(DATABASE_NAME)

    connection.row_factory = sqlite3.Row

    return connection


def create_table():

    with get_connection() as connection:

        connection.execute("""
        CREATE TABLE IF NOT EXISTS students (

            id INTEGER PRIMARY KEY AUTOINCREMENT,

            name TEXT NOT NULL,

            age INTEGER NOT NULL CHECK(age > 0),

            course TEXT NOT NULL,

            marks REAL NOT NULL CHECK(marks >= 0 AND marks <= 100)

        )
        """)


def add_student():

    name = input("Enter student name: ").strip()
    age_input = input("Enter age: ").strip()
    course = input("Enter course: ").strip()
    marks_input = input("Enter marks: ").strip()

    if not name or not course:
        print("Name and course are required.")
        return

    try:

        age = int(age_input)
        marks = float(marks_input)

        if age <= 0:
            print("Age must be positive.")
            return

        if not 0 <= marks <= 100:
            print("Marks must be between 0 and 100.")
            return

        with get_connection() as connection:

            cursor = connection.execute("""
            INSERT INTO students (name, age, course, marks)
            VALUES (?, ?, ?, ?)
            """, (name, age, course, marks))

            print("Student added successfully!")
            print("Student ID:", cursor.lastrowid)

    except ValueError:

        print("Age and marks must be numeric.")

    except sqlite3.Error as error:

        print("Database Error:", error)


def view_students():

    try:

        with get_connection() as connection:

            students = connection.execute("""
            SELECT * FROM students
            ORDER BY id
            """).fetchall()

        if not students:
            print("No student records found.")
            return

        print("\n========== STUDENT RECORDS ==========")

        for student in students:

            print("\nID:", student["id"])
            print("Name:", student["name"])
            print("Age:", student["age"])
            print("Course:", student["course"])
            print("Marks:", student["marks"])

    except sqlite3.Error as error:

        print("Database Error:", error)


def search_student():

    student_id = input("Enter student ID: ").strip()

    if not student_id.isdigit() or int(student_id) <= 0:
        print("Invalid student ID.")
        return

    try:

        with get_connection() as connection:

            student = connection.execute("""
            SELECT * FROM students
            WHERE id = ?
            """, (int(student_id),)).fetchone()

        if student is None:
            print("Student not found.")
            return

        print("\nStudent Details:")
        print("ID:", student["id"])
        print("Name:", student["name"])
        print("Age:", student["age"])
        print("Course:", student["course"])
        print("Marks:", student["marks"])

    except sqlite3.Error as error:

        print("Database Error:", error)


def update_student():

    student_id = input("Enter student ID: ").strip()

    if not student_id.isdigit() or int(student_id) <= 0:
        print("Invalid student ID.")
        return

    name = input("Enter new name: ").strip()
    age_input = input("Enter new age: ").strip()
    course = input("Enter new course: ").strip()
    marks_input = input("Enter new marks: ").strip()

    if not name or not course:
        print("Name and course are required.")
        return

    try:

        age = int(age_input)
        marks = float(marks_input)

        if age <= 0 or not 0 <= marks <= 100:
            print("Invalid age or marks.")
            return

        with get_connection() as connection:

            cursor = connection.execute("""
            UPDATE students

            SET name = ?,
                age = ?,
                course = ?,
                marks = ?

            WHERE id = ?
            """, (
                name,
                age,
                course,
                marks,
                int(student_id)
            ))

            if cursor.rowcount == 0:
                print("Student not found.")
            else:
                print("Student updated successfully!")

    except ValueError:

        print("Age and marks must be numeric.")

    except sqlite3.Error as error:

        print("Database Error:", error)


def delete_student():

    student_id = input("Enter student ID: ").strip()

    if not student_id.isdigit() or int(student_id) <= 0:
        print("Invalid student ID.")
        return

    try:

        with get_connection() as connection:

            cursor = connection.execute("""
            DELETE FROM students
            WHERE id = ?
            """, (int(student_id),))

            if cursor.rowcount == 0:
                print("Student not found.")
            else:
                print("Student deleted successfully!")

    except sqlite3.Error as error:

        print("Database Error:", error)


def display_top_students():

    try:

        with get_connection() as connection:

            students = connection.execute("""
            SELECT * FROM students
            ORDER BY marks DESC
            LIMIT 5
            """).fetchall()

        if not students:
            print("No student records found.")
            return

        print("\n========== TOP STUDENTS ==========")

        for student in students:

            print(
                student["name"],
                "-",
                student["marks"]
            )

    except sqlite3.Error as error:

        print("Database Error:", error)


def display_statistics():

    try:

        with get_connection() as connection:

            result = connection.execute("""
            SELECT
                COUNT(*) AS total_students,
                AVG(marks) AS average_marks,
                MAX(marks) AS highest_marks,
                MIN(marks) AS lowest_marks
            FROM students
            """).fetchone()

        print("\n========== STUDENT STATISTICS ==========")

        print("Total Students:", result["total_students"])
        print("Average Marks:", result["average_marks"])
        print("Highest Marks:", result["highest_marks"])
        print("Lowest Marks:", result["lowest_marks"])

    except sqlite3.Error as error:

        print("Database Error:", error)


def main():

    create_table()

    while True:

        print("\n========== STUDENT DATABASE SYSTEM ==========")

        print("1. Add Student")
        print("2. View All Students")
        print("3. Search Student")
        print("4. Update Student")
        print("5. Delete Student")
        print("6. Display Top Students")
        print("7. Display Statistics")
        print("8. Exit")

        choice = input("\nEnter your choice: ").strip()

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

            display_top_students()

        elif choice == "7":

            display_statistics()

        elif choice == "8":

            print("Thank you for using Student Database System!")
            break

        else:

            print("Invalid choice. Please try again.")


if __name__ == "__main__":

    main()
```

## Step 2: Run the Project

Open the terminal inside the `Student-Database-System` folder.

```bash
python main.py
```

Expected menu:

```text
========== STUDENT DATABASE SYSTEM ==========

1. Add Student
2. View All Students
3. Search Student
4. Update Student
5. Delete Student
6. Display Top Students
7. Display Statistics
8. Exit

Enter your choice:
```

### Example Test

Add the following students:

```text
Name: Rahul
Age: 20
Course: Python
Marks: 85

Name: Priya
Age: 21
Course: Java
Marks: 92

Name: Amit
Age: 19
Course: Python
Marks: 78
```

Then test:

- View all three students.
- Search for Priya using her ID.
- Update Rahul's marks.
- Display the top students.
- Display statistics.
- Delete Amit.
- Close and restart the application.
- Verify that the remaining records are still available.

**Important:** The database file persists after the application closes. This is the main difference between temporary Python variables and database storage.

---

# 26. Student Practice Exercises

## Beginner Level

1. Import the `sqlite3` module.
2. Create a database named `college.db`.
3. Create a table named `courses`.
4. Insert five course records.
5. Retrieve all records using SELECT.
6. Retrieve a record using its ID.
7. Update a course name.
8. Delete a course record.
9. Display the total number of records.
10. Display all records in alphabetical order.

## Intermediate Level

1. Create an employee database.
2. Store employee ID, name, department and salary.
3. Retrieve employees belonging to a particular department.
4. Find employees earning more than 40,000.
5. Display the highest-paid employee.
6. Calculate average salary.
7. Count employees department-wise using GROUP BY.
8. Use parameterized queries for all user inputs.
9. Implement complete CRUD operations.
10. Handle database errors using exception handling.

## Advanced Level

1. Create a library management database.
2. Create separate books and members tables.
3. Connect tables using foreign keys.
4. Display borrowed books using JOIN.
5. Create a bank transaction database.
6. Use transactions to handle multiple related operations.
7. Build an inventory management system.
8. Implement search, filtering and sorting.
9. Use `sqlite3.Row` for named column access.
10. Export selected database records into a CSV file.

---

# 27. Trainer Assessment

Ask the student to explain and demonstrate:

1. What is a database?
2. Why do applications need databases?
3. What is SQL?
4. What is SQLite?
5. What is the difference between SQLite and MySQL?
6. What is the purpose of `sqlite3`?
7. What does `sqlite3.connect()` do?
8. What is a database cursor?
9. What is the purpose of `execute()`?
10. Why do we use `commit()`?
11. What is the difference between `fetchone()` and `fetchall()`?
12. What is a primary key?
13. What is a foreign key?
14. What are SQL constraints?
15. What is SQL injection?
16. Why are parameterized queries important?
17. What is the difference between DELETE and DROP?
18. What is the purpose of WHERE?
19. What is the difference between WHERE and HAVING?
20. What is a JOIN?
21. What is a database transaction?
22. What is the difference between commit and rollback?
23. What is `sqlite3.Row`?
24. How does Python handle SQLite exceptions?

### Practical Assessment

Ask the student to independently:

- Create a database.
- Create multiple related tables.
- Insert records.
- Retrieve and filter records.
- Update and delete records.
- Use aggregate functions.
- Perform JOIN operations.
- Handle transactions.
- Handle database exceptions.
- Build a complete database-driven application.

---

# 28. Completion Criteria

Day 38 is complete when the student can:

- Explain database fundamentals and SQL.
- Understand SQLite and its advantages.
- Connect Python to an SQLite database.
- Create tables and insert records.
- Retrieve and filter database records.
- Update and delete existing records.
- Use sorting and aggregate functions.
- Understand primary keys and foreign keys.
- Perform JOIN operations.
- Use transactions and rollback.
- Write safe parameterized SQL queries.
- Handle SQLite exceptions.
- Build the Student Database Management System independently.

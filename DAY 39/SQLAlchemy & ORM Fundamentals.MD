
# Day 39 – SQLAlchemy & ORM Fundamentals

## 1. Introduction to ORM

### What is ORM?

ORM stands for **Object-Relational Mapping**.

ORM is a programming technique that allows developers to interact with relational databases using programming language objects instead of writing SQL queries for every operation.

In Python, we can use classes and objects to represent database tables and records.

### Understanding ORM with an Example

Suppose we have a database table named `students`.

| id | name | age | marks |
|---|---|---|---|
| 1 | Rahul | 20 | 85 |
| 2 | Priya | 21 | 92 |

Without ORM, we write SQL:

```sql
INSERT INTO students (name, age, marks)
VALUES ('Rahul', 20, 85);
```

With ORM, we can create a Python object:

```python
student = Student(
    name="Rahul",
    age=20,
    marks=85
)

session.add(student)
session.commit()
```

The ORM converts Python operations into the corresponding SQL statements.

### Important ORM Terminology

| Term | Meaning |
|---|---|
| ORM | Object-Relational Mapping |
| Model | Python class representing a database table |
| Object | Individual record represented by a class instance |
| Column | Field in a database table |
| Session | Manages database operations and transactions |
| Engine | Manages database connectivity |
| Query | Request to retrieve or manipulate data |
| Migration | Controlled change to database structure |

---

## 2. Why Do We Need ORM?

Consider a large application with many database tables.

Writing SQL manually for every operation can become difficult to maintain.

ORM provides an object-oriented approach to database operations.

### Advantages of ORM

1. Reduces repetitive SQL code.
2. Allows database operations using Python objects.
3. Supports relationships between tables.
4. Makes application code easier to organize.
5. Supports multiple database systems through different database drivers.
6. Provides tools for transaction management.
7. Helps separate database models from application logic.

### Disadvantages of ORM

1. Requires learning additional concepts.
2. Can generate inefficient SQL if used incorrectly.
3. Complex queries may still require SQL knowledge.
4. Adds an abstraction layer.
5. Debugging generated SQL may require additional understanding.

### SQL vs ORM

| Direct SQL | ORM |
|---|---|
| Uses SQL queries | Uses Python classes and objects |
| More direct control over SQL | Abstracts many SQL operations |
| Requires manual query construction | ORM generates SQL |
| Useful for database-level control | Useful for application development |

**Important:** ORM does not eliminate SQL. Understanding SQL is still essential because the ORM generates SQL queries internally.

---

## 3. Introduction to SQLAlchemy

SQLAlchemy is a popular Python SQL toolkit and Object-Relational Mapper.

It provides two major approaches:

1. SQLAlchemy Core – Work with SQL expressions and database tables.
2. SQLAlchemy ORM – Work with Python classes and objects mapped to database tables.

In this lesson, we will focus mainly on SQLAlchemy ORM.

### Why Use SQLAlchemy?

- Supports SQLite, PostgreSQL, MySQL and other databases.
- Provides object-oriented database operations.
- Supports table relationships.
- Supports transactions.
- Supports SQL query generation.
- Can be used in web applications and backend systems.

### SQLAlchemy Architecture

```text
Python Application
        |
        v
SQLAlchemy ORM
        |
        v
SQLAlchemy Engine
        |
        v
Database Driver
        |
        v
Database
```

---

## 4. Installing SQLAlchemy

SQLAlchemy is a third-party Python package.

Open the terminal:

```bash
python -m pip install SQLAlchemy
```

### Verify Installation

```bash
python -c "import sqlalchemy; print(sqlalchemy.__version__)"
```

Example output:

```text
2.x.x
```

The exact version may differ.

### Import SQLAlchemy

```python
import sqlalchemy

print("SQLAlchemy imported successfully!")
```

Expected output:

```text
SQLAlchemy imported successfully!
```

### Create requirements.txt

```text
SQLAlchemy
```

Install the dependencies:

```bash
python -m pip install -r requirements.txt
```

---

## 5. Understanding SQLAlchemy Engine

An Engine is the main entry point for database connectivity in SQLAlchemy.

It manages connections between the Python application and the database.

### Creating an SQLite Engine

```python
from sqlalchemy import create_engine

engine = create_engine("sqlite:///school.db")

print("Database engine created successfully!")
```

Expected output:

```text
Database engine created successfully!
```

### Understanding the Database URL

```python
sqlite:///school.db
```

This specifies:

- `sqlite` – Database system.
- `///` – Relative SQLite database path.
- `school.db` – Database filename.

### Different Database URLs

SQLite:

```python
sqlite:///school.db
```

In-memory SQLite:

```python
sqlite://
```

PostgreSQL example:

```python
postgresql+psycopg://username:password@localhost:5432/school
```

MySQL example:

```python
mysql+pymysql://username:password@localhost:3306/school
```

The PostgreSQL and MySQL examples require their respective database drivers and running database servers.

### Important Engine Methods

| Method | Purpose |
|---|---|
| `create_engine()` | Creates an engine |
| `engine.connect()` | Opens a connection |
| `engine.begin()` | Opens a connection with a transaction |
| `engine.dispose()` | Releases pooled connections |

An Engine is generally created once and reused throughout the application.

---

## 6. Understanding Declarative Base and Models

In SQLAlchemy ORM, a model is a Python class mapped to a database table.

We use SQLAlchemy's declarative mapping system to define models.

SQLAlchemy 2.x provides `DeclarativeBase` for this purpose.

### Example: Create a Base Class

```python
from sqlalchemy.orm import DeclarativeBase

class Base(DeclarativeBase):
    pass
```

All our ORM model classes will inherit from this Base class.

### Create a Student Model

```python
from sqlalchemy import String, Integer
from sqlalchemy.orm import DeclarativeBase, Mapped, mapped_column


class Base(DeclarativeBase):
    pass


class Student(Base):

    __tablename__ = "students"

    id: Mapped[int] = mapped_column(
        primary_key=True
    )

    name: Mapped[str] = mapped_column(
        String(100)
    )

    age: Mapped[int] = mapped_column(
        Integer
    )
```

### Understanding the Code

- `Student` is a Python class.
- `__tablename__` defines the database table name.
- `id`, `name` and `age` are mapped columns.
- `Mapped` describes the Python type of the mapped attribute.
- `mapped_column()` defines database column configuration.
- `primary_key=True` identifies the primary key.

### Model vs Table

| Python ORM | Database |
|---|---|
| Class | Table |
| Object | Row |
| Attribute | Column |
| Object creation | Record creation |
| Attribute update | Column update |

---

## 7. Creating Tables Using ORM

SQLAlchemy provides `Base.metadata.create_all()` to create tables defined in the model metadata.

### Complete Example

```python
from sqlalchemy import create_engine, String
from sqlalchemy.orm import DeclarativeBase, Mapped, mapped_column


class Base(DeclarativeBase):
    pass


class Student(Base):

    __tablename__ = "students"

    id: Mapped[int] = mapped_column(primary_key=True)

    name: Mapped[str] = mapped_column(String(100))

    age: Mapped[int]


engine = create_engine("sqlite:///school.db")

Base.metadata.create_all(engine)

print("Database tables created successfully!")
```

Expected output:

```text
Database tables created successfully!
```

If the table already exists, `create_all()` does not recreate it.

**Important:** `create_all()` creates missing tables. It does not automatically modify existing table structures when you change a model. For controlled schema changes, use database migrations such as Alembic.

---

## 8. Understanding Session

A Session manages ORM operations between Python objects and the database.

It is used to:

- Add objects.
- Retrieve records.
- Update records.
- Delete records.
- Manage transactions.

### Create a Session

```python
from sqlalchemy import create_engine
from sqlalchemy.orm import sessionmaker

engine = create_engine("sqlite:///school.db")

SessionLocal = sessionmaker(bind=engine)

session = SessionLocal()

print("Database session created!")

session.close()
```

### Session vs Engine

| Engine | Session |
|---|---|
| Manages database connectivity | Manages ORM operations |
| Creates and manages connections | Tracks objects and changes |
| Usually reused | Created for a unit of work |
| Works at database connectivity level | Works at ORM level |

### Best Practice

Create a session for a specific unit of work and close it after completing the operations.

SQLAlchemy also supports:

```python
with SessionLocal() as session:
    pass
```

This closes the session automatically when the block exits. It does not automatically commit changes.

---

## 9. Inserting Records Using ORM

We can insert records by creating model objects and adding them to a session.

### Example

```python
from sqlalchemy import create_engine, String
from sqlalchemy.orm import (
    DeclarativeBase,
    Mapped,
    mapped_column,
    sessionmaker
)


class Base(DeclarativeBase):
    pass


class Student(Base):

    __tablename__ = "students"

    id: Mapped[int] = mapped_column(primary_key=True)

    name: Mapped[str] = mapped_column(String(100))

    age: Mapped[int]


engine = create_engine("sqlite:///school.db")

Base.metadata.create_all(engine)

SessionLocal = sessionmaker(bind=engine)

with SessionLocal() as session:

    student = Student(
        name="Rahul",
        age=20
    )

    session.add(student)

    session.commit()

    print("Student inserted successfully!")
    print("Student ID:", student.id)
```

### Understanding the Process

1. Create a Student object.
2. Add the object to the session.
3. Commit the transaction.
4. SQLAlchemy generates and executes the required INSERT statement.

### Adding Multiple Records

```python
with SessionLocal() as session:

    students = [
        Student(name="Priya", age=21),
        Student(name="Amit", age=19),
        Student(name="Neha", age=20)
    ]

    session.add_all(students)

    session.commit()

    print("Multiple students inserted!")
```

**Important:** Running this example repeatedly creates additional records.

---

## 10. Understanding the Session Object States

SQLAlchemy tracks objects during their lifecycle.

Important object states:

| State | Meaning |
|---|---|
| Transient | Object created but not associated with a session |
| Pending | Object added to a session but not yet inserted |
| Persistent | Object associated with a session and database identity |
| Deleted | Object marked for deletion |
| Detached | Object is no longer associated with its session |

### Example

```python
from sqlalchemy import inspect

with SessionLocal() as session:

    student = Student(
        name="Karan",
        age=22
    )

    print("Before add:", inspect(student).transient)

    session.add(student)

    print("After add:", inspect(student).pending)

    session.flush()

    print("After flush:", inspect(student).persistent)

    session.rollback()
```

### Understanding flush()

`flush()` sends pending changes to the database inside the current transaction.

It does not commit the transaction.

A later rollback can still undo those changes.

---

## 11. Retrieving Records Using ORM

SQLAlchemy 2.x provides the `select()` function for ORM queries.

### Example 1: Retrieve All Students

```python
from sqlalchemy import select

with SessionLocal() as session:

    statement = select(Student)

    result = session.scalars(statement)

    students = result.all()

    for student in students:

        print(student.id)
        print(student.name)
        print(student.age)
```

### Example 2: Retrieve a Student by ID

```python
with SessionLocal() as session:

    student = session.get(Student, 1)

    if student:

        print("Name:", student.name)
        print("Age:", student.age)

    else:

        print("Student not found.")
```

### Example 3: Retrieve the First Matching Student

```python
with SessionLocal() as session:

    statement = select(Student).where(
        Student.name == "Rahul"
    )

    student = session.scalars(statement).first()

    if student:
        print(student.name)
    else:
        print("Student not found.")
```

### Example 4: Retrieve Multiple Matching Records

```python
with SessionLocal() as session:

    statement = select(Student).where(
        Student.age >= 20
    )

    students = session.scalars(statement).all()

    for student in students:
        print(student.name, student.age)
```

---

## 12. Filtering Records Using where()

The `where()` method filters database records.

### Equal Condition

```python
statement = select(Student).where(
    Student.name == "Rahul"
)
```

### Greater Than

```python
statement = select(Student).where(
    Student.age > 20
)
```

### Less Than

```python
statement = select(Student).where(
    Student.age < 25
)
```

### Multiple Conditions Using AND

```python
from sqlalchemy import and_

statement = select(Student).where(
    and_(
        Student.age >= 18,
        Student.age <= 25
    )
)
```

We can also use Python's overloaded `&` operator:

```python
statement = select(Student).where(
    (Student.age >= 18) & (Student.age <= 25)
)
```

### Multiple Conditions Using OR

```python
from sqlalchemy import or_

statement = select(Student).where(
    or_(
        Student.age == 19,
        Student.age == 21
    )
)
```

### IN Operator

```python
statement = select(Student).where(
    Student.age.in_([19, 20, 21])
)
```

### LIKE Operator

```python
statement = select(Student).where(
    Student.name.like("R%")
)
```

This finds names beginning with R.

### NOT EQUAL

```python
statement = select(Student).where(
    Student.name != "Rahul"
)
```

### Execute the Query

```python
with SessionLocal() as session:

    students = session.scalars(statement).all()

    for student in students:
        print(student.name)
```

---

## 13. Sorting and Limiting Records

SQLAlchemy supports sorting using `order_by()`.

### Ascending Order

```python
statement = select(Student).order_by(
    Student.name.asc()
)
```

### Descending Order

```python
statement = select(Student).order_by(
    Student.age.desc()
)
```

### Limit Results

```python
statement = select(Student).limit(5)
```

### Offset Results

```python
statement = select(Student).offset(5).limit(5)
```

This skips the first five records and retrieves the next five.

### Complete Example

```python
with SessionLocal() as session:

    statement = (
        select(Student)
        .order_by(Student.age.desc())
        .limit(5)
    )

    students = session.scalars(statement).all()

    for student in students:
        print(student.name, student.age)
```

---

## 14. Updating Records Using ORM

To update a record, retrieve the object and modify its attributes.

### Example

```python
with SessionLocal() as session:

    student = session.get(Student, 1)

    if student:

        student.name = "Rahul Gupta"
        student.age = 21

        session.commit()

        print("Student updated successfully!")

    else:

        print("Student not found.")
```

### How It Works

1. Retrieve an existing object.
2. Change its attributes.
3. SQLAlchemy tracks the modifications.
4. `commit()` saves the changes.

We do not need to write an UPDATE statement manually for this operation.

---

## 15. Deleting Records Using ORM

The `delete()` method marks an ORM object for deletion.

### Example

```python
with SessionLocal() as session:

    student = session.get(Student, 1)

    if student:

        session.delete(student)

        session.commit()

        print("Student deleted successfully!")

    else:

        print("Student not found.")
```

### Important

`session.delete()` marks an object for deletion.

The actual database change is finalized when the transaction commits.

---

## 16. Understanding Rollback and Transactions

A transaction groups database operations into one logical unit.

SQLAlchemy sessions support transactions.

### Commit

```python
session.commit()
```

Saves the pending changes.

### Rollback

```python
session.rollback()
```

Reverts uncommitted changes.

### Example

```python
with SessionLocal() as session:

    try:

        student = Student(
            name="Temporary Student",
            age=20
        )

        session.add(student)

        session.flush()

        print("Student temporarily inserted.")

        raise ValueError("Simulated error")

        session.commit()

    except Exception as error:

        session.rollback()

        print("Transaction rolled back:", error)
```

The record will not be permanently saved because the transaction is rolled back.

### Important Best Practice

Use:

```python
try:

    session.add(student)

    session.commit()

except Exception:

    session.rollback()

    raise
```

This ensures that a failed transaction is rolled back before the error is propagated.

---

## 17. Understanding One-to-Many Relationships

A one-to-many relationship means one record in a table can be associated with multiple records in another table.

Example:

One department can have many employees.

```text
Department
    |
    |---- Employee 1
    |
    |---- Employee 2
    |
    |---- Employee 3
```

### Database Structure

Departments:

| id | name |
|---|---|
| 1 | IT |
| 2 | HR |

Employees:

| id | name | department_id |
|---|---|---|
| 1 | Rahul | 1 |
| 2 | Priya | 1 |
| 3 | Amit | 2 |

### Define Models

```python
from sqlalchemy import ForeignKey, String
from sqlalchemy.orm import (
    DeclarativeBase,
    Mapped,
    mapped_column,
    relationship
)


class Base(DeclarativeBase):
    pass


class Department(Base):

    __tablename__ = "departments"

    id: Mapped[int] = mapped_column(primary_key=True)

    name: Mapped[str] = mapped_column(String(100))

    employees: Mapped[list["Employee"]] = relationship(
        back_populates="department"
    )


class Employee(Base):

    __tablename__ = "employees"

    id: Mapped[int] = mapped_column(primary_key=True)

    name: Mapped[str] = mapped_column(String(100))

    department_id: Mapped[int] = mapped_column(
        ForeignKey("departments.id")
    )

    department: Mapped["Department"] = relationship(
        back_populates="employees"
    )
```

### Understanding the Relationship

- `ForeignKey()` creates the database-level relationship.
- `relationship()` defines the ORM-level relationship.
- `back_populates` connects both sides of the relationship.

### Create Tables

```python
engine = create_engine("sqlite:///company.db")

Base.metadata.create_all(engine)
```

### Insert Related Records

```python
SessionLocal = sessionmaker(bind=engine)

with SessionLocal() as session:

    department = Department(name="IT")

    employee1 = Employee(name="Rahul")
    employee2 = Employee(name="Priya")

    department.employees.append(employee1)
    department.employees.append(employee2)

    session.add(department)

    session.commit()

    print("Department and employees inserted!")
```

SQLAlchemy handles the relationship between the records.

### Access Related Records

```python
with SessionLocal() as session:

    department = session.get(Department, 1)

    if department:

        print("Department:", department.name)

        for employee in department.employees:
            print(employee.name)
```

---

## 18. Understanding Many-to-Many Relationships

A many-to-many relationship means:

- One student can enroll in multiple courses.
- One course can contain multiple students.

Example:

```text
Student Rahul
    |
    |---- Python
    |
    |---- SQL

Student Priya
    |
    |---- Python
    |
    |---- Java
```

A junction table connects both tables.

### Association Table

```python
from sqlalchemy import Table, Column, ForeignKey

student_courses = Table(
    "student_courses",
    Base.metadata,

    Column(
        "student_id",
        ForeignKey("students.id"),
        primary_key=True
    ),

    Column(
        "course_id",
        ForeignKey("courses.id"),
        primary_key=True
    )
)
```

### Define Models

```python
from sqlalchemy import String
from sqlalchemy.orm import Mapped, mapped_column, relationship


class Student(Base):

    __tablename__ = "students"

    id: Mapped[int] = mapped_column(primary_key=True)

    name: Mapped[str] = mapped_column(String(100))

    courses: Mapped[list["Course"]] = relationship(
        secondary=student_courses,
        back_populates="students"
    )


class Course(Base):

    __tablename__ = "courses"

    id: Mapped[int] = mapped_column(primary_key=True)

    title: Mapped[str] = mapped_column(String(100))

    students: Mapped[list["Student"]] = relationship(
        secondary=student_courses,
        back_populates="courses"
    )
```

### Important

This is a separate model example. Do not define another `Student` class with the same table name in the same metadata as the earlier Student model. Use a separate project or combine the model definitions carefully.

### Add a Course to a Student

```python
with SessionLocal() as session:

    student = Student(name="Rahul")

    course = Course(title="Python")

    student.courses.append(course)

    session.add(student)

    session.commit()
```

---

## 19. Understanding Model Constraints and Defaults

SQLAlchemy supports database constraints and default values.

### Example

```python
from sqlalchemy import String, CheckConstraint
from sqlalchemy.orm import Mapped, mapped_column


class Product(Base):

    __tablename__ = "products"

    id: Mapped[int] = mapped_column(primary_key=True)

    name: Mapped[str] = mapped_column(
        String(100),
        nullable=False
    )

    price: Mapped[float] = mapped_column(
        nullable=False
    )

    stock: Mapped[int] = mapped_column(
        default=0
    )

    __table_args__ = (
        CheckConstraint(
            "price >= 0",
            name="check_product_price"
        ),
    )
```

### Important Column Options

| Option | Purpose |
|---|---|
| `primary_key=True` | Marks primary key |
| `nullable=False` | Prevents NULL |
| `unique=True` | Prevents duplicate values |
| `default=` | Python-side default |
| `server_default=` | Database-side default |
| `index=True` | Creates an index |
| `ForeignKey()` | References another table |

**Important:** A Python-side `default` is applied by SQLAlchemy when it constructs an INSERT. A `server_default` is defined at the database level.

---

## 20. Understanding Database Indexes

An index helps a database locate records more efficiently.

Imagine searching for a student's email in a table containing thousands of records.

Without an index, the database may need to inspect many rows.

An index can speed up searches on frequently queried columns.

### Create an Indexed Column

```python
email: Mapped[str] = mapped_column(
    String(150),
    unique=True,
    index=True
)
```

### Advantages

- Faster searches for suitable queries.
- Better performance for some filtering operations.
- Can improve lookup and join performance.

### Disadvantages

- Requires additional storage.
- Adds overhead to INSERT, UPDATE and DELETE operations.
- Too many indexes can reduce performance.

Create indexes based on actual query patterns, not on every column.

---

## 21. Understanding SQLAlchemy Core vs ORM

SQLAlchemy provides two main ways to work with databases.

### SQLAlchemy Core

Core focuses on database tables, SQL expressions and connections.

Example:

```python
from sqlalchemy import create_engine, MetaData, Table, Column, Integer, String, insert, select

engine = create_engine("sqlite:///core.db")

metadata = MetaData()

students = Table(
    "students",
    metadata,

    Column("id", Integer, primary_key=True),

    Column("name", String(100)),

    Column("age", Integer)
)

metadata.create_all(engine)

with engine.begin() as connection:

    connection.execute(
        insert(students),
        {
            "name": "Rahul",
            "age": 20
        }
    )

    result = connection.execute(
        select(students)
    )

    for record in result:
        print(record)
```

### SQLAlchemy ORM

ORM focuses on Python classes and objects.

Example:

```python
student = Student(
    name="Rahul",
    age=20
)

session.add(student)

session.commit()
```

### Comparison

| SQLAlchemy Core | SQLAlchemy ORM |
|---|---|
| Table-oriented | Object-oriented |
| Uses SQL expressions | Uses mapped Python classes |
| More direct database control | Manages object persistence |
| Useful for SQL-heavy operations | Useful for domain-based applications |

---

## 22. Understanding Database Migrations

A database migration is a controlled change to an existing database structure.

Examples:

- Adding a new column.
- Removing a column.
- Renaming a column.
- Creating a new table.
- Changing a relationship.

Changing a Python model does not automatically update an existing database table.

For production applications, developers commonly use **Alembic**, a database migration tool that works with SQLAlchemy.

### Install Alembic

```bash
python -m pip install alembic
```

### Initialize Alembic

```bash
alembic init migrations
```

This creates a migration configuration and a migrations directory.

### Important Commands

```bash
alembic revision --autogenerate -m "Create student table"
```

Generates a migration based on detected model changes.

```bash
alembic upgrade head
```

Applies available migrations.

```bash
alembic downgrade -1
```

Reverts the latest migration where supported by the migration script.

**Important:** Autogenerated migrations must be reviewed before applying them. Alembic cannot reliably infer every intended schema change, especially certain column renames or data transformations.

---

# 23. Mini Project – SQLAlchemy Student Management System

## Project Description

Create a menu-driven Student Management System using SQLAlchemy ORM and SQLite.

Instead of writing SQL queries directly for every CRUD operation, use Python model classes and SQLAlchemy sessions.

### Features

1. Add student.
2. View all students.
3. Search student by ID.
4. Search students by name.
5. Update student details.
6. Delete student.
7. Display top students.
8. Calculate student statistics.
9. Exit application.

### Project Structure

```text
Day-39/
│
├── Day-39-Practical.md
│
└── Student-ORM-System/
    │
    ├── main.py
    ├── database.py
    ├── models.py
    ├── operations.py
    ├── requirements.txt
    └── school.db
```

The database file will be created automatically.

## Step 1: Create requirements.txt

```text
SQLAlchemy
```

Install:

```bash
python -m pip install -r requirements.txt
```

## Step 2: Create database.py

This file manages database connectivity and session creation.

```python
from sqlalchemy import create_engine
from sqlalchemy.orm import sessionmaker, DeclarativeBase


DATABASE_URL = "sqlite:///school.db"


engine = create_engine(
    DATABASE_URL,
    echo=False
)


class Base(DeclarativeBase):
    pass


SessionLocal = sessionmaker(
    bind=engine
)


def get_session():

    return SessionLocal()
```

## Step 3: Create models.py

This file defines the database model.

```python
from sqlalchemy import String, CheckConstraint
from sqlalchemy.orm import Mapped, mapped_column

from database import Base


class Student(Base):

    __tablename__ = "students"

    id: Mapped[int] = mapped_column(
        primary_key=True
    )

    name: Mapped[str] = mapped_column(
        String(100),
        nullable=False
    )

    age: Mapped[int] = mapped_column(
        nullable=False
    )

    course: Mapped[str] = mapped_column(
        String(100),
        nullable=False
    )

    marks: Mapped[float] = mapped_column(
        nullable=False
    )

    __table_args__ = (
        CheckConstraint(
            "age > 0",
            name="check_student_age"
        ),

        CheckConstraint(
            "marks >= 0 AND marks <= 100",
            name="check_student_marks"
        ),
    )
```

## Step 4: Create operations.py

This file contains database operations.

```python
from sqlalchemy import select, func

from database import get_session
from models import Student


def add_student(name, age, course, marks):

    with get_session() as session:

        student = Student(
            name=name,
            age=age,
            course=course,
            marks=marks
        )

        session.add(student)

        session.commit()

        print("Student added successfully!")
        print("Student ID:", student.id)


def view_students():

    with get_session() as session:

        students = session.scalars(
            select(Student).order_by(Student.id)
        ).all()

        if not students:

            print("No students found.")
            return

        for student in students:

            print("\nID:", student.id)
            print("Name:", student.name)
            print("Age:", student.age)
            print("Course:", student.course)
            print("Marks:", student.marks)


def search_student(student_id):

    with get_session() as session:

        student = session.get(Student, student_id)

        if student is None:

            print("Student not found.")
            return

        print("\nID:", student.id)
        print("Name:", student.name)
        print("Age:", student.age)
        print("Course:", student.course)
        print("Marks:", student.marks)


def search_by_name(name):

    with get_session() as session:

        statement = select(Student).where(
            Student.name.ilike(f"%{name}%")
        )

        students = session.scalars(statement).all()

        if not students:

            print("No matching students found.")
            return

        for student in students:

            print(
                student.id,
                student.name,
                student.course,
                student.marks
            )


def update_student(student_id, name, age, course, marks):

    with get_session() as session:

        student = session.get(Student, student_id)

        if student is None:

            print("Student not found.")
            return

        student.name = name
        student.age = age
        student.course = course
        student.marks = marks

        session.commit()

        print("Student updated successfully!")


def delete_student(student_id):

    with get_session() as session:

        student = session.get(Student, student_id)

        if student is None:

            print("Student not found.")
            return

        session.delete(student)

        session.commit()

        print("Student deleted successfully!")


def display_top_students():

    with get_session() as session:

        statement = (
            select(Student)
            .order_by(Student.marks.desc())
            .limit(5)
        )

        students = session.scalars(statement).all()

        if not students:

            print("No students found.")
            return

        print("\n========== TOP STUDENTS ==========")

        for student in students:

            print(
                student.name,
                "-",
                student.marks
            )


def display_statistics():

    with get_session() as session:

        statement = select(
            func.count(Student.id),
            func.avg(Student.marks),
            func.max(Student.marks),
            func.min(Student.marks)
        )

        result = session.execute(statement).one()

        print("\n========== STATISTICS ==========")

        print("Total Students:", result[0])
        print("Average Marks:", result[1])
        print("Highest Marks:", result[2])
        print("Lowest Marks:", result[3])
```

**Note:** SQLite's `LIKE` behavior is generally case-insensitive for ASCII characters. The `ilike()` method is SQLAlchemy's case-insensitive matching operator; exact behavior can depend on the database backend.

## Step 5: Create main.py

This file handles user interaction.

```python
from sqlalchemy import create_engine

from database import Base, engine
from operations import (
    add_student,
    view_students,
    search_student,
    search_by_name,
    update_student,
    delete_student,
    display_top_students,
    display_statistics
)


def initialize_database():

    Base.metadata.create_all(engine)


def get_student_id():

    value = input("Enter student ID: ").strip()

    if not value.isdigit() or int(value) <= 0:

        print("Invalid student ID.")
        return None

    return int(value)


def get_student_details():

    name = input("Enter name: ").strip()
    age_input = input("Enter age: ").strip()
    course = input("Enter course: ").strip()
    marks_input = input("Enter marks: ").strip()

    if not name or not course:

        print("Name and course are required.")
        return None

    try:

        age = int(age_input)
        marks = float(marks_input)

        if age <= 0:

            print("Age must be positive.")
            return None

        if not 0 <= marks <= 100:

            print("Marks must be between 0 and 100.")
            return None

        return name, age, course, marks

    except ValueError:

        print("Age and marks must be numeric.")
        return None


def main():

    initialize_database()

    while True:

        print("\n========== STUDENT ORM SYSTEM ==========")

        print("1. Add Student")
        print("2. View All Students")
        print("3. Search Student by ID")
        print("4. Search Student by Name")
        print("5. Update Student")
        print("6. Delete Student")
        print("7. Display Top Students")
        print("8. Display Statistics")
        print("9. Exit")

        choice = input("\nEnter choice: ").strip()

        try:

            if choice == "1":

                details = get_student_details()

                if details:
                    add_student(*details)

            elif choice == "2":

                view_students()

            elif choice == "3":

                student_id = get_student_id()

                if student_id is not None:
                    search_student(student_id)

            elif choice == "4":

                name = input("Enter student name: ").strip()

                if name:
                    search_by_name(name)
                else:
                    print("Name cannot be empty.")

            elif choice == "5":

                student_id = get_student_id()

                if student_id is None:
                    continue

                details = get_student_details()

                if details:
                    update_student(student_id, *details)

            elif choice == "6":

                student_id = get_student_id()

                if student_id is not None:
                    delete_student(student_id)

            elif choice == "7":

                display_top_students()

            elif choice == "8":

                display_statistics()

            elif choice == "9":

                print("Thank you for using Student ORM System!")
                break

            else:

                print("Invalid choice.")

        except Exception as error:

            print("Operation failed:", error)


if __name__ == "__main__":

    main()
```

## Step 6: Run the Project

Open the terminal inside the `Student-ORM-System` folder.

```bash
python main.py
```

Expected menu:

```text
========== STUDENT ORM SYSTEM ==========

1. Add Student
2. View All Students
3. Search Student by ID
4. Search Student by Name
5. Update Student
6. Delete Student
7. Display Top Students
8. Display Statistics
9. Exit

Enter choice:
```

### Test the Application

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

- View all students.
- Search for a student by ID.
- Search by name.
- Update a student's marks.
- Delete a student.
- Display top students.
- Display statistics.
- Close and reopen the application.
- Verify that records remain stored.

### Important Project Notes

1. SQLAlchemy automatically generates SQL statements for ORM operations.
2. The `school.db` file stores the records.
3. The models are defined in `models.py`.
4. Database connectivity is managed in `database.py`.
5. CRUD operations are separated into `operations.py`.
6. `main.py` handles the user interface.
7. The project uses SQLite, so no external database server is required.

---

# 24. Student Practice Exercises

## Beginner Level

1. Install SQLAlchemy.
2. Create an SQLite engine.
3. Define a `Product` model.
4. Create a database table using `create_all()`.
5. Insert five product objects.
6. Retrieve all products.
7. Search for a product by ID.
8. Update a product price.
9. Delete a product.
10. Print all products in ascending order.

## Intermediate Level

1. Create an Employee model with name, department and salary.
2. Retrieve employees with salary above 40,000.
3. Find the employee with the highest salary.
4. Calculate average employee salary.
5. Search employees by department.
6. Implement complete CRUD operations.
7. Use session rollback when an error occurs.
8. Add unique and NOT NULL constraints.
9. Create a Department and Employee one-to-many relationship.
10. Retrieve all employees belonging to a department.

## Advanced Level

1. Create a Library Management System using SQLAlchemy.
2. Create Book and Author models.
3. Implement a one-to-many relationship.
4. Create Student and Course models with a many-to-many relationship.
5. Use aggregate functions with SQLAlchemy.
6. Implement sorting, filtering and pagination.
7. Compare SQLAlchemy Core and ORM.
8. Display generated SQL using `echo=True`.
9. Create an Alembic migration for a new column.
10. Build a complete Employee Management System using ORM.

---

# 25. Trainer Assessment

Ask the student to explain and demonstrate:

1. What is ORM?
2. What is SQLAlchemy?
3. What is the difference between SQL and ORM?
4. What is SQLAlchemy Core?
5. What is SQLAlchemy ORM?
6. What is an Engine?
7. What is a Model?
8. What is `DeclarativeBase`?
9. What is `mapped_column()`?
10. What is a Session?
11. What is the difference between Engine and Session?
12. What does `session.add()` do?
13. What does `session.commit()` do?
14. What does `session.rollback()` do?
15. What is the difference between `flush()` and `commit()`?
16. How do we retrieve records using `select()`?
17. What is a one-to-many relationship?
18. What is a many-to-many relationship?
19. What is a ForeignKey?
20. What is `relationship()`?
21. What are database indexes?
22. What is the purpose of Alembic?
23. Does changing a model automatically update an existing table?
24. Why is SQL knowledge still important when using ORM?

### Practical Assessment

Ask the student to independently:

- Install SQLAlchemy.
- Create an engine.
- Define ORM models.
- Create database tables.
- Insert and retrieve records.
- Filter and sort records.
- Update and delete records.
- Implement relationships.
- Manage transactions.
- Build a complete ORM-based application.

---

# 26. Completion Criteria

Day 39 is complete when the student can:

- Explain ORM fundamentals.
- Understand SQLAlchemy architecture.
- Install and configure SQLAlchemy.
- Create an SQLite engine.
- Define models using declarative mapping.
- Create database tables.
- Manage database sessions.
- Perform CRUD operations using ORM.
- Filter, sort and limit records.
- Manage transactions using commit and rollback.
- Understand one-to-many and many-to-many relationships.
- Use constraints and indexes.
- Explain SQLAlchemy Core vs ORM.
- Understand the purpose of database migrations.
- Build the Student ORM Management System independently.

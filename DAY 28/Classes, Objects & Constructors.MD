
# Day 28 – Classes, Objects & Constructors

## 1. Recap of Classes and Objects

In the previous lesson, we learned that:

- A class is a blueprint used to create objects.
- An object is an instance of a class.
- Attributes store object data.
- Methods define object behavior.
- `self` refers to the current object.

Example:

```python
class Student:

    def display(self):
        print("Student Name:", self.name)


student1 = Student()

student1.name = "Raj"

student1.display()
```

Output:

```text
Student Name: Raj
```

In this lesson, we will learn how to initialize object data automatically when an object is created.

---

## 2. What Is a Constructor?

A constructor is a special method associated with object initialization.

In Python, `__init__()` is commonly called the initializer method.

It runs automatically after a new object has been created.

We use it to initialize an object's attributes.

### Syntax

```python
class ClassName:

    def __init__(self):
        # Initialization code
        pass
```

### Example

```python
class Student:

    def __init__(self):
        print("Student object initialized")


student1 = Student()
student2 = Student()
```

Output:

```text
Student object initialized
Student object initialized
```

The `__init__()` method runs automatically for each newly created object.

### Important Note

Technically:

- `__new__()` creates and returns a new object.
- `__init__()` initializes the already-created object.

For beginner-level Python development, we generally use `__init__()` to initialize object attributes.

---

## 3. Understanding __init__()

The `__init__()` method is defined inside a class.

It receives `self` as its first parameter.

Example:

```python
class Student:

    def __init__(self):
        self.name = "Raj"
        self.age = 21

    def display(self):
        print("Name:", self.name)
        print("Age:", self.age)


student1 = Student()

student1.display()
```

Output:

```text
Name: Raj
Age: 21
```

### Explanation

1. Python creates a new `Student` object.
2. Python calls `__init__()` automatically.
3. `self` refers to the newly created object.
4. `self.name` stores the student's name.
5. `self.age` stores the student's age.
6. The `display()` method accesses these attributes.

We do not need to assign the attributes separately after creating the object.

---

## 4. Constructor with Parameters

We can pass values to a constructor to initialize different objects with different data.

Example:

```python
class Student:

    def __init__(self, name, age):
        self.name = name
        self.age = age

    def display(self):
        print("Name:", self.name)
        print("Age:", self.age)


student1 = Student("Raj", 21)
student2 = Student("Aman", 22)

student1.display()
student2.display()
```

Output:

```text
Name: Raj
Age: 21
Name: Aman
Age: 22
```

### Understanding the Parameters

```python
def __init__(self, name, age):
    self.name = name
    self.age = age
```

- `self` refers to the current object.
- `name` receives the value passed during object creation.
- `age` receives the age passed during object creation.
- `self.name` stores the value as an instance attribute.
- `self.age` stores the value as an instance attribute.

When we write:

```python
student1 = Student("Raj", 21)
```

Python automatically passes the new object as `self`.

We provide only `"Raj"` and `21` as arguments.

---

## 5. Default Parameters in Constructors

Constructors can also use default parameter values.

Example:

```python
class Student:

    def __init__(self, name, age=18):
        self.name = name
        self.age = age

    def display(self):
        print("Name:", self.name)
        print("Age:", self.age)


student1 = Student("Raj", 21)
student2 = Student("Aman")

student1.display()
student2.display()
```

Output:

```text
Name: Raj
Age: 21
Name: Aman
Age: 18
```

If an age is not provided, Python uses the default value of `18`.

### Multiple Default Parameters

```python
class Employee:

    def __init__(self, name, department="General", salary=20000):
        self.name = name
        self.department = department
        self.salary = salary

    def display(self):
        print("Name:", self.name)
        print("Department:", self.department)
        print("Salary:", self.salary)


employee1 = Employee("Raj", "IT", 40000)
employee2 = Employee("Aman")

employee1.display()
employee2.display()
```

Output:

```text
Name: Raj
Department: IT
Salary: 40000
Name: Aman
Department: General
Salary: 20000
```

Remember that parameters without default values must come before parameters with default values.

---

## 6. Positional and Keyword Arguments in Constructors

We can pass constructor arguments using positional or keyword arguments.

### 6.1 Positional Arguments

Values are assigned according to their position.

```python
class Employee:

    def __init__(self, name, age, salary):
        self.name = name
        self.age = age
        self.salary = salary


employee1 = Employee("Raj", 21, 30000)

print(employee1.name)
print(employee1.age)
print(employee1.salary)
```

Output:

```text
Raj
21
30000
```

### 6.2 Keyword Arguments

Values are assigned using parameter names.

```python
class Employee:

    def __init__(self, name, age, salary):
        self.name = name
        self.age = age
        self.salary = salary


employee1 = Employee(
    salary=40000,
    name="Aman",
    age=22
)

print(employee1.name)
print(employee1.age)
print(employee1.salary)
```

Output:

```text
Aman
22
40000
```

Keyword arguments improve readability when a constructor has several parameters.

---

## 7. Instance Attributes

Instance attributes belong to individual objects.

Every object can maintain its own attribute values.

They are commonly initialized using `self` inside `__init__()`.

Example:

```python
class Student:

    def __init__(self, name, marks):
        self.name = name
        self.marks = marks


student1 = Student("Raj", 85)
student2 = Student("Aman", 92)

print(student1.name, student1.marks)
print(student2.name, student2.marks)
```

Output:

```text
Raj 85
Aman 92
```

Both objects have their own `name` and `marks` attributes.

### Updating Instance Attributes

```python
class Student:

    def __init__(self, name, marks):
        self.name = name
        self.marks = marks


student1 = Student("Raj", 85)

print("Before:", student1.marks)

student1.marks = 95

print("After:", student1.marks)
```

Output:

```text
Before: 85
After: 95
```

Instance attributes can be updated after object creation.

### Adding an Attribute After Object Creation

```python
class Student:

    def __init__(self, name):
        self.name = name


student1 = Student("Raj")

student1.city = "Mumbai"

print(student1.name)
print(student1.city)
```

Output:

```text
Raj
Mumbai
```

Python generally allows instance attributes to be added dynamically, unless the class restricts this behavior using mechanisms such as `__slots__`.

---

## 8. Class Attributes

Class attributes are defined directly inside the class, outside instance methods.

They are associated with the class and are accessible through the class itself or its instances.

Example:

```python
class Student:

    school_name = "ABC Public School"

    def __init__(self, name):
        self.name = name


student1 = Student("Raj")
student2 = Student("Aman")

print(Student.school_name)
print(student1.school_name)
print(student2.school_name)
```

Output:

```text
ABC Public School
ABC Public School
ABC Public School
```

All three accesses refer to the same class attribute.

### Updating a Class Attribute

```python
class Student:

    school_name = "ABC School"

    def __init__(self, name):
        self.name = name


student1 = Student("Raj")
student2 = Student("Aman")

Student.school_name = "XYZ School"

print(student1.school_name)
print(student2.school_name)
```

Output:

```text
XYZ School
XYZ School
```

Changing the attribute through the class updates the value used by instances that do not have their own attribute with the same name.

### Important: Class Attribute Shadowing

When we assign an attribute through an instance, Python can create an instance attribute with the same name.

Example:

```python
class Student:

    school_name = "ABC School"

    def __init__(self, name):
        self.name = name


student1 = Student("Raj")
student2 = Student("Aman")

student1.school_name = "Private School"

print(student1.school_name)
print(student2.school_name)
print(Student.school_name)
```

Output:

```text
Private School
ABC School
ABC School
```

Here:

- `Student.school_name` is the class attribute.
- `student1.school_name` is an instance attribute.
- `student2` still reads the class attribute.

This behavior is called attribute shadowing.

---

## 9. Instance Attributes vs Class Attributes

| Instance Attributes | Class Attributes |
|---|---|
| Belong to individual objects | Belong to the class |
| Usually initialized using `self` | Defined directly inside the class |
| Can have different values for each object | Shared when accessed through instances without shadowing |
| Accessed using object references | Accessed using class or object references |
| Example: Student name | Example: School name |

### Combined Example

```python
class Employee:

    company = "Tech Solutions"

    def __init__(self, name, salary):
        self.name = name
        self.salary = salary

    def display(self):
        print("Company:", Employee.company)
        print("Name:", self.name)
        print("Salary:", self.salary)


employee1 = Employee("Raj", 40000)
employee2 = Employee("Aman", 50000)

employee1.display()
employee2.display()
```

Output:

```text
Company: Tech Solutions
Name: Raj
Salary: 40000
Company: Tech Solutions
Name: Aman
Salary: 50000
```

---

## 10. The __dict__ Attribute

Python objects commonly provide a `__dict__` attribute containing their instance attributes.

Example:

```python
class Student:

    school = "ABC School"

    def __init__(self, name, age):
        self.name = name
        self.age = age


student1 = Student("Raj", 21)

print(student1.__dict__)
print(Student.__dict__["school"])
```

Output:

```text
{'name': 'Raj', 'age': 21}
ABC School
```

Notice:

- `student1.__dict__` contains instance attributes.
- The class dictionary contains class attributes and other class information.

Not every Python object has an instance `__dict__`; for example, classes using `__slots__` can restrict it.

---

## 11. Multiple Objects with a Single Class

A single class can create many independent objects.

Example:

```python
class Product:

    category = "Electronics"

    def __init__(self, name, price):
        self.name = name
        self.price = price

    def display(self):
        print("Category:", Product.category)
        print("Product:", self.name)
        print("Price:", self.price)


product1 = Product("Laptop", 55000)
product2 = Product("Keyboard", 1500)
product3 = Product("Mouse", 800)

products = [product1, product2, product3]

for product in products:
    product.display()
    print("----------------")
```

Output:

```text
Category: Electronics
Product: Laptop
Price: 55000
----------------
Category: Electronics
Product: Keyboard
Price: 1500
----------------
Category: Electronics
Product: Mouse
Price: 800
----------------
```

This is useful when managing multiple records of the same type.

---

## 12. Constructor Initialization with Calculations

A constructor can perform calculations while initializing object attributes.

Example:

```python
class Rectangle:

    def __init__(self, length, width):
        self.length = length
        self.width = width

        self.area = length * width
        self.perimeter = 2 * (length + width)

    def display(self):
        print("Length:", self.length)
        print("Width:", self.width)
        print("Area:", self.area)
        print("Perimeter:", self.perimeter)


rectangle1 = Rectangle(10, 5)

rectangle1.display()
```

Output:

```text
Length: 10
Width: 5
Area: 50
Perimeter: 30
```

The calculated values are stored as instance attributes during initialization.

---

## 13. Constructor Validation

We can validate values inside `__init__()` before storing them.

Example:

```python
class Student:

    def __init__(self, name, marks):
        if not name.strip():
            raise ValueError("Student name cannot be empty")

        if not 0 <= marks <= 100:
            raise ValueError("Marks must be between 0 and 100")

        self.name = name
        self.marks = marks

    def display(self):
        print("Name:", self.name)
        print("Marks:", self.marks)


student1 = Student("Raj", 85)

student1.display()
```

Output:

```text
Name: Raj
Marks: 85
```

Invalid example:

```python
student2 = Student("Aman", 150)
```

Output:

```text
ValueError: Marks must be between 0 and 100
```

A constructor should not create an object in an invalid state when the class requires valid initial data.

---

## 14. Constructor vs Normal Method

| Constructor / Initializer | Normal Method |
|---|---|
| Commonly uses `__init__()` | Can have any valid method name |
| Runs automatically during object initialization | Must be called explicitly |
| Used to initialize object attributes | Used to perform object operations |
| Receives `self` automatically | Instance methods also receive `self` |
| One `__init__()` definition per class | A class can have many methods |

Example:

```python
class Student:

    def __init__(self, name):
        self.name = name
        print("Object initialized")

    def display(self):
        print("Student Name:", self.name)


student1 = Student("Raj")

student1.display()
```

Output:

```text
Object initialized
Student Name: Raj
```

---

## 15. Can Python Have Multiple Constructors?

Python does not support traditional constructor overloading in the same way as some other languages.

Defining multiple methods with the same name inside a class does not create multiple overloads. The later definition replaces the earlier one.

Incorrect approach:

```python
class Student:

    def __init__(self, name):
        self.name = name

    def __init__(self, name, age):
        self.name = name
        self.age = age
```

The second `__init__()` replaces the first definition.

A common solution is to use default parameters.

```python
class Student:

    def __init__(self, name, age=None):
        self.name = name
        self.age = age

    def display(self):
        print("Name:", self.name)
        print("Age:", self.age)


student1 = Student("Raj")
student2 = Student("Aman", 22)

student1.display()
student2.display()
```

Output:

```text
Name: Raj
Age: None
Name: Aman
Age: 22
```

We can also use `*args` or class methods as alternative constructors when the design requires more flexibility.

---

## 16. The __del__() Method – Introduction

`__del__()` is a special method that may be called when an object is finalized.

Example:

```python
class Student:

    def __init__(self, name):
        self.name = name
        print("Student object created")

    def __del__(self):
        print("Student object finalized")


student1 = Student("Raj")

del student1

print("Program continues")
```

A possible output is:

```text
Student object created
Student object finalized
Program continues
```

### Important Notes

- `del student1` removes the variable reference; it does not directly guarantee immediate object destruction.
- `__del__()` timing depends on object lifetime and Python implementation.
- It should not be relied upon for essential cleanup.
- Use context managers (`with`) for reliable resource management.

---

# 17. Practical Programs

## Program 1: Student Management

```python
class Student:

    school = "ABC School"

    def __init__(self, name, roll_number, marks):
        self.name = name
        self.roll_number = roll_number
        self.marks = marks

    def display(self):
        print("School:", Student.school)
        print("Name:", self.name)
        print("Roll Number:", self.roll_number)
        print("Marks:", self.marks)

    def calculate_grade(self):
        if self.marks >= 90:
            return "A"

        elif self.marks >= 75:
            return "B"

        elif self.marks >= 60:
            return "C"

        else:
            return "D"


student1 = Student("Raj", 101, 92)
student2 = Student("Aman", 102, 78)

student1.display()
print("Grade:", student1.calculate_grade())

student2.display()
print("Grade:", student2.calculate_grade())
```

## Program 2: Employee Salary Calculator

```python
class Employee:

    company = "Tech Solutions"

    def __init__(self, name, basic_salary):
        self.name = name
        self.basic_salary = basic_salary

        self.hra = basic_salary * 0.20
        self.da = basic_salary * 0.10

        self.total_salary = (
            self.basic_salary + self.hra + self.da
        )

    def display_salary(self):
        print("Employee:", self.name)
        print("Basic Salary:", self.basic_salary)
        print("HRA:", self.hra)
        print("DA:", self.da)
        print("Total Salary:", self.total_salary)


employee1 = Employee("Raj", 30000)

employee1.display_salary()
```

Output:

```text
Employee: Raj
Basic Salary: 30000
HRA: 6000.0
DA: 3000.0
Total Salary: 39000.0
```

## Program 3: Bank Account Initialization

```python
class BankAccount:

    bank_name = "National Bank"

    def __init__(self, account_number, holder_name, balance=0):
        self.account_number = account_number
        self.holder_name = holder_name
        self.balance = balance

    def deposit(self, amount):
        if amount <= 0:
            print("Invalid deposit amount")
            return

        self.balance += amount
        print("Deposit successful")

    def show_balance(self):
        print("Bank:", BankAccount.bank_name)
        print("Account:", self.account_number)
        print("Holder:", self.holder_name)
        print("Balance:", self.balance)


account1 = BankAccount("101", "Raj", 5000)
account2 = BankAccount("102", "Aman")

account1.deposit(2000)

account1.show_balance()
account2.show_balance()
```

## Program 4: Product Inventory

```python
class Product:

    store_name = "Smart Store"

    def __init__(self, product_id, name, price, quantity):
        self.product_id = product_id
        self.name = name
        self.price = price
        self.quantity = quantity

    def calculate_stock_value(self):
        return self.price * self.quantity

    def display(self):
        print("Store:", Product.store_name)
        print("Product ID:", self.product_id)
        print("Name:", self.name)
        print("Price:", self.price)
        print("Quantity:", self.quantity)
        print("Stock Value:", self.calculate_stock_value())


product1 = Product(101, "Laptop", 55000, 5)
product2 = Product(102, "Mouse", 800, 20)

product1.display()
product2.display()
```

## Program 5: Circle Calculator

```python
class Circle:

    PI = 3.14159

    def __init__(self, radius):
        if radius <= 0:
            raise ValueError("Radius must be positive")

        self.radius = radius

    def calculate_area(self):
        return Circle.PI * self.radius ** 2

    def calculate_circumference(self):
        return 2 * Circle.PI * self.radius

    def display(self):
        print("Radius:", self.radius)
        print("Area:", self.calculate_area())
        print("Circumference:", self.calculate_circumference())


circle1 = Circle(7)

circle1.display()
```

---

# 18. Mini Project – Employee Management System

## Project Description

Create an Employee Management System using classes and objects.

The system should store employee information and calculate salary details.

### Requirements

1. Create an `Employee` class.
2. Store employee ID, name, department and basic salary.
3. Create a class attribute for the company name.
4. Initialize employee data using `__init__()`.
5. Calculate HRA, DA and total salary.
6. Display individual employee information.
7. Create multiple employee objects.
8. Store employee objects inside a list.
9. Display all employees.
10. Calculate the total salary expense.

## Complete Project Code

```python
class Employee:

    company_name = "Tech Solutions"

    def __init__(self, employee_id, name, department, basic_salary):
        if not name.strip():
            raise ValueError("Employee name cannot be empty")

        if basic_salary < 0:
            raise ValueError("Salary cannot be negative")

        self.employee_id = employee_id
        self.name = name
        self.department = department
        self.basic_salary = basic_salary

        self.hra = basic_salary * 0.20
        self.da = basic_salary * 0.10

        self.total_salary = (
            self.basic_salary + self.hra + self.da
        )

    def display(self):
        print("\nEmployee ID:", self.employee_id)
        print("Name:", self.name)
        print("Department:", self.department)
        print("Basic Salary:", self.basic_salary)
        print("HRA:", self.hra)
        print("DA:", self.da)
        print("Total Salary:", self.total_salary)

    def get_total_salary(self):
        return self.total_salary


class EmployeeManagementSystem:

    def __init__(self):
        self.employees = []

    def add_employee(self):
        try:
            employee_id = input("Enter employee ID: ").strip()

            if not employee_id:
                raise ValueError("Employee ID cannot be empty")

            if any(
                employee.employee_id == employee_id
                for employee in self.employees
            ):
                raise ValueError("Employee ID already exists")

            name = input("Enter employee name: ").strip()
            department = input("Enter department: ").strip()
            basic_salary = float(input("Enter basic salary: "))

            employee = Employee(
                employee_id,
                name,
                department,
                basic_salary
            )

            self.employees.append(employee)

            print("Employee added successfully!")

        except ValueError as error:
            print("Input Error:", error)

    def display_all_employees(self):
        if not self.employees:
            print("No employee records found.")
            return

        for employee in self.employees:
            employee.display()

    def search_employee(self):
        employee_id = input("Enter employee ID: ").strip()

        for employee in self.employees:

            if employee.employee_id == employee_id:
                employee.display()
                return

        print("Employee not found!")

    def calculate_total_salary(self):
        total = sum(
            employee.get_total_salary()
            for employee in self.employees
        )

        print("Total Monthly Salary Expense:", total)

    def run(self):

        while True:

            print("\n===== EMPLOYEE MANAGEMENT SYSTEM =====")
            print("Company:", Employee.company_name)

            print("1. Add Employee")
            print("2. Display All Employees")
            print("3. Search Employee")
            print("4. Calculate Total Salary")
            print("5. Exit")

            choice = input("Enter your choice: ").strip()

            if choice == "1":
                self.add_employee()

            elif choice == "2":
                self.display_all_employees()

            elif choice == "3":
                self.search_employee()

            elif choice == "4":
                self.calculate_total_salary()

            elif choice == "5":
                print("Thank you for using the system!")
                break

            else:
                print("Invalid choice!")


system = EmployeeManagementSystem()

system.run()
```

## Sample Output

```text
===== EMPLOYEE MANAGEMENT SYSTEM =====
Company: Tech Solutions

1. Add Employee
2. Display All Employees
3. Search Employee
4. Calculate Total Salary
5. Exit

Enter your choice: 1

Enter employee ID: 101
Enter employee name: Raj
Enter department: IT
Enter basic salary: 30000

Employee added successfully!

===== EMPLOYEE MANAGEMENT SYSTEM =====

Enter your choice: 2

Employee ID: 101
Name: Raj
Department: IT
Basic Salary: 30000.0
HRA: 6000.0
DA: 3000.0
Total Salary: 39000.0
```

### Project Improvement Tasks

1. Add an update employee feature.
2. Add a delete employee feature.
3. Search employees by department.
4. Display the highest-paid employee.
5. Calculate average employee salary.
6. Add employee joining dates.
7. Add input validation for employee IDs.
8. Save employee records to a file.

**Note:** This project stores records in memory. Data will be lost when the program closes. File and database persistence will be developed in later lessons.

---

# 19. Student Practice Exercises

## Basic Level

1. Create a `Student` class with a constructor that accepts a name.
2. Create a `Car` class with brand, model and color attributes.
3. Create a `Mobile` class with a default price.
4. Create an `Employee` class with name and salary.
5. Create a `Book` class with title, author and price.
6. Create a `Rectangle` class that initializes length and width.

## Intermediate Level

7. Create a `BankAccount` class with account number, holder name and initial balance.
8. Create a `Product` class with a class attribute for store name.
9. Demonstrate the difference between class and instance attributes.
10. Create a `Student` class that validates marks during initialization.
11. Create a `Circle` class that calculates area and circumference.
12. Create an `Employee` class that calculates total salary.
13. Create a class with default and keyword constructor arguments.

## Advanced Level

14. Create a `ShoppingCart` class that initializes an empty product list.
15. Create a `Library` class that stores multiple book objects.
16. Create a `Hospital` class that manages patient objects.
17. Create a `School` class that manages student objects and calculates average marks.
18. Create an `Inventory` class that calculates total stock value.
19. Create a `Vehicle` class that stores common information about different vehicles.
20. Build an Employee Management System with add, search, update and delete operations.

---

# 20. Trainer Assessment

Ask the student to explain and demonstrate:

1. What is a constructor?
2. What is the purpose of `__init__()`?
3. When does `__init__()` execute?
4. What is the difference between `__new__()` and `__init__()`?
5. How do we pass parameters to a constructor?
6. What are default constructor parameters?
7. What is the difference between positional and keyword arguments?
8. What are instance attributes?
9. What are class attributes?
10. What is attribute shadowing?
11. What is the purpose of `__dict__`?
12. Can Python have multiple constructors with the same name?
13. What is the difference between a constructor and a normal method?
14. What is the purpose of `__del__()`?
15. How can we validate data during object initialization?

## Practical Assessment

Ask the student to independently:

- Create a class with a parameterized constructor.
- Initialize at least four instance attributes.
- Define and access a class attribute.
- Create multiple objects from the same class.
- Demonstrate class attribute shadowing.
- Add constructor validation.
- Store multiple objects inside a list.
- Complete the Employee Management System.

---

# 21. Day 28 Completion Criteria

The student should be able to:

- Understand object initialization.
- Use the `__init__()` method.
- Explain the basic role of `__new__()`.
- Create parameterized constructors.
- Use default constructor parameters.
- Pass positional and keyword arguments.
- Create and update instance attributes.
- Create and access class attributes.
- Understand attribute shadowing.
- Differentiate class and instance attributes.
- Inspect object attributes using `__dict__`.
- Validate object data during initialization.
- Understand the introductory purpose of `__del__()`.
- Create multiple objects from one class.
- Build an object-oriented management system.

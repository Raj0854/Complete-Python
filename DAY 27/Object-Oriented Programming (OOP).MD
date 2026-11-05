
# Day 27 – OOP Introduction (Object-Oriented Programming)

## 1. Introduction to OOP

OOP stands for **Object-Oriented Programming**.

It is a programming approach in which we organize code using classes and objects.

Instead of writing the entire program as separate functions and statements, OOP allows us to group related data and functionality together.

### Real-World Example

Consider a Car.

A car has some properties:

- Brand
- Model
- Color
- Speed

A car also performs some actions:

- Start
- Stop
- Accelerate
- Brake

In OOP:

- Properties are represented by attributes.
- Actions are represented by methods.
- A class defines the structure.
- An object is an individual instance of a class.

### Example Without OOP

```python
car1_brand = "Toyota"
car1_model = "Fortuner"
car1_color = "Black"

car2_brand = "Honda"
car2_model = "City"
car2_color = "White"

print(car1_brand, car1_model, car1_color)
print(car2_brand, car2_model, car2_color)
```

Output:

```text
Toyota Fortuner Black
Honda City White
```

This works, but managing many cars would require many separate variables.

OOP provides a more organized way to manage such data.

---

## 2. Why Do We Need OOP?

OOP helps us:

1. Organize large programs.
2. Reuse code.
3. Represent real-world entities.
4. Keep related data and functionality together.
5. Make programs easier to maintain.
6. Reduce unnecessary code duplication.
7. Build scalable applications.

### Example: Without OOP vs With OOP

Without OOP:

```python
student1_name = "Raj"
student1_marks = 85

student2_name = "Aman"
student2_marks = 90

student3_name = "Rahul"
student3_marks = 78
```

With OOP, we can define one structure for all students and create individual student objects.

---

## 3. What Is a Class?

A **class** is a blueprint or template used to create objects.

It defines what data and functionality its objects can have.

### Syntax

```python
class ClassName:
    # Attributes and methods
    pass
```

### Example

```python
class Student:
    pass
```

Here:

- `class` is the keyword used to define a class.
- `Student` is the class name.
- `pass` is used as a placeholder because the class body is currently empty.

### Naming Convention

Class names generally follow PascalCase.

Examples:

```python
class Student:
    pass


class BankAccount:
    pass


class EmployeeManagementSystem:
    pass
```

---

## 4. What Is an Object?

An **object** is an instance of a class.

A class defines a structure, while an object represents an actual entity created using that structure.

### Example

```python
class Student:
    pass


student1 = Student()

print(student1)
```

Output will look similar to:

```text
<__main__.Student object at 0x000001...>
```

The memory address may differ each time the program runs.

### Creating Multiple Objects

```python
class Student:
    pass


student1 = Student()
student2 = Student()
student3 = Student()

print(student1)
print(student2)
print(student3)
```

Each call to `Student()` creates a separate object.

### Understanding the Relationship

```text
             Student Class
                  |
        ---------------------
        |         |         |
     student1  student2  student3
      Object    Object    Object
```

One class can be used to create many objects.

---

## 5. Attributes – Data Inside Objects

Attributes are variables associated with a class or an object.

They represent the properties or data of an object.

There are two common types:

1. Instance attributes.
2. Class attributes.

We will understand their detailed differences in the next lesson. For now, let's introduce both.

### 5.1 Instance Attributes

Instance attributes belong to individual objects.

They can be different for every object.

Example:

```python
class Student:
    pass


student1 = Student()

student1.name = "Raj"
student1.age = 21
student1.marks = 85

print(student1.name)
print(student1.age)
print(student1.marks)
```

Output:

```text
Raj
21
85
```

We can assign different attributes to another object:

```python
class Student:
    pass


student1 = Student()
student1.name = "Raj"
student1.marks = 85

student2 = Student()
student2.name = "Aman"
student2.marks = 92

print(student1.name, student1.marks)
print(student2.name, student2.marks)
```

Output:

```text
Raj 85
Aman 92
```

Both objects belong to the same class but contain different data.

### 5.2 Class Attributes

Class attributes are defined directly inside the class, outside its methods.

They are shared through the class and are available to its instances.

Example:

```python
class Student:
    school_name = "ABC Public School"


student1 = Student()
student2 = Student()

print(student1.school_name)
print(student2.school_name)
print(Student.school_name)
```

Output:

```text
ABC Public School
ABC Public School
ABC Public School
```

Both objects can access the same class attribute.

---

## 6. Methods – Functions Inside a Class

A method is a function defined inside a class.

Methods represent the actions or behavior of objects.

Example:

```python
class Student:

    def display(self):
        print("Welcome to Python OOP!")


student1 = Student()

student1.display()
```

Output:

```text
Welcome to Python OOP!
```

Here:

- `display()` is a method.
- `student1` is an object.
- `student1.display()` calls the method using the object.
- `self` refers to the current instance.

### Another Example

```python
class Car:

    def start(self):
        print("Car started")

    def stop(self):
        print("Car stopped")


car1 = Car()

car1.start()
car1.stop()
```

Output:

```text
Car started
Car stopped
```

---

## 7. Understanding self

`self` represents the current object or instance of a class.

It allows methods to access the attributes and other methods belonging to that object.

### Example

```python
class Student:

    def display(self):
        print("Student object:", self)


student1 = Student()
student2 = Student()

student1.display()
student2.display()
```

Each call displays a reference to a different object.

### Accessing Object Attributes Using self

```python
class Student:

    def display(self):
        print("Name:", self.name)
        print("Age:", self.age)


student1 = Student()

student1.name = "Raj"
student1.age = 21

student1.display()
```

Output:

```text
Name: Raj
Age: 21
```

The `self.name` and `self.age` expressions access attributes belonging to the current object.

### Why Is self Important?

Consider two objects:

```python
class Student:

    def display(self):
        print("Name:", self.name)


student1 = Student()
student1.name = "Raj"

student2 = Student()
student2.name = "Aman"

student1.display()
student2.display()
```

Output:

```text
Name: Raj
Name: Aman
```

The same method works with different objects because `self` refers to the object that called it.

**Important:** `self` is a naming convention, not a Python keyword. However, you should use `self` for normal instance methods.

---

## 8. Methods with Parameters

Methods can accept parameters just like normal functions.

Example:

```python
class Calculator:

    def add(self, num1, num2):
        result = num1 + num2
        print("Addition:", result)


calc = Calculator()

calc.add(10, 20)
calc.add(50, 30)
```

Output:

```text
Addition: 30
Addition: 80
```

The object is passed automatically as the first argument to an instance method. Therefore, we provide only the two numbers when calling `calc.add()`.

### Method Returning a Value

```python
class Calculator:

    def multiply(self, num1, num2):
        return num1 * num2


calc = Calculator()

result = calc.multiply(5, 4)

print("Multiplication:", result)
```

Output:

```text
Multiplication: 20
```

Methods can use `return` just like normal functions.

---

## 9. Object State and Behavior

Every object can have:

- State: Data stored in its attributes.
- Behavior: Actions performed through its methods.
- Identity: The fact that it is a distinct object.

Example:

```python
class Fan:

    def turn_on(self):
        self.status = "ON"
        print("Fan is ON")

    def turn_off(self):
        self.status = "OFF"
        print("Fan is OFF")

    def show_status(self):
        print("Current Status:", self.status)


fan1 = Fan()

fan1.turn_on()
fan1.show_status()

fan1.turn_off()
fan1.show_status()
```

Output:

```text
Fan is ON
Current Status: ON
Fan is OFF
Current Status: OFF
```

Here:

- `status` represents the state.
- `turn_on()` and `turn_off()` represent behavior.
- `fan1` is the object.

---

## 10. Class vs Object

| Class | Object |
|---|---|
| A blueprint or template | An instance of a class |
| Defines attributes and methods | Contains actual data and uses methods |
| Defined using `class` | Created by calling the class |
| One class can create many objects | Each object has its own identity |
| Example: `Student` | Example: `student1` |

Example:

```python
class Mobile:

    def call(self):
        print("Calling...")


mobile1 = Mobile()
mobile2 = Mobile()
```

`Mobile` is the class, while `mobile1` and `mobile2` are its objects.

---

## 11. The type() Function with Objects

Python's `type()` function tells us the type of an object.

Example:

```python
class Student:
    pass


student1 = Student()

print(type(student1))
print(type(10))
print(type("Python"))
print(type([1, 2, 3]))
```

Output:

```text
<class '__main__.Student'>
<class 'int'>
<class 'str'>
<class 'list'>
```

This demonstrates that Python's built-in data types are also represented using classes.

---

## 12. The isinstance() Function

`isinstance()` checks whether an object belongs to a particular class or type.

### Syntax

```python
isinstance(object, classinfo)
```

Example:

```python
class Student:
    pass


student1 = Student()

print(isinstance(student1, Student))
print(isinstance(10, int))
print(isinstance("Python", str))
```

Output:

```text
True
True
True
```

It returns:

- `True` if the object is an instance of the specified class or type.
- `False` otherwise.

---

## 13. Object Identity

Every object has its own identity.

The `id()` function returns an integer representing the object's identity during its lifetime.

Example:

```python
class Student:
    pass


student1 = Student()
student2 = Student()

print(id(student1))
print(id(student2))

print(student1 is student2)
```

Output:

```text
Different identity values
Different identity values
False
```

The exact identity values depend on the running program.

### Comparing Objects

```python
class Student:
    pass


student1 = Student()
student2 = student1

print(student1 is student2)
```

Output:

```text
True
```

Both variables refer to the same object.

Remember:

- `==` checks equality of values according to the object's equality implementation.
- `is` checks whether two references point to the same object.

---

## 14. Instance Methods, Class Methods and Static Methods – Introduction

Python classes support three commonly used method types.

### 14.1 Instance Methods

Instance methods work with individual object data.

They receive `self` as their first parameter.

```python
class Student:

    def display(self):
        print("Student information")


student1 = Student()

student1.display()
```

### 14.2 Class Methods

Class methods work with class-level data.

They use the `@classmethod` decorator and receive `cls` as the first parameter.

```python
class Student:

    school = "ABC School"

    @classmethod
    def show_school(cls):
        print("School:", cls.school)


Student.show_school()
```

Output:

```text
School: ABC School
```

### 14.3 Static Methods

Static methods do not automatically receive `self` or `cls`.

They use the `@staticmethod` decorator.

```python
class Calculator:

    @staticmethod
    def add(a, b):
        return a + b


print(Calculator.add(10, 20))
```

Output:

```text
30
```

### Comparison

| Method Type | First Automatic Argument | Main Purpose |
|---|---|---|
| Instance Method | `self` | Work with object data |
| Class Method | `cls` | Work with class data |
| Static Method | None | Related utility functionality |

We will explore these method types in more detail in later OOP lessons.

---

## 15. OOP vs Procedural Programming

Python supports different programming approaches.

### Procedural Programming

In procedural programming, code is organized mainly around functions and step-by-step instructions.

Example:

```python
def calculate_area(length, width):
    return length * width


area = calculate_area(10, 5)

print("Area:", area)
```

### Object-Oriented Programming

In OOP, data and related functionality are organized inside classes.

```python
class Rectangle:

    def calculate_area(self, length, width):
        return length * width


rectangle = Rectangle()

area = rectangle.calculate_area(10, 5)

print("Area:", area)
```

Output:

```text
Area: 50
```

### Comparison

| Procedural Programming | Object-Oriented Programming |
|---|---|
| Focuses on functions | Focuses on objects |
| Data and functions are often separate | Data and behavior are grouped |
| Suitable for many small tasks | Useful for organizing larger applications |
| Code reuse through functions | Code reuse through functions, classes and inheritance |

Both approaches are useful. OOP is not automatically the best choice for every program.

---

# 16. Practical Programs

## Program 1: Student Information

```python
class Student:

    def display(self):
        print("Name:", self.name)
        print("Age:", self.age)
        print("Course:", self.course)


student1 = Student()

student1.name = "Raj"
student1.age = 21
student1.course = "Python"

student1.display()
```

Output:

```text
Name: Raj
Age: 21
Course: Python
```

## Program 2: Employee Information

```python
class Employee:

    def display(self):
        print("Employee Name:", self.name)
        print("Employee ID:", self.employee_id)
        print("Salary:", self.salary)


employee1 = Employee()

employee1.name = "Aman"
employee1.employee_id = 101
employee1.salary = 30000

employee1.display()
```

## Program 3: Rectangle Area

```python
class Rectangle:

    def calculate_area(self, length, width):
        return length * width


rectangle1 = Rectangle()

area = rectangle1.calculate_area(10, 5)

print("Rectangle Area:", area)
```

Output:

```text
Rectangle Area: 50
```

## Program 4: Bank Account

```python
class BankAccount:

    def show_balance(self):
        print("Account Holder:", self.name)
        print("Balance:", self.balance)

    def deposit(self, amount):
        self.balance += amount
        print("Deposit Successful!")


account1 = BankAccount()

account1.name = "Raj"
account1.balance = 5000

account1.show_balance()

account1.deposit(2000)

account1.show_balance()
```

Output:

```text
Account Holder: Raj
Balance: 5000
Deposit Successful!
Account Holder: Raj
Balance: 7000
```

Note: This is an introductory example. Input validation and secure transaction handling will be added in more advanced projects.

## Program 5: Mobile Phone

```python
class Mobile:

    def show_details(self):
        print("Brand:", self.brand)
        print("Model:", self.model)
        print("Price:", self.price)

    def make_call(self, number):
        print("Calling:", number)


mobile1 = Mobile()

mobile1.brand = "Samsung"
mobile1.model = "Galaxy S Series"
mobile1.price = 60000

mobile1.show_details()
mobile1.make_call("9876543210")
```

## Program 6: Multiple Objects

```python
class Product:

    def display(self):
        print("Product:", self.name)
        print("Price:", self.price)


product1 = Product()
product1.name = "Keyboard"
product1.price = 1200

product2 = Product()
product2.name = "Mouse"
product2.price = 500

product3 = Product()
product3.name = "Monitor"
product3.price = 12000

product1.display()
product2.display()
product3.display()
```

## Program 7: Temperature Converter

```python
class TemperatureConverter:

    def celsius_to_fahrenheit(self, celsius):
        return (celsius * 9 / 5) + 32

    def fahrenheit_to_celsius(self, fahrenheit):
        return (fahrenheit - 32) * 5 / 9


converter = TemperatureConverter()

print("Fahrenheit:", converter.celsius_to_fahrenheit(25))

print("Celsius:", converter.fahrenheit_to_celsius(98.6))
```

Output:

```text
Fahrenheit: 77.0
Celsius: 37.0
```

---

# 17. Mini Project – Basic Library Management System

## Project Description

Create a simple Library Management System using classes and objects.

The system should manage books and their availability.

### Requirements

1. Create a `Book` class.
2. Store book title, author and availability.
3. Create a method to display book information.
4. Create a method to borrow a book.
5. Create a method to return a book.
6. Create multiple book objects.
7. Display all books.

### Complete Project Code

```python
class Book:

    def display_details(self):
        print("\nBook Title:", self.title)
        print("Author:", self.author)

        if self.available:
            print("Status: Available")
        else:
            print("Status: Borrowed")

    def borrow_book(self):
        if self.available:
            self.available = False
            print(self.title, "borrowed successfully!")
        else:
            print(self.title, "is already borrowed.")

    def return_book(self):
        if not self.available:
            self.available = True
            print(self.title, "returned successfully!")
        else:
            print(self.title, "is already available.")


book1 = Book()
book1.title = "Python Basics"
book1.author = "John Smith"
book1.available = True

book2 = Book()
book2.title = "Learning Programming"
book2.author = "David Miller"
book2.available = True

book3 = Book()
book3.title = "Advanced Python"
book3.author = "Robert Wilson"
book3.available = False


books = [book1, book2, book3]


def display_all_books():
    print("\n===== LIBRARY BOOKS =====")

    for book in books:
        book.display_details()


while True:

    print("\n===== LIBRARY MANAGEMENT SYSTEM =====")
    print("1. Display All Books")
    print("2. Borrow Book")
    print("3. Return Book")
    print("4. Exit")

    choice = input("Enter your choice: ")

    if choice == "1":
        display_all_books()

    elif choice == "2":

        title = input("Enter book title: ")

        found = False

        for book in books:
            if book.title.lower() == title.lower():
                book.borrow_book()
                found = True
                break

        if not found:
            print("Book not found!")

    elif choice == "3":

        title = input("Enter book title: ")

        found = False

        for book in books:
            if book.title.lower() == title.lower():
                book.return_book()
                found = True
                break

        if not found:
            print("Book not found!")

    elif choice == "4":
        print("Thank you for using the library system!")
        break

    else:
        print("Invalid choice!")
```

### Sample Output

```text
===== LIBRARY MANAGEMENT SYSTEM =====
1. Display All Books
2. Borrow Book
3. Return Book
4. Exit

Enter your choice: 1

===== LIBRARY BOOKS =====

Book Title: Python Basics
Author: John Smith
Status: Available

Book Title: Learning Programming
Author: David Miller
Status: Available

Book Title: Advanced Python
Author: Robert Wilson
Status: Borrowed
```

### Project Improvement Tasks

After completing the basic project, add:

1. Book ID.
2. Student information.
3. Search book by ID.
4. Display only available books.
5. Count total available and borrowed books.
6. Add new books.
7. Remove books.
8. Maintain a list of borrowed books.

---

# 18. Student Practice Exercises

## Basic Level

1. Create an empty `Student` class and create three objects.
2. Create a `Car` class and assign brand, model and color to an object.
3. Create a `Mobile` class with brand and price attributes.
4. Create a `Person` class with a method to display personal information.
5. Create a `Calculator` class with addition and subtraction methods.
6. Create a `Rectangle` class that calculates area.

## Intermediate Level

7. Create an `Employee` class with name, employee ID and salary.
8. Create a `BankAccount` class with deposit and balance methods.
9. Create a `Product` class and create five different product objects.
10. Create a `Circle` class with methods to calculate area and circumference.
11. Create a `Book` class with borrow and return methods.
12. Create a `Student` class that calculates average marks.

## Advanced Level

13. Create a `ShoppingCart` class with add and remove product methods.
14. Create a `Library` class that manages multiple book objects.
15. Create a `Hospital` class that stores patient objects.
16. Create a `Vehicle` class with multiple objects representing different vehicles.
17. Create a `School` class that manages multiple student objects.
18. Create a `Restaurant` class that manages menu items and their prices.

---

# 19. Trainer Assessment

Ask the student to explain and demonstrate:

1. What is Object-Oriented Programming?
2. Why do we use OOP?
3. What is a class?
4. What is an object?
5. What is the difference between a class and an object?
6. What are attributes?
7. What are methods?
8. What is `self`?
9. What is the difference between instance attributes and class attributes?
10. What is object state and behavior?
11. What does `type()` do with objects?
12. What is the purpose of `isinstance()`?
13. What is the difference between `==` and `is`?
14. What are instance, class and static methods?
15. How is OOP different from procedural programming?

## Practical Assessment

Ask the student to independently:

- Create a class with at least three attributes.
- Create at least three objects from that class.
- Add two or more methods.
- Access object attributes using `self`.
- Create a class containing both data and behavior.
- Complete the Library Management System.

---

# 20. Day 27 Completion Criteria

The student should be able to:

- Explain the concept of OOP.
- Understand classes and objects.
- Create classes and multiple objects.
- Define and access attributes.
- Understand instance and class attributes.
- Create and call methods.
- Understand the purpose of `self`.
- Pass parameters to methods.
- Return values from methods.
- Understand object state, behavior and identity.
- Use `type()`, `isinstance()` and `id()`.
- Understand the introduction to instance, class and static methods.
- Build a basic object-oriented application.
- Complete the Library Management System.

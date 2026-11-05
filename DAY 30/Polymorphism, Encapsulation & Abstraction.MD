
# Day 30 – Polymorphism, Encapsulation & Abstraction

## 1. Introduction to OOP Pillars

Object-Oriented Programming is based on four major concepts:

1. Encapsulation – Combining data and methods inside a class.
2. Inheritance – Reusing properties and methods from another class.
3. Polymorphism – Same interface, different behavior.
4. Abstraction – Hiding internal implementation and exposing essential functionality.

Today, we will learn the remaining three concepts in detail.

---

## 2. Polymorphism in Python

### What is Polymorphism?

Polymorphism means "many forms".

In Python, polymorphism allows the same method name or operation to behave differently depending on the object or data type.

### Example 1: Same Function, Different Data Types

```python
print(len("Python"))
print(len([10, 20, 30, 40]))
print(len({"name": "Raj", "age": 22}))
```

**Output:**
```text
6
4
2
```

The same `len()` function works with strings, lists and dictionaries.

### Example 2: Same Operator, Different Behavior

```python
print(10 + 20)
print("Hello " + "Python")
print([1, 2] + [3, 4])
```

**Output:**
```text
30
Hello Python
[1, 2, 3, 4]
```

The `+` operator performs different operations depending on the data types.

---

## 3. Method Overriding

Method overriding occurs when a child class provides its own implementation of a method already defined in its parent class.

It is commonly used to achieve runtime polymorphism.

### Example

```python
class Animal:
    def sound(self):
        print("Animals make sounds")


class Dog(Animal):
    def sound(self):
        print("Dog barks")


class Cat(Animal):
    def sound(self):
        print("Cat meows")


animal = Animal()
dog = Dog()
cat = Cat()

animal.sound()
dog.sound()
cat.sound()
```

**Output:**
```text
Animals make sounds
Dog barks
Cat meows
```

### Explanation

- `Animal` defines the original `sound()` method.
- `Dog` overrides it with its own implementation.
- `Cat` also overrides the same method.
- The method that runs depends on the actual object.

### Example 2: Employee Salary

```python
class Employee:
    def calculate_salary(self):
        return 20000


class Manager(Employee):
    def calculate_salary(self):
        return 50000


class Developer(Employee):
    def calculate_salary(self):
        return 35000


employees = [
    Employee(),
    Manager(),
    Developer()
]

for employee in employees:
    print(employee.calculate_salary())
```

**Output:**
```text
20000
50000
35000
```

The same method produces different results for different objects.

---

## 4. Duck Typing

### What is Duck Typing?

Duck typing is a Python concept in which an object's suitability is determined by the methods and behavior it provides, rather than its class or type.

The idea is:

"If an object behaves like a duck, Python can treat it like a duck."

### Example

```python
class Dog:
    def speak(self):
        print("Dog is barking")


class Cat:
    def speak(self):
        print("Cat is meowing")


class Robot:
    def speak(self):
        print("Robot is speaking")


def make_speak(obj):
    obj.speak()


dog = Dog()
cat = Cat()
robot = Robot()

make_speak(dog)
make_speak(cat)
make_speak(robot)
```

**Output:**
```text
Dog is barking
Cat is meowing
Robot is speaking
```

### Explanation

- `make_speak()` does not check the object's class.
- It only expects the object to provide a `speak()` method.
- All three objects work because they implement that method.

This is called duck typing.

**Important:** If an object does not have the required method, Python raises an `AttributeError`.

---

## 5. Method Overloading in Python

### What is Method Overloading?

Method overloading traditionally means defining multiple methods with the same name but different parameters.

Some programming languages support this directly.

Python does not support traditional method overloading based only on different parameter counts or types.

### Incorrect Expectation

```python
class Calculator:
    def add(self, a, b):
        return a + b

    def add(self, a, b, c):
        return a + b + c


obj = Calculator()
print(obj.add(10, 20))
```

This raises a `TypeError` because the second `add()` definition replaces the first one.

### Python Alternative 1: Default Arguments

```python
class Calculator:
    def add(self, a, b, c=0):
        return a + b + c


obj = Calculator()

print(obj.add(10, 20))
print(obj.add(10, 20, 30))
```

**Output:**
```text
30
60
```

### Python Alternative 2: *args

```python
class Calculator:
    def add(self, *numbers):
        return sum(numbers)


obj = Calculator()

print(obj.add(10, 20))
print(obj.add(10, 20, 30))
print(obj.add(10, 20, 30, 40))
```

**Output:**
```text
30
60
100
```

Python provides flexible ways to handle different numbers of arguments.

---

## 6. Operator Overloading

### What is Operator Overloading?

Operator overloading allows developers to define how operators behave when used with custom objects.

Python uses special methods, also called magic methods or dunder methods, for this purpose.

Examples:

| Operator | Special Method |
|---|---|
| `+` | `__add__()` |
| `-` | `__sub__()` |
| `*` | `__mul__()` |
| `==` | `__eq__()` |
| `<` | `__lt__()` |
| `>` | `__gt__()` |
| `str()` | `__str__()` |
| `len()` | `__len__()` |

### Example 1: Overloading the + Operator

```python
class Number:
    def __init__(self, value):
        self.value = value

    def __add__(self, other):
        return self.value + other.value


n1 = Number(10)
n2 = Number(20)

print(n1 + n2)
```

**Output:**
```text
30
```

### Explanation

When Python executes:

```python
n1 + n2
```

It internally calls:

```python
n1.__add__(n2)
```

### Example 2: Overloading the == Operator

```python
class Student:
    def __init__(self, name, marks):
        self.name = name
        self.marks = marks

    def __eq__(self, other):
        return self.marks == other.marks


s1 = Student("Raj", 85)
s2 = Student("Aman", 85)
s3 = Student("Rahul", 90)

print(s1 == s2)
print(s1 == s3)
```

**Output:**
```text
True
False
```

### Example 3: Using __str__()

```python
class Student:
    def __init__(self, name, age):
        self.name = name
        self.age = age

    def __str__(self):
        return f"{self.name} is {self.age} years old"


student = Student("Raj", 22)

print(student)
```

**Output:**
```text
Raj is 22 years old
```

`__str__()` controls the readable string representation of an object.

---

# PART 2 – ENCAPSULATION

## 7. What is Encapsulation?

Encapsulation means combining data and the methods that operate on that data inside a single class.

It also involves controlling how an object's internal data is accessed or modified.

### Real-World Example

Consider a bank account.

A user should not be able to change the account balance to any arbitrary value.

Instead, the account should provide methods such as:

- `deposit()`
- `withdraw()`
- `check_balance()`

These methods control how the balance changes.

---

## 8. Access Conventions in Python

Python commonly uses three naming conventions for attributes.

### 1. Public Attributes

Public attributes can be accessed from outside the class.

```python
class Student:
    def __init__(self, name):
        self.name = name


student = Student("Raj")

print(student.name)
```

**Output:**
```text
Raj
```

### 2. Protected-Like Attributes

A single underscore indicates that an attribute is intended for internal use or subclass use.

```python
class Employee:
    def __init__(self):
        self._salary = 30000


employee = Employee()

print(employee._salary)
```

**Output:**
```text
30000
```

Python does not strictly prevent external access to `_salary`.

The underscore is a convention that communicates intended usage.

### 3. Private-Like Attributes

A double underscore triggers name mangling.

```python
class BankAccount:
    def __init__(self, balance):
        self.__balance = balance

    def show_balance(self):
        print(self.__balance)


account = BankAccount(5000)

account.show_balance()
```

**Output:**
```text
5000
```

Direct access using `account.__balance` will normally raise an `AttributeError`.

Python internally changes the attribute name to something similar to:

```python
_BankAccount__balance
```

This mechanism is called name mangling.

**Important:** Double underscores do not provide absolute security or strict privacy.

---

## 9. Encapsulation Using Methods

We can control access to internal data through class methods.

### Example: Bank Account

```python
class BankAccount:
    def __init__(self, balance):
        self.__balance = balance

    def deposit(self, amount):
        if amount > 0:
            self.__balance += amount
            print("Deposit successful")
        else:
            print("Invalid deposit amount")

    def withdraw(self, amount):
        if amount <= 0:
            print("Invalid withdrawal amount")
        elif amount > self.__balance:
            print("Insufficient balance")
        else:
            self.__balance -= amount
            print("Withdrawal successful")

    def check_balance(self):
        print("Current Balance:", self.__balance)


account = BankAccount(5000)

account.deposit(2000)
account.withdraw(1000)
account.check_balance()
```

**Output:**
```text
Deposit successful
Withdrawal successful
Current Balance: 6000
```

### Explanation

- The balance is stored in `__balance`.
- External code uses the provided methods.
- Validation happens before changing the balance.
- The class controls its internal state.

---

## 10. Getters and Setters

Getters and setters are methods used to read and update an attribute in a controlled way.

### Getter

A getter returns the value of an attribute.

### Setter

A setter updates the value after applying validation.

### Example

```python
class Student:
    def __init__(self, marks):
        self.__marks = marks

    def get_marks(self):
        return self.__marks

    def set_marks(self, marks):
        if 0 <= marks <= 100:
            self.__marks = marks
        else:
            print("Invalid marks")


student = Student(80)

print(student.get_marks())

student.set_marks(95)

print(student.get_marks())

student.set_marks(150)
```

**Output:**
```text
80
95
Invalid marks
```

---

## 11. Using @property

Python provides the `@property` decorator to create managed attributes.

It allows us to access getter and setter methods using normal attribute syntax.

### Example

```python
class Student:
    def __init__(self, marks):
        self.__marks = marks

    @property
    def marks(self):
        return self.__marks

    @marks.setter
    def marks(self, value):
        if 0 <= value <= 100:
            self.__marks = value
        else:
            raise ValueError("Marks must be between 0 and 100")


student = Student(80)

print(student.marks)

student.marks = 95

print(student.marks)
```

**Output:**
```text
80
95
```

If we execute:

```python
student.marks = 150
```

Python raises:

```text
ValueError: Marks must be between 0 and 100
```

### Why Use @property?

- Provides controlled access to attributes.
- Allows validation before updating values.
- Keeps attribute access simple.
- Helps change internal implementation without changing the public interface.

In Python, `@property` is often preferred over manually creating simple getter and setter methods.

---

# PART 3 – ABSTRACTION

## 12. What is Abstraction?

Abstraction means hiding unnecessary implementation details and exposing only the essential functionality.

The user knows what an object does without needing to know exactly how it works internally.

### Real-World Example

Consider an ATM.

A user can:

- Withdraw money.
- Check balance.
- Deposit money.

The user does not need to understand the internal banking network, database queries or transaction processing.

The ATM exposes simple operations while hiding internal complexity.

---

## 13. Abstraction Using Abstract Classes

Python provides the `abc` module for creating abstract classes.

Important components:

- `ABC`: Base class for defining abstract classes.
- `@abstractmethod`: Marks a method that must be implemented by concrete subclasses.

### Basic Syntax

```python
from abc import ABC, abstractmethod


class Shape(ABC):

    @abstractmethod
    def calculate_area(self):
        pass
```

Here, `Shape` is an abstract class.

Its abstract method `calculate_area()` must be implemented by concrete subclasses.

---

## 14. Implementing an Abstract Class

```python
from abc import ABC, abstractmethod


class Shape(ABC):

    @abstractmethod
    def calculate_area(self):
        pass


class Circle(Shape):
    def __init__(self, radius):
        self.radius = radius

    def calculate_area(self):
        return 3.14 * self.radius * self.radius


class Rectangle(Shape):
    def __init__(self, length, width):
        self.length = length
        self.width = width

    def calculate_area(self):
        return self.length * self.width


circle = Circle(5)
rectangle = Rectangle(10, 5)

print("Circle Area:", circle.calculate_area())
print("Rectangle Area:", rectangle.calculate_area())
```

**Output:**
```text
Circle Area: 78.5
Rectangle Area: 50
```

### Explanation

1. `Shape` defines the common interface.
2. `calculate_area()` is an abstract method.
3. `Circle` implements the method using its own formula.
4. `Rectangle` implements the same method differently.
5. Both classes follow the same interface.

This example combines abstraction and polymorphism.

---

## 15. Cannot Instantiate an Abstract Class

An abstract class cannot be instantiated while it still has unimplemented abstract methods.

Example:

```python
from abc import ABC, abstractmethod


class Vehicle(ABC):

    @abstractmethod
    def start(self):
        pass


vehicle = Vehicle()
```

**Output:**

```text
TypeError: Can't instantiate abstract class Vehicle
```

A concrete child class must implement all inherited abstract methods before its objects can be created.

### Example

```python
class Car(Vehicle):
    def start(self):
        print("Car started")


car = Car()
car.start()
```

**Output:**
```text
Car started
```

---

## 16. Multiple Abstract Methods

An abstract class can contain multiple abstract methods.

```python
from abc import ABC, abstractmethod


class Employee(ABC):

    @abstractmethod
    def calculate_salary(self):
        pass

    @abstractmethod
    def display_details(self):
        pass


class Developer(Employee):

    def calculate_salary(self):
        return 40000

    def display_details(self):
        print("Employee Role: Developer")


developer = Developer()

developer.display_details()
print("Salary:", developer.calculate_salary())
```

**Output:**
```text
Employee Role: Developer
Salary: 40000
```

The child class must implement both abstract methods to become concrete.

---

## 17. Difference Between Encapsulation and Abstraction

| Encapsulation | Abstraction |
|---|---|
| Combines data and methods | Hides implementation details |
| Controls access to internal data | Exposes essential operations |
| Focuses on data protection and controlled modification | Focuses on interface and complexity reduction |
| Uses classes, naming conventions and properties | Uses abstract classes and interfaces |
| Example: Bank account balance | Example: ATM operations |

---

## 18. Difference Between Overriding and Overloading

| Method Overriding | Method Overloading |
|---|---|
| Child class redefines a parent method | Same method name with different parameter signatures |
| Supported in Python | Traditional method overloading is not directly supported |
| Commonly used for runtime polymorphism | Can be approximated using default arguments or `*args` |
| Requires inheritance | Does not necessarily require inheritance |

---

## 19. Composition vs Inheritance

Inheritance represents an "is-a" relationship.

Example:
- Car is a Vehicle.
- Manager is an Employee.

Composition represents a "has-a" relationship.

Example:
- Car has an Engine.
- Computer has a Processor.

### Composition Example

```python
class Engine:
    def start(self):
        print("Engine started")


class Car:
    def __init__(self):
        self.engine = Engine()

    def start_car(self):
        self.engine.start()
        print("Car is ready")


car = Car()
car.start_car()
```

**Output:**
```text
Engine started
Car is ready
```

Use inheritance when there is a genuine "is-a" relationship. Use composition when one object contains or uses another object.

---

# PART 4 – PRACTICAL PROGRAMS

## 20. Program 1: Shape Area Calculator Using Polymorphism

```python
class Circle:
    def area(self, radius):
        return 3.14 * radius * radius


class Rectangle:
    def area(self, length, width):
        return length * width


class Square:
    def area(self, side):
        return side * side


shapes = [
    Circle(),
    Rectangle(),
    Square()
]

print("Circle Area:", shapes[0].area(5))
print("Rectangle Area:", shapes[1].area(10, 5))
print("Square Area:", shapes[2].area(4))
```

**Output:**
```text
Circle Area: 78.5
Rectangle Area: 50
Square Area: 16
```

Notice that each class provides its own `area()` implementation.

---

## 21. Program 2: Secure Employee Salary Management

```python
class Employee:
    def __init__(self, name, salary):
        self.name = name
        self.__salary = salary

    def get_salary(self):
        return self.__salary

    def set_salary(self, salary):
        if salary >= 0:
            self.__salary = salary
        else:
            print("Salary cannot be negative")


employee = Employee("Raj", 30000)

print("Employee:", employee.name)
print("Salary:", employee.get_salary())

employee.set_salary(40000)

print("Updated Salary:", employee.get_salary())
```

**Output:**
```text
Employee: Raj
Salary: 30000
Updated Salary: 40000
```

---

## 22. Program 3: Payment Processing Using Abstraction and Polymorphism

```python
from abc import ABC, abstractmethod


class PaymentMethod(ABC):

    @abstractmethod
    def pay(self, amount):
        pass


class CreditCardPayment(PaymentMethod):

    def pay(self, amount):
        print(f"Paid Rs. {amount} using Credit Card")


class UPIPayment(PaymentMethod):

    def pay(self, amount):
        print(f"Paid Rs. {amount} using UPI")


class CashPayment(PaymentMethod):

    def pay(self, amount):
        print(f"Paid Rs. {amount} using Cash")


def process_payment(payment_method, amount):
    payment_method.pay(amount)


credit_card = CreditCardPayment()
upi = UPIPayment()
cash = CashPayment()

process_payment(credit_card, 1500)
process_payment(upi, 2000)
process_payment(cash, 500)
```

**Output:**
```text
Paid Rs. 1500 using Credit Card
Paid Rs. 2000 using UPI
Paid Rs. 500 using Cash
```

This example demonstrates:

- Abstraction through `PaymentMethod`.
- Polymorphism through different `pay()` implementations.
- A common interface for multiple payment methods.

This is only a learning simulation. It does not process real payments.

---

# PART 5 – MINI PROJECT

## 23. Mini Project: Payment Processing Management System

### Project Description

Create a payment processing system using OOP concepts.

The system should support multiple payment methods:

1. Credit Card
2. UPI
3. Cash

The project must demonstrate abstraction, encapsulation and polymorphism.

### Project Requirements

#### A. Abstract Payment Class

Create an abstract class named `PaymentMethod`.

It should contain:

- An abstract method `pay(amount)`.
- A method for displaying payment information if needed.

#### B. Credit Card Payment Class

Create `CreditCardPayment`.

Requirements:

- Inherit from `PaymentMethod`.
- Store cardholder name.
- Store card number as a private-like attribute.
- Display only the last four digits of the card number.
- Implement `pay()`.

For this learning project, use dummy card details only.

#### C. UPI Payment Class

Create `UPIPayment`.

Requirements:

- Inherit from `PaymentMethod`.
- Store the UPI ID.
- Validate that the UPI ID is not empty.
- Implement `pay()`.

#### D. Cash Payment Class

Create `CashPayment`.

Requirements:

- Inherit from `PaymentMethod`.
- Implement `pay()`.

#### E. Payment Manager

Create a class named `PaymentManager`.

Requirements:

- Store payment records in a list.
- Accept a payment method object.
- Process payment through the common `pay()` interface.
- Store the payment amount and payment method.
- Display payment history.
- Calculate total payments.

#### F. Validation

Apply these rules:

- Payment amount must be greater than zero.
- Invalid amounts should not be recorded.
- Card details should not be displayed completely.
- UPI ID must not be empty.

### Sample Expected Output

```text
===== PAYMENT PROCESSING SYSTEM =====

1. Credit Card Payment
2. UPI Payment
3. Cash Payment
4. View Payment History
5. View Total Payments
6. Exit

Enter your choice: 2

Enter UPI ID: raj@upi
Enter Amount: 1500

Payment Successful!
Payment Method: UPI
Amount: Rs. 1500

Enter your choice: 4

===== PAYMENT HISTORY =====

1. UPI - Rs. 1500

Enter your choice: 5

Total Payments: Rs. 1500
```

### Concepts Used

| Concept | Implementation |
|---|---|
| Class and Object | Payment classes |
| Inheritance | Payment method subclasses |
| Abstraction | PaymentMethod abstract class |
| Encapsulation | Private-like card details |
| Polymorphism | Different `pay()` implementations |
| Lists | Payment history |
| Methods | Payment operations |
| Conditional Statements | Menu handling |
| Loops | Repeated menu execution |
| Exception Handling | Invalid input handling |

### Project Challenge

After completing the basic project, add:

1. Transaction ID generation using `uuid`.
2. Payment date and time using `datetime`.
3. Search payment by transaction ID.
4. Filter payments by payment method.
5. Calculate the highest payment.
6. Save payment history to a file.

---

# PART 6 – STUDENT PRACTICE

## 24. Practice Questions

### Basic Level

1. Explain polymorphism with a real-world example.
2. What is method overriding?
3. What is duck typing?
4. Does Python support traditional method overloading?
5. What is operator overloading?
6. What are magic methods?
7. Explain encapsulation.
8. What is the difference between public and private-like attributes?
9. What is name mangling?
10. What is abstraction?

### Intermediate Level

11. Create a parent class `Animal` with a method `sound()`. Override it in `Dog`, `Cat` and `Cow`.

12. Create a `Calculator` class that accepts any number of arguments using `*args` and returns their sum.

13. Create a `Product` class with a private-like price attribute. Use `@property` to validate its price.

14. Create an abstract class `Notification` with an abstract method `send()`. Implement it in `EmailNotification` and `SMSNotification`.

15. Overload the `+` operator for a class named `Distance`.

16. Create an abstract class `Shape` with an abstract method `area()`. Implement it in `Circle`, `Rectangle` and `Triangle`.

17. Create a `BankAccount` class with private-like balance and methods for deposit, withdrawal and balance checking.

18. Create a class that implements `__str__()` and `__len__()`.

### Advanced Level

19. Design a vehicle rental system using abstraction and polymorphism.

20. Create an employee salary system where each employee type calculates salary differently.

21. Build a library management system using encapsulation for book availability.

22. Create a notification system supporting Email, SMS and WhatsApp using a common abstract interface.

23. Explain when composition is better than inheritance. Demonstrate with a practical example.

---

# PART 7 – TRAINER ASSESSMENT

## 25. Practical Assessment

Ask the student to complete these tasks without copying the examples:

| Task | Marks |
|---|---:|
| Implement method overriding | 10 |
| Demonstrate duck typing | 10 |
| Implement operator overloading | 10 |
| Use encapsulation with validation | 15 |
| Implement a property using `@property` | 10 |
| Create an abstract class | 15 |
| Implement polymorphism with multiple objects | 10 |
| Complete the Payment Processing System | 20 |
| **Total** | **100** |

### Oral Questions

1. What is the difference between inheritance and polymorphism?
2. Why is method overriding useful?
3. How does duck typing work?
4. Why does Python use name mangling?
5. Are private-like attributes completely inaccessible?
6. What is the purpose of `@property`?
7. What is an abstract method?
8. Can we create an object of an abstract class with unimplemented abstract methods?
9. What is the difference between abstraction and encapsulation?
10. What is the difference between inheritance and composition?

---

## 26. Completion Criteria

The student should be able to:

- Explain the four major OOP pillars.
- Demonstrate polymorphism using method overriding.
- Understand and implement duck typing.
- Use default arguments and `*args` as alternatives to traditional method overloading.
- Implement basic operator overloading.
- Apply encapsulation using naming conventions and properties.
- Validate attribute values using setters.
- Create abstract classes using `ABC`.
- Implement abstract methods in child classes.
- Explain abstraction, encapsulation and polymorphism with practical examples.
- Complete the Payment Processing Management System.

**Day 30 Completed – Polymorphism, Encapsulation & Abstraction**

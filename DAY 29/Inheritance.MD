
# Day 29 – Inheritance in Python

## 1. Introduction to Inheritance

Inheritance is an Object-Oriented Programming (OOP) concept that allows one class to acquire the attributes and methods of another class.

It helps us reuse existing code instead of writing the same functionality repeatedly.

### Real-World Example

Consider a company with different types of employees:

- Manager
- Developer
- Designer

All employees have some common properties:

- Name
- Employee ID
- Salary

However, each employee type may have additional properties and responsibilities.

Instead of creating completely separate classes with duplicated code, we can create a common `Employee` class and inherit it into other classes.

### Basic Terminology

- **Parent Class:** The class whose features are inherited.
- **Child Class:** The class that inherits features from another class.
- **Base Class:** Another name for the parent class.
- **Derived Class:** Another name for the child class.

---

## 2. Why Do We Need Inheritance?

Inheritance helps us:

1. Reuse existing code.
2. Reduce code duplication.
3. Organize related classes.
4. Extend existing functionality.
5. Maintain common behavior in one place.
6. Build hierarchical relationships between classes.

### Without Inheritance

```python
class Manager:

    def __init__(self, name, salary):
        self.name = name
        self.salary = salary

    def display(self):
        print("Name:", self.name)
        print("Salary:", self.salary)


class Developer:

    def __init__(self, name, salary):
        self.name = name
        self.salary = salary

    def display(self):
        print("Name:", self.name)
        print("Salary:", self.salary)


manager = Manager("Raj", 60000)
developer = Developer("Aman", 45000)

manager.display()
developer.display()
```

The same initialization and display functionality is repeated.

### With Inheritance

```python
class Employee:

    def __init__(self, name, salary):
        self.name = name
        self.salary = salary

    def display(self):
        print("Name:", self.name)
        print("Salary:", self.salary)


class Manager(Employee):
    pass


class Developer(Employee):
    pass


manager = Manager("Raj", 60000)
developer = Developer("Aman", 45000)

manager.display()
developer.display()
```

Output:

```text
Name: Raj
Salary: 60000
Name: Aman
Salary: 45000
```

Both child classes reuse the constructor and method of `Employee`.

---

## 3. Basic Inheritance Syntax

### Syntax

```python
class ParentClass:
    # Parent class attributes and methods
    pass


class ChildClass(ParentClass):
    # Child class attributes and methods
    pass
```

The child class name is followed by the parent class name inside parentheses.

### Example

```python
class Animal:

    def eat(self):
        print("Animal is eating")


class Dog(Animal):
    pass


dog1 = Dog()

dog1.eat()
```

Output:

```text
Animal is eating
```

Here:

- `Animal` is the parent class.
- `Dog` is the child class.
- `Dog` inherits the `eat()` method.
- The `dog1` object can access the inherited method.

---

## 4. Parent Class and Child Class

A parent class contains common attributes and methods.

A child class inherits those features and can also define its own functionality.

Example:

```python
class Vehicle:

    def start(self):
        print("Vehicle started")

    def stop(self):
        print("Vehicle stopped")


class Car(Vehicle):

    def play_music(self):
        print("Music started")


car1 = Car()

car1.start()
car1.play_music()
car1.stop()
```

Output:

```text
Vehicle started
Music started
Vehicle stopped
```

The `Car` class has access to:

- Its own `play_music()` method.
- The inherited `start()` method.
- The inherited `stop()` method.

---

## 5. Types of Inheritance in Python

Python supports several inheritance structures.

The commonly taught types are:

1. Single Inheritance
2. Multiple Inheritance
3. Multilevel Inheritance
4. Hierarchical Inheritance
5. Hybrid Inheritance

Let's understand each type.

---

## 6. Single Inheritance

Single inheritance occurs when one child class inherits from one parent class.

### Structure

```text
Parent Class
     |
     v
Child Class
```

### Example

```python
class Animal:

    def eat(self):
        print("Animal eats food")


class Dog(Animal):

    def bark(self):
        print("Dog barks")


dog1 = Dog()

dog1.eat()
dog1.bark()
```

Output:

```text
Animal eats food
Dog barks
```

### Explanation

- `Animal` is the parent class.
- `Dog` is the child class.
- `Dog` inherits `eat()`.
- `Dog` also defines its own `bark()` method.

This is called single inheritance because one child inherits from one parent.

---

## 7. Multilevel Inheritance

Multilevel inheritance occurs when a class inherits from another child class, creating multiple levels.

### Structure

```text
Grandparent Class
       |
       v
Parent Class
       |
       v
Child Class
```

### Example

```python
class Grandparent:

    def show_grandparent(self):
        print("This is the Grandparent class")


class Parent(Grandparent):

    def show_parent(self):
        print("This is the Parent class")


class Child(Parent):

    def show_child(self):
        print("This is the Child class")


child1 = Child()

child1.show_grandparent()
child1.show_parent()
child1.show_child()
```

Output:

```text
This is the Grandparent class
This is the Parent class
This is the Child class
```

### Explanation

- `Parent` inherits from `Grandparent`.
- `Child` inherits from `Parent`.
- `Child` can access methods available through both parent levels.

This structure is called multilevel inheritance.

---

## 8. Multiple Inheritance

Multiple inheritance occurs when one child class inherits from more than one parent class.

### Structure

```text
Parent A       Parent B
     \           /
      \         /
       \       /
       Child Class
```

### Example

```python
class Father:

    def father_property(self):
        print("Father owns a house")


class Mother:

    def mother_property(self):
        print("Mother owns a car")


class Child(Father, Mother):

    def child_details(self):
        print("Child inherits from both parents")


child1 = Child()

child1.father_property()
child1.mother_property()
child1.child_details()
```

Output:

```text
Father owns a house
Mother owns a car
Child inherits from both parents
```

### Explanation

- `Father` is the first parent.
- `Mother` is the second parent.
- `Child` inherits from both.
- The child can access methods from both parent classes.

### Important Note

Python supports multiple inheritance, but it can introduce complexity when parent classes define methods with the same name.

Python uses Method Resolution Order (MRO) to determine which method is selected.

We will study MRO later in this lesson.

---

## 9. Hierarchical Inheritance

Hierarchical inheritance occurs when multiple child classes inherit from the same parent class.

### Structure

```text
           Parent Class
           /          \
          /            \
         v              v
     Child A          Child B
```

### Example

```python
class Animal:

    def eat(self):
        print("Animal eats food")


class Dog(Animal):

    def bark(self):
        print("Dog barks")


class Cat(Animal):

    def meow(self):
        print("Cat meows")


dog1 = Dog()
cat1 = Cat()

dog1.eat()
dog1.bark()

cat1.eat()
cat1.meow()
```

Output:

```text
Animal eats food
Dog barks
Animal eats food
Cat meows
```

Both child classes reuse the common functionality of `Animal`.

---

## 10. Hybrid Inheritance

Hybrid inheritance combines two or more inheritance patterns.

### Example

```python
class Person:

    def show_person(self):
        print("Person information")


class Student(Person):

    def study(self):
        print("Student is studying")


class Employee(Person):

    def work(self):
        print("Employee is working")


class WorkingStudent(Student, Employee):

    def show_status(self):
        print("Student and employee")


person1 = WorkingStudent()

person1.show_person()
person1.study()
person1.work()
person1.show_status()
```

Output:

```text
Person information
Student is studying
Employee is working
Student and employee
```

### Explanation

- `Student` inherits from `Person`.
- `Employee` inherits from `Person`.
- `WorkingStudent` inherits from both `Student` and `Employee`.

This combines hierarchical and multiple inheritance.

**Note:** Hybrid inheritance can create complex inheritance relationships. Python's MRO helps determine the method lookup order.

---

## 11. The super() Function

The `super()` function provides access to methods of the next class in the Method Resolution Order.

It is commonly used to call a parent class's implementation from a child class.

### Example Without super()

```python
class Parent:

    def display(self):
        print("Parent display method")


class Child(Parent):

    def display(self):
        print("Child display method")
        Parent.display(self)


child1 = Child()

child1.display()
```

Output:

```text
Child display method
Parent display method
```

Here, we explicitly call `Parent.display(self)`.

### Example Using super()

```python
class Parent:

    def display(self):
        print("Parent display method")


class Child(Parent):

    def display(self):
        print("Child display method")
        super().display()


child1 = Child()

child1.display()
```

Output:

```text
Child display method
Parent display method
```

`super()` avoids hardcoding the parent class name and follows Python's MRO.

---

## 12. Using super() with Constructors

One of the most common uses of `super()` is calling the parent class's initializer.

Example:

```python
class Person:

    def __init__(self, name, age):
        self.name = name
        self.age = age


class Student(Person):

    def __init__(self, name, age, course):
        super().__init__(name, age)
        self.course = course

    def display(self):
        print("Name:", self.name)
        print("Age:", self.age)
        print("Course:", self.course)


student1 = Student("Raj", 21, "Python")

student1.display()
```

Output:

```text
Name: Raj
Age: 21
Course: Python
```

### Explanation

```python
super().__init__(name, age)
```

This calls the next initializer in the MRO.

The parent initializes:

- `name`
- `age`

The child initializes:

- `course`

This avoids repeating the parent's initialization code.

---

## 13. Method Overriding

Method overriding occurs when a child class defines a method with the same name as a method inherited from its parent class.

The child implementation is used when that method is called on the child object.

### Example

```python
class Animal:

    def sound(self):
        print("Animal makes a sound")


class Dog(Animal):

    def sound(self):
        print("Dog barks")


dog1 = Dog()

dog1.sound()
```

Output:

```text
Dog barks
```

The `Dog` class overrides the `sound()` method of `Animal`.

### Calling the Parent Method After Overriding

We can still call the parent implementation using `super()`.

```python
class Animal:

    def sound(self):
        print("Animal makes a sound")


class Dog(Animal):

    def sound(self):
        super().sound()
        print("Dog barks")


dog1 = Dog()

dog1.sound()
```

Output:

```text
Animal makes a sound
Dog barks
```

---

## 14. Method Resolution Order (MRO)

Method Resolution Order defines the order in which Python searches classes for a method or attribute.

It becomes especially important in multiple and hybrid inheritance.

### Example

```python
class A:

    def show(self):
        print("Class A")


class B(A):

    def show(self):
        print("Class B")


class C(A):

    def show(self):
        print("Class C")


class D(B, C):
    pass


obj = D()

obj.show()
```

Output:

```text
Class B
```

Why?

Because Python checks classes according to the MRO.

### Checking MRO

Use the `mro()` method or the `__mro__` attribute.

```python
print(D.mro())
```

Output will look like:

```text
[<class '__main__.D'>,
 <class '__main__.B'>,
 <class '__main__.C'>,
 <class '__main__.A'>,
 <class 'object'>]
```

The exact display includes Python class representations.

The lookup order is:

```text
D → B → C → A → object
```

### Another Way

```python
print(D.__mro__)
```

Both methods show the class lookup order.

### Important: The object Class

In Python, almost all user-defined classes ultimately inherit from the built-in `object` class.

Example:

```python
class Student:
    pass


print(Student.__bases__)
```

Output:

```text
(<class 'object'>,)
```

---

## 15. Inheritance and Attribute Access

A child class can access inherited attributes and methods.

Example:

```python
class Employee:

    company = "Tech Solutions"

    def __init__(self, name, salary):
        self.name = name
        self.salary = salary


class Manager(Employee):

    def show_details(self):
        print("Company:", self.company)
        print("Name:", self.name)
        print("Salary:", self.salary)


manager1 = Manager("Raj", 60000)

manager1.show_details()
```

Output:

```text
Company: Tech Solutions
Name: Raj
Salary: 60000
```

The child class accesses:

- The inherited class attribute `company`.
- The inherited instance attributes `name` and `salary`.

---

## 16. Checking Inheritance Relationships

Python provides built-in functions to inspect inheritance relationships.

### 16.1 issubclass()

`issubclass()` checks whether one class inherits from another class.

Syntax:

```python
issubclass(child_class, parent_class)
```

Example:

```python
class Animal:
    pass


class Dog(Animal):
    pass


class Cat:
    pass


print(issubclass(Dog, Animal))
print(issubclass(Cat, Animal))
```

Output:

```text
True
False
```

### 16.2 isinstance()

`isinstance()` checks whether an object belongs to a class or one of its subclasses.

Example:

```python
class Animal:
    pass


class Dog(Animal):
    pass


dog1 = Dog()

print(isinstance(dog1, Dog))
print(isinstance(dog1, Animal))
```

Output:

```text
True
True
```

A `Dog` object is also considered an instance of `Animal` because `Dog` inherits from `Animal`.

### 16.3 Accessing Parent Classes

Use `__bases__` to inspect the direct parent classes.

```python
class A:
    pass


class B:
    pass


class C(A, B):
    pass


print(C.__bases__)
```

Output:

```text
(<class '__main__.A'>, <class '__main__.B'>)
```

---

## 17. Inheritance with Different Constructors

A child class may define its own constructor.

If the child defines `__init__()`, Python does not automatically call the parent's `__init__()`.

Use `super()` when the parent initialization is required.

### Example Without Calling Parent Constructor

```python
class Person:

    def __init__(self, name):
        self.name = name


class Student(Person):

    def __init__(self, course):
        self.course = course


student1 = Student("Python")

print(student1.course)
```

Output:

```text
Python
```

However, the object does not have a `name` attribute because the parent initializer was not called.

### Correct Example

```python
class Person:

    def __init__(self, name):
        self.name = name


class Student(Person):

    def __init__(self, name, course):
        super().__init__(name)
        self.course = course


student1 = Student("Raj", "Python")

print(student1.name)
print(student1.course)
```

Output:

```text
Raj
Python
```

---

## 18. Multiple Inheritance and super()

In multiple inheritance, `super()` follows MRO rather than simply calling a particular parent class.

Example:

```python
class A:

    def show(self):
        print("Class A")
        super().show()


class B:

    def show(self):
        print("Class B")
        super().show()


class C:

    def show(self):
        print("Class C")


class D(A, B, C):
    pass


obj = D()

obj.show()
```

Output:

```text
Class A
Class B
Class C
```

### Explanation

The MRO is:

```text
D → A → B → C → object
```

Each `super().show()` moves to the next class in the MRO.

This pattern is useful in cooperative multiple inheritance.

However, every class in such a method chain must be designed to cooperate correctly. For complex applications, avoid mixing unrelated inheritance designs.

---

## 19. Private and Protected-Like Attributes in Inheritance

Python uses naming conventions and name mangling to manage attribute visibility.

### 19.1 Public Attributes

Public attributes can be accessed normally.

```python
class Parent:

    def __init__(self):
        self.name = "Raj"


class Child(Parent):
    pass


obj = Child()

print(obj.name)
```

### 19.2 Protected-Like Attributes

A single leading underscore indicates that an attribute is intended for internal use.

```python
class Parent:

    def __init__(self):
        self._salary = 50000


class Child(Parent):

    def display(self):
        print("Salary:", self._salary)


obj = Child()

obj.display()
```

Output:

```text
Salary: 50000
```

The underscore is a convention, not strict access control.

### 19.3 Private-Like Attributes

A double leading underscore triggers name mangling.

```python
class Parent:

    def __init__(self):
        self.__password = "secret"

    def show_password(self):
        print(self.__password)


class Child(Parent):

    def display(self):
        self.show_password()


obj = Child()

obj.display()
```

Output:

```text
secret
```

The child can use the inherited public method, but it cannot directly access `self.__password` using that name.

Python changes the internal attribute name to include the class name.

Name mangling is not a security mechanism; it mainly helps avoid accidental name conflicts.

---

## 20. Advantages and Disadvantages of Inheritance

### Advantages

1. Code reusability.
2. Reduced code duplication.
3. Easier maintenance of shared functionality.
4. Logical class relationships.
5. Easier extension of existing classes.
6. Supports method overriding and polymorphism.

### Disadvantages

1. Deep inheritance hierarchies can become difficult to understand.
2. Changes in a parent class may affect multiple child classes.
3. Multiple inheritance can create complicated method lookup.
4. Child classes can become tightly coupled to parent classes.
5. Inheritance may be unnecessary when classes do not have a genuine "is-a" relationship.

**Best Practice:** Use inheritance when a child class genuinely represents a specialized form of its parent. Otherwise, consider composition.

---

# 21. Practical Programs

## Program 1: Person and Student

```python
class Person:

    def __init__(self, name, age):
        self.name = name
        self.age = age

    def display_person(self):
        print("Name:", self.name)
        print("Age:", self.age)


class Student(Person):

    def __init__(self, name, age, course):
        super().__init__(name, age)
        self.course = course

    def display_student(self):
        self.display_person()
        print("Course:", self.course)


student1 = Student("Raj", 21, "Python")

student1.display_student()
```

## Program 2: Employee and Manager

```python
class Employee:

    def __init__(self, name, salary):
        self.name = name
        self.salary = salary

    def display(self):
        print("Name:", self.name)
        print("Salary:", self.salary)


class Manager(Employee):

    def __init__(self, name, salary, department):
        super().__init__(name, salary)
        self.department = department

    def display(self):
        super().display()
        print("Department:", self.department)


manager1 = Manager("Raj", 70000, "IT")

manager1.display()
```

## Program 3: Vehicle and Car

```python
class Vehicle:

    def __init__(self, brand, speed):
        self.brand = brand
        self.speed = speed

    def display_vehicle(self):
        print("Brand:", self.brand)
        print("Speed:", self.speed)


class Car(Vehicle):

    def __init__(self, brand, speed, fuel_type):
        super().__init__(brand, speed)
        self.fuel_type = fuel_type

    def display_car(self):
        self.display_vehicle()
        print("Fuel Type:", self.fuel_type)


car1 = Car("Toyota", 180, "Petrol")

car1.display_car()
```

## Program 4: Animal Sound

```python
class Animal:

    def sound(self):
        print("Animal makes a sound")


class Dog(Animal):

    def sound(self):
        print("Dog barks")


class Cat(Animal):

    def sound(self):
        print("Cat meows")


dog1 = Dog()
cat1 = Cat()

dog1.sound()
cat1.sound()
```

## Program 5: Multiple Inheritance

```python
class Camera:

    def take_photo(self):
        print("Photo captured")


class MusicPlayer:

    def play_music(self):
        print("Music playing")


class Smartphone(Camera, MusicPlayer):

    def make_call(self):
        print("Calling...")


phone1 = Smartphone()

phone1.take_photo()
phone1.play_music()
phone1.make_call()
```

## Program 6: Hierarchical Inheritance

```python
class Shape:

    def show_category(self):
        print("This is a geometric shape")


class Circle(Shape):

    def calculate_area(self, radius):
        return 3.14159 * radius ** 2


class Rectangle(Shape):

    def calculate_area(self, length, width):
        return length * width


circle1 = Circle()
rectangle1 = Rectangle()

circle1.show_category()
print("Circle Area:", circle1.calculate_area(7))

rectangle1.show_category()
print("Rectangle Area:", rectangle1.calculate_area(10, 5))
```

## Program 7: Multilevel Inheritance

```python
class Person:

    def __init__(self, name):
        self.name = name


class Employee(Person):

    def __init__(self, name, employee_id):
        super().__init__(name)
        self.employee_id = employee_id


class Manager(Employee):

    def __init__(self, name, employee_id, department):
        super().__init__(name, employee_id)
        self.department = department

    def display(self):
        print("Name:", self.name)
        print("Employee ID:", self.employee_id)
        print("Department:", self.department)


manager1 = Manager("Raj", 101, "IT")

manager1.display()
```

---

# 22. Mini Project – Employee Role Management System

## Project Description

Create an Employee Role Management System using inheritance.

The application should support different employee roles:

- General Employee
- Developer
- Manager

All employee types should share common information, while each role has its own additional attributes and behavior.

### Requirements

1. Create a parent class named `Employee`.
2. Store employee ID, name and basic salary.
3. Create a `Developer` child class.
4. Create a `Manager` child class.
5. Use `super()` to initialize parent attributes.
6. Add role-specific attributes.
7. Override the display method.
8. Calculate salary based on role.
9. Create multiple employee objects.
10. Display employee information.

## Complete Project Code

```python
class Employee:

    company_name = "Tech Solutions"

    def __init__(self, employee_id, name, basic_salary):
        if not employee_id:
            raise ValueError("Employee ID cannot be empty")

        if not name.strip():
            raise ValueError("Employee name cannot be empty")

        if basic_salary < 0:
            raise ValueError("Salary cannot be negative")

        self.employee_id = employee_id
        self.name = name
        self.basic_salary = basic_salary

    def calculate_salary(self):
        return self.basic_salary

    def display(self):
        print("\nCompany:", Employee.company_name)
        print("Employee ID:", self.employee_id)
        print("Name:", self.name)
        print("Role: General Employee")
        print("Total Salary:", self.calculate_salary())


class Developer(Employee):

    def __init__(
        self,
        employee_id,
        name,
        basic_salary,
        programming_language
    ):
        super().__init__(employee_id, name, basic_salary)
        self.programming_language = programming_language

    def calculate_salary(self):
        bonus = self.basic_salary * 0.15
        return self.basic_salary + bonus

    def display(self):
        print("\nCompany:", Employee.company_name)
        print("Employee ID:", self.employee_id)
        print("Name:", self.name)
        print("Role: Developer")
        print("Programming Language:", self.programming_language)
        print("Basic Salary:", self.basic_salary)
        print("Total Salary:", self.calculate_salary())


class Manager(Employee):

    def __init__(
        self,
        employee_id,
        name,
        basic_salary,
        department,
        team_size
    ):
        super().__init__(employee_id, name, basic_salary)
        self.department = department
        self.team_size = team_size

    def calculate_salary(self):
        bonus = self.basic_salary * 0.25
        return self.basic_salary + bonus

    def display(self):
        print("\nCompany:", Employee.company_name)
        print("Employee ID:", self.employee_id)
        print("Name:", self.name)
        print("Role: Manager")
        print("Department:", self.department)
        print("Team Size:", self.team_size)
        print("Basic Salary:", self.basic_salary)
        print("Total Salary:", self.calculate_salary())


class EmployeeManagementSystem:

    def __init__(self):
        self.employees = []

    def add_employee(self):

        try:
            employee_id = input("Enter employee ID: ").strip()

            if any(
                employee.employee_id == employee_id
                for employee in self.employees
            ):
                raise ValueError("Employee ID already exists")

            name = input("Enter employee name: ").strip()

            basic_salary = float(
                input("Enter basic salary: ")
            )

            print("\nSelect Employee Role")
            print("1. General Employee")
            print("2. Developer")
            print("3. Manager")

            role = input("Enter role choice: ").strip()

            if role == "1":

                employee = Employee(
                    employee_id,
                    name,
                    basic_salary
                )

            elif role == "2":

                language = input(
                    "Enter programming language: "
                ).strip()

                employee = Developer(
                    employee_id,
                    name,
                    basic_salary,
                    language
                )

            elif role == "3":

                department = input(
                    "Enter department: "
                ).strip()

                team_size = int(
                    input("Enter team size: ")
                )

                if team_size < 0:
                    raise ValueError(
                        "Team size cannot be negative"
                    )

                employee = Manager(
                    employee_id,
                    name,
                    basic_salary,
                    department,
                    team_size
                )

            else:
                print("Invalid role choice!")
                return

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

        employee_id = input(
            "Enter employee ID: "
        ).strip()

        for employee in self.employees:

            if employee.employee_id == employee_id:
                employee.display()
                return

        print("Employee not found!")

    def calculate_total_salary(self):

        total = sum(
            employee.calculate_salary()
            for employee in self.employees
        )

        print("Total Salary Expense:", total)

    def run(self):

        while True:

            print("\n===== EMPLOYEE ROLE MANAGEMENT =====")
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
                print("Thank you!")
                break

            else:
                print("Invalid choice!")


system = EmployeeManagementSystem()

system.run()
```

## Sample Output

```text
===== EMPLOYEE ROLE MANAGEMENT =====
1. Add Employee
2. Display All Employees
3. Search Employee
4. Calculate Total Salary
5. Exit

Enter your choice: 1

Enter employee ID: 101
Enter employee name: Raj
Enter basic salary: 40000

Select Employee Role
1. General Employee
2. Developer
3. Manager

Enter role choice: 2
Enter programming language: Python

Employee added successfully!

Enter your choice: 2

Company: Tech Solutions
Employee ID: 101
Name: Raj
Role: Developer
Programming Language: Python
Basic Salary: 40000.0
Total Salary: 46000.0
```

### Project Improvement Tasks

1. Add a Designer employee class.
2. Add an HR Manager class.
3. Add employee deletion.
4. Add employee updates.
5. Search employees by role.
6. Display the highest-paid employee.
7. Calculate role-wise salary expenses.
8. Store employee information in a file.

---

# 23. Student Practice Exercises

## Basic Level

1. Create a `Person` parent class and a `Student` child class.
2. Create an `Animal` class and inherit it into `Dog`.
3. Create a `Vehicle` parent class and a `Car` child class.
4. Create an `Employee` parent class and a `Manager` child class.
5. Demonstrate single inheritance using a `Shape` class.
6. Create a child class that accesses a parent method.

## Intermediate Level

7. Create a multilevel inheritance structure using `Person`, `Employee` and `Manager`.
8. Create multiple inheritance using `Camera`, `MusicPlayer` and `Smartphone`.
9. Create hierarchical inheritance using `Animal`, `Dog` and `Cat`.
10. Use `super()` to call a parent constructor.
11. Override a parent method in a child class.
12. Demonstrate the difference between inherited and overridden methods.
13. Use `issubclass()` and `isinstance()` to inspect inheritance.

## Advanced Level

14. Create a hybrid inheritance example.
15. Create a multiple inheritance example and inspect its MRO.
16. Create a class hierarchy for a school management system.
17. Create a vehicle rental system using inheritance.
18. Create an employee payroll system with multiple employee roles.
19. Create a banking system with different account types.
20. Build a Library Management System using inheritance.

---

# 24. Trainer Assessment

Ask the student to explain and demonstrate:

1. What is inheritance?
2. Why do we use inheritance?
3. What is a parent class?
4. What is a child class?
5. What is single inheritance?
6. What is multiple inheritance?
7. What is multilevel inheritance?
8. What is hierarchical inheritance?
9. What is hybrid inheritance?
10. What is the purpose of `super()`?
11. What is method overriding?
12. What is Method Resolution Order?
13. How can we check a class's MRO?
14. What happens when a child class defines its own constructor?
15. What is the difference between `issubclass()` and `isinstance()`?
16. What is name mangling?
17. What are the advantages and disadvantages of inheritance?
18. When should we prefer composition over inheritance?

## Practical Assessment

Ask the student to independently:

- Create a parent class with attributes and methods.
- Create at least two child classes.
- Demonstrate single inheritance.
- Demonstrate multilevel inheritance.
- Demonstrate multiple inheritance.
- Use `super()` in a child constructor.
- Override at least one parent method.
- Inspect MRO.
- Build an employee role management application.

---

# 25. Day 29 Completion Criteria

The student should be able to:

- Understand inheritance.
- Create parent and child classes.
- Implement single inheritance.
- Implement multiple inheritance.
- Implement multilevel inheritance.
- Implement hierarchical inheritance.
- Understand hybrid inheritance.
- Use `super()` correctly.
- Override inherited methods.
- Understand Method Resolution Order.
- Inspect inheritance using `mro()` and `__mro__`.
- Use `issubclass()` and `isinstance()`.
- Understand inheritance and constructor behavior.
- Understand public, protected-like and private-like attributes.
- Build applications using inheritance.
- Complete the Employee Role Management System.

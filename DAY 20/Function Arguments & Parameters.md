
# Day 20 – Function Arguments & Parameters

## 1. Introduction to Function Arguments

In Day 19, we learned how to create and call functions using parameters and arguments.

Today, we will explore different ways of passing information to functions.

Consider this example:

```python
def greet(name):
    print("Hello", name)

greet("Raj")
```

**Output:**
```text
Hello Raj
```

Here:
- `name` is a parameter.
- `"Raj"` is an argument.

### Parameter vs Argument

| Parameter | Argument |
|---|---|
| Variable defined inside the function definition | Actual value passed when calling the function |
| Receives data | Supplies data |
| Example: `name` | Example: `"Raj"` |

---

## 2. Positional Arguments

Positional arguments are passed according to the position of parameters in the function definition.

### Example 1: Basic positional arguments

```python
def student_details(name, age, course):
    print("Name:", name)
    print("Age:", age)
    print("Course:", course)

student_details("Raj", 21, "Python")
```

**Output:**
```text
Name: Raj
Age: 21
Course: Python
```

Python assigns:
- `"Raj"` to `name`
- `21` to `age`
- `"Python"` to `course`

### Example 2: Changing the order

```python
def introduce(name, city):
    print(name, "lives in", city)

introduce("Raj", "Mumbai")
introduce("Mumbai", "Raj")
```

**Output:**
```text
Raj lives in Mumbai
Mumbai lives in Raj
```

The second call produces an incorrect meaning because positional arguments are assigned by position.

**Important:** The order of positional arguments matters.

### Practice

Create a function that accepts:
- Product name
- Price
- Quantity

Display all three values.

---

## 3. Keyword Arguments

Keyword arguments are passed using parameter names.

They allow us to specify which value belongs to which parameter.

### Example

```python
def student_details(name, age, course):
    print("Name:", name)
    print("Age:", age)
    print("Course:", course)

student_details(
    course="Python",
    name="Raj",
    age=21
)
```

**Output:**
```text
Name: Raj
Age: 21
Course: Python
```

Notice that the order is different, but Python assigns the values correctly.

### Positional vs Keyword Arguments

```python
def calculate_area(length, width):
    print("Area:", length * width)

# Positional arguments
calculate_area(10, 5)

# Keyword arguments
calculate_area(length=10, width=5)

# Keyword arguments in a different order
calculate_area(width=5, length=10)
```

**Output:**
```text
Area: 50
Area: 50
Area: 50
```

### Advantages of Keyword Arguments

- Improve code readability.
- Allow arguments to be passed in a different order.
- Make function calls easier to understand.
- Useful when functions have many parameters.

---

## 4. Default Arguments

A default argument is a parameter that already has a value in the function definition.

If the caller does not provide that argument, Python uses its default value.

### Example 1: Basic default argument

```python
def greet(name, message="Welcome"):
    print(message, name)

greet("Raj")
greet("Altaf", "Good Morning")
```

**Output:**
```text
Welcome Raj
Good Morning Altaf
```

Explanation:

- First call: `message` uses its default value.
- Second call: `"Good Morning"` replaces the default value.

### Example 2: Default values in calculations

```python
def calculate_bill(price, quantity=1):
    total = price * quantity
    print("Total Bill:", total)

calculate_bill(500)
calculate_bill(500, 3)
```

**Output:**
```text
Total Bill: 500
Total Bill: 1500
```

### Important Rule: Default Parameter Ordering

Parameters without default values must come before parameters with default values.

**Correct:**

```python
def student(name, age, course="Python"):
    print(name, age, course)

student("Raj", 21)
```

**Output:**
```text
Raj 21 Python
```

**Incorrect:**

```python
def student(name, course="Python", age):
    print(name, age, course)
```

This produces a `SyntaxError`.

Reason: A non-default parameter cannot follow a default parameter.

---

## 5. Combining Positional and Keyword Arguments

Python allows us to combine positional and keyword arguments.

However, positional arguments must come before keyword arguments.

### Correct Example

```python
def employee(name, department, salary):
    print("Name:", name)
    print("Department:", department)
    print("Salary:", salary)

employee("Raj", department="IT", salary=35000)
```

**Output:**
```text
Name: Raj
Department: IT
Salary: 35000
```

### Incorrect Example

```python
def employee(name, department, salary):
    print(name, department, salary)

employee(name="Raj", "IT", 35000)
```

This produces a `SyntaxError`.

**Rule:**

```python
function(positional_arguments, keyword_arguments)
```

Do not place positional arguments after keyword arguments.

### Another Common Error

```python
def student(name, age):
    print(name, age)

student("Raj", name="Altaf", age=21)
```

This produces a `TypeError` because `name` receives two values.

---

## 6. Variable-Length Positional Arguments – *args

Sometimes we do not know how many positional arguments a function will receive.

Python provides `*args` for this situation.

`*args` collects additional positional arguments into a tuple.

### Example 1: Basic *args

```python
def add_numbers(*args):
    print(args)

add_numbers(10, 20, 30)
add_numbers(5, 10)
add_numbers(1, 2, 3, 4, 5)
```

**Output:**
```text
(10, 20, 30)
(5, 10)
(1, 2, 3, 4, 5)
```

Notice that the values are stored in a tuple.

### Example 2: Calculate the sum

```python
def add_numbers(*args):
    total = 0

    for number in args:
        total += number

    return total

print(add_numbers(10, 20))
print(add_numbers(10, 20, 30))
print(add_numbers(5, 10, 15, 20, 25))
```

**Output:**
```text
30
60
75
```

### Example 3: Find the maximum number

```python
def find_maximum(*numbers):
    if len(numbers) == 0:
        return None

    maximum = numbers[0]

    for number in numbers:
        if number > maximum:
            maximum = number

    return maximum

print(find_maximum(10, 50, 20, 80, 30))
print(find_maximum(5, 15, 25))
```

**Output:**
```text
80
25
```

### Example 4: Normal parameter with *args

```python
def student_marks(name, *marks):
    print("Student:", name)
    print("Marks:", marks)

    total = sum(marks)
    print("Total:", total)

student_marks("Raj", 80, 90, 85, 95)
```

**Output:**
```text
Student: Raj
Marks: (80, 90, 85, 95)
Total: 350
```

**Important:**

- `args` is a conventional name, not a reserved keyword.
- `*` is what makes the parameter collect extra positional arguments.
- Inside the function, `args` is a tuple.

---

## 7. Variable-Length Keyword Arguments – **kwargs

Sometimes a function needs to accept an unknown number of keyword arguments.

Python provides `**kwargs`.

It collects additional keyword arguments into a dictionary.

### Example 1: Basic **kwargs

```python
def student_details(**kwargs):
    print(kwargs)

student_details(
    name="Raj",
    age=21,
    course="Python"
)
```

**Output:**
```text
{'name': 'Raj', 'age': 21, 'course': 'Python'}
```

### Example 2: Accessing dictionary values

```python
def student_details(**kwargs):
    for key, value in kwargs.items():
        print(key, ":", value)

student_details(
    name="Raj",
    age=21,
    city="Mumbai",
    course="Python"
)
```

**Output:**
```text
name : Raj
age : 21
city : Mumbai
course : Python
```

### Example 3: Employee profile

```python
def employee_profile(**details):
    print("Employee Profile")

    for key, value in details.items():
        print(f"{key}: {value}")

employee_profile(
    name="Raj",
    department="IT",
    salary=35000,
    city="Mumbai",
    experience="1 Year"
)
```

**Output:**
```text
Employee Profile
name: Raj
department: IT
salary: 35000
city: Mumbai
experience: 1 Year
```

**Important:**

- `kwargs` is a conventional name.
- `**` collects extra keyword arguments.
- Inside the function, `kwargs` is a dictionary.

---

## 8. Using *args and **kwargs Together

We can use normal parameters, `*args`, keyword-only parameters and `**kwargs` in one function.

### Example

```python
def order_details(customer, *items, payment_method="Cash", **extra_details):
    print("Customer:", customer)
    print("Items:", items)
    print("Payment Method:", payment_method)
    print("Additional Details:", extra_details)

order_details(
    "Raj",
    "Laptop",
    "Mouse",
    "Keyboard",
    payment_method="UPI",
    city="Mumbai",
    delivery="Express"
)
```

**Output:**
```text
Customer: Raj
Items: ('Laptop', 'Mouse', 'Keyboard')
Payment Method: UPI
Additional Details: {'city': 'Mumbai', 'delivery': 'Express'}
```

### Understanding Parameter Order

A function can use parameters in this general order:

```python
def example(normal, *args, keyword_only=None, **kwargs):
    pass
```

The order is:

1. Normal positional or positional-or-keyword parameters.
2. `*args` for extra positional arguments.
3. Keyword-only parameters.
4. `**kwargs` for extra keyword arguments.

We will explore keyword-only parameters in the next section.

---

## 9. Keyword-Only Arguments

Keyword-only arguments must be passed using their parameter names.

We can create keyword-only parameters by placing `*` in the function definition.

### Example

```python
def create_account(name, *, email, password):
    print("Name:", name)
    print("Email:", email)
    print("Password:", password)

create_account(
    "Raj",
    email="raj@example.com",
    password="12345"
)
```

**Output:**
```text
Name: Raj
Email: raj@example.com
Password: 12345
```

### Incorrect Example

```python
def create_account(name, *, email, password):
    print(name, email, password)

create_account("Raj", "raj@example.com", "12345")
```

This produces a `TypeError`.

Reason: `email` and `password` are keyword-only parameters.

### Why Are Keyword-Only Arguments Useful?

Consider a function that accepts many settings:

```python
def connect_database(host, *, port, username, timeout):
    print("Host:", host)
    print("Port:", port)
    print("Username:", username)
    print("Timeout:", timeout)

connect_database(
    "localhost",
    port=3306,
    username="admin",
    timeout=30
)
```

Keyword-only parameters make function calls easier to read and reduce mistakes.

---

## 10. Positional-Only Arguments

Positional-only arguments must be passed according to their position.

Python provides `/` to define positional-only parameters.

This feature is available in Python 3.8 and later.

### Example

```python
def calculate_area(length, width, /):
    return length * width

print(calculate_area(10, 5))
```

**Output:**
```text
50
```

### Incorrect Example

```python
def calculate_area(length, width, /):
    return length * width

print(calculate_area(length=10, width=5))
```

This produces a `TypeError`.

Reason: Both parameters are positional-only.

### Combining Positional-Only and Keyword-Only Arguments

```python
def calculate_bill(price, quantity, /, *, discount, tax):
    subtotal = price * quantity
    final_amount = subtotal - discount + tax

    return final_amount

result = calculate_bill(
    500,
    2,
    discount=50,
    tax=20
)

print("Final Amount:", result)
```

**Output:**
```text
Final Amount: 970
```

Here:
- `price` and `quantity` are positional-only.
- `discount` and `tax` are keyword-only.

---

## 11. Argument Unpacking

Argument unpacking allows us to pass values from an existing collection into a function.

Python uses:
- `*` to unpack an iterable into positional arguments.
- `**` to unpack a dictionary into keyword arguments.

### Example 1: Unpacking a list using *

```python
def add_numbers(a, b, c):
    print("Total:", a + b + c)

numbers = [10, 20, 30]

add_numbers(*numbers)
```

**Output:**
```text
Total: 60
```

Python effectively passes:

```python
add_numbers(10, 20, 30)
```

### Example 2: Unpacking a tuple

```python
def student(name, age, course):
    print(name, age, course)

details = ("Raj", 21, "Python")

student(*details)
```

**Output:**
```text
Raj 21 Python
```

### Example 3: Unpacking a dictionary using **

```python
def employee(name, department, salary):
    print("Name:", name)
    print("Department:", department)
    print("Salary:", salary)

details = {
    "name": "Raj",
    "department": "IT",
    "salary": 35000
}

employee(**details)
```

**Output:**
```text
Name: Raj
Department: IT
Salary: 35000
```

The dictionary keys must match the function's parameter names.

### Example 4: Combining * and **

```python
def order(customer, product, quantity, payment):
    print("Customer:", customer)
    print("Product:", product)
    print("Quantity:", quantity)
    print("Payment:", payment)

basic_details = ("Raj", "Laptop")
extra_details = {
    "quantity": 2,
    "payment": "UPI"
}

order(*basic_details, **extra_details)
```

**Output:**
```text
Customer: Raj
Product: Laptop
Quantity: 2
Payment: UPI
```

---

## 12. Passing Lists and Dictionaries to Functions

Functions can receive collections such as lists and dictionaries as arguments.

### Example 1: Passing a list

```python
def display_marks(marks):
    for mark in marks:
        print(mark)

student_marks = [80, 90, 85, 95]

display_marks(student_marks)
```

**Output:**
```text
80
90
85
95
```

### Example 2: Modifying a list inside a function

```python
def add_item(items):
    items.append("Keyboard")

products = ["Laptop", "Mouse"]

add_item(products)

print(products)
```

**Output:**
```text
['Laptop', 'Mouse', 'Keyboard']
```

The original list changes because the function modifies the same list object.

### Example 3: Reassigning a parameter

```python
def replace_list(items):
    items = ["Monitor", "Printer"]

products = ["Laptop", "Mouse"]

replace_list(products)

print(products)
```

**Output:**
```text
['Laptop', 'Mouse']
```

The original list remains unchanged.

Reason: Reassigning the local parameter does not replace the caller's variable.

### Example 4: Modifying a dictionary

```python
def update_employee(employee):
    employee["salary"] = 40000
    employee["city"] = "Mumbai"

details = {
    "name": "Raj",
    "salary": 30000
}

update_employee(details)

print(details)
```

**Output:**
```text
{'name': 'Raj', 'salary': 40000, 'city': 'Mumbai'}
```

**Important:** Mutable objects such as lists and dictionaries can be modified inside functions. These changes can be visible to the caller.

---

## 13. Common Function Argument Errors

Understanding argument errors helps us debug Python programs.

### Error 1: Missing Required Argument

```python
def greet(name):
    print("Hello", name)

greet()
```

**Error:**
```text
TypeError: missing 1 required positional argument: 'name'
```

Reason: The function requires one argument, but none was provided.

### Error 2: Too Many Positional Arguments

```python
def add(a, b):
    print(a + b)

add(10, 20, 30)
```

**Error:**
```text
TypeError: takes 2 positional arguments but 3 were given
```

Reason: The function accepts only two positional arguments.

### Error 3: Unexpected Keyword Argument

```python
def student(name):
    print(name)

student(username="Raj")
```

**Error:**
```text
TypeError: got an unexpected keyword argument 'username'
```

Reason: The function does not have a parameter named `username`.

### Error 4: Multiple Values for One Parameter

```python
def employee(name, salary):
    print(name, salary)

employee("Raj", name="Altaf", salary=30000)
```

**Error:**
```text
TypeError: got multiple values for argument 'name'
```

Reason: `name` receives both a positional and a keyword value.

---

## 14. Mutable Default Argument Problem

This is an important Python concept.

Consider the following code:

### Incorrect Approach

```python
def add_student(name, students=[]):
    students.append(name)
    return students

print(add_student("Raj"))
print(add_student("Altaf"))
print(add_student("Aman"))
```

**Output:**
```text
['Raj']
['Raj', 'Altaf']
['Raj', 'Altaf', 'Aman']
```

Why does this happen?

Python creates the default list once when the function is defined. The same list is reused across calls that omit the argument.

This can cause unexpected results.

### Correct Approach: Use None

```python
def add_student(name, students=None):
    if students is None:
        students = []

    students.append(name)

    return students

print(add_student("Raj"))
print(add_student("Altaf"))
print(add_student("Aman"))
```

**Output:**
```text
['Raj']
['Altaf']
['Aman']
```

Each function call now creates a fresh list.

**Rule:** Avoid using mutable objects such as lists, dictionaries and sets as default parameter values. Use `None` and create the object inside the function.

---

# 15. Practical Programs

## Program 1: Sum of Any Number of Values

```python
def calculate_sum(*numbers):
    total = sum(numbers)
    return total

result = calculate_sum(10, 20, 30, 40, 50)

print("Total:", result)
```

**Output:**
```text
Total: 150
```

## Program 2: Student Details Using Keyword Arguments

```python
def student_details(**details):
    print("STUDENT INFORMATION")

    for key, value in details.items():
        print(f"{key}: {value}")

student_details(
    name="Raj",
    age=21,
    course="Python",
    city="Mumbai"
)
```

**Output:**
```text
STUDENT INFORMATION
name: Raj
age: 21
course: Python
city: Mumbai
```

## Program 3: Employee Profile with Default Arguments

```python
def employee_profile(name, department="General", salary=20000):
    print("Employee:", name)
    print("Department:", department)
    print("Salary:", salary)

employee_profile("Raj")

print()

employee_profile("Altaf", "IT", 35000)
```

**Output:**
```text
Employee: Raj
Department: General
Salary: 20000

Employee: Altaf
Department: IT
Salary: 35000
```

## Program 4: Shopping Cart Using *args

```python
def shopping_cart(*prices):
    total = sum(prices)

    print("Products:", len(prices))
    print("Total Amount:", total)

shopping_cart(500, 1200, 300, 800)
```

**Output:**
```text
Products: 4
Total Amount: 2800
```

## Program 5: Application Configuration Using **kwargs

```python
def application_config(**settings):
    print("APPLICATION CONFIGURATION")

    for key, value in settings.items():
        print(f"{key}: {value}")

application_config(
    app_name="Student Management",
    version="1.0",
    debug=True,
    database="SQLite",
    port=5000
)
```

**Output:**
```text
APPLICATION CONFIGURATION
app_name: Student Management
version: 1.0
debug: True
database: SQLite
port: 5000
```

## Program 6: Flexible Billing Function

```python
def generate_bill(customer, *prices, discount=0, tax=0):
    subtotal = sum(prices)

    discount_amount = subtotal * discount / 100
    amount_after_discount = subtotal - discount_amount

    tax_amount = amount_after_discount * tax / 100
    final_amount = amount_after_discount + tax_amount

    print("Customer:", customer)
    print("Subtotal:", subtotal)
    print("Discount:", discount_amount)
    print("Tax:", tax_amount)
    print("Final Amount:", final_amount)

generate_bill(
    "Raj",
    1000,
    500,
    200,
    discount=10,
    tax=5
)
```

**Output:**
```text
Customer: Raj
Subtotal: 1700
Discount: 170.0
Tax: 76.5
Final Amount: 1606.5
```

---

# 16. Mini Project – Flexible Order Management System

## Project Description

Create a Python-based Order Management System using functions and different argument techniques.

The system should support:
- Customer information.
- Multiple products in one order.
- Flexible product quantities.
- Optional discount and tax.
- Additional customer information.
- Bill calculation and display.

### Project Requirements

Create the following functions:

1. `display_products()`
2. `create_order()`
3. `calculate_total()`
4. `calculate_discount()`
5. `generate_invoice()`
6. `main()`

### Sample Code

```python
products = {
    "Laptop": 50000,
    "Mouse": 500,
    "Keyboard": 1200,
    "Monitor": 12000,
    "Headphones": 2000
}


def display_products():
    print("\nAVAILABLE PRODUCTS")

    for product, price in products.items():
        print(f"{product}: Rs. {price}")


def calculate_total(*prices):
    return sum(prices)


def calculate_discount(amount, discount=0):
    return amount * discount / 100


def create_order(customer, *items, discount=0, tax=0, **customer_details):

    selected_prices = []
    valid_items = []

    for item in items:
        if item in products:
            selected_prices.append(products[item])
            valid_items.append(item)
        else:
            print("Product not found:", item)

    if not valid_items:
        print("No valid products selected.")
        return

    subtotal = calculate_total(*selected_prices)

    discount_amount = calculate_discount(subtotal, discount)

    amount_after_discount = subtotal - discount_amount

    tax_amount = amount_after_discount * tax / 100

    final_amount = amount_after_discount + tax_amount

    generate_invoice(
        customer,
        valid_items,
        subtotal,
        discount_amount,
        tax_amount,
        final_amount,
        **customer_details
    )


def generate_invoice(
    customer,
    items,
    subtotal,
    discount,
    tax,
    final_amount,
    **customer_details
):

    print("\n========== INVOICE ==========")

    print("Customer:", customer)

    print("\nProducts:")

    for item in items:
        print(f"- {item}: Rs. {products[item]}")

    print("\nAdditional Details:")

    for key, value in customer_details.items():
        print(f"{key}: {value}")

    print("\nSubtotal:", subtotal)
    print("Discount:", discount)
    print("Tax:", tax)
    print("Final Amount:", final_amount)

    print("=============================")


def main():

    display_products()

    create_order(
        "Raj",
        "Laptop",
        "Mouse",
        "Keyboard",
        discount=10,
        tax=5,
        city="Mumbai",
        payment_method="UPI"
    )


main()
```

### Expected Output

```text
AVAILABLE PRODUCTS
Laptop: Rs. 50000
Mouse: Rs. 500
Keyboard: Rs. 1200
Monitor: Rs. 12000
Headphones: Rs. 2000

========== INVOICE ==========
Customer: Raj

Products:
- Laptop: Rs. 50000
- Mouse: Rs. 500
- Keyboard: Rs. 1200

Additional Details:
city: Mumbai
payment_method: UPI

Subtotal: 51700
Discount: 5170.0
Tax: 2326.5
Final Amount: 48856.5
=============================
```

### Project Extension Tasks

After completing the basic project, implement these improvements:

1. Allow users to select products through `input()`.
2. Accept multiple customer details using `**kwargs`.
3. Add quantity support for each product.
4. Prevent negative quantities and prices.
5. Allow the user to choose a discount percentage.
6. Add a delivery charge.
7. Display a detailed invoice.
8. Handle invalid product names.
9. Add a menu to create multiple orders.
10. Store completed orders in a list.

---

# 17. Student Practice Exercises

## Exercise 1 – Basic Arguments

Create a function that accepts:
- Name
- Age
- City

Display all information.

## Exercise 2 – Keyword Arguments

Create a function that accepts employee information and call it using keyword arguments in a different order.

## Exercise 3 – Default Arguments

Create a function `calculate_salary()` that accepts:
- Basic salary
- Bonus (default: 2000)
- Allowance (default: 1000)

Calculate and return the total salary.

## Exercise 4 – *args

Create a function that accepts any number of integers and returns:
- Sum
- Average
- Maximum
- Minimum

Handle the case where no numbers are provided.

## Exercise 5 – **kwargs

Create a function that accepts any number of product details and displays them in a structured format.

## Exercise 6 – Combined Arguments

Create a function that accepts:
- Employee name as a normal parameter.
- Multiple project names using `*args`.
- Department as a keyword-only argument.
- Additional employee information using `**kwargs`.

## Exercise 7 – Argument Unpacking

Create:
- A list containing three numbers.
- A dictionary containing three student details.

Pass both collections to suitable functions using argument unpacking.

## Exercise 8 – Mutable Default Argument

Write an incorrect function that uses a list as a default argument.

Observe its behaviour and then correct it using `None`.

## Exercise 9 – Positional-Only and Keyword-Only

Create a function that accepts:
- Product name as positional-only.
- Price as positional-only.
- Quantity as keyword-only.
- Discount as keyword-only.

Calculate the final price.

## Exercise 10 – Real-World Function Design

Create a function for a restaurant billing system that supports:
- Customer name.
- Multiple item prices.
- Optional discount.
- Optional tax.
- Additional customer information.

---

# 18. Trainer Assessment

Ask the student to explain and demonstrate the following:

| Assessment Question | Expected Understanding |
|---|---|
| What is a parameter? | Variable in a function definition |
| What is an argument? | Value passed during a function call |
| What are positional arguments? | Values assigned according to position |
| What are keyword arguments? | Values assigned using parameter names |
| What are default arguments? | Parameters with predefined values |
| What does `*args` do? | Collects extra positional arguments into a tuple |
| What does `**kwargs` do? | Collects extra keyword arguments into a dictionary |
| What is a keyword-only argument? | Must be passed using its parameter name |
| What is a positional-only argument? | Must be passed according to position |
| What does `*` do during a function call? | Unpacks an iterable into positional arguments |
| What does `**` do during a function call? | Unpacks a dictionary into keyword arguments |
| Why should mutable default arguments be avoided? | Their objects are reused across function calls |

### Practical Assessment

The student must independently create a function that:

1. Accepts a customer name.
2. Accepts any number of product prices.
3. Accepts an optional discount.
4. Accepts tax as a keyword-only argument.
5. Accepts additional customer details using `**kwargs`.
6. Calculates the final bill.
7. Displays a properly formatted invoice.

---

# 19. Completion Criteria

Mark Day 20 as completed when the student can:

- Understand positional and keyword arguments.
- Use default arguments correctly.
- Combine positional and keyword arguments.
- Work with variable-length arguments using `*args`.
- Work with variable-length keyword arguments using `**kwargs`.
- Understand keyword-only and positional-only parameters.
- Perform argument unpacking using `*` and `**`.
- Pass lists and dictionaries into functions.
- Understand how mutable arguments behave.
- Avoid common argument-related errors.
- Explain and fix mutable default argument problems.
- Complete the Flexible Order Management System independently.

**Trainer Note:** The student should understand not only how to use these argument types but also when each one is useful in real-world Python applications.

---

**End of Day 20 – Function Arguments & Parameters**


# Day 1 – Introduction to Programming & Python
## Practical Training Guide

**Level:** Absolute Beginner  
**Duration:** 5 Days  
**Category:** Practical Training  
**Prerequisite:** No coding knowledge required.

## Training Objective

Is Day ka objective student ko zero coding knowledge se Python programming ka basic practical experience dena hai.

Student Day complete karne ke baad:
- Python environment setup kar payega.
- Python programs create aur execute kar payega.
- Basic Python syntax understand karega.
- print() function use kar payega.
- Comments aur indentation understand karega.
- Basic programming instructions likh payega.

---

# Day 1 – Programming Basics & Python Environment Setup

## 1. Understanding Programming Through Practice

### Concept Explanation

Programming ka simple meaning hai computer ko instructions dena.

Computer khud se nahi samajhta ki hume kya karwana hai. Hum programming language mein instructions likhte hain aur computer un instructions ko execute karta hai.

**Real-Life Example:**

Suppose hume computer se do numbers add karwane hain.

Process:
1. Computer ko first number denge.
2. Computer ko second number denge.
3. Computer ko addition karne ka instruction denge.
4. Computer result display karega.

Yahi programming ka basic concept hai.

### Trainer Activity

Student se ye questions poochho:

1. Programming kya hoti hai?
2. Computer ko instructions kaun deta hai?
3. Programming ka real-life example batao.

---

## 2. Python Installation Verification

### Concept Explanation

Python programs execute karne ke liye system mein Python interpreter installed hona chahiye.

Python interpreter hamare written code ko process aur execute karta hai.

### Step 1: Open Terminal

Windows mein:
- Press `Win + R`.
- Type `cmd`.
- Press Enter.

### Step 2: Check Python Version

```bash
python --version
```

**Expected Output:**

```text
Python 3.x.x
```

### Step 3: Check pip

```bash
pip --version
```

**Explanation:**

`pip` Python ka package installer hai. Iska use external Python libraries install karne ke liye hota hai.

### Student Task

- Python version check karo.
- pip version check karo.
- Dono commands ka output identify karo.

---

## 3. VS Code Setup

### Concept Explanation

VS Code ek code editor hai jisme hum programming code write, edit aur execute kar sakte hain.

Python extension VS Code ko Python development support provide karti hai.

### Setup Steps

1. Install Visual Studio Code.
2. Open VS Code.
3. Open Extensions.
4. Search for Python.
5. Install Microsoft Python Extension.
6. Select Python Interpreter.
7. Open integrated terminal.

### Create First Project

Folder structure:

```text
Python-Training/
│
└── Day-01/
    │
    └── hello.py
```

### Student Task

- Project folder create karo.
- `hello.py` file create karo.
- File ko VS Code mein open karo.
- Python interpreter select karo.

---

# Day 2 – First Python Program & print() Function

## 1. Understanding Python Program Structure

### Concept Explanation

Python program instructions ka collection hota hai.

Python mein hum `.py` extension wali files mein code write karte hain.

Example:

```python
print("Hello World")
```

**Code Explanation:**

- `print` Python ka built-in function hai.
- `()` function ko call karne ke liye use hota hai.
- `"Hello World"` ek string value hai.
- Python is text ko terminal mein display karega.

### Expected Output

```text
Hello World
```

### Important Concept

Python mein function execute karne ke liye uska naam aur parentheses use kiye jaate hain.

---

## 2. Understanding print() Function

### Concept Explanation

`print()` Python ka built-in function hai.

Iska use output screen ya terminal par display karne ke liye hota hai.

### Example 1 – Printing Text

```python
print("Welcome to Python")
```

**Explanation:**

Double quotes ke andar likha text terminal par display hoga.

### Example 2 – Printing Numbers

```python
print(100)
print(250)
print(500)
```

**Explanation:**

Numbers ko print karne ke liye quotes ki zarurat nahi hoti.

### Example 3 – Printing Multiple Values

```python
print("Raj", 22, "Python Developer")
```

**Output:**

```text
Raj 22 Python Developer
```

**Explanation:**

Ek hi print statement mein multiple values comma se separate karke pass kar sakte hain.

---

## 3. Understanding sep Parameter

### Concept Explanation

`sep` ka full form separator hai.

Jab print function mein multiple values hoti hain, tab default separator space hota hai.

Hum `sep` se default space ko change kar sakte hain.

### Example

```python
print("2026", "11", "03", sep="-")
```

**Output:**

```text
2026-11-03
```

### Another Example

```python
print("Python", "Java", "C++", sep=" | ")
```

**Output:**

```text
Python | Java | C++
```

---

## 4. Understanding end Parameter

### Concept Explanation

Normally Python ka print function output ke baad new line create karta hai.

`end` parameter se hum decide kar sakte hain ki output ke baad kya add hona chahiye.

### Example 1 – Default Behavior

```python
print("Hello")
print("World")
```

**Output:**

```text
Hello
World
```

### Example 2 – Custom End

```python
print("Hello", end=" ")
print("World")
```

**Output:**

```text
Hello World
```

### Example 3 – Using Hyphen

```python
print("Python", end="-")
print("Programming")
```

**Output:**

```text
Python-Programming
```

---

## 5. Practical Exercises – Day 2

1. Print your full name.
2. Print your age.
3. Print your city and country.
4. Print three different programming languages.
5. Display your introduction in a single print statement.
6. Use `sep` to display a date.
7. Use `end` to display two messages on the same line.
8. Create a simple welcome message using multiple print statements.

### Day 2 Assessment

Student ko bina help ke:
- Text print karna aana chahiye.
- Numbers print karne aane chahiye.
- Multiple values print karna aana chahiye.
- `sep` aur `end` ka difference explain karna aana chahiye.

---

# Day 3 – Python Syntax, Indentation & Comments

## 1. Understanding Python Syntax

### Concept Explanation

Syntax ka matlab programming language ke rules hota hai.

Har programming language ke apne syntax rules hote hain.

Agar hum Python ke syntax rules follow nahi karte, toh program mein errors aa sakte hain.

### Correct Example

```python
print("Hello Python")
```

### Incorrect Example

```python
print("Hello Python"
```

**Explanation:**

Incorrect example mein closing parenthesis missing hai.

Python is wajah se SyntaxError generate karega.

### Important Concepts

- Statements
- Expressions
- Parentheses
- Quotation Marks
- Case Sensitivity
- Syntax Errors

---

## 2. Understanding Indentation

### Concept Explanation

Indentation ka matlab code ke beginning mein spaces dena hota hai.

Python mein indentation code blocks define karne ke liye use hoti hai.

Normally Python mein 4 spaces indentation ke liye recommended hain.

### Example – Correct Indentation

```python
if 10 > 5:
    print("10 is greater than 5")
```

### Example – Incorrect Indentation

```python
if 10 > 5:
print("10 is greater than 5")
```

**Explanation:**

Second example mein indentation missing hai, isliye Python IndentationError generate karega.

### Important Points

- Python indentation ko seriously consider karta hai.
- Normally 4 spaces use karo.
- Same code block mein consistent indentation rakho.
- Tabs aur spaces ko unnecessarily mix mat karo.

---

## 3. Understanding Comments

### Concept Explanation

Comments code ke andar written explanations hote hain.

Python interpreter comments ko execute nahi karta.

Comments ka main purpose code ko readable aur understandable banana hai.

### Single-Line Comment

```python
# This is a single-line comment

print("Hello Python")
```

### Inline Comment

```python
name = "Raj"  # Student name
```

### Multiple-Line Explanation

```python
# Student Information
# Name: Raj
# Course: Python
# Level: Beginner

print("Student Details")
```

**Important:** Python mein dedicated multiline comment syntax nahi hai. Multiple lines ke comments ke liye generally har line par `#` use kiya jata hai.

---

## 4. Understanding Case Sensitivity

### Concept Explanation

Python case-sensitive language hai.

Matlab uppercase aur lowercase letters ko different consider kiya jata hai.

### Example

```python
name = "Raj"
Name = "Altaf"

print(name)
print(Name)
```

**Output:**

```text
Raj
Altaf
```

**Explanation:**

`name` aur `Name` Python ke liye two different identifiers hain.

---

## 5. Practical Exercises – Day 3

1. Write a program with correct Python syntax.
2. Create a program containing a syntax error and fix it.
3. Write a program using proper indentation.
4. Create a program containing single-line comments.
5. Write inline comments in a program.
6. Create two variables with different capitalization.
7. Identify syntax errors in a given Python program.

### Day 3 Assessment

Student ko:
- Python syntax explain karna aana chahiye.
- Indentation ka purpose samajhna chahiye.
- Comments create karne aane chahiye.
- Case sensitivity understand honi chahiye.

---

# Day 4 – Keywords, Identifiers & Python Shell

## 1. Understanding Keywords

### Concept Explanation

Keywords Python ke reserved words hote hain.

Inka already Python language mein special meaning hota hai.

Hum keywords ko normal variable names ke roop mein use nahi kar sakte.

### Examples

```python
if
else
for
while
class
def
return
True
False
None
```

### Practical Example

```python
age = 20

if age >= 18:
    print("Eligible")
```

**Explanation:**

`if` Python keyword hai. Iska use condition check karne ke liye hota hai.

---

## 2. Understanding Identifiers

### Concept Explanation

Identifiers Python program mein variables, functions, classes aur other objects ko diye gaye names hote hain.

### Example

```python
name = "Raj"
age = 22
city = "Mumbai"
```

Yahan:
- `name` = Identifier
- `age` = Identifier
- `city` = Identifier

### Identifier Naming Rules

1. Identifier letters se start ho sakta hai.
2. Underscore `_` se start ho sakta hai.
3. Numbers se start nahi ho sakta.
4. Spaces allowed nahi hain.
5. Python keywords identifiers nahi ban sakte.
6. Identifiers case-sensitive hote hain.

### Valid Identifiers

```python
name = "Raj"
student_age = 22
_marks = 90
age2 = 25
```

### Invalid Identifiers

```python
2name = "Raj"
student age = 22
class = "Python"
```

---

## 3. Python Shell vs Python Script

### Concept Explanation

Python mein code execute karne ke two common ways hain.

**Python Shell:**

Ismein hum commands directly enter karte hain aur immediate output milta hai.

**Python Script:**

Ismein hum code ko `.py` file mein save karte hain aur baad mein execute karte hain.

### Python Shell Example

```python
>>> 10 + 20
30
>>> print("Hello")
Hello
```

### Python Script Example

Create `main.py`:

```python
a = 10
b = 20

print(a + b)
```

Run:

```bash
python main.py
```

Output:

```text
30
```

### Difference

| Python Shell | Python Script |
|---|---|
| Interactive mode | Script mode |
| Direct execution | File-based execution |
| Quick testing | Complete programs |
| Commands are entered directly | Code is saved in `.py` files |

---

## 4. Practical Exercises – Day 4

1. Identify 10 Python keywords.
2. Create 5 valid identifiers.
3. Identify 5 invalid identifiers.
4. Write a program using different variable names.
5. Execute arithmetic expressions in Python Shell.
6. Create and execute a Python script.
7. Explain the difference between Shell and Script.

### Day 4 Assessment

Student ko keywords, identifiers aur Python execution methods samajhne chahiye.

---

# Day 5 – Final Practice & Mini Project

## 1. Revision of Basic Concepts

Student ke saath previous four days ke concepts revise karo.

**Topics:**
- Programming Fundamentals
- Python Introduction
- Python Installation
- Python Environment
- print() Function
- sep and end Parameters
- Python Syntax
- Indentation
- Comments
- Keywords
- Identifiers
- Python Shell vs Script

---

## 2. Independent Coding Exercises

### Exercise 1 – Personal Introduction

Create a Python program that displays:

- Full Name
- Age
- City
- Course
- Learning Goal

### Exercise 2 – Multiple Print Statements

Display your introduction using at least five print statements.

### Exercise 3 – Using sep Parameter

Display the following output:

```text
Python | Java | C++ | JavaScript
```

### Exercise 4 – Using end Parameter

Display the following output using multiple print statements:

```text
Welcome To Python Programming
```

### Exercise 5 – Comments

Create a program with at least five meaningful comments.

### Exercise 6 – Syntax Correction

Find and correct errors in the following code:

```python
print("Hello Python"

if 10 > 5:
print("Correct")
```

### Exercise 7 – Identifier Practice

Identify valid and invalid identifiers:

```text
name
2student
student_name
class
age2
student age
```

---

## 3. Mini Project – Student Introduction System

### Project Description

Student ek simple introduction program create karega jo terminal par formatted student details display karega.

### Requirements

- Display project heading.
- Display student name.
- Display age.
- Display city.
- Display course name.
- Display learning goal.
- Use multiple print statements.
- Use `sep` and `end` parameters.
- Add meaningful comments.

### Expected Output

```text
================================
       STUDENT INTRODUCTION
================================

Name: Raj
Age: 22
City: Mumbai
Course: Python Programming
Goal: Become a Python Developer

================================
       THANK YOU!
================================
```

---

## 4. Final Assessment – Day 1

### Theory Questions

1. What is Programming?
2. What is Python?
3. Who developed Python?
4. Explain any five features of Python.
5. What is a Python Interpreter?
6. What is the difference between Python Shell and Script?
7. What is the purpose of print()?
8. What is indentation?
9. What are comments?
10. What are keywords and identifiers?

### Practical Assessment

- [ ] Python Installation Verification
- [ ] VS Code Setup
- [ ] Create Python Files
- [ ] Execute Python Programs
- [ ] Use print() Function
- [ ] Use sep Parameter
- [ ] Use end Parameter
- [ ] Write Comments
- [ ] Apply Correct Indentation
- [ ] Identify Keywords
- [ ] Create Valid Identifiers
- [ ] Use Python Shell
- [ ] Execute Python Scripts
- [ ] Complete All Coding Exercises
- [ ] Complete Mini Project

---

## Day 1 Completion Criteria

Student ko next Day tabhi start karna chahiye jab woh:

1. Python environment independently setup kar sake.
2. Basic Python programs khud likh sake.
3. print() function properly use kar sake.
4. Syntax aur indentation errors identify kar sake.
5. Keywords aur identifiers distinguish kar sake.
6. Python Shell aur Script mein code execute kar sake.
7. Mini project bina trainer ki help ke complete kar sake.

**Day 1 Status: Completed**

**Next Day: Day 2 – Variables & Data Types**

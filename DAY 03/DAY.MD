
# Day 03 — Python Interpreter, First Program and Basic Syntax

---

# Part 1 — Understanding the Python Interpreter

## 1.1 What is an Interpreter?

A Python interpreter is the software responsible for executing Python programs.

When we write Python code, the interpreter processes the code and handles its execution.

### Example

```python
print("Hello Python")
```

When this code is executed:

1. Python reads the source code.
2. It processes the instruction.
3. The `print()` function displays the message.
4. The result appears in the output.

### Trainer Demonstration

Open VS Code and create a file named:

`interpreter_demo.py`

Write:

```python
print("Python Interpreter")
print("Executing my first program")
```

Run:

```bash
python interpreter_demo.py
```

### Expected Output

```text
Python Interpreter
Executing my first program
```

### Important Understanding

Python is commonly described as an interpreted language. Its implementation generally compiles source code into bytecode, which is then executed by the Python virtual machine.

The student does not need to understand bytecode internals yet.

---

# Part 2 — Python Shell vs Python Script

## 2.1 What is Python Shell?

Python Shell is an interactive environment where we can execute Python instructions one at a time.

It is useful for testing small expressions and understanding Python behaviour.

### Step 1 — Open Python Shell

Open the VS Code terminal and execute:

```bash
python
```

You should see a Python prompt similar to:

```text
>>>
```

This indicates that Python is ready to accept instructions.

### Step 2 — Execute Instructions

Enter:

```python
print("Hello")
```

Output:

```text
Hello
```

Now enter:

```python
print(10 + 20)
```

Output:

```text
30
```

Now enter:

```python
print("Learning Python Shell")
```

Output:

```text
Learning Python Shell
```

### Step 3 — Exit Python Shell

Execute:

```python
exit()
```

Alternatively, press `Ctrl + Z`, followed by Enter, in Windows Command Prompt.

## 2.2 What is a Python Script?

A Python script is a file containing Python instructions saved with the `.py` extension.

Scripts are useful when we need to write, save, reuse and execute multiple instructions.

### Practical Demonstration

Create:

`script_demo.py`

Write:

```python
print("This is a Python script")
print("First instruction")
print("Second instruction")
print("Third instruction")
```

Run:

```bash
python script_demo.py
```

### Expected Output

```text
This is a Python script
First instruction
Second instruction
Third instruction
```

## 2.3 Difference Between Shell and Script

| Python Shell | Python Script |
|---|---|
| Interactive environment | Saved Python file |
| Executes instructions immediately | Executes saved instructions |
| Useful for quick testing | Useful for complete programs |
| Usually not saved automatically | Can be saved and reused |
| Uses the `>>>` prompt | Uses `.py` files |

### Student Practice

1. Open Python Shell.
2. Display your name.
3. Calculate `50 + 25`.
4. Display a welcome message.
5. Exit the Shell.
6. Create a Python script performing the same tasks.

---

# Part 3 — Your First Python Program

## 3.1 Understanding Hello World

The first program in many programming courses is called Hello World.

It helps beginners understand how to write and execute a basic instruction.

Create:

`hello_world.py`

Write:

```python
print("Hello, World!")
```

### Expected Output

```text
Hello, World!
```

### Understanding the Code

- `print` is a built-in Python function.
- Parentheses `()` contain the value passed to the function.
- Double quotation marks define a string literal.
- The text inside the quotation marks is displayed on the screen.

## 3.2 Display Multiple Messages

Create:

`introduction.py`

```python
print("Hello!")
print("My name is Raj")
print("I am learning Python")
print("I want to become a developer")
```

### Expected Output

```text
Hello!
My name is Raj
I am learning Python
I want to become a developer
```

### Important Concept

Python executes normal sequential instructions from top to bottom.

### Student Practice

Create a program that displays:

1. Your name.
2. Your age.
3. Your city.
4. Your training course.
5. Your career goal.

---

# Part 4 — Understanding the print() Function

## 4.1 What is print()?

`print()` is a built-in Python function used to display information on the output screen.

It can display text, numbers, calculations and multiple values.

## 4.2 Printing Text

```python
print("Welcome to Python")
```

Output:

```text
Welcome to Python
```

Text values must be enclosed in quotation marks.

## 4.3 Printing Numbers

```python
print(100)
print(250)
print(500)
```

Output:

```text
100
250
500
```

Numbers can be printed without quotation marks.

## 4.4 Printing Calculations

```python
print(10 + 20)
print(50 - 15)
print(5 * 4)
print(100 / 10)
```

Output:

```text
30
35
20
10.0
```

Explain that Python evaluates the mathematical expression before displaying the result.

## 4.5 Printing Multiple Values

The `print()` function accepts multiple values separated by commas.

```python
print("Raj", 25, "Developer")
```

Output:

```text
Raj 25 Developer
```

By default, `print()` separates multiple values with a space.

## 4.6 Understanding sep Parameter

The `sep` parameter controls the separator between multiple printed values.

```python
print("2026", "11", "03", sep="-")
```

Output:

```text
2026-11-03
```

Another example:

```python
print("Python", "Java", "PHP", sep=" | ")
```

Output:

```text
Python | Java | PHP
```

## 4.7 Understanding end Parameter

By default, `print()` moves to a new line after displaying the output.

The `end` parameter changes what is printed at the end.

```python
print("Hello", end=" ")
print("World")
```

Output:

```text
Hello World
```

Another example:

```python
print("Python", end=" - ")
print("Programming")
```

Output:

```text
Python - Programming
```

## 4.8 Understanding Escape Characters

Escape characters are special character sequences used inside strings.

### New Line: `\n`

```python
print("Hello\nWorld")
```

Output:

```text
Hello
World
```

### Tab: `\t`

```python
print("Name\tAge")
print("Raj\t25")
```

Output:

```text
Name    Age
Raj     25
```

### Double Quote: `\"`

```python
print("He said, \"Hello\"")
```

Output:

```text
He said, "Hello"
```

### Backslash: `\\`

```python
print("C:\\Users\\Student")
```

Output:

```text
C:\Users\Student
```

### Student Practice

Write programs using:

1. `print()` to display your introduction.
2. `print()` to display three numbers.
3. `print()` to calculate two mathematical expressions.
4. `sep` to display a date using hyphens.
5. `end` to display two words on the same line.
6. `\n` to display text on multiple lines.
7. `\t` to display information in tabular form.

---

# Part 5 — Python Syntax

## 5.1 What is Syntax?

Syntax refers to the rules and structure that must be followed when writing Python code.

Just as a human language has grammar rules, Python has syntax rules.

If we do not follow the rules, Python may produce a syntax error or another error.

## 5.2 Correct Syntax

```python
print("Hello Python")
```

This is valid Python syntax.

## 5.3 Incorrect Syntax Examples

### Missing Closing Parenthesis

```python
print("Hello Python"
```

This produces a syntax error.

### Missing Quotation Mark

```python
print("Hello Python)
```

This also produces a syntax error.

### Incorrect Function Name

```python
Print("Hello Python")
```

Python is case-sensitive. `Print` and `print` are different names.

### Practical Demonstration

Create:

`syntax_practice.py`

Write a correct program first.

Then intentionally introduce one mistake at a time and execute the program.

Observe the error message and fix the code.

### Important Rule

Read the complete error message. Python often provides the filename and line number where it detected a problem.

---

# Part 6 — Indentation in Python

## 6.1 What is Indentation?

Indentation means adding spaces at the beginning of a line.

Python uses indentation to define code blocks.

Unlike languages that commonly use curly braces to define blocks, Python relies on indentation.

### Example

```python
if True:
    print("Inside the block")

print("Outside the block")
```

Output:

```text
Inside the block
Outside the block
```

Explain that the first `print()` is indented because it belongs to the `if` block.

The second `print()` is not indented, so it is outside that block.

The student does not need to learn the full `if` statement today. The example is only to demonstrate indentation.

## 6.2 Incorrect Indentation

```python
if True:
print("Hello")
```

This produces an `IndentationError` because the statement inside the block is not indented.

## 6.3 Standard Indentation Rule

Python's official style guide recommends four spaces per indentation level.

Example:

```python
if True:
    print("First line")
    print("Second line")
```

### Trainer Demonstration

1. Create a Python file.
2. Write the correct indentation example.
3. Remove the indentation.
4. Run the program.
5. Observe the error.
6. Restore the four spaces.
7. Run it again.

### Student Practice

Identify which lines should be indented:

```python
if True:
    print("Python")
    print("Programming")
print("Completed")
```

Explain why the last line is outside the block.

---

# Part 7 — Comments in Python

## 7.1 What are Comments?

Comments are notes written inside source code for humans.

Python ignores comments during normal program execution.

Comments help developers explain code and make programs easier to maintain.

## 7.2 Single-Line Comments

Use `#` to write a single-line comment.

```python
# This is my first Python comment

print("Hello Python")
```

Output:

```text
Hello Python
```

The comment is not displayed.

## 7.3 Comments Above Instructions

```python
# Display student information

print("Name: Raj")
print("Course: Python")
```

## 7.4 Inline Comments

Comments can also appear after a statement.

```python
print("Hello")  # Display a welcome message
```

## 7.5 Multi-Line Explanatory Comments

Python does not have a separate multi-line comment syntax.

For multiple comment lines, use `#` on each line.

```python
# This program displays
# student information
# using print statements

print("Student Details")
```

### Important Note: Triple Quotes

Triple-quoted strings can span multiple lines:

```python
"""
This is a multi-line string.
It is not a dedicated Python comment syntax.
"""
```

Do not teach triple-quoted strings as the standard way to create comments. They are string literals and are commonly used for docstrings in appropriate locations.

### Student Practice

Create a program containing:

- One comment at the top.
- Two inline comments.
- Three `print()` statements.
- A short explanation of what the program does.

---

# Part 8 — Keywords in Python

## 8.1 What are Keywords?

Keywords are reserved words in Python that have special meanings in the language.

They are part of Python's syntax and cannot be used as ordinary identifiers.

Examples:

- `if`
- `else`
- `for`
- `while`
- `def`
- `class`
- `return`
- `True`
- `False`
- `None`
- `import`
- `try`
- `except`

### Practical Demonstration

Create:

`keywords_demo.py`

Write:

```python
import keyword

print(keyword.kwlist)
```

### Expected Output

Python will display a list of reserved keywords for the installed Python version.

The exact list may differ between Python versions.

### Check Whether a Word is a Keyword

```python
import keyword

print(keyword.iskeyword("if"))
print(keyword.iskeyword("hello"))
```

Output:

```text
True
False
```

### Explanation

- `import` loads a module.
- `keyword` is a standard Python module.
- `keyword.iskeyword()` checks whether a word is a reserved keyword.
- `True` means the word is a keyword.
- `False` means it is not a keyword.

### Student Practice

Use `keyword.iskeyword()` to check:

1. `for`
2. `while`
3. `name`
4. `class`
5. `student`
6. `return`

---

# Part 9 — Identifiers in Python

## 9.1 What is an Identifier?

An identifier is a name used to identify a programming element, such as a variable, function or class.

Examples:

```python
student_name = "Raj"
age = 20
total_marks = 450
```

Here:

- `student_name` is an identifier.
- `age` is an identifier.
- `total_marks` is an identifier.

Detailed variable concepts will be covered in the next lesson.

## 9.2 Rules for Naming Identifiers

### Rule 1 — Must Start With a Letter or Underscore

Valid:

```python
name = "Raj"
_age = 20
student1 = "Amit"
```

Invalid:

```python
1student = "Raj"
```

An identifier cannot start with a number.

### Rule 2 — Cannot Start With a Special Character

Invalid:

```python
@name = "Raj"
```

### Rule 3 — Spaces Are Not Allowed

Invalid:

```python
student name = "Raj"
```

Correct:

```python
student_name = "Raj"
```

### Rule 4 — Keywords Cannot Be Used

Invalid:

```python
class = "Python"
```

`class` is a reserved keyword.

### Rule 5 — Python is Case-Sensitive

```python
name = "Raj"
Name = "Amit"
```

These are two different identifiers.

### Rule 6 — Underscores Are Allowed

Valid:

```python
first_name = "Raj"
total_marks = 450
```

## 9.3 Naming Convention

Python recommends `snake_case` for variable and function names.

Example:

```python
student_name = "Raj"
total_price = 500
employee_id = 101
```

Use descriptive names instead of unclear names.

Good:

```python
student_age = 20
```

Less descriptive:

```python
x = 20
```

### Student Practice

Identify whether these identifiers are valid or invalid:

1. `student`
2. `student_name`
3. `1student`
4. `_student`
5. `student-name`
6. `studentName`
7. `class`
8. `total_marks`
9. `my age`
10. `Age`

Explain why each invalid identifier is incorrect.

---

# Part 10 — Complete Practical Assignment

## Assignment 1 — Introduction Program

Create:

`my_introduction.py`

Display:

- Your full name.
- Your city.
- Your training course.
- Your learning goal.
- Your favourite programming language.

Requirements:

- Use at least five `print()` statements.
- Add comments.
- Use correct syntax.
- Save and execute the file.

## Assignment 2 — Output Formatting

Create:

`student_details.py`

Expected output:

```text
========== STUDENT DETAILS ==========
Name       : Raj
Course     : Python Programming
Level      : Beginner
Goal       : Software Developer
=====================================
```

Requirements:

- Use `print()`.
- Use `sep` or separate print statements.
- Use comments.
- Use appropriate string formatting with escape characters where needed.

## Assignment 3 — Mathematical Output

Create:

`basic_calculations.py`

Display the results of:

1. 50 + 25
2. 100 - 40
3. 12 * 5
4. 100 / 4
5. 15 + 10 * 2

Expected output:

```text
Addition: 75
Subtraction: 60
Multiplication: 60
Division: 25.0
Calculation: 35
```

## Assignment 4 — Keyword Checker

Create:

`keyword_checker.py`

```python
import keyword

print(keyword.iskeyword("if"))
print(keyword.iskeyword("name"))
print(keyword.iskeyword("class"))
print(keyword.iskeyword("student"))
```

Explain the output of each line.

## Assignment 5 — Debugging Practice

Correct the following code:

### Problem A

```python
print("Hello Python"
```

### Problem B

```python
Print("Welcome")
```

### Problem C

```python
if True:
print("Learning Python")
```

### Problem D

```python
# Student Introduction
print("My name is Raj"
print("I am learning Python")
```

The student must identify the errors, correct them and execute each program.

---

# Part 11 — Day 3 Trainer Assessment

- [ ] Student understands the Python interpreter.
- [ ] Student can open and use Python Shell.
- [ ] Student understands the difference between Shell and Script.
- [ ] Student can create and execute Python files.
- [ ] Student understands the `print()` function.
- [ ] Student can use `sep` and `end`.
- [ ] Student understands escape characters.
- [ ] Student can identify basic syntax errors.
- [ ] Student understands Python indentation.
- [ ] Student can write single-line and multi-line comments.
- [ ] Student understands Python keywords.
- [ ] Student can identify valid and invalid identifiers.
- [ ] Student can debug basic Python programs.

## Day 3 Completion Criteria

The student must independently create Python scripts, display formatted output, use comments, follow syntax and indentation rules, and identify keywords and valid identifiers.

**Next Lesson:** Day 4 — Variables and Data Types in Python.

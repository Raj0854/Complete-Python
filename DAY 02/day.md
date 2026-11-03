
# Day 02 — Python Installation and Development Environment Setup

---

# Part 1 — Real-World Applications of Python

## 1.1 Where is Python Used?

Python is a general-purpose programming language. It is used in different areas of software development.

### 1. Web Development

Python is used to create websites and backend applications.

Popular frameworks:

- Django
- Flask
- FastAPI

Examples:
- Login systems
- User management
- REST APIs
- E-commerce backends

### 2. Artificial Intelligence and Machine Learning

Python is widely used to develop intelligent systems.

Popular libraries:

- TensorFlow
- PyTorch
- Scikit-learn

Examples:
- Image recognition
- Chatbots
- Recommendation systems
- Prediction systems

### 3. Automation

Python can automate repetitive tasks.

Examples:
- Renaming multiple files
- Organizing folders
- Sending automated reports
- Processing Excel files
- Automating browser tasks

### 4. Data Science

Python can process, analyze and visualize data.

Popular libraries:

- NumPy
- Pandas
- Matplotlib

Examples:
- Sales reports
- Data analysis
- Business dashboards
- Statistical calculations

### 5. Desktop Applications

Python can be used to create desktop software.

Popular libraries:

- Tkinter
- PySide
- PyQt

Examples:
- Calculator
- Inventory management software
- Desktop management tools

### Student Practice

For each application, write one real-world problem that Python could solve.

---

# Part 2 — Comparing Programming Languages

## 2.1 Python vs Other Languages

Different programming languages are designed for different purposes.

No programming language is universally best. The right choice depends on project requirements.

| Language | Common Uses | Key Characteristic |
|---|---|---|
| Python | AI, automation, backend | Readable syntax |
| JavaScript | Web development | Browser support |
| Java | Enterprise applications | JVM ecosystem |
| C | System programming | Low-level control |
| C++ | Games, high-performance software | Performance and control |
| PHP | Backend web development | Server-side web development |

## 2.2 Practical Code Comparison

### Python

```python
print("Hello World")
```

### JavaScript

```javascript
console.log("Hello World");
```

### PHP

```php
<?php
echo "Hello World";
?>
```

### Java

```java
System.out.println("Hello World");
```

### C

```c
#include <stdio.h>

int main() {
    printf("Hello World");
    return 0;
}
```

### Trainer Explanation

All these programs display the same message, but their syntax and execution environments are different.

- Python uses `print()`.
- JavaScript uses `console.log()`.
- PHP commonly uses `echo`.
- Java uses `System.out.println()`.
- C uses `printf()`.

### Student Practice

1. Which language uses `console.log()`?
2. Which language is widely used in AI and data science?
3. Which language commonly uses `echo`?
4. Which language is commonly used for system programming?
5. Write one common use of each language.

---

# Part 3 — Installing Python

## 3.1 Understanding Python Installation

Python is a programming language. To execute Python programs, the computer needs a Python interpreter.

Installing Python provides the interpreter and other necessary components.

We will install Python on Windows.

### Step 1 — Open Python Website

Visit:

https://www.python.org/downloads/

Download a stable Python 3 release compatible with the operating system.

### Step 2 — Start Installation

1. Open the downloaded installer.
2. Locate the option `Add Python to PATH`.
3. Select this checkbox.
4. Click `Install Now`.
5. Wait until installation is complete.

**Important:** Adding Python to PATH allows Windows to locate Python from the terminal without manually specifying its installation directory.

### Step 3 — Verify Installation

Open Windows Command Prompt.

Press:

`Windows + R`

Type:

```text
cmd
```

Press Enter.

Execute:

```bash
python --version
```

Expected output will look similar to:

```text
Python 3.x.x
```

The exact version depends on the installed release.

### Step 4 — Check Python Launcher

Execute:

```bash
py --version
```

Expected output:

```text
Python 3.x.x
```

### Step 5 — Locate Python Installation

Execute:

```bash
where python
```

This displays the Python executable paths available through PATH.

### Step 6 — Check pip

Execute:

```bash
python -m pip --version
```

Expected output will show the installed pip version and its location.

## 3.2 Understanding pip

`pip` is Python's package installer.

It allows developers to install third-party Python packages.

Example:

```bash
python -m pip install requests
```

Do not install unnecessary packages today. We will learn package installation when required.

## 3.3 Common Installation Problems

### Problem 1: 'python' is not recognized

Possible reasons:

- Python is not installed.
- Python was not added to PATH.
- Terminal was opened before installation completed.

Solution:

1. Close Command Prompt.
2. Open it again.
3. Execute `python --version`.
4. If it still fails, repair PATH configuration or reinstall Python with Add Python to PATH selected.

### Problem 2: Microsoft Store Opens

Windows may have an App Execution Alias enabled.

Check:

Settings → Apps → Advanced app settings → App execution aliases.

Disable conflicting `python.exe` and `python3.exe` aliases if they prevent the installed Python from being used.

### Problem 3: Multiple Python Versions

Execute:

```bash
py -0p
```

This lists Python versions detected by the Python launcher.

---

# Part 4 — Installing Visual Studio Code

## 4.1 What is VS Code?

Visual Studio Code is a source-code editor.

It provides features that make writing and managing code easier.

Features include:

- Syntax highlighting
- Code completion
- Error highlighting
- Integrated terminal
- Debugging
- Extensions

### Step 1 — Download VS Code

Visit:

https://code.visualstudio.com/

Download the Windows installer.

### Step 2 — Install VS Code

1. Open the downloaded installer.
2. Accept the license agreement.
3. Select the installation location.
4. Continue through the setup.
5. Enable useful additional options if available:
   - Add to PATH
   - Add Open with Code action
   - Register Code as an editor
6. Complete the installation.

### Step 3 — Open VS Code

Launch Visual Studio Code.

Understand these main areas:

| Area | Purpose |
|---|---|
| Explorer | Manage files and folders |
| Editor | Write and edit code |
| Search | Find text in project files |
| Source Control | Manage Git changes |
| Extensions | Install additional functionality |
| Terminal | Execute commands |

### Trainer Demonstration

Show the student how to:

1. Open VS Code.
2. Open a folder.
3. Create a new file.
4. Save a file.
5. Open the integrated terminal.

---

# Part 5 — Installing Python Extension

## 5.1 Why Do We Need an Extension?

VS Code is a general-purpose code editor.

The Python extension adds Python-specific development features.

These include:

- Python code completion
- IntelliSense
- Debugging support
- Python interpreter selection
- Code navigation

### Installation Steps

1. Open VS Code.
2. Click the Extensions icon.
3. Search for `Python`.
4. Find the extension published by Microsoft.
5. Click Install.

Official extension:

https://marketplace.visualstudio.com/items?itemName=ms-python.python

### Verify Installation

1. Create a new file.
2. Save it with the `.py` extension.
3. Check whether Python language features are available.

## 5.2 Select Python Interpreter

VS Code needs to know which Python installation should execute the code.

Steps:

1. Open VS Code.
2. Press `Ctrl + Shift + P`.
3. Search for `Python: Select Interpreter`.
4. Select the installed Python version.
5. Verify the selected interpreter in VS Code.

If multiple Python versions are installed, select the version intended for this training.

---

# Part 6 — Creating the First Python Project

## 6.1 Create a Project Folder

Create a folder on your computer:

```text
Python-Training
```

Open VS Code.

Select:

File → Open Folder → Python-Training

### Step 2 — Create a Python File

Inside Explorer:

1. Click New File.
2. Enter the filename:

```text
hello.py
```

### Understanding the .py Extension

Python source files use the `.py` extension.

Examples:

- hello.py
- calculator.py
- student.py
- main.py

### Step 3 — Write Your First Program

Inside `hello.py`, write:

```python
print("Hello, World!")
```

Save the file using:

`Ctrl + S`

### Step 4 — Run the Program

Open the terminal:

`Ctrl + ``

Make sure the terminal is inside the project folder.

Execute:

```bash
python hello.py
```

Expected output:

```text
Hello, World!
```

### Understand What Happened

1. The terminal received the command `python hello.py`.
2. Python located the specified file.
3. The interpreter executed the instructions.
4. The `print()` function displayed the message.
5. The output appeared in the terminal.

## 6.2 Run Using the VS Code Run Button

1. Open `hello.py`.
2. Locate the Run Python File button.
3. Click it.
4. Observe the output in the terminal.

Explain that the Run button executes the currently open Python file using the selected interpreter.

---

# Part 7 — Understanding the Terminal

## 7.1 What is a Terminal?

A terminal is a text-based interface used to interact with the operating system.

Developers use it to:

- Execute programs
- Navigate folders
- Install packages
- Run development commands
- Manage projects

## 7.2 Important Windows Commands

| Command | Purpose |
|---|---|
| `cd` | Change directory |
| `dir` | List files and folders |
| `mkdir` | Create a directory |
| `cls` | Clear Command Prompt |
| `python --version` | Check Python version |
| `python filename.py` | Execute a Python file |
| `where python` | Locate Python executable |

### Practical Demonstration

Create a folder:

```bash
mkdir Day02Practice
```

Enter the folder:

```bash
cd Day02Practice
```

Display current directory:

```bash
cd
```

List files:

```bash
dir
```

Clear the screen:

```bash
cls
```

Explain that Windows Command Prompt, PowerShell and the VS Code terminal are different command-line environments. Some commands behave differently depending on the shell.

---

# Part 8 — Hands-On Tasks

## Task 1 — Installation Verification

Run all commands and record the results:

```bash
python --version
py --version
python -m pip --version
where python
py -0p
```

## Task 2 — VS Code Setup

Verify:

- [ ] VS Code installed successfully.
- [ ] Python extension installed.
- [ ] Python interpreter selected.
- [ ] Project folder opened.
- [ ] Python file created.
- [ ] Integrated terminal opened.

## Task 3 — Create Multiple Programs

Create these files inside your `Python-Training` folder.

### welcome.py

```python
print("Welcome to Python Training")
```

### student.py

```python
print("Student Name: Your Name")
print("Course: Python Programming")
print("Level: Beginner")
```

### introduction.py

```python
print("Hello!")
print("I am learning programming.")
print("I am learning Python.")
print("My goal is to become a developer.")
```

Run each file separately:

```bash
python welcome.py
python student.py
python introduction.py
```

## Task 4 — Independent Execution

Without using the VS Code Run button:

1. Open the integrated terminal.
2. Navigate to the project folder.
3. Execute `hello.py` using the Python command.
4. Execute `student.py`.
5. Verify the output.

---

# Part 9 — Assignment

## Assignment: Python Environment Setup

The student must independently:

1. Install Python.
2. Verify the Python version.
3. Verify pip.
4. Install Visual Studio Code.
5. Install the Python extension.
6. Select the Python interpreter.
7. Create a project folder.
8. Create three Python files.
9. Run all three programs successfully.
10. Explain the difference between Python and VS Code.
11. Explain what the terminal does.
12. Explain the purpose of PATH.

---

# Part 10 — Trainer Assessment

- [ ] Python is installed correctly.
- [ ] Python is accessible through the terminal.
- [ ] pip is working.
- [ ] VS Code is installed.
- [ ] Python extension is installed.
- [ ] Correct interpreter is selected.
- [ ] Student understands the project folder structure.
- [ ] Student can create and save `.py` files.
- [ ] Student can execute Python files through the terminal.
- [ ] Student can use the VS Code Run button.
- [ ] Student can identify and resolve basic setup errors.

## Day 2 Completion Criteria

The student must independently create a Python project folder, create Python files, write code, save files and execute programs using the terminal.

**Next Lesson:** Day 3 — Python Interpreter, Python Shell vs Script, First Program, print(), Syntax, Indentation, Comments, Keywords and Identifiers.

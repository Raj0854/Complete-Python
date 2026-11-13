
# Day 40 – Virtual Environments, pip & Dependencies

## 1. Introduction to Python Environments

A Python environment is the setup in which Python code runs.

It includes:

- Python interpreter
- Installed packages
- Project dependencies
- Environment configuration

For example, a project may require:

- Flask
- SQLAlchemy
- Requests

Another project may require different packages or different package versions.

Managing these dependencies separately is important.

### Understanding the Problem

Imagine you are working on two projects.

**Project A:**

```text
Flask 2.x
SQLAlchemy 2.x
```

**Project B:**

```text
Flask 3.x
SQLAlchemy 1.x
```

If both projects use the same global Python environment, installing or upgrading a package for one project may affect the other.

This can create compatibility problems.

### Solution: Virtual Environments

A virtual environment creates an isolated Python environment for a project.

Each project can have its own installed packages without interfering with other projects.

```text
Computer
   |
   |---- Python Installation
   |
   |---- Project A
   |       |
   |       |---- Virtual Environment A
   |       |---- Flask
   |       |---- SQLAlchemy
   |
   |---- Project B
           |
           |---- Virtual Environment B
           |---- Different Flask Version
           |---- Different SQLAlchemy Version
```

---

## 2. What Is pip?

`pip` is Python's standard package installer.

It is used to install, upgrade, remove and manage Python packages from package repositories such as PyPI.

PyPI stands for **Python Package Index**.

Website:

https://pypi.org/

### Common pip Commands

Check pip version:

```bash
python -m pip --version
```

Install a package:

```bash
python -m pip install requests
```

Upgrade a package:

```bash
python -m pip install --upgrade requests
```

Uninstall a package:

```bash
python -m pip uninstall requests
```

List installed packages:

```bash
python -m pip list
```

Show package information:

```bash
python -m pip show requests
```

Save installed packages:

```bash
python -m pip freeze
```

### Why Use `python -m pip`?

Instead of:

```bash
pip install requests
```

Prefer:

```bash
python -m pip install requests
```

This runs pip through the selected Python interpreter and reduces the chance of installing packages into the wrong Python installation.

---

## 3. Checking Python Installation

Before creating a virtual environment, check the Python installation.

### Check Python Version

```bash
python --version
```

Example output:

```text
Python 3.x.x
```

### Find Python Executable

Windows:

```bash
where python
```

Linux/macOS:

```bash
which python
```

### Check pip

```bash
python -m pip --version
```

If pip is unavailable, try:

```bash
python -m ensurepip --upgrade
```

Then verify again:

```bash
python -m pip --version
```

---

## 4. Creating a Virtual Environment

Python provides the built-in `venv` module for creating virtual environments.

No separate package installation is required.

### Step 1: Create a Project Folder

```bash
mkdir MyPythonProject
cd MyPythonProject
```

### Step 2: Create a Virtual Environment

Windows:

```bash
python -m venv venv
```

Linux/macOS:

```bash
python3 -m venv venv
```

This creates a directory named `venv`.

### Project Structure

```text
MyPythonProject/
    |
    |---- venv/
```

The virtual environment contains its own Python executable and package installation location.

### Understanding the Command

```bash
python -m venv venv
```

- `python` – Runs Python.
- `-m` – Executes a Python module.
- `venv` – Built-in virtual environment module.
- Last `venv` – Name of the environment directory.

You can choose another name:

```bash
python -m venv .venv
```

`.venv` is a common naming convention.

---

## 5. Activating a Virtual Environment

Creating a virtual environment does not automatically activate it.

You must activate it before installing packages or running project commands.

### Windows – Command Prompt

```cmd
venv\Scripts\activate.bat
```

### Windows – PowerShell

```powershell
.\venv\Scripts\Activate.ps1
```

If PowerShell blocks activation because of its execution policy, you can use Command Prompt or temporarily adjust the policy for the current PowerShell process:

```powershell
Set-ExecutionPolicy -Scope Process -ExecutionPolicy Bypass
```

Then activate:

```powershell
.\venv\Scripts\Activate.ps1
```

This changes the policy only for the current PowerShell session.

### Linux/macOS

```bash
source venv/bin/activate
```

### How to Verify Activation

After activation, the terminal generally displays the environment name.

Example:

```text
(venv) C:\MyPythonProject>
```

The `(venv)` prefix indicates that the virtual environment is active.

### Important

The activation command differs depending on the operating system and terminal.

---

## 6. Deactivating a Virtual Environment

To exit an active virtual environment:

```bash
deactivate
```

The environment prefix disappears from the terminal.

Example:

Before:

```text
(venv) C:\MyPythonProject>
```

After:

```text
C:\MyPythonProject>
```

Deactivation does not delete the virtual environment.

It simply returns the terminal to its previous Python environment.

---

## 7. Installing Packages Inside a Virtual Environment

Activate the environment first.

Then install a package:

```bash
python -m pip install requests
```

Install multiple packages:

```bash
python -m pip install requests flask sqlalchemy
```

Check installed packages:

```bash
python -m pip list
```

Example output:

```text
Package       Version
------------- -------
pip           25.x
requests      2.x
```

The exact versions may differ.

### Verify the Package Location

```bash
python -m pip show requests
```

Look for:

```text
Location: ...\MyPythonProject\venv\Lib\site-packages
```

This confirms that the package is installed inside the virtual environment.

### Test the Package

Create `test_requests.py`:

```python
import requests

print("Requests package imported successfully!")
print("Version:", requests.__version__)
```

Run:

```bash
python test_requests.py
```

Expected output:

```text
Requests package imported successfully!
Version: 2.x.x
```

The version may differ.

---

## 8. Understanding Global vs Virtual Environment Packages

### Global Environment

Packages installed into the main Python installation are generally available outside individual virtual environments.

### Virtual Environment

Packages installed into an active virtual environment belong to that environment.

### Comparison

| Global Environment | Virtual Environment |
|---|---|
| Shared across projects | Isolated for a project |
| Package changes can affect other projects | Package changes stay within the environment |
| Can become difficult to manage | Easier dependency management |
| Less suitable for separate project requirements | Recommended for project development |

### Practical Demonstration

1. Deactivate your virtual environment.
2. Run:

```bash
python -m pip list
```

3. Activate the virtual environment again.
4. Run the same command.

You may see different installed packages in each environment.

**Important:** A virtual environment is isolated from other project environments, but it still uses the underlying base Python installation.

---

## 9. Understanding requirements.txt

`requirements.txt` is a text file commonly used to list project dependencies.

It helps another developer install the packages required by your project.

### Example Project

```text
StudentManagementSystem/
    |
    |---- main.py
    |---- database.py
    |---- models.py
    |---- requirements.txt
    |---- venv/
```

### Create requirements.txt

Example:

```text
requests
SQLAlchemy
Flask
```

Each line represents a dependency.

### Install Dependencies from requirements.txt

```bash
python -m pip install -r requirements.txt
```

pip installs the listed packages.

### Why Is requirements.txt Important?

Suppose you share your project with another developer.

Instead of asking them to install packages individually, you can share the dependency list.

They can run:

```bash
python -m pip install -r requirements.txt
```

---

## 10. Understanding pip freeze

`pip freeze` displays installed packages in a format that can be used as a requirements file.

### Display Installed Packages

```bash
python -m pip freeze
```

Example:

```text
Flask==3.x.x
requests==2.x.x
SQLAlchemy==2.x.x
```

The exact versions may differ.

### Save Dependencies to requirements.txt

```bash
python -m pip freeze > requirements.txt
```

This writes installed package versions into the file.

### Install Exact Versions

Suppose requirements.txt contains:

```text
requests==2.32.0
```

This specifies that version 2.32.0 is required.

Install it using:

```bash
python -m pip install -r requirements.txt
```

### Version Specifiers

| Syntax | Meaning |
|---|---|
| `requests==2.32.0` | Exactly version 2.32.0 |
| `requests>=2.30.0` | Version 2.30.0 or newer |
| `requests<=2.32.0` | Version 2.32.0 or older |
| `requests!=2.31.0` | Excludes version 2.31.0 |
| `requests~=2.30.0` | Compatible release range beginning at 2.30.0 |

### Important Difference

`pip list` is intended for displaying installed packages in a readable format.

`pip freeze` outputs installed packages in a requirements-style format.

---

## 11. Installing a Specific Package Version

Sometimes a project requires an older or specific package version.

### Install a Specific Version

```bash
python -m pip install requests==2.31.0
```

### Upgrade to Latest Compatible Version

```bash
python -m pip install --upgrade requests
```

### Check Installed Version

```bash
python -m pip show requests
```

Or:

```bash
python -c "import requests; print(requests.__version__)"
```

### Why Package Versions Matter

Different package versions may contain:

- Different features.
- Bug fixes.
- Security updates.
- Breaking changes.
- Different Python compatibility requirements.

Always check project compatibility before upgrading important dependencies.

---

## 12. Uninstalling and Reinstalling Packages

### Uninstall a Package

```bash
python -m pip uninstall requests
```

pip asks for confirmation.

### Skip Confirmation

```bash
python -m pip uninstall -y requests
```

### Reinstall a Package

```bash
python -m pip install --force-reinstall requests
```

### Install Without Using Cached Packages

```bash
python -m pip install --no-cache-dir requests
```

### Important

Before removing a package, check whether other parts of your project depend on it.

---

## 13. Understanding Python Interpreter Selection in VS Code

VS Code can have multiple Python installations and virtual environments.

Selecting the correct interpreter is important.

### Steps

1. Open the project folder in VS Code.
2. Press `Ctrl + Shift + P`.
3. Search for `Python: Select Interpreter`.
4. Select the interpreter inside your project environment.
5. Open a new terminal.
6. Verify the selected Python.

### Windows Example

```powershell
python -c "import sys; print(sys.executable)"
```

Expected path:

```text
C:\MyPythonProject\venv\Scripts\python.exe
```

### Linux/macOS Example

```bash
python -c "import sys; print(sys.executable)"
```

Expected path:

```text
/path/to/MyPythonProject/venv/bin/python
```

### Important

Selecting an interpreter in VS Code and activating an environment in a terminal are related but separate operations.

Always verify the interpreter path when troubleshooting package import errors.

---

## 14. Understanding .gitignore for Virtual Environments

A virtual environment contains many files and installed packages.

It should generally not be uploaded to GitHub.

Instead, upload your project code and dependency file.

### Create .gitignore

```text
venv/
.venv/

__pycache__/
*.py[cod]

.env

.pytest_cache/
```

### Why Ignore venv?

1. It can contain thousands of files.
2. It increases repository size.
3. It is specific to the local machine.
4. Another developer can recreate it using requirements.txt.

### Example Project Structure

```text
MyPythonProject/
    |
    |---- .venv/
    |---- .gitignore
    |---- requirements.txt
    |---- main.py
    |---- README.md
```

The `.venv` directory remains on your computer but is excluded from Git tracking.

### Important

Do not commit `.env` files containing API keys, passwords or other secrets.

---

## 15. Understanding Environment Variables

Environment variables store configuration outside the source code.

They are useful for:

- API keys.
- Database URLs.
- Secret tokens.
- Application configuration.
- Environment-specific settings.

### Problem with Hardcoding Secrets

Avoid:

```python
API_KEY = "my-secret-api-key"
```

If this code is uploaded to GitHub, the secret may become publicly visible.

### Read an Environment Variable

```python
import os

api_key = os.getenv("API_KEY")

if api_key:
    print("API key is configured.")
else:
    print("API key is missing.")
```

### Set Environment Variable in Windows PowerShell

```powershell
$env:API_KEY = "your-secret-value"
```

### Set Environment Variable in Linux/macOS

```bash
export API_KEY="your-secret-value"
```

### Verify

```python
import os

print(os.getenv("API_KEY"))
```

### Important

Environment variables configured this way are generally available to processes launched from that terminal session.

Do not print real secrets in logs or share them in screenshots.

---

## 16. Using python-dotenv

`python-dotenv` is a third-party package that loads environment variables from a `.env` file.

### Install

```bash
python -m pip install python-dotenv
```

### Create .env

```text
API_KEY=your-secret-value
DATABASE_URL=sqlite:///school.db
```

### Create config.py

```python
import os
from dotenv import load_dotenv

load_dotenv()

API_KEY = os.getenv("API_KEY")

DATABASE_URL = os.getenv("DATABASE_URL")

print("Database URL:", DATABASE_URL)

if API_KEY:
    print("API key loaded successfully.")
else:
    print("API key not found.")
```

### Run

```bash
python config.py
```

Expected output:

```text
Database URL: sqlite:///school.db
API key loaded successfully.
```

### Update requirements.txt

```text
python-dotenv
```

Or regenerate the full environment dependency list using:

```bash
python -m pip freeze > requirements.txt
```

### Important Security Rules

1. Never upload `.env` to GitHub.
2. Add `.env` to `.gitignore`.
3. Share a `.env.example` file with placeholder values.
4. Never put real passwords or API keys in source code.
5. If a secret is accidentally published, rotate or revoke it.

---

## 17. Understanding Dependency Conflicts

A dependency conflict occurs when two or more packages require incompatible versions of another package.

### Example

```text
Package A requires Library X version 1.x

Package B requires Library X version 2.x
```

The requirements may be incompatible.

### Why Conflicts Happen

- Different package version requirements.
- Outdated dependencies.
- Incompatible Python versions.
- Package upgrades introducing breaking changes.

### Check Dependency Information

```bash
python -m pip show requests
```

### Check Installed Package Compatibility

```bash
python -m pip check
```

This checks whether installed packages have compatible dependencies.

Example output when no broken requirements are found:

```text
No broken requirements found.
```

### Recommended Solutions

1. Use a separate virtual environment for each project.
2. Check package compatibility.
3. Avoid unnecessary package upgrades.
4. Keep dependency versions documented.
5. Use a clean environment when troubleshooting.

---

## 18. Understanding Python Package Installation Locations

Python packages are installed into a directory called `site-packages`.

### Find the Location

```python
import site

print(site.getsitepackages())
```

### Find Python Executable

```python
import sys

print(sys.executable)
```

### Find Package Location

```python
import requests

print(requests.__file__)
```

These commands help troubleshoot situations where Python cannot find an installed package.

---

## 19. Creating a Clean Development Environment

A professional Python project should have a predictable development environment.

### Recommended Project Structure

```text
PythonProject/
    |
    |---- .venv/
    |
    |---- src/
    |      |
    |      |---- main.py
    |
    |---- tests/
    |
    |---- requirements.txt
    |
    |---- .gitignore
    |
    |---- .env.example
    |
    |---- README.md
```

### Recommended Setup Workflow

1. Create the project directory.
2. Open the project in VS Code.
3. Create a virtual environment.
4. Activate the environment.
5. Upgrade pip if needed.
6. Install project dependencies.
7. Create requirements.txt.
8. Create .gitignore.
9. Select the correct VS Code interpreter.
10. Run and test the project.

### Upgrade pip

```bash
python -m pip install --upgrade pip
```

### Verify Environment

```bash
python --version
python -m pip --version
python -m pip list
python -c "import sys; print(sys.executable)"
```

---

# 20. Mini Project – Python Environment Setup Manager

## Project Description

Create a small Python command-line application that displays information about the current Python environment and installed packages.

This project will help students understand:

- Python interpreter information.
- Virtual environment detection.
- Installed packages.
- Package version information.
- Dependency management.
- Environment configuration.

## Project Structure

```text
EnvironmentManager/
    |
    |---- main.py
    |---- requirements.txt
    |---- .gitignore
    |---- README.md
    |---- .env.example
```

## Step 1: Create requirements.txt

```text
python-dotenv
```

Install dependencies:

```bash
python -m pip install -r requirements.txt
```

## Step 2: Create .gitignore

```text
.venv/
venv/

__pycache__/
*.py[cod]

.env
.pytest_cache/
```

## Step 3: Create .env.example

```text
APP_NAME=EnvironmentManager
APP_MODE=development
```

This file contains sample configuration, not real secrets.

## Step 4: Create main.py

```python
import sys
import os
import platform
import site

from importlib.metadata import distributions
from dotenv import load_dotenv


load_dotenv()


def display_python_information():

    print("\n========== PYTHON INFORMATION ==========")

    print("Python Version:", sys.version)

    print("Python Executable:", sys.executable)

    print("Platform:", platform.platform())

    print("Python Implementation:", platform.python_implementation())


def display_environment_information():

    print("\n========== ENVIRONMENT INFORMATION ==========")

    prefix = os.path.normcase(sys.prefix)

    base_prefix = os.path.normcase(sys.base_prefix)

    is_virtual = prefix != base_prefix

    print("Virtual Environment:", is_virtual)

    print("Environment Path:", sys.prefix)

    print("Base Python Path:", sys.base_prefix)

    print("Site Packages:", site.getsitepackages())


def display_installed_packages():

    print("\n========== INSTALLED PACKAGES ==========")

    packages = sorted(
        distributions(),
        key=lambda package: (
            package.metadata.get("Name") or ""
        ).lower()
    )

    if not packages:

        print("No packages found.")

        return

    for package in packages:

        name = package.metadata.get("Name", "Unknown")

        version = package.version

        print(f"{name} == {version}")


def display_application_configuration():

    print("\n========== APPLICATION CONFIGURATION ==========")

    app_name = os.getenv(
        "APP_NAME",
        "Unknown"
    )

    app_mode = os.getenv(
        "APP_MODE",
        "development"
    )

    print("Application Name:", app_name)

    print("Application Mode:", app_mode)


def main():

    while True:

        print("\n========== ENVIRONMENT MANAGER ==========")

        print("1. Python Information")

        print("2. Environment Information")

        print("3. Installed Packages")

        print("4. Application Configuration")

        print("5. Display Everything")

        print("6. Exit")

        choice = input("\nEnter choice: ").strip()

        if choice == "1":

            display_python_information()

        elif choice == "2":

            display_environment_information()

        elif choice == "3":

            display_installed_packages()

        elif choice == "4":

            display_application_configuration()

        elif choice == "5":

            display_python_information()

            display_environment_information()

            display_installed_packages()

            display_application_configuration()

        elif choice == "6":

            print("Environment Manager closed.")

            break

        else:

            print("Invalid choice. Try again.")


if __name__ == "__main__":

    main()
```

## Step 5: Run the Project

Activate the virtual environment and execute:

```bash
python main.py
```

Expected menu:

```text
========== ENVIRONMENT MANAGER ==========

1. Python Information
2. Environment Information
3. Installed Packages
4. Application Configuration
5. Display Everything
6. Exit

Enter choice:
```

### Sample Environment Output

```text
========== ENVIRONMENT INFORMATION ==========

Virtual Environment: True

Environment Path: .../EnvironmentManager/.venv

Base Python Path: .../Python
```

The exact paths depend on the operating system and Python installation.

### Project Challenges

1. Add an option to search for a specific installed package.
2. Display only package names and versions.
3. Export installed packages to a text file.
4. Display the number of installed packages.
5. Check whether a package is installed.
6. Add an option to display Python's executable path.
7. Display the application mode from the `.env` file.
8. Add proper error handling.

---

# 21. Student Practice Exercises

## Beginner Level

1. Check the installed Python version.
2. Check the pip version.
3. Install the `requests` package.
4. Display installed packages using pip.
5. Create a virtual environment named `venv`.
6. Activate the environment.
7. Install SQLAlchemy inside the environment.
8. Verify the SQLAlchemy installation.
9. Deactivate the environment.
10. Explain the difference between global and virtual environments.

## Intermediate Level

1. Create two separate Python projects.
2. Create an independent virtual environment for each project.
3. Install Flask in one environment.
4. Install Requests in another environment.
5. Compare the installed package lists.
6. Create requirements.txt.
7. Generate requirements.txt using `pip freeze`.
8. Install packages using requirements.txt.
9. Create a `.gitignore` file.
10. Configure environment variables.

## Advanced Level

1. Create a project using a virtual environment.
2. Install specific versions of multiple packages.
3. Export dependencies to requirements.txt.
4. Recreate the project environment from scratch.
5. Use `pip check` to inspect dependency compatibility.
6. Configure python-dotenv.
7. Build a package information utility.
8. Create a `.env.example` file.
9. Configure VS Code to use the correct interpreter.
10. Document the complete setup procedure in README.md.

---

# 22. Trainer Assessment

Ask the student to explain:

1. What is a Python environment?
2. What is pip?
3. What is PyPI?
4. What is a virtual environment?
5. Why do we use virtual environments?
6. What is the purpose of the `venv` module?
7. How do we create a virtual environment?
8. How do we activate and deactivate it?
9. What is the difference between global and virtual environments?
10. What is requirements.txt?
11. What does `pip freeze` do?
12. What is the difference between `pip list` and `pip freeze`?
13. How do we install a specific package version?
14. What is a dependency conflict?
15. Why should virtual environments not be uploaded to GitHub?
16. What is `.gitignore`?
17. What are environment variables?
18. What is python-dotenv?
19. Why should API keys not be hardcoded?
20. How do we select a Python interpreter in VS Code?

### Practical Assessment

Ask the student to independently:

- Create a Python project.
- Create a virtual environment.
- Activate the environment.
- Install multiple dependencies.
- Generate requirements.txt.
- Recreate the environment from requirements.txt.
- Configure `.gitignore`.
- Configure environment variables.
- Verify the correct Python interpreter.
- Run the project successfully.

---

# 23. Completion Criteria

Day 40 is complete when the student can:

- Explain Python environments and package management.
- Use pip to install, upgrade and uninstall packages.
- Create and activate virtual environments.
- Work with independent environments for different projects.
- Manage dependencies using requirements.txt.
- Understand package version specifications.
- Troubleshoot basic dependency conflicts.
- Select the correct interpreter in VS Code.
- Use `.gitignore` correctly.
- Configure environment variables.
- Use python-dotenv.
- Build and run the Environment Setup Manager independently.

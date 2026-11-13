
# Day 45 – Git, GitHub & Python Project Structure

## 1. Introduction to Version Control

Version Control is a system that tracks changes made to files over time.

It helps developers:
- Track changes in code.
- Restore previous versions.
- Work with multiple developers.
- Maintain project history.
- Create separate development branches.
- Collaborate without overwriting each other's work.

### Example

Imagine you are developing a Student Management System.

You make these changes:

```text
Version 1: Added student registration.
Version 2: Added student search.
Version 3: Added student update.
Version 4: Fixed a registration bug.
```

Git tracks these changes and allows you to return to an earlier version when needed.

### What is Git?

Git is a distributed version control system.

It is installed on your computer and tracks changes in your project.

### What is GitHub?

GitHub is an online platform that hosts Git repositories.

It allows developers to:
- Store code online.
- Collaborate with others.
- Review code.
- Manage project issues.
- Share projects publicly or privately.

### Git vs GitHub

| Git | GitHub |
|---|---|
| Version control tool | Code hosting platform |
| Works locally | Works online |
| Tracks code changes | Hosts Git repositories |
| Supports branches | Supports pull requests |
| Can work without internet | Requires internet for remote operations |

---

## 2. Installing Git

Download Git from:

https://git-scm.com/

Install Git using the default installation options.

Verify installation:

```bash
git --version
```

Expected output will look similar to:

```text
git version 2.x.x
```

The exact version may differ.

### Configure Git Identity

Git uses your name and email address to identify commits.

Configure your name:

```bash
git config --global user.name "Your Name"
```

Configure your email:

```bash
git config --global user.email "your-email@example.com"
```

Set the default branch name:

```bash
git config --global init.defaultBranch main
```

Check configuration:

```bash
git config --list
```

View a specific setting:

```bash
git config user.name
git config user.email
```

**Important:** Use the email address associated with your GitHub account if you want your commits to be linked to that account.

---

## 3. Understanding a Git Repository

A repository is a project directory tracked by Git.

A Git repository contains a hidden `.git` directory.

This directory stores:
- Commit history.
- Branch information.
- Repository configuration.
- Version control data.

### Three Important Areas in Git

Git uses three main areas:

1. Working Directory
2. Staging Area
3. Repository

### Working Directory

This is where you create and modify files.

Example:

```python
print("Hello Python")
```

### Staging Area

This is where you select changes that should be included in the next commit.

Command:

```bash
git add main.py
```

### Repository

This stores committed snapshots of your project.

Command:

```bash
git commit -m "Add main Python file"
```

### Git Workflow

```text
Working Directory
       |
       | git add
       v
Staging Area
       |
       | git commit
       v
Local Repository
       |
       | git push
       v
GitHub Repository
```

---

## 4. Creating Your First Git Repository

Create a project folder:

```bash
mkdir GitPractice
cd GitPractice
```

Create a Python file named `main.py`:

```python
print("Welcome to Git and GitHub")
```

Initialize Git:

```bash
git init
```

Expected output will indicate that an empty Git repository was initialized.

Check repository status:

```bash
git status
```

Git will show `main.py` as an untracked file.

### Add a File to Staging

```bash
git add main.py
```

Check status:

```bash
git status
```

### Commit Your Changes

```bash
git commit -m "Add initial Python program"
```

Expected output will show that a commit was created.

### Check Commit History

```bash
git log
```

Compact history:

```bash
git log --oneline
```

### Important Commands

| Command | Purpose |
|---|---|
| `git init` | Initialize repository |
| `git status` | Check file status |
| `git add` | Stage changes |
| `git commit` | Save a commit |
| `git log` | View commit history |
| `git log --oneline` | Compact history |

---

## 5. Understanding Git Add and Commit

Suppose you modify `main.py`:

```python
print("Welcome to Git and GitHub")
print("Learning Version Control")
```

Check changes:

```bash
git status
```

View unstaged changes:

```bash
git diff
```

Stage the file:

```bash
git add main.py
```

View staged changes:

```bash
git diff --staged
```

Commit:

```bash
git commit -m "Add version control learning message"
```

### Adding Multiple Files

Add all changes in the current repository:

```bash
git add .
```

Commit:

```bash
git commit -m "Update project files"
```

**Note:** Review `git status` before staging everything. Do not accidentally commit private files, database files, or generated files.

---

## 6. Understanding Git File States

Git commonly displays these file states:

| State | Meaning |
|---|---|
| Untracked | Git is not tracking the file |
| Modified | A tracked file has changed |
| Staged | Changes are ready for commit |
| Committed | Changes are saved in repository history |

### Example Workflow

```text
Create file
    |
    v
Untracked
    |
    | git add
    v
Staged
    |
    | git commit
    v
Committed
    |
    | Edit file
    v
Modified
```

---

## 7. Undoing Changes Safely

Git provides commands to undo different types of changes.

### Discard Unstaged Changes

```bash
git restore main.py
```

This restores the file to its last committed or staged version.

**Warning:** Uncommitted changes in the working file can be permanently lost.

### Remove a File from Staging

```bash
git restore --staged main.py
```

This removes the file from the staging area but keeps its changes in the working directory.

### Undo a Published Commit Safely

Use:

```bash
git revert COMMIT_ID
```

This creates a new commit that reverses the changes introduced by an earlier commit.

Find the commit ID:

```bash
git log --oneline
```

Example:

```bash
git revert abc1234
```

Replace `abc1234` with the actual commit ID.

### Understanding Git Reset

```bash
git reset --soft HEAD~1
```

Moves the current branch back one commit while keeping changes staged.

```bash
git reset --mixed HEAD~1
```

Moves the current branch back one commit and keeps changes unstaged.

```bash
git reset --hard HEAD~1
```

Moves the current branch back one commit and discards changes from the working directory and staging area.

**Important:** `--hard` can permanently destroy uncommitted work. Avoid it unless you fully understand the consequences.

Do not rewrite published Git history casually. Prefer `git revert` when reversing commits already shared with others.

---

## 8. Understanding .gitignore

Sometimes a project contains files that should not be uploaded to GitHub.

Examples:
- Python cache files.
- Virtual environments.
- Database files.
- Environment variables.
- IDE settings.

A `.gitignore` file tells Git which untracked files and directories to ignore.

Create a file named:

```text
.gitignore
```

Example:

```gitignore
# Python cache
__pycache__/
*.py[cod]

# Virtual environments
.venv/
venv/
env/

# Environment variables and secrets
.env
.env.*

# Database files
*.db
*.sqlite3

# IDE settings
.vscode/
.idea/

# Operating system files
.DS_Store
Thumbs.db

# Test and coverage output
.pytest_cache/
.coverage
htmlcov/
```

### Important Notes

- `.gitignore` does not automatically remove files already tracked by Git.
- Never commit passwords, API keys, tokens, or private credentials.
- If a secret has already been pushed, deleting the file is not enough. Rotate or revoke the exposed secret.

### Check Ignored Files

```bash
git status --ignored
```

### Stop Tracking an Already Tracked File

For example:

```bash
git rm --cached database.db
```

Then commit the change:

```bash
git add .gitignore
git commit -m "Ignore local database file"
```

---

## 9. Creating a GitHub Repository

Open:

https://github.com/

1. Create an account or sign in.
2. Click the New Repository option.
3. Enter a repository name.
4. Select Public or Private.
5. Create the repository.

For this exercise, create:

```text
GitPractice
```

If your local project already contains files and commits, create an empty GitHub repository without initializing it with a README or `.gitignore`.

### Connect Local Repository to GitHub

Copy the repository URL from GitHub.

Example:

```text
https://github.com/username/GitPractice.git
```

Add the remote:

```bash
git remote add origin https://github.com/username/GitPractice.git
```

Verify:

```bash
git remote -v
```

Rename the current branch to main if necessary:

```bash
git branch -M main
```

Push your code:

```bash
git push -u origin main
```

The `-u` option sets the upstream branch so future pushes can usually use:

```bash
git push
```

**Note:** GitHub may require browser-based authentication or a supported credential manager. A GitHub account password is not normally used as an HTTPS Git password.

---

## 10. Understanding Push, Pull, Fetch and Clone

### git push

Uploads local commits to the remote repository.

```bash
git push
```

### git pull

Downloads remote changes and integrates them into the current branch.

```bash
git pull
```

### git fetch

Downloads remote updates without merging them into the current branch.

```bash
git fetch
```

After fetching, inspect remote changes:

```bash
git log HEAD..origin/main --oneline
```

### git clone

Downloads an existing repository and creates a local working copy.

```bash
git clone https://github.com/username/GitPractice.git
```

### Command Comparison

| Command | Purpose |
|---|---|
| `git push` | Upload local commits |
| `git pull` | Fetch and integrate remote changes |
| `git fetch` | Download remote updates only |
| `git clone` | Copy a remote repository locally |

---

## 11. Working with Git Branches

A branch allows developers to work on a separate line of development.

For example:

```text
main
 |
 |---- feature/student-search
 |
 |---- feature/student-update
```

The `main` branch usually contains the stable project version.

Feature branches are used to develop individual features.

### View Branches

```bash
git branch
```

### Create and Switch to a New Branch

```bash
git switch -c feature/student-search
```

### Switch to Another Branch

```bash
git switch main
```

### Create a Branch Without Switching

```bash
git branch feature/student-update
```

### Switch to an Existing Branch

```bash
git switch feature/student-update
```

### Delete a Branch

```bash
git branch -d feature/student-search
```

Git normally prevents deleting a branch that has unmerged work.

To force-delete a branch:

```bash
git branch -D feature/student-search
```

Use force deletion only when you are certain the work is no longer needed.

---

## 12. Merging Branches

Merging combines changes from one branch into another.

Suppose you created:

```text
feature/student-search
```

After completing the feature:

```bash
git add .
git commit -m "Add student search feature"
```

Switch to main:

```bash
git switch main
```

Merge the feature branch:

```bash
git merge feature/student-search
```

If the merge succeeds, the changes become part of `main`.

Delete the feature branch after confirming the merge:

```bash
git branch -d feature/student-search
```

---

## 13. Understanding Merge Conflicts

A merge conflict occurs when Git cannot automatically combine changes.

For example, two developers modify the same part of `main.py`.

Git may display:

```text
<<<<<<< HEAD
print("Welcome Student")
=======
print("Welcome Admin")
>>>>>>> feature/welcome-message
```

These markers identify conflicting changes.

### Resolving a Conflict

1. Open the conflicting file.
2. Review both versions.
3. Decide which content should remain.
4. Edit the file manually.
5. Remove all conflict markers.
6. Save the file.
7. Stage the resolved file.
8. Complete the merge.

Commands:

```bash
git add main.py
git commit -m "Resolve welcome message merge conflict"
```

If Git opened an editor for a merge commit, save and close it to complete the merge.

**Important:** Do not blindly delete one side of a conflict. Understand the changes before resolving it.

---

## 14. Understanding Pull Requests

A Pull Request (PR) is a GitHub feature used to propose changes from one branch into another.

Example:

```text
main
  |
  |---- feature/login-system
```

After completing the feature:

1. Push the feature branch.
2. Open GitHub.
3. Select the feature branch.
4. Create a Pull Request.
5. Add a title and description.
6. Ask another developer to review it.
7. Make requested changes if necessary.
8. Merge the Pull Request.

### Common Pull Request Activities

- Code review.
- Discussion.
- Automated testing.
- Suggestions.
- Approving changes.
- Merging branches.

A Pull Request is a collaboration and review process. It is not the same as `git push`.

---

## 15. Understanding GitHub Issues

GitHub Issues help teams track project work.

Examples:

```text
Issue 1: Fix student registration validation.
Issue 2: Add student search.
Issue 3: Improve error handling.
Issue 4: Write unit tests.
```

An issue can contain:
- Title.
- Description.
- Labels.
- Assignee.
- Comments.
- Project references.

Developers use issues to organize bugs, improvements, and tasks.

---

## 16. Professional Python Project Structure

A professional Python project should have a clear and organized directory structure.

Example:

```text
StudentManagement/
│
├── src/
│   └── student_management/
│       ├── __init__.py
│       ├── main.py
│       ├── student.py
│       ├── operations.py
│       └── validation.py
│
├── tests/
│   ├── __init__.py
│   └── test_student.py
│
├── data/
│   └── .gitkeep
│
├── docs/
│
├── .gitignore
├── README.md
├── requirements.txt
└── pyproject.toml
```

### Purpose of Each Folder and File

| File/Folder | Purpose |
|---|---|
| `src/` | Contains application source code |
| `student_management/` | Main Python package |
| `__init__.py` | Marks a regular Python package |
| `main.py` | Application entry point |
| `student.py` | Student-related classes and data |
| `operations.py` | Application operations |
| `validation.py` | Input validation functions |
| `tests/` | Automated tests |
| `data/` | Local data files |
| `docs/` | Project documentation |
| `.gitignore` | Files Git should ignore |
| `README.md` | Project documentation |
| `requirements.txt` | Python dependencies |
| `pyproject.toml` | Project and tool configuration |

**Note:** The `src/` layout separates importable application code from other project files. A package in `src/` generally needs to be installed into the environment, often using an editable install during development.

### What is __init__.py?

It is a Python package initialization file.

Example:

```python
# student_management/__init__.py

print("Student Management package loaded")
```

It can also expose selected package functionality.

Example:

```python
from .student import Student
```

Modern Python supports namespace packages without `__init__.py`, but regular packages commonly include it.

---

## 17. Creating a Modular Python Project

Create this structure:

```text
StudentManagement/
│
├── student_management/
│   ├── __init__.py
│   ├── student.py
│   ├── operations.py
│   └── main.py
│
└── README.md
```

### student.py

```python
class Student:

    def __init__(self, student_id, name, marks):
        self.student_id = student_id
        self.name = name
        self.marks = marks

    def display(self):
        print("ID:", self.student_id)
        print("Name:", self.name)
        print("Marks:", self.marks)
```

### operations.py

```python
from student_management.student import Student


students = []


def add_student(student_id, name, marks):

    student = Student(student_id, name, marks)

    students.append(student)

    print("Student added successfully")


def view_students():

    if not students:
        print("No students found")
        return

    for student in students:
        student.display()
        print("-" * 20)
```

### main.py

```python
from student_management.operations import (
    add_student,
    view_students
)


def main():

    add_student(101, "Rahul", 85)
    add_student(102, "Priya", 92)

    print("\nStudent Records")

    view_students()


if __name__ == "__main__":
    main()
```

Run from the project root:

```bash
python -m student_management.main
```

Expected output:

```text
Student added successfully
Student added successfully

Student Records
ID: 101
Name: Rahul
Marks: 85
--------------------
ID: 102
Name: Priya
Marks: 92
--------------------
```

This example uses a regular package directly from the project root. It is a simple demonstration of modular code organization.

---

## 18. Understanding README.md

A README file explains what a project does and how someone can use it.

A professional README commonly includes:

1. Project name.
2. Project description.
3. Features.
4. Technologies used.
5. Project structure.
6. Installation instructions.
7. Usage instructions.
8. Testing instructions.
9. Contribution guidelines.
10. License information, when applicable.

### Example README.md

```markdown
# Student Management System

A Python application for managing student records.

## Features

- Add students
- View students
- Search students
- Update student records
- Delete student records

## Technologies

- Python
- Object-Oriented Programming

## Installation

Clone the repository:

git clone https://github.com/username/StudentManagement.git

Move into the project directory:

cd StudentManagement

## Usage

Run:

python -m student_management.main

## Testing

Run the test suite:

python -m unittest discover -s tests
```

A good README should contain accurate commands that work with the actual project structure.

---

## 19. Understanding requirements.txt

The `requirements.txt` file lists third-party Python dependencies.

Example:

```text
requests==2.32.3
pytest==8.3.5
```

Install dependencies:

```bash
python -m pip install -r requirements.txt
```

Generate a list of installed packages:

```bash
python -m pip freeze > requirements.txt
```

View installed packages:

```bash
python -m pip list
```

**Important:** Do not blindly place every globally installed package into a project's dependency file. Use a project-specific virtual environment.

---

## 20. Introduction to pyproject.toml

`pyproject.toml` is a modern Python project configuration file.

It can store:
- Project metadata.
- Build system configuration.
- Development tool settings.
- Package configuration.
- Dependency information.

Example:

```toml
[project]
name = "student-management"
version = "1.0.0"
description = "A simple student management application"
requires-python = ">=3.10"
dependencies = []

[project.optional-dependencies]
dev = [
    "pytest"
]

[tool.pytest.ini_options]
testpaths = ["tests"]
```

Install development dependencies when using this project configuration:

```bash
python -m pip install -e ".[dev]"
```

This command assumes the project has a valid build configuration. For a complete installable package, configure the build system and package discovery appropriately.

`requirements.txt` is commonly used to list dependencies, while `pyproject.toml` can define broader project metadata and configuration.

---

## 21. Common Git Mistakes

| Mistake | Better Practice |
|---|---|
| Forgetting to commit | Check `git status` regularly |
| Committing everything blindly | Review staged changes |
| Uploading `.env` | Add secrets to `.gitignore` |
| Working directly on main | Use feature branches |
| Writing unclear commit messages | Use descriptive messages |
| Ignoring merge conflicts | Review both sides |
| Using `reset --hard` carelessly | Understand its data-loss risk |
| Forgetting to pull remote changes | Sync before collaborating |
| Committing virtual environments | Ignore `.venv/` |
| Writing an empty README | Document setup and usage |

### Good Commit Messages

```text
Add student registration feature
Fix student search validation
Update employee salary calculation
Add unit tests for student operations
Improve project documentation
```

Avoid vague messages such as:

```text
update
changes
final
done
```

---

## 22. Practical Exercise – Git Commands

Create a new project:

```text
GitExercise/
    main.py
    README.md
    .gitignore
```

Complete these tasks:

1. Initialize a Git repository.
2. Check repository status.
3. Add `main.py`.
4. Create the first commit.
5. Modify `main.py`.
6. View the changes using `git diff`.
7. Stage the changes.
8. Commit the changes.
9. Create a feature branch.
10. Add a new Python function.
11. Commit the feature.
12. Switch to main.
13. Merge the feature branch.
14. Connect the repository to GitHub.
15. Push the repository.
16. Verify that the files are visible on GitHub.

---

## 23. Mini Project – Student Management System with Git and GitHub

### Project Description

Take an existing Student Management CLI application and prepare it as a professionally organized, version-controlled Python project.

### Suggested Structure

```text
StudentManagement/
│
├── student_management/
│   ├── __init__.py
│   ├── student.py
│   ├── operations.py
│   ├── validation.py
│   └── main.py
│
├── tests/
│   ├── __init__.py
│   └── test_student.py
│
├── data/
│
├── .gitignore
├── README.md
└── requirements.txt
```

### Application Features

- Add student.
- View all students.
- Search student by ID.
- Update student details.
- Delete student.
- Calculate average marks.
- Display highest-scoring student.
- Validate student input.

### Git and GitHub Requirements

1. Organize the Python files into modules.
2. Create a README file.
3. Create a `.gitignore` file.
4. Initialize a Git repository.
5. Create meaningful commits.
6. Create a GitHub repository.
7. Push the main branch.
8. Create a feature branch named `feature/student-search`.
9. Implement student search in that branch.
10. Commit and push the feature branch.
11. Create a Pull Request on GitHub.
12. Review and merge the Pull Request.
13. Verify the final project on GitHub.

### Expected Final Result

The student should have:
- A modular Python project.
- A Git repository with meaningful history.
- A GitHub repository.
- A useful README.
- A working `.gitignore`.
- At least one feature branch.
- A merged Pull Request.

---

## 24. Student Practice Questions

### Conceptual Questions

1. What is version control?
2. What is Git?
3. What is GitHub?
4. Explain the difference between Git and GitHub.
5. What is a repository?
6. What is the staging area?
7. What is a commit?
8. What is a branch?
9. What is a merge conflict?
10. What is a Pull Request?
11. What is `.gitignore`?
12. What is the purpose of README.md?
13. What is the purpose of requirements.txt?
14. What is pyproject.toml?
15. Why should developers avoid committing API keys?

### Practical Questions

1. Create a Git repository.
2. Add and commit a Python file.
3. Display the commit history.
4. Check differences between file versions.
5. Create a new branch.
6. Merge a feature branch.
7. Create a `.gitignore` file for a Python project.
8. Connect a local repository to GitHub.
9. Clone an existing repository.
10. Create a Pull Request.

---

## 25. Trainer Assessment

Ask the student to demonstrate the following:

| Assessment | Expected Result |
|---|---|
| Git installation | Git runs successfully |
| Git configuration | Name and email configured |
| Repository initialization | Repository created |
| Staging and committing | Changes committed correctly |
| Git history | Can inspect commit history |
| Branch management | Can create and switch branches |
| Merge operation | Can merge a feature branch |
| GitHub connection | Local repository connected |
| Push and pull | Can synchronize changes |
| .gitignore | Unnecessary files excluded |
| README | Project documented |
| Python structure | Application organized into modules |
| Pull Request | Can create and merge a PR |

---

## 26. Completion Criteria

Day 45 is complete when the student can:

- Explain Git and GitHub.
- Create and manage a Git repository.
- Track changes using commits.
- Use staging and working directory correctly.
- Create and merge branches.
- Understand and resolve basic merge conflicts.
- Push and pull code from GitHub.
- Clone repositories.
- Create a useful `.gitignore`.
- Write a project README.
- Organize Python applications into modules and packages.
- Understand the basic purpose of `requirements.txt` and `pyproject.toml`.
- Publish a structured Python project on GitHub.

**Trainer Note:** The student should complete the Student Management System project and publish it on GitHub before moving to the next learning track.

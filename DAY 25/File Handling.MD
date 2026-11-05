
# Day 25 – Python File Handling

## 1. Introduction to File Handling

Until now, most of our programs have stored data in variables, lists and dictionaries.

But there is one major problem: when the program terminates, data stored in memory is generally lost.

For example:

```python
student_name = "Raj"
student_marks = 90

print(student_name)
print(student_marks)
```

If we close the program, these variable values are not automatically saved.

To store data permanently, we use **File Handling**.

### What is File Handling?

File handling means performing operations on files using a programming language.

Python allows us to:

- Create files.
- Read existing files.
- Write data into files.
- Append new data.
- Update file contents.
- Delete files.
- Work with directories.
- Handle text and binary files.

### Common File Types

| File Type | Extension | Purpose |
|---|---|---|
| Text File | `.txt` | Store plain text |
| Python File | `.py` | Store Python code |
| CSV File | `.csv` | Store tabular data |
| JSON File | `.json` | Store structured data |
| PDF File | `.pdf` | Store documents |
| Image File | `.png`, `.jpg` | Store images |
| Binary File | `.bin` | Store binary data |

We will first focus on text files.

---

## 2. Opening a File Using open()

Python provides the built-in `open()` function to open files.

### Syntax

```python
file = open("filename", "mode")
```

Parameters:

- `filename`: Name or path of the file.
- `mode`: Specifies what operation we want to perform.

Example:

```python
file = open("student.txt", "r")
```

This attempts to open `student.txt` in read mode.

**Important:** If the file does not exist, opening it in read mode raises `FileNotFoundError`.

---

## 3. Understanding File Modes

File modes determine how Python interacts with a file.

| Mode | Meaning |
|---|---|
| `r` | Read an existing file |
| `w` | Write; creates or truncates a file |
| `a` | Append; creates a file if it does not exist |
| `x` | Create a new file; fails if it already exists |
| `t` | Text mode |
| `b` | Binary mode |
| `r+` | Read and write an existing file |
| `w+` | Read and write; truncates or creates |
| `a+` | Read and append; creates if missing |

### Important Differences

**Read (`r`):**

- File must exist.
- Existing content is not modified.

**Write (`w`):**

- Creates the file if it does not exist.
- Removes the existing content if the file already exists.

**Append (`a`):**

- Adds new content at the end.
- Preserves existing content.
- Creates the file if it does not exist.

**Exclusive Create (`x`):**

- Creates a new file.
- Raises `FileExistsError` if the file already exists.

---

## 4. Creating and Writing a File

We can use write mode (`w`) to create a file and write data into it.

### Example

```python
file = open("student.txt", "w")

file.write("Welcome to Python File Handling")

file.close()
```

This creates `student.txt` and writes the text.

### Understanding write()

The `write()` method writes a string into the file.

```python
file.write("Hello Python")
```

It returns the number of characters written.

### Writing Multiple Lines

```python
file = open("student.txt", "w")

file.write("Student Name: Raj\n")
file.write("Course: Python\n")
file.write("Marks: 90\n")

file.close()
```

File content:

```text
Student Name: Raj
Course: Python
Marks: 90
```

The `\n` character creates a new line.

### Writing Multiple Lines Using writelines()

```python
file = open("student.txt", "w")

lines = [
    "Python\n",
    "Java\n",
    "JavaScript\n",
    "C++\n"
]

file.writelines(lines)

file.close()
```

**Important:** `writelines()` does not automatically add newline characters. Add `\n` yourself when required.

---

## 5. Closing a File

After opening a file, we should close it when we finish working with it.

```python
file = open("student.txt", "w")

file.write("Hello World")

file.close()
```

Why close a file?

- Releases system resources.
- Helps ensure buffered data is flushed.
- Prevents unnecessary open file handles.

A common problem is forgetting to close a file.

Python provides a better solution called the `with` statement.

---

## 6. Using the with Statement

The `with` statement is the recommended way to work with files.

It automatically closes the file when the block finishes, including when an exception occurs.

### Syntax

```python
with open("filename", "mode") as file:

    # File operations
    pass
```

### Example

```python
with open("student.txt", "w") as file:

    file.write("Welcome to Python")
    file.write("\nLearning File Handling")

print("File operation completed")
```

Output:

```text
File operation completed
```

We do not need to call `file.close()` manually.

**Best Practice:** Prefer `with open()` for normal file operations.

---

## 7. Reading a File

Python provides several methods to read file contents.

Before reading, create a file named `student.txt` with the following content:

```text
Name: Raj
Course: Python
Marks: 90
```

### 7.1 read()

`read()` reads the entire file content as a string by default.

```python
with open("student.txt", "r") as file:

    content = file.read()

    print(content)
```

Output:

```text
Name: Raj
Course: Python
Marks: 90
```

We can also specify the number of characters:

```python
with open("student.txt", "r") as file:

    content = file.read(10)

    print(content)
```

Output:

```text
Name: Raj
C
```

### 7.2 readline()

`readline()` reads one line at a time.

```python
with open("student.txt", "r") as file:

    first_line = file.readline()

    print(first_line)
```

Output:

```text
Name: Raj
```

Read multiple lines:

```python
with open("student.txt", "r") as file:

    line1 = file.readline()
    line2 = file.readline()

    print(line1, end="")
    print(line2, end="")
```

Output:

```text
Name: Raj
Course: Python
```

### 7.3 readlines()

`readlines()` reads all lines and returns them as a list of strings.

```python
with open("student.txt", "r") as file:

    lines = file.readlines()

    print(lines)
```

Output:

```text
['Name: Raj\n', 'Course: Python\n', 'Marks: 90']
```

### Comparison

| Method | Description | Return Type |
|---|---|---|
| `read()` | Reads the entire content or specified number of characters | String |
| `readline()` | Reads one line | String |
| `readlines()` | Reads all lines into a list | List |

---

## 8. Reading a File Using a Loop

We can directly iterate over a file object.

This is useful when processing large text files because it avoids loading the entire file into memory at once.

```python
with open("student.txt", "r") as file:

    for line in file:

        print(line, end="")
```

Output:

```text
Name: Raj
Course: Python
Marks: 90
```

### Removing Extra Newline Characters

Sometimes printed lines contain unwanted blank lines.

We can use `strip()`:

```python
with open("student.txt", "r") as file:

    for line in file:

        print(line.strip())
```

---

## 9. Appending Data to a File

Append mode (`a`) adds new content at the end of an existing file.

It does not delete existing content.

```python
with open("student.txt", "a") as file:

    file.write("\nCity: Mumbai")
    file.write("\nAge: 21")
```

Updated file:

```text
Name: Raj
Course: Python
Marks: 90
City: Mumbai
Age: 21
```

### Practical Example – Save Multiple Messages

```python
while True:

    message = input("Enter message: ")

    if message.lower() == "exit":
        break

    with open("messages.txt", "a") as file:

        file.write(message + "\n")

print("Messages saved successfully")
```

Every message is added to the file.

---

## 10. Understanding File Pointer

When a file is opened, Python maintains a position called the file pointer.

It indicates where the next read or write operation will happen.

### 10.1 tell()

`tell()` returns the current file pointer position.

```python
with open("student.txt", "r") as file:

    print(file.tell())

    file.read(5)

    print(file.tell())
```

Example Output:

```text
0
5
```

### 10.2 seek()

`seek()` moves the file pointer to a specified position.

```python
with open("student.txt", "r") as file:

    print(file.read(5))

    file.seek(0)

    print(file.read(5))
```

Output:

```text
Name:
Name:
```

### Understanding seek()

```python
file.seek(offset, whence)
```

Common `whence` values:

| Value | Meaning |
|---|---|
| `0` | Beginning of file |
| `1` | Current position |
| `2` | End of file |

For text files, seeking to the beginning with `seek(0)` is straightforward. Arbitrary byte offsets are generally intended for binary files.

---

## 11. Writing and Reading Using r+ Mode

`r+` allows reading and writing an existing file.

The file must already exist.

```python
with open("student.txt", "r+") as file:

    content = file.read()

    print("Existing Content:")
    print(content)

    file.seek(0)

    file.write("Updated Student Information")
```

**Important:** `r+` does not automatically truncate the file. If the new text is shorter, old characters can remain at the end.

To replace the entire file content, use `w` or explicitly truncate it when appropriate.

---

## 12. Understanding w+ and a+ Modes

### 12.1 w+ Mode

Allows reading and writing, but truncates existing content when the file is opened.

```python
with open("data.txt", "w+") as file:

    file.write("Hello Python")

    file.seek(0)

    print(file.read())
```

Output:

```text
Hello Python
```

### 12.2 a+ Mode

Allows reading and appending.

The file pointer initially starts at the end for writing.

```python
with open("data.txt", "a+") as file:

    file.write("\nNew Line")

    file.seek(0)

    print(file.read())
```

Output:

```text
Hello Python
New Line
```

We used `seek(0)` because the pointer is positioned at the end after opening in append mode and writing.

---

## 13. Creating a File Using x Mode

`x` mode creates a new file only if it does not already exist.

```python
try:

    with open("new_file.txt", "x") as file:

        file.write("New file created")

    print("File created successfully")

except FileExistsError:

    print("File already exists")
```

This prevents accidentally overwriting an existing file.

---

## 14. Working with File Paths

A file can be opened using:

- File name
- Relative path
- Absolute path

### 14.1 Relative Path

A relative path is interpreted from the current working directory.

```python
with open("student.txt", "r") as file:

    print(file.read())
```

### 14.2 Absolute Path

An absolute path specifies the full file location.

Windows example:

```python
with open("C:/Users/Student/Desktop/student.txt", "r") as file:

    print(file.read())
```

Another Windows example using a raw string:

```python
file_path = r"C:\Users\Student\Desktop\student.txt"

with open(file_path, "r") as file:

    print(file.read())
```

Raw strings are useful for Windows paths because backslashes can otherwise be interpreted as escape characters.

### 14.3 Using pathlib

```python
from pathlib import Path

file_path = Path("data") / "student.txt"

with open(file_path, "r") as file:

    print(file.read())
```

---

## 15. Checking Whether a File Exists

We can use `os.path.exists()` or `Path.exists()`.

### Using os

```python
import os

if os.path.exists("student.txt"):

    print("File exists")

else:

    print("File does not exist")
```

### Using pathlib

```python
from pathlib import Path

file_path = Path("student.txt")

if file_path.exists():

    print("Path exists")

else:

    print("Path does not exist")
```

For checking specifically whether it is a file:

```python
if file_path.is_file():
    print("This is a file")
```

---

## 16. Deleting a File

We can delete a file using `os.remove()` or `Path.unlink()`.

### Using os

```python
import os

if os.path.exists("student.txt"):

    os.remove("student.txt")

    print("File deleted")

else:

    print("File not found")
```

### Using pathlib

```python
from pathlib import Path

file_path = Path("student.txt")

if file_path.is_file():

    file_path.unlink()

    print("File deleted")
```

**Warning:** File deletion is permanent in normal use. Always verify the file path before deleting anything.

---

## 17. File Information

Python can provide information about files.

### Using os.path

```python
import os

file_path = "student.txt"

if os.path.isfile(file_path):

    print("File Size:", os.path.getsize(file_path), "bytes")
    print("Absolute Path:", os.path.abspath(file_path))
    print("File Name:", os.path.basename(file_path))
    print("Directory:", os.path.dirname(os.path.abspath(file_path)))
```

### Using pathlib

```python
from pathlib import Path

file_path = Path("student.txt")

if file_path.exists():

    print("Name:", file_path.name)
    print("Suffix:", file_path.suffix)
    print("Size:", file_path.stat().st_size)
    print("Absolute Path:", file_path.resolve())
```

---

## 18. Working with Binary Files

Text files store readable characters.

Binary files store data as bytes.

Examples:

- Images
- Audio
- Video
- PDFs
- Executable files

Binary modes include:

- `rb`: Read binary data.
- `wb`: Write binary data.
- `ab`: Append binary data.

### Example – Copy an Image

```python
with open("source.jpg", "rb") as source:

    data = source.read()

with open("copy.jpg", "wb") as destination:

    destination.write(data)

print("Image copied successfully")
```

The file is copied as bytes instead of text.

### Better Approach – Copy Using shutil

```python
import shutil

shutil.copy2("source.jpg", "copy.jpg")

print("File copied successfully")
```

For ordinary file copying, `shutil` is generally more convenient.

---

## 19. Encoding and Decoding

Text files contain bytes, but Python works with strings.

Encoding converts text into bytes.

Decoding converts bytes back into text.

### Encoding

```python
text = "Hello Python"

encoded_data = text.encode("utf-8")

print(encoded_data)
```

Output:

```text
b'Hello Python'
```

### Decoding

```python
decoded_text = encoded_data.decode("utf-8")

print(decoded_text)
```

Output:

```text
Hello Python
```

### Specifying Encoding While Opening a File

```python
with open("student.txt", "w", encoding="utf-8") as file:

    file.write("Python सीखना आसान है")
```

Reading:

```python
with open("student.txt", "r", encoding="utf-8") as file:

    print(file.read())
```

**Best Practice:** Explicitly use `encoding="utf-8"` when working with text files, especially when they may contain non-English characters.

---

## 20. Handling Large Files

Reading an entire file using `read()` can consume significant memory if the file is very large.

Instead, process it line by line.

```python
with open("large_file.txt", "r", encoding="utf-8") as file:

    for line in file:

        process_line = line.strip()

        if process_line:
            print(process_line)
```

This avoids loading all lines into memory at once.

### Reading in Chunks

We can also read a fixed number of characters at a time.

```python
with open("large_file.txt", "r", encoding="utf-8") as file:

    while True:

        chunk = file.read(100)

        if not chunk:
            break

        print(chunk)
```

This reads up to 100 characters per iteration.

---

## 21. Common File Handling Errors

### 21.1 FileNotFoundError

Occurs when a file does not exist at the specified path.

```python
try:

    with open("unknown.txt", "r") as file:

        print(file.read())

except FileNotFoundError:

    print("File not found")
```

### 21.2 PermissionError

Occurs when the program does not have the required permission to access a file.

```python
try:

    with open("protected.txt", "w") as file:

        file.write("Hello")

except PermissionError:

    print("Permission denied")
```

### 21.3 IsADirectoryError

Occurs when we try to open a directory as if it were a regular file.

```python
try:

    with open("Reports", "r") as file:

        print(file.read())

except IsADirectoryError:

    print("The specified path is a directory")
```

### 21.4 UnicodeDecodeError

Can occur when Python tries to decode file bytes using an incompatible text encoding.

```python
try:

    with open("data.txt", "r", encoding="utf-8") as file:

        print(file.read())

except UnicodeDecodeError:

    print("Unable to decode file using UTF-8")
```

Use the correct encoding for the file. Do not silently ignore decoding errors unless losing characters is acceptable.

### 21.5 ValueError – Operation on a Closed File

```python
file = open("student.txt", "r")

file.close()

try:

    file.read()

except ValueError:

    print("File is already closed")
```

### 21.6 Common File Handling Mistakes

| Mistake | Problem | Solution |
|---|---|---|
| Forgetting to close a file | Resources remain occupied | Use `with` |
| Using `w` instead of `a` | Existing content is deleted | Select the correct mode |
| Incorrect file path | File cannot be found | Verify the path |
| Wrong encoding | Text may not decode | Use the correct encoding |
| Reading huge files at once | High memory usage | Process line by line |
| Using text mode for images | Data may become corrupted | Use binary mode |

---

## 22. Practical Program – Notes Application

Create a small application that saves and displays notes.

```python
def add_note():

    note = input("Enter your note: ")

    with open("notes.txt", "a", encoding="utf-8") as file:

        file.write(note + "\n")

    print("Note saved successfully")


def view_notes():

    try:

        with open("notes.txt", "r", encoding="utf-8") as file:

            content = file.read()

            if content.strip():
                print("\nYOUR NOTES")
                print(content)

            else:
                print("No notes available")

    except FileNotFoundError:

        print("No notes file found")


def main():

    while True:

        print("\n===== NOTES APPLICATION =====")
        print("1. Add Note")
        print("2. View Notes")
        print("3. Exit")

        choice = input("Enter choice: ")

        if choice == "1":

            add_note()

        elif choice == "2":

            view_notes()

        elif choice == "3":

            print("Application closed")
            break

        else:

            print("Invalid choice")


if __name__ == "__main__":
    main()
```

### Run

```bash
python notes.py
```

### Sample Output

```text
===== NOTES APPLICATION =====
1. Add Note
2. View Notes
3. Exit

Enter choice: 1
Enter your note: Learn Python file handling
Note saved successfully
```

After adding multiple notes, select View Notes.

```text
YOUR NOTES
Learn Python file handling
Practice file operations
Complete Day 25
```

---

## 23. Mini Project – File-Based Student Record Management System

Build a student management application that stores student records in a text file.

Unlike previous projects that stored records only in dictionaries, this project will preserve records after the program closes.

### Project Structure

```text
StudentRecordSystem/
│
├── main.py
│
└── data/
    └── students.txt
```

The `data` folder and `students.txt` file will be created automatically.

### File: main.py

```python
from pathlib import Path

DATA_FOLDER = Path("data")
FILE_PATH = DATA_FOLDER / "students.txt"


def initialize_file():

    DATA_FOLDER.mkdir(exist_ok=True)

    FILE_PATH.touch(exist_ok=True)


def add_student():

    student_id = input("Enter Student ID: ").strip()
    name = input("Enter Student Name: ").strip()

    if not student_id or not name:
        print("Student ID and name cannot be empty")
        return

    try:
        marks = float(input("Enter Marks: "))

    except ValueError:
        print("Marks must be numeric")
        return

    if not 0 <= marks <= 100:
        print("Marks must be between 0 and 100")
        return

    students = get_students()

    if any(student["id"] == student_id for student in students):
        print("Student ID already exists")
        return

    with open(FILE_PATH, "a", encoding="utf-8") as file:

        file.write(f"{student_id}|{name}|{marks}\n")

    print("Student added successfully")


def get_students():

    students = []

    with open(FILE_PATH, "r", encoding="utf-8") as file:

        for line in file:

            line = line.strip()

            if not line:
                continue

            parts = line.split("|")

            if len(parts) != 3:
                continue

            student_id, name, marks = parts

            try:
                marks = float(marks)

            except ValueError:
                continue

            students.append({
                "id": student_id,
                "name": name,
                "marks": marks
            })

    return students


def view_students():

    students = get_students()

    if not students:
        print("No student records found")
        return

    print("\n===== STUDENT RECORDS =====")

    for student in students:

        print("\nStudent ID:", student["id"])
        print("Name:", student["name"])
        print("Marks:", student["marks"])


def search_student():

    student_id = input("Enter Student ID: ").strip()

    students = get_students()

    for student in students:

        if student["id"] == student_id:

            print("\nStudent Found")
            print("ID:", student["id"])
            print("Name:", student["name"])
            print("Marks:", student["marks"])

            return

    print("Student not found")


def update_student():

    student_id = input("Enter Student ID: ").strip()

    students = get_students()

    for student in students:

        if student["id"] == student_id:

            name = input("Enter New Name: ").strip()

            if not name:
                print("Name cannot be empty")
                return

            try:
                marks = float(input("Enter New Marks: "))

            except ValueError:
                print("Marks must be numeric")
                return

            if not 0 <= marks <= 100:
                print("Marks must be between 0 and 100")
                return

            student["name"] = name
            student["marks"] = marks

            save_students(students)

            print("Student updated successfully")

            return

    print("Student not found")


def delete_student():

    student_id = input("Enter Student ID: ").strip()

    students = get_students()

    updated_students = [
        student for student in students
        if student["id"] != student_id
    ]

    if len(updated_students) == len(students):

        print("Student not found")
        return

    save_students(updated_students)

    print("Student deleted successfully")


def save_students(students):

    with open(FILE_PATH, "w", encoding="utf-8") as file:

        for student in students:

            file.write(
                f"{student['id']}|"
                f"{student['name']}|"
                f"{student['marks']}\n"
            )


def show_statistics():

    students = get_students()

    if not students:
        print("No records available")
        return

    marks = [student["marks"] for student in students]

    average = sum(marks) / len(marks)

    topper = max(students, key=lambda student: student["marks"])

    print("\n===== STUDENT STATISTICS =====")
    print("Total Students:", len(students))
    print("Average Marks:", round(average, 2))
    print("Topper:", topper["name"])
    print("Topper Marks:", topper["marks"])


def main():

    initialize_file()

    while True:

        print("\n===== STUDENT RECORD MANAGEMENT =====")

        print("1. Add Student")
        print("2. View Students")
        print("3. Search Student")
        print("4. Update Student")
        print("5. Delete Student")
        print("6. Show Statistics")
        print("7. Exit")

        choice = input("Enter choice: ")

        if choice == "1":
            add_student()

        elif choice == "2":
            view_students()

        elif choice == "3":
            search_student()

        elif choice == "4":
            update_student()

        elif choice == "5":
            delete_student()

        elif choice == "6":
            show_statistics()

        elif choice == "7":
            print("Application closed")
            break

        else:
            print("Invalid choice")


if __name__ == "__main__":
    main()
```

### Run the Project

Open the terminal inside `StudentRecordSystem`.

```bash
python main.py
```

### Sample Output

```text
===== STUDENT RECORD MANAGEMENT =====

1. Add Student
2. View Students
3. Search Student
4. Update Student
5. Delete Student
6. Show Statistics
7. Exit

Enter choice: 1

Enter Student ID: 101
Enter Student Name: Raj
Enter Marks: 90

Student added successfully
```

### Stored File Content

The program creates:

`data/students.txt`

Example content:

```text
101|Raj|90.0
102|Aman|85.0
103|Rohit|95.0
```

### Important Project Notes

- Student records are stored in a text file.
- Data remains available after restarting the application.
- The program supports Add, View, Search, Update and Delete.
- Update and Delete operations rewrite the file.
- This is a beginner-level storage format, not a production database.
- The `|` character is used as a delimiter. Names containing this character would require additional validation or a proper serialization format.

---

## 24. Student Practice Exercises

Complete these exercises independently.

### Exercise 1 – File Creation

Create a file named `welcome.txt`.

Write:

- Your name.
- Your course.
- Your city.
- Your favourite programming language.

### Exercise 2 – File Reading

Read `welcome.txt` using:

- `read()`
- `readline()`
- `readlines()`

Observe the difference.

### Exercise 3 – Append Data

Create a program that accepts multiple tasks from the user and stores them in `tasks.txt`.

Stop when the user enters `exit`.

### Exercise 4 – Word Counter

Read a text file and calculate:

- Total characters.
- Total words.
- Total lines.
- Number of vowels.

### Exercise 5 – File Search

Ask the user for a word and search for it inside a text file.

Display whether the word exists.

### Exercise 6 – File Copy

Copy the contents of one text file into another file.

Try both:

- Manual copying using file operations.
- Copying using `shutil`.

### Exercise 7 – Log File

Create a simple application that stores login activity in `login.log`.

Each entry should contain:

- Username.
- Activity.
- Date and time.

Use `datetime` and append mode.

### Exercise 8 – File Statistics

Create a program that displays:

- File name.
- File extension.
- File size.
- Absolute path.
- Total lines.

### Exercise 9 – Backup Application

Create a program that copies an important text file into a backup folder.

Do not overwrite an existing backup without checking first.

### Exercise 10 – Student Record System

Extend the mini-project by adding:

- Search by student name.
- Pass/fail report.
- Highest marks.
- Lowest marks.
- Total number of passed students.

---

## 25. Trainer Assessment

| Assessment Area | Verification |
|---|---|
| File creation | Student creates files using Python |
| File modes | Student understands `r`, `w`, `a`, `x` |
| Reading | Student uses `read`, `readline`, `readlines` |
| Writing | Student writes single and multiple lines |
| Appending | Student preserves existing content |
| Context manager | Student uses `with` correctly |
| File pointer | Student understands `seek` and `tell` |
| File paths | Student works with relative and absolute paths |
| File deletion | Student safely removes files |
| Binary files | Student understands binary mode |
| Encoding | Student uses UTF-8 |
| Error handling | Student handles common file errors |
| Mini project | Student builds a persistent file-based application |

## 26. Completion Criteria

Mark Day 25 as complete when the student can:

- Explain file handling and its importance.
- Create and open files using `open()`.
- Understand common file modes.
- Read files using different methods.
- Write and append data.
- Use the `with` statement.
- Understand file pointers and their operations.
- Work with relative and absolute paths.
- Check, rename and delete files.
- Understand text and binary modes.
- Use UTF-8 encoding.
- Handle common file-related exceptions.
- Build an application that stores data permanently in files.

**Day 25 Completed – Python File Handling**

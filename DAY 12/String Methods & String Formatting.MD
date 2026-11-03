
# Day 12 – Python String Methods & String Formatting

## 1. Introduction to String Methods

Python provides several built-in string methods that help us manipulate, search, validate and format text.

A string method is a function that is called using a string object.

### Syntax

```python
string.method()
```

### Example

```python
name = "raj"

print(name.upper())
```

Output:

```text
RAJ
```

**Important:** Strings are immutable. String methods return a new string instead of modifying the original string.

```python
name = "raj"

result = name.upper()

print("Original:", name)
print("Result:", result)
```

Output:

```text
Original: raj
Result: RAJ
```

---

## 2. Changing Letter Case

Python provides several methods for changing the case of characters.

### A. upper()

Converts all characters into uppercase.

```python
text = "hello python"

print(text.upper())
```

Output:

```text
HELLO PYTHON
```

### B. lower()

Converts all characters into lowercase.

```python
text = "HELLO PYTHON"

print(text.lower())
```

Output:

```text
hello python
```

### C. capitalize()

Converts the first character to uppercase and the remaining characters to lowercase.

```python
text = "hello PYTHON"

print(text.capitalize())
```

Output:

```text
Hello python
```

### D. title()

Converts the first character of each word to uppercase.

```python
text = "python programming language"

print(text.title())
```

Output:

```text
Python Programming Language
```

### E. swapcase()

Converts uppercase characters to lowercase and lowercase characters to uppercase.

```python
text = "Hello PYTHON"

print(text.swapcase())
```

Output:

```text
hELLO python
```

---

## 3. Removing Unwanted Characters

Python provides methods to remove whitespace or specified characters from strings.

### A. strip()

Removes whitespace from both ends of a string.

```python
text = "   Hello Python   "

print(text.strip())
```

Output:

```text
Hello Python
```

### B. lstrip()

Removes whitespace from the left side.

```python
text = "   Hello Python"

print(text.lstrip())
```

Output:

```text
Hello Python
```

### C. rstrip()

Removes whitespace from the right side.

```python
text = "Hello Python   "

print(text.rstrip())
```

Output:

```text
Hello Python
```

### D. Removing Specific Characters

```python
text = "###Python###"

print(text.strip("#"))
```

Output:

```text
Python
```

**Important:** `strip()` removes matching characters from the beginning and end. It does not remove every occurrence from the middle of a string.

---

## 4. Searching Inside Strings

Python provides methods to search for characters and substrings.

### A. find()

Returns the first index where the substring is found.

Returns `-1` if the substring does not exist.

```python
text = "Python Programming"

print(text.find("Python"))
print(text.find("Programming"))
print(text.find("Java"))
```

Output:

```text
0
7
-1
```

### B. rfind()

Returns the highest index where the substring is found.

```python
text = "Python is easy. Python is powerful."

print(text.rfind("Python"))
```

Output:

```text
16
```

### C. index()

Works like `find()`, but raises a `ValueError` if the substring is not found.

```python
text = "Python Programming"

print(text.index("Python"))
```

Output:

```text
0
```

### D. count()

Returns the number of occurrences of a substring.

```python
text = "Python is easy. Python is powerful."

print(text.count("Python"))
```

Output:

```text
2
```

### Difference Between find() and index()

| find() | index() |
|---|---|
| Returns the matching index | Returns the matching index |
| Returns `-1` if not found | Raises `ValueError` if not found |
| Useful for safe searching | Useful when a match is expected |

---

## 5. Replacing Text

The `replace()` method replaces occurrences of one substring with another.

### Syntax

```python
string.replace(old, new, count)
```

- `old`: Text to replace.
- `new`: Replacement text.
- `count`: Optional maximum number of replacements.

### Example 1

```python
text = "I like Java"

result = text.replace("Java", "Python")

print(result)
```

Output:

```text
I like Python
```

### Example 2: Replace Multiple Occurrences

```python
text = "apple apple apple"

print(text.replace("apple", "mango"))
```

Output:

```text
mango mango mango
```

### Example 3: Limit Replacements

```python
text = "apple apple apple"

print(text.replace("apple", "mango", 2))
```

Output:

```text
mango mango apple
```

---

## 6. Splitting Strings

The `split()` method divides a string into a list of smaller strings.

### Syntax

```python
string.split(separator, maxsplit)
```

### Example 1: Split by Spaces

```python
text = "Python is easy to learn"

words = text.split()

print(words)
```

Output:

```text
['Python', 'is', 'easy', 'to', 'learn']
```

### Example 2: Split by Comma

```python
data = "Raj,Developer,Python"

result = data.split(",")

print(result)
```

Output:

```text
['Raj', 'Developer', 'Python']
```

### Example 3: Limit Splitting

```python
text = "Python is easy to learn"

print(text.split(" ", 2))
```

Output:

```text
['Python', 'is', 'easy to learn']
```

---

## 7. Joining Strings

The `join()` method combines elements of an iterable into a single string.

### Syntax

```python
separator.join(iterable)
```

### Example 1

```python
words = ["Python", "is", "easy"]

result = " ".join(words)

print(result)
```

Output:

```text
Python is easy
```

### Example 2: Join Using Hyphen

```python
words = ["2026", "11", "03"]

result = "-".join(words)

print(result)
```

Output:

```text
2026-11-03
```

### Example 3: Join Using Comma

```python
names = ["Raj", "Amit", "Neha"]

result = ", ".join(names)

print(result)
```

Output:

```text
Raj, Amit, Neha
```

**Important:** `join()` expects string elements. Non-string elements must be converted before joining.

---

## 8. String Validation Methods

Python provides methods to check the type of characters inside a string.

These methods return Boolean values: `True` or `False`.

### A. isalpha()

Returns True if all characters are alphabetic and the string is not empty.

```python
text = "Python"

print(text.isalpha())
```

Output:

```text
True
```

### B. isdigit()

Returns True if all characters are digits.

```python
text = "12345"

print(text.isdigit())
```

Output:

```text
True
```

### C. isalnum()

Returns True if all characters are alphabetic or numeric and the string is not empty.

```python
text = "Python123"

print(text.isalnum())
```

Output:

```text
True
```

### D. isspace()

Returns True if all characters are whitespace and the string is not empty.

```python
text = "   "

print(text.isspace())
```

Output:

```text
True
```

### E. islower()

Checks whether all cased characters are lowercase.

```python
text = "python"

print(text.islower())
```

Output:

```text
True
```

### F. isupper()

Checks whether all cased characters are uppercase.

```python
text = "PYTHON"

print(text.isupper())
```

Output:

```text
True
```

### G. istitle()

Checks whether the string follows title-case formatting.

```python
text = "Python Programming"

print(text.istitle())
```

Output:

```text
True
```

### H. startswith()

Checks whether a string starts with a specified prefix.

```python
text = "Python Programming"

print(text.startswith("Python"))
```

Output:

```text
True
```

### I. endswith()

Checks whether a string ends with a specified suffix.

```python
text = "report.pdf"

print(text.endswith(".pdf"))
```

Output:

```text
True
```

### Comparison Table

| Method | Purpose |
|---|---|
| `isalpha()` | Checks alphabetic characters |
| `isdigit()` | Checks digit characters |
| `isalnum()` | Checks letters and digits |
| `isspace()` | Checks whitespace |
| `islower()` | Checks lowercase |
| `isupper()` | Checks uppercase |
| `istitle()` | Checks title case |
| `startswith()` | Checks beginning of string |
| `endswith()` | Checks ending of string |

**Note:** `isdigit()` checks digit characters, not whether a string is a valid Python integer literal. For example, some Unicode digit characters are accepted by `isdigit()` but may not work with `int()`.

---

## 9. String Formatting

String formatting allows us to insert variables and values into strings.

Python supports multiple formatting techniques.

### A. String Concatenation

```python
name = "Raj"
age = 22

message = "My name is " + name + " and my age is " + str(age)

print(message)
```

Output:

```text
My name is Raj and my age is 22
```

The `str()` function is required here because we cannot directly concatenate a string and an integer.

### B. Using % Formatting

This is an older string-formatting technique.

```python
name = "Raj"
age = 22

print("My name is %s and I am %d years old." % (name, age))
```

Output:

```text
My name is Raj and I am 22 years old.
```

Common format specifiers:

| Specifier | Meaning |
|---|---|
| `%s` | String |
| `%d` | Integer |
| `%f` | Floating-point number |
| `%.2f` | Float with 2 decimal places |

### C. Using str.format()

The `format()` method inserts values into placeholders.

```python
name = "Raj"
age = 22

message = "My name is {} and I am {} years old."

print(message.format(name, age))
```

Output:

```text
My name is Raj and I am 22 years old.
```

### Using Positional Arguments

```python
print("{0} is learning {1}".format("Raj", "Python"))
```

Output:

```text
Raj is learning Python
```

### Using Named Placeholders

```python
message = "Name: {name}, Age: {age}"

print(message.format(name="Raj", age=22))
```

Output:

```text
Name: Raj, Age: 22
```

### D. f-Strings

f-strings are a modern and readable way to format strings.

They allow variables and expressions to be written directly inside curly braces.

```python
name = "Raj"
age = 22

print(f"My name is {name} and I am {age} years old.")
```

Output:

```text
My name is Raj and I am 22 years old.
```

### Using Expressions in f-Strings

```python
a = 10
b = 20

print(f"Sum: {a + b}")
```

Output:

```text
Sum: 30
```

### Formatting Decimal Places

```python
price = 125.6789

print(f"Price: {price:.2f}")
```

Output:

```text
Price: 125.68
```

### Formatting with Commas

```python
amount = 1500000

print(f"Amount: {amount:,}")
```

Output:

```text
Amount: 1,500,000
```

### Percentage Formatting

```python
percentage = 0.8567

print(f"Percentage: {percentage:.2%}")
```

Output:

```text
Percentage: 85.67%
```

**Recommendation:** Prefer f-strings for most new Python code because they are readable and convenient.

---

## 10. String Alignment and Padding

Python provides methods to align and pad strings.

### A. center()

Centers a string within a specified width.

```python
text = "Python"

print(text.center(20, "-"))
```

Output:

```text
-------Python-------
```

### B. ljust()

Aligns a string to the left.

```python
text = "Python"

print(text.ljust(15, "-"))
```

Output:

```text
Python---------
```

### C. rjust()

Aligns a string to the right.

```python
text = "Python"

print(text.rjust(15, "-"))
```

Output:

```text
---------Python
```

### D. zfill()

Pads a string with zeros on the left until it reaches the specified width.

```python
number = "25"

print(number.zfill(5))
```

Output:

```text
00025
```

---

## 11. Partitioning Strings

The `partition()` method divides a string into three parts:

1. Text before the separator.
2. The separator itself.
3. Text after the separator.

### Example

```python
email = "raj@gmail.com"

result = email.partition("@")

print(result)
```

Output:

```text
('raj', '@', 'gmail.com')
```

### Using rpartition()

`rpartition()` searches for the last occurrence of the separator.

```python
text = "one-two-three"

print(text.rpartition("-"))
```

Output:

```text
('one-two', '-', 'three')
```

---

## 12. Practical Programs

### Program 1: Clean User Input

```python
name = input("Enter your name: ")

name = name.strip().title()

print("Welcome,", name)
```

Example:

```text
Enter your name:    raj gupta
Welcome, Raj Gupta
```

### Program 2: Email Validation – Basic

```python
email = input("Enter your email: ").strip()

if email.count("@") == 1 and email.endswith(".com"):
    print("Basic email format accepted")
else:
    print("Invalid email format")
```

**Note:** This is only a basic exercise. It is not a complete email validation system.

### Program 3: Count Word Frequency

```python
text = input("Enter a sentence: ").lower()

words = text.split()

word = input("Enter word to search: ").lower()

count = words.count(word)

print("Word frequency:", count)
```

### Program 4: Remove Extra Spaces

```python
text = input("Enter a sentence: ")

words = text.split()

cleaned_text = " ".join(words)

print("Cleaned text:", cleaned_text)
```

Example:

```text
Enter a sentence: Python    is     very    easy

Cleaned text: Python is very easy
```

### Program 5: Replace a Word

```python
text = input("Enter a sentence: ")

old_word = input("Word to replace: ")
new_word = input("New word: ")

result = text.replace(old_word, new_word)

print("Updated sentence:", result)
```

### Program 6: Check File Extension

```python
filename = input("Enter filename: ").strip()

if filename.lower().endswith(".pdf"):
    print("PDF file")
elif filename.lower().endswith(".jpg"):
    print("JPG image")
elif filename.lower().endswith(".png"):
    print("PNG image")
else:
    print("Unknown file type")
```

### Program 7: Format Student Details

```python
name = input("Enter student name: ")
roll_number = int(input("Enter roll number: "))
marks = float(input("Enter marks: "))

print("\n===== STUDENT DETAILS =====")
print(f"Name        : {name.title()}")
print(f"Roll Number : {roll_number:04d}")
print(f"Marks       : {marks:.2f}")
```

Example:

```text
Enter student name: raj
Enter roll number: 7
Enter marks: 87.567

===== STUDENT DETAILS =====
Name        : Raj
Roll Number : 0007
Marks       : 87.57
```

---

## 13. Student Practice Exercises

Solve these programs independently.

1. Convert a sentence into uppercase and lowercase.
2. Convert a name into title case.
3. Remove leading and trailing spaces from user input.
4. Count how many times a word occurs in a sentence.
5. Find the position of a word using `find()`.
6. Replace a particular word in a sentence.
7. Split a sentence into individual words.
8. Join a list of names using commas.
9. Check whether a string contains only alphabetic characters.
10. Check whether a string contains only digits.
11. Validate whether a filename ends with `.pdf`.
12. Count uppercase and lowercase characters using string methods.
13. Format student details using f-strings.
14. Display a price with two decimal places.
15. Remove extra spaces between words.
16. Extract the username and domain from an email using `partition()`.
17. Create a formatted invoice using f-strings.
18. Format a number with commas as thousands separators.

---

## 14. Mini Project – Student Data Formatter

Create a Python program that accepts student information and generates a clean formatted report.

### Requirements

Ask the user for:

- Student name
- Email address
- Roll number
- Course name
- Marks in three subjects

### Program Behaviour

1. Remove unnecessary spaces from the name and email.
2. Format the student name using `title()`.
3. Convert the email address to lowercase.
4. Check that the email contains exactly one `@` symbol.
5. Calculate total marks.
6. Calculate percentage assuming each subject is out of 100.
7. Display all information using f-strings.
8. Format marks and percentage to two decimal places.
9. Display a clear report heading.

### Expected Output

```text
===== STUDENT REPORT =====

Student Name : Raj Gupta
Email        : raj@gmail.com
Roll Number  : 0007
Course       : Python Development

Subject 1    : 85.00
Subject 2    : 90.00
Subject 3    : 88.00

Total Marks  : 263.00 / 300
Percentage   : 87.67%
```

### Rules

- Use string methods for cleaning and formatting.
- Use `float()` for marks.
- Use f-strings for report generation.
- Use conditional statements for basic email validation.
- Do not use external libraries.

### Challenge

Extend the project to:

- Accept multiple students.
- Generate a separate report for each student.
- Display the highest percentage.
- Display student names in alphabetical order.

---

## 15. Common Mistakes to Avoid

1. Forgetting that string methods return new strings.
2. Using `find()` and `index()` interchangeably without understanding their differences.
3. Forgetting that `split()` returns a list.
4. Using `join()` with non-string elements.
5. Confusing `strip()` with `replace()`.
6. Assuming `strip()` removes characters from the middle.
7. Forgetting that string comparisons are case-sensitive.
8. Using incorrect placeholders in `str.format()`.
9. Forgetting the `f` prefix in f-strings.
10. Using `%d` for floating-point values without understanding conversion.
11. Assuming basic email checks guarantee a valid email address.

---

## 16. Trainer Assessment

Ask the student:

1. What is a string method?
2. What is the difference between `upper()` and `lower()`?
3. What does `capitalize()` do?
4. What is the difference between `strip()`, `lstrip()` and `rstrip()`?
5. What is the difference between `find()` and `index()`?
6. What does `count()` return?
7. What is the difference between `split()` and `join()`?
8. What is the purpose of `isalpha()` and `isdigit()`?
9. What is the difference between `%` formatting and f-strings?
10. What does `{price:.2f}` mean?
11. What is the purpose of `startswith()` and `endswith()`?
12. What does `partition()` return?
13. Why should we prefer f-strings in modern Python?
14. Do string methods modify the original string?

### Practical Assessment

- Clean and format user input.
- Search and replace text.
- Split and join strings.
- Validate basic string content.
- Format numeric values using f-strings.
- Complete the Student Data Formatter independently.

### Completion Criteria

The student should be able to:

- Use common Python string methods.
- Search, replace, split and join strings.
- Validate string content.
- Format output using f-strings.
- Apply string alignment and padding.
- Clean user-provided text.
- Complete the Student Data Formatter independently.

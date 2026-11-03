
# Day 11 – Python Strings Fundamentals

## 1. Introduction to Strings

A string is a sequence of characters enclosed within quotation marks.

Strings are used to store text-based information such as:

- Names
- Email addresses
- Phone numbers
- Messages
- Addresses
- Passwords

Python supports three ways to define strings:

### A. Single Quotes

```python
name = 'Raj'
print(name)
```

Output:

```text
Raj
```

### B. Double Quotes

```python
name = "Raj"
print(name)
```

Output:

```text
Raj
```

### C. Triple Quotes

Triple quotes are commonly used for multiline strings.

```python
message = """Welcome to Python.
Python is easy to learn.
Let's start programming."""

print(message)
```

Output:

```text
Welcome to Python.
Python is easy to learn.
Let's start programming.
```

**Important:** Single and double quotes are interchangeable for ordinary strings. Choose the quotation style that makes your text easier to write and read.

---

## 2. String Variables

We can store strings inside variables.

```python
first_name = "Raj"
last_name = "Gupta"

print(first_name)
print(last_name)
```

Output:

```text
Raj
Gupta
```

### Combining String Variables

```python
first_name = "Raj"
last_name = "Gupta"

full_name = first_name + " " + last_name

print(full_name)
```

Output:

```text
Raj Gupta
```

The `+` operator joins strings together. This operation is called concatenation.

---

## 3. String Length – len()

The `len()` function returns the total number of characters in a string.

Spaces and special characters are also counted.

### Example

```python
message = "Hello Python"

print(len(message))
```

Output:

```text
12
```

### Another Example

```python
name = "Raj"

length = len(name)

print("Name:", name)
print("Length:", length)
```

Output:

```text
Name: Raj
Length: 3
```

---

## 4. String Indexing

Indexing allows us to access individual characters from a string.

Python uses zero-based indexing.

This means the first character has index `0`.

### Example

```python
language = "Python"

print(language[0])
print(language[1])
print(language[2])
print(language[3])
print(language[4])
print(language[5])
```

Output:

```text
P
y
t
h
o
n
```

### Understanding String Index Positions

For the string `"PYTHON"`:

| Character | P | Y | T | H | O | N |
|---|---|---|---|---|---|---|
| Positive Index | 0 | 1 | 2 | 3 | 4 | 5 |
| Negative Index | -6 | -5 | -4 | -3 | -2 | -1 |

### Negative Indexing

Negative indexing allows us to access characters from the end of a string.

```python
language = "Python"

print(language[-1])
print(language[-2])
print(language[-3])
```

Output:

```text
n
o
h
```

### Important

If we access an index that does not exist, Python raises an `IndexError`.

```python
language = "Python"

print(language[10])
```

Output:

```text
IndexError: string index out of range
```

---

## 5. String Slicing

Slicing allows us to extract a portion of a string.

### Syntax

```python
string[start:stop:step]
```

| Parameter | Meaning |
|---|---|
| start | Starting index (included) |
| stop | Ending index (excluded) |
| step | Interval between characters |

### Example 1: Basic Slicing

```python
language = "Python"

print(language[0:3])
print(language[2:5])
```

Output:

```text
Pyt
tho
```

### Example 2: Start Index Only

```python
language = "Python"

print(language[2:])
```

Output:

```text
thon
```

Python extracts characters from index 2 to the end.

### Example 3: Stop Index Only

```python
language = "Python"

print(language[:4])
```

Output:

```text
Pyth
```

Python starts from index 0 and stops before index 4.

### Example 4: Complete String

```python
language = "Python"

print(language[:])
```

Output:

```text
Python
```

### Example 5: Using Step

```python
number = "123456789"

print(number[::2])
```

Output:

```text
13579
```

### Example 6: Reverse a String

```python
language = "Python"

print(language[::-1])
```

Output:

```text
nohtyP
```

A step of `-1` reads the string backwards.

---

## 6. String Immutability

Strings in Python are immutable.

Immutable means that once a string is created, its individual characters cannot be changed directly.

### Incorrect Example

```python
name = "Python"

name[0] = "J"
```

Output:

```text
TypeError: 'str' object does not support item assignment
```

### Correct Approach

Create a new string instead.

```python
name = "Python"

new_name = "J" + name[1:]

print(new_name)
```

Output:

```text
Jython
```

The original string remains unchanged.

### Another Example

```python
name = "Raj"

name = "A" + name[1:]

print(name)
```

Output:

```text
Aaj
```

Here, Python creates a new string and assigns it to the variable `name`.

---

## 7. String Concatenation

Concatenation means joining two or more strings.

Python uses the `+` operator for concatenation.

### Example

```python
first_name = "Raj"
last_name = "Gupta"

full_name = first_name + " " + last_name

print(full_name)
```

Output:

```text
Raj Gupta
```

### Concatenating Multiple Strings

```python
a = "Python"
b = "Programming"
c = "Language"

result = a + " " + b + " " + c

print(result)
```

Output:

```text
Python Programming Language
```

---

## 8. String Repetition

The `*` operator repeats a string a specified number of times.

### Example

```python
word = "Python "

print(word * 3)
```

Output:

```text
Python Python Python
```

### Another Example

```python
symbol = "*"

print(symbol * 10)
```

Output:

```text
**********
```

---

## 9. Checking Character Membership

The `in` and `not in` operators check whether a character or substring exists inside a string.

### Example: in

```python
message = "Python Programming"

print("Python" in message)
print("Java" in message)
```

Output:

```text
True
False
```

### Example: not in

```python
message = "Python Programming"

print("Java" not in message)
print("Python" not in message)
```

Output:

```text
True
False
```

**Important:** String membership checks are case-sensitive.

```python
message = "Python"

print("python" in message)
```

Output:

```text
False
```

---

## 10. Traversing a String Using Loops

Traversing means accessing each character of a string one by one.

### Example 1: Using for Loop

```python
language = "Python"

for character in language:
    print(character)
```

Output:

```text
P
y
t
h
o
n
```

### Example 2: Using Indexing and for Loop

```python
language = "Python"

for i in range(len(language)):
    print(i, language[i])
```

Output:

```text
0 P
1 y
2 t
3 h
4 o
5 n
```

### Example 3: Using while Loop

```python
language = "Python"

i = 0

while i < len(language):
    print(language[i])
    i += 1
```

---

## 11. Useful Built-in Functions for Strings

Python provides several built-in functions that can work with strings.

### A. len()

Returns the number of characters.

```python
text = "Hello"

print(len(text))
```

Output:

```text
5
```

### B. max()

Returns the character with the highest Unicode code point.

```python
text = "Python"

print(max(text))
```

Output:

```text
y
```

### C. min()

Returns the character with the lowest Unicode code point.

```python
text = "Python"

print(min(text))
```

Output:

```text
P
```

### D. sorted()

Returns a sorted list of characters.

```python
text = "python"

print(sorted(text))
```

Output:

```text
['h', 'n', 'o', 'p', 't', 'y']
```

### E. ord()

Returns the Unicode code point of a character.

```python
print(ord("A"))
print(ord("a"))
```

Output:

```text
65
97
```

### F. chr()

Converts a Unicode code point into a character.

```python
print(chr(65))
print(chr(97))
```

Output:

```text
A
a
```

---

## 12. String Comparison

Python allows us to compare strings using comparison operators.

String comparison is case-sensitive and uses Unicode code point ordering.

### Example 1: Equality

```python
a = "Python"
b = "Python"

print(a == b)
```

Output:

```text
True
```

### Example 2: Inequality

```python
a = "Python"
b = "Java"

print(a != b)
```

Output:

```text
True
```

### Example 3: Case-Sensitive Comparison

```python
a = "python"
b = "Python"

print(a == b)
```

Output:

```text
False
```

### Example 4: Alphabetical Comparison

```python
print("Apple" < "Banana")
print("Cat" > "Bat")
```

Output:

```text
True
True
```

---

## 13. Escape Characters in Strings

Escape characters are special characters that begin with a backslash (`\`).

They are used to format strings.

| Escape Character | Meaning |
|---|---|
| `\n` | New line |
| `\t` | Horizontal tab |
| `\\` | Backslash |
| `\'` | Single quotation mark |
| `\"` | Double quotation mark |

### Example 1: New Line

```python
print("Hello\nPython")
```

Output:

```text
Hello
Python
```

### Example 2: Tab

```python
print("Name:\tRaj")
```

Output:

```text
Name:   Raj
```

### Example 3: Quotation Marks

```python
print("He said, \"Python is easy.\"")
```

Output:

```text
He said, "Python is easy."
```

---

## 14. Raw Strings

A raw string treats backslashes as literal characters instead of interpreting them as escape sequences.

Raw strings are commonly used for Windows file paths and regular expressions.

### Example

```python
path = r"C:\Users\Raj\Desktop"

print(path)
```

Output:

```text
C:\Users\Raj\Desktop
```

**Note:** A raw string cannot end with an odd number of backslashes because the final backslash would escape the closing quotation mark.

---

## 15. Practical Programs

### Program 1: Count Characters in a String

```python
text = input("Enter a string: ")

print("Total characters:", len(text))
```

### Program 2: Reverse a String

```python
text = input("Enter a string: ")

reverse = text[::-1]

print("Reversed string:", reverse)
```

### Program 3: Count Vowels

```python
text = input("Enter a string: ")

vowels = "aeiouAEIOU"
count = 0

for character in text:
    if character in vowels:
        count += 1

print("Total vowels:", count)
```

### Program 4: Count Consonants

```python
text = input("Enter a string: ")

vowels = "aeiouAEIOU"
count = 0

for character in text:
    if character.isalpha() and character not in vowels:
        count += 1

print("Total consonants:", count)
```

### Program 5: Count Spaces

```python
text = input("Enter a sentence: ")

count = 0

for character in text:
    if character == " ":
        count += 1

print("Total spaces:", count)
```

### Program 6: Check Whether a String Is a Palindrome

A palindrome is a word or sequence that reads the same forwards and backwards.

```python
text = input("Enter a word: ")

reverse = text[::-1]

if text == reverse:
    print("Palindrome")
else:
    print("Not a palindrome")
```

Example:

```text
Enter a word: madam
Palindrome
```

### Program 7: Count Digits in a String

```python
text = input("Enter a string: ")

count = 0

for character in text:
    if character.isdigit():
        count += 1

print("Total digits:", count)
```

### Program 8: Count Uppercase and Lowercase Characters

```python
text = input("Enter a string: ")

uppercase = 0
lowercase = 0

for character in text:
    if character.isupper():
        uppercase += 1
    elif character.islower():
        lowercase += 1

print("Uppercase characters:", uppercase)
print("Lowercase characters:", lowercase)
```

---

## 16. Student Practice Exercises

Solve these programs independently.

1. Ask the user for a name and print its length.
2. Access the first and last characters of a string.
3. Print a string in reverse order.
4. Extract the first five characters using slicing.
5. Print every second character of a string.
6. Check whether a particular word exists inside a sentence.
7. Count vowels in a sentence.
8. Count consonants in a sentence.
9. Count digits and spaces in a string.
10. Count uppercase and lowercase characters.
11. Check whether a word is a palindrome.
12. Compare two strings.
13. Replace the first character of a string by creating a new string.
14. Display every character with its index.
15. Count the total number of alphabetic characters.

---

## 17. Mini Project – Text Analyzer System

Create a Python program that analyzes text entered by the user.

### Requirements

1. Ask the user to enter a sentence.
2. Display the following menu:

```text
===== TEXT ANALYZER =====

1. Count Total Characters
2. Count Vowels
3. Count Consonants
4. Count Digits
5. Count Spaces
6. Count Uppercase Characters
7. Count Lowercase Characters
8. Reverse Text
9. Check Palindrome
10. Exit

Enter your choice:
```

3. Perform the selected operation.
4. Display the result.
5. Show the menu again until the user selects Exit.

### Rules

- Use string indexing and slicing where appropriate.
- Use `len()` to count characters.
- Use loops to traverse the string.
- Use conditional statements for character classification.
- Use a `while` loop for the menu.
- Validate invalid menu choices.
- Do not use advanced libraries.

### Challenge

Extend the project to:

- Count special characters.
- Display the first and last character.
- Find the frequency of a character entered by the user.
- Check whether a sentence is a palindrome after ignoring spaces and letter case.

---

## 18. Common Mistakes to Avoid

1. Assuming string indexing starts from 1.
2. Forgetting that negative indexing starts from `-1`.
3. Using an invalid index.
4. Forgetting that the stop index in slicing is excluded.
5. Trying to modify a string character directly.
6. Forgetting that string comparison is case-sensitive.
7. Confusing string concatenation with numeric addition.
8. Forgetting to convert user input when working with numbers.
9. Misunderstanding escape characters.
10. Forgetting that `len()` also counts spaces.

---

## 19. Trainer Assessment

Ask the student:

1. What is a string in Python?
2. What are the different ways to create strings?
3. What is zero-based indexing?
4. What is negative indexing?
5. What is string slicing?
6. What does `string[::-1]` do?
7. What does string immutability mean?
8. What is string concatenation?
9. What is the difference between `in` and `not in`?
10. How can we traverse a string using a loop?
11. What is the purpose of `ord()` and `chr()`?
12. What is a raw string?
13. What is the difference between `\n` and `\t`?
14. Why is `"python" == "Python"` False?

### Practical Assessment

- Reverse a string using slicing.
- Count vowels and consonants.
- Check whether a word is a palindrome.
- Count uppercase, lowercase and numeric characters.
- Complete the Text Analyzer System independently.

### Completion Criteria

The student should be able to:

- Create and manipulate basic strings.
- Understand positive and negative indexing.
- Extract portions of strings using slicing.
- Explain string immutability.
- Traverse strings using loops.
- Perform basic string comparisons.
- Analyze characters using conditions and loops.
- Complete the Text Analyzer System independently.

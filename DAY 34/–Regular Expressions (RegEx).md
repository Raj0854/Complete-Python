
# Day 34 – Regular Expressions (RegEx)

## 1. Introduction to Regular Expressions

Regular Expressions (RegEx) are patterns used to search, match, validate, extract, and replace text.

Python provides the built-in `re` module to work with regular expressions.

### Why Do We Use RegEx?

RegEx is useful when we need to:

- Find a phone number inside a paragraph.
- Extract email addresses from text.
- Check whether a string follows a particular pattern.
- Find dates, numbers, or hashtags.
- Replace unwanted text.
- Validate basic input formats.

### Example

```python
import re

text = "My phone number is 9876543210"

result = re.search(r"\d{10}", text)

if result:
    print("Phone number found:", result.group())
else:
    print("Phone number not found")
```

**Output:**
```text
Phone number found: 9876543210
```

Here:
- `re` is the regular expression module.
- `\d` represents a digit.
- `{10}` means exactly 10 repetitions.
- `search()` searches for a matching pattern.
- `group()` returns the matched text.

---

## 2. Importing the re Module

Python provides the `re` module as part of its standard library.

No additional installation is required.

```python
import re

text = "Python is easy to learn"

result = re.search("Python", text)

print(result)
```

**Output:**
```text
<re.Match object; ...>
```

If no match is found, the result is `None`.

```python
import re

text = "I am learning Python"

result = re.search("Java", text)

print(result)
```

**Output:**
```text
None
```

---

## 3. Raw Strings in Regular Expressions

Regular expressions commonly use backslashes (`\`).

Python also uses backslashes for special string characters such as `\n` and `\t`.

To avoid unwanted escape-sequence interpretation, use raw strings by adding `r` before the string.

### Normal String

```python
pattern = "\\d+"
```

### Raw String

```python
pattern = r"\d+"
```

Both represent the same regular expression pattern.

**Recommended:** Use raw strings for regular expression patterns.

---

## 4. Basic Regular Expression Characters

RegEx uses special characters called metacharacters.

| Character | Meaning |
|---|---|
| `.` | Matches any character except newline by default |
| `^` | Matches the beginning of a string or line |
| `$` | Matches the end of a string or line |
| `*` | Matches zero or more repetitions |
| `+` | Matches one or more repetitions |
| `?` | Matches zero or one repetition |
| `{}` | Specifies the number of repetitions |
| `[]` | Defines a character set |
| `()` | Groups expressions |
| `|` | Represents OR |
| `\` | Introduces a special sequence or escapes a metacharacter |

### 4.1 Dot (.)

Matches any character except a newline by default.

```python
import re

text = "cat cot cut"

result = re.findall(r"c.t", text)

print(result)
```

**Output:**
```text
['cat', 'cot', 'cut']
```

### 4.2 Caret (^)

Matches the beginning of a string.

```python
import re

text = "Python is powerful"

result = re.search(r"^Python", text)

print(bool(result))
```

**Output:**
```text
True
```

### 4.3 Dollar ($)

Matches the end of a string.

```python
import re

text = "I love Python"

result = re.search(r"Python$", text)

print(bool(result))
```

**Output:**
```text
True
```

### 4.4 Asterisk (*)

Matches zero or more repetitions of the preceding character or group.

```python
import re

text = "color colour colouur"

result = re.findall(r"colou*r", text)

print(result)
```

**Output:**
```text
['color', 'colour', 'colouur']
```

### 4.5 Plus (+)

Matches one or more repetitions.

```python
import re

text = "a aa aaa b"

result = re.findall(r"a+", text)

print(result)
```

**Output:**
```text
['a', 'aa', 'aaa']
```

### 4.6 Question Mark (?)

Matches zero or one repetition.

```python
import re

text = "color colour"

result = re.findall(r"colou?r", text)

print(result)
```

**Output:**
```text
['color', 'colour']
```

### 4.7 Curly Braces {}

Specifies the number of repetitions.

| Pattern | Meaning |
|---|---|
| `a{3}` | Exactly 3 repetitions |
| `a{2,}` | At least 2 repetitions |
| `a{2,5}` | Between 2 and 5 repetitions |

Example:

```python
import re

text = "a aa aaa aaaa aaaaaa"

result = re.findall(r"a{2,4}", text)

print(result)
```

**Output:**
```text
['aa', 'aaa', 'aaaa', 'aaaa']
```

### 4.8 Character Set ([])

Matches one character from the specified set.

```python
import re

text = "cat bat rat mat"

result = re.findall(r"[cb]at", text)

print(result)
```

**Output:**
```text
['cat', 'bat']
```

More examples:

```python
import re

print(re.findall(r"[aeiou]", "python programming"))
print(re.findall(r"[0-9]", "Room 204"))
print(re.findall(r"[a-z]", "Hello123"))
```

**Output:**
```text
['o', 'o', 'a', 'i', 'o', 'a', 'i']
['2', '0', '4']
['e', 'l', 'l', 'o']
```

Character set shortcuts:

- `[a-z]`: lowercase English letters.
- `[A-Z]`: uppercase English letters.
- `[0-9]`: digits.
- `[a-zA-Z]`: English letters.
- `[^0-9]`: any character except digits.

### 4.9 Alternation (|)

Works like the OR operator.

```python
import re

text = "I like Python and Java"

result = re.findall(r"Python|Java", text)

print(result)
```

**Output:**
```text
['Python', 'Java']
```

### 4.10 Groups ()

Parentheses group parts of a pattern and can capture matching text.

```python
import re

text = "2026-11-05"

result = re.search(r"(\d{4})-(\d{2})-(\d{2})", text)

if result:
    print(result.group(0))
    print(result.group(1))
    print(result.group(2))
    print(result.group(3))
```

**Output:**
```text
2026-11-05
2026
11
05
```

- `group(0)` returns the complete match.
- `group(1)` returns the first captured group.
- `group(2)` returns the second captured group.
- `group(3)` returns the third captured group.

---

## 5. Special Character Sequences

Python RegEx provides shortcuts for commonly used character types.

| Pattern | Meaning |
|---|---|
| `\d` | Any Unicode decimal digit |
| `\D` | Any character that is not a decimal digit |
| `\w` | Unicode word character: letters, digits and underscore |
| `\W` | Any character that is not a word character |
| `\s` | Whitespace character |
| `\S` | Non-whitespace character |
| `\b` | Word boundary |
| `\B` | Not a word boundary |

### 5.1 Digits (\d)

```python
import re

text = "My age is 25 and my score is 90"

result = re.findall(r"\d", text)

print(result)
```

**Output:**
```text
['2', '5', '9', '0']
```

Use `\d+` to match complete numbers:

```python
print(re.findall(r"\d+", "Age 25, Score 90"))
```

**Output:**
```text
['25', '90']
```

### 5.2 Non-Digits (\D)

```python
import re

text = "Room 204"

result = re.findall(r"\D+", text)

print(result)
```

**Output:**
```text
['Room ']
```

### 5.3 Word Characters (\w)

```python
import re

text = "Python_123 is easy!"

result = re.findall(r"\w+", text)

print(result)
```

**Output:**
```text
['Python_123', 'is', 'easy']
```

### 5.4 Whitespace (\s)

```python
import re

text = "Python is easy to learn"

result = re.findall(r"\s", text)

print(len(result))
```

**Output:**
```text
4
```

### 5.5 Word Boundary (\b)

Matches a boundary between a word character and a non-word character.

```python
import re

text = "Python is easy. I love Python programming."

result = re.findall(r"\bPython\b", text)

print(result)
```

**Output:**
```text
['Python', 'Python']
```

It does not match `Python` as part of a larger word such as `Pythonic`.

---

## 6. Greedy and Non-Greedy Quantifiers

Quantifiers are greedy by default. They try to match as much text as possible.

Adding `?` after a quantifier makes it non-greedy (lazy), meaning it matches as little text as possible while still satisfying the pattern.

### Greedy Example

```python
import re

text = "<h1>Welcome</h1><h2>Python</h2>"

result = re.findall(r"<.*>", text)

print(result)
```

**Output:**
```text
['<h1>Welcome</h1><h2>Python</h2>']
```

### Non-Greedy Example

```python
import re

text = "<h1>Welcome</h1><h2>Python</h2>"

result = re.findall(r"<.*?>", text)

print(result)
```

**Output:**
```text
['<h1>', '</h1>', '<h2>', '</h2>']
```

Common greedy and lazy pairs:

| Greedy | Non-Greedy |
|---|---|
| `*` | `*?` |
| `+` | `+?` |
| `?` | `??` |
| `{2,5}` | `{2,5}?` |

---

## 7. Important Functions of the re Module

Python's `re` module provides several functions for working with patterns.

### 7.1 re.match()

Checks for a match only at the beginning of a string.

```python
import re

text = "Python is easy"

result = re.match(r"Python", text)

if result:
    print("Match found")
else:
    print("No match")
```

**Output:**
```text
Match found
```

Example without a beginning match:

```python
import re

text = "I love Python"

result = re.match(r"Python", text)

print(result)
```

**Output:**
```text
None
```

### 7.2 re.search()

Searches the entire string and returns the first matching result.

```python
import re

text = "I am learning Python programming"

result = re.search(r"Python", text)

if result:
    print("Found:", result.group())
    print("Start:", result.start())
    print("End:", result.end())
```

**Output:**
```text
Found: Python
Start: 14
End: 20
```

### 7.3 re.fullmatch()

Checks whether the entire string matches the pattern.

```python
import re

text = "12345"

result = re.fullmatch(r"\d+", text)

print(bool(result))
```

**Output:**
```text
True
```

Another example:

```python
import re

text = "12345abc"

result = re.fullmatch(r"\d+", text)

print(bool(result))
```

**Output:**
```text
False
```

### 7.4 Difference Between match(), search() and fullmatch()

| Function | Purpose |
|---|---|
| `match()` | Checks from the beginning |
| `search()` | Finds the first match anywhere |
| `fullmatch()` | Requires the entire string to match |

### 7.5 re.findall()

Returns all non-overlapping matches in a list.

```python
import re

text = "My marks are 80, 90 and 95"

result = re.findall(r"\d+", text)

print(result)
```

**Output:**
```text
['80', '90', '95']
```

### 7.6 re.finditer()

Returns an iterator containing match objects.

```python
import re

text = "Python 100 Java 200"

result = re.finditer(r"\d+", text)

for match in result:
    print(match.group(), match.start(), match.end())
```

**Output:**
```text
100 7 10
200 16 19
```

### 7.7 re.split()

Splits a string wherever the pattern matches.

```python
import re

text = "Python,Java;C++ PHP"

result = re.split(r"[,;\s]+", text)

print(result)
```

**Output:**
```text
['Python', 'Java', 'C++', 'PHP']
```

### 7.8 re.sub()

Replaces matching text with another value.

```python
import re

text = "My phone number is 9876543210"

result = re.sub(r"\d", "*", text)

print(result)
```

**Output:**
```text
My phone number is **********
```

### 7.9 re.subn()

Works like `sub()` but also returns the number of replacements.

```python
import re

text = "Python 123 Java 456"

result = re.subn(r"\d+", "NUMBER", text)

print(result)
```

**Output:**
```text
('Python NUMBER Java NUMBER', 2)
```

### 7.10 re.escape()

Escapes special RegEx characters so they can be searched as literal text.

```python
import re

text = "Price is $100.00"

pattern = re.escape("$100.00")

result = re.search(pattern, text)

print(result.group())
```

**Output:**
```text
$100.00
```

### 7.11 re.compile()

Compiles a regular expression into a reusable pattern object.

```python
import re

pattern = re.compile(r"\d+")

text1 = "Age: 25"
text2 = "Score: 90"

print(pattern.findall(text1))
print(pattern.findall(text2))
```

**Output:**
```text
['25']
['90']
```

Use `re.compile()` when the same pattern is used repeatedly.

---

## 8. Capturing and Non-Capturing Groups

Groups allow us to organize patterns and extract specific parts of matched text.

### 8.1 Capturing Groups

Normal parentheses create capturing groups.

```python
import re

text = "Raj Sharma"

result = re.search(r"(\w+)\s+(\w+)", text)

if result:
    print("Full name:", result.group(0))
    print("First name:", result.group(1))
    print("Last name:", result.group(2))
```

**Output:**
```text
Full name: Raj Sharma
First name: Raj
Last name: Sharma
```

### 8.2 Non-Capturing Groups

Use `(?:...)` when you want to group parts of a pattern without capturing them.

```python
import re

text = "Python Java"

result = re.findall(r"(?:Python|Java)", text)

print(result)
```

**Output:**
```text
['Python', 'Java']
```

### 8.3 Named Groups

Named groups give meaningful names to captured values.

Syntax:

```python
(?P<name>pattern)
```

Example:

```python
import re

text = "Date: 2026-11-05"

pattern = r"(?P<year>\d{4})-(?P<month>\d{2})-(?P<day>\d{2})"

result = re.search(pattern, text)

if result:
    print(result.group("year"))
    print(result.group("month"))
    print(result.group("day"))
```

**Output:**
```text
2026
11
05
```

### 8.4 Backreferences

Backreferences match the same text captured by an earlier group.

```python
import re

text = "hello hello world"

result = re.search(r"\b(\w+)\s+\1\b", text)

if result:
    print("Repeated word:", result.group(1))
```

**Output:**
```text
Repeated word: hello
```

Here, `\1` refers to the first captured group.

---

## 9. Regular Expression Flags

Flags modify how a regular expression behaves.

| Flag | Meaning |
|---|---|
| `re.IGNORECASE` | Ignores uppercase/lowercase differences |
| `re.MULTILINE` | Makes `^` and `$` work at each line boundary |
| `re.DOTALL` | Allows `.` to match newline characters |
| `re.VERBOSE` | Allows readable patterns with comments and whitespace |

### 9.1 IGNORECASE

```python
import re

text = "PYTHON is powerful"

result = re.search(r"python", text, re.IGNORECASE)

print(bool(result))
```

**Output:**
```text
True
```

### 9.2 MULTILINE

```python
import re

text = """Python
Java
Python"""

result = re.findall(r"^Python", text, re.MULTILINE)

print(result)
```

**Output:**
```text
['Python', 'Python']
```

### 9.3 DOTALL

```python
import re

text = "Hello\nPython"

result = re.search(r"Hello.Python", text, re.DOTALL)

print(bool(result))
```

**Output:**
```text
True
```

### 9.4 VERBOSE

Allows patterns to be written across multiple lines for better readability.

```python
import re

pattern = re.compile(
    r"""
    \d{4}    # Year
    -
    \d{2}    # Month
    -
    \d{2}    # Day
    """,
    re.VERBOSE
)

text = "2026-11-05"

print(bool(pattern.fullmatch(text)))
```

**Output:**
```text
True
```

---

## 10. Practical Pattern Validation

RegEx can check whether text follows a particular format.

Remember: a pattern-based check does not always prove that the supplied information is real or valid according to every external standard.

### 10.1 Basic Email Pattern

```python
import re

email = input("Enter email: ")

pattern = r"^[A-Za-z0-9._%+-]+@[A-Za-z0-9.-]+\.[A-Za-z]{2,}$"

if re.fullmatch(pattern, email):
    print("Email format looks valid")
else:
    print("Invalid email format")
```

**Sample Output:**
```text
Enter email: raj@example.com
Email format looks valid
```

This is a basic format check, not complete email validation. Production systems should use appropriate validation libraries and verify ownership by sending a confirmation message.

### 10.2 Basic 10-Digit Phone Number Check

```python
import re

phone = input("Enter phone number: ")

pattern = r"^[0-9]{10}$"

if re.fullmatch(pattern, phone):
    print("Valid phone format")
else:
    print("Invalid phone format")
```

**Sample Output:**
```text
Enter phone number: 9876543210
Valid phone format
```

This checks only for exactly 10 ASCII digits. It does not verify whether the number is assigned or active.

### 10.3 Password Format Check

Requirements:
- At least 8 characters.
- At least one uppercase letter.
- At least one lowercase letter.
- At least one digit.
- At least one special character.

```python
import re

password = input("Enter password: ")

pattern = r"^(?=.*[A-Z])(?=.*[a-z])(?=.*\d)(?=.*[^A-Za-z0-9\s])\S{8,}$"

if re.fullmatch(pattern, password):
    print("Password format accepted")
else:
    print("Password does not meet the requirements")
```

**Sample Output:**
```text
Enter password: Hello@123
Password format accepted
```

The expressions `(?=...)` are called positive lookaheads. They check that a condition exists without consuming characters.

### 10.4 Basic URL Pattern

```python
import re

url = input("Enter URL: ")

pattern = r"^https?://[A-Za-z0-9.-]+\.[A-Za-z]{2,}(?::\d{1,5})?(?:/[^\s]*)?$"

if re.fullmatch(pattern, url):
    print("URL format looks valid")
else:
    print("Invalid URL format")
```

**Sample Output:**
```text
Enter URL: https://www.example.com
URL format looks valid
```

This is a simplified URL pattern. It does not cover every valid URL or verify that a website exists.

### 10.5 Basic IPv4 Address Pattern

```python
import re

ip = input("Enter IPv4 address: ")

pattern = r"^(?:[0-9]{1,3}\.){3}[0-9]{1,3}$"

if re.fullmatch(pattern, ip):
    parts = ip.split(".")

    if all(0 <= int(part) <= 255 for part in parts):
        print("Valid IPv4 address format")
    else:
        print("Invalid IPv4 address")
else:
    print("Invalid IPv4 address format")
```

**Sample Output:**
```text
Enter IPv4 address: 192.168.1.10
Valid IPv4 address format
```

The extra numeric check is necessary because the regular expression alone would also accept values such as `999.999.999.999`.

---

## 11. Practical Text Extraction Programs

### 11.1 Extract All Numbers

```python
import re

text = "I purchased 3 books for 750 rupees and 2 pens for 50 rupees."

numbers = re.findall(r"\d+", text)

print(numbers)
```

**Output:**
```text
['3', '750', '2', '50']
```

### 11.2 Extract Dates

```python
import re

text = "Meeting dates: 05-11-2026, 12-12-2026"

dates = re.findall(r"\b\d{2}-\d{2}-\d{4}\b", text)

print(dates)
```

**Output:**
```text
['05-11-2026', '12-12-2026']
```

This extracts date-shaped strings; it does not check whether a calendar date actually exists.

### 11.3 Extract Hashtags

```python
import re

text = "Learning #Python and #Programming is fun. #Coding"

hashtags = re.findall(r"(?<!\w)#[A-Za-z0-9_]+", text)

print(hashtags)
```

**Output:**
```text
['#Python', '#Programming', '#Coding']
```

### 11.4 Extract Words

```python
import re

text = "Python is easy, powerful, and useful!"

words = re.findall(r"\b\w+\b", text)

print(words)
```

**Output:**
```text
['Python', 'is', 'easy', 'powerful', 'and', 'useful']
```

### 11.5 Extract Email Addresses

```python
import re

text = """
Contact us:
admin@example.com
support@gmail.com
invalid-email
"""

pattern = r"\b[A-Za-z0-9._%+-]+@[A-Za-z0-9.-]+\.[A-Za-z]{2,}\b"

emails = re.findall(pattern, text)

print(emails)
```

**Output:**
```text
['admin@example.com', 'support@gmail.com']
```

### 11.6 Extract Phone Numbers

```python
import re

text = """
Raj: 9876543210
Amit: 8765432109
Neha: 7654321098
"""

phones = re.findall(r"\b[0-9]{10}\b", text)

print(phones)
```

**Output:**
```text
['9876543210', '8765432109', '7654321098']
```

### 11.7 Replace Multiple Spaces

```python
import re

text = "Python     is     very      easy"

result = re.sub(r"\s+", " ", text)

print(result)
```

**Output:**
```text
Python is very easy
```

### 11.8 Mask Phone Numbers

```python
import re

text = "Contact number: 9876543210"

result = re.sub(r"\d(?=\d{4})", "*", text)

print(result)
```

**Output:**
```text
Contact number: ******3210
```

### 11.9 Mask Email Addresses

```python
import re

email = "raj@example.com"

result = re.sub(
    r"(?<=^)[A-Za-z0-9._%+-](?=[A-Za-z0-9._%+-]*@)",
    "*",
    email
)

print(result)
```

**Output:**
```text
***@example.com
```

This example masks the local part of a basic email-shaped string. For real-world masking, use a carefully tested function that also handles edge cases.

### 11.10 Split Text Using Multiple Separators

```python
import re

text = "Python,Java;C++|PHP"

result = re.split(r"[,;|]", text)

print(result)
```

**Output:**
```text
['Python', 'Java', 'C++', 'PHP']
```

**Important:** For actual CSV files, use Python's built-in `csv` module instead of splitting on commas with RegEx. CSV supports quoted values and escaped delimiters.

---

## 12. Common RegEx Mistakes

### Mistake 1: Using match() Instead of search()

```python
import re

text = "I love Python"

print(re.match(r"Python", text))
```

Output:
```text
None
```

`match()` checks only the beginning. Use `search()` to find a match anywhere.

### Mistake 2: Forgetting Raw Strings

Prefer:

```python
pattern = r"\d+"
```

Instead of:

```python
pattern = "\\d+"
```

### Mistake 3: Confusing * and +

- `*` allows zero or more repetitions.
- `+` requires at least one repetition.

### Mistake 4: Using search() for Complete Validation

```python
import re

text = "123ABC"

print(bool(re.search(r"\d+", text)))
```

Output:
```text
True
```

This only finds digits somewhere in the text.

For complete numeric validation:

```python
print(bool(re.fullmatch(r"\d+", text)))
```

Output:
```text
False
```

### Mistake 5: Making Patterns Too Complicated

A very complex pattern can become difficult to understand and maintain.

Use:
- Small patterns.
- Named groups.
- `re.VERBOSE`.
- Comments and test cases.

### Mistake 6: Treating a Regex Match as Proof of Validity

A matching email pattern does not prove that an email address exists. A matching phone pattern does not prove that a phone number is active.

Always use the appropriate validation method for the application.

---

## 13. Practical Exercises

### Exercise 1: Basic Pattern Matching

Write programs to:

1. Find the word `Python` in a sentence.
2. Check whether a string starts with `Hello`.
3. Check whether a string ends with `.com`.
4. Extract all digits from a string.
5. Extract all lowercase English letters.
6. Find all words containing exactly five English letters.

### Exercise 2: Quantifiers and Character Sets

1. Find all numbers containing exactly four digits.
2. Find words starting with `P`.
3. Find words ending with `ing`.
4. Find strings containing two or more consecutive digits.
5. Extract all vowels from a sentence.
6. Find all words that contain only letters.

### Exercise 3: re Module Functions

1. Demonstrate the difference between `match()` and `search()`.
2. Use `fullmatch()` to validate a five-digit PIN.
3. Extract all prices from a paragraph.
4. Replace all numbers with `XXX`.
5. Split a sentence using spaces, commas, and semicolons.
6. Use `finditer()` to print every match and its position.

### Exercise 4: Validation

1. Write a basic email format checker.
2. Validate a 10-digit phone number.
3. Validate a basic password format.
4. Check a date in `DD-MM-YYYY` format.
5. Check an IPv4 address with a numeric range check.
6. Write a basic URL format checker.

### Exercise 5: Text Processing

1. Extract all hashtags from a social media post.
2. Extract all email addresses from a paragraph.
3. Extract all phone numbers from a contact list.
4. Mask all but the last four digits of a phone number.
5. Remove extra spaces from a paragraph.
6. Find repeated consecutive words.

---

## 14. Mini Project – Contact Information Extractor

### Project Description

Create a Python program that scans a block of text and extracts useful contact information.

The program should identify:

- Email addresses.
- 10-digit phone numbers.
- Dates in `DD-MM-YYYY` format.
- Hashtags.
- Basic HTTP/HTTPS URLs.

It should also:
- Count the total number of matches in each category.
- Display extracted information separately.
- Mask phone numbers.
- Replace email addresses with `[EMAIL HIDDEN]` in a masked copy of the text.

### Step 1: Create the Project File

Create:

```text
contact_extractor.py
```

### Step 2: Import the Module

```python
import re
```

### Step 3: Prepare Sample Text

```python
text = """
Hello, my name is Raj.

Contact:
Email: raj@example.com
Support: help@gmail.com

Phone: 9876543210
Alternate: 8765432109

Meeting date: 05-11-2026

Visit https://www.example.com

Follow us:
#Python #Programming #Learning
"""
```

### Step 4: Create Regular Expression Patterns

```python
email_pattern = r"\b[A-Za-z0-9._%+-]+@[A-Za-z0-9.-]+\.[A-Za-z]{2,}\b"

phone_pattern = r"\b[0-9]{10}\b"

date_pattern = r"\b\d{2}-\d{2}-\d{4}\b"

hashtag_pattern = r"(?<!\w)#[A-Za-z0-9_]+"

url_pattern = r"https?://[A-Za-z0-9.-]+\.[A-Za-z]{2,}(?::\d{1,5})?(?:/[^\s]*)?"
```

### Step 5: Extract Information

```python
emails = re.findall(email_pattern, text)
phones = re.findall(phone_pattern, text)
dates = re.findall(date_pattern, text)
hashtags = re.findall(hashtag_pattern, text)
urls = re.findall(url_pattern, text)
```

### Step 6: Display Results

```python
print("CONTACT INFORMATION REPORT")

print("\nEmail Addresses:")
for email in emails:
    print(email)

print("\nPhone Numbers:")
for phone in phones:
    print(phone)

print("\nDates:")
for date in dates:
    print(date)

print("\nHashtags:")
for hashtag in hashtags:
    print(hashtag)

print("\nURLs:")
for url in urls:
    print(url)
```

### Step 7: Display Summary

```python
print("\nSUMMARY")

print("Total Emails:", len(emails))
print("Total Phone Numbers:", len(phones))
print("Total Dates:", len(dates))
print("Total Hashtags:", len(hashtags))
print("Total URLs:", len(urls))
```

### Step 8: Mask Sensitive Information

```python
masked_text = re.sub(phone_pattern, lambda match: "*" * 6 + match.group()[-4:], text)

masked_text = re.sub(email_pattern, "[EMAIL HIDDEN]", masked_text)

print("\nMASKED TEXT:")
print(masked_text)
```

### Expected Output (Summary)

```text
SUMMARY

Total Emails: 2
Total Phone Numbers: 2
Total Dates: 1
Total Hashtags: 3
Total URLs: 1
```

### Project Challenges

1. Allow users to enter their own text.
2. Extract multiple dates and phone numbers.
3. Save the extracted report to a text file.
4. Add an option to search for a particular email address.
5. Display the number of unique email addresses.
6. Handle empty input.
7. Add a menu-driven interface.

**Note:** This is an educational text scanner. Its patterns are simplified and do not guarantee complete validation of real-world contact information.

---

## 15. Trainer Assessment

Ask the student the following questions:

1. What is a regular expression?
2. Why do we use the `re` module?
3. Why are raw strings recommended for RegEx?
4. What is the difference between `\d` and `\D`?
5. What is the difference between `*` and `+`?
6. What does `{2,5}` mean?
7. What is the difference between `match()` and `search()`?
8. What is the purpose of `fullmatch()`?
9. What is the difference between `findall()` and `finditer()`?
10. What does `sub()` do?
11. What are capturing groups?
12. What is a named group?
13. What is the purpose of `re.IGNORECASE`?
14. What is the difference between greedy and non-greedy matching?
15. Why is RegEx alone not sufficient for complete email validation?

### Practical Assessment

Ask the student to independently:

- Extract all numbers from a paragraph.
- Find email addresses using RegEx.
- Validate a basic phone number format.
- Replace extra spaces.
- Extract hashtags.
- Mask phone numbers.
- Complete the Contact Information Extractor project.

---

## 16. Completion Criteria

The student should be able to:

- Explain the purpose of regular expressions.
- Import and use the `re` module.
- Understand metacharacters and special sequences.
- Use quantifiers and character sets.
- Understand greedy and non-greedy matching.
- Use `match()`, `search()`, `fullmatch()`, `findall()` and `finditer()`.
- Replace and split text using RegEx.
- Use capturing groups and named groups.
- Apply common regular expression flags.
- Create basic format-validation patterns.
- Extract and mask information from text.
- Complete the Contact Information Extractor mini-project.

**Day 34 Completed: Regular Expressions (RegEx).**


# Day 35 – Date, Time & Calendar

## 1. Introduction to Date and Time

Python provides built-in modules to work with dates, times, timestamps and calendars.

The three important modules are:

| Module | Purpose |
|---|---|
| `datetime` | Work with dates, times and date-time values |
| `time` | Work with timestamps, delays and system time |
| `calendar` | Display and inspect calendars |

### Real-World Applications

- Calculate a person's age.
- Find the number of days between two dates.
- Calculate employee working hours.
- Create appointment and booking systems.
- Generate invoices with timestamps.
- Calculate deadlines and due dates.
- Display monthly calendars.

Import the required modules:

```python
import datetime
import time
import calendar
```

---

## 2. Working with the datetime Module

The `datetime` module provides classes to work with dates and times.

Important classes:

| Class | Purpose |
|---|---|
| `date` | Stores year, month and day |
| `time` | Stores hour, minute, second and microsecond |
| `datetime` | Stores both date and time |
| `timedelta` | Represents a duration or time difference |
| `timezone` | Represents a fixed UTC offset |

### 2.1 Get the Current Date

Use `date.today()` to get today's date.

```python
from datetime import date

today = date.today()

print(today)
print(today.year)
print(today.month)
print(today.day)
```

**Sample Output:**

```text
2026-11-05
2026
11
5
```

The actual output depends on the system date.

### 2.2 Create a Custom Date

Use `date(year, month, day)`.

```python
from datetime import date

my_date = date(2026, 12, 25)

print(my_date)
print("Year:", my_date.year)
print("Month:", my_date.month)
print("Day:", my_date.day)
```

**Output:**

```text
2026-12-25
Year: 2026
Month: 12
Day: 25
```

Invalid dates raise `ValueError`.

```python
from datetime import date

# This date does not exist.
my_date = date(2026, 2, 30)
```

### 2.3 Get the Current Date and Time

Use `datetime.now()`.

```python
from datetime import datetime

current = datetime.now()

print(current)
print("Year:", current.year)
print("Month:", current.month)
print("Day:", current.day)
print("Hour:", current.hour)
print("Minute:", current.minute)
print("Second:", current.second)
```

**Sample Output:**

```text
2026-11-05 14:30:25.123456
Year: 2026
Month: 11
Day: 5
Hour: 14
Minute: 30
Second: 25
```

The exact output changes according to the current system time.

### 2.4 Create a Custom Date and Time

Use `datetime(year, month, day, hour, minute, second)`.

```python
from datetime import datetime

custom = datetime(2026, 12, 25, 10, 30, 45)

print(custom)
```

**Output:**

```text
2026-12-25 10:30:45
```

### 2.5 Get Individual Date and Time Components

```python
from datetime import datetime

current = datetime.now()

print("Date:", current.date())
print("Time:", current.time())
print("Year:", current.year)
print("Month:", current.month)
print("Day:", current.day)
print("Hour:", current.hour)
print("Minute:", current.minute)
print("Second:", current.second)
```

### 2.6 Get the Day of the Week

Use `weekday()` or `isoweekday()`.

```python
from datetime import date

today = date(2026, 11, 5)

print(today.weekday())
print(today.isoweekday())
```

**Output:**

```text
3
4
```

Difference:

| Method | Monday | Sunday |
|---|---:|---:|
| `weekday()` | 0 | 6 |
| `isoweekday()` | 1 | 7 |

---

## 3. Working with the time Class

The `time` class represents a time of day.

It does not store a date.

```python
from datetime import time

my_time = time(14, 30, 45)

print(my_time)
print("Hour:", my_time.hour)
print("Minute:", my_time.minute)
print("Second:", my_time.second)
```

**Output:**

```text
14:30:45
Hour: 14
Minute: 30
Second: 45
```

### Create Time with Microseconds

```python
from datetime import time

my_time = time(10, 20, 30, 500000)

print(my_time)
```

**Output:**

```text
10:20:30.500000
```

---

## 4. Formatting Dates and Times with strftime()

`strftime()` converts a date or time into a formatted string.

Syntax:

```python
datetime_object.strftime(format)
```

### Common Formatting Directives

| Directive | Meaning | Example |
|---|---|---|
| `%Y` | Four-digit year | 2026 |
| `%y` | Two-digit year | 26 |
| `%m` | Month number | 11 |
| `%B` | Full month name | November |
| `%b` | Short month name | Nov |
| `%d` | Day of month | 05 |
| `%A` | Full weekday name | Thursday |
| `%a` | Short weekday name | Thu |
| `%H` | Hour (24-hour) | 14 |
| `%I` | Hour (12-hour) | 02 |
| `%M` | Minute | 30 |
| `%S` | Second | 45 |
| `%p` | AM/PM | PM |
| `%f` | Microseconds | 500000 |
| `%j` | Day of the year | 309 |
| `%w` | Weekday number (Sunday = 0) | 4 |
| `%z` | UTC offset | +0530 |
| `%Z` | Timezone name | IST (if provided by timezone) |
| `%%` | Literal percent sign | % |

### Example 1: Format a Date

```python
from datetime import datetime

current = datetime.now()

print(current.strftime("%d-%m-%Y"))
print(current.strftime("%B %d, %Y"))
print(current.strftime("%A"))
```

**Sample Output:**

```text
05-11-2026
November 05, 2026
Thursday
```

### Example 2: Format Time

```python
from datetime import datetime

current = datetime.now()

print(current.strftime("%H:%M:%S"))
print(current.strftime("%I:%M:%S %p"))
```

**Sample Output:**

```text
14:30:45
02:30:45 PM
```

### Example 3: Custom Date and Time Format

```python
from datetime import datetime

current = datetime.now()

formatted = current.strftime(
    "Today is %A, %d %B %Y. Time: %I:%M %p"
)

print(formatted)
```

**Sample Output:**

```text
Today is Thursday, 05 November 2026. Time: 02:30 PM
```

---

## 5. Converting Strings into Dates with strptime()

`strptime()` converts a string into a date-time object using a specified format.

Syntax:

```python
datetime.strptime(date_string, format)
```

### Example 1: Convert a Date String

```python
from datetime import datetime

date_string = "05-11-2026"

result = datetime.strptime(date_string, "%d-%m-%Y")

print(result)
print(type(result))
```

**Output:**

```text
2026-11-05 00:00:00
<class 'datetime.datetime'>
```

### Example 2: Convert Date and Time

```python
from datetime import datetime

date_string = "05-11-2026 02:30 PM"

result = datetime.strptime(
    date_string,
    "%d-%m-%Y %I:%M %p"
)

print(result)
```

**Output:**

```text
2026-11-05 14:30:00
```

### Difference Between strftime() and strptime()

| Method | Purpose |
|---|---|
| `strftime()` | Date-time object to formatted string |
| `strptime()` | Formatted string to date-time object |

Remember:

- `f` in `strftime` relates to formatting.
- `p` in `strptime` relates to parsing.

---

## 6. Date Calculations with timedelta

`timedelta` represents a duration or difference between dates and times.

It can be used to add or subtract days, weeks, hours, minutes and seconds.

### 6.1 Add Days to a Date

```python
from datetime import date, timedelta

today = date(2026, 11, 5)

future = today + timedelta(days=10)

print(future)
```

**Output:**

```text
2026-11-15
```

### 6.2 Subtract Days

```python
from datetime import date, timedelta

today = date(2026, 11, 5)

previous = today - timedelta(days=5)

print(previous)
```

**Output:**

```text
2026-10-31
```

### 6.3 Add Weeks

```python
from datetime import date, timedelta

today = date(2026, 11, 5)

future = today + timedelta(weeks=2)

print(future)
```

**Output:**

```text
2026-11-19
```

### 6.4 Add Hours and Minutes

```python
from datetime import datetime, timedelta

current = datetime(2026, 11, 5, 10, 30)

future = current + timedelta(hours=3, minutes=45)

print(future)
```

**Output:**

```text
2026-11-05 14:15:00
```

### 6.5 Calculate the Difference Between Two Dates

Subtracting two dates returns a `timedelta` object.

```python
from datetime import date

date1 = date(2026, 11, 5)
date2 = date(2026, 11, 20)

difference = date2 - date1

print("Difference:", difference)
print("Days:", difference.days)
```

**Output:**

```text
Difference: 15 days, 0:00:00
Days: 15
```

### 6.6 Calculate the Difference Between Two Times

```python
from datetime import datetime

start = datetime(2026, 11, 5, 9, 0)
end = datetime(2026, 11, 5, 17, 30)

difference = end - start

print("Total seconds:", difference.total_seconds())
print("Total hours:", difference.total_seconds() / 3600)
```

**Output:**

```text
Total seconds: 30600.0
Total hours: 8.5
```

### Important timedelta Attributes

| Attribute / Method | Purpose |
|---|---|
| `.days` | Whole days |
| `.seconds` | Remaining seconds within a day |
| `.microseconds` | Remaining microseconds |
| `.total_seconds()` | Total duration in seconds |

Use `total_seconds()` when you need the complete duration.

---

## 7. Comparing Dates and Times

Date and datetime objects can be compared.

```python
from datetime import date

date1 = date(2026, 11, 5)
date2 = date(2026, 11, 10)

print(date1 < date2)
print(date1 > date2)
print(date1 == date2)
```

**Output:**

```text
True
False
False
```

### Check Whether a Deadline Has Passed

```python
from datetime import date

today = date.today()
deadline = date(2026, 12, 31)

if today > deadline:
    print("Deadline passed")
elif today == deadline:
    print("Deadline is today")
else:
    print("Deadline is upcoming")
```

The output depends on the date when the program runs.

---

## 8. Timezones in Python

A timezone identifies the time offset or timezone rules associated with a date-time value.

Python supports timezone-aware date-time objects.

### 8.1 Current UTC Time

```python
from datetime import datetime, timezone

utc_now = datetime.now(timezone.utc)

print(utc_now)
```

The exact output depends on the current time.

### 8.2 Create a Fixed Timezone

```python
from datetime import datetime, timezone, timedelta

india_timezone = timezone(timedelta(hours=5, minutes=30))

india_time = datetime.now(india_timezone)

print(india_time)
print(india_time.strftime("%d-%m-%Y %I:%M %p %z"))
```

### 8.3 Convert UTC to Another Fixed Offset

```python
from datetime import datetime, timezone, timedelta

utc_now = datetime.now(timezone.utc)

india_timezone = timezone(timedelta(hours=5, minutes=30))

india_time = utc_now.astimezone(india_timezone)

print("UTC:", utc_now)
print("India:", india_time)
```

**Important:**

- A naive datetime has no timezone information.
- An aware datetime has timezone information.
- Do not directly compare naive and aware datetime objects; Python raises `TypeError`.
- A fixed UTC offset does not represent every historical or future timezone rule.
- For full timezone database support, use `zoneinfo` (Python 3.9+).

### 8.4 Using zoneinfo

```python
from datetime import datetime
from zoneinfo import ZoneInfo

india_time = datetime.now(ZoneInfo("Asia/Kolkata"))
new_york_time = datetime.now(ZoneInfo("America/New_York"))

print("India:", india_time)
print("New York:", new_york_time)
```

This uses timezone database information. On some systems, the timezone database may need to be installed separately.

---

## 9. Working with the time Module

The `time` module provides functions for working with system time, timestamps and delays.

```python
import time
```

### 9.1 Get Current Timestamp

Use `time.time()`.

A timestamp represents the number of seconds since the Unix epoch (1970-01-01 00:00:00 UTC).

```python
import time

timestamp = time.time()

print(timestamp)
```

**Sample Output:**

```text
1793889000.123456
```

The exact value changes with time.

### 9.2 Convert Timestamp into Readable Time

```python
import time

timestamp = time.time()

result = time.ctime(timestamp)

print(result)
```

**Sample Output:**

```text
Thu Nov  5 14:30:00 2026
```

The output uses the local timezone.

### 9.3 Use localtime()

Converts a timestamp into a local time structure.

```python
import time

current = time.localtime()

print("Year:", current.tm_year)
print("Month:", current.tm_mon)
print("Day:", current.tm_mday)
print("Hour:", current.tm_hour)
print("Minute:", current.tm_min)
```

### 9.4 Format Time with time.strftime()

```python
import time

current = time.localtime()

formatted = time.strftime("%d-%m-%Y %I:%M %p", current)

print(formatted)
```

**Sample Output:**

```text
05-11-2026 02:30 PM
```

### 9.5 Delay Execution with sleep()

`sleep()` pauses the program for a specified number of seconds.

```python
import time

print("Start")

time.sleep(2)

print("End")
```

**Output:**

```text
Start
End
```

There is approximately a two-second delay between the messages.

### 9.6 Create a Countdown Timer

```python
import time

seconds = 5

while seconds > 0:
    print(seconds)
    time.sleep(1)
    seconds -= 1

print("Time Up!")
```

**Output:**

```text
5
4
3
2
1
Time Up!
```

### 9.7 Measure Execution Time with perf_counter()

`time.perf_counter()` is useful for measuring elapsed time.

```python
import time

start = time.perf_counter()

total = 0

for number in range(1, 1000001):
    total += number

end = time.perf_counter()

print("Total:", total)
print("Execution time:", end - start, "seconds")
```

**Sample Output:**

```text
Total: 500000500000
Execution time: 0.08 seconds
```

The execution time depends on the computer.

Use `perf_counter()` instead of `time.time()` for measuring short-duration performance.

---

## 10. Working with the calendar Module

Python's `calendar` module provides functions to inspect and display calendars.

```python
import calendar
```

### 10.1 Display a Full Year Calendar

```python
import calendar

print(calendar.calendar(2026))
```

This displays all twelve months of 2026.

### 10.2 Display a Specific Month

```python
import calendar

print(calendar.month(2026, 11))
```

**Output:**

```text
   November 2026
Mo Tu We Th Fr Sa Su
                   1
 2  3  4  5  6  7  8
 9 10 11 12 13 14 15
16 17 18 19 20 21 22
23 24 25 26 27 28 29
30
```

### 10.3 Check Whether a Year Is a Leap Year

```python
import calendar

year = 2024

if calendar.isleap(year):
    print("Leap year")
else:
    print("Not a leap year")
```

**Output:**

```text
Leap year
```

### 10.4 Count Leap Years in a Range

```python
import calendar

count = calendar.leapdays(2000, 2026)

print(count)
```

**Output:**

```text
7
```

The ending year is excluded from the range.

### 10.5 Get the Number of Days in a Month

```python
import calendar

year = 2026
month = 2

result = calendar.monthrange(year, month)

print("First weekday:", result[0])
print("Number of days:", result[1])
```

**Output:**

```text
First weekday: 6
Number of days: 28
```

The first weekday uses Monday = 0 and Sunday = 6.

### 10.6 Get Weekday Name

```python
import calendar

weekday = calendar.weekday(2026, 11, 5)

print(calendar.day_name[weekday])
```

**Output:**

```text
Thursday
```

### 10.7 Change the First Day of the Week

By default, Python calendars start with Monday.

```python
import calendar

calendar.setfirstweekday(calendar.SUNDAY)

print(calendar.month(2026, 11))
```

**Output begins with:**

```text
   November 2026
Su Mo Tu We Th Fr Sa
```

This changes the calendar module's first weekday setting for the current program.

### 10.8 Get Calendar Data as Lists

```python
import calendar

result = calendar.monthcalendar(2026, 11)

for week in result:
    print(week)
```

**Output:**

```text
[0, 0, 0, 0, 0, 0, 1]
[2, 3, 4, 5, 6, 7, 8]
[9, 10, 11, 12, 13, 14, 15]
[16, 17, 18, 19, 20, 21, 22]
[23, 24, 25, 26, 27, 28, 29]
[30, 0, 0, 0, 0, 0, 0]
```

Here, `0` represents a day outside the selected month.

---

## 11. Practical Date and Time Programs

### 11.1 Age Calculator

```python
from datetime import date

birth_year = int(input("Enter birth year: "))
birth_month = int(input("Enter birth month: "))
birth_day = int(input("Enter birth day: "))

today = date.today()
birth_date = date(birth_year, birth_month, birth_day)

if birth_date > today:
    print("Birth date cannot be in the future")
else:
    age = today.year - birth_date.year

    if (today.month, today.day) < (birth_date.month, birth_date.day):
        age -= 1

    print("Your age is:", age)
```

**Sample Output:**

```text
Enter birth year: 2000
Enter birth month: 5
Enter birth day: 10
Your age is: 26
```

The result depends on today's date.

### 11.2 Days Remaining Until a Date

```python
from datetime import date

today = date.today()
target = date(2026, 12, 31)

remaining = (target - today).days

if remaining > 0:
    print(remaining, "days remaining")
elif remaining == 0:
    print("Today is the target date")
else:
    print("Target date has passed")
```

### 11.3 Find the Next Birthday

```python
from datetime import date

today = date.today()

birth_month = int(input("Enter birth month: "))
birth_day = int(input("Enter birth day: "))

try:
    birthday = date(today.year, birth_month, birth_day)

    if birthday < today:
        birthday = date(today.year + 1, birth_month, birth_day)

    remaining = (birthday - today).days

    print("Next birthday:", birthday)
    print("Days remaining:", remaining)

except ValueError:
    print("Invalid birthday")
```

Note: This basic example needs an additional policy for birthdays on February 29 in non-leap years.

### 11.4 Calculate Employee Working Hours

```python
from datetime import datetime

start_time = input("Enter start time (HH:MM): ")
end_time = input("Enter end time (HH:MM): ")

start = datetime.strptime(start_time, "%H:%M")
end = datetime.strptime(end_time, "%H:%M")

if end < start:
    end += timedelta(days=1)

working_hours = (end - start).total_seconds() / 3600

print("Working hours:", working_hours)
```

**Important:** Add this import at the beginning:

```python
from datetime import datetime, timedelta
```

**Sample Output:**

```text
Enter start time (HH:MM): 09:00
Enter end time (HH:MM): 17:30
Working hours: 8.5
```

### 11.5 Find the Day of a Given Date

```python
from datetime import datetime

date_string = input("Enter date (DD-MM-YYYY): ")

try:
    result = datetime.strptime(date_string, "%d-%m-%Y")

    print("Day:", result.strftime("%A"))

except ValueError:
    print("Invalid date")
```

### 11.6 Generate a Monthly Calendar

```python
import calendar

year = int(input("Enter year: "))
month = int(input("Enter month: "))

if 1 <= month <= 12:
    print(calendar.month(year, month))
else:
    print("Invalid month")
```

### 11.7 Simple Stopwatch

```python
import time

input("Press Enter to start...")

start = time.perf_counter()

input("Press Enter to stop...")

end = time.perf_counter()

elapsed = end - start

print("Elapsed time:", round(elapsed, 2), "seconds")
```

### 11.8 Calculate the Number of Days Between Two Dates

```python
from datetime import datetime

date1 = input("Enter first date (DD-MM-YYYY): ")
date2 = input("Enter second date (DD-MM-YYYY): ")

try:
    first = datetime.strptime(date1, "%d-%m-%Y")
    second = datetime.strptime(date2, "%d-%m-%Y")

    difference = abs((second - first).days)

    print("Total difference:", difference, "days")

except ValueError:
    print("Please enter valid dates")
```

---

## 12. Common Date and Time Errors

### Error 1: Invalid Date

```python
from datetime import date

# February does not have 30 days.
date(2026, 2, 30)
```

Raises:

```text
ValueError
```

### Error 2: Incorrect Date Format

```python
from datetime import datetime

datetime.strptime("2026/11/05", "%d-%m-%Y")
```

Raises:

```text
ValueError
```

The input format and specified format must match.

### Error 3: Comparing Different Date-Time Types

A `date` object and a `datetime` object cannot always be compared directly.

Convert them to compatible types before comparison.

### Error 4: Confusing Timestamp and Formatted String

```python
import time

print(time.time())
print(time.ctime())
```

- `time.time()` returns a numeric timestamp.
- `time.ctime()` returns a readable string.

### Error 5: Ignoring Timezones

Comparing or calculating with different timezone assumptions can produce incorrect results.

Use timezone-aware datetime objects when working with real-world events across timezones.

---

## 13. Practical Exercises

### Exercise 1: datetime Basics

1. Print the current date.
2. Print the current date and time.
3. Create a custom date.
4. Display year, month and day separately.
5. Display the current weekday.
6. Create a custom time object.

### Exercise 2: Date Formatting

1. Display the date in `DD-MM-YYYY` format.
2. Display the full month name.
3. Display the weekday name.
4. Display time in 12-hour format.
5. Convert a date string into a datetime object.
6. Convert a datetime object into a formatted string.

### Exercise 3: timedelta

1. Add 30 days to today's date.
2. Subtract 15 days from a date.
3. Find the date after 10 weeks.
4. Calculate the difference between two dates.
5. Calculate the total duration between two times.
6. Find how many days remain until New Year.

### Exercise 4: time Module

1. Display the current timestamp.
2. Convert a timestamp into readable local time.
3. Create a countdown timer.
4. Pause program execution for five seconds.
5. Measure the execution time of a loop.
6. Create a simple stopwatch.

### Exercise 5: calendar Module

1. Display the calendar of the current year.
2. Display a selected month.
3. Check whether a year is a leap year.
4. Find the number of days in a month.
5. Find the weekday of a particular date.
6. Display a calendar starting from Sunday.

---

## 14. Mini Project – Date and Time Utility System

### Project Description

Create a menu-driven application that provides different date and time utilities.

### Project Requirements

The program should provide:

1. Display current date and time.
2. Display formatted date.
3. Calculate age.
4. Calculate days between two dates.
5. Find the next birthday.
6. Display a monthly calendar.
7. Check leap year.
8. Start a countdown timer.
9. Measure elapsed time using a stopwatch.
10. Exit the program.

### Step 1: Create Project File

```text
date_time_utility.py
```

### Step 2: Import Required Modules

```python
from datetime import date, datetime, timedelta
import time
import calendar
```

### Step 3: Create Current Date Function

```python
def show_current_datetime():
    current = datetime.now()

    print("\nCurrent Date and Time:", current)
    print("Formatted:", current.strftime("%d-%m-%Y %I:%M:%S %p"))
```

### Step 4: Create Age Calculator Function

```python
def calculate_age():
    try:
        birth_date = input("Enter birth date (DD-MM-YYYY): ")

        birth = datetime.strptime(birth_date, "%d-%m-%Y").date()
        today = date.today()

        if birth > today:
            print("Birth date cannot be in the future")
            return

        age = today.year - birth.year

        if (today.month, today.day) < (birth.month, birth.day):
            age -= 1

        print("Your age:", age)

    except ValueError:
        print("Invalid date")
```

### Step 5: Create Date Difference Function

```python
def calculate_date_difference():
    try:
        first = input("Enter first date (DD-MM-YYYY): ")
        second = input("Enter second date (DD-MM-YYYY): ")

        date1 = datetime.strptime(first, "%d-%m-%Y").date()
        date2 = datetime.strptime(second, "%d-%m-%Y").date()

        difference = abs((date2 - date1).days)

        print("Difference:", difference, "days")

    except ValueError:
        print("Invalid date format")
```

### Step 6: Create Monthly Calendar Function

```python
def show_calendar():
    try:
        year = int(input("Enter year: "))
        month = int(input("Enter month: "))

        if not 1 <= month <= 12:
            print("Invalid month")
            return

        print(calendar.month(year, month))

    except ValueError:
        print("Please enter valid numeric values")
```

### Step 7: Create Leap Year Function

```python
def check_leap_year():
    try:
        year = int(input("Enter year: "))

        if calendar.isleap(year):
            print("Leap year")
        else:
            print("Not a leap year")

    except ValueError:
        print("Invalid year")
```

### Step 8: Create Countdown Function

```python
def countdown():
    try:
        seconds = int(input("Enter countdown seconds: "))

        if seconds < 0:
            print("Enter a positive number")
            return

        while seconds > 0:
            print(seconds)
            time.sleep(1)
            seconds -= 1

        print("Time Up!")

    except ValueError:
        print("Invalid input")
```

### Step 9: Create Stopwatch Function

```python
def stopwatch():
    input("Press Enter to start...")
    start = time.perf_counter()

    input("Press Enter to stop...")
    end = time.perf_counter()

    print("Elapsed time:", round(end - start, 2), "seconds")
```

### Step 10: Create Main Menu

```python
def main():
    while True:
        print("\n===== DATE AND TIME UTILITY SYSTEM =====")

        print("1. Current Date and Time")
        print("2. Calculate Age")
        print("3. Date Difference")
        print("4. Monthly Calendar")
        print("5. Check Leap Year")
        print("6. Countdown Timer")
        print("7. Stopwatch")
        print("8. Exit")

        choice = input("Enter your choice: ")

        if choice == "1":
            show_current_datetime()

        elif choice == "2":
            calculate_age()

        elif choice == "3":
            calculate_date_difference()

        elif choice == "4":
            show_calendar()

        elif choice == "5":
            check_leap_year()

        elif choice == "6":
            countdown()

        elif choice == "7":
            stopwatch()

        elif choice == "8":
            print("Thank you for using the system!")
            break

        else:
            print("Invalid choice. Try again.")


if __name__ == "__main__":
    main()
```

### Step 11: Run the Project

```bash
python date_time_utility.py
```

**Sample Output:**

```text
===== DATE AND TIME UTILITY SYSTEM =====

1. Current Date and Time
2. Calculate Age
3. Date Difference
4. Monthly Calendar
5. Check Leap Year
6. Countdown Timer
7. Stopwatch
8. Exit

Enter your choice: 5

Enter year: 2024
Leap year
```

### Project Challenges

1. Add a next-birthday calculator.
2. Add a function to calculate the remaining days until a deadline.
3. Display the current UTC and India time.
4. Add an option to format dates in multiple formats.
5. Save calculation history in a text file.
6. Handle invalid inputs without crashing.
7. Add a menu option to display the full yearly calendar.

---

## 15. Trainer Assessment

Ask the student:

1. What is the purpose of the `datetime` module?
2. What is the difference between `date` and `datetime`?
3. What does `datetime.now()` return?
4. What is the difference between `strftime()` and `strptime()`?
5. What is a `timedelta` object?
6. How can we calculate the difference between two dates?
7. What is a timestamp?
8. What is the purpose of `time.sleep()`?
9. Why do we use `time.perf_counter()`?
10. What is the purpose of the `calendar` module?
11. How can we check whether a year is a leap year?
12. What is the difference between naive and aware datetime objects?
13. What is the purpose of timezone information?
14. What does `calendar.monthrange()` return?
15. Why should we use `total_seconds()` for complete duration calculations?

### Practical Assessment

Ask the student to independently:

- Display the current date and time.
- Convert a string into a date.
- Format a date in multiple formats.
- Calculate age.
- Calculate the difference between dates.
- Create a countdown timer.
- Display a monthly calendar.
- Complete the Date and Time Utility System.

---

## 16. Completion Criteria

The student should be able to:

- Work with the `datetime`, `time` and `calendar` modules.
- Create and inspect date and time objects.
- Format and parse date-time strings.
- Perform date calculations using `timedelta`.
- Compare dates and calculate durations.
- Understand timestamps and timezones.
- Measure execution time.
- Create countdown timers and stopwatches.
- Display and inspect monthly and yearly calendars.
- Build a menu-driven date and time utility application.

**Day 35 Completed: Date, Time & Calendar.**

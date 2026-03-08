# Chapter 1: Python Basics
### *Complete In-Depth Notes — Cybersecurity Edition*

---

## 📋 TOPICS WE'LL COVER IN THIS CHAPTER

```
1. Entering Expressions into the Interactive Shell
2. The Integer, Floating-Point, and String Data Types
3. String Concatenation and Replication
4. Storing Values in Variables
   ├── Assignment Statements
   └── Variable Names
5. Your First Program
6. Dissecting Your Program
   ├── Comments
   ├── The print() Function
   ├── The input() Function
   ├── Printing the User's Name
   ├── The len() Function
   └── The str(), int(), and float() Functions
```

---

# 1. ENTERING EXPRESSIONS INTO THE INTERACTIVE SHELL

## What is the Interactive Shell?

When you open **IDLE** (Python's built-in editor), you get two environments:

```
┌──────────────────────────────────────────┐
│  INTERACTIVE SHELL  →  Type & run        │
│                         instantly        │
│  FILE EDITOR       →  Write full scripts │
│                         & save them      │
└──────────────────────────────────────────┘
```

The shell shows `>>>` — this is called the **prompt**. You type an expression, press Enter, and Python immediately evaluates it.

---

## What is an Expression?

An **expression** is any combination of **values** and **operators** that Python can evaluate down to a single value.

```python
>>> 2 + 2
4

>>> 10 - 3
7

>>> 6 * 9
54

>>> 22 / 7
3.142857142857143

>>> 2 ** 10        # 2 to the power of 10
1024

>>> 17 % 3         # Modulo — remainder after division
2
```

---

## All Arithmetic Operators

| Operator | Operation | Example | Result |
|----------|-----------|---------|--------|
| `+` | Addition | `5 + 3` | `8` |
| `-` | Subtraction | `9 - 4` | `5` |
| `*` | Multiplication | `4 * 3` | `12` |
| `/` | Division | `10 / 4` | `2.5` |
| `//` | Integer Division | `10 // 4` | `2` |
| `%` | Modulo (Remainder) | `10 % 3` | `1` |
| `**` | Exponent | `2 ** 8` | `256` |

---

## 🛡️ Cybersecurity Relevance — Modulo & Exponent

```python
# Modulo is used heavily in cryptography
# Example: Caesar Cipher shift calculation
shift = 3
char_code = ord('Z')        # ord() gets ASCII value → 90
shifted = (char_code - 65 + shift) % 26 + 65
print(chr(shifted))         # chr() converts back → 'C'

# Exponents are the backbone of RSA encryption
# 2**256 is the keyspace of many encryption algorithms
print(2 ** 256)             # A number with 77 digits
```

---

## Order of Operations (PEMDAS)

Python follows standard math order:

```python
>>> 2 + 3 * 6        # Multiplication first
20

>>> (2 + 3) * 6      # Parentheses first
30

>>> 2 ** 3 ** 2      # Exponent right-to-left → 2 ** 9
512
```

**Order:** Parentheses → Exponents → Multiplication/Division → Addition/Subtraction

---

# 2. THE INTEGER, FLOATING-POINT, AND STRING DATA TYPES

## What is a Data Type?

A **data type** tells Python what kind of value something is and what operations are valid on it.

```
┌─────────────────────────────────────────────────────┐
│  THREE CORE DATA TYPES IN CHAPTER 1                 │
│                                                     │
│  INTEGER  (int)   →  Whole numbers   →  42, -7, 0  │
│  FLOAT    (float) →  Decimal numbers →  3.14, -0.5 │
│  STRING   (str)   →  Text            →  "hello"    │
└─────────────────────────────────────────────────────┘
```

---

## Integers (`int`)

Whole numbers — positive, negative, or zero. **No decimal point.**

```python
>>> type(42)
<class 'int'>

>>> type(-100)
<class 'int'>

>>> type(0)
<class 'int'>
```

---

## Floating-Point Numbers (`float`)

Numbers **with** a decimal point.

```python
>>> type(3.14)
<class 'float'>

>>> type(-0.001)
<class 'float'>

>>> type(2.0)          # Even though it's "whole", the dot makes it float
<class 'float'>
```

### ⚠️ Important Float Behavior

```python
>>> 0.1 + 0.2
0.30000000000000004    # Floating point imprecision — critical to know!
```

This is a fundamental limitation of how computers store decimals in binary. This matters in **cryptographic calculations** where precision is critical.

---

## Strings (`str`)

Any text wrapped in **single** or **double** quotes.

```python
>>> type("hello")
<class 'str'>

>>> type('world')
<class 'str'>

>>> type("42")          # This is a STRING not an integer!
<class 'str'>
```

### Rules for Strings

```python
# Single quotes
'This is a string'

# Double quotes
"This is also a string"

# You can use one type to contain the other
"It's a valid string"       # Single quote INSIDE double quotes ✅
'He said "hello"'           # Double quotes INSIDE single quotes ✅

# Mismatching causes an error
'It's broken'               # ❌ SyntaxError — Python thinks string ends at "It"
```

---

# 3. STRING CONCATENATION AND REPLICATION

## String Concatenation — Joining Strings

The `+` operator **joins** strings together when used with string values.

```python
>>> "Hello" + " " + "World"
'Hello World'

>>> "cyber" + "security"
'cybersecurity'

>>> "password" + "123"
'password123'
```

### ⚠️ Critical Rule — No Mixing Types

```python
>>> "The answer is " + 42          # ❌ TypeError
TypeError: can only concatenate str (not "int") to str

>>> "The answer is " + str(42)     # ✅ Convert first
'The answer is 42'
```

---

## String Replication — Repeating Strings

The `*` operator **repeats** a string when used with a string and an integer.

```python
>>> "Ha" * 3
'HaHaHa'

>>> "-" * 50               # Create a divider line
'--------------------------------------------------'

>>> "A" * 5
'AAAAA'
```

### 🛡️ Cybersecurity Use — Replication

```python
# Creating padding in network packet analysis
header = "=" * 40
print(header)
print("PACKET CAPTURE RESULTS")
print(header)

# Brute force character generation concept
charset = "abc"
print(charset[0] * 3)    # 'aaa' — basics of brute force thinking
```

---

# 4. STORING VALUES IN VARIABLES

## What is a Variable?

A **variable** is a named storage location in memory that holds a value. Think of it as a labeled box.

```
┌─────────┐          ┌───────────────┐
│  name   │  ──────► │   "Alice"     │  ← Value stored in memory
└─────────┘          └───────────────┘
   Label                   Box
```

---

## Assignment Statements

The `=` sign is the **assignment operator**. It stores a value into a variable.

```
variable_name = value
```

```python
>>> spam = 42
>>> spam
42

>>> name = "Alice"
>>> name
'Alice'

>>> pi = 3.14159
>>> pi
3.14159
```

### Variables Can Be Reassigned

```python
>>> spam = 42
>>> spam = spam + 1      # Take old value, add 1, store back
>>> spam
43

>>> spam = 100           # Completely replace old value
>>> spam
100
```

### Multiple Variables

```python
>>> target_ip = "192.168.1.1"
>>> port = 80
>>> protocol = "HTTP"
>>> is_open = True

>>> target_ip
'192.168.1.1'
```

---

## Variable Names — Rules & Conventions

### Hard Rules (Breaking these = Error)

| Rule | Valid | Invalid |
|------|-------|---------|
| Letters, numbers, underscores only | `my_var` | `my-var` ❌ |
| Cannot start with a number | `var1` | `1var` ❌ |
| Cannot be a Python keyword | `myList` | `list` ❌ |
| Case sensitive | `spam` ≠ `Spam` | — |

### Python Reserved Keywords (Cannot use as variable names)

```python
False    None     True     and      as       assert
async    await    break    class    continue  def
del      elif     else     except   finally   for
from     global   if       import   in        is
lambda   nonlocal not      or       pass      raise
return   try      while    with     yield
```

### Naming Conventions

```python
# ✅ Good — snake_case (Python standard)
target_ip = "192.168.1.1"
open_port = 443
scan_result = True

# ✅ Also valid — camelCase (common in other languages)
targetIp = "192.168.1.1"

# ❌ Bad — vague names
x = "192.168.1.1"
a = 443

# 🛡️ Cybersecurity naming examples
victim_host = "10.0.0.5"
payload_size = 1024
hash_value = "5f4dcc3b5aa765d61d8327deb882cf99"
encrypted_data = ""
```

---

# 5. YOUR FIRST PROGRAM

Here is the first complete program from the book. Let's build it and fully understand every line.

```python
# This program says hello and asks for my name.

print("Hello, world!")
print("What is your name?")    # Ask for their name
myName = input()
print("It is good to meet you, " + myName)
print("The length of your name is:")
print(len(myName))
print("What is your age?")
myAge = input()
print("You will be " + str(int(myAge) + 1) + " in a year.")
```

**Sample Run:**
```
Hello, world!
What is your name?
Alice
It is good to meet you, Alice
The length of your name is:
5
What is your age?
27
You will be 28 in a year.
```

---

# 6. DISSECTING YOUR PROGRAM

## Comments

A **comment** is a note in your code for humans — Python completely ignores it.

```python
# This is a single-line comment

# Everything after the # symbol is ignored by Python
x = 5    # You can add comments at the end of a line too
```

### Why Comments Matter in Security Scripts

```python
# TARGET: Internal network range
# PURPOSE: Authorized penetration test - Client XYZ
# DATE: 2024-01-15
# AUTHOR: Security Team

target_range = "192.168.1.0/24"    # /24 = 256 addresses
scan_type = "SYN"                   # Stealth scan type
```

Good commenting habits are **essential** in security work — you must document what your tools do and why, especially for legal/audit purposes.

---

## The `print()` Function

`print()` displays output to the screen.

```python
print("Hello, world!")              # Print a string
print(42)                           # Print an integer
print(3.14)                         # Print a float
print("Value:", 42)                 # Print multiple items (comma-separated)
print()                             # Print a blank line
```

### print() with `end` and `sep` Parameters

```python
# Default behavior adds newline at end
print("Line 1")
print("Line 2")
# Output:
# Line 1
# Line 2

# Change end character
print("Line 1", end=" ")
print("Line 2")
# Output: Line 1 Line 2

# Change separator between items
print("192", "168", "1", "1", sep=".")
# Output: 192.168.1.1   ← Useful for IP formatting!
```

---

## The `input()` Function

`input()` **pauses** the program and waits for the user to type something and press Enter. It **always returns a string.**

```python
myName = input()                    # Basic input, no prompt
myName = input("Enter your name: ") # With a prompt message
```

### ⚠️ Critical Rule — input() ALWAYS Returns a String

```python
age = input("Enter your age: ")
print(type(age))                    # <class 'str'> — even if you type 25!

# This will FAIL:
age = input("Enter age: ")
print(age + 1)                      # ❌ TypeError — can't add str + int

# This is CORRECT:
age = input("Enter age: ")
print(int(age) + 1)                 # ✅ Convert to int first
```

### 🛡️ Cybersecurity Use — Input for Tools

```python
# Building an interactive security tool
target = input("Enter target IP address: ")
port = input("Enter port to scan: ")
print("Scanning " + target + " on port " + port + "...")
```

---

## Printing the User's Name

```python
myName = input("What is your name? ")
print("It is good to meet you, " + myName)
```

The `+` here concatenates the fixed string with the variable's value.

```
What is your name? Bob
It is good to meet you, Bob
```

---

## The `len()` Function

`len()` returns the **number of characters** in a string (including spaces).

```python
>>> len("hello")
5

>>> len("cybersecurity")
13

>>> len("")                 # Empty string
0

>>> len("192.168.1.1")      # IP address length
11

>>> myName = "Alice"
>>> len(myName)
5
```

### ⚠️ len() Only Works on Strings and Sequences

```python
>>> len(42)                 # ❌ TypeError — integers have no length
TypeError: object of type 'int' has no len()

>>> len("42")               # ✅ String "42" has length 2
2
```

### 🛡️ Cybersecurity Use — len()

```python
password = input("Enter password: ")

if len(password) < 8:
    print("WEAK: Password too short!")
elif len(password) < 12:
    print("MODERATE: Consider a longer password")
else:
    print("OK: Password length is acceptable")
```

---

## The `str()`, `int()`, and `float()` Functions

These are **type conversion** functions — they convert values from one data type to another.

### `str()` — Convert to String

```python
>>> str(42)
'42'

>>> str(3.14)
'3.14'

>>> str(True)
'True'

# Essential for concatenation
age = 25
print("I am " + str(age) + " years old.")   # ✅
```

### `int()` — Convert to Integer

```python
>>> int("42")
42

>>> int(3.99)          # Truncates — does NOT round
3

>>> int(True)          # True = 1 in Python
1

>>> int(False)         # False = 0 in Python
0
```

### ⚠️ int() Will Crash on Invalid Input

```python
>>> int("hello")       # ❌ ValueError
ValueError: invalid literal for int() with base 10: 'hello'

>>> int("3.14")        # ❌ ValueError — can't convert decimal string to int directly
ValueError: invalid literal for int() with base 10: '3.14'

>>> int(float("3.14")) # ✅ Convert to float first, then int
3
```

### `float()` — Convert to Float

```python
>>> float("3.14")
3.14

>>> float(42)
42.0

>>> float("42")
42.0
```

### Complete Conversion Reference

```
┌──────────────────────────────────────────────────────┐
│  CONVERSION TABLE                                    │
│                                                      │
│  str(42)        →  "42"      int to str             │
│  str(3.14)      →  "3.14"    float to str           │
│  int("42")      →  42        str to int             │
│  int(3.99)      →  3         float to int (truncate)│
│  float("3.14")  →  3.14      str to float           │
│  float(42)      →  42.0      int to float           │
└──────────────────────────────────────────────────────┘
```

---

## Putting It All Together — Age Calculator (Annotated)

```python
print("What is your age?")
myAge = input()                      # Returns string e.g. "27"
print("You will be " + str(int(myAge) + 1) + " in a year.")
```

**Breaking down `str(int(myAge) + 1)` step by step:**

```
myAge = "27"                → input() always returns a string
int(myAge) = 27             → convert string "27" to integer 27
int(myAge) + 1 = 28         → perform arithmetic
str(28) = "28"              → convert back to string for concatenation
"You will be " + "28" + " in a year." → final concatenation
```

---

# 🛡️ CHAPTER 1 — CYBERSECURITY MINI PROJECT

## Simple Target Information Gatherer

```python
# ==========================================
# TARGET INFO GATHERER v1.0
# Purpose: Practice tool - Authorized use only
# ==========================================

print("=" * 45)
print("       TARGET INFORMATION GATHERER")
print("=" * 45)

# Gather information
target_name = input("Enter target hostname: ")
target_ip = input("Enter target IP address: ")
port = input("Enter port number: ")
analyst = input("Analyst name: ")

# Display report
print()
print("-" * 45)
print("SCAN REPORT")
print("-" * 45)
print("Analyst    : " + analyst)
print("Target     : " + target_name)
print("IP Address : " + target_ip)
print("Port       : " + port)
print("IP Length  : " + str(len(target_ip)) + " characters")
print("Host Length: " + str(len(target_name)) + " characters")
print("-" * 45)
```

**Sample Output:**
```
=============================================
       TARGET INFORMATION GATHERER
=============================================
Enter target hostname: example.com
Enter target IP address: 93.184.216.34
Enter port number: 443
Analyst name: Alice

---------------------------------------------
SCAN REPORT
---------------------------------------------
Analyst    : Alice
Target     : example.com
IP Address : 93.184.216.34
Port       : 443
IP Length  : 13 characters
Host Length: 11 characters
---------------------------------------------
```

---

# ⚠️ COMMON ERRORS IN CHAPTER 1

| Error | Cause | Fix |
|-------|-------|-----|
| `TypeError: can only concatenate str` | Mixing str + int | Use `str()` to convert |
| `ValueError: invalid literal for int()` | Passing non-numeric string to int() | Validate input first |
| `NameError: name 'x' is not defined` | Using variable before assigning it | Assign before use |
| `SyntaxError: EOL while scanning string` | Unclosed quote | Close all quote marks |

---

# 📝 CHAPTER 1 SUMMARY

```
✅ Expressions — values + operators evaluated by Python
✅ Data Types — int, float, str (and how to check with type())
✅ Operators — +, -, *, /, //, %, **
✅ Concatenation — joining strings with +
✅ Replication — repeating strings with *
✅ Variables — named storage, assignment with =
✅ Variable naming rules — snake_case, no keywords, no starting with numbers
✅ print() — output to screen, with end= and sep= options
✅ input() — always returns a string, pauses for user input
✅ len() — counts characters in a string
✅ str(), int(), float() — type conversion functions
```

---

# 🧪 PRACTICE EXERCISES

**Exercise 1:** Write a program that asks for a username and password, then prints both along with the total combined character length.

**Exercise 2:** Ask for two numbers, convert them to integers, and print their sum, difference, product, and the remainder when the first is divided by the second.

**Exercise 3:** Build a basic "target profile" tool that collects: IP address, hostname, open port, and operating system — then displays it as a formatted report.
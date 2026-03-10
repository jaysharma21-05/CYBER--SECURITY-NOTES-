# Chapter 2: Flow Control
### *Complete In-Depth Notes — Cybersecurity Edition*

---

## 📋 TOPICS WE'LL COVER IN THIS CHAPTER

```
1. Boolean Values
2. Comparison Operators
3. Boolean Operators
   ├── Binary Boolean Operators (and, or)
   └── The not Operator
4. Mixing Boolean and Comparison Operators
5. Elements of Flow Control
   ├── Conditions
   └── Blocks of Code
6. Program Execution
7. Flow Control Statements
   ├── if Statements
   ├── else Statements
   ├── elif Statements
   ├── while Loop Statements
   ├── break Statements
   ├── continue Statements
   └── for Loops and range()
8. Importing Modules
9. Ending a Program with sys.exit()
```

---

# 1. BOOLEAN VALUES

## What is a Boolean?

A **Boolean** is a data type that has only **two possible values:**

```python
True
False
```

> ⚠️ Capital T and F — this is mandatory in Python

```python
>>> type(True)
<class 'bool'>

>>> type(False)
<class 'bool'>

# Booleans are actually integers underneath
>>> int(True)
1
>>> int(False)
0
```

---

## Why Booleans Matter

Every decision your program makes comes down to a Boolean.

```
┌─────────────────────────────────────────────┐
│  Is the port open?        →  True / False   │
│  Is the password correct? →  True / False   │
│  Is the IP in range?      →  True / False   │
│  Did the login succeed?   →  True / False   │
└─────────────────────────────────────────────┘
```

```python
port_open = True
login_success = False
is_admin = True

print(port_open)        # True
print(login_success)    # False
```

---

# 2. COMPARISON OPERATORS

Comparison operators **compare two values** and always return a Boolean (`True` or `False`).

## All Comparison Operators

| Operator | Meaning | Example | Result |
|----------|---------|---------|--------|
| `==` | Equal to | `5 == 5` | `True` |
| `!=` | Not equal to | `5 != 3` | `True` |
| `<` | Less than | `3 < 5` | `True` |
| `>` | Greater than | `5 > 3` | `True` |
| `<=` | Less than or equal | `5 <= 5` | `True` |
| `>=` | Greater than or equal | `6 >= 5` | `True` |

---

## Examples in the Shell

```python
>>> 42 == 42
True

>>> 42 == 99
False

>>> 42 != 99
True

>>> 10 > 5
True

>>> 10 < 5
False

>>> 10 >= 10
True

>>> 10 <= 9
False
```

---

## ⚠️ Critical Distinction — `=` vs `==`

```python
# = is ASSIGNMENT — stores a value
spam = 42           # Store 42 into spam

# == is COMPARISON — checks if equal
spam == 42          # Ask: is spam equal to 42? → True
```

```python
# This is one of the MOST COMMON beginner mistakes
if spam = 42:       # ❌ SyntaxError — cannot assign inside if
if spam == 42:      # ✅ Correct comparison
```

---

## Comparing Different Data Types

```python
>>> 42 == "42"          # int vs string
False                   # Different types are never equal

>>> 42 == 42.0          # int vs float
True                    # Same value, different type — True

>>> True == 1           # Boolean vs int
True

>>> False == 0
True
```

---

## 🛡️ Cybersecurity Use — Comparisons

```python
# Port range validation
port = int(input("Enter port number : "))
print(port >= 1)          # Is it a valid port?
print(port <= 65535)      # Is it within valid range?

# Password length check
password = input("Enter password : ")
print(len(password) >= 8)     # True if strong enough

# IP octet validation
octet = int(input("Enter IP octet : "))
print(octet >= 0)
print(octet <= 255)
```

---

# 3. BOOLEAN OPERATORS

Boolean operators combine or modify Boolean values.

```
Three Boolean Operators:
├── and
├── or
└── not
```

---

## `and` Operator

Returns `True` only if **BOTH** sides are `True`.

### Truth Table — `and`

| A | B | A and B |
|---|---|---------|
| True | True | **True** |
| True | False | False |
| False | True | False |
| False | False | False |

```python
>>> True and True
True

>>> True and False
False

>>> False and True
False

>>> False and False
False
```

### Real Example:

```python
>>> (5 > 3) and (10 > 7)
True                        # Both True → True

>>> (5 > 3) and (10 > 20)
False                       # One is False → False
```

---

## `or` Operator

Returns `True` if **AT LEAST ONE** side is `True`.

### Truth Table — `or`

| A | B | A or B |
|---|---|--------|
| True | True | True |
| True | False | **True** |
| False | True | **True** |
| False | False | False |

```python
>>> True or False
True

>>> False or False
False

>>> False or True
True
```

---

## `not` Operator

**Reverses** the Boolean value. `True` becomes `False`, `False` becomes `True`.

```python
>>> not True
False

>>> not False
True

>>> not (5 > 3)
False                   # 5 > 3 is True → not True → False
```

---

## 🛡️ Cybersecurity Use — Boolean Operators

```python
# Valid port check — must be between 1 AND 65535
port = 443
is_valid = (port >= 1) and (port <= 65535)
print(is_valid)             # True

# Check if port is well-known OR registered
is_well_known = (port >= 1) and (port <= 1023)
is_registered = (port >= 1024) and (port <= 49151)
is_notable = is_well_known or is_registered
print(is_notable)           # True

# Check if port is NOT open
port_open = False
port_closed = not port_open
print(port_closed)          # True
```

---

# 4. MIXING BOOLEAN AND COMPARISON OPERATORS

You can chain comparisons and boolean operators together for complex conditions.

```python
>>> (4 < 5) and (5 < 6)
True

>>> (4 < 5) and (9 < 6)
False

>>> (1 == 2) or (2 == 2)
True

>>> not (1 == 2)
True
```

## Order of Evaluation

```
Priority (highest to lowest):
1. Comparison operators  →  ==, !=, <, >, <=, >=
2. not
3. and
4. or
```

```python
>>> True or False and False
True        # 'and' evaluates first → False and False = False
            # Then → True or False = True

>>> (True or False) and False
False       # Parentheses first → True and False = False
```

---

# 5. ELEMENTS OF FLOW CONTROL

## What is Flow Control?

By default Python runs code **line by line, top to bottom.** Flow control lets you **change that order** — skip lines, repeat lines, branch different paths.

```
┌─────────────────────────────────────────────┐
│  Normal flow  →  Line 1, 2, 3, 4, 5...      │
│                                             │
│  Flow control →  Line 1, 2, skip 3,         │
│                  repeat 4 five times,        │
│                  jump to line 8...           │
└─────────────────────────────────────────────┘
```

---

## Conditions

A **condition** is any expression that evaluates to `True` or `False`. It's what goes inside `if`, `while` etc.

```python
# These are all valid conditions:
spam == 10
password != "admin"
port >= 1 and port <= 65535
len(username) > 0
is_admin == True
is_admin              # Same as is_admin == True
```

---

## Blocks of Code

A **block** is a group of lines that belong together, defined by **indentation** (4 spaces or 1 tab).

```python
if condition:
    # This is a block
    # All these lines are indented
    # They run together or not at all
    line_1
    line_2
    line_3
# Back to no indent = outside the block
```

### Rules for Blocks:

```
1. Blocks begin when indentation INCREASES
2. Blocks end when indentation DECREASES
3. Blocks can contain other blocks (nested)
```

```python
if True:
    print("Block 1 - line 1")      # Block 1
    print("Block 1 - line 2")      # Block 1
    if True:
        print("Block 2 - nested")  # Block 2 (nested inside Block 1)
    print("Block 1 - line 4")      # Back to Block 1
print("Outside all blocks")        # No block
```

---

# 6. PROGRAM EXECUTION

```python
# Python starts here — line 1
print("Start")          # Line 1 — executes
print("Middle")         # Line 2 — executes
print("End")            # Line 3 — executes
# Program ends here
```

Flow control **redirects** this execution path based on conditions.

---

# 7. FLOW CONTROL STATEMENTS

---

## `if` Statements

The most basic flow control. Run a block of code **only if** a condition is `True`.

### Syntax:

```python
if condition:
    # code to run if condition is True
```

```python
# Basic example
spam = 10

if spam == 10:
    print("spam is ten")        # This runs

if spam == 99:
    print("spam is 99")         # This does NOT run
```

### 🛡️ Cybersecurity Example:

```python
password = input("Enter password : ")

if len(password) < 8:
    print("WARNING: Password is too short!")

if password == "admin":
    print("CRITICAL: Default password detected!")

if password == "password":
    print("CRITICAL: Extremely weak password!")
```

---

## `else` Statements

Runs when the `if` condition is `False` — the **alternative path.**

### Syntax:

```python
if condition:
    # runs if condition is True
else:
    # runs if condition is False
```

```python
password = input("Enter password : ")

if len(password) >= 8:
    print("Password length is acceptable")
else:
    print("Password is too short!")
```

```python
port = int(input("Enter port : "))

if port >= 1 and port <= 65535:
    print("Valid port number")
else:
    print("Invalid port number!")
```

---

## `elif` Statements

Stands for **"else if"** — check multiple conditions in sequence.

### Syntax:

```python
if condition1:
    # runs if condition1 is True
elif condition2:
    # runs if condition1 False AND condition2 True
elif condition3:
    # runs if condition1,2 False AND condition3 True
else:
    # runs if ALL conditions are False
```

### ⚠️ Key Rule — Only ONE block runs:

```python
# Python checks top to bottom
# The FIRST True condition wins
# All others are SKIPPED
```

```python
score = 75

if score >= 90:
    print("Grade: A")
elif score >= 80:
    print("Grade: B")
elif score >= 70:
    print("Grade: C")        # ← This runs (75 >= 70 is True)
elif score >= 60:
    print("Grade: D")        # ← Skipped even though 75 >= 60
else:
    print("Grade: F")
```

### 🛡️ Cybersecurity Example — Port Classifier:

```python
port = int(input("Enter port number : "))

if port < 1 or port > 65535:
    print("INVALID port number")
elif port <= 1023:
    print("WELL-KNOWN port (System port)")
    print("Requires admin/root privileges")
elif port <= 49151:
    print("REGISTERED port (User port)")
elif port <= 65535:
    print("DYNAMIC/PRIVATE port (Ephemeral)")
```

**Sample Runs:**
```
Enter port number : 80
WELL-KNOWN port (System port)
Requires admin/root privileges

Enter port number : 8080
REGISTERED port (User port)

Enter port number : 52341
DYNAMIC/PRIVATE port (Ephemeral)
```

---

## `while` Loop Statements

Repeats a block of code **as long as** a condition remains `True`.

### Syntax:

```python
while condition:
    # code to repeat
```

```python
# Basic countdown
count = 5

while count > 0:
    print("Count: " + str(count))
    count = count - 1       # MUST change condition or loops forever!

print("Done!")
```

**Output:**
```
Count: 5
Count: 4
Count: 3
Count: 2
Count: 1
Done!
```

### ⚠️ Infinite Loop — Dangerous!

```python
# ❌ This runs FOREVER — condition never becomes False
while True:
    print("This never stops!")

# Press Ctrl+C to force stop a runaway program
```

### Useful Infinite Loop with Break:

```python
# Keep asking until valid input received
while True:
    port = int(input("Enter port (1-65535) : "))
    if port >= 1 and port <= 65535:
        break               # Exit the loop
    print("Invalid! Try again.")

print("Valid port entered: " + str(port))
```

---

### 🛡️ Cybersecurity Example — Login Attempt Limiter:

```python
# Simulate login with max 3 attempts
correct_password = "secure123"
attempts = 0
max_attempts = 3

while attempts < max_attempts:
    password = input("Enter password : ")
    attempts = attempts + 1

    if password == correct_password:
        print("✅ Access Granted!")
        break
    else:
        remaining = max_attempts - attempts
        if remaining > 0:
            print("❌ Wrong password! " + str(remaining) + " attempts left.")
        
if attempts == max_attempts and password != correct_password:
    print("🔒 Account locked! Max attempts reached.")
```

**Sample Run:**
```
Enter password : hello
❌ Wrong password! 2 attempts left.
Enter password : test
❌ Wrong password! 1 attempts left.
Enter password : abc
🔒 Account locked! Max attempts reached.
```

---

## `break` Statements

**Immediately exits** the loop — no condition check, just jumps out.

```python
while True:
    user_input = input("Type 'quit' to exit : ")
    if user_input == "quit":
        break                   # Exit loop immediately
    print("You typed: " + user_input)

print("Loop exited")
```

---

## `continue` Statements

**Skips the rest** of the current iteration and goes back to the top of the loop.

```python
# Print numbers 1-10, skip multiples of 3
num = 0

while num < 10:
    num = num + 1
    if num % 3 == 0:
        continue            # Skip print, go back to while check
    print(num)
```

**Output:** `1 2 4 5 7 8 10` (3, 6, 9 are skipped)

### 🛡️ Cybersecurity Use — continue:

```python
# Scan ports but skip known safe ones
port = 0

while port < 100:
    port = port + 1
    if port == 80 or port == 443:
        continue            # Skip these ports
    print("Checking port: " + str(port))
```

---

## `for` Loops and `range()`

A `for` loop runs a block of code **a specific number of times.**

### Syntax:

```python
for variable in range(n):
    # runs n times
```

```python
# Run 5 times
for i in range(5):
    print("Iteration: " + str(i))
```

**Output:**
```
Iteration: 0
Iteration: 1
Iteration: 2
Iteration: 3
Iteration: 4
```

> `range(5)` generates: 0, 1, 2, 3, 4 — starts at 0, stops BEFORE 5

---

## `range()` — Three Forms

```python
range(stop)              # 0 to stop-1
range(start, stop)       # start to stop-1
range(start, stop, step) # start to stop-1, jumping by step
```

```python
# range(stop)
for i in range(5):
    print(i)            # 0, 1, 2, 3, 4

# range(start, stop)
for i in range(2, 6):
    print(i)            # 2, 3, 4, 5

# range(start, stop, step)
for i in range(0, 10, 2):
    print(i)            # 0, 2, 4, 6, 8

# Counting backwards
for i in range(5, 0, -1):
    print(i)            # 5, 4, 3, 2, 1
```

### 🛡️ Cybersecurity Example — Port Scanner Skeleton:

```python
print("=" * 40)
print("   BASIC PORT RANGE SCANNER")
print("=" * 40)

target = input("Enter target IP : ")
start_port = int(input("Start port     : "))
end_port = int(input("End port       : "))

print()
print("Scanning " + target + " ports " + str(start_port) + "-" + str(end_port))
print("-" * 40)

for port in range(start_port, end_port + 1):
    print("Checking port : " + str(port))

print("-" * 40)
print("Scan complete!")
```

**Sample Output:**
```
========================================
   BASIC PORT RANGE SCANNER
========================================
Enter target IP : 192.168.1.1
Start port     : 80
End port       : 85

Scanning 192.168.1.1 ports 80-85
----------------------------------------
Checking port : 80
Checking port : 81
Checking port : 82
Checking port : 83
Checking port : 84
Checking port : 85
----------------------------------------
Scan complete!
```

---

# 8. IMPORTING MODULES

## What is a Module?

A **module** is a Python file containing pre-written functions you can use in your programs. Python comes with many built-in modules.

```python
import module_name
```

```python
import random
import sys
import math
import os
```

---

## Using Module Functions

After importing, use `module_name.function_name()`

```python
import random

print(random.randint(1, 10))        # Random integer between 1 and 10
print(random.randint(1, 100))       # Random integer between 1 and 100
```

---

## `from import` Statements

Import a **specific function** from a module — no need to use module name prefix.

```python
from random import randint

print(randint(1, 10))           # No need to write random.randint()
```

```python
from sys import exit

exit()                          # No need to write sys.exit()
```

### Which style to use?

```python
# Use import module — when using many functions from module
import random
random.randint(1, 10)
random.choice(['a', 'b', 'c'])

# Use from module import — when using just one specific function
from random import randint
randint(1, 10)
```

---

## Useful Modules for Cybersecurity

```python
import random      # Random number generation (password tools)
import sys         # System functions (exit, argv)
import os          # Operating system interaction
import math        # Mathematical functions
import time        # Time and delays
import hashlib     # Hashing (MD5, SHA256) ← very important
import socket      # Network connections ← very important
import re          # Regular expressions ← very important
```

---

## 🛡️ Cybersecurity Example — Random Password Generator:

```python
import random

print("=" * 40)
print("    RANDOM PASSWORD GENERATOR")
print("=" * 40)

# Character sets
lowercase = "abcdefghijklmnopqrstuvwxyz"
uppercase = "ABCDEFGHIJKLMNOPQRSTUVWXYZ"
digits    = "0123456789"
symbols   = "!@#$%^&*"

all_chars = lowercase + uppercase + digits + symbols

length = int(input("Enter password length : "))

password = ""
for i in range(length):
    password = password + random.choice(all_chars)

print("Generated Password : " + password)
print("Password Length    : " + str(len(password)))
```

**Sample Output:**
```
========================================
    RANDOM PASSWORD GENERATOR
========================================
Enter password length : 12
Generated Password : kR7#mP2$xN9@
Password Length    : 12
```

---

# 9. ENDING A PROGRAM WITH `sys.exit()`

`sys.exit()` immediately **terminates** the program at any point.

```python
import sys

print("Program starting...")
sys.exit()                      # Program stops HERE
print("This never prints")      # Never reached
```

### 🛡️ Cybersecurity Use — Early Exit on Error:

```python
import sys

print("=" * 40)
print("   SECURE TARGET SCANNER")
print("=" * 40)

target = input("Enter target IP : ")

if target == "":
    print("ERROR: No target specified!")
    sys.exit()                  # Stop program immediately

port = int(input("Enter port : "))

if port < 1 or port > 65535:
    print("ERROR: Invalid port number!")
    sys.exit()                  # Stop program immediately

print("Scanning " + target + " on port " + str(port) + "...")
print("Scan initiated successfully.")
```

---

# 🛡️ CHAPTER 2 — COMPLETE CYBERSECURITY PROJECT

## Login Security System with Port Classifier

```python
import sys
import random

# ==========================================
# SECURITY SYSTEM v2.0
# ==========================================

print("=" * 45)
print("       SECURITY ACCESS SYSTEM".center(45))
print("=" * 45)

# --- LOGIN SECTION ---
correct_user = "admin"
correct_pass = "cyber2024"
max_attempts = 3
attempts = 0

while attempts < max_attempts:
    username = input("Username : ")
    password = input("Password : ")
    attempts = attempts + 1

    if username == correct_user and password == correct_pass:
        print("✅ Login successful! Welcome, " + username)
        break
    else:
        remaining = max_attempts - attempts
        if remaining > 0:
            print("❌ Invalid credentials! " + str(remaining) + " attempts left.")
        
if attempts == max_attempts and (username != correct_user or password != correct_pass):
    print("🔒 SYSTEM LOCKED - Too many failed attempts!")
    sys.exit()

# --- PORT CLASSIFIER SECTION ---
print()
print("=" * 45)
print("         PORT CLASSIFIER".center(45))
print("=" * 45)

for i in range(3):
    port = int(input("Enter port to classify : "))

    if port < 1 or port > 65535:
        print("⚠️  INVALID port number")
    elif port <= 1023:
        print("🔵 WELL-KNOWN port — Service: ", end="")
        if port == 21:
            print("FTP")
        elif port == 22:
            print("SSH")
        elif port == 23:
            print("Telnet (INSECURE!)")
        elif port == 80:
            print("HTTP")
        elif port == 443:
            print("HTTPS")
        else:
            print("Unknown service")
    elif port <= 49151:
        print("🟡 REGISTERED port")
    else:
        print("🟢 DYNAMIC/PRIVATE port")

print()
print("=" * 45)
print("        Session Complete".center(45))
print("=" * 45)
```

---

# 📝 CHAPTER 2 SUMMARY

```
✅ Boolean Values     — True / False only
✅ Comparison Ops     — ==, !=, <, >, <=, >=
✅ Boolean Ops        — and, or, not + truth tables
✅ if / elif / else   — decision branching
✅ while loop         — repeat while condition True
✅ break              — exit loop immediately
✅ continue           — skip current iteration
✅ for loop           — repeat fixed number of times
✅ range()            — range(stop) / range(start,stop) / range(start,stop,step)
✅ import             — load modules
✅ sys.exit()         — terminate program early
```

---

# 🧪 PRACTICE EXERCISES

**Exercise 1:** Write a number guessing game — program picks random number 1-20, user has 5 attempts, tell them higher/lower each time.

**Exercise 2:** Build a password strength checker using `if/elif/else` — check length, and print Weak / Moderate / Strong / Very Strong.

**Exercise 3:** Use a `for` loop with `range()` to print a multiplication table for any number the user enters.
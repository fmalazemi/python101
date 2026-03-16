# Python Quick Reference Guide
### Introduction to Programming — Python

> **How to use this reference:** Each section shows the **syntax** (the rule for writing the code), one **example** (a working code snippet), and the **output** (what Python prints when you run it). Use this guide while writing and practising code.

---

## Table of Contents

1. [Print Statement](#1-print-statement)
2. [Comments](#2-comments)
3. [Variables and Assignment](#3-variables-and-assignment)
4. [Data Types](#4-data-types)
5. [Type Conversion](#5-type-conversion)
6. [Arithmetic Operators](#6-arithmetic-operators)
7. [String Operations](#7-string-operations)
8. [User Input](#8-user-input)
9. [f-Strings (Formatted Output)](#9-f-strings-formatted-output)
10. [Comparison Operators](#10-comparison-operators)
11. [Logical Operators](#11-logical-operators)
12. [if / elif / else Statement](#12-if--elif--else-statement)
13. [while Loop](#13-while-loop)
14. [for Loop](#14-for-loop)
15. [range() Function](#15-range-function)
16. [break and continue](#16-break-and-continue)
17. [Lists](#17-lists)
18. [List Methods](#18-list-methods)
19. [Tuples](#19-tuples)
20. [Dictionaries](#20-dictionaries)
21. [Dictionary Methods](#21-dictionary-methods)
22. [Sets](#22-sets)
23. [Functions](#23-functions)
24. [Function Parameters and Return Values](#24-function-parameters-and-return-values)
25. [Default Parameters](#25-default-parameters)
26. [Variable Scope](#26-variable-scope)
27. [String Methods](#27-string-methods)
28. [String Slicing](#28-string-slicing)
29. [List Comprehension](#29-list-comprehension)
30. [File Handling — Reading](#30-file-handling--reading)
31. [File Handling — Writing](#31-file-handling--writing)
32. [Exception Handling (try / except)](#32-exception-handling-try--except)
33. [Importing Modules](#33-importing-modules)
34. [math Module](#34-math-module)
35. [random Module](#35-random-module)
36. [Common Built-in Functions](#36-common-built-in-functions)

---

## 1. Print Statement

**Syntax**
```python
print(value)
print(value1, value2, ...)
print(value, end="")        # no newline at the end
print(value1, value2, sep=", ")  # custom separator
```

**Example**
```python
print("Hello, World!")
print("Score:", 95)
print("A", "B", "C", sep="-")
```

**Output**
```
Hello, World!
Score: 95
A-B-C
```

---

## 2. Comments

**Syntax**
```python
# This is a single-line comment

"""
This is a
multi-line comment (docstring).
"""
```

**Example**
```python
# Calculate the area of a rectangle
length = 10   # in centimetres
width = 5
area = length * width
print(area)
```

**Output**
```
50
```

---

## 3. Variables and Assignment

**Syntax**
```python
variable_name = value
```

- Variable names must start with a letter or underscore.
- Variable names are case-sensitive (`age` and `Age` are different).
- Use `snake_case` for multi-word names (e.g., `student_name`).

**Example**
```python
student_name = "Sara"
age = 20
gpa = 3.75
print(student_name, age, gpa)
```

**Output**
```
Sara 20 3.75
```

---

## 4. Data Types

**Syntax**
```python
type(value)   # returns the data type
```

| Type    | Description          | Example Value   |
|---------|----------------------|-----------------|
| `int`   | Whole number         | `42`            |
| `float` | Decimal number       | `3.14`          |
| `str`   | Text (string)        | `"Hello"`       |
| `bool`  | True or False        | `True`, `False` |

**Example**
```python
x = 10
y = 3.14
z = "Python"
flag = True

print(type(x))
print(type(y))
print(type(z))
print(type(flag))
```

**Output**
```
<class 'int'>
<class 'float'>
<class 'str'>
<class 'bool'>
```

---

## 5. Type Conversion

**Syntax**
```python
int(value)    # convert to integer
float(value)  # convert to float
str(value)    # convert to string
bool(value)   # convert to boolean
```

**Example**
```python
num_str = "25"
num_int = int(num_str)
num_float = float(num_str)

print(num_int + 5)
print(num_float + 0.5)
print(str(100) + " points")
```

**Output**
```
30
25.5
100 points
```

---

## 6. Arithmetic Operators

**Syntax**

| Operator | Operation        | Example    |
|----------|------------------|------------|
| `+`      | Addition         | `5 + 3`    |
| `-`      | Subtraction      | `5 - 3`    |
| `*`      | Multiplication   | `5 * 3`    |
| `/`      | Division (float) | `5 / 2`    |
| `//`     | Integer division | `5 // 2`   |
| `%`      | Modulus (remainder) | `5 % 2` |
| `**`     | Exponentiation   | `2 ** 3`   |

**Example**
```python
a = 10
b = 3

print(a + b)
print(a - b)
print(a * b)
print(a / b)
print(a // b)
print(a % b)
print(a ** b)
```

**Output**
```
13
7
30
3.3333333333333335
3
1
1000
```

---

## 7. String Operations

**Syntax**
```python
str1 + str2          # concatenation (joining)
str1 * n             # repetition
len(string)          # length of string
```

**Example**
```python
first = "Hello"
second = "World"

print(first + " " + second)
print("-" * 10)
print(len(first))
```

**Output**
```
Hello World
----------
5
```

---

## 8. User Input

**Syntax**
```python
variable = input("Prompt message: ")
```

> `input()` always returns a **string**. Use `int()` or `float()` to convert when needed.

**Example**
```python
name = input("Enter your name: ")
print("Welcome,", name)
```

**Output** *(assuming the user types "Ali")*
```
Enter your name: Ali
Welcome, Ali
```

---

## 9. f-Strings (Formatted Output)

**Syntax**
```python
f"text {variable} text"
f"text {expression}"
f"{value:.2f}"   # format float to 2 decimal places
```

**Example**
```python
name = "Layla"
score = 87.5

print(f"Student: {name}")
print(f"Score: {score:.1f}")
print(f"Double score: {score * 2}")
```

**Output**
```
Student: Layla
Score: 87.5
Double score: 175.0
```

---

## 10. Comparison Operators

**Syntax**

| Operator | Meaning               | Example     |
|----------|-----------------------|-------------|
| `==`     | Equal to              | `5 == 5`    |
| `!=`     | Not equal to          | `5 != 3`    |
| `>`      | Greater than          | `7 > 4`     |
| `<`      | Less than             | `3 < 9`     |
| `>=`     | Greater than or equal | `5 >= 5`    |
| `<=`     | Less than or equal    | `4 <= 6`    |

> Comparison operators return a `bool`: either `True` or `False`.

**Example**
```python
x = 10
print(x == 10)
print(x > 15)
print(x != 5)
print(x <= 10)
```

**Output**
```
True
False
True
True
```

---

## 11. Logical Operators

**Syntax**

| Operator | Meaning                          | Example            |
|----------|----------------------------------|--------------------|
| `and`    | True if **both** are True        | `x > 0 and x < 10`|
| `or`     | True if **at least one** is True | `x < 0 or x > 5`  |
| `not`    | Reverses the result              | `not True`         |

**Example**
```python
age = 20
has_id = True

print(age >= 18 and has_id)
print(age < 18 or has_id)
print(not has_id)
```

**Output**
```
True
True
False
```

---

## 12. if / elif / else Statement

**Syntax**
```python
if condition:
    # runs if condition is True
elif another_condition:
    # runs if above is False and this is True
else:
    # runs if all conditions above are False
```

> **Important:** Indentation (4 spaces or 1 tab) is required. Python uses indentation to define blocks of code.

**Example**
```python
grade = 75

if grade >= 90:
    print("Excellent")
elif grade >= 70:
    print("Good")
elif grade >= 50:
    print("Pass")
else:
    print("Fail")
```

**Output**
```
Good
```

---

## 13. while Loop

**Syntax**
```python
while condition:
    # block runs as long as condition is True
```

**Example**
```python
count = 1

while count <= 5:
    print("Count:", count)
    count = count + 1
```

**Output**
```
Count: 1
Count: 2
Count: 3
Count: 4
Count: 5
```

---

## 14. for Loop

**Syntax**
```python
for variable in sequence:
    # block runs once for each item in sequence
```

**Example**
```python
fruits = ["apple", "banana", "cherry"]

for fruit in fruits:
    print(fruit)
```

**Output**
```
apple
banana
cherry
```

---

## 15. range() Function

**Syntax**
```python
range(stop)              # 0 to stop-1
range(start, stop)       # start to stop-1
range(start, stop, step) # start to stop-1, stepping by step
```

**Example**
```python
for i in range(1, 10, 2):
    print(i)
```

**Output**
```
1
3
5
7
9
```

---

## 16. break and continue

**Syntax**
```python
break      # exits the loop immediately
continue   # skips the rest of the current iteration
```

**Example**
```python
for i in range(1, 8):
    if i == 4:
        continue       # skip 4
    if i == 7:
        break          # stop at 7
    print(i)
```

**Output**
```
1
2
3
5
6
```

---

## 17. Lists

**Syntax**
```python
my_list = [item1, item2, item3]
my_list[index]          # access by index (starts at 0)
my_list[index] = value  # change an item
len(my_list)            # number of items
```

**Example**
```python
scores = [85, 90, 78, 95]

print(scores[0])         # first item
print(scores[-1])        # last item
print(len(scores))       # number of items

scores[2] = 80           # update item at index 2
print(scores)
```

**Output**
```
85
95
4
[85, 90, 80, 95]
```

---

## 18. List Methods

**Syntax**

| Method              | Description                        |
|---------------------|------------------------------------|
| `list.append(x)`    | Add `x` to the end                 |
| `list.insert(i, x)` | Insert `x` at index `i`            |
| `list.remove(x)`    | Remove first occurrence of `x`     |
| `list.pop(i)`       | Remove and return item at index `i`|
| `list.sort()`       | Sort in ascending order            |
| `list.reverse()`    | Reverse the list                   |
| `list.index(x)`     | Return index of first `x`          |
| `list.count(x)`     | Count occurrences of `x`           |

**Example**
```python
numbers = [3, 1, 4, 1, 5]

numbers.append(9)
numbers.sort()
print(numbers)

numbers.remove(1)
print(numbers)

print(numbers.count(1))
```

**Output**
```
[1, 1, 3, 4, 5, 9]
[1, 3, 4, 5, 9]
1
```

---

## 19. Tuples

**Syntax**
```python
my_tuple = (item1, item2, item3)
my_tuple[index]   # access by index
```

> Tuples are **immutable** — their values cannot be changed after creation.

**Example**
```python
coordinates = (10.5, 25.3)

print(coordinates[0])
print(coordinates[1])
print(len(coordinates))
```

**Output**
```
10.5
25.3
2
```

---

## 20. Dictionaries

**Syntax**
```python
my_dict = {key1: value1, key2: value2}
my_dict[key]          # access value by key
my_dict[key] = value  # add or update a key-value pair
del my_dict[key]      # remove a key-value pair
```

**Example**
```python
student = {
    "name": "Omar",
    "age": 21,
    "gpa": 3.5
}

print(student["name"])
student["age"] = 22
print(student)
```

**Output**
```
Omar
{'name': 'Omar', 'age': 22, 'gpa': 3.5}
```

---

## 21. Dictionary Methods

**Syntax**

| Method              | Description                            |
|---------------------|----------------------------------------|
| `dict.keys()`       | Returns all keys                       |
| `dict.values()`     | Returns all values                     |
| `dict.items()`      | Returns all key-value pairs            |
| `dict.get(key, d)`  | Returns value, or `d` if key missing   |
| `dict.pop(key)`     | Removes and returns value for key      |

**Example**
```python
person = {"name": "Noor", "city": "Kuwait", "age": 25}

print(person.keys())
print(person.values())
print(person.get("city"))
print(person.get("email", "Not found"))
```

**Output**
```
dict_keys(['name', 'city', 'age'])
dict_values(['Noor', 'Kuwait', 25])
Kuwait
Not found
```

---

## 22. Sets

**Syntax**
```python
my_set = {item1, item2, item3}
my_set.add(item)       # add an item
my_set.remove(item)    # remove an item
```

> Sets are **unordered** and contain **no duplicate** values.

**Example**
```python
colours = {"red", "blue", "green", "red"}

print(colours)

colours.add("yellow")
print(colours)
print(len(colours))
```

**Output** *(order may vary)*
```
{'red', 'blue', 'green'}
{'red', 'blue', 'green', 'yellow'}
4
```

---

## 23. Functions

**Syntax**
```python
def function_name():
    # body of the function

function_name()   # calling the function
```

**Example**
```python
def greet():
    print("Hello, welcome to Python!")

greet()
greet()
```

**Output**
```
Hello, welcome to Python!
Hello, welcome to Python!
```

---

## 24. Function Parameters and Return Values

**Syntax**
```python
def function_name(parameter1, parameter2):
    # body
    return result
```

**Example**
```python
def add(a, b):
    result = a + b
    return result

total = add(7, 3)
print(total)
print(add(100, 200))
```

**Output**
```
10
300
```

---

## 25. Default Parameters

**Syntax**
```python
def function_name(param1, param2=default_value):
    # body
```

**Example**
```python
def greet(name, message="Good morning"):
    print(f"{message}, {name}!")

greet("Sara")
greet("Ali", "Good evening")
```

**Output**
```
Good morning, Sara!
Good evening, Ali!
```

---

## 26. Variable Scope

**Syntax**
```python
# Global variable — defined outside all functions
x = 10

def my_function():
    # Local variable — defined inside a function
    y = 20
    print(x)   # can access global variable
    print(y)

my_function()
# print(y)  # ERROR: y is not accessible here
```

**Example**
```python
total = 0   # global variable

def add_to_total(n):
    global total
    total = total + n

add_to_total(5)
add_to_total(3)
print(total)
```

**Output**
```
8
```

---

## 27. String Methods

**Syntax**

| Method               | Description                              |
|----------------------|------------------------------------------|
| `str.upper()`        | Convert to uppercase                     |
| `str.lower()`        | Convert to lowercase                     |
| `str.strip()`        | Remove leading/trailing whitespace       |
| `str.replace(a, b)`  | Replace `a` with `b`                     |
| `str.split(sep)`     | Split into a list by separator           |
| `str.startswith(x)`  | Returns `True` if string starts with `x`|
| `str.endswith(x)`    | Returns `True` if string ends with `x`  |
| `str.find(x)`        | Returns index of first `x` (or -1)      |
| `"sep".join(list)`   | Join list items into a string            |

**Example**
```python
text = "  Hello, Python!  "

print(text.strip())
print(text.strip().lower())
print(text.strip().replace("Python", "World"))
print(text.strip().split(", "))
```

**Output**
```
Hello, Python!
hello, python!
Hello, World!
['Hello', 'Python!']
```

---

## 28. String Slicing

**Syntax**
```python
string[start:stop]         # from start to stop-1
string[start:stop:step]    # with step
string[:stop]              # from beginning to stop-1
string[start:]             # from start to end
string[-n:]                # last n characters
```

**Example**
```python
word = "Programming"

print(word[0:4])     # first 4 characters
print(word[4:])      # from index 4 to end
print(word[-3:])     # last 3 characters
print(word[::2])     # every other character
print(word[::-1])    # reversed
```

**Output**
```
Prog
ramming
ing
Pormmn
gnimmargorP
```

---

## 29. List Comprehension

**Syntax**
```python
new_list = [expression for item in iterable]
new_list = [expression for item in iterable if condition]
```

**Example**
```python
numbers = [1, 2, 3, 4, 5, 6]

squares = [n ** 2 for n in numbers]
evens   = [n for n in numbers if n % 2 == 0]

print(squares)
print(evens)
```

**Output**
```
[1, 4, 9, 16, 25, 36]
[2, 4, 6]
```

---

## 30. File Handling — Reading

**Syntax**
```python
with open("filename.txt", "r") as file:
    content = file.read()        # read entire file as a string

with open("filename.txt", "r") as file:
    lines = file.readlines()     # read all lines into a list
```

**Example**
```python
# Assume "notes.txt" contains:
# Line one
# Line two

with open("notes.txt", "r") as file:
    for line in file:
        print(line.strip())
```

**Output**
```
Line one
Line two
```

---

## 31. File Handling — Writing

**Syntax**
```python
with open("filename.txt", "w") as file:   # write (overwrites)
    file.write("text")

with open("filename.txt", "a") as file:   # append (adds to end)
    file.write("text")
```

**Example**
```python
with open("output.txt", "w") as file:
    file.write("Hello, file!\n")
    file.write("Second line.\n")

print("File written successfully.")
```

**Output**
```
File written successfully.
```
*(The file `output.txt` now contains two lines.)*

---

## 32. Exception Handling (try / except)

**Syntax**
```python
try:
    # code that might cause an error
except ErrorType:
    # code that runs if the error occurs
finally:
    # code that always runs (optional)
```

**Example**
```python
try:
    number = int(input("Enter a number: "))
    print(10 / number)
except ValueError:
    print("That is not a valid number.")
except ZeroDivisionError:
    print("Cannot divide by zero.")
finally:
    print("Done.")
```

**Output** *(if user enters 0)*
```
Enter a number: 0
Cannot divide by zero.
Done.
```

---

## 33. Importing Modules

**Syntax**
```python
import module_name
import module_name as alias
from module_name import function_name
```

**Example**
```python
import math
from math import sqrt

print(math.pi)
print(math.floor(4.9))
print(sqrt(16))
```

**Output**
```
3.141592653589793
4
4.0
```

---

## 34. math Module

**Syntax**

| Function / Constant   | Description                   |
|-----------------------|-------------------------------|
| `math.pi`             | The value of π (3.14159…)     |
| `math.sqrt(x)`        | Square root of `x`            |
| `math.pow(x, y)`      | `x` raised to the power `y`  |
| `math.floor(x)`       | Round down to nearest integer |
| `math.ceil(x)`        | Round up to nearest integer   |
| `math.abs(x)`         | Absolute value *(use `abs()`)*|
| `math.factorial(n)`   | Factorial of `n`              |

**Example**
```python
import math

print(math.sqrt(49))
print(math.pow(2, 8))
print(math.ceil(3.2))
print(math.floor(3.9))
print(math.factorial(5))
```

**Output**
```
7.0
256.0
4
3
120
```

---

## 35. random Module

**Syntax**

| Function                      | Description                               |
|-------------------------------|-------------------------------------------|
| `random.random()`             | Random float between 0.0 and 1.0         |
| `random.randint(a, b)`        | Random integer between `a` and `b`       |
| `random.choice(sequence)`     | Random item from a sequence              |
| `random.shuffle(list)`        | Shuffle a list in place                  |
| `random.sample(sequence, k)`  | `k` unique random items from sequence   |

**Example**
```python
import random

print(random.randint(1, 10))
print(random.random())

colours = ["red", "green", "blue", "yellow"]
print(random.choice(colours))

random.shuffle(colours)
print(colours)
```

**Output** *(values will vary each run)*
```
7
0.4823156789012345
green
['yellow', 'red', 'blue', 'green']
```

---

## 36. Common Built-in Functions

**Syntax**

| Function          | Description                                        |
|-------------------|----------------------------------------------------|
| `print(x)`        | Display output                                     |
| `input(msg)`      | Read input from user (returns string)              |
| `len(x)`          | Length of a string, list, tuple, dict, or set      |
| `type(x)`         | Data type of `x`                                   |
| `int(x)`          | Convert to integer                                 |
| `float(x)`        | Convert to float                                   |
| `str(x)`          | Convert to string                                  |
| `bool(x)`         | Convert to boolean                                 |
| `abs(x)`          | Absolute value                                     |
| `round(x, n)`     | Round `x` to `n` decimal places                   |
| `max(iterable)`   | Largest value                                      |
| `min(iterable)`   | Smallest value                                     |
| `sum(iterable)`   | Sum of all values                                  |
| `sorted(iterable)`| Return a sorted list (does not modify original)   |
| `range(start, stop, step)` | Generate a sequence of integers        |
| `enumerate(iterable)` | Loop with index and value                     |
| `zip(a, b)`       | Combine two iterables pair by pair                 |

**Example**
```python
numbers = [4, 1, 9, 2, 7]

print(len(numbers))
print(max(numbers))
print(min(numbers))
print(sum(numbers))
print(sorted(numbers))
print(round(3.14159, 2))
print(abs(-42))

for index, value in enumerate(numbers):
    print(index, value)
```

**Output**
```
5
9
1
23
[1, 2, 4, 7, 9]
3.14
42
0 4
1 1
2 9
3 2
4 7
```

---

*End of Python Quick Reference Guide*
*Introduction to Programming — Python Course*

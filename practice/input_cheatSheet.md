# Python Input, `int()`, `float()`, and `eval()` Cheat Sheet

The `input()` function lets a program receive information from the user.

## Most Important Rule

> `input()` always returns a string.

```python
value = input("Enter something: ")
print(type(value))  # <class 'str'>
```

Convert the input when you need a different data type:

```python
name = input("Enter your name: ")          # str
age = int(input("Enter your age: "))      # int
height = float(input("Enter height: "))   # float
```

## Quick Reference

| Code | User enters | Stored value | Type |
|---|---:|---:|---|
| `input("Value: ")` | `25` | `"25"` | `str` |
| `int(input("Value: "))` | `25` | `25` | `int` |
| `float(input("Value: "))` | `25` | `25.0` | `float` |
| `float(input("Value: "))` | `25.5` | `25.5` | `float` |
| `eval(input("Value: "))` | `10 + 5` | `15` | `int` |

---

## 1. Basic Use of `input()`

### Syntax

```python
variable = input("Prompt shown to the user: ")
```

### Example

```python
name = input("Enter your name: ")
print("Hello, " + name + "!")
```

Example run:

```text
Enter your name: Sara
Hello, Sara!
```

The prompt is optional, but including one tells the user what to enter:

```python
name = input()
```

This works, but the user sees no instructions.

---

## 2. Input Is Always a String

Suppose the user enters `20`:

```python
age = input("Enter your age: ")

print(age)        # 20
print(type(age))  # <class 'str'>
```

Although the value looks like a number, Python stores it as text.

This code causes an error:

```python
age = input("Enter your age: ")

# Error: age is a string, not a number
# next_age = age + 1
```

Convert the input first:

```python
age = int(input("Enter your age: "))
next_age = age + 1

print("Next year, you will be", next_age)
```

---

## 3. Using `int()` with Input

`int()` converts a valid whole-number string into an integer.

### Syntax

```python
number = int(input("Enter a whole number: "))
```

### Example

```python
quantity = int(input("Enter the quantity: "))
total_items = quantity + 5

print("Total items:", total_items)
```

Example run:

```text
Enter the quantity: 12
Total items: 17
```

### Valid input for `int()`

```python
int("25")   # 25
int("-8")   # -8
int("+12")  # 12
int(" 42 ") # 42
```

### Invalid input for `int()`

```python
# Each line would cause a ValueError:
# int("4.5")
# int("hello")
# int("")
```

The string `"4.5"` is not a whole-number string, so `int("4.5")` fails.

### Converting a float to an integer

When `int()` receives a float, it removes the decimal part by truncating toward zero. It does not round.

```python
print(int(7.9))   # 7
print(int(7.1))   # 7
print(int(-7.9))  # -7
```

If the user may enter a decimal but you want only its integer part:

```python
number = int(float(input("Enter a number: ")))
print(number)
```

If the user enters `7.9`, the program prints `7`.

---

## 4. Using `float()` with Input

`float()` converts a valid numeric string into a floating-point number.

Use it when the user may enter a decimal value.

### Syntax

```python
number = float(input("Enter a number: "))
```

### Example

```python
price = float(input("Enter the price: $"))
quantity = int(input("Enter the quantity: "))
total = price * quantity

print("Total: $", round(total, 2))
```

Example run:

```text
Enter the price: $3.50
Enter the quantity: 4
Total: $ 14.0
```

### Valid input for `float()`

```python
float("3.5")    # 3.5
float("8")      # 8.0
float("-2.75")  # -2.75
float(" 6.2 ")  # 6.2
float("1e3")    # 1000.0
```

### Invalid input for `float()`

```python
# Each line would cause a ValueError:
# float("hello")
# float("$12.50")
# float("")
```

Do not include currency symbols or units in numeric input:

```text
12.50     Correct
$12.50    Incorrect for float()
```

---

## 5. Choosing Between `input()`, `int()`, and `float()`

| Expected user input | Recommended code |
|---|---|
| Name | `name = input("Name: ")` |
| City | `city = input("City: ")` |
| Whole-number age | `age = int(input("Age: "))` |
| Number of students | `students = int(input("Students: "))` |
| Price | `price = float(input("Price: "))` |
| Temperature | `temperature = float(input("Temperature: "))` |
| Height or weight | `height = float(input("Height: "))` |

Ask: **Does this value need arithmetic?**

- If no, keep it as a string.
- If it must be a whole number, use `int()`.
- If it may contain a decimal, use `float()`.

---

## 6. Getting Multiple Inputs

Use a separate `input()` call for each value:

```python
length = float(input("Enter the length: "))
width = float(input("Enter the width: "))

area = length * width
print("Area:", area)
```

Another example:

```python
first_name = input("Enter your first name: ")
last_name = input("Enter your last name: ")
age = int(input("Enter your age: "))

print(f"{first_name} {last_name} is {age} years old.")
```

---

## 7. Cleaning Input with `.strip()`

`.strip()` removes spaces from the beginning and end of a string:

```python
name = input("Enter your name: ").strip()
print("Hello, " + name + "!")
```

You can normalize text input with `.lower()`:

```python
answer = input("Continue? (yes or no): ").strip().lower()

if answer == "yes":
    print("Continuing...")
elif answer == "no":
    print("Stopping...")
else:
    print("Invalid answer.")
```

`int()` and `float()` already accept outer spaces, but `.strip()` can make your intention clear:

```python
age = int(input("Enter your age: ").strip())
```

---

## 8. Using `eval()` with Input

`eval()` evaluates a string as a Python expression and returns the expression's value.

### Basic example

```python
result = eval("10 + 5")
print(result)        # 15
print(type(result))  # <class 'int'>
```

With `input()`:

```python
expression = input("Enter an arithmetic expression: ")
result = eval(expression)
print("Result:", result)
```

Example run:

```text
Enter an arithmetic expression: (10 + 5) * 2
Result: 30
```

`eval()` can return different types depending on the expression:

| User enters | Result | Type |
|---|---:|---|
| `10` | `10` | `int` |
| `10.5` | `10.5` | `float` |
| `10 + 5` | `15` | `int` |
| `8 > 3` | `True` | `bool` |
| `"hello"` | `"hello"` | `str` |

### Critical security warning

> **Never use `eval()` with untrusted user input in a real application.**

`eval()` does not only calculate arithmetic. It can execute Python expressions, which may allow a malicious user to access data or run harmful operations.

This pattern is unsafe when users are not completely trusted:

```python
# Unsafe for real applications:
result = eval(input("Enter an expression: "))
```

Only use it in a controlled classroom exercise where the input is known and trusted—or avoid it entirely.

---

## 9. Safer Alternatives to `eval()`

### When you need a whole number

```python
number = int(input("Enter a whole number: "))
```

### When you need a decimal number

```python
number = float(input("Enter a number: "))
```

### When the user chooses an operation

Instead of evaluating arbitrary text, ask for the numbers and operation separately:

```python
first = float(input("Enter the first number: "))
operator = input("Enter +, -, *, or /: ").strip()
second = float(input("Enter the second number: "))

if operator == "+":
    result = first + second
elif operator == "-":
    result = first - second
elif operator == "*":
    result = first * second
elif operator == "/":
    if second == 0:
        result = "Cannot divide by zero"
    else:
        result = first / second
else:
    result = "Invalid operator"

print("Result:", result)
```

This approach allows only the operations that the program explicitly supports.

### When you need a Python literal

For trusted Python-style literal values, `ast.literal_eval()` is more restricted than `eval()`:

```python
import ast

value = ast.literal_eval(input("Enter a literal value: "))
print(value)
```

It accepts values such as numbers, strings, lists, tuples, dictionaries, booleans, and `None`, but it does not evaluate general arithmetic expressions such as `10 + 5`.

> `ast.literal_eval()` is more restricted, but very large or deeply nested input can still cause resource problems. Apply input limits in real applications.

---

## 10. Common Errors

### Adding a number to an unconverted input string

```python
# Wrong
# age = input("Age: ")
# print(age + 1)

# Correct
age = int(input("Age: "))
print(age + 1)
```

### Using `int()` for decimal input

```python
# Wrong if the user enters 4.5
# number = int(input("Number: "))

# Correct
number = float(input("Number: "))
```

### Expecting `int()` to round

```python
print(int(6.9))    # 6
print(round(6.9))  # 7
```

### Entering symbols with a number

```text
Enter the price: 12.50     Correct
Enter the price: $12.50    Causes a ValueError
```

### Using `eval()` just to read a number

```python
# Unnecessary and unsafe for untrusted input
# number = eval(input("Number: "))

# Better
number = float(input("Number: "))
```

---

## Combined Example

This program collects text, integer, and decimal input:

```python
name = input("Enter your name: ").strip().title()
age = int(input("Enter your age: "))
height = float(input("Enter your height in meters: "))

print(f"Name: {name}")
print(f"Age next year: {age + 1}")
print(f"Height: {height:.2f} meters")
```

Example run:

```text
Enter your name: sara ali
Enter your age: 20
Enter your height in meters: 1.65
Name: Sara Ali
Age next year: 21
Height: 1.65 meters
```

## Quick Practice

Predict the value and type of each variable:

```python
a = input("Enter 10: ")
b = int("10")
c = float("10")
d = int(7.9)
e = eval("7 + 3 * 2")
```

### Answers

Assuming the user enters `10` for `a`:

| Variable | Value | Type |
|---|---:|---|
| `a` | `"10"` | `str` |
| `b` | `10` | `int` |
| `c` | `10.0` | `float` |
| `d` | `7` | `int` |
| `e` | `13` | `int` |

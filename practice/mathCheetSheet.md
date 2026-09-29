# Python Math Built-in Functions Cheat Sheet

Python provides several built-in functions for working with numbers. You can use these functions without importing any modules.

## Quick Reference

| Function | Purpose | Example | Result |
|---|---|---|---|
| `pow(x, y)` | Raises `x` to the power of `y` | `pow(2, 3)` | `8` |
| `round(number)` | Rounds to the nearest integer | `round(4.6)` | `5` |
| `round(number, digits)` | Rounds to a chosen number of decimal places | `round(3.14159, 2)` | `3.14` |
| `int(value)` | Converts a value to an integer | `int("25")` | `25` |
| `float(value)` | Converts a value to a decimal number | `float("3.5")` | `3.5` |
| `abs(number)` | Returns the absolute value | `abs(-12)` | `12` |
| `min(a, b, ...)` | Returns the smallest value | `min(7, 2, 9)` | `2` |
| `max(a, b, ...)` | Returns the largest value | `max(7, 2, 9)` | `9` |
| `divmod(a, b)` | Returns the quotient and remainder | `divmod(17, 5)` | `(3, 2)` |

---

## `pow()` — Raise a Number to a Power

### Syntax

```python
pow(base, exponent)
```

### Examples

```python
result = pow(2, 3)
print(result)
```

Output:

```text
8
```

This means:

```text
2³ = 2 × 2 × 2 = 8
```

More examples:

```python
print(pow(5, 2))    # 25
print(pow(10, 3))   # 1000
print(pow(4, 0.5))  # 2.0
```

The exponent operator `**` does the same basic calculation:

```python
print(2 ** 3)       # 8
print(pow(2, 3))    # 8
```

### Three-argument form

`pow()` can also calculate a power and then find the remainder:

```python
result = pow(2, 5, 3)
print(result)
```

Output:

```text
2
```

This is equivalent to:

```python
(2 ** 5) % 3
```

---

## `round()` — Round a Number

### Syntax

```python
round(number)
round(number, number_of_digits)
```

### Round to the nearest integer

```python
print(round(4.2))  # 4
print(round(4.7))  # 5
```

### Round to decimal places

```python
price = 12.5678

print(round(price, 1))  # 12.6
print(round(price, 2))  # 12.57
print(round(price, 3))  # 12.568
```

### Important: numbers ending in `.5`

Python rounds an exact halfway value toward the nearest even number:

```python
print(round(2.5))  # 2
print(round(3.5))  # 4
print(round(4.5))  # 4
print(round(5.5))  # 6
```

This behavior is sometimes called **round half to even**.

### Displaying money

`round()` calculates a rounded number, but it does not always display trailing zeros:

```python
price = round(5.2, 2)
print(price)  # 5.2
```

To display exactly two decimal places, use an f-string:

```python
price = 5.2
print(f"${price:.2f}")  # $5.20
```

---

## `int()` — Convert to an Integer

### Syntax

```python
int(value)
```

### Convert a string

```python
age_text = "20"
age = int(age_text)

print(age)       # 20
print(age + 1)   # 21
```

This is especially useful with `input()` because `input()` returns a string:

```python
age = int(input("Enter your age: "))
print("Next year, you will be", age + 1)
```

### Convert a float

```python
print(int(8.9))   # 8
print(int(3.2))   # 3
print(int(-4.9))  # -4
```

> `int()` does not round a decimal number. It removes the decimal part by truncating toward zero.

### Invalid conversion

The text must represent a whole number:

```python
int("25")    # Works: 25
int("25.5")  # Error
int("hello") # Error
```

To convert the string `"25.5"` to an integer, convert it to a float first:

```python
number = int(float("25.5"))
print(number)  # 25
```

---

## `float()` — Convert to a Decimal Number

### Syntax

```python
float(value)
```

### Convert a string

```python
price_text = "19.99"
price = float(price_text)

print(price)       # 19.99
print(price * 2)   # 39.98
```

Use `float()` when the user may enter a decimal number:

```python
height = float(input("Enter your height in meters: "))
print("Your height is", height, "meters.")
```

### Convert an integer

```python
print(float(7))   # 7.0
print(float(-3))  # -3.0
```

### Invalid conversion

The text must represent a valid number:

```python
float("3.14")  # Works: 3.14
float("8")     # Works: 8.0
float("hello") # Error
```

---

## `abs()` — Find the Absolute Value

The absolute value is the distance from zero, so it is never negative.

```python
print(abs(-10))   # 10
print(abs(10))    # 10
print(abs(-3.5))  # 3.5
```

Example: find the difference between two temperatures:

```python
morning = 12
afternoon = 20
difference = abs(morning - afternoon)

print(difference)  # 8
```

---

## `min()` and `max()` — Find the Smallest or Largest Value

```python
print(min(8, 3, 12))  # 3
print(max(8, 3, 12))  # 12
```

Example:

```python
score1 = 76
score2 = 91
score3 = 84

lowest = min(score1, score2, score3)
highest = max(score1, score2, score3)

print("Lowest score:", lowest)    # 76
print("Highest score:", highest)  # 91
```

---

## `divmod()` — Get the Quotient and Remainder

`divmod(a, b)` returns two values:

1. The whole-number quotient of `a // b`
2. The remainder of `a % b`

```python
result = divmod(17, 5)
print(result)  # (3, 2)
```

This means that 5 fits into 17 three times, with 2 remaining.

The two results can be stored in separate variables:

```python
minutes = 135
hours, remaining_minutes = divmod(minutes, 60)

print(hours)              # 2
print(remaining_minutes)  # 15
```

---

## Common Conversions

| Original value | Code | Result | Result type |
|---|---|---|---|
| `"42"` | `int("42")` | `42` | `int` |
| `"42"` | `float("42")` | `42.0` | `float` |
| `"4.2"` | `float("4.2")` | `4.2` | `float` |
| `4.9` | `int(4.9)` | `4` | `int` |
| `4` | `float(4)` | `4.0` | `float` |
| `3.14159` | `round(3.14159, 2)` | `3.14` | `float` |

## Combined Example

This program asks for the radius of a circle, calculates its area, and rounds the result to two decimal places:

```python
radius = float(input("Enter the circle's radius: "))
pi = 3.14159

area = pi * pow(radius, 2)
rounded_area = round(area, 2)

print("Area:", rounded_area)
```

Example run:

```text
Enter the circle's radius: 5
Area: 78.54
```

## Quick Practice

Try to predict each result before running the code:

```python
print(pow(3, 2))
print(round(7.856, 1))
print(int(6.99))
print(float("12"))
print(abs(-15))
print(min(5, 9, 2))
print(max(5, 9, 2))
print(divmod(23, 4))
```

### Answers

```text
9
7.9
6
12.0
15
2
9
(5, 3)
```

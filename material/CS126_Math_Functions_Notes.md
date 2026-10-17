# CS126 – Introduction to Python

## Mathematical Functions

**Instructor:** Dr. Fawaz Alazemi

---

## Learning Objectives

After studying these notes, you should be able to:

1. Use the built-in functions `abs`, `round`, `pow`, `max`, `min`, `sum`, and `divmod`.
2. Explain what a **module** is, and use `import math`, `from math import …`, and `import math as m`.
3. Use `math.sqrt`, `math.pow`, `math.ceil`, `math.floor`, `math.trunc`, `math.factorial`, `math.log`, `math.exp`, `math.sin`, and `math.cos`.
4. Use the constants `math.pi`, `math.e`, and `math.nan`.
5. Choose the right rounding function for a problem, and avoid mistakes with negatives, degrees, and `nan`.

---

## 1. Introduction

Python can already do arithmetic with `+`, `-`, `*`, `/`, `//`, `%`, and `**`. For many everyday tasks we also need **ready-made math tools**: the largest value, a square root, rounding up, the area of a circle, an angle.

Python provides these tools in two places:

| Where | How to use | Examples |
|---|---|---|
| **Built-in functions** | always available | `abs`, `round`, `pow`, `max`, `min`, `sum`, `divmod` |
| **The `math` module** | must be **imported** first | `sqrt`, `ceil`, `floor`, `trunc`, `factorial`, `log`, `exp`, `sin`, `cos`, `pi`, `e`, `nan` |

A **module** is a file that contains extra functions and values. Python comes with many modules. Think of one as a toolbox on a shelf: it is there, but you must bring it to your program before you can use it.

---

## 2. Built-in Math Functions

### 2.1 abs(): absolute value

`abs(x)` gives the distance of `x` from zero. The result is never negative:

```python
print(abs(-7), abs(-2.5), abs(3))
temp_today = 44
temp_yesterday = 47
print(abs(temp_today - temp_yesterday))
```

```text
7 2.5 3
3
```

`abs` is useful for a **difference** when you do not care which value is bigger.

### 2.2 round()

```python
print(round(3.14159, 2))
print(round(7.6))
print(round(1234, -2))
```

```text
3.14
8
1200
```

- `round(x)` gives the nearest whole number (an `int`).
- `round(x, n)` keeps `n` digits after the decimal point (a `float`).
- A negative `n` rounds to tens (`-1`), hundreds (`-2`), and so on.

**Rounding halves.** When a number is **exactly** halfway between two whole numbers, Python rounds to the **even** one:

```python
print(round(0.5), round(1.5), round(2.5), round(3.5))
print(round(-2.5))
```

```text
0 2 2 4
-2
```

This is called **banker's rounding**. It prevents a bias: if halves always went up, adding many rounded numbers would give a total that is too large.

A second surprise comes from the way computers store decimals. `2.675` cannot be stored exactly, so it is really a tiny bit less than 2.675:

```python
print(round(2.675, 2))
```

```text
2.67
```

For everyday work this is rarely a problem, but do not be surprised by it.

### 2.3 pow()

`pow(x, y)` is the same as `x ** y`:

```python
print(pow(2, 10), 2 ** 10)
print(pow(9, 0.5), pow(2, -1))
```

```text
1024 1024
3.0 0.5
```

A power of `0.5` is a square root; a negative power is `1 / x`.

### 2.4 max(), min(), sum()

`max` and `min` accept **either** one collection (list, tuple, set, string) **or** several separate values. `sum` accepts a collection of numbers:

```python
temps = [44, 46, 48, 45]
print(max(temps), min(temps))
print(max(3, 9, 2), min(3, 9, 2))
print(sum(temps))
print(sum(temps) / len(temps))
print(max(temps) - min(temps))
```

```text
48 44
9 2
183
45.75
4
```

- The **average** is `sum(x) / len(x)`.
- The **range** (spread) is `max(x) - min(x)`.

### 2.5 divmod()

`divmod(a, b)` returns a **tuple** with the quotient and the remainder: `(a // b, a % b)`.

```python
print(divmod(17, 5))
print(17 // 5, 17 % 5)
```

```text
(3, 2)
3 2
```

Because the result is a tuple, you can **unpack** it into two variables. This is perfect for converting units:

```python
minutes = 135
hours, mins = divmod(minutes, 60)
print(hours, "h", mins, "min")
fils = 3750
kd, rest = divmod(fils, 1000)
print(kd, "KD and", rest, "fils")
```

```text
2 h 15 min
3 KD and 750 fils
```

---

## 3. Importing Modules

### 3.1 import math

```python
import math
print(math.sqrt(25))
print(math.pi)
```

```text
5.0
3.141592653589793
```

- Write `import math` **once**, normally at the **top** of the program.
- Then use the **module name**, a **dot**, and the **tool name**: `math.sqrt`, `math.pi`.

Without the import, Python does not know the name `math`:

```text
print(math.sqrt(25))

NameError: name 'math' is not defined
```

### 3.2 from math import …

```python
from math import sqrt, pi
print(sqrt(16))
print(round(pi, 2))
```

```text
4.0
3.14
```

- Only the **named** tools are imported, and you use them **without** the `math.` prefix.
- Anything you did not name is **not** available. After `from math import sqrt, pi`, calling `floor(2.5)` gives a `NameError`, and so does `math.pi` (the name `math` itself was not imported).

### 3.3 import math as m

```python
import math as m
print(m.floor(7.9))
```

```text
7
```

`as` gives the module a shorter **nickname** (an **alias**).

### 3.4 from math import *

The star imports **everything** from the module. It works, but it is **not recommended**:

- a reader cannot tell where a name came from;
- it can silently replace your own variables. For example, `math` contains a value called `e`, which would replace a variable `e` you created earlier.

### 3.5 Summary

| Import style | How you call it | When to use |
|---|---|---|
| `import math` | `math.sqrt(x)` | the clearest; recommended for beginners |
| `from math import sqrt, pi` | `sqrt(x)`, `pi` | when you use a few tools many times |
| `import math as m` | `m.sqrt(x)` | when the module name is long |
| `from math import *` | `sqrt(x)` | avoid |

---

## 4. Functions from the math Module

### 4.1 math.sqrt() and math.pow()

```python
import math
print(math.sqrt(16), math.sqrt(2))
print(math.pow(2, 3), pow(2, 3), 2 ** 3)
print(math.pow(9, 0.5))
```

```text
4.0 1.4142135623730951
8.0 8 8
3.0
```

- `math.sqrt(x)` returns the square root, always as a **float**.
- `math.pow(x, y)` also always returns a **float**. The built-in `pow` and `**` keep whole numbers as `int`.

A negative number has no real square root:

```text
math.sqrt(-1)

ValueError: math domain error
```

"Domain error" means the input is outside the values the function accepts. (Newer versions of Python may word this message slightly differently.)

### 4.2 math.ceil(), math.floor(), math.trunc()

All three remove the decimal part and return an `int`, but they move in different directions:

| Function | Direction | `4.7` | `-4.7` |
|---|---|---|---|
| `math.ceil` | **up** (toward +∞) | 5 | −4 |
| `math.floor` | **down** (toward −∞) | 4 | −5 |
| `math.trunc` | **toward zero** (just cut off the decimals) | 4 | −4 |
| `round` | nearest | 5 | −5 |

```python
import math
print(math.ceil(4.2), math.floor(4.8))
print(math.ceil(-4.2), math.floor(-4.2))
print(math.trunc(4.7), math.trunc(-4.7))
print(int(-4.7))
```

```text
5 4
-4 -5
4 -4
-4
```

- For **positive** numbers, `floor` and `trunc` give the same result. For **negative** numbers, they do not.
- `int(x)` behaves like `trunc(x)`.

**Choosing the right one.** Think about the **rule** of the problem:

| Rule | Function | Example |
|---|---|---|
| "How many do I need?" (never too few) | `ceil` | buses, boxes, started hours |
| "How many complete ones fit?" | `floor` | full boxes from a number of eggs |
| "Just drop the decimals" | `trunc` / `int` | |
| "Nearest value" | `round` | displaying a result |

```python
import math
students = 47
bus_seats = 12
print(math.ceil(students / bus_seats))
print(math.floor(students / bus_seats))
```

```text
4
3
```

4 buses are **needed**; 3 buses can be **completely filled**.

### 4.3 math.factorial()

`math.factorial(n)` = 1 × 2 × 3 × … × n, written **n!**:

```python
import math
print(math.factorial(5))
print(math.factorial(0))
print(math.factorial(10))
```

```text
120
1
3628800
```

Factorials count arrangements: 5 students can stand in a line in 5! = 120 different orders. By definition, 0! = 1.

It only accepts whole numbers 0 or greater:

```text
math.factorial(-1)
ValueError: factorial() not defined for negative values

math.factorial(5.0)
TypeError: 'float' object cannot be interpreted as an integer
```

### 4.4 math.e, math.exp(), math.log()

```python
import math
print(math.e)
print(math.exp(1), math.exp(0), math.exp(2))
print(math.log(math.e))
print(math.log(100, 10), math.log10(1000))
print(math.log(8, 2), math.log2(8))
```

```text
2.718281828459045
2.718281828459045 1.0 7.38905609893065
1.0
2.0 3.0
3.0 3.0
```

- `math.e` ≈ 2.718 is an important constant in science, finance, and growth problems.
- `math.exp(x)` = e<sup>x</sup>.
- `math.log(x)` is the **natural logarithm** (base e). It is the opposite of `exp`: `log(exp(x))` gives back `x`.
- `math.log(x, b)` uses base `b`.
- `math.log10(x)` and `math.log2(x)` are shortcuts for bases 10 and 2, and they are slightly more accurate:

```python
import math
print(math.log(1000, 10), math.log10(1000))
```

```text
2.9999999999999996 3.0
```

A logarithm answers the question: **"To what power must I raise the base to get this number?"** For example, 10<sup>2</sup> = 100, so log<sub>10</sub>(100) = 2.

The logarithm of 0 or of a negative number does not exist:

```text
math.log(0)

ValueError: math domain error
```

### 4.5 math.pi, math.sin(), math.cos()

```python
import math
print(math.pi)
print(math.sin(math.pi / 2), math.cos(0))
print(math.sin(math.pi))
```

```text
3.141592653589793
1.0 1.0
1.2246467991473532e-16
```

**Radians, not degrees.** `sin` and `cos` expect the angle in **radians**. A full circle is 360° = 2π radians, so 180° = π radians. Convert with `math.radians` and `math.degrees`:

```python
import math
angle = math.radians(30)
print(angle)
print(math.sin(angle), round(math.sin(angle), 4))
print(math.degrees(math.pi))
```

```text
0.5235987755982988
0.49999999999999994 0.5
180.0
```

**Tiny errors.** `1.2246467991473532e-16` means 1.22 × 10<sup>−16</sup>, which is practically 0. The true value of sin(π) is exactly 0, but computers store decimals with tiny errors. Use `round()` to display clean results.

### 4.6 math.nan

`nan` means **"not a number"**. It is a special `float` used for a missing or invalid value:

```python
import math
x = math.nan
print(x, type(x))
print(x + 5)
print(x == x)
print(math.isnan(x))
```

```text
nan <class 'float'>
nan
False
True
```

- Any calculation with `nan` gives `nan`.
- `nan` is **not equal to anything — not even itself**. So `x == math.nan` can never find it.
- Always check with `math.isnan(x)`.

```python
import math
reading = math.nan
if math.isnan(reading):
    print("No reading today")
else:
    print("Reading:", reading)
```

```text
No reading today
```

---

## 5. Worked Examples

### 5.1 Which pizza is better value?

```python
import math
small_d, small_price = 25, 2.5
large_d, large_price = 35, 4.5
small_area = math.pi * (small_d / 2) ** 2
large_area = math.pi * (large_d / 2) ** 2
small_fils = small_price * 1000 / small_area
large_fils = large_price * 1000 / large_area
print(round(small_area), round(large_area))
print(round(small_fils, 2), round(large_fils, 2))
if large_fils < small_fils:
    print("Better value: large")
else:
    print("Better value: small")
```

```text
491 962
5.09 4.68
Better value: large
```

The area of a circle is π r², with r = diameter / 2. The large pizza costs 4.68 fils per cm², the small one 5.09.

### 5.2 Parking fee

```python
import math
minutes = 135
hours, mins = divmod(minutes, 60)
print("Parked:", hours, "h", mins, "min")
paid_hours = math.ceil(minutes / 60)
fee = paid_hours * 0.25
print("Paid hours:", paid_hours)
print("Fee:", fee, "KD")
```

```text
Parked: 2 h 15 min
Paid hours: 3
Fee: 0.75 KD
```

Every **started** hour is charged, so we round **up**. `round(2.25)` would give 2 — the wrong fee.

### 5.3 A wheelchair ramp

```python
import math
height = 0.5
length = 6
ramp = math.sqrt(height ** 2 + length ** 2)
angle = math.degrees(math.atan(height / length))
print("Ramp length:", round(ramp, 2), "m")
print("Angle:", round(angle, 1), "degrees")
if angle <= 5:
    print("Safe")
else:
    print("Too steep")
```

```text
Ramp length: 6.02 m
Angle: 4.8 degrees
Safe
```

- The ramp is the hypotenuse of a right triangle: √(height² + length²) (Pythagoras).
- `math.atan` is the opposite of tan: it turns "opposite ÷ adjacent" into an angle in radians, and `math.degrees` converts it.

---

## 6. Common Mistakes

### Mistake 1: Forgetting the math. prefix

```text
import math
print(sqrt(16))

NameError: name 'sqrt' is not defined
```

**Fix:** `math.sqrt(16)`, or import the name with `from math import sqrt`.

### Mistake 2: Using math. after from … import

```text
from math import sqrt
print(math.pi)

NameError: name 'math' is not defined
```

**Fix:** `from math import sqrt, pi` and then `print(pi)`.

### Mistake 3: Degrees instead of radians

```python
import math
print(math.cos(60))
print(round(math.cos(math.radians(60)), 4))
```

```text
-0.9524129804151563
0.5
```

The first line calculates the cosine of 60 **radians**.

### Mistake 4: floor with negative numbers

```python
import math
print(math.floor(-3.6), math.trunc(-3.6))
```

```text
-4 -3
```

To simply remove the decimal part, use `trunc` (or `int`), not `floor`.

### Mistake 5: round when you need ceil

```python
import math
eggs = 100
print(round(eggs / 12), math.ceil(eggs / 12))
```

```text
8 9
```

Eight boxes hold only 96 eggs. When you must cover **everything**, use `ceil`.

### Mistake 6: Testing nan with ==

```python
import math
x = math.nan
print(x == math.nan, math.isnan(x))
```

```text
False True
```

---

## 7. Mini Practice Questions

**Q1.** What does `print(abs(-4) + round(2.5))` print?

**Q2.** What does `print(divmod(23, 4))` print?

**Q3.** What do `math.ceil(-1.5)`, `math.floor(-1.5)`, and `math.trunc(-1.5)` return?

**Q4.** After `from math import pi`, which works: `pi`, `math.pi`, or `sqrt(4)`?

**Q5.** What is the type of `math.sqrt(9)`? Of `pow(3, 2)`?

### Answers

1. **`6`** — `abs(-4)` is 4, and `round(2.5)` is 2 (halves go to even).
2. **`(5, 3)`**
3. **−1, −2, −1**
4. Only **`pi`**.
5. `float` (3.0) and `int` (9).

---

## 8. Ask AI to Help You Understand

```text
Explain the difference between math.ceil, math.floor, math.trunc, and round in Python
using the numbers 4.7 and -4.7. Give one real-life situation for each.
```

```text
Explain the three ways to import in Python: import math, from math import sqrt,
and import math as m. When should a beginner use each one?
```

```text
Why does math.sin(math.radians(30)) give 0.49999999999999994 instead of 0.5?
Explain radians and floating-point errors simply.
```

> **Remember:** Always run the code yourself. AI can make mistakes, and running code is the only way to be sure.

---

## 9. Summary

- **Built-ins** (no import): `abs`, `round` (halves → even), `pow`, `max`, `min`, `sum`, `divmod` (returns a tuple).
- **Import** with `import math` (use `math.name`), `from math import name` (use `name`), or `import math as m` (use `m.name`). Avoid `from math import *`.
- `math.sqrt` and `math.pow` always return floats.
- `ceil` goes up, `floor` goes down, `trunc` goes toward zero — choose by the rule of the problem.
- `math.factorial(n)` needs a whole number ≥ 0.
- `math.exp` and `math.log` are opposites; `log(x, b)` uses base `b`; `math.e` ≈ 2.718.
- `math.sin` and `math.cos` use **radians**; convert with `math.radians`. `math.pi` ≈ 3.14159.
- `math.nan` is a float for "not a number"; check it with `math.isnan`, never `==`.

---

## Basic Exercises

> Exercises 1–9 are the same as in the slides. Exercises 10–12 are extra practice.

**Exercise 1.** Predict the output.

```python
print(abs(-12), round(3.456, 1), pow(3, 2))
print(max(4, 9, 1), min([4, 9, 1]))
print(sum((4, 9, 1)))
```

**Exercise 2.** Predict the output.

```python
import math
print(math.ceil(7.1), math.floor(7.9))
print(math.trunc(-7.9), math.sqrt(49))
```

**Exercise 3.** Find and fix the error.

```text
import math
print(factorial(5))
```

**Exercise 10.** Predict the output.

```python
print(divmod(-7, 2), abs(-7) // 2)
```

## Practice Exercises

**Exercise 4.** Use `divmod` to convert `seconds = 3725` into minutes and seconds, and print `62 min 5 s`.

**Exercise 5.** Using `from math import pi`, print the area of a circle with radius 7, rounded to 2 decimal places.

**Exercise 6.** A box holds 12 eggs. How many boxes are needed for 100 eggs? Use the right function from `math`.

**Exercise 11.** A right triangle has sides `a = 5` and `b = 12`. Print the length of the third side (the hypotenuse) using `math.sqrt`.

## Challenge Exercises

**Exercise 7.** Predict the output, and explain the first line.

```python
print(round(0.5), round(1.5), round(2.5))
import math
print(math.floor(-2.5), math.trunc(-2.5))
print(math.ceil(-2.5))
```

**Exercise 8.** Print `sin(30°)` and `cos(60°)`, both rounded to 4 decimals. (Both should be 0.5.)

**Exercise 9.** Predict the output.

```python
import math as m
x = m.nan
print(x == x, m.isnan(x))
print(m.log(m.e), m.log(1000, 10))
print(m.exp(0), m.factorial(3))
```

**Exercise 12.** For `marks = [72, 95, 58, 88]`, print the average rounded to 1 decimal place, the range (highest − lowest), and the average rounded **up** to a whole number.

---

# Exercise Solutions

### Solution 1

```text
12 3.5 9
9 1
14
```

### Solution 2

`ceil` goes up, `floor` goes down, `trunc` goes toward zero, and `sqrt` returns a float.

```text
8 7
-7 7.0
```

### Solution 3

With `import math`, the function must be written with the prefix; otherwise Python gives `NameError: name 'factorial' is not defined`.

```python
import math
print(math.factorial(5))
```

```text
120
```

Another correct answer: `from math import factorial`, then `print(factorial(5))`.

### Solution 4

```python
seconds = 3725
m, s = divmod(seconds, 60)
print(m, "min", s, "s")
```

```text
62 min 5 s
```

### Solution 5

```python
from math import pi
print(round(pi * 7 ** 2, 2))
```

```text
153.94
```

### Solution 6

100 / 12 = 8.33…, so 9 boxes are needed. Round **up**:

```python
import math
print(math.ceil(100 / 12))
```

```text
9
```

### Solution 7

```text
0 2 2
-3 -2
-2
```

Exact halves are rounded to the nearest **even** number, so 0.5 → 0, 1.5 → 2, and 2.5 → 2. For −2.5: `floor` goes down to −3, `trunc` goes toward zero to −2, and `ceil` goes up to −2.

### Solution 8

```python
import math
print(round(math.sin(math.radians(30)), 4))
print(round(math.cos(math.radians(60)), 4))
```

```text
0.5
0.5
```

### Solution 9

```text
False True
1.0 2.9999999999999996
1.0 6
```

`nan` is never equal to itself. `log(e)` is 1. `log(1000, 10)` should be 3 but shows a tiny floating-point error (`math.log10(1000)` gives exactly `3.0`). e⁰ = 1 and 3! = 6.

### Solution 10

`-7 // 2` is −4 (floor division goes **down**), and the remainder is 1, because −4 × 2 + 1 = −7. `abs(-7) // 2` is `7 // 2` = 3.

```text
(-4, 1) 3
```

### Solution 11

```python
import math
a = 5
b = 12
print(math.sqrt(a ** 2 + b ** 2))
```

```text
13.0
```

### Solution 12

```python
import math
marks = [72, 95, 58, 88]
avg = sum(marks) / len(marks)
print(round(avg, 1))
print(max(marks) - min(marks))
print(math.ceil(avg))
```

```text
78.2
37
79
```

The average is exactly 78.25. Rounding to 1 decimal place sends this exact half to the **even** digit, giving 78.2. `ceil` always goes up, giving 79.

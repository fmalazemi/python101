# Lecture 3: Arithmetic Operations and Expressions in Python

---

## Table of Contents

1. [Learning Objectives](#1-learning-objectives)
2. [Why This Topic Matters](#2-why-this-topic-matters)
3. [Introduction](#3-introduction)
4. [Arithmetic Operators in Python](#4-arithmetic-operators-in-python)
   - 4.1 [Addition and Subtraction](#41-addition-and-subtraction)
   - 4.2 [Multiplication and Division](#42-multiplication-and-division)
   - 4.3 [Floor Division](#43-floor-division)
   - 4.4 [Modulus (Remainder)](#44-modulus-remainder)
   - 4.5 [Exponentiation (Power)](#45-exponentiation-power)
5. [Operator Reference Table](#5-operator-reference-table)
6. [Expressions in Python](#6-expressions-in-python)
7. [Operator Precedence](#7-operator-precedence)
8. [Using Variables in Calculations](#8-using-variables-in-calculations)
9. [Mini-Programs](#9-mini-programs)
   - 9.1 [Area of a Rectangle](#91-area-of-a-rectangle)
   - 9.2 [Average of Three Marks](#92-average-of-three-marks)
   - 9.3 [Price After Discount](#93-price-after-discount)
10. [Common Mistakes](#10-common-mistakes)
11. [Summary](#11-summary)
12. [Exercises](#12-exercises)

---

## 1. Learning Objectives

By the end of this lecture, you will be able to:

- Use Python's arithmetic operators: `+`, `-`, `*`, `/`, `//`, `%`, `**`
- Understand what an expression is and how Python evaluates it
- Apply the rules of operator precedence correctly
- Use variables to store and reuse values in calculations
- Write small programs that perform real-world calculations

---

## 2. Why This Topic Matters

Almost every useful program performs some kind of calculation. Whether you are building a shopping application that computes a total price, a grade system that calculates an average, or a navigation tool that estimates travel time — arithmetic is at the core. Learning how Python handles numbers and calculations gives you the tools to write programs that solve real problems.

---

## 3. Introduction

In mathematics, you write expressions such as `5 + 3` or `10 / 2`. Python understands the same kind of expressions. When Python evaluates an expression, it performs the calculation and produces a result called a **value**.

An **operator** is a symbol that tells Python what kind of calculation to perform. The numbers or variables used in the calculation are called **operands**.

> **Analogy:** Think of an operator as a verb in a sentence. Just as the verb "add" tells you what action to perform, the operator `+` tells Python to perform addition.

---

## 4. Arithmetic Operators in Python

### 4.1 Addition and Subtraction

Addition uses the `+` operator. Subtraction uses the `-` operator. These work exactly as they do in mathematics.

```python
# Addition
total_price = 25 + 15
print(total_price)

# Subtraction
remaining_distance = 100 - 40
print(remaining_distance)
```

**Output:**
```
40
60
```

**Explanation:** Python adds `25` and `15` to get `40`, then stores it in `total_price`. It subtracts `40` from `100` to get `60`, stored in `remaining_distance`.

#### Try It Yourself

Run the code above. Then change the values and observe how the output changes. Try subtracting a larger number from a smaller one (for example, `10 - 30`) and observe the result.

---

### 4.2 Multiplication and Division

Multiplication uses the `*` operator. Division uses the `/` operator.

> **Important:** Python always returns a **float** (decimal number) when you use `/`, even if the result is a whole number.

```python
# Multiplication
area = 6 * 4
print(area)

# Division
share = 50 / 4
print(share)

# Division that produces a whole number — result is still a float
result = 10 / 2
print(result)
```

**Output:**
```
24
12.5
5.0
```

**Explanation:** `6 * 4` gives `24`. `50 / 4` gives `12.5`. Notice that `10 / 2` gives `5.0`, not `5`. This is because `/` always produces a float in Python.

#### Try It Yourself

Modify the code to calculate the cost per person if a bill of `KD 18.500` is split among `5` people. Print the result.

---

### 4.3 Floor Division

Floor division uses the `//` operator. It divides two numbers and **rounds the result down** to the nearest whole number. The result is always an integer (when both operands are integers).

> **Analogy:** Imagine you have 17 chocolates and want to distribute them equally among 5 people. Each person gets 3 chocolates, and 2 are left over. The `//` operator gives you the `3` (how many each person receives).

```python
chocolates = 17
people = 5

each_gets = chocolates // people
print(each_gets)
```

**Output:**
```
3
```

**Explanation:** `17 // 5` calculates how many times 5 fits completely into 17. The answer is 3. The remainder is discarded.

#### Try It Yourself

You have `200` minutes of video content. Each class session is `45` minutes long. Use floor division to find how many complete sessions can be held.

---

### 4.4 Modulus (Remainder)

The modulus operator `%` returns the **remainder** after division.

> **Analogy:** Using the same chocolate example, after giving 3 chocolates to each of the 5 people (15 total), you have `17 - 15 = 2` left over. The `%` operator gives you this remainder.

```python
chocolates = 17
people = 5

leftover = chocolates % people
print(leftover)
```

**Output:**
```
2
```

**Explanation:** `17 % 5` gives `2` because `17 = (5 × 3) + 2`. The remainder is `2`.

The modulus operator is very useful. A common use is to check whether a number is even or odd:

```python
number = 14

remainder = number % 2
print(remainder)
```

**Output:**
```
0
```

**Explanation:** If `number % 2` equals `0`, the number is even. If it equals `1`, the number is odd.

#### Try It Yourself

A student scored `137` points in a quiz. Each level requires exactly `25` points. Use `//` to find the student's level and `%` to find the remaining points.

---

### 4.5 Exponentiation (Power)

The exponentiation operator `**` raises a number to a power.

```python
# 2 raised to the power of 8
result = 2 ** 8
print(result)

# Square of 9
square = 9 ** 2
print(square)

# Square root (raising to the power of 0.5)
root = 25 ** 0.5
print(root)
```

**Output:**
```
256
81
5.0
```

**Explanation:** `2 ** 8` means 2 × 2 × 2 × 2 × 2 × 2 × 2 × 2, which equals `256`. Raising a number to `0.5` is equivalent to taking its square root.

#### Try It Yourself

Calculate the volume of a cube where each side has a length of `7` units. (Hint: volume = side³, which means `side ** 3`.)

---

## 5. Operator Reference Table

| Operator | Name             | Example   | Result |
|----------|------------------|-----------|--------|
| `+`      | Addition         | `8 + 3`   | `11`   |
| `-`      | Subtraction      | `8 - 3`   | `5`    |
| `*`      | Multiplication   | `8 * 3`   | `24`   |
| `/`      | Division         | `8 / 3`   | `2.666...` |
| `//`     | Floor Division   | `8 // 3`  | `2`    |
| `%`      | Modulus          | `8 % 3`   | `2`    |
| `**`     | Exponentiation   | `8 ** 3`  | `512`  |

---

## 6. Expressions in Python

An **expression** is a combination of values, variables, and operators that Python can evaluate to produce a result.

The following are all valid expressions:

```python
5 + 3          # evaluates to 8
10 * 2 - 4     # evaluates to 16
100 / 4 + 5    # evaluates to 30.0
```

You can assign the result of an expression to a variable:

```python
total = 10 * 2 - 4
print(total)
```

**Output:**
```
16
```

**Explanation:** Python first evaluates the expression `10 * 2 - 4` to get `16`, then stores that value in the variable `total`.

---

## 7. Operator Precedence

When an expression contains more than one operator, Python does not simply evaluate it from left to right. Instead, Python follows **operator precedence** — a set of rules that determines which operation is performed first.

> **Analogy:** Think of precedence like the rules for reading a recipe. You do not simply read ingredient by ingredient — you follow the order: prepare first, then mix, then bake. Similarly, Python follows an order of operations.

The order from highest to lowest precedence is:

| Priority | Operator | Description        |
|----------|----------|--------------------|
| 1 (highest) | `**`  | Exponentiation     |
| 2        | `*`, `/`, `//`, `%` | Multiplication, Division, Floor Division, Modulus |
| 3 (lowest)  | `+`, `-` | Addition, Subtraction |

When two operators have the same precedence, Python evaluates them **from left to right**.

You can always use **parentheses `()`** to control the order of evaluation explicitly.

### Example: Without Parentheses

```python
result = 2 + 3 * 4
print(result)
```

**Output:**
```
14
```

**Explanation:** Python evaluates `3 * 4` first (because `*` has higher precedence than `+`), giving `12`. Then it computes `2 + 12 = 14`.

### Example: With Parentheses

```python
result = (2 + 3) * 4
print(result)
```

**Output:**
```
20
```

**Explanation:** The parentheses force Python to evaluate `2 + 3` first, giving `5`. Then it computes `5 * 4 = 20`.

### Example: Multiple Operators

```python
result = 10 + 2 ** 3 - 6 / 2
print(result)
```

**Output:**
```
15.0
```

**Explanation:** Python evaluates in this order:
1. `2 ** 3` → `8`
2. `6 / 2` → `3.0`
3. `10 + 8` → `18`
4. `18 - 3.0` → `15.0`

#### Try It Yourself

Before running the code, predict the output of:

```python
print(5 + 10 // 3 * 2 - 1)
```

Then run it and check your prediction. Can you explain each step?

---

## 8. Using Variables in Calculations

Variables make expressions more readable and allow values to be reused easily. Instead of writing the same number repeatedly, you store it in a variable and use the variable name.

```python
price_per_kg = 2.500
quantity_kg = 4

total_cost = price_per_kg * quantity_kg
print("Total cost:", total_cost)
```

**Output:**
```
Total cost: 10.0
```

**Explanation:** The values are stored in clearly named variables. The expression `price_per_kg * quantity_kg` is easy to understand at a glance.

If the price changes, you only need to update the value in one place — the variable definition.

#### Try It Yourself

Modify the program above to include a discount of `0.500` KD. Subtract the discount from `total_cost` and print the final price.

---

## 9. Mini-Programs

The following examples demonstrate how arithmetic operators are used together in small, practical programs.

### 9.1 Area of a Rectangle

```python
# Area of a Rectangle
# Formula: area = length * width

length = 8
width = 5

area = length * width

print("Length:", length)
print("Width:", width)
print("Area:", area)
```

**Output:**
```
Length: 8
Width: 5
Area: 40
```

**Explanation:** The variables `length` and `width` store the dimensions. The expression `length * width` computes the area and stores it in `area`.

#### Try It Yourself

Extend this program to also calculate the **perimeter** of the rectangle. The formula is: `perimeter = 2 * (length + width)`. Print both the area and the perimeter.

---

### 9.2 Average of Three Marks

```python
# Average of Three Marks

mark1 = 78
mark2 = 85
mark3 = 92

total = mark1 + mark2 + mark3
average = total / 3

print("Total marks:", total)
print("Average mark:", average)
```

**Output:**
```
Total marks: 255
Average mark: 85.0
```

**Explanation:** The three marks are summed to get the total. The total is then divided by `3` to calculate the average. Note that the result is a float (`85.0`) because `/` always returns a float.

#### Try It Yourself

Change the marks to `65`, `70`, and `88`. Predict the output before running the code.

---

### 9.3 Price After Discount

```python
# Price After Discount

original_price = 120
discount_percent = 15

discount_amount = original_price * discount_percent / 100
final_price = original_price - discount_amount

print("Original price:", original_price)
print("Discount amount:", discount_amount)
print("Final price:", final_price)
```

**Output:**
```
Original price: 120
Discount amount: 18.0
Final price: 102.0
```

**Explanation:** The discount amount is calculated as a percentage of the original price. The final price is obtained by subtracting the discount. Note the use of parentheses in the formula: Python evaluates `original_price * discount_percent` first (left to right, same precedence as `/`), then divides by `100`.

#### Try It Yourself

Change the discount to `25%` and the price to `200`. What is the final price?

---

## 10. Common Mistakes

### Mistake 1: Using `/` When Floor Division Is Needed

**Wrong:**
```python
pages = 100
pages_per_chapter = 12
chapters = pages / pages_per_chapter
print(chapters)
```

**Output:**
```
8.333333333333334
```

**Correct:**
```python
pages = 100
pages_per_chapter = 12
chapters = pages // pages_per_chapter
print(chapters)
```

**Output:**
```
8
```

**Explanation:** When you need a whole number (for example, counting complete chapters), use `//` instead of `/`. Division `/` always returns a float, even when the result happens to be a whole number.

---

### Mistake 2: Confusing `**` with `*` for Powers

**Wrong:**
```python
result = 3 * 3   # This is 3 × 3 = 9, not 3 to the power of 3
print(result)
```

**Output:**
```
9
```

**Correct:**
```python
result = 3 ** 3  # This is 3³ = 27
print(result)
```

**Output:**
```
27
```

**Explanation:** `*` is multiplication. `**` is exponentiation (power). These are different operations. `3 ** 3` means 3 × 3 × 3 = 27, not 3 × 3 = 9.

---

### Mistake 3: Ignoring Operator Precedence

**Wrong (incorrect understanding):**
```python
# Student expects: (2 + 3) * 4 = 20
result = 2 + 3 * 4
print(result)
```

**Output:**
```
14
```

**Correct:**
```python
# Use parentheses to enforce the intended order
result = (2 + 3) * 4
print(result)
```

**Output:**
```
20
```

**Explanation:** Without parentheses, `*` is evaluated before `+`. If you intend addition to happen first, you must use parentheses explicitly.

---

### Mistake 4: Trying to Add a String and a Number

**Wrong:**
```python
price = "50"
tax = 5
total = price + tax
print(total)
```

**Output (Error):**
```
TypeError: can only concatenate str (not "int") to str
```

**Correct:**
```python
price = 50       # Use an integer, not a string
tax = 5
total = price + tax
print(total)
```

**Output:**
```
55
```

**Explanation:** If `price` is a string (enclosed in quotes), Python cannot add it to a number. Ensure that values used in arithmetic are stored as `int` or `float`, not as `str`. If the value comes from `input()`, convert it first using `int()` or `float()`.

---

### Mistake 5: Division by Zero

**Wrong:**
```python
total = 100
people = 0
share = total / people
print(share)
```

**Output (Error):**
```
ZeroDivisionError: division by zero
```

**Correct:**
```python
total = 100
people = 4
share = total / people
print(share)
```

**Output:**
```
25.0
```

**Explanation:** Dividing any number by zero is undefined in mathematics, and Python raises a `ZeroDivisionError`. Before performing division, ensure the divisor is not zero.

---

## 11. Summary

In this lecture, you learned how to perform calculations in Python using arithmetic operators.

**Key Operators:**

- `+` adds two values
- `-` subtracts the second value from the first
- `*` multiplies two values
- `/` divides and always returns a float
- `//` divides and returns the whole number (floor)
- `%` returns the remainder after division
- `**` raises a number to a power

**Key Concepts:**

- An **expression** is a combination of values, variables, and operators that evaluates to a result.
- Python follows **operator precedence**: `**` is evaluated first, then `*`, `/`, `//`, `%`, then `+` and `-`.
- Use **parentheses `()`** to control the order of evaluation and to make your intent clear.
- Store values in **variables** to make your code readable and easy to modify.
- Always check the **data type** of your values before performing arithmetic — mixing strings and numbers causes errors.

---

## 12. Exercises

### Part A: Understanding Questions

1. What is the difference between the `/` operator and the `//` operator in Python? Give one example where you would prefer `//` over `/`.

2. What does the `%` operator return? Give an example using real numbers.

3. Explain what operator precedence means. What is the precedence order for `+`, `*`, and `**`?

4. Why does `10 / 2` produce `5.0` and not `5`? How would you get the integer `5` instead?

5. What error occurs when you try to add a string and an integer? How can you fix it?

---

### Part B: Code Tracing

Predict the output of each code block **before** running it. Then run the code to verify your prediction.

**Exercise 1:**
```python
x = 10
y = 3
print(x + y)
print(x - y)
print(x * y)
print(x / y)
print(x // y)
print(x % y)
print(x ** y)
```

**Exercise 2:**
```python
result = 4 + 2 * 3 ** 2 - 1
print(result)
```

**Exercise 3:**
```python
a = 100
b = 6
print(a // b)
print(a % b)
```

**Exercise 4:**
```python
val = (5 + 3) * (10 - 4) / 4
print(val)
```

---

### Part C: Code Writing

**Exercise 1 — Circle Area:**
Write a program that calculates the area of a circle. Store the radius in a variable. Use the value `3.14159` for pi.
Formula: `area = pi * radius ** 2`

**Exercise 2 — Speed Calculation:**
A car travels `360` kilometres in `4` hours. Write a program that calculates and prints the average speed.
Formula: `speed = distance / time`

**Exercise 3 — Convert Minutes to Hours and Minutes:**
Write a program that takes a total number of minutes (for example, `137`) and calculates how many complete hours and how many remaining minutes it represents.
- Use `//` to find the hours.
- Use `%` to find the remaining minutes.
- Print the result in the format: `2 hours and 17 minutes`

**Exercise 4 — Total Bill:**
A student buys 3 notebooks at `KD 0.750` each and 2 pens at `KD 0.200` each. Write a program that calculates and prints the total cost.

**Exercise 5 — Simple Interest:**
Write a program that calculates simple interest.
Formula: `interest = principal * rate * time / 100`
Use these values: `principal = 500`, `rate = 6`, `time = 3`.
Print the interest and the total amount (principal + interest).

---

### Part D: Code Modification

**Exercise 1:**
The program below has an error. Identify the problem and fix it.

```python
length = "12"
width = 5
area = length * width
print("Area:", area)
```

**Exercise 2:**
The following program attempts to find the number of complete weeks in a year (365 days) and the remaining days. However, it uses the wrong operators. Fix the program.

```python
days = 365
weeks = days / 7
remaining = days / 7
print("Weeks:", weeks)
print("Remaining days:", remaining)
```

**Exercise 3:**
The program below calculates the average of four exam scores, but it does not follow the correct order of operations. The programmer intended to sum all four scores before dividing. Fix the program using parentheses.

```python
score1 = 70
score2 = 85
score3 = 90
score4 = 75
average = score1 + score2 + score3 + score4 / 4
print("Average:", average)
```

**Exercise 4:**
Extend the rectangle program from Section 9.1 so that it also:
- Asks the user to enter the length and width using `input()`
- Converts the input to integers using `int()`
- Calculates and prints both the area and the perimeter

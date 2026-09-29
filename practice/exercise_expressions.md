# Python Expressions and Boolean Expressions

## Evaluate the Final Value

For each exercise, determine the final value of the variable named `result` **without running the code**.

For extra practice, also identify the final value's type: `int`, `float`, or `bool`.

> Remember Python's operator precedence: parentheses, exponentiation, multiplication/division, addition/subtraction, comparisons, `not`, `and`, and then `or`.

## Exercises

### 1. Addition

```python
result = 8 + 3
```

What is the final value of `result`?

[View solution](#solution-1)

### 2. Addition and Subtraction

```python
result = 12 - 5 + 2
```

What is the final value of `result`?

[View solution](#solution-2)

### 3. Multiplication Before Addition

```python
result = 4 * 3 + 2
```

What is the final value of `result`?

[View solution](#solution-3)

### 4. Using Parentheses

```python
result = (4 + 3) * 2
```

What is the final value of `result`?

[View solution](#solution-4)

### 5. Regular Division

```python
result = 18 / 3 + 1
```

What is the final value and type of `result`?

[View solution](#solution-5)

### 6. Floor Division

```python
result = 17 // 5
```

What is the final value of `result`?

[View solution](#solution-6)

### 7. Remainder

```python
result = 17 % 5
```

What is the final value of `result`?

[View solution](#solution-7)

### 8. Exponentiation

```python
result = 2 ** 3 + 1
```

What is the final value of `result`?

[View solution](#solution-8)

### 9. Variables in an Expression

```python
x = 7
y = 2
result = x * y + x
```

What is the final value of `result`?

[View solution](#solution-9)

### 10. Updating a Variable

```python
number = 10
number = number + 5
result = number * 2
```

What is the final value of `result`?

[View solution](#solution-10)

### 11. Mixed Arithmetic Operators

```python
a = 20
b = 6
result = a // b + a % b
```

What is the final value of `result`?

[View solution](#solution-11)

### 12. A Longer Arithmetic Expression

```python
x = 5
y = 3
result = (x + y) ** 2 // 4
```

What is the final value of `result`?

[View solution](#solution-12)

### 13. Greater Than

```python
result = 8 > 3
```

What is the final value and type of `result`?

[View solution](#solution-13)

### 14. Equality with Different Numeric Types

```python
result = 5 == 5.0
```

What is the final value of `result`?

[View solution](#solution-14)

### 15. Comparison with an Expression

```python
result = 7 != 3 + 4
```

What is the final value of `result`?

[View solution](#solution-15)

### 16. Boolean `and`

```python
result = 10 >= 10 and 4 < 6
```

What is the final value of `result`?

[View solution](#solution-16)

### 17. Boolean `or`

```python
result = 3 > 5 or 8 == 8
```

What is the final value of `result`?

[View solution](#solution-17)

### 18. Boolean `not`

```python
result = not (6 < 2)
```

What is the final value of `result`?

[View solution](#solution-18)

### 19. Boolean Operator Precedence

```python
result = True or False and False
```

What is the final value of `result`?

[View solution](#solution-19)

### 20. Combining `not`, `and`, and `or`

```python
result = not True or True and False
```

What is the final value of `result`?

[View solution](#solution-20)

### 21. Checking a Range

```python
x = 12
result = x > 5 and x < 20
```

What is the final value of `result`?

[View solution](#solution-21)

### 22. Even Number Check

```python
x = 7
result = x % 2 == 0
```

What is the final value of `result`?

[View solution](#solution-22)

### 23. A Mixed Arithmetic and Boolean Expression

```python
x = 4
y = 9
result = x * 2 > y or y - x == 5
```

What is the final value of `result`?

[View solution](#solution-23)

### 24. Logic with Parentheses

```python
temperature = 30
result = not (temperature < 20 or temperature > 35)
```

What is the final value of `result`?

[View solution](#solution-24)

### 25. Case-Sensitive String Comparison

```python
username = "admin"
password = "python"
result = username == "admin" and password == "Python"
```

What is the final value of `result`?

[View solution](#solution-25)

### 26. Age or Permission

```python
age = 17
has_permission = True
result = age >= 18 or has_permission
```

What is the final value of `result`?

[View solution](#solution-26)

### 27. Chained Comparisons

```python
a = 5
b = 10
c = 15
result = a < b < c and c - a == 10
```

What is the final value of `result`?

[View solution](#solution-27)

### 28. A More Complex Expression

```python
x = 6
y = 4
result = (x + y) / 2 == 5 and x ** 2 > y ** 2
```

What is the final value of `result`?

[View solution](#solution-28)

### 29. Short-Circuit Evaluation

```python
x = 0
result = x != 0 and 10 / x > 2
```

What is the final value of `result`? Does the program attempt to calculate `10 / x`?

[View solution](#solution-29)

### 30. Final Challenge

```python
a = 3
b = 8
c = 2
result = not (a + c > b) and (b % a == c or c ** 2 == 4)
```

What is the final value of `result`?

[View solution](#solution-30)

---

## Solutions

### Solution 1

```python
result = 11
```

The type is `int`.

[Back to Exercise 1](#1-addition)

### Solution 2

```python
result = 9
```

Addition and subtraction have equal precedence, so Python evaluates them from left to right: `12 - 5 = 7`, then `7 + 2 = 9`.

[Back to Exercise 2](#2-addition-and-subtraction)

### Solution 3

```python
result = 14
```

Multiplication happens first: `4 * 3 = 12`, then `12 + 2 = 14`.

[Back to Exercise 3](#3-multiplication-before-addition)

### Solution 4

```python
result = 14
```

The parentheses are evaluated first: `4 + 3 = 7`, then `7 * 2 = 14`.

[Back to Exercise 4](#4-using-parentheses)

### Solution 5

```python
result = 7.0
```

`18 / 3` produces the float `6.0`. Adding `1` produces `7.0`, which is also a `float`.

[Back to Exercise 5](#5-regular-division)

### Solution 6

```python
result = 3
```

Floor division returns the whole-number quotient. Five fits into 17 three complete times.

[Back to Exercise 6](#6-floor-division)

### Solution 7

```python
result = 2
```

After dividing 17 by 5, the remainder is `2`.

[Back to Exercise 7](#7-remainder)

### Solution 8

```python
result = 9
```

Exponentiation happens first: `2 ** 3 = 8`, then `8 + 1 = 9`.

[Back to Exercise 8](#8-exponentiation)

### Solution 9

```python
result = 21
```

Substitute the variable values: `7 * 2 + 7 = 14 + 7 = 21`.

[Back to Exercise 9](#9-variables-in-an-expression)

### Solution 10

```python
result = 30
```

After the update, `number` is `15`. Therefore, `result` is `15 * 2`, or `30`.

[Back to Exercise 10](#10-updating-a-variable)

### Solution 11

```python
result = 5
```

`20 // 6` is `3`, and `20 % 6` is `2`. Therefore, `3 + 2 = 5`.

[Back to Exercise 11](#11-mixed-arithmetic-operators)

### Solution 12

```python
result = 16
```

`5 + 3 = 8`, `8 ** 2 = 64`, and `64 // 4 = 16`.

[Back to Exercise 12](#12-a-longer-arithmetic-expression)

### Solution 13

```python
result = True
```

Eight is greater than three. The type is `bool`.

[Back to Exercise 13](#13-greater-than)

### Solution 14

```python
result = True
```

Although one value is an `int` and the other is a `float`, they represent the same numeric value.

[Back to Exercise 14](#14-equality-with-different-numeric-types)

### Solution 15

```python
result = False
```

`3 + 4` is `7`, so the expression becomes `7 != 7`, which is `False`.

[Back to Exercise 15](#15-comparison-with-an-expression)

### Solution 16

```python
result = True
```

`10 >= 10` is `True`, and `4 < 6` is also `True`. Therefore, `True and True` is `True`.

[Back to Exercise 16](#16-boolean-and)

### Solution 17

```python
result = True
```

`3 > 5` is `False`, but `8 == 8` is `True`. Therefore, `False or True` is `True`.

[Back to Exercise 17](#17-boolean-or)

### Solution 18

```python
result = True
```

`6 < 2` is `False`. Applying `not` changes it to `True`.

[Back to Exercise 18](#18-boolean-not)

### Solution 19

```python
result = True
```

`and` is evaluated before `or`. First, `False and False` is `False`. Then, `True or False` is `True`.

[Back to Exercise 19](#19-boolean-operator-precedence)

### Solution 20

```python
result = False
```

`not` is evaluated first, followed by `and`, and then `or`:

```text
not True or True and False
False or True and False
False or False
False
```

[Back to Exercise 20](#20-combining-not-and-and-or)

### Solution 21

```python
result = True
```

Twelve is greater than 5 and less than 20, so both comparisons are `True`.

[Back to Exercise 21](#21-checking-a-range)

### Solution 22

```python
result = False
```

`7 % 2` is `1`. Therefore, the comparison `1 == 0` is `False`.

[Back to Exercise 22](#22-even-number-check)

### Solution 23

```python
result = True
```

`4 * 2 > 9` is `False`, but `9 - 4 == 5` is `True`. Therefore, `False or True` is `True`.

[Back to Exercise 23](#23-a-mixed-arithmetic-and-boolean-expression)

### Solution 24

```python
result = True
```

`30 < 20` is `False`, and `30 > 35` is `False`. The expression inside the parentheses is therefore `False`. Applying `not` changes it to `True`.

[Back to Exercise 24](#24-logic-with-parentheses)

### Solution 25

```python
result = False
```

The username comparison is `True`, but string comparisons are case-sensitive. Therefore, `"python" == "Python"` is `False`, and `True and False` is `False`.

[Back to Exercise 25](#25-case-sensitive-string-comparison)

### Solution 26

```python
result = True
```

`17 >= 18` is `False`, but `has_permission` is `True`. Therefore, `False or True` is `True`.

[Back to Exercise 26](#26-age-or-permission)

### Solution 27

```python
result = True
```

`5 < 10 < 15` is `True`, and `15 - 5 == 10` is also `True`. Therefore, `True and True` is `True`.

[Back to Exercise 27](#27-chained-comparisons)

### Solution 28

```python
result = True
```

`(6 + 4) / 2` is `5.0`, and `5.0 == 5` is `True`. Also, `6 ** 2` is greater than `4 ** 2`. Both sides of `and` are `True`.

[Back to Exercise 28](#28-a-more-complex-expression)

### Solution 29

```python
result = False
```

`x != 0` is `False`. With `and`, Python stops as soon as it finds a `False` value, because the complete expression cannot become `True`. Therefore, Python does **not** evaluate `10 / x`, and no division-by-zero error occurs.

[Back to Exercise 29](#29-short-circuit-evaluation)

### Solution 30

```python
result = True
```

Step by step:

```text
a + c > b                 → 3 + 2 > 8 → False
not False                 → True
b % a == c                → 8 % 3 == 2 → True
c ** 2 == 4               → 2 ** 2 == 4 → True
True or True              → True
True and True             → True
```

[Back to Exercise 30](#30-final-challenge)

# Python Exercises Worksheet

> **Topics covered:** `if`, `if-else`, `if-elif-else`, nested `if`, `while` loop, `for` loop, nested loops
>
> **Instructions:** Try to solve each exercise on your own before revealing the answer. Click **"Show Answer"** to check your work.

---

## Easy

---

### 1. Positive or Negative — *Write a Program*

Write a program that asks the user for a number. Print `"Positive"` if the number is greater than zero, and `"Negative"` otherwise.

> **Hint:** Use `int(input(...))` to read a number, then a simple `if-else`.

<details>
<summary>Show Answer</summary>

```python
num = int(input("Enter a number: "))

if num > 0:
    print("Positive")
else:
    print("Negative")
```

</details>

---

### 2. Predict the Output — *Simple `if-else`*

What will the following code print?

```python
x = 10
if x > 20:
    print("Big")
else:
    print("Small")
```

<details>
<summary>Show Answer</summary>

```
Small
```

`x` is `10`, which is **not** greater than `20`, so the `else` branch runs.

</details>

---

### 3. Even or Odd — *Write a Program*

Write a program that reads a number from the user and prints whether it is **even** or **odd**.

> **Hint:** A number is even if `num % 2 == 0`.

<details>
<summary>Show Answer</summary>

```python
num = int(input("Enter a number: "))

if num % 2 == 0:
    print("Even")
else:
    print("Odd")
```

</details>

---

### 4. Predict the Output — *`if-elif-else`*

What will the following code print?

```python
score = 75

if score >= 90:
    print("A")
elif score >= 80:
    print("B")
elif score >= 70:
    print("C")
else:
    print("F")
```

<details>
<summary>Show Answer</summary>

```
C
```

`score` is `75`. The first two conditions (`>= 90` and `>= 80`) are false, but `75 >= 70` is true, so `"C"` is printed.

</details>

---

### 5. Print 1 to 5 — *Complete the Code*

Fill in the blank so the loop prints the numbers `1` through `5`, each on its own line.

```python
for i in range(___):
    print(i)
```

> **Hint:** `range(a, b)` produces numbers from `a` up to (but **not** including) `b`.

<details>
<summary>Show Answer</summary>

```python
for i in range(1, 6):
    print(i)
```

**Output:**

```
1
2
3
4
5
```

</details>

---

### 6. Countdown — *Write a Program*

Use a `while` loop to print a countdown from `5` to `1`, then print `"Go!"`.

<details>
<summary>Show Answer</summary>

```python
count = 5

while count >= 1:
    print(count)
    count = count - 1

print("Go!")
```

**Output:**

```
5
4
3
2
1
Go!
```

</details>

---

### 7. Find and Fix the Mistake — *Infinite Loop*

This code is supposed to print the numbers `1` to `3`, but it runs forever. Find and fix the bug.

```python
x = 1
while x <= 3:
    print(x)
```

<details>
<summary>Show Answer</summary>

The variable `x` is never updated inside the loop, so the condition `x <= 3` is always true.

**Fix — add `x = x + 1` inside the loop:**

```python
x = 1
while x <= 3:
    print(x)
    x = x + 1
```

</details>

---

### 8. Predict the Output — *`for` Loop*

What will the following code print?

```python
total = 0
for i in range(1, 4):
    total = total + i
print(total)
```

<details>
<summary>Show Answer</summary>

```
6
```

The loop adds `1 + 2 + 3 = 6`.

</details>

---

### 9. Age Group — *Write a Program*

Write a program that asks for the user's age and prints:

- `"Child"` if age is under 13
- `"Teenager"` if age is 13 to 17
- `"Adult"` if age is 18 or older

<details>
<summary>Show Answer</summary>

```python
age = int(input("Enter your age: "))

if age < 13:
    print("Child")
elif age <= 17:
    print("Teenager")
else:
    print("Adult")
```

</details>

---

### 10. Sum of Numbers — *Complete the Code*

Fill in the blanks so this program calculates the sum of numbers from `1` to `10` using a `while` loop.

```python
total = 0
i = 1

while i <= ___:
    total = total + ___
    i = i + 1

print(total)
```

<details>
<summary>Show Answer</summary>

```python
total = 0
i = 1

while i <= 10:
    total = total + i
    i = i + 1

print(total)
```

**Output:** `55`

</details>

---

## Medium

---

### 11. Largest of Three — *Write a Program*

Write a program that asks the user for three numbers and prints the largest one.

> **Hint:** Use `if-elif-else` or nested `if` statements to compare all three.

<details>
<summary>Show Answer</summary>

```python
a = int(input("Enter first number: "))
b = int(input("Enter second number: "))
c = int(input("Enter third number: "))

if a >= b and a >= c:
    print("Largest:", a)
elif b >= a and b >= c:
    print("Largest:", b)
else:
    print("Largest:", c)
```

</details>

---

### 12. Predict the Output — *Nested `if`*

What will the following code print?

```python
x = 15

if x > 10:
    if x > 20:
        print("Very big")
    else:
        print("Big")
else:
    print("Small")
```

<details>
<summary>Show Answer</summary>

```
Big
```

`x` is `15`. The outer condition `x > 10` is true, so we enter the inner `if`. The inner condition `x > 20` is false, so the inner `else` runs and prints `"Big"`.

</details>

---

### 13. Multiplication Table — *Write a Program*

Ask the user for a number `n`. Use a `for` loop to print the multiplication table of `n` from `1` to `10`. The output should look like:

```
3 x 1 = 3
3 x 2 = 6
...
3 x 10 = 30
```

<details>
<summary>Show Answer</summary>

```python
n = int(input("Enter a number: "))

for i in range(1, 11):
    print(n, "x", i, "=", n * i)
```

</details>

---

### 14. Find and Fix the Mistake — *`if-elif` Logic Error*

This program should print the season based on the month number (1–12), but it has a bug. Find and fix it.

```python
month = int(input("Enter month (1-12): "))

if month >= 3 and month <= 5:
    print("Spring")
if month >= 6 and month <= 8:
    print("Summer")
if month >= 9 and month <= 11:
    print("Autumn")
if month == 12 or month <= 2:
    print("Winter")
```

> **Hint:** What happens if month is `3`? Does the program print only one season? What keyword should you use instead of multiple `if` statements?

<details>
<summary>Show Answer</summary>

The code uses separate `if` statements instead of `elif`. While this particular version may seem to work, it is logically incorrect because every condition is checked independently. The proper fix is to use `elif` so that only one branch is ever executed:

```python
month = int(input("Enter month (1-12): "))

if month >= 3 and month <= 5:
    print("Spring")
elif month >= 6 and month <= 8:
    print("Summer")
elif month >= 9 and month <= 11:
    print("Autumn")
elif month == 12 or month <= 2:
    print("Winter")
else:
    print("Invalid month")
```

Using `elif` makes the intent clear and prevents unexpected behavior if conditions overlap in future edits. The added `else` handles invalid input.

</details>

---

### 15. Password Checker — *Write a Program*

Write a program that keeps asking the user for a password until they type `"python123"`. When the correct password is entered, print `"Access granted"`.

> **Hint:** Use a `while` loop that runs as long as the input is not equal to the correct password.

<details>
<summary>Show Answer</summary>

```python
password = input("Enter password: ")

while password != "python123":
    print("Wrong password. Try again.")
    password = input("Enter password: ")

print("Access granted")
```

</details>

---

### 16. Predict the Output — *`while` with `break`*

What will the following code print?

```python
i = 1
while True:
    if i > 4:
        break
    print(i)
    i = i + 1
```

<details>
<summary>Show Answer</summary>

```
1
2
3
4
```

The loop runs indefinitely but uses `break` to exit when `i > 4`. So it prints `1`, `2`, `3`, `4`, and then stops.

</details>

---

### 17. Count Digits — *Write a Program*

Write a program that reads a positive integer from the user and counts how many digits it has, using a `while` loop.

Example: if the input is `4821`, the output is `4`.

> **Hint:** Repeatedly divide the number by 10 (integer division) and count how many times you can do it before the number becomes 0.

<details>
<summary>Show Answer</summary>

```python
num = int(input("Enter a positive integer: "))
count = 0

while num > 0:
    num = num // 10
    count = count + 1

print("Number of digits:", count)
```

</details>

---

### 18. Complete the Code — *Sum Until Zero*

Complete the program so it keeps reading numbers from the user and adds them up. When the user enters `0`, the program stops and prints the total.

```python
total = 0

while True:
    num = int(input("Enter a number (0 to stop): "))
    if num == ___:
        ___
    total = total + num

print("Total:", ___)
```

<details>
<summary>Show Answer</summary>

```python
total = 0

while True:
    num = int(input("Enter a number (0 to stop): "))
    if num == 0:
        break
    total = total + num

print("Total:", total)
```

</details>

---

### 19. Nested `if` — Ticket Pricing — *Write a Program*

Write a program for a movie theater that asks the user's age and the day of the week (`"weekday"` or `"weekend"`). Print the ticket price according to these rules:

| Age         | Weekday | Weekend |
|-------------|---------|---------|
| Under 12    | $5      | $7      |
| 12 to 64    | $10     | $14     |
| 65 or older | $6      | $8      |

<details>
<summary>Show Answer</summary>

```python
age = int(input("Enter your age: "))
day = input("Enter day type (weekday/weekend): ")

if age < 12:
    if day == "weekday":
        print("Ticket price: $5")
    else:
        print("Ticket price: $7")
elif age <= 64:
    if day == "weekday":
        print("Ticket price: $10")
    else:
        print("Ticket price: $14")
else:
    if day == "weekday":
        print("Ticket price: $6")
    else:
        print("Ticket price: $8")
```

</details>

---

### 20. Predict the Output — *`for` with `continue`*

What will the following code print?

```python
for i in range(1, 8):
    if i % 3 == 0:
        continue
    print(i, end=" ")
```

<details>
<summary>Show Answer</summary>

```
1 2 4 5 7
```

The loop goes from `1` to `7`. When `i` is a multiple of `3` (i.e., `3` and `6`), `continue` skips the `print`, so those numbers are not shown.

</details>

---

## Hard

---

### 21. Simple Rectangle — *Nested Loops*

Write a program that asks the user for a number of rows and columns, then prints a rectangle of stars.

Example for rows = 3 and columns = 5:

```
*****
*****
*****
```

<details>
<summary>Show Answer</summary>

```python
rows = int(input("Enter number of rows: "))
cols = int(input("Enter number of columns: "))

for i in range(rows):
    for j in range(cols):
        print("*", end="")
    print()
```

</details>

---

### 22. Right Triangle Pattern — *Nested Loops*

Write a program that asks the user for a number `n` and prints a right triangle of stars with `n` rows.

Example for `n = 5`:

```
*
**
***
****
*****
```

<details>
<summary>Show Answer</summary>

```python
n = int(input("Enter number of rows: "))

for i in range(1, n + 1):
    for j in range(i):
        print("*", end="")
    print()
```

</details>

---

### 23. Number Pyramid — *Nested Loops*

Write a program that reads a number `n` and prints the following pattern.

Example for `n = 5`:

```
1
12
123
1234
12345
```

<details>
<summary>Show Answer</summary>

```python
n = int(input("Enter number of rows: "))

for i in range(1, n + 1):
    for j in range(1, i + 1):
        print(j, end="")
    print()
```

</details>

---

### 24. Prime Number Checker — *Write a Program*

Write a program that reads a number from the user and prints whether it is a **prime number** or not.

A prime number is a number greater than 1 that has no divisors other than 1 and itself.

> **Hint:** Use a `for` loop to check if any number from `2` to `num - 1` divides `num` evenly. Use a variable like `is_prime` to track the result.

<details>
<summary>Show Answer</summary>

```python
num = int(input("Enter a number: "))

if num <= 1:
    print("Not a prime number")
else:
    is_prime = True
    for i in range(2, num):
        if num % i == 0:
            is_prime = False
            break

    if is_prime:
        print(num, "is a prime number")
    else:
        print(num, "is not a prime number")
```

</details>

---

### 25. Predict the Output — *Nested Loop*

What will the following code print?

```python
for i in range(1, 4):
    for j in range(1, 4):
        if i == j:
            print("*", end=" ")
        else:
            print(0, end=" ")
    print()
```

<details>
<summary>Show Answer</summary>

```
* 0 0 
0 * 0 
0 0 * 
```

The code prints a `*` when the row and column numbers are equal (`i == j`), forming a diagonal. All other positions get `0`.

</details>

---

### 26. FizzBuzz — *Write a Program*

Write a program that prints numbers from `1` to `30`. But:

- For multiples of 3, print `"Fizz"` instead of the number.
- For multiples of 5, print `"Buzz"` instead of the number.
- For multiples of **both** 3 and 5, print `"FizzBuzz"`.

> **Hint:** Check the "both" condition **first**, because if you check for 3 or 5 first, the combined case will never be reached.

<details>
<summary>Show Answer</summary>

```python
for i in range(1, 31):
    if i % 3 == 0 and i % 5 == 0:
        print("FizzBuzz")
    elif i % 3 == 0:
        print("Fizz")
    elif i % 5 == 0:
        print("Buzz")
    else:
        print(i)
```

</details>

---

### 27. Find and Fix the Mistake — *Nested Loop Bug*

This code should print a 3×3 grid of numbers like:

```
1 2 3
4 5 6
7 8 9
```

But it doesn't work correctly. Find and fix the bug.

```python
num = 1
for i in range(3):
    for j in range(3):
        print(num, end=" ")
    print()
    num = num + 1
```

<details>
<summary>Show Answer</summary>

The bug is that `num = num + 1` is in the **outer** loop. It should be in the **inner** loop so that `num` increases after every number is printed, not after every row.

**Fixed code:**

```python
num = 1
for i in range(3):
    for j in range(3):
        print(num, end=" ")
        num = num + 1
    print()
```

</details>

---

### 28. Centered Pyramid — *Nested Loops*

Write a program that asks the user for a number `n` and prints a centered pyramid of stars.

Example for `n = 5`:

```
    *
   ***
  *****
 *******
*********
```

> **Hint:** For each row `i` (starting from 1), you need `n - i` spaces followed by `2 * i - 1` stars.

<details>
<summary>Show Answer</summary>

```python
n = int(input("Enter number of rows: "))

for i in range(1, n + 1):
    for s in range(n - i):
        print(" ", end="")
    for s in range(2 * i - 1):
        print("*", end="")
    print()
```

</details>

---

### 29. Guess the Number Game — *Loops + Conditionals*

Write a number guessing game. The secret number is `42`. The program should:

1. Ask the user to guess the number.
2. If the guess is too high, print `"Too high!"`.
3. If the guess is too low, print `"Too low!"`.
4. If the guess is correct, print `"Correct!"` and tell them how many attempts it took.
5. Keep looping until the user guesses correctly.

<details>
<summary>Show Answer</summary>

```python
secret = 42
attempts = 0

while True:
    guess = int(input("Guess the number: "))
    attempts = attempts + 1

    if guess > secret:
        print("Too high!")
    elif guess < secret:
        print("Too low!")
    else:
        print("Correct!")
        print("It took you", attempts, "attempts.")
        break
```

</details>

---

### 30. Diamond Pattern — *Nested Loops*

Write a program that reads a number `n` and prints a diamond shape of stars.

Example for `n = 5`:

```
    *
   ***
  *****
 *******
*********
 *******
  *****
   ***
    *
```

> **Hint:** The top half is a centered pyramid (rows 1 to n). The bottom half is an inverted pyramid (rows n−1 down to 1). Use two separate sets of nested loops.

<details>
<summary>Show Answer</summary>

```python
n = int(input("Enter the number of rows for the top half: "))

# Top half (including the middle row)
for i in range(1, n + 1):
    for s in range(n - i):
        print(" ", end="")
    for s in range(2 * i - 1):
        print("*", end="")
    print()

# Bottom half
for i in range(n - 1, 0, -1):
    for s in range(n - i):
        print(" ", end="")
    for s in range(2 * i - 1):
        print("*", end="")
    print()
```

</details>

---

*End of worksheet — good luck!*

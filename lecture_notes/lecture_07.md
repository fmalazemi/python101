# Lecture 7: `for` Loops and the `range()` Function

---

## Table of Contents

1. [Learning Objectives](#1-learning-objectives)
2. [Why This Topic Matters](#2-why-this-topic-matters)
3. [Introduction](#3-introduction)
4. [The Structure of a `for` Loop](#4-the-structure-of-a-for-loop)
   - 4.1 [The Loop Variable](#41-the-loop-variable)
   - 4.2 [Try It Yourself](#42-try-it-yourself)
5. [The `range()` Function](#5-the-range-function)
   - 5.1 [`range(stop)`](#51-rangestop)
   - 5.2 [`range(start, stop)`](#52-rangestart-stop)
   - 5.3 [`range(start, stop, step)`](#53-rangestart-stop-step)
   - 5.4 [Try It Yourself](#54-try-it-yourself)
6. [Practical Examples](#6-practical-examples)
   - 6.1 [Printing a Series of Numbers](#61-printing-a-series-of-numbers)
   - 6.2 [Calculating a Total (Summation)](#62-calculating-a-total-summation)
   - 6.3 [Displaying a Simple Pattern](#63-displaying-a-simple-pattern)
7. [`for` Loops vs. `while` Loops](#7-for-loops-vs-while-loops)
8. [Common Mistakes](#8-common-mistakes)
9. [Summary](#9-summary)
10. [Exercises](#10-exercises)

---

## 1. Learning Objectives

By the end of this lecture, you will be able to:

- Explain what a `for` loop is and when to use it.
- Write a `for` loop using the `range()` function.
- Use the three forms of `range()`: `range(stop)`, `range(start, stop)`, and `range(start, stop, step)`.
- Use a `for` loop to print numbers, calculate totals, and display text patterns.
- Explain the difference between a `for` loop and a `while` loop.
- Identify and avoid common mistakes, including off-by-one errors.

---

## 2. Why This Topic Matters

In programming, one of the most common tasks is repeating an action a specific number of times. For example:

- Print a greeting message 10 times.
- Add up the numbers from 1 to 100.
- Display a row of stars for a pattern.

Writing the same line of code many times is inefficient and impractical. The `for` loop solves this problem. It allows you to instruct Python to repeat a block of code a defined number of times — automatically and cleanly.

The `for` loop is one of the most frequently used tools in Python programming. Mastering it will allow you to write programs that process lists of data, repeat calculations, and generate output patterns.

---

## 3. Introduction

A **loop** is a programming structure that repeats a block of code multiple times. In Lecture 6, you learned about the `while` loop, which repeats code as long as a condition is `True`.

The **`for` loop** is different. You use it when you know exactly **how many times** you want to repeat something.

### Analogy: The Instruction Card

Imagine you have a stack of 5 identical instruction cards. Each card says: *"Do this action."* You pick up each card one by one, follow the instruction, and stop when the stack is empty. The `for` loop works in exactly the same way — it repeats an action for every item in a defined sequence, then stops automatically.

The `range()` function is the tool that creates that sequence of numbers for the loop to work through.

---

## 4. The Structure of a `for` Loop

A `for` loop in Python has the following structure:

```python
for variable in sequence:
    # code to repeat
```

- `for` — the keyword that starts the loop.
- `variable` — a name you choose. It holds the current value from the sequence on each repetition.
- `in` — a keyword connecting the variable to the sequence.
- `sequence` — a series of values the loop will go through (often created with `range()`).
- The **indented block** — the code that runs on every repetition.

Here is the simplest example:

```python
for i in range(5):
    print("Hello!")
```

**Output:**
```
Hello!
Hello!
Hello!
Hello!
Hello!
```

**Explanation:** The loop runs 5 times. On each repetition, Python executes `print("Hello!")`. The word `Hello!` appears 5 times in total.

---

### 4.1 The Loop Variable

The **loop variable** (named `i` in the example above) automatically takes a new value from the sequence on each repetition of the loop. You can use this variable inside the loop body.

```python
for i in range(5):
    print(i)
```

**Output:**
```
0
1
2
3
4
```

**Explanation:** By default, `range(5)` generates the numbers 0, 1, 2, 3, and 4 — **not** 1 to 5. On each repetition, `i` takes the next value in that sequence and `print(i)` displays it. This is an important detail that will be discussed further in Section 5.

> **Note on naming:** The name `i` is a common convention for loop variables because it stands for *index* (position). However, you may use any valid variable name. A descriptive name is often more readable, for example `for number in range(10)`.

---

### 4.2 Try It Yourself

Open your Python environment and try the following:

1. Run the example above. Observe which number the loop starts from and which number it ends at.
2. Change `range(5)` to `range(10)`. How many lines are printed?
3. Change `print(i)` to `print(i * 2)`. What do you observe?

---

## 5. The `range()` Function

The `range()` function generates a sequence of integers (whole numbers). It is used with `for` loops to control how many times the loop runs and which values the loop variable takes.

There are three ways to use `range()`:

---

### 5.1 `range(stop)`

```python
range(stop)
```

Generates integers from **0** up to, but **not including**, `stop`.

```python
for i in range(4):
    print(i)
```

**Output:**
```
0
1
2
3
```

**Explanation:** `range(4)` produces the values 0, 1, 2, 3. It stops before reaching 4. The sequence contains exactly **4** numbers.

| Call | Values Produced |
|------|----------------|
| `range(3)` | 0, 1, 2 |
| `range(5)` | 0, 1, 2, 3, 4 |
| `range(1)` | 0 |

---

### 5.2 `range(start, stop)`

```python
range(start, stop)
```

Generates integers from `start` up to, but **not including**, `stop`.

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

**Explanation:** `range(1, 6)` starts at 1 and stops before 6. This is useful when you want to work with numbers beginning from 1 instead of 0.

| Call | Values Produced |
|------|----------------|
| `range(1, 5)` | 1, 2, 3, 4 |
| `range(3, 8)` | 3, 4, 5, 6, 7 |
| `range(10, 13)` | 10, 11, 12 |

---

### 5.3 `range(start, stop, step)`

```python
range(start, stop, step)
```

Generates integers from `start` up to, but **not including**, `stop`, advancing by `step` each time.

```python
for i in range(0, 10, 2):
    print(i)
```

**Output:**
```
0
2
4
6
8
```

**Explanation:** The loop starts at 0 and increases by 2 each time. It stops before reaching 10.

You can also use a **negative step** to count downwards:

```python
for i in range(5, 0, -1):
    print(i)
```

**Output:**
```
5
4
3
2
1
```

**Explanation:** The loop starts at 5, decreases by 1 each time (`step = -1`), and stops before reaching 0.

| Call | Values Produced |
|------|----------------|
| `range(0, 10, 2)` | 0, 2, 4, 6, 8 |
| `range(1, 10, 3)` | 1, 4, 7 |
| `range(10, 0, -2)` | 10, 8, 6, 4, 2 |

---

### 5.4 Try It Yourself

Experiment with the following exercises in your Python environment:

1. Use `range(2, 11)` in a loop and print each number. What is the first number? What is the last?
2. Use `range(0, 20, 5)` and print each number. What values appear?
3. Use `range(10, 0, -1)` to count down from 10 to 1.
4. What happens if you write `range(5, 5)`? Run it and observe the result.

---

## 6. Practical Examples

This section demonstrates how `for` loops and `range()` are used to solve small, realistic tasks.

---

### 6.1 Printing a Series of Numbers

**Task:** Print the numbers from 1 to 10, one per line.

```python
for number in range(1, 11):
    print(number)
```

**Output:**
```
1
2
3
4
5
6
7
8
9
10
```

**Explanation:** `range(1, 11)` generates 1 through 10. The loop variable is named `number` to make the code more readable. On each repetition, `print(number)` displays the current value.

> **Try it yourself:** Modify the code to print only the **even** numbers from 2 to 20. Hint: use `range(2, 21, 2)`.

---

### 6.2 Calculating a Total (Summation)

**Task:** Calculate the sum of all integers from 1 to 5.

```python
total = 0

for i in range(1, 6):
    total = total + i

print("The total is:", total)
```

**Output:**
```
The total is: 15
```

**Explanation:**

- `total` is initialised to 0 before the loop begins. This is a variable that **accumulates** (collects) the running sum.
- On each repetition, the current value of `i` is added to `total`.
- The loop runs for `i = 1, 2, 3, 4, 5`.
- After the loop ends, `total` holds the final sum: 1 + 2 + 3 + 4 + 5 = 15.
- `print()` is **outside** the loop (not indented), so it runs only once, after all repetitions are complete.

The table below shows the value of `total` after each repetition:

| Repetition | `i` | `total` after addition |
|-----------|-----|------------------------|
| 1 | 1 | 1 |
| 2 | 2 | 3 |
| 3 | 3 | 6 |
| 4 | 4 | 10 |
| 5 | 5 | 15 |

> **Try it yourself:** Modify the program to calculate the sum of integers from 1 to 100. Only one number needs to change.

---

### 6.3 Displaying a Simple Pattern

**Task:** Print a triangle pattern of stars with 5 rows.

```python
for i in range(1, 6):
    print("*" * i)
```

**Output:**
```
*
**
***
****
*****
```

**Explanation:** On each repetition, `"*" * i` produces a string of `i` asterisks. When `i = 1`, the result is `"*"`. When `i = 3`, the result is `"***"`. This creates a growing triangle shape.

> **Try it yourself:**
> 1. Change `range(1, 6)` to `range(1, 8)`. How does the output change?
> 2. Replace `"*"` with `"-"`. What is the new output?
> 3. Try to print the triangle in reverse order (5 stars on the first line, 1 on the last). Hint: use `range(5, 0, -1)`.

---

## 7. `for` Loops vs. `while` Loops

Both `for` and `while` loops repeat code. However, they are best suited for different situations.

| Feature | `for` Loop | `while` Loop |
|---|---|---|
| Best used when | You know **exactly** how many times to repeat | You repeat until a **condition** becomes `False` |
| Counting | Handles counting automatically with `range()` | You must update the counter manually |
| Risk of infinite loop | Very low — `range()` has a defined end | Higher — if condition never becomes `False`, the loop never stops |
| Common use case | Iterating over a fixed sequence | Waiting for user input, unknown number of repetitions |

**Use a `for` loop when:** you want to repeat something a specific, known number of times (e.g., "repeat 10 times", "go through 5 items").

**Use a `while` loop when:** you want to repeat something until a condition changes, and you do not know in advance how many repetitions will be needed (e.g., "keep asking until the user types a valid number").

### Comparison Example

The following two programs produce the same output. Study the differences:

**Using a `for` loop:**

```python
for i in range(1, 4):
    print(i)
```

**Using a `while` loop:**

```python
i = 1
while i < 4:
    print(i)
    i = i + 1
```

**Output (both programs):**
```
1
2
3
```

**Observation:** The `for` loop is shorter and less error-prone for this task. The `while` loop requires you to initialise `i`, check the condition, and increment `i` manually. Forgetting the increment (`i = i + 1`) would cause an infinite loop.

---

## 8. Common Mistakes

### Mistake 1: Off-by-One Error with `range()`

A very common mistake is using the wrong stop value in `range()`, which causes the loop to run one time too many or one time too few.

**Incorrect — intended to print 1 to 5, but prints 1 to 4:**

```python
for i in range(1, 5):
    print(i)
```

**Output:**
```
1
2
3
4
```

**Correct — prints 1 to 5:**

```python
for i in range(1, 6):
    print(i)
```

**Explanation:** `range(start, stop)` stops **before** `stop`. To include the number 5, the stop value must be 6.

---

### Mistake 2: Assuming `range()` Starts at 1

Many beginners assume that `range(5)` produces 1, 2, 3, 4, 5. It does not.

**Incorrect assumption:**

```python
for i in range(5):
    print(i)
# Student expects: 1, 2, 3, 4, 5
```

**Actual output:**
```
0
1
2
3
4
```

**Correct — if you want 1 to 5:**

```python
for i in range(1, 6):
    print(i)
```

**Explanation:** `range(n)` always starts at 0. If you need to start from 1, use `range(1, n+1)`.

---

### Mistake 3: Incorrect Indentation

Python uses indentation (spaces at the start of a line) to define which code belongs inside the loop. If the indentation is wrong, the program will not behave as expected.

**Incorrect — `print` is outside the loop:**

```python
for i in range(3):
    total = i + 1
print(total)  # runs only once, after the loop
```

**Correct — `print` is inside the loop:**

```python
for i in range(3):
    total = i + 1
    print(total)  # runs on every repetition
```

**Output (correct version):**
```
1
2
3
```

**Explanation:** Any statement that should run on every repetition must be indented inside the loop body. A statement at the original indentation level runs **after** the loop is finished.

---

### Mistake 4: Modifying the Loop Variable Inside the Loop

Changing the value of the loop variable inside the loop body does not affect how many times the loop runs. `range()` has already determined the sequence.

**Incorrect assumption — trying to skip numbers by modifying `i`:**

```python
for i in range(5):
    i = i + 2  # This has no lasting effect
    print(i)
```

**Output:**
```
2
3
4
5
6
```

**Explanation:** On each new repetition, Python assigns the next value from `range(5)` to `i`, overwriting any changes made inside the loop. To skip numbers, use the `step` argument in `range()` instead: `range(0, 10, 3)`.

---

### Mistake 5: Using a Negative Step Without Adjusting `start` and `stop`

When counting downwards, beginners sometimes forget that `start` must be greater than `stop`.

**Incorrect — produces no output:**

```python
for i in range(1, 5, -1):
    print(i)
```

**Output:** *(nothing)*

**Correct — counts down from 5 to 1:**

```python
for i in range(5, 0, -1):
    print(i)
```

**Output:**
```
5
4
3
2
1
```

**Explanation:** When the step is negative, `start` must be **greater than** `stop`. If `start` is less than or equal to `stop` with a negative step, the range is empty and the loop never runs.

---

## 9. Summary

This lecture introduced the `for` loop and the `range()` function — two fundamental tools for repeating actions a known number of times in Python.

**Key concepts:**

- A `for` loop repeats a block of code for every value in a given sequence.
- The **loop variable** automatically holds the current value from the sequence on each repetition.
- `range(stop)` — generates integers from 0 up to (not including) `stop`.
- `range(start, stop)` — generates integers from `start` up to (not including) `stop`.
- `range(start, stop, step)` — generates integers with a custom interval and supports negative steps for counting down.
- Use a `for` loop when the number of repetitions is known in advance.
- Use a `while` loop when repetition depends on a condition that may change unpredictably.
- Common mistakes include off-by-one errors, assuming `range()` starts at 1, and incorrect indentation.

**Quick reference:**

```python
# Basic for loop
for i in range(5):          # runs 5 times: i = 0, 1, 2, 3, 4
    print(i)

# Starting from 1
for i in range(1, 6):       # i = 1, 2, 3, 4, 5
    print(i)

# Custom step
for i in range(0, 10, 2):   # i = 0, 2, 4, 6, 8
    print(i)

# Counting down
for i in range(5, 0, -1):   # i = 5, 4, 3, 2, 1
    print(i)
```

**Next lecture:** Lists — storing and working with collections of values.

---

## 10. Exercises

Complete the following exercises. Write and run your code in your Python environment.

---

### Part A: Understanding Questions

Answer the following questions in your own words.

1. What is the difference between a `for` loop and a `while` loop? When would you choose one over the other?

2. What values does `range(1, 8)` produce? Write them out.

3. What values does `range(0, 15, 3)` produce? Write them out.

4. Explain what the loop variable does. What happens to it on each repetition of the loop?

5. Why is `range(5)` not the same as `range(1, 6)`?

---

### Part B: Code Tracing

Read each program carefully and write the output **without running the code first**. Then run the code to check your answer.

**Exercise 1:**

```python
for i in range(3):
    print(i * 3)
```

**Exercise 2:**

```python
total = 0
for i in range(1, 5):
    total = total + i
    print(total)
```

**Exercise 3:**

```python
for i in range(10, 4, -2):
    print(i)
```

**Exercise 4:**

```python
for i in range(4):
    print("=" * (i + 1))
```

---

### Part C: Code Writing

Write a Python program for each of the following tasks.

**Exercise 5:**  
Print all odd numbers from 1 to 19. Use `range()` with a step value.

**Exercise 6:**  
Write a program that uses a `for` loop to calculate and print the **product** (multiplication result) of all integers from 1 to 5. The final answer should be 120.

> Hint: Initialise a variable `product = 1` before the loop. Multiply it by `i` on each repetition.

**Exercise 7:**  
Write a program that asks the user to enter a number `n`, and then prints all multiples of 3 from 3 up to and including `n * 3`.

Example: If the user enters `5`, the output should be:
```
3
6
9
12
15
```

**Exercise 8:**  
Write a program that prints the following pattern using a `for` loop:
```
1
22
333
4444
55555
```

> Hint: On row `i`, you need to print the digit `i` repeated `i` times. Use `str(i) * i`.

---

### Part D: Code Modification

Read each program and make the required changes.

**Exercise 9:**  
The following program is intended to print the numbers from 1 to 10, but it has an off-by-one error. Find and fix the mistake.

```python
for i in range(1, 10):
    print(i)
```

**Exercise 10:**  
The program below calculates a sum, but the `print` statement is in the wrong position. The programmer wants to display only the **final total**, not the running sum after each step. Fix the indentation so that the output is a single line showing the final total.

```python
total = 0
for i in range(1, 6):
    total = total + i
    print("Final total:", total)
```

**Exercise 11 (Challenge):**  
The following program prints a countdown from 5 to 1, but it is written using a `while` loop. Rewrite it using a `for` loop. Your output must be identical.

```python
i = 5
while i >= 1:
    print(i)
    i = i - 1
print("Go!")
```

Expected output:
```
5
4
3
2
1
Go!
```

---

*End of Lecture 7*

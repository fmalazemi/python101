# Lecture 4: Making Decisions with `if`, `elif`, and `else`

---

## Learning Objectives

By the end of this lecture, you will be able to:

- Explain what a conditional statement is and why it is useful
- Use `if`, `elif`, and `else` to control the flow of a program
- Write and apply comparison operators: `==`, `!=`, `>`, `<`, `>=`, `<=`
- Recognise and fix common mistakes in conditional statements
- Build small programs that make decisions based on user input

---

## Why This Topic Matters

Every useful program must respond differently to different situations. A grade calculator must display "Pass" for some scores and "Fail" for others. A login system must accept correct passwords and reject incorrect ones. A weather app must recommend an umbrella when it rains.

Without the ability to make decisions, a program would do the same thing every time, regardless of the input. Conditional statements give your program the ability to choose between actions. This is one of the most fundamental skills in programming.

---

## 1. Introduction

### What Is a Conditional Statement?

A **conditional statement** is an instruction that tells the program: *"Do this only if a certain condition is true."*

Think of a traffic light. When the light is red, you stop. When it is green, you go. The driver makes a decision based on what the light shows. A conditional statement works the same way — the program checks a condition and then decides what to do.

In Python, the main tools for making decisions are the keywords `if`, `elif`, and `else`.

---

## 2. Comparison Operators

Before writing conditional statements, you need to understand how Python compares values. A **comparison operator** compares two values and returns either `True` or `False`. These two values are called **Boolean values**.

| Operator | Meaning                  | Example   | Result  |
|----------|--------------------------|-----------|---------|
| `==`     | Equal to                 | `5 == 5`  | `True`  |
| `!=`     | Not equal to             | `5 != 3`  | `True`  |
| `>`      | Greater than             | `7 > 3`   | `True`  |
| `<`      | Less than                | `2 < 6`   | `True`  |
| `>=`     | Greater than or equal to | `5 >= 5`  | `True`  |
| `<=`     | Less than or equal to    | `4 <= 3`  | `False` |

> **Important note:** The operator `==` checks if two values are equal. The operator `=` assigns a value to a variable. These are two different things. Confusing them is one of the most common beginner mistakes.

### Try It Yourself

Open your Python environment and type these lines one at a time. Observe the result:

```python
print(10 == 10)
print(10 == 9)
print(7 > 3)
print(4 <= 4)
print(5 != 5)
```

Each line prints either `True` or `False`. You are seeing how Python evaluates comparisons.

---

## 3. The `if` Statement

### Explanation

The `if` statement tells Python: *"Run this block of code only if the condition is true."* If the condition is false, Python skips the block entirely.

The structure is:

```
if condition:
    # code to run if the condition is true
```

The colon (`:`) after the condition is required. The code inside the block must be **indented** — moved to the right by one level (usually four spaces). Indentation tells Python which lines belong to the `if` block.

### Analogy

Imagine a door with a sign: *"Enter only if you have a ticket."* If you have a ticket, you enter. If you do not, you walk past without entering. The `if` statement works exactly like this sign.

### Worked Example — Checking a Positive Number

```python
number = 8

if number > 0:
    print("The number is positive.")
```

**Output:**
```
The number is positive.
```

**Explanation:** Python checks whether `number > 0`. Since `8 > 0` is `True`, it runs the indented line and prints the message.

Now change `number = 8` to `number = -3` and run it again. Nothing is printed, because `-3 > 0` is `False` and the block is skipped.

### Try It Yourself

Write a program that stores a temperature value and prints `"It is hot."` only if the temperature is greater than `35`.

---

## 4. The `if`–`else` Statement

### Explanation

The `else` statement provides an alternative action. It says: *"If the condition is true, do this. Otherwise, do that."*

```
if condition:
    # code to run if the condition is true
else:
    # code to run if the condition is false
```

Only one of the two blocks will ever run — never both.

### Analogy

You check the weather before leaving home. *If it is raining, take an umbrella. Otherwise, leave without one.* There are exactly two possibilities, and you choose one based on the condition.

### Worked Example — Pass or Fail

```python
score = 55

if score >= 50:
    print("Result: Pass")
else:
    print("Result: Fail")
```

**Output:**
```
Result: Pass
```

**Explanation:** Python checks whether `score >= 50`. Since `55 >= 50` is `True`, it runs the first block. If `score` were `40`, the condition would be `False` and the program would print `"Result: Fail"` instead.

### Worked Example — Even or Odd

```python
number = 7

if number % 2 == 0:
    print("The number is even.")
else:
    print("The number is odd.")
```

**Output:**
```
The number is odd.
```

**Explanation:** The `%` operator gives the remainder of a division. `7 % 2` equals `1`, not `0`, so the condition `number % 2 == 0` is `False`. Python runs the `else` block.

### Try It Yourself

Modify the pass/fail example above:

1. Change the score to `49`. What is the output?
2. Change the passing threshold from `50` to `60`. Run it again with the original score of `55`.

---

## 5. The `if`–`elif`–`else` Statement

### Explanation

Sometimes there are more than two possibilities. The `elif` keyword (short for *else if*) lets you check multiple conditions in sequence. Python checks each condition from top to bottom and runs only the first block whose condition is `True`. If none of the conditions are true, the `else` block runs.

```
if condition_1:
    # code if condition_1 is true
elif condition_2:
    # code if condition_2 is true
elif condition_3:
    # code if condition_3 is true
else:
    # code if none of the above are true
```

You may use as many `elif` branches as needed. The `else` at the end is optional, but it is good practice to include it as a safety net.

### Analogy

Think of a traffic light with three colours. *If the light is green, go. Else if the light is yellow, slow down. Else if the light is red, stop.* Each colour leads to a different action, and you check each one in order.

### Worked Example — Grade Classification

```python
score = 72

if score >= 90:
    print("Grade: A")
elif score >= 75:
    print("Grade: B")
elif score >= 60:
    print("Grade: C")
elif score >= 50:
    print("Grade: D")
else:
    print("Grade: F")
```

**Output:**
```
Grade: C
```

**Explanation:** Python checks each condition in order:
- `72 >= 90` → `False` → move to next
- `72 >= 75` → `False` → move to next
- `72 >= 60` → `True` → print `"Grade: C"` and stop

Python does not check the remaining conditions once it finds the first `True` result.

### Worked Example — Age Category

```python
age = 16

if age < 13:
    print("Child")
elif age < 18:
    print("Teenager")
elif age < 65:
    print("Adult")
else:
    print("Senior")
```

**Output:**
```
Teenager
```

**Explanation:** `16 < 13` is `False`. `16 < 18` is `True`, so Python prints `"Teenager"` and stops.

### Try It Yourself

Add a new `elif` branch to the grade example that prints `"Grade: A+"` for scores of `100` or above. Where should this new branch be placed? Why?

---

## 6. Indentation — A Critical Rule in Python

### Explanation

**Indentation** means adding spaces at the beginning of a line to show that it belongs to a block of code. In Python, indentation is not optional — it is a rule of the language.

The standard is to use **four spaces** for each level of indentation. Most code editors do this automatically when you press the `Tab` key.

### What Happens Without Indentation

```python
# Incorrect — this will cause an error
score = 80
if score >= 50:
print("Pass")
```

**Error message:**
```
IndentationError: expected an indented block after 'if' statement
```

**Corrected version:**

```python
score = 80
if score >= 50:
    print("Pass")
```

The four spaces before `print("Pass")` tell Python that this line belongs to the `if` block.

### Worked Example — Multiple Lines in a Block

You can have more than one line inside a block, as long as each line is indented equally.

```python
temperature = 38

if temperature > 37.5:
    print("You have a fever.")
    print("Please rest and drink water.")
    print("Consider seeing a doctor.")
else:
    print("Your temperature is normal.")
```

**Output:**
```
You have a fever.
Please rest and drink water.
Consider seeing a doctor.
```

All three `print` statements are at the same indentation level, so all three belong to the `if` block.

---

## 7. Using `if` with User Input

In real programs, the condition often depends on input from the user. The following example combines `input()`, type conversion, and a conditional statement.

### Worked Example — Voting Eligibility

```python
age = int(input("Enter your age: "))

if age >= 18:
    print("You are eligible to vote.")
else:
    print("You are not yet eligible to vote.")
```

**Sample run (user enters 20):**
```
Enter your age: 20
You are eligible to vote.
```

**Sample run (user enters 15):**
```
Enter your age: 15
You are not yet eligible to vote.
```

**Explanation:** The `input()` function always returns a string. The `int()` function converts that string to an integer so that the comparison `age >= 18` works correctly.

### Try It Yourself

Extend the voting eligibility program to also print `"You are exactly 18 — welcome to your first vote!"` when the user is exactly 18. You will need to adjust the `if`–`else` to an `if`–`elif`–`else`.

---

## 8. Common Mistakes and How to Avoid Them

### Mistake 1 — Using `=` Instead of `==`

**Incorrect:**
```python
score = 80
if score = 80:       # This is an assignment, not a comparison
    print("Correct score")
```

**Error message:**
```
SyntaxError: invalid syntax
```

**Correct:**
```python
score = 80
if score == 80:
    print("Correct score")
```

**Explanation:** A single `=` assigns a value. A double `==` compares two values. Inside an `if` condition, you almost always need `==`.

---

### Mistake 2 — Missing the Colon

**Incorrect:**
```python
if score >= 50
    print("Pass")
```

**Error message:**
```
SyntaxError: expected ':'
```

**Correct:**
```python
if score >= 50:
    print("Pass")
```

**Explanation:** Python requires a colon at the end of every `if`, `elif`, and `else` line.

---

### Mistake 3 — Missing Indentation

**Incorrect:**
```python
if score >= 50:
print("Pass")
```

**Error message:**
```
IndentationError: expected an indented block
```

**Correct:**
```python
if score >= 50:
    print("Pass")
```

**Explanation:** The body of an `if` block must be indented with four spaces (or one tab). Python uses indentation to understand the structure of your program.

---

### Mistake 4 — Comparing a String to a Number

**Incorrect:**
```python
age = input("Enter your age: ")
if age >= 18:
    print("Adult")
```

**Error message:**
```
TypeError: '>=' not supported between instances of 'str' and 'int'
```

**Correct:**
```python
age = int(input("Enter your age: "))
if age >= 18:
    print("Adult")
```

**Explanation:** The `input()` function always returns a string. You must convert it to an integer with `int()` before comparing it to a number.

---

### Mistake 5 — Placing `else` After Conditions Without `if`

**Incorrect:**
```python
else:
    print("None of the above")
```

**Error message:**
```
SyntaxError: invalid syntax
```

**Correct:**
```python
if score >= 90:
    print("A")
elif score >= 50:
    print("Pass")
else:
    print("Fail")
```

**Explanation:** `else` cannot stand alone. It must always follow an `if` (or an `elif`).

---

## 9. Summary

In this lecture, you learned how to make decisions in Python using conditional statements.

- A **comparison operator** compares two values and returns `True` or `False`.
- An **`if` statement** runs a block of code only when a condition is `True`.
- An **`if`–`else` statement** chooses between two blocks depending on whether a condition is `True` or `False`.
- An **`if`–`elif`–`else` statement** handles more than two possibilities by checking conditions in order.
- **Indentation** is mandatory in Python. The body of every `if`, `elif`, and `else` block must be indented by four spaces.
- Use `==` for comparison and `=` for assignment. Mixing these up is a very common mistake.
- Always convert user input with `int()` or `float()` before using it in a numeric comparison.

| Structure | Use When |
|---|---|
| `if` only | You want to do something only if a condition is true |
| `if`–`else` | You want to choose between exactly two actions |
| `if`–`elif`–`else` | You want to choose between three or more actions |

---

## Exercises

### Part A — Understanding Questions

1. What is the difference between `=` and `==` in Python? Give one example of each.

2. What does the following expression evaluate to? Explain your reasoning.
   ```python
   10 >= 10
   ```

3. In an `if`–`elif`–`else` chain, how many blocks will Python execute? Explain why.

4. What does Python do when the condition of an `if` statement is `False` and there is no `else` block?

5. Why must the body of an `if` statement be indented?

---

### Part B — Code Tracing

6. What is the output of the following program? Trace through it step by step.

   ```python
   x = 15

   if x > 20:
       print("Large")
   elif x > 10:
       print("Medium")
   else:
       print("Small")
   ```

7. What is the output of the following program?

   ```python
   a = 5
   b = 5

   if a != b:
       print("Different")
   else:
       print("Same")
   ```

8. Trace through the following program when the user enters `42`. What is printed?

   ```python
   number = int(input("Enter a number: "))

   if number > 0:
       print("Positive")
   elif number < 0:
       print("Negative")
   else:
       print("Zero")
   ```

---

### Part C — Code Writing

9. Write a program that asks the user to enter a number. If the number is even, print `"Even"`. If it is odd, print `"Odd"`.
   *(Hint: Use the `%` operator. A number is even if `number % 2 == 0`.)*

10. Write a program that asks the user to enter a password. If the password is `"python123"`, print `"Access granted"`. Otherwise, print `"Access denied"`.

11. Write a program that asks the user to enter a temperature in Celsius. Print one of the following messages based on the value:
    - Below `0`: `"Freezing"`
    - Between `0` and `15` (inclusive): `"Cold"`
    - Between `16` and `25` (inclusive): `"Comfortable"`
    - Above `25`: `"Hot"`

12. Write a program that asks the user to enter two numbers. Print which one is greater, or print `"They are equal"` if both are the same.

---

### Part D — Code Modification

13. The following program has an error. Find and fix it.

    ```python
    score = 75
    if score = 75:
        print("Perfect score!")
    ```

14. The following program has an indentation error. Correct it so that it runs properly.

    ```python
    age = 20
    if age >= 18:
    print("You may enter.")
    else:
    print("Entry not allowed.")
    ```

15. The following program asks the user for a number but crashes when a number is entered. Explain why, and fix the error.

    ```python
    number = input("Enter a number: ")
    if number > 0:
        print("Positive")
    else:
        print("Not positive")
    ```

16. Extend the following program so that it also prints `"Excellent!"` when the score is greater than or equal to `95`, before checking for `"Pass"` or `"Fail"`.

    ```python
    score = int(input("Enter your score: "))

    if score >= 50:
        print("Pass")
    else:
        print("Fail")
    ```

---

*End of Lecture 4*

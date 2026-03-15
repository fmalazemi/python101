# Lecture 5: Logical Operators and Nested Conditions

---

## Table of Contents

1. [Learning Objectives](#learning-objectives)
2. [Why This Topic Matters](#why-this-topic-matters)
3. [Introduction](#introduction)
4. [The Concept of Truth in Programming](#the-concept-of-truth-in-programming)
5. [Logical Operator: `and`](#logical-operator-and)
6. [Logical Operator: `or`](#logical-operator-or)
7. [Logical Operator: `not`](#logical-operator-not)
8. [Combining Multiple Conditions](#combining-multiple-conditions)
9. [Nested `if` Statements](#nested-if-statements)
10. [A Warning: Keeping Conditions Simple](#a-warning-keeping-conditions-simple)
11. [Common Mistakes and Misconceptions](#common-mistakes-and-misconceptions)
12. [Summary](#summary)
13. [Exercises](#exercises)

---

## Learning Objectives

By the end of this lecture, you will be able to:

- Use the logical operators `and`, `or`, and `not` to build compound conditions
- Explain the difference between `and` and `or`
- Use `not` to reverse the result of a condition
- Write nested `if` statements to handle multi-level decisions
- Identify and avoid common errors when combining conditions

---

## Why This Topic Matters

In previous lectures, you learned how to make simple decisions using `if`, `elif`, and `else`. However, real-world decisions rarely depend on just one condition.

Consider these situations:

- A website allows login **only if** a username is correct **and** a password is correct.
- A store offers a discount **if** a customer is a student **or** a senior citizen.
- A system sends an alert **if** the temperature is **not** within a safe range.

Without logical operators, you would need to write many separate `if` statements to handle such cases. Logical operators allow you to express these decisions clearly in a single condition.

---

## Introduction

A **logical operator** is a special word that connects two or more conditions and produces a single `True` or `False` result.

Python provides three logical operators:

| Operator | Meaning                                      |
|----------|----------------------------------------------|
| `and`    | True only if **both** conditions are true    |
| `or`     | True if **at least one** condition is true   |
| `not`    | Reverses the truth value of a condition      |

These operators allow you to write programs that make more precise and realistic decisions.

---

## The Concept of Truth in Programming

Before studying logical operators, it is helpful to understand how Python treats `True` and `False`.

Every condition in Python evaluates to one of two values:

- `True` — the condition is satisfied
- `False` — the condition is not satisfied

These are called **Boolean values**, named after the mathematician George Boole. You have already used Boolean values in `if` statements. For example:

```python
age = 20
print(age >= 18)   # Output: True
print(age < 10)    # Output: False
```

**Explanation:**  
The expression `age >= 18` checks whether the value of `age` is greater than or equal to 18. Since `age` is 20, the result is `True`. The expression `age < 10` is `False` because 20 is not less than 10.

Logical operators work by combining these `True` and `False` values to produce a new result.

---

## Logical Operator: `and`

### Explanation

The `and` operator combines two conditions. The result is `True` **only if both conditions are true**. If either condition is `False`, the entire expression is `False`.

**Analogy:** Think of a security checkpoint at an event. You are allowed to enter only if you have a valid ticket **and** your name is on the guest list. If either condition fails, you cannot enter — both must be satisfied.

### Syntax

```python
condition_one and condition_two
```

### Truth Table for `and`

| Condition A | Condition B | A `and` B |
|-------------|-------------|-----------|
| True        | True        | **True**  |
| True        | False       | False     |
| False       | True        | False     |
| False       | False       | False     |

### Worked Example 1: Checking Age and Membership

```python
age = 25
is_member = True

if age >= 18 and is_member:
    print("Access granted.")
else:
    print("Access denied.")
```

**Output:**
```
Access granted.
```

**Explanation:**  
The condition checks two things: whether `age >= 18` (which is `True` because 25 >= 18) and whether `is_member` is `True`. Since both are `True`, the `and` expression evaluates to `True`, and the program prints `"Access granted."`.

Now change `is_member = False` and run the code again. The output changes to `"Access denied."` because the second condition is now `False`.

### Try It Yourself

- Change `age` to `15`. What is the output? Why?
- Change `is_member` to `False` while keeping `age = 25`. What happens?
- Add a third condition: check that `age <= 60` as well. What happens if `age = 70`?

---

## Logical Operator: `or`

### Explanation

The `or` operator combines two conditions. The result is `True` if **at least one** of the conditions is true. The result is `False` only if **both** conditions are false.

**Analogy:** A museum offers free admission to visitors who are students **or** senior citizens. You only need to satisfy one of these conditions to receive the discount — you do not need to be both.

### Syntax

```python
condition_one or condition_two
```

### Truth Table for `or`

| Condition A | Condition B | A `or` B  |
|-------------|-------------|-----------|
| True        | True        | True      |
| True        | False       | True      |
| False       | True        | True      |
| False       | False       | **False** |

### Worked Example 2: Museum Discount

```python
is_student = False
is_senior = True

if is_student or is_senior:
    print("You qualify for a free ticket.")
else:
    print("Full price applies.")
```

**Output:**
```
You qualify for a free ticket.
```

**Explanation:**  
`is_student` is `False`, but `is_senior` is `True`. Because at least one condition is `True`, the entire `or` expression evaluates to `True`, and the visitor receives the discount.

### Worked Example 3: Checking for Weekend

```python
day = "Saturday"

if day == "Saturday" or day == "Sunday":
    print("It is the weekend.")
else:
    print("It is a weekday.")
```

**Output:**
```
It is the weekend.
```

**Explanation:**  
The condition checks whether `day` equals `"Saturday"` or `"Sunday"`. Since `day` is `"Saturday"`, the first condition is `True`. The `or` operator returns `True`, so the program prints the weekend message.

### Try It Yourself

- Change `day` to `"Monday"`. What is the output?
- Change `day` to `"Sunday"`. Does the output change?
- Modify the program to also print `"Enjoy your day!"` if it is a weekend.

---

## Logical Operator: `not`

### Explanation

The `not` operator reverses the truth value of a condition. If a condition is `True`, `not` makes it `False`. If a condition is `False`, `not` makes it `True`.

**Analogy:** Imagine a sign that says "Entry allowed if the door is **not** locked." If the door is locked (`True`), then `not locked` is `False`, and entry is not allowed. If the door is unlocked (`False`), then `not locked` is `True`, and entry is allowed.

### Syntax

```python
not condition
```

### Truth Table for `not`

| Condition A | `not` A   |
|-------------|-----------|
| True        | **False** |
| False       | **True**  |

### Worked Example 4: Using `not`

```python
is_logged_in = False

if not is_logged_in:
    print("Please log in to continue.")
else:
    print("Welcome back!")
```

**Output:**
```
Please log in to continue.
```

**Explanation:**  
`is_logged_in` is `False`. The expression `not is_logged_in` becomes `not False`, which evaluates to `True`. Therefore, the `if` block runs and the user is asked to log in.

### Try It Yourself

- Change `is_logged_in` to `True`. What is the output?
- Rewrite the condition **without** using `not`. Does it produce the same result?
- Create a variable `is_banned = True`. Use `not` to allow access only if the user is not banned.

---

## Combining Multiple Conditions

You can combine `and`, `or`, and `not` in a single expression to write more complex conditions. However, Python evaluates these operators in a specific order:

1. `not` is evaluated first
2. `and` is evaluated second
3. `or` is evaluated last

It is strongly recommended to use **parentheses** to make the intended meaning clear, even when they are not strictly required.

### Worked Example 5: Combined Conditions

```python
age = 17
has_permission = True

if age >= 18 or has_permission:
    print("You may proceed.")
else:
    print("Access not allowed.")
```

**Output:**
```
You may proceed.
```

**Explanation:**  
`age >= 18` is `False` (17 is not >= 18), but `has_permission` is `True`. Because `or` only requires one condition to be `True`, the result is `True` and the user may proceed.

### Worked Example 6: Using Parentheses for Clarity

```python
temperature = 35
is_raining = False

if temperature > 30 and not is_raining:
    print("Good weather for outdoor activities.")
else:
    print("Stay indoors.")
```

**Output:**
```
Good weather for outdoor activities.
```

**Explanation:**  
The condition has two parts:
- `temperature > 30` → `True` (35 > 30)
- `not is_raining` → `not False` → `True`

Both parts are `True`, so the `and` expression is `True`.

### Try It Yourself

- Change `is_raining` to `True`. What is the output? Why?
- Change `temperature` to `25`. What happens?
- Add another condition using `or`: the message should also appear if `temperature` is below 10 (very cold but no rain).

---

## Nested `if` Statements

### Explanation

A **nested `if` statement** is an `if` statement written inside another `if` statement. This structure is used when a second decision depends on the result of a first decision.

**Analogy:** Imagine you are at a cinema. First, you check whether a ticket is available. If a ticket **is** available, you then check whether you can afford it. The second check only matters if the first check passes.

### Syntax

```python
if condition_one:
    if condition_two:
        # runs only if both conditions are true
```

### Worked Example 7: Cinema Ticket

```python
ticket_available = True
can_afford = True

if ticket_available:
    if can_afford:
        print("Enjoy the movie!")
    else:
        print("You cannot afford the ticket.")
else:
    print("Sorry, no tickets are available.")
```

**Output:**
```
Enjoy the movie!
```

**Explanation:**  
The outer `if` checks whether a ticket is available. Since `ticket_available` is `True`, the program enters the outer block. Inside, it checks whether the user can afford the ticket. Since `can_afford` is also `True`, it prints `"Enjoy the movie!"`.

Try changing `can_afford = False` and observe the output. Then change `ticket_available = False` and observe what happens.

### Worked Example 8: Grade Classification

This example shows nested conditions used to classify a student's grade.

```python
score = 72

if score >= 50:
    print("You have passed.")
    if score >= 90:
        print("Grade: A")
    elif score >= 75:
        print("Grade: B")
    else:
        print("Grade: C")
else:
    print("You have failed.")
```

**Output:**
```
You have passed.
Grade: C
```

**Explanation:**  
The outer `if` checks whether the student passed (score >= 50). Since 72 >= 50, it prints `"You have passed."`. The program then enters the nested structure to determine the grade. Since 72 is not >= 90 and not >= 75, it falls to the `else` branch and prints `"Grade: C"`.

### Try It Yourself

- Change `score` to `91`. What is the output?
- Change `score` to `45`. What is the output?
- Add a fourth grade level: print `"Grade: D"` for scores between 50 and 59.

---

## A Warning: Keeping Conditions Simple

As your programs grow, it can be tempting to write very long or complex conditions. This makes code difficult to read and increases the chance of errors.

**Problematic example:**

```python
if age >= 18 and age <= 65 and is_member and not is_banned and score > 50:
    print("Eligible.")
```

While this code may be correct, it is hard to read at a glance.

**Better approach — break it into steps:**

```python
is_valid_age = 18 <= age <= 65
is_eligible_member = is_member and not is_banned
has_passed = score > 50

if is_valid_age and is_eligible_member and has_passed:
    print("Eligible.")
```

**Why this is better:**
- Each condition is named clearly.
- The final `if` statement reads almost like an English sentence.
- If an error occurs, it is easier to identify which condition is wrong.

As a rule: if a condition requires more than two or three parts, consider splitting it into named Boolean variables first.

---

## Common Mistakes and Misconceptions

### Mistake 1: Using `and` when `or` is needed

**Wrong:**
```python
day = "Saturday"

if day == "Saturday" and day == "Sunday":
    print("It is the weekend.")
```

**Correct:**
```python
day = "Saturday"

if day == "Saturday" or day == "Sunday":
    print("It is the weekend.")
```

**Explanation:**  
A variable cannot equal two different values at the same time. The condition `day == "Saturday" and day == "Sunday"` is always `False`. Use `or` when checking whether a variable matches one of several possible values.

---

### Mistake 2: Forgetting to repeat the variable in comparisons

**Wrong:**
```python
colour = "red"

if colour == "red" or "blue":
    print("Match found.")
```

**Correct:**
```python
colour = "red"

if colour == "red" or colour == "blue":
    print("Match found.")
```

**Explanation:**  
In Python, `"blue"` on its own is a non-empty string, which is always treated as `True`. This means the condition in the wrong version is **always** `True`, regardless of the value of `colour`. Always write the full comparison for each value.

---

### Mistake 3: Misunderstanding `not`

**Wrong:**
```python
is_open = True

if not is_open == True:
    print("The shop is closed.")
```

**Correct:**
```python
is_open = True

if not is_open:
    print("The shop is closed.")
```

**Explanation:**  
The expression `not is_open` is clearer and equivalent to checking whether `is_open` is `False`. Avoid writing `not variable == True` as it adds unnecessary complexity.

---

### Mistake 4: Incorrect indentation in nested `if` statements

**Wrong:**
```python
has_ticket = True
is_adult = True

if has_ticket:
print("Ticket confirmed.")      # Missing indentation
    if is_adult:
        print("Adult entry.")
```

**Correct:**
```python
has_ticket = True
is_adult = True

if has_ticket:
    print("Ticket confirmed.")
    if is_adult:
        print("Adult entry.")
```

**Explanation:**  
Every block inside an `if` statement must be consistently indented. Python uses indentation to determine which lines belong to which block. Missing or inconsistent indentation causes an `IndentationError`.

---

### Mistake 5: Confusing `and` logic with everyday language

**Wrong thinking:**  
"Show a message if the user is not an admin and not a moderator" — a beginner might write:

```python
if not role == "admin" and "moderator":
    print("Access limited.")
```

**Correct:**
```python
role = "user"

if role != "admin" and role != "moderator":
    print("Access limited.")
```

**Explanation:**  
Each condition must be written as a complete comparison. The expression `and "moderator"` does not compare `role` to `"moderator"` — it simply evaluates `"moderator"` as a non-empty string, which is always `True`.

---

## Summary

In this lecture, you learned how to combine conditions using logical operators.

**Key concepts:**

- `and` — returns `True` only when **both** conditions are `True`
- `or` — returns `True` when **at least one** condition is `True`
- `not` — reverses a Boolean value: `True` becomes `False`, and `False` becomes `True`
- **Nested `if`** — an `if` statement placed inside another `if` statement, used when decisions depend on each other
- **Clarity rule** — when conditions become complex, use named Boolean variables to keep code readable

**Quick reference:**

```python
# and: both must be true
if age >= 18 and has_id:
    print("Entry allowed.")

# or: at least one must be true
if is_student or is_senior:
    print("Discount applied.")

# not: reverses the condition
if not is_logged_in:
    print("Please log in.")

# nested if
if has_ticket:
    if seat_available:
        print("Enjoy the show!")
```

In Lecture 6, you will learn about **loops** — a way to repeat actions in your program without writing the same code multiple times.

---

## Exercises

### Part A: Understanding Questions

**A1.**  
What is a logical operator? Name the three logical operators in Python and describe what each one does.

**A2.**  
Explain why the following condition is always `False`, regardless of the value of `day`:

```python
if day == "Monday" and day == "Tuesday":
```

**A3.**  
What is the result of each of the following expressions? Write `True` or `False` for each.

```python
True and False
True or False
not True
False or False
not False and True
```

**A4.**  
What is a nested `if` statement? Give a real-life situation where a nested `if` would be more appropriate than a single `if` with `and`.

---

### Part B: Code Tracing

**B1.**  
Read the following program carefully. Write the output without running it. Then run the program to check your answer.

```python
x = 10
y = 5

if x > 8 and y < 10:
    print("Condition A")
else:
    print("Condition B")
```

**B2.**  
Trace through the following code and write the output step by step.

```python
is_raining = True
has_umbrella = False

if is_raining and not has_umbrella:
    print("You will get wet.")
elif is_raining and has_umbrella:
    print("You are prepared.")
else:
    print("No rain today.")
```

**B3.**  
What does the following program print when `score = 82`? Trace each condition carefully.

```python
score = 82

if score >= 50:
    print("Passed")
    if score >= 80:
        print("Distinction")
    elif score >= 65:
        print("Merit")
    else:
        print("Pass")
else:
    print("Failed")
```

---

### Part C: Code Writing

**C1.**  
Write a program that asks the user to enter their age and whether they have a valid ID (`yes` or `no`). Print `"Entry allowed."` only if the user is 18 or older **and** has a valid ID. Otherwise, print `"Entry denied."`

**C2.**  
Write a program that asks the user to enter a number. Print `"In range"` if the number is between 1 and 100 (inclusive). Print `"Out of range"` otherwise.  
*(Hint: Use `and` to check both conditions at once.)*

**C3.**  
Write a program that asks the user to enter a day of the week. Print `"Weekend"` if the day is Saturday or Sunday. Print `"Weekday"` for any other input.

**C4.**  
Write a program that asks the user whether a library is open (`yes` or `no`) and whether they have a library card (`yes` or `no`). Use a nested `if` statement to print one of the following messages:
- `"You can borrow books."` — if the library is open **and** they have a card
- `"You need a library card."` — if the library is open but they have no card
- `"The library is closed."` — if the library is not open

---

### Part D: Code Modification

**D1.**  
The following program has a logic error. Find the error and correct it.

```python
number = 15

if number > 10 and number > 20:
    print("Number is greater than 20.")
elif number > 10:
    print("Number is between 11 and 20.")
else:
    print("Number is 10 or less.")
```

**D2.**  
Modify the program below so that it also prints `"Speed is acceptable."` if the speed is between 40 and 120 km/h (inclusive), and `"Speed is out of safe range."` otherwise.

```python
speed = int(input("Enter speed in km/h: "))
print(speed)
```

**D3.**  
The following program uses a nested `if`. Rewrite it using `and` so that it produces the same output but uses only a single `if`-`else` structure (no nesting).

```python
has_passport = True
has_visa = True

if has_passport:
    if has_visa:
        print("You may board the flight.")
    else:
        print("You need a visa.")
else:
    print("You need a passport.")
```

*(Note: Focus on the case where both conditions are true. Consider whether the rewritten version handles all cases the same way.)*

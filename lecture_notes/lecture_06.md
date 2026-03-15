# Lecture 6: Repetition with `while` Loops

---

## Table of Contents

1. [Why This Topic Matters](#why-this-topic-matters)
2. [Learning Objectives](#learning-objectives)
3. [Introduction](#introduction)
4. [The Structure of a `while` Loop](#the-structure-of-a-while-loop)
   - [The Loop Condition](#the-loop-condition)
   - [The Loop Body](#the-loop-body)
   - [The Update Step](#the-update-step)
5. [Tracing a Loop Step by Step](#tracing-a-loop-step-by-step)
6. [Counting with a `while` Loop](#counting-with-a-while-loop)
7. [Repeating Until the User Gives Correct Input](#repeating-until-the-user-gives-correct-input)
8. [Infinite Loops](#infinite-loops)
9. [Common Mistakes](#common-mistakes)
10. [Summary](#summary)
11. [Exercises](#exercises)

---

## Why This Topic Matters

Repetition is one of the most powerful ideas in programming. Consider these everyday tasks:

- A cashier scans items one by one until there are no more items.
- A student practises a vocabulary word until they can spell it correctly.
- An ATM asks for a PIN again and again until the correct PIN is entered.

Without loops, a program would need to repeat the same lines of code manually, once for each repetition. This is impractical and error-prone. The `while` loop allows a program to repeat a block of code automatically, as many times as needed, based on a condition. Mastering loops is an essential step toward writing useful, real-world programs.

---

## Learning Objectives

By the end of this lecture, you will be able to:

- Explain what a `while` loop is and why it is useful.
- Write a `while` loop with a correct condition, body, and update step.
- Trace a loop step by step to predict its output.
- Use a `while` loop to count and to validate user input.
- Recognise and avoid infinite loops.

---

## Introduction

In previous lectures, you learned how to make decisions using `if` statements. An `if` statement runs a block of code **once**, only when a condition is true. But what if you need to repeat an action **many times**?

A **loop** is a programming structure that repeats a block of code. Python provides more than one kind of loop. In this lecture, you will learn the **`while` loop**, which repeats a block of code **as long as a condition remains true**.

> **Analogy:** Think of a `while` loop like a security guard at a door. The guard checks a rule: *"Is this person on the list?"* As long as the answer is *"No"*, the guard keeps turning people away. The moment the answer is *"Yes"*, the guard stops checking and lets the person in. The loop keeps running *while* the condition is true and stops when the condition becomes false.

---

## The Structure of a `while` Loop

A `while` loop has three essential parts:

1. **The loop condition** — a Boolean expression that is checked before every repetition.
2. **The loop body** — the block of code that runs if the condition is true.
3. **The update step** — a statement inside the loop body that changes a value so that the condition will eventually become false.

Here is the general structure:

```python
while condition:
    # loop body
    # update step
```

- The word `while` begins the loop.
- The `condition` is evaluated before each repetition.
- If the condition is `True`, the loop body runs.
- If the condition is `False`, the loop stops and the program continues with the next statement after the loop.
- The loop body is indented (4 spaces), just like the body of an `if` statement.

---

### The Loop Condition

The **loop condition** is a Boolean expression — it evaluates to either `True` or `False`. Python checks this condition before every repetition of the loop.

- If the condition is `True` → the loop body runs.
- If the condition is `False` → the loop ends immediately.

If the condition is already `False` before the loop begins, the loop body will **never run**.

---

### The Loop Body

The **loop body** is the block of indented code that runs each time the condition is true. All lines inside the loop body must be indented consistently.

Each execution of the loop body is called one **iteration**.

---

### The Update Step

The **update step** is a statement inside the loop body that changes the value of the variable used in the condition. Without an update step, the condition never changes, and the loop runs forever.

> **Analogy:** Imagine you are climbing stairs. The condition is: *"Are there more steps?"* The update step is: *"Take one step."* Each time you take a step, you get closer to the top. Without taking a step, you would never reach the top — you would be stuck at the same stair forever.

---

## Tracing a Loop Step by Step

Tracing a loop means following the program line by line, recording the value of each variable at each step. This is an important skill for understanding and debugging loops.

Consider this simple loop:

```python
counter = 1

while counter <= 3:
    print(counter)
    counter = counter + 1

print("Done")
```

**Output:**
```
1
2
3
Done
```

Let us trace this loop step by step.

| Iteration | Value of `counter` before check | Condition `counter <= 3` | Action |
|-----------|----------------------------------|--------------------------|--------|
| Before loop | 1 | — | `counter` is set to 1 |
| 1st check | 1 | `True` | Print `1`, then `counter` becomes `2` |
| 2nd check | 2 | `True` | Print `2`, then `counter` becomes `3` |
| 3rd check | 3 | `True` | Print `3`, then `counter` becomes `4` |
| 4th check | 4 | `False` | Loop ends |
| After loop | — | — | Print `Done` |

Notice the following:
- The condition is checked **before** each iteration, not after.
- The update step (`counter = counter + 1`) increases `counter` by 1 each time.
- When `counter` reaches `4`, the condition `counter <= 3` becomes `False`, and the loop stops.

> **Try it yourself:** Run the code above. Then change `counter <= 3` to `counter <= 5`. What is the new output? Try to predict the result before running it.

---

## Counting with a `while` Loop

One of the most common uses of a `while` loop is **counting** — repeating something a specific number of times.

### Example 1: Count from 1 to 5

```python
number = 1

while number <= 5:
    print(number)
    number = number + 1
```

**Output:**
```
1
2
3
4
5
```

**Explanation:**
- `number` starts at `1`.
- The condition `number <= 5` is checked. It is `True`, so the loop body runs.
- `number` is printed, then increased by `1`.
- This repeats until `number` becomes `6`, at which point the condition is `False` and the loop ends.

> **Try it yourself:** Modify the program to count from `1` to `10`. Then modify it to count from `5` to `1` (counting down). Hint: use `number = number - 1` and adjust the condition.

---

### Example 2: Count Down from 5 to 1

```python
number = 5

while number >= 1:
    print(number)
    number = number - 1

print("Lift off!")
```

**Output:**
```
5
4
3
2
1
Lift off!
```

**Explanation:**
- This time, `number` starts at `5` and decreases by `1` each iteration.
- The condition `number >= 1` is true as long as `number` is 1 or greater.
- After printing `1`, `number` becomes `0`, the condition becomes `False`, and the loop ends.
- The program then prints `"Lift off!"`.

> **Try it yourself:** Change the starting number to `10`. Then change the message at the end to something of your choice.

---

### Example 3: Print the Sum of Numbers from 1 to 10

```python
total = 0
number = 1

while number <= 10:
    total = total + number
    number = number + 1

print("The sum is:", total)
```

**Output:**
```
The sum is: 55
```

**Explanation:**
- `total` starts at `0` and accumulates the sum.
- `number` starts at `1` and increases by `1` each iteration.
- In each iteration, the current value of `number` is added to `total`.
- After `number` exceeds `10`, the loop ends and the sum is printed.
- The variable `total` is called an **accumulator** because it collects a running total.

> **Try it yourself:** Modify the program to calculate the sum of numbers from `1` to `100`. Try to predict the result before running it.

---

## Repeating Until the User Gives Correct Input

A very practical use of the `while` loop is **input validation** — asking the user to enter a value again and again until they provide an acceptable answer.

### Example 4: Keep Asking Until the User Enters a Positive Number

```python
number = int(input("Enter a positive number: "))

while number <= 0:
    print("That is not a positive number. Please try again.")
    number = int(input("Enter a positive number: "))

print("Thank you! You entered:", number)
```

**Example interaction:**
```
Enter a positive number: -3
That is not a positive number. Please try again.
Enter a positive number: 0
That is not a positive number. Please try again.
Enter a positive number: 7
Thank you! You entered: 7
```

**Explanation:**
- The program asks for input once before the loop begins.
- The condition `number <= 0` checks whether the input is invalid.
- If the input is invalid, the user is asked to try again.
- The loop continues until the user enters a number greater than `0`.
- Notice that the `input()` statement appears **twice**: once before the loop (to get the first value) and once inside the loop (to get the next value if needed).

> **Try it yourself:** Modify the program to ask the user to enter a number between `1` and `10`. The loop should repeat until the user enters a valid number in that range.

---

### Example 5: Keep Asking Until the User Enters the Correct Password

```python
password = input("Enter the password: ")

while password != "python123":
    print("Incorrect password. Try again.")
    password = input("Enter the password: ")

print("Access granted.")
```

**Example interaction:**
```
Enter the password: hello
Incorrect password. Try again.
Enter the password: python
Incorrect password. Try again.
Enter the password: python123
Access granted.
```

**Explanation:**
- The condition `password != "python123"` is `True` as long as the entered password is wrong.
- The loop ends only when the user enters `"python123"` exactly.
- The string comparison is **case-sensitive**: `"Python123"` would not be accepted.

> **Try it yourself:** Change the password to a word of your choice. Then modify the program to also print how many attempts the user made before entering the correct password.

---

## Infinite Loops

An **infinite loop** is a loop that never stops because its condition never becomes `False`. Infinite loops are one of the most common mistakes beginners make.

### Example of an Infinite Loop

```python
# WARNING: Do not run this code as written.
counter = 1

while counter <= 5:
    print(counter)
    # The update step is missing!
```

**What happens:**
- `counter` starts at `1`.
- The condition `counter <= 5` is always `True` because `counter` never changes.
- The program prints `1` forever and never stops.

If you accidentally run an infinite loop, you can stop the program by pressing **Ctrl + C** in the terminal.

### Another Example of an Infinite Loop

```python
# WARNING: Do not run this code as written.
counter = 1

while counter <= 5:
    print(counter)
    counter = counter - 1  # Moving in the wrong direction!
```

**What happens:**
- `counter` starts at `1` and decreases: `0`, `-1`, `-2`, ...
- The condition `counter <= 5` is always `True` because `counter` keeps getting smaller.
- The loop never ends.

### How to Avoid Infinite Loops

Always ask yourself these three questions before running a `while` loop:

1. **Does the loop have a condition?** The condition must be a Boolean expression.
2. **Does the loop body change the variable used in the condition?** There must be an update step.
3. **Does the update step move toward making the condition false?** The variable must change in the right direction.

> **Analogy:** Imagine you are draining a bathtub. The condition is: *"Is there still water?"* The update step is: *"Pull the plug."* If you never pull the plug (missing update step), or if you keep adding water (wrong direction), the tub never empties. You are stuck in an infinite loop.

---

## Common Mistakes

### Mistake 1: Forgetting the Update Step

**Incorrect code:**
```python
count = 1

while count <= 3:
    print("Hello")
    # count is never updated — infinite loop!
```

**Correct code:**
```python
count = 1

while count <= 3:
    print("Hello")
    count = count + 1
```

**Explanation:** Without `count = count + 1`, the variable `count` stays at `1` forever. The condition `count <= 3` is always `True`, so the loop never ends.

---

### Mistake 2: Wrong Initial Value Causes the Loop to Never Run

**Incorrect code:**
```python
count = 10

while count <= 5:
    print(count)
    count = count + 1
```

**Output:**
```
(nothing is printed)
```

**Explanation:** The condition `count <= 5` is already `False` when `count` starts at `10`. The loop body never executes. Check that your starting value makes the condition `True` at the beginning.

---

### Mistake 3: Off-by-One Error

**Incorrect code — intending to print 1 through 5:**
```python
count = 1

while count < 5:
    print(count)
    count = count + 1
```

**Output:**
```
1
2
3
4
```

**Correct code:**
```python
count = 1

while count <= 5:
    print(count)
    count = count + 1
```

**Output:**
```
1
2
3
4
5
```

**Explanation:** Using `<` instead of `<=` stops the loop one iteration too early. This is called an **off-by-one error**. Always check whether your condition should use `<` or `<=`.

---

### Mistake 4: Incorrect Indentation in the Loop Body

**Incorrect code:**
```python
count = 1

while count <= 3:
    print(count)
count = count + 1   # This line is outside the loop!
```

**What happens:** The update step runs only once, after the loop ends — but by then, the loop has already run infinitely. All lines inside the loop body must be indented by the same amount.

**Correct code:**
```python
count = 1

while count <= 3:
    print(count)
    count = count + 1   # This line is inside the loop.
```

---

### Mistake 5: Using `=` Instead of `==` in the Condition

**Incorrect code:**
```python
answer = ""

while answer = "yes":   # SyntaxError!
    print("You said yes.")
    answer = input("Again? ")
```

**Correct code:**
```python
answer = ""

while answer != "yes":
    answer = input("Type 'yes' to continue: ")

print("You said yes.")
```

**Explanation:** A single `=` is the **assignment operator** (it stores a value). The **comparison operator** is `==` (it checks if two values are equal). Using `=` inside a condition causes a `SyntaxError`. Python will not allow this.

---

## Summary

- A **`while` loop** repeats a block of code as long as a condition is `True`.
- Every `while` loop has three parts:
  - **Condition** — checked before each iteration.
  - **Body** — the indented block that runs each iteration.
  - **Update step** — changes the variable so the condition eventually becomes `False`.
- The loop stops when the condition becomes `False`.
- If the condition is `False` from the start, the loop body never runs.
- An **infinite loop** occurs when the condition never becomes `False`. Always include an update step that moves toward ending the loop.
- `while` loops are useful for counting, repeating tasks a set number of times, and validating user input.
- **Tracing** a loop step by step — recording variable values at each iteration — is a reliable method for understanding what a loop does.

---

## Exercises

### Part A: Understanding Questions

1. What are the three parts of a `while` loop? Describe the role of each part in your own words.

2. What happens if the condition of a `while` loop is `False` before the loop begins? Does the loop body run at all? Explain.

3. What is an infinite loop? Describe two different ways an infinite loop can occur.

4. What is the difference between the `=` operator and the `==` operator? Why does using `=` in a loop condition cause an error?

5. What does it mean to *trace* a loop? Why is tracing a useful skill?

---

### Part B: Code Tracing

6. Trace the following loop. Write down the value of `x` at the start of each iteration and the output of the program.

```python
x = 10

while x > 4:
    print(x)
    x = x - 3
```

7. Trace the following loop. What does it print?

```python
total = 0
n = 1

while n <= 4:
    total = total + n
    n = n + 1

print(total)
```

8. Look at the following loop. Without running it, explain what will happen and why.

```python
value = 5

while value > 0:
    print(value)
    value = value + 1
```

---

### Part C: Code Writing

9. Write a program that uses a `while` loop to print all even numbers from `2` to `20`, one number per line.

10. Write a program that asks the user to enter a number. The program should keep asking until the user enters a number that is greater than `100`. When the user finally enters a valid number, print: `"Great! You entered a number greater than 100."`

11. Write a program that uses a `while` loop to calculate and print the product (multiplication) of all integers from `1` to `5`. The result should be `120`.

12. Write a program that keeps asking the user to enter a word. The program should stop and print `"Goodbye!"` only when the user types `"quit"`.

---

### Part D: Code Modification

13. The following program is supposed to print the numbers from `1` to `6`, but it contains an error. Find the error, explain it, and write the corrected version.

```python
count = 1

while count < 6:
    print(count)
    count = count + 1
```

14. The following program is supposed to count down from `5` to `1` and then print `"Done!"`, but it runs forever. Identify the problem and fix it.

```python
n = 5

while n >= 1:
    print(n)

print("Done!")
```

15. Modify the following program so that, in addition to printing each number, it also prints whether the number is odd or even. Use an `if` statement inside the loop body.

```python
number = 1

while number <= 8:
    print(number)
    number = number + 1
```

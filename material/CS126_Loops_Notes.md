# CS126 – Introduction to Python

## Loops: The for Loop

**Instructor:** Dr. Fawaz Alazemi

---

## Learning Objectives

After studying these notes, you should be able to:

1. Explain what a loop is and why programs need loops.
2. Write a `for` loop with the correct syntax, colon, and indentation.
3. Loop over the items of a list and the characters of a string.
4. Use the three forms of `range()` to repeat code and to count with numbers.
5. Use `range(len(...))` when you need index positions, and explain when this is better than a simple loop.
6. Combine a `for` loop with `if` statements to add up values, count items, find the largest or smallest value, and build new lists and strings.
7. Read a loop and trace it step by step with a trace table.
8. Recognize and fix the most common `for` loop mistakes.

---

## 1. Introduction

### 1.1 The problem: repeating work

Programs often need to do the same thing many times. For example:

- Print the grade of every student in a class.
- Add up the prices of all items in a shopping basket.
- Count how many days in July were hotter than 48 °C in Kuwait.
- Check every character of a password.

You already know how to store many values in one **list**, and how to access one value with an **index** such as `grades[0]`. But look at what happens if we want to print every grade:

```python
grades = [85, 92, 78, 95]
print(grades[0])
print(grades[1])
print(grades[2])
print(grades[3])
```

```text
85
92
78
95
```

This works, but it has three serious problems:

1. **It does not scale.** A class of 200 students needs 200 `print` lines.
2. **It breaks easily.** If one student is added to the list, the program does not print the new grade. If a student is removed, `grades[3]` causes an `IndexError`.
3. **It repeats itself.** The four lines are almost the same. Repeated code is harder to read and harder to fix.

### 1.2 The solution: a loop

A **loop** is a part of a program that **repeats** a block of code. Python has two kinds of loops. In this lecture we study the **`for` loop**, which repeats a block of code **once for each item in a sequence**.

```python
grades = [85, 92, 78, 95]
for grade in grades:
    print(grade)
```

```text
85
92
78
95
```

These three lines work for a list of 4 grades, 400 grades, or even 0 grades. If the list changes, the loop automatically adapts.

### 1.3 A real-life picture

Think of a cashier at a supermarket. You put your items on the counter. The cashier does the same action for **each item**: pick it up, scan it, put it in a bag. When there are no items left, the cashier stops and tells you the total.

A `for` loop works the same way:

| Supermarket | Python `for` loop |
|---|---|
| The basket of items | The sequence (list, string, or range) |
| The item in the cashier's hand | The loop variable |
| Pick up, scan, bag | The loop body |
| Scanning one item | One iteration |
| No items left → stop | The loop ends |

---

## 2. Main Concepts and Vocabulary

Before we write loops, we need a few new words.

| Term | Meaning | Example |
|---|---|---|
| **Loop** | Code that repeats a block of statements | the whole `for` statement |
| **Sequence** | A group of values stored in order | `[85, 92, 78]`, `"Kuwait"`, `range(5)` |
| **Loop variable** | A variable that holds the *current* item | `grade` in `for grade in grades:` |
| **Loop body** | The indented lines that repeat | `print(grade)` |
| **Iteration** | One run of the loop body | printing one grade |
| **Trace table** | A table that shows the variables in every iteration | see Section 4 |

In this lecture, we loop over three kinds of sequences:

- **Lists** — the loop variable takes each **item** of the list.
- **Strings** — the loop variable takes each **character** of the string.
- **Ranges** — the loop variable takes each **whole number** produced by `range()`.

---

## 3. Syntax of the for Loop

### 3.1 General form

```text
for loop_variable in sequence:
    statement 1
    statement 2
    ...
statement after the loop
```

### 3.2 Each part explained

| Part | What it is | Rules |
|---|---|---|
| `for` | A Python keyword that starts the loop | Always lowercase |
| `loop_variable` | A new variable name that you choose | Follows normal variable naming rules |
| `in` | A Python keyword that connects the variable and the sequence | Always lowercase |
| `sequence` | A list, a string, or a `range(...)` | Can be a variable or written directly |
| `:` | Colon at the end of the header line | Required — forgetting it is a `SyntaxError` |
| Indented body | The statements that repeat | Use 4 spaces; every body line has the same indentation |

The first line (`for ... :`) is called the **loop header**.

### 3.3 Indentation decides what repeats

You saw indentation with `if` statements. Loops use exactly the same rule: **the indented lines belong to the loop; the first line that is not indented is after the loop.**

```python
for n in [1, 2, 3]:
    print("Inside")
print("Outside")
```

```text
Inside
Inside
Inside
Outside
```

`print("Inside")` is indented, so it runs once for each of the 3 items. `print("Outside")` is not indented, so it runs **once**, after the loop has finished.

Now indent both lines:

```python
for n in [1, 2, 3]:
    print("Inside")
    print("Also inside")
```

```text
Inside
Also inside
Inside
Also inside
Inside
Also inside
```

Both lines are in the body, so the **pair** of lines repeats 3 times.

### 3.4 Choosing the loop variable name

You can choose any valid variable name. Good names make code easier to read:

- Use a **singular** name for one item from a **plural** list: `for grade in grades:`, `for city in cities:`, `for price in prices:`.
- Use `ch` or `letter` for characters of a string: `for ch in word:`.
- Use `i` (short for *index*) when looping over numbers from `range()`: `for i in range(5):`.

Python does not understand English. The name `grade` does not "know" that it holds a grade. The following loop works exactly the same, but it is harder to read:

```python
grades = [85, 92]
for x in grades:
    print(x)
```

```text
85
92
```

---

## 4. How a for Loop Runs, Step by Step

### 4.1 The steps

When Python reaches a `for` loop, it does the following:

1. Look at the sequence. Are there any items left?
2. If **yes**: store the next item in the loop variable, then run the whole body.
3. Go back to step 1.
4. If **no** items are left: the loop ends. Python continues with the first line after the loop.

### 4.2 A complete example with a trace table

```python
countries = ["Kuwait", "Qatar", "Oman"]
for country in countries:
    print("Hello from", country)
print("Done!")
```

```text
Hello from Kuwait
Hello from Qatar
Hello from Oman
Done!
```

Step-by-step walkthrough:

1. `countries` stores a list with 3 strings.
2. The loop starts. The first item is `"Kuwait"`, so `country` becomes `"Kuwait"`.
3. The body runs: `Hello from Kuwait` is printed.
4. There are items left. `country` becomes `"Qatar"`. The body prints `Hello from Qatar`.
5. `country` becomes `"Oman"`. The body prints `Hello from Oman`.
6. There are no items left. The loop ends.
7. `print("Done!")` runs once.

| Iteration | `country` | Printed |
|---|---|---|
| 1 | `"Kuwait"` | `Hello from Kuwait` |
| 2 | `"Qatar"` | `Hello from Qatar` |
| 3 | `"Oman"` | `Hello from Oman` |
| — | (no items left) | loop ends |

The number of iterations is equal to the number of items in the sequence. This list has 3 items, so the body runs 3 times.

### 4.3 The loop variable after the loop

After the loop ends, the loop variable still exists. It keeps the **last** value it was given:

```python
countries = ["Kuwait", "Qatar", "Oman"]
for country in countries:
    print("Visiting", country)
print("Last value:", country)
```

```text
Visiting Kuwait
Visiting Qatar
Visiting Oman
Last value: Oman
```

This is useful to know when you read other people's code, but you should not depend on it. If the list were empty, the loop would never run and `country` would not exist.

### 4.4 A loop can run zero times

If the sequence is empty, there is nothing to visit, so the body never runs:

```python
names = []
for name in names:
    print("Hello", name)
print("Finished")
```

```text
Finished
```

This is not an error. It is correct behavior: zero items means zero iterations.

---

## 5. Looping Over a List

When you loop over a list, the loop variable takes each **item**, from index 0 to the last index, in order.

```python
temps = [46, 48, 44]
for t in temps:
    print("Temperature:", t, "C")
```

```text
Temperature: 46 C
Temperature: 48 C
Temperature: 44 C
```

The body can do calculations with each item. For example, converting prices from Kuwaiti Dinar to fils (1 KD = 1000 fils):

```python
prices_kd = [2, 5, 1]
for price in prices_kd:
    fils = price * 1000
    print(price, "KD =", fils, "fils")
```

```text
2 KD = 2000 fils
5 KD = 5000 fils
1 KD = 1000 fils
```

The list can also be written directly in the loop header:

```python
for team in ["Qadsia", "Kuwait SC", "Arabi"]:
    print("Team:", team)
```

```text
Team: Qadsia
Team: Kuwait SC
Team: Arabi
```

---

## 6. Looping Over a String

A string is a sequence of **characters**. When you loop over a string, the loop variable takes one character at a time, from left to right.

```python
word = "Kuwait"
for letter in word:
    print(letter)
```

```text
K
u
w
a
i
t
```

### Important notes about strings

- **Every character counts**, including spaces, digits, and punctuation. The string `"Hi 5!"` has 5 characters, so the loop below runs 5 times.

```python
for ch in "Hi 5!":
    print("[" + ch + "]")
```

```text
[H]
[i]
[ ]
[5]
[!]
```

- Each character is itself a **string** of length 1. You can join it with other strings using `+`, compare it with `==`, or test it with `in`.

```python
for ch in "GCC":
    print(ch + "!")
```

```text
G!
C!
C!
```

### The two meanings of `in`

You have already seen `in` as a **membership test** that gives `True` or `False`:

```python
print("a" in "Kuwait")
print("z" in "Kuwait")
```

```text
True
False
```

In a `for` loop header, `in` has a different job: it means "take each item from". Both can appear in the same program:

```python
for ch in "Doha":          # "take each character from"
    if ch in "aeiou":      # "is ch one of these?"
        print(ch, "is a vowel")
```

```text
o is a vowel
a is a vowel
```

---

## 7. The range() Function

### 7.1 Why we need range()

Sometimes you do not have a list. You just want to:

- Repeat something a fixed number of times, or
- Count through numbers, like 1 to 10, or 10 down to 1.

`range()` creates a sequence of **whole numbers** (integers) for a loop to visit.

### 7.2 Form 1: `range(stop)`

`range(stop)` produces the numbers from **0** up to **stop − 1**.

```python
for i in range(5):
    print(i)
```

```text
0
1
2
3
4
```

Notice:

- It **starts at 0**.
- It **stops before** 5. The number 5 is **not included**.
- It produces exactly **5 numbers**. In general, `range(n)` gives `n` numbers.

The last point makes `range(n)` perfect for repeating something `n` times:

```python
for i in range(3):
    print("Welcome to CS126")
```

```text
Welcome to CS126
Welcome to CS126
Welcome to CS126
```

Here we never use `i` in the body. We only need the loop to run 3 times.

### 7.3 Form 2: `range(start, stop)`

`range(start, stop)` produces numbers from **start** up to **stop − 1**.

```python
for i in range(2, 6):
    print(i)
```

```text
2
3
4
5
```

To count from 1 to 10, the stop value must be 11. You can check this with `list()`:

```python
print(list(range(1, 11)))
```

```text
[1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
```

> **Tip:** `list(range(...))` turns a range into a list, so you can print it and see all its numbers at once. This is a good way to check a range before you use it in a loop.

### 7.4 Form 3: `range(start, stop, step)`

The third value, **step**, is how much to add each time. The default step is 1.

```python
for i in range(1, 10, 2):
    print(i)
```

```text
1
3
5
7
9
```

The sequence starts at 1 and adds 2 each time: 1, 3, 5, 7, 9. The next number would be 11, which is not less than 10, so it stops.

### 7.5 Counting down with a negative step

A **negative** step makes `range()` count **down**. Then start must be **larger** than stop.

```python
for i in range(5, 0, -1):
    print(i)
print("Take off!")
```

```text
5
4
3
2
1
Take off!
```

Again, the stop value (0) is **not included**.

### 7.6 Empty ranges

If the numbers cannot move from start toward stop, the range is empty and the loop runs **zero times**:

```python
print(list(range(3, 3)))
print(list(range(5, 2)))
print(list(range(1, 5, -1)))
```

```text
[]
[]
[]
```

- `range(3, 3)`: start equals stop.
- `range(5, 2)`: counting up from 5 can never reach 2.
- `range(1, 5, -1)`: counting down from 1 can never reach 5.

### 7.7 range() works only with integers

All values given to `range()` must be whole numbers. `range(2.5)` causes a `TypeError`.

### 7.8 Quick reference

| Goal | Code | Numbers |
|---|---|---|
| 0 to 4 | `range(5)` | 0 1 2 3 4 |
| 1 to 5 | `range(1, 6)` | 1 2 3 4 5 |
| Even numbers 2 to 10 | `range(2, 11, 2)` | 2 4 6 8 10 |
| Multiples of 5 below 20 | `range(0, 20, 5)` | 0 5 10 15 |
| 10 down to 1 | `range(10, 0, -1)` | 10 9 8 … 1 |
| Repeat 7 times | `range(7)` | 7 numbers |

**Rule to remember:** the stop value is **never** included. Choose stop to be "one step past" the last number you want.

---

## 8. Looping with Index Positions: range(len(...))

### 8.1 The idea

`len(lst)` gives the number of items in a list. The indexes of the list are `0, 1, …, len(lst) − 1`. That is exactly what `range(len(lst))` produces!

```python
courses = ["CS126", "MATH101", "ENG110"]
print(len(courses))
print(list(range(len(courses))))
```

```text
3
[0, 1, 2]
```

So this loop visits every **index** of the list:

```python
courses = ["CS126", "MATH101", "ENG110"]
for i in range(len(courses)):
    print(i, courses[i])
```

```text
0 CS126
1 MATH101
2 ENG110
```

Walkthrough:

1. `len(courses)` is 3, so `range(3)` gives 0, 1, 2.
2. When `i` is 0, `courses[0]` is `"CS126"`.
3. When `i` is 1, `courses[1]` is `"MATH101"`.
4. When `i` is 2, `courses[2]` is `"ENG110"`.

### 8.2 Simple loop or index loop?

| Style | Loop variable holds | Use it when |
|---|---|---|
| `for c in courses:` | the **value** | you only need each value (most common) |
| `for i in range(len(courses)):` | the **index** | you need the position, you want to **change** list items, or you need to read **two lists** at the same position |

Prefer the simple style when it is enough. It is shorter and easier to read.

### 8.3 Example: showing a position number

People count from 1, but indexes start at 0. Add 1 when you display a position:

```python
queue = ["Ahmad", "Sara", "Fahad"]
for i in range(len(queue)):
    print("Position", i + 1, ":", queue[i])
```

```text
Position 1 : Ahmad
Position 2 : Sara
Position 3 : Fahad
```

### 8.4 Example: reading two lists together

If two lists are related by position, one index can read both:

```python
students = ["Noor", "Ali", "Mona"]
marks = [88, 59, 74]
for i in range(len(students)):
    print(students[i], "scored", marks[i])
```

```text
Noor scored 88
Ali scored 59
Mona scored 74
```

The two lists must have the **same length**; otherwise you may get an `IndexError`.

### 8.5 Example: changing items in a list

To change the items stored in a list, you must assign to `lst[i]`:

```python
prices = [1, 2, 3]
for i in range(len(prices)):
    prices[i] = prices[i] * 2
print(prices)
```

```text
[2, 4, 6]
```

See Common Mistake 6 for why `for p in prices: p = p * 2` does **not** work.

---

## 9. Common Loop Patterns

Most loops you will write follow a few standard **patterns**. Learn these patterns and you can solve many problems by combining them.

### 9.1 Pattern 1: The accumulator (adding up)

An **accumulator** is a variable that **collects** a result while the loop runs. The recipe is:

1. **Before** the loop: create the accumulator with a starting value (usually `0`).
2. **Inside** the loop: update it with each item.
3. **After** the loop: use the final result.

```python
prices = [1.25, 0.75, 2.5, 0.5]   # shopping prices in KD
total = 0
for price in prices:
    total = total + price
print("Total:", total, "KD")
```

```text
Total: 5.0 KD
```

| Step | `price` | `total` after this step |
|---|---|---|
| before loop | — | 0 |
| iteration 1 | 1.25 | 1.25 |
| iteration 2 | 0.75 | 2.0 |
| iteration 3 | 2.5 | 4.5 |
| iteration 4 | 0.5 | 5.0 |

The line `total = total + price` means "take the old total, add the price, and store the new value back in `total`". Python also allows the short form `total += price`, which does exactly the same thing.

#### Calculating an average

An average needs the total **and** the count. The total comes from the loop; the count comes from `len()`. The division happens **after** the loop:

```python
grades = [85, 92, 78, 95, 70]
total = 0
for g in grades:
    total = total + g
average = total / len(grades)
print("Total:", total)
print("Average:", average)
```

```text
Total: 420
Average: 84.0
```

Running total: 85 → 177 → 255 → 350 → 420. Then `420 / 5` is `84.0`. Remember that `/` always gives a float, even when the division is exact.

#### Multiplying instead of adding

An accumulator does not always add. To multiply values, start at `1`, not `0` (starting at 0 would make the answer always 0):

```python
numbers = [2, 3, 4]
product = 1
for n in numbers:
    product = product * n
print(product)
```

```text
24
```

### 9.2 Pattern 2: The counter (counting with if)

A **counter** counts how many items pass a test. It is a special accumulator that adds **1**, not the value.

```python
temps = [46, 48, 44, 50, 47, 43, 49]   # Kuwait, one week in July
hot_days = 0
for t in temps:
    if t >= 48:
        hot_days = hot_days + 1
print("Very hot days:", hot_days)
```

```text
Very hot days: 3
```

| `t` | `t >= 48`? | `hot_days` |
|---|---|---|
| 46 | False | 0 |
| 48 | True | 1 |
| 44 | False | 1 |
| 50 | True | 2 |
| 47 | False | 2 |
| 43 | False | 2 |
| 49 | True | 3 |

Notice the three levels of indentation:

- `for` is at the left edge.
- `if` is indented once — it is **inside the loop**, so it runs for every temperature.
- `hot_days = hot_days + 1` is indented twice — it is **inside the if**, so it runs only when the test is `True`.

You can use any logical expression as the test, including `and`, `or`, and `not`:

```python
temps = [46, 48, 44, 50, 47, 43, 49]
count = 0
for t in temps:
    if t >= 45 and t <= 48:
        count = count + 1
print("Days from 45 to 48:", count)
```

```text
Days from 45 to 48: 3
```

(46, 48, and 47.)

#### Counting characters in a string

```python
city = "Kuwait City"
vowels = "aeiouAEIOU"
count = 0
for ch in city:
    if ch in vowels:
        count = count + 1
print("Vowels:", count)
```

```text
Vowels: 4
```

The loop visits all 11 characters (including the space). Only `u`, `a`, `i`, and `i` are vowels. The letter `y` is not in the `vowels` string, so it is not counted.

### 9.3 Pattern 3: Finding the largest or smallest value

To find the largest value, keep the "best so far" in a variable and replace it whenever you find something bigger.

```python
temps = [46, 48, 44, 50, 47, 43, 49]
highest = temps[0]
for t in temps:
    if t > highest:
        highest = t
print("Highest:", highest)
```

```text
Highest: 50
```

**Why start with `temps[0]` and not `0`?** Imagine the list of winter temperatures in a cold country: `[-5, -12, -3]`. If `highest` started at 0, no value would be bigger than 0, and the program would wrongly report 0. Starting with the first item of the list is always safe.

To find the **smallest** value, change only the comparison from `>` to `<`.

Python has built-in functions `max()` and `min()` that do this for you. We learn the loop version because the same idea works for problems that `max()` cannot solve directly — for example, finding *which* student has the highest mark.

```python
students = ["Noor", "Ali", "Mona"]
marks = [88, 59, 94]
best = 0
for i in range(len(marks)):
    if marks[i] > marks[best]:
        best = i
print("Top student:", students[best])
```

```text
Top student: Mona
```

Here `best` stores the **index** of the best mark so far, starting with index 0.

### 9.4 Pattern 4: Building a new list (filtering)

Start with an **empty list** before the loop and use `.append()` to add items that pass a test:

```python
grades = [85, 92, 58, 74, 49]
passed = []
for g in grades:
    if g >= 60:
        passed.append(g)
print(passed)
```

```text
[85, 92, 74]
```

The original list `grades` is not changed. We built a **new** list.

You can also append a **changed** version of each item:

```python
celsius = [20, 30, 45]
fahrenheit = []
for c in celsius:
    fahrenheit.append(c * 9 / 5 + 32)
print(fahrenheit)
```

```text
[68.0, 86.0, 113.0]
```

### 9.5 Pattern 5: Building a new string

Start with an **empty string** `""` and join characters with `+`:

```python
word = "CS126"
result = ""
for ch in word:
    result = ch + result
print(result)
```

```text
621SC
```

Because each new character goes to the **front** (`ch + result`), the string is reversed:

| `ch` | `result` after |
|---|---|
| `"C"` | `"C"` |
| `"S"` | `"SC"` |
| `"1"` | `"1SC"` |
| `"2"` | `"21SC"` |
| `"6"` | `"621SC"` |

If you write `result = result + ch` instead, you get a copy of the original string in the same order.

Another example: remove all spaces from a phone number.

```python
phone = "965 2222 3333"
digits = ""
for ch in phone:
    if ch != " ":
        digits = digits + ch
print(digits)
```

```text
96522223333
```

### 9.6 Combining patterns: a mobile data package

Real programs often combine several patterns. Here a student has a 10 GB mobile package and records the data used each day.

```python
usage = [1.5, 2, 0.5, 3, 1, 2.5, 1]
limit = 10
total = 0
for i in range(len(usage)):
    total = total + usage[i]
    if total > limit:
        print("Day", i + 1, "total", total, "- over!")
    else:
        print("Day", i + 1, "total", total)
```

```text
Day 1 total 1.5
Day 2 total 3.5
Day 3 total 4.0
Day 4 total 7.0
Day 5 total 8.0
Day 6 total 10.5 - over!
Day 7 total 11.5 - over!
```

Ideas used:

- `range(len(usage))` gives indexes 0 to 6; `i + 1` turns them into day numbers 1 to 7.
- `total` is an accumulator. Because one value (1.5) is a float, `total` becomes a float, which is why we see `4.0` and `7.0`.
- The `if / else` is inside the loop, so the total is checked **every day**.
- The `print` is also inside the loop on purpose, because we want one line per day.

---

## 10. Nested Loops (A Loop Inside a Loop)

The body of a loop can contain **another loop**. This is called a **nested loop**.

```python
sizes = ["Small", "Large"]
drinks = ["Tea", "Coffee", "Karak"]
for size in sizes:
    for drink in drinks:
        print(size, drink)
```

```text
Small Tea
Small Coffee
Small Karak
Large Tea
Large Coffee
Large Karak
```

**Rule:** for **each** item of the outer loop, the inner loop runs **completely** from start to end.

1. `size` becomes `"Small"`. The inner loop runs 3 times: Tea, Coffee, Karak.
2. `size` becomes `"Large"`. The inner loop runs 3 times again: Tea, Coffee, Karak.
3. The outer loop has no items left. Everything ends.

The inner body runs 2 × 3 = **6** times in total.

A classic example is a small multiplication table:

```python
for row in range(1, 4):
    for col in range(1, 4):
        print(row, "x", col, "=", row * col)
```

```text
1 x 1 = 1
1 x 2 = 2
1 x 3 = 3
2 x 1 = 2
2 x 2 = 4
2 x 3 = 6
3 x 1 = 3
3 x 2 = 6
3 x 3 = 9
```

Use different names for the two loop variables (`row` and `col`), so the inner loop does not overwrite the outer loop's variable.

---

## 11. Important Notes

- The number of iterations equals the number of items in the sequence. A list of 7 items gives 7 iterations; `range(4)` gives 4 iterations.
- The loop visits items **in order**: lists from index 0 to the end, strings from left to right, ranges from start toward stop.
- Accumulators and counters are created **before** the loop. Results are usually printed **after** the loop.
- A `print` **inside** the loop prints once per item; a `print` **after** the loop prints once.
- The loop variable holds a **copy** of the current value. Assigning a new value to it does not change the list.
- `range()` never includes its stop value and accepts only integers.
- Use the simple style `for item in lst:` unless you really need indexes.
- Use the same indentation (4 spaces) everywhere. Do not mix tabs and spaces.

---

## 12. Common Mistakes

### Mistake 1: Forgetting the colon

**Incorrect**

```python
# Incorrect
for g in grades
    print(g)
```

**Why?** Every loop header must end with `:`. Python stops with `SyntaxError: expected ':'`.

**Correct**

```python
grades = [85, 92]
for g in grades:
    print(g)
```

### Mistake 2: Forgetting to indent the body

**Incorrect**

```python
# Incorrect
for g in grades:
print(g)
```

**Why?** A loop must have at least one indented line. Python stops with `IndentationError: expected an indented block`.

**Correct**

```python
grades = [85, 92]
for g in grades:
    print(g)
```

### Mistake 3: Resetting the accumulator inside the loop

**Incorrect**

```python
prices = [3, 5, 2]
for p in prices:
    total = 0
    total = total + p
print(total)
```

```text
2
```

**Why?** `total = 0` runs in **every** iteration, so the earlier prices are thrown away. Only the last price (2) remains.

**Correct**

```python
prices = [3, 5, 2]
total = 0
for p in prices:
    total = total + p
print(total)
```

```text
10
```

### Mistake 4: Off-by-one error with range()

**Incorrect**

```python
# goal: print 1 to 5
for i in range(1, 5):
    print(i)
```

```text
1
2
3
4
```

**Why?** The stop value is not included, so 5 is missing. This kind of mistake, where you are wrong by exactly one, is called an **off-by-one error**.

**Correct**

```python
for i in range(1, 6):
    print(i)
```

```text
1
2
3
4
5
```

### Mistake 5: Printing inside the loop instead of after it

**Incorrect**

```python
nums = [4, 8, 6]
total = 0
for n in nums:
    total = total + n
    print("Total:", total)
```

```text
Total: 4
Total: 12
Total: 18
```

**Why?** The `print` is indented, so it is part of the body and runs every time. We wanted only the final total.

**Correct**

```python
nums = [4, 8, 6]
total = 0
for n in nums:
    total = total + n
print("Total:", total)
```

```text
Total: 18
```

### Mistake 6: Changing the loop variable to change the list

**Incorrect**

```python
prices = [1, 2, 3]
for p in prices:
    p = p * 2
print(prices)
```

```text
[1, 2, 3]
```

**Why?** In each iteration, `p` receives a copy of the current value. `p = p * 2` changes only `p`, not the item stored in the list.

**Correct**

```python
prices = [1, 2, 3]
for i in range(len(prices)):
    prices[i] = prices[i] * 2
print(prices)
```

```text
[2, 4, 6]
```

### Mistake 7: Using an index as if it were a value

**Incorrect**

```python
marks = [70, 80, 90]
total = 0
for i in range(len(marks)):
    total = total + i
print(total)
```

```text
3
```

**Why?** `i` is the index (0, 1, 2), not the mark. The program adds 0 + 1 + 2 = 3.

**Correct**

```python
marks = [70, 80, 90]
total = 0
for i in range(len(marks)):
    total = total + marks[i]
print(total)
```

```text
240
```

(Or, more simply, `for m in marks: total = total + m`.)

### Mistake 8: Starting the maximum at 0

**Incorrect**

```python
temps = [-5, -12, -3]
highest = 0
for t in temps:
    if t > highest:
        highest = t
print(highest)
```

```text
0
```

**Why?** No temperature is bigger than 0, so `highest` never changes, and 0 is not even in the list.

**Correct**

```python
temps = [-5, -12, -3]
highest = temps[0]
for t in temps:
    if t > highest:
        highest = t
print(highest)
```

```text
-3
```

---

## 13. Mini Practice Questions

Try these quickly before looking at the answers at the end of this section.

**Q1.** How many times does the body run?

```python
for i in range(2, 8, 2):
    print(i)
```

**Q2.** What does this print?

```python
n = 0
for ch in "Doha":
    n = n + 1
print(n)
```

**Q3.** Write the `range()` call that produces `3, 6, 9, 12`.

**Q4.** What does this print?

```python
for x in [10, 20]:
    print(x)
print(x + 1)
```

**Q5.** True or false: `for i in range(5, 1):` causes an error.

**Q6.** What does this print?

```python
word = "abc"
result = ""
for ch in word:
    result = result + ch + ch
print(result)
```

### Answers to Mini Practice

1. **3 times** — `i` is 2, 4, 6. Eight is the stop value and is not included.
2. **`4`** — the loop counts the characters of `"Doha"`, the same as `len("Doha")`.
3. **`range(3, 13, 3)`** — any stop from 13 to 15 also works.
4. **`10`, `20`, then `21`** — after the loop, `x` keeps its last value, 20.
5. **False** — it is an empty range, so the loop simply runs zero times.
6. **`aabbcc`** — each character is added twice.

---

## 14. Ask AI to Help You Understand

You can use an AI assistant as a private tutor. Ask it to **explain** and to **give hints**, not just to give answers. Here are some useful prompts:

```text
Explain how a Python for loop works using a list of 4 prices in Kuwaiti Dinar.
Show me a trace table for each iteration. Do not give me exercises yet.
```

```text
I am confused about why range(1, 5) does not include 5.
Explain it with 3 different small examples and a number line.
```

```text
Explain the difference between "for x in my_list" and
"for i in range(len(my_list))". When should a beginner use each one?
```

```text
Here is my Python code and the output I expected. Do not fix it for me.
Give me one hint at a time to help me find the mistake myself.
[paste your code here]
```

```text
Give me three simple exercises about Python for loops with lists and strings.
Give me hints first and do not show the solutions unless I ask.
```

> **Remember:** Always run the code yourself. AI can make mistakes, and running code is the only way to be sure.

---

## 15. Summary

- A **loop** repeats a block of code. A **`for` loop** runs its body **once for each item** in a sequence.
- Syntax: `for variable in sequence:` followed by an **indented** body. The colon and the indentation are required.
- Looping over a **list** gives each item; looping over a **string** gives each character; looping over a **range** gives each number.
- `range(stop)`, `range(start, stop)`, and `range(start, stop, step)` create whole numbers. The **stop value is never included**. A negative step counts down.
- `range(len(lst))` gives the **indexes** of a list. Use it when you need positions, need to read two lists together, or need to change list items.
- Common patterns:
  - **Accumulator:** start before the loop, add each value inside the loop, use the result after.
  - **Counter:** add 1 when an `if` test is true.
  - **Maximum / minimum:** start with the first item; replace it when you find something better.
  - **Building:** start with `[]` or `""`; add to it inside the loop.
- In a **nested loop**, the inner loop runs completely for each item of the outer loop.
- Use a **trace table** to understand any loop.

---

## Basic Exercises

> Exercises 1–12 are the same as in the slides. Exercises 13–16 are extra practice.

**Exercise 1.** Predict the output.

```python
for x in [3, 6, 9]:
    print(x * 2)
```

**Exercise 2.** Predict the output.

```python
for i in range(1, 10, 3):
    print(i)
```

**Exercise 3.** Find and fix the **two** errors.

```python
cities = ["Kuwait", "Doha", "Muscat"]
for city in cities
print(city)
```

**Exercise 4.** Complete the code so it prints `10`, `15`, `20`, `25`, one number per line.

```python
for n in range(___, ___, ___):
    print(n)
```

**Exercise 13.** Predict the output. (Hint: `"*" * 3` is `"***"`.)

```python
for i in range(4):
    print("*" * (i + 1))
```

## Practice Exercises

**Exercise 5.** Write a program that prints the total of these restaurant prices (KD):

```python
prices = [3, 5, 2, 10]
```

**Exercise 6.** Write a program that counts how many students passed (a mark of 60 or more):

```python
marks = [55, 72, 90, 48, 60, 81]
```

**Exercise 7.** Modify this code so it prints only the countries whose names have **more than 5 characters**.

```python
gcc = ["Kuwait", "Saudi Arabia", "UAE",
       "Qatar", "Bahrain", "Oman"]
for country in gcc:
    print(country)
```

**Exercise 8.** Explain what this code does and give its output.

```python
word = "banana"
count = 0
for ch in word:
    if ch == "a":
        count = count + 1
print(count)
```

**Exercise 14.** Use `range()` with a step to add up all the **even** numbers from 2 to 20 (including 20). Print the result.

## Challenge Exercises

**Exercise 9.** Find the **lowest** winter temperature **without** using `min()`:

```python
temps = [18, 12, 21, 9, 15]
```

**Exercise 10.** Use `range()` to print the 7 times table from 1 to 5:

```text
7 x 1 = 7
7 x 2 = 14
7 x 3 = 21
7 x 4 = 28
7 x 5 = 35
```

**Exercise 11.** These are approximate flight distances from Kuwait (km). Print each city that is **farther than 800 km**, then print how many such cities there are.

```python
cities = ["Riyadh", "Doha", "Manama",
          "Dubai", "Muscat"]
km = [540, 560, 425, 850, 1190]
```

**Exercise 12.** This code should print the total of the list **once**. What does it print now? Fix it.

```python
nums = [4, 8, 6, 2]
for n in nums:
    total = 0
    total = total + n
    print(total)
```

**Exercise 15.** A football team scored these goals in six matches:

```python
goals = [2, 0, 3, 1, 0, 4]
```

Using **one** loop, print the number of matches with **no goals** and the **total** number of goals, like this:

```text
Matches with no goals: 2
Total goals: 10
```

**Exercise 16.** A shop gives a 10% discount. Build a **new list** `sale` that contains each price multiplied by `0.9`, then print it. The original list must not change.

```python
prices = [10, 20, 5]
```

---

# Exercise Solutions

### Solution 1

Each item is multiplied by 2 before printing.

```text
6
12
18
```

### Solution 2

Start at 1, add 3 each time, stop before 10. The next value, 10, is the stop value, so it is not printed.

```text
1
4
7
```

### Solution 3

Error 1: the colon is missing at the end of the `for` line. Error 2: the body is not indented.

```python
cities = ["Kuwait", "Doha", "Muscat"]
for city in cities:
    print(city)
```

```text
Kuwait
Doha
Muscat
```

### Solution 4

Start at 10 and step by 5. The stop value must be larger than 25 but not larger than 30, so that 25 is the last number printed. Any stop from 26 to 30 works.

```python
for n in range(10, 30, 5):
    print(n)
```

```text
10
15
20
25
```

### Solution 5

Accumulator pattern: start at 0 before the loop, add each price, print after the loop.

```python
prices = [3, 5, 2, 10]
total = 0
for p in prices:
    total = total + p
print("Total:", total, "KD")
```

```text
Total: 20 KD
```

### Solution 6

Counter pattern: add 1 only when the mark is 60 or more. The marks 72, 90, 60, and 81 pass.

```python
marks = [55, 72, 90, 48, 60, 81]
passed = 0
for m in marks:
    if m >= 60:
        passed = passed + 1
print("Passed:", passed)
```

```text
Passed: 4
```

### Solution 7

Add an `if` inside the loop that tests the length of each name.

```python
gcc = ["Kuwait", "Saudi Arabia", "UAE",
       "Qatar", "Bahrain", "Oman"]
for country in gcc:
    if len(country) > 5:
        print(country)
```

```text
Kuwait
Saudi Arabia
Bahrain
```

"Kuwait" has exactly 6 characters, so it passes. "Qatar" has exactly 5, so it does not.

### Solution 8

The code counts how many times the letter `"a"` appears in `"banana"`. The loop visits b, a, n, a, n, a; the counter increases for each of the three `a` characters.

```text
3
```

### Solution 9

Start with the first temperature, and replace it whenever a smaller one appears.

```python
temps = [18, 12, 21, 9, 15]
lowest = temps[0]
for t in temps:
    if t < lowest:
        lowest = t
print("Lowest:", lowest)
```

```text
Lowest: 9
```

Trace of `lowest`: 18 → 12 → 12 → 9 → 9.

### Solution 10

`range(1, 6)` gives 1 to 5. Each line prints `7 x i = 7*i`.

```python
for i in range(1, 6):
    print("7 x", i, "=", 7 * i)
```

```text
7 x 1 = 7
7 x 2 = 14
7 x 3 = 21
7 x 4 = 28
7 x 5 = 35
```

### Solution 11

The two lists are related by position, so we loop over indexes and read both lists with the same `i`.

```python
cities = ["Riyadh", "Doha", "Manama",
          "Dubai", "Muscat"]
km = [540, 560, 425, 850, 1190]
count = 0
for i in range(len(cities)):
    if km[i] > 800:
        print(cities[i])
        count = count + 1
print("Count:", count)
```

```text
Dubai
Muscat
Count: 2
```

### Solution 12

Currently, `total` is reset to 0 in every iteration and printed inside the loop, so the program just prints each number:

```text
4
8
6
2
```

Fix: create `total` **before** the loop, and move `print` **after** the loop (remove its indentation).

```python
nums = [4, 8, 6, 2]
total = 0
for n in nums:
    total = total + n
print(total)
```

```text
20
```

### Solution 13

`i` takes 0, 1, 2, 3, so `i + 1` is 1, 2, 3, 4 and the number of stars grows by one each line.

```text
*
**
***
****
```

### Solution 14

`range(2, 21, 2)` gives 2, 4, …, 20. The stop must be 21 (or 22) so that 20 is included.

```python
total = 0
for n in range(2, 21, 2):
    total = total + n
print(total)
```

```text
110
```

### Solution 15

One loop can update a counter and an accumulator at the same time.

```python
goals = [2, 0, 3, 1, 0, 4]
no_goal = 0
total = 0
for g in goals:
    total = total + g
    if g == 0:
        no_goal = no_goal + 1
print("Matches with no goals:", no_goal)
print("Total goals:", total)
```

```text
Matches with no goals: 2
Total goals: 10
```

### Solution 16

Start with an empty list and append each new price. Because we never assign to `prices[i]`, the original list stays the same.

```python
prices = [10, 20, 5]
sale = []
for p in prices:
    sale.append(p * 0.9)
print(sale)
print(prices)
```

```text
[9.0, 18.0, 4.5]
[10, 20, 5]
```

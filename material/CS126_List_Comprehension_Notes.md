# CS126 – Introduction to Python

## List Comprehension

**Instructor:** Dr. Fawaz Alazemi

---

## Learning Objectives

After studying these notes, you should be able to:

1. Explain what a list comprehension is and what problem it solves.
2. Write the basic form `[expression for item in sequence]` and read it aloud in plain English.
3. Convert a `for` loop that uses `append()` into a list comprehension, and convert a comprehension back into a loop.
4. Build lists from other lists, from strings, and from `range()`.
5. **Filter** items with an `if` at the end of a comprehension.
6. Use a **conditional expression** (`A if condition else B`) to **choose** a value for every item.
7. Combine comprehensions with `len()` and `sum()`, and with indexes to work on two lists at once.
8. Decide when a normal loop is clearer than a comprehension.
9. Recognize and fix the most common list comprehension mistakes.

---

## 1. Introduction

### 1.1 A pattern you have already used many times

In the loops lectures, you often built a **new list** from an old one. The steps were always the same:

1. Create an **empty list**.
2. Write a `for` loop over a sequence.
3. Inside the loop, `append()` a value to the new list.

```python
nums = [1, 2, 3, 4]
squares = []
for n in nums:
    squares.append(n * n)
print(squares)
```

```text
[1, 4, 9, 16]
```

This works well. But this pattern is so common that Python gives us a shorter way to write it.

### 1.2 The same program with a list comprehension

```python
nums = [1, 2, 3, 4]
squares = [n * n for n in nums]
print(squares)
```

```text
[1, 4, 9, 16]
```

The three lines that built the list became **one line**. The result is exactly the same.

### 1.3 Why use list comprehensions?

- **Shorter:** one line instead of three or four.
- **Clear purpose:** when a reader sees `[ ... for ... in ... ]`, they know immediately that a new list is being built.
- **Reads like English:** `[n * n for n in nums]` reads as *"n times n, for each n in nums"*.
- **Very common:** you will see list comprehensions in almost every Python program, book, and website, so you need to be able to read them.

### 1.4 Where does the name come from?

The word *comprehension* comes from mathematics, where we describe a set by a rule, for example: *"the set of x², for every x from 1 to 4"*. A list comprehension describes a list by a rule in the same way.

---

## 2. Main Concepts and Vocabulary

| Term | Meaning | In `[n * 2 for n in nums if n > 0]` |
|---|---|---|
| **List comprehension** | An expression in `[ ]` that builds a new list from a sequence | the whole thing |
| **Expression** | The value calculated for each item and put in the new list | `n * 2` |
| **Loop variable** | Holds the current item, exactly like in a `for` loop | `n` |
| **Sequence** | Where the items come from (list, string, range) | `nums` |
| **Condition** (optional) | A test; only items where it is `True` are used | `n > 0` |
| **Filtering** | Keeping only some items | done by `if n > 0` |
| **Conditional expression** | An expression that chooses between two values: `A if condition else B` | (see Section 9) |

---

## 3. The Basic Syntax

### 3.1 General form

```text
new_list = [expression for item in sequence]
```

| Part | Meaning | Rules |
|---|---|---|
| `[` and `]` | Square brackets | They tell Python the result is a **list** |
| `expression` | The value to put in the new list | Usually uses the loop variable |
| `for` | Keyword | Same as in a `for` loop |
| `item` | Loop variable | Any valid variable name |
| `in` | Keyword | Same as in a `for` loop |
| `sequence` | A list, a string, or a `range()` | Anything you can loop over with `for` |

Two important differences from a `for` loop:

- There is **no colon** `:`.
- There is **no indentation**. Everything is on one line (inside the brackets).

### 3.2 Reading a comprehension aloud

Practice reading comprehensions in English. Start from the expression, then say "for each":

| Code | Read it as |
|---|---|
| `[p * 1000 for p in prices]` | "p times 1000, for each p in prices" |
| `[len(c) for c in cities]` | "the length of c, for each c in cities" |
| `[ch for ch in "Oman"]` | "ch, for each character ch in "Oman"" |
| `[i * i for i in range(5)]` | "i squared, for each i from 0 to 4" |

If you can read it aloud, you can understand it.

---

## 4. How Python Runs a List Comprehension

### 4.1 Step by step

Python runs a list comprehension like the loop it replaces:

1. Start with an empty new list.
2. Take the first item from the sequence and store it in the loop variable.
3. Evaluate the expression and add the result to the **end** of the new list.
4. Repeat steps 2–3 for every item.
5. When there are no items left, the finished list is the result.

### 4.2 Example with a trace table

Kuwaiti prices in KD converted to fils (1 KD = 1000 fils):

```python
prices_kd = [2, 5, 1, 3]
prices_fils = [p * 1000 for p in prices_kd]
print(prices_fils)
print(prices_kd)
```

```text
[2000, 5000, 1000, 3000]
[2, 5, 1, 3]
```

| Step | `p` | `p * 1000` | New list so far |
|---|---|---|---|
| 1 | 2 | 2000 | `[2000]` |
| 2 | 5 | 5000 | `[2000, 5000]` |
| 3 | 1 | 1000 | `[2000, 5000, 1000]` |
| 4 | 3 | 3000 | `[2000, 5000, 1000, 3000]` |

Notice two things:

- The new list has the **same number of items** as `prices_kd`, in the **same order**.
- `prices_kd` itself has **not changed**.

---

## 5. Converting Between Loops and Comprehensions

### 5.1 Loop → comprehension

Start from a loop that builds a list:

```python
cities = ["Kuwait", "Doha", "Muscat"]
lengths = []
for c in cities:
    lengths.append(len(c))
print(lengths)
```

```text
[6, 4, 6]
```

Recipe:

1. Write the name of the new list and `= [ ]`.
2. Inside the brackets, write the expression from `append(...)` **first**: `len(c)`.
3. After it, copy the loop header **without the colon**: `for c in cities`.

```python
cities = ["Kuwait", "Doha", "Muscat"]
lengths = [len(c) for c in cities]
print(lengths)
```

```text
[6, 4, 6]
```

This recipe only works when the loop does **one thing**: append one value per item (possibly with an `if`). If the loop does other jobs, such as printing or updating several variables, keep the loop.

### 5.2 Comprehension → loop

Reading a comprehension is easier if you can "unfold" it into a loop in your head:

```python
codes = ["KW", "SA", "QA"]
flags = [c + "-GCC" for c in codes]
print(flags)
```

```text
['KW-GCC', 'SA-GCC', 'QA-GCC']
```

is the same as:

```python
codes = ["KW", "SA", "QA"]
flags = []
for c in codes:
    flags.append(c + "-GCC")
print(flags)
```

```text
['KW-GCC', 'SA-GCC', 'QA-GCC']
```

When you see a comprehension you do not understand, rewrite it as a loop. Then trace the loop.

---

## 6. What Can the Expression Be?

The expression can be **any expression** that gives a value. It is evaluated once for each item.

| Expression type | Example | Result |
|---|---|---|
| Arithmetic | `[n + 1 for n in [5, 6, 7]]` | `[6, 7, 8]` |
| Function call | `[len(c) for c in ["UAE", "Oman"]]` | `[3, 4]` |
| String joining | `["Dr. " + n for n in ["Ali", "Mona"]]` | `['Dr. Ali', 'Dr. Mona']` |
| String repetition | `["*" * n for n in [1, 2, 3]]` | `['*', '**', '***']` |
| Indexing | `[w[0] for w in ["Kuwait", "Qatar"]]` | `['K', 'Q']` |
| Slicing | `[w[:3] for w in ["Kuwait", "Bahrain"]]` | `['Kuw', 'Bah']` |
| Comparison | `[t >= 45 for t in [46, 40]]` | `[True, False]` |
| The item itself | `[x for x in "abc"]` | `['a', 'b', 'c']` |
| A fixed value | `[0 for i in range(4)]` | `[0, 0, 0, 0]` |

Let us check a few of them by running them:

```python
print(["*" * n for n in [1, 2, 3]])
print([w[:3] for w in ["Kuwait", "Bahrain"]])
print([0 for i in range(4)])
```

```text
['*', '**', '***']
['Kuw', 'Bah']
[0, 0, 0, 0]
```

The last example is useful when you need a list of a certain size filled with a starting value, for example a list of 4 scores that all start at 0.

---

## 7. Sources: Lists, Strings, and range()

### 7.1 From a list

You have seen many examples already. The loop variable takes each item of the list.

### 7.2 From a string

The loop variable takes each **character**. The result is always a **list**, not a string.

```python
letters = [ch for ch in "Oman"]
print(letters)
```

```text
['O', 'm', 'a', 'n']
```

```python
doubled = [ch + ch for ch in "GCC"]
print(doubled)
```

```text
['GG', 'CC', 'CC']
```

### 7.3 From range()

You do not need an existing list. `range()` can provide the numbers:

```python
squares = [i * i for i in range(1, 6)]
print(squares)

table7 = [7 * i for i in range(1, 11)]
print(table7)

countdown = [i for i in range(10, 0, -2)]
print(countdown)
```

```text
[1, 4, 9, 16, 25]
[7, 14, 21, 28, 35, 42, 49, 56, 63, 70]
[10, 8, 6, 4, 2]
```

Remember the rules of `range()`: it starts at 0 by default, and the stop value is **never** included.

---

## 8. Filtering with if

### 8.1 Syntax

```text
new_list = [expression for item in sequence if condition]
```

The `if condition` goes at the **end**. For each item:

- If the condition is `True`, the expression is evaluated and added to the new list.
- If the condition is `False`, the item is **skipped**.

### 8.2 Loop version and comprehension version

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

```python
grades = [85, 92, 58, 74, 49]
passed = [g for g in grades if g >= 60]
print(passed)
```

```text
[85, 92, 74]
```

The order of the parts in the comprehension is: **expression → for → if**. In the loop, the order is **for → if → append(expression)**. The expression moves from the end to the front.

| `g` | `g >= 60` | Added? |
|---|---|---|
| 85 | True | yes |
| 92 | True | yes |
| 58 | False | no |
| 74 | True | yes |
| 49 | False | no |

A filtered list can be **shorter** than the original. It can even be **empty**:

```python
grades = [40, 35, 52]
passed = [g for g in grades if g >= 60]
print(passed)
```

```text
[]
```

### 8.3 Any logical expression can be the condition

```python
temps = [46, 48, 44, 50, 47, 43, 49]
print([t for t in temps if t >= 48])
print([t for t in temps if t >= 45 and t <= 47])
print([t for t in temps if t < 44 or t > 49])
print([t for t in temps if not t == 50])
```

```text
[48, 50, 49]
[46, 47]
[50, 43]
[46, 48, 44, 47, 43, 49]
```

Notice that the result keeps the **original order**: 50 comes before 43 because it comes first in `temps`.

With strings, `in` is very useful:

```python
word = "Kuwait City"
vowels = [ch for ch in word if ch in "aeiou"]
print(vowels)
```

```text
['u', 'a', 'i', 'i']
```

Note that `"C"` is not in `"aeiou"`, and neither is the space. Also, uppercase vowels such as `"A"` would not be found, because `"A"` is not in `"aeiou"`. Use `"aeiouAEIOU"` to include both.

### 8.4 Filtering and changing at the same time

The expression and the condition are independent. You can keep some items **and** change them:

```python
prices = [3, 12, 7, 20]
sale = [p / 2 for p in prices if p > 10]
print(sale)
```

```text
[6.0, 10.0]
```

Only prices above 10 KD are kept, and each kept price is halved. (`/` always gives a float.)

---

## 9. Choosing a Value with if … else

### 9.1 First, a new tool: the conditional expression

You know the `if` **statement**:

```python
mark = 72
if mark >= 60:
    result = "Pass"
else:
    result = "Fail"
print(result)
```

```text
Pass
```

Python also has a **conditional expression** that does the same job in one line:

```text
value_if_true if condition else value_if_false
```

```python
mark = 72
result = "Pass" if mark >= 60 else "Fail"
print(result)
```

```text
Pass
```

How Python evaluates it:

1. Check the condition `mark >= 60`.
2. If it is `True`, the whole expression gives `"Pass"`.
3. If it is `False`, the whole expression gives `"Fail"`.

Rules:

- It **must** have both `if` and `else`. There is no "if only" version.
- It gives a **value**, so you can use it anywhere a value is allowed: in an assignment, in `print()`, or as the expression of a list comprehension.
- Use it only for **simple** choices between two values. For anything more complex, use a normal `if` statement.

```python
temp = 38
print("Hot" if temp >= 45 else "Warm")
```

```text
Warm
```

### 9.2 Using it inside a list comprehension

Because a conditional expression is just an expression, it can be the expression part of a comprehension:

```text
new_list = [A if condition else B for item in sequence]
```

```python
marks = [72, 55, 60, 91]
results = ["Pass" if m >= 60 else "Fail" for m in marks]
print(results)
```

```text
['Pass', 'Fail', 'Pass', 'Pass']
```

Here, **every** mark produces a value — either `"Pass"` or `"Fail"`. So the new list has the **same length** as `marks`.

Another example: replace negative readings with 0.

```python
nums = [4, -2, 7, -5]
fixed = [n if n > 0 else 0 for n in nums]
print(fixed)
```

```text
[4, 0, 7, 0]
```

### 9.3 Filter `if` versus choose `if … else`

This is the most important difference in this lecture.

| | Filter | Choose |
|---|---|---|
| Form | `[x for x in seq if cond]` | `[A if cond else B for x in seq]` |
| Position of `if` | at the **end**, after `for` | at the **front**, before `for` |
| `else` | **not allowed** | **required** |
| What happens to items where `cond` is False | removed | replaced by `B` |
| Length of new list | same or shorter | always the same |

```python
nums = [4, -2, 7, -5]
print([n * 10 for n in nums])
print([n for n in nums if n > 0])
print([n if n > 0 else 0 for n in nums])
```

```text
[40, -20, 70, -50]
[4, 7]
[4, 0, 7, 0]
```

**Memory tip:** an `if` at the end is a **gate** (it lets items through or not). An `if … else` at the front is a **fork** (every item takes one of two roads).

### 9.4 Using both together (optional)

You can choose **and** filter in the same comprehension. The fork goes at the front and the gate at the end:

```python
nums = [3, -1, 8, 0, 5]
labels = ["even" if n % 2 == 0 else "odd" for n in nums if n > 0]
print(labels)
```

```text
['odd', 'even', 'odd']
```

First the gate keeps only 3, 8, and 5. Then the fork labels each one. This is correct Python, but it is getting harder to read. Use it only when it stays clear.

---

## 10. Comprehensions with len() and sum()

A comprehension gives a list, and you already know functions that work on lists.

### 10.1 Counting with len()

```python
temps = [46, 48, 44, 50, 47, 43, 49]
hot_days = len([t for t in temps if t >= 48])
print("Very hot days:", hot_days)
```

```text
Very hot days: 3
```

Compare this with the counter pattern from the loops lecture: one line instead of five.

### 10.2 Totals with sum()

```python
bills = [12, 45, 8, 30]   # KD
big_total = sum([b for b in bills if b > 10])
print("Total of big bills:", big_total)
```

```text
Total of big bills: 87
```

```python
nums = [1, 2, 3, 4, 5, 6]
print(sum([n * n for n in nums if n % 2 == 0]))
```

```text
56
```

The even numbers are 2, 4, 6; their squares are 4, 16, 36; and 4 + 16 + 36 = 56.

### 10.3 Average of selected items

```python
grades = [85, 92, 58, 74, 49]
passed = [g for g in grades if g >= 60]
average = sum(passed) / len(passed)
print("Average of passing grades:", average)
```

```text
Average of passing grades: 83.66666666666667
```

Be careful: if no grade passes, `passed` is empty and `len(passed)` is 0, so the division causes a `ZeroDivisionError`. Check `if len(passed) > 0:` first when this can happen.

---

## 11. Working with Two Lists Using Indexes

When two lists are related by **position** (item 0 of one list belongs with item 0 of the other), loop over the **indexes** with `range(len(...))`:

```python
prices = [1.5, 4, 2.25]    # KD per item
qty = [2, 1, 4]            # quantity of each item
line = [prices[i] * qty[i] for i in range(len(prices))]
print(line)
print("Total:", sum(line), "KD")
```

```text
[3.0, 4, 9.0]
Total: 16.0 KD
```

| `i` | `prices[i]` | `qty[i]` | product |
|---|---|---|---|
| 0 | 1.5 | 2 | 3.0 |
| 1 | 4 | 1 | 4 |
| 2 | 2.25 | 4 | 9.0 |

You can also **filter** by one list and **keep** values from the other:

```python
names = ["Noor", "Ali", "Mona", "Fahad"]
marks = [88, 59, 74, 45]
passed = [names[i] for i in range(len(names)) if marks[i] >= 60]
print(passed)
```

```text
['Noor', 'Mona']
```

Both lists must have the same length. If `marks` is shorter than `names`, `marks[i]` causes an `IndexError`.

---

## 12. Important Facts

### 12.1 The original list does not change

```python
nums = [1, 2, 3]
doubled = [n * 2 for n in nums]
print(nums)
print(doubled)
```

```text
[1, 2, 3]
[2, 4, 6]
```

If you want to **replace** the old list, assign the result back to the same name:

```python
nums = [1, 2, 3]
nums = [n * 2 for n in nums]
print(nums)
```

```text
[2, 4, 6]
```

### 12.2 The loop variable exists only inside the comprehension

After a `for` loop, the loop variable still exists. After a list comprehension, it does **not**:

```python
for k in range(3):
    print(k)
print("After the loop:", k)
```

```text
0
1
2
After the loop: 2
```

```text
squares = [j * j for j in range(3)]
print(j)
NameError: name 'j' is not defined
```

This is a good thing: the comprehension does not accidentally change a variable with the same name outside it.

### 12.3 An empty sequence gives an empty list

```python
print([x * 2 for x in []])
print([ch for ch in ""])
```

```text
[]
[]
```

### 12.4 Long comprehensions can use several lines

Inside brackets, Python allows you to continue on the next line. This makes long comprehensions easier to read:

```python
names = ["Noor", "Ali", "Mona", "Fahad"]
marks = [88, 59, 74, 45]
passed = [names[i]
          for i in range(len(names))
          if marks[i] >= 60]
print(passed)
```

```text
['Noor', 'Mona']
```

---

## 13. When to Use a Normal Loop Instead

List comprehensions are a **shortcut for building lists**. They are not a replacement for every loop.

**Use a comprehension when:**

- You want to create a **new list**.
- Each new item comes from **one simple expression** (with an optional simple filter or choice).
- The whole idea fits comfortably on one line (or a few short lines).

**Use a normal loop when:**

- You do not need a list — for example, you only want to **print** something.
- Each item needs **several steps**, or an `if / elif / else` with three or more cases.
- You need to update **several variables** at the same time (for example a total and a counter).
- The comprehension becomes **hard to read**.

Readable code is more important than short code. Ask yourself: *"Would a classmate understand this line quickly?"* If not, use a loop.

Here is a case where a loop is clearer, because each grade needs three possible letters:

```python
marks = [91, 76, 58]
letters = []
for m in marks:
    if m >= 90:
        letters.append("A")
    elif m >= 60:
        letters.append("P")
    else:
        letters.append("F")
print(letters)
```

```text
['A', 'P', 'F']
```

---

## 14. Optional: A Comprehension with Two for Parts

This section is for students who want to go further. You will not need it for the exercises in this lecture.

A comprehension can contain **two** `for` parts. It works like a **nested loop**: the second `for` is the inner loop.

```python
sizes = ["Small", "Large"]
drinks = ["Tea", "Karak"]
menu = [s + " " + d for s in sizes for d in drinks]
print(menu)
```

```text
['Small Tea', 'Small Karak', 'Large Tea', 'Large Karak']
```

The same thing as a nested loop:

```python
sizes = ["Small", "Large"]
drinks = ["Tea", "Karak"]
menu = []
for s in sizes:
    for d in drinks:
        menu.append(s + " " + d)
print(menu)
```

```text
['Small Tea', 'Small Karak', 'Large Tea', 'Large Karak']
```

These quickly become hard to read, so use them carefully.

---

## 15. Common Mistakes

### Mistake 1: Writing the parts in loop order

**Incorrect**

```python
# Incorrect
nums = [1, 2, 3]
doubled = [for n in nums: n * 2]
```

**Why?** In a comprehension, the expression comes **first**, and there is **no colon**. Python gives a `SyntaxError`.

**Correct**

```python
nums = [1, 2, 3]
doubled = [n * 2 for n in nums]
print(doubled)
```

```text
[2, 4, 6]
```

### Mistake 2: Using round brackets

**Incorrect**

```text
nums = [1, 2, 3]
doubled = (n * 2 for n in nums)
print(doubled)
<generator object <genexpr> at 0x7f...>
```

**Why?** Round brackets do not create a list. They create a different kind of object (a *generator*) that you will not study in this course. Printing it does not show the values.

**Correct:** use square brackets `[ ]`.

### Mistake 3: Putting `else` after a filter

**Incorrect**

```python
# Incorrect
nums = [4, -2, 7]
pos = [n for n in nums if n > 0 else 0]
```

**Why?** An `if` at the **end** is a filter, and a filter cannot have `else`. `SyntaxError`.

**Correct** — decide what you want:

```python
nums = [4, -2, 7]
print([n for n in nums if n > 0])            # remove negatives
print([n if n > 0 else 0 for n in nums])     # replace negatives
```

```text
[4, 7]
[4, 0, 7]
```

### Mistake 4: `if` at the front without `else`

**Incorrect**

```python
# Incorrect
nums = [4, -2, 7]
pos = [n if n > 0 for n in nums]
```

**Why?** An `if` at the **front** is a conditional expression, and it must have `else`. `SyntaxError`. If you only want to keep some items, move the `if` to the end.

### Mistake 5: Not storing the result

**Incorrect**

```python
prices = [1, 2, 3]
[p * 2 for p in prices]
print(prices)
```

```text
[1, 2, 3]
```

**Why?** The comprehension creates a new list, but it is not stored in any variable, so it is lost immediately. The original list never changes.

**Correct**

```python
prices = [1, 2, 3]
prices = [p * 2 for p in prices]
print(prices)
```

```text
[2, 4, 6]
```

### Mistake 6: Using a comprehension only to print

**Incorrect**

```python
cities = ["Kuwait", "Doha"]
x = [print(c) for c in cities]
print(x)
```

```text
Kuwait
Doha
[None, None]
```

**Why?** `print()` displays text but gives back the value `None`. The comprehension builds a useless list of `None` values. Comprehensions are for building lists, not for doing actions.

**Correct**

```python
cities = ["Kuwait", "Doha"]
for c in cities:
    print(c)
```

```text
Kuwait
Doha
```

### Mistake 7: Using the loop variable after the comprehension

**Incorrect**

```text
squares = [k * k for k in range(4)]
print("Last k was", k)
NameError: name 'k' is not defined
```

**Why?** The loop variable of a comprehension exists only inside the brackets.

**Correct:** if you need the last value, take it from the list (`squares[-1]`) or use a normal loop.

### Mistake 8: Forgetting that the expression is the item itself

**Incorrect** (goal: keep the even numbers)

```python
nums = [3, 4, 7, 10]
evens = [n % 2 == 0 for n in nums]
print(evens)
```

```text
[False, True, False, True]
```

**Why?** The test was written in the **expression** position, so the new list contains the results of the test (`True` / `False`), not the numbers.

**Correct:** the expression is `n`; the test goes in the filter.

```python
nums = [3, 4, 7, 10]
evens = [n for n in nums if n % 2 == 0]
print(evens)
```

```text
[4, 10]
```

---

## 16. Mini Practice Questions

Try these before looking at the answers at the end of this section.

**Q1.** What does this print?

```python
print([x + x for x in "ab"])
```

**Q2.** How many items does this list have?

```python
r = [i for i in range(20) if i % 5 == 0]
```

**Q3.** Rewrite as a comprehension:

```python
result = []
for n in range(1, 4):
    result.append(n * 100)
```

**Q4.** Which line is correct Python, A or B?

```text
A:  [n for n in nums if n > 0 else 0]
B:  [n if n > 0 else 0 for n in nums]
```

**Q5.** What does this print?

```python
words = ["Kuwait", "UAE", "Oman"]
print([w for w in words if len(w) > 3])
```

**Q6.** What does this print?

```python
print(len([c for c in "Bahrain" if c == "a"]))
```

### Answers to Mini Practice

1. **`['aa', 'bb']`** — each character is joined to itself.
2. **4 items:** `[0, 5, 10, 15]`.
3. **`result = [n * 100 for n in range(1, 4)]`**, which gives `[100, 200, 300]`.
4. **B.** An `if … else` must be at the front. A filter `if` at the end cannot have `else`.
5. **`['Kuwait', 'Oman']`** — `"UAE"` has 3 characters, and `3 > 3` is `False`.
6. **`2`** — `"Bahrain"` contains the letter `"a"` twice.

---

## 17. Ask AI to Help You Understand

Use an AI assistant as a private tutor. Ask it to explain and give hints, not only answers.

```text
Explain Python list comprehensions to me using a list of 5 prices in Kuwaiti Dinar.
For each example, also show the equivalent for loop. Do not give me exercises yet.
```

```text
I am confused about the difference between
[x for x in nums if x > 0] and [x if x > 0 else 0 for x in nums].
Explain it with a small list and show what happens to each item.
```

```text
Give me 5 for loops that use append(), one at a time.
Ask me to rewrite each as a list comprehension and wait for my answer before correcting it.
```

```text
Here is a list comprehension I do not understand. Rewrite it as a normal for loop,
then trace it step by step with a table. [paste the comprehension here]
```

```text
Give me three simple exercises about Python list comprehensions with filtering.
Give me hints first and do not show the solutions unless I ask.
```

> **Remember:** Always run the code yourself. AI can make mistakes, and running code is the only way to be sure.

---

## 18. Summary

- A **list comprehension** builds a **new list** in one line: `[expression for item in sequence]`.
- It replaces the pattern **empty list → `for` loop → `append()`**. To convert, put the `append` expression first and the `for` header after it, with no colon.
- The **expression** can be any value: arithmetic, a function call, string operations, indexing, slicing, a comparison, or the item itself.
- The **sequence** can be a list, a string, or a `range()`.
- **Filter** with `if condition` at the **end** — no `else`; the list may get shorter.
- **Choose** with `A if condition else B` at the **front** — `else` is required; the length stays the same.
- Combine with `len()` to count and `sum()` to add up.
- Use `range(len(...))` to work with two related lists.
- The original list is never changed. Store the result in a variable.
- The loop variable exists only inside the comprehension.
- If a comprehension is hard to read, or you are not building a list, use a normal loop.

---

## Basic Exercises

> Exercises 1–12 are the same as in the slides. Exercises 13–16 are extra practice.

**Exercise 1.** Predict the output.

```python
print([n * 10 for n in [1, 2, 3]])
```

**Exercise 2.** Predict the output.

```python
print([c for c in "Doha" if c != "o"])
```

**Exercise 3.** This line should keep the numbers greater than 3 and double them. Find and fix the error.

```text
result = [x * 2 for x in nums if x > 3 else x]
```

**Exercise 4.** Rewrite this loop as a list comprehension.

```python
cities = ["Kuwait", "Riyadh", "Manama"]
lengths = []
for city in cities:
    lengths.append(len(city))
```

**Exercise 13.** Predict the output.

```python
print([len(w) for w in ["UAE", "Oman", "Kuwait"]])
```

## Practice Exercises

**Exercise 5.** Use a list comprehension to make a list of the first 6 multiples of 5, starting from 5: `[5, 10, 15, 20, 25, 30]`.

**Exercise 6.** From `marks = [55, 72, 90, 48, 60, 81]`, build a list of the **failing** marks (below 60). Then print how many there are.

**Exercise 7.** From `temps = [46, 38, 50, 41]`, build a list that has `"Hot"` for 45 or more, and `"Warm"` otherwise.

**Exercise 8.** Explain what this code does and give its output.

```python
gcc = ["Kuwait", "Saudi Arabia", "UAE",
       "Qatar", "Bahrain", "Oman"]
long_names = [g for g in gcc if len(g) > 5]
print(long_names)
```

**Exercise 14.** Use `range()` and a filter to build a list of all multiples of 7 between 1 and 50.

## Challenge Exercises

**Exercise 9.** Use one comprehension to build the list of names of students who **passed** (60 or more).

```python
names = ["Noor", "Ali", "Mona", "Fahad"]
marks = [88, 59, 74, 45]
```

**Exercise 10.** Rewrite this comprehension as a normal `for` loop. What does it print?

```python
odd_sq = [x * x for x in range(1, 8) if x % 2 == 1]
print(odd_sq)
```

**Exercise 11.** Use a comprehension and `len()` to count the vowels (upper or lower case) in `"Kuwait University"`.

**Exercise 12.** Electricity readings (kWh) for 5 homes are below. Readings above 3000 kWh are charged at double. Build a list where each reading **more than 3000** is **doubled** and the others stay the same. Print the list and its sum.

```python
kwh = [2500, 3200, 1800, 4100, 3000]
```

**Exercise 15.** The string below contains letters, spaces, and digits. Use list comprehensions to (a) build a list of the **digit characters**, then (b) build a list of those digits as **integers** using `int()`, and (c) print their sum.

```python
text = "Kuwait City 2026"
```

**Exercise 16.** A shop gives **25% off**, but only on items that cost **more than 10 KD**. Cheaper items keep their price. Build the list of new prices with one comprehension. (25% off means `p - p / 4`.)

```python
prices = [8, 12, 20, 40]
```

---

# Exercise Solutions

### Solution 1

Each number is multiplied by 10.

```text
[10, 20, 30]
```

### Solution 2

The filter keeps every character that is not `"o"`. The result is a list of characters.

```text
['D', 'h', 'a']
```

### Solution 3

An `if` at the end is a filter, and a filter cannot have `else`. Since the goal is to **keep** only numbers greater than 3, remove `else x`:

```python
nums = [2, 5, 1, 8]
result = [x * 2 for x in nums if x > 3]
print(result)
```

```text
[10, 16]
```

### Solution 4

Move the `append()` expression to the front and drop the colon.

```python
cities = ["Kuwait", "Riyadh", "Manama"]
lengths = [len(city) for city in cities]
print(lengths)
```

```text
[6, 6, 6]
```

### Solution 5

`range(1, 7)` gives 1 to 6, and each is multiplied by 5.

```python
multiples = [5 * i for i in range(1, 7)]
print(multiples)
```

```text
[5, 10, 15, 20, 25, 30]
```

Another correct answer: `[i for i in range(5, 31, 5)]`.

### Solution 6

```python
marks = [55, 72, 90, 48, 60, 81]
failing = [m for m in marks if m < 60]
print(failing)
print("Failing:", len(failing))
```

```text
[55, 48]
Failing: 2
```

60 is not below 60, so it is not included.

### Solution 7

Every temperature gets a label, so we use `if … else` at the front.

```python
temps = [46, 38, 50, 41]
labels = ["Hot" if t >= 45 else "Warm" for t in temps]
print(labels)
```

```text
['Hot', 'Warm', 'Hot', 'Warm']
```

### Solution 8

The code builds a new list containing only the GCC country names that have **more than 5 characters**. "Kuwait" has 6, "Saudi Arabia" has 12 (the space counts), and "Bahrain" has 7. "Qatar" has exactly 5, so it is not included.

```text
['Kuwait', 'Saudi Arabia', 'Bahrain']
```

### Solution 9

Loop over the indexes. Use `marks[i]` in the condition, and `names[i]` as the expression.

```python
names = ["Noor", "Ali", "Mona", "Fahad"]
marks = [88, 59, 74, 45]
passed = [names[i] for i in range(len(names)) if marks[i] >= 60]
print(passed)
```

```text
['Noor', 'Mona']
```

### Solution 10

The comprehension has a filter, so the loop has an `if` inside it.

```python
odd_sq = []
for x in range(1, 8):
    if x % 2 == 1:
        odd_sq.append(x * x)
print(odd_sq)
```

```text
[1, 9, 25, 49]
```

The odd numbers from 1 to 7 are 1, 3, 5, 7; their squares are 1, 9, 25, 49.

### Solution 11

```python
text = "Kuwait University"
vowels = [ch for ch in text if ch in "aeiouAEIOU"]
print("Vowels:", len(vowels))
```

```text
Vowels: 7
```

The vowels are u, a, i (in "Kuwait") and U, i, e, i (in "University"). The uppercase `U` is counted because `"aeiouAEIOU"` includes uppercase vowels.

### Solution 12

Every reading produces a value, so this is a **choose** (`if … else`), not a filter.

```python
kwh = [2500, 3200, 1800, 4100, 3000]
charged = [k * 2 if k > 3000 else k for k in kwh]
print(charged)
print("Total:", sum(charged))
```

```text
[2500, 6400, 1800, 8200, 3000]
Total: 21900
```

3000 is not **more than** 3000, so it stays the same.

### Solution 13

Each word is replaced by its length.

```text
[3, 4, 6]
```

### Solution 14

```python
sevens = [n for n in range(1, 51) if n % 7 == 0]
print(sevens)
```

```text
[7, 14, 21, 28, 35, 42, 49]
```

Another correct answer without a filter: `[7 * i for i in range(1, 8)]`.

### Solution 15

```python
text = "Kuwait City 2026"
digit_chars = [ch for ch in text if ch in "0123456789"]
digits = [int(ch) for ch in digit_chars]
print(digit_chars)
print(digits)
print("Sum:", sum(digits))
```

```text
['2', '0', '2', '6']
[2, 0, 2, 6]
Sum: 10
```

The first list contains **strings**, so `sum()` would not work on it. The second comprehension converts each one to an integer.

### Solution 16

Every price produces a value (some changed, some not), so we use `if … else` at the front.

```python
prices = [8, 12, 20, 40]
new_prices = [p - p / 4 if p > 10 else p for p in prices]
print(new_prices)
```

```text
[8, 9.0, 15.0, 30.0]
```

8 is not more than 10, so it stays `8` (an integer). The other prices are reduced by a quarter; because `/` gives a float, they become `9.0`, `15.0`, and `30.0`.

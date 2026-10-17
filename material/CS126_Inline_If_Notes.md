# CS126 – Introduction to Python

## Inline if and Inline else if

**Instructor:** Dr. Fawaz Alazemi

---

## Learning Objectives

After studying these notes, you should be able to:

1. Explain what an inline if (a **conditional expression**) is, and how it differs from a regular `if` statement.
2. Write the form `value_if_true if condition else value_if_false` and name each part.
3. Convert a regular `if / else` that assigns one variable into an inline if, and convert it back.
4. Use an inline if with numbers, strings, lists, tuples, sets, and the logical operators `and`, `or`, `not`.
5. Explain why only one of the two values is calculated, and use this to avoid errors.
6. Write an **inline else if** (a chained conditional expression): `A if c1 else B if c2 else C`.
7. Use brackets correctly when an inline if is part of a bigger expression.
8. Decide when an inline if makes code clearer and when a regular `if` is the better choice.

---

## 1. Introduction

### 1.1 A pattern you write very often

You already know the regular `if / else` statement. Very often, its only job is to choose **which value** to store in a variable:

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

Four lines are used to make **one** decision about **one** value. The same variable name, `result`, is written twice.

### 1.2 The same decision in one line

Python lets you write this choice as a single **expression**:

```python
mark = 72
result = "Pass" if mark >= 60 else "Fail"
print(result)
```

```text
Pass
```

This is called an **inline if**. Its official name in Python is a **conditional expression**. You can read it almost like an English sentence:

> *"result is `"Pass"` if the mark is at least 60, else `"Fail"`."*

### 1.3 Why learn it?

- It is **shorter** when the decision is simple.
- It keeps the decision **next to** the place where the value is used.
- It can be used **inside** other code: inside `print()`, inside a calculation, inside a string.
- It is very common in Python programs written by others, so you need to be able to **read** it.

### 1.4 What about "else if"?

A regular `if` can test more than one condition with `elif`. The inline if can do the same by putting **another inline if after `else`**:

```python
temp = 38
level = "Very hot" if temp >= 45 else "Hot" if temp >= 30 else "Mild"
print(level)
```

```text
Hot
```

We call this the **inline else if** (or a **chained** conditional expression). Section 9 explains it in detail.

---

## 2. Main Concepts and Vocabulary

| Term | Meaning | Example |
|---|---|---|
| **Statement** | A complete instruction that **does** something | `x = 5`, a regular `if` block |
| **Expression** | Code that **produces a value** | `3 + 4`, `len("abc")`, `x > 5` |
| **Condition** | An expression that is `True` or `False` | `mark >= 60` |
| **Conditional expression** (inline if) | An expression that gives one of two values depending on a condition | `"Pass" if mark >= 60 else "Fail"` |
| **Chained conditional expression** (inline else if) | An inline if whose `else` part is another inline if | `A if c1 else B if c2 else C` |
| **Operator priority** (precedence) | The order in which Python applies operators | `*` before `+` |

The key idea of this lecture:

- A regular `if` is a **statement**: it decides which **lines of code run**.
- An inline `if` is an **expression**: it decides which **value you get**.

---

## 3. Syntax

### 3.1 General form

```text
value_if_true if condition else value_if_false
```

| Part | Meaning |
|---|---|
| `value_if_true` | The value of the whole expression when the condition is `True` |
| `if` | Keyword |
| `condition` | Any expression that is `True` or `False` (comparisons, `in`, `and`, `or`, `not`, …) |
| `else` | Keyword — **always required** |
| `value_if_false` | The value of the whole expression when the condition is `False` |

### 3.2 Important differences from a regular if

| | Regular `if` | Inline `if` |
|---|---|---|
| Kind | statement | expression |
| Gives a value? | No | Yes |
| Order | `if condition:` → true block → `else:` → false block | true value → `if condition` → `else` false value |
| Colons and indentation | Yes | No |
| `else` required? | No | **Yes** |
| Each branch can contain | many lines | **one value** |

Notice the order: in an inline if, the **True value comes first**, before the word `if`. This feels strange at first, but it matches how we often speak: *"Take an umbrella **if** it rains, **else** sunglasses."*

### 3.3 Using the result

Because an inline if produces a value, you can use it anywhere a value is allowed:

```python
temp = 47
label = "Hot" if temp >= 45 else "Normal"
print(label)
print("Hot" if temp >= 45 else "Normal")
print("Today is " + ("hot" if temp >= 45 else "normal"))
```

```text
Hot
Hot
Today is hot
```

1. Stored in a variable.
2. Passed directly to `print()`.
3. Used as part of a bigger string expression (note the brackets — see Section 7).

---

## 4. How an Inline if Is Evaluated

### 4.1 The steps

When Python meets `A if condition else B`:

1. It evaluates the **condition** first.
2. If the condition is `True`, it evaluates **A**, and that is the result.
3. If the condition is `False`, it evaluates **B**, and that is the result.

### 4.2 Walkthrough

```python
n = 7
kind = "even" if n % 2 == 0 else "odd"
print(n, "is", kind)
```

```text
7 is odd
```

1. Python evaluates the condition `n % 2 == 0`.
2. `7 % 2` is `1`, and `1 == 0` is `False`.
3. So Python uses the value after `else`: `"odd"`.
4. `kind` stores `"odd"`.

With `n = 10`, the condition `10 % 2 == 0` is `True`, so `kind` would be `"even"`.

### 4.3 Only one value is calculated

Python **never** calculates the value that is not chosen. This is useful for avoiding errors:

```python
total = 90
count = 0
avg = total / count if count != 0 else 0
print(avg)
```

```text
0
```

The condition `count != 0` is `False`, so Python goes straight to the `else` value. It never tries `total / count`, which would cause a `ZeroDivisionError`.

The same idea protects list indexes:

```python
names = []
first = names[0] if len(names) > 0 else "nobody"
print(first)
```

```text
nobody
```

`names[0]` would cause an `IndexError` on an empty list, but it is never evaluated.

---

## 5. Converting Between Regular if and Inline if

### 5.1 From regular if to inline if

An `if / else` can become an inline if when **both branches assign a value to the same variable** (and do nothing else).

```python
age = 20
if age >= 18:
    status = "Adult"
else:
    status = "Minor"
print(status)
```

```text
Adult
```

Recipe:

1. Write the variable and `=`: `status =`
2. Write the **True value**: `"Adult"`
3. Write `if` and the **condition**: `if age >= 18`
4. Write `else` and the **False value**: `else "Minor"`
5. No colons, no indentation.

```python
age = 20
status = "Adult" if age >= 18 else "Minor"
print(status)
```

```text
Adult
```

### 5.2 From inline if to regular if

Reading an inline if is easier if you can "unfold" it:

```text
x = A if condition else B
```

means exactly:

```text
if condition:
    x = A
else:
    x = B
```

### 5.3 When you cannot convert

Do **not** convert to an inline if when:

- the two branches change **different** variables,
- a branch has **more than one** line,
- the branches perform **actions** (such as printing different messages and also changing data),
- there is an `if` with **no** `else` (the inline if always needs `else`).

```python
balance = 30
amount = 50
if balance < amount:
    print("Not enough money")
else:
    balance = balance - amount
    print("Paid")
```

```text
Not enough money
```

This must stay a regular `if`: the branches do different things, and one branch has two lines.

---

## 6. Using Inline if with Different Types

### 6.1 Numbers

```python
a = 14
b = 9
bigger = a if a > b else b
print(bigger)
```

```text
14
```

```python
x = -8
distance = x if x >= 0 else -x
print(distance)
```

```text
8
```

The second example gives the **absolute value** of `x` (its distance from zero).

A member discount:

```python
price = 20
member = True
discount = price * 0.1 if member else 0
total = price - discount
print("Discount:", discount)
print("Total:", total, "KD")
```

```text
Discount: 2.0
Total: 18.0 KD
```

### 6.2 Strings

```python
ch = "e"
print("vowel" if ch in "aeiou" else "consonant")
```

```text
vowel
```

Choosing a default when text is empty:

```python
name = "  "
shown = name.strip() if name.strip() != "" else "Guest"
print("Welcome,", shown)
```

```text
Welcome, Guest
```

Adding `"s"` only when there is more than one item:

```python
count = 1
print(str(count) + " item" + ("" if count == 1 else "s"))
count = 3
print(str(count) + " item" + ("" if count == 1 else "s"))
```

```text
1 item
3 items
```

### 6.3 Lists, tuples, and sets

Any condition you know works, including `len()`, `in`, and indexes:

```python
cart = []
print("Empty cart" if len(cart) == 0 else "Ready to pay")
weekend = ("Fri", "Sat")
day = "Sat"
print("Day off" if day in weekend else "Work day")
allowed = {"sara", "ali"}
user = "fahad"
print("Welcome" if user in allowed else "Access denied")
temps = [44, 46, 49]
print("Warmer" if temps[-1] > temps[0] else "Not warmer")
```

```text
Empty cart
Day off
Access denied
Warmer
```

The **values** can also be lists, tuples, or sets:

```python
vip = True
benefits = ["lounge", "fast track"] if vip else []
print(len(benefits), benefits)
```

```text
2 ['lounge', 'fast track']
```

### 6.4 Logical operators

The condition can combine several tests with `and`, `or`, and `not`:

```python
age = 15
student = False
price = 2 if age < 12 or student else 3.5
print("Ticket:", price, "KD")
gpa = 3.7
credits = 40
honor = "Yes" if gpa >= 3.5 and credits >= 30 else "No"
print("Honor list:", honor)
blocked = False
print("Login OK" if not blocked else "Blocked")
```

```text
Ticket: 3.5 KD
Honor list: Yes
Login OK
```

Python reads everything between `if` and `else` as **one** condition. In the first example, `15 < 12 or False` is `False`, so the price is 3.5.

When the condition is long, store it in a variable first. This keeps the inline if short:

```python
gpa = 3.7
credits = 40
qualified = gpa >= 3.5 and credits >= 30
honor = "Yes" if qualified else "No"
print(honor)
```

```text
Yes
```

---

## 7. Operator Priority: Use Brackets

### 7.1 The inline if has the lowest priority

Python applies operators in a fixed order: for example, `*` before `+`. The inline if comes **almost last** — after `+`, `-`, `*`, comparisons, `and`, and `or`. This means Python collects as much as possible into the True value and the False value **before** it applies the inline if.

### 7.2 A hidden bug with +

```python
cost = 50
msg = "Level: " + "high" if cost > 100 else "low"
print(msg)
```

```text
low
```

We expected `Level: low`. Python actually read the line as:

```text
msg = ("Level: " + "high") if cost > 100 else "low"
```

so in the False case, the `"Level: "` part is lost.

**Fix:** put brackets around the inline if, so Python knows exactly where it starts and ends:

```python
cost = 50
msg = "Level: " + ("high" if cost > 100 else "low")
print(msg)
```

```text
Level: low
```

### 7.3 A hidden bug with -

```python
price = 10
member = False
total = price - 2 if member else 0
print(total)
```

```text
0
```

Python read this as `(price - 2) if member else 0`, so non-members pay **nothing**! The correct version:

```python
price = 10
member = False
total = price - (2 if member else 0)
print(total)
```

```text
10
```

### 7.4 The rule

> When an inline if is **part of** a bigger expression, put it in **brackets**.

When the inline if is the **whole** right-hand side of `=` or the **whole** argument of `print()`, brackets are not needed (but they are never wrong).

---

## 8. Good Style: Values, Not Actions

The following code **works**, but it is considered poor style:

```python
mark = 72
print("Pass") if mark >= 60 else print("Fail")
```

```text
Pass
```

Here the inline if is used to choose an **action**, not a value. The value it produces is thrown away. It is clearer to choose the **value** and call `print()` once:

```python
mark = 72
print("Pass" if mark >= 60 else "Fail")
```

```text
Pass
```

Rule of thumb: **use an inline if when you want a value. Use a regular `if` when you want to choose between actions.**

---

## 9. Inline else if (Chained Conditional Expressions)

### 9.1 From elif to inline else if

A regular `if` with `elif`:

```python
temp = 38
if temp >= 45:
    level = "Very hot"
elif temp >= 30:
    level = "Hot"
else:
    level = "Mild"
print(level)
```

```text
Hot
```

The same decision as an inline else if:

```python
temp = 38
level = "Very hot" if temp >= 45 else "Hot" if temp >= 30 else "Mild"
print(level)
```

```text
Hot
```

General form:

```text
A if condition1 else B if condition2 else C
```

There is **no** `elif` keyword in the inline form. Instead, the part after the first `else` is itself a complete inline if.

### 9.2 How Python reads it

Python groups a chained inline if from the **right**, like this:

```text
A if condition1 else (B if condition2 else C)
```

So:

1. Check `condition1`. If `True`, the result is **A**, and nothing else is checked.
2. If `False`, evaluate the part after `else`, which is another inline if:
   - check `condition2`; if `True`, the result is **B**,
   - otherwise the result is **C**.

This is exactly how `if / elif / else` works: conditions are checked **from left to right**, and the **first** `True` condition wins.

| `temp` | `temp >= 45`? | `temp >= 30`? | Result |
|---|---|---|---|
| 48 | True | (not checked) | `"Very hot"` |
| 38 | False | True | `"Hot"` |
| 22 | False | False | `"Mild"` |

### 9.3 Writing it over several lines

A long chained inline if is hard to read on one line. Put it inside **brackets**, and then you may break it over several lines:

```python
temp = 22
level = ("Very hot" if temp >= 45 else
         "Hot" if temp >= 30 else
         "Mild")
print(level)
```

```text
Mild
```

Each line now shows one "value if condition" pair, which looks similar to an `if / elif / else` ladder.

### 9.4 Letter grades

```python
mark = 85
letter = ("A" if mark >= 90 else
          "B" if mark >= 80 else
          "C" if mark >= 70 else
          "D" if mark >= 60 else
          "F")
print("Mark", mark, "-> grade", letter)
```

```text
Mark 85 -> grade B
```

Trace for `mark = 85`:

1. `85 >= 90` → False → move on.
2. `85 >= 80` → True → the result is `"B"`. The remaining conditions are not checked.

This works, but five choices in one expression is near the limit of what is easy to read. Many programmers would write a regular `if / elif / else` here. Both are correct — choose the clearer one.

### 9.5 The order of conditions matters

Because the first `True` condition wins, overlapping conditions must be written from the **strictest** to the **widest**:

```python
mark = 95
wrong = "C" if mark >= 70 else "B" if mark >= 80 else "A"
right = "A" if mark >= 90 else "B" if mark >= 80 else "C"
print(wrong, right)
```

```text
C A
```

In `wrong`, `95 >= 70` is checked first and is `True`, so the result is `"C"` — the other conditions never get a chance.

### 9.6 Positive, negative, or zero

```python
x = 0
sign = "positive" if x > 0 else "negative" if x < 0 else "zero"
print(sign)
```

```text
zero
```

---

## 10. When to Use an Inline if

### 10.1 Good uses

- Choosing **one value** from **two** (sometimes three) simple options.
- Both values are **short**.
- The result goes into a variable, a `print()`, or a calculation.

```python
subtotal = 25
fee = 0 if subtotal >= 20 else 1.5
print(fee)
```

```text
0
```

### 10.2 Better as a regular if

- Each branch needs **several lines** or performs **actions**.
- The branches change **different variables**.
- There are **many** choices, or the conditions are long and complicated.
- An inline if would need to be **nested inside another** inline if in a confusing way.

### 10.3 The readability test

Ask yourself: *"Would a classmate understand this line in one reading?"* If not, use a regular `if`. Short code is good; **clear** code is better.

---

## 11. Quick Reference

| Goal | Inline form |
|---|---|
| Two choices | `x = A if cond else B` |
| Three choices (else if) | `x = A if c1 else B if c2 else C` |
| Inside `print()` | `print("Yes" if ok else "No")` |
| Inside a calculation | `total = price - (2 if member else 0)` |
| Inside a string | `"Level: " + ("high" if n > 100 else "low")` |
| Larger of two values | `big = a if a > b else b` |
| Absolute value | `d = x if x >= 0 else -x` |
| Safe division | `avg = t / n if n != 0 else 0` |
| Safe first item | `first = lst[0] if len(lst) > 0 else None` |
| Default text | `shown = name if name != "" else "Guest"` |

---

## 12. Worked Examples

### 12.1 Online order

```python
subtotal = 17.5
member = True
shipping = 0 if subtotal >= 20 or member else 1.5
discount = subtotal * 0.05 if member else 0
total = subtotal + shipping - discount
print("Shipping:", shipping)
print("Discount:", discount)
print("Total:", total, "KD")
print("Free shipping!" if shipping == 0 else "")
```

```text
Shipping: 0
Discount: 0.875
Total: 16.625 KD
Free shipping!
```

1. `17.5 >= 20` is `False`, but `member` is `True`, so the `or` condition is `True` → shipping is 0.
2. The member discount is 17.5 × 0.05 = 0.875.
3. Total = 17.5 + 0 − 0.875 = 16.625.
4. Because shipping is 0, the last line prints the message.

### 12.2 Electricity bill with tiers

```python
kwh = 2500
rate_fils = (3 if kwh <= 1000 else
             5 if kwh <= 3000 else
             10)
bill = kwh * rate_fils / 1000
level = "low" if bill < 10 else "high"
print("Rate:", rate_fils, "fils per kWh")
print("Bill:", bill, "KD")
print("Usage level:", level)
```

```text
Rate: 5 fils per kWh
Bill: 12.5 KD
Usage level: high
```

(The rates are simple examples, not official prices.)

### 12.3 Weekly temperature summary

```python
temps = [44, 46, 48, 45, 47, 49, 43]
first = temps[0]
last = temps[-1]
trend = ("warmer" if last > first else
         "cooler" if last < first else
         "the same")
hot_week = "Yes" if 49 in temps or 50 in temps else "No"
print("The week ended", trend)
print("Reached 49 or 50:", hot_week)
print(len(temps), "day" if len(temps) == 1 else "days")
```

```text
The week ended cooler
Reached 49 or 50: Yes
7 days
```

### 12.4 Mobile data package

```python
used = 12.5
limit = 10
extra = used - limit if used > limit else 0
print("Extra cost:", extra * 1.5, "KD")
print("Over limit" if used > limit else
      "At limit" if used == limit else "Under limit")
```

```text
Extra cost: 3.75 KD
Over limit
```

The first inline if needs no brackets because it is the **whole** right side of `=`: Python reads it as `(used - limit) if used > limit else 0`, which is what we want.

---

## 13. Important Notes

- An inline if is an **expression**: it always produces a value.
- Order: **True value**, `if`, condition, `else`, **False value**.
- The `else` part is **always required**.
- Only the chosen value is calculated — the other one is skipped completely.
- In a chained inline if, conditions are checked **from left to right**, and the first `True` one wins. Put the strictest condition first.
- The inline if has very **low priority**. Use **brackets** when it is part of a bigger expression.
- Inside brackets, a long inline if may be split over several lines.
- Use inline if for **values**, not for choosing actions.
- If an inline if is hard to read, use a regular `if / elif / else`.

---

## 14. Common Mistakes

### Mistake 1: Forgetting else

**Incorrect**

```text
mark = 72
result = "Pass" if mark >= 60

SyntaxError: expected 'else' after 'if' expression
```

**Correct**

```python
mark = 72
result = "Pass" if mark >= 60 else "Fail"
print(result)
```

```text
Pass
```

### Mistake 2: Using the regular-if order

**Incorrect**

```text
mark = 72
result = if mark >= 60 "Pass" else "Fail"

SyntaxError: invalid syntax
```

**Why?** The True value must come **before** `if`.

**Correct:** `result = "Pass" if mark >= 60 else "Fail"`

### Mistake 3: Adding colons

**Incorrect**

```text
result = "Pass" if mark >= 60: else: "Fail"

SyntaxError: invalid syntax
```

**Why?** The inline if has **no** colons. Colons belong only to the regular `if` statement.

### Mistake 4: Missing brackets with +

**Incorrect**

```python
cost = 50
msg = "Level: " + "high" if cost > 100 else "low"
print(msg)
```

```text
low
```

**Correct**

```python
cost = 50
msg = "Level: " + ("high" if cost > 100 else "low")
print(msg)
```

```text
Level: low
```

### Mistake 5: Missing brackets with -

**Incorrect**

```python
price = 10
member = False
total = price - 2 if member else 0
print(total)
```

```text
0
```

**Correct**

```python
price = 10
member = False
total = price - (2 if member else 0)
print(total)
```

```text
10
```

### Mistake 6: Wrong order of conditions in a chain

**Incorrect**

```python
mark = 95
letter = "C" if mark >= 70 else "B" if mark >= 80 else "A"
print(letter)
```

```text
C
```

**Correct** — strictest condition first:

```python
mark = 95
letter = "A" if mark >= 90 else "B" if mark >= 80 else "C"
print(letter)
```

```text
A
```

### Mistake 7: Using an inline if to choose actions

**Poor style**

```python
mark = 45
print("Pass") if mark >= 60 else print("Fail")
```

```text
Fail
```

**Better**

```python
mark = 45
print("Pass" if mark >= 60 else "Fail")
```

```text
Fail
```

### Mistake 8: Trying to put two statements in one branch

**Incorrect**

```text
x = 5
count = 0 if x > 3 else count = 1

SyntaxError: ...
```

**Why?** Each side of an inline if must be a single **value**, not an assignment or several statements. If you need to do more than choose one value, use a regular `if`.

---

## 15. Mini Practice Questions

Try these before looking at the answers at the end of this section.

**Q1.** What does this print?

```python
x = 12
print("big" if x > 10 else "small", "even" if x % 2 == 0 else "odd")
```

**Q2.** What does this print?

```python
s = "Kuwait"
print(s[0] if len(s) > 0 else "empty")
```

**Q3.** Which line is correct Python?

```text
A:  y = 5 if x > 0
B:  y = 5 if x > 0 else 0
C:  y = if x > 0 5 else 0
```

**Q4.** What does this print?

```python
a = 3
b = 3
print("A wins" if a > b else "B wins" if b > a else "Draw")
```

**Q5.** What does this print, and why?

```python
n = 4
print(10 + 1 if n > 5 else 0)
```

**Q6.** Rewrite as one line:

```text
if score >= 50:
    color = "green"
else:
    color = "red"
```

### Answers to Mini Practice

1. **`big even`**
2. **`K`**
3. **B.** A has no `else`; C has the wrong order.
4. **`Draw`** — both conditions are `False`.
5. **`0`** — Python reads `(10 + 1) if n > 5 else 0`, and `4 > 5` is `False`. Write `10 + (1 if n > 5 else 0)` if you want 10.
6. **`color = "green" if score >= 50 else "red"`**

---

## 16. Ask AI to Help You Understand

```text
Explain the Python conditional expression (inline if) to a beginner.
Compare it with a regular if/else that assigns one variable.
Use an example about student marks. Do not give me exercises yet.
```

```text
Why does "Level: " + "high" if x > 100 else "low" not work as expected in Python?
Explain operator priority in simple words and show how brackets fix it.
```

```text
Show me how to turn an if/elif/else that chooses one value into a chained
conditional expression. Then explain when the regular if/elif/else is clearer.
```

```text
Give me five short regular if/else blocks, one at a time. For each one,
ask me whether it can be written as an inline if, and wait for my answer.
```

```text
Give me five "predict the output" questions about Python inline if and
chained inline if. Give me hints first and do not show the answers unless I ask.
```

> **Remember:** Always run the code yourself. AI can make mistakes, and running code is the only way to be sure.

---

## 17. Summary

- An **inline if** (conditional expression) chooses a **value**: `A if condition else B`.
- It is an **expression**, so it can be stored, printed, or used inside calculations and strings.
- The **True value comes first**, and the `else` part is **always required**.
- Python evaluates the condition first and then calculates **only** the chosen value.
- The **inline else if** chains conditions: `A if c1 else B if c2 else C`. They are checked from left to right; the first `True` wins.
- The inline if has very low priority: use **brackets** when it is part of a bigger expression.
- Use it for short, simple choices between values. For actions, several lines, or many choices, use a regular `if / elif / else`.

---

## Basic Exercises

> Exercises 1–12 are the same as in the slides. Exercises 13–16 are extra practice.

**Exercise 1.** Predict the output.

```python
x = 7
print("odd" if x % 2 == 1 else "even")
y = -3
print(y if y > 0 else -y)
```

**Exercise 2.** Predict the output.

```python
t = 38
print("Hot" if t >= 45 else
      "Warm" if t >= 30 else "Cool")
```

**Exercise 3.** Find and fix the error.

```text
mark = 55
result = "Pass" if mark >= 60
print(result)
```

**Exercise 4.** Rewrite as one line with an inline if.

```text
if age >= 18:
    status = "Adult"
else:
    status = "Minor"
```

**Exercise 13.** Predict the output.

```python
items = ["pen"]
word = "item" if len(items) == 1 else "items"
print(len(items), word)
```

## Practice Exercises

**Exercise 5.** Parking costs nothing for the first hour; after that it is **0.25 KD per hour** for every hour. Use an inline if to print the fee for `hours = 3`, then for `hours = 1`.

**Exercise 6.** For a list `cart`, print `Cart is empty` or `Cart has N items` with one inline if. Test with `["rice", "tea"]`.

**Exercise 7.** Rewrite this with one inline else if.

```text
if speed > 120:
    label = "Too fast"
elif speed >= 60:
    label = "Normal"
else:
    label = "Slow"
```

**Exercise 8.** Explain what this code does and give its output.

```python
price = 5
member = False
total = price - (1 if member else 0)
print(total)
```

**Exercise 14.** A shop gives free delivery inside Kuwait City and charges 2 KD elsewhere. Given `area = "Jahra"`, use an inline if to set `delivery`, then print the total for a 12 KD order.

## Challenge Exercises

**Exercise 9.** This should print `Level: low`, but it prints `low`. Explain why, and fix it.

```python
cost = 50
msg = "Level: " + "high" if cost > 100 else "low"
print(msg)
```

**Exercise 10.** Use an inline else if to choose the rate: 3 fils per kWh up to 1000 kWh, 5 fils up to 3000, otherwise 10 fils. Print the bill in KD for `kwh = 4000`.

**Exercise 11.** Predict the output.

```python
a = 4
b = 9
big = a if a > b else b
small = b if a > b else a
same = "equal" if a == b else "different"
print(big - small, same)
```

**Exercise 12.** Using inline ifs only (no regular `if`), find the **largest** of three numbers `a, b, c = 12, 30, 7` and print it.

**Exercise 15.** A set `present = {"Ali", "Sara", "Mona"}` holds the students who attended. For `student = "Fahad"`, print `Fahad: present` or `Fahad: absent`, using `+` and an inline if inside brackets.

**Exercise 16.** Body temperature (°C) is classified as `"Low"` below 36.0, `"Normal"` from 36.0 up to 37.5, `"Fever"` above 37.5 up to 39.0, and `"High fever"` above 39.0. Write one chained inline if (split over several lines inside brackets) and test it with `temp = 38.2`.

---

# Exercise Solutions

### Solution 1

`7 % 2` is 1, so the first condition is `True` → `"odd"`. For `y = -3`, `-3 > 0` is `False`, so the result is `-y`, which is 3.

```text
odd
3
```

### Solution 2

`38 >= 45` is `False`, so Python moves to the second inline if. `38 >= 30` is `True`, so the result is `"Warm"`.

```text
Warm
```

### Solution 3

The `else` part is missing, which is a `SyntaxError: expected 'else' after 'if' expression`.

```python
mark = 55
result = "Pass" if mark >= 60 else "Fail"
print(result)
```

```text
Fail
```

### Solution 4

```python
age = 20
status = "Adult" if age >= 18 else "Minor"
print(status)
```

```text
Adult
```

### Solution 5

```python
hours = 3
fee = 0 if hours <= 1 else hours * 0.25
print("Fee:", fee, "KD")
hours = 1
fee = 0 if hours <= 1 else hours * 0.25
print("Fee:", fee, "KD")
```

```text
Fee: 0.75 KD
Fee: 0 KD
```

No brackets are needed: the inline if is the whole right side, and Python reads the False value as `hours * 0.25`, which is what we want.

### Solution 6

```python
cart = ["rice", "tea"]
print("Cart is empty" if len(cart) == 0
      else "Cart has " + str(len(cart)) + " items")
```

```text
Cart has 2 items
```

Here the `+` operations are all **inside** the False value, so they belong together, and no extra brackets are needed. The outer brackets of `print(...)` allow the line break.

### Solution 7

```python
speed = 90
label = ("Too fast" if speed > 120 else
         "Normal" if speed >= 60 else
         "Slow")
print(label)
```

```text
Normal
```

### Solution 8

The code charges members 1 KD less. Because `member` is `False`, the inline if in brackets gives 0, so the total stays 5. The brackets make sure that only the **discount** is chosen, not the whole price.

```text
5
```

### Solution 9

The inline if has the lowest priority, so Python reads the line as `("Level: " + "high") if cost > 100 else "low"`. When the condition is `False`, the whole result is just `"low"`. Put brackets around the inline if:

```python
cost = 50
msg = "Level: " + ("high" if cost > 100 else "low")
print(msg)
```

```text
Level: low
```

### Solution 10

```python
kwh = 4000
rate = (3 if kwh <= 1000 else
        5 if kwh <= 3000 else 10)
print("Bill:", kwh * rate / 1000, "KD")
```

```text
Bill: 40.0 KD
```

4000 is above 3000, so the rate is 10 fils: 4000 × 10 = 40000 fils = 40.0 KD.

### Solution 11

`4 > 9` is `False`, so `big` is `b` (9) and `small` is `a` (4). `4 == 9` is `False`, so `same` is `"different"`.

```text
5 different
```

### Solution 12

```python
a, b, c = 12, 30, 7
largest = (a if a >= b and a >= c else
           b if b >= c else
           c)
print(largest)
```

```text
30
```

If `a` is at least as large as both others, it wins. Otherwise the largest is either `b` or `c`, and the second inline if chooses between them.

### Solution 13

The list has one item, so the condition is `True`.

```text
1 item
```

### Solution 14

```python
area = "Jahra"
order = 12
delivery = 0 if area == "Kuwait City" else 2
print("Total:", order + delivery, "KD")
```

```text
Total: 14 KD
```

### Solution 15

```python
present = {"Ali", "Sara", "Mona"}
student = "Fahad"
print(student + ": " + ("present" if student in present else "absent"))
```

```text
Fahad: absent
```

Without the brackets, the False case would print only `absent`, losing the name.

### Solution 16

```python
temp = 38.2
status = ("Low" if temp < 36.0 else
          "Normal" if temp <= 37.5 else
          "Fever" if temp <= 39.0 else
          "High fever")
print(status)
```

```text
Fever
```

The conditions are checked in order: `38.2 < 36.0` is `False`, `38.2 <= 37.5` is `False`, and `38.2 <= 39.0` is `True`, so the result is `"Fever"`. Because each condition is only checked when the earlier ones were `False`, we do not need to write `temp >= 36.0 and temp <= 37.5`.

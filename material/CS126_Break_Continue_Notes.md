# CS126 – Introduction to Python

## Loop Control: break and continue

**Instructor:** Dr. Fawaz Alazemi

---

## Learning Objectives

After studying these notes, you should be able to:

1. Use `break` to stop a loop early, and say where Python continues afterwards.
2. Use `continue` to skip the rest of one round of a loop.
3. Use both keywords in `for` loops and in `while` loops.
4. Write `while True` loops that end with `break`, and compare them with condition-controlled `while` loops.
5. Use a **flag** variable to know, after a loop, whether `break` happened.
6. Explain what `break` and `continue` do inside **nested** loops.
7. Trace loops that contain `break` and `continue`, and avoid the common mistakes, including infinite loops caused by `continue`.

---

## 1. Introduction

### 1.1 What we already know

A `for` loop runs its body once for **every** item of a sequence. A `while` loop runs its body **as long as** its condition is `True`. In both cases, the loop decides when to stop **at the top** of each round:

- the `for` loop stops when no items are left;
- the `while` loop stops when the condition is `False`.

### 1.2 The problem

Sometimes we want to change this normal behaviour **from inside the body**:

- **Stop early.** We are searching a list for the first mark of 100. Once we find it, there is no reason to check the remaining items.
- **Skip an item.** We are calculating an average, but some marks are `0` because the student was absent. We want to ignore those items and carry on with the rest.

Look at this search without any loop control:

```python
marks = [72, 100, 85, 100, 64]
for m in marks:
    print("Checking", m)
    if m == 100:
        print("Found a full mark!")
```

```text
Checking 72
Checking 100
Found a full mark!
Checking 85
Checking 100
Found a full mark!
Checking 64
```

The loop found the full mark in round 2, but kept going to the end. It even reported a second full mark, which we did not ask for. With 10,000 students, most of the work would be wasted.

### 1.3 The two keywords

Python has two keywords that change how a loop runs:

| Keyword | Meaning | Real-life picture |
|---|---|---|
| `break` | Stop the **whole loop** now. | You leave a restaurant queue because your friend already bought the food. |
| `continue` | Stop **this round** now, and go to the next round. | You are marking exam papers, find a blank one, put it aside, and go on to the next paper. |

---

## 2. Vocabulary

| Term | Meaning |
|---|---|
| **Round** (iteration) | One run of the loop body |
| **`break`** | A keyword that ends the loop immediately |
| **`continue`** | A keyword that ends the current round and starts the next one |
| **`while True`** | A `while` loop whose condition is always true; it needs `break` to stop |
| **Flag** | A variable (usually `True`/`False`) that remembers whether something happened |
| **Nested loop** | A loop inside the body of another loop |
| **Innermost loop** | In nested loops, the loop that is directly around a statement |
| **Infinite loop** | A loop that never ends |

---

## 3. The break Statement

### 3.1 Syntax

```text
for item in sequence:
    # code that runs every round
    if condition:
        break
    # this code is skipped in the round where break runs
# Python continues here after break
```

Each part explained:

- `break` is a **keyword**. It is written alone on its own line, with no brackets and no value.
- It is almost always inside an `if`. That way the loop stops only **when a certain condition is True**. Without an `if`, the loop would stop in its very first round.
- When `break` runs, Python **leaves the loop at once**. Any lines below `break` in the body are not run, and no more rounds happen.
- Python then continues with the **first line after the loop** (the first line that is not indented under it).
- `break` works in the same way in `for` loops and `while` loops.

### 3.2 Example: the first hot day

```python
temps = [44, 47, 51, 49, 53]
for t in temps:
    print("Checking", t)
    if t > 50:
        print("First day above 50:", t)
        break
print("Done")
```

```text
Checking 44
Checking 47
Checking 51
First day above 50: 51
Done
```

Trace table:

| Round | `t` | `t > 50`? | What happens |
|---|---|---|---|
| 1 | 44 | False | the round ends normally; next round |
| 2 | 47 | False | the round ends normally; next round |
| 3 | 51 | **True** | print the message, then **break** |

The values 49 and 53 are **never checked**. After `break`, Python jumps to `print("Done")`.

### 3.3 Where you put the print matters

Compare these two loops:

```python
for n in range(1, 10):
    if n == 4:
        break
    print(n)
print("End")
```

```text
1
2
3
End
```

```python
for ch in "Kuwait":
    print(ch)
    if ch == "w":
        break
```

```text
K
u
w
```

In the first loop, the check comes **before** `print`, so `4` is never printed. In the second loop, `print` comes **before** the check, so `w` is printed first, and then the loop stops. When you trace a loop with `break`, always look at the **order** of the lines in the body.

### 3.4 The loop variable after break

After `break`, the loop variable keeps the value it had in the round where `break` ran:

```python
for n in range(1, 100):
    if n * n > 50:
        break
print("First n with n*n > 50:", n)
```

```text
First n with n*n > 50: 8
```

7 × 7 = 49 is not more than 50, but 8 × 8 = 64 is. The loop stops with `n` equal to 8, and we can use that value after the loop.

---

## 4. break in a while Loop: while True

### 4.1 The pattern

Sometimes the decision to stop can only be made in the **middle** of a round — for example, right after the user types something. For this, Python programmers often write:

```text
while True:
    # get a value
    if value means stop:
        break
    # use the value
```

`while True` has a condition that is **always** True, so on its own the loop would never end. The `break` inside gives it an exit **from the inside**.

<!-- inputs: Kuwait|Oman|quit -->
```python
while True:
    name = input("Country (or quit): ")
    if name == "quit":
        break
    print("Welcome,", name)
print("Goodbye")
```

```text
Country (or quit): Kuwait
Welcome, Kuwait
Country (or quit): Oman
Welcome, Oman
Country (or quit): quit
Goodbye
```

Step by step:

1. `while True` starts the loop.
2. The user types `Kuwait`. It is not `"quit"`, so the welcome message is printed.
3. The user types `Oman`. Same again.
4. The user types `quit`. The `if` is True, so `break` ends the loop.
5. Python continues after the loop and prints `Goodbye`.

### 4.2 Comparing with the sentinel loop you already know

In the while-loop lecture you wrote the same kind of program like this:

<!-- inputs: Kuwait|Oman|quit -->
```python
name = input("Country (or quit): ")
while name != "quit":
    print("Welcome,", name)
    name = input("Country (or quit): ")
print("Goodbye")
```

```text
Country (or quit): Kuwait
Welcome, Kuwait
Country (or quit): Oman
Welcome, Oman
Country (or quit): quit
Goodbye
```

Both versions are correct. Differences:

| | Condition loop | `while True` + `break` |
|---|---|---|
| `input` written | twice (before the loop and at the end of the body) | once |
| Where the stop check is | at the top, in the `while` line | in the middle, in an `if` |
| Risk | forgetting the second `input` → infinite loop | forgetting the `break` → infinite loop |

Choose the version that you find clearer. `while True` is very common for menus and for reading input until a stop word.

**Warning:** a `while True` loop **must** contain a `break` that can actually be reached. Otherwise it is an infinite loop. (Press **Ctrl + C** to stop a program that is stuck.)

---

## 5. The continue Statement

### 5.1 Syntax

```text
for item in sequence:
    if condition:
        continue
    # this code is skipped in this round only
# the loop then goes on with the next item
```

- `continue` is a keyword, written alone on its own line.
- When it runs, the rest of the body is skipped **for this round only**.
- Python goes back to the **top** of the loop:
  - in a `for` loop, it takes the **next item**;
  - in a `while` loop, it **checks the condition** again.
- The loop does **not** end. Only one round is cut short.

### 5.2 Example: skipping absent students

```python
marks = [80, 0, 95, 0, 70]
total = 0
count = 0
for m in marks:
    if m == 0:
        continue        # skip absent students
    total = total + m
    count = count + 1
print("Students present:", count)
print("Average:", total / count)
```

```text
Students present: 3
Average: 81.66666666666667
```

| `m` | `m == 0`? | `total` | `count` |
|---|---|---|---|
| 80 | False | 80 | 1 |
| 0 | **True** → skip | 80 | 1 |
| 95 | False | 175 | 2 |
| 0 | **True** → skip | 175 | 2 |
| 70 | False | 245 | 3 |

When `m` is 0, `continue` skips **both** update lines, so neither `total` nor `count` changes. The average is 245 / 3 = 81.67, and the absent students do not lower it.

### 5.3 continue with strings

Count the letters of a city name without counting spaces:

```python
city = "Kuwait City"
letters = 0
for ch in city:
    if ch == " ":
        continue
    letters = letters + 1
print("Letters:", letters)
print("Length:", len(city))
```

```text
Letters: 10
Length: 11
```

Print only the digits of a code:

```python
code = "KWT-2026-A"
for ch in code:
    if ch not in "0123456789":
        continue
    print(ch)
```

```text
2
0
2
6
```

Here `ch not in "0123456789"` is True for every character that is not a digit, and those rounds are skipped.

### 5.4 continue in a while loop: update first

In a `for` loop, Python moves to the next item **by itself**. In a `while` loop, **you** must change the loop variable. If the update line comes **after** `continue`, it is skipped as well — and the variable may never change.

This loop is meant to print the odd numbers from 1 to 9, but it gets stuck (do **not** run it):

```text
n = 1
while n <= 9:
    if n % 2 == 0:
        continue      # n stays 2 forever
    print(n)
    n = n + 1
```

What happens:

1. n = 1: odd, so `1` is printed and n becomes 2.
2. n = 2: even, so `continue` runs. `n = n + 1` is **skipped**.
3. The condition `2 <= 9` is still True, n is still 2, `continue` runs again… forever.

The fix is to update **before** the `continue` can happen:

```python
n = 0
while n < 9:
    n = n + 1           # update FIRST
    if n % 2 == 0:
        continue        # skip even numbers
    print(n)
```

```text
1
3
5
7
9
```

Notice that `n` now starts at 0 and the condition is `n < 9`, because `n` is increased at the **start** of each round.

---

## 6. break and continue Compared

### 6.1 The same loop, two keywords

```python
for n in range(1, 8):
    if n == 4:
        break
    print(n)
```

```text
1
2
3
```

```python
for n in range(1, 8):
    if n == 4:
        continue
    print(n)
```

```text
1
2
3
5
6
7
```

With `break`, the whole loop ends at 4. With `continue`, only the round for 4 is skipped.

### 6.2 Quick reference

| | `break` | `continue` |
|---|---|---|
| What it does | ends the loop immediately | ends the current round only |
| Where Python goes next | the first line **after** the loop | the **top** of the loop (next item / check the condition) |
| Rounds after it | none | all remaining rounds still run |
| Typical use | found what we need; user typed "quit"; too many attempts | ignore bad, empty, or unwanted values |
| Common pattern | `while True:` … `if …: break` | `if bad: continue` at the start of the body |
| Outside a loop | `SyntaxError: 'break' outside loop` | `SyntaxError: 'continue' not properly in loop` |

A helpful question: *"When this happens, do I want to **stop everything** (`break`) or **ignore just this one** (`continue`)?"*

### 6.3 continue or if?

Any `continue` can be replaced by an `if` with the **opposite** condition:

```python
for m in [80, 0, 95]:
    if m == 0:
        continue
    print("Mark:", m)
    print("Grade points:", m / 25)
```

```text
Mark: 80
Grade points: 3.2
Mark: 95
Grade points: 3.8
```

```python
for m in [80, 0, 95]:
    if m != 0:
        print("Mark:", m)
        print("Grade points:", m / 25)
```

```text
Mark: 80
Grade points: 3.2
Mark: 95
Grade points: 3.8
```

When is `continue` better?

- When the main work in the body is **long**. With `continue`, you handle the bad cases at the top ("guard checks"), and the main work stays at one level of indentation.
- When there are **several** reasons to skip an item. Each one can be a short `if … continue` at the top, instead of one long combined condition.

For a short body, a plain `if` is often clearer. Both are correct; choose the one that is easiest to read.

---

## 7. break and continue in Nested Loops

`break` and `continue` affect **only the loop they are directly inside** — the **innermost** loop. The outer loop carries on.

```python
for row in range(1, 4):
    for col in range(1, 5):
        if col == 3:
            break      # inner loop only
        print(row, col)
    print("End of row", row)
```

```text
1 1
1 2
End of row 1
2 1
2 2
End of row 2
3 1
3 2
End of row 3
```

Step by step for `row = 1`:

1. The inner loop starts with `col = 1`: print `1 1`.
2. `col = 2`: print `1 2`.
3. `col = 3`: `break` ends the **inner** loop. `col = 4` never happens.
4. Python continues after the inner loop, inside the outer loop: print `End of row 1`.
5. The outer loop goes on to `row = 2`, and everything repeats.

To see which loop a `break` belongs to, look at the **indentation**: it belongs to the nearest loop above it that it is indented under.

`continue` works the same way: in a nested loop, it skips to the next round of the **inner** loop.

---

## 8. Using a Flag with break

After a loop ends, we often need to know **why** it ended: did `break` run (we found something), or did the loop simply finish (we found nothing)? A **flag** variable answers this.

The pattern:

```text
found = False            # 1. assume "not found"
for item in sequence:
    if item matches:
        found = True     # 2. remember that it happened
        break            # 3. stop searching
if found:                # 4. decide after the loop
    ...
else:
    ...
```

Example — is 7 in the list?

```python
nums = [4, 9, 7, 2]
found = False
for x in nums:
    if x == 7:
        found = True
        break
print("Found 7?", found)
```

```text
Found 7? True
```

(For a simple "is it in the list?" question, you already know a shorter way: `7 in nums`. The flag pattern is useful when you need to do more than just check — for example, record the position, print each step, or test a condition such as "greater than 50".)

---

## 9. Worked Examples

### 9.1 Searching for a student ID

```python
ids = [2301, 2315, 2342, 2367, 2388]
target = 2342
found = False
for i in range(len(ids)):
    print("Checking", ids[i])
    if ids[i] == target:
        found = True
        break
if found:
    print("Found at position", i)
else:
    print("Not found")
```

```text
Checking 2301
Checking 2315
Checking 2342
Found at position 2
```

1. `found` starts as `False`.
2. The loop uses `range(len(ids))` because we need the **index** for the message.
3. At index 2, the ID matches. `found` becomes `True`, and `break` stops the search.
4. After `break`, `i` still holds 2.
5. The `if` after the loop uses the flag to print the right message.

Only 3 of the 5 IDs were checked. With `target = 2399`, the loop would check all five, `found` would stay `False`, and the program would print `Not found`.

### 9.2 Three password attempts

<!-- inputs: abc123|kuwait2026 -->
```python
password = "kuwait2026"
logged_in = False
for attempt in range(1, 4):
    guess = input("Password: ")
    if guess == password:
        logged_in = True
        break
    print("Wrong. Attempts left:", 3 - attempt)
if logged_in:
    print("Welcome!")
else:
    print("Account locked.")
```

```text
Password: abc123
Wrong. Attempts left: 2
Password: kuwait2026
Welcome!
```

1. `range(1, 4)` gives at most **3** rounds: 1, 2, 3.
2. Round 1: wrong guess. The `if` is False, so the "Wrong" message runs, and the loop continues.
3. Round 2: correct guess. `logged_in = True`, then `break`. The "Wrong" line is skipped, and round 3 never happens.
4. After the loop, the flag chooses `Welcome!`.

If all three guesses are wrong:

<!-- inputs: a|b|c -->
```python
password = "kuwait2026"
logged_in = False
for attempt in range(1, 4):
    guess = input("Password: ")
    if guess == password:
        logged_in = True
        break
    print("Wrong. Attempts left:", 3 - attempt)
if logged_in:
    print("Welcome!")
else:
    print("Account locked.")
```

```text
Password: a
Wrong. Attempts left: 2
Password: b
Wrong. Attempts left: 1
Password: c
Wrong. Attempts left: 0
Account locked.
```

This combines a `for` loop (a fixed maximum number of rounds) with `break` (an early exit on success).

### 9.3 A shopping total with both keywords

<!-- inputs: 2.5|-3|4|done -->
```python
total = 0
while True:
    text = input("Price (or done): ")
    if text == "done":
        break                    # stop the loop
    price = float(text)
    if price <= 0:
        print("Skipped:", price)
        continue                 # ignore this price
    total = total + price
print("Total:", total, "KD")
```

```text
Price (or done): 2.5
Price (or done): -3
Skipped: -3.0
Price (or done): 4
Price (or done): done
Total: 6.5 KD
```

| Typed | Action | `total` |
|---|---|---|
| 2.5 | add | 2.5 |
| -3 | `continue` (skip) | 2.5 |
| 4 | add | 6.5 |
| done | `break` (stop) | 6.5 |

Two important details:

- The check for `"done"` comes **before** `float(text)`. `float("done")` would cause a `ValueError`.
- `continue` ignores **one** bad price, while `break` ends the **whole** input loop.

---

## 10. Important Notes

- `break` and `continue` can only be used **inside a loop**. Inside an `if` that is not in a loop, they cause a `SyntaxError`.
- Put them inside an `if`. A `break` or `continue` at the main level of the body runs in **every** round (or in the first round, for `break`).
- In a `while` loop, make sure the loop variable is updated **before** any `continue`.
- `while True` needs a reachable `break`.
- In nested loops, they act on the **innermost** loop only.
- `continue` as the **last** line of a body does nothing useful, because the round was ending anyway.
- A loop over 8 items with `break` runs **at most** 8 rounds, and possibly fewer.

---

## 11. Common Mistakes

### Mistake 1: break not inside the if

```text
temps = [44, 47, 51]
for t in temps:
    if t > 50:
        print("Hot:", t)
    break
```

Nothing is printed. `break` is indented under `for`, not under `if`, so it runs at the end of round 1 and the loop stops before 51 is reached.

**Correct:**

```python
temps = [44, 47, 51]
for t in temps:
    if t > 50:
        print("Hot:", t)
        break
```

```text
Hot: 51
```

### Mistake 2: break or continue outside a loop

```text
age = 15
if age < 18:
    break

SyntaxError: 'break' outside loop
```

An `if` is not a loop. To "do nothing more" in an `if`, simply put the remaining code inside an `else`, or print a message.

### Mistake 3: break instead of continue

```python
# Goal: add all positive prices
total = 0
for p in [2.5, -1, 4.0, 3.5]:
    if p < 0:
        break
    total = total + p
print(total)
```

```text
2.5
```

`break` ends the loop at -1, so 4.0 and 3.5 are never added. The goal was to ignore one value, so `continue` is needed:

```python
total = 0
for p in [2.5, -1, 4.0, 3.5]:
    if p < 0:
        continue
    total = total + p
print(total)
```

```text
10.0
```

### Mistake 4: continue before the update in a while loop

See Section 5.4. The program prints `1` and then gets stuck forever. Move the update to the top of the body.

### Mistake 5: while True without break

```text
while True:
    print("Hello")
```

This never stops. Every `while True` loop needs an `if … break` that can become true.

### Mistake 6: checking the stop word after converting

```text
while True:
    price = float(input("Price (or done): "))
    if price == "done":
        break

ValueError: could not convert string to float: 'done'
```

`float` fails on `"done"` before the `if` is reached. Read the text first, check for the stop word, and only then convert (as in Worked Example 9.3).

---

## 12. Mini Practice Questions

**Q1.** In one sentence, what is the difference between `break` and `continue`?

**Q2.** What does this print?

```text
for n in range(10, 0, -2):
    if n < 5:
        break
    print(n)
```

**Q3.** What does this print?

```text
for ch in "a-b-c":
    if ch == "-":
        continue
    print(ch)
```

**Q4.** Can `continue` cause an infinite loop in a `for` loop over a list?

**Q5.** A `break` is inside the inner loop of a nested loop. Does the outer loop stop?

### Answers

1. `break` ends the whole loop; `continue` ends only the current round.
2. `10`, `8`, `6` (each on its own line). At 4, `4 < 5` is True, so the loop stops.
3. `a`, `b`, `c` (each on its own line). The dashes are skipped.
4. No. A `for` loop moves to the next item by itself. The danger is in `while` loops.
5. No. Only the inner loop stops; the outer loop continues with its next round.

---

## 13. Ask AI to Help You Understand

```text
Explain the difference between break and continue in Python loops to a beginner.
Use one short example for each and show the output. Do not give me exercises yet.
```

```text
Show me a while loop that uses continue and becomes an infinite loop.
Explain step by step why it never ends, and then show the corrected version.
```

```text
Give me four short Python loops that use break or continue, one at a time.
Ask me to predict the output, and wait for my answer before telling me if I am right.
```

```text
Explain what break does inside a nested loop in Python, using a small example
with two for loops and range(). Trace it step by step.
```

> **Remember:** Always run the code yourself to check what the AI says.

---

## 14. Summary

- `break` ends the **whole loop** immediately; Python continues with the first line after the loop.
- `continue` ends the **current round**; the loop goes on with the next item (or checks the condition again).
- Both work in `for` and `while` loops, and are almost always placed inside an `if`.
- `while True` + `break` is a common pattern for reading input until a stop word.
- In a `while` loop, update the loop variable **before** `continue`, or the loop may never end.
- In nested loops, both keywords act on the **innermost** loop only.
- A **flag** variable tells you after the loop whether `break` happened.
- Ask: stop everything (`break`) or ignore just this one (`continue`)?

---

## Basic Exercises

> Exercises 1–12 are the same as in the slides. Exercises 13–15 are extra practice.

**Exercise 1.** Predict the output.

```text
for n in range(1, 10):
    if n == 5:
        break
    print(n)
```

**Exercise 2.** Predict the output.

```text
for n in range(1, 7):
    if n % 2 == 0:
        continue
    print(n)
```

**Exercise 3.** Predict the output.

```text
for ch in "Doha":
    if ch == "h":
        break
    print(ch)
```

**Exercise 4.** `break` or `continue`?

1. Stop reading input when the user types "quit".
2. Ignore empty strings in a list of names.
3. Stop searching once the item is found.
4. Ignore negative values when adding numbers.

## Practice Exercises

**Exercise 5.** Given `temps = [41, 44, 47, 52, 49, 53]`, use a loop with `break` to print the **first** temperature above 50.

**Exercise 6.** Given `prices = [2.5, -1, 4.0, 0, 3.5]`, use `continue` to add up only the prices that are **greater than 0**, and print the total.

**Exercise 7.** This program should print 1 to 10 without 5, but it never ends. Find the error and fix it.

```text
n = 1
while n <= 10:
    if n == 5:
        continue
    print(n)
    n = n + 1
```

**Exercise 8.** Using `while True` and `break`, read words until the user types `stop`. Then print how many words were typed (not counting "stop").

**Exercise 13.** Count the **consonants** in `"Kuwait City"`: use `continue` to skip spaces and vowels (`a e i o u`, small or capital). Print the count.

**Exercise 14.** A bank account has a balance of 100 KD. The withdrawals `[30, 50, 40, 10]` are processed in order. Stop at the first withdrawal that is larger than the balance, and print `Not enough money for` followed by that amount. Finally, print the balance.

## Challenge Exercises

**Exercise 9.** Predict the output.

```text
for i in range(1, 4):
    for j in range(1, 4):
        if j == i:
            break
        print(i, j)
```

**Exercise 10.** Read a whole number greater than 1. Use a loop, a flag, and `break` to print whether it is **prime** (it has no divisor between 2 and the number − 1).

**Exercise 11.** Rewrite this loop **without** `continue`, so it prints the same output.

```text
for city in ["Kuwait", "", "Doha", ""]:
    if city == "":
        continue
    print("City:", city)
```

**Exercise 12.** Read exam marks until the user types `-1`. Skip any mark outside 0–100 (print `Invalid: …`). At the end, print the number of valid marks and their average, rounded to 1 decimal place.

**Exercise 15.** Using `while True`, go through the numbers 1, 2, 3, … Skip every multiple of 3 with `continue`. Add each number that is not skipped to a running total and print the number and the total. Stop with `break` as soon as the total is **more than 30**.

---

# Exercise Solutions

### Solution 1

When `n` is 5, the loop stops **before** `print(n)`.

```python
for n in range(1, 10):
    if n == 5:
        break
    print(n)
```

```text
1
2
3
4
```

### Solution 2

Even numbers are skipped.

```python
for n in range(1, 7):
    if n % 2 == 0:
        continue
    print(n)
```

```text
1
3
5
```

### Solution 3

The loop stops at `h`, before printing it.

```python
for ch in "Doha":
    if ch == "h":
        break
    print(ch)
```

```text
D
o
```

### Solution 4

1. `break` — stop the whole loop.
2. `continue` — skip one item.
3. `break` — no need to search further.
4. `continue` — skip one value and keep adding.

### Solution 5

```python
temps = [41, 44, 47, 52, 49, 53]
for t in temps:
    if t > 50:
        print("First above 50:", t)
        break
```

```text
First above 50: 52
```

53 is also above 50, but the loop has already stopped.

### Solution 6

```python
prices = [2.5, -1, 4.0, 0, 3.5]
total = 0
for p in prices:
    if p <= 0:
        continue
    total = total + p
print("Total:", total)
```

```text
Total: 10.0
```

The condition is `p <= 0` because "greater than 0" means 0 must also be skipped. 2.5 + 4.0 + 3.5 = 10.0.

### Solution 7

When `n` is 5, `continue` skips `n = n + 1`, so `n` stays 5 and the condition stays True forever. Move the update **before** the check:

```python
n = 0
while n < 10:
    n = n + 1
    if n == 5:
        continue
    print(n)
```

```text
1
2
3
4
6
7
8
9
10
```

`n` now starts at 0 and the condition is `n < 10`, because `n` is increased at the start of each round.

### Solution 8

<!-- inputs: Kuwait|Doha|Muscat|stop -->
```python
count = 0
while True:
    word = input("Word: ")
    if word == "stop":
        break
    count = count + 1
print("Words typed:", count)
```

```text
Word: Kuwait
Word: Doha
Word: Muscat
Word: stop
Words typed: 3
```

`count = count + 1` comes **after** the `break` check, so "stop" is not counted.

### Solution 9

```python
for i in range(1, 4):
    for j in range(1, 4):
        if j == i:
            break
        print(i, j)
```

```text
2 1
3 1
3 2
```

- `i = 1`: `j = 1` equals `i`, so the inner loop breaks at once. Nothing is printed.
- `i = 2`: prints `2 1`; at `j = 2`, break.
- `i = 3`: prints `3 1` and `3 2`; at `j = 3`, break.

The `break` stops only the inner loop; the outer loop always runs all three rounds.

### Solution 10

<!-- inputs: 21 -->
```python
n = int(input("Number: "))
is_prime = True
for d in range(2, n):
    if n % d == 0:
        is_prime = False
        print("Divisible by", d)
        break
if is_prime:
    print(n, "is prime")
else:
    print(n, "is not prime")
```

```text
Number: 21
Divisible by 3
21 is not prime
```

With the input 13:

<!-- inputs: 13 -->
```python
n = int(input("Number: "))
is_prime = True
for d in range(2, n):
    if n % d == 0:
        is_prime = False
        print("Divisible by", d)
        break
if is_prime:
    print(n, "is prime")
else:
    print(n, "is not prime")
```

```text
Number: 13
13 is prime
```

One divisor is enough to show that a number is not prime, so `break` stops the search early. If no divisor is found, the loop ends normally and the flag stays `True`.

### Solution 11

Use an `if` with the **opposite** condition (`==` becomes `!=`), and move the work inside it:

```python
for city in ["Kuwait", "", "Doha", ""]:
    if city != "":
        print("City:", city)
```

```text
City: Kuwait
City: Doha
```

### Solution 12

<!-- inputs: 85|120|70|-5|90|-1 -->
```python
total = 0
count = 0
while True:
    mark = int(input("Mark (-1 to end): "))
    if mark == -1:
        break           # end of input
    if mark < 0 or mark > 100:
        print("Invalid:", mark)
        continue        # skip this mark
    total = total + mark
    count = count + 1
print("Valid marks:", count)
print("Average:", round(total / count, 1))
```

```text
Mark (-1 to end): 85
Mark (-1 to end): 120
Invalid: 120
Mark (-1 to end): 70
Mark (-1 to end): -5
Invalid: -5
Mark (-1 to end): 90
Mark (-1 to end): -1
Valid marks: 3
Average: 81.7
```

The check for `-1` must come **first**. Otherwise -1 would be caught by the "outside 0–100" check and reported as invalid instead of ending the input. Valid marks: 85 + 70 + 90 = 245; 245 / 3 = 81.67 → 81.7.

### Solution 13

```python
city = "Kuwait City"
count = 0
for ch in city:
    if ch == " ":
        continue
    if ch in "aeiouAEIOU":
        continue
    count = count + 1
print("Consonants:", count)
```

```text
Consonants: 6
```

The consonants are K, w, t, C, t, y. Two separate `if … continue` checks at the top keep the main work (counting) simple.

### Solution 14

```python
balance = 100
for w in [30, 50, 40, 10]:
    if w > balance:
        print("Not enough money for", w)
        break
    balance = balance - w
print("Balance:", balance)
```

```text
Not enough money for 40
Balance: 20
```

100 − 30 = 70, then 70 − 50 = 20. The next withdrawal, 40, is larger than 20, so the loop stops. The withdrawal of 10 is never processed.

### Solution 15

```python
n = 0
total = 0
while True:
    n = n + 1
    if n % 3 == 0:
        continue
    total = total + n
    print(n, total)
    if total > 30:
        break
```

```text
1 1
2 3
4 7
5 12
7 19
8 27
10 37
```

`n` is updated at the **start** of the body, so `continue` cannot cause an infinite loop. The multiples 3, 6, and 9 are skipped. After adding 10, the total is 37, which is more than 30, so `break` ends the loop.

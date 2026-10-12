# CS126 – Introduction to Python

## Loops: The while Loop

**Instructor:** Dr. Fawaz Alazemi

---

## Learning Objectives

After studying these notes, you should be able to:

1. Explain how a `while` loop works and how it is different from a `for` loop.
2. Write a `while` loop with a correct condition, colon, and indented body.
3. Build a counting loop with its three parts: **initialize**, **test**, and **update**.
4. Explain what an infinite loop is, find its cause, and stop a program that is stuck in one.
5. Use a `while` loop when the number of repetitions is **not known** in advance.
6. Use `while` loops with list indexes, compound conditions (`and`, `or`), and user input.
7. Use the **sentinel** and **input validation** patterns.
8. Trace a `while` loop step by step with a trace table.
9. Choose between a `for` loop and a `while` loop for a given problem.

---

## 1. Introduction

### 1.1 What we already know: the for loop

In the last lecture you learned the `for` loop. A `for` loop visits **each item** of a sequence:

```python
for i in range(3):
    print("Hello")
```

```text
Hello
Hello
Hello
```

Before the loop starts, Python already knows how many times it will run: once for each item. This kind of repetition is called **definite repetition**, because the number of repetitions is fixed (definite) before the loop begins.

### 1.2 A different kind of problem

Now think about these problems:

- You save **150 KD** every month. **How many months** until you have at least **1000 KD**?
- A program asks for a student's grade. If the user types `120`, the program should **ask again** — and keep asking **until** the grade is between 0 and 100.
- A cashier enters prices one by one. The program keeps adding **until** the cashier types `0`.

In each case, we do **not** know in advance how many times we must repeat. The program must keep going **until something happens**. This is called **indefinite repetition**.

A `for` loop is not a natural fit here, because there is no fixed sequence to loop over. Python gives us a second loop for this: the **`while` loop**.

### 1.3 The idea in one sentence

> A `while` loop repeats its body **as long as a condition is `True`**, and stops as soon as the condition becomes `False`.

### 1.4 A real-life picture

*"While the tea is too hot, wait one minute."*

1. Check: is the tea too hot? Yes → wait one minute.
2. Check again: still too hot? Yes → wait one more minute.
3. Check again: too hot? No → stop waiting and drink.

You did not decide "wait exactly 4 minutes" at the beginning. You **checked a condition** before each repetition. This is exactly how a `while` loop works.

---

## 2. Main Concepts and Vocabulary

| Term | Meaning | Example |
|---|---|---|
| **Condition** | A logical expression that is `True` or `False` | `count <= 5` |
| **Loop body** | The indented lines that repeat | `print(count)` |
| **Iteration** | One run of the loop body | printing one number |
| **Loop control variable** | The variable that the condition checks and the body changes | `count` |
| **Infinite loop** | A loop whose condition never becomes `False` | forgetting to change `count` |
| **Sentinel** | A special value that tells the loop to stop | the word `"quit"` |
| **Input validation** | Checking user input and asking again if it is wrong | grade must be 0–100 |

---

## 3. Syntax of the while Loop

### 3.1 General form

```text
while condition:
    statement 1
    statement 2
    ...
statement after the loop
```

### 3.2 Each part explained

| Part | What it is | Rules |
|---|---|---|
| `while` | A Python keyword that starts the loop | Always lowercase |
| `condition` | Any logical expression | The same kind of expression you use in an `if` statement: comparisons (`<`, `>=`, `==`, `!=`), `and`, `or`, `not`, `in` |
| `:` | Colon at the end of the header line | Required — forgetting it is a `SyntaxError` |
| Indented body | The statements that repeat | Use 4 spaces; all body lines have the same indentation |

### 3.3 `if` versus `while`

An `if` statement and a `while` loop look very similar. The difference is what happens **after** the body runs.

```python
x = 1
if x < 4:
    print("if:", x)
    x = x + 1
```

```text
if: 1
```

```python
x = 1
while x < 4:
    print("while:", x)
    x = x + 1
```

```text
while: 1
while: 2
while: 3
```

- The `if` checks the condition **once**. Its body runs **at most one time**.
- The `while` checks the condition, runs the body, and then **goes back and checks again**. It keeps going until the condition is `False`.

You can think of a `while` loop as "an `if` that keeps repeating".

---

## 4. How a while Loop Runs, Step by Step

### 4.1 The steps

1. Python evaluates the condition.
2. If it is **`True`**: run the whole body, then go back to step 1.
3. If it is **`False`**: skip the body. The loop ends, and Python continues with the first line after the loop.

Important: the condition is checked only at the **start** of each iteration. If the condition becomes `False` in the middle of the body, the rest of the body still runs. The loop only stops at the next check.

### 4.2 A complete example with a trace table

```python
count = 1
while count <= 5:
    print(count)
    count = count + 1
print("Done")
```

```text
1
2
3
4
5
Done
```

Step-by-step walkthrough:

1. `count` is set to 1.
2. Check: `1 <= 5` is `True`. Print 1. `count` becomes 2.
3. Check: `2 <= 5` is `True`. Print 2. `count` becomes 3.
4. … the same happens for 3, 4, and 5 …
5. After printing 5, `count` becomes 6.
6. Check: `6 <= 5` is `False`. The loop ends.
7. `print("Done")` runs once.

| Check | `count` | `count <= 5` | Action |
|---|---|---|---|
| 1 | 1 | True | print 1, count → 2 |
| 2 | 2 | True | print 2, count → 3 |
| 3 | 3 | True | print 3, count → 4 |
| 4 | 4 | True | print 4, count → 5 |
| 5 | 5 | True | print 5, count → 6 |
| 6 | 6 | False | loop ends |

Notice: the condition was checked **6** times, but the body ran only **5** times. The last check is the one that stops the loop.

### 4.3 The value after the loop

After the loop, `count` is **6**, not 5. It keeps the value that made the condition `False`.

```python
count = 1
while count <= 5:
    count = count + 1
print("After the loop, count is", count)
```

```text
After the loop, count is 6
```

This is useful: the value after the loop often tells us something (for example, how many months were needed).

### 4.4 A while loop can run zero times

If the condition is `False` at the very first check, the body never runs:

```python
x = 8
while x < 5:
    print("Hello")
print("End")
```

```text
End
```

This is not an error. It is normal behavior.

### 4.5 The condition is checked at the start, not in the middle

```python
n = 10
while n > 0:
    n = n - 4
    print(n)
```

```text
6
2
-2
```

When `n` is 2, the condition `2 > 0` is `True`, so the body runs. Inside the body, `n` becomes −2 **and then** it is printed. Only at the next check does Python notice that `-2 > 0` is `False`.

---

## 5. The Three Parts of a Counting Loop

Most `while` loops that count have three parts. Learn to look for them every time you read or write a loop.

```python
count = 1             # 1. INITIALIZE
while count <= 5:     # 2. TEST
    print(count)
    count = count + 1 # 3. UPDATE
```

```text
1
2
3
4
5
```

| Part | Where | Purpose | What happens if it is missing or wrong |
|---|---|---|---|
| **Initialize** | before the loop | give the control variable a starting value | `NameError`, or the loop starts at the wrong place |
| **Test** | the `while` line | decide whether to run the body again | the loop runs too many or too few times |
| **Update** | inside the body | move the variable toward making the test `False` | infinite loop |

### 5.1 Changing the three parts

By changing the three parts, you can count in many ways:

**Count by 2:**

```python
n = 2
while n <= 10:
    print(n)
    n = n + 2
```

```text
2
4
6
8
10
```

**Count down:**

```python
n = 5
while n > 0:
    print(n)
    n = n - 1
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

When counting down, the update **subtracts** and the test usually uses `>` or `>=`.

### 5.2 `<` versus `<=`

The comparison in the test decides whether the last value is included:

| Test | Values printed when starting at 1 and adding 1 |
|---|---|
| `while i < 5:` | 1, 2, 3, 4 |
| `while i <= 5:` | 1, 2, 3, 4, 5 |

Both are correct Python. Choose the one that matches your goal. A good habit: after writing a loop, ask yourself *"What is the last value that passes the test?"*

---

## 6. Infinite Loops

### 6.1 What is an infinite loop?

An **infinite loop** is a loop whose condition **never becomes `False`**. The program never reaches the code after the loop. It may print the same thing forever, or it may look "frozen" because it is busy looping without printing anything.

```python
# This never stops — do not run it!
count = 1
while count <= 5:
    print(count)
```

Here `count` is always 1, so `count <= 5` is always `True`. The program prints `1` forever.

### 6.2 How to stop a program in an infinite loop

- In a terminal or in IDLE: press **Ctrl + C**. Python stops with a `KeyboardInterrupt` message.
- In editors such as Thonny, VS Code, or PyCharm: press the **Stop** button (usually a red square).

Do not panic — an infinite loop does not damage your computer. Stop the program, find the cause, and fix it.

### 6.3 Common causes of infinite loops

1. **No update.** The body never changes the control variable.
2. **The update is outside the loop.** It is not indented, so it runs only after the loop — which never ends.
3. **The update goes the wrong way.** For example, `n = n + 1` when the test is `n > 0`.
4. **The variable jumps over the stopping value.** For example, `while n != 10:` with `n` taking 1, 3, 5, 7, 9, 11, … It never equals 10.
5. **Input is read only once.** The loop waits for the user to type `"no"`, but never asks again.
6. **Comparing a string with a number.** `input()` returns a string, so `"1234" != 1234` is always `True`.

### 6.4 A checklist for every while loop

Before you run a `while` loop, ask:

- ✔ Is the control variable **initialized** before the loop?
- ✔ Does the body **change** something that the condition checks?
- ✔ Does that change move **toward** making the condition `False`?
- ✔ Can the variable **skip over** the stopping value? If yes, use `<` / `>` instead of `!=`.

Here is the safe version of cause 4:

```python
n = 1
while n < 10:
    n = n + 2
print(n)
```

```text
11
```

---

## 7. Repeating Until a Goal Is Reached

This is where `while` loops really shine: the program finds **how many** repetitions are needed.

### 7.1 Savings goal

```python
balance = 0
months = 0
while balance < 1000:
    balance = balance + 150
    months = months + 1
print("Months:", months)
print("Balance:", balance, "KD")
```

```text
Months: 7
Balance: 1050 KD
```

| `months` | `balance` | `balance < 1000`? |
|---|---|---|
| 0 | 0 | True |
| 1 | 150 | True |
| 2 | 300 | True |
| 3 | 450 | True |
| 4 | 600 | True |
| 5 | 750 | True |
| 6 | 900 | True |
| 7 | 1050 | False → stop |

Two variables change in each iteration:

- `balance` is the **loop control variable** — the condition checks it.
- `months` is a **counter** — it records how many times the body ran.

Notice that the balance is **1050**, not exactly 1000. The loop stops at the first value that is **not** less than 1000.

### 7.2 Growth: doubling

A video is shared by 3 people. Every day, the number of people who have seen it doubles. How many days until more than 100 people have seen it?

```python
viewers = 3
days = 0
while viewers <= 100:
    viewers = viewers * 2
    days = days + 1
print("Days:", days)
print("Viewers:", viewers)
```

```text
Days: 6
Viewers: 192
```

Trace of `viewers`: 3 → 6 → 12 → 24 → 48 → 96 → 192.

### 7.3 Decrease: using something up

A phone battery is at 100%. A game uses 15% every hour. How many full hours can you play?

```python
battery = 100
hours = 0
while battery >= 15:
    battery = battery - 15
    hours = hours + 1
print("Hours:", hours)
print("Battery left:", battery, "%")
```

```text
Hours: 6
Battery left: 10 %
```

The condition `battery >= 15` means "there is enough battery for one more full hour".

---

## 8. while Loops with Lists

### 8.1 Visiting every item with an index

You can visit every item of a list with a `while` loop and an index variable:

```python
temps = [46, 48, 44, 50]
i = 0
while i < len(temps):
    print("Day", i + 1, ":", temps[i])
    i = i + 1
```

```text
Day 1 : 46
Day 2 : 48
Day 3 : 44
Day 4 : 50
```

- **Initialize:** `i = 0`, the first index.
- **Test:** `i < len(temps)`. The last valid index is `len(temps) - 1`, which is 3.
- **Update:** `i = i + 1`, move to the next index.

If you write `i <= len(temps)`, the loop tries `temps[4]`, which does not exist. Python stops with an `IndexError: list index out of range`.

For simply visiting every item, `for t in temps:` is shorter and safer. The `while` version becomes useful when the loop should **stop early**.

### 8.2 Stopping early with a compound condition

Find the first day hotter than 50 °C:

```python
temps = [46, 48, 44, 51, 47, 52]
i = 0
while i < len(temps) and temps[i] <= 50:
    i = i + 1
if i < len(temps):
    print("First day above 50:", i + 1)
else:
    print("No day above 50")
```

```text
First day above 50: 4
```

The condition has **two parts** joined with `and`. The loop continues only while **both** are `True`:

1. `i < len(temps)` — "there are still items to check".
2. `temps[i] <= 50` — "the current day is not above 50 yet".

The loop stops as soon as **either** part is `False`. After the loop, we use an `if` to find out **which** part stopped it:

- If `i < len(temps)` is still `True`, then the loop stopped because it **found** a day above 50.
- Otherwise, it reached the end of the list without finding one.

Try the same code with a list that has no day above 50:

```python
temps = [46, 48, 44]
i = 0
while i < len(temps) and temps[i] <= 50:
    i = i + 1
if i < len(temps):
    print("First day above 50:", i + 1)
else:
    print("No day above 50")
```

```text
No day above 50
```

### 8.3 Why the order of the two parts matters (short-circuit evaluation)

When Python evaluates `A and B`, it first evaluates `A`. If `A` is `False`, the whole expression must be `False`, so Python **does not evaluate `B` at all**. This is called **short-circuit evaluation**.

In the search above, when `i` reaches `len(temps)`, the left part `i < len(temps)` is `False`, so Python never evaluates `temps[i]` — which would be an `IndexError`. If we wrote the parts the other way round:

```text
while temps[i] <= 50 and i < len(temps):
```

then `temps[i]` would be evaluated first, and the program would crash when `i` goes past the end. **Always put the index check first.**

### 8.4 Processing while a condition holds: ATM withdrawals

```python
balance = 500
requests = [100, 150, 80, 200, 50]
i = 0
while i < len(requests) and requests[i] <= balance:
    balance = balance - requests[i]
    print("Paid", requests[i], "KD - balance", balance)
    i = i + 1
print("Requests completed:", i)
```

```text
Paid 100 KD - balance 400
Paid 150 KD - balance 250
Paid 80 KD - balance 170
Requests completed: 3
```

The fourth request (200 KD) is larger than the balance (170 KD), so the loop stops there. The last request (50 KD) is never checked, even though there would be enough money for it. The loop stops at the **first** request that cannot be paid, because the requests must be handled in order.

---

## 9. while Loops with User Input

`input()` waits for the user to type something and press Enter, and it always returns a **string**. Use `int()` or `float()` when you need a number.

The examples below show a **sample run**: the text after each prompt is what the user typed.

### 9.1 The sentinel pattern

A **sentinel** is a special value that means "stop". The user types it when there is no more data.

<!-- inputs: Sara|Fahad|quit -->
```python
name = input("Enter a name (or quit): ")
while name != "quit":
    print("Welcome,", name)
    name = input("Enter a name (or quit): ")
print("Goodbye")
```

```text
Enter a name (or quit): Sara
Welcome, Sara
Enter a name (or quit): Fahad
Welcome, Fahad
Enter a name (or quit): quit
Goodbye
```

The structure is always the same:

1. Read the **first** value **before** the loop (this is the initialize step).
2. The condition checks whether it is the sentinel (this is the test).
3. Process the value.
4. Read the **next** value as the **last line** of the body (this is the update).

Why read twice? If we read only inside the loop, the condition would have nothing to check the first time. If we read only before the loop, the value would never change, and the loop would be infinite.

Note: the sentinel check is **case-sensitive**. Typing `Quit` or `QUIT` does not stop this loop, because `"Quit" != "quit"` is `True`.

### 9.2 Adding up input until a sentinel

A cashier enters prices. Typing `0` means "finished".

<!-- inputs: 2.5|1.25|0.75|0 -->
```python
total = 0
items = 0
price = float(input("Price (0 to finish): "))
while price != 0:
    total = total + price
    items = items + 1
    price = float(input("Price (0 to finish): "))
print("Items:", items)
print("Total:", total, "KD")
```

```text
Price (0 to finish): 2.5
Price (0 to finish): 1.25
Price (0 to finish): 0.75
Price (0 to finish): 0
Items: 3
Total: 4.5 KD
```

This loop combines the **sentinel** pattern with an **accumulator** (`total`) and a **counter** (`items`). The sentinel value 0 is **not** added to the total and **not** counted, because the loop stops before processing it.

### 9.3 Input validation

**Input validation** means checking that the user's input is acceptable and asking again if it is not.

<!-- inputs: 120|-5|85 -->
```python
grade = int(input("Enter grade (0-100): "))
while grade < 0 or grade > 100:
    print("Invalid grade. Try again.")
    grade = int(input("Enter grade (0-100): "))
print("Saved:", grade)
```

```text
Enter grade (0-100): 120
Invalid grade. Try again.
Enter grade (0-100): -5
Invalid grade. Try again.
Enter grade (0-100): 85
Saved: 85
```

Tips for writing the condition:

- The condition describes the **bad** input — the reason to **keep asking**.
- A valid grade is `grade >= 0 and grade <= 100`. The bad case is the opposite: `grade < 0 or grade > 100`.
- You can also write `while not (grade >= 0 and grade <= 100):`. Both are correct.

If the user types a valid grade the first time, the body runs **zero** times and the grade is saved immediately.

Another validation example — choosing from a menu:

<!-- inputs: 5|x|2 -->
```python
choice = input("Choose 1, 2, or 3: ")
while choice not in ["1", "2", "3"]:
    print("Please type 1, 2, or 3.")
    choice = input("Choose 1, 2, or 3: ")
print("You chose option", choice)
```

```text
Choose 1, 2, or 3: 5
Please type 1, 2, or 3.
Choose 1, 2, or 3: x
Please type 1, 2, or 3.
Choose 1, 2, or 3: 2
You chose option 2
```

Here we keep the choice as a **string** and compare it with a list of strings. This also works when the user types a letter, which `int()` could not convert.

### 9.4 A guessing game

<!-- inputs: 4|9|7 -->
```python
secret = 7
guess = int(input("Guess (1-10): "))
tries = 1
while guess != secret:
    if guess < secret:
        print("Too low")
    else:
        print("Too high")
    guess = int(input("Guess (1-10): "))
    tries = tries + 1
print("Correct! Tries:", tries)
```

```text
Guess (1-10): 4
Too low
Guess (1-10): 9
Too high
Guess (1-10): 7
Correct! Tries: 3
```

`tries` starts at 1 because the first guess is read before the loop. Each new guess inside the loop adds 1.

---

## 10. Working with the Digits of a Number

Two arithmetic operators are very useful with `while` loops:

- `n % 10` gives the **last digit** of `n` (the remainder after dividing by 10). Example: `2026 % 10` is `6`.
- `n // 10` **removes** the last digit (integer division). Example: `2026 // 10` is `202`.

### 10.1 Counting digits

```python
n = 2026
digits = 0
while n > 0:
    n = n // 10
    digits = digits + 1
print("Digits:", digits)
```

```text
Digits: 4
```

| `n` before | `n > 0`? | `n` after | `digits` |
|---|---|---|---|
| 2026 | True | 202 | 1 |
| 202 | True | 20 | 2 |
| 20 | True | 2 | 3 |
| 2 | True | 0 | 4 |
| 0 | False | — | loop ends |

The number of iterations depends on how big the number is — a perfect job for `while`.

(Note: this program prints `Digits: 0` for `n = 0`, because the body never runs. Handling 0 correctly would need an extra `if`.)

### 10.2 Reversing a number

```python
n = 1234
reverse = 0
while n > 0:
    last = n % 10
    reverse = reverse * 10 + last
    n = n // 10
print(reverse)
```

```text
4321
```

| `n` | `last` | `reverse` |
|---|---|---|
| 1234 | 4 | 4 |
| 123 | 3 | 43 |
| 12 | 2 | 432 |
| 1 | 1 | 4321 |

---

## 11. for or while?

### 11.1 Comparison

| | `for` loop | `while` loop |
|---|---|---|
| Repeats | once for each item in a sequence | as long as a condition is `True` |
| Best when | you know the items or the count | you repeat **until** something happens |
| Update | automatic | written by **you** |
| Can be infinite? | not when looping over a list or range | yes, if the condition never becomes `False` |
| Typical uses | process every item, count with `range()` | goals, searching with early stop, input loops, validation |

### 11.2 Converting a for loop into a while loop

Every `for` loop over a `range()` can be rewritten as a `while` loop using the three parts:

```python
for i in range(10, 0, -2):
    print(i)
```

```text
10
8
6
4
2
```

```python
i = 10          # range start
while i > 0:    # range stop (counting down → use >)
    print(i)
    i = i - 2   # range step
```

```text
10
8
6
4
2
```

| `range(start, stop, step)` | `while` version |
|---|---|
| start | initialize: `i = start` |
| stop (counting up) | test: `while i < stop:` |
| stop (counting down) | test: `while i > stop:` |
| step | update: `i = i + step` |

### 11.3 A simple rule

> If you can say **"for each …"** or **"… times"**, use `for`.
> If you can say **"until …"** or **"as long as …"**, use `while`.

---

## 12. Important Notes

- The condition is checked **before** each iteration, never in the middle of the body.
- The body can run **zero** times.
- Every counting `while` loop needs **initialize**, **test**, and **update**. The update must be **inside** the body (indented).
- Prefer `<`, `<=`, `>`, `>=` over `!=` when the variable might **skip** the stopping value.
- With lists, test the index **first**: `i < len(lst) and lst[i] ...`.
- `input()` returns a **string**. Convert it with `int()` or `float()` before comparing it with numbers.
- With input loops, read **before** the loop and **again** at the end of the body.
- If your program seems frozen, it may be in an infinite loop. Stop it with **Ctrl + C** or the Stop button.

---

## 13. Common Mistakes

### Mistake 1: Forgetting the colon

**Incorrect**

```python
# Incorrect
count = 1
while count <= 3
    print(count)
    count = count + 1
```

**Why?** The `while` header must end with `:`. Python gives `SyntaxError: expected ':'`.

**Correct**

```python
count = 1
while count <= 3:
    print(count)
    count = count + 1
```

```text
1
2
3
```

### Mistake 2: Forgetting the update

**Incorrect**

```text
count = 1
while count <= 3:
    print(count)
```

**Why?** `count` never changes, so `count <= 3` is always `True`. The program prints `1` forever.

**Correct:** add `count = count + 1` inside the body (see Mistake 1).

### Mistake 3: Update outside the loop

**Incorrect**

```text
count = 1
while count <= 3:
    print(count)
count = count + 1
```

**Why?** The update is not indented, so it is **after** the loop, not inside it. The loop never ends, so the update never runs. Infinite loop.

**Correct:** indent the update to the same level as `print(count)`.

### Mistake 4: Off-by-one in the condition

**Incorrect**

```python
# goal: print 1 to 5
i = 1
while i < 5:
    print(i)
    i = i + 1
```

```text
1
2
3
4
```

**Why?** `5 < 5` is `False`, so 5 is never printed.

**Correct**

```python
i = 1
while i <= 5:
    print(i)
    i = i + 1
```

```text
1
2
3
4
5
```

### Mistake 5: Update moves the wrong way

**Incorrect**

```text
n = 10
while n > 0:
    print(n)
    n = n + 1
```

**Why?** `n` becomes 11, 12, 13, … and is always greater than 0. Infinite loop.

**Correct**

```python
n = 10
while n > 0:
    print(n)
    n = n - 1
```

### Mistake 6: Using `!=` when the value can be skipped

**Incorrect**

```text
n = 1
while n != 10:
    n = n + 2
```

**Why?** `n` takes the values 1, 3, 5, 7, 9, 11, … and is never equal to 10. Infinite loop.

**Correct**

```python
n = 1
while n < 10:
    n = n + 2
print(n)
```

```text
11
```

### Mistake 7: Reading input only once

**Incorrect**

```text
answer = input("Continue? ")
while answer != "no":
    print("Working...")
```

**Why?** If the user types `yes`, the answer never changes, so the loop prints `Working...` forever.

**Correct**

<!-- inputs: yes|yes|no -->
```python
answer = input("Continue? ")
while answer != "no":
    print("Working...")
    answer = input("Continue? ")
```

```text
Continue? yes
Working...
Continue? yes
Working...
Continue? no
```

### Mistake 8: Comparing a string with a number

**Incorrect**

```text
pin = input("PIN: ")
while pin != 1234:
    pin = input("PIN: ")
```

**Why?** `input()` returns the string `"1234"`, and a string is never equal to the number `1234`. The condition is always `True` — even when the user types the correct PIN.

**Correct** (convert to a number, or compare with a string):

<!-- inputs: 1111|1234 -->
```python
pin = int(input("PIN: "))
while pin != 1234:
    pin = int(input("PIN: "))
print("Access granted")
```

```text
PIN: 1111
PIN: 1234
Access granted
```

### Mistake 9: Checking the list item before the index

**Incorrect**

```python
# Incorrect
temps = [46, 48, 44]
i = 0
while temps[i] <= 50 and i < len(temps):
    i = i + 1
```

**Why?** When `i` becomes 3, Python evaluates `temps[3]` first and stops with an `IndexError`.

**Correct**

```python
temps = [46, 48, 44]
i = 0
while i < len(temps) and temps[i] <= 50:
    i = i + 1
print(i)
```

```text
3
```

---

## 14. Mini Practice Questions

Try these before looking at the answers at the end of this section.

**Q1.** How many times does the body run?

```python
k = 0
while k < 12:
    k = k + 4
```

**Q2.** What does this print?

```python
k = 1
while k < 100:
    k = k * 2
print(k)
```

**Q3.** Which part (initialize, test, or update) is missing? What happens when you run it?

```text
total = 0
while total < 50:
    print(total)
```

**Q4.** Write the condition for a loop that keeps asking for an age while the age is **less than 18 or greater than 60**.

**Q5.** True or false: the body of a `while` loop always runs at least once.

**Q6.** What does this print?

```python
word = "Kuwait"
i = 0
while i < len(word) and word[i] != "a":
    i = i + 1
print(i)
```

### Answers to Mini Practice

1. **3 times** — `k` becomes 4, 8, 12. Then `12 < 12` is `False`.
2. **`128`** — `k` takes 1, 2, 4, 8, 16, 32, 64, 128. Then `128 < 100` is `False`.
3. The **update** is missing. `total` stays 0, so the loop prints `0` forever (infinite loop).
4. `while age < 18 or age > 60:`
5. **False** — if the condition is `False` at the first check, the body runs zero times.
6. **`3`** — it stops at the first `"a"`, which is at index 3 (`K`=0, `u`=1, `w`=2, `a`=3).

---

## 15. Ask AI to Help You Understand

Use an AI assistant as a private tutor. Ask it to explain and to give hints — not just answers.

```text
Explain the Python while loop to me using a savings example in Kuwaiti Dinar.
Show a trace table for every iteration. Do not give me exercises yet.
```

```text
I keep writing infinite while loops. Give me 4 short buggy examples,
one at a time, and let me find the problem before you explain it.
```

```text
Explain the difference between a for loop and a while loop.
Give me 5 everyday problems and ask me which loop fits each one.
Wait for my answers before telling me if I am right.
```

```text
Explain why "i < len(lst) and lst[i] > 0" is safe but
"lst[i] > 0 and i < len(lst)" can crash. Use a list of 3 numbers.
```

```text
Here is my while loop and the output I expected. Do not fix it for me.
Give me one hint at a time to help me find the mistake myself.
[paste your code here]
```

> **Remember:** Always run the code yourself. AI can make mistakes, and running the code is the only way to be sure.

---

## 16. Summary

- A **`while` loop** repeats its body **as long as** its condition is `True`. It is used for **indefinite repetition** — when we do not know the number of repetitions in advance.
- Syntax: `while condition:` followed by an indented body.
- The condition is checked **before every iteration**. The body may run **zero** times.
- Counting loops need three parts: **initialize** (before), **test** (the condition), **update** (inside the body).
- If the condition never becomes `False`, the program is stuck in an **infinite loop**. Stop it with **Ctrl + C**.
- Common patterns:
  - **Repeat until a goal** (savings, growth, using something up).
  - **Search with early stop** using `i < len(lst) and ...` — index check first.
  - **Sentinel loop:** read before the loop, read again at the end of the body.
  - **Input validation:** the condition describes the bad input; keep asking while it is bad.
  - **Digit processing** with `% 10` and `// 10`.
- Use **`for`** for "for each …" or "… times". Use **`while`** for "until …" or "as long as …".

---

## Basic Exercises

> Exercises 1–12 are the same as in the slides. Exercises 13–16 are extra practice.

**Exercise 1.** Predict the output.

```python
x = 1
while x < 20:
    print(x)
    x = x * 3
```

**Exercise 2.** Predict the output.

```python
n = 10
while n > 0:
    n = n - 4
    print(n)
```

**Exercise 3.** Find and fix the **two** errors. (Hint: one error stops the program from running; the other makes it run forever.)

```text
count = 1
while count <= 3
    print(count)
```

**Exercise 4.** How many times does `"Hi"` print? Explain.

```python
i = 5
while i < 5:
    print("Hi")
    i = i + 1
```

**Exercise 13.** This program should count down from 5 to 1, but it never stops. Explain why and fix it.

```text
n = 5
while n > 0:
    print(n)
n = n - 1
```

## Practice Exercises

**Exercise 5.** Use a `while` loop to print the even numbers from 2 to 10.

**Exercise 6.** A student has **200 KD** and saves **75 KD** every month. Use a `while` loop to find how many months until the balance is **at least 650 KD**. Print the number of months and the final balance.

**Exercise 7.** Complete the code so it prints the total of the list (`20`).

```text
prices = [2, 4, 6, 8]
total = 0
i = ___
while i ___ len(prices):
    total = total + ___
    ___
print(total)
```

**Exercise 8.** Rewrite this `for` loop as a `while` loop with the same output.

```python
for i in range(10, 0, -2):
    print(i)
```

**Exercise 14.** A car's petrol tank has **50 litres**. Each trip uses **7 litres**. Use a `while` loop to count how many full trips the car can make. Print the number of trips and the litres left.

## Challenge Exercises

**Exercise 9.** A bacteria sample starts with **10** cells and **doubles** every hour. Use a `while` loop to find how many hours until there are **more than 1000** cells. Print the hours and the final number of cells.

**Exercise 10.** Write a program that finds the **sum of the digits** of `n = 4083`. The answer should be 15. (Hint: `n % 10` gives the last digit.)

**Exercise 11.** Predict the output. Make a trace table for `i` and `total`.

```python
i = 0
total = 0
while i < 10 and total < 8:
    total = total + i
    i = i + 1
print(i, total)
```

**Exercise 12.** Write a program that keeps asking the user for a password until it has **at least 8 characters**. Print `Too short` for each password that is too short. When a good password is entered, print `Password accepted`.

**Exercise 15.** Write a guessing game where the secret number is **7** and the user has **at most 3 tries**. The loop must stop when the guess is correct **or** when 3 tries have been used. After the loop, print `You win!` if the last guess was correct, otherwise print `No more tries. The number was 7`.

**Exercise 16.** A ball is dropped from a height of **32 metres**. After each bounce it reaches **half** of its previous height. Use a `while` loop to count how many bounces it takes until the height is **less than 1 metre**. Print the number of bounces and the final height.

---

# Exercise Solutions

### Solution 1

`x` is multiplied by 3 in each iteration: 1, 3, 9. The next value, 27, makes `x < 20` `False`.

```text
1
3
9
```

### Solution 2

The update happens **before** the `print`, so the new value is printed. When `n` is 2, the condition is still `True`, so `n` becomes −2 and is printed. Then `-2 > 0` is `False`.

```text
6
2
-2
```

### Solution 3

Error 1: the colon is missing after the condition (`SyntaxError`).
Error 2: there is no update, so `count` would stay 1 forever (infinite loop).

```python
count = 1
while count <= 3:
    print(count)
    count = count + 1
```

```text
1
2
3
```

### Solution 4

**Zero times.** `i` starts at 5, and `5 < 5` is `False` at the first check, so the body never runs. Nothing is printed.

### Solution 5

```python
n = 2
while n <= 10:
    print(n)
    n = n + 2
```

```text
2
4
6
8
10
```

Using `<=` makes sure 10 is included.

### Solution 6

```python
balance = 200
months = 0
while balance < 650:
    balance = balance + 75
    months = months + 1
print("Months:", months)
print("Balance:", balance, "KD")
```

```text
Months: 6
Balance: 650 KD
```

Balance: 200 → 275 → 350 → 425 → 500 → 575 → 650. "At least 650" means the loop continues while the balance is **less than** 650.

### Solution 7

```python
prices = [2, 4, 6, 8]
total = 0
i = 0
while i < len(prices):
    total = total + prices[i]
    i = i + 1
print(total)
```

```text
20
```

The blanks are: `0`, `<`, `prices[i]`, and `i = i + 1`.

### Solution 8

`range(10, 0, -2)` starts at 10, stops before 0, and steps by −2.

```python
i = 10
while i > 0:
    print(i)
    i = i - 2
```

```text
10
8
6
4
2
```

### Solution 9

"More than 1000" means the loop continues while `cells <= 1000`.

```python
cells = 10
hours = 0
while cells <= 1000:
    cells = cells * 2
    hours = hours + 1
print("Hours:", hours)
print("Cells:", cells)
```

```text
Hours: 7
Cells: 1280
```

Cells: 10 → 20 → 40 → 80 → 160 → 320 → 640 → 1280.

### Solution 10

In each iteration, add the last digit to the total, then remove it.

```python
n = 4083
total = 0
while n > 0:
    total = total + n % 10
    n = n // 10
print("Sum of digits:", total)
```

```text
Sum of digits: 15
```

| `n` | `n % 10` | `total` |
|---|---|---|
| 4083 | 3 | 3 |
| 408 | 8 | 11 |
| 40 | 0 | 11 |
| 4 | 4 | 15 |

### Solution 11

| `i` before | `total < 8`? | `total` after | `i` after |
|---|---|---|---|
| 0 | True (0) | 0 | 1 |
| 1 | True (0) | 1 | 2 |
| 2 | True (1) | 3 | 3 |
| 3 | True (3) | 6 | 4 |
| 4 | True (6) | 10 | 5 |
| 5 | False (10) | — | — |

The loop stops because `total < 8` becomes `False` (while `i < 10` is still `True`).

```text
5 10
```

### Solution 12

<!-- inputs: abc|kuwait2026 -->
```python
password = input("Password: ")
while len(password) < 8:
    print("Too short")
    password = input("Password: ")
print("Password accepted")
```

```text
Password: abc
Too short
Password: kuwait2026
Password accepted
```

This is the input validation pattern: the condition `len(password) < 8` describes the bad case.

### Solution 13

The update `n = n - 1` is **not indented**, so it is outside the loop. Inside the loop, `n` stays 5 forever, so the program prints 5 again and again. Fix: indent the update.

```python
n = 5
while n > 0:
    print(n)
    n = n - 1
```

```text
5
4
3
2
1
```

### Solution 14

The loop continues while there is enough petrol for one more full trip.

```python
tank = 50
trips = 0
while tank >= 7:
    tank = tank - 7
    trips = trips + 1
print("Trips:", trips)
print("Left:", tank, "litres")
```

```text
Trips: 7
Left: 1 litres
```

### Solution 15

The compound condition stops the loop for **either** reason. After the loop, an `if` checks which reason it was.

<!-- inputs: 3|9|5 -->
```python
secret = 7
guess = int(input("Guess (1-10): "))
tries = 1
while guess != secret and tries < 3:
    guess = int(input("Guess again: "))
    tries = tries + 1
if guess == secret:
    print("You win!")
else:
    print("No more tries. The number was", secret)
```

```text
Guess (1-10): 3
Guess again: 9
Guess again: 5
No more tries. The number was 7
```

Another sample run, where the user wins on the second try:

<!-- inputs: 4|7 -->
```python
secret = 7
guess = int(input("Guess (1-10): "))
tries = 1
while guess != secret and tries < 3:
    guess = int(input("Guess again: "))
    tries = tries + 1
if guess == secret:
    print("You win!")
else:
    print("No more tries. The number was", secret)
```

```text
Guess (1-10): 4
Guess again: 7
You win!
```

### Solution 16

```python
height = 32
bounces = 0
while height >= 1:
    height = height / 2
    bounces = bounces + 1
print("Bounces:", bounces)
print("Height:", height, "m")
```

```text
Bounces: 6
Height: 0.5 m
```

Height: 32 → 16.0 → 8.0 → 4.0 → 2.0 → 1.0 → 0.5. When the height is exactly 1.0, `1.0 >= 1` is still `True`, so the ball bounces once more.

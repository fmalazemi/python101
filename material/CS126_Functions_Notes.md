# CS126 – Introduction to Python

## Functions: Defining Functions and Returning Values

**Instructor:** Dr. Fawaz Alazemi

---

## Learning Objectives

After studying these notes, you should be able to:

1. Explain what a **function** is and why programs use functions.
2. **Define** a function with `def`, and **call** it.
3. Describe the order in which Python runs a program that defines and calls functions.
4. Use **parameters** and **arguments** to give data to a function.
5. Use `return` to send a value back, and use the returned value in other code.
6. Write **void functions** and explain the value `None`.
7. **Return several values** from one function and unpack them.
8. Explain the difference between `print` and `return`, and choose the right one.

---

## 1. Introduction

### 1.1 You already use functions

Since the first lectures, you have been **using** functions that Python provides:

```python
print(len("Kuwait"))
print(max(4, 9, 2))
print(round(3.756, 1))
```

```text
6
9
3.8
```

Each of these is a **built-in function**: a piece of code with a name. You give it values in brackets, it does its job, and (for most of them) it gives a result back. You do not need to know how `max` finds the largest number — you only need to know its **name**, what to **give** it, and what it **gives back**.

In this lecture you will learn to write **your own** functions that work in exactly the same way.

### 1.2 Why write functions?

Look at this program, which applies a 10% discount to three prices:

```python
price1 = 20
print(price1 - price1 * 10 / 100)
price2 = 35
print(price2 - price2 * 10 / 100)
price3 = 8
print(price3 - price3 * 10 / 100)
```

```text
18.0
31.5
7.2
```

The same calculation is written **three times**. If the discount changes to 15%, we must change three lines — and if we forget one, the program gives a wrong answer. With a function, we write the calculation **once**:

```python
def after_discount(price):
    return price - price * 10 / 100

print(after_discount(20))
print(after_discount(35))
print(after_discount(8))
```

```text
18.0
31.5
7.2
```

Functions help us to:

- **avoid repeating** the same code;
- **change** a calculation in one place only;
- give a **meaningful name** to a piece of work (`after_discount` explains itself);
- **split** a big program into small parts that are easier to write, read, and test.

---

## 2. Vocabulary

| Term | Meaning |
|---|---|
| **Function** | A named block of code that does one job |
| **Define** | Create a function with `def` (teach Python the new name) |
| **Call** | Run a function by writing its name and brackets: `greet("Ali")` |
| **Body** | The indented lines inside the function |
| **Parameter** | A variable name in the `def` line that receives a value |
| **Argument** | The actual value given in a call |
| **`return`** | A keyword that sends a value back to the call and ends the function |
| **Return value** | The value a function gives back |
| **Void function** | A function with no return value; it gives back `None` |
| **`None`** | A special Python value that means "no value" |
| **Unpacking** | Putting the items of a tuple into several variables: `a, b = (1, 2)` |

---

## 3. Defining and Calling a Function

### 3.1 Syntax

```text
def function_name(parameters):
    statement 1
    statement 2
    return value        # optional
```

Each part explained:

| Part | Meaning |
|---|---|
| `def` | a keyword that means "define a function" |
| `function_name` | the name you choose; same rules as variable names (letters, digits, underscores; cannot start with a digit) |
| `( )` | brackets — always needed, even when there are no parameters |
| `parameters` | names for the input values, separated by commas (can be empty) |
| `:` | a colon ends the first line |
| body | the indented code of the function (4 spaces), just like the body of an `if` |
| `return value` | optional; sends a result back |

Good function names describe the **job**, using small letters and underscores: `after_discount`, `rectangle_area`, `show_menu`, `letter_grade`. A function name often starts with a verb, because a function **does** something.

### 3.2 Defining does not run the code

```python
def say_welcome():
    print("Welcome to CS126!")
```

This program prints **nothing**. The `def` block only **teaches** Python a new name and remembers the body for later. The body runs only when the function is **called**.

### 3.3 Calling a function

To call a function, write its name followed by brackets:

```python
def say_welcome():
    print("Welcome to CS126!")

say_welcome()     # call 1
say_welcome()     # call 2
```

```text
Welcome to CS126!
Welcome to CS126!
```

Each call runs the **whole body** once. The brackets are essential: `say_welcome` without brackets only names the function; it does not run it.

### 3.4 The order in which Python runs the code

```python
def show_line():           # 1
    print("----------")  # 2

print("Report")          # 4
show_line()              # 5
print("Total: 50 KD")    # 6
show_line()              # 7
```

```text
Report
----------
Total: 50 KD
----------
```

| Step | Line | What happens |
|---|---|---|
| 1 | 1 | Python learns the name `show_line` and skips its body |
| 2 | 4 | prints `Report` |
| 3 | 5 | call: Python **jumps** into the function |
| 4 | 2 | prints the dashes |
| 5 | — | the body is finished: Python **jumps back** to just after line 5 |
| 6 | 6 | prints the total |
| 7 | 7 | call again: jump to line 2, print the dashes, jump back |

A function call is like a short trip: Python **leaves** the main program, runs the function body, and **returns** to exactly where it left.

Because Python reads from top to bottom, a function must be **defined before it is called**. Usually, all `def` blocks are written at the top of the file, and the main program comes after them.

---

## 4. Parameters and Arguments

### 4.1 One parameter

A function becomes much more useful when we can give it data:

```python
def greet(name):
    print("Hello,", name)

greet("Sara")
greet("Ahmad")
```

```text
Hello, Sara
Hello, Ahmad
```

- `name` is a **parameter**: the variable name written in the `def` line.
- `"Sara"` and `"Ahmad"` are **arguments**: the actual values given in each call.

When a function is called, each argument is **copied into** its parameter, and then the body runs. In the first call, `name` holds `"Sara"`; in the second call, it holds `"Ahmad"`.

A simple way to remember: the **p**arameter is the **p**lace (the empty box); the **a**rgument is the **a**ctual value put into it.

### 4.2 Several parameters

Parameters are separated by commas, and so are arguments:

```python
def show_item(item, price):
    print(item, "costs", price, "KD")

show_item("Coffee", 1.25)
show_item(0.75, "Water")   # wrong order!
```

```text
Coffee costs 1.25 KD
0.75 costs Water KD
```

Arguments are matched to parameters **by position**: the first argument goes into the first parameter, the second into the second, and so on. Python does not understand the meaning of your values, so if you give them in the wrong order, you get a wrong result without any error.

### 4.3 The number of arguments must match

If you give too few or too many arguments, Python stops with a `TypeError`:

```text
show_item("Tea")

TypeError: show_item() missing 1 required positional argument: 'price'
```

```text
show_item("Tea", 0.5, 3)

TypeError: show_item() takes 2 positional arguments but 3 were given
```

### 4.4 Arguments can be any expression

An argument can be a value, a variable, or a calculation. Python works out its value **before** calling the function:

```python
def show_item(item, price):
    print(item, "costs", price, "KD")

drink = "Juice"
show_item(drink, 0.25 * 2)
```

```text
Juice costs 0.5 KD
```

---

## 5. Returning a Value

### 5.1 The return statement

```python
def square(n):
    return n * n

result = square(5)
print(result)
print(square(3) + square(4))
```

```text
25
25
```

`return` does two things:

1. It **sends a value back** to the place where the function was called.
2. It **ends** the function immediately.

How `result = square(5)` works, step by step:

1. Python calls `square`, and the parameter `n` gets the value 5.
2. The body calculates `n * n`, which is 25.
3. `return` sends 25 back.
4. The call `square(5)` is **replaced** by 25, so the line becomes `result = 25`.

In the same way, `square(3) + square(4)` becomes `9 + 16`, which is 25.

### 5.2 Using a returned value

A returned value is a normal value, so it can be used **anywhere** a value can be used:

```python
def rectangle_area(width, height):
    return width * height

a = rectangle_area(4, 3)          # store
print(a)
print(rectangle_area(2, 5))       # print
total = a + rectangle_area(1, 6)  # calculate
print(total)
if rectangle_area(10, 10) > 50:   # compare
    print("Big room")
```

```text
12
10
18
Big room
```

It can also be given as an argument to another function:

```python
def rectangle_area(width, height):
    return width * height

print(max(rectangle_area(4, 3), rectangle_area(2, 7)))
```

```text
14
```

### 5.3 return ends the function

A function can contain **several** `return` statements — for example, one in each branch of an `if`. In each call, only **one** of them runs:

```python
def pass_or_fail(mark):
    if mark >= 60:
        return "Pass"
    else:
        return "Fail"

print(pass_or_fail(75))
print(pass_or_fail(42))
```

```text
Pass
Fail
```

Because `return` ends the function, any line after it (in the same block) **never runs**:

```python
def bigger(a, b):
    if a > b:
        return a
    return b
    print("This never runs")

print(bigger(7, 12))
```

```text
12
```

Step by step for `bigger(7, 12)`:

1. `a` = 7, `b` = 12.
2. `7 > 12` is False, so `return a` is skipped.
3. `return b` sends back 12 and **ends** the function.
4. The `print` line is never reached.

Notice that `return b` does not need an `else`: if `return a` had run, the function would already have ended.

### 5.4 A function can call another function

```python
def square(n):
    return n * n

def sum_of_squares(a, b):
    return square(a) + square(b)

print(sum_of_squares(3, 4))
```

```text
25
```

`sum_of_squares` calls `square` twice. Small functions that each do one job can be combined to build bigger ones.

---

## 6. print versus return

This is the most important difference in this lecture, and the most common source of mistakes.

```python
def add_print(a, b):
    print(a + b)

x = add_print(2, 3)
print("x is", x)
```

```text
5
x is None
```

```python
def add_return(a, b):
    return a + b

x = add_return(2, 3)
print("x is", x)
```

```text
x is 5
```

| | `print(...)` inside a function | `return ...` |
|---|---|---|
| Who receives the value | the **person** looking at the screen | the **program**, at the place of the call |
| Can the program use the value later? | No | Yes |
| What the call gives back | `None` (unless there is also a return) | the returned value |
| Does it end the function? | No | Yes |

**print** = show to the person. **return** = give to the program.

A good habit: functions that **calculate** something should **return** the result, and let the caller decide whether to print it, store it, or use it in another calculation.

---

## 7. Void Functions and None

### 7.1 What is a void function?

A **void function** does a job — usually printing something — but does **not** return a value.

```python
def print_receipt(item, price):
    print("Item:", item)
    print("Price:", price, "KD")
    print("Thank you!")

print_receipt("Shawarma", 0.75)
```

```text
Item: Shawarma
Price: 0.75 KD
Thank you!
```

Void functions are useful for **actions**: showing a menu, printing a receipt or report, displaying a message.

### 7.2 None

Even a void function gives something back: the special value **`None`**, which means "no value".

```python
def print_receipt(item, price):
    print("Item:", item)
    print("Price:", price, "KD")
    print("Thank you!")

value = print_receipt("Juice", 0.5)
print(value)
print(type(value))
```

```text
Item: Juice
Price: 0.5 KD
Thank you!
None
<class 'NoneType'>
```

So:

- Call a void function **on its own line**. Storing its result is not useful.
- If you see `None` printed unexpectedly, or an error mentioning `'NoneType'`, check whether a function **forgot to return** its result.

`print` itself is a void function:

```python
x = print("Hi")
print(x)
```

```text
Hi
None
```

### 7.3 return with no value

A `return` with nothing after it ends the function and gives back `None`. It can be used to leave a void function early:

```python
def check_age(age):
    if age < 0:
        print("Invalid age")
        return
    print("Age accepted:", age)

check_age(-3)
check_age(20)
```

```text
Invalid age
Age accepted: 20
```

---

## 8. Returning Several Values

### 8.1 How it works

To return more than one value, write them after `return`, separated by **commas**:

```python
def split_time(minutes):
    hours = minutes // 60
    mins = minutes % 60
    return hours, mins

h, m = split_time(135)
print(h, "hours and", m, "minutes")

t = split_time(90)
print(t, type(t))
```

```text
2 hours and 15 minutes
(1, 30) <class 'tuple'>
```

What really happens: Python puts the values in a **tuple** and returns that **one** tuple. (Remember from the tuples lecture: commas make a tuple.) You can then:

- **unpack** it into separate variables: `h, m = split_time(135)`; or
- keep the tuple and use **indexes**: `t[0]` is the hours, `t[1]` is the minutes.

```python
def split_time(minutes):
    hours = minutes // 60
    mins = minutes % 60
    return hours, mins

t = split_time(200)
print("Hours:", t[0])
print("Minutes:", t[1])
```

```text
Hours: 3
Minutes: 20
```

### 8.2 The number of variables must match

When you unpack, you need exactly one variable for each returned value:

```text
a, b, c = split_time(90)

ValueError: not enough values to unpack (expected 3, got 2)
```

The values arrive **in the same order** as they are written after `return`. If you swap the variable names (`m, h = split_time(135)`), `m` will hold the hours — Python does not look at the names.

### 8.3 A longer example

```python
def grade_stats(marks):
    lowest = min(marks)
    highest = max(marks)
    average = sum(marks) / len(marks)
    return lowest, highest, average

low, high, avg = grade_stats([72, 95, 58, 88])
print("Lowest:", low)
print("Highest:", high)
print("Average:", avg)
```

```text
Lowest: 58
Highest: 95
Average: 78.25
```

1. The list `[72, 95, 58, 88]` is copied into the parameter `marks`.
2. The function uses the built-in functions `min`, `max`, `sum`, and `len` to calculate three values.
3. `return` sends back the tuple `(58, 95, 78.25)`.
4. The tuple is unpacked into `low`, `high`, and `avg`, in the same order.

One call gives three results. Without returning several values, we would need three separate functions.

---

## 9. Kinds of Functions: Summary

| Kind | Example definition | Example call | Gives back |
|---|---|---|---|
| No parameters, void | `def show_menu():` / `print("1. Tea")` | `show_menu()` | `None` |
| Parameters, void | `def greet(name):` / `print("Hi", name)` | `greet("Ali")` | `None` |
| Returns one value | `def square(n):` / `return n * n` | `x = square(4)` | `16` |
| Returns several values | `def split_time(m):` / `return m // 60, m % 60` | `h, m = split_time(75)` | `(1, 15)` |

---

## 10. Variables Inside a Function

Variables created inside a function — including its parameters — exist **only while the function runs**, and only **inside** it. They are called **local variables**.

```text
def find_tax(price):
    tax = price * 0.15

find_tax(100)
print(tax)

NameError: name 'tax' is not defined
```

`tax` was created inside `find_tax`. After the function ends, it no longer exists. The correct way to get a result out of a function is to **return** it:

```python
def find_tax(price):
    return price * 0.15

tax = find_tax(100)
print(tax)
```

```text
15.0
```

A variable outside the function may have the **same name** as one inside, but they are **different variables**. In Worked Example 11.3, `litres` and `cost` inside `trip_fuel` are separate from `litres` and `cost` in the main program.

---

## 11. Worked Examples

### 11.1 A discount calculator

<!-- inputs: 25|20 -->
```python
def final_price(price, percent):
    discount = price * percent / 100
    return price - discount

p = float(input("Price (KD): "))
d = float(input("Discount %: "))
result = final_price(p, d)
print("You pay:", result, "KD")
print("You save:", p - result, "KD")
```

```text
Price (KD): 25
Discount %: 20
You pay: 20.0 KD
You save: 5.0 KD
```

1. Python learns the function `final_price` but does not run it yet.
2. The user types 25 and 20; they are converted to floats.
3. `final_price(25.0, 20.0)` is called: `price` = 25.0, `percent` = 20.0.
4. Inside: `discount` = 25.0 × 20.0 / 100 = 5.0.
5. `return` sends back 25.0 − 5.0 = 20.0, which is stored in `result`.
6. Because the value was **returned**, the main program can use it again to calculate the saving.

### 11.2 Letter grade and report

```python
def letter_grade(mark):          # returns a value
    if mark >= 90:
        return "A"
    elif mark >= 75:
        return "B"
    elif mark >= 60:
        return "C"
    else:
        return "F"

def print_report(name, mark):    # void function
    grade = letter_grade(mark)
    print(name, "-", mark, "-", grade)

print_report("Noor", 93)
print_report("Fahad", 67)
```

```text
Noor - 93 - A
Fahad - 67 - C
```

- `letter_grade` **calculates** something, so it **returns** the letter.
- `print_report` **shows** a line, so it is a **void** function.
- `print_report` **calls** `letter_grade`.
- For Fahad: 67 is not ≥ 90 and not ≥ 75, but it is ≥ 60, so the result is `"C"`.

Because `letter_grade` returns its result, it can be used elsewhere too:

```python
def letter_grade(mark):
    if mark >= 90:
        return "A"
    elif mark >= 75:
        return "B"
    elif mark >= 60:
        return "C"
    else:
        return "F"

if letter_grade(88) == "B":
    print("Good work")
```

```text
Good work
```

### 11.3 Trip fuel and cost (two return values)

The distance from Kuwait City to Dammam is about 400 km.

```python
def trip_fuel(km, km_per_litre, price):
    litres = km / km_per_litre
    cost = litres * price
    return litres, round(cost, 3)

litres, cost = trip_fuel(400, 12.5, 0.085)
print("Fuel needed:", litres, "litres")
print("Fuel cost:", cost, "KD")
```

```text
Fuel needed: 32.0 litres
Fuel cost: 2.72 KD
```

1. The arguments are matched by position: `km` = 400, `km_per_litre` = 12.5, `price` = 0.085.
2. `litres` = 400 / 12.5 = 32.0.
3. `cost` = 32.0 × 0.085 = 2.72.
4. `return litres, round(cost, 3)` sends back the tuple `(32.0, 2.72)`.
5. The tuple is unpacked into two variables in the main program.

---

## 12. Important Notes

- A function must be **defined before** it is called.
- Defining a function does **not** run it. Calling it does.
- Always use **brackets** to call a function, even with no arguments: `show_menu()`.
- The body must be **indented**, like the body of an `if`.
- Arguments are matched to parameters **by position**, and their **number** must match.
- `return` **ends** the function. Lines after it in the same block do not run.
- A function with no `return` gives back `None`.
- `return a, b` returns **one tuple**.
- Variables inside a function are **local**: to use a result outside, return it.

---

## 13. Common Mistakes

### Mistake 1: Forgetting the brackets in a call

```text
def say_hi():
    print("Hi!")

say_hi
```

Nothing is printed. Without `( )`, the function is only named, not called. If you print it, you see something like `<function say_hi at 0x...>` — the function itself, not its result. **Fix:** `say_hi()`.

### Mistake 2: Calling before defining

```text
print(cube(2))

def cube(n):
    return n ** 3

NameError: name 'cube' is not defined
```

**Fix:** move the `def` block above the call.

### Mistake 3: print instead of return

```text
def add(a, b):
    print(a + b)

total = add(2, 3) * 2

5
TypeError: unsupported operand type(s) for *: 'NoneType' and 'int'
```

`add` prints 5 but returns `None`, and `None * 2` is impossible. **Fix:** `return a + b`.

### Mistake 4: Wrong number of arguments

```text
def area(width, height):
    return width * height

print(area(5))

TypeError: area() missing 1 required positional argument: 'height'
```

**Fix:** give both arguments: `area(5, 2)`.

### Mistake 5: Using a local variable outside the function

See Section 10. **Fix:** return the value and store it in a variable in the main program.

### Mistake 6: Code after return

```python
def get_total(a, b):
    return a + b
    print("Total calculated")

print(get_total(4, 6))
```

```text
10
```

The message is never printed, because `return` ends the function. **Fix:** put the `print` before the `return` (or remove it).

### Mistake 7: Wrong number of variables when unpacking

```text
def split_time(minutes):
    return minutes // 60, minutes % 60

a, b, c = split_time(90)

ValueError: not enough values to unpack (expected 3, got 2)
```

**Fix:** use exactly two variables: `h, m = split_time(90)`.

---

## 14. Mini Practice Questions

**Q1.** What is the difference between a parameter and an argument?

**Q2.** What does a function return if it has no `return` statement?

**Q3.** What does this print?

```text
def f(x):
    return x + 1
    return x + 2

print(f(5))
```

**Q4.** What is the type of the value returned by `return 3, 4`?

**Q5.** Should a function that calculates a total use `print` or `return`? Why?

### Answers

1. A parameter is the name in the `def` line; an argument is the actual value given in the call.
2. `None`.
3. `6` — the first `return` ends the function.
4. `tuple` — the value `(3, 4)`.
5. `return`, so that the program can use the total later (store it, compare it, or print it).

---

## 15. Ask AI to Help You Understand

```text
Explain Python functions to a beginner: def, parameters, arguments, and return.
Use one short example about prices in Kuwaiti Dinar. Do not use loops.
```

```text
Explain the difference between print and return inside a Python function.
Show a small example where using print instead of return causes a problem.
```

```text
Show me how a Python function can return two values, and how to unpack them.
Then give me two short practice questions, with hints only, and wait for my answers.
```

```text
Look at my function and tell me whether it should be a void function or return a value.
Explain why, but do not rewrite the whole program for me:
[paste your function here]
```

> **Remember:** Always run the code yourself to check what the AI says.

---

## 16. Summary

- A **function** is a named block of code that does one job. Define it with `def name(parameters):` and an indented body.
- Defining does not run the code; **calling** `name(arguments)` does. A call jumps into the function and back.
- **Arguments** are copied into **parameters** by position; their number must match.
- `return value` sends a value back to the call and **ends** the function. The call is replaced by the returned value.
- A **void function** has no return value; it gives back `None`.
- `return a, b` returns a **tuple**; unpack it with `x, y = f(...)`.
- **print** shows to the person; **return** gives to the program.
- Variables inside a function are **local**: return the results you need outside.

---

## Basic Exercises

> Exercises 1–12 are the same as in the slides. Exercises 13–15 are extra practice.

**Exercise 1.** In this code, name: the function, the parameters, the arguments, and the value stored in `a`.

```text
def rectangle_area(width, height):
    return width * height

a = rectangle_area(4, 3)
```

**Exercise 2.** Predict the output.

```text
def double(n):
    return n * 2

print(double(4))
print(double("ab"))
print(double(3) + 1)
```

**Exercise 3.** Predict the output.

```text
def greet(name):
    print("Hello,", name)

x = greet("Noor")
print(x)
```

**Exercise 4.** Which functions are **void**, and which **return** a value?

```text
def a(n):
    print(n * 2)

def b(n):
    return n * 2

def c():
    print("Menu")
```

## Practice Exercises

**Exercise 5.** Write a function `c_to_f(c)` that **returns** the temperature in Fahrenheit (`c * 9 / 5 + 32`). Print the result for 45 °C.

**Exercise 6.** Write a function `is_even(n)` that returns `True` if `n` is even, and `False` otherwise. Test it with 7 and 10.

**Exercise 7.** Write a **void** function `show_ticket(name, flight)` that prints two lines: `Passenger: …` and `Flight: …`. Call it once.

**Exercise 8.** Find and fix the error.

```text
def add(a, b):
    print(a + b)

total = add(2, 3) * 2
print(total)
```

**Exercise 13.** Write a function `bmi(weight, height)` that returns the body mass index, `weight / height²`, rounded to 1 decimal place. Print the result for 70 kg and 1.75 m.

## Challenge Exercises

**Exercise 9.** Write a function `circle(r)` that returns **two** values: the area (π r²) and the circumference (2 π r), each rounded to 2 decimal places. Use `math.pi`. Print both for r = 3.

**Exercise 10.** Write a function `min_max(a, b, c)` that returns the smallest and the largest of three numbers. Call it with 7, 2, 9 and print the results.

**Exercise 11.** Predict the output.

```text
def square(n):
    return n * n

def sum_of_squares(a, b):
    return square(a) + square(b)

print(sum_of_squares(3, 4))
```

**Exercise 12.** Write `split_bill(total, people)` that returns the 10% tip and the amount each person pays (total + tip, divided by people), both rounded to 3 places. Use 24 KD and 4 people.

**Exercise 14.** Write a function `swap(a, b)` that returns the two values in the opposite order. Use it so that `x = 3` and `y = 8` become `x = 8` and `y = 3`, then print `x` and `y`.

**Exercise 15.** Electricity costs 0.005 KD per unit. Write a function `electricity(units)` that returns two values: the cost, and the text `"High"` if more than 3000 units were used, otherwise `"Normal"`. Print the results for 3500 units and for 1200 units.

---

# Exercise Solutions

### Solution 1

| Part | Answer |
|---|---|
| Function | `rectangle_area` |
| Parameters | `width`, `height` |
| Arguments | `4`, `3` |
| Value in `a` | `12` |

### Solution 2

```python
def double(n):
    return n * 2

print(double(4))
print(double("ab"))
print(double(3) + 1)
```

```text
8
abab
7
```

`"ab" * 2` repeats the string. `double(3)` returns 6, and 6 + 1 = 7.

### Solution 3

```python
def greet(name):
    print("Hello,", name)

x = greet("Noor")
print(x)
```

```text
Hello, Noor
None
```

`greet` prints but does not return anything, so `x` is `None`.

### Solution 4

- `a` — **void**: it prints `n * 2`, but returns `None`.
- `b` — **returns** a value.
- `c` — **void**.

### Solution 5

```python
def c_to_f(c):
    return c * 9 / 5 + 32

print(c_to_f(45))
```

```text
113.0
```

### Solution 6

```python
def is_even(n):
    return n % 2 == 0

print(is_even(7), is_even(10))
```

```text
False True
```

`n % 2 == 0` is already `True` or `False`, so it can be returned directly. A longer version with `if`/`else` that returns `True` or `False` is also correct.

### Solution 7

```python
def show_ticket(name, flight):
    print("Passenger:", name)
    print("Flight:", flight)

show_ticket("Maryam", "KU101")
```

```text
Passenger: Maryam
Flight: KU101
```

### Solution 8

`add` prints the sum instead of returning it, so `add(2, 3)` gives `None`, and `None * 2` causes a `TypeError`. Return the sum instead:

```python
def add(a, b):
    return a + b

total = add(2, 3) * 2
print(total)
```

```text
10
```

### Solution 9

```python
import math

def circle(r):
    area = round(math.pi * r ** 2, 2)
    circumference = round(2 * math.pi * r, 2)
    return area, circumference

a, c = circle(3)
print("Area:", a)
print("Circumference:", c)
```

```text
Area: 28.27
Circumference: 18.85
```

### Solution 10

```python
def min_max(a, b, c):
    return min(a, b, c), max(a, b, c)

small, large = min_max(7, 2, 9)
print(small, large)
```

```text
2 9
```

The first returned value goes into `small`, and the second into `large`.

### Solution 11

```python
def square(n):
    return n * n

def sum_of_squares(a, b):
    return square(a) + square(b)

print(sum_of_squares(3, 4))
```

```text
25
```

`square(3)` returns 9 and `square(4)` returns 16; 9 + 16 = 25.

### Solution 12

```python
def split_bill(total, people):
    tip = total * 0.10
    each = (total + tip) / people
    return round(tip, 3), round(each, 3)

tip, each = split_bill(24, 4)
print("Tip:", tip, "KD")
print("Each person pays:", each, "KD")
```

```text
Tip: 2.4 KD
Each person pays: 6.6 KD
```

The tip is 24 × 0.10 = 2.4, and (24 + 2.4) / 4 = 6.6.

### Solution 13

```python
def bmi(weight, height):
    return round(weight / height ** 2, 1)

print(bmi(70, 1.75))
```

```text
22.9
```

1.75² = 3.0625, and 70 / 3.0625 = 22.857…, which rounds to 22.9.

### Solution 14

```python
def swap(a, b):
    return b, a

x = 3
y = 8
x, y = swap(x, y)
print(x, y)
```

```text
8 3
```

`swap(3, 8)` returns the tuple `(8, 3)`, which is unpacked into `x` and `y`.

### Solution 15

```python
def electricity(units):
    cost = units * 0.005
    if units > 3000:
        level = "High"
    else:
        level = "Normal"
    return cost, level

cost, level = electricity(3500)
print(cost, level)
cost, level = electricity(1200)
print(cost, level)
```

```text
17.5 High
6.0 Normal
```

The function calculates the cost, chooses the level with an `if`, and returns both values together.

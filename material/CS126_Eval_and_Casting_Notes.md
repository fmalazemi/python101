# CS126 – Introduction to Python

## Casting and the eval() Function

**Instructor:** Dr. Fawaz Alazemi

---

## Learning Objectives

After studying these notes, you should be able to:

1. Explain what a **type** is and why some operations fail when types are mixed.
2. Explain the difference between **automatic (implicit)** conversion and **explicit** conversion (casting).
3. Use `int()`, `float()`, `str()`, and `bool()`, and predict their results.
4. Convert between collections with `list()`, `tuple()`, and `set()`.
5. Recognize casting errors: `ValueError` and `TypeError`.
6. Use casting with `input()` to read text, whole numbers, and decimal numbers.
7. Use `eval(input())` to read numbers, expressions, several values on one line, and collections.
8. Compare `eval()` with casting, and explain why `eval()` is unsafe with input you do not trust.

---

## 1. Introduction

### 1.1 Every value has a type

Every value in Python has a **type**. You have already met several:

| Value | Type |
|---|---|
| `25` | `int` (whole number) |
| `3.5` | `float` (decimal number) |
| `"Kuwait"` | `str` (string, text) |
| `True` | `bool` (True or False) |
| `[1, 2]`, `(1, 2)`, `{1, 2}` | `list`, `tuple`, `set` |

The type decides what an operation does. For example, `+` **adds** numbers but **joins** strings:

```python
print(5 + 3)
print("5" + "3")
```

```text
8
53
```

### 1.2 The problem with input()

`input()` always returns a **string**, even when the user types digits:

<!-- inputs: 5|3 -->
```python
a = input("First number: ")
b = input("Second number: ")
print(a + b)
print(type(a))
```

```text
First number: 5
Second number: 3
53
<class 'str'>
```

To calculate with typed numbers, we must **change the type** of the value. This lecture shows two ways to do this:

1. **Casting** — functions such as `int()`, `float()`, and `str()`.
2. **`eval()`** — a function that reads text as Python code.

---

## 2. Vocabulary

| Term | Meaning |
|---|---|
| **Type** | The kind of a value: int, float, str, bool, list, … |
| **Casting** (type conversion) | Making a new value of another type from an existing value |
| **Implicit conversion** | A conversion Python does automatically |
| **Explicit conversion** | A conversion you write yourself, such as `int("5")` |
| **Expression** | Code that has a value, such as `3 + 4` or `[1, 2]` |
| **Evaluate** | Work out the value of an expression |
| **Unpacking** | Storing the items of a tuple in several variables: `a, b = (1, 2)` |
| **ValueError** | The value has the right type, but the wrong content: `int("hello")` |
| **TypeError** | The operation cannot be used with this type at all: `list(5)` |

---

## 3. Casting

### 3.1 What casting means

**Casting** means making a value of a **new type** from an existing value. We call the name of the type as if it were a function:

```python
text = "25"
number = int(text)
print(number + 1)
print(type(text), type(number))
```

```text
26
<class 'str'> <class 'int'>
```

Notice that `text` is **still a string** after the cast. Casting does **not** change the original value — it creates a **new** one. If you want to keep the new value, you must store it in a variable.

The casting functions you will use most:

| Function | Makes a… |
|---|---|
| `int()` | whole number |
| `float()` | decimal number |
| `str()` | string |
| `bool()` | `True` or `False` |
| `list()`, `tuple()`, `set()` | collection |

### 3.2 Automatic (implicit) conversion

Sometimes Python converts a value **by itself**:

```python
print(5 + 2.0)     # int + float gives a float
print(10 / 2)      # / always gives a float
print(True + 1)    # True counts as 1
```

```text
7.0
5.0
2
```

Python only does this when it is **safe** — when no information can be lost. An `int` can become a `float` (5 → 5.0), but Python will never turn a `float` into an `int` by itself, because the decimal part would be lost.

Python also **never** mixes text and numbers automatically. This line causes an error:

```text
print("Age: " + 19)

TypeError: can only concatenate str (not "int") to str
```

In these cases, **you** must convert the value — that is explicit conversion, or casting:

```python
print("Age: " + str(19))
```

```text
Age: 19
```

### 3.3 int() — convert to a whole number

```python
print(int("42"))      # from text
print(int(" 42 "))    # spaces around the number are ignored
print(int(7.9))       # from a float
print(int(-7.9))
print(int(True))      # from a bool
print(int(False))
```

```text
42
42
7
-7
1
0
```

Important rules:

- **From a string:** the text must contain a **whole number** (digits, possibly with a `+` or `-` sign and spaces around). Text with a dot, a comma, or letters gives a `ValueError`.
- **From a float:** the decimal part is **cut off** (this is called *truncation*). `int(7.9)` is `7`, not `8`. For negative numbers, `int(-7.9)` is `-7`.
- **From a bool:** `True` becomes `1` and `False` becomes `0`.

If you want the **nearest** whole number instead, use `round()`:

```python
print(int(7.9), round(7.9))
```

```text
7 8
```

To convert text such as `"7.9"` to a whole number, cast twice — first to `float`, then to `int`:

```python
print(int(float("7.9")))
```

```text
7
```

### 3.4 float() — convert to a decimal number

```python
print(float("3.75"))   # from text with a dot
print(float("3"))      # from whole-number text
print(float(8))        # from an int
print(float(False))    # from a bool
```

```text
3.75
3.0
8.0
0.0
```

- `float()` accepts text with **or without** a dot.
- The result always has a decimal part, even if it is `.0`.
- `float()` is the best choice for prices, temperatures, weights, and distances.

<!-- inputs: 1.250 -->
```python
price = float(input("Price (KD): "))
print(price * 2)
```

```text
Price (KD): 1.250
2.5
```

### 3.5 str() — convert to text

`str()` works with **any** value:

```python
age = 19
gpa = 3.5
msg = "Age " + str(age) + ", GPA " + str(gpa)
print(msg)
print(str(3) + str(4))
print(str([1, 2]))
```

```text
Age 19, GPA 3.5
34
[1, 2]
```

When do you need `str()`?

- When you **join** a number with text using `+`.
- When you want to use **string tools** on a number. For example, `len(str(2026))` counts the digits of 2026:

```python
year = 2026
print(len(str(year)))
print(str(year)[0])     # first digit
```

```text
4
2
```

You do **not** need `str()` when you use commas in `print()`, because `print` accepts values of any type:

```python
print("Age", 19)
```

```text
Age 19
```

### 3.6 bool() — convert to True or False

`bool()` returns `False` for "empty" or "zero" values, and `True` for everything else:

```python
print(bool(0), bool(25), bool(-3))
print(bool(0.0), bool(0.1))
print(bool(""), bool("Ali"))
print(bool([]), bool([0]))
print(bool("0"), bool("False"))
```

```text
False True True
False True
False True
False True
True True
```

| Gives `False` | Gives `True` |
|---|---|
| `0`, `0.0` | any other number (also negative numbers) |
| `""` (empty string) | any non-empty string, even `" "`, `"0"`, `"False"` |
| `[]`, `()`, `set()` (empty collections) | any collection with at least one item, even `[0]` |

**Be careful:** `bool("False")` is `True`. `bool()` does not read the meaning of the word — it only checks whether the string is empty. This means `bool(input())` is almost never what you want. To check whether the user typed a certain word, compare the text:

<!-- inputs: yes -->
```python
answer = input("Do you agree? (yes/no) ")
agree = answer == "yes"
print(agree)
```

```text
Do you agree? (yes/no) yes
True
```

### 3.7 Casting collections: list(), tuple(), set()

These functions make a **new collection** from the items of another collection (or a string):

```python
codes = ["KWT", "UAE", "KWT", "QAT"]
print(tuple(codes))
print(set(codes) == {"KWT", "UAE", "QAT"})
print(len(set(codes)))
print(list((10, 20, 30)))
print(list("CS126"))
print(sorted(set("banana")))
```

```text
('KWT', 'UAE', 'KWT', 'QAT')
True
3
[10, 20, 30]
['C', 'S', '1', '2', '6']
['a', 'b', 'n']
```

Common uses:

- `set(x)` removes duplicates, so `len(set(x))` counts the **different** values.
- `tuple(x)` makes a fixed copy that cannot be changed.
- `list(x)` makes a changeable copy, for example of a tuple.
- From a **string**, each **character** becomes one item.

A single number is **not** a collection, so it cannot be converted to one:

```text
list(5)

TypeError: 'int' object is not iterable
```

("Iterable" means "something whose items can be taken one by one". Strings, lists, tuples, and sets are iterable; numbers are not.)

### 3.8 Casting summary

| Code | Result | Note |
|---|---|---|
| `int("12")` | `12` | text of a whole number |
| `int("12.5")` | ValueError | int text cannot contain a dot |
| `int(12.5)` | `12` | decimals cut off |
| `int("1,000")` | ValueError | commas are not allowed |
| `int("")` | ValueError | empty text |
| `float("12")` | `12.0` | |
| `float("abc")` | ValueError | not a number |
| `str(12.5)` | `'12.5'` | `str` always works |
| `bool("False")` | `True` | non-empty string |
| `list("ab")` | `['a', 'b']` | one item per character |
| `list(12)` | TypeError | a number is not a collection |

The error messages look like this:

```text
int("12.5")   →  ValueError: invalid literal for int() with base 10: '12.5'
float("abc")  →  ValueError: could not convert string to float: 'abc'
list(12)      →  TypeError: 'int' object is not iterable
```

### 3.9 Casting with input()

Choose the cast by **what the user should type**:

<!-- inputs: Sara|20|3.6 -->
```python
name = input("Name: ")           # text: no cast
age = int(input("Age: "))         # whole number
gpa = float(input("GPA: "))       # decimal number
print(name + " will be " + str(age + 1) + " next year")
print("GPA out of 100:", gpa / 4 * 100)
```

```text
Name: Sara
Age: 20
GPA: 3.6
Sara will be 21 next year
GPA out of 100: 90.0
```

How `int(input("Age: "))` runs:

1. The **inner** call runs first: `input` shows the prompt and returns the text `"20"`.
2. `int("20")` makes the number `20`.
3. The number is stored in `age`.

If the user types something that is not a whole number (for example `twenty` or `20.5`), `int()` stops the program with a `ValueError`.

**Not everything made of digits should be cast.** Phone numbers, civil ID numbers, and area codes are made of digits, but we never do math with them, and casting would remove leading zeros (`int("0096")` is `96`). Keep them as strings.

---

## 4. The eval() Function

### 4.1 What eval() does

`eval(text)` treats the string `text` **as if it were Python code**, calculates its value, and returns that value. The name comes from **evaluate**: "work out the value".

```python
x = eval("3 + 4")
print(x, type(x))
print(eval("2 ** 10"))
print(eval("7 / 2"))
print(eval("8 - 3 * 2"))
```

```text
7 <class 'int'>
1024
3.5
2
```

The text must be an **expression** — something that has a value, such as a number, a calculation, or a list. Statements such as `x = 5` are not allowed.

### 4.2 Casting vs eval: who decides the type?

With casting, **you** choose the type: `float("5")` always gives a float. With `eval`, the **text** chooses the type, using normal Python rules:

```python
print(type(eval("5")))
print(type(eval("5.5")))
print(type(eval("[1, 2, 3]")))
print(type(eval("(29, 47)")))
print(type(eval("{1, 2, 2}")))
print(type(eval("'Kuwait'")))
print(type(eval("5 > 3")))
```

```text
<class 'int'>
<class 'float'>
<class 'list'>
<class 'tuple'>
<class 'set'>
<class 'str'>
<class 'bool'>
```

### 4.3 eval(input()) — reading numbers

<!-- inputs: 5|2.5 -->
```python
a = eval(input("First number: "))
b = eval(input("Second number: "))
print(a + b)
print(type(a), type(b))
```

```text
First number: 5
Second number: 2.5
7.5
<class 'int'> <class 'float'>
```

As with casting, `input` runs first and returns the text; then `eval` turns the text into a value. The user can type a whole number or a decimal, and `eval` gives an `int` or a `float` to match.

### 4.4 Reading an expression

The user can type a calculation, which casting cannot handle:

<!-- inputs: 10 / 4 -->
```python
x = eval(input("x: "))
print(x, type(x))
```

```text
x: 10 / 4
2.5 <class 'float'>
```

`float("10 / 4")` would give a `ValueError`.

### 4.5 Reading several values in one line

When the user types values separated by **commas**, `eval` produces a **tuple** (commas make a tuple). The tuple can be **unpacked** into variables:

<!-- inputs: 8, 3.5 -->
```python
w, h = eval(input("Width, height: "))
print("Area:", w * h)
```

```text
Width, height: 8, 3.5
Area: 28.0
```

<!-- inputs: 90, 85, 77 -->
```python
a, b, c = eval(input("Three marks: "))
print("Average:", (a + b + c) / 3)
```

```text
Three marks: 90, 85, 77
Average: 84.0
```

Rules:

- Values must be separated by **commas**. Spaces alone (`8 3.5`) give a `SyntaxError`.
- The number of values must **equal** the number of variables, or you get a `ValueError`.

Casting cannot do this: `int("8, 3")` gives a `ValueError`.

### 4.6 Reading a list — and casting the result

The brackets the user types decide the type: `[ ]` list, `( )` tuple, `{ }` set. After `eval` has built the collection, you can use casting to convert it further:

<!-- inputs: [44, 46, 48, 46, 47] -->
```python
temps = eval(input("Temperatures: "))
print(type(temps), len(temps))
print("Max:", max(temps), "Min:", min(temps))
print("Different values:", len(set(temps)))
print("Fixed copy:", tuple(temps))
```

```text
Temperatures: [44, 46, 48, 46, 47]
<class 'list'> 5
Max: 48 Min: 44
Different values: 4
Fixed copy: (44, 46, 48, 46, 47)
```

Do **not** confuse `eval` with `list()`. Casting the input text with `list()` gives a list of **characters**, not numbers:

```python
print(list("[4, 5]"))
```

```text
['[', '4', ',', ' ', '5', ']']
```

### 4.7 eval() and text

Do **not** use `eval` to read text. The word `Kuwait` (without quotes) would be read as a **variable name**, causing `NameError: name 'Kuwait' is not defined`. Plain `input()` already returns a string.

### 4.8 eval() can use your variables

```python
price = 2.5
qty = 4
print(eval("price * qty"))
```

```text
10.0
```

The text given to `eval` can use **anything** in your program. That is powerful — and it is the reason `eval` is dangerous (Section 6).

---

## 5. eval() Compared with Casting

| User types | `int(text)` | `float(text)` | `eval(text)` |
|---|---|---|---|
| `5` | `5` | `5.0` | `5` |
| `5.5` | ValueError | `5.5` | `5.5` |
| `2+3` | ValueError | ValueError | `5` |
| `8, 3` | ValueError | ValueError | `(8, 3)` |
| `05` | `5` | `5.0` | SyntaxError |
| `hello` | ValueError | ValueError | NameError |

- **Casting:** you choose the type, and only one value of that kind is accepted. Predictable and **safe**.
- **eval:** the text chooses the type; numbers, expressions, several values, and lists are accepted. **Flexible** but **risky**.

### Errors eval() can cause

| User types | Result | Reason |
|---|---|---|
| `hello` | `NameError: name 'hello' is not defined` | text without quotes is read as a variable name |
| `3 4` | `SyntaxError: invalid syntax` | values must be separated by commas |
| (nothing) | `SyntaxError` | an empty string is not an expression |
| `05` | `SyntaxError: leading zeros in decimal integer literals are not permitted; …` | Python numbers cannot start with 0 |
| `1, 2, 3` for `a, b = …` | `ValueError: too many values to unpack (expected 2)` | 3 values, 2 variables |
| `5,` | no error, but the result is `(5,)` | the comma creates a tuple |

### Checking the result with type()

Because `eval` accepts many kinds of input, the result may not be what your program expects. Check it with `type()`:

<!-- inputs: [90, 85] -->
```python
value = eval(input("Enter a number: "))
if type(value) in (int, float):
    print("Square:", value ** 2)
else:
    print("That is not a number:", type(value))
```

```text
Enter a number: [90, 85]
That is not a number: <class 'list'>
```

---

## 6. Safety: eval() Runs Whatever Is Typed

`eval` does not only convert numbers. It runs **any Python expression**, including function calls:

<!-- inputs: print("I ran your code!") -->
```python
x = eval(input("Enter a number: "))
print("You entered:", x)
```

```text
Enter a number: print("I ran your code!")
I ran your code!
You entered: None
```

The user did not type a number, and Python **ran their code**. Here it only printed a message, but a malicious user could type an expression that deletes files, reads private information, or crashes the program.

**The rule for this course:**

- `eval(input())` is acceptable in **your own practice programs**, where **you** are the only user.
- In **real** programs (websites, apps, anything other people use), **never** pass user input to `eval`.
- Use casting — `int()` or `float()` — for numbers. Casting functions never run code: if the text is not a number, they simply give a `ValueError`.

### Which should I use?

| You want… | Use |
|---|---|
| text from the user | `input()` alone |
| one whole number from the user | `int(input())` |
| one decimal number from the user | `float(input())` |
| to join a number with text using `+` | `str(number)` |
| to remove duplicates / make a fixed copy | `set()` / `tuple()` |
| several numbers in one line, an expression, or a list — in a practice program | `eval(input())` |

Good habit: choose the **simplest, safest** tool that does the job.

---

## 7. Worked Examples

### 7.1 Petrol station receipt (casting)

<!-- inputs: Ahmad|40 -->
```python
name = input("Customer name: ")
litres = float(input("Litres pumped: "))
price = 0.085                  # KD per litre
total = round(litres * price, 3)
print("Customer: " + name)
print("Litres: " + str(litres))
print("Total: " + str(total) + " KD")
```

```text
Customer name: Ahmad
Litres pumped: 40
Customer: Ahmad
Litres: 40.0
Total: 3.4 KD
```

Step by step:

1. `name` stays text — a name needs no cast.
2. `float("40")` gives `40.0`. We use `float` because a customer might buy 35.5 litres.
3. `40.0 * 0.085` is calculated and rounded to 3 decimal places (fils): `3.4`.
4. `str()` turns `litres` and `total` into text so `+` can join them with other text.

### 7.2 Room area and flooring cost (eval and casting)

<!-- inputs: 4.5, 3|6.75 -->
```python
length, width = eval(input("Length, width (m): "))
price = float(input("Price per m² (KD): "))
area = length * width
cost = area * price
print("Area:", area, "m²")
print("Cost:", round(cost, 3), "KD")
```

```text
Length, width (m): 4.5, 3
Price per m² (KD): 6.75
Area: 13.5 m²
Cost: 91.125 KD
```

`eval` is used only where casting cannot do the job — reading two values in one line. The single price uses `float()`, which is simpler and safer.

### 7.3 A grade report from a list

<!-- inputs: [72, 95, 58, 95, 61] -->
```python
marks = eval(input("Marks as a list: "))
avg = sum(marks) / len(marks)
print("Students: " + str(len(marks)))
print("Different marks: " + str(len(set(marks))))
print("Average: " + str(round(avg, 1)))
print("Average (whole): " + str(int(avg)))
if avg >= 60:
    print("Class passed on average")
else:
    print("Class needs support")
```

```text
Marks as a list: [72, 95, 58, 95, 61]
Students: 5
Different marks: 4
Average: 76.2
Average (whole): 76
Class passed on average
```

Step by step:

1. `eval` builds a real list of numbers from the typed text.
2. `set(marks)` removes the repeated 95, so there are 4 different marks.
3. The sum is 381, and 381 / 5 = 76.2. `int(76.2)` cuts off the decimals: 76.
4. `str()` lets every number be joined with text.

---

## 8. Important Notes

- Casting creates a **new** value. Write `x = int(x)` if you want `x` itself to hold the new value.
- `int()` **cuts off** decimals; `round()` rounds to the nearest whole number.
- `int("3.5")` fails, but `int(float("3.5"))` works.
- `str()` can convert **any** value; the other casts can fail.
- `bool()` checks only for "empty" or "zero", not for meaning.
- `list(text)` splits text into characters; `eval(text)` reads a list typed in brackets.
- Prefer casting. Use `eval` only when casting cannot do the job, and only with input you trust.

---

## 9. Common Mistakes

### Mistake 1: Forgetting to convert input

```text
side = input("Side: ")
print("Area:", side * side)

TypeError: can't multiply sequence by non-int of type 'str'
```

**Fix:** `side = float(input("Side: "))`.

### Mistake 2: Joining a number with text

```text
total = 2.5 * 4
print("Total: " + total + " KD")

TypeError: can only concatenate str (not "float") to str
```

**Fix:** `print("Total: " + str(total) + " KD")`, or use commas: `print("Total:", total, "KD")`.

### Mistake 3: Using int() for a decimal value

```text
weight = int(input("Weight: "))      # user types: 72.5

ValueError: invalid literal for int() with base 10: '72.5'
```

**Fix:** use `float(input(...))`.

### Mistake 4: Using bool() on typed text

<!-- inputs: False -->
```python
ans = bool(input("Agree? "))
print(ans)
```

```text
Agree? False
True
```

Any non-empty text is `True`. **Fix:** compare the text: `ans = input("Agree? ") == "True"`.

### Mistake 5: Not storing the result of a cast

```python
x = "5"
int(x)          # the new value is thrown away
print(x + "1")
```

```text
51
```

**Fix:** `x = int(x)`, then `print(x + 1)` gives `6`.

### Mistake 6: Using eval to read text

```text
city = eval(input("City: "))      # user types: Kuwait

NameError: name 'Kuwait' is not defined
```

**Fix:** `city = input("City: ")`.

### Mistake 7: Typing values without commas for eval

```text
a, b = eval(input("Two numbers: "))   # user types: 4 9

SyntaxError: invalid syntax
```

**Fix:** the user must type `4, 9`. Make the prompt clear: `"Two numbers separated by a comma: "`.

### Mistake 8: Using eval when casting is enough

`age = eval(input("Your age: "))` works, but it lets the user run any code. Since only a whole number is needed, use `int(input(...))`.

---

## 10. Mini Practice Questions

**Q1.** What is `int(9.99)`? What is `round(9.99)`?

**Q2.** What is `float("4")`? What is `int("4.0")`?

**Q3.** What is `bool(" ")` (a string containing one space)?

**Q4.** What is `list("abc")`? What is `eval("[1, 2]")`?

**Q5.** The user types `3, 4` for `x = eval(input())`. What is `type(x)`?

**Q6.** Why are casting functions safer than `eval`?

### Answers

1. `9` and `10`.
2. `4.0`; `int("4.0")` gives a **ValueError** (a dot in int text).
3. `True` — the string is not empty.
4. `['a', 'b', 'c']`; the list `[1, 2]`.
5. `<class 'tuple'>`.
6. Casting functions only convert one kind of value and never run code; `eval` runs any expression the user types.

---

## 11. Ask AI to Help You Understand

```text
Explain casting in Python to a beginner using int(), float(), str(), and bool().
Give one short example for each, with the output. Do not use loops.
```

```text
Why does int("3.5") give an error in Python but int(3.5) works?
Explain simply, and show how to convert "3.5" to 3.
```

```text
Compare eval(input()) with int(input()) and float(input()) in a table of example inputs.
Then explain why eval() is dangerous. Do not give me exercises yet.
```

```text
Give me five short Python casting expressions, one at a time, and ask me to predict the
result or the error. Wait for my answer before telling me if I am right.
```

> **Remember:** Always run the code yourself. AI can make mistakes, and running code is the only way to be sure.

---

## 12. Summary

- `input()` always returns a **string**.
- **Casting** makes a new value of another type: `int()`, `float()`, `str()`, `bool()`, `list()`, `tuple()`, `set()`.
- Python converts automatically only when it is safe (int → float); it never mixes text and numbers by itself.
- `int()` cuts off decimals; `int("3.5")` is a `ValueError`.
- Use `str()` to join numbers with text using `+`.
- `bool()` is `False` only for empty or zero values.
- `eval(text)` calculates text as a Python expression; the text decides the type.
- `a, b = eval(input())` reads two values typed with a comma.
- `eval` runs **any** code: prefer casting, and use `eval` only with input you trust.

---

## Basic Exercises

> Exercises 1–12 are the same as in the slides. Exercises 13–15 are extra practice.

**Exercise 1.** Predict the output.

```text
print(int(7.9), float(4))
print(str(3) + str(4), int(True))
```

**Exercise 2.** Predict the output.

```text
print(bool(0), bool("0"))
print(bool(""), bool([0]))
```

**Exercise 3.** Predict the output.

```text
print(eval("8 - 3 * 2"))
print(eval("9 / 3"), type(eval("9 / 3")))
```

**Exercise 4.** The user types `6` both times. Predict the output.

```text
a = input("a: ")
b = int(input("b: "))
print(a * 2, b * 2)
```

## Practice Exercises

**Exercise 5.** Find and fix the error.

```text
price = 2.5
qty = 4
print("Total: " + price * qty)
```

**Exercise 6.** Read the user's age with casting, and print a message such as `You will be 24 in 5 years` using `+` to join the text.

**Exercise 7.** Using **one** `input`, read a car's distance (km) and fuel used (litres), for example `420, 35`. Print the km per litre.

**Exercise 8.** Read a list of temperatures with `eval(input())`. Print the highest, the lowest, and how many **different** temperatures there are.

**Exercise 13.** Read a price and a discount percentage in one line, for example `25, 10`. Print the price after the discount.

## Challenge Exercises

**Exercise 9.** For each line, give the result or the error type.

1. `int("12")`
2. `int("12.5")`
3. `int(float("12.5"))`
4. `list(12)`
5. `list("12")`

**Exercise 10.** Read a whole number and print how many **digits** it has (e.g. `2026` → 4). *Hint: cast twice.*

**Exercise 11.** Read one value with `eval(input())`. If it is an `int` or `float`, print its square; if it is a list, print its length; otherwise print `Unsupported type`.

**Exercise 12.** Explain why this program is dangerous, and rewrite it safely.

```text
age = eval(input("Your age: "))
print("Next year you will be", age + 1)
```

**Exercise 14.** Read three side lengths in one line (e.g. `3, 4, 5`). Print `Right triangle` if a² + b² = c² (assume c is the longest), otherwise `Not a right triangle`.

**Exercise 15.** The user types a list of GCC country codes, for example `["KWT", "UAE", "KWT", "OMN"]`. Print the number of different codes, and the codes as a sorted list with no duplicates.

---

# Exercise Solutions

### Solution 1

`int` cuts off the decimals, `float(4)` adds `.0`, `str + str` joins text, and `True` is 1.

```python
print(int(7.9), float(4))
print(str(3) + str(4), int(True))
```

```text
7 4.0
34 1
```

### Solution 2

Only empty or zero values are `False`. `"0"` is a non-empty string and `[0]` is a list with one item.

```python
print(bool(0), bool("0"))
print(bool(""), bool([0]))
```

```text
False True
False True
```

### Solution 3

`*` is calculated before `-`; `/` always gives a float.

```python
print(eval("8 - 3 * 2"))
print(eval("9 / 3"), type(eval("9 / 3")))
```

```text
2
3.0 <class 'float'>
```

### Solution 4

`a` is the string `"6"`, so `a * 2` repeats it. `b` is the number 6, so `b * 2` is 12.

<!-- inputs: 6|6 -->
```python
a = input("a: ")
b = int(input("b: "))
print(a * 2, b * 2)
```

```text
a: 6
b: 6
66 12
```

### Solution 5

`price * qty` is the float `10.0`, which cannot be joined to text with `+`. Cast it with `str()`:

```python
price = 2.5
qty = 4
print("Total: " + str(price * qty))
```

```text
Total: 10.0
```

### Solution 6

<!-- inputs: 19 -->
```python
age = int(input("Age: "))
older = str(age + 5)
print("You will be " + older + " in 5 years")
```

```text
Age: 19
You will be 24 in 5 years
```

The addition `age + 5` must happen **before** the cast to `str`; otherwise it would be text joining, not math.

### Solution 7

<!-- inputs: 420, 35 -->
```python
km, litres = eval(input("Distance, fuel: "))
print("km per litre:", km / litres)
```

```text
Distance, fuel: 420, 35
km per litre: 12.0
```

### Solution 8

<!-- inputs: [44, 46, 49, 43, 46] -->
```python
temps = eval(input("Temperatures: "))
print(max(temps), min(temps), len(set(temps)))
```

```text
Temperatures: [44, 46, 49, 43, 46]
49 43 4
```

`set(temps)` removes the repeated 46, leaving 4 different values.

### Solution 9

| | Code | Result |
|---|---|---|
| 1 | `int("12")` | `12` |
| 2 | `int("12.5")` | `ValueError` — int text cannot contain a dot |
| 3 | `int(float("12.5"))` | `12` — text → 12.5 → 12 |
| 4 | `list(12)` | `TypeError` — a number is not a collection |
| 5 | `list("12")` | `['1', '2']` — one item per character |

### Solution 10

Cast to `int` so that only a whole number is accepted, then cast to `str` so that `len` can count its characters.

<!-- inputs: 2026 -->
```python
n = int(input("Whole number: "))
digits = len(str(n))
print("Number of digits: " + str(digits))
```

```text
Whole number: 2026
Number of digits: 4
```

For a negative number, use `len(str(abs(n)))` so that the minus sign is not counted.

### Solution 11

<!-- inputs: [3, 8, 1] -->
```python
value = eval(input("Value: "))
if type(value) in (int, float):
    print(value ** 2)
elif type(value) == list:
    print(len(value))
else:
    print("Unsupported type")
```

```text
Value: [3, 8, 1]
3
```

With the input `5`, it prints 25; with `(1, 2)`, it prints `Unsupported type`.

### Solution 12

`eval` runs **any** Python expression the user types, not only numbers, so a user could type harmful code and Python would run it. The program needs only a whole number, so casting with `int()` is enough — and it is safe, because `int()` never runs code; anything that is not a whole number causes a `ValueError`.

<!-- inputs: 19 -->
```python
age = int(input("Your age: "))
print("Next year you will be", age + 1)
```

```text
Your age: 19
Next year you will be 20
```

### Solution 13

<!-- inputs: 25, 10 -->
```python
price, percent = eval(input("Price, discount %: "))
final = price * (1 - percent / 100)
print("Final price:", round(final, 3))
```

```text
Price, discount %: 25, 10
Final price: 22.5
```

### Solution 14

<!-- inputs: 3, 4, 5 -->
```python
a, b, c = eval(input("Sides: "))
if a ** 2 + b ** 2 == c ** 2:
    print("Right triangle")
else:
    print("Not a right triangle")
```

```text
Sides: 3, 4, 5
Right triangle
```

9 + 16 = 25, so the condition is `True`.

### Solution 15

<!-- inputs: ["KWT", "UAE", "KWT", "OMN"] -->
```python
codes = eval(input("Codes: "))
different = set(codes)
print(len(different))
print(sorted(different))
```

```text
Codes: ["KWT", "UAE", "KWT", "OMN"]
3
['KWT', 'OMN', 'UAE']
```

`set()` removes the duplicate `"KWT"`, and `sorted()` returns the codes as a list in alphabetical order. The user must type the quotes, so that `eval` reads the codes as strings, not as variable names.

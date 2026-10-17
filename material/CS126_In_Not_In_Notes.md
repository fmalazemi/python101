# CS126 – Introduction to Python

## The in and not in Operators

**Instructor:** Dr. Fawaz Alazemi

---

## Learning Objectives

After studying these notes, you should be able to:

1. Explain what a **membership operator** is and what `in` and `not in` return.
2. Use `in` with **strings** to search for a character or a piece of text (a substring).
3. Use `in` with **lists**, **tuples**, and **sets** to search for a whole item.
4. Explain clearly the difference between "text inside a string" and "item inside a collection".
5. Explain why `in` does not look inside inner lists.
6. Use `in` and `not in` inside `if` statements and together with `and`, `or`, and `not`.
7. Replace long `==` / `or` chains with a single `in` test, and avoid the `x == "a" or "b"` trap.
8. Clean values (spaces, case, type) before checking them.
9. Choose between `in`, `find()`, and `count()`, and between a list and a set for membership tests.

---

## 1. Introduction

### 1.1 A very common question

Programs constantly ask questions like:

- Is this day a **weekend** day?
- Is this user **allowed** to log in?
- Does this email address contain an **@**?
- Is this course **offered** this semester?
- Is this item **sold out**?

All of these are the same kind of question: **"Is this value one of those?"** or **"Is this text inside that text?"**

### 1.2 Without in

With only `==` and `or`, the code quickly becomes long:

```python
day = "Sat"
if day == "Fri" or day == "Sat":
    print("Weekend")
```

```text
Weekend
```

That works for two values. But checking a student ID against a class list of 200 students this way would be impossible to write and read.

### 1.3 With in

```python
day = "Sat"
if day in ("Fri", "Sat"):
    print("Weekend")
```

```text
Weekend
```

The `in` operator asks the question directly: *"Is `day` in this group?"* The code is short, clear, and works for any number of values.

You have already seen `in` briefly in earlier lectures. This lecture studies it carefully, so you know exactly what it checks in each situation.

---

## 2. Main Concepts and Vocabulary

| Term | Meaning | Example |
|---|---|---|
| **Operator** | A symbol or word that works on values | `+`, `==`, `and`, `in` |
| **Membership operator** | An operator that checks whether a value is inside something | `in`, `not in` |
| **Container** | A value that holds other values: string, list, tuple, set | `["a", "b"]` |
| **Member** | A value that is inside the container | `"a"` is a member of `["a", "b"]` |
| **Substring** | A piece of text inside a string | `"wa"` in `"Kuwait"` |
| **Boolean** | The type of `True` and `False` | `"a" in "cat"` → `True` |

---

## 3. Syntax and Result

### 3.1 General form

```text
value in container
value not in container
```

| Expression | Meaning | Result |
|---|---|---|
| `x in c` | Is `x` inside `c`? | `True` or `False` |
| `x not in c` | Is `x` **not** inside `c`? | `True` or `False` |

```python
print("a" in "cat")
print("z" in "cat")
print("z" not in "cat")
```

```text
True
False
True
```

### 3.2 Important points

- The result is always a **Boolean**: `True` or `False`.
- `not in` is written as **two words**, but it is **one** operator. It always gives the opposite of `in`.
- Because the result is a Boolean, you can use it anywhere a condition is allowed: in an `if`, in a variable, or with `and`, `or`, `not`.

```python
gcc = ("Kuwait", "Qatar", "Oman")
answer = "Qatar" in gcc
print(answer)
print(type(answer))
```

```text
True
<class 'bool'>
```

---

## 4. in with Strings

### 4.1 Looking for a substring

When the right side is a **string**, `in` checks whether the left side appears **as a piece of text** anywhere inside it:

```python
city = "Kuwait City"
print("K" in city)
print("wait" in city)
print("City" in city)
print(" " in city)
```

```text
True
True
True
True
```

The left side can be one character or several characters.

### 4.2 The characters must be together and in order

```python
city = "Kuwait City"
print("Ku City" in city)
print("tiaw" in city)
print("t C" in city)
```

```text
False
False
True
```

- `"Ku City"` is not there: in the real string, `"wait "` comes between `"Ku"` and `"City"`.
- `"tiaw"` has the right letters but in the wrong order.
- `"t C"` appears: the `t` at the end of "Kuwait", a space, and the `C` of "City".

### 4.3 Case matters

```python
city = "Kuwait City"
print("city" in city)
print("city" in city.lower())
```

```text
False
True
```

To search without caring about capital letters, convert the string (and the search text) to the same case first.

### 4.4 The empty string

The empty string `""` is considered to be inside **every** string:

```python
print("" in "Kuwait")
print("" in "")
```

```text
True
True
```

You will rarely need this, but it can surprise you when a variable is unexpectedly empty.

### 4.5 Both sides must be strings

```text
year = "2026"
print(6 in year)

TypeError: 'in <string>' requires string as left operand, not int
```

To search a string, the value on the left must also be a string:

```python
year = "2026"
print("6" in year)
print(str(6) in year)
```

```text
True
True
```

### 4.6 Checking one character against a group

A string of allowed characters is a quick way to test **one** character:

```python
ch = "e"
print(ch in "aeiou")
d = "7"
print(d in "0123456789")
op = "*"
print(op in "+-*/")
```

```text
True
True
True
```

---

## 5. in with Lists, Tuples, and Sets

### 5.1 Looking for a whole item

When the right side is a **list**, **tuple**, or **set**, `in` checks whether **some item is equal (`==`)** to the value:

```python
gcc = ["Kuwait", "Qatar", "Oman"]
print("Qatar" in gcc)
print("Iraq" in gcc)
print("Iraq" not in gcc)
```

```text
True
False
True
```

### 5.2 Whole items only — not parts of items

```python
gcc = ["Kuwait", "Qatar", "Oman"]
print("Qat" in gcc)
print("man" in gcc)
```

```text
False
False
```

No item is **equal** to `"Qat"` or `"man"`. `in` does not search **inside** the strings that are items of the list.

### 5.3 Case and type matter

`in` uses `==`, so the value must be exactly equal to an item:

```python
gcc = ["Kuwait", "Qatar", "Oman"]
print("qatar" in gcc)
marks = [85, 92, 78]
print(92 in marks)
print("92" in marks)
```

```text
False
True
False
```

One small detail: because `in` uses `==`, a whole number and a float with the same value match, since `1 == 1.0` is `True`:

```python
print(1 in [1.0, 2.5])
```

```text
True
```

### 5.4 Tuples

Tuples behave exactly like lists for `in`:

```python
weekend = ("Fri", "Sat")
print("Sat" in weekend)
print("Sun" not in weekend)
point = (29, 47)
print(47 in point)
```

```text
True
True
True
```

### 5.5 Sets: the best for membership

```python
allowed = {"sara", "ali", "mona"}
print("ali" in allowed)
print("fahad" not in allowed)
```

```text
True
True
```

The answer is the same as with a list, but the **speed** is very different:

- A **list** or **tuple** checks its items **one by one** until it finds a match. With a million items, a "not found" answer needs a million comparisons.
- A **set** is organized so that it can answer **almost instantly**, whatever its size.

So when the main job of a collection is to answer "is it there?" many times, store it in a **set**.

### 5.6 Strings vs collections: the key difference

This is the most important idea in the lecture:

```python
print("wa" in "Kuwait")
print("wa" in ["Kuwait"])
print("Kuwait" in ["Kuwait"])
print("wa" in ["Kuwait"][0])
```

```text
True
False
True
True
```

| Right side | `in` checks… |
|---|---|
| a **string** | whether the text appears **anywhere inside** it |
| a **list, tuple, or set** | whether an **item is equal** to the value |

In the last line, `["Kuwait"][0]` is the **string** `"Kuwait"`, so `in` searches for text again.

**Before using `in`, always ask: what type is on the right side?**

---

## 6. Collections Inside Collections

`in` only looks at the **direct** items of a collection. It does not look inside inner lists:

```python
data = [[1, 2], [3, 4]]
print([1, 2] in data)
print(1 in data)
print(1 in data[0])
print((1, 2) in data)
```

```text
True
False
True
False
```

- The items of `data` are the two lists `[1, 2]` and `[3, 4]`.
- `[1, 2]` is equal to the first item → `True`.
- `1` is **inside** an item, but it is not an item itself → `False`.
- `data[0]` is the list `[1, 2]`, and `1` is one of its items → `True`.
- A tuple is never equal to a list → `False`.

Another example with a tuple:

```python
t = ("a", ["b", "c"], "d")
print("b" in t)
print(["b", "c"] in t)
print("c" in t[1])
```

```text
False
True
True
```

---

## 7. not in

### 7.1 The opposite of in

```python
banned = {"spam", "scam"}
word = "hello"
print(word not in banned)
```

```text
True
```

| `x in c` | `x not in c` |
|---|---|
| `True` | `False` |
| `False` | `True` |

### 7.2 Three ways to write the same thing

```python
banned = {"spam", "scam"}
word = "hello"
print(word not in banned)
print(not word in banned)
print(not (word in banned))
```

```text
True
True
True
```

All three are correct, but `word not in banned` is the **preferred** style. It reads like English and is the easiest to understand.

---

## 8. in and not in with if Statements

### 8.1 Basic use

```python
weekend = ("Fri", "Sat")
day = "Mon"
if day in weekend:
    print("Enjoy your weekend")
else:
    print("Have a good work day")
```

```text
Have a good work day
```

### 8.2 With elif

```python
offered = ("CS126", "MATH101", "ENG110")
full = {"MATH101"}
course = "MATH101"
if course not in offered:
    print(course, "is not offered")
elif course in full:
    print(course, "is full")
else:
    print("Registered in", course)
```

```text
MATH101 is full
```

Walkthrough:

1. `"MATH101" not in offered` → `False` (it is offered), so skip.
2. `"MATH101" in full` → `True`, so print that it is full.

A big advantage: to change which courses are offered or full, you change only the **data** (the tuple and the set). The `if` statement stays the same.

---

## 9. Combining with and, or, not

### 9.1 Several conditions

```python
email = "sara@ku.edu.kw"
ok = "@" in email and "." in email
ok = ok and " " not in email
print(ok)
```

```text
True
```

```python
students = {"sara", "ali", "mona"}
blocked = {"ali"}
user = "ali"
if user in students and user not in blocked:
    print("Welcome")
else:
    print("Access denied")
```

```text
Access denied
```

`in` and `not in` are evaluated **before** `and`, `or`, and `not`, so no brackets are needed in these conditions.

### 9.2 Saving results in Boolean variables

A long condition is easier to read when each part has a clear name:

```python
age_group = "child"
day = "Tue"
is_discount = age_group in ("child", "student", "senior")
is_offer_day = day in {"Mon", "Tue"}
price = 3.5
if is_discount or is_offer_day:
    price = 2
print(is_discount, is_offer_day)
print("Ticket:", price, "KD")
```

```text
True True
Ticket: 2 KD
```

Names that start with `is_` or `has_` make it clear that the variable holds `True` or `False`.

---

## 10. Replacing Long or Chains

### 10.1 The improvement

```python
code = "QA"
if code == "KW" or code == "SA" or code == "QA" or code == "AE":
    print("GCC country")
```

```text
GCC country
```

can be written as:

```python
code = "QA"
gcc = {"KW", "SA", "QA", "AE", "BH", "OM"}
if code in gcc:
    print("GCC country")
```

```text
GCC country
```

The `in` version is shorter, easier to read, and easier to update: adding a new code means adding one item to the set.

### 10.2 The or trap

A very common beginner mistake is to write:

```python
day = "Mon"
if day == "Fri" or "Sat":
    print("Weekend")
```

```text
Weekend
```

It prints `Weekend` even though the day is Monday! Python reads the condition as:

```text
(day == "Fri") or ("Sat")
```

The left part is `False`, but the right part is just the string `"Sat"`. In a condition, any **non-empty string counts as True**, so the whole condition is always `True`.

**Correct versions:**

```python
day = "Mon"
if day == "Fri" or day == "Sat":
    print("Weekend")
if day in ("Fri", "Sat"):
    print("Weekend")
print("done")
```

```text
done
```

The same trap happens with `in`:

```python
ch = "x"
if ch in "a" or "e":
    print("vowel?")
```

```text
vowel?
```

Again, `"e"` alone counts as `True`. The correct check is `ch in "ae"` (or `ch in ("a", "e")`).

---

## 11. Clean First, Then Check

`in` needs an **exact** match. Text typed by users often has extra spaces or different capital letters:

```python
answer = "  YES "
print(answer in ("yes", "no"))
clean = answer.strip().lower()
print(clean in ("yes", "no"))
```

```text
False
True
```

A good habit:

1. Store the allowed values in **one** style (for example, all small letters).
2. **Clean** the value to the same style with `strip()` and `lower()` (or `title()`, `upper()`).
3. Then use `in`.

```python
cities = ["Kuwait", "Doha", "Muscat"]
city = "  kuwait "
print(city.strip().title() in cities)
```

```text
True
```

Types must also match. If you have a number but the collection holds strings, convert first:

```python
ids = ["101", "102", "103"]
student_id = 102
print(student_id in ids)
print(str(student_id) in ids)
```

```text
False
True
```

---

## 12. in Compared with find() and count()

| Question | Best tool | Result |
|---|---|---|
| Is it there? (yes / no) | `in` | `True` / `False` |
| Where is it? | `find()` / `index()` | a position |
| How many times? | `count()` | a number |

```python
s = "banana"
print("an" in s)
print(s.find("an"))
print(s.count("an"))
names = ["Ali", "Sara", "Ali"]
print("Ali" in names)
print(names.count("Ali"))
```

```text
True
1
2
True
2
```

For a yes/no question, `in` is the clearest choice. `s.find(x) != -1` and `s.count(x) > 0` give the same answer but are harder to read.

---

## 13. Worked Examples

### 13.1 Checking an email address

```python
email = "Sara.Ali@KU.edu.kw".strip().lower()
has_at = "@" in email
has_space = " " in email
kuwaiti = ".kw" in email[-3:]
if not has_at or has_space:
    print("Invalid email")
elif kuwaiti:
    print("Valid Kuwaiti email:", email)
else:
    print("Valid email:", email)
```

```text
Valid Kuwaiti email: sara.ali@ku.edu.kw
```

1. The email is cleaned first.
2. `has_at` is `True` and `has_space` is `False`, so `not has_at or has_space` is `False`.
3. The last three characters are `".kw"`, so the address is Kuwaiti.

### 13.2 A café order

```python
menu = ("tea", "coffee", "karak", "juice")
sold_out = {"juice"}
sizes = ("S", "M", "L")
drink = " Karak ".strip().lower()
size = "XL"
if drink not in menu:
    print("Sorry,", drink, "is not on the menu")
elif drink in sold_out:
    print("Sorry,", drink, "is sold out")
elif size not in sizes:
    print("Please choose size S, M, or L")
else:
    print("Order:", size, drink)
```

```text
Please choose size S, M, or L
```

A **tuple** holds the fixed menu and sizes; a **set** holds the sold-out items, which change during the day.

### 13.3 Password rules (without loops)

```python
pw = "Kuwait2026"
common = ["123456", "password", "qwerty"]
digits = set("0123456789")
has_digit = len(set(pw) & digits) > 0
has_upper = pw.lower() != pw
too_common = pw.lower() in common
has_name = "kuwait" in pw.lower()
print(has_digit, has_upper, too_common, has_name)
if too_common or not has_digit or not has_upper:
    print("Weak password")
elif has_name:
    print("OK, but avoid place names")
else:
    print("Strong password")
```

```text
True True False True
OK, but avoid place names
```

- `pw.lower() in common` uses `in` with a **list**: is the whole password one of the common ones?
- `"kuwait" in pw.lower()` uses `in` with a **string**: does the password contain this text?
- To check "does the password contain **any** digit?" without a loop, we use a **set intersection**: the characters of the password that are also digits. If that set is not empty, there is at least one digit.

### 13.4 A phone shop

```python
available = {"Galaxy", "iPhone", "Pixel"}
out_of_stock = ["Pixel"]
model = "  galaxy ".strip().title()
if model not in available:
    print("We do not sell this model")
elif model in out_of_stock:
    print("Out of stock")
else:
    print("Available")
```

```text
Available
```

---

## 14. Quick Reference

| Container | `in` checks | Example | Result |
|---|---|---|---|
| string | substring (text) | `"wa" in "Kuwait"` | `True` |
| string | case-sensitive | `"WA" in "Kuwait"` | `False` |
| string | empty string | `"" in "Kuwait"` | `True` |
| list | whole item (`==`) | `"Qat" in ["Qatar"]` | `False` |
| list | type matters | `"92" in [92]` | `False` |
| tuple | whole item (`==`) | `"Sat" in ("Fri", "Sat")` | `True` |
| set | whole item, fastest | `"ali" in {"ali", "sara"}` | `True` |
| nested list | outer items only | `1 in [[1, 2]]` | `False` |
| any | opposite of `in` | `"x" not in "abc"` | `True` |

---

## 15. Important Notes

- `in` and `not in` always return `True` or `False`.
- With a **string** on the right, `in` searches for **text**; both sides must be strings.
- With a **list, tuple, or set**, `in` searches for an **equal item**.
- `in` does not search inside inner lists or inside the strings stored in a list.
- Matching is **exact**: capital letters, spaces, and types all matter.
- Prefer `x not in c` over `not x in c`.
- `x in (a, b)` is the correct short form of `x == a or x == b`. Never write `x == a or b`.
- For many membership tests on a large collection, use a **set**.

---

## 16. Common Mistakes

### Mistake 1: The or trap

**Incorrect**

```python
day = "Mon"
if day == "Fri" or "Sat":
    print("Weekend")
```

```text
Weekend
```

**Correct**

```python
day = "Mon"
if day in ("Fri", "Sat"):
    print("Weekend")
else:
    print("Work day")
```

```text
Work day
```

### Mistake 2: Expecting a substring search in a list

**Incorrect** (goal: does any name contain `"man"`?)

```python
gcc = ["Kuwait", "Oman", "Qatar"]
print("man" in gcc)
```

```text
False
```

**Why?** With a list, `in` looks for a **whole item** equal to `"man"`.

**Correct** — search inside a specific item:

```python
gcc = ["Kuwait", "Oman", "Qatar"]
print("man" in gcc[1])
```

```text
True
```

(Checking every item needs a loop, which you will learn later.)

### Mistake 3: Wrong case or extra spaces

**Incorrect**

```python
cities = ["Kuwait", "Doha"]
city = "kuwait "
print(city in cities)
```

```text
False
```

**Correct**

```python
cities = ["Kuwait", "Doha"]
city = "kuwait "
print(city.strip().title() in cities)
```

```text
True
```

### Mistake 4: Number vs string

**Incorrect**

```python
ids = ["101", "102", "103"]
print(102 in ids)
```

```text
False
```

**Correct**

```python
ids = ["101", "102", "103"]
print("102" in ids)
```

```text
True
```

### Mistake 5: A number on the left of a string search

**Incorrect**

```text
year = "2026"
print(6 in year)

TypeError: 'in <string>' requires string as left operand, not int
```

**Correct**

```python
year = "2026"
print("6" in year)
```

```text
True
```

### Mistake 6: Expecting in to look inside inner lists

**Incorrect**

```python
data = [[1, 2], [3, 4]]
print(3 in data)
```

```text
False
```

**Correct**

```python
data = [[1, 2], [3, 4]]
print(3 in data[1])
```

```text
True
```

### Mistake 7: Writing not in the confusing way

**Works, but harder to read**

```python
banned = {"spam"}
word = "hello"
if not word in banned:
    print("OK")
```

```text
OK
```

**Better style**

```python
banned = {"spam"}
word = "hello"
if word not in banned:
    print("OK")
```

```text
OK
```

---

## 17. Mini Practice Questions

Try these before looking at the answers at the end of this section.

**Q1.** What does this print?

```python
print("cat" in "concatenate", "cat" in ["concatenate"])
```

**Q2.** What does this print?

```python
nums = (1, 2, 3)
print(3 in nums, 3.0 in nums, "3" in nums)
```

**Q3.** Rewrite using `in`: `if x == 1 or x == 3 or x == 5:`

**Q4.** What does this print?

```python
s = {"a", "b"}
print("a" not in s, "c" not in s)
```

**Q5.** What does this print, and why?

```python
grade = "C"
if grade == "A" or "B":
    print("Excellent")
else:
    print("Keep trying")
```

**Q6.** What does this print?

```python
t = ("x", ("y", "z"))
print("y" in t, ("y", "z") in t, "z" in t[1])
```

### Answers to Mini Practice

1. **`True False`** — `"concatenate"` contains the text `"cat"`, but the list does not contain an item equal to `"cat"`.
2. **`True True False`** — `3 == 3.0`, but the string `"3"` is not equal to the number 3.
3. **`if x in (1, 3, 5):`**
4. **`False True`**
5. **`Excellent`** — the condition is `(grade == "A") or "B"`, and `"B"` alone counts as `True`. Correct: `if grade in ("A", "B"):`.
6. **`False True True`**

---

## 18. Ask AI to Help You Understand

```text
Explain the Python in and not in operators to a beginner.
Show how in behaves differently with a string and with a list,
using the word "Kuwait". Do not use loops or dictionaries, and do not give me exercises yet.
```

```text
Why does  if day == "Fri" or "Sat":  always run in Python?
Explain step by step what Python evaluates, and show two correct versions.
```

```text
Why is checking membership in a set faster than in a list?
Explain it simply with an everyday comparison, without technical details.
```

```text
Give me five "predict the output" questions about in and not in with
strings, lists, tuples, and sets. Give hints first and do not show the
answers unless I ask.
```

> **Remember:** Always run the code yourself. AI can make mistakes, and running code is the only way to be sure.

---

## 19. Summary

- `in` and `not in` are **membership operators**. They return `True` or `False`.
- With a **string**, `x in s` is `True` when the text `x` appears somewhere inside `s` (characters together and in order). Both sides must be strings.
- With a **list, tuple, or set**, `x in c` is `True` when some item is **equal** to `x`. It does not look inside items or inner lists.
- Matching is exact: **case**, **spaces**, and **type** matter. Clean the value first.
- `not in` is the opposite of `in`; it is the preferred way to write "not inside".
- Use `in` in `if` statements and with `and`, `or`, `not`; store results in clearly named Boolean variables.
- Replace `x == a or x == b` with `x in (a, b)`, and never write `x == a or b`.
- **Sets** give the fastest membership tests.

---

## Basic Exercises

> Exercises 1–12 are the same as in the slides. Exercises 13–16 are extra practice.

**Exercise 1.** Predict the output.

```python
s = "Kuwait City"
print("City" in s, "city" in s)
print("K" in s, " " not in s)
```

**Exercise 2.** Predict the output.

```python
nums = [1, 2, 3]
print(2 in nums, "2" in nums, 4 not in nums)
```

**Exercise 3.** This prints `Weekend` for Monday! Find the problem and fix it using `in`.

```python
day = "Mon"
if day == "Fri" or "Sat":
    print("Weekend")
```

**Exercise 4.** Predict the output.

```python
gcc = ["Kuwait", "Qatar"]
print("Kuwait" in gcc, "Kuw" in gcc)
print("Kuw" in gcc[0])
```

**Exercise 13.** Predict the output.

```python
t = ("Fri", "Sat")
print("fri" in t, "Fri" in t)
print("Fr" in t, "Fr" in t[0])
```

## Practice Exercises

**Exercise 5.** For `email = "sara@ku.edu.kw"`, print `Valid` if it contains `"@"` and `"."` and has no spaces; otherwise `Invalid`.

**Exercise 6.** For `ch = "E"`, print `vowel` or `consonant`, ignoring case, using `in`.

**Exercise 7.** Rewrite this condition using `in`.

```text
if (color == "red" or
        color == "green" or
        color == "blue"):
    print("Primary light color")
```

**Exercise 8.** Explain both results and give the output.

```python
allowed = {"ali", "sara"}
user = " Ali "
print(user in allowed)
print(user.strip().lower() in allowed)
```

**Exercise 14.** The GCC country codes are stored as `gcc = {"KW", "SA", "QA", "AE", "BH", "OM"}`. A user typed `code = "  qa "`. Clean the input and print `GCC` or `Not GCC`.

## Challenge Exercises

**Exercise 9.** Print the right message for `course = "MATH101"`: *not offered*, *already taken*, *full*, or *registered* (check in that order).

```python
offered = ("CS126", "MATH101", "ENG110")
taken = ["CS126"]
full = {"ENG110"}
```

**Exercise 10.** Predict the output.

```python
data = [[1, 2], [3, 4]]
print([1, 2] in data, 1 in data)
print(1 in data[0], (1, 2) in data)
```

**Exercise 11.** Without loops, check `pw = "kuwait2026"`: does it contain a digit? a capital letter? Print `Strong` only if it has both and at least 8 characters; otherwise `Weak`.

**Exercise 12.** Predict the output.

```python
s = "banana"
print("an" in s, "nab" in s, "" in s)
print("a" in s and "z" not in s)
```

**Exercise 15.** A list of ticket numbers is stored as numbers: `tickets = [1001, 1005, 1010]`. A customer types a ticket number as text: `typed = "1005"`. Print whether the ticket is valid.

**Exercise 16.** Without loops, print whether the word `"rhythm"` contains **no vowels** at all. (Hint: use a set intersection with `set("aeiou")`.)

---

# Exercise Solutions

### Solution 1

`"City"` appears; `"city"` with a small `c` does not. `"K"` appears, and the string does contain a space, so `" " not in s` is `False`.

```text
True False
True False
```

### Solution 2

The number `2` is an item. The string `"2"` is not equal to the number 2. `4` is not in the list.

```text
True False True
```

### Solution 3

Python reads the condition as `(day == "Fri") or "Sat"`. The string `"Sat"` alone counts as `True`, so the condition is always `True`. Use `in`:

```python
day = "Mon"
if day in ("Fri", "Sat"):
    print("Weekend")
else:
    print("Work day")
```

```text
Work day
```

### Solution 4

`"Kuwait"` is a whole item. `"Kuw"` is not an item, but it is text inside the string `gcc[0]`.

```text
True False
True
```

### Solution 5

```python
email = "sara@ku.edu.kw"
ok = "@" in email and "." in email
if ok and " " not in email:
    print("Valid")
else:
    print("Invalid")
```

```text
Valid
```

### Solution 6

```python
ch = "E"
if ch.lower() in "aeiou":
    print("vowel")
else:
    print("consonant")
```

```text
vowel
```

### Solution 7

```python
color = "green"
if color in ("red", "green", "blue"):
    print("Primary light color")
```

```text
Primary light color
```

### Solution 8

`" Ali "` has spaces and a capital letter, so it is not exactly equal to any item → `False`. After `strip().lower()`, it becomes `"ali"`, which is in the set → `True`.

```text
False
True
```

### Solution 9

```python
offered = ("CS126", "MATH101", "ENG110")
taken = ["CS126"]
full = {"ENG110"}
course = "MATH101"
if course not in offered:
    print("Not offered")
elif course in taken:
    print("Already taken")
elif course in full:
    print("Full")
else:
    print("Registered in", course)
```

```text
Registered in MATH101
```

### Solution 10

`[1, 2]` is an item of `data`. `1` is only inside an item. `data[0]` is `[1, 2]`, which contains `1`. A tuple is never equal to a list.

```text
True False
True False
```

### Solution 11

```python
pw = "kuwait2026"
digits = set("0123456789")
has_digit = len(set(pw) & digits) > 0
has_upper = pw.lower() != pw
print(has_digit, has_upper)
if has_digit and has_upper and len(pw) >= 8:
    print("Strong")
else:
    print("Weak")
```

```text
True False
Weak
```

`set(pw) & digits` contains the digits that appear in the password (`{'2', '0', '6'}`), so it is not empty. `pw.lower()` is the same as `pw`, so there are no capital letters.

### Solution 12

`"an"` and `""` are inside `"banana"`; `"nab"` is not. `"a"` is inside and `"z"` is not, so `True and True` is `True`.

```text
True False True
True
```

### Solution 13

`"fri"` is not equal to `"Fri"` (case). `"Fr"` is not a whole item of the tuple, but it is text inside the string `t[0]`.

```text
False True
False True
```

### Solution 14

```python
gcc = {"KW", "SA", "QA", "AE", "BH", "OM"}
code = "  qa "
if code.strip().upper() in gcc:
    print("GCC")
else:
    print("Not GCC")
```

```text
GCC
```

### Solution 15

The list holds numbers, so the typed text must be converted with `int()`:

```python
tickets = [1001, 1005, 1010]
typed = "1005"
print(typed in tickets)
print(int(typed) in tickets)
```

```text
False
True
```

### Solution 16

```python
word = "rhythm"
shared = set(word) & set("aeiou")
print(len(shared) == 0)
```

```text
True
```

The intersection contains the vowels that appear in the word. It is empty, so the word has no vowels.

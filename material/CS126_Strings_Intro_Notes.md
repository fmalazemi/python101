# CS126 – Introduction to Python

## Introduction to Strings

**Instructor:** Dr. Fawaz Alazemi

---

## Learning Objectives

After studying these notes, you should be able to:

1. Explain what a string is and create strings with single, double, and triple quotes.
2. Put quotes and special characters inside strings using escape sequences such as `\n`, `\t`, `\"`, and `\\`.
3. Find the length of a string with `len()`.
4. Join strings with `+` and repeat them with `*`.
5. Explain the difference between `"5"` and `5`, and convert with `str()`, `int()`, and `float()`.
6. Read one character with an **index** (positive or negative) and avoid `IndexError`.
7. Take part of a string with **slicing**: `s[start:stop:step]`.
8. Explain why strings are **immutable** and how to build a new string instead.
9. Use `in`, `not in`, `==`, `!=`, `<`, and `>` with strings inside `if` statements.
10. Use common string methods: `upper`, `lower`, `title`, `capitalize`, `strip`, `replace`, `find`, `count`, `startswith`, `endswith`, `isdigit`, `isalpha`, `isupper`, and `islower`.

---

## 1. Introduction

### 1.1 Text is everywhere

So far, most of your programs have worked with **numbers**. But a huge part of real data is **text**:

- names of students and cities,
- email addresses and passwords,
- phone numbers and civil ID numbers,
- course codes such as `CS126`,
- messages shown to the user.

In Python, text is stored as a **string**. Strings are one of the most used data types in all of programming.

### 1.2 What is a string?

A **string** is a **sequence of characters** written inside quotes. A **character** is one symbol: a letter (`a`, `K`), a digit (`7`), a space, or a symbol (`@`, `-`, `!`).

```python
name = "Sara"
city = 'Kuwait City'
course = "CS126"
print(name, city, course)
print(type(name))
```

```text
Sara Kuwait City CS126
<class 'str'>
```

The type name for strings in Python is `str`.

Notice that `"CS126"` contains digits, but it is still a string, because it is inside quotes. Python treats it as **text**, not as a number.

---

## 2. Main Concepts and Vocabulary

| Term | Meaning | Example |
|---|---|---|
| **String** | A sequence of characters in quotes | `"Kuwait"` |
| **Character** | One symbol in a string | `"K"` |
| **Empty string** | A string with no characters | `""` |
| **Length** | Number of characters | `len("Oman")` is 4 |
| **Concatenation** | Joining strings with `+` | `"Ku" + "wait"` |
| **Index** | Position of a character, starting at 0 | `"Oman"[0]` is `"O"` |
| **Slice** | A part of a string | `"Kuwait"[0:3]` is `"Kuw"` |
| **Substring** | A string that appears inside another | `"wa"` in `"Kuwait"` |
| **Escape sequence** | A backslash code for a special character | `\n` (new line) |
| **Immutable** | Cannot be changed after it is created | strings |
| **Method** | A function that belongs to a value, called with a dot | `"abc".upper()` |

---

## 3. Creating Strings

### 3.1 Single and double quotes

Python accepts **single quotes** `'...'` and **double quotes** `"..."`. They work exactly the same:

```python
a = "Kuwait"
b = 'Kuwait'
print(a == b)
```

```text
True
```

The quotes only mark where the string **starts** and **ends**. They are not part of the text, so `print()` does not show them.

Choose one style and use it consistently. In these notes we use double quotes.

### 3.2 The empty string

```python
empty = ""
print(len(empty))
print("[" + empty + "]")
```

```text
0
[]
```

The empty string has no characters. It is useful as a starting value, or to check whether the user typed anything.

### 3.3 Quotes inside a string

If your text contains a quote character, you have two options.

**Option 1:** use the **other** kind of quote around the string:

```python
print("It's hot in Kuwait")
print('He said "Welcome"')
```

```text
It's hot in Kuwait
He said "Welcome"
```

**Option 2:** put a **backslash** `\` before the inner quote:

```python
print("He said \"Welcome\"")
print('It\'s hot')
```

```text
He said "Welcome"
It's hot
```

### 3.4 Escape sequences

A backslash followed by a letter creates a special character. These are called **escape sequences**:

| Write | Meaning |
|---|---|
| `\n` | new line |
| `\t` | tab (a wide space, useful for columns) |
| `\"` | a double quote |
| `\'` | a single quote |
| `\\` | one backslash |

```python
print("Kuwait\nDoha\nMuscat")
print("C:\\Users\\Sara")
```

```text
Kuwait
Doha
Muscat
C:\Users\Sara
```

Each escape sequence counts as **one** character, even though you type two symbols:

```python
print(len("Hi\n"))
```

```text
3
```

### 3.5 Triple quotes for text on several lines

Three quotes (`"""` or `'''`) let a string continue over several lines:

```python
message = """Dear student,
Your exam is on Sunday.
Good luck!"""
print(message)
```

```text
Dear student,
Your exam is on Sunday.
Good luck!
```

---

## 4. Length: len()

`len()` gives the number of characters in a string. **Every** character counts: letters, digits, spaces, and symbols.

```python
print(len("Kuwait"))
print(len("Kuwait City"))
print(len("CS 126!"))
print(len(""))
```

```text
6
11
7
0
```

`"Kuwait City"` has 11 characters: 6 letters, 1 space, and 4 letters.

`len()` is often used with `if` to check input:

```python
password = "abc12"
if len(password) < 8:
    print("Password must have at least 8 characters")
```

```text
Password must have at least 8 characters
```

---

## 5. Joining and Repeating Strings

### 5.1 Concatenation with +

The `+` operator **joins** two strings into a new string. This is called **concatenation**.

```python
first = "Fawaz"
last = "Alazemi"
print(first + last)
print(first + " " + last)
print("Dr. " + first + " " + last)
```

```text
FawazAlazemi
Fawaz Alazemi
Dr. Fawaz Alazemi
```

`+` does **not** add a space automatically. If you want a space, you must add `" "` yourself.

### 5.2 `+` versus commas in print()

When you give `print()` several values separated by **commas**, it puts a space between them automatically. With `+`, you build one string, and you control every space.

```python
first = "Fawaz"
last = "Alazemi"
print(first, last)
print(first + last)
```

```text
Fawaz Alazemi
FawazAlazemi
```

### 5.3 Repetition with *

The `*` operator repeats a string a whole number of times:

```python
print("Ha" * 3)
print("-" * 20)
print("=" * 3 + " Menu " + "=" * 3)
```

```text
HaHaHa
--------------------
=== Menu ===
```

As in math, `*` is done **before** `+`:

```python
print("ab" * 2 + "c")
```

```text
ababc
```

Repeating 0 times (or a negative number of times) gives the empty string.

---

## 6. Strings and Numbers

### 6.1 `"5"` is not `5`

`5` is a **number**. `"5"` is a **string** containing the character 5. They behave very differently:

```python
print(5 + 3)
print("5" + "3")
print("5" * 3)
print(5 * 3)
```

```text
8
53
555
15
```

- With numbers, `+` **adds** and `*` **multiplies**.
- With strings, `+` **joins** and `*` **repeats**.

### 6.2 Mixing strings and numbers with + is an error

```text
age = 20
print("Age: " + age)

TypeError: can only concatenate str (not "int") to str
```

Python does not guess whether you want to add or join, so it stops with an error.

### 6.3 Converting

| Function | Converts | Example | Result |
|---|---|---|---|
| `str(x)` | anything → string | `str(20)` | `"20"` |
| `int(x)` | string of digits → integer | `int("20")` | `20` |
| `float(x)` | string of a number → float | `float("2.5")` | `2.5` |

```python
age = 20
print("Age: " + str(age))
print(int("5") + int("3"))
print(float("1.5") * 2)
```

```text
Age: 20
8
3.0
```

`int()` only works if the string looks like a whole number. `int("abc")` and `int("2.5")` cause a `ValueError`.

### 6.4 `input()` always gives a string

When a user types something, `input()` returns it as a **string**, even if they typed digits. Convert it before doing math:

<!-- inputs: 7 -->
```python
qty = input("How many items? ")
print(qty * 2)
print(int(qty) * 2)
```

```text
How many items? 7
77
14
```

---

## 7. Indexing: One Character at a Time

### 7.1 Positive indexes

Every character in a string has a position number called an **index**. The first index is **0**:

| Character | K | u | w | a | i | t |
|---|---|---|---|---|---|---|
| Index | 0 | 1 | 2 | 3 | 4 | 5 |

```python
word = "Kuwait"
print(word[0])
print(word[3])
print(word[5])
```

```text
K
a
t
```

Each result is itself a string of length 1. You can join it with `+`:

```python
code = "CS126"
print(code[2] + code[-1])
```

```text
16
```

Notice: `"1" + "6"` is `"16"`, not 7, because these are strings.

### 7.2 Negative indexes

You can also count from the **end**. The last character is −1:

| Character | K | u | w | a | i | t |
|---|---|---|---|---|---|---|
| Positive index | 0 | 1 | 2 | 3 | 4 | 5 |
| Negative index | −6 | −5 | −4 | −3 | −2 | −1 |

```python
word = "Kuwait"
print(word[-1])
print(word[-2])
print(word[len(word) - 1])
```

```text
t
i
t
```

`word[-1]` and `word[len(word) - 1]` are the same, but `-1` is shorter and works for any length.

### 7.3 IndexError

Using an index that does not exist stops the program:

```text
word = "Kuwait"
print(word[6])

IndexError: string index out of range
```

For a string of length `n`, the valid positive indexes are `0` to `n - 1`, and the valid negative indexes are `-1` to `-n`. The empty string has no valid index.

---

## 8. Slicing: Part of a String

### 8.1 Basic slices

`s[start:stop]` gives the characters from `start` up to, but **not including**, `stop`:

```python
city = "Kuwait City"
print(city[0:6])
print(city[7:11])
print(city[2:4])
```

```text
Kuwait
City
wa
```

Index table for `"Kuwait City"`:

| K | u | w | a | i | t | (space) | C | i | t | y |
|---|---|---|---|---|---|---|---|---|---|---|
| 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 |

`city[7:11]` takes indexes 7, 8, 9, 10 → `"City"`. The number of characters is `stop − start`, here 11 − 7 = 4.

### 8.2 Leaving out start or stop

```python
code = "KWT-2026"
print(code[:3])
print(code[4:])
print(code[-4:])
print(code[:-5])
```

```text
KWT
2026
2026
KWT
```

| Slice | Meaning |
|---|---|
| `s[:n]` | the first `n` characters |
| `s[n:]` | from index `n` to the end |
| `s[-n:]` | the last `n` characters |
| `s[:-n]` | everything except the last `n` characters |
| `s[:]` | the whole string |

### 8.3 Step

A third number gives the **step**:

```python
code = "KWT-2026"
print(code[::2])
print(code[1::2])
print(code[::-1])
```

```text
KT22
W-06
6202-TWK
```

- `code[::2]` takes indexes 0, 2, 4, 6 → `K`, `T`, `2`, `2`.
- `code[1::2]` takes indexes 1, 3, 5, 7 → `W`, `-`, `0`, `6`.
- `code[::-1]` walks backwards → the reversed string.

### 8.4 Slices never cause IndexError

If a slice goes past the end, Python just stops at the end:

```python
city = "Kuwait City"
print(city[7:100])
print("[" + city[20:] + "]")
```

```text
City
[]
```

---

## 9. Strings Are Immutable

### 9.1 You cannot change a character

```text
word = "cat"
word[0] = "b"

TypeError: 'str' object does not support item assignment
```

Strings are **immutable**: once a string is created, its characters cannot be changed.

### 9.2 Build a new string instead

```python
word = "cat"
word = "b" + word[1:]
print(word)
```

```text
bat
```

What happened:

1. `word[1:]` is `"at"`.
2. `"b" + "at"` creates a **new** string `"bat"`.
3. The name `word` now refers to the new string. The old `"cat"` was never changed.

### 9.3 Why this matters for methods

Because strings cannot change, **every string method gives back a new string** and leaves the original alone. You must **save** the result if you want to keep it (Section 12).

---

## 10. Searching with in and not in

`a in b` is `True` if the text `a` appears **anywhere** inside the string `b`:

```python
email = "sara@ku.edu.kw"
print("@" in email)
print("ku.edu" in email)
print("gmail" in email)
print(" " not in email)
```

```text
True
True
False
True
```

The search is **case-sensitive**:

```python
print("KU" in "sara@ku.edu.kw")
print("ku" in "sara@ku.edu.kw")
```

```text
False
True
```

With `if`:

```python
email = "sara@ku.edu.kw"
if "@" not in email:
    print("Invalid email")
else:
    print("Looks OK")
```

```text
Looks OK
```

---

## 11. Comparing Strings

### 11.1 Equality

`==` is `True` only if both strings have exactly the same characters, in the same order, with the same case:

```python
print("Kuwait" == "Kuwait")
print("Kuwait" == "kuwait")
print("Kuwait" == "Kuwait ")
print("Doha" != "Dubai")
```

```text
True
False
False
True
```

The third line is `False` because of the extra space at the end.

### 11.2 Order: < and >

Strings are compared character by character, like words in a dictionary:

```python
print("apple" < "banana")
print("Doha" < "Dubai")
print("cat" < "category")
```

```text
True
True
True
```

- `"Doha" < "Dubai"`: the first characters are equal (`D`), so Python compares the second ones: `o` comes before `u`.
- `"cat" < "category"`: a shorter string that is the start of a longer one comes first.

Be careful: **all uppercase letters come before all lowercase letters**, and **digits come before letters**:

```python
print("Zebra" < "apple")
print("9" < "A")
print("10" < "9")
```

```text
True
True
True
```

`"10" < "9"` is `True` because these are strings: Python compares `"1"` with `"9"` first. To compare numbers, convert them with `int()`.

### 11.3 Comparing without caring about case

Convert both sides to the same case first:

```python
answer = "Yes"
if answer.lower() == "yes":
    print("Confirmed")
```

```text
Confirmed
```

---

## 12. String Methods

### 12.1 What is a method?

A **method** is a function that belongs to a value. You call it with a **dot**:

```text
string.method_name(arguments)
```

For example, `name.upper()` means "take `name` and give me an uppercase version". Some methods need arguments inside the brackets, such as `replace("-", "")`.

**Important:** string methods **never change** the original string. They **return** a new value.

```python
name = "sara"
big = name.upper()
print(name)
print(big)
```

```text
sara
SARA
```

To change what `name` refers to, assign the result back: `name = name.upper()`.

### 12.2 Changing case

```python
name = "fawaz ALAZEMI"
print(name.upper())
print(name.lower())
print(name.title())
print(name.capitalize())
```

```text
FAWAZ ALAZEMI
fawaz alazemi
Fawaz Alazemi
Fawaz alazemi
```

| Method | Result |
|---|---|
| `upper()` | all letters capital |
| `lower()` | all letters small |
| `title()` | first letter of **each word** capital, the rest small |
| `capitalize()` | first letter of the **whole string** capital, the rest small |

Characters that are not letters (digits, spaces, symbols) are not changed.

### 12.3 Removing spaces: strip(), lstrip(), rstrip()

```python
raw = "   Ali   "
print("[" + raw + "]")
print("[" + raw.strip() + "]")
print("[" + raw.lstrip() + "]")
print("[" + raw.rstrip() + "]")
```

```text
[   Ali   ]
[Ali]
[Ali   ]
[   Ali]
```

- `strip()` removes spaces (and tabs and new lines) at **both** ends.
- `lstrip()` removes them only on the **left**; `rstrip()` only on the **right**.
- Spaces in the **middle** are never removed.

Users often type extra spaces by accident, so `strip()` is very useful when cleaning input.

### 12.4 Replacing text: replace(old, new)

```python
phone = "965-5123-4567"
print(phone.replace("-", ""))
print(phone.replace("-", " "))
msg = "Hello Ali, bye Ali"
print(msg.replace("Ali", "Sara"))
print(msg.replace("Mona", "Sara"))
```

```text
96551234567
965 5123 4567
Hello Sara, bye Sara
Hello Ali, bye Ali
```

- `replace()` changes **every** match.
- Replacing with `""` **deletes** the old text.
- If the old text is not found, you get the same text back (no error).
- It is case-sensitive.

### 12.5 Finding text: find(x)

`find(x)` returns the **index** where `x` first appears, or **−1** if it does not appear:

```python
email = "sara@ku.edu.kw"
print(email.find("@"))
print(email.find("."))
print(email.find("ku"))
print(email.find("gmail"))
```

```text
4
7
5
-1
```

`find()` is powerful together with slicing:

```python
email = "sara@ku.edu.kw"
at = email.find("@")
user = email[:at]
domain = email[at + 1:]
print(user)
print(domain)
```

```text
sara
ku.edu.kw
```

Always check for −1 before using the result as a position (see Common Mistake 7).

### 12.6 Counting: count(x)

```python
print("banana".count("a"))
print("banana".count("an"))
print("banana".count("z"))
print("sara@ku.edu.kw".count("."))
```

```text
3
2
0
2
```

### 12.7 Methods that answer True or False

| Method | `True` when… |
|---|---|
| `s.startswith(x)` | `s` begins with `x` |
| `s.endswith(x)` | `s` ends with `x` |
| `s.isdigit()` | `s` is not empty and every character is a digit 0–9 |
| `s.isalpha()` | `s` is not empty and every character is a letter |
| `s.isupper()` | `s` has letters and all of them are capitals |
| `s.islower()` | `s` has letters and all of them are small |

```python
file = "report.pdf"
print(file.endswith(".pdf"))
print(file.startswith("rep"))
print("2026".isdigit())
print("20 26".isdigit())
print("-5".isdigit())
print("Kuwait".isalpha())
print("New York".isalpha())
print("KUWAIT".isupper())
```

```text
True
True
True
False
False
True
False
True
```

Note: a space, a minus sign, or a decimal point is **not** a digit, and a space is **not** a letter.

These methods are perfect for checking input before converting it:

```python
text = "25"
if text.isdigit():
    print(int(text) * 2)
else:
    print("Please type a whole number")
```

```text
50
```

### 12.8 Chaining methods

Because each method returns a string, you can call another method on the result:

```python
name = "  aHMAD alsaleh   "
clean = name.strip().title()
print("[" + clean + "]")
```

```text
[Ahmad Alsaleh]
```

Python works from left to right: first `strip()`, then `title()` on the stripped string.

---

## 13. Worked Examples

### 13.1 Checking an email address

```python
email = "  Sara.Ali@KU.edu.kw "
email = email.strip().lower()
at = email.find("@")
if at <= 0 or email.count("@") != 1:
    print("Invalid email")
else:
    user = email[:at]
    domain = email[at + 1:]
    print("Clean email:", email)
    print("User:", user)
    print("Domain:", domain)
    if domain.endswith(".kw"):
        print("This is a Kuwaiti address")
```

```text
Clean email: sara.ali@ku.edu.kw
User: sara.ali
Domain: ku.edu.kw
This is a Kuwaiti address
```

1. `strip()` removes the outer spaces; `lower()` makes the email easier to compare.
2. `find("@")` gives 8. If it were −1 (no `@`) or 0 (nothing before `@`), the email would be invalid.
3. `count("@") != 1` rejects emails with two `@` symbols.
4. Slicing splits the email into the user part and the domain part.

### 13.2 A Kuwaiti mobile number

```python
phone = " +965 5123-4567 "
phone = phone.strip()
phone = phone.replace(" ", "").replace("-", "")
if phone.startswith("+965"):
    phone = phone[4:]
if len(phone) == 8 and phone.isdigit():
    if phone[0] in "569":
        print("Valid mobile:", phone[:4] + " " + phone[4:])
    else:
        print("Not a mobile number")
else:
    print("Wrong format")
```

```text
Valid mobile: 5123 4567
```

| Step | `phone` |
|---|---|
| start | `" +965 5123-4567 "` |
| `strip()` | `"+965 5123-4567"` |
| remove spaces and dashes | `"+96551234567"` |
| remove `"+965"` with `[4:]` | `"51234567"` |

The check `phone[0] in "569"` uses `in` with a string: it is `True` if the first character is `5`, `6`, or `9`.

### 13.3 Reading a course code

```python
code = "CS126-2026-F"
dash = code.find("-")
subject = code[:2]
number = code[2:dash]
year = code[dash + 1:dash + 5]
term = code[-1]
print("Subject:", subject)
print("Number:", number)
print("Year:", year)
if term == "F":
    print("Term: Fall")
elif term == "S":
    print("Term: Spring")
else:
    print("Term: Summer")
```

```text
Subject: CS
Number: 126
Year: 2026
Term: Fall
```

`find("-")` is 5. So the course number is `code[2:5]`, and the year is `code[6:10]`.

### 13.4 A receipt line

```python
item = "Chicken machboos"
price = 3.75
qty = 2
total = price * qty
line = item + " x" + str(qty) + " = " + str(total) + " KD"
print(line)
print("-" * len(line))
```

```text
Chicken machboos x2 = 7.5 KD
----------------------------
```

`str()` converts the numbers so they can be joined. `"-" * len(line)` draws a line exactly as long as the text above it.

---

## 14. Important Notes

- Strings are written in quotes; the quotes are not part of the text.
- `len()` counts **every** character, including spaces and escape sequences (each counts as one).
- `+` joins strings and never adds spaces; `*` repeats.
- `"5" + "3"` is `"53"`; `"5" + 3` is an error. Convert with `str()` or `int()`.
- `input()` always returns a string.
- Indexes start at 0; `s[-1]` is the last character.
- In a slice, the stop index is **not included**. Slices never cause `IndexError`.
- Strings are **immutable**. Methods return **new** strings — save the result.
- `in`, `==`, `<`, `find()`, `count()`, and `replace()` are **case-sensitive**.
- `find()` returns −1 when the text is not found.

---

## 15. Common Mistakes

### Mistake 1: Joining a string and a number

**Incorrect**

```text
total = 15
print("Total: " + total + " KD")

TypeError: can only concatenate str (not "int") to str
```

**Correct**

```python
total = 15
print("Total: " + str(total) + " KD")
print("Total:", total, "KD")
```

```text
Total: 15 KD
Total: 15 KD
```

### Mistake 2: Adding numbers that are stored as strings

**Incorrect**

```python
a = "10"
b = "20"
print(a + b)
```

```text
1020
```

**Why?** `a` and `b` are strings, so `+` joins them.

**Correct**

```python
a = "10"
b = "20"
print(int(a) + int(b))
```

```text
30
```

### Mistake 3: Forgetting the quotes

**Incorrect**

```text
city = Kuwait

NameError: name 'Kuwait' is not defined
```

**Why?** Without quotes, Python thinks `Kuwait` is a variable name.

**Correct:** `city = "Kuwait"`

### Mistake 4: Not saving the result of a method

**Incorrect**

```python
name = "sara"
name.upper()
print(name)
```

```text
sara
```

**Why?** `upper()` returns a new string, but it was not saved. The original string never changes.

**Correct**

```python
name = "sara"
name = name.upper()
print(name)
```

```text
SARA
```

### Mistake 5: Case-sensitive comparisons

**Incorrect**

```python
answer = "Yes"
if answer == "yes":
    print("Confirmed")
else:
    print("Not confirmed")
```

```text
Not confirmed
```

**Correct**

```python
answer = "Yes"
if answer.lower() == "yes":
    print("Confirmed")
else:
    print("Not confirmed")
```

```text
Confirmed
```

### Mistake 6: Wrong slice positions

**Incorrect** (goal: the first 3 letters)

```python
s = "Kuwait"
print(s[1:3])
```

```text
uw
```

**Why?** Index 1 is the **second** character, and the stop (3) is not included.

**Correct**

```python
s = "Kuwait"
print(s[:3])
```

```text
Kuw
```

### Mistake 7: Using find() without checking for −1

**Incorrect**

```python
email = "sara.ku.edu"
at = email.find("@")
print(email[:at])
```

```text
sara.ku.ed
```

**Why?** There is no `@`, so `find()` returned −1, and `email[:-1]` silently removed the last character. No error appears, so the bug is hard to see.

**Correct**

```python
email = "sara.ku.edu"
at = email.find("@")
if at == -1:
    print("No @ in email")
else:
    print(email[:at])
```

```text
No @ in email
```

### Mistake 8: Trying to change one character

**Incorrect**

```text
word = "cat"
word[0] = "b"

TypeError: 'str' object does not support item assignment
```

**Correct**

```python
word = "cat"
word = "b" + word[1:]
print(word)
```

```text
bat
```

### Mistake 9: Comparing numbers as strings

**Incorrect**

```python
a = "10"
b = "9"
if a > b:
    print(a, "is bigger")
else:
    print(b, "is bigger")
```

```text
9 is bigger
```

**Why?** As strings, `"10"` is compared with `"9"` character by character, and `"1"` comes before `"9"`.

**Correct**

```python
a = "10"
b = "9"
if int(a) > int(b):
    print(a, "is bigger")
else:
    print(b, "is bigger")
```

```text
10 is bigger
```

---

## 16. Mini Practice Questions

Try these before looking at the answers at the end of this section.

**Q1.** What does this print?

```python
print(len("Hi there"), "Hi" * 2, "3" + "4")
```

**Q2.** What does this print?

```python
s = "Python"
print(s[1:4], s[-2:], s[::2])
```

**Q3.** What does this print?

```python
print("Doha".upper(), "  x ".strip() + "!", "aaa".replace("a", "b"))
```

**Q4.** What does `"Kuwait".find("w")` return? What does `"Kuwait".find("W")` return?

**Q5.** True or false: after `s = "abc"` and `s.upper()`, the value of `s` is `"ABC"`.

**Q6.** What does this print?

```python
print("10" < "9", 10 < 9)
```

### Answers to Mini Practice

1. **`8 HiHi 34`** — the space counts in the length.
2. **`yth on Pto`**
3. **`DOHA x! bbb`**
4. **2** and **−1** (`find` is case-sensitive).
5. **False** — strings are immutable; the result of `upper()` was not saved.
6. **`True False`** — as strings, `"1"` comes before `"9"`; as numbers, 10 is not less than 9.

---

## 17. Ask AI to Help You Understand

```text
Explain Python string indexing and slicing using the word "Kuwait".
Show a table of positive and negative indexes, then explain s[1:4], s[:3], s[-2:], and s[::-1].
Do not use loops or lists, and do not give me exercises yet.
```

```text
Why does "5" + "3" give "53" in Python, while 5 + 3 gives 8?
Explain str(), int(), and float() with two small examples each.
```

```text
Explain why Python strings are immutable. Why does name.upper() not change name?
Show the correct way to keep the uppercase version.
```

```text
Show me how find() and slicing can be used together to separate an email address
into the part before @ and the part after it. Explain what happens if @ is missing.
```

```text
Give me five "predict the output" questions about Python string methods
(upper, lower, strip, replace, find, count). Do not use loops or lists.
Give me hints first and do not show the answers unless I ask.
```

> **Remember:** Always run the code yourself. AI can make mistakes, and running code is the only way to be sure.

---

## 18. Summary

- A **string** is a sequence of characters in quotes (`"..."`, `'...'`, or `"""..."""`).
- Escape sequences such as `\n`, `\t`, `\"`, and `\\` put special characters in a string.
- `len()` counts every character. `+` joins strings, `*` repeats them.
- Strings and numbers are different types; convert with `str()`, `int()`, `float()`. `input()` returns a string.
- **Indexing** `s[i]` gives one character; indexes start at 0, and `-1` is the last character.
- **Slicing** `s[start:stop:step]` gives part of a string; the stop is not included; `s[::-1]` reverses.
- Strings are **immutable**: you cannot change a character; build a new string instead.
- `in` / `not in` search for text; `==`, `!=`, `<`, `>` compare strings; all are case-sensitive.
- Methods return **new** values: `upper`, `lower`, `title`, `capitalize`, `strip`, `replace`, `find` (−1 if missing), `count`, `startswith`, `endswith`, `isdigit`, `isalpha`, `isupper`, `islower`.

---

## Basic Exercises

> Exercises 1–12 are the same as in the slides. Exercises 13–16 are extra practice.

**Exercise 1.** Predict the output.

```python
s = "Kuwait"
print(s[0], s[-1], len(s))
```

**Exercise 2.** Predict the output.

```python
print("Ha" * 3 + "!")
print("5" + "5")
print(5 + 5)
```

**Exercise 3.** Find and fix the error.

```text
age = 20
print("Age: " + age)
```

**Exercise 4.** Predict the output.

```python
city = "Kuwait City"
print(city[0:6])
print(city[7:])
print(city[-2:])
```

**Exercise 13.** Predict the output.

```python
print("Kuwait\nCity")
print("A\\B")
print(len("A\\B"))
```

## Practice Exercises

**Exercise 5.** Clean `name = "  fahad alazemi  "` so it prints as `Fahad Alazemi`, then print its length.

**Exercise 6.** For `email = "sara@ku.edu.kw"`, print `Valid Kuwaiti email` if it contains `"@"` **and** ends with `".kw"`; otherwise print `Not valid`.

**Exercise 7.** Remove the dashes from `phone = "965-5123-4567"`, then print the result and its number of digits.

**Exercise 8.** Explain what each part does and give the output.

```python
s = "banana"
print(s.count("a"), s.find("n"), s.upper())
```

**Exercise 14.** A user typed a username: `user = "  Ali_2026 "`. Usernames are stored in small letters with no spaces at the ends. Print the cleaned username, and print `Too short` if it has fewer than 6 characters, otherwise `OK`.

## Challenge Exercises

**Exercise 9.** Print the initials of `full = "Mona Alsabah"` as `M.A.` Use `find(" ")` so it works for any first and last name.

**Exercise 10.** A word is a **palindrome** if it reads the same backwards. Check `word = "Level"` without caring about capitals, and print `Level is a palindrome` or `Level is not a palindrome`.

**Exercise 11.** Predict the output.

```python
s = "Kuwait University"
print(s.find("U"), s.count("i"))
print(s[s.find(" ") + 1:].lower())
print(s.replace("i", "!")[:6])
```

**Exercise 12.** A Kuwaiti mobile number must have 8 characters, all digits, and start with 5, 6, or 9. Check `num = "6512345A"` and print `Valid` or `Invalid`.

**Exercise 15.** Hide a password when showing it on screen: keep the first and last characters, and replace every other character with `*`. For `pw = "kuwait123"`, print `k*******3`. Your code must work for any password with at least 2 characters.

**Exercise 16.** Names in a report are stored as `"Last, First"`, for example `entry = "Alazemi, Fawaz"`. Use `find()` and slicing to print the name as `Fawaz Alazemi`.

---

# Exercise Solutions

### Solution 1

`s[0]` is the first character, `s[-1]` the last, and `"Kuwait"` has 6 characters.

```text
K t 6
```

### Solution 2

`"Ha" * 3` repeats the string, then `+ "!"` joins. `"5" + "5"` joins two strings. `5 + 5` adds two numbers.

```text
HaHaHa!
55
10
```

### Solution 3

`age` is an integer, and `+` cannot join a string and a number (`TypeError`). Convert it with `str()`:

```python
age = 20
print("Age: " + str(age))
```

```text
Age: 20
```

Another correct answer: `print("Age:", age)`.

### Solution 4

- `city[0:6]` → indexes 0–5.
- `city[7:]` → from index 7 to the end.
- `city[-2:]` → the last two characters.

```text
Kuwait
City
ty
```

### Solution 5

```python
name = "  fahad alazemi  "
name = name.strip().title()
print(name)
print(len(name))
```

```text
Fahad Alazemi
13
```

### Solution 6

```python
email = "sara@ku.edu.kw"
if "@" in email and email.endswith(".kw"):
    print("Valid Kuwaiti email")
else:
    print("Not valid")
```

```text
Valid Kuwaiti email
```

### Solution 7

```python
phone = "965-5123-4567"
digits = phone.replace("-", "")
print(digits)
print(len(digits))
```

```text
96551234567
11
```

### Solution 8

- `s.count("a")` counts how many times `"a"` appears → 3.
- `s.find("n")` gives the index of the first `"n"` → 2 (`b`=0, `a`=1, `n`=2).
- `s.upper()` returns a new string in capital letters. `s` itself is unchanged.

```text
3 2 BANANA
```

### Solution 9

The first initial is `full[0]`. The last name starts one place after the space, at `full[space + 1]`.

```python
full = "Mona Alsabah"
space = full.find(" ")
initials = full[0] + "." + full[space + 1] + "."
print(initials)
```

```text
M.A.
```

### Solution 10

```python
word = "Level"
w = word.lower()
if w == w[::-1]:
    print(word, "is a palindrome")
else:
    print(word, "is not a palindrome")
```

```text
Level is a palindrome
```

Without `lower()`, the program would compare `"Level"` with `"leveL"`, which are not equal.

### Solution 11

```text
7 3
university
Kuwa!t
```

- `"U"` is at index 7 (`K`=0, …, space=6, `U`=7). There are 3 small `"i"` letters: one in "Kuwait" and two in "University". The capital `U` is not counted.
- `s.find(" ") + 1` is 7, so the slice is `"University"`, and `lower()` makes it `"university"`.
- `replace()` gives `"Kuwa!t Un!vers!ty"`; its first 6 characters are `"Kuwa!t"`.

### Solution 12

```python
num = "6512345A"
ok = len(num) == 8 and num.isdigit()
if ok and num[0] in "569":
    print("Valid")
else:
    print("Invalid")
```

```text
Invalid
```

The length is 8 and the first digit is 6, but `"A"` is not a digit, so `isdigit()` is `False`.

### Solution 13

`\n` starts a new line. `\\` is one backslash, so the string `"A\\B"` has 3 characters: `A`, `\`, `B`.

```text
Kuwait
City
A\B
3
```

### Solution 14

```python
user = "  Ali_2026 "
user = user.strip().lower()
print(user)
if len(user) < 6:
    print("Too short")
else:
    print("OK")
```

```text
ali_2026
OK
```

### Solution 15

The number of stars is the length minus the 2 characters we keep.

```python
pw = "kuwait123"
hidden = pw[0] + "*" * (len(pw) - 2) + pw[-1]
print(hidden)
```

```text
k*******3
```

`len(pw)` is 9, so there are 7 stars. The brackets around `len(pw) - 2` make sure the subtraction happens before the repetition.

### Solution 16

```python
entry = "Alazemi, Fawaz"
comma = entry.find(",")
last = entry[:comma]
first = entry[comma + 2:]
print(first + " " + last)
```

```text
Fawaz Alazemi
```

`find(",")` is 7. The last name is everything before the comma. The first name starts 2 places after the comma, to skip the comma and the space.

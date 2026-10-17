# CS126 – Introduction to Python

## Advanced Strings

**Instructor:** Dr. Fawaz Alazemi

---

## Learning Objectives

After studying these notes, you should be able to:

1. Search a string with `find()` and `rfind()`, including the optional `start` and `end` positions.
2. Explain the difference between `find()`/`rfind()` and `index()`/`rindex()`.
3. Combine searching with slicing to extract parts of a string, and handle the "not found" case safely.
4. Count non-overlapping occurrences with `count()`.
5. Use `replace(old, new)` and `replace(old, new, count)`.
6. Change case with `upper()`, `lower()`, `title()`, `capitalize()`, and `swapcase()`, and use them to search and compare without caring about case.
7. Check text with `startswith()`, `endswith()`, `isdigit()`, `isalpha()`, `isalnum()`, `isspace()`, `isupper()`, and `islower()`.
8. Clean text with `strip()`, `lstrip()`, and `rstrip()`, with and without a set of characters.
9. Build strings with `+`, `+=`, `*`, `str()`, `join()`, and **f-strings**, and break them with `split()`.
10. Chain several methods in one expression.

---

## 1. Introduction

### 1.1 Why "advanced" strings?

In the introduction to strings, you learned to create strings, index and slice them, and use a few methods. Real programs, however, must handle **messy** text that comes from users, files, and websites:

- an email address typed with capital letters and extra spaces,
- a phone number written as `"+965 5123-4567"`,
- a file name such as `"report.final.pdf"`,
- a line of data such as `"Machboos,3.5,2"`.

To work with text like this, we need to **find** things inside strings, **replace** parts, **change case**, **check** what kind of text we have, and **build** new strings neatly. This lecture gives you a complete toolbox for these jobs.

### 1.2 One rule to remember

Strings are **immutable**: once a string is created, it can never be changed. Therefore:

> Every string method **returns a new value**. The original string stays the same. If you want to keep the result, you must **save** it in a variable.

```python
city = "kuwait"
city.upper()
print(city)
city = city.upper()
print(city)
```

```text
kuwait
KUWAIT
```

The first call to `upper()` created `"KUWAIT"`, but nobody saved it. The second line saved the new string back into `city`.

---

## 2. Main Concepts and Vocabulary

| Term | Meaning | Example |
|---|---|---|
| **Method** | A function that belongs to a value, called with a dot | `s.find("a")` |
| **Argument** | A value given inside the brackets | `"a"` in `s.find("a")` |
| **Return value** | The value a method gives back | `find` returns an index |
| **Substring** | A string that appears inside another string | `"wa"` in `"Kuwait"` |
| **Index** | A position in a string, starting at 0 | `s[3]` |
| **Separator** | Text that separates parts of a string | `","` in `"a,b,c"` |
| **Concatenation** | Joining strings together | `"Ku" + "wait"` |
| **Chaining** | Calling a method on the result of another method | `s.strip().lower()` |
| **f-string** | A string with `f` before it, in which `{ }` holds values | `f"Hi {name}"` |

---

## 3. Searching with find() and rfind()

### 3.1 find(): the first position

`s.find(x)` returns the **index** where the substring `x` **first** begins. If `x` does not appear, it returns **−1**.

| Character | b | a | n | a | n | a |
|---|---|---|---|---|---|---|
| Index | 0 | 1 | 2 | 3 | 4 | 5 |

```python
s = "banana"
print(s.find("a"))
print(s.find("nan"))
print(s.find("x"))
print(s.find("A"))
```

```text
1
2
-1
-1
```

- The first `"a"` is at index 1.
- `"nan"` starts at index 2. For a longer substring, `find` gives the index of its **first character**.
- `"x"` is not in the string → −1. This is **not** an error.
- The search is **case-sensitive**, so `"A"` is not found.

**Why −1?** Every real position is 0 or more, so −1 cannot be confused with a real position. Be careful, though: −1 *is* a valid index in Python (the last character). Section 6 shows why this matters.

### 3.2 find() with start and end

`find` accepts two more arguments:

```text
s.find(x, start, end)
```

- `start`: where the search begins (default 0).
- `end`: where it stops — **not included**, exactly like a slice (default: the end of the string).

```python
s = "banana"
print(s.find("a", 2))
print(s.find("a", 4))
print(s.find("a", 0, 3))
print(s.find("n", 0, 2))
```

```text
3
5
1
-1
```

- `find("a", 2)` starts at index 2 and finds the `"a"` at index 3.
- `find("a", 4)` starts at index 4 and finds index 5.
- `find("a", 0, 3)` only looks at indexes 0, 1, 2 → finds index 1.
- `find("n", 0, 2)` only looks at indexes 0 and 1 → no `"n"` there → −1.

The answer is always an index in the **whole** string, not in the searched part.

### 3.3 Finding the second occurrence

Start the second search **one position after** the first result:

```python
s = "banana"
first = s.find("a")
second = s.find("a", first + 1)
third = s.find("a", second + 1)
print(first, second, third)
```

```text
1 3 5
```

### 3.4 rfind(): the last position

`s.rfind(x)` returns the index where `x` **last** begins (the "r" stands for "right", because it searches from the right side). It also returns −1 if `x` is not found.

```python
s = "banana"
print(s.find("a"), s.rfind("a"))
print(s.rfind("an"))
print(s.rfind("x"))
```

```text
1 5
3
-1
```

Important: the index returned by `rfind` is still counted **from the left**, starting at 0. Only the search direction is different.

`rfind` also accepts `start` and `end`:

```python
s = "banana"
print(s.rfind("a", 0, 5))
```

```text
3
```

Within indexes 0–4, the last `"a"` is at index 3.

### 3.5 When to use rfind

`rfind` is the right tool whenever you need the **last** part of something:

```python
file = "report.final.pdf"
dot = file.rfind(".")
print(file[dot + 1:])
```

```text
pdf
```

Other examples: the last name in a full name (after the last space), the file name in a path (after the last `/`), the top-level domain of an email (after the last `.`).

---

## 4. index() and rindex()

`index()` and `rindex()` work exactly like `find()` and `rfind()`, with one difference: if the substring is **not found**, they raise a **ValueError** instead of returning −1.

```python
s = "banana"
print(s.index("n"))
print(s.rindex("n"))
print(s.find("z"))
```

```text
2
4
-1
```

```text
s = "banana"
print(s.index("z"))

ValueError: substring not found
```

| Method | Found | Not found |
|---|---|---|
| `find` / `rfind` | index | `-1` |
| `index` / `rindex` | index | `ValueError` |

**Which one should you use?**

- Use `find` when "not found" is a **normal** possibility and you will check for −1.
- Use `index` when the text **must** be there. If it is not, the error stops the program and tells you that something is wrong, instead of continuing with a wrong −1.

You can also check first with `in`:

```python
s = "banana"
if "z" in s:
    print(s.index("z"))
else:
    print("z is not in the string")
```

```text
z is not in the string
```

---

## 5. Counting with count()

`s.count(x)` returns how many times `x` appears in `s`:

```python
s = "banana"
print(s.count("a"))
print(s.count("an"))
print(s.count("x"))
print(s.count("a", 3))
```

```text
3
2
0
2
```

Like `find`, `count` accepts optional `start` and `end` positions. `s.count("a", 3)` counts only from index 3 onward (indexes 3 and 5).

Matches **do not overlap**. After a match is found, the search continues **after** it:

```python
print("aaaa".count("aa"))
print("Mississippi".count("ss"))
```

```text
2
2
```

`"aaaa"` contains `"aa"` at positions 0 and 2. The `"aa"` that starts at position 1 overlaps the first match, so it is not counted.

---

## 6. Search + Slice: Extracting Parts of a String

### 6.1 The pattern

Searching gives a **position**; slicing uses positions. Together they let you pull out any part of a string:

| Part | Slice |
|---|---|
| Everything **before** position `p` | `s[:p]` |
| Everything **after** position `p` | `s[p + 1:]` |
| Everything **between** positions `a` and `b` | `s[a + 1:b]` |

The `+ 1` skips the separator character itself.

### 6.2 Example: an email address

```python
email = "sara.ali@ku.edu.kw"
at = email.find("@")
user = email[:at]
domain = email[at + 1:]
country = email[email.rfind(".") + 1:]
print(user)
print(domain)
print(country)
```

```text
sara.ali
ku.edu.kw
kw
```

### 6.3 Example: text between two separators

```python
date = "2026-10-16"
a = date.find("-")
b = date.rfind("-")
print(a, b)
print(date[a + 1:b])
```

```text
4 7
10
```

### 6.4 Example: separators longer than one character

If the separator has more than one character, skip its full length:

```python
url = "https://www.ku.edu.kw/cs"
start = url.find("//") + 2
end = url.find("/", start)
print(url[start:end])
```

```text
www.ku.edu.kw
```

- `url.find("//")` is 6, and `"//"` has 2 characters, so the domain starts at 8.
- `url.find("/", start)` searches for the next `/` **after** the domain begins.

### 6.5 Always handle "not found"

If the separator is missing, `find` returns −1, and slicing with −1 gives a **wrong result without any error**:

```python
email = "sara.ku.edu"
at = email.find("@")
print(at)
print(email[:at])
```

```text
-1
sara.ku.ed
```

`email[:-1]` means "everything except the last character". The program continues with wrong data. Always check:

```python
email = "sara.ku.edu"
at = email.find("@")
if at == -1:
    print("No @ found")
else:
    print(email[:at])
```

```text
No @ found
```

---

## 7. Replacing with replace()

### 7.1 Basic use

`s.replace(old, new)` returns a new string in which **every** `old` is replaced by `new`:

```python
phone = "965-5123-4567"
print(phone.replace("-", " "))
print(phone.replace("-", ""))
print(phone)
```

```text
965 5123 4567
96551234567
965-5123-4567
```

- Replacing with the empty string `""` **deletes** the old text.
- `phone` itself is not changed.

### 7.2 Limiting the number of replacements

A third argument, `count`, limits how many matches are replaced, starting from the left:

```python
phone = "965-5123-4567"
print(phone.replace("-", " ", 1))
s = "a-b-c-d"
print(s.replace("-", "/", 2))
```

```text
965 5123-4567
a/b/c-d
```

### 7.3 Details

```python
msg = "Ali met Ali at KU"
print(msg.replace("Ali", "Sara"))
print(msg.replace("ali", "Sara"))
print(msg.replace("Ali", "Sara").replace("KU", "Kuwait University"))
```

```text
Sara met Sara at KU
Ali met Ali at KU
Sara met Sara at Kuwait University
```

- `replace` is **case-sensitive**: `"ali"` does not match `"Ali"`.
- If there is no match, you get the **same** text back, with no error.
- Several `replace` calls can be **chained** (Section 12).

---

## 8. Changing Case

### 8.1 The five case methods

```python
s = "welcome to KUWAIT city"
print(s.upper())
print(s.lower())
print(s.title())
print(s.capitalize())
print(s.swapcase())
```

```text
WELCOME TO KUWAIT CITY
welcome to kuwait city
Welcome To Kuwait City
Welcome to kuwait city
WELCOME TO kuwait CITY
```

| Method | Effect |
|---|---|
| `upper()` | every letter becomes a capital |
| `lower()` | every letter becomes small |
| `title()` | first letter of **each word** capital, the rest small |
| `capitalize()` | first letter of the **whole string** capital, the rest small |
| `swapcase()` | capitals become small, small letters become capitals |

Digits, spaces, and symbols are never changed.

### 8.2 A note about title()

`title()` treats **any** non-letter as the end of a word. This is helpful for names with a dash, but strange with apostrophes:

```python
print("al-ali".title())
print("ali's book".title())
```

```text
Al-Ali
Ali'S Book
```

### 8.3 Ignoring case when searching and comparing

To search or compare **without caring about case**, convert **both** sides to the same case first, usually with `lower()`:

```python
text = "Welcome to KUWAIT University"
word = "kuwait"
print(text.find(word))
print(text.lower().find(word))
print(word in text.lower())
answer = "YeS"
print(answer.lower() == "yes")
```

```text
-1
11
True
True
```

Because `lower()` does not change the length or the positions, an index found in `text.lower()` is also correct for `text`:

```python
text = "Welcome to KUWAIT University"
pos = text.lower().find("kuwait")
print(text[pos:pos + 6])
```

```text
KUWAIT
```

---

## 9. Checking Text: True or False

### 9.1 startswith() and endswith()

```python
print("+96551234567".startswith("+965"))
print("report.pdf".endswith(".pdf"))
print("photo.JPG".endswith(".jpg"))
print("photo.JPG".lower().endswith(".jpg"))
```

```text
True
True
False
True
```

They can also take a **tuple** of possible endings (or beginnings). The result is `True` if **any** of them matches:

```python
f = "photo.png"
print(f.endswith((".png", ".jpg", ".gif")))
```

```text
True
```

### 9.2 The is…() methods

| Method | `True` when the string is not empty and… |
|---|---|
| `isdigit()` | every character is a digit 0–9 |
| `isalpha()` | every character is a letter |
| `isalnum()` | every character is a letter or a digit |
| `isspace()` | every character is a space (or tab, newline) |
| `isupper()` | it has letters, and all of them are capitals |
| `islower()` | it has letters, and all of them are small |

```python
print("2026".isdigit(), "20.5".isdigit(), "-5".isdigit())
print("Kuwait".isalpha(), "New York".isalpha())
print("CS126".isalnum(), "CS 126".isalnum())
print("   ".isspace(), "".isspace())
print("KU2026".isupper(), "ku2026".islower())
```

```text
True False False
True False
True False
True False
True True
```

Notes:

- A decimal point, a minus sign, and a space are **not** digits.
- A space is **not** a letter, so `"New York".isalpha()` is `False`.
- The empty string gives `False` for all `is…()` methods.
- `isupper()` and `islower()` ignore digits and symbols; they only look at letters.

These methods are useful before converting input:

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

---

## 10. Cleaning with strip(), lstrip(), rstrip()

### 10.1 Removing spaces

```python
raw = "   Ali   "
print("[" + raw.strip() + "]")
print("[" + raw.lstrip() + "]")
print("[" + raw.rstrip() + "]")
```

```text
[Ali]
[Ali   ]
[   Ali]
```

Spaces in the **middle** are never removed.

### 10.2 Removing other characters

You can give `strip` a string of characters to remove from the ends:

```python
print("...Hello!!!".strip(".!"))
print("0050".lstrip("0"))
print("**Sale**".strip("*"))
```

```text
Hello
50
Sale
```

### 10.3 A common trap

The argument is a **set of characters**, not a word. `strip` removes **any** of those characters from the ends, one at a time, until it reaches a character that is not in the set:

```python
print("report.txt".rstrip(".txt"))
```

```text
repor
```

`rstrip(".txt")` removed `t`, `x`, `t`, `.`, and then the `t` at the end of "report", because `t` is in the set. To remove an exact ending, use slicing (or `replace` when it is safe):

```python
name = "report.txt"
if name.endswith(".txt"):
    name = name[:-4]
print(name)
```

```text
report
```

---

## 11. Building Strings

### 11.1 Concatenation with +

```python
first = "Fawaz"
last = "Alazemi"
full = first + " " + last
print(full)
```

```text
Fawaz Alazemi
```

`+` never adds spaces automatically.

Both sides must be strings. A number must be converted with `str()`:

```text
total = 7.5
print("Total: " + total)

TypeError: can only concatenate str (not "float") to str
```

```python
total = 7.5
print("Total: " + str(total) + " KD")
```

```text
Total: 7.5 KD
```

### 11.2 Adding to a string with +=

`s += x` is a short way to write `s = s + x`:

```python
msg = "Total"
msg += ": "
msg += str(7.5) + " KD"
print(msg)
```

```text
Total: 7.5 KD
```

The string is not changed — each `+=` builds a **new** string and stores it in `msg`.

### 11.3 Repetition with *

```python
print("=" * 12)
print("ab" * 2 + "c")
```

```text
============
ababc
```

`*` is done before `+`, as in mathematics.

### 11.4 join(): many pieces with a separator

```text
separator.join(list_of_strings)
```

```python
gcc = ["Kuwait", "Qatar", "Oman"]
print(", ".join(gcc))
print(" - ".join(gcc))
print("".join(["C", "S", "1", "2", "6"]))
print("/".join(("16", "10", "2026")))
```

```text
Kuwait, Qatar, Oman
Kuwait - Qatar - Oman
CS126
16/10/2026
```

- `join` is a method of the **separator** string, not of the list.
- The separator goes **between** items only.
- It works with lists and tuples. With a set, the order is not fixed.
- Every item must be a **string**; `"-".join([1, 2])` causes a `TypeError`.

When you have many pieces, `join` is cleaner and easier to read than many `+` signs.

### 11.5 f-strings

An **f-string** is a string with the letter `f` just before the opening quote. Inside it, anything in curly brackets `{ }` is **evaluated** and inserted into the text:

```python
name = "Sara"
qty = 3
price = 0.25
print(f"{name} bought {qty} teas.")
print(f"Total: {qty * price} KD")
print(f"{name.upper()} has {len(name)} letters")
```

```text
Sara bought 3 teas.
Total: 0.75 KD
SARA has 4 letters
```

Advantages:

- no `+` signs and no `str()` conversions,
- spaces appear exactly where you type them,
- any expression can go inside `{ }`, including calculations and method calls.

**Decimal places.** Add `:.Nf` after the value to show exactly `N` digits after the decimal point. In Kuwait, money is often shown with 3 decimals (fils):

```python
price = 3.5
qty = 2
print(f"Total: {price * qty:.3f} KD")
gpa = 3.456
print(f"GPA: {gpa:.2f}")
```

```text
Total: 7.000 KD
GPA: 3.46
```

`:.2f` **rounds** the value to 2 decimals for display. The variable itself is not changed.

Comparing the methods:

```python
name = "Sara"
qty = 3
print(name + " bought " + str(qty) + " teas.")
print(f"{name} bought {qty} teas.")
```

```text
Sara bought 3 teas.
Sara bought 3 teas.
```

---

## 12. Breaking Strings with split()

### 12.1 Splitting on spaces

`s.split()` with **no argument** breaks a string into a **list** of words. It splits on any amount of whitespace and **ignores** extra spaces at the start, at the end, and between words:

```python
s = "  Kuwait  City   2026 "
print(s.split())
```

```text
['Kuwait', 'City', '2026']
```

### 12.2 Splitting on a separator

`s.split(sep)` splits at **every** occurrence of `sep`:

```python
line = "Machboos,3.5,2"
parts = line.split(",")
print(parts)
print(len(parts))
```

```text
['Machboos', '3.5', '2']
3
```

The pieces are always **strings**. Convert them to do arithmetic:

```python
line = "Machboos,3.5,2"
parts = line.split(",")
total = float(parts[1]) * int(parts[2])
print(parts[0], total)
```

```text
Machboos 7.0
```

### 12.3 split() versus split(" ")

With an explicit separator, two separators next to each other produce an **empty string**:

```python
s = "Kuwait  City"
print(s.split())
print(s.split(" "))
print("a,b,,c".split(","))
```

```text
['Kuwait', 'City']
['Kuwait', '', 'City']
['a', 'b', '', 'c']
```

For ordinary text with spaces, `split()` with no argument is almost always what you want.

### 12.4 split and join together

`split` and `join` are opposites: string → list → string. Together they can clean or reformat text:

```python
messy = "  python   is    FUN  "
neat = " ".join(messy.split())
print("[" + neat + "]")
print(neat.capitalize())
date = "2026-10-16"
print("/".join(date.split("-")[::-1]))
```

```text
[python is FUN]
Python is fun
16/10/2026
```

---

## 13. Chaining Methods

Because each method returns a string, you can call another method on the result. Python works **from left to right**:

```python
raw = "  +965 5123-4567  "
clean = raw.strip().replace(" ", "").replace("-", "")
print(clean)
```

```text
+96551234567
```

| Step | Result |
|---|---|
| `raw` | `"  +965 5123-4567  "` |
| `.strip()` | `"+965 5123-4567"` |
| `.replace(" ", "")` | `"+9655123-4567"` |
| `.replace("-", "")` | `"+96551234567"` |

The last method in a chain decides the type of the result. For example, `s.lower().split()` gives a **list**, and `s.lower().count("a")` gives a **number** — you cannot call a string method after those.

Chaining is powerful, but keep it readable. If a chain becomes long, break it into several lines with clear variable names.

---

## 14. Worked Examples

### 14.1 Cleaning a full name

```python
raw = "  sara mohammad AL-ALI  "
name = raw.strip().title()
first_space = name.find(" ")
last_space = name.rfind(" ")
first = name[:first_space]
last = name[last_space + 1:]
mid = name[first_space + 1]
initials = name[0] + mid + last[0]
print(name)
print(f"{last}, {first}")
print("Initials:", initials)
```

```text
Sara Mohammad Al-Ali
Al-Ali, Sara
Initials: SMA
```

1. `strip()` removes the outer spaces; `title()` fixes the case, including after the dash.
2. `find(" ")` gives the end of the first name; `rfind(" ")` gives the start of the last name. This works no matter how many middle names there are.
3. Slicing takes whole names; indexing takes single letters.
4. An f-string builds `"Last, First"`.

### 14.2 Reading a file path

```python
path = "C:/Users/ali/report.final.pdf"
slash = path.rfind("/")
folder = path[:slash]
filename = path[slash + 1:]
dot = filename.rfind(".")
ext = filename[dot + 1:].upper()
print("Folder:", folder)
print("File:", filename[:dot])
print("Type:", ext)
print("Is PDF?", filename.lower().endswith(".pdf"))
```

```text
Folder: C:/Users/ali
File: report.final
Type: PDF
Is PDF? True
```

Using `find(".")` instead of `rfind(".")` would wrongly give the extension `"final.pdf"`.

### 14.3 A receipt line

```python
line = " machboos , 3.5 , 2 "
parts = line.split(",")
item = parts[0].strip().title()
price = float(parts[1])
qty = int(parts[2])
total = price * qty
print(f"{item} x{qty} = {total:.3f} KD")
print("-" * 24)
```

```text
Machboos x2 = 7.000 KD
------------------------
```

`float()` and `int()` ignore spaces at the start and end, so `" 3.5 "` and `" 2 "` convert correctly.

### 14.4 A café order

```python
order = "  KARAK x4 @ 0.15 "
o = order.strip()
x = o.find(" x")
at = o.find("@")
drink = o[:x].title()
qty = int(o[x + 2:at])
price = float(o[at + 1:])
print(f"{qty} x {drink} = {qty * price:.3f} KD")
```

```text
4 x Karak = 0.600 KD
```

`" x"` is two characters long, so the quantity starts at `x + 2`.

---

## 15. Quick Reference

| Code (`s = "banana"`) | Result | Note |
|---|---|---|
| `s.find("a")` | `1` | first position |
| `s.find("a", 2)` | `3` | search from index 2 |
| `s.rfind("a")` | `5` | last position |
| `s.find("x")` | `-1` | not found |
| `s.index("x")` | `ValueError` | not found |
| `s.count("a")` | `3` | non-overlapping |
| `s.replace("a", "o")` | `'bonono'` | all matches |
| `s.replace("a", "o", 1)` | `'bonana'` | first match only |
| `s.upper()` / `s.lower()` | `'BANANA'` / `'banana'` | |
| `"ab Cd".title()` | `'Ab Cd'` | |
| `"ab cd".capitalize()` | `'Ab cd'` | |
| `"aB".swapcase()` | `'Ab'` | |
| `"a.pdf".endswith(".pdf")` | `True` | can take a tuple |
| `"x1".isalnum()` | `True` | |
| `"..a..".strip(".")` | `'a'` | set of characters |
| `"-".join(["a", "b"])` | `'a-b'` | strings only |
| `"a  b".split()` | `['a', 'b']` | ignores extra spaces |
| `"a,,b".split(",")` | `['a', '', 'b']` | |
| `f"{2.5:.3f}"` | `'2.500'` | 3 decimals |

---

## 16. Important Notes

- String methods **never** change the original string. Save the result.
- `find`/`rfind` return **−1** when not found; `index`/`rindex` raise **ValueError**.
- The `end` position in `find(x, start, end)` is **not included**, like a slice.
- `rfind` searches from the right, but its answer is still counted from the left.
- Before slicing with a position from `find`, check that it is not −1.
- `find`, `count`, `replace`, `in`, `startswith`, and `endswith` are **case-sensitive**. Use `lower()` on both sides to ignore case.
- `strip(chars)` removes a **set of characters**, not an exact word.
- `+` needs strings on both sides; use `str()` or an f-string.
- `join` belongs to the separator: `", ".join(items)`. All items must be strings.
- `split()` with no argument ignores extra spaces; `split(" ")` does not.
- The pieces from `split` are strings; convert them before doing math.

---

## 17. Common Mistakes

### Mistake 1: Not saving the result of a method

**Incorrect**

```python
name = "sara"
name.upper()
print(name)
```

```text
sara
```

**Correct**

```python
name = "sara"
name = name.upper()
print(name)
```

```text
SARA
```

### Mistake 2: Slicing with −1 from find()

**Incorrect**

```python
email = "sara.ku.edu"
at = email.find("@")
print(email[:at])
```

```text
sara.ku.ed
```

**Correct**

```python
email = "sara.ku.edu"
at = email.find("@")
if at == -1:
    print("No @ found")
else:
    print(email[:at])
```

```text
No @ found
```

### Mistake 3: Using find when you need the last match

**Incorrect**

```python
file = "report.final.pdf"
dot = file.find(".")
print(file[dot + 1:])
```

```text
final.pdf
```

**Correct**

```python
file = "report.final.pdf"
dot = file.rfind(".")
print(file[dot + 1:])
```

```text
pdf
```

### Mistake 4: Forgetting that searches are case-sensitive

**Incorrect**

```python
text = "Visit KUWAIT Towers"
print(text.find("Kuwait"))
```

```text
-1
```

**Correct**

```python
text = "Visit KUWAIT Towers"
print(text.lower().find("kuwait"))
```

```text
6
```

### Mistake 5: Forgetting the separator's length

**Incorrect** (goal: the text after `"//"`)

```python
url = "https://ku.edu.kw"
start = url.find("//")
print(url[start + 1:])
```

```text
/ku.edu.kw
```

**Correct**

```python
url = "https://ku.edu.kw"
start = url.find("//")
print(url[start + 2:])
```

```text
ku.edu.kw
```

### Mistake 6: Joining a string and a number with +

**Incorrect**

```text
total = 7.5
print("Total: " + total + " KD")

TypeError: can only concatenate str (not "float") to str
```

**Correct**

```python
total = 7.5
print("Total: " + str(total) + " KD")
print(f"Total: {total} KD")
```

```text
Total: 7.5 KD
Total: 7.5 KD
```

### Mistake 7: Calling join on the list

**Incorrect**

```text
names = ["Ali", "Sara"]
print(names.join(", "))

AttributeError: 'list' object has no attribute 'join'
```

**Correct**

```python
names = ["Ali", "Sara"]
print(", ".join(names))
```

```text
Ali, Sara
```

### Mistake 8: Using strip to remove a word

**Incorrect** (goal: remove `".txt"`)

```python
print("report.txt".rstrip(".txt"))
```

```text
repor
```

**Correct**

```python
name = "report.txt"
if name.endswith(".txt"):
    name = name[:-4]
print(name)
```

```text
report
```

### Mistake 9: Doing math with split() pieces

**Incorrect**

```python
parts = "3,4".split(",")
print(parts[0] + parts[1])
```

```text
34
```

**Why?** The pieces are strings, so `+` joins them.

**Correct**

```python
parts = "3,4".split(",")
print(int(parts[0]) + int(parts[1]))
```

```text
7
```

---

## 18. Mini Practice Questions

Try these before looking at the answers at the end of this section.

**Q1.** What does this print?

```python
s = "Kuwait University"
print(s.find("i"), s.rfind("i"), s.count("i"))
```

**Q2.** What does this print?

```python
print("a-b-c-d".replace("-", "+", 2))
```

**Q3.** What is the difference between `"abc".find("z")` and `"abc".index("z")`?

**Q4.** What does this print?

```python
print(" ".join("Kuwait is hot".split()[::-1]))
```

**Q5.** What does this print?

```python
x = 0.5
print(f"{x * 3:.3f} KD")
```

**Q6.** What does this print?

```python
print("xxHixx".strip("x"), "CS126".isalpha(), "photo.PNG".lower().endswith(".png"))
```

### Answers to Mini Practice

1. **`4 14 3`** — the capital `U` is not counted as `i`.
2. **`a+b+c-d`**
3. `find` returns **−1**; `index` raises a **ValueError**.
4. **`hot is Kuwait`**
5. **`1.500 KD`**
6. **`Hi False True`**

---

## 19. Ask AI to Help You Understand

```text
Explain the difference between find() and rfind() in Python using the word "banana".
Draw the indexes in a table and show find("a"), rfind("a"), and find("a", 2).
Do not use loops, and do not give me exercises yet.
```

```text
Show me how to extract the user name, the domain, and the last part of an email
address using find(), rfind(), and slicing. Explain what happens if @ is missing.
```

```text
Why does "report.txt".rstrip(".txt") give "repor"? Explain how strip() with
characters really works, and show a correct way to remove ".txt".
```

```text
Compare three ways to build the text "Sara bought 3 teas for 0.750 KD":
using +, using join(), and using an f-string. Which is easiest to read and why?
```

```text
Give me five "predict the output" questions using find, rfind, replace, upper,
lower, split, and join. Do not use loops. Give hints first and do not show
the answers unless I ask.
```

> **Remember:** Always run the code yourself. AI can make mistakes, and running code is the only way to be sure.

---

## 20. Summary

- **Search:** `find(x, start, end)` gives the first position, `rfind` the last; both return **−1** if `x` is missing. `index`/`rindex` raise **ValueError** instead. `count` counts non-overlapping matches.
- **Extract:** combine a position with slicing — `s[:p]`, `s[p + 1:]`, `s[a + 1:b]` — and always handle −1.
- **Replace:** `replace(old, new)` replaces all matches; `replace(old, new, count)` only the first `count`.
- **Case:** `upper`, `lower`, `title`, `capitalize`, `swapcase`. Use `lower()` on both sides to ignore case.
- **Check:** `startswith`, `endswith` (can take a tuple), `isdigit`, `isalpha`, `isalnum`, `isspace`, `isupper`, `islower`.
- **Clean:** `strip`, `lstrip`, `rstrip` — with an optional **set** of characters.
- **Build:** `+`, `+=`, `*`, `str()`, `"sep".join(list)`, and f-strings with `{value:.3f}`.
- **Break:** `split()` (any spaces) or `split(sep)`; the pieces are strings.
- **Chain** methods from left to right, and **always save** the result: strings never change.

---

## Basic Exercises

> Exercises 1–12 are the same as in the slides. Exercises 13–16 are extra practice.

**Exercise 1.** Predict the output.

```python
s = "banana"
print(s.find("a"), s.rfind("a"))
print(s.find("a", 2), s.find("x"))
```

**Exercise 2.** Predict the output.

```python
t = "Hello World"
print(t.upper())
print(t.swapcase())
print(t.replace("o", "0"))
```

**Exercise 3.** This should print `SARA`. Find the problem and fix it.

```python
name = "sara"
name.upper()
print(name)
```

**Exercise 4.** Predict the output.

```python
words = ["Kuwait", "is", "hot"]
print(" ".join(words))
print("-".join(words))
print("Kuwait  City".split())
```

**Exercise 13.** Predict the output.

```python
s = "Mississippi"
print(s.count("ss"), s.find("ss"), s.rfind("ss"))
```

## Practice Exercises

**Exercise 5.** For `file = "photo.2026.jpg"`, use `rfind` to print the name part (`photo.2026`) and the extension (`jpg`).

**Exercise 6.** For `phone = "965-5123-4567"`, print it with only the **first** dash replaced by a space, then with **all** dashes removed.

**Exercise 7.** For `text = "Welcome to KUWAIT University"`, print whether `"kuwait"` appears (ignoring case) and its position.

**Exercise 8.** Explain the result and give the output.

```python
s = "a,b,,c"
parts = s.split(",")
print(parts, len(parts))
```

**Exercise 14.** For `name = "Noor"` and `gpa = 3.456`, use one f-string to print `Noor has a GPA of 3.46`.

## Challenge Exercises

**Exercise 9.** For `email = "Sara.Ali@KU.edu.kw"`: make it lowercase, then print the user name, the domain, and the last part after the final dot (`kw`).

**Exercise 10.** Count how many times the word `"the"` appears in `"The cat and the hat and THE bat"`, ignoring case.

**Exercise 11.** Predict the output.

```python
s = "2026-10-16"
parts = s.split("-")
print("/".join(parts[::-1]))
print(s.replace("-", "", 1))
print(s.rfind("-") - s.find("-"))
```

**Exercise 12.** Turn `"  python   is   FUN  "` into `"Python is fun"` using `split`, `join`, and one case method.

**Exercise 15.** Hide the middle of a phone number: for `phone = "96551234567"`, keep the first 3 and the last 3 digits and replace the rest with `*`, giving `965*****567`. Your code must work for any length of 7 or more.

**Exercise 16.** For `url = "https://www.ku.edu.kw/cs/index.html"`, print the domain (`www.ku.edu.kw`) using `find` with a start position, and the page name (`index.html`) using `rfind`.

---

# Exercise Solutions

### Solution 1

The first `"a"` is at index 1 and the last at index 5. Searching from index 2, the next `"a"` is at index 3. `"x"` is not found.

```text
1 5
3 -1
```

### Solution 2

```text
HELLO WORLD
hELLO wORLD
Hell0 W0rld
```

`replace` changes every small `o` into the digit `0`.

### Solution 3

There is no error message, but the result is wrong: `upper()` returns a new string, which was not saved, so `name` is still `"sara"`.

```python
name = "sara"
name = name.upper()
print(name)
```

```text
SARA
```

### Solution 4

```text
Kuwait is hot
Kuwait-is-hot
['Kuwait', 'City']
```

`split()` with no argument ignores the double space.

### Solution 5

```python
file = "photo.2026.jpg"
dot = file.rfind(".")
print(file[:dot])
print(file[dot + 1:])
```

```text
photo.2026
jpg
```

`rfind` finds the **last** dot, so `photo.2026` stays together.

### Solution 6

```python
phone = "965-5123-4567"
print(phone.replace("-", " ", 1))
print(phone.replace("-", ""))
```

```text
965 5123-4567
96551234567
```

### Solution 7

```python
text = "Welcome to KUWAIT University"
low = text.lower()
print("kuwait" in low)
print(low.find("kuwait"))
```

```text
True
11
```

### Solution 8

Each comma separates two pieces. Between the two commas in `",,"` there is nothing, so that piece is the empty string `''`. Three commas produce four pieces.

```text
['a', 'b', '', 'c'] 4
```

### Solution 9

```python
email = "Sara.Ali@KU.edu.kw".lower()
at = email.find("@")
print(email[:at])
print(email[at + 1:])
print(email[email.rfind(".") + 1:])
```

```text
sara.ali
ku.edu.kw
kw
```

### Solution 10

```python
s = "The cat and the hat and THE bat"
words = s.lower().split()
print(words.count("the"))
```

```text
3
```

Lowercasing makes `"The"`, `"the"`, and `"THE"` the same. Splitting into words and using the list's `count` makes sure we count whole words only — `s.lower().count("the")` would also count `"the"` inside words such as `"there"` or `"other"`.

### Solution 11

```text
16/10/2026
202610-16
3
```

- `split("-")` gives `['2026', '10', '16']`; `[::-1]` reverses it; `join` puts `/` between the parts.
- `replace` with count 1 removes only the first dash.
- `rfind("-")` is 7 and `find("-")` is 4, so the difference is 3.

### Solution 12

```python
s = "  python   is   FUN  "
neat = " ".join(s.split())
print(neat.capitalize())
```

```text
Python is fun
```

### Solution 13

`"Mississippi"` contains `"ss"` at index 2 and index 5.

```text
2 2 5
```

### Solution 14

```python
name = "Noor"
gpa = 3.456
print(f"{name} has a GPA of {gpa:.2f}")
```

```text
Noor has a GPA of 3.46
```

`:.2f` rounds 3.456 to 3.46 for display.

### Solution 15

```python
phone = "96551234567"
hidden = phone[:3] + "*" * (len(phone) - 6) + phone[-3:]
print(hidden)
```

```text
965*****567
```

The phone has 11 digits. We keep 3 + 3 = 6, so 11 − 6 = 5 stars are needed. The brackets around `len(phone) - 6` make the subtraction happen before the repetition.

### Solution 16

```python
url = "https://www.ku.edu.kw/cs/index.html"
start = url.find("//") + 2
end = url.find("/", start)
print(url[start:end])
print(url[url.rfind("/") + 1:])
```

```text
www.ku.edu.kw
index.html
```

`find("//")` is 6, so the domain starts at 8. Searching for the next `/` from there finds the end of the domain. `rfind("/")` finds the last slash, and the page name is everything after it.

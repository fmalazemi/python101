# CS126 – Introduction to Python

## Tuples

**Instructor:** Dr. Fawaz Alazemi

---

## Learning Objectives

After studying these notes, you should be able to:

1. Explain what a tuple is and why Python has tuples as well as lists.
2. Create tuples, including the empty tuple and a tuple with one item.
3. Read tuple items with indexing and slicing, and use `len()`, `in`, `min()`, `max()`, and `sum()` with tuples.
4. Explain what **immutable** means, and recognize the errors you get when you try to change a tuple.
5. Build new tuples with `+`, `*`, and slicing.
6. Use the two tuple methods `count()` and `index()`.
7. Convert between tuples and lists with `tuple()` and `list()`.
8. **Unpack** a tuple into several variables, and swap two variables in one line.
9. Work with tuples inside tuples and tuples inside lists.
10. Compare tuples with lists and choose the right one for a task.

---

## 1. Introduction

### 1.1 What we know so far

In the previous lectures you learned about **lists**:

```python
days = ["Sun", "Mon", "Tue"]
days[0] = "Sat"
print(days)
```

```text
['Sat', 'Mon', 'Tue']
```

Lists are **mutable**: you can change their items at any time. This is very useful for data that changes, such as a shopping cart or a list of registered students.

### 1.2 The problem: some data should never change

Some data, however, should **stay the same** for the whole program:

- the days of the week,
- the names of the 12 months,
- the six GCC countries,
- the location of Kuwait City on the map,
- a person's date of birth.

If this data is stored in a list, one wrong line of code can change it by accident, and Python will not warn you:

```python
months = ["Jan", "Feb", "Mar"]
months[1] = "February!!"
print(months)
```

```text
['Jan', 'February!!', 'Mar']
```

The program keeps running with wrong data, and the bug may only be found much later.

### 1.3 The solution: tuples

A **tuple** is like a list that is **locked**. You can read its items, but you cannot change, add, or remove them. If any code tries, Python stops immediately with an error, so the mistake is found at once.

```text
months = ("Jan", "Feb", "Mar")
months[1] = "February!!"

TypeError: 'tuple' object does not support item assignment
```

### 1.4 A real-life picture

Think of a **list** as a whiteboard: you can write, erase, and rewrite. A **tuple** is like a printed certificate: you can read it as many times as you like, but you cannot change what is printed. If you need a different certificate, a **new** one must be printed.

---

## 2. Main Concepts and Vocabulary

| Term | Meaning | Example |
|---|---|---|
| **Tuple** | An ordered, immutable collection of values | `(1, 2, 3)` |
| **Immutable** | Cannot be changed after it is created | tuples, strings |
| **Mutable** | Can be changed after it is created | lists |
| **Empty tuple** | A tuple with no items | `()` |
| **One-item tuple** | A tuple with exactly one item; needs a comma | `(5,)` |
| **Packing** | Putting several values into one tuple | `t = 1, 2, 3` |
| **Unpacking** | Taking the items out of a tuple into variables | `a, b, c = t` |
| **Nested tuple** | A tuple that contains other tuples | `((1, 2), (3, 4))` |

---

## 3. Creating Tuples

### 3.1 Syntax

```text
name = (item1, item2, item3, ...)
```

- **Round brackets** (parentheses) `( )` surround the items.
- **Commas** separate the items.

```python
location = (29.37, 47.98)
student = ("Sara", 20, "CS")
gcc = ("Kuwait", "Saudi Arabia", "UAE", "Qatar", "Bahrain", "Oman")
print(location)
print(student)
print(gcc)
print(type(gcc))
```

```text
(29.37, 47.98)
('Sara', 20, 'CS')
('Kuwait', 'Saudi Arabia', 'UAE', 'Qatar', 'Bahrain', 'Oman')
<class 'tuple'>
```

Like lists, tuples can hold any kind of value, and they can mix types.

### 3.2 The empty tuple

```python
empty = ()
print(empty)
print(len(empty))
```

```text
()
0
```

An empty tuple is less useful than an empty list, because you cannot add items to it later.

### 3.3 The comma makes the tuple

In fact, it is the **commas** that create a tuple, not the brackets. The brackets are optional in many places:

```python
nums = 1, 2, 3
print(nums)
print(type(nums))
```

```text
(1, 2, 3)
<class 'tuple'>
```

Writing values separated by commas like this is called **packing**. Even though the brackets are optional, it is good style to write them, because they make the code easier to read.

### 3.4 A tuple with one item needs a comma

This is the most surprising rule about tuples:

```python
a = (5)
b = (5,)
print(a, type(a))
print(b, type(b))
```

```text
5 <class 'int'>
(5,) <class 'tuple'>
```

Why? Round brackets are also used in arithmetic, for example `(2 + 3) * 4`. So Python reads `(5)` as "the number 5 in brackets". To make a one-item tuple, you **must** add a comma after the item: `(5,)`.

The same applies to strings:

```python
x = ("Kuwait")
y = ("Kuwait",)
print(type(x), len(x))
print(type(y), len(y))
```

```text
<class 'str'> 6
<class 'tuple'> 1
```

`x` is a string of 6 characters. `y` is a tuple containing one item.

### 3.5 Creating a tuple from a list or a string

The `tuple()` function converts a list or a string into a tuple:

```python
print(tuple([10, 20, 30]))
print(tuple("KWT"))
print(tuple())
```

```text
(10, 20, 30)
('K', 'W', 'T')
()
```

With a string, each **character** becomes one item.

---

## 4. Reading Tuples

Reading a tuple works **exactly** like reading a list. Everything you learned about indexes and slices applies.

### 4.1 Indexing

```python
days = ("Sun", "Mon", "Tue", "Wed")
print(days[0])
print(days[2])
print(days[-1])
print(days[-2])
```

```text
Sun
Tue
Wed
Tue
```

| Item | "Sun" | "Mon" | "Tue" | "Wed" |
|---|---|---|---|---|
| Positive index | 0 | 1 | 2 | 3 |
| Negative index | −4 | −3 | −2 | −1 |

An index that does not exist causes an `IndexError`:

```text
days = ("Sun", "Mon", "Tue", "Wed")
print(days[4])

IndexError: tuple index out of range
```

### 4.2 Slicing

A slice of a tuple is a **new tuple**:

```python
days = ("Sun", "Mon", "Tue", "Wed", "Thu")
print(days[1:3])
print(days[:2])
print(days[-2:])
print(days[::-1])
```

```text
('Mon', 'Tue')
('Sun', 'Mon')
('Wed', 'Thu')
('Thu', 'Wed', 'Tue', 'Mon', 'Sun')
```

The usual slicing rules apply: the stop index is not included, and a slice never causes an `IndexError`.

### 4.3 Functions that read a tuple

Functions that only **read** data work on tuples just like on lists:

```python
prices = (2.5, 1.25, 4, 0.75)
print(len(prices))
print(min(prices))
print(max(prices))
print(sum(prices))
print(sum(prices) / len(prices))
```

```text
4
0.75
4
8.5
2.125
```

The same rules as for lists apply: `sum()` needs numbers, and `min()`/`max()` need items that can be compared with each other.

### 4.4 Membership: in and not in

```python
weekend = ("Fri", "Sat")
day = "Fri"
if day in weekend:
    print(day, "is a weekend day")
print("Sun" not in weekend)
```

```text
Fri is a weekend day
True
```

---

## 5. Tuples Are Immutable

### 5.1 You cannot change an item

```text
scores = (80, 90, 70)
scores[0] = 85

TypeError: 'tuple' object does not support item assignment
```

### 5.2 You cannot add or remove items

Tuples do **not** have methods such as `append()`, `insert()`, `extend()`, `remove()`, `sort()`, or `reverse()`. All of these methods change a list, and a tuple cannot be changed.

```text
scores = (80, 90, 70)
scores.append(60)

AttributeError: 'tuple' object has no attribute 'append'
```

An `AttributeError` means "this type of value does not have that method".

### 5.3 Tuples and strings are alike

You have already met another immutable type: the **string**. Strings and tuples both allow reading (indexing, slicing, `len`, `in`) but do not allow changing.

| | String | Tuple | List |
|---|---|---|---|
| Holds | characters | any values | any values |
| Read with index / slice | ✔ | ✔ | ✔ |
| Change an item | ✘ | ✘ | ✔ |
| Mutable? | No | No | Yes |

### 5.4 Why is immutability useful?

1. **Safety:** data that must not change is protected from mistakes.
2. **Clear meaning:** when another programmer sees a tuple, they know the data is fixed.
3. **Records:** a tuple naturally represents one "record" whose parts belong together, such as `(day, month, year)`.

---

## 6. Building New Tuples

Even though a tuple cannot change, you can always build a **new** tuple from it. Then you can give the new tuple the same variable name.

### 6.1 Concatenation with +

```python
a = (1, 2)
b = (3, 4)
c = a + b
print(c)
print(a)
print(b)
```

```text
(1, 2, 3, 4)
(1, 2)
(3, 4)
```

`a` and `b` did not change; `c` is a new tuple.

Both sides of `+` must be **tuples**. To add a single item, wrap it in a one-item tuple:

```python
days = ("Sun", "Mon")
days = days + ("Tue",)
print(days)
```

```text
('Sun', 'Mon', 'Tue')
```

`days + "Tue"` would cause a `TypeError`, and `days + ["Tue"]` too, because you cannot join a tuple with a string or a list.

### 6.2 Repetition with *

```python
print((0,) * 5)
print(("Ha", "!") * 2)
```

```text
(0, 0, 0, 0, 0)
('Ha', '!', 'Ha', '!')
```

### 6.3 Replacing an item by building a new tuple

Combine slicing and `+`:

```python
date = (12, 10, 2026)
date = (13,) + date[1:]
print(date)
```

```text
(13, 10, 2026)
```

Step by step:

1. `date[1:]` is `(10, 2026)`.
2. `(13,) + (10, 2026)` is `(13, 10, 2026)`, a **new** tuple.
3. The name `date` now refers to the new tuple. The old tuple was not changed.

Replacing an item in the middle:

```python
rgb = (255, 128, 0)
rgb = rgb[:1] + (200,) + rgb[2:]
print(rgb)
```

```text
(255, 200, 0)
```

### 6.4 The convert–change–convert pattern

Another way is to convert to a list, change the list, and convert back:

```python
rgb = (255, 128, 0)
temp = list(rgb)
temp[1] = 200
rgb = tuple(temp)
print(rgb)
```

```text
(255, 200, 0)
```

This pattern is clear and easy to read, especially when you change several items. But if you find yourself changing a tuple often, the data should probably be a **list** instead.

---

## 7. Tuple Methods: count() and index()

Tuples have only **two** methods, and neither of them changes the tuple.

### 7.1 count(x)

Returns how many times `x` appears:

```python
votes = ("yes", "no", "yes", "yes")
print(votes.count("yes"))
print(votes.count("no"))
print(votes.count("maybe"))
```

```text
3
1
0
```

### 7.2 index(x)

Returns the position of the **first** `x`:

```python
votes = ("yes", "no", "yes", "yes")
print(votes.index("no"))
print(votes.index("yes"))
```

```text
1
0
```

If `x` is not in the tuple, `index()` causes a `ValueError`. Check with `in` first:

```python
gcc = ("Kuwait", "Qatar", "Oman")
country = "Egypt"
if country in gcc:
    print(country, "is at index", gcc.index(country))
else:
    print(country, "is not in the tuple")
```

```text
Egypt is not in the tuple
```

---

## 8. Comparing Tuples

### 8.1 Equality

Two tuples are equal if they have the same items in the same order:

```python
print((1, 2) == (1, 2))
print((1, 2) == (2, 1))
print((1, 2) != (1, 3))
```

```text
True
False
True
```

A tuple is **never** equal to a list, even with the same items, because they are different types:

```python
print((1, 2) == [1, 2])
print(list((1, 2)) == [1, 2])
```

```text
False
True
```

### 8.2 Order: < and >

Tuples are compared **item by item**, like words in a dictionary. Python compares the first items; if they are equal, it compares the second items, and so on:

```python
print((2, 9) < (2, 10))
print((1, 5) < (2, 0))
print((3, 1) > (3,))
```

```text
True
True
True
```

- `(2, 9) < (2, 10)`: the first items are equal (2), so Python compares 9 and 10.
- `(1, 5) < (2, 0)`: the first items already decide: 1 < 2.
- `(3, 1) > (3,)`: when one tuple is the start of the other, the shorter one is smaller.

This is useful for things like dates stored as `(year, month, day)`:

```python
exam = (2026, 12, 20)
today = (2026, 10, 12)
if today < exam:
    print("The exam has not happened yet")
```

```text
The exam has not happened yet
```

---

## 9. Unpacking

### 9.1 What is unpacking?

**Unpacking** takes the items out of a tuple and stores each one in its own variable, in a single line:

```python
student = ("Sara", 20, "CS")
name, age, major = student
print(name)
print(age)
print(major)
```

```text
Sara
20
CS
```

Each variable on the left gets the item at the **same position** on the right:

| Variable | Item |
|---|---|
| `name` | `student[0]` → `"Sara"` |
| `age` | `student[1]` → `20` |
| `major` | `student[2]` → `"CS"` |

Unpacking is the same as writing three assignments, but shorter and clearer:

```python
student = ("Sara", 20, "CS")
name = student[0]
age = student[1]
major = student[2]
print(name, age, major)
```

```text
Sara 20 CS
```

### 9.2 The numbers must match

The number of variables must equal the number of items:

```text
student = ("Sara", 20, "CS")
name, age = student

ValueError: too many values to unpack (expected 2)
```

```text
point = (29, 47)
x, y, z = point

ValueError: not enough values to unpack (expected 3, got 2)
```

### 9.3 Packing and unpacking together

You can create several variables in one line. The right side is packed into a tuple, and then unpacked into the variables:

```python
city, code = "Kuwait City", 965
print(city)
print(code)
```

```text
Kuwait City
965
```

### 9.4 Swapping two variables

With unpacking, you can swap two variables **without** a temporary variable:

```python
a = 3
b = 8
a, b = b, a
print(a, b)
```

```text
8 3
```

How it works:

1. Python first evaluates the right side `b, a`. This builds the tuple `(8, 3)`.
2. Then it unpacks: `a` gets 8 and `b` gets 3.

Because the right side is fully built **before** any variable changes, no value is lost.

### 9.5 Unpacking lists

Unpacking also works with lists (and strings):

```python
first, second = [10, 20]
x, y, z = "abc"
print(first, second)
print(x, y, z)
```

```text
10 20
a b c
```

---

## 10. Nested Tuples and Tuples in Lists

### 10.1 A tuple of tuples

```python
capitals = (("Kuwait City", 965),
            ("Riyadh", 966),
            ("Doha", 974))
print(capitals[1])
print(capitals[2][0])
print(capitals[0][1])
city, code = capitals[0]
print(city, "+" + str(code))
```

```text
('Riyadh', 966)
Doha
965
Kuwait City +965
```

Use two indexes: the first chooses the inner tuple, the second chooses the item inside it.

### 10.2 A list of tuples

A very common combination: a **list** (which can grow and change) that contains **tuples** (fixed records):

```python
points = [(29, 47), (25, 51)]
print(points[0])
points[1] = (24, 54)
print(points)
```

```text
(29, 47)
[(29, 47), (24, 54)]
```

- `points[1] = (24, 54)` is allowed: we replaced an **item of the list** with a new tuple.
- `points[1][0] = 24` would **not** be allowed: that tries to change the tuple itself.

---

## 11. Lists vs Tuples

### 11.1 Side-by-side comparison

| | List | Tuple |
|---|---|---|
| Brackets | `[1, 2, 3]` | `(1, 2, 3)` |
| Empty | `[]` | `()` |
| One item | `[5]` | `(5,)` |
| Type name | `list` | `tuple` |
| Mutable? | Yes | No |
| Index, slice, `len`, `in` | ✔ | ✔ |
| `min`, `max`, `sum` | ✔ | ✔ |
| `+` and `*` | ✔ (new list) | ✔ (new tuple) |
| `x[i] = value` | ✔ | ✘ `TypeError` |
| `append`, `insert`, `extend`, `remove`, `sort`, `reverse` | ✔ | ✘ `AttributeError` |
| `count`, `index` | ✔ | ✔ |
| Convert | `list(t)` | `tuple(lst)` |
| Typical use | a collection that grows or changes | a fixed group of related values |

### 11.2 How to choose

**Choose a tuple when:**

- the data must **not change** (months, GCC countries, fixed settings),
- the values form **one record** whose positions have meaning: a date `(day, month, year)`, a location `(latitude, longitude)`, a color `(red, green, blue)`,
- you want Python to **protect** the data from accidental changes.

**Choose a list when:**

- items will be **added, removed, or changed** (shopping cart, to-do list),
- the **number** of items is not fixed (registered students, messages),
- you want to **sort** or edit the items.

A simple rule: *"Will this data change while the program runs?"* If yes → list. If no → tuple.

---

## 12. Worked Examples

### 12.1 A location

```python
kuwait_city = (29.37, 47.98)
lat, lon = kuwait_city
print("Latitude:", lat)
print("Longitude:", lon)
if lat > 0:
    print("North of the equator")
else:
    print("South of the equator")
```

```text
Latitude: 29.37
Longitude: 47.98
North of the equator
```

A location is two numbers that belong together and do not change, so a tuple is a natural choice.

### 12.2 Updating a student record

```python
record = (2026014, "Ali", "Math")
print("Before:", record)
record = record[:2] + ("CS",)
print("After:", record)
sid, name, major = record
print(name, "(" + str(sid) + ") studies", major)
```

```text
Before: (2026014, 'Ali', 'Math')
After: (2026014, 'Ali', 'CS')
Ali (2026014) studies CS
```

The record is "updated" by building a new tuple on purpose. It cannot change by accident somewhere else in the program.

### 12.3 Days of the week

```python
WEEK = ("Sun", "Mon", "Tue", "Wed", "Thu", "Fri", "Sat")
WEEKEND = ("Fri", "Sat")
today = "Thu"
num = WEEK.index(today)
tomorrow = WEEK[num + 1]
print(today, "is day", num + 1, "of", len(WEEK))
print("Tomorrow is", tomorrow)
if tomorrow in WEEKEND:
    print("Tomorrow is the weekend!")
```

```text
Thu is day 5 of 7
Tomorrow is Fri
Tomorrow is the weekend!
```

Note: if `today` were `"Sat"`, `num + 1` would be 7, and `WEEK[7]` would cause an `IndexError`. You will learn a neat way to "wrap around" to the start later; for now, an `if` can handle it:

```python
WEEK = ("Sun", "Mon", "Tue", "Wed", "Thu", "Fri", "Sat")
today = "Sat"
num = WEEK.index(today)
if num == len(WEEK) - 1:
    tomorrow = WEEK[0]
else:
    tomorrow = WEEK[num + 1]
print("Tomorrow is", tomorrow)
```

```text
Tomorrow is Sun
```

### 12.4 A football result

```python
match = ("Qadsia", 2, "Kuwait SC", 3)
home, hg, away, ag = match
print(home, hg, "-", ag, away)
if hg > ag:
    print("Winner:", home)
elif ag > hg:
    print("Winner:", away)
else:
    print("Draw")
```

```text
Qadsia 2 - 3 Kuwait SC
Winner: Kuwait SC
```

---

## 13. Important Notes

- A one-item tuple needs a comma: `(5,)`. `(5)` is just the number 5.
- The **commas** make a tuple; brackets are optional but recommended.
- Reading a tuple (index, slice, `len`, `in`, `min`, `max`, `sum`) works exactly like a list.
- A slice of a tuple is a tuple.
- Tuples are **immutable**: `t[i] = x` is a `TypeError`; `append` and the other changing methods do not exist (`AttributeError`).
- `+`, `*`, and slicing create **new** tuples. `+` needs a tuple on both sides.
- Tuples have only two methods: `count()` and `index()`. `index()` fails with `ValueError` if the item is missing.
- A tuple is never `==` to a list.
- When unpacking, the number of variables must equal the number of items.
- `a, b = b, a` swaps two variables.

---

## 14. Common Mistakes

### Mistake 1: Forgetting the comma in a one-item tuple

**Incorrect**

```python
colors = ("red")
print(type(colors))
print(len(colors))
```

```text
<class 'str'>
3
```

**Why?** Without a comma, `("red")` is just the string `"red"`, so `len()` counted its 3 letters.

**Correct**

```python
colors = ("red",)
print(type(colors))
print(len(colors))
```

```text
<class 'tuple'>
1
```

### Mistake 2: Trying to change an item

**Incorrect**

```text
date = (12, 10, 2026)
date[0] = 13

TypeError: 'tuple' object does not support item assignment
```

**Correct** — build a new tuple:

```python
date = (12, 10, 2026)
date = (13,) + date[1:]
print(date)
```

```text
(13, 10, 2026)
```

### Mistake 3: Using list methods on a tuple

**Incorrect**

```text
cart = ("rice", "tea")
cart.append("milk")

AttributeError: 'tuple' object has no attribute 'append'
```

**Why?** A tuple cannot grow. A shopping cart changes, so it should be a **list** from the start.

**Correct**

```python
cart = ["rice", "tea"]
cart.append("milk")
print(cart)
```

```text
['rice', 'tea', 'milk']
```

### Mistake 4: Joining a tuple with a single value

**Incorrect**

```text
days = ("Sun", "Mon")
days = days + "Tue"

TypeError: can only concatenate tuple (not "str") to tuple
```

**Correct**

```python
days = ("Sun", "Mon")
days = days + ("Tue",)
print(days)
```

```text
('Sun', 'Mon', 'Tue')
```

### Mistake 5: Wrong number of variables when unpacking

**Incorrect**

```text
student = ("Sara", 20, "CS")
name, age = student

ValueError: too many values to unpack (expected 2)
```

**Correct**

```python
student = ("Sara", 20, "CS")
name, age, major = student
print(name, age, major)
```

```text
Sara 20 CS
```

### Mistake 6: index() on a missing value

**Incorrect**

```text
gcc = ("Kuwait", "Qatar", "Oman")
print(gcc.index("Egypt"))

ValueError: tuple.index(x): x not in tuple
```

**Correct**

```python
gcc = ("Kuwait", "Qatar", "Oman")
if "Egypt" in gcc:
    print(gcc.index("Egypt"))
else:
    print("Egypt is not in the tuple")
```

```text
Egypt is not in the tuple
```

### Mistake 7: Comparing a tuple with a list

**Incorrect** (expecting `True`)

```python
answer = (1, 2, 3)
print(answer == [1, 2, 3])
```

```text
False
```

**Why?** A tuple and a list are different types, so they are never equal.

**Correct**

```python
answer = (1, 2, 3)
print(answer == (1, 2, 3))
print(list(answer) == [1, 2, 3])
```

```text
True
True
```

---

## 15. Mini Practice Questions

Try these before looking at the answers at the end of this section.

**Q1.** What does this print?

```python
t = ("a", "b", "c", "d")
print(t[1], t[-1], t[1:3])
```

**Q2.** What is the type of each variable?

```text
p = (3)
q = (3,)
r = 3, 4
s = ()
```

**Q3.** What does this print?

```python
t = (4, 5, 6)
x, y, z = t
print(z, x + y, t[1:])
```

**Q4.** Which line causes an error, and which error?

```text
A: t = (1, 2); print(t + (3,))
B: t = (1, 2); t[0] = 5
C: t = (1, 2); print(t * 2)
```

**Q5.** What does this print?

```python
print((1, 2, 3) < (1, 3), (1, 2) == [1, 2])
```

**Q6.** What does this print?

```python
t = ("x", "y", "x", "z", "x")
print(t.count("x"), t.index("z"))
```

### Answers to Mini Practice

1. **`b d ('b', 'c')`**
2. `p` is an **int**; `q`, `r`, and `s` are **tuples**.
3. **`6 9 (5, 6)`**
4. **B** causes a `TypeError` (tuples cannot be changed). A prints `(1, 2, 3)`; C prints `(1, 2, 1, 2)`.
5. **`True False`** — 2 < 3 decides the first; a tuple is never equal to a list.
6. **`3 3`**

---

## 16. Ask AI to Help You Understand

```text
Explain the difference between Python lists and tuples to a beginner.
Use one example from daily life in Kuwait for each.
Do not use loops, and do not give me exercises yet.
```

```text
Why is (5) not a tuple in Python, but (5,) is? Explain with three small examples.
```

```text
Explain tuple unpacking step by step, including how a, b = b, a swaps two variables.
Show what happens in memory using a simple text drawing.
```

```text
If tuples cannot be changed, how can I "update" a tuple? Show me two different ways,
and explain when I should use a list instead.
```

```text
Give me five situations and ask me whether each one should use a list or a tuple.
Wait for my answer each time before telling me if I am right and why.
```

> **Remember:** Always run the code yourself. AI can make mistakes, and running code is the only way to be sure.

---

## 17. Summary

- A **tuple** is an ordered collection of values in round brackets: `(1, 2, 3)`.
- The **commas** make a tuple. A one-item tuple needs a comma: `(5,)`. `()` is the empty tuple.
- Tuples are read like lists: indexes, negative indexes, slices (which give tuples), `len`, `in`, `min`, `max`, `sum`.
- Tuples are **immutable**: no item assignment and no `append`, `remove`, `sort`, etc.
- `+`, `*`, and slicing build **new** tuples. `tuple()` and `list()` convert between the two types.
- The only tuple methods are `count()` and `index()`.
- Tuples compare item by item; a tuple is never equal to a list.
- **Unpacking** puts each item into its own variable: `a, b, c = t`. `a, b = b, a` swaps.
- Use a **tuple** for fixed data and records; use a **list** for data that changes.

---

## Basic Exercises

> Exercises 1–12 are the same as in the slides. Exercises 13–16 are extra practice.

**Exercise 1.** Predict the output.

```python
t = (10, 20, 30, 40)
print(t[1], t[-1], len(t))
print(t[1:3])
```

**Exercise 2.** Predict the output.

```python
a = (5)
b = (5,)
c = 5, 6
print(type(a), type(b), type(c))
```

**Exercise 3.** This should make `"Sat"` the first day. Find the error and fix it **without** changing the tuple into a list.

```text
days = ("Sun", "Mon", "Tue")
days[0] = "Sat"
```

**Exercise 4.** Predict the output.

```python
t = (3, 1, 3, 2, 3)
print(t.count(3), t.index(2), 3 in t)
```

**Exercise 13.** Predict the output.

```python
t = ("a",)
print(len(t), t * 3)
```

## Practice Exercises

**Exercise 5.** Store Kuwait's information in a tuple: `("Kuwait", "Kuwait City", "KWD", 965)`. Unpack it and print:

```text
Kuwait: capital Kuwait City, currency KWD, code +965
```

**Exercise 6.** For `prices = (2.5, 1.25, 4, 0.75)`, print the lowest, the highest, the total, and the average.

**Exercise 7.** A color is stored as `rgb = (255, 128, 0)`. Use `list()` and `tuple()` to change the middle value to 200, then print the new tuple.

**Exercise 8.** Explain what this code does and give its output.

```python
a, b = 3, 8
a, b = b, a
print(a, b)
```

**Exercise 14.** A date is stored as `date = (12, 10, 2026)`. Unpack it into `day`, `month`, and `year`, then print it as `12/10/2026` using `str()` and `+`.

## Challenge Exercises

**Exercise 9.** Join the two tuples into `week`. Print `week`, its length, the index of `"Fri"`, and the last two days.

```python
weekdays = ("Sun", "Mon", "Tue", "Wed", "Thu")
weekend = ("Fri", "Sat")
```

**Exercise 10.** Print Mona's mark. Then explain why `students[0][1] = 85` fails, and give Ali 85 by building a **new** `students` tuple.

```python
students = (("Ali", 80), ("Mona", 95))
```

**Exercise 11.** Predict the output.

```python
t = (1, 2) * 2 + (3,)
print(t, len(t), t.count(2))
```

**Exercise 12.** List or tuple? Choose for each and give a reason:

1. The names of the 12 months
2. A shopping cart
3. The GPS location of Jaber Al-Ahmad Stadium
4. Students currently registered in CS126

**Exercise 15.** A tuple of exam scores is `scores = (72, 95, 58, 88)`. Produce a **sorted** tuple `(58, 72, 88, 95)`. (Hint: tuples have no `sort()`, but lists do.)

**Exercise 16.** App versions are often written like `"2.9"` and `"2.10"`. Store them as tuples `(2, 9)` and `(2, 10)`, and compare them. Then compare the **strings** `"2.10" > "2.9"`. Print both results and explain why they are different.

---

# Exercise Solutions

### Solution 1

Index 1 is `20`, the last item is `40`, there are 4 items, and the slice `t[1:3]` is a new tuple with indexes 1 and 2.

```text
20 40 4
(20, 30)
```

### Solution 2

`(5)` has no comma, so it is just an integer. `(5,)` and `5, 6` contain commas, so they are tuples.

```text
<class 'int'> <class 'tuple'> <class 'tuple'>
```

### Solution 3

A tuple cannot be changed, so `days[0] = "Sat"` causes a `TypeError`. Build a new tuple from `"Sat"` and the rest of the old one:

```python
days = ("Sun", "Mon", "Tue")
days = ("Sat",) + days[1:]
print(days)
```

```text
('Sat', 'Mon', 'Tue')
```

### Solution 4

`3` appears three times; the first `2` is at index 3; `3 in t` is `True`.

```text
3 3 True
```

### Solution 5

```python
info = ("Kuwait", "Kuwait City", "KWD", 965)
country, capital, currency, code = info
msg = country + ": capital " + capital
msg = msg + ", currency " + currency
print(msg + ", code +" + str(code))
```

```text
Kuwait: capital Kuwait City, currency KWD, code +965
```

`code` is a number, so it must be converted with `str()` before joining.

### Solution 6

```python
prices = (2.5, 1.25, 4, 0.75)
print("Lowest:", min(prices))
print("Highest:", max(prices))
print("Total:", sum(prices))
print("Average:", sum(prices) / len(prices))
```

```text
Lowest: 0.75
Highest: 4
Total: 8.5
Average: 2.125
```

### Solution 7

```python
rgb = (255, 128, 0)
temp = list(rgb)
temp[1] = 200
rgb = tuple(temp)
print(rgb)
```

```text
(255, 200, 0)
```

### Solution 8

The code **swaps** the values of `a` and `b`. The right side `b, a` first builds the tuple `(8, 3)`; then it is unpacked so that `a` gets 8 and `b` gets 3.

```text
8 3
```

### Solution 9

```python
weekdays = ("Sun", "Mon", "Tue", "Wed", "Thu")
weekend = ("Fri", "Sat")
week = weekdays + weekend
print(week)
print(len(week), week.index("Fri"))
print(week[-2:])
```

```text
('Sun', 'Mon', 'Tue', 'Wed', 'Thu', 'Fri', 'Sat')
7 5
('Fri', 'Sat')
```

### Solution 10

`students[0]` is the tuple `("Ali", 80)`. Tuples cannot be changed, so `students[0][1] = 85` causes a `TypeError`. Instead, build a new outer tuple containing a new inner tuple for Ali and the unchanged tuple for Mona:

```python
students = (("Ali", 80), ("Mona", 95))
print(students[1][1])
students = (("Ali", 85), students[1])
print(students)
```

```text
95
(('Ali', 85), ('Mona', 95))
```

### Solution 11

`*` is done before `+`: `(1, 2) * 2` is `(1, 2, 1, 2)`, then `+ (3,)` gives `(1, 2, 1, 2, 3)`. It has 5 items, and `2` appears twice.

```text
(1, 2, 1, 2, 3) 5 2
```

### Solution 12

| | Choice | Reason |
|---|---|---|
| 1. Months | **Tuple** | The 12 month names never change. |
| 2. Shopping cart | **List** | Items are added and removed. |
| 3. Stadium location | **Tuple** | Two fixed numbers that form one location. |
| 4. Registered students | **List** | Students add and drop the course, so the collection changes. |

### Solution 13

`("a",)` is a one-item tuple. `* 3` repeats it.

```text
1 ('a', 'a', 'a')
```

### Solution 14

```python
date = (12, 10, 2026)
day, month, year = date
print(str(day) + "/" + str(month) + "/" + str(year))
```

```text
12/10/2026
```

### Solution 15

Convert to a list, sort the list, and convert back:

```python
scores = (72, 95, 58, 88)
temp = list(scores)
temp.sort()
scores = tuple(temp)
print(scores)
```

```text
(58, 72, 88, 95)
```

### Solution 16

```python
v1 = (2, 10)
v2 = (2, 9)
print(v1 > v2)
print("2.10" > "2.9")
```

```text
True
False
```

- The **tuples** are compared item by item as numbers: the first items are equal (2), and then 10 > 9, so `(2, 10)` is the newer version.
- The **strings** are compared character by character: `"2"` equals `"2"`, `"."` equals `"."`, and then `"1"` is compared with `"9"`. Since `"1"` comes before `"9"`, `"2.10"` is considered smaller.

This is a good example of choosing the right data type: storing version numbers as tuples of integers gives the correct order.

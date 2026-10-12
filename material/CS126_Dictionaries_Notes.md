# CS126 – Introduction to Python

## Dictionaries

**Instructor:** Dr. Fawaz Alazemi

---

## Learning Objectives

After studying these notes, you should be able to:

1. Explain what a dictionary is: a collection of **key → value** pairs.
2. Create dictionaries, including the empty dictionary `{}`.
3. Read values with `d[key]` and `d.get(key, default)`, and explain when each one is the better choice.
4. Add, change, and remove pairs with `d[key] = value`, `del`, `pop()`, and `clear()`.
5. Use `in`, `len()`, `keys()`, `values()`, `items()`, `update()`, and `sorted()` with dictionaries.
6. State the rules for keys (unique, immutable) and store lists or dictionaries as values.
7. Use a dictionary as a **lookup table** and as a **counter**.
8. Recognize and fix `KeyError` and other common dictionary mistakes.
9. Compare dictionaries with lists, tuples, and sets, and choose the right structure for a task.

---

## 1. Introduction

### 1.1 The problem: finding things by name

So far, you have three ways to store many values:

- a **list** — ordered, changeable,
- a **tuple** — ordered, fixed,
- a **set** — unique items, no order.

With lists and tuples you find an item by its **position**. With sets you can only ask whether an item is **in** the set. But very often we want to find information by a **name** or an **ID**:

- What is **Sara's** phone number?
- What is the price of **tea**?
- What is the capital of **Qatar**?
- What is the name of the student with ID **2026014**?

Here is a phone book built from two lists:

```python
names = ["Ali", "Sara", "Mona"]
phones = ["55512345", "66698765", "99911122"]
i = names.index("Sara")
print(phones[i])
```

```text
66698765
```

This works, but it is fragile:

- We first have to find the **position** of `"Sara"`, then use that position in the other list.
- The two lists must stay in **exactly** the same order forever. If someone adds a name to one list but forgets the other, every number after it belongs to the wrong person.

### 1.2 The solution: a dictionary

A **dictionary** connects each name directly to its value:

```python
phones = {"Ali": "55512345",
          "Sara": "66698765",
          "Mona": "99911122"}
print(phones["Sara"])
```

```text
66698765
```

There are no positions to calculate and no second list to keep in order. Each name is tied to its own number.

### 1.3 A real-life picture

Think of a real dictionary (or a phone book). You look up a **word**, and you find its **meaning**. You never ask for "the 1,207th word" — you look it up by the word itself.

In Python:

- the **word** is called the **key**,
- the **meaning** is called the **value**,
- together they form a **key-value pair**.

---

## 2. Main Concepts and Vocabulary

| Term | Meaning | Example |
|---|---|---|
| **Dictionary** | A collection of key-value pairs | `{"tea": 0.25}` |
| **Key** | The name used to look up a value; unique | `"tea"` |
| **Value** | The data stored for a key | `0.25` |
| **Pair** (item) | One key together with its value | `"tea": 0.25` |
| **Empty dictionary** | A dictionary with no pairs | `{}` |
| **Lookup** | Finding a value by its key | `menu["tea"]` |
| **KeyError** | The error when a key does not exist | `menu["pizza"]` |
| **`None`** | Python's special value meaning "nothing" | what `get()` returns for a missing key |

---

## 3. Creating Dictionaries

### 3.1 Syntax

```text
name = {key1: value1, key2: value2, ...}
```

- **Curly brackets** `{ }` surround the pairs.
- A **colon** `:` separates each key from its value.
- **Commas** separate the pairs.

```python
menu = {"tea": 0.25, "coffee": 1.0, "juice": 0.75}
student = {"name": "Sara", "age": 20, "major": "CS"}
codes = {965: "Kuwait", 966: "Saudi Arabia"}
print(menu)
print(student)
print(codes)
print(type(menu))
```

```text
{'tea': 0.25, 'coffee': 1.0, 'juice': 0.75}
{'name': 'Sara', 'age': 20, 'major': 'CS'}
{965: 'Kuwait', 966: 'Saudi Arabia'}
<class 'dict'>
```

- Keys are often **strings**, but numbers (and tuples) can be keys too.
- Values can be **any** type, and different pairs can have different value types.
- The type name is `dict`.

### 3.2 The empty dictionary

```python
empty = {}
print(empty)
print(len(empty))
print(type(empty))
```

```text
{}
0
<class 'dict'>
```

This is why an **empty set** must be written `set()`: the curly brackets `{}` were already taken by dictionaries.

### 3.3 Long dictionaries on several lines

Inside curly brackets you may continue on the next line. This makes larger dictionaries much easier to read:

```python
caps = {
    "Kuwait": "Kuwait City",
    "Saudi Arabia": "Riyadh",
    "Qatar": "Doha",
}
print(len(caps))
```

```text
3
```

A comma after the last pair is allowed and is common in this style.

### 3.4 Order

Python remembers the order in which pairs were **added**, and it prints them in that order. But you never use this order to **find** a value — you always use the key.

---

## 4. Reading Values

### 4.1 With square brackets: d[key]

```python
student = {"name": "Sara", "age": 20, "major": "CS"}
print(student["name"])
print(student["age"] + 1)
print("Major: " + student["major"])
```

```text
Sara
21
Major: CS
```

`student["age"]` is the value `20`, so it can be used in arithmetic, joined to strings, compared in `if` statements, and so on.

### 4.2 KeyError

If the key does not exist, Python stops with a `KeyError`:

```text
student = {"name": "Sara", "age": 20, "major": "CS"}
print(student["gpa"])

KeyError: 'gpa'
```

Keys are **case-sensitive**, so `student["Name"]` is also a `KeyError`.

### 4.3 There are no positions

The square brackets of a dictionary contain a **key**, not a position:

```text
student = {"name": "Sara", "age": 20}
print(student[0])

KeyError: 0
```

Python looked for a key equal to the number 0 and did not find one. A dictionary has no "first item" that you can reach with an index.

### 4.4 Safe reading with get()

`d.get(key)` returns the value if the key exists, and `None` if it does not. With a second argument, `d.get(key, default)` returns `default` instead of `None`:

```python
stock = {"rice": 10, "tea": 4}
print(stock.get("rice"))
print(stock.get("milk"))
print(stock.get("milk", 0))
print(stock.get("tea", 0))
```

```text
10
None
0
4
```

| Code | Key exists | Key missing |
|---|---|---|
| `d[k]` | the value | `KeyError` |
| `d.get(k)` | the value | `None` |
| `d.get(k, x)` | the value | `x` |

`get()` only **reads**. It never adds a key to the dictionary:

```python
stock = {"rice": 10}
print(stock.get("milk", 0))
print(stock)
```

```text
0
{'rice': 10}
```

**Which one should you use?**

- Use `d[k]` when the key **must** be there. If it is missing, the error tells you something is wrong.
- Use `d.get(k, default)` when a missing key is **normal** and you have a sensible default.

---

## 5. Checking Keys and Counting Pairs

### 5.1 in and not in check keys

```python
caps = {"Kuwait": "Kuwait City", "Qatar": "Doha", "Oman": "Muscat"}
print("Qatar" in caps)
print("Bahrain" in caps)
print("Bahrain" not in caps)
print("Doha" in caps)
```

```text
True
False
True
False
```

`in` looks only at the **keys**. `"Doha"` is a value, not a key, so `"Doha" in caps` is `False`. To search the values, use `values()` (Section 8).

`in` is the classic way to avoid a `KeyError`:

```python
caps = {"Kuwait": "Kuwait City", "Qatar": "Doha", "Oman": "Muscat"}
country = "Bahrain"
if country in caps:
    print(caps[country])
else:
    print(country, "is not in the dictionary")
```

```text
Bahrain is not in the dictionary
```

### 5.2 len() counts pairs

```python
caps = {"Kuwait": "Kuwait City", "Qatar": "Doha", "Oman": "Muscat"}
print(len(caps))
```

```text
3
```

---

## 6. Adding, Changing, and Removing

Dictionaries are **mutable**.

### 6.1 Adding and changing with d[key] = value

The same statement does two different jobs:

- If the key does **not** exist, a new pair is **added**.
- If the key **already** exists, its value is **replaced**.

```python
menu = {"tea": 0.25, "coffee": 1.0}
menu["juice"] = 0.75
menu["tea"] = 0.3
print(menu)
print(len(menu))
```

```text
{'tea': 0.3, 'coffee': 1.0, 'juice': 0.75}
3
```

You can use the old value to compute the new one:

```python
scores = {"Ali": 80}
scores["Ali"] = scores["Ali"] + 5
print(scores)
```

```text
{'Ali': 85}
```

Compare with a list: `lst[10] = x` on a short list is an `IndexError`, because a list cannot grow by assigning to a new position. A dictionary can always grow by assigning to a new key.

### 6.2 Removing with del

```python
cart = {"rice": 2, "tea": 1, "milk": 3}
del cart["tea"]
print(cart)
```

```text
{'rice': 2, 'milk': 3}
```

`del` with a missing key causes a `KeyError`.

### 6.3 Removing with pop()

`pop(key)` removes the pair **and gives back** its value:

```python
cart = {"rice": 2, "milk": 3}
qty = cart.pop("milk")
print(qty)
print(cart)
print(cart.pop("bread", 0))
```

```text
3
{'rice': 2}
0
```

- `pop(key)` with a missing key causes a `KeyError`.
- `pop(key, default)` returns `default` instead, and nothing is removed.

### 6.4 Removing everything with clear()

```python
cart = {"rice": 2, "milk": 3}
cart.clear()
print(cart)
```

```text
{}
```

### 6.5 Summary

| Code | Effect | Key missing |
|---|---|---|
| `d[k] = v` | add a pair, or replace the value | adds it |
| `del d[k]` | remove the pair | `KeyError` |
| `d.pop(k)` | remove the pair and return the value | `KeyError` |
| `d.pop(k, x)` | same | returns `x` |
| `d.clear()` | remove all pairs | — |

---

## 7. Rules for Keys and Values

### 7.1 Keys are unique

A dictionary cannot contain the same key twice. If you write a key twice, the **last** value wins:

```python
d = {"x": 1, "y": 2, "x": 3}
print(d)
print(len(d))
```

```text
{'x': 3, 'y': 2}
2
```

### 7.2 Values may repeat

```python
grades = {"Ali": "A", "Sara": "A", "Mona": "B"}
print(len(grades))
```

```text
3
```

Many keys can share the same value. Only the keys must be unique.

### 7.3 Keys must be immutable

Keys follow the same rule as set items: they must be **immutable**. Strings, numbers, Booleans, and **tuples** are allowed; lists, sets, and dictionaries are not.

```python
places = {(29, 47): "Kuwait City", (25, 51): "Doha"}
print(places[(29, 47)])
```

```text
Kuwait City
```

```text
places = {[29, 47]: "Kuwait City"}

TypeError: unhashable type: 'list'
```

Why? If a key could change after being stored, Python would no longer be able to find its value.

### 7.4 Values can be anything

There is **no** restriction on values. A value can be a number, a string, a list, a tuple, a set, or even another dictionary (Section 10).

### 7.5 Keys are case-sensitive and type-sensitive

```python
d = {"Name": "Sara", 1: "one"}
print("name" in d)
print("1" in d)
print(1 in d)
```

```text
False
False
True
```

---

## 8. Looking Inside: keys(), values(), items()

### 8.1 The three views

```python
prices = {"tea": 0.25, "coffee": 1.0, "juice": 0.75}
print(list(prices.keys()))
print(list(prices.values()))
print(list(prices.items()))
```

```text
['tea', 'coffee', 'juice']
[0.25, 1.0, 0.75]
[('tea', 0.25), ('coffee', 1.0), ('juice', 0.75)]
```

- `keys()` gives all the keys.
- `values()` gives all the values.
- `items()` gives all the pairs, each as a **tuple** `(key, value)`.

These methods return special "view" objects. They are not lists, so you **cannot** use an index on them directly. Wrap them in `list()` when you want to print them neatly or use an index:

```python
prices = {"tea": 0.25, "coffee": 1.0, "juice": 0.75}
first_key = list(prices.keys())[0]
print(first_key)
pair = list(prices.items())[1]
item, price = pair
print(item, price)
```

```text
tea
coffee 1.0
```

The last two lines unpack a `(key, value)` tuple — the same unpacking you learned with tuples.

### 8.2 Functions on values

```python
prices = {"tea": 0.25, "coffee": 1.0, "juice": 0.75}
print(sum(prices.values()))
print(max(prices.values()))
print(min(prices.values()))
print(0.75 in prices.values())
```

```text
2.0
1.0
0.25
True
```

### 8.3 sorted() gives sorted keys

```python
prices = {"tea": 0.25, "coffee": 1.0, "juice": 0.75}
print(sorted(prices))
print(sorted(prices.values()))
```

```text
['coffee', 'juice', 'tea']
[0.25, 0.75, 1.0]
```

`sorted(d)` works on the **keys**. Also, `min(d)` and `max(d)` work on the keys, not the values — a common surprise:

```python
prices = {"tea": 0.25, "coffee": 1.0, "juice": 0.75}
print(max(prices))
print(max(prices.values()))
```

```text
tea
1.0
```

`max(prices)` gives `"tea"` because `"tea"` is the alphabetically largest **key**.

---

## 9. Merging with update()

`a.update(b)` copies every pair from `b` into `a`:

```python
menu = {"tea": 0.25, "coffee": 1.0}
changes = {"coffee": 1.25, "karak": 0.15}
menu.update(changes)
print(menu)
print(changes)
```

```text
{'tea': 0.25, 'coffee': 1.25, 'karak': 0.15}
{'coffee': 1.25, 'karak': 0.15}
```

- Keys only in `changes` are **added** (`"karak"`).
- Keys in both are **replaced** by the value from `changes` (`"coffee"`).
- `menu` changes; `changes` does not.

---

## 10. Values That Are Lists or Dictionaries

### 10.1 A detailed record

Values can be collections themselves. This lets one dictionary describe something with many parts:

```python
student = {
    "name": "Ali",
    "courses": ["CS126", "MATH101"],
    "grades": {"CS126": 88, "MATH101": 75},
}
print(student["courses"])
print(student["courses"][0])
print(student["grades"]["MATH101"])
```

```text
['CS126', 'MATH101']
CS126
75
```

Read the brackets from **left to right**:

1. `student["courses"]` → the list `['CS126', 'MATH101']`
2. `[0]` → the first item of that list → `'CS126'`

and:

1. `student["grades"]` → the dictionary `{'CS126': 88, 'MATH101': 75}`
2. `["MATH101"]` → the value for that key → `75`

### 10.2 Changing the inner collections

```python
student = {
    "name": "Ali",
    "courses": ["CS126", "MATH101"],
    "grades": {"CS126": 88, "MATH101": 75},
}
student["courses"].append("ENG110")
student["grades"]["ENG110"] = 90
print(len(student["courses"]))
print(student["grades"])
```

```text
3
{'CS126': 88, 'MATH101': 75, 'ENG110': 90}
```

### 10.3 One key, several values

Because keys are unique, you cannot give one key two separate values. Use a **list** as the value instead:

```python
phones = {"Ali": ["55512345", "66600000"]}
print(phones["Ali"][1])
print(len(phones["Ali"]))
```

```text
66600000
2
```

---

## 11. Two Useful Patterns

### 11.1 Lookup tables

A dictionary can replace a long chain of `if / elif`:

```python
code = "QA"
if code == "KW":
    country = "Kuwait"
elif code == "QA":
    country = "Qatar"
elif code == "OM":
    country = "Oman"
else:
    country = "Unknown"
print(country)
```

```text
Qatar
```

```python
names = {"KW": "Kuwait", "QA": "Qatar", "OM": "Oman"}
code = "QA"
print(names.get(code, "Unknown"))
print(names.get("XX", "Unknown"))
```

```text
Qatar
Unknown
```

The dictionary version is shorter, and adding a new country means adding **one pair** instead of another `elif` block. The default value of `get()` plays the role of the `else`.

### 11.2 Counting with get()

To count how many times something happens, use this line:

```text
counts[thing] = counts.get(thing, 0) + 1
```

```python
votes = {}
vote = "yes"
votes[vote] = votes.get(vote, 0) + 1
vote = "no"
votes[vote] = votes.get(vote, 0) + 1
vote = "yes"
votes[vote] = votes.get(vote, 0) + 1
print(votes)
```

```text
{'yes': 2, 'no': 1}
```

| Line | `votes.get(vote, 0)` | `votes` after |
|---|---|---|
| first `"yes"` | 0 (not there yet) | `{'yes': 1}` |
| `"no"` | 0 | `{'yes': 1, 'no': 1}` |
| second `"yes"` | 1 | `{'yes': 2, 'no': 1}` |

Here we wrote the line three times. Once you learn loops, this single line will count thousands of items.

---

## 12. Dictionaries vs Lists, Tuples, and Sets

### 12.1 Comparison table

| | List | Tuple | Set | Dictionary |
|---|---|---|---|---|
| Written as | `[1, 2]` | `(1, 2)` | `{1, 2}` | `{"a": 1}` |
| Empty | `[]` | `()` | `set()` | `{}` |
| Stores | items | items | unique items | key → value pairs |
| Find an item by | position | position | only `in` | **key** |
| Ordered? | Yes | Yes | No | Keeps insertion order |
| Duplicates? | Yes | Yes | No | Keys: no · Values: yes |
| Can change? | Yes | No | Yes | Yes |
| `in` checks | items | items | items | **keys** |
| `len()` counts | items | items | items | pairs |
| Missing access | `IndexError` | `IndexError` | — | `KeyError` |
| Must be immutable | — | — | items | **keys** |

### 12.2 How to choose

Ask: *"How will I find the data I need?"*

- **By position** ("the third temperature", "the first person in line") → **list** (or **tuple** if it must not change).
- **Only "is it there?"**, with no repeats ("has this student attended?") → **set**.
- **By a name or an ID** ("the price of tea", "the student with ID 2026014") → **dictionary**.

| Situation | Best choice |
|---|---|
| Customers waiting in line at a bank | List |
| A date of birth `(15, 3, 2006)` | Tuple |
| IDs of students present today | Set |
| Each GCC country and its capital | Dictionary |
| Price of each item in a supermarket | Dictionary |
| This week's temperatures, in order | List |

### 12.3 Tuple record or dictionary record?

Both can store one record:

```python
student_t = ("Sara", 20, "CS")
student_d = {"name": "Sara", "age": 20, "major": "CS"}
print(student_t[2])
print(student_d["major"])
```

```text
CS
CS
```

`student_d["major"]` explains itself; `student_t[2]` requires you to remember that position 2 is the major. Use a **tuple** for small, fixed records where the positions are obvious (a date, a location). Use a **dictionary** when the record has several named fields, or when fields may be added or changed.

---

## 13. Worked Examples

### 13.1 A restaurant order

```python
menu = {"machboos": 3.5, "tea": 0.25, "juice": 0.75}
order = {"machboos": 2, "tea": 3}
total = menu["machboos"] * order["machboos"]
total = total + menu["tea"] * order["tea"]
print("Items ordered:", list(order.keys()))
print("Total:", total, "KD")
item = "kunafa"
if item not in menu:
    print(item, "is not on the menu")
```

```text
Items ordered: ['machboos', 'tea']
Total: 7.75 KD
kunafa is not on the menu
```

The **item name** connects the two dictionaries: `menu` gives the price and `order` gives the quantity.

### 13.2 Updating a student record

```python
student = {"id": 2026014, "name": "Noor", "credits": 45}
student["major"] = "CS"
student["credits"] = student["credits"] + 15
old = student.pop("id")
print(student)
print("Removed ID:", old)
if student["credits"] >= 60:
    print(student["name"], "is a sophomore")
```

```text
{'name': 'Noor', 'credits': 60, 'major': 'CS'}
Removed ID: 2026014
Noor is a sophomore
```

### 13.3 Currency converter

```python
to_kwd = {"USD": 0.3, "SAR": 0.08, "EUR": 0.35}
amount = 200
currency = "SAR"
if currency in to_kwd:
    result = amount * to_kwd[currency]
    print(amount, currency, "=", result, "KWD")
else:
    print("Unknown currency:", currency)
```

```text
200 SAR = 16.0 KWD
```

(The rates are simple examples, not real exchange rates.)

### 13.4 Electricity bill by customer type

```python
rate_fils = {"home": 5, "business": 10}
kind = "home"
kwh = 1500
rate = rate_fils.get(kind)
if rate is None:
    print("Unknown customer type")
else:
    bill = kwh * rate / 1000
    print("Bill:", bill, "KD")
```

```text
Bill: 7.5 KD
```

Here `get()` returns `None` for an unknown type. `rate is None` is the standard way to check for `None` (it means "is exactly the value None"). 1500 kWh × 5 fils = 7500 fils = 7.5 KD.

---

## 14. Important Notes

- Pairs are written `key: value` inside `{ }`. `{}` is an empty **dictionary**, not a set.
- Read with `d[key]` (KeyError if missing) or `d.get(key, default)`.
- `d[key] = value` adds a new pair **or** replaces an existing value.
- `in`, `len()`, `sorted()`, `min()`, and `max()` work on **keys**. Use `d.values()` for values.
- Keys are **unique** (the last one wins) and **immutable** (strings, numbers, tuples). Values can be anything.
- Keys are case-sensitive and type-sensitive: `"Name"` ≠ `"name"`, `1` ≠ `"1"`.
- `keys()`, `values()`, and `items()` are not lists; use `list()` before indexing.
- `e = d` does not copy a dictionary; both names refer to the same dictionary (as with lists).

---

## 15. Common Mistakes

### Mistake 1: Reading a missing key with [ ]

**Incorrect**

```text
prices = {"tea": 0.25, "coffee": 1.0}
print(prices["juice"])

KeyError: 'juice'
```

**Correct**

```python
prices = {"tea": 0.25, "coffee": 1.0}
print(prices.get("juice", "not on the menu"))
```

```text
not on the menu
```

### Mistake 2: Using a position instead of a key

**Incorrect**

```text
student = {"name": "Sara", "age": 20}
print(student[0])

KeyError: 0
```

**Correct**

```python
student = {"name": "Sara", "age": 20}
print(student["name"])
```

```text
Sara
```

### Mistake 3: Using in to search the values

**Incorrect** (goal: is Doha one of the capitals?)

```python
caps = {"Kuwait": "Kuwait City", "Qatar": "Doha"}
print("Doha" in caps)
```

```text
False
```

**Correct**

```python
caps = {"Kuwait": "Kuwait City", "Qatar": "Doha"}
print("Doha" in caps.values())
```

```text
True
```

### Mistake 4: Expecting duplicate keys

**Incorrect** (goal: two numbers for Ali)

```python
phones = {"Ali": "555", "Ali": "666"}
print(phones)
```

```text
{'Ali': '666'}
```

**Correct**

```python
phones = {"Ali": ["555", "666"]}
print(phones["Ali"])
```

```text
['555', '666']
```

### Mistake 5: Using a list as a key

**Incorrect**

```text
places = {[29, 47]: "Kuwait City"}

TypeError: unhashable type: 'list'
```

**Correct** — use a tuple:

```python
places = {(29, 47): "Kuwait City"}
print(places[(29, 47)])
```

```text
Kuwait City
```

### Mistake 6: Indexing keys() directly

**Incorrect**

```text
prices = {"tea": 0.25, "coffee": 1.0}
print(prices.keys()[0])

TypeError: 'dict_keys' object is not subscriptable
```

**Correct**

```python
prices = {"tea": 0.25, "coffee": 1.0}
print(list(prices.keys())[0])
```

```text
tea
```

### Mistake 7: Wrong case in a key

**Incorrect**

```python
user = {"Name": "Sara"}
print(user.get("name"))
```

```text
None
```

**Why?** `"Name"` and `"name"` are different keys. `get()` hides the problem by returning `None` instead of raising an error. Choose one style for keys (for example, all small letters) and use it everywhere.

### Mistake 8: Using max() on a dictionary to find the largest value

**Incorrect** (goal: the highest price)

```python
prices = {"tea": 0.25, "coffee": 1.0}
print(max(prices))
```

```text
tea
```

**Correct**

```python
prices = {"tea": 0.25, "coffee": 1.0}
print(max(prices.values()))
```

```text
1.0
```

---

## 16. Mini Practice Questions

Try these before looking at the answers at the end of this section.

**Q1.** What does this print?

```python
d = {"a": 5, "b": 7}
print(d["b"], len(d), "a" in d, 5 in d)
```

**Q2.** What does this print?

```python
d = {"a": 1}
d["b"] = 2
d["a"] = 3
print(d)
```

**Q3.** What is the difference between `d.pop("x")` and `d.pop("x", 0)` when `"x"` is not a key?

**Q4.** Which of these can be dictionary keys: `"CS126"`, `126`, `(1, 2)`, `[1, 2]`, `{1, 2}`?

**Q5.** What does this print?

```python
d = {"a": 1, "b": 2}
d["c"] = d.get("a", 0) + d.get("z", 10)
print(d["c"], len(d), "z" in d)
```

**Q6.** What does this print?

```python
s = {"name": "Ali", "marks": [70, 85]}
print(s["marks"][-1], len(s))
```

### Answers to Mini Practice

1. **`7 2 True False`** — `5 in d` checks the keys, and 5 is a value.
2. **`{'a': 3, 'b': 2}`**
3. `d.pop("x")` raises a **KeyError**; `d.pop("x", 0)` returns **0** and nothing changes.
4. **`"CS126"`, `126`, and `(1, 2)`**. Lists and sets are mutable, so they cannot be keys.
5. **`11 3 False`** — `get()` only reads; it never adds `"z"`.
6. **`85 2`** — the dictionary has 2 pairs; the list inside has 2 marks.

---

## 17. Ask AI to Help You Understand

```text
Explain Python dictionaries to a beginner who knows lists, tuples, and sets.
Use a restaurant menu in Kuwait (items and prices in KD) as the main example.
Do not use loops, and do not give me exercises yet.
```

```text
What is the difference between d[key] and d.get(key, default) in Python?
Give me one situation where each one is the better choice.
```

```text
Why must dictionary keys be immutable, while values can be anything?
Explain with a small example using a tuple key and a list value.
```

```text
Explain the counting pattern counts[x] = counts.get(x, 0) + 1 step by step,
using three votes: "yes", "no", "yes". Show the dictionary after each step.
```

```text
Give me five situations and ask me whether each should use a list, a tuple,
a set, or a dictionary. Wait for my answer each time before telling me if I am right.
```

> **Remember:** Always run the code yourself. AI can make mistakes, and running code is the only way to be sure.

---

## 18. Summary

- A **dictionary** stores **key: value** pairs in curly brackets. `{}` is the empty dictionary.
- Read a value with `d[key]` (KeyError if missing) or `d.get(key, default)` (never fails).
- `d[key] = value` adds a new pair or replaces an existing value.
- Remove pairs with `del d[key]`, `d.pop(key)` (returns the value), or `d.clear()`.
- `in`, `len()`, and `sorted()` work on **keys**. `keys()`, `values()`, and `items()` let you see the keys, the values, and the pairs.
- `update()` merges another dictionary in; its values win for shared keys.
- Keys are **unique** and **immutable**; values can be anything, including lists and dictionaries.
- Dictionaries are ideal as **lookup tables** and **counters**.
- **List/tuple:** find by position. **Set:** unique items, membership. **Dictionary:** find by key.

---

## Basic Exercises

> Exercises 1–12 are the same as in the slides. Exercises 13–16 are extra practice.

**Exercise 1.** Predict the output.

```python
caps = {"Kuwait": "Kuwait City",
        "Qatar": "Doha", "Oman": "Muscat"}
print(caps["Qatar"])
print(len(caps))
print("Doha" in caps)
```

**Exercise 2.** Predict the output.

```python
d = {"a": 1, "b": 2}
d["c"] = 3
d["a"] = 10
print(d)
```

**Exercise 3.** Find the error and fix it so the program prints 0 for a missing item.

```text
prices = {"tea": 0.25, "coffee": 1}
print(prices["juice"])
```

**Exercise 4.** Predict the output.

```python
d = {"x": 1, "y": 2, "x": 3}
print(d, len(d))
```

**Exercise 13.** Predict the output.

```python
d = {"Kuwait": 965, "Qatar": 974}
print(list(d.keys()))
print(list(d.values()))
print(list(d.items())[0])
```

## Practice Exercises

**Exercise 5.** Start with `book = {"Ali": "55512345", "Sara": "66698765"}`. Add Mona (`"99911122"`), change Ali's number to `"55500000"`, delete Sara, then print the dictionary.

**Exercise 6.** Using the menu and order below, print the total price.

```python
menu = {"machboos": 3.5, "tea": 0.25,
        "juice": 0.75}
order = {"machboos": 2, "juice": 3}
```

**Exercise 7.** For `student = {"name": "Noor", "credits": 45}`: add `"major": "CS"`, add 15 credits, then print the dictionary.

**Exercise 8.** Explain each value and give the output.

```python
stock = {"rice": 10}
print(stock.get("rice", 0))
print(stock.get("milk", 0))
print(stock.get("milk"))
```

**Exercise 14.** A small English-to-Arabic word list is stored as `words = {"hello": "marhaba", "thanks": "shukran", "yes": "naam"}`. Print the translation of `"thanks"`, then print the translation of `"goodbye"` or `unknown word` if it is not in the dictionary.

## Challenge Exercises

**Exercise 9.** Start with `votes = {}`. Using the `get()` counting pattern, record three votes: `"yes"`, `"no"`, `"yes"`. Print `votes`.

**Exercise 10.** For the record below, print Ali's MATH101 grade. Then add `"ENG110"` to his courses with grade 90. Print the number of courses and the grades.

```python
ali = {"courses": ["CS126", "MATH101"],
       "grades": {"CS126": 88, "MATH101": 75}}
```

**Exercise 11.** Predict the output. Be careful!

```python
d = {"a": 1}
e = d
e["b"] = 2
d.pop("a")
print(d, e, "a" in e)
```

**Exercise 12.** List, tuple, set, or dictionary? Give a reason:

1. Each GCC country and its capital
2. The IDs of students present today
3. This week's temperatures, in order
4. A date of birth

**Exercise 15.** A shop's prices are stored in `old = {"rice": 2.5, "tea": 1.25, "milk": 0.5}`. New prices arrive: `new = {"tea": 1.5, "dates": 3.0}`. Merge them so `old` has the latest prices. Print the sorted list of items, the new price of tea, and the number of items.

**Exercise 16.** Electricity prices (fils per kWh) depend on the customer type: `rate_fils = {"home": 5, "business": 10}`. For a business customer who used 2400 kWh, print the bill in KD (1 KD = 1000 fils). If the type were `"factory"`, the program should print `Unknown customer type` instead.

---

# Exercise Solutions

### Solution 1

`caps["Qatar"]` is the value for key `"Qatar"`. There are 3 pairs. `in` checks keys, and `"Doha"` is a value.

```text
Doha
3
False
```

### Solution 2

`"c"` is a new key, so it is added. `"a"` already exists, so its value is replaced.

```text
{'a': 10, 'b': 2, 'c': 3}
```

### Solution 3

`"juice"` is not a key, so `prices["juice"]` causes `KeyError: 'juice'`. Use `get()` with a default value:

```python
prices = {"tea": 0.25, "coffee": 1}
print(prices.get("juice", 0))
```

```text
0
```

### Solution 4

Keys are unique. The second `"x"` replaces the first, so there are only 2 pairs.

```text
{'x': 3, 'y': 2} 2
```

### Solution 5

```python
book = {"Ali": "55512345", "Sara": "66698765"}
book["Mona"] = "99911122"
book["Ali"] = "55500000"
del book["Sara"]
print(book)
```

```text
{'Ali': '55500000', 'Mona': '99911122'}
```

Phone numbers are stored as strings because we never do arithmetic with them, and a number cannot keep a leading 0.

### Solution 6

```python
menu = {"machboos": 3.5, "tea": 0.25,
        "juice": 0.75}
order = {"machboos": 2, "juice": 3}
total = menu["machboos"] * order["machboos"]
total = total + menu["juice"] * order["juice"]
print(total)
```

```text
9.25
```

3.5 × 2 = 7.0 and 0.75 × 3 = 2.25, so the total is 9.25.

### Solution 7

```python
student = {"name": "Noor", "credits": 45}
student["major"] = "CS"
student["credits"] = student["credits"] + 15
print(student)
```

```text
{'name': 'Noor', 'credits': 60, 'major': 'CS'}
```

### Solution 8

- `"rice"` is a key → its value `10`.
- `"milk"` is not a key → the default `0`.
- `"milk"` is not a key and there is no default → `None`.

```text
10
0
None
```

### Solution 9

```python
votes = {}
votes["yes"] = votes.get("yes", 0) + 1
votes["no"] = votes.get("no", 0) + 1
votes["yes"] = votes.get("yes", 0) + 1
print(votes)
```

```text
{'yes': 2, 'no': 1}
```

The first time each key appears, `get()` returns 0, so the count becomes 1. The second `"yes"` reads 1 and stores 2.

### Solution 10

```python
ali = {"courses": ["CS126", "MATH101"],
       "grades": {"CS126": 88, "MATH101": 75}}
print(ali["grades"]["MATH101"])
ali["courses"].append("ENG110")
ali["grades"]["ENG110"] = 90
print(len(ali["courses"]))
print(ali["grades"])
```

```text
75
3
{'CS126': 88, 'MATH101': 75, 'ENG110': 90}
```

### Solution 11

`e = d` does not make a copy: `d` and `e` are two names for the **same** dictionary, just like with lists. So adding `"b"` through `e` and removing `"a"` through `d` both change the one dictionary.

```text
{'b': 2} {'b': 2} False
```

### Solution 12

| | Choice | Reason |
|---|---|---|
| 1. Country and capital | **Dictionary** | Look up a capital by the country name. |
| 2. IDs present today | **Set** | Each ID once; fast "is this student present?" checks. |
| 3. Temperatures in order | **List** | Order matters and values may repeat. |
| 4. Date of birth | **Tuple** | A small fixed record: (day, month, year). |

### Solution 13

```text
['Kuwait', 'Qatar']
[965, 974]
('Kuwait', 965)
```

`items()` gives each pair as a tuple, and `[0]` takes the first pair of the list.

### Solution 14

```python
words = {"hello": "marhaba", "thanks": "shukran", "yes": "naam"}
print(words["thanks"])
print(words.get("goodbye", "unknown word"))
```

```text
shukran
unknown word
```

### Solution 15

```python
old = {"rice": 2.5, "tea": 1.25, "milk": 0.5}
new = {"tea": 1.5, "dates": 3.0}
old.update(new)
print(sorted(old))
print(old["tea"])
print(len(old))
```

```text
['dates', 'milk', 'rice', 'tea']
1.5
4
```

`"tea"` is in both dictionaries, so its price is replaced by the new one. `"dates"` is only in `new`, so it is added.

### Solution 16

```python
rate_fils = {"home": 5, "business": 10}
kind = "business"
kwh = 2400
if kind in rate_fils:
    bill = kwh * rate_fils[kind] / 1000
    print("Bill:", bill, "KD")
else:
    print("Unknown customer type")
```

```text
Bill: 24.0 KD
```

2400 kWh × 10 fils = 24000 fils = 24.0 KD. With `kind = "factory"`, the `in` test is `False`, so the program prints `Unknown customer type`.

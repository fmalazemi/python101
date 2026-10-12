# CS126 – Introduction to Python

## Advanced Methods for Lists

**Instructor:** Dr. Fawaz Alazemi

---

## Learning Objectives

After studying these notes, you should be able to:

1. Take parts of a list with **slicing**, using `lst[start:stop]` and `lst[start:stop:step]`, including negative indexes.
2. Use the built-in functions `len()`, `sum()`, `min()`, and `max()`, and know which kinds of data each one accepts.
3. Add items to a list with `append()`, `insert()`, and `extend()`, and join lists with `+` (concatenation).
4. Remove an item with `remove()`, and avoid errors by checking with `in` first.
5. Reorder a list with `sort()` (including `reverse=True`) and `reverse()`.
6. Build one string from a list of strings with `join()`.
7. Explain the difference between tools that **change** a list and tools that **give back a new value**.
8. Know which tools also work on **strings** and **tuples**, and which work on **lists only**.

---

## 1. Introduction

### 1.1 Where we are

You already know how to:

- create a list: `grades = [85, 92, 78]`
- read one item with an index: `grades[0]`
- change one item: `grades[1] = 95`
- check membership: `92 in grades`

That is enough for small tasks. But real programs need to do much more with lists. For example, a program that manages student grades may need to:

- show only the **top three** grades,
- calculate the **average**, the **highest**, and the **lowest**,
- **add** a new student's grade, or **remove** a wrong one,
- **sort** the grades,
- print all names as one neat line: `Ali, Mona, Sara`.

Python gives us ready-made tools for all of these. This lecture teaches the most important ones.

### 1.2 Two kinds of tools: functions and methods

The tools in this lecture come in two forms. It is important to recognize them, because they behave differently.

**Functions** are written as `name(list)`. The list goes **inside** the brackets:

```python
grades = [85, 92, 78]
print(len(grades))
print(max(grades))
print(grades)
```

```text
3
92
[85, 92, 78]
```

A function **looks at** the list and **gives back** an answer. The list itself does **not** change. You have already used functions like `print()`, `len()`, and `type()`.

**Methods** are written as `list.name(...)`. You write the list, a **dot**, then the method name:

```python
grades = [85, 92, 78]
grades.append(60)
print(grades)
```

```text
[85, 92, 78, 60]
```

A **method** is a function that belongs to a particular type of data. List methods **belong to lists**, so you call them on a list with a dot. Most list methods **change** the list they are called on.

You have seen methods before with strings, for example `"kuwait".upper()`.

### 1.3 Plan for this lecture

| Part | Tools | Do they change the list? |
|---|---|---|
| Slicing | `lst[start:stop:step]` | No — gives a new list |
| Functions | `len()`, `sum()`, `min()`, `max()` | No — give back a value |
| Adding | `append()`, `insert()`, `extend()`, `+` | Methods: yes. `+`: no |
| Removing | `remove()` | Yes |
| Ordering | `sort()`, `reverse()` | Yes |
| Making strings | `join()` | No — gives a string |

---

## 2. Main Concepts and Vocabulary

| Term | Meaning | Example |
|---|---|---|
| **Index** | The position of one item | `nums[2]` |
| **Negative index** | Position counted from the end; `-1` is the last item | `nums[-1]` |
| **Slice** | A new list made from part of a list | `nums[1:4]` |
| **Function** | A named tool used as `name(value)` | `len(nums)` |
| **Method** | A function that belongs to a type, used with a dot | `nums.sort()` |
| **Argument** | A value given inside the brackets of a function or method | `"dates"` in `cart.append("dates")` |
| **Return value** | The value a function or method gives back | `len([1, 2])` returns `2` |
| **`None`** | A special Python value meaning "no value" | what `sort()` returns |
| **Mutable** | Can be changed after it is created | lists |
| **Immutable** | Cannot be changed after it is created | strings, tuples |
| **Concatenation** | Joining two sequences with `+` | `[1] + [2]` |
| **Nested list** | A list stored inside another list | `[1, [2, 3]]` |

---

## 3. Review: Positive and Negative Indexes

Every item in a list has **two** indexes: a positive one (counting from the start, beginning at 0) and a negative one (counting from the end, beginning at −1).

```python
nums = [10, 20, 30, 40, 50, 60]
```

| Item | 10 | 20 | 30 | 40 | 50 | 60 |
|---|---|---|---|---|---|---|
| Positive index | 0 | 1 | 2 | 3 | 4 | 5 |
| Negative index | −6 | −5 | −4 | −3 | −2 | −1 |

```python
nums = [10, 20, 30, 40, 50, 60]
print(nums[0], nums[3])
print(nums[-1], nums[-2])
```

```text
10 40
60 50
```

Negative indexes are very useful when you want items near the **end** of a list but do not want to calculate the length. `nums[-1]` is always the last item, whatever the length of the list.

An **index** gives you **one item**. A **slice** gives you a **new list** containing several items.

---

## 4. Slicing

### 4.1 Basic slice: `lst[start:stop]`

A slice takes the items from index `start` up to, **but not including**, index `stop`.

```python
nums = [10, 20, 30, 40, 50, 60]
print(nums[1:4])
print(nums[0:2])
print(nums[2:3])
```

```text
[20, 30, 40]
[10, 20]
[30]
```

Walkthrough for `nums[1:4]`:

1. Start at index 1 → `20` is included.
2. Index 2 → `30` is included.
3. Index 3 → `40` is included.
4. Index 4 is the **stop** → stop here; `50` is **not** included.

**Counting rule:** the number of items in `lst[start:stop]` is `stop − start` (when both are inside the list). For `nums[1:4]`, that is 4 − 1 = 3 items.

Notice that `nums[2:3]` gives a **list** with one item, `[30]`, while `nums[2]` gives the item itself, `30`.

**Why is stop not included?** It makes many things simple. For example, `nums[0:3]` and `nums[3:6]` fit together perfectly with no overlap and no gap: the first three items and the next three items.

### 4.2 Leaving out start or stop

You can leave out `start`, `stop`, or both:

- No `start` → begin at the **first** item.
- No `stop` → go to the **end** of the list.

```python
temps = [44, 46, 48, 45, 47, 49, 43]   # Sunday to Saturday
print(temps[:3])
print(temps[4:])
print(temps[:])
```

```text
[44, 46, 48]
[47, 49, 43]
[44, 46, 48, 45, 47, 49, 43]
```

| Slice | Meaning |
|---|---|
| `lst[:n]` | the first `n` items |
| `lst[n:]` | everything from index `n` to the end |
| `lst[:]` | a **copy** of the whole list |

### 4.3 Negative indexes in slices

```python
temps = [44, 46, 48, 45, 47, 49, 43]
print(temps[-2:])
print(temps[:-1])
print(temps[-3:-1])
print(temps[1:-1])
```

```text
[49, 43]
[44, 46, 48, 45, 47, 49]
[47, 49]
[46, 48, 45, 47, 49]
```

| Slice | Meaning |
|---|---|
| `lst[-n:]` | the last `n` items |
| `lst[:-1]` | everything except the last item |
| `lst[1:-1]` | everything except the first and the last item |

### 4.4 Adding a step: `lst[start:stop:step]`

The third number is the **step**: how far to jump each time. The default step is 1.

```python
nums = [10, 20, 30, 40, 50, 60]
print(nums[::2])
print(nums[1::2])
print(nums[0:5:3])
```

```text
[10, 30, 50]
[20, 40, 60]
[10, 40]
```

- `nums[::2]`: start at index 0, take every second item → indexes 0, 2, 4.
- `nums[1::2]`: start at index 1, every second item → indexes 1, 3, 5.
- `nums[0:5:3]`: indexes 0 and 3 (the next would be 6, which is past the stop).

### 4.5 Negative step: walking backwards

A **negative** step walks from right to left. Then `start` should be to the **right** of `stop`.

```python
nums = [10, 20, 30, 40, 50, 60]
print(nums[::-1])
print(nums[4:1:-1])
print(nums[::-2])
```

```text
[60, 50, 40, 30, 20, 10]
[50, 40, 30]
[60, 40, 20]
```

`lst[::-1]` is the standard way to get a **reversed copy** of a list.

### 4.6 Important facts about slicing

**Slicing never changes the original list.** It always creates a new one:

```python
nums = [10, 20, 30, 40]
part = nums[1:3]
part[0] = 999
print(part)
print(nums)
```

```text
[999, 30]
[10, 20, 30, 40]
```

**Slicing never causes an IndexError.** If the numbers go past the end, Python simply stops at the end. If nothing is selected, you get an empty list:

```python
nums = [10, 20, 30, 40]
print(nums[2:100])
print(nums[10:])
print(nums[3:1])
```

```text
[30, 40]
[]
[]
```

Compare this with a single index: `nums[100]` **does** cause an `IndexError`.

**Slicing works on strings and tuples too.** The result has the same type as the original:

```python
city = "Kuwait City"
print(city[:6])
print(city[-4:])
print(city[::-1])
point = (5, 8, 2, 9)
print(point[1:3])
```

```text
Kuwait
City
ytiC tiawuK
(8, 2)
```

### 4.7 Slicing summary

| Goal | Slice |
|---|---|
| First 3 items | `lst[:3]` |
| Last 3 items | `lst[-3:]` |
| All except the first | `lst[1:]` |
| All except the last | `lst[:-1]` |
| Items at index 2, 3, 4 | `lst[2:5]` |
| Every second item | `lst[::2]` |
| Reversed copy | `lst[::-1]` |
| Full copy | `lst[:]` |

---

## 5. Functions That Look at a List

These four functions **do not change** the list. They look at it and give back a value.

### 5.1 `len()` — how many items

```python
prices = [1.25, 0.75, 2.5, 0.5]
print(len(prices))
print(len([]))
print(len("Kuwait"))
print(len((3, 4)))
```

```text
4
0
6
2
```

`len()` works on lists, strings (number of characters), and tuples. An empty list has length 0.

A nested list counts as **one** item:

```python
print(len([1, 2, [3, 4, 5]]))
```

```text
3
```

`len()` is often used to find the **last index**: the last index of a list is always `len(lst) - 1`.

```python
grades = [85, 92, 78, 95]
print(grades[len(grades) - 1])
print(grades[-1])
```

```text
95
95
```

### 5.2 `sum()` — total of numbers

```python
prices = [1.25, 0.75, 2.5, 0.5]
print(sum(prices))
print(sum([10, 20, 30]))
print(sum([]))
```

```text
5.0
60
0
```

Rules for `sum()`:

- All items must be **numbers** (integers or floats). It works on lists and tuples of numbers.
- `sum([])` is `0`.
- It does **not** work on strings: `sum(["a", "b"])` causes a `TypeError`. To combine strings, use `join()` (Section 10).

### 5.3 `min()` and `max()` — smallest and largest

With numbers:

```python
temps = [44, 46, 48, 45, 47, 49, 43]
print(max(temps))
print(min(temps))
```

```text
49
43
```

With strings, Python compares in **alphabetical order** (more precisely, in the order of character codes):

```python
cities = ["Muscat", "Doha", "Kuwait"]
print(min(cities))
print(max(cities))
```

```text
Doha
Muscat
```

Be careful with uppercase and lowercase. In Python, **all uppercase letters come before all lowercase letters**. So:

```python
print(min(["oman", "Qatar"]))
print(max(["apple", "Zebra"]))
```

```text
Qatar
apple
```

`"Qatar"` starts with an uppercase `Q`, which comes before the lowercase `o`. To avoid surprises, keep your strings in the same case.

Rules for `min()` and `max()`:

- Items must be **comparable**: all numbers, or all strings. A mix such as `[3, "a"]` causes a `TypeError`.
- An **empty** list causes a `ValueError`, because there is no smallest or largest item.
- They also work on tuples and strings (for a string, they give the smallest or largest **character**).

### 5.4 Combining functions

These functions are often combined in one expression:

```python
grades = [85, 92, 78, 95, 70]
average = sum(grades) / len(grades)
spread = max(grades) - min(grades)
print("Average:", average)
print("Spread:", spread)
```

```text
Average: 84.0
Spread: 25
```

Step by step:

1. `sum(grades)` is 85 + 92 + 78 + 95 + 70 = 420.
2. `len(grades)` is 5.
3. `420 / 5` is `84.0` (division with `/` always gives a float).
4. `max(grades)` is 95 and `min(grades)` is 70, so the spread is 25.

You can also apply them to a **slice**:

```python
temps = [44, 46, 48, 45, 47, 49, 43]
weekdays = temps[:5]
print("Weekday average:", sum(weekdays) / len(weekdays))
print("Hottest weekend day:", max(temps[-2:]))
```

```text
Weekday average: 46.0
Hottest weekend day: 49
```

---

## 6. Adding Items

### 6.1 `append(item)` — add one item at the end

```python
cart = ["milk", "bread"]
cart.append("dates")
print(cart)
print(len(cart))
```

```text
['milk', 'bread', 'dates']
3
```

| Before | After `cart.append("dates")` |
|---|---|
| `['milk', 'bread']` | `['milk', 'bread', 'dates']` |

Key facts:

- `append()` adds **exactly one** item, always at the **end**.
- It **changes** the list. You do not need to (and must not) write `cart = ...`.
- It returns `None` (see Section 11).
- It can add any kind of value, including another list (see 6.3).

### 6.2 `insert(index, item)` — add at a position

```python
queue = ["Ali", "Sara", "Fahad"]
queue.insert(1, "Mona")
print(queue)
queue.insert(0, "Noor")
print(queue)
```

```text
['Ali', 'Mona', 'Sara', 'Fahad']
['Noor', 'Ali', 'Mona', 'Sara', 'Fahad']
```

How it works:

1. The new item is placed **at** the given index.
2. The item that was at that index, and every item after it, moves one place to the **right**.

`insert()` takes **two** arguments, in this order: the **index** first, then the **item**.

| Call | Effect |
|---|---|
| `lst.insert(0, x)` | `x` becomes the first item |
| `lst.insert(len(lst), x)` | same as `lst.append(x)` |
| `lst.insert(100, x)` | index past the end → `x` is added at the end (no error) |

```python
x = [1, 2, 3]
x.insert(10, 99)
print(x)
```

```text
[1, 2, 3, 99]
```

### 6.3 `extend(other)` — add every item of another list

```python
a = ["Kuwait", "Qatar"]
a.extend(["Oman", "UAE"])
print(a)
print(len(a))
```

```text
['Kuwait', 'Qatar', 'Oman', 'UAE']
4
```

Compare with `append()` given the same list:

```python
b = ["Kuwait", "Qatar"]
b.append(["Oman", "UAE"])
print(b)
print(len(b))
print(b[2])
```

```text
['Kuwait', 'Qatar', ['Oman', 'UAE']]
3
['Oman', 'UAE']
```

- `extend()` opens the other list and adds **each item separately**.
- `append()` adds the other list as **one single item**, creating a **nested list**.

| Method | Argument | Items added |
|---|---|---|
| `append(x)` | any one value | always 1 |
| `extend(other)` | a list (or tuple, or string) | as many as `other` has |

Be careful with strings: `extend()` treats a string as a sequence of characters.

```python
letters = ["a"]
letters.extend("bc")
print(letters)
```

```text
['a', 'b', 'c']
```

### 6.4 Concatenation with `+`

The `+` operator joins two lists into a **new** list:

```python
first = [1, 2]
second = [3, 4]
both = first + second
print(both)
print(first)
print(second)
```

```text
[1, 2, 3, 4]
[1, 2]
[3, 4]
```

You already know `+` with strings (`"Kuwait" + " City"`). With lists it works the same way.

| | `a + b` | `a.extend(b)` |
|---|---|---|
| Creates | a **new** list | nothing new |
| Changes `a`? | No | Yes |
| Use the result with | `c = a + b` | just `a` afterwards |

Rules for `+`:

- **Both** sides must be lists. `[1, 2] + 3` causes a `TypeError`. Write `[1, 2] + [3]`.
- A list cannot be added to a tuple with `+`, even though both are sequences.

```python
a = [1]
b = a + [2, 3]
print(a, b)
```

```text
[1] [1, 2, 3]
```

---

## 7. Removing Items: `remove(value)`

```python
items = ["pen", "book", "pen", "bag"]
items.remove("pen")
print(items)
```

```text
['book', 'pen', 'bag']
```

Key facts:

- `remove()` searches by **value**, not by index. `items.remove("pen")` means "remove the item that equals `"pen"`".
- It removes only the **first** matching item. The second `"pen"` stays.
- The items after the removed one move one place to the **left**.
- If the value is **not** in the list, Python stops with a `ValueError`.

### 7.1 Removing safely

Use `in` with an `if` statement to check first:

```python
items = ["book", "pen", "bag"]
if "phone" in items:
    items.remove("phone")
else:
    print("phone is not in the list")
print(items)
```

```text
phone is not in the list
['book', 'pen', 'bag']
```

This pattern — **check with `in`, then `remove()`** — prevents your program from crashing when the value might not be there.

### 7.2 Removing all copies of a value

`remove()` only deletes one copy at a time. To delete every copy, you need to repeat it. This needs a **loop**, which we will study in a later lecture. For now, if you know there are exactly two copies, you can call `remove()` twice.

```python
votes = ["yes", "no", "yes"]
votes.remove("yes")
votes.remove("yes")
print(votes)
```

```text
['no']
```

---

## 8. Ordering: `sort()`

```python
temps = [46, 44, 49, 45]
temps.sort()
print(temps)
temps.sort(reverse=True)
print(temps)
```

```text
[44, 45, 46, 49]
[49, 46, 45, 44]
```

- `sort()` arranges the items from **smallest to largest** (ascending order).
- `sort(reverse=True)` arranges them from **largest to smallest** (descending order). Here `reverse=True` is a special kind of argument written with a name and `=`. Write it exactly like this.
- `sort()` **changes** the list. The original order is **lost**.

With strings, `sort()` uses alphabetical order (uppercase before lowercase, as with `min()` and `max()`):

```python
gcc = ["Qatar", "Bahrain", "Kuwait", "Oman"]
gcc.sort()
print(gcc)
```

```text
['Bahrain', 'Kuwait', 'Oman', 'Qatar']
```

Rules for `sort()`:

- All items must be comparable: all numbers or all strings. `[3, "a", 1]` cannot be sorted (`TypeError`).
- `sort()` is a **list** method. Tuples and strings are immutable, so they have **no** `sort()` method.

### 8.1 Keeping the original order

If you need both the original order and a sorted version, sort a **copy** made with `[:]`:

```python
original = [5, 2, 9]
ordered = original[:]
ordered.sort()
print(original)
print(ordered)
```

```text
[5, 2, 9]
[2, 5, 9]
```

---

## 9. Flipping: `reverse()` and `[::-1]`

```python
days = ["Sun", "Mon", "Tue"]
days.reverse()
print(days)
```

```text
['Tue', 'Mon', 'Sun']
```

`reverse()` flips the list **in place**: the last item becomes the first, and so on. It changes the list and returns `None`.

### 9.1 `reverse()` is not "sort backwards"

`reverse()` does **not** look at the values. It only flips the current order:

```python
nums = [3, 1, 2]
nums.reverse()
print(nums)
```

```text
[2, 1, 3]
```

To get largest-to-smallest, use `sort(reverse=True)`.

### 9.2 `reverse()` versus `[::-1]`

| | `lst.reverse()` | `lst[::-1]` |
|---|---|---|
| Kind | method | slice |
| Changes `lst`? | Yes | No |
| Returns | `None` | a new reversed list |
| Works on strings/tuples? | No (lists only) | Yes |

```python
days = ["Sun", "Mon", "Tue"]
back = days[::-1]
print(back)
print(days)
```

```text
['Tue', 'Mon', 'Sun']
['Sun', 'Mon', 'Tue']
```

---

## 10. From a List to a String: `join()`

### 10.1 Syntax

```text
separator.join(list_of_strings)
```

`join()` takes a list of strings and glues them together into **one string**, putting the **separator** between each pair of items.

```python
countries = ["Kuwait", "Oman", "Qatar"]
print(", ".join(countries))
print(" - ".join(countries))
print("\n".join(countries))
```

```text
Kuwait, Oman, Qatar
Kuwait - Oman - Qatar
Kuwait
Oman
Qatar
```

(`"\n"` is the newline character, so each country is printed on its own line.)

### 10.2 Important details

- `join()` is a **string** method, not a list method. The **separator** comes first, before the dot: `", ".join(names)`. Writing `names.join(", ")` causes an `AttributeError`.
- The separator goes **between** items only — not before the first or after the last.
- An **empty** separator `""` glues the items with nothing between them:

```python
letters = ["C", "S", "1", "2", "6"]
print("".join(letters))
```

```text
CS126
```

- The result is a **string**. The list does **not** change.
- **Every item must be a string.** A number in the list causes a `TypeError`. Store numbers as strings when you plan to join them, for example `["12", "10", "2026"]`.
- `join()` also works with a **tuple** of strings: `"-".join(("12", "10"))` gives `"12-10"`.
- Joining a list with one item gives that item; joining an empty list gives an empty string `""`.

```python
print("/".join(["2026"]))
print("[" + "/".join([]) + "]")
```

```text
2026
[]
```

### 10.3 Example: building a sentence

```python
words = ["Python", "is", "fun"]
sentence = " ".join(words) + "!"
print(sentence)
print(len(sentence))
```

```text
Python is fun!
14
```

---

## 11. Methods Return None

The methods `append()`, `insert()`, `extend()`, `remove()`, `sort()`, and `reverse()` all **change the list in place** and return the special value **`None`**, which means "nothing".

```python
nums = [3, 1, 2]
result = nums.sort()
print(result)
print(nums)
```

```text
None
[1, 2, 3]
```

This leads to one of the most common beginner mistakes:

```python
nums = [3, 1, 2]
nums = nums.sort()
print(nums)
```

```text
None
```

The list was sorted, but then the name `nums` was given the value `None`, so the sorted list is lost.

**Rule:** call these methods on a line **by themselves**. Do not assign their result, and do not put them inside `print()`.

| Tool | Changes the list? | Returns |
|---|---|---|
| `lst[a:b:s]` | No | new list |
| `len(lst)` | No | integer |
| `sum(lst)` | No | number |
| `min(lst)`, `max(lst)` | No | an item |
| `a + b` | No | new list |
| `sep.join(lst)` | No | string |
| `lst.append(x)` | **Yes** | `None` |
| `lst.insert(i, x)` | **Yes** | `None` |
| `lst.extend(other)` | **Yes** | `None` |
| `lst.remove(x)` | **Yes** | `None` |
| `lst.sort()` | **Yes** | `None` |
| `lst.reverse()` | **Yes** | `None` |

---

## 12. Which Tools Work on Strings and Tuples?

Lists are **mutable** (changeable). Strings and tuples are **immutable** (they cannot be changed after they are created). So:

| Tool | List | Tuple | String |
|---|---|---|---|
| Slicing | ✔ | ✔ | ✔ |
| `len()` | ✔ | ✔ | ✔ |
| `sum()` | ✔ (numbers) | ✔ (numbers) | ✘ |
| `min()`, `max()` | ✔ | ✔ | ✔ (characters) |
| `+` | ✔ (list + list) | ✔ (tuple + tuple) | ✔ (string + string) |
| `append`, `insert`, `extend`, `remove`, `sort`, `reverse` | ✔ | ✘ | ✘ |
| `join()` (as the items to join) | ✔ (strings only) | ✔ (strings only) | — |

```python
t = (4, 1, 3)
print(len(t), sum(t), min(t), max(t))
print(t[::-1])
print(t + (9,))
```

```text
3 8 1 4
(3, 1, 4)
(4, 1, 3, 9)
```

---

## 13. Worked Examples

### 13.1 Grade report

```python
scores = [72, 95, 58, 88, 61, 79]
scores.sort(reverse=True)
print("Sorted:", scores)
print("Top 3:", scores[:3])
print("Highest:", max(scores), "Lowest:", min(scores))
print("Average:", sum(scores) / len(scores))
```

```text
Sorted: [95, 88, 79, 72, 61, 58]
Top 3: [95, 88, 79]
Highest: 95 Lowest: 58
Average: 75.5
```

1. After `sort(reverse=True)`, the highest score is at index 0.
2. So `scores[:3]` is the **top three** scores.
3. `max()` and `min()` do not need a sorted list, but here they confirm the first and last items.
4. The total is 453, and 453 / 6 = 75.5.

### 13.2 Shopping list

```python
cart = ["milk", "bread"]
cart.append("dates")
cart.insert(0, "water")
cart.extend(["rice", "tea"])
cart.remove("bread")
cart.sort()
print(cart)
print("Items:", len(cart))
print("Buy: " + ", ".join(cart))
```

```text
['dates', 'milk', 'rice', 'tea', 'water']
Items: 5
Buy: dates, milk, rice, tea, water
```

| Step | `cart` after the step |
|---|---|
| start | `['milk', 'bread']` |
| `append("dates")` | `['milk', 'bread', 'dates']` |
| `insert(0, "water")` | `['water', 'milk', 'bread', 'dates']` |
| `extend(["rice", "tea"])` | `['water', 'milk', 'bread', 'dates', 'rice', 'tea']` |
| `remove("bread")` | `['water', 'milk', 'dates', 'rice', 'tea']` |
| `sort()` | `['dates', 'milk', 'rice', 'tea', 'water']` |

### 13.3 Planning a trip

```python
route = ["Kuwait", "Dubai"]
route.insert(1, "Doha")
back = route[::-1]
trip = route + back[1:]
print(" -> ".join(route))
print(" -> ".join(trip))
print("Stops:", len(trip))
```

```text
Kuwait -> Doha -> Dubai
Kuwait -> Doha -> Dubai -> Doha -> Kuwait
Stops: 5
```

1. `insert(1, "Doha")` adds a stopover between Kuwait and Dubai.
2. `route[::-1]` creates the return route `['Dubai', 'Doha', 'Kuwait']` without changing `route`.
3. `back[1:]` removes the first `'Dubai'`, so it is not listed twice.
4. `route + back[1:]` creates the full trip as a new list.
5. `join()` turns each list into a readable string.

### 13.4 Electricity bill summary

A family's monthly electricity use (kWh) for the first half of the year:

```python
usage = [1200, 1100, 1500, 2300, 3100, 3600]
months = ["Jan", "Feb", "Mar", "Apr", "May", "Jun"]
print("Total:", sum(usage), "kWh")
print("Highest month:", max(usage), "kWh")
print("Last 3 months:", ", ".join(months[-3:]))
print("Their total:", sum(usage[-3:]), "kWh")
```

```text
Total: 12800 kWh
Highest month: 3600 kWh
Last 3 months: Apr, May, Jun
Their total: 9000 kWh
```

The same slice `[-3:]` is used on two **related** lists, so the months and the numbers stay matched.

---

## 14. Important Notes

- A slice **never** changes the list and **never** gives an `IndexError`.
- `len()`, `sum()`, `min()`, `max()`, `+`, and `join()` **give back** a value. Save it in a variable or print it.
- `append()`, `insert()`, `extend()`, `remove()`, `sort()`, and `reverse()` **change** the list and return `None`. Do not assign their result.
- `append()` adds **one** item; `extend()` adds **many**.
- `insert(index, item)` — index first, item second.
- `remove()` removes by **value**, only the **first** match, and fails if the value is missing.
- `sort()` and `min()` / `max()` need items of the **same kind**.
- `join()` is called on the **separator**, and every item must be a **string**.
- Methods that change a list exist only for **lists**, not for strings or tuples.

---

## 15. Common Mistakes

### Mistake 1: Assigning the result of a method

**Incorrect**

```python
nums = [3, 1, 2]
nums = nums.sort()
print(nums)
```

```text
None
```

**Why?** `sort()` sorts the list and returns `None`. That `None` then replaces the list.

**Correct**

```python
nums = [3, 1, 2]
nums.sort()
print(nums)
```

```text
[1, 2, 3]
```

The same mistake happens with `append()`, `insert()`, `extend()`, `remove()`, and `reverse()`.

### Mistake 2: Printing a method call

**Incorrect**

```python
cart = ["milk"]
print(cart.append("tea"))
```

```text
None
```

**Why?** `print()` shows the return value of `append()`, which is `None`.

**Correct**

```python
cart = ["milk"]
cart.append("tea")
print(cart)
```

```text
['milk', 'tea']
```

### Mistake 3: Using `append()` to add several items

**Incorrect** (goal: add two grades)

```python
grades = [80, 90]
grades.append([70, 60])
print(grades)
```

```text
[80, 90, [70, 60]]
```

**Why?** `append()` adds the list `[70, 60]` as one nested item.

**Correct**

```python
grades = [80, 90]
grades.extend([70, 60])
print(grades)
```

```text
[80, 90, 70, 60]
```

### Mistake 4: Removing a value that is not there

**Incorrect**

```text
cart = ["rice", "tea"]
cart.remove("milk")
ValueError: list.remove(x): x not in list
```

**Correct**

```python
cart = ["rice", "tea"]
if "milk" in cart:
    cart.remove("milk")
print(cart)
```

```text
['rice', 'tea']
```

### Mistake 5: Using `remove()` with an index

**Incorrect** (goal: remove the item at index 0)

```text
nums = [5, 0, 9]
nums.remove(0)
print(nums)
[5, 9]
```

**Why?** `remove(0)` removes the **value** 0, not the item at index 0. Here it happened to delete the wrong item.

**Correct:** pass the **value** you want to delete:

```python
nums = [5, 0, 9]
nums.remove(nums[0])
print(nums)
```

```text
[0, 9]
```

### Mistake 6: Writing `join()` the wrong way round

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

### Mistake 7: Joining numbers

**Incorrect**

```text
date = [12, 10, 2026]
print("/".join(date))
TypeError: sequence item 0: expected str instance, int found
```

**Correct**

```python
date = ["12", "10", "2026"]
print("/".join(date))
```

```text
12/10/2026
```

### Mistake 8: Expecting the stop index to be included

**Incorrect** (goal: the first three items)

```python
nums = [10, 20, 30, 40]
print(nums[0:2])
```

```text
[10, 20]
```

**Why?** The stop index is not included, so `[0:2]` gives only 2 items.

**Correct**

```python
nums = [10, 20, 30, 40]
print(nums[0:3])
print(nums[:3])
```

```text
[10, 20, 30]
[10, 20, 30]
```

### Mistake 9: Using `reverse()` to sort from largest to smallest

**Incorrect**

```python
nums = [3, 1, 2]
nums.reverse()
print(nums)
```

```text
[2, 1, 3]
```

**Why?** `reverse()` only flips the current order.

**Correct**

```python
nums = [3, 1, 2]
nums.sort(reverse=True)
print(nums)
```

```text
[3, 2, 1]
```

---

## 16. Mini Practice Questions

Try these before looking at the answers at the end of this section.

**Q1.** What does this print?

```python
x = ["a", "b", "c", "d", "e"]
print(x[1:3], x[-1], x[::2])
```

**Q2.** What does this print?

```python
data = [5, 3, 8]
print(sum(data[1:]), max(data) - min(data))
```

**Q3.** What is the length of `lst` after this code?

```python
lst = [1, 2]
lst.extend([3, 4])
lst.append([5, 6])
```

**Q4.** What does this print?

```python
a = [5, 2, 9]
b = a[:]
b.sort()
print(a, b)
```

**Q5.** Write one line that prints `"K-W-T"` from `letters = ["K", "W", "T"]`.

**Q6.** True or false: `(3, 1, 2).sort()` sorts a tuple.

### Answers to Mini Practice

1. **`['b', 'c'] e ['a', 'c', 'e']`**
2. **`11 5`** — `data[1:]` is `[3, 8]` with sum 11; 8 − 3 = 5.
3. **5** — `[1, 2, 3, 4, [5, 6]]`. `extend` added two items; `append` added one nested list.
4. **`[5, 2, 9] [2, 5, 9]`** — `b` is a copy, so sorting it does not change `a`.
5. **`print("-".join(letters))`**
6. **False** — tuples are immutable and have no `sort()` method. Python gives an `AttributeError`.

---

## 17. Ask AI to Help You Understand

```text
Explain Python list slicing to me using a list of 7 daily temperatures in Kuwait.
Show what lst[1:4], lst[:3], lst[-2:], and lst[::-1] give, and explain each one.
Do not give me exercises yet.
```

```text
What is the difference between append() and extend() in Python?
Use a small shopping list example and draw the list before and after each call.
```

```text
I wrote nums = nums.sort() and now my list is None. Explain why this happens,
and list which other list methods behave the same way.
```

```text
Explain how ", ".join(names) works. Why is join written after the separator
and not after the list? Show what happens if the list contains a number.
```

```text
Give me five short Python questions about list methods (append, insert, extend,
remove, sort, reverse) where I must predict the output. Do not use loops.
Give me hints first and do not show the answers unless I ask.
```

> **Remember:** Always run the code yourself. AI can make mistakes, and running code is the only way to be sure.

---

## 18. Summary

- **Slicing** `lst[start:stop:step]` gives a **new** list. Start is included; stop is **not**. Leave out start/stop to go to the beginning/end. `lst[::-1]` is a reversed copy, `lst[:]` is a copy. Slicing works on strings and tuples too.
- **Functions** `len()`, `sum()`, `min()`, `max()` look at a list and give back a value. `sum()` needs numbers; `min()`/`max()` need items of the same kind and a non-empty list.
- **Adding:** `append(x)` adds one item at the end; `insert(i, x)` adds at index `i`; `extend(other)` adds every item of `other`; `a + b` creates a new combined list.
- **Removing:** `remove(x)` deletes the first item equal to `x`; check with `if x in lst` first.
- **Ordering:** `sort()` orders small → large, `sort(reverse=True)` large → small; `reverse()` flips the current order.
- **Making strings:** `"sep".join(list_of_strings)` builds one string. Every item must be a string.
- Methods that change a list return **`None`** — never write `lst = lst.method()`.
- Only **lists** can be changed. Strings and tuples support slicing and the functions, but not the changing methods.

---

## Basic Exercises

> Exercises 1–12 are the same as in the slides. Exercises 13–16 are extra practice.

**Exercise 1.** Predict the output.

```python
nums = [10, 20, 30, 40, 50, 60]
print(nums[1:4])
print(nums[-2:])
print(nums[::2])
```

**Exercise 2.** Predict the output.

```python
prices = [3, 1.5, 7, 2]
print(len(prices), min(prices))
print(max(prices), sum(prices))
```

**Exercise 3.** Find and fix the error.

```python
cities = ["Kuwait", "Doha"]
cities = cities.append("Muscat")
print(cities)
```

**Exercise 4.** Predict the output.

```python
lst = [1, 2, 3]
lst.append([4, 5])
print(lst)
print(len(lst))
```

**Exercise 13.** Predict the output.

```python
x = ["a", "c"]
x.insert(1, "b")
x.insert(0, "z")
print(x)
```

## Practice Exercises

**Exercise 5.** Kuwait temperatures for one week (Sunday to Saturday):

```python
temps = [44, 46, 48, 45, 47, 49, 43]
```

Print the last two days (Friday and Saturday) using a slice, then the highest, the lowest, and the average temperature.

**Exercise 6.** Start with `queue = ["Ali", "Sara", "Fahad"]`. Mona joins at the **end**, Noor is a VIP and goes to the **front**, then Sara **leaves**. Print the queue.

**Exercise 7.** Combine the two lists into one, sort it A to Z, and print it as one string separated by `", "`.

```python
a = ["Qatar", "Kuwait", "Oman"]
b = ["UAE", "Bahrain", "Saudi Arabia"]
```

**Exercise 8.** Explain what this code does and give its output.

```python
letters = ["t", "i", "a", "w", "u", "K"]
letters.reverse()
print("".join(letters))
```

**Exercise 14.** A course code is stored as a string: `code = "KWT-2026-CS126"`. Use slicing to print the country part `KWT`, the year `2026`, and the course `CS126`, each on its own line.

## Challenge Exercises

**Exercise 9.** Five judges give scores. Drop the **highest** and the **lowest**, then print the remaining scores and their average. (Hint: sort, then slice.)

```python
judges = [8, 9, 7, 10, 6]
```

**Exercise 10.** Using `if … in`, remove `"Doha"` from the list if it is there; otherwise print `Doha is not in the list`. Then do the same for `"Riyadh"` and print the list.

```python
cities = ["Kuwait", "Riyadh", "Muscat"]
```

**Exercise 11.** Print this date in two forms, `12/10/2026` and `2026-10-12`, **without** changing `parts`.

```python
parts = ["12", "10", "2026"]
```

**Exercise 12.** Predict the output. Be careful!

```python
a = [3, 1, 2]
b = a + [5]
a.sort()
print(a, b)
print(a[::-1])
print(b[-2:])
```

**Exercise 15.** The **median** of a list with an odd number of items is the middle value after sorting. Find and print the median of `nums = [7, 3, 9, 1, 5]`. Your code must work for **any** odd-length list, so use `len()` and `//` to find the middle index.

**Exercise 16.** Start with `words = ["is", "Python", "fun"]`. Using **only** list methods (`remove`, `insert`, `append`, …), rearrange the list into `["Python", "is", "really", "fun"]`. Then use `join()` to print `Python is really fun!`.

---

# Exercise Solutions

### Solution 1

- `nums[1:4]` → indexes 1, 2, 3.
- `nums[-2:]` → the last two items.
- `nums[::2]` → indexes 0, 2, 4.

```text
[20, 30, 40]
[50, 60]
[10, 30, 50]
```

### Solution 2

There are 4 prices. The smallest is 1.5, the largest is 7, and the total is 3 + 1.5 + 7 + 2 = 13.5.

```text
4 1.5
7 13.5
```

### Solution 3

`append()` changes the list and returns `None`. Assigning that result made `cities` equal to `None`, so the program prints `None`. Call `append()` on its own line:

```python
cities = ["Kuwait", "Doha"]
cities.append("Muscat")
print(cities)
```

```text
['Kuwait', 'Doha', 'Muscat']
```

### Solution 4

`append()` adds the list `[4, 5]` as **one** item, creating a nested list. So the length is 4, not 5.

```text
[1, 2, 3, [4, 5]]
4
```

### Solution 5

```python
temps = [44, 46, 48, 45, 47, 49, 43]
print("Weekend:", temps[-2:])
print("Highest:", max(temps))
print("Lowest:", min(temps))
print("Average:", sum(temps) / len(temps))
```

```text
Weekend: [49, 43]
Highest: 49
Lowest: 43
Average: 46.0
```

The total is 322, and 322 / 7 = 46.0.

### Solution 6

```python
queue = ["Ali", "Sara", "Fahad"]
queue.append("Mona")
queue.insert(0, "Noor")
queue.remove("Sara")
print(queue)
```

```text
['Noor', 'Ali', 'Fahad', 'Mona']
```

After `append`: Ali, Sara, Fahad, Mona. After `insert(0, ...)`: Noor, Ali, Sara, Fahad, Mona. After `remove("Sara")`: Noor, Ali, Fahad, Mona.

### Solution 7

```python
a = ["Qatar", "Kuwait", "Oman"]
b = ["UAE", "Bahrain", "Saudi Arabia"]
gcc = a + b
gcc.sort()
print(", ".join(gcc))
```

```text
Bahrain, Kuwait, Oman, Qatar, Saudi Arabia, UAE
```

Using `a.extend(b)` and then sorting `a` also works, but it changes `a`.

### Solution 8

`reverse()` flips the list into `["K", "u", "w", "a", "i", "t"]`. Then `"".join()` glues the letters together with nothing between them.

```text
Kuwait
```

### Solution 9

After sorting, the lowest score is first and the highest is last, so `[1:-1]` removes both.

```python
judges = [8, 9, 7, 10, 6]
judges.sort()
middle = judges[1:-1]
print(middle)
print(sum(middle) / len(middle))
```

```text
[7, 8, 9]
8.0
```

### Solution 10

```python
cities = ["Kuwait", "Riyadh", "Muscat"]
if "Doha" in cities:
    cities.remove("Doha")
else:
    print("Doha is not in the list")
if "Riyadh" in cities:
    cities.remove("Riyadh")
else:
    print("Riyadh is not in the list")
print(cities)
```

```text
Doha is not in the list
['Kuwait', 'Muscat']
```

### Solution 11

`parts[::-1]` makes a reversed **copy**, so `parts` itself is not changed.

```python
parts = ["12", "10", "2026"]
print("/".join(parts))
print("-".join(parts[::-1]))
print(parts)
```

```text
12/10/2026
2026-10-12
['12', '10', '2026']
```

Using `parts.reverse()` would also print the second form, but it would change `parts`, which the exercise does not allow.

### Solution 12

`b = a + [5]` creates a **new** list from the **current** contents of `a`. Sorting `a` afterwards does not affect `b`.

```text
[1, 2, 3] [3, 1, 2, 5]
[3, 2, 1]
[2, 5]
```

### Solution 13

After `insert(1, "b")`: `['a', 'b', 'c']`. After `insert(0, "z")`: `['z', 'a', 'b', 'c']`.

```text
['z', 'a', 'b', 'c']
```

### Solution 14

```python
code = "KWT-2026-CS126"
print(code[:3])
print(code[4:8])
print(code[-5:])
```

```text
KWT
2026
CS126
```

Index 3 is the first `-`, so the year starts at index 4. The last five characters are the course code.

### Solution 15

```python
nums = [7, 3, 9, 1, 5]
nums.sort()
middle = len(nums) // 2
print("Sorted:", nums)
print("Median:", nums[middle])
```

```text
Sorted: [1, 3, 5, 7, 9]
Median: 5
```

For 5 items, `5 // 2` is 2, which is the middle index. For 7 items, `7 // 2` is 3, also the middle. This is why the code works for any odd-length list.

### Solution 16

```python
words = ["is", "Python", "fun"]
words.remove("Python")
words.insert(0, "Python")
words.insert(2, "really")
print(words)
print(" ".join(words) + "!")
```

```text
['Python', 'is', 'really', 'fun']
Python is really fun!
```

Step by step: after `remove`: `['is', 'fun']`; after `insert(0, "Python")`: `['Python', 'is', 'fun']`; after `insert(2, "really")`: `['Python', 'is', 'really', 'fun']`.

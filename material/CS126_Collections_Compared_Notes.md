# CS126 – Introduction to Python

## List vs Tuple vs Set vs String

**Instructor:** Dr. Fawaz Alazemi

---

## Learning Objectives

After studying these notes, you should be able to:

1. Create a string, a list, a tuple, and a set, including the empty and one-item versions of each.
2. List the operations that work on **all four** types.
3. Explain the three key differences between them: **order**, **duplicates**, and **mutability**.
4. Know which operations work only on some of the types: indexing, slicing, `+`, `*`, `count`, `index`, and set operations.
5. Explain what kinds of values each type can hold.
6. Predict whether a method changes the value or returns a new one.
7. Convert between the four types with `list()`, `tuple()`, `set()`, `sorted()`, `split()`, and `join()`.
8. Predict the result of `==` and `in` for each type.
9. Choose the most suitable type for a task, and explain the choice.

---

## 1. Introduction

### 1.1 Why a review lecture?

In the last few lectures you met four ways to store a group of values:

- **strings** — text,
- **lists** — ordered, changeable collections,
- **tuples** — ordered, fixed collections,
- **sets** — collections of unique values with no order.

Each was studied on its own. But in real programs, the most important skill is to **choose the right one** for each piece of data — and to know what each can and cannot do. This lecture puts the four types side by side so you can see clearly how they are **similar** and how they are **different**.

### 1.2 A first look

```python
name = "Kuwait"
cart = ["rice", "tea", "rice"]
date = (16, 10, 2026)
ids = {101, 102, 103}
print(type(name), type(cart))
print(type(date), type(ids))
```

```text
<class 'str'> <class 'list'>
<class 'tuple'> <class 'set'>
```

All four are **collections**: one variable that holds several values. A string is a collection of **characters**; the other three can hold other kinds of values.

---

## 2. Main Concepts and Vocabulary

| Term | Meaning |
|---|---|
| **Collection** | A value that holds several other values |
| **Item** (element) | One value inside a collection |
| **Ordered** | Items have positions (indexes 0, 1, 2, …) and keep the order they were given |
| **Duplicate** | The same value appearing more than once |
| **Mutable** | Can be changed after it is created (add, remove, replace items) |
| **Immutable** | Cannot be changed after it is created |
| **Conversion** | Making a value of one type from a value of another type, e.g. `list("abc")` |

---

## 3. Creating Each Type

### 3.1 Syntax summary

| Type | Written with | Several items | Empty | One item |
|---|---|---|---|---|
| String | quotes | `"abc"` | `""` | `"a"` |
| List | `[ ]` | `[1, 2, 3]` | `[]` | `[5]` |
| Tuple | `( )` | `(1, 2, 3)` | `()` | `(5,)` |
| Set | `{ }` | `{1, 2, 3}` | `set()` | `{5}` |

### 3.2 Two traps

**The one-item tuple needs a comma.** Without it, the brackets are just ordinary brackets, as in arithmetic:

```python
print(type((5)), type((5,)))
```

```text
<class 'int'> <class 'tuple'>
```

**The empty set is `set()`, not `{}`.** Empty curly brackets create a **dictionary**, a different type that you will learn later:

```python
print(type({}), type(set()))
```

```text
<class 'dict'> <class 'set'>
```

---

## 4. The Three Key Questions

Almost every difference between the four types comes from three questions:

| Question | String | List | Tuple | Set |
|---|---|---|---|---|
| **Ordered?** (positions, indexes) | ✔ | ✔ | ✔ | ✘ |
| **Duplicates allowed?** | ✔ | ✔ | ✔ | ✘ |
| **Mutable?** (can change) | ✘ | ✔ | ✘ | ✔ |

Two patterns are worth remembering:

- For **order** and **duplicates**, the **set** is the odd one out.
- For **mutability**, the types form two pairs: **list and set** can change; **string and tuple** cannot.

The following sections look at each of these differences, and then at the similarities.

---

## 5. Similarities

### 5.1 len() and in work on all four

```python
s = "Oman"
l = ["Oman", "Qatar"]
t = ("Oman", "Qatar")
st = {"Oman", "Qatar"}
print(len(s), len(l), len(t), len(st))
```

```text
4 2 2 2
```

`len()` counts the **characters** of a string and the **items** of a list, tuple, or set.

`in` also works on all four, and always returns `True` or `False`. But **what it looks for** depends on the type:

```python
s = "Oman"
l = ["Oman", "Qatar"]
t = ("Oman", "Qatar")
st = {"Oman", "Qatar"}
print("man" in s, "man" in l)
print("Oman" in t, "Oman" in st)
```

```text
True False
True True
```

| Type | `x in c` is `True` when… |
|---|---|
| string | the text `x` appears somewhere inside `c` |
| list / tuple / set | an item of `c` is **equal** to `x` |

Membership tests are also much **faster** on a set than on a list or tuple, especially for large collections.

### 5.2 min(), max(), sum(), sorted()

These functions only **read** the items, so they work on all four types:

```python
l = [4, 1, 3]
t = (4, 1, 3)
st = {4, 1, 3}
print(min(l), max(t), sum(st))
print(sorted(l), sorted(t), sorted(st))
print(min("Kuwait"), sorted("cab"))
```

```text
1 4 8
[1, 3, 4] [1, 3, 4] [1, 3, 4]
K ['a', 'b', 'c']
```

- `sorted()` always returns a **list**, whatever type you give it.
- With a string, these functions work on its **characters**. `"K"` is the smallest character of `"Kuwait"` because capital letters come before small letters.
- `sum()` needs numbers, so it does **not** work on strings.

### 5.3 Indexing and slicing (string, list, tuple)

The three **ordered** types share indexes and slices:

```python
s = "Kuwait"
l = [10, 20, 30, 40]
t = (10, 20, 30, 40)
print(s[0], l[0], t[0])
print(s[-1], l[-1], t[-1])
print(s[1:3], l[1:3], t[1:3])
print(s[::-1], l[::-1], t[::-1])
```

```text
K 10 10
t 40 40
uw [20, 30] (20, 30)
tiawuK [40, 30, 20, 10] (40, 30, 20, 10)
```

A slice always gives back the **same type**: a slice of a string is a string, of a list is a list, of a tuple is a tuple.

Sets have no positions, so they cannot be indexed or sliced:

```text
st = {10, 20, 30}
print(st[0])

TypeError: 'set' object is not subscriptable
```

### 5.4 + and * (string, list, tuple)

```python
print("ab" + "cd", "ab" * 2)
print([1, 2] + [3], [0] * 3)
print((1, 2) + (3,), (0,) * 3)
```

```text
abcd abab
[1, 2, 3] [0, 0, 0]
(1, 2, 3) (0, 0, 0)
```

- `+` joins two values of the **same type**; `*` repeats.
- The result is always a **new** value; the originals do not change.
- Mixing types is an error: `[1] + (2,)` and `"a" + [1]` cause a `TypeError`.

Sets do not support `+` or `*`. To combine two sets, use **union** (`|`):

```python
print({1, 2} | {2, 3})
```

```text
{1, 2, 3}
```

### 5.5 count() and index() (string, list, tuple)

The three ordered types share these two methods:

```python
s = "banana"
l = list(s)
t = tuple(s)
print(s.count("a"), l.count("a"), t.count("a"))
print(s.index("n"), l.index("n"), t.index("n"))
```

```text
3 3 3
2 2 2
```

Sets have neither: every item appears at most once (so a count would always be 0 or 1), and there are no positions (so there is no index).

---

## 6. Difference 1: Order

Strings, lists, and tuples **remember the order** in which their items were given. Every item has a position, and the order never changes by itself.

A set has **no order**. When you print a set, Python chooses the order, and for strings it may be different every time you run the program:

```python
st = {"Sun", "Mon", "Tue"}
print(len(st))
print(sorted(st))
```

```text
3
['Mon', 'Sun', 'Tue']
```

`sorted()` gives a predictable order, but it is **alphabetical**, not the original order. The original order is lost as soon as the values go into a set.

**Rule:** if the order matters — a queue, the days of the week, the steps of a recipe, a list of temperatures by day — **do not** use a set.

---

## 7. Difference 2: Duplicates

Strings, lists, and tuples keep **every** copy of a value. A set keeps **one** copy:

```python
visits = ["Ali", "Sara", "Ali", "Ali"]
print(len(visits), visits.count("Ali"))
t = tuple(visits)
print(len(t), t.count("Ali"))
st = set(visits)
print(len(st))
print("banana".count("a"), len(set("banana")))
```

```text
4 3
4 3
2
3 3
```

This gives two very useful patterns:

- `len(set(x))` — the number of **different** values in `x`.
- `sorted(set(x))` — the different values, in sorted order, as a list.

But be careful: removing duplicates is not always correct. If two students both scored 88, both grades must be counted in the average:

```python
grades = [88, 75, 88]
print(sum(grades) / len(grades))
print(sum(set(grades)) / len(set(grades)))
```

```text
83.66666666666667
81.5
```

The second line is **wrong** as an average, because one 88 was lost.

---

## 8. Difference 3: Mutability

### 8.1 Mutable types: list and set

Lists and sets can be changed after they are created:

```python
l = [1, 2, 3]
l[0] = 9
l.append(4)
st = {1, 2}
st.add(3)
st.remove(1)
print(l, st)
```

```text
[9, 2, 3, 4] {2, 3}
```

- A list can change an item by **position**, add items, and remove items.
- A set cannot change "the item at a position" (it has none), but it can **add** and **remove** items.

### 8.2 Immutable types: string and tuple

Strings and tuples cannot be changed at all:

```text
s = "cat"
s[0] = "b"

TypeError: 'str' object does not support item assignment
```

```text
t = (1, 2, 3)
t[0] = 9

TypeError: 'tuple' object does not support item assignment
```

They also have no methods such as `append()` or `remove()`.

### 8.3 "Changing" an immutable value

You can always **build a new** string or tuple, and give it the old variable name:

```python
s = "cat"
s = "b" + s[1:]
print(s)
t = (1, 2, 3)
t = (9,) + t[1:]
print(t)
```

```text
bat
(9, 2, 3)
```

For more complicated changes to a tuple, convert it to a list, change the list, and convert it back:

```python
t = (1, 2, 3)
temp = list(t)
temp.append(4)
t = tuple(temp)
print(t)
```

```text
(1, 2, 3, 4)
```

If you need to change a collection often, it should probably be a **list** (or a set) from the start.

### 8.4 Why have immutable types at all?

- **Safety:** data that must not change (a date of birth, the days of the week) is protected from accidental changes.
- **Clear meaning:** a reader immediately knows the value is fixed.
- **Set items:** only immutable values can be stored in a set (Section 9).

---

## 9. Difference 4: What Can Be Stored Inside

| Type | Items can be… |
|---|---|
| String | only **characters** |
| List | anything — numbers, strings, tuples, even other lists |
| Tuple | anything — numbers, strings, lists, other tuples |
| Set | only **immutable** values — numbers, strings, tuples |

```python
mixed = [5, "Kuwait", (29, 47), [1, 2]]
print(len(mixed), mixed[3][1])
places = {(29, 47), (25, 51)}
print((29, 47) in places)
```

```text
4 2
True
```

A list cannot be an item of a set, because a set item must never change:

```text
s = {[29, 47]}

TypeError: unhashable type: 'list'
```

This is one more reason to store a pair such as a location as a **tuple**.

Notice also the difference between strings and tuples: both are immutable, but a string can hold **only characters**, while a tuple can hold **any** values.

---

## 10. Methods

### 10.1 Overview

| Type | Common methods | Do they change the value? |
|---|---|---|
| String | `upper`, `lower`, `strip`, `replace`, `find`, `split`, `startswith`, `count`, `index` | Never — they return a new value |
| List | `append`, `insert`, `extend`, `remove`, `sort`, `reverse`, `count`, `index` | Most of them change the list and return `None` |
| Tuple | `count`, `index` | Never |
| Set | `add`, `update`, `remove`, `discard`, `union`, `intersection`, `difference` | `add`, `update`, `remove`, `discard` change it; `union` etc. return a new set |

### 10.2 Change in place, or return a new value?

This difference is a common source of bugs.

**List methods usually change the list and return `None`:**

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

**String methods always return a new string and leave the original alone:**

```python
s = "kuwait"
result = s.upper()
print(result)
print(s)
```

```text
KUWAIT
kuwait
```

**The function `sorted()` returns a new list and leaves the original alone:**

```python
nums = [3, 1, 2]
new = sorted(nums)
print(new, nums)
```

```text
[1, 2, 3] [3, 1, 2]
```

Rule of thumb:

- **Mutable** type (list, set): methods usually **change it in place**. Do not save their result (`nums = nums.sort()` makes `nums` equal to `None`).
- **Immutable** type (string, tuple): methods **return** a new value. Always save it (`s = s.upper()`).

---

## 11. Comparing with ==

```python
print("ab" == "ba")
print([1, 2] == [2, 1])
print((1, 2) == (2, 1))
print({1, 2} == {2, 1})
print([1, 2] == (1, 2))
print(list((1, 2)) == [1, 2])
```

```text
False
False
False
True
False
True
```

| Comparison | Equal when… |
|---|---|
| string with string, list with list, tuple with tuple | same items in the **same order** |
| set with set | same items, **any** order |
| different types (e.g. list with tuple) | never equal |

To compare a list with a tuple, convert one of them first.

---

## 12. Converting Between the Types

### 12.1 Conversion functions

| To get a… | Use | Example | Result |
|---|---|---|---|
| list | `list(x)` | `list("abc")` | `['a', 'b', 'c']` |
| list of words | `s.split()` | `"a b c".split()` | `['a', 'b', 'c']` |
| tuple | `tuple(x)` | `tuple([1, 2])` | `(1, 2)` |
| set | `set(x)` | `set([3, 1, 3])` | `{1, 3}` |
| sorted list | `sorted(x)` | `sorted({3, 1, 2})` | `[1, 2, 3]` |
| string | `"sep".join(x)` | `"-".join(["a", "b"])` | `'a-b'` |

```python
word = "banana"
print(list(word))
print(tuple(word))
print(sorted(set(word)))
nums = [3, 1, 3, 2]
print(tuple(nums), set(nums))
print("-".join(["a", "b", "c"]))
print("a b c".split())
```

```text
['b', 'a', 'n', 'a', 'n', 'a']
('b', 'a', 'n', 'a', 'n', 'a')
['a', 'b', 'n']
(3, 1, 3, 2) {1, 2, 3}
a-b-c
['a', 'b', 'c']
```

### 12.2 Notes on conversions

- `list()`, `tuple()`, and `set()` on a **string** split it into **characters**.
- `set()` removes duplicates and **loses the order**.
- `join()` needs a collection of **strings**.
- `str([1, 2])` does not join items — it gives the text `"[1, 2]"`, which is rarely what you want:

```python
print(str([1, 2]))
print(len(str([1, 2])))
```

```text
[1, 2]
6
```

### 12.3 A common chain: remove duplicates, keep a sorted result

```python
t = (5, 3, 8, 3)
clean = tuple(sorted(set(t)))
print(clean)
```

```text
(3, 5, 8)
```

`set` removes the duplicate 3, `sorted` gives a list in order, and `tuple` makes the result fixed.

---

## 13. The Complete Comparison

| | String | List | Tuple | Set |
|---|---|---|---|---|
| Example | `"abc"` | `[1, 2]` | `(1, 2)` | `{1, 2}` |
| Empty | `""` | `[]` | `()` | `set()` |
| One item | `"a"` | `[5]` | `(5,)` | `{5}` |
| Holds | characters | anything | anything | immutable values |
| Ordered / indexes / slices | ✔ | ✔ | ✔ | ✘ |
| Duplicates | ✔ | ✔ | ✔ | ✘ (removed) |
| Mutable | ✘ | ✔ | ✘ | ✔ |
| `len`, `in`, `min`, `max`, `sorted` | ✔ | ✔ | ✔ | ✔ |
| `sum` | ✘ | ✔ | ✔ | ✔ |
| `+` and `*` | ✔ | ✔ | ✔ | ✘ (use `\|`) |
| `count`, `index` | ✔ | ✔ | ✔ | ✘ |
| Union, intersection, difference | ✘ | ✘ | ✘ | ✔ |
| `in` checks | text | items | items | items (fastest) |
| `==` cares about order | ✔ | ✔ | ✔ | ✘ |
| Methods change the value? | never | usually | never | some |

---

## 14. How to Choose

### 14.1 Three questions

1. **Is it text?** → **string**.
2. **Do you need each value only once, and the order does not matter** (or do you mainly ask "is it there?")? → **set**.
3. **Will the data change while the program runs?** → yes: **list**; no: **tuple**.

### 14.2 Examples

| Situation | Choice | Reason |
|---|---|---|
| A student's name | String | text |
| A shopping cart | List | items are added and removed |
| Daily temperatures for a week | List | order matters; values can repeat |
| Every grade in an exam | List | two equal grades must both count |
| A date (16, 10, 2026) | Tuple | a fixed record; position gives meaning |
| Days of the week | Tuple | fixed and ordered |
| GPS location of Kuwait Towers | Tuple | two fixed numbers |
| IDs of students present today | Set | unique; fast "is present?" checks |
| Different words in an essay | Set | each word once |
| Allowed usernames | Set | fast membership checks |

### 14.3 Using several types together

Real programs usually use several types at once — each for the data it suits best:

```python
name = "  noor alsabah "
birth = (12, 5, 2006)
grades = [88, 75, 88]
courses = {"CS126", "MATH101"}
name = name.strip().title()
grades.append(92)
courses.add("CS126")
courses.add("ENG110")
day, month, year = birth
print(name, "born in", year)
print(len(grades), sum(grades) / len(grades))
print(len(courses), sorted(courses))
```

```text
Noor Alsabah born in 2006
4 85.75
3 ['CS126', 'ENG110', 'MATH101']
```

- **String:** the name, cleaned with string methods (and saved back, because strings are immutable).
- **Tuple:** the birth date never changes; it is unpacked into three variables.
- **List:** the grades grow, and the repeated 88 is correct — both count.
- **Set:** adding `"CS126"` a second time does nothing; each course appears once.

---

## 15. Worked Examples

### 15.1 The same data, four ways

```python
s = "banana"
l = list(s)
t = tuple(s)
st = set(s)
print(len(s), len(l), len(t), len(st))
print(s.count("a"), l.count("a"), t.count("a"))
print(s[0], l[0], t[0])
print("n" in s, "n" in l, "n" in t, "n" in st)
l[0] = "B"
print("".join(l), s)
```

```text
6 6 6 3
3 3 3
b b b
True True True True
Banana banana
```

1. The string, list, and tuple each keep all 6 characters; the set keeps only the 3 different ones.
2. `count` and indexing work on the three ordered types.
3. `in` works on all four.
4. Only the list can be changed. `join` turns it back into a string, and the original string `s` is unchanged.

### 15.2 From text to clean data and back

```python
text = "Kuwait,Qatar,Kuwait,Oman,Qatar,Kuwait"
visits = text.split(",")
print(len(visits), visits.count("Kuwait"))
unique = set(visits)
print(len(unique))
ordered = tuple(sorted(unique))
print(ordered)
print(" | ".join(ordered))
```

```text
6 3
3
('Kuwait', 'Oman', 'Qatar')
Kuwait | Oman | Qatar
```

| Step | Conversion | Why |
|---|---|---|
| 1 | string → list (`split`) | to work with separate values and count them |
| 2 | list → set | to remove duplicates |
| 3 | set → sorted list → tuple | to get a fixed, ordered result |
| 4 | tuple → string (`join`) | to display it nicely |

### 15.3 Exam grades

```python
line = "90 85 90 70 85 95"
grades = line.split()
print(len(grades))
different = set(grades)
print(len(different))
print(tuple(sorted(different)))
```

```text
6
4
('70', '85', '90', '95')
```

Note that the grades are still **strings** (they came from `split`). Sorting works here because all of them have two digits; to do arithmetic, each would need `int()` — which requires a loop, covered later.

---

## 16. Important Notes

- All four types share `len`, `in`, `min`, `max`, and `sorted`.
- Only the **ordered** types (string, list, tuple) have indexes, slices, `+`, `*`, `count`, and `index`.
- Only **sets** remove duplicates and support union, intersection, and difference.
- **List and set** are mutable; **string and tuple** are immutable.
- A string holds only characters; a set holds only immutable values; lists and tuples hold anything.
- `in` looks for **text** in a string and for an **equal item** in the other types.
- `sorted()` always returns a list.
- `==` is order-sensitive for strings, lists, and tuples, but not for sets; different types are never equal.
- Empty set: `set()`. One-item tuple: `(5,)`.

---

## 17. Common Mistakes

### Mistake 1: Using {} for an empty set

**Incorrect**

```text
visitors = {}
visitors.add("Ali")

AttributeError: 'dict' object has no attribute 'add'
```

**Correct**

```python
visitors = set()
visitors.add("Ali")
print(visitors)
```

```text
{'Ali'}
```

### Mistake 2: Forgetting the comma in a one-item tuple

**Incorrect**

```python
colors = ("red")
print(type(colors), len(colors))
```

```text
<class 'str'> 3
```

**Correct**

```python
colors = ("red",)
print(type(colors), len(colors))
```

```text
<class 'tuple'> 1
```

### Mistake 3: Calling a list method on a tuple or string

**Incorrect**

```text
t = (3, 1, 2)
t.sort()

AttributeError: 'tuple' object has no attribute 'sort'
```

**Correct**

```python
t = (3, 1, 2)
t = tuple(sorted(t))
print(t)
```

```text
(1, 2, 3)
```

### Mistake 4: Indexing a set

**Incorrect**

```text
ids = {101, 102, 103}
print(ids[0])

TypeError: 'set' object is not subscriptable
```

**Correct**

```python
ids = {101, 102, 103}
print(sorted(ids)[0])
```

```text
101
```

### Mistake 5: set("word") instead of {"word"}

**Incorrect** (goal: a set with one city)

```python
cities = set("Doha")
print(len(cities))
```

```text
4
```

**Correct**

```python
cities = {"Doha"}
print(len(cities))
```

```text
1
```

### Mistake 6: Comparing a list with a tuple

**Incorrect**

```python
answer = (1, 2, 3)
key = [1, 2, 3]
print(answer == key)
```

```text
False
```

**Correct**

```python
answer = (1, 2, 3)
key = [1, 2, 3]
print(list(answer) == key)
```

```text
True
```

### Mistake 7: Saving the result of a list method

**Incorrect**

```python
nums = [3, 1, 2]
nums = nums.sort()
print(nums)
```

```text
None
```

**Correct**

```python
nums = [3, 1, 2]
nums.sort()
print(nums)
```

```text
[1, 2, 3]
```

### Mistake 8: Not saving the result of a string method

**Incorrect**

```python
city = "kuwait"
city.upper()
print(city)
```

```text
kuwait
```

**Correct**

```python
city = "kuwait"
city = city.upper()
print(city)
```

```text
KUWAIT
```

### Mistake 9: Using a set when duplicates matter

**Incorrect** (goal: total of all payments)

```python
payments = [5, 10, 5]
print(sum(set(payments)))
```

```text
15
```

**Correct**

```python
payments = [5, 10, 5]
print(sum(payments))
```

```text
20
```

---

## 18. Mini Practice Questions

Try these before looking at the answers at the end of this section.

**Q1.** Which types support indexing: string, list, tuple, set?

**Q2.** Which types are mutable?

**Q3.** What does this print?

```python
print(len("aab"), len(["a", "a", "b"]), len(set("aab")))
```

**Q4.** What does this print?

```python
print(sorted((3, 1, 2)), type(sorted({3, 1, 2})))
```

**Q5.** What does this print?

```python
print("ab" in "cabd", "ab" in ["cabd"], "cabd" in ("cabd",))
```

**Q6.** Which line causes an error: `"a" * 3`, `[1] * 3`, `(1,) * 3`, `{1} * 3`?

### Answers to Mini Practice

1. **String, list, and tuple.** Sets have no positions.
2. **List and set.**
3. **`3 3 2`**
4. **`[1, 2, 3] <class 'list'>`** — `sorted` always returns a list.
5. **`True False True`**
6. **`{1} * 3`** — sets do not support `*`.

---

## 19. Ask AI to Help You Understand

```text
Compare Python strings, lists, tuples, and sets in a simple table for a beginner:
ordered or not, duplicates or not, mutable or not, and one everyday example of each.
Do not use loops or dictionaries, and do not give me exercises yet.
```

```text
Why can't I write t[0] = 5 for a tuple or s[0] = "x" for a string, when I can for a list?
Explain mutability with a simple real-life comparison.
```

```text
Why does nums.sort() return None, while name.upper() returns a new string?
Explain the difference between methods that change a value and methods that return a new one.
```

```text
Give me eight short situations, one at a time, and ask me whether to use a string,
a list, a tuple, or a set. Wait for my answer each time before telling me if I am right and why.
```

> **Remember:** Always run the code yourself. AI can make mistakes, and running code is the only way to be sure.

---

## 20. Summary

- **String:** text; ordered; duplicates allowed; **immutable**; holds only characters.
- **List:** ordered; duplicates allowed; **mutable**; holds anything.
- **Tuple:** ordered; duplicates allowed; **immutable**; holds anything.
- **Set:** **unordered**; **no duplicates**; mutable; holds only immutable values.
- **Shared by all four:** `len`, `in`, `min`, `max`, `sorted` (and `sum` for numbers).
- **Shared by the ordered types:** indexes, slices, `+`, `*`, `count`, `index`.
- **Only sets:** union `|`, intersection `&`, difference `-`, and automatic removal of duplicates.
- Mutable types change in place (methods return `None`); immutable types return new values (always save them).
- Convert with `list()`, `tuple()`, `set()`, `sorted()`, `split()`, and `join()`.
- Choose by asking: **text? unique? will it change?** — and use several types together when it helps.

---

## Basic Exercises

> Exercises 1–12 are the same as in the slides. Exercises 13–16 are extra practice.

**Exercise 1.** Predict the output.

```python
print(type("a"), type(["a"]))
print(type(("a",)), type({"a"}))
```

**Exercise 2.** Predict the output.

```python
data = "hello"
print(len(data), len(list(data)))
print(len(set(data)))
```

**Exercise 3.** Find the error and fix it so the program prints the sorted values.

```text
t = (3, 1, 2)
t.sort()
print(t)
```

**Exercise 4.** Predict the output.

```python
print([1, 2] == [2, 1], (1, 2) == (1, 2))
print({1, 2} == {2, 1}, [1, 2] == (1, 2))
```

**Exercise 13.** Predict the output.

```python
x = "abc"
print(x + "d", x * 2, x[::-1], len(set(x + x)))
```

## Practice Exercises

**Exercise 5.** For `grades = [90, 85, 90, 70, 85]`, print the number of grades, the number of **different** grades, the highest grade, and the different grades as a sorted list.

**Exercise 6.** A string cannot be changed. Convert `word = "Kuwait"` to a list, change the first letter to `"k"`, and join it back into a string. Print the result.

**Exercise 7.** Which lines cause an error? Explain each one.

```text
s = "abc"
t = (1, 2)
l = [1, 2]
st = {1, 2}
s[0] = "x"     # A
t[0] = 9       # B
l[0] = 9       # C
st[0] = 9      # D
```

**Exercise 8.** Predict and explain.

```python
a = [1, 2, 3]
b = (1, 2, 3)
c = {1, 2, 3}
print(2 in a, 2 in b, 2 in c)
print(sum(a) == sum(b) == sum(c))
```

**Exercise 14.** For `sentence = "the cat and the hat"`, print the number of words, the number of **different** words, the first word, and whether `"hat"` is one of the words.

## Challenge Exercises

**Exercise 9.** Choose string, list, tuple, or set, and give a reason:

1. The characters used in a password (each once)
2. The days of the week
3. A shopping cart
4. A student's full name
5. IDs of students present today

**Exercise 10.** Predict the output.

```python
s = "a,b,a,c"
parts = s.split(",")
print(parts, len(parts))
u = sorted(set(parts))
print(u, "-".join(u))
```

**Exercise 11.** For `t = (5, 3, 8, 3)`, build a **tuple** with the different values in sorted order: `(3, 5, 8)`. Then print whether 8 is in it, and its index.

**Exercise 12.** Predict the output.

```python
x = [1, 2]
y = (1, 2)
z = {1, 2}
print(x + [3], y + (3,), z | {3})
print(x * 2, len(y * 3))
```

**Exercise 15.** Country codes are stored as `codes = ("KW", "QA", "KW", "OM")`. Print how many times `"KW"` appears, how many **different** codes there are, and the different codes as a sorted list.

**Exercise 16.** Each line below causes an error. Explain why, and give a correct line that adds the value.

```text
t = (1, 2)
t.append(3)        # A
s = "hi"
s.append("!")      # B
st = {1, 2}
st.append(3)       # C
```

---

# Exercise Solutions

### Solution 1

```text
<class 'str'> <class 'list'>
<class 'tuple'> <class 'set'>
```

`("a",)` has a comma, so it is a tuple.

### Solution 2

`"hello"` has 5 characters, and the list of its characters also has 5 items. The set keeps only the different characters: h, e, l, o.

```text
5 5
4
```

### Solution 3

Tuples have no `sort()` method (`AttributeError: 'tuple' object has no attribute 'sort'`), because sorting would change the tuple. Use the function `sorted()`, which works on any type and returns a new list, then convert back to a tuple:

```python
t = (3, 1, 2)
t = tuple(sorted(t))
print(t)
```

```text
(1, 2, 3)
```

### Solution 4

- `[1, 2] == [2, 1]` → `False`: lists care about order.
- `(1, 2) == (1, 2)` → `True`.
- `{1, 2} == {2, 1}` → `True`: sets ignore order.
- `[1, 2] == (1, 2)` → `False`: a list is never equal to a tuple.

```text
False True
True False
```

### Solution 5

```python
grades = [90, 85, 90, 70, 85]
print(len(grades), len(set(grades)))
print(max(grades), sorted(set(grades)))
```

```text
5 3
90 [70, 85, 90]
```

### Solution 6

```python
word = "Kuwait"
letters = list(word)
letters[0] = "k"
word = "".join(letters)
print(word)
```

```text
kuwait
```

The string itself cannot change, but a list of its characters can. `join` builds a new string from the changed list. (A shorter way for this case: `"k" + word[1:]`.)

### Solution 7

Only **C** works.

- **A** — strings are immutable: `TypeError: 'str' object does not support item assignment`.
- **B** — tuples are immutable: `TypeError: 'tuple' object does not support item assignment`.
- **C** — lists are mutable: `l` becomes `[9, 2]`.
- **D** — sets have no positions: `TypeError: 'set' object does not support item assignment`.

### Solution 8

`in` works on all three collections, and `2` is an item of each. `sum` works on all three; each sum is 6, so the chained comparison is `True`.

```text
True True True
True
```

### Solution 9

| | Choice | Reason |
|---|---|---|
| 1. Characters used in a password | **Set** | each character only once |
| 2. Days of the week | **Tuple** | fixed and ordered |
| 3. Shopping cart | **List** | items are added and removed |
| 4. A student's full name | **String** | it is text |
| 5. IDs of students present | **Set** | unique IDs; fast "is present?" |

### Solution 10

`split` makes a list that keeps the duplicate `"a"`. `set` removes it, `sorted` gives a sorted list, and `join` builds a string.

```text
['a', 'b', 'a', 'c'] 4
['a', 'b', 'c'] a-b-c
```

### Solution 11

```python
t = (5, 3, 8, 3)
clean = tuple(sorted(set(t)))
print(clean)
print(8 in clean, clean.index(8))
```

```text
(3, 5, 8)
True 2
```

### Solution 12

Lists and tuples are joined with `+`; sets are combined with `|`. `x * 2` repeats the list; `y * 3` is a tuple of 6 items.

```text
[1, 2, 3] (1, 2, 3) {1, 2, 3}
[1, 2, 1, 2] 6
```

### Solution 13

`x + "d"` joins; `x * 2` repeats; `x[::-1]` reverses; `x + x` is `"abcabc"`, which has 3 different characters.

```text
abcd abcabc cba 3
```

### Solution 14

```python
sentence = "the cat and the hat"
words = sentence.split()
print(len(words), len(set(words)))
print(words[0], "hat" in words)
```

```text
5 4
the True
```

`"the"` appears twice, so there are 5 words but only 4 different words.

### Solution 15

```python
codes = ("KW", "QA", "KW", "OM")
print(codes.count("KW"))
print(len(set(codes)))
print(sorted(set(codes)))
```

```text
2
3
['KW', 'OM', 'QA']
```

### Solution 16

- **A** — tuples are immutable and have no `append`. Build a new tuple: `t = t + (3,)`.
- **B** — strings are immutable and have no `append`. Build a new string: `s = s + "!"`.
- **C** — sets have no `append` because they have no "end" (no order). Use `add`: `st.add(3)`.

```python
t = (1, 2)
t = t + (3,)
s = "hi"
s = s + "!"
st = {1, 2}
st.add(3)
print(t, s, st)
```

```text
(1, 2, 3) hi! {1, 2, 3}
```

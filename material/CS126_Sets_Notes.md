# CS126 – Introduction to Python

## Sets

**Instructor:** Dr. Fawaz Alazemi

---

## Learning Objectives

After studying these notes, you should be able to:

1. Explain what a set is: a collection of **unique** items with **no order**.
2. Create sets with curly brackets and with `set()`, including the empty set.
3. Use sets to remove duplicates from lists, tuples, and strings.
4. Explain why sets have no indexes, and use `sorted()` when you need a fixed order.
5. Use `len()`, `in`, `not in`, `==`, `min()`, `max()`, and `sum()` with sets.
6. Change a set with `add()`, `update()`, `remove()`, `discard()`, and `clear()`.
7. Combine sets with union (`|`), intersection (`&`), difference (`-`), and symmetric difference (`^`).
8. Test subsets and supersets with `<=` and `>=`.
9. Know which values can be stored in a set.
10. Compare sets with lists and tuples, and choose the right structure for a task.

---

## 1. Introduction

### 1.1 Two common problems

You already know two ways to store many values: **lists** and **tuples**. Both keep items **in order**, and both allow **repeated** values. That is often exactly what we want — but not always.

**Problem 1: repeated values.** A café records the name of each customer who visits:

```python
visits = ["Ali", "Sara", "Ali", "Mona", "Ali"]
print(len(visits))
```

```text
5
```

There were 5 **visits**, but how many **different** customers? With what we know so far, answering that question is not easy.

**Problem 2: comparing groups.** Sara and Ali each have a list of courses. Which courses do they take **together**? Which does only Sara take? Comparing two lists item by item is hard without loops.

### 1.2 The solution: sets

A **set** solves both problems:

```python
visits = ["Ali", "Sara", "Ali", "Mona", "Ali"]
print(len(set(visits)))
sara = {"CS126", "MATH101", "ENG110"}
ali = {"CS126", "PHYS101", "ENG110"}
print(len(sara & ali))
```

```text
3
2
```

- `set(visits)` keeps each name only **once**, so there are 3 different customers.
- `sara & ali` gives the courses that are in **both** sets: 2 courses.

### 1.3 Sets in mathematics

You may remember sets from mathematics: A = {1, 2, 3}. A mathematical set has two important properties:

1. Each element appears **once**. {1, 1, 2} is the same set as {1, 2}.
2. There is **no order**. {1, 2, 3} is the same set as {3, 1, 2}.

Python sets follow exactly the same rules, and support the same operations: union, intersection, and difference.

### 1.4 A real-life picture

Think of a set as a **bag of name badges** at an event. Each person has exactly one badge, so no name appears twice. The badges are mixed up inside the bag, so there is no "first" or "second" badge. You can only ask: *"Is Sara's badge in the bag?"*

---

## 2. Main Concepts and Vocabulary

| Term | Meaning | Example |
|---|---|---|
| **Set** | An unordered collection of unique items | `{1, 2, 3}` |
| **Unique** | Each value appears at most once | `{1, 1, 2}` becomes `{1, 2}` |
| **Unordered** | Items have no positions | no `s[0]` |
| **Empty set** | A set with no items | `set()` |
| **Union** | Items in A **or** B (or both) | `A \| B` |
| **Intersection** | Items in A **and** B | `A & B` |
| **Difference** | Items in A but **not** in B | `A - B` |
| **Symmetric difference** | Items in **exactly one** of A and B | `A ^ B` |
| **Subset** | Every item of A is also in B | `A <= B` |
| **Superset** | A contains every item of B | `A >= B` |

---

## 3. Creating Sets

### 3.1 With curly brackets

```text
name = {item1, item2, item3, ...}
```

```python
nums = {3, 1, 2}
print(nums)
print(type(nums))
print(len(nums))
```

```text
{1, 2, 3}
<class 'set'>
3
```

- **Curly brackets** `{ }` surround the items.
- **Commas** separate the items.

### 3.2 From a list, tuple, or string: set()

The `set()` function converts other collections into a set, keeping each value only once:

```python
print(set([4, 4, 5, 6, 5]))
print(set((7, 7, 8)))
print(len(set("banana")))
```

```text
{4, 5, 6}
{8, 7}
3
```

With a string, each **character** becomes an item. `"banana"` has the characters b, a, n — three different ones.

Notice that `set((7, 7, 8))` printed as `{8, 7}`. Python chose that order, not us. This is normal for sets (see Section 5).

### 3.3 The empty set: set(), not {}

```python
empty = set()
print(empty)
print(len(empty))
print(type({}))
```

```text
set()
0
<class 'dict'>
```

Be careful: `{}` does **not** create an empty set. It creates an empty **dictionary**, another Python type that you will learn about later. The only way to write an empty set is `set()`.

### 3.4 Mixed types

Like lists and tuples, a set can contain different types:

```python
s = {5, 2.5, "Kuwait", (29, 47)}
print(len(s))
print("Kuwait" in s)
```

```text
4
True
```

But there is a limit on which values can be stored — see Section 9.

---

## 4. Sets Remove Duplicates

### 4.1 One copy of each value

When you create a set, or add to it, duplicates are dropped automatically:

```python
grades = [90, 85, 90, 70, 85, 90]
unique = set(grades)
print(len(grades))
print(len(unique))
print(set([1, 1, 1]))
```

```text
6
3
{1}
```

The list has 6 grades, but only 3 **different** values: 70, 85, and 90.

### 4.2 Counting different values

A very common use: `len(set(x))` counts the **different** values in a list, tuple, or string.

```python
answers = ("A", "C", "A", "B", "A", "C")
print("Different answers:", len(set(answers)))
word = "Mississippi"
print("Different letters:", len(set(word)))
```

```text
Different answers: 3
Different letters: 4
```

"Mississippi" has the letters M, i, s, p — four different characters.

### 4.3 Case and type still matter

Sets use **equality** to decide whether two items are the same:

```python
print(len({"Doha", "doha", "Doha"}))
print(len({1, "1"}))
```

```text
2
2
```

- `"Doha"` and `"doha"` are different strings.
- `1` (a number) and `"1"` (a string) are different values.

---

## 5. Sets Have No Order

### 5.1 No indexes and no slices

Because set items have no positions, you cannot use `[ ]` with a set:

```text
gcc = {"Kuwait", "Qatar", "Oman"}
print(gcc[0])

TypeError: 'set' object is not subscriptable
```

"Not subscriptable" means "you cannot use square brackets with this value". Slices like `gcc[0:2]` fail for the same reason.

### 5.2 The printed order is not guaranteed

When you print a set, Python shows the items in **its own** order, which may look random:

```python
gcc = {"Kuwait", "Qatar", "Oman"}
print(gcc)
```

One possible output (order may differ):

```text
{'Oman', 'Kuwait', 'Qatar'}
```

For sets of strings, the order may even be different **each time you run the program**. Never write a program that depends on the order of a set.

### 5.3 Getting a fixed order: sorted()

When you need the items in a fixed order — for example, to print them neatly — use the built-in function `sorted()`. It returns a new **sorted list** and does not change the set:

```python
gcc = {"Kuwait", "Qatar", "Oman"}
print(sorted(gcc))
print(sorted({30, 10, 20}))
```

```text
['Kuwait', 'Oman', 'Qatar']
[10, 20, 30]
```

`sorted()` works on lists, tuples, strings, and sets. It always gives a **list**.

---

## 6. Reading a Set: in, len, ==, min, max, sum

### 6.1 Membership: the main job of a set

```python
allowed = {"sara", "ali", "mona"}
user = "ali"
if user in allowed:
    print("Welcome,", user)
else:
    print("Access denied")
print("fahad" not in allowed)
```

```text
Welcome, ali
True
```

Checking `x in s` is what sets are best at. A set can answer "is it in?" **very quickly**, even when it holds millions of items. A list must look at its items one by one, so it gets slower as it grows.

### 6.2 Length

```python
print(len({"Kuwait", "Qatar", "Oman"}))
print(len(set()))
```

```text
3
0
```

### 6.3 Equality: order does not matter

Two sets are equal if they contain the same items, in **any** order:

```python
print({1, 2, 3} == {3, 2, 1})
print([1, 2, 3] == [3, 2, 1])
print((1, 2, 3) == (3, 2, 1))
print({1, 2} == {1, 2, 2})
```

```text
True
False
False
True
```

- Sets ignore order, so the first comparison is `True`.
- Lists and tuples are ordered, so a different order means **not** equal.
- `{1, 2, 2}` is the same set as `{1, 2}`.

### 6.4 min, max, sum

These functions only read the items, so they work with sets:

```python
scores = {72, 95, 58, 88}
print(min(scores), max(scores), sum(scores))
```

```text
58 95 313
```

---

## 7. Changing a Set

Sets are **mutable**: you can add and remove items. Like list methods, these methods change the set **in place** and return `None`.

### 7.1 add(x): add one item

```python
ids = {101, 102}
ids.add(103)
print(ids)
ids.add(101)
print(ids)
```

```text
{101, 102, 103}
{101, 102, 103}
```

Adding a value that is already there does nothing — **no error** and **no duplicate**.

### 7.2 update(collection): add many items

```python
ids = {101, 102, 103}
ids.update([104, 105, 102])
print(ids)
print(len(ids))
```

```text
{101, 102, 103, 104, 105}
5
```

`update()` adds every item from a list, tuple, string, or another set. Items already in the set are ignored.

There is no `append()` or `insert()` for sets: those methods are about **positions**, and sets have none.

### 7.3 remove(x) and discard(x)

Both delete an item. The difference is what happens when the item is **not** there:

```python
ids = {101, 102, 103}
ids.remove(102)
print(ids)
ids.discard(999)
print(ids)
```

```text
{101, 103}
{101, 103}
```

```text
ids = {101, 103}
ids.remove(999)

KeyError: 999
```

| Method | Item present | Item missing |
|---|---|---|
| `remove(x)` | removes it | **KeyError** |
| `discard(x)` | removes it | does nothing |

When to use which?

- Use `remove()` when the item **should** be there. If it is not, the error tells you about a bug.
- Use `discard()` when the item **may or may not** be there and either case is fine.

You can also check first with `in`:

```python
cart = {"rice", "tea"}
if "milk" in cart:
    cart.remove("milk")
else:
    print("milk is not in the cart")
```

```text
milk is not in the cart
```

### 7.4 clear(): remove everything

```python
cart = {"rice", "tea"}
cart.clear()
print(cart)
print(len(cart))
```

```text
set()
0
```

---

## 8. Set Operations

Set operations combine two sets and produce a **new** set. The original sets do **not** change.

We will use these two sets for all examples:

```python
A = {1, 2, 3, 4}
B = {3, 4, 5, 6}
```

```text
        A                B
   +---------+------+---------+
   |  1, 2   | 3, 4 |  5, 6   |
   | only A  | both | only B  |
   +---------+------+---------+
```

### 8.1 Union: A | B

All items that are in A **or** B (or both), each listed once:

```python
A = {1, 2, 3, 4}
B = {3, 4, 5, 6}
print(A | B)
print(A.union(B))
```

```text
{1, 2, 3, 4, 5, 6}
{1, 2, 3, 4, 5, 6}
```

### 8.2 Intersection: A & B

Only the items that are in **both** A and B:

```python
A = {1, 2, 3, 4}
B = {3, 4, 5, 6}
print(A & B)
print(A.intersection(B))
print({1, 2} & {3, 4})
```

```text
{3, 4}
{3, 4}
set()
```

If the sets have nothing in common, the result is the **empty set**.

### 8.3 Difference: A - B

Items in A that are **not** in B:

```python
A = {1, 2, 3, 4}
B = {3, 4, 5, 6}
print(A - B)
print(B - A)
print(A.difference(B))
```

```text
{1, 2}
{5, 6}
{1, 2}
```

**Order matters** for difference: `A - B` and `B - A` are usually different. Think of `A - B` as "start with A, then take away anything that is also in B".

### 8.4 Symmetric difference: A ^ B

Items in **exactly one** of the sets — not in both:

```python
A = {1, 2, 3, 4}
B = {3, 4, 5, 6}
print(A ^ B)
print(A.symmetric_difference(B))
print((A | B) - (A & B))
```

```text
{1, 2, 5, 6}
{1, 2, 5, 6}
{1, 2, 5, 6}
```

The last line shows another way to think about it: "everything" minus "the shared part".

### 8.5 Summary of operations

| Operation | Operator | Method | Meaning | `A = {1,2,3,4}`, `B = {3,4,5,6}` |
|---|---|---|---|---|
| Union | `A \| B` | `A.union(B)` | in A or B | `{1, 2, 3, 4, 5, 6}` |
| Intersection | `A & B` | `A.intersection(B)` | in both | `{3, 4}` |
| Difference | `A - B` | `A.difference(B)` | in A, not in B | `{1, 2}` |
| Symmetric difference | `A ^ B` | `A.symmetric_difference(B)` | in exactly one | `{1, 2, 5, 6}` |

The operators and the methods give the same result. The operators are shorter; the method names are easier to remember at first. Use whichever you find clearer.

### 8.6 Operations do not change the original sets

```python
A = {1, 2, 3, 4}
B = {3, 4, 5, 6}
C = A | B
print(A)
print(B)
print(C)
```

```text
{1, 2, 3, 4}
{3, 4, 5, 6}
{1, 2, 3, 4, 5, 6}
```

---

## 9. Subsets and Supersets

### 9.1 Subset: A <= B

`A <= B` is `True` if **every** item of A is also in B:

```python
required = {"CS126", "MATH101"}
taken = {"CS126", "ENG110", "MATH101"}
print(required <= taken)
print(required.issubset(taken))
print({1, 2} <= {1, 2})
print({1, 5} <= {1, 2, 3})
```

```text
True
True
True
False
```

Every set is a subset of itself, so `{1, 2} <= {1, 2}` is `True`.

### 9.2 Superset: A >= B

`A >= B` is `True` if A contains every item of B. It is the same as `B <= A`:

```python
taken = {"CS126", "ENG110", "MATH101"}
print(taken >= {"CS126"})
print(taken.issuperset({"CS126", "PHYS101"}))
```

```text
True
False
```

### 9.3 Example: which requirements are missing?

```python
required = {"CS126", "MATH101", "ENG110"}
taken = {"CS126", "ARAB101"}
if required <= taken:
    print("All requirements done")
else:
    missing = required - taken
    print("Still need:", sorted(missing))
```

```text
Still need: ['ENG110', 'MATH101']
```

---

## 10. What Can Be Stored in a Set?

Set items must be **immutable** values: numbers, strings, Booleans, and **tuples**. Lists and sets cannot be set items, because they can change after being stored.

```python
s = {5, 2.5, "Kuwait", (29, 47), True}
print(len(s))
print((29, 47) in s)
```

```text
5
True
```

```text
s = {[29, 47]}

TypeError: unhashable type: 'list'
```

"Unhashable" is Python's word for "cannot be used as a set item". This is one more reason to store a location as a **tuple** `(29, 47)` rather than a list.

A related surprise: `True` and `1` are considered equal in Python, so a set cannot contain both:

```python
print(len({1, True}))
```

```text
1
```

You will rarely meet this, but it explains strange results if you mix them.

---

## 11. Converting Between Lists, Tuples, and Sets

| To get… | Use | Example | Result |
|---|---|---|---|
| a set | `set(x)` | `set([3, 1, 3])` | `{1, 3}` |
| a list | `list(x)` | `list({2, 1})` | `[1, 2]` (any order) |
| a tuple | `tuple(x)` | `tuple({5})` | `(5,)` |
| a sorted list | `sorted(x)` | `sorted({3, 1, 2})` | `[1, 2, 3]` |

### 11.1 Removing duplicates from a list

```python
nums = [5, 3, 5, 1, 3, 9]
unique = list(set(nums))
unique.sort()
print(unique)
print(sorted(set(nums)))
```

```text
[1, 3, 5, 9]
[1, 3, 5, 9]
```

Both lines give the same result. Converting to a set removes the duplicates, but it also **loses the original order**, so we sort afterwards to get a predictable result.

---

## 12. Lists vs Tuples vs Sets

### 12.1 Comparison table

| | List | Tuple | Set |
|---|---|---|---|
| Written as | `[1, 2, 3]` | `(1, 2, 3)` | `{1, 2, 3}` |
| Empty | `[]` | `()` | `set()` |
| Ordered? | Yes | Yes | **No** |
| Duplicates? | Allowed | Allowed | **Removed** |
| Indexes and slices | ✔ | ✔ | ✘ |
| Can change? | Yes | No | Yes (add/remove only) |
| Add items | `append`, `insert`, `extend` | ✘ | `add`, `update` |
| Remove items | `remove` | ✘ | `remove`, `discard` |
| `len`, `in`, `min`, `max`, `sum` | ✔ | ✔ | ✔ |
| `==` cares about order? | Yes | Yes | No |
| Union, intersection, difference | ✘ | ✘ | ✔ |
| Items must be immutable? | No | No | **Yes** |

### 12.2 How to choose

Ask yourself three questions:

1. **Does the order matter?** If yes → list or tuple.
2. **Will the data change?** If yes → list (or set); if no → tuple.
3. **Should each value appear only once, or do I need fast "is it in?" checks or group comparisons?** If yes → set.

| Situation | Best choice | Why |
|---|---|---|
| Customers in a queue | List | order matters; people join and leave |
| Daily temperatures for a week | List | order matters; values can repeat |
| A date `(12, 10, 2026)` | Tuple | fixed record; position gives meaning |
| GPS location of Kuwait Towers | Tuple | two fixed numbers |
| Different words used in an essay | Set | each word once; order not needed |
| GCC countries a traveler has visited | Set | no repeats; order not needed |
| Allowed usernames | Set | fast membership checks |

---

## 13. Worked Examples

### 13.1 Unique visitors

```python
visits = ["Ali", "Sara", "Ali", "Mona",
          "Sara", "Ali", "Fahad"]
people = set(visits)
print("Visits:", len(visits))
print("Different people:", len(people))
print("Ali came", visits.count("Ali"), "times")
if "Noor" not in people:
    print("Noor did not visit")
```

```text
Visits: 7
Different people: 4
Ali came 3 times
Noor did not visit
```

Both structures are useful here: the **list** remembers every visit (so we can count repeats), and the **set** gives the different people (and fast membership checks).

### 13.2 Comparing course schedules

```python
sara = {"CS126", "MATH101", "ENG110", "ARAB101"}
ali = {"CS126", "PHYS101", "ENG110"}
common = sara & ali
print("Study together:", sorted(common))
print("Only Sara:", sorted(sara - ali))
print("Only Ali:", sorted(ali - sara))
print("All courses:", len(sara | ali))
if len(common) >= 2:
    print("Good study partners!")
```

```text
Study together: ['CS126', 'ENG110']
Only Sara: ['ARAB101', 'MATH101']
Only Ali: ['PHYS101']
All courses: 5
Good study partners!
```

The union has 4 + 3 − 2 = 5 courses: we add both sizes and subtract the shared courses, which would otherwise be counted twice.

### 13.3 Food allergy check

```python
dish = {"rice", "chicken", "nuts", "milk"}
allergies = {"nuts", "eggs"}
problem = dish & allergies
if len(problem) > 0:
    print("Not safe:", sorted(problem))
else:
    print("Safe to eat")
```

```text
Not safe: ['nuts']
```

### 13.4 Checking a password's characters

```python
password = "kuwait2026"
chars = set(password)
digits = set("0123456789")
print("Different characters:", len(chars))
if len(chars & digits) == 0:
    print("Add at least one digit")
else:
    print("Digits used:", sorted(chars & digits))
```

```text
Different characters: 9
Digits used: ['0', '2', '6']
```

`set(password)` has the characters k, u, w, a, i, t, 2, 0, 6 — nine different ones. The intersection with the set of digit characters shows which digits appear.

---

## 14. Important Notes

- A set holds **unique** values with **no order**.
- The empty set is `set()`. `{}` is an empty **dictionary**.
- `set(x)` removes duplicates; `len(set(x))` counts different values.
- Sets have **no indexes and no slices** (`TypeError: ... not subscriptable`).
- The printed order of a set is not guaranteed. Use `sorted()` for a fixed order.
- `==` between sets ignores order.
- `add()` and `update()` never create duplicates and never raise an error for existing items.
- `remove()` raises `KeyError` for a missing item; `discard()` does not.
- `|`, `&`, `-`, `^` give **new** sets and do not change the originals. For `-`, the order of the sets matters.
- Set items must be immutable: numbers, strings, tuples — not lists or sets.

---

## 15. Common Mistakes

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

### Mistake 2: Using an index with a set

**Incorrect**

```text
ids = {101, 102, 103}
print(ids[0])

TypeError: 'set' object is not subscriptable
```

**Correct** — if you need an order, sort first:

```python
ids = {101, 102, 103}
ordered = sorted(ids)
print(ordered[0])
```

```text
101
```

### Mistake 3: Removing a missing item with remove()

**Incorrect**

```text
cart = {"rice", "tea"}
cart.remove("milk")

KeyError: 'milk'
```

**Correct**

```python
cart = {"rice", "tea"}
cart.discard("milk")
print(len(cart))
```

```text
2
```

### Mistake 4: Adding a list with add()

**Incorrect**

```text
tags = {"python"}
tags.add(["loops", "sets"])

TypeError: unhashable type: 'list'
```

**Why?** `add()` tries to store the whole list as **one** item, and lists cannot be set items.

**Correct**

```python
tags = {"python"}
tags.update(["loops", "sets"])
print(sorted(tags))
```

```text
['loops', 'python', 'sets']
```

### Mistake 5: set("word") instead of {"word"}

**Incorrect** (goal: a set containing one city)

```python
cities = set("Kuwait")
print(len(cities))
```

```text
6
```

**Why?** `set("Kuwait")` makes a set of **characters**.

**Correct**

```python
cities = {"Kuwait"}
print(len(cities))
```

```text
1
```

### Mistake 6: Depending on the order of a set

**Incorrect**

```text
names = {"Sara", "Ali", "Mona"}
print(list(names)[0])    # expecting "Sara"
```

**Why?** The order of a set is not guaranteed, so "the first item" could be any of the three names, and it may change between runs.

**Correct:** if order matters, keep a **list**; if you need a predictable order from a set, use `sorted(names)`.

### Mistake 7: Using a set when duplicates matter

**Incorrect** (goal: total of all payments)

```python
payments = [5, 10, 5, 20]
print(sum(set(payments)))
```

```text
35
```

**Why?** Converting to a set removed the second 5 KD payment. Two payments of the same amount are still two payments.

**Correct**

```python
payments = [5, 10, 5, 20]
print(sum(payments))
```

```text
40
```

---

## 16. Mini Practice Questions

Try these before looking at the answers at the end of this section.

**Q1.** What does this print?

```python
print(len({5, 5, 6, 6, 6, 7}))
```

**Q2.** What does this print?

```python
A = {1, 2, 3}
B = {2, 3, 4}
print(A & B, A - B, len(A | B))
```

**Q3.** Which of these creates an empty set: `{}`, `set()`, or `set([])`?

**Q4.** What does this print?

```python
s = {1, 2, 3}
s.add(2)
s.add(4)
s.discard(1)
print(len(s), 1 in s, sum(s))
```

**Q5.** True or false: `{1, 2} <= {1, 2, 3}`.

**Q6.** What does this print?

```python
print(sorted(set("hello")))
```

### Answers to Mini Practice

1. **`3`** — the different values are 5, 6, 7.
2. **`{2, 3} {1} 4`**
3. **`set()` and `set([])`** both create an empty set. `{}` creates an empty dictionary.
4. **`3 False 9`** — the set is `{2, 3, 4}`.
5. **True** — every item of `{1, 2}` is in `{1, 2, 3}`.
6. **`['e', 'h', 'l', 'o']`** — the two `l`s become one.

---

## 17. Ask AI to Help You Understand

```text
Explain Python sets to a beginner who knows lists and tuples.
Use an example of students and courses at a university in Kuwait.
Do not use loops, and do not give me exercises yet.
```

```text
Explain union, intersection, difference, and symmetric difference in Python
using two small sets of numbers. Draw a simple text Venn diagram for each one.
```

```text
Why does Python print a set in a different order than I wrote it?
Why can't I use an index like s[0] with a set? Explain simply.
```

```text
What is the difference between remove() and discard() for Python sets?
Give one situation where each one is the better choice.
```

```text
Give me five situations and ask me whether each should use a list, a tuple, or a set.
Wait for my answer each time before telling me if I am right and why.
```

> **Remember:** Always run the code yourself. AI can make mistakes, and running code is the only way to be sure.

---

## 18. Summary

- A **set** is an unordered collection of **unique** items: `{1, 2, 3}`. The empty set is `set()`.
- `set(x)` converts a list, tuple, or string into a set and removes duplicates.
- Sets have **no indexes or slices**, and the printed order is not guaranteed. `sorted(s)` gives a sorted list.
- `in` / `not in` (very fast), `len`, `min`, `max`, `sum` work on sets. `==` ignores order.
- `add(x)` and `update(c)` add items; `remove(x)` (error if missing), `discard(x)` (no error), and `clear()` remove items.
- **Union** `|`, **intersection** `&`, **difference** `-`, and **symmetric difference** `^` create new sets.
- `A <= B` tests whether A is a **subset** of B.
- Set items must be **immutable** (numbers, strings, tuples).
- **List:** ordered, changeable, duplicates allowed. **Tuple:** ordered, fixed. **Set:** unordered, unique, changeable, great for membership and comparing groups.

---

## Basic Exercises

> Exercises 1–12 are the same as in the slides. Exercises 13–16 are extra practice.

**Exercise 1.** Predict the output.

```python
s = {3, 1, 3, 2, 1}
print(len(s))
print(2 in s, 5 in s)
```

**Exercise 2.** Predict the output.

```python
a = {1, 2, 3, 4}
b = {3, 4, 5}
print(a & b)
print(a | b)
print(a - b)
```

**Exercise 3.** Find and fix the error.

```text
empty = {}
empty.add(5)
```

**Exercise 4.** Predict the output.

```python
print(len(set("banana")))
print(len("banana"))
print({1, 2} == {2, 1})
```

**Exercise 13.** Predict the output.

```python
letters = set("hello")
print(len(letters))
print("l" in letters, "z" in letters)
```

## Practice Exercises

**Exercise 5.** For the list below, print the number of visits, the number of different visitors, and whether `"Fahad"` visited.

```python
visitors = ["Ali", "Sara", "Ali",
            "Mona", "Sara", "Ali"]
```

**Exercise 6.** Print the courses both students take (sorted), the number of different courses, and the courses only Sara takes (sorted).

```python
sara = {"CS126", "MATH101", "ENG110"}
ali = {"CS126", "PHYS101", "ENG110"}
```

**Exercise 7.** Start with `tags = {"python", "beginner"}`. Add `"loops"`, remove `"beginner"`, then remove `"java"` **without an error**. Print the sorted tags.

**Exercise 8.** Explain each result and give the output.

```python
print({1, 2, 3} == {3, 2, 1})
print([1, 2, 3] == [3, 2, 1])
print((1, 2) == (2, 1))
```

**Exercise 14.** A student must pass `required = {"CS126", "MATH101"}` to graduate. They have passed `taken = {"CS126", "ENG110", "MATH101"}`. Use a subset test to print `Can graduate` or `Cannot graduate yet`.

## Challenge Exercises

**Exercise 9.** Remove the duplicates from `nums = [5, 3, 5, 1, 3, 9]`. The result must be a **sorted list**: `[1, 3, 5, 9]`.

**Exercise 10.** A dish contains `{"rice", "nuts", "chicken", "milk"}`. A customer is allergic to `{"milk", "eggs"}`. Print `Not safe:` and the problem ingredients (sorted), or `Safe`.

**Exercise 11.** Predict the output.

```python
s = {1, 2}
s.add(2)
s.add(3)
s.discard(7)
s.update([4, 1])
print(s, len(s))
```

**Exercise 12.** List, tuple, or set? Choose and give a reason:

1. The different words used in an essay
2. The GPS location of Kuwait Towers
3. Customers waiting in line at a bank
4. The GCC countries a traveler has visited

**Exercise 15.** How many **different letters** are in `"Kuwait University"`? Ignore the difference between capital and small letters, and do not count the space.

**Exercise 16.** Two classes have these students. Print (sorted) the students who are in **exactly one** of the classes, and the number of students in **both**.

```python
class_a = {"Ali", "Sara", "Mona", "Fahad"}
class_b = {"Sara", "Noor", "Fahad", "Omar"}
```

---

# Exercise Solutions

### Solution 1

The duplicates are removed, so the set is `{1, 2, 3}`. 2 is in the set; 5 is not.

```text
3
True False
```

### Solution 2

- `a & b`: in both → `{3, 4}`
- `a | b`: in either → `{1, 2, 3, 4, 5}`
- `a - b`: in `a` but not `b` → `{1, 2}`

```text
{3, 4}
{1, 2, 3, 4, 5}
{1, 2}
```

### Solution 3

`{}` creates an empty **dictionary**, which has no `add()` method, so Python gives `AttributeError: 'dict' object has no attribute 'add'`. Use `set()`:

```python
empty = set()
empty.add(5)
print(empty)
```

```text
{5}
```

### Solution 4

`set("banana")` is `{'b', 'a', 'n'}` (3 items), while the string has 6 characters. Sets ignore order, so `{1, 2} == {2, 1}`.

```text
3
6
True
```

### Solution 5

```python
visitors = ["Ali", "Sara", "Ali",
            "Mona", "Sara", "Ali"]
people = set(visitors)
print(len(visitors), len(people))
print("Fahad" in people)
```

```text
6 3
False
```

### Solution 6

```python
sara = {"CS126", "MATH101", "ENG110"}
ali = {"CS126", "PHYS101", "ENG110"}
print(sorted(sara & ali))
print(len(sara | ali))
print(sorted(sara - ali))
```

```text
['CS126', 'ENG110']
4
['MATH101']
```

### Solution 7

```python
tags = {"python", "beginner"}
tags.add("loops")
tags.remove("beginner")
tags.discard("java")
print(sorted(tags))
```

```text
['loops', 'python']
```

`remove()` is fine for `"beginner"` because we know it is there. `discard()` is needed for `"java"` because it is not in the set.

### Solution 8

- Sets are **unordered**, so `{1, 2, 3}` and `{3, 2, 1}` are the same set → `True`.
- Lists are **ordered**, so a different order means a different list → `False`.
- Tuples are also **ordered** → `False`.

```text
True
False
False
```

### Solution 9

```python
nums = [5, 3, 5, 1, 3, 9]
result = sorted(set(nums))
print(result)
```

```text
[1, 3, 5, 9]
```

Another correct answer: `result = list(set(nums))` followed by `result.sort()`.

### Solution 10

```python
dish = {"rice", "nuts", "chicken", "milk"}
allergies = {"milk", "eggs"}
problem = dish & allergies
if len(problem) > 0:
    print("Not safe:", sorted(problem))
else:
    print("Safe")
```

```text
Not safe: ['milk']
```

### Solution 11

- `s.add(2)`: 2 is already there → no change.
- `s.add(3)`: the set becomes `{1, 2, 3}`.
- `s.discard(7)`: 7 is not there → no change, no error.
- `s.update([4, 1])`: adds 4; 1 is already there.

```text
{1, 2, 3, 4} 4
```

### Solution 12

| | Choice | Reason |
|---|---|---|
| 1. Different words in an essay | **Set** | Each word is needed only once; order does not matter. |
| 2. GPS location of Kuwait Towers | **Tuple** | Two fixed numbers whose order (latitude, longitude) matters. |
| 3. Customers in line | **List** | The order matters, and people join and leave. |
| 4. GCC countries visited | **Set** | Visiting a country twice still counts once; order does not matter. |

### Solution 13

`"hello"` has the characters h, e, l, l, o; the set keeps h, e, l, o.

```text
4
True False
```

### Solution 14

```python
required = {"CS126", "MATH101"}
taken = {"CS126", "ENG110", "MATH101"}
if required <= taken:
    print("Can graduate")
else:
    print("Cannot graduate yet")
```

```text
Can graduate
```

### Solution 15

```python
text = "Kuwait University"
letters = set(text.lower().replace(" ", ""))
print(len(letters))
print(sorted(letters))
```

```text
12
['a', 'e', 'i', 'k', 'n', 'r', 's', 't', 'u', 'v', 'w', 'y']
```

`lower()` makes `K` and `U` small letters, so they match `k` and `u`; `replace(" ", "")` removes the space before the set is made.

### Solution 16

```python
class_a = {"Ali", "Sara", "Mona", "Fahad"}
class_b = {"Sara", "Noor", "Fahad", "Omar"}
print(sorted(class_a ^ class_b))
print(len(class_a & class_b))
```

```text
['Ali', 'Mona', 'Noor', 'Omar']
2
```

The symmetric difference gives the students in exactly one class. The intersection (Sara and Fahad) has 2 students.

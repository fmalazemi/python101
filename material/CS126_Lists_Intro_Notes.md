# CS126 – Introduction to Python

## Introduction to Lists

**Instructor:** Dr. Fawaz Alazemi

---

## Learning Objectives

After studying these notes, you should be able to:

1. Explain what a list is, and why programs need lists instead of many separate variables.
2. Create lists of numbers, strings, and mixed values, and create an empty list.
3. Read any item using a **positive** or **negative** index.
4. Use `len()` to find the number of items and the last valid index.
5. Recognize and avoid an `IndexError`.
6. Change an item in a list, and explain why lists can change but strings cannot.
7. Use `in`, `not in`, `==`, and `!=` with lists, inside `if` statements.
8. Read and change items in a simple nested list.
9. Explain what happens when two variable names refer to the same list.

---

## 1. Introduction

### 1.1 The problem: many related values

Until now, each variable stored **one** value:

```python
grade1 = 85
grade2 = 92
grade3 = 78
grade4 = 95
grade5 = 70
```

This works for five students, but it quickly becomes a problem:

- A class of 200 students would need 200 variable names.
- If a new student joins, you must add a new variable **and** change the code that uses the grades.
- Nothing tells Python that these five variables belong together.

Real data often comes in groups: the grades of a class, the temperatures of a week, the prices in a shopping basket, the GCC countries, the courses in a semester. We need a way to store a **group** of values under **one** name.

### 1.2 The solution: a list

A **list** stores many values, in order, in a single variable:

```python
grades = [85, 92, 78, 95, 70]
print(grades)
```

```text
[85, 92, 78, 95, 70]
```

Now all five grades live together under the name `grades`. As you will see, you can still reach each grade individually by its position.

### 1.3 A real-life picture

Think of one row of seats in a classroom. The whole row has one name ("Row A"), and each seat has a number. To find a student, you say "Row A, seat 3". A list works the same way: the list has one name, and each item has a position number called an **index**.

---

## 2. Main Concepts and Vocabulary

| Term | Meaning | Example |
|---|---|---|
| **List** | An ordered collection of values in one variable | `[85, 92, 78]` |
| **Item** (element) | One value inside a list | `92` |
| **Index** | The position number of an item, starting at 0 | in `grades[1]`, the index is `1` |
| **Negative index** | A position counted from the end; −1 is the last item | `grades[-1]` |
| **Empty list** | A list with no items | `[]` |
| **Length** | The number of items in a list | `len(grades)` |
| **Mutable** | Can be changed after it is created | lists |
| **Immutable** | Cannot be changed after it is created | strings |
| **Nested list** | A list that contains other lists as items | `[[1, 2], [3, 4]]` |

---

## 3. Creating Lists

### 3.1 Syntax

```text
name = [item1, item2, item3, ...]
```

- **Square brackets** `[ ]` begin and end the list.
- **Commas** separate the items.
- Spaces after the commas are optional, but they make the list easier to read.

### 3.2 Different kinds of lists

```python
temps = [44, 46, 48]
cities = ["Kuwait", "Doha"]
student = ["Sara", 20, 3.6]
flags = [True, False, True]
empty = []
print(temps)
print(cities)
print(student)
print(flags)
print(empty)
```

```text
[44, 46, 48]
['Kuwait', 'Doha']
['Sara', 20, 3.6]
[True, False, True]
[]
```

Notice:

- When Python prints a list of strings, it shows each string with **single quotes**, even if you wrote double quotes. This is only how Python displays it; the strings are the same.
- A list can contain values of **different types** (`student` has a string, an integer, and a float). In practice, most lists contain items of **one** type, because that makes them easier to work with.
- An **empty list** `[]` has no items. It is useful as a starting point that you fill later.

### 3.3 The type of a list

```python
temps = [44, 46, 48]
print(type(temps))
```

```text
<class 'list'>
```

### 3.4 Lists can contain variables and expressions

The items are evaluated when the list is created:

```python
price = 2
qty = 3
order = [price, qty, price * qty]
print(order)
```

```text
[2, 3, 6]
```

### 3.5 Long lists can use several lines

Inside square brackets, you may continue on the next line. This keeps long lists readable:

```python
gcc = ["Kuwait", "Saudi Arabia", "UAE",
       "Qatar", "Bahrain", "Oman"]
print(gcc)
```

```text
['Kuwait', 'Saudi Arabia', 'UAE', 'Qatar', 'Bahrain', 'Oman']
```

---

## 4. Indexes: Reading Items

### 4.1 Positive indexes

Every item has an **index**. Just like with strings, the first index is **0**:

```python
grades = [85, 92, 78, 95, 70]
```

| Item | 85 | 92 | 78 | 95 | 70 |
|---|---|---|---|---|---|
| Index | 0 | 1 | 2 | 3 | 4 |

To read an item, write the list name followed by the index in square brackets:

```python
grades = [85, 92, 78, 95, 70]
print(grades[0])
print(grades[3])
```

```text
85
95
```

**Why does counting start at 0?** You can think of the index as "how many steps from the beginning". The first item is 0 steps from the beginning, the second is 1 step, and so on. Many programming languages count this way.

Rule of thumb: **the n-th item is at index n − 1.** The 1st item is at index 0, the 5th item is at index 4.

### 4.2 Using items like variables

An expression like `grades[2]` can be used anywhere a value can be used: in arithmetic, in `print()`, in conditions, and in other expressions.

```python
prices = [2.5, 1.25, 4]
total = prices[0] + prices[1]
print("Total:", total, "KD")
if prices[2] > 3:
    print("The third dish is expensive")
```

```text
Total: 3.75 KD
The third dish is expensive
```

```python
names = ["Ali", "Mona", "Sara"]
print(names[2] + " and " + names[0])
print("Length of the first name:", len(names[0]))
```

```text
Sara and Ali
Length of the first name: 3
```

In the last line, `names[0]` is the string `"Ali"`, so `len(names[0])` is the length of that **string** (3 characters).

The index can also be a **variable** or an **expression**:

```python
days = ["Sun", "Mon", "Tue", "Wed", "Thu"]
i = 2
print(days[i])
print(days[i + 1])
```

```text
Tue
Wed
```

### 4.3 Negative indexes

You can also count from the **end** of a list. The last item has index −1, the one before it −2, and so on:

| Item | 85 | 92 | 78 | 95 | 70 |
|---|---|---|---|---|---|
| Positive index | 0 | 1 | 2 | 3 | 4 |
| Negative index | −5 | −4 | −3 | −2 | −1 |

```python
grades = [85, 92, 78, 95, 70]
print(grades[-1])
print(grades[-2])
print(grades[-5])
```

```text
70
95
85
```

Negative indexes are very useful because `lst[-1]` is **always** the last item, no matter how long the list is. You do not need to know the length.

---

## 5. The Length of a List: len()

### 5.1 Counting items

`len()` gives the number of **items** in a list:

```python
gcc = ["Kuwait", "Saudi Arabia", "UAE",
       "Qatar", "Bahrain", "Oman"]
print(len(gcc))
print(len([]))
print(len(["Saudi Arabia"]))
```

```text
6
0
1
```

Important: `len()` counts **items**, not characters. `"Saudi Arabia"` is one item, even though the string has 12 characters.

### 5.2 Finding the last index

Because indexes start at 0, the **last** index is always one less than the length:

```text
last index = len(lst) - 1
```

```python
gcc = ["Kuwait", "Saudi Arabia", "UAE",
       "Qatar", "Bahrain", "Oman"]
print(gcc[len(gcc) - 1])
print(gcc[-1])
```

```text
Oman
Oman
```

Both lines print the last item. `gcc[-1]` is shorter and is preferred.

### 5.3 Finding the middle item

For a list with an **odd** number of items, the middle index is `len(lst) // 2` (`//` is integer division):

```python
temps = [44, 46, 48, 45, 47, 49, 43]
middle = len(temps) // 2
print(middle)
print(temps[middle])
```

```text
3
45
```

With 7 items, `7 // 2` is 3, and index 3 is the 4th item — exactly the middle (3 items before it, 3 after it).

---

## 6. IndexError: Index Out of Range

### 6.1 What causes it

If you use an index that does not exist, Python stops the program with an **IndexError**:

```text
cities = ["Kuwait", "Doha", "Muscat"]
print(cities[3])

IndexError: list index out of range
```

There are 3 items, so the valid positive indexes are 0, 1, and 2. Index 3 would be the **fourth** item, which does not exist.

The same happens with negative indexes that go too far: `cities[-4]` is also an error, because the valid negative indexes are −1, −2, and −3.

### 6.2 Valid indexes

| List length | Valid positive indexes | Valid negative indexes |
|---|---|---|
| 3 | 0, 1, 2 | −1, −2, −3 |
| n | 0 to n − 1 | −1 to −n |
| 0 (empty) | none | none |

An **empty list** has no valid indexes at all. `[][0]` is an `IndexError`.

### 6.3 Checking before you read

You can use `len()` with an `if` statement to make sure an index is valid:

```python
cities = ["Kuwait", "Doha", "Muscat"]
i = 5
if i < len(cities):
    print(cities[i])
else:
    print("There is no item at index", i)
```

```text
There is no item at index 5
```

---

## 7. Changing Items

### 7.1 Syntax

To change an item, put the index on the **left** side of `=`:

```text
lst[index] = new_value
```

```python
grades = [85, 92, 78]
grades[2] = 81
print(grades)
```

```text
[85, 92, 81]
```

The item at index 2 was **replaced**. The other items, and the length of the list, did not change.

### 7.2 Using the old value

The right side of `=` is calculated **first**, so you can use the old value to make the new one:

```python
grades = [85, 92, 78]
grades[0] = grades[0] + 5
print(grades)
```

```text
[90, 92, 78]
```

Step by step:

1. Python reads `grades[0]`, which is 85.
2. It calculates 85 + 5 = 90.
3. It stores 90 at index 0.

### 7.3 You can only replace items that already exist

Assigning to an index that does not exist is an error. It does **not** add a new item:

```text
grades = [85, 92, 78]
grades[3] = 60

IndexError: list assignment index out of range
```

Adding new items to a list is done with **list methods**, which you will learn in the next lecture.

### 7.4 Swapping two items

To exchange two items, you need a **temporary variable**:

```python
race = ["Fahad", "Ali", "Noor"]
temp = race[0]
race[0] = race[1]
race[1] = temp
print(race)
```

```text
['Ali', 'Fahad', 'Noor']
```

| Step | Code | `temp` | `race` |
|---|---|---|---|
| start | | — | Fahad, Ali, Noor |
| 1 | `temp = race[0]` | Fahad | Fahad, Ali, Noor |
| 2 | `race[0] = race[1]` | Fahad | Ali, Ali, Noor |
| 3 | `race[1] = temp` | Fahad | Ali, Fahad, Noor |

Why is `temp` needed? After step 2, the value `"Fahad"` is no longer in the list. If we had not saved it in `temp`, it would be lost.

---

## 8. Lists Are Mutable; Strings Are Immutable

### 8.1 What lists and strings have in common

You already know strings well, and lists behave like them in many ways:

| Feature | String | List |
|---|---|---|
| Contains | characters | any values |
| Index starts at 0 | ✔ | ✔ |
| Negative indexes | ✔ | ✔ |
| `len()` | number of characters | number of items |
| `in` / `not in` | ✔ | ✔ |
| Can change one item? | **✘ No** | **✔ Yes** |

### 8.2 The big difference

A **list** is **mutable**: you can change its items after it is created.

```python
letters = ["c", "a", "t"]
letters[0] = "b"
print(letters)
```

```text
['b', 'a', 't']
```

A **string** is **immutable**: you cannot change its characters.

```text
word = "cat"
word[0] = "b"

TypeError: 'str' object does not support item assignment
```

To get a different string, you must create a **new** string, for example `word = "b" + "at"`.

This difference is the main reason lists exist: they let you keep a collection of values and update them over time — like correcting a grade or updating a price.

---

## 9. Membership: in and not in

### 9.1 Checking for an item

`x in lst` is `True` if **some item** in the list is **equal** to `x`. `x not in lst` is the opposite.

```python
gcc = ["Kuwait", "Qatar", "Oman"]
print("Qatar" in gcc)
print("Egypt" in gcc)
print("Egypt" not in gcc)
```

```text
True
False
True
```

The result is a Boolean (`True` or `False`), so you can use it directly in an `if` statement.

### 9.2 The match must be exact

`in` checks for **equality**. Two values must be exactly the same, including uppercase/lowercase and type:

```python
gcc = ["Kuwait", "Qatar", "Oman"]
print("kuwait" in gcc)
ids = ["101", "102"]
print(102 in ids)
print("102" in ids)
```

```text
False
False
True
```

- `"kuwait"` (lowercase k) is not equal to `"Kuwait"`.
- `102` (a number) is not equal to `"102"` (a string).

### 9.3 `in` with strings versus `in` with lists

With a **string**, `in` finds any **part** of the string. With a **list**, `in` compares **whole items**:

```python
print("wa" in "Kuwait")
print("wa" in ["Kuwait"])
print("Kuwait" in ["Kuwait"])
```

```text
True
False
True
```

---

## 10. Lists with if Statements

Membership tests and item values work naturally with `if`, `elif`, and `else`.

### 10.1 Course registration

```python
offered = ["CS126", "MATH101", "ENG110"]
full = ["MATH101"]
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

1. `"MATH101" not in offered` → `False` (it is offered), so skip the first block.
2. `"MATH101" in full` → `True`, so print that the course is full.
3. The `else` is skipped.

With `course = "CS126"`, the output would be `Registered in CS126`. With `course = "PHYS101"`, it would be `PHYS101 is not offered`.

### 10.2 Combining with and / or

```python
admins = ["dr.fawaz", "dr.huda"]
students = ["sara", "ali", "mona"]
blocked = ["ali"]
user = "ali"
if user in admins:
    print("Welcome, administrator")
elif user in students and user not in blocked:
    print("Welcome, student")
else:
    print("Access denied")
```

```text
Access denied
```

`"ali" in students` is `True`, but `"ali" not in blocked` is `False`, so the `and` gives `False`, and the `else` runs.

A nice feature of this design: to block or unblock a student, you only change the **list**. The `if` statement stays the same.

### 10.3 Comparing items

```python
temps = [41, 44, 47]
if temps[-1] > temps[0]:
    print("It got warmer")
else:
    print("It did not get warmer")
```

```text
It got warmer
```

---

## 11. Comparing Lists: == and !=

Two lists are **equal** when they have the **same items** in the **same order**:

```python
a = [1, 2, 3]
b = [1, 2, 3]
c = [3, 2, 1]
print(a == b)
print(a == c)
print(a != c)
print([] == [])
print([1, 2] == [1, 2, 3])
```

```text
True
False
True
True
False
```

- `a == c` is `False` because the order is different.
- `[1, 2] == [1, 2, 3]` is `False` because the lengths differ.

Example: checking answers.

```python
answers = ["A", "C", "B"]
key = ["A", "C", "D"]
if answers == key:
    print("All correct!")
else:
    print("Some answers are wrong")
print("Question 1 correct:", answers[0] == key[0])
print("Question 3 correct:", answers[2] == key[2])
```

```text
Some answers are wrong
Question 1 correct: True
Question 3 correct: False
```

---

## 12. Nested Lists

### 12.1 A list inside a list

A list item can itself be a list. This is called a **nested list**. It is useful for data that looks like a **table**:

```python
students = [["Ali", 80], ["Mona", 95], ["Sara", 72]]
print(len(students))
print(students[1])
```

```text
3
['Mona', 95]
```

`students` has **3** items, and each item is a small list `[name, mark]`.

|  | [0] name | [1] mark |
|---|---|---|
| **[0]** | "Ali" | 80 |
| **[1]** | "Mona" | 95 |
| **[2]** | "Sara" | 72 |

### 12.2 Two indexes

To reach a value inside an inner list, use **two** indexes:

```text
lst[row][column]
```

```python
students = [["Ali", 80], ["Mona", 95], ["Sara", 72]]
print(students[1][0])
print(students[2][1])
print(students[-1][0])
```

```text
Mona
72
Sara
```

How Python reads `students[1][0]`:

1. `students[1]` → `["Mona", 95]`
2. `["Mona", 95][0]` → `"Mona"`

### 12.3 Changing an item in a nested list

```python
students = [["Ali", 80], ["Mona", 95], ["Sara", 72]]
students[0][1] = 85
print(students)
```

```text
[['Ali', 85], ['Mona', 95], ['Sara', 72]]
```

### 12.4 Inner lists can have different lengths

```python
x = [[1, 2], [3, 4, 5]]
print(len(x), len(x[0]), len(x[1]))
print(x[-1][-1])
```

```text
2 2 3
5
```

---

## 13. Two Names for One List

### 13.1 What happens with `b = a`

When you write `b = a` with a list, Python does **not** make a copy. It makes `b` **another name** for the **same** list:

```python
a = [1, 2, 3]
b = a
b[0] = 99
print(a)
print(b)
```

```text
[99, 2, 3]
[99, 2, 3]
```

There is only **one** list in memory, and both `a` and `b` refer to it. A change made through `b` is visible through `a`, and the other way round.

### 13.2 Why this did not happen with numbers and strings

With numbers and strings, you never noticed this, because they cannot be changed in place. For example:

```python
x = 5
y = x
y = 10
print(x, y)
```

```text
5 10
```

`y = 10` does not change the value 5; it simply makes `y` refer to a new value. With a list, `b[0] = 99` changes the list **itself**, so every name for that list sees the change.

### 13.3 Creating a separate list

If you write the list out again, you get a **separate** list:

```python
a = [1, 2, 3]
b = [1, 2, 3]
b[0] = 99
print(a)
print(b)
print(a == b)
```

```text
[1, 2, 3]
[99, 2, 3]
False
```

In the next lecture, you will learn a short way to make a copy of any list.

---

## 14. Worked Examples

### 14.1 A student record

```python
student = ["Sara", 20, "CS", 3.4]
print("Name:", student[0])
print("Major:", student[2])
student[3] = 3.6
if student[3] >= 3.5:
    print(student[0], "is on the honor list")
print(student)
```

```text
Name: Sara
Major: CS
Sara is on the honor list
['Sara', 20, 'CS', 3.6]
```

In this list, each **position** has a meaning: index 0 is the name, 1 the age, 2 the major, 3 the GPA. The program depends on this order, so it must never change.

### 14.2 Weekly temperatures

```python
temps = [44, 46, 48, 45, 47, 94, 43]
temps[5] = 49
first = temps[0]
last = temps[-1]
middle = temps[len(temps) // 2]
print("Sunday:", first, "Saturday:", last)
print("Wednesday:", middle)
if last < first:
    print("The week ended cooler")
else:
    print("The week ended warmer or the same")
```

```text
Sunday: 44 Saturday: 43
Wednesday: 45
The week ended cooler
```

1. The reading at index 5 (Friday) was typed wrongly as 94; we replace it with 49.
2. `temps[0]` and `temps[-1]` are the first and last days.
3. `len(temps) // 2` is 3, the middle index (Wednesday).
4. 43 < 44, so the week ended cooler.

### 14.3 Mobile packages

```python
packages = ["Basic", "Plus", "Max"]
prices = [5, 9, 15]
print(packages[-1], prices[-1])
prices[1] = prices[1] + 2
if "Gold" not in packages:
    print("Gold is not available")
print(prices)
```

```text
Max 15
Gold is not available
[5, 11, 15]
```

The two lists are **parallel**: `prices[i]` is the price of `packages[i]`. Using the same index on both lists keeps the name and the price together.

---

## 15. Important Notes

- Lists are written with **square brackets** and **commas**.
- Indexes start at **0**. The last index is `len(lst) - 1`, or simply `-1`.
- `len()` counts **items**, not characters.
- An index that does not exist causes an **IndexError**, both when reading and when assigning.
- `lst[i] = value` **replaces** an existing item; it never adds a new one.
- Lists are **mutable**; strings are **immutable**.
- `in` / `not in` compare **whole items** and need an **exact** match (case and type).
- `==` is `True` only for the same items in the same order.
- `b = a` does **not** copy a list.

---

## 16. Common Mistakes

### Mistake 1: Starting to count at 1

**Incorrect** (goal: the first grade)

```python
grades = [85, 92, 78]
print(grades[1])
```

```text
92
```

**Why?** Index 1 is the **second** item.

**Correct**

```python
grades = [85, 92, 78]
print(grades[0])
```

```text
85
```

### Mistake 2: Using `len()` as the last index

**Incorrect**

```text
grades = [85, 92, 78]
print(grades[len(grades)])

IndexError: list index out of range
```

**Why?** `len(grades)` is 3, but the last index is 2.

**Correct**

```python
grades = [85, 92, 78]
print(grades[len(grades) - 1])
print(grades[-1])
```

```text
78
78
```

### Mistake 3: A missing comma

**Incorrect**

```python
cities = ["Kuwait" "Doha", "Oman"]
print(cities)
print(len(cities))
```

```text
['KuwaitDoha', 'Oman']
2
```

**Why?** When two strings are written next to each other with no comma, Python **joins** them into one string. There is no error message, so this mistake is easy to miss. Always check that every pair of items has a comma between them.

**Correct**

```python
cities = ["Kuwait", "Doha", "Oman"]
print(len(cities))
```

```text
3
```

### Mistake 4: Forgetting quotes around strings

**Incorrect**

```text
cities = [Kuwait, Doha]

NameError: name 'Kuwait' is not defined
```

**Why?** Without quotes, Python thinks `Kuwait` is a variable name.

**Correct:** `cities = ["Kuwait", "Doha"]`

### Mistake 5: Trying to add an item with an index

**Incorrect**

```text
grades = [85, 92, 78]
grades[3] = 60

IndexError: list assignment index out of range
```

**Why?** `lst[i] = x` only replaces an existing item. Adding items uses list methods (next lecture).

### Mistake 6: Searching with the wrong type or case

**Incorrect**

```python
ids = ["101", "102", "103"]
print(102 in ids)
gcc = ["Kuwait", "Qatar"]
print("qatar" in gcc)
```

```text
False
False
```

**Correct**

```python
ids = ["101", "102", "103"]
print("102" in ids)
gcc = ["Kuwait", "Qatar"]
print("Qatar" in gcc)
```

```text
True
True
```

### Mistake 7: Trying to change a string like a list

**Incorrect**

```text
word = "cat"
word[0] = "b"

TypeError: 'str' object does not support item assignment
```

**Correct:** create a new string: `word = "b" + "at"`, or use a list of characters if you need to change items.

### Mistake 8: Expecting `b = a` to copy

**Incorrect** (goal: keep the original prices)

```python
prices = [5, 9, 15]
new_prices = prices
new_prices[0] = 6
print(prices)
```

```text
[6, 9, 15]
```

**Why?** `new_prices` and `prices` are the same list.

**Correct** (for now — write a separate list):

```python
prices = [5, 9, 15]
new_prices = [6, 9, 15]
print(prices)
print(new_prices)
```

```text
[5, 9, 15]
[6, 9, 15]
```

---

## 17. Mini Practice Questions

Try these before looking at the answers at the end of this section.

**Q1.** What does this print?

```python
x = ["a", "b", "c", "d"]
print(x[2], x[-2], len(x))
```

**Q2.** A list has 10 items. What are the first and last valid positive indexes? What are the valid negative indexes?

**Q3.** What does this print?

```python
nums = [4, 7, 1]
nums[2] = nums[0] * nums[1]
print(nums)
```

**Q4.** Which of these lines causes an error, and which error?

```text
A: lst = [1, 2, 3]; print(lst[-3])
B: lst = [1, 2, 3]; print(lst[3])
C: lst = [];        print(len(lst))
```

**Q5.** What does this print?

```python
print([1, 2, 3] == [1, 2, 3], [1, 2, 3] == [3, 2, 1])
```

**Q6.** What does this print?

```python
x = [[1, 2], [3, 4, 5]]
print(len(x), len(x[1]), x[-1][-1])
```

### Answers to Mini Practice

1. **`c c 4`** — index 2 and index −2 are the same item in a list of 4.
2. **0 and 9**; negative indexes **−1 to −10**.
3. **`[4, 7, 28]`** — 4 × 7 = 28 replaces the item at index 2.
4. **B** causes an `IndexError` (index 3 does not exist). A prints `1`; C prints `0`.
5. **`True False`** — order matters.
6. **`2 3 5`**

---

## 18. Ask AI to Help You Understand

```text
Explain Python lists to me as if I have only learned strings and if statements.
Use a list of 5 temperatures in Kuwait. Show positive and negative indexes in a table.
Do not use loops and do not give me exercises yet.
```

```text
Why do Python indexes start at 0? Give me three small examples
and explain how to find the last index of a list.
```

```text
Explain the difference between a list and a string in Python.
Focus on why I can change lst[0] but not word[0]. Use small examples.
```

```text
I wrote b = a and then changed b, and a also changed. Explain why this happens
with lists but not with numbers. Use a simple drawing made of text.
```

```text
Give me five "predict the output" questions about Python list indexing,
len(), and the in operator. Do not use loops or list methods.
Give me hints first and do not show the answers unless I ask.
```

> **Remember:** Always run the code yourself. AI can make mistakes, and running code is the only way to be sure.

---

## 19. Summary

- A **list** stores many values, in order, in one variable: `[item1, item2, ...]`.
- Items can be numbers, strings, Booleans, other lists, or a mix. `[]` is an empty list.
- **Indexes** start at 0. Negative indexes count from the end; `-1` is the last item.
- `len(lst)` is the number of items; valid indexes are `0` to `len(lst) - 1`.
- A missing index causes an **IndexError**.
- `lst[i] = value` **replaces** an existing item. Lists are **mutable**; strings are **immutable**.
- `in` and `not in` test whether a whole item is in the list, with an exact match.
- `==` compares lists item by item, in order.
- A **nested list** uses two indexes: `lst[row][column]`.
- `b = a` gives a second name to the **same** list; it does not copy it.

---

## Basic Exercises

> Exercises 1–12 are the same as in the slides. Exercises 13–16 are extra practice.

**Exercise 1.** Predict the output.

```python
colors = ["red", "green", "blue", "white"]
print(colors[1])
print(colors[-1])
print(len(colors))
```

**Exercise 2.** Predict the output.

```python
nums = [10, 20, 30]
nums[1] = 25
print(nums)
```

**Exercise 3.** This should print the last day. Find and fix the error.

```text
days = ["Sun", "Mon", "Tue"]
print(days[3])
```

**Exercise 4.** Predict the output.

```python
gcc = ["Kuwait", "Qatar", "Oman"]
print("Oman" in gcc)
print("oman" in gcc)
print("Iraq" not in gcc)
```

**Exercise 13.** Print the **middle** item of `cities = ["Riyadh", "Doha", "Kuwait", "Manama", "Muscat"]` using `len()` and `//`, so your code would also work for any other list with an odd number of items.

## Practice Exercises

**Exercise 5.** Create a list of these GCC capitals: Kuwait City, Riyadh, Doha, Abu Dhabi, Manama. Print the first one, the last one (use a **negative** index), and the number of capitals.

**Exercise 6.** Using indexes, print the total and the average of `prices = [1.5, 3, 2.25]`.

**Exercise 7.** For `grades = [70, 85, 90]`: the second grade should be 88, and the first grade gets 5 bonus marks. Change the list, then print it.

**Exercise 8.** Explain what this code does and give its output.

```python
menu = ["tea", "coffee", "juice"]
order = "karak"
if order in menu:
    print("Coming right up")
else:
    print("Sorry, we only have", menu[0],
          "or", menu[1])
```

**Exercise 14.** Write a program that prints `Same` if the first and last items of a list are equal, and `Different` otherwise. Test it with `["Kuwait", "Doha", "Kuwait"]` and with `[3, 5, 7]`.

## Challenge Exercises

**Exercise 9.** Swap the **first** and **last** items. Your code must work for a list of **any** length.

```python
names = ["Ali", "Mona", "Sara", "Fahad"]
```

**Exercise 10.** Print Mona's mark. Then change Ali's mark to 85 and print the whole list.

```python
marks = [["Ali", 80], ["Mona", 95]]
```

**Exercise 11.** Predict the output. Explain why.

```python
a = [1, 2, 3]
b = a
b[0] = 99
print(a)
```

**Exercise 12.** A list holds exactly 3 temperatures. Print `Rising` if each is higher than the one before, `Falling` if each is lower, otherwise `Mixed`. Test with `[41, 44, 47]`.

**Exercise 15.** "Rotate" a 3-item list to the left: the first item moves to the end. For `x = ["a", "b", "c"]`, the result should be `['b', 'c', 'a']`. Create the result as a **new list** built from indexes of `x`.

**Exercise 16.** A tic-tac-toe board is stored as a nested list. Print `X wins` if the three cells on the diagonal from the top-left to the bottom-right are all `"X"`; otherwise print `No winner on this diagonal`.

```python
board = [["X", "O", "X"],
         [" ", "X", "O"],
         ["O", " ", "X"]]
```

---

# Exercise Solutions

### Solution 1

Index 1 is the second item. Index −1 is the last item. The list has 4 items.

```text
green
white
4
```

### Solution 2

Only the item at index 1 is replaced.

```text
[10, 25, 30]
```

### Solution 3

There are 3 items, so the valid indexes are 0, 1, and 2. Index 3 causes an `IndexError`. Use 2 or, better, −1:

```python
days = ["Sun", "Mon", "Tue"]
print(days[-1])
```

```text
Tue
```

### Solution 4

`in` needs an exact match, so `"oman"` (lowercase) is not found.

```text
True
False
True
```

### Solution 5

```python
capitals = ["Kuwait City", "Riyadh", "Doha",
            "Abu Dhabi", "Manama"]
print(capitals[0])
print(capitals[-1])
print(len(capitals))
```

```text
Kuwait City
Manama
5
```

### Solution 6

```python
prices = [1.5, 3, 2.25]
total = prices[0] + prices[1] + prices[2]
print("Total:", total)
print("Average:", total / len(prices))
```

```text
Total: 6.75
Average: 2.25
```

### Solution 7

```python
grades = [70, 85, 90]
grades[1] = 88
grades[0] = grades[0] + 5
print(grades)
```

```text
[75, 88, 90]
```

### Solution 8

The program checks whether the customer's order is an item in the menu. `"karak"` is not in the list, so the `else` block runs and suggests the first two drinks (`menu[0]` and `menu[1]`).

```text
Sorry, we only have tea or coffee
```

### Solution 9

Use index 0 for the first item and −1 for the last, so the code works for any length. A temporary variable keeps the first value safe.

```python
names = ["Ali", "Mona", "Sara", "Fahad"]
temp = names[0]
names[0] = names[-1]
names[-1] = temp
print(names)
```

```text
['Fahad', 'Mona', 'Sara', 'Ali']
```

### Solution 10

The first index chooses the inner list; the second chooses the item inside it.

```python
marks = [["Ali", 80], ["Mona", 95]]
print(marks[1][1])
marks[0][1] = 85
print(marks)
```

```text
95
[['Ali', 85], ['Mona', 95]]
```

### Solution 11

`b = a` does not create a new list. `a` and `b` are two names for the **same** list, so changing `b[0]` also changes what `a` shows.

```text
[99, 2, 3]
```

### Solution 12

```python
t = [41, 44, 47]
if t[1] > t[0] and t[2] > t[1]:
    print("Rising")
elif t[1] < t[0] and t[2] < t[1]:
    print("Falling")
else:
    print("Mixed")
```

```text
Rising
```

Test with `[47, 44, 41]` (prints `Falling`) and `[41, 47, 44]` (prints `Mixed`) to check all three cases.

### Solution 13

```python
cities = ["Riyadh", "Doha", "Kuwait", "Manama", "Muscat"]
middle = len(cities) // 2
print(cities[middle])
```

```text
Kuwait
```

`len(cities)` is 5, and `5 // 2` is 2.

### Solution 14

```python
x = ["Kuwait", "Doha", "Kuwait"]
if x[0] == x[-1]:
    print("Same")
else:
    print("Different")
y = [3, 5, 7]
if y[0] == y[-1]:
    print("Same")
else:
    print("Different")
```

```text
Same
Different
```

### Solution 15

```python
x = ["a", "b", "c"]
rotated = [x[1], x[2], x[0]]
print(rotated)
print(x)
```

```text
['b', 'c', 'a']
['a', 'b', 'c']
```

The new list is built from the items of `x` in a different order. Because `rotated` is a separate list, `x` is not changed.

### Solution 16

```python
board = [["X", "O", "X"],
         [" ", "X", "O"],
         ["O", " ", "X"]]
if board[0][0] == "X" and board[1][1] == "X" and board[2][2] == "X":
    print("X wins")
else:
    print("No winner on this diagonal")
```

```text
X wins
```

The diagonal cells are row 0 column 0, row 1 column 1, and row 2 column 2.

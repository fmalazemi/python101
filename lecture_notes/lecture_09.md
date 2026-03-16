# Lecture 9: Lists and Working with Collections of Data

---

## Table of Contents

1. [Why This Topic Matters](#why-this-topic-matters)
2. [Learning Objectives](#learning-objectives)
3. [Introduction](#introduction)
4. [What Is a List?](#what-is-a-list)
5. [Creating a List](#creating-a-list)
6. [Accessing Elements: Indexing](#accessing-elements-indexing)
7. [Updating Elements](#updating-elements)
8. [Common List Methods](#common-list-methods)
   - [append()](#append)
   - [remove()](#remove)
   - [len()](#len)
9. [Looping Through a List](#looping-through-a-list)
10. [Practical Examples](#practical-examples)
11. [Common Mistakes and Misconceptions](#common-mistakes-and-misconceptions)
12. [Summary](#summary)
13. [Exercises](#exercises)

---

## Why This Topic Matters

In real programs, you rarely work with just one value at a time. A student record system stores dozens of marks. A shopping application manages hundreds of items. A weather program tracks temperatures for every day of the year.

Storing each of these values in a separate variable would be impractical and inefficient. Python's **list** solves this problem by allowing you to store multiple values in a single, organised structure.

Lists are one of the most frequently used tools in Python programming. Mastering them is essential for writing useful, real-world programs.

---

## Learning Objectives

By the end of this lecture, you will be able to:

- Explain what a list is and why it is useful
- Create a list and access its elements using indexing
- Update, add, and remove elements from a list
- Use the built-in functions `len()`, `append()`, and `remove()`
- Write a loop that processes every element in a list

---

## Introduction

So far in this course, each variable has held exactly one value at a time — one number, one string, one result. This works well for simple problems, but many real tasks involve a **collection** of related values.

Consider the following scenario: you want to store the exam marks of five students. Using separate variables, you would write:

```python
mark1 = 78
mark2 = 85
mark3 = 90
mark4 = 62
mark5 = 74
```

This is inconvenient. What if there were fifty students? What if you needed to calculate the average? You would have to write each variable name individually every time.

A **list** solves this problem elegantly. It allows you to store all five marks — or fifty — in a single variable, and work with them efficiently.

---

## What Is a List?

A **list** is an ordered collection of values stored in a single variable. Each value in the list is called an **element** (also called an **item**).

### Analogy: A Shelf with Numbered Positions

Imagine a shelf with several numbered slots. Each slot holds one object — a book, a box, or any item. The shelf itself has one name, but each position on the shelf is identified by a number.

```
Shelf: "marks"
 ┌──────┬──────┬──────┬──────┬──────┐
 │  78  │  85  │  90  │  62  │  74  │
 └──────┴──────┴──────┴──────┴──────┘
   [0]    [1]    [2]    [3]    [4]
```

- The shelf is the **list**.
- Each slot is an **element**.
- The number above each slot is its **index** — its position in the list.

> **Key point:** In Python, list positions start at **0**, not 1. The first element is at index `0`, the second at index `1`, and so on.

---

## Creating a List

To create a list in Python, write the values separated by commas, enclosed in **square brackets** `[ ]`.

**Syntax:**

```python
list_name = [value1, value2, value3, ...]
```

### Example 1: A List of Marks

```python
marks = [78, 85, 90, 62, 74]
print(marks)
```

**Output:**
```
[78, 85, 90, 62, 74]
```

**Explanation:** The variable `marks` now holds five integer values. When you print the list, Python displays all elements enclosed in square brackets.

---

### Example 2: A List of Names

```python
students = ["Ali", "Sara", "Omar", "Lena", "Yousef"]
print(students)
```

**Output:**
```
['Ali', 'Sara', 'Omar', 'Lena', 'Yousef']
```

**Explanation:** A list can contain strings. Notice that each string is enclosed in quotation marks, just as with regular string variables.

---

### Example 3: A List of Shopping Items

```python
shopping = ["milk", "bread", "eggs", "butter"]
print(shopping)
```

**Output:**
```
['milk', 'bread', 'eggs', 'butter']
```

> **Note:** A list can also be empty. An **empty list** is written as `[]`. You will often create an empty list and add items to it later.

```python
cart = []
print(cart)
```

**Output:**
```
[]
```

### Try It Yourself

Create a list called `cities` containing the names of three cities you know. Print the list.

---

## Accessing Elements: Indexing

To access a single element from a list, write the list name followed by the element's **index** in square brackets.

**Syntax:**

```python
list_name[index]
```

### Example 4: Accessing Elements by Index

```python
marks = [78, 85, 90, 62, 74]

print(marks[0])   # First element
print(marks[1])   # Second element
print(marks[4])   # Fifth (last) element
```

**Output:**
```
78
85
74
```

**Explanation:** `marks[0]` retrieves the value at position 0, which is `78`. `marks[4]` retrieves the value at position 4, which is `74`.

---

### Negative Indexing

Python also allows **negative indexing**, which counts from the end of the list. The last element has index `-1`, the second-to-last has index `-2`, and so on.

```python
marks = [78, 85, 90, 62, 74]

print(marks[-1])   # Last element
print(marks[-2])   # Second-to-last element
```

**Output:**
```
74
62
```

**Explanation:** Negative indexing is useful when you want to access elements from the end of the list without knowing the total number of elements.

### Index Reference Table

| Index (positive) | Index (negative) | Value |
|:-----------------:|:-----------------:|:-----:|
| 0                 | -5                | 78    |
| 1                 | -4                | 85    |
| 2                 | -3                | 90    |
| 3                 | -2                | 62    |
| 4                 | -1                | 74    |

### Try It Yourself

Using the `students` list from Example 2, print the name of the first student and the last student using both positive and negative indexing.

---

## Updating Elements

You can change the value of an element by assigning a new value to a specific index.

**Syntax:**

```python
list_name[index] = new_value
```

### Example 5: Updating an Element

```python
marks = [78, 85, 90, 62, 74]
print("Before:", marks)

marks[3] = 70   # Change the fourth element from 62 to 70
print("After:", marks)
```

**Output:**
```
Before: [78, 85, 90, 62, 74]
After: [78, 85, 90, 70, 74]
```

**Explanation:** The element at index `3` (which was `62`) has been replaced by `70`. All other elements remain unchanged.

### Try It Yourself

Create a list called `prices` with three values. Change the second price to a different value and print the updated list.

---

## Common List Methods

A **method** is a built-in action that belongs to a specific type of object. Lists have several useful methods. You call a method using the format:

```python
list_name.method_name(argument)
```

---

### `append()`

The `append()` method adds a new element to the **end** of a list.

**Syntax:**

```python
list_name.append(new_value)
```

#### Example 6: Adding an Element with append()

```python
shopping = ["milk", "bread", "eggs"]
print("Before:", shopping)

shopping.append("butter")
print("After:", shopping)
```

**Output:**
```
Before: ['milk', 'bread', 'eggs']
After: ['milk', 'bread', 'eggs', 'butter']
```

**Explanation:** The string `"butter"` is added to the end of the `shopping` list. The original elements are not affected.

#### Try It Yourself

Start with an empty list called `fruits`. Use `append()` to add three fruit names to it, one at a time. Print the list after each addition.

---

### `remove()`

The `remove()` method removes the **first occurrence** of a specified value from the list.

**Syntax:**

```python
list_name.remove(value)
```

#### Example 7: Removing an Element with remove()

```python
shopping = ["milk", "bread", "eggs", "butter"]
print("Before:", shopping)

shopping.remove("bread")
print("After:", shopping)
```

**Output:**
```
Before: ['milk', 'bread', 'eggs', 'butter']
After: ['milk', 'eggs', 'butter']
```

**Explanation:** The element `"bread"` is found and removed. The remaining elements shift to fill the empty position.

> **Important:** If the value does not exist in the list, Python will raise a `ValueError`. Always be certain the value exists before calling `remove()`, or handle the error appropriately.

#### Try It Yourself

Create a list of five numbers. Remove one of the numbers using `remove()` and print the result.

---

### `len()`

The `len()` function returns the **number of elements** in a list. It is not a method of the list itself but a built-in Python function that works with lists (and other types).

**Syntax:**

```python
len(list_name)
```

#### Example 8: Finding the Length of a List

```python
marks = [78, 85, 90, 62, 74]
total_students = len(marks)
print("Number of students:", total_students)
```

**Output:**
```
Number of students: 5
```

**Explanation:** `len(marks)` counts the elements in the list and returns the integer `5`. This value is stored in `total_students` and then printed.

#### Try It Yourself

Create a list of your five favourite foods. Use `len()` to print how many items are in the list.

---

## Looping Through a List

One of the most powerful features of lists is the ability to **loop through** all elements automatically. You use a `for` loop to visit each element one by one.

**Syntax:**

```python
for item in list_name:
    # do something with item
```

The variable `item` (you may name it anything) takes the value of each element in the list, one at a time, from first to last.

---

### Example 9: Printing All Elements

```python
students = ["Ali", "Sara", "Omar", "Lena", "Yousef"]

for student in students:
    print(student)
```

**Output:**
```
Ali
Sara
Omar
Lena
Yousef
```

**Explanation:** The loop visits each name in the `students` list. On each iteration, the variable `student` holds the current name, which is then printed.

---

### Example 10: Summing a List of Numbers

```python
marks = [78, 85, 90, 62, 74]
total = 0

for mark in marks:
    total = total + mark

print("Total marks:", total)
```

**Output:**
```
Total marks: 389
```

**Explanation:** The variable `total` starts at `0`. On each iteration, the current mark is added to `total`. After the loop completes, `total` holds the sum of all marks.

---

### Example 11: Calculating the Average

```python
marks = [78, 85, 90, 62, 74]
total = 0

for mark in marks:
    total = total + mark

average = total / len(marks)
print("Average mark:", average)
```

**Output:**
```
Average mark: 77.8
```

**Explanation:** After summing all marks, the total is divided by the number of students (obtained using `len(marks)`). This gives the average mark.

### Try It Yourself

Create a list of five temperatures (as numbers). Write a loop that prints each temperature. Then calculate and print the average temperature.

---

## Practical Examples

### Example 12: Printing a Numbered Shopping List

```python
shopping = ["milk", "bread", "eggs", "butter"]

for i in range(len(shopping)):
    print(i + 1, "-", shopping[i])
```

**Output:**
```
1 - milk
2 - bread
3 - eggs
4 - butter
```

**Explanation:** `range(len(shopping))` generates the numbers `0, 1, 2, 3`. On each iteration, `i` holds the current index. `shopping[i]` retrieves the element at that index. `i + 1` is used for display so the list starts at 1 rather than 0.

---

### Example 13: Finding the Highest Mark

```python
marks = [78, 85, 90, 62, 74]
highest = marks[0]   # Assume the first mark is the highest

for mark in marks:
    if mark > highest:
        highest = mark

print("Highest mark:", highest)
```

**Output:**
```
Highest mark: 90
```

**Explanation:** The variable `highest` is initialised with the first element. The loop then compares each mark to `highest`. If a mark is greater, it becomes the new `highest`. After all elements are checked, `highest` holds the maximum value.

### Try It Yourself

Modify the example above to find the **lowest** mark in the list instead.

---

## Common Mistakes and Misconceptions

### Mistake 1: Using an Index That Is Out of Range

Python lists are zero-indexed, and valid indices range from `0` to `len(list) - 1`. Using an index outside this range causes an `IndexError`.

**Wrong:**
```python
marks = [78, 85, 90]
print(marks[3])   # Index 3 does not exist
```

**Error:**
```
IndexError: list index out of range
```

**Correct:**
```python
marks = [78, 85, 90]
print(marks[2])   # Last valid index is 2
```

**Explanation:** A list with 3 elements has valid indices `0`, `1`, and `2`. Index `3` does not exist.

---

### Mistake 2: Forgetting That Indexing Starts at 0

Many beginners expect the first element to be at index `1`.

**Wrong assumption:**
```python
students = ["Ali", "Sara", "Omar"]
print(students[1])   # Expecting "Ali", but gets "Sara"
```

**Output:**
```
Sara
```

**Correct:**
```python
students = ["Ali", "Sara", "Omar"]
print(students[0])   # Correct: "Ali" is at index 0
```

---

### Mistake 3: Using remove() with a Value That Does Not Exist

If the specified value is not in the list, `remove()` raises a `ValueError`.

**Wrong:**
```python
shopping = ["milk", "bread", "eggs"]
shopping.remove("butter")   # "butter" is not in the list
```

**Error:**
```
ValueError: list.remove(x): x not in list
```

**Correct approach:** Check if the item exists before removing it.
```python
shopping = ["milk", "bread", "eggs"]
item = "butter"

if item in shopping:
    shopping.remove(item)
else:
    print(item, "is not in the list.")
```

---

### Mistake 4: Modifying a List While Iterating Over It

Changing the size of a list (by adding or removing elements) while looping through it can lead to unexpected behaviour or errors.

**Problematic:**
```python
numbers = [1, 2, 3, 4, 5]
for number in numbers:
    if number == 3:
        numbers.remove(number)   # Avoid this
```

**Better approach:** Loop over a copy of the list, or collect items to remove and process them after the loop.

---

### Mistake 5: Confusing len() with the Last Index

`len()` returns the total count of elements. The last valid index is always `len(list) - 1`.

**Wrong:**
```python
marks = [78, 85, 90]
print(marks[len(marks)])   # This is index 3, which does not exist
```

**Error:**
```
IndexError: list index out of range
```

**Correct:**
```python
marks = [78, 85, 90]
print(marks[len(marks) - 1])   # Correct: last element
# Or, more simply:
print(marks[-1])
```

---

## Summary

A **list** is an ordered, mutable collection of elements stored in a single variable.

| Operation             | Syntax                          | Description                              |
|-----------------------|---------------------------------|------------------------------------------|
| Create a list         | `x = [1, 2, 3]`                 | Stores multiple values in one variable   |
| Access an element     | `x[0]`                          | Retrieves the element at index 0         |
| Update an element     | `x[1] = 10`                     | Replaces the element at index 1          |
| Add an element        | `x.append(value)`               | Adds a value to the end of the list      |
| Remove an element     | `x.remove(value)`               | Removes the first occurrence of a value  |
| Count elements        | `len(x)`                        | Returns the number of elements           |
| Loop through a list   | `for item in x:`                | Visits each element one by one           |

**Key points to remember:**

1. List indices start at `0`.
2. The last valid index is `len(list) - 1`, or equivalently `-1`.
3. `append()` adds to the end; `remove()` removes by value.
4. A `for` loop is the standard way to process all elements in a list.
5. Accessing an index that does not exist causes an `IndexError`.

---

## Exercises

### Part A — Understanding Questions

**A1.** What is the index of the first element in any Python list? What is the index of the last element in a list that contains six elements?

**A2.** What is the difference between `append()` and `remove()`? When would you use each one?

**A3.** What error does Python raise when you try to access an index that does not exist in a list? Write an example that would cause this error.

**A4.** What does `len()` return for an empty list `[]`?

---

### Part B — Code Tracing

**B1.** What is the output of the following code? Trace through it step by step before running it.

```python
colours = ["red", "green", "blue", "yellow"]
print(colours[0])
print(colours[-1])
print(len(colours))
colours[1] = "purple"
print(colours)
```

**B2.** What is the output of the following code?

```python
numbers = [10, 20, 30, 40, 50]
total = 0
for n in numbers:
    total = total + n
print(total)
```

**B3.** What is the output of the following code? What change does each line make to the list?

```python
items = ["pen", "notebook", "ruler"]
items.append("eraser")
items.remove("notebook")
print(items)
print(len(items))
```

---

### Part C — Code Writing

**C1.** Write a program that:
- Creates a list of five student names
- Prints each name on a separate line using a `for` loop

**C2.** Write a program that:
- Creates a list of six numbers
- Calculates and prints the sum of all the numbers
- Calculates and prints the average

**C3.** Write a program that:
- Starts with an empty list called `groceries`
- Asks the user to enter three items using `input()`
- Appends each item to the list
- Prints the final list

**C4.** Write a program that:
- Creates a list of five marks (integers)
- Prints each mark with its position number (starting from 1), formatted as:
  ```
  Student 1: 78
  Student 2: 85
  ...
  ```

---

### Part D — Code Modification

**D1.** The following program is intended to print only the marks that are greater than or equal to 80. It currently prints all marks. Modify it to meet the requirement.

```python
marks = [78, 85, 90, 62, 74, 88, 55, 91]

for mark in marks:
    print(mark)
```

**D2.** The following program calculates the sum of a list of numbers. Modify it so that it also prints the **largest** number in the list, without using any built-in functions other than `len()` and `print()`.

```python
numbers = [15, 42, 8, 73, 26, 61]
total = 0

for n in numbers:
    total = total + n

print("Sum:", total)
```

**D3.** The following program creates a shopping list and prints it. Modify it to:
1. Remove `"eggs"` from the list
2. Add `"cheese"` to the list
3. Print the updated list and its length

```python
shopping = ["milk", "bread", "eggs", "butter"]
print(shopping)
```

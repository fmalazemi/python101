# Python List Cheat Sheet

## Creating a List

```python
L = [10, 20, 30, 40, 50]
```

Lists are:

- Ordered
- Mutable
- Indexed starting from `0`

```text
Value:   10   20   30   40   50
Index:    0    1    2    3    4
Index:   -5   -4   -3   -2   -1
```

---

# Accessing Elements

```python
L[0]       # 10
L[2]       # 30
L[-1]      # 50
L[-2]      # 40
```

---

# Slicing

General form:

```python
L[start : stop : step]
```

The `stop` position is **not included**.

```python
L = [10, 20, 30, 40, 50, 60]
```

### Basic slicing

```python
L[1:4]
# [20, 30, 40]
```

```python
L[:3]
# [10, 20, 30]
```

```python
L[3:]
# [40, 50, 60]
```

```python
L[:]
# [10, 20, 30, 40, 50, 60]
```

---

## Slicing with Steps

```python
L[::2]
# [10, 30, 50]
```

```python
L[1::2]
# [20, 40, 60]
```

```python
L[::3]
# [10, 40]
```

---

## Negative Indexes in Slicing

```python
L[-3:]
# [40, 50, 60]
```

```python
L[:-2]
# [10, 20, 30, 40]
```

```python
L[-4:-1]
# [30, 40, 50]
```

---

# Reverse a List

### Using slicing

```python
L[::-1]
```

Example:

```python
L = [10, 20, 30, 40]

L[::-1]
# [40, 30, 20, 10]
```

This creates a new reversed list.

### Using `reverse()`

```python
L.reverse()
```

Example:

```python
L = [10, 20, 30]

L.reverse()

print(L)
# [30, 20, 10]
```

`reverse()` changes the original list.

---

# `append()`

Adds one element to the end of the list.

```python
L = [10, 20, 30]

L.append(40)

print(L)
# [10, 20, 30, 40]
```

---

# `extend()`

Adds multiple elements to the end of a list.

```python
L = [10, 20]

L.extend([30, 40, 50])

print(L)
# [10, 20, 30, 40, 50]
```

Compare:

```python
L.append([30, 40])
```

produces:

```python
[10, 20, [30, 40]]
```

while:

```python
L.extend([30, 40])
```

produces:

```python
[10, 20, 30, 40]
```

---

# `insert()`

Inserts an element at a specific position.

```python
L.insert(index, value)
```

Example:

```python
L = [10, 20, 40]

L.insert(2, 30)

print(L)
# [10, 20, 30, 40]
```

---

# `remove()`

Removes the **first occurrence** of a value.

```python
L.remove(value)
```

Example:

```python
L = [10, 20, 30, 20]

L.remove(20)

print(L)
# [10, 30, 20]
```

If the value does not exist, Python produces an error.

---

# `pop()`

Removes and returns an element.

```python
L.pop()
```

removes the last element.

Example:

```python
L = [10, 20, 30]

x = L.pop()

print(x)
# 30

print(L)
# [10, 20]
```

You can also specify an index:

```python
L.pop(1)
```

---

# `index()`

Returns the index of the first occurrence of a value.

```python
L.index(value)
```

Example:

```python
L = [10, 20, 30, 20]

L.index(20)
# 1
```

If the value does not exist, Python produces an error.

---

# `max()`

Returns the largest element.

```python
L = [40, 10, 80, 20]

max(L)
# 80
```

---

# `min()`

Returns the smallest element.

```python
L = [40, 10, 80, 20]

min(L)
# 10
```

---

# `sum()`

Returns the sum of the elements.

```python
L = [10, 20, 30]

sum(L)
# 60
```

---

# `len()`

Returns the number of elements.

```python
L = [10, 20, 30, 40]

len(L)
# 4
```

---

# Checking if an Element Exists

Use `in`:

```python
L = [10, 20, 30]

20 in L
# True
```

```python
50 in L
# False
```

Use `not in`:

```python
50 not in L
# True
```

---

# Changing an Element

```python
L = [10, 20, 30]

L[1] = 100

print(L)
# [10, 100, 30]
```

---

# String `find()` and `rfind()`

> `find()` and `rfind()` are **string methods**, not list methods.

```python
S = "hello world"
```

## `find()`

Returns the index of the **first occurrence**.

```python
S.find("o")
# 4
```

Example:

```python
S = "banana"

S.find("a")
# 1
```

If the text is not found:

```python
S.find("x")
# -1
```

---

## `rfind()`

Returns the index of the **last occurrence**.

```python
S = "banana"

S.rfind("a")
# 5
```

If the text is not found:

```python
S.rfind("x")
# -1
```

---

# `find()` vs `index()`

For strings:

```python
S = "hello"
```

```python
S.find("x")
# -1
```

but:

```python
S.index("x")
```

produces an error.

---

# Quick Reference Table

| Operation | Example | Purpose |
|---|---|---|
| Access | `L[2]` | Get one element |
| Negative index | `L[-1]` | Get last element |
| Slice | `L[1:4]` | Get part of a list |
| Step | `L[::2]` | Get every second element |
| Reverse | `L[::-1]` | Create reversed list |
| Reverse original | `L.reverse()` | Reverse list in place |
| Add one | `L.append(10)` | Add one element |
| Add many | `L.extend([10,20])` | Add multiple elements |
| Insert | `L.insert(2,10)` | Insert at an index |
| Remove | `L.remove(10)` | Remove first matching value |
| Pop | `L.pop()` | Remove and return an element |
| Find index | `L.index(10)` | Find first matching index |
| Maximum | `max(L)` | Largest value |
| Minimum | `min(L)` | Smallest value |
| Sum | `sum(L)` | Sum of values |
| Length | `len(L)` | Number of elements |
| Membership | `10 in L` | Check if value exists |
| String find | `S.find("x")` | First occurrence |
| String rfind | `S.rfind("x")` | Last occurrence |

---

# Slicing Rule to Remember

```python
L[start : stop : step]
```

For a positive step:

```text
start → → → stop
```

For a negative step:

```text
start ← ← ← stop
```

The `stop` index is always excluded.

Example:

```python
L = [10, 20, 30, 40, 50]
```

```python
L[1:4]
# [20, 30, 40]
```

```python
L[4:1:-1]
# [50, 40, 30]
```

```python
L[::-1]
# [50, 40, 30, 20, 10]
```

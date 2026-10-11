# Python Slicing Exercises

Use the following lists and strings unless a question defines its own data.

```python
L = [10, 20, 30, 40, 50, 60, 70, 80, 90, 100]

S = "KUWAIT"
```

For each question:

1. Predict the output **before running the code**.
2. Then test your answer using Python.
3. Explain why the slice produces that result.

---

## Part 1 — Basic Slicing

### Question 1

What is the output?

```python
print(L[2:5])
```

---

### Question 2

What is the output?

```python
print(L[0:4])
```

---

### Question 3

What is the output?

```python
print(L[5:8])
```

---

### Question 4

What is the output?

```python
print(L[:4])
```

---

### Question 5

What is the output?

```python
print(L[6:])
```

---

### Question 6

What is the output?

```python
print(L[:])
```

What is special about this slice?

---

## Part 2 — Understanding the Stop Position

### Question 7

What is the output?

```python
print(L[2:3])
```

---

### Question 8

What is the output?

```python
print(L[2:2])
```

Explain why.

---

### Question 9

What is the output?

```python
print(L[4:1])
```

Why does Python produce this result?

---

### Question 10

What is the output?

```python
print(L[8:20])
```

Does Python produce an error because index `20` does not exist?

---

## Part 3 — Using Steps

### Question 11

What is the output?

```python
print(L[1:8:2])
```

---

### Question 12

What is the output?

```python
print(L[0:10:3])
```

---

### Question 13

What is the output?

```python
print(L[::2])
```

---

### Question 14

What is the output?

```python
print(L[1::2])
```

---

### Question 15

What is the output?

```python
print(L[::3])
```

---

## Part 4 — Negative Indexes

### Question 16

What is the output?

```python
print(L[-3:])
```

---

### Question 17

What is the output?

```python
print(L[:-3])
```

---

### Question 18

What is the output?

```python
print(L[-5:-2])
```

---

### Question 19

What is the output?

```python
print(L[-8:-3:2])
```

---

### Question 20

What is the output?

```python
print(L[-4:])
```

Rewrite the same slice using positive indexes.

---

## Part 5 — Negative Steps

### Question 21

What is the output?

```python
print(L[::-1])
```

What common operation does this perform?

---

### Question 22

What is the output?

```python
print(L[7:2:-1])
```

---

### Question 23

What is the output?

```python
print(L[8:1:-2])
```

---

### Question 24

What is the output?

```python
print(L[-1:-6:-1])
```

---

### Question 25

What is the output?

```python
print(L[-5:-1:-1])
```

Explain carefully why the result is produced.

---

## Part 6 — Strings and Slicing

Use:

```python
S = "KUWAIT"
```

### Question 26

What is the output?

```python
print(S[1:4])
```

---

### Question 27

What is the output?

```python
print(S[::-1])
```

---

### Question 28

What is the output?

```python
print(S[::2])
```

---

## Part 7 — Write the Slice Yourself

### Question 29

Using only slicing, write an expression that extracts:

```text
[30, 40, 50, 60]
```

from:

```python
L = [10, 20, 30, 40, 50, 60, 70, 80, 90, 100]
```

Your answer should have the form:

```python
L[...]
```

---

### Question 30

Using only slicing, write an expression that produces:

```text
[100, 80, 60, 40, 20]
```

from:

```python
L = [10, 20, 30, 40, 50, 60, 70, 80, 90, 100]
```

Your answer should have the form:

```python
L[...]
```

---

# Challenge Rule

For every slicing expression, try to identify the three components:

```python
  L[start : stop : step]
```

Then ask yourself:

- Where does the slice start?
- Where does it stop?
- Is the stop position included or excluded?
- Which direction does it move?
- How large is each step?

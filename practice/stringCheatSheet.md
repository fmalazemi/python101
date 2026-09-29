# Python Strings Cheat Sheet

A **string** is text stored inside quotation marks. Python uses the type `str` for strings.

## Quick Reference

| Operation | Example | Result |
|---|---|---|
| Create a string | `name = "Sara"` | `Sara` |
| Join strings | `"Hello " + "Sara"` | `Hello Sara` |
| Repeat a string | `"Hi! " * 3` | `Hi! Hi! Hi! ` |
| Find the length | `len("Python")` | `6` |
| Get one character | `"Python"[0]` | `P` |
| Get part of a string | `"Python"[0:3]` | `Pyt` |
| Convert to uppercase | `"hello".upper()` | `HELLO` |
| Convert to lowercase | `"HELLO".lower()` | `hello` |
| Remove outer spaces | `"  hi  ".strip()` | `hi` |
| Replace text | `"cat".replace("c", "h")` | `hat` |
| Check for text | `"Py" in "Python"` | `True` |

---

## 1. Creating Strings

Use single or double quotation marks:

```python
first_name = "Sara"
city = 'Kuwait City'

print(first_name)  # Sara
print(city)        # Kuwait City
```

Both styles create a string:

```python
print(type("Hello"))  # <class 'str'>
print(type('Hello'))  # <class 'str'>
```

Choose quotation marks that make the text easier to write:

```python
message = "I'm learning Python."
quote = 'She said, "Hello!"'

print(message)
print(quote)
```

## 2. Empty Strings

An empty string contains no characters:

```python
message = ""

print(message)       # Prints an empty line
print(len(message))  # 0
```

An empty string is different from a string containing one space:

```python
print(len(""))   # 0
print(len(" "))  # 1
```

---

## 3. Getting String Input

`input()` always returns a string:

```python
name = input("Enter your name: ")
print("Hello, " + name + "!")
```

Even if the user enters digits, the result is still a string:

```python
age = input("Enter your age: ")
print(type(age))  # <class 'str'>
```

Convert the string when you need to perform arithmetic:

```python
age = int(input("Enter your age: "))
print(age + 1)
```

---

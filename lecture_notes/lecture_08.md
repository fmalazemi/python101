# Lecture 8: Working with Strings in Python

---

## Learning Objectives

By the end of this lecture, you will be able to:

- Explain what a string is and how Python stores text data
- Access individual characters in a string using indexing
- Combine strings using concatenation (`+`) and repetition (`*`)
- Use common string methods: `lower()`, `upper()`, `strip()`, `replace()`
- Measure the length of a string using `len()`
- Recognise and correct common mistakes when working with strings

---

## Why This Topic Matters

Almost every real program works with text in some form. A program may ask for a user's name, display a message, read a file, or process a sentence. In Python, text is stored as a **string**. Understanding strings is essential for building useful and interactive programs.

---

## 1. What Is a String?

A **string** is a sequence of characters. A character can be a letter, a digit, a space, or a symbol. In Python, a string is written between quotation marks.

Think of a string as a row of boxes, where each box holds one character. The boxes are arranged in a fixed order, and each box has a number — called an **index** — that tells you its position.

```python
greeting = "Hello"
```

In this example, `"Hello"` is a string. It contains five characters: `H`, `e`, `l`, `l`, `o`.

You can use either single quotes (`'`) or double quotes (`"`) to create a string. Both work the same way.

```python
name = 'Sara'
message = "Welcome to Python!"
```

> **Try it yourself:** Create a variable called `city` and assign it the name of a city. Print it.

---

## 2. String Indexing — Accessing Individual Characters

### 2.1 What Is an Index?

Each character in a string has a position number called an **index**. In Python, counting starts at **zero**, not one. This is called **zero-based indexing**.

**Analogy:** Imagine seats in a row at a cinema. The first seat is seat number 0, the second is seat number 1, and so on.

For the string `"Python"`:

| Index | 0 | 1 | 2 | 3 | 4 | 5 |
|-------|---|---|---|---|---|---|
| Character | P | y | t | h | o | n |

### 2.2 Accessing a Character

To access a single character, write the variable name followed by the index in square brackets.

```python
language = "Python"
print(language[0])   # Output: P
print(language[1])   # Output: y
print(language[5])   # Output: n
```

**Explanation:** `language[0]` retrieves the character at index 0, which is `"P"`. The index is written inside square brackets `[ ]`.

### 2.3 Negative Indexing

Python also allows **negative indices**. A negative index counts from the end of the string. Index `-1` refers to the last character.

```python
word = "Python"
print(word[-1])   # Output: n
print(word[-2])   # Output: o
```

**Explanation:** Negative indexing is useful when you want to access characters at the end of a string without knowing its exact length.

> **Try it yourself:** Create a string with your full name. Print the first character and the last character using both positive and negative indexing.

---

## 3. The `len()` Function

The `len()` function returns the number of characters in a string. This is called the **length** of the string.

```python
name = "Ahmed"
print(len(name))   # Output: 5
```

**Explanation:** `"Ahmed"` has five characters, so `len(name)` returns `5`. Note that spaces are also counted as characters.

```python
sentence = "I love Python"
print(len(sentence))   # Output: 13
```

> **Try it yourself:** Ask the user to enter their name using `input()`. Then print the number of characters in the name.

---

## 4. String Concatenation

**Concatenation** means joining two or more strings together. In Python, you use the `+` operator to concatenate strings.

**Analogy:** Think of concatenation like connecting two pieces of rope. Each piece is a string, and `+` ties them together into one longer string.

```python
first_name = "Sara"
last_name = "Ali"
full_name = first_name + " " + last_name
print(full_name)   # Output: Sara Ali
```

**Explanation:** Three strings are joined: `"Sara"`, `" "` (a space), and `"Ali"`. The result is stored in `full_name`. Without the space, the output would be `"SaraAli"`, which is incorrect.

Another example:

```python
greeting = "Hello, "
name = "Omar"
message = greeting + name + "!"
print(message)   # Output: Hello, Omar!
```

> **Try it yourself:** Ask the user to enter their first name and last name separately. Join them with a space and print the full name.

---

## 5. String Repetition

You can repeat a string a certain number of times using the `*` operator.

```python
line = "-" * 20
print(line)   # Output: --------------------
```

**Explanation:** The string `"-"` is repeated 20 times. This is useful for creating visual separators in output.

Another example:

```python
word = "ha"
laugh = word * 3
print(laugh)   # Output: hahaha
```

> **Try it yourself:** Print the word `"Python"` repeated 5 times on one line.

---

## 6. Common String Methods

A **method** is a built-in action that belongs to a specific data type. String methods perform operations on string values. You call a method by writing the variable name, followed by a dot (`.`), followed by the method name and parentheses.

```python
text = "hello"
print(text.upper())   # Output: HELLO
```

### 6.1 `upper()` and `lower()`

- `upper()` converts all characters in a string to uppercase.
- `lower()` converts all characters in a string to lowercase.

```python
name = "sara"
print(name.upper())   # Output: SARA

title = "INTRODUCTION TO PYTHON"
print(title.lower())   # Output: introduction to python
```

**Explanation:** These methods do not change the original variable. They return a new string with the transformation applied. The original value of `name` remains `"sara"`.

**Common use case:** When comparing user input, it is often useful to convert everything to lowercase so that `"YES"`, `"Yes"`, and `"yes"` are treated as the same.

```python
answer = input("Do you want to continue? ").lower()
print(answer)
```

> **Try it yourself:** Ask the user to enter a sentence. Print it in all uppercase and then in all lowercase.

---

### 6.2 `strip()`

The `strip()` method removes **leading and trailing whitespace** from a string. Whitespace includes spaces, tabs, and newline characters at the beginning and end of a string.

**Analogy:** Think of `strip()` as trimming the extra blank spaces from the left and right edges of a piece of paper.

```python
user_input = "   Ahmed   "
clean_input = user_input.strip()
print(clean_input)          # Output: Ahmed
print(len(user_input))      # Output: 11
print(len(clean_input))     # Output: 5
```

**Explanation:** The original string has spaces before and after `"Ahmed"`. After calling `strip()`, those spaces are removed. This is especially useful when processing input from the user, who may accidentally add extra spaces.

> **Try it yourself:** Ask the user to enter their name. Use `strip()` to clean the input, then print a greeting using the cleaned name.

---

### 6.3 `replace()`

The `replace()` method replaces all occurrences of one substring with another.

**Syntax:**

```python
string.replace(old, new)
```

- `old` is the substring you want to replace.
- `new` is the substring you want to put in its place.

```python
sentence = "I like cats. Cats are great."
new_sentence = sentence.replace("cats", "dogs")
print(new_sentence)   # Output: I like dogs. Cats are great.
```

**Explanation:** Only the first occurrence of `"cats"` (lowercase) was replaced. The word `"Cats"` (with a capital letter) was not changed because `replace()` is case-sensitive. This means uppercase and lowercase letters are treated as different.

Another example:

```python
message = "Hello World"
print(message.replace("World", "Python"))   # Output: Hello Python
```

> **Try it yourself:** Store the sentence `"The sky is grey"` in a variable. Use `replace()` to change `"grey"` to `"blue"` and print the result.

---

## 7. Summary of String Methods

| Method | Description | Example | Result |
|--------|-------------|---------|--------|
| `upper()` | Converts to uppercase | `"hello".upper()` | `"HELLO"` |
| `lower()` | Converts to lowercase | `"HELLO".lower()` | `"hello"` |
| `strip()` | Removes leading/trailing spaces | `"  hi  ".strip()` | `"hi"` |
| `replace(old, new)` | Replaces a substring | `"cat".replace("c","b")` | `"bat"` |
| `len()` | Returns the number of characters | `len("Python")` | `6` |

---

## 8. Common Mistakes and Misconceptions

### Mistake 1: Using a number where a string is expected

```python
age = 20
message = "I am " + age + " years old."   # Error!
```

**Error message:**

```
TypeError: can only concatenate str (not "int") to str
```

**Correction:** Convert the integer to a string using `str()`.

```python
age = 20
message = "I am " + str(age) + " years old."
print(message)   # Output: I am 20 years old.
```

**Explanation:** The `+` operator cannot join a string and an integer directly. You must convert the integer to a string first. Alternatively, you can use an f-string:

```python
message = f"I am {age} years old."
```

---

### Mistake 2: Index out of range

```python
word = "Hi"
print(word[5])   # Error!
```

**Error message:**

```
IndexError: string index out of range
```

**Explanation:** `"Hi"` has only two characters (indices 0 and 1). Index 5 does not exist. Always make sure the index you use is within the valid range.

---

### Mistake 3: Forgetting that strings are immutable

In Python, strings **cannot be changed after they are created**. This is called **immutability**. Methods like `upper()` and `replace()` do not modify the original string — they return a new one.

```python
name = "sara"
name.upper()        # This does NOT change name
print(name)         # Output: sara
```

**Correction:** Assign the result to a variable.

```python
name = "sara"
name = name.upper()
print(name)         # Output: SARA
```

---

### Mistake 4: Mixing up `len()` syntax

`len()` is a function, not a method. It is called with parentheses around the string or variable, not with a dot.

```python
# Wrong
name = "Omar"
print(name.len())   # Error!

# Correct
print(len(name))    # Output: 4
```

---

## 9. Summary

In this lecture, you learned the following:

- A **string** is a sequence of characters enclosed in quotation marks.
- Characters in a string are accessed using **indexing**, starting from index `0`.
- **Negative indices** count from the end of the string.
- The `len()` function returns the number of characters in a string.
- The `+` operator **concatenates** (joins) strings.
- The `*` operator **repeats** a string a given number of times.
- String **methods** perform operations on strings: `upper()`, `lower()`, `strip()`, and `replace()`.
- Strings are **immutable** — methods return new strings without changing the original.
- You cannot concatenate a string with an integer directly; use `str()` or an f-string.

---

## 10. Exercises

### Part A — Understanding Questions

1. What is a string in Python? Give two examples of values that are strings and two examples that are not.

2. What does "zero-based indexing" mean? Why does Python start counting from 0 instead of 1?

3. Explain the difference between `upper()` and `lower()`. When might `lower()` be useful in a program that processes user input?

4. What does the `strip()` method do? Why is it useful when working with input from users?

5. What does it mean that strings are **immutable**? How does this affect how you use string methods?

---

### Part B — Code Tracing

Trace through the following code carefully and write the exact output for each `print()` statement. Do not run the code until you have written your answers.

**Exercise 1:**

```python
text = "Programming"
print(text[0])
print(text[3])
print(text[-1])
print(len(text))
```

**Exercise 2:**

```python
a = "Hello"
b = "World"
c = a + ", " + b + "!"
print(c)
print(len(c))
```

**Exercise 3:**

```python
word = "  Python  "
print(word.strip())
print(word.strip().upper())
print(len(word))
print(len(word.strip()))
```

**Exercise 4:**

```python
message = "I love tea"
new_message = message.replace("tea", "coffee")
print(message)
print(new_message)
```

---

### Part C — Code Writing

1. Write a program that asks the user to enter their name. The program should:
   - Print the name in all uppercase letters.
   - Print the number of characters in the name.
   - Print a greeting in the format: `Hello, [NAME]!`

2. Write a program that asks the user to enter two words. The program should:
   - Print the two words joined together with no space.
   - Print the two words joined together with a single space between them.
   - Print the total number of characters in both words combined (not counting the space).

3. Write a program that stores the sentence `"  welcome to the python course  "` in a variable. The program should:
   - Remove the extra spaces using `strip()`.
   - Convert the result to title case using the `.title()` method (look it up — Python has many built-in string methods).
   - Print the final result.

4. Write a program that asks the user to enter a sentence. The program should count and print the number of characters in the sentence (including spaces).

---

### Part D — Code Modification

1. The following program has an error. Identify the error, explain why it occurs, and fix it.

```python
score = 95
print("Your score is: " + score)
```

2. The following program is supposed to print the last character of a name, but it does not work correctly. Fix it.

```python
name = "Fatima"
print(name[6])
```

3. The following code is supposed to clean a user's input and print it in lowercase. However, it does not store the result correctly. Fix the code so that it works as intended.

```python
user_input = "   HELLO WORLD   "
user_input.strip()
user_input.lower()
print(user_input)
```

4. Modify the following program so that it prints the separator line using repetition (`*`) instead of typing the dashes manually.

```python
print("Student Report")
print("--------------------")
print("Name: Ali")
print("--------------------")
```

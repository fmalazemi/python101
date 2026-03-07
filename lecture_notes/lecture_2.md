# Lecture 2: Variables, Basic Data Types, and User Input

---

## Why This Topic Matters

Every useful program works with information. A program that calculates a student's grade must store that grade somewhere. A program that greets a user by name must remember that name. In Python, we use **variables** to store and work with information.

Understanding variables and data types is the foundation of all programming. Without them, a program cannot remember anything, perform calculations, or communicate meaningfully with the user.

---

## Learning Objectives

By the end of this lecture, you will be able to:

- Explain what a variable is and why it is useful
- Identify the three basic data types: `int`, `float`, and `str`
- Store values in variables using the assignment operator (`=`)
- Print the value of a variable
- Use `input()` to receive information from the user
- Explain why `input()` always returns text
- Convert text to a number using `int()` and `float()`

---

## 1. Introduction

Imagine you are solving a mathematics problem on paper. You write: *"Let x = 5."* You have given the name *x* to the value *5*. Later in the problem, whenever you write *x*, you mean *5*.

Python works in exactly the same way. You give a name to a piece of information, and Python remembers it for you. This named piece of information is called a **variable**.

---

## 2. What Is a Variable?

### Explanation

A **variable** is a named storage location in the computer's memory. You choose the name, and Python stores the value under that name. Whenever you use the name later, Python retrieves the stored value.

### Analogy: A Labeled Box

Think of a variable as a **labeled box**:

- The **label** is the variable name (for example, `age`).
- The **contents** of the box are the value (for example, `20`).
- You can open the box to read the value, or you can replace the contents with a new value.

```
┌─────────────┐
│     20      │  ← value stored inside
└─────────────┘
     age         ← label (variable name)
```

You can change what is inside the box at any time. The label stays the same, but the contents can change.

---

## 3. Storing a Value in a Variable (Assignment)

### Explanation

To store a value in a variable, we use the **assignment operator**: the equals sign `=`.

The syntax is:

```
variable_name = value
```

This is called an **assignment statement**. It tells Python: *"Store this value under this name."*

> **Important:** In programming, `=` does **not** mean "is equal to." It means "store the value on the right into the variable on the left."

### Example 1: Storing and Printing a Variable

```python
age = 20
print(age)
```

**Output:**
```
20
```

**Explanation:**
- Line 1: Python creates a variable named `age` and stores the value `20` in it.
- Line 2: Python retrieves the value stored in `age` and prints it to the screen.

### Example 2: Changing the Value of a Variable

```python
score = 10
print(score)

score = 95
print(score)
```

**Output:**
```
10
95
```

**Explanation:**  
The variable `score` first holds `10`. Then it is reassigned to `95`. The old value is replaced. The box now contains new contents.

### Try It Yourself

Run the code above. Then try the following modifications:

1. Change the initial value of `score` to `50`. What does the output look like?
2. Add a third line that changes `score` again and prints it.
3. Create a new variable called `name` and assign your own name to it. Print it.

---

## 4. Variable Naming Rules

Before introducing data types, it is important to know how to name variables correctly.

| Rule | Correct Example | Incorrect Example |
|---|---|---|
| Use letters, digits, or underscores | `student_age` | `student-age` |
| Must not start with a digit | `score1` | `1score` |
| No spaces allowed | `first_name` | `first name` |
| Case-sensitive (`age` ≠ `Age`) | `age`, `Age` | — |
| Avoid Python reserved words | `total` | `for`, `if`, `print` |

> **Good practice:** Choose names that clearly describe what the variable stores. For example, `student_name` is better than `x` because it tells you what the variable represents.

---

## 5. Basic Data Types

### Explanation

Not all information is the same. The number `42` is different from the text `"hello"`. Python uses **data types** to distinguish between different kinds of information.

A **data type** tells Python what kind of value a variable holds and what operations can be performed on it.

In this lecture, we focus on three fundamental data types:

| Data Type | Name in Python | Example |
|---|---|---|
| Whole numbers | `int` (integer) | `5`, `100`, `-3` |
| Decimal numbers | `float` | `3.14`, `0.5`, `-1.7` |
| Text | `str` (string) | `"hello"`, `"Ahmed"` |

---

### 5.1 Integers (`int`)

An **integer** is a whole number — a number with no decimal point. It can be positive, negative, or zero.

**Examples:** `0`, `1`, `-10`, `500`

```python
year = 2025
temperature = -3
count = 0

print(year)
print(temperature)
print(count)
```

**Output:**
```
2025
-3
0
```

**Explanation:**  
Each variable stores a whole number. There are no decimal points. Python recognises these as integers automatically.

---

### 5.2 Floats (`float`)

A **float** (short for *floating-point number*) is a number that includes a decimal point. Use floats when precision beyond whole numbers is needed.

**Examples:** `3.14`, `0.5`, `-2.7`, `100.0`

```python
price = 9.99
height = 1.75
pi = 3.14159

print(price)
print(height)
print(pi)
```

**Output:**
```
9.99
1.75
3.14159
```

**Explanation:**  
Each variable stores a decimal number. Python recognises the decimal point and treats these as floats.

> **Note:** Even `100.0` is a float because it contains a decimal point, even though its value is a whole number.

---

### 5.3 Strings (`str`)

A **string** is a sequence of characters — letters, digits, spaces, or symbols — enclosed in quotation marks. Strings are used to represent text.

You can use either single quotes `'...'` or double quotes `"..."`.

**Examples:** `"hello"`, `'Python'`, `"student_01"`, `"I am learning."`

```python
first_name = "Sara"
greeting = "Hello, welcome to Python!"
course_code = "CS101"

print(first_name)
print(greeting)
print(course_code)
```

**Output:**
```
Sara
Hello, welcome to Python!
CS101
```

**Explanation:**  
Each variable stores text. Python treats everything between the quotation marks as a string, including numbers like `"101"` — because it is enclosed in quotes, it is text, not a number.

### Try It Yourself

Create three variables:
1. An integer representing the number of students in your class.
2. A float representing the average score of the class.
3. A string containing the name of your course.

Print all three variables.

---

## 6. Checking the Data Type with `type()`

Python provides a built-in function called `type()` that tells you the data type of any value or variable.

```python
age = 20
gpa = 3.75
name = "Ali"

print(type(age))
print(type(gpa))
print(type(name))
```

**Output:**
```
<class 'int'>
<class 'float'>
<class 'str'>
```

**Explanation:**  
- `age` is an `int` (integer).
- `gpa` is a `float` (decimal number).
- `name` is a `str` (string/text).

You will use `type()` frequently when checking whether a variable holds the kind of value you expect.

---

## 7. Getting Input from the User

### Explanation

So far, all the values in our programs have been written directly in the code. However, most programs need to interact with the user — asking for their name, age, or other information.

Python provides the built-in function `input()` to receive information from the user while the program is running.

### How `input()` Works

When Python executes `input()`, it:

1. Displays a message (called a **prompt**) on the screen.
2. **Pauses** and waits for the user to type something.
3. When the user presses Enter, Python captures what was typed and stores it in a variable.

### Example 3: Asking for a Name

```python
name = input("What is your name? ")
print("Hello,", name)
```

**Example interaction:**
```
What is your name? Sara
Hello, Sara
```

**Explanation:**  
- `input("What is your name? ")` displays the prompt and waits.
- The user types `Sara` and presses Enter.
- Python stores `"Sara"` in the variable `name`.
- `print("Hello,", name)` displays the greeting with the entered name.

> **Note:** The space before the closing quote in `"What is your name? "` is intentional. It creates a small gap between the prompt and the user's typed text, making the interaction easier to read.

### Try It Yourself

Run the example above. Then modify it:

1. Change the greeting so it says: `"Nice to meet you, [name]!"`
2. Add a second `input()` that asks for the user's favourite colour and print a sentence using it.

---

## 8. Important Rule: `input()` Always Returns a String

### Explanation

This is one of the most important rules in Python:

> **`input()` always returns a string (`str`), regardless of what the user types.**

Even if the user types the number `25`, Python stores it as the text `"25"`, not the number `25`.

### Example 4: Demonstrating That `input()` Returns a String

```python
age = input("How old are you? ")
print(type(age))
```

**Example interaction:**
```
How old are you? 25
<class 'str'>
```

**Explanation:**  
Even though the user typed `25`, `type(age)` shows `str`. Python did not store a number — it stored the text `"25"`.

This matters because you **cannot perform arithmetic** on text. If you try to add `5` to `"25"`, Python will produce an error.

---

## 9. Type Conversion: `int()` and `float()`

### Explanation

To use a number entered by the user in calculations, you must **convert** it from a string to a number. This process is called **type conversion** (also called *type casting*).

Python provides two functions for this:

| Function | Purpose | Example |
|---|---|---|
| `int()` | Converts to a whole number | `int("25")` → `25` |
| `float()` | Converts to a decimal number | `float("3.5")` → `3.5` |

### Example 5: Converting Input to an Integer

```python
age_text = input("How old are you? ")
age = int(age_text)
print("Next year, you will be", age + 1)
```

**Example interaction:**
```
How old are you? 20
Next year, you will be 21
```

**Explanation:**  
- Line 1: `input()` stores the user's response as a string in `age_text`.
- Line 2: `int(age_text)` converts the string `"20"` into the integer `20` and stores it in `age`.
- Line 3: Python can now perform arithmetic — `age + 1` equals `21`.

### Example 6: A Shorter Version (Combining Input and Conversion)

It is common to combine `input()` and `int()` on the same line:

```python
age = int(input("How old are you? "))
print("Next year, you will be", age + 1)
```

**Explanation:**  
This is equivalent to Example 5 but written in a single step. Python first runs `input()`, receives the text, then immediately passes it to `int()`, which converts it to a number.

### Example 7: Converting Input to a Float

```python
height = float(input("Enter your height in metres: "))
print("Your height is", height, "metres.")
```

**Example interaction:**
```
Enter your height in metres: 1.75
Your height is 1.75 metres.
```

**Explanation:**  
Use `float()` when the user may enter a decimal number.

### Try It Yourself

Write a program that:
1. Asks the user for two whole numbers.
2. Converts both inputs to integers.
3. Prints their sum.

---

## 10. Combining Variables and Strings in Output

When printing messages that include variable values, there are several approaches. Two simple methods are shown here.

### Method 1: Using Commas in `print()`

```python
name = "Lena"
age = 22
print("Name:", name, "Age:", age)
```

**Output:**
```
Name: Lena Age: 22
```

### Method 2: Using f-strings (Formatted Strings)

An **f-string** allows you to embed variable values directly inside a string. Place the letter `f` before the opening quote, and put variable names inside curly braces `{}`.

```python
name = "Lena"
age = 22
print(f"My name is {name} and I am {age} years old.")
```

**Output:**
```
My name is Lena and I am 22 years old.
```

**Explanation:**  
Python replaces `{name}` with the value of `name`, and `{age}` with the value of `age`. F-strings produce clean, readable output and are widely used in Python.

---

## 11. Common Mistakes and Misconceptions

### Mistake 1: Forgetting that `=` is assignment, not equality

```python
# This stores 10 in x. It does not ask "is x equal to 10?"
x = 10
```

Beginners sometimes confuse `=` (assignment) with `==` (comparison, which we will study later).

---

### Mistake 2: Using a variable before assigning it

```python
print(score)   # Error! score has not been defined yet.
score = 85
```

You must always assign a value to a variable before using it. Python reads code from top to bottom.

---

### Mistake 3: Performing arithmetic on a string

```python
age = input("Enter your age: ")
print(age + 1)   # Error! age is a string, not a number.
```

**Correction:**
```python
age = int(input("Enter your age: "))
print(age + 1)   # Now this works correctly.
```

---

### Mistake 4: Forgetting quotation marks around strings

```python
name = Sara    # Error! Python looks for a variable called Sara.
name = "Sara"  # Correct.
```

Without quotation marks, Python interprets `Sara` as a variable name, not text.

---

### Mistake 5: Using `int()` on a decimal string

```python
value = int("3.14")  # Error! int() cannot convert "3.14" directly.
value = float("3.14")  # Correct. Use float() for decimal numbers.
```

If the string contains a decimal point, use `float()`, not `int()`.

---

## 12. Summary

| Concept | Key Point |
|---|---|
| Variable | A named storage location. Uses the `=` operator to assign a value. |
| `int` | A whole number with no decimal point. Example: `5`, `-3`. |
| `float` | A number with a decimal point. Example: `3.14`, `0.5`. |
| `str` | A sequence of characters enclosed in quotes. Example: `"hello"`. |
| `type()` | A function that returns the data type of a value. |
| `input()` | Pauses the program and waits for user input. Always returns a `str`. |
| `int()` | Converts a string to an integer. |
| `float()` | Converts a string to a float. |
| f-string | A formatted string that embeds variable values using `{variable}`. |

---

## Exercises

### Section A: Understanding Questions

**A1.**  
In your own words, explain what a variable is. Use the "labeled box" analogy in your answer.

**A2.**  
What is the difference between an `int` and a `float`? Give one example of each.

**A3.**  
Why does `input()` always return a string? Why is this important to know?

**A4.**  
Look at the following code. What will be printed?

```python
city = "Muscat"
city = "Dubai"
print(city)
```

Explain your answer.

---

### Section B: Code Tracing

**B1.**  
Trace through the following code and write down exactly what is printed:

```python
x = 5
y = 3
x = x + y
print(x)
print(y)
```

**B2.**  
What is the output of the following code? Explain each line.

```python
first_name = "Ahmad"
age = 19
print(f"{first_name} is {age} years old.")
print(type(age))
```

**B3.**  
The following code contains an error. Identify the error and explain how to fix it.

```python
number = input("Enter a number: ")
result = number + 10
print(result)
```

---

### Section C: Code Writing

**C1.**  
Write a program that:
- Stores your first name in a variable
- Stores your age in a variable
- Prints a sentence using both variables

Use an f-string for the output.

**C2.**  
Write a program that asks the user for:
- Their name
- Their favourite number

Then prints a message in the following format:  
`Hello, [name]! Your favourite number is [number].`

**C3.**  
Write a program that:
- Asks the user to enter two decimal numbers
- Converts both inputs to floats
- Prints the sum of the two numbers

**C4.**  
Write a program that asks the user for their birth year. The program should then calculate and print their approximate age, assuming the current year is 2025.

---

### Section D: Code Modification

**D1.**  
The following program runs without errors, but the output is not what was intended. Identify the problem and fix it.

```python
num1 = input("Enter first number: ")
num2 = input("Enter second number: ")
print("The sum is:", num1 + num2)
```

*Hint: Run the program and observe the output carefully.*

**D2.**  
Modify the following program so that it prints the result using an f-string instead of commas.

```python
product = "Python Textbook"
price = 15.99
print("Product:", product, "Price:", price)
```

**D3.**  
The program below asks the user for their name but does not use it in the output. Modify it so the greeting includes the user's name.

```python
name = input("Enter your name: ")
print("Welcome to the Introduction to Python course!")
```

---

*End of Lecture 2*

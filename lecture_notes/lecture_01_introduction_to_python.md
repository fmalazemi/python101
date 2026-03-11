# Lecture 1: Introduction to Python and Writing Your First Program

---

## Learning Objectives

By the end of this lecture, you will be able to:

1. Explain what programming is and why it is useful.
2. Describe what Python is and why it is a good language for beginners.
3. Identify the key parts of a simple Python program.
4. Write and run a basic Python program.
5. Use the `print()` function to display text and numbers on the screen.
6. Recognise and correct common beginner mistakes.

---

## Why This Topic Matters

Every application you use — a search engine, a messaging app, a weather forecast — was created by a programmer. Programming is the skill of giving precise instructions to a computer so that it can perform useful tasks automatically.

Python is one of the most widely used programming languages in the world today. It is used in web development, data science, artificial intelligence, automation, and academic research. Because Python is designed to be readable and simple, it is the ideal first language for anyone beginning their programming journey.

Learning to write your first program is a small but important step. It builds the foundation for everything that follows.

---

## 1. What Is Programming?

### Explanation

A **program** is a set of instructions that tells a computer what to do. Writing those instructions is called **programming** (also called **coding**).

A computer is extremely fast and accurate, but it is also completely literal. It does exactly what you tell it to do — nothing more, nothing less. If your instructions are unclear or contain an error, the computer will not guess what you meant. It will either produce the wrong result or report an error.

### Analogy: A Program Is Like a Recipe

Think of a recipe for making tea:

1. Boil water.
2. Place a tea bag in a cup.
3. Pour the hot water into the cup.
4. Wait three minutes.
5. Remove the tea bag.

Each step is clear, ordered, and unambiguous. A recipe does not say "do something with water." It gives exact instructions. A program works in the same way — each instruction must be precise and written in the correct order.

### Key Terms

| Term | Meaning |
|---|---|
| **Program** | A list of instructions for a computer to follow |
| **Programming** | The act of writing a program |
| **Programmer** | A person who writes programs |

---

## 2. What Is Python?

### Explanation

**Python** is a programming language. A **programming language** is a formal system of words and symbols that humans use to write instructions for a computer.

There are many programming languages (for example, Java, C++, JavaScript). Python was created by Guido van Rossum and first released in 1991. It was designed with one important goal: to be easy to read and write.

### Why Python Is Good for Beginners

- Python code looks similar to plain English, which makes it easier to understand.
- Python has a simple and consistent structure.
- Python is free and available on all major operating systems.
- Python is used professionally in many industries, so learning it has real value.

### Example: Comparing Two Languages

Here is how you display the message "Hello, world!" in two different languages.

**In C++ (a more complex language):**
```cpp
#include <iostream>
int main() {
    std::cout << "Hello, world!" << std::endl;
    return 0;
}
```

**In Python:**
```python
print("Hello, world!")
```

Python requires far fewer symbols and words to accomplish the same task. This clarity is one of the main reasons Python is recommended for beginners.

---

## 3. Key Concepts: Source Code, Output, and Syntax

### 3.1 Source Code

**Source code** is the text that a programmer writes. It is the set of instructions, written in a programming language, that tells the computer what to do.

When you write a Python program, the text you type is your source code.

### 3.2 Output

**Output** is what the computer produces after running your program. It is the result that you see on the screen.

For example, if your source code says "display the word Hello", then the output is:

```
Hello
```

Think of source code as the recipe, and output as the finished dish.

### 3.3 Syntax

**Syntax** refers to the rules of a programming language — the correct way to write instructions so that the computer can understand them.

Every language has syntax. In English, the sentence "The cat sat on the mat" follows correct syntax. The sentence "sat cat the mat on the" does not — the words are correct, but the order and structure are wrong.

Python has its own syntax rules. If you break a syntax rule, Python will display an error message and will not run your program.

---

## 4. Writing Your First Python Program

### 4.1 The `print()` Function

The most fundamental action in Python is displaying information on the screen. You do this using the `print()` function.

**A function** is a named instruction that performs a specific task. `print()` is a built-in Python function whose task is to display output.

The syntax is:

```python
print(something)
```

The word or value you want to display is placed inside the parentheses.

---

### 4.2 Displaying Text

To display text, you write the text inside quotation marks. Text in a program is called a **string**.

```python
print("Hello, world!")
```

**Output:**
```
Hello, world!
```

**Explanation:**

- `print` is the name of the function.
- The parentheses `()` tell Python that you are calling (using) this function.
- `"Hello, world!"` is the string — a piece of text enclosed in quotation marks.
- Python reads this instruction, takes the text between the quotation marks, and displays it on the screen.

#### Try It Yourself

1. Type the program above exactly as shown and run it.
2. Change the text to display your own name. For example: `print("My name is Laila.")`
3. Observe the output each time.

---

### 4.3 Displaying Numbers

You can also display numbers using `print()`. When displaying a number, you do not use quotation marks.

```python
print(42)
```

**Output:**
```
42
```

```python
print(3.14)
```

**Output:**
```
3.14
```

**Explanation:**

- Numbers do not need quotation marks because they are not text — they are numerical values.
- Python can display whole numbers (called **integers**) and decimal numbers (called **floats**, short for floating-point numbers).

#### Try It Yourself

1. Display the number `100`.
2. Display the number `9.99`.
3. Display the number `0`.
4. Observe that no quotation marks are used.

---

### 4.4 Displaying Multiple Lines

You can use several `print()` statements in one program. Each statement displays its output on a new line.

```python
print("Welcome to Python.")
print("This is my first program.")
print("Programming is a useful skill.")
```

**Output:**
```
Welcome to Python.
This is my first program.
Programming is a useful skill.
```

**Explanation:**

- Python runs the program from top to bottom, one line at a time.
- Each `print()` statement produces one line of output.
- The order of the statements in your code determines the order of the output.

#### Try It Yourself

1. Write a program with three `print()` statements that introduces yourself. Include your name, your country, and your area of study.
2. Change the order of the statements and observe how the output changes.

---

### 4.5 Displaying Text and Numbers Together

You can display both text and numbers in a single `print()` statement by separating them with a comma.

```python
print("My age is", 21)
```

**Output:**
```
My age is 21
```

**Explanation:**

- The comma inside `print()` tells Python to display both items in sequence, separated by a space.
- The text `"My age is"` is a string (in quotation marks).
- The number `21` is an integer (no quotation marks).
- Python combines them and displays the result on one line.

#### Try It Yourself

1. Display the sentence: `The year is 2025` using both a string and a number.
2. Display your name and your favourite number together on one line.

---

## 5. Common Mistakes and Misconceptions

Beginners often make the same types of mistakes when writing their first Python programs. The following table describes the most common errors, their causes, and how to correct them.

### 5.1 Forgetting Quotation Marks Around Text

```python
# Incorrect
print(Hello)
```

**Error message:**
```
NameError: name 'Hello' is not defined
```

**Correct version:**
```python
print("Hello")
```

**Explanation:** When you write text without quotation marks, Python thinks you are referring to a variable (a stored value) with that name. Since no variable called `Hello` exists, Python reports an error. Always enclose text in quotation marks.

---

### 5.2 Forgetting the Parentheses

```python
# Incorrect
print "Hello"
```

**Error message:**
```
SyntaxError: Missing parentheses in call to 'print'
```

**Correct version:**
```python
print("Hello")
```

**Explanation:** In Python 3, `print` must always be followed by parentheses. Without them, Python does not recognise the instruction and reports a syntax error.

---

### 5.3 Mismatched Quotation Marks

```python
# Incorrect
print("Hello')
```

**Error message:**
```
SyntaxError: EOL while scanning string literal
```

**Correct version:**
```python
print("Hello")
```

**Explanation:** A string must begin and end with the same type of quotation mark — either both double quotes `"..."` or both single quotes `'...'`. Mixing them causes a syntax error.

---

### 5.4 Incorrect Capitalisation of `print`

```python
# Incorrect
Print("Hello")
```

**Error message:**
```
NameError: name 'Print' is not defined
```

**Correct version:**
```python
print("Hello")
```

**Explanation:** Python is **case-sensitive**, which means it treats `print` and `Print` as two completely different words. The built-in function is always written in lowercase: `print`.

---

### 5.5 Putting a Number in Quotation Marks When You Want to Calculate

```python
print("5" + "3")
```

**Output:**
```
53
```

**Explanation:** When numbers are enclosed in quotation marks, Python treats them as text, not as numerical values. Adding two strings joins them together (this is called **concatenation**). If you want to add the numbers mathematically, do not use quotation marks:

```python
print(5 + 3)
```

**Output:**
```
8
```

---

## 6. Summary

| Concept | Key Point |
|---|---|
| Program | A set of instructions for a computer |
| Python | A beginner-friendly programming language |
| Source code | The text of a program, written by the programmer |
| Output | The result displayed after a program runs |
| Syntax | The rules for writing correct code |
| `print()` | A function that displays output on the screen |
| String | Text enclosed in quotation marks |
| Integer | A whole number, written without quotation marks |

**Core rules to remember:**

- Text (strings) must be enclosed in quotation marks: `"like this"` or `'like this'`.
- Numbers do not use quotation marks: `42` or `3.14`.
- `print` must always be written in lowercase.
- Always include parentheses after `print`.
- Python runs your program from top to bottom, one line at a time.

---

## 7. Exercises

The following exercises are designed to reinforce the concepts covered in this lecture. Attempt each exercise by writing and running the code in Python.

---

### Section A — Understanding Questions

1. In your own words, explain what a program is. Use the recipe analogy or create your own analogy.

2. What is the difference between **source code** and **output**? Give one example of each.

3. Why does Python require quotation marks around text? What happens if you forget them?

4. What does it mean to say that Python is **case-sensitive**? Give one example that illustrates this.

5. What is **syntax**? Why is correct syntax important when writing a program?

---

### Section B — Code Tracing

*For each program below, write down the output you expect before running the code. Then run the code and check your answer.*

**Exercise 6:**
```python
print("Good morning.")
print("Today is a great day to learn Python.")
print("Let us begin.")
```

**Exercise 7:**
```python
print(100)
print(3.5)
print(0)
```

**Exercise 8:**
```python
print("The answer is", 42)
print("Pi is approximately", 3.14159)
```

**Exercise 9:**

What will happen when you run the following code? Explain your answer before running it.
```python
print("10" + "20")
```

---

### Section C — Code Writing

*Write Python programs for the following tasks.*

**Exercise 10:**
Write a program that displays the following three lines exactly:
```
Hello, world!
Welcome to Python.
I am ready to learn.
```

**Exercise 11:**
Write a program that displays your full name, your age, and the name of your university — each on a separate line.

**Exercise 12:**
Write a program that displays the following sentence using both a string and a number in a single `print()` statement:
```
There are 7 days in a week.
```

**Exercise 13:**
Write a program that displays the results of the following calculations. Use `print()` once for each:
- 15 + 7
- 100 - 45
- 6 × 8 (use `*` for multiplication in Python)

---

### Section D — Code Modification

*Each exercise below contains a program with one or more errors. Find the error, explain what is wrong, and write the corrected version.*

**Exercise 14:**
```python
print(Hello, world!)
```

**Exercise 15:**
```python
Print("Welcome to Python.")
```

**Exercise 16:**
```python
print("My favourite number is" 7)
```

**Exercise 17:**
```python
print('Python is easy to learn.")
```

**Exercise 18 (Slightly Challenging):**

The following program is intended to display three separate lines of output, but it produces an error. Identify the mistake and correct it.
```python
print("Line one.")
print("Line two."
print("Line three.")
```

---

### Section E — Slightly Challenging

**Exercise 19:**
Without running the code first, predict the output of the following program. Then run it and explain any difference between your prediction and the actual output.

```python
print("1" + "2" + "3")
print(1 + 2 + 3)
```

**Exercise 20:**
Write a short Python program (at least five `print()` statements) that displays a simple introduction about yourself. Include your name, age, country of origin, field of study, and one reason why you want to learn programming. Use a combination of plain text and text-with-number statements.

---

*End of Lecture 1*

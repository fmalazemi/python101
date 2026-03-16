# Lecture 10: Functions — Organizing Code into Reusable Parts

---

## Learning Objectives

By the end of this lecture, you will be able to:

- Explain what a function is and why functions are useful
- Define a function using the `def` keyword
- Call a function to execute its code
- Write functions that accept parameters (inputs)
- Write functions that return values (outputs)
- Distinguish between printing inside a function and returning a value

---

## Why This Topic Matters

As your programs grow longer, you will notice that some tasks appear again and again. Without functions, you would have to rewrite the same code every time you need it. This makes programs difficult to read, difficult to fix, and easy to break.

Functions allow you to write a piece of code once, give it a name, and then use it as many times as you need. This is one of the most important habits in programming. Nearly every program you will ever write — in Python or in any other language — relies heavily on functions.

---

## 1. What Is a Function?

A **function** is a named block of code that performs a specific task. You define it once and can execute it (or "call" it) at any point in your program.

**Analogy:** Think of a function as a machine in a factory. You place raw materials into the machine (input), the machine performs an operation, and it produces a finished product (output). You can use the same machine as many times as you need — you do not rebuild it each time.

In Python:
- The **input** to a function is called a **parameter** (or **argument**)
- The **output** from a function is called the **return value**

Some functions take no input and produce no output — they simply perform an action, such as printing a message.

---

## 2. Defining a Function

To create a function in Python, use the `def` keyword. This tells Python: "I am about to define a function."

**Syntax:**

```python
def function_name():
    # code to execute
```

- `def` — the keyword that begins a function definition
- `function_name` — the name you choose for your function (follow the same rules as variable names)
- `()` — parentheses that will hold parameters (left empty for now)
- `:` — a colon that ends the function header
- The indented block below is the **function body** — the code that runs when the function is called

> **Important:** Defining a function does not run it. You must **call** the function separately.

---

### 2.1 A Simple Function with No Parameters

**Example 1 — A greeting function:**

```python
def greet():
    print("Hello! Welcome to the Python course.")
```

This defines a function called `greet`. When this code runs, nothing happens yet — the function is only defined.

To execute it, you must **call** it:

```python
greet()
```

**Output:**

```
Hello! Welcome to the Python course.
```

**Explanation:**
- `def greet():` creates the function and gives it the name `greet`
- `greet()` calls the function — this is what actually runs the code inside it
- Notice that the call looks like the function name followed by parentheses

---

#### Try It Yourself

1. Define a function called `show_date` that prints: `"Today we will study functions."`
2. Call the function.
3. Try calling the function three times in a row. What do you observe?

---

### 2.2 Calling a Function Multiple Times

One of the great advantages of functions is reusability. You can call the same function as many times as needed.

**Example 2 — Calling a function multiple times:**

```python
def print_separator():
    print("--------------------")

print_separator()
print("Student Name: Ali")
print_separator()
print("Grade: A")
print_separator()
```

**Output:**

```
--------------------
Student Name: Ali
--------------------
Grade: A
--------------------
```

**Explanation:**
The `print_separator` function prints a line of dashes. Instead of typing `print("--------------------")` three times, you write the function once and call it wherever you need it. If you ever want to change the separator, you only change it in one place.

---

## 3. Functions with Parameters

A **parameter** is a variable that a function receives as input. It allows the function to work with different values each time it is called.

**Syntax:**

```python
def function_name(parameter):
    # use parameter here
```

---

### 3.1 One Parameter

**Example 3 — A personalised greeting:**

```python
def greet_student(name):
    print("Hello,", name, "! Welcome to class.")
```

Here, `name` is the parameter. It acts as a placeholder for whatever value you pass when you call the function.

```python
greet_student("Sara")
greet_student("Omar")
greet_student("Lena")
```

**Output:**

```
Hello, Sara ! Welcome to class.
Hello, Omar ! Welcome to class.
Hello, Lena ! Welcome to class.
```

**Explanation:**
Each time you call `greet_student`, you provide a value (called an **argument**) inside the parentheses. Python assigns that value to the parameter `name` for the duration of the function call.

---

#### Try It Yourself

1. Modify `greet_student` so that it also prints: `"Good luck with your studies!"`
2. Write a function called `announce` that takes one parameter `subject` and prints: `"Today's lecture is about: [subject]"`
3. Call `announce` with three different subjects.

---

### 3.2 Multiple Parameters

A function can accept more than one parameter. Separate them with commas.

**Example 4 — Calculating the area of a rectangle:**

```python
def calculate_area(length, width):
    area = length * width
    print("The area is:", area)
```

```python
calculate_area(5, 3)
calculate_area(10, 4)
```

**Output:**

```
The area is: 15
The area is: 40
```

**Explanation:**
- The function `calculate_area` receives two parameters: `length` and `width`
- When you call `calculate_area(5, 3)`, Python sets `length = 5` and `width = 3`
- The order of the arguments matters — the first argument is assigned to the first parameter, and so on

---

#### Try It Yourself

1. Write a function called `calculate_perimeter` that takes `length` and `width` as parameters and prints the perimeter of a rectangle. (Perimeter = 2 × length + 2 × width)
2. Call your function with two different sets of values.

---

## 4. Return Values

So far, all our functions have printed their results. However, in many situations, you need the function to **give back** a value so that you can use it later in your program.

A **return value** is the output that a function sends back to the code that called it. You use the `return` keyword to do this.

**Syntax:**

```python
def function_name(parameter):
    result = # some calculation
    return result
```

---

### 4.1 Returning a Single Value

**Example 5 — Area function with a return value:**

```python
def calculate_area(length, width):
    area = length * width
    return area
```

```python
room_area = calculate_area(6, 4)
print("The room area is:", room_area)
```

**Output:**

```
The room area is: 24
```

**Explanation:**
- The function calculates `area` and sends it back using `return`
- The calling code receives the value and stores it in the variable `room_area`
- The returned value can then be used anywhere in the program — printed, stored, or used in further calculations

---

### 4.2 Using the Return Value Directly

You do not have to store the return value in a variable. You can use it directly:

```python
print("Area:", calculate_area(7, 3))
```

**Output:**

```
Area: 21
```

---

### 4.3 A Practical Example — Maximum of Two Numbers

**Example 6 — Finding the larger of two numbers:**

```python
def find_maximum(a, b):
    if a > b:
        return a
    else:
        return b
```

```python
result = find_maximum(15, 9)
print("The maximum is:", result)

print("The maximum is:", find_maximum(100, 250))
```

**Output:**

```
The maximum is: 15
The maximum is: 250
```

**Explanation:**
- The function compares `a` and `b`
- It returns whichever is larger
- A function can have more than one `return` statement, but only one will execute per call
- Once Python reaches a `return` statement, it immediately exits the function

---

#### Try It Yourself

1. Write a function called `find_minimum` that takes two numbers and returns the smaller one.
2. Write a function called `square` that takes a number and returns its square (the number multiplied by itself).
3. Call each function and print the results.

---

## 5. The Difference Between Printing and Returning

This is a very common source of confusion for beginners. It is important to understand the difference clearly.

| | `print()` inside a function | `return` inside a function |
|---|---|---|
| **What it does** | Displays output on the screen | Sends a value back to the caller |
| **Can you use the result later?** | No | Yes |
| **Visible to the user?** | Yes (immediately) | Only if you print the returned value |

**Example 7 — Comparing print and return:**

```python
def add_with_print(a, b):
    print(a + b)

def add_with_return(a, b):
    return a + b
```

```python
# Using the print version
result1 = add_with_print(3, 4)
print("Result1 is:", result1)
```

**Output:**

```
7
Result1 is: None
```

**Explanation:**
`add_with_print` displays `7` on the screen, but it does not return a value. When you try to store its output in `result1`, Python assigns `None` — because no value was returned. `None` is Python's way of saying "nothing."

```python
# Using the return version
result2 = add_with_return(3, 4)
print("Result2 is:", result2)
```

**Output:**

```
Result2 is: 7
```

**Explanation:**
`add_with_return` sends back the value `7`. The calling code stores it in `result2` and can use it freely.

**Rule of thumb:** Use `return` when you want to use the result of a function elsewhere in your code. Use `print` only when you want to display something directly and do not need the value again.

---

## 6. Common Mistakes

### Mistake 1 — Defining a function but forgetting to call it

```python
def greet():
    print("Hello!")

# The function is defined, but never called.
# Nothing will happen.
```

**Fix:** Always call the function after defining it:

```python
def greet():
    print("Hello!")

greet()  # This actually runs the function
```

---

### Mistake 2 — Calling a function before defining it

```python
greet()  # Error: greet is not yet defined

def greet():
    print("Hello!")
```

**Error:**

```
NameError: name 'greet' is not defined
```

**Fix:** Always define the function before calling it. In Python, the `def` block must appear earlier in the file than the call.

---

### Mistake 3 — Forgetting that `print` does not return a value

```python
def double(n):
    print(n * 2)

result = double(5)
print(result + 1)  # Error!
```

**Error:**

```
TypeError: unsupported operand type(s) for +: 'NoneType' and 'int'
```

**Fix:** Use `return` when you need to use the result:

```python
def double(n):
    return n * 2

result = double(5)
print(result + 1)  # Output: 11
```

---

### Mistake 4 — Incorrect number of arguments

```python
def greet_student(name):
    print("Hello,", name)

greet_student("Ali", "Omar")  # Too many arguments
```

**Error:**

```
TypeError: greet_student() takes 1 positional argument but 2 were given
```

**Fix:** Match the number of arguments to the number of parameters:

```python
greet_student("Ali")
```

---

### Mistake 5 — Using a variable defined inside a function outside of it

```python
def calculate():
    answer = 42

calculate()
print(answer)  # Error!
```

**Error:**

```
NameError: name 'answer' is not defined
```

**Explanation:** Variables created inside a function exist only within that function. This is called **scope**. To use a value outside a function, you must `return` it.

**Fix:**

```python
def calculate():
    answer = 42
    return answer

result = calculate()
print(result)  # Output: 42
```

---

## 7. Summary

| Concept | Explanation |
|---|---|
| `def` | Keyword used to define a function |
| Function name | The name you give to the function (follows variable naming rules) |
| Parameter | A variable that receives input when the function is called |
| Argument | The actual value you pass to a function when calling it |
| `return` | Sends a value back to the caller; exits the function immediately |
| Calling a function | Writing the function name followed by parentheses: `function_name()` |
| `None` | Python's value for "nothing"; returned automatically if there is no `return` |

**Key principles to remember:**

- Define a function with `def`, then call it by name
- Parameters make functions flexible — they allow the same function to work with different inputs
- Use `return` when you need to use the result of a function in other parts of your code
- A function that only prints is not the same as a function that returns

---

## Exercises

### Part A — Understanding Questions

1. What is the purpose of a function in a Python program?
2. What is the difference between a parameter and an argument? Give an example of each.
3. What does the `return` keyword do? What happens if a function has no `return` statement?
4. Why is it a problem to call a function before it has been defined?
5. What is `None` in Python? When does a function return `None`?

---

### Part B — Code Tracing

**Question 1:** What is the output of the following code? Trace through it step by step.

```python
def multiply(x, y):
    result = x * y
    return result

a = multiply(3, 4)
b = multiply(a, 2)
print(b)
```

**Question 2:** What is the output of the following code?

```python
def check_positive(n):
    if n > 0:
        return "positive"
    else:
        return "not positive"

print(check_positive(10))
print(check_positive(-3))
print(check_positive(0))
```

**Question 3:** Identify the mistake in this code. What will happen when it runs?

```python
def add(a, b):
    print(a + b)

total = add(5, 7)
print("Total:", total * 2)
```

---

### Part C — Code Writing

1. Write a function called `greet_user` that takes a name as a parameter and prints: `"Good morning, [name]!"`

2. Write a function called `celsius_to_fahrenheit` that takes a temperature in Celsius and **returns** the equivalent temperature in Fahrenheit.
   - Formula: `fahrenheit = (celsius * 9 / 5) + 32`
   - Call the function with three different values and print each result.

3. Write a function called `is_even` that takes an integer and **returns** `True` if the number is even, and `False` if it is odd.
   - Call the function with several numbers and print the results.

4. Write a function called `calculate_bmi` that takes a person's weight in kilograms and height in metres and **returns** their Body Mass Index (BMI).
   - Formula: `bmi = weight / (height ** 2)`
   - Call the function with two different sets of values and print each result.

---

### Part D — Code Modification

1. The following function prints the square of a number. Modify it so that it **returns** the square instead of printing it. Then write code that calls the function and uses the returned value in a calculation.

```python
def square(n):
    print(n * n)
```

2. The following function always greets the same person. Modify it to accept a `name` parameter so it can greet anyone.

```python
def greet():
    print("Hello, Ahmed! How are you today?")
```

3. The following function is supposed to return the larger of two numbers, but it contains a mistake. Find and correct the mistake.

```python
def find_max(a, b):
    if a > b:
        return b
    else:
        return a
```

4. Extend the `calculate_area` function from this lecture so that it also **returns** the perimeter of the rectangle (`perimeter = 2 * length + 2 * width`). The function should return both values. *(Hint: In Python, you can return two values separated by a comma: `return area, perimeter`)*

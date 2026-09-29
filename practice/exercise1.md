# Python Introductory Exercises

These exercises progress from easy to challenging. They use only:

- Variables
- Expressions and operators
- `if`
- `if-else`
- `if-elif-else`
- Basic `input()` and `print()`

> Assume the user enters valid numeric input whenever a number is requested.

## Exercises

### 1. Personal Greeting — Easy

Ask the user for their name, store it in a variable, and print a greeting in this format:

```text
Hello, Sara!
```

[View solution](#solution-1)

### 2. Age Next Year — Easy

Ask the user for their current age. Calculate and print how old they will be next year.

Example:

```text
Enter your age: 18
Next year, you will be 19 years old.
```

[View solution](#solution-2)

### 3. Rectangle Calculator — Easy

Ask the user for the length and width of a rectangle. Calculate and print its area and perimeter.

Use these formulas:

```text
area = length × width
perimeter = 2 × (length + width)
```

[View solution](#solution-3)

### 4. Temperature Converter — Easy

Ask the user for a temperature in Celsius. Convert it to Fahrenheit and print the result.

Use this formula:

```text
Fahrenheit = Celsius × 9 / 5 + 32
```

[View solution](#solution-4)

### 5. Total Bill — Easy

Ask the user for the price of one item and the quantity purchased. Calculate the subtotal, add 5% tax, and print the final total.

[View solution](#solution-5)

### 6. Positive Number Check — Easy

Ask the user for a number. If the number is greater than zero, print:

```text
The number is positive.
```

If it is zero or negative, the program does not need to print anything.

[View solution](#solution-6)

### 7. Passing Grade — Easy

Ask the user for a grade from 0 to 100. If the grade is 60 or higher, print `Pass`. Otherwise, print `Fail`.

[View solution](#solution-7)

### 8. Even or Odd — Easy–Medium

Ask the user for an integer. Print whether the number is even or odd.

Hint: use the remainder operator `%`.

[View solution](#solution-8)

### 9. Larger Number — Easy–Medium

Ask the user for two numbers. Print the larger number. If both numbers are equal, print `The numbers are equal.`

[View solution](#solution-9)

### 10. Number Sign — Medium

Ask the user for a number. Print whether it is positive, negative, or zero.

[View solution](#solution-10)

### 11. Ticket Price by Age — Medium

Ask the user for their age and calculate the ticket price:

- Under 5: free
- From 5 through 12: $5
- From 13 through 59: $10
- 60 or older: $7

Print the ticket price.

[View solution](#solution-11)

### 12. Grade Letter — Medium

Ask the user for a grade from 0 to 100 and print its letter grade:

- 90–100: `A`
- 80–89: `B`
- 70–79: `C`
- 60–69: `D`
- Below 60: `F`

[View solution](#solution-12)

### 13. Simple Calculator — Medium

Ask the user for two numbers and an operator (`+`, `-`, `*`, or `/`). Perform the chosen operation and print the result.

If the operator is not supported, print `Invalid operator`.

If the user tries to divide by zero, print `Cannot divide by zero`.

[View solution](#solution-13)

### 14. Discount Calculator — Medium

Ask the user for the total purchase amount. Apply a discount according to these rules:

- Less than $50: no discount
- $50 up to $99.99: 10% discount
- $100 up to $199.99: 15% discount
- $200 or more: 20% discount

Print the discount amount and the final price.

[View solution](#solution-14)

### 15. Triangle Validity — Medium

Ask the user for three side lengths. A triangle is valid only if:

- Every side is greater than zero.
- The sum of every pair of sides is greater than the remaining side.

Print `Valid triangle` or `Invalid triangle`.

[View solution](#solution-15)

### 16. Triangle Type — Medium–Hard

Ask the user for three side lengths. Assume the sides form a valid triangle. Print its type:

- `Equilateral` if all three sides are equal
- `Isosceles` if exactly two sides are equal
- `Scalene` if all three sides are different

[View solution](#solution-16)

### 17. Leap Year — Hard

Ask the user for a year. Print whether it is a leap year.

A year is a leap year when:

- It is divisible by 400, or
- It is divisible by 4 but not divisible by 100.

[View solution](#solution-17)

### 18. Shipping Cost — Hard

Ask the user for the package weight in kilograms and whether they want express shipping (`yes` or `no`). Calculate the base shipping cost:

- Up to 1 kg: $5
- More than 1 kg and up to 5 kg: $10
- More than 5 kg and up to 10 kg: $15
- More than 10 kg: $25

Express shipping adds 50% to the base cost. Print the final shipping cost.

[View solution](#solution-18)

### 19. Electricity Bill — Hard

Ask the user for the number of electricity units consumed. Calculate the bill using progressive rates:

- First 100 units: $0.10 per unit
- Next 100 units (101–200): $0.15 per unit
- Any units above 200: $0.25 per unit

For example, 250 units cost:

```text
(100 × $0.10) + (100 × $0.15) + (50 × $0.25)
```

If the calculated bill is more than $40, add a 5% surcharge. Print the final bill.

[View solution](#solution-19)

### 20. Date Validator — Hard

Ask the user for a day, month, and year. Print whether the date is valid.

Requirements:

- The month must be from 1 to 12.
- The day must be valid for the selected month.
- April, June, September, and November have 30 days.
- February has 28 days, or 29 in a leap year.
- All other months have 31 days.

[View solution](#solution-20)

---

## Solutions

### Solution 1

```python
name = input("Enter your name: ")
print("Hello, " + name + "!")
```

[Back to Exercise 1](#1-personal-greeting--easy)

### Solution 2

```python
age = int(input("Enter your age: "))
age_next_year = age + 1
print("Next year, you will be", age_next_year, "years old.")
```

[Back to Exercise 2](#2-age-next-year--easy)

### Solution 3

```python
length = float(input("Enter the length: "))
width = float(input("Enter the width: "))

area = length * width
perimeter = 2 * (length + width)

print("Area:", area)
print("Perimeter:", perimeter)
```

[Back to Exercise 3](#3-rectangle-calculator--easy)

### Solution 4

```python
celsius = float(input("Enter the temperature in Celsius: "))
fahrenheit = celsius * 9 / 5 + 32
print("Temperature in Fahrenheit:", fahrenheit)
```

[Back to Exercise 4](#4-temperature-converter--easy)

### Solution 5

```python
price = float(input("Enter the price of one item: "))
quantity = int(input("Enter the quantity: "))

subtotal = price * quantity
tax = subtotal * 0.05
total = subtotal + tax

print("Subtotal: $", round(subtotal, 2))
print("Tax: $", round(tax, 2))
print("Final total: $", round(total, 2))
```

[Back to Exercise 5](#5-total-bill--easy)

### Solution 6

```python
number = float(input("Enter a number: "))

if number > 0:
    print("The number is positive.")
```

[Back to Exercise 6](#6-positive-number-check--easy)

### Solution 7

```python
grade = float(input("Enter the grade: "))

if grade >= 60:
    print("Pass")
else:
    print("Fail")
```

[Back to Exercise 7](#7-passing-grade--easy)

### Solution 8

```python
number = int(input("Enter an integer: "))

if number % 2 == 0:
    print("The number is even.")
else:
    print("The number is odd.")
```

[Back to Exercise 8](#8-even-or-odd--easymedium)

### Solution 9

```python
first = float(input("Enter the first number: "))
second = float(input("Enter the second number: "))

if first > second:
    print("The larger number is", first)
elif second > first:
    print("The larger number is", second)
else:
    print("The numbers are equal.")
```

[Back to Exercise 9](#9-larger-number--easymedium)

### Solution 10

```python
number = float(input("Enter a number: "))

if number > 0:
    print("Positive")
elif number < 0:
    print("Negative")
else:
    print("Zero")
```

[Back to Exercise 10](#10-number-sign--medium)

### Solution 11

```python
age = int(input("Enter your age: "))

if age < 5:
    price = 0
elif age <= 12:
    price = 5
elif age <= 59:
    price = 10
else:
    price = 7

print("Ticket price: $", price)
```

[Back to Exercise 11](#11-ticket-price-by-age--medium)

### Solution 12

```python
grade = float(input("Enter the grade: "))

if grade >= 90:
    letter = "A"
elif grade >= 80:
    letter = "B"
elif grade >= 70:
    letter = "C"
elif grade >= 60:
    letter = "D"
else:
    letter = "F"

print("Letter grade:", letter)
```

[Back to Exercise 12](#12-grade-letter--medium)

### Solution 13

```python
first = float(input("Enter the first number: "))
operator = input("Enter an operator (+, -, *, /): ")
second = float(input("Enter the second number: "))

if operator == "+":
    print("Result:", first + second)
elif operator == "-":
    print("Result:", first - second)
elif operator == "*":
    print("Result:", first * second)
elif operator == "/":
    if second == 0:
        print("Cannot divide by zero")
    else:
        print("Result:", first / second)
else:
    print("Invalid operator")
```

[Back to Exercise 13](#13-simple-calculator--medium)

### Solution 14

```python
total = float(input("Enter the purchase amount: $"))

if total < 50:
    discount_rate = 0
elif total < 100:
    discount_rate = 0.10
elif total < 200:
    discount_rate = 0.15
else:
    discount_rate = 0.20

discount = total * discount_rate
final_price = total - discount

print("Discount: $", round(discount, 2))
print("Final price: $", round(final_price, 2))
```

[Back to Exercise 14](#14-discount-calculator--medium)

### Solution 15

```python
side1 = float(input("Enter the first side: "))
side2 = float(input("Enter the second side: "))
side3 = float(input("Enter the third side: "))

all_positive = side1 > 0 and side2 > 0 and side3 > 0
follows_triangle_rule = (
    side1 + side2 > side3
    and side1 + side3 > side2
    and side2 + side3 > side1
)

if all_positive and follows_triangle_rule:
    print("Valid triangle")
else:
    print("Invalid triangle")
```

[Back to Exercise 15](#15-triangle-validity--medium)

### Solution 16

```python
side1 = float(input("Enter the first side: "))
side2 = float(input("Enter the second side: "))
side3 = float(input("Enter the third side: "))

if side1 == side2 and side2 == side3:
    print("Equilateral")
elif side1 == side2 or side1 == side3 or side2 == side3:
    print("Isosceles")
else:
    print("Scalene")
```

[Back to Exercise 16](#16-triangle-type--mediumhard)

### Solution 17

```python
year = int(input("Enter a year: "))

if year % 400 == 0:
    print("Leap year")
elif year % 100 == 0:
    print("Not a leap year")
elif year % 4 == 0:
    print("Leap year")
else:
    print("Not a leap year")
```

[Back to Exercise 17](#17-leap-year--hard)

### Solution 18

```python
weight = float(input("Enter the package weight in kg: "))
express = input("Express shipping (yes or no): ")

if weight <= 1:
    base_cost = 5
elif weight <= 5:
    base_cost = 10
elif weight <= 10:
    base_cost = 15
else:
    base_cost = 25

if express == "yes":
    final_cost = base_cost * 1.50
else:
    final_cost = base_cost

print("Shipping cost: $", round(final_cost, 2))
```

[Back to Exercise 18](#18-shipping-cost--hard)

### Solution 19

```python
units = float(input("Enter the number of units consumed: "))

if units <= 100:
    bill = units * 0.10
elif units <= 200:
    bill = 100 * 0.10 + (units - 100) * 0.15
else:
    bill = 100 * 0.10 + 100 * 0.15 + (units - 200) * 0.25

if bill > 40:
    bill = bill * 1.05

print("Final bill: $", round(bill, 2))
```

[Back to Exercise 19](#19-electricity-bill--hard)

### Solution 20

```python
day = int(input("Enter the day: "))
month = int(input("Enter the month: "))
year = int(input("Enter the year: "))

if year % 400 == 0:
    leap_year = True
elif year % 100 == 0:
    leap_year = False
elif year % 4 == 0:
    leap_year = True
else:
    leap_year = False

if month == 2:
    if leap_year:
        maximum_day = 29
    else:
        maximum_day = 28
elif month == 4 or month == 6 or month == 9 or month == 11:
    maximum_day = 30
elif month == 1 or month == 3 or month == 5 or month == 7 or month == 8 or month == 10 or month == 12:
    maximum_day = 31
else:
    maximum_day = 0

if maximum_day != 0 and day >= 1 and day <= maximum_day:
    print("Valid date")
else:
    print("Invalid date")
```

[Back to Exercise 20](#20-date-validator--hard)

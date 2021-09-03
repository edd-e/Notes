# Python<!-- omit in toc -->

Python is an interpreted programming language and it is dynamically typed.
(These notes are for Python 3)

## Table of contents<!-- omit in toc -->

- [Hello world](#hello-world)
- [Indentation](#indentation)
- [Variables](#variables)
- [Constants](#constants)
- [Comments](#comments)
- [Data types](#data-types)
  - [Numbers](#numbers)
    - [Numeric operations](#numeric-operations)
  - [Strings](#strings)
    - [String functions](#string-functions)
    - [String interpolation](#string-interpolation)
- [Lists](#lists)
  - [List functions](#list-functions)
  - [Slicing](#slicing)
  - [Ranges](#ranges)
  - [List comprehensions](#list-comprehensions)
- [Loops](#loops)
  - [For](#for)
  - [While](#while)
- [Control flow](#control-flow)
  - [If/else statements](#ifelse-statements)
  - [Boolean operators](#boolean-operators)
  - [Checking for empty lists](#checking-for-empty-lists)
- [Functions](#functions)
  - [Defining functions](#defining-functions)
  - [Passing parameters](#passing-parameters)
  - [Passing lists to functions](#passing-lists-to-functions)
- [Classes](#classes)

## Hello world

File: `hello_world.py`

Code:

```python
print("Hello world!")
```

## Indentation

Python uses indentation (instead of braces) as part of the language syntax.

## Variables

Python variable names can contain only letters, numbers, and underscores.

A variable name cannot begin with a number.

By convention, variable names are written in `snake_case`.

You can also assign multiple variables in a single line:

```python
apples = 5
last_name = "Bates"
x, y, z = 0, 0, 0
```

To define a null variable, use the `None` keyword:

```python
error_code = None
```

## Constants

Python does **not** have a constant type. To declare a constant, declare a variable name in all capital letters and treat the variable as a constant in the code.

```python
MAX_CAPACITY = 24
```

## Comments

Single line comments:

```python
# Single line comment
```

Multi-line comments:

```python
"""
This is
a multi-line
comment
"""
```

## Data types

Python has a variety of built-in data types, including numeric, sequence, and binary types. There is also a string and a boolean type.

Python is dynamically typed, there is no need to declare the data type.

### Numbers

There are four numeric types.

- Integers.
- Long integers.
- Floating point numbers.
- Complex numbers.

Long numbers can use underscores to improve readability:

```python
long_number = 37_000_000_000
```

#### Numeric operations

Python supports all basic arithmetic operations (`+`, `-`, `*`, `/`, `%`), as well as the following operations:

| Numeric Operation    | Result                                                   |
| -------------------- | -------------------------------------------------------- |
| x // y               | Floor division                                           |
| abs(x)               | Absolute value                                           |
| int(x)               | Converts x to integer                                    |
| long(x)              | Converts x to long integer                               |
| float(x)             | Converts x to floating point                             |
| complex(re,im)       | A complex number with real part re and imaginary part im |
| pow(x,y) or x \*\* y | x to the power y                                         |

### Strings

Strings can be defined using single quotes or double quotes:

```python
sentence_1 = "This is a string"
sentence_2 = 'This is also a string'
```

In practice, it is best to choose a single style and remain consistent.

Strings are treated as lists, with the distinction that strings are immutable and lists are mutable.

#### String functions

These are a few commonly used string functions where `str` is some string:

| Function                    | Returns:                                                      |
| --------------------------- | ------------------------------------------------------------- |
| len(`str`)                  | The length of the string                                      |
| `str`.upper()               | The string with all the letters in uppercase                  |
| `str`.lower()               | The string with all the letters in lowercase                  |
| `str`.title()               | The string with each word capitalized                         |
| `"separator"`.join(`str`)   | The string with `"separator"` inserted between each character |
| `str`.split(`"x"`)          | A list where the string is split everywhere that `"x"` occurs |
| `str`.replace(`"a"`, `"b"`) | The string where every `"a"` is replaced with `"b"`           |

#### String interpolation

Python provides f-strings (as of python 3.6) to insert a variable's value into a string:

```python
visitor_name = "Sam"
visitor_count = 7
welcome_message = f"Hello {visitor_name}, you are visitor number {visitor_count} today!"
print(welcome_message) # prints: "Hello Sam, you are visitor number 7 today!"
```

Alternatively, for python 3.5 and below, there is the format() method:

```python
visitor_name = "Sam"
visitor_count = 7
welcome_message = "Hello {}, you are visitor number {} today!".format(visitor_name, visitor_count)
print(welcome_message) # prints: "Hello Sam, you are visitor number 7 today!"
```

## Lists

A list is a collection of items indexed by integers. Lists are mutable and they can even contain mixed types.

```python
numbers = [5, 2, 5, 3, 1, 8]
words = ["home", "airplane", "blue", "cycling"]
things = [7, "word", 5.2, False]
```

Note: `List` is built into Python. Arrays are also supported though they must be imported (Ex: `import array`). Lists and arrays work in the same way with a few distinctions.

### List functions

These are a few commonly used list functions on some `list`: (Note that the `[]` brackets should not be typed and denote that the enclosed parameter(s) is optional.)

| Function                          | Result                                                                                                |
| --------------------------------- | ----------------------------------------------------------------------------------------------------- |
| len(`list`)                       | Returns the length of the list                                                                        |
| del(`list`[`i`])                  | Removes the item at position `i` of the list                                                          |
| `list`.append(`x`)                | Adds the item `x` to the end of the list                                                              |
| `list`.insert(`i, x`)             | Inserts the item `x` at the `i` index of the list                                                     |
| `list`.extend(`iterable`)         | Extends the list by appending all the items in `iterable`                                             |
| `list`.index(`x[, start[, end]]`) | Returns the first index of the item `x` in the list. (Or within the `start` to `end` indices.)        |
| `list`.count(`x`)                 | Returns the number if times the item `x` appears in the list                                          |
| `list`.remove(`x`)                | Removes the first item `x` in the list                                                                |
| `list`.pop(`[i]`)                 | Removes the last item of the list and returns it. (Or removes the item at index `i`, and returns it.) |
| `list`.clear()                    | Removes all items from the list                                                                       |
| `list`.reverse()                  | Reverses the items of the list                                                                        |
| `list`.copy()                     | Returns a copy of the list                                                                            |

### Slicing

Slicing refers to accessing parts of a sequential data type, such as tuples, strings, ranges, and lists.

Slicing operator syntax example:

```python
list[start:end:step]
```

| Operation            | Returns                                     |
| -------------------- | ------------------------------------------- |
| `list`[`start:stop`] | Items from `start` to `stop - 1`            |
| `list`[`start:`]     | Items from `start` to the end of the list   |
| `list`[`:stop`]      | Items from the beginning through `stop - 1` |
| `list`[`:`]          | A copy of the whole list                    |
| `list`[`::2`]        | Every 2nd item of the list                  |
| `list`[`::-1`]       | A copy of the list in reverse               |
| `list`[`-1`]         | The last item in the list                   |
| `list`[`-2:`]        | The last two items in the list              |

Note: You can use the `slice()` function to achieve the same results.

```python
list[start:stop:step]
# or
list[slice(start, stop, step)]
```

### Ranges

The `range()` function produces a range object. A range can be converted to a list.

```python
zero_to_ten = list(range(11))
# result: [0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
```

Range can also have a start, stop (stop - 1), and step just like slices.

```python
list(range(0, 100, 20))
# result: [0, 20, 40, 60, 80]
```

### List comprehensions

List comprehensions are used to return a new list with transformed values.

Syntax:

```python
[operation for item in list]
```

With if condition:

```python
[operation for item in list if condition]
```

With if/else condition:

```python
[operation if condition else other_operation for item in list]
```

Example: Given a list of integers, make a new list where each number is squared.

```python
squared = [x ** 2 for x in range(10)]
# result: [0, 1, 4, 9, 16, 25, 36, 49, 64, 81]
```

## Loops

### For

For loop example:

```python
for w in words:
    print(w)
```

For loop with enumeration example:

```python
for i, w in enumerate(words):
    print((i, w))   #(i, w) is a tuple, an immutable collection
```

For loop with range example:

```python
for n in range(2, 10):
    print(n)
```

### While

While loop example:

```python
i = 0

while i < 9:
    print(i)
    i += 1
```

While/else example:

```python
i = 0

while i < 9:
    print("Working...")
    i += 1
else:
    print("Done")
```

## Control flow

### If/else statements

If/else conditions are marked with a `:`. Python uses `elif` as the keyword for "else if". The else block following an if/elif is optional.

If/else syntax example:

```python
if x == y:
    print(f"{x} and {y} are equal")
elif x > y:
    print(f"{x} is greater")
else:
    print(f"{y} is greater")
```

### Boolean operators

Python supports all the standard boolean comparison operations (`==`, `!=`, `<`, `>`, `<=`, `>=`).

The keywords `and`, `or`, and `not` are used to evaluate boolean expressions.

Example:

```python
print(not True) # prints: False

print(9 != 5 or 3 < 6) # prints: True
```

### Checking for empty lists

Empty lists evaluate to False, to check if a list is empty:

```python
todo_list = []

if len(todo_list) == 0:
  print("The list is empty!")

# equivalent
if not todo_list:
    print("The list is empty!")
```

To iterate a list:

```python
for item in list_of_things:
   print(item)
```

Comparing items across lists:

```python
shopping_list = ["bread", "ham", "bacon", "cheese"]
daily_specials = ["bacon", "steak", "turkey"]

for item in shopping_list:
    if item in daily_specials:
        print(f"There's a sale on {item}!")
```

## Functions

Functions are defined using the `def` keyword, use indentation instead of braces for the body of the function.

### Defining functions

The syntax examples for defining a function:

```python
def function_name():
    print("Inside a function")
```

### Passing parameters

Syntax examples for functions that take parameters:

```python
def greet(person_name):
    return f"Hi {person_name}!"

# Function call:
greet("Nancy")
```

Functions can take an arbitrary number of arguments using the `*` operator:

```python
def greet(*people):
    for person in people:
        print(f"Hi {person}!")

# sample call with multiple arguments:
greet("Alice", "Wendy", "Ben", "Jerry")
```

Default values can be specified for parameters:

```python
def favorite_menu_item(menu_item="house specialty"):
    print(f"My favorite food here is the {menu_item}!")

# sample call:
favorite_menu_item("steak and potatoes")
favorite_menu_item() # defaults to "house specialty"
```

### Passing lists to functions

Lists are passed directly into functions.

```python
numbers_list = [1, 2, 3]

def insert_hundreds(some_list):
    some_list.extend([100, 100, 100])

insert_hundreds(numbers_list)
print(numbers_list) # numbers_list is now [1, 2, 3, 100, 100, 100]
```

To work with the list without modifying the source, pass a copy of the list when calling the function.

```python
another_list = [1, 2, 3]
insert_hundreds(another_list[:])
print(another_list) # another_list is still [1, 2, 3]
```

## Classes

In python, class variables are called attributes. Class functions are called methods.

Every method definition requires a `self` parameter and it must come before any other parameter. Self is the reference to the instance itself. When calling a method, self is passed automatically and does not need to be written in the call.

Class syntax:

```python
class Car:

    def __init__(self, make, model, driver_name=None):
        self.make = make
        self.model = model
        self.driver_name = driver_name

    def drive(self):
        if self.driver_name is None:
            print(f"The {self.make} {self.model} is safely parked.")
        else:
            print(f"{self.driver_name} drove away in the {self.make} {self.model}.")
```

# Data Types

Data types in Python link values (or data) with methods that define what operations can be performed on this data. The choice of a data type determines what actions are possible and how they are implemented.

Python offers many different data types. To begin, we will focus on two fundamental types: **Numbers** and **Strings**.

## Numbers

Working with numbers in Python is very intuitive and behaves similarly to a calculator. Python differentiates between **Integers** (`int`) and **Floats** (from the term "floating point number"). **Integers** are whole numbers (e.g., `5`), while **Floats** are decimal numbers (e.g., `5.01`).

Note: Floats are not exact representations of real numbers due to rounding performed by computers for floating-point numbers.

### Examples:

```python
>>> 5
5

>>> 5.01
5.01
```

Handling signs:
```python
# Positive
+5  # 5

# Negative
-5  # -5
```

And basic arithmetic operations work as expected:
```python
# Addition
5 + 7  # 12

# Subtraction
5 - 7  # -2

# Multiplication
5 * 7  # 35

# Division
5 / 2  # 2.5
```

**Note**: Division in Python always returns a `float`, even if the result is a whole number:

```python
print(type(5 / 1))
```

Output:
```
<class 'float'>
```

This example also shows that you can check the data type in Python using `type()`.

### Advanced Arithmetic Operations:
```python
# Integer Division
5 // 2  # 2

# Modulo (remainder of a division)
5 % 2  # 1

# Exponentiation
10 ** 2  # 100
```

## Combining Print Statements and Arithmetic Operations

Multiple arithmetic operations can be chained and displayed using the `print()` function:
```python
print(22 * 27 * 7 / 2)
```

Output:
```
2079.0
```

Parentheses can also be used:
```python
print((22 * 27 + 12) / 2)
print(22 * 27 + 12 / 2)
```

Output:
```
303.0
600.0
```

Parentheses can also improve code readability, even when they are not mathematically necessary:
```python
print((22 * 27 * 7) / 2)  # perfectly fine!
```

Other common number operations:
```python
# Integer Division
5 // 2  # 2 (this is NOT the same as rounding!)

# Modulo
5 % 2  # 1

# Exponentiation
10 ** 2  # 100
```

## Strings

Strings are sequences of characters and are defined using either `'` or `"`.

```python
>>> "5 + 7"
'5 + 7'
```

```python
>>> "Whatever you want to type. 123*..."
'Whatever you want to type. 123*...'
```

### Quiz: Which of the following statements does NOT return an error?
```python
>>> "five" + "five"

>>> "five" + 5

>>> 2 * "five"

>>> "five" - "ive"
```
(Try them out!)

### Basic String Operations
Python provides a variety of functions for processing strings. Here are some basic examples:

Strings can be concatenated (added together):
```python
print("Take this!" + " And that!")
```

Output:
```
Take this! And that!
```

However, strings and numbers cannot be concatenated without explicit conversion:
<!--pytest-codeblocks:expect-error-->
```python
"100" + 5  # => TypeError
```

That makes sense. But wait! How does Python know whether something is an `integer (int)`, a `float`, or a `string (str)` if we haven’t defined it anywhere?

## Duck Typing

Python uses a principle called **duck typing**, where the data type is assigned automatically based on the given values (unless explicitly defined otherwise). Duck typing is named after an old saying:

*"When I see a bird that walks like a duck and swims like a duck and quacks like a duck, I call that bird a duck."* ([Wikipedia](https://en.wikipedia.org/wiki/Duck_test#History)).

## Changing Data Types
There are situations where we explicitly want to change a data type, for example, from `float` to `int`:

```python
print(5 + int(7.00001))  # 12
```

Output:
```
12
```

Be careful! This is not rounding but truncating the decimal part:
```python
>>> int(12.9)
12
```

(If rounding is needed, use `int(round(12.9))`.)

Numbers can also be created from strings:
```python
>>> 5 + int("19")
24
```

But don’t expect magic here. Python only recognizes obvious numbers in strings, not something like:
<!--pytest-codeblocks:expect-error-->
```python
int("seven")  # => ValueError: invalid literal for int() with base 10: 'seven'
```

Conversely, we often want to convert a number into a string:
```python
>>> str(5) + "19"
'519'
```

This is frequently done to output a string:
```python
print("7 + 5 = " + str(7 + 5))
```

Output:
```
7 + 5 = 12
```

A more common and convenient way to combine strings and numbers is using **f-strings**. These are marked with `f"..."` before the quotation marks. Within f-strings, values—whether numbers, strings, or other data types—are automatically converted to strings if placed inside curly braces. For example:

```python
print(f"This is {8} times better than that.")
```

Output:
```
This is 8 times better than that.
```

We’ll use this frequently in practice.
```
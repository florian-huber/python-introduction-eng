# Special Functions

We’ve already looked at functions in Python. As a reminder:  
Functions are defined using `def`. Functions must be called to be executed by the interpreter. They can theoretically take any number of parameters (or arguments). Functions return variables using `return` and terminate execution at that point. If no explicit `return` statement is provided, a function returns `None`.  

Below, we’ll briefly cover some special types of functions.

---

## Recursive Functions

Recursive functions are functions that call themselves.  
A classic example is calculating factorials.  

Recall: The factorial of *n* is the product of all whole numbers from 1 to *n*.  
For example, the factorial of four is:  
`4! = 1 * 2 * 3 * 4 = 24`

A Python function for this might look like this:

```python
def factorial_recursive(n):
    # Base case: 1! = 1
    if n == 1:
        return 1

    # Recursive case: n! = n * (n-1)!
    else:
        return n * factorial_recursive(n-1)


print(factorial_recursive(6))  # => 720
```

In general, recursive functions are rarely used.  
They often become very slow and inefficient for complex tasks.

---

## Local Functions

Local functions are functions defined **inside another function**.

```python
def outer_function():
    def inner_function():
        pass  # Code for the inner function goes here

    # The main function uses inner_function
    inner_function()
```

Here’s an example of such a function (`double_n_times()`) with a local/inner function (`double_number()`):

```python
def double_n_times(a, n):
    def double_number(number):
        return number * 2

    for _ in range(n):
        a = double_number(a)
    return a

print(double_n_times(5, 10))  # => 5120
```

And an example in the context of string handling (note: `.lower()` is a string method that converts all letters in a string to lowercase):

```python
def greeting(name):
    """Prints a greeting that depends on the given name string."""
    def is_friend(name):
        friends_list = ["tom", "anna", "erik"]
        return name.lower() in friends_list

    # Print greeting
    if is_friend(name):
        print(f"Hi {name}!!")
    else:
        print(f"Hello {name}.")
```

> ### Mini Quiz:  
> What is the output of `greeting("Anna")`?  
> a) Hello Anna.  
> b) False  
> c) Hi Anna!!

```python
greeting("Anna")  # => Hi Anna!!
greeting("Sandra")  # => Hello Sandra.
```

---

### When to Use Local Functions

Local functions make sense as small helper functions if:
- They are not needed by other functions.
- They are called multiple times within the outer function.
- They improve the readability of the outer function.

For example:
```python
def is_friend(name):
    """Return True if name is in friends_list."""
    friends_list = ["tom", "anna", "erik"]
    return name.lower() in friends_list


def greeting(name):
    """Prints a greeting depending on the name string."""
    if is_friend(name):
        print(f"Hi {name}!!")
    else:
        print(f"Hello {name}.")

def goodbye(name):
    """Prints a goodbye depending on the name string."""
    if is_friend(name):
        print(f"Bye {name}!!")
    else:
        print(f"Goodbye {name}.")
```

---

## Functions with Variable Numbers of Parameters

All the functions we’ve seen so far expect a fixed number of parameters. Sometimes, we may want to allow an **open-ended** number of arguments. Python provides `*args` (short for *arguments*) for this purpose:

```python
def multiply_all(*args):
    product = 1
    for num in args:
        product *= num
    print(product)

multiply_all(1, 2, 3, 4)  # => 24
```

### Operators `+=`, `-=`, `*=`, `/=`
Python allows shorthand operations like `+=`, `-=`, `*=`, and `/=`:

```python
a = 5
a += 2  # Equivalent to a = a + 2
a -= 2  # Equivalent to a = a - 2
a *= 2  # Equivalent to a = a * 2
a /= 2  # Equivalent to a = a / 2
```

### Example with `math.prod()`
Instead of manually calculating the product, Python’s `math` library offers a built-in function:

```python
import math

def multiply_all(*args):
    print(math.prod(args))

multiply_all(1, 2, 3, 4)  # => 24
```

---

## `**kwargs`: Variable Numbers of Named Parameters

Analogous to `*args`, Python allows an arbitrary number of **named parameters** using `**kwargs` (short for *keyword arguments*). While this is more commonly used in advanced programming, here’s an example:

```python
def guess_the_animal(**kwargs):
    """Provide hints as key-value pairs for guessing an animal."""
    print("Hi! Can you guess what animal I mean?")
    for key, value in kwargs.items():
        print(f"{key}: {value}")


guess_the_animal(legs=4, color="gray", weight="5000 kg") 
# Output:
# Hi! Can you guess what animal I mean?
# legs: 4
# color: gray
# weight: 5000 kg
```

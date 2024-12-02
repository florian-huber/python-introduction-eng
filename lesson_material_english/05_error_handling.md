# Error Handling

By now, everyone has likely encountered a Python error or two...

For example:
<!-- pytest-codeblocks:expect-error -->
```python
print(this)  # => NameError: name 'this' is not defined
```

or:
<!-- pytest-codeblocks:expect-error -->
```python
else = 5  # => SyntaxError: invalid syntax
```

or:
<!-- pytest-codeblocks:expect-error -->
```python
open("nonexistent_file")  # => FileNotFoundError: [Errno 2] No such file or directory: 'nonexistent_file'
```

or:
<!-- pytest-codeblocks:expect-error -->
```python
5 / 0  # => ZeroDivisionError: division by zero
```

Some errors, such as `else = 5`, indicate genuine mistakes in the code that need to be corrected (and luckily Python prevents this). However, errors can also occur during program execution and aren't always a reason to stop the entire program.

```python
def divider(number, divide_by):
    """Divides 'number' by 'divide_by'.
    
    Returns None for division by zero.
    """
    if divide_by == 0:
        return None
    return number / divide_by

print(divider(5, 0))
```

The issue: Not all errors are as easily anticipated. A better approach is to **catch** errors using Python's `try: except` mechanism:

```python
try:
    print(this)
except:
    print("The program continued running...")
```

Or like this:

```python
try:
    print(this)
except Exception as error:
    print(error)
print("The program continued running...")
```

Back to the `divider` function:

```python
def divider(number, divide_by):
    """Divides 'number' by 'divide_by'.
    
    Returns None for division by zero.
    """
    try:
        return number / divide_by
    except ZeroDivisionError:
        return None

print(divider(5, 0))
```

> ### Mini Quiz:
> What happens if the function is called with:
> `print(divider("text", 2))`
>  
> a) None  
> b) te  
> c) TypeError  

---

### Common Error Types

+ **IOError** – For example, when a file cannot be opened.
+ **ImportError** – When a Python module cannot be found or loaded.
+ **ValueError** – When a function receives an argument of the correct type but with an invalid value.
+ **TypeError** – When a function receives an argument of an invalid type.
+ **KeyboardInterrupt** – When the user interrupts execution using the keyboard (e.g., `Ctrl+C`).

---

Sometimes, we intentionally want to raise errors. This can be done using `raise`:

<!-- pytest-codeblocks:expect-error -->
```python
raise Exception("Something went wrong")
```

Or:

<!-- pytest-codeblocks:expect-error -->
```python
x = "hello"

if not isinstance(x, int):
    raise TypeError("Only integers are allowed")
```

---

## `assert`

Often, it’s simpler to use the `assert` keyword to handle such cases:

<!-- pytest-codeblocks:expect-error -->
```python
selected_number = "hello"
assert isinstance(selected_number, int), "Expected an integer"
```

Example:

```python
def hour_to_am_pm(hour):
    """Convert a 24-hour time to 12-hour clock format."""
    assert 0 <= hour <= 24, "Hour must be between 0 and 24"
    
    if 1 <= hour <= 12:
        print(f"{hour} a.m.")
    elif hour == 0:
        print("12 a.m.")
    else:
        print(f"{hour - 12} p.m.")


hour_to_am_pm(13)  # => 1 p.m.
```

If the input doesn't meet the conditions, an assertion error is raised:

<!-- pytest-codeblocks:expect-error -->
```python
hour_to_am_pm(25)  # => AssertionError: Hour must be between 0 and 24
```
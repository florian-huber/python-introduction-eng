# String Handling
## (String Processing)

Strings are one of the most frequently used data formats in Python, alongside numeric data types. They are essential when dealing with text input, filenames, comments, text-based searches, text files, etc.

At the start of the lecture, we encountered some basic string operations:

```python
print("this" + "that")
print(10 * "?")
```

Strings are sequences in Python, which means sequence methods can be used on them, such as:

```python
print("that" in "thatsame")  # => True
print("x" not in "abcdefg")  # => True
```

Slicing works on strings as well:

```python
print("Yes No"[:2])  # => Yes
```

> ### MINI QUIZ:
> Quick review: What does the following command output?
```python
s = "all good"
print(len(s))
```
> a) ValueError  
> b) 8  
> c) 9  
> d) all good  

> And this one?  
```python
s = "nothing is good!"
print(s[-7:])
```
> a) is good!  
> b) sthcin  
> c) ValueError  

---

## Escape Characters - Fix the String

Some characters or character combinations are interpreted specially by Python. For example, the following would raise an error:

<!-- pytest-codeblocks:expect-error-->
```python
print("This says "Stop"!")  # => SyntaxError: invalid syntax
```

This can be fixed using different quotation marks:

```python
print('This says "Stop"!')  # => This says "Stop"!
```

Alternatively, escape sequences using a backslash (`\`) can resolve such issues:

```python
print("This says \"Stop\"!")  # => This says "Stop"!
print("A backslash looks like this: \\")
```

Paths on Windows, for example, often require double backslashes for this reason:

```python
path = "C:\\User\\Desktop\\"
filename = path + "testfile.txt"
```

Escape sequences can also insert special characters, such as `\n` for a newline:

```python
print("With this, we can write long \n texts across lines.")
```

---

## String Methods

Python provides a wide range of string methods. Let’s cover the most important ones.

When unsure of the appropriate method, refer to resources like the [Python Documentation](https://docs.python.org/3.9/library/index.html) or [w3schools.com](https://www.w3schools.com/python/default.asp).

### Table of String Methods

| **Method**      | **Description**                                                                 |
|------------------|---------------------------------------------------------------------------------|
| `count()`        | Counts occurrences of a specified value in a string                            |
| `encode()`       | Returns an encoded version of the string                                       |
| `endswith()`     | Returns True if the string ends with the specified value                       |
| `index()`        | Returns the position of a specified value                                      |
| `islower()`      | Returns True if all characters are lowercase                                   |
| `isupper()`      | Returns True if all characters are uppercase                                   |
| `join()`         | Joins elements of an iterable to the end of the string                         |
| `lower()`        | Converts the string to lowercase                                               |
| `strip()`        | Removes leading and trailing whitespace (or specified characters)             |
| `replace()`      | Replaces a specified value with another value in the string                   |
| `split()`        | Splits the string at a specified separator and returns a list                 |
| `startswith()`   | Returns True if the string starts with the specified value                    |
| `upper()`        | Converts the string to uppercase                                               |

---

### `.replace()`

To replace specific characters, words, or substrings, use `.replace()`:

```python
s = "Sometimes we dislike some characters"
s.replace("i", "!")
print(s)  # => Nothing happens?
```

String methods do not modify the original string but return a new one:

```python
s_new = s.replace("i", "!")
print(s_new)
```

You can chain multiple method calls:

```python
print(s.replace("i", "!").replace("e", "3"))
```

> ### Mini Quiz!
> What does the following command output?
```python
print("abc".replace("ab", "cc").replace("c", "x"))
```
> a) ccx  
> b) ab  
> c) xxx  
> d) abx  

---

### `.upper()` and `.lower()`

These methods handle case transformations. For example:

```python
tweet = "this is unfair"
tweet_trumpified = tweet.upper() + "!"
print(tweet_trumpified)  # => THIS IS UNFAIR!
```

And back to lowercase with `.lower()`:

```python
tweet_moderated = tweet_trumpified.lower()
print(tweet_moderated)
```

To standardize user input:

```python
entry1 = " Muster, Markus. "  # Contains whitespace and a period
entry2 = "Test, Trude   "  # Extra whitespace
```

Use `.strip()` to remove leading and trailing whitespace (or other characters):

```python
print(entry1.strip())
print(entry2.strip())
```

---

### Splitting Strings

To split strings into smaller, meaningful parts, use `.split()`. For example:

```python
name = "Muster, Markus"
pieces = name.split(",")  # Splits the string at each ','
print(pieces)
```

Or:

```python
sentence = "Many sentences have many words, sometimes even punctuation!"
words = sentence.split(" ")
print(words)
print(f"This sentence has {len(words)} words.")
```

You can combine `.replace()` with `.split()` for further processing:

```python
sentence = "Many sentences have many words, sometimes even punctuation!"
sentence_cleaned = sentence.replace(",", "").replace("!", "").replace(".", "")
words = sentence_cleaned.split(" ")
print(words)
print(f"This sentence has {len(words)} words.")
```

---

### String Queries

Python provides several ways to query strings:

#### `.startswith()` and `.endswith()`
```python
s = "name: Markus"
s.startswith("name:")  # => True
s.endswith(".")  # => False
```

#### `.count()` Counts occurrences of a substring:
```python
s = "Most texts have some 'e's."
print(s.count("s"))  # => 3
print(s.count("te"))  # => 2
print(s.count("Te"))  # => 1
```

#### `.index()` Finds the position of the first occurrence:
```python
index_te = s.index("te")
print(f"Position in string: {index_te}")
print(s[index_te])
```

---

### Encodings (Character Encodings)

Characters are stored on computers using encodings. The most common is **Unicode**, particularly `utf-8`. Another older standard is **ASCII**.

For now, this is primarily informational. If you encounter a `UnicodeDecodeError` while working with strings, remember this topic as a starting point for troubleshooting.
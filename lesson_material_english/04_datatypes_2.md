# Data Types II

We’ve already encountered several data types. Now, let’s take a closer look and discuss additional important types. Let’s begin with a quick review.

It’s crucial to understand that variables in Python don’t contain the data/values directly. They are simply names linked to the memory location where the value is stored.

This explains why the following happens:

```python
a = [5]
b = a
b.append(4)
print(a)
```

---

## Review of Data Types We’ve Worked With

### Numbers

We’ve frequently used integers and floats (floating-point numbers):

```python
type(6)  # => int
type(6.0)  # => float
```

We haven’t discussed complex numbers yet, but for completeness:

```python
type(2j + 3)  # => complex
```

---

### Strings

```python
type("abcdefg")
type('abcdefg')
type("""abcdefg""")  # e.g., in function "docstrings"
```

---

### Lists & Tuples

We’ve already seen lists and tuples, which seem similar at first glance:

```python
my_list = ["abc", "ABC", 5, 0.315]
my_tuple = ("abc", "ABC", 5, 0.315)

print(my_list[-1])
print(my_tuple[-1])
```

However, their behavior differs significantly!

- **Lists (`list`)** are mutable and come with many methods/functions:

```python
my_list = ["abc"]

my_list.append("something else")
my_list.insert(1, "xyz")
my_list[2] = "XYZ"
print(my_list)  # => ['abc', 'xyz', 'XYZ']
```

---

### Boolean and None

We’ve seen these types without discussing them as separate data types:
- **Boolean (`bool`)**: Can only be `True` or `False`.
- **NoneType (`None`)**: Represents the absence of a value or object.

---

## Sets and Dictionaries

Python includes two additional widely used data types: **sets** and **dictionaries**.

---

### Sets

```python
my_set = {"yes", "no", "maybe"}
```

At first glance, sets may resemble tuples or lists. However, consider this:

```python
my_set[0]  # => TypeError: 'set' object is not subscriptable
```

**Sets are not sequences!** Elements have no indices. Other operations (e.g., membership tests) still work:

```python
"maybe" in my_set  # => True
```

Even a `for`-loop works:

```python
for s in my_set:
    print(f"Well, {s}...")
```

The differences between sets and lists align with their usage in everyday language or mathematics. For instance:

```python
animals = {"cat", "dog", "elephant", "lion", "dog"}
print(animals)  # => {'cat', 'dog', 'elephant', 'lion'}
```

---

#### Combining Sets

When combining sets, duplicates are automatically removed. Operations include:

- **Union** (`A ∪ B`):

```python
animal_set1 = {"cat", "dog", "elephant", "lion"}
animal_set2 = {"parrot", "cat", "dog", "goldfish", "cow"}

all_animals = animal_set1.union(animal_set2)
print(all_animals)
```

- **Intersection** (`A ∩ B`):

```python
most_popular = animal_set1.intersection(animal_set2)
print(f"Named twice: {most_popular}")
```

> Mini Quiz: What animals are output here?  
> a) {'parrot', 'goldfish', 'cow'}  
> b) {'cat', 'dog'}  
> c) {'elephant', 'lion'}  
> d) {}

- **Symmetric Difference**:

```python
named_once = animal_set1.symmetric_difference(animal_set2)
print(f"Named once: {named_once}")
```

---

### Dictionaries

Dictionaries allow data to be stored as key-value pairs:

```python
my_dict = {"Hallo": "hello",
           "Tschüss": "bye",
           "Danke": "thanks"}

print(my_dict["Danke"])  # => thanks
```

Keys must be unique:

```python
my_dict = {"Hallo": "hello",
           "Hallo": "hi"}
print(my_dict["Hallo"])  # => 'hi'
```

---

#### Modifying Dictionaries

Dictionaries are mutable. Entries can be added, removed, or modified:

```python
my_dict["password"] = "prettyfl0wer"
my_dict["hair color"] = "blond"
print(my_dict)
```

Check for a specific key:

```python
print("password" in my_dict)  # => True
```

Retrieve all keys, values, or key-value pairs:

```python
print(my_dict.keys())
print(my_dict.values())
print(my_dict.items())
```

---

### Nested Dictionaries

Dictionaries can also contain other dictionaries, enabling more complex data structures:

```python
hogwarts = {
    "Dumbeldore": {"surname": "Albus", "function": "headmaster"},
    "Lockhart": {"surname": "Gilderoy", "function": "teacher"},
    "Granger": {"surname": "Hermione", "function": "pupil"}
}

print(hogwarts["Granger"]["surname"])  # => Hermione
```

---

## Copying Objects: `=`, `copy()`, `deepcopy()`

### Shallow Copy (`copy()`)

A shallow copy only duplicates the top-level structure:

```python
hogwarts = {"Dumbeldore": {"surname": "Albus", "function": "headmaster"}}
hogwarts_copy = hogwarts.copy()
hogwarts_copy["Dumbeldore"]["function"] = "former headmaster"

print(hogwarts["Dumbeldore"]["function"])  # => former headmaster
```

---

### Deep Copy (`deepcopy()`)

For nested objects, use `deepcopy()`:

```python
import copy

hogwarts = {"Dumbeldore": {"surname": "Albus", "function": "headmaster"}}
hogwarts_copy = copy.deepcopy(hogwarts)
hogwarts_copy["Dumbeldore"]["function"] = "former headmaster"

print(hogwarts["Dumbeldore"]["function"])  # => headmaster
```
```python
my_list1 = [[1, 2, 3], 12, 15]
my_list2 = copy.deepcopy(my_list1)

my_list2[0][0] = 54321
print(my_list1[0])  # => [1, 2, 3]
```
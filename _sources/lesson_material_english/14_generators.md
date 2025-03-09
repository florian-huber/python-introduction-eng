# Generators / Iterators

Let's start with a short quiz question:

When a Pandas DataFrame has been created (e.g. by importing a.csv file with `read_csv()`), where are the values of the DataFrame stored?
>
> (a) In the folder I am currently working in.
> (b) In a temporary folder on the hard disk.
(c) In the main memory.
(d) In the processor memory (cache).

For those who are a little familiar with the structure of a computer, this is easy to answer. And yet it was not an issue for us when programming with Python. However, this is becoming increasingly important for further steps. The data, like all variables that we create in the Python interpreter, is stored in the main memory. This is good and right and has not been a problem that we had to worry about so far.

However, the more we look at really big data, the more important this topic will become. This is because the main memory is fast, but very limited in scope. This means that in many cases, it can lead to problems if we want to store too much data in the main memory at the same time.

One way to deal with this better is to use generators. These offer the possibility to only load (or generate) as much data as is currently needed. But before we get to generators, let's start with a more general variant, the iterator.

## Iterators

In Python, iterators are objects that can iterate through a sequence of values. They make it possible to iterate over a series of elements in a for loop without having to know the exact number of elements in advance. An iterator object must implement the iterator protocol, which defines the **iter**() and **next**() methods.

The **iter**() method returns the iterator object itself and is called automatically when a for loop is started. The **next**() method returns the next element in the sequence and is called automatically when the for loop requests the next element. If there is no next element, a StopIteration exception is raised.

An example of how to use iterators is to use the built-in `iter()` function on a list or tuple:

```python
numbers = [1, 2, 3, 4, 5]
iterator = iter(numbers)
print(next(iterator)) # 1
print(next(iterator)) # 2
print(next(iterator)) # 3
```

In this example, the iter() function is used to create an iterator for the numbers list. The iterator is stored in the variable iterator. The next() function is used to query the next element in the iterator, which is then output.

### What's the point?

At first glance, it may not be immediately clear what the iterator concept brings to this example. After all, we could just as easily use a for loop for this:

```python
numbers = [1, 2, 3, 4, 5]
for number in numbers:
    print(number)
```

An iterator is not really useful if you just want to replace a for loop. However, it offers the possibility of extracting individual elements and also remembers where we left off. The real added value of iterators becomes particularly apparent with so-called generators.

## Generators

Generators (generators) are special iterators that are created in Python using the yield statement. They make it possible to create an iterator without having to store the entire sequence in memory. Instead, only the values that are currently needed are created. This makes generators particularly useful for processing large amounts of data or for processing infinite sequences.

In Python, generators are easy to create and are defined almost exactly like we have been defining functions, with the important exception that we use `yield` instead of `return`.
The expression `yield`, just like return, returns values when it is reached in the code. Unlike `return`, however, a function call does not end at the `yield` but continues with the following call after it (e.g. via a `next()`). Here is a short example:

```python
# A simple generator function
def my_generator():
    n = 1
    print('This is printed first')
    # Generator function contains yield statements
    yield n

    n += 1
    print('This is printed second')
    yield n

    n += 1
    print('This is printed at last')
    yield n

a = my_generator()
next(a)
```

### Example: city name generator

Let's imagine we want to generate a large number of city names (e.g. for a game). We can do this in the usual way with:

```python
import numpy as np

def city_name_generator():
    beginnings = [“Upper”, “Lower”, “Old”, “New”, “Small”, “King”, “Gold”]
    middle = [“river”, “lake”, “forest”, “meadow”],
    endings = [“house”, “home”, “engine”, “village”, “town”, “brook”]
    return np.random.choice(beginnings) + np.random.choice(middle) + np.random.choice(endings)

for _ in range(10):
    print(city_name_generator())
```

But this only gives me random combinations, so there may be a lot of duplicates. 

How can we turn this into a real Python generator?
One possibility would be as follows:

```python
def city_name_generator():
    beginnings = [“Ober”, “Unter”, “Alt”, “Neu”, “Klein”, “Königs”, “Gold”]
    middle = [“”, “stream”, “lake”, “forest”, “meadow”, “”, “”]
    endings = [“house”, “home”, “engine”, “village”, “town”, “brook”]
    for a in beginnings:
        for b in middle:
            for c in endings:
                yield a + b + c

city = city_name_generator()
for _ in range(10):
    print(next(city)) 
```

But also by using `list()` to convert all elements into a list:

```python
# create a new instance of the generator to start with beginning
city = city_name_generator()
all_cities = list(city)
```

### Infinite sequences

Another use case for generators is infinite sequences. Here is a simple example:

```python
def all_seventh():
    n = 0
    while True:
        yield n
        n += 7

seventh = all_seventh()
print(next(seventh))
```

With each `next()`, the generator goes through the series of sevens for as long as we want. However, only the requested elements are calculated, making the generator very efficient here.

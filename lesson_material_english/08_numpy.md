# Numerical Data in Python with NumPy

`NumPy` is arguably the most important Python library for working with (numerical) data. The name itself comes from **Num**erical **Py**thon. NumPy introduces not only a central new data type, the **NumPy array**, but also a wide range of functions and methods for working with vectors, matrices, and tensors.

NumPy often simplifies coding tasks and is optimized for computational speed, as its core methods are implemented using compiled C libraries.

Let’s start with an example.

Imagine we’ve collected survey data. Participants rated how much they agreed with various statements on a scale from 1 (not at all) to 5 (completely). The data is imported into Python as lists, and we want to compare the answers of two participants. Specifically, we calculate the difference in values at corresponding positions. Using Python lists, we might code it as follows:

```python
survey_person1 = [2, 3, 5, 4, 5, 2, 1, 3, 4, 4, 3]
survey_person2 = [4, 4, 2, 2, 4, 4, 3, 1, 5, 4, 2]

survey_diffs = []
for i in range(len(survey_person1)):
    survey_diffs.append(survey_person1[i] - survey_person2[i])
    
print(survey_diffs)

# Now calculate the absolute differences --> abs()
print([abs(x) for x in survey_diffs])
~~~

With NumPy, this task is much simpler:

```python
import numpy as np

survey_person1 = np.array([2, 3, 5, 4, 5, 2, 1, 3, 4, 4, 3])
survey_person2 = np.array([4, 4, 2, 2, 4, 4, 3, 1, 5, 4, 2])

print(survey_person1 - survey_person2)
print(abs(survey_person1 - survey_person2))
```

Here, we immediately used NumPy’s central data type: NumPy arrays!

```python
print(type(survey_person1))  # => <class 'numpy.ndarray'>
```

------

## Creating NumPy Arrays

NumPy arrays can be easily created from Python lists:

```python
import numpy as np

a = np.array([2, 5.9, 7.7, 100.0])
b = np.array([[2, 4, 7],
              [3, 5, 11]])

print(a)
print(b)
```

NumPy arrays differ from lists in several key ways:

- All elements must have the same data type (e.g., all floats or integers). NumPy supports a wide range of numerical data types ([NumPy data types](https://numpy.org/doc/stable/user/basics.types.html)).
- For tables/matrices/tensors, all rows must have the same number of elements (unlike nested lists in Python).
- Python dynamically adjusts the memory allocation for numbers, while NumPy arrays allocate fixed memory for each number (e.g., all entries as `int64` or `float64`).

------

## Getting Information About NumPy Arrays

You can query the following properties of a NumPy array:

- **Data type**: `.dtype`
- **Shape** (rows, columns): `.shape`
- **Total number of elements**: `.size`
- **Number of dimensions**: `.ndim`

```python
import numpy as np

b = np.array([[2, 4, 7],
              [3, 5, 11]])

print("Matrix shape:", b.shape)
print("Total number of elements:", b.size)
print("Matrix dimensions:", b.ndim)
print("Data type:", b.dtype)
```

------

## Slicing and Indexing

NumPy arrays support slicing and indexing, similar to Python lists, but with additional features:

```python
import numpy as np

matrix_list = [[1, 2, 3],
               [4, 5, 6],
               [7, 8, 9]]

print(matrix_list[1])
print(matrix_list[1][2])

matrix = np.array([[1, 2, 3],
                   [4, 5, 6],
                   [7, 8, 9]])

print(matrix[1])
print(matrix[1][2])
```

> Mini-Quiz: What is the value of `matrix[1][2]`?

NumPy also supports **multi-indexing** for simpler syntax:

```python
print(matrix[1, 2])

# Other slicing options:
print("First row:", matrix[0, :])
print("Last column:", matrix[:, -1])
print("Lower-right corner:", matrix[1:, 1:])
```

NumPy arrays allow advanced indexing using lists, arrays, or Boolean masks:

```python
indices = [2, 0, 2, 0]
print(matrix[indices])

# Boolean mask
mask = [True, False, True]
print(matrix[mask])
```

------

## Mathematical Operations on Arrays

NumPy arrays support element-wise operations:

```python
import numpy as np

numbers = np.array([4, 5, 2, 3, 1, 5, 5, 2])
print(numbers - 5)

other_numbers = np.array([2, 5, 1, 1, 4, 3, 4, 3])
print(numbers - other_numbers)
```

The same applies to other operations:

```python
numbers = np.array([4, 5, 2, 3, 1, 5, 5, 2])
print(numbers * 5)

other_numbers = np.array([2, 5, 1, 1, 4, 3, 4, 3])
print(numbers * other_numbers)
```

------

## Useful NumPy Methods

NumPy provides many methods for numerical and statistical operations. For example, `.sum()` calculates the sum of all elements:

```python
import numpy as np

matrix = np.array([[1, 2, 3],
                   [4, 5, 6],
                   [7, 8, 9]])

print(matrix.sum())
print(np.sum(matrix))
```

You can calculate sums along specific axes:

```python
print(matrix.sum(axis=0))  # Sum of each column
print(matrix.sum(axis=1))  # Sum of each row
```

------

## Creating Arrays

Other ways to create arrays include:

- **Zeros and ones**:

  ```python
  data = np.zeros((3, 4))
  print(data)
  
  data = np.ones((3, 4))
  print(data)
  ```

- **Random values**:

  ```python
  data = np.random.random((3, 4))
  print(data)
  ```

- **Range of values** (`np.arange`):

  ```python
  data = np.arange(-10, 10, 1)
  print(data)
  ```

- **Linearly spaced values** (`np.linspace`):

  ```python
  data = np.linspace(-10, 10, num=10)
  print(data)
  ```

------

## Modifying Arrays

NumPy arrays can be modified like lists:

```python
data = np.array([1, 2, 3, 4, 5, 6, 7, 8])
data[-1] = 12
data[:3] = -1
print(data)
```

Arrays can also be concatenated using `np.concatenate`:

```python
a = np.array([1, 2, 3, 4])
b = np.array([5, 6, 7, 8])

arr = np.concatenate((a, b))
print(arr)
```

For multidimensional arrays, specify the axis:

```python
a = np.array([[1, 2],
              [3, 4]])
b = np.array([[5, 6],
              [7, 8]])

arr = np.concatenate((a, b), axis=0)
print(arr)

arr = np.concatenate((a, b), axis=1)
print(arr)
```

Arrays can also be reshaped or flattened:

```python
data = np.array([1, 2, 3, 4, 5, 6])

data_reshaped = data.reshape(3, 2)
print(data_reshaped)

data_flattened = data_reshaped.flatten()
print(data_flattened)

```

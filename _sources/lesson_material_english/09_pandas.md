**Jupyter Notebooks**

So far, we have either written our Python code in a console (actually only for testing purposes), or mainly in a development environment like Spyder. The latter is and remains the preferred way to develop more extensive code.

However, there is another environment that is very good for working with Python and is particularly suitable for data science tasks and initial explorations of data sets: **Jupyter Notebook**. All the following code examples are therefore also shown in such notebooks.

Jupyter Notebook is part of the Anaconda installation and generates notebook files that end with `.ipynb`. Jupyter Notebook can be started via the start menu (under Anaconda) or by entering the command `jupyter notebook` in the terminal.

The use of Jupyter notebooks will be demonstrated in the lecture and we will also cover it in the next tutorial. Otherwise, there is a lot of material on how to use notebooks on the internet, for example here: https://realpython.com/jupyter-notebook-introduction/.



# Pandas!

Numpy is **the** Python tool when it comes to handling large amounts of data. But for many data science-type tasks, certain things are missing. And that's exactly why there are **Pandas** (which internally uses Numpy arrays, among other things):

- Heterogeneous data types within a table
- Labels
- More options for handling missing values
- More data types

Pandas (the name stands for **Pan**el **Da**ta) is usually imported as follows:

```python
import pandas as pd
```

In Numpy, we mainly dealt with Numpy arrays, the central data type in Numpy.

In Pandas, there are two data types that we will work with: **DataFrame** and **Series**. We start with the former. 

```python
import pandas as pd
import numpy as np

my_dict = {“city”: [“Essen”, “Bochum”, “Dortmund”],
“inhabitants": [591032, 364454, 587696],
“xyz“: np.random.random(3)}

df = pd.DataFrame(my_dict, index=[”a”, ‘b’, ‘c’])
```

Here we have created a DataFrame using a dictionary. The keys are then assigned to the column names and the rows are assigned the desired names via `index`. Alternatively, `index` can also be omitted, in which case Pandas simply numbers the rows with 0, 1, 2...

But how do we actually look at the whole thing now?

In this case, we still have a relatively small table and can simply look at it with `print(df)`. In Jupyter notebook it is even easier and we just enter `df`.

Pandas DataFrames can also be created in many other ways, e.g. from lists:

```python
import pandas as pd
import numpy as np

my_list = [[“Essen”, 591032, np.random.random(1)[0]],
[“Bochum”, 364454, np.random.random(1)[0]],
[“Dortmund”, 587696, np.random.random(1)[0]]]

df = pd.DataFrame(my_list,
columns=[“city”, “inhabitants”, “xyz”],
index=[“a”, “b”, “c”])
```



## Slicing and Indexing

Slicing and indexing, i.e. the targeted “cutting” (slicing) and addressing (indexing) of tables to display only certain data, is one of the central elements when working with large amounts of data. With Numpy, we have already seen how powerful, but also how difficult this can be. In Pandas, there are often even more options and it can quickly become confusing. However, good slicing/indexing skills in Pandas quickly become real superpowers when it comes to data science ;)

OK, but every beginning... 

We have just seen that a dictionary can be converted into a DataFrame. And the contents can also be accessed in a similar way, namely via the column names (either individually or as a list):

<!-- pytest-codeblocks:cont -->

```python
df[“inhabitants”]

cols = [“city”, “inhabitants”]
df[cols]
```

To select certain rows, you can use `.loc`, i.e. `.loc[“a”]` for a single row or a list or range for multiple rows

```python
import pandas as pd
import numpy as np

df = pd.DataFrame({“city”: [“Essen”, “Bochum”, “Dortmund”],
“inhabitants“: [591032, 364454, 587696],
“xyz”: np.random.random(3)},
index=[“a”, “b”, “c”])

df.loc[“a”]

# or via list
rows = [“a”, “c”]
df.loc[rows]

# or via range with :
df.loc[“a”:“b”]

# This can also be combined with columns
df.loc[“a”, [“city”, “inhabitants”]]
```

Alternatively, there is still a way via the indices, namely with `.iloc`, and that suddenly looks like Numpy again:

<!-- pytest-codeblocks:cont -->

```python
df.iloc[0:2]

# or rows and columns
df.iloc[0:2, 1:]
```

Summary:

- `[ ]` to select columns
- `.loc[row_labels, column_labels]` to select elements by their labels (row and column names)
- `.iloc[row_positions, column_positions]` to select elements by their indices

### Adding/Removing Elements

Additional columns can be added to a DataFrame in exactly the same way as for dictionaries:

```python
import pandas as pd
import numpy as np

df = pd.DataFrame({“city”: [“Essen”, “Bochum”, “Dortmund”],
“inhabitants“: [591032, 364454, 587696],
“xyz”: np.random.random(3)},
index=[“a”, “b”, “c”])

df[“height”] = [116, 100, 86]
df
```

The reverse step would be to completely remove a column, which can be done with `del df[“xyz”]`.



### Now: go Data Science

*The following part is probably easier to understand using the corresponding Jupyter Notebook (or to work with it right away!).*

So far, we have only looked at simple examples to get to know the methods of Pandas a little. But the whole thing only gets interesting when we start playing with larger data sets. Of course, what constitutes a “large” data set is relative, but here I mean data that is at least so large that we cannot understand it completely with a quick glance at a table.

For this purpose, we will start working with the “Pokemon Dataset” that can be downloaded from “Kaggle”: https://www.kaggle.com/rounakbanik/pokemon

### Importing data

Loading data from text files is usually quite easy with Pandas, as Pandas provides corresponding functions for this. Among other things, to import CSV or Excel files.


```python
import os

root = os.getcwd()
filename = os.path.join(root, “exercises”, 'pokemon.csv') # adjust according to your own path!

data = pd.read_csv(filename, delimiter=“,”)
# also possible here: data = pd.read_csv(filename) because delimiter=“,” is the “default” parameter

data.head() # or: data.tail()
cols = ['name', 'type1', 'type2', 'speed', 'abilities','attack',
'defense', 'height_m', 'hp', 'weight_kg',
'generation', 'is_legendary']
data_selected = data[cols]
data_selected.head()
```

We can get a first impression of the data (at least the numerical entries) with:


```python
data_selected.describe()
```

After that, we come to the actual core of the Pandas analysis. By combining slicing/indexing and other Pandas methods, various aspects of the data can be explored quickly and effectively.

For example, to see what types of Pokemon there are


```python
data_selected[“type1”].unique()
```

And how many of each type there are:


```python
data_selected[“type1”].value_counts()
```

### How do I get the values now?

Pandas usually returns either a **DataFrame** (table) or a **Series** (a single column with row names). In some cases, however, we only want the actual values from the column (or from the table). For this, Pandas offers the option of outputting a Numpy array with `.values`.


```python
values = data_selected[“type1”].value_counts().values
print(values)
print(type(values))
```

[114 105 78 72 53 52 45 39 32 32 29 28 27 27 24 23 18 3]
<class 'numpy.ndarray'>

## Sorting

Unlike numpy and lists, there is no pandas.sort() method, but two different methods: 

- pandas.sort_index() - sorts by index
- pandas.sort_values() - sorts by column values

Unlike lists, there is no “reverse” parameter, but there is “ascending”, which can be set to False to reverse the sort.


```python
data_selected.sort_values([“speed”, “name”])

# or: data_selected.sort_values([“speed”, “name”], ascending=False)
```



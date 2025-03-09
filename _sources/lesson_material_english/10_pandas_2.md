# Pandas - Part 2

In the first part, we saw how to read a.csv file and explore basic properties. Here, we will take it a few steps further in dealing with (complex) data sets.

## Data cleaning

Data cleaning involves rearranging and processing data with the aim of making it more useful for subsequent analysis. We already took a step in this direction last time by reducing the number of columns to the most important ones.

```python
import pandas as pd
import numpy as np
import os

root = os.getcwd()
filename = os.path.join(root, “my_data_folder”, 'pokemon.csv')

data = pd.read_csv(filename, delimiter=“,”)

cols = [
    'name', 'type1', 'type2', 'speed', 'abilities','attack',
    'defense', 'height_m', 'hp', 'weight_kg',
    'generation', 'is_legendary'
]
data_selected = data[cols]
```

With `data_selected.info()` we can see that some columns do not contain the required 801 entries.

If we look at the table (e.g. with `data_selected.head()`), we see that some entries are called `NaN`. This stands for Not-a-Number and is the Numpy format for missing/unknown entries. 

Pandas offers a range of options for dealing with such missing values. NaNs also exist in Numpy, but we have not explicitly looked at them there. In Numpy, such an entry can be created as `np.nan`.

In Pandas, these can be queried using `.isnull()` or `isna()`, where `.any()` indicates that the value should be True if at least one element is a NaN. Both methods do the same here, although “isnull” is perhaps confusing because it does not indicate whether a value is zero, but only whether a value is not present (NaN --> True).

```python
print(data_selected.isna().any())

print(data_selected.isnull().any())
```

We can now display all columns in which individual values are missing:

```python
data_selected[data.columns[data.isna().any()]]
```

### And now? What to do with NaNs?

Depending on what we want to do with our data, there are different strategies for dealing with missing values. In many cases, we can simply ignore them. If we calculate mean values (`.mean()`) or similar, these values are automatically not counted.

In other cases, we may want to replace the values, e.g. with “0”. But be careful! After that, these values will be counted when calculating sums or averages.

#### Replacing NaN

In Pandas, you can replace values with `.fillna()`:

```python
data_selected.fillna(0).head()
```

But we can also use strings or other formats:

python
data_selected.fillna(“unknown”).head()

If NaN cannot simply be replaced and should not occur in the further steps, then either the corresponding columns or rows must be removed from the table. This can be done in Pandas with `.dropna()`.

```python
data_selected.dropna().head()
```

Or to remove all columns with NaNs:

```python
data_selected.dropna(axis=1).head()
```

### Important:

In Python, there are two options for methods that want to modify “their” object:

1) The object remains unchanged and a modified copy is output via `return`.
2) The object itself is modified.

In the case of Pandas, (1) usually takes place, see also https://pandas.pydata.org/pandas-docs/stable/user_guide/indexing.html#indexing-view-versus-copy.

This means that if we want to receive a modified DataFrame, we have to create it with `=`:

```python
data_na_removed = data_selected.dropna()
data_na_removed.head()
```

## Digging a bit deeper...

Let's take the analysis of the data a step further. What if we want to know more about individual groups?

We can use masks to address specific questions:

```python
mask = data_selected[“type1”] == “bug”
data_selected[mask].head()
```

We can also use such masks to query properties about individual groups:

```python
data_selected[mask][“weight_kg”].mean()
```

In principle, this works quite well and does what it is supposed to do. But (of course) Pandas also has a function for this that makes it even easier: groupby().

## Groupby

Pandas `groupby` (see [Pandas documentation](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.groupby.html)).

With grouby, all entries with certain categories can be summarized in Pandas. This makes it easy to quickly compare many properties.

```python
data_selected.groupby(“type1”).mean()
```

Here the entries are sorted alphabetically by “type1”. To change the sorting, we simply add a `sort_values()` to sort by the desired column:

```python
data_selected.groupby(“type1”).mean().sort_values(“speed”)
```

Groupby can also be used to count the number of elements in the respective groups:

```python
data_selected.groupby(“type1”).count()
```

It is even possible to combine multiple groupby actions to create groups and subgroups:

python
data_selected.groupby([“type1”, “is_legendary”]).mean()

This allows us to see what the average values are for a pokemon of a certain type, depending on whether it is “legendary” or not.



## Plotting

Finally, a few short plotting examples.

Since we just used `groupby`, we can also use this to create a plot. Incidentally, “stacked=True” means that the different bars should be attached to each other.

```python
cols = [“attack”, “defense”, “hp”, “speed”, “weight_kg”]
data_selected.groupby(“type1”).mean()[cols].plot.barh(stacked=True)
```

There are nicer plots, but at least we can quickly see that the “weight_kg” entry in particular depends very much on the respective type1 group! So let's have another plot for it:

```python
data_selected.groupby(“type1”).mean()[“weight_kg”].plot.barh()
```

#### Intermezzo: data visualization

Why is the plot up here pretty bad?

--> The order makes it **very** confusing! Imagine I ask which type is at position 3, 4, or 5...

The axis label for the x-axis is missing.

In general: Pandas plots with the help of [`matplotlib`](https://matplotlib.org/). For more elaborate graphics and customizations, the plots are therefore also programmed with matplotlib. But Pandas just gives you quick access to explore different plots.

Simple adjustments can also be made quite well with Pandas, or matplotlib commands can be combined with Pandas.

Therefore, here is another attempt:

```python
ax = data_selected.groupby(“type1”).mean()[“weight_kg”].sort_values().plot.barh()
ax.set_xlabel(“weight [kg]”)
```

With Pandas, such calls quickly become very long and complicated because more and more functions/methods can be added one after the other. To make it a little clearer, you can also work with intermediate steps!

```python
data_groupby_type = data_selected.groupby(“type1”)
data_mean_weight = data_groupby_type.mean()[“weight_kg”]
ax = data_mean_weight.sort_values().plot.barh()
ax.set_xlabel(“weight [kg]”)
```



### A few more examples in the Jupyter Notebook of the lecture

... moving stuff to jupyter notebooks (soon)



## Pandas is huge!

Finally, we would like to point out that we will not be able to cover the full range of Pandas in 2-3, or even 4-5 lectures. So the main thing is that you familiarize yourself with how to use Pandas and DataFrames and how to perform simple operations with them (e.g. slicing, sorting). For everything else, you can always check forums or the Pandas documentation to see if there is already a suitable Pandas method for your specific question:

https://pandas.pydata.org/pandas-docs/stable/reference/frame.html
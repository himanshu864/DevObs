#ml #ai #python 

 **DataFrames** which are the central data structure in the pandas API.

A DataFrame is similar to an in-memory spreadsheet. Like a spreadsheet:

- A DataFrame stores data in cells.
- A DataFrame has named columns (usually) and numbered rows.

## Create a DataFrame

Instantiate a `pd.DataFrame(data=[], column=[])` class to generate a DataFrame.

```python
import numpy as np
import pandas as pd

# Create and populate a 5x2 NumPy array.
my_data = np.array([[0, 3], [10, 7], [20, 9], [30, 14], [40, 15]])

# Create a Python list that holds the names of the two columns.
my_column_names = ['temperature', 'activity']

# Create a DataFrame.
my_dataframe = pd.DataFrame(data=my_data, columns=my_column_names)

print(my_dataframe)
#    temperature  activity
# 0            0         3
# 1           10         7
# 2           20         9
# 3           30        14
# 4           40        15
```

## Adding a new column to DataFrame

```python
# add 'adjusted' column with custom values
my_dataframe['adjusted'] = [1,2,3,4,5]

# add 'adjusted' column with modified values
my_dataframe['adjusted'] = my_dataframe['activity'] + 2

print(my_dataframe)
#    temperature  activity  adjusted
# 0            0         3         5
# 1           10         7         9
# 2           20         9        11
# 3           30        14        16
# 4           40        15        17
```

## Accessing subset of DataFrame

```python
print("Rows #0, #1, and #2:")
print(my_dataframe.head(3), '\n')
#    temperature  activity  adjusted
# 0            0         3         5
# 1           10         7         9
# 2           20         9        11 

print("Row #2:")
print(my_dataframe.iloc[[2]], '\n')
#    temperature  activity  adjusted
# 2           20         9        11 

print("Rows #1, #2, and #3:")
print(my_dataframe[1:4], '\n')
#    temperature  activity  adjusted
# 1           10         7         9
# 2           20         9        11
# 3           30        14        16 

print("Column 'temperature':")
print(my_dataframe['temperature'])
# 0     0
# 1    10
# 2    20
# 3    30
# 4    40
# Name: temperature, dtype: int64
```

## Referencing vs Copying DataFrame

```python
reference_to_df = df # shallow copy

copying_to_df = df.copy() # deep copy
```


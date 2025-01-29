#ml #ai #python #math #dev 

 **DataFrames** which are the central data structure in the pandas API.

A DataFrame is similar to an in-memory spreadsheet. Like a spreadsheet:

- A DataFrame stores data in cells.
- A DataFrame has named columns (usually) and numbered rows.

## Create a Dataframe

```python
import numpy as np
import pandas as pd

# Create and populate a 5x2 NumPy array.
my_data = np.array([[0, 3], [10, 7], [20, 9], [30, 14], [40, 15]])

# Create a Python list that holds the names of the two columns.
my_column_names = ['temperature', 'activity']

# Create a DataFrame.
my_dataframe = pd.DataFrame(data=my_data, columns=my_column_names)

# Print the entire DataFrame
print(my_dataframe)
```

## Adding a row to Dataframe


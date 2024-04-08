---
title: Python Libs
summary: A note about Python Libraries.
description: A note about Python Libraries.
tags:
  - Python
---

# Pandas

---

### Import


````python
import pandas as pd
````

---

### Create a DataFrame


````python
# The data dictionary can be like this
data = {'col_1': [3, 2, 1, 0], 'col_2': ['a', 'b', 'c', 'd']}
# or a list of dicts
data = [
	{'col1':'value1','col2':'value1'},
	{'col1':'value2','col2':'value2'}
]

# Create DataFrame form dict 
df = pd.DataFrame.from_dict(data)
````

---

### Select Columns


````python
# This can be used to rearrange the columns order
df = df[['my_column_name_3', 'my_column_name_1', 'my_column_name_4']]
````

---

### Rename Columns


````python
df = df.rename(columns={'column_name_1': 'my_column_name_1'})
````

---

### Drop Columns


````python
df = df.drop(columns=['my_column_name_3', 'my_column_name_4'])
````

---

### Sort Values


````python
df = df.sort_values(by='my_column_name_2')
````

---

### Group By and Count


````python
df = df.groupby(['my_column_name_2']).size().reset_index(name='count')
````

---

### Left Join


````python
merged_df = pd.merge(
	left_dataset,
	right_dataset,
	how='left',
	left_on='left_column_name',
	right_on='right_column_name'
)
````

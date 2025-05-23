---
title: Python Libs
summary: A note about Python Libraries.
description: A note about Python Libraries.
tags:
  - Python
---

# Typing

---

### Iterable

The Iterable type represent every type that can be iterated (that can be looped through\_): `list`, `tuple`, `set`, ...

````python
from typing import Iterable

players_iterable: Iterator[str] = ['Player1, Player2, Player3']
players_iterable: Iterator[str] = ('Player1, Player2, Player3')
players_iterable: Iterator[str] = {'Player1, Player2, Player3'}
````

---

### Iterator

When we get an information form an iterator with `next()` or `list()` it is removed from the iterator.

````python
from typing import Iterator

players: list[str] = ['Player1, Player2, Player3']
players_iter: Iterator[str] = iter(players)

print(next(players_iter)) # Player1
print(next(players_iter)) # Player2
print(next(players_iter)) # Player3
print(list(players_iter)) # []
````

---

### Generator

#### Basis

A generator as 3 parameters:

* 1st is the type to **yield**
* 2nd is the type that can be **sent to** the generator
* 3rd is the type that is **returned** by the generator

Note: a Generator is under the hood an Iterator

#### Yield Example

````python
from typing import Generator


def fibonacci_generator() -> Generator[int, None, None]
	a, b = 0, 1
	while True:
		yield a
		a, b = b, (a + b)


fib_gen: Generator[int, None, None] = fibonacci_generator()
n: int = 10
line_break: str = '-' * 20


while True:
	input(f'Press "enter" for the next {n} numbers of ficonnacci)
	for i in range(n):
		print(f'{next(fib_gen)}')
	print(line_break)


````

Source : [Indently - 5 Useful Generator Functions In Python](https://www.youtube.com/watch?v=1OSEzdOpmWQ)

#### Yield + Return Example

````python
from typing import Generator


def read(path: string) -> Generator[str, None, str]:
	with open(path, 'r') as file:
		for line in file:
			yield line.strip()
	return 'This is the end of the file.'


reader: Generator[str, None, str] = read('file.txt')
while True:
	input(f'Press "enter for the next line") 
	try:
		print(next(reader))
	except StopIteration as e:
		# StopIteration the return of the Genenrator
		print('StopIteration:', e.value)
		sys.exit()
````

Source : [Indently - 5 Useful Generator Functions In Python](https://www.youtube.com/watch?v=1OSEzdOpmWQ)

### Yield + Send Example

````python
from typing import Generator


def cumulative_sum() -> Generator[float, float, None]:
	total: flaot = 0
	while True:
		total += yield total # yield act like retrive 

cumulative_generator: Generator[float, float, None] = cumulative_sum()
next(cumulative_generator) # start the generator
while True:
	value: float = float(input('Enter a value: '))
	current_sum: float = cumulative_generator.send(value)
	print(f'Cumulative sum: {current_sum}')
````

Source : [Indently - 5 Useful Generator Functions In Python](https://www.youtube.com/watch?v=1OSEzdOpmWQ)

# Time

---

### Import


````python
import datetime
import locale
````

---

### Basis


````python
print(locale.getlocale())
#('en_US', 'UTF-8')

# Set local to get right format for the date
locale.setlocale(locale.LC_TIME, locale.getlocale())


print(f'{datetime.datetime.now()}')
#2024-08-02 22:30:04.850285

print(f'{datetime.datetime.now():%c}')
#Fri 02 Aug 2024 10:30:01 PM 

print(f'{datetime.datetime.now():%x}')
#08/02/2024
````

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

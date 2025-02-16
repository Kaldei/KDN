---
title: Python
summary: A note about Python.
description: A note about Python.
tags:
  - Python
---

# Virtual Env

---

### Create Venv


 > 
 > **<font color=red>python -m venv</font> myVenv/**</br>
 > Create Venv.

---

### Windows


 > 
 > **myVenv<font color=red>/scripts/activate</font>**</br>	
 > Activate Venv.

 > 
 > **<font color=red>deactivate</font>**</br>
 > Deactivate Venv.

---

### Linux


 > 
 > **<font color=red>source</font> myVenv<font color=red>/bin/activate</font>**</br>
 > Activate Venv.

 > 
 > **<font color=red>deactivate</font>**</br>
 > Deactivate Venv.

# Data Types

---

### Tuples

Tuples are like lists, but can’t be changed (immutable).

````py
# Declare an empty typle
empty_tuple = ()
````

````
# Declare a tuple
players = "player1", "player2"
````

Note: A tuple is not defined by parenthesis, it is defined by commas (except for declaring an empty tuple).

# String Manipulation

---

### Input / Output


 > 
 > **<font color=red>input("</font>Message<font color=red>")</font>**</br>
 > Keyboard input.
 > 
 > **<font color=red>print("</font>Message<font color=red>")</font>**</br>
 > Write a message to the output.

 > 
 > **<font color=red>print("</font>Message <font color=red>{}".format(</font>myVar<font color=red>))</font>**</br>
 > Replace `{}` with `myVar`.
 > 
 > **<font color=red>print("</font>Message<font color=red>",</font> myVar<font color=red>)</font>**</br>
 > Variable concatenation.
 > 
 > **<font color=red>print(f "</font>Message <font color=red>{</font>myVar<font color=red>}")</font>**</br>
 > Replace `{myVar}` with `myVar`.

 > 
 > **<font color=red>print(r "</font>c:\path\name<font color=red>")</font>**</br>
 > Do not interpret special characters (e.g. `\`', `\n`).

 > 
 > **<font color=red>print("</font>Message<font color=red>" +</font> myString<font color=red>)</font>**</br>
 > String concatenation.
 > 
 > **<font color=red>print("</font>Message<font color=red>".join(</font>myString<font color=red>))</font>**</br>
 > String concatenation.

---

### Strip & Split


 > 
 > **<font color=red>split("</font>,<font color=red>")</font>**</br>
 > Split a string based on a delimiter.

 > 
 > **myString<font color=red>.strip(\[</font>chars<font color=red>\])</font>**</br>
 > Remove all "chars" at the beginning and the end of the string.
 > 
 > **myString<font color=red>.rstrip(\[</font>chars<font color=red>\])</font>**</br>
 > Remove all "chars" at the end of the string.

---

### Encoding


 > 
 > **<font color=red>ord('</font>A<font color=red>')</font>**</br>
 > Convert character to Decimal ASCII code.
 > 
 > **<font color=red>chr(</font>65<font color=red>)</font>**</br>
 > Convert Decimal ASCII code to character.

 > 
 > **<font color=red>"\x</font>41<font color=red>"</font>**</br>
 > Convert Hexadecimal ASCII code to character.

 > 
 > **<font color=red>bytes("</font>myString<font color=red>", "UTF-8")</font>**</br>
 > Convert a string into an array of bytes.

---

### Misc


 > 
 > **<font color=red>str(</font>intVar<font color=red>)</font>**</br>
 > Convert int variable to string.
 > 
 > **<font color=red>len(</font>myVar<font color=red>)</font>**</br>
 > Count the number of characters in the variable.

 > 
 > **myString<font color=red>.title()</font>**</br>
 > Convert to title (e.g. This Is A Title).
 > 
 > **myString<font color=red>.upper()</font>**</br>
 > Convert to uppercase.
 > 
 > **myString<font color=red>.lower()</font>**</br>
 > Convert to lowercase.

# Files

---

### Read File


````py
with open("myFile.txt", "r") as file:
  # Get entire file content
  file_data = file.read()

  # Get all lines at once
  lines = file.read().splitlines()

  # Get lines one by one
  line1 = file.readline()
  line2 = file.readline()
````

This syntax handles automatically closing the file if anything goes wrong inside the `with` block.

---

### Write File


````py
with open('myFile.txt', 'w', encoding="utf-8") as file:
  file.write('This is a line\n')
````

This syntax handles automatically closing the file if anything goes wrong inside the `with` block.

---

### Read File (Old Way)


````py
from typing import TextIO

file: textIO = open('myFile.txt')
try:
	content: str = file.read()
	print(content)
finally:
	file.close()
````

# OOP

---

### Main

This condition will be evaluated to `True` if this file is the one that was run. This is not the case is the file is imported thus the condition is will be evaluated to `False`. 

````py
if __name__ == '__main__':
	print("Hello")
````

---

### Class


````py
class Player:
    # Constructor
    def __init__(self, name:str) -> None:
		self.name: str = name
        self.health: int = 100
        self.max_health: int = 100
        
	# Method
	def increase_max_health(self) -> None:
		self.max_health += 10
````

````py
# Init new instance of the class (a new object)
myPlayer: Player = Player(name: 'myPlayerName')

# Use a method
myPlayer.increase_max_health()

# Access an attribute
print(myPlayer.max_health) # Will print 110
````

---

### Class Attributes vs Instance Attributes


````py
class Player:
	# Class Attribute
	max_mana: int = 100
	
    # Constructor
    def __init__(self) -> None:
        # Instance Attribute
        self.health: int = 100
````

````py
myPlayer1: Player = Player()
myPlayer2: Player = Player()

# Implicitly create an Instance Attribute
myPlayer1.max_mana = 200
print(myPlayer1.max_mana) # Will print 200
print(myPlayer2.max_mana) # Will print 100

# Change the Class Attribute value
Player.max_mana = 300
print(myPlayer1.max_mana) # Will print 300
print(myPlayer2.max_mana) # Will print 300
````

---

### @staticmethod

Adding the `@staticmethod` annotation allows creating a method that don't require anything from the object (`self`). This method could be defined outside the class but if its only relevant to this class, it can be nice to keep the code inside this class.

````py
class Player:
    # Constructor
    def __init__(self) -> None:
        self.health: int = 100
        self.max_health: int = 100

	# Non static method
	def increase_max_health(self) -> None:
		self.max_health += 10

	# Static method
	@staticmethod
	def say_hello() -> None:
		print("Hello")
````

Also, `@staticmethod` allows calling the method even if no object were instantiated.

````py
Player.say_hello()
````

---

### Dunder Methods


````py
class Player:
    # Constructor
    def __init__(self) -> None:
        self.health: int = 100
        self.max_health: int = 100
   
	# Dunder Methods
	__add__(self, other):
		...

	__mul__(self, other):
		...

	# __str__ should return something user friendly
	# If __str__ is not defined is will fallback to __repr__
	__str__(self) -> str:
		...

	# __repr__ should return something usefull for developpers
	# Default is memory address
	__repr__(self) -> str:
		...

````

````py
myPlayer1: Player = Player()
myPlayer2: Player = Player()

print(myPlayer1 + myPlayer2) # Will use dunder method __add__
print(myPlayer1 * myPlayer2) # Will use dunder method __mul__
print(myPlayer1) # Will use dunder method __str__
print(repr(myPlayer1)) # Will use dunder method __str__
````

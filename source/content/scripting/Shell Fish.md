---
title: Shell Fish
summary: A note about the Fish shell.
description: A note about the Fish shell.
tags:
  - fish
---

# Basis

---

### Fish

Fish generally works like other shells, like Bash or Zsh. 
A few important differences can be found at [https://fishshell.com/docs/current/tutorial.html](https://fishshell.com/docs/current/tutorial.html) by searching for the magic phrase "unlike other shells".

---

### Config

 > 
 > **<font color=red>fish_config</font>**</br>
 > Open web interface to config fish.

 > 
 > **<font color=red>fish_add_path</font> /my/path/to/add**</br>
 > Add new path to PATH.

---

### Alias

 > 
 > **<font color=red>alias --save</font> k<font color=red>=</font>"kubectl"**</br>
 > Create an alias (`--save` make permanent).

# Variables

---

### Set Variable

 > 
 > **<font color=red>set</font> MY_VAR myValue**</br>
 > Set variable.

 > 
 > **<font color=red>-x</font>**</br>
 > Export the variable (make it an environment variable, available to child processes).
 > 
 > **<font color=red>-g</font>**</br>
 > Global variable (available to all function in the same shell).
 > 
 > **<font color=red>-U</font>**</br>
 > Set "Universal" variable (available all fish instances and persist across restarts).

# Structures

---

### While

 > 
 > **<font color=red>while read</font> line<font color=red>;</font> echo $line<font color=red>; end \<</font> myFile.txt**</br>
 > One liner version of while loop to read file.

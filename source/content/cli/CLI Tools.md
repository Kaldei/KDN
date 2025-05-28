---
title: CLI Tools
summary: Useful CLI tools and utilities for scripting.
description: Useful CLI tools and utilities for scripting.
tags:
  - cli_utils
---

# String Manipulation Utilities

---

### Grep


 > 
 > **<font color=red>grep</font> myString myFile**</br>
 > Return lines containing myString.

 > 
 > **<font color=red>grep -e</font> myString1 <font color=red>-e</font> myString2**</br>
 > Match multiple patterns.

 > 
 > **<font color=red>grep -E</font>**</br>
 > Use a Regex.
 > 
 > **<font color=red>grep -F</font>**</br>
 > Interpret patterns as fixed strings.

 > 
 > **<font color=red>grep -i</font>**</br>
 > Return lines that correspond to the string but is not case-sensitive.

 > 
 > **<font color=red>grep -A</font> 12**</br>
 > Return 12 lines after the match.
 > 
 > **<font color=red>grep -B</font> 12**</br>
 > Return 12 lines before the match.
 > 
 > **<font color=red>grep -C</font> 12**</br>
 > Return 12 lines before and after the match.

 > 
 > **<font color=red>grep -x</font>**</br>
 > Return lines that correspond exactly to the string.
 > 
 > **<font color=red>grep -v</font>**</br>
 > Return lines that do not contain the string.

 > 
 > **<font color=red>grep -c</font>**</br>
 > Counts the number of lines containing the string.
 > 
 > **<font color=red>grep -n</font>**</br>
 > Each line containing the string is numbered.

 > 
 > **<font color=red>grep -l</font>**</br>
 > Return the names of files containing the string.
 > 
 > **<font color=red>grep -h</font>**</br>
 > Do not return the folder prefix.

 > 
 > **<font color=red>grep -vxFf</font> myFileA myFileB**</br>
 > Prints all lines in `fileA` that are not found in `fileB`.

---

### Cut


 > 
 > **<font color=red>cut -c</font> 1<font color=red>-</font>12**</br>
 > Return characters from 1 to 12 of the input string.
 > 
 > **<font color=red>cut -c -</font>12**</br>
 > Return the first 12 characters of the input string.
 > 
 > **<font color=red>cut -c</font> 12<font color=red>-</font>**</br>
 > Return the last 12 characters of the input string.
 > 
 > **<font color=red>cut -c</font> 1<font color=red>,</font>12**</br>
 > Return characters  1 and 12 of the input string.

 > 
 > **<font color=red>cut -d</font> : <font color=red>-f</font> 2**</br>
 > Return the second field (`-f 2`). Field separator is defined with `-d`.

---

### Sed


 > 
 > **<font color=red>sed -d</font>**</br>
 > Remove a line (`"/.../d"`).
 > 
 > **<font color=red>sed -s</font>**</br>
 > Replace a string (`"s/old/new/"`).

 > 
 > **<font color=red>sed -g</font>**</br>
 > Apply on all lines (`"/old/new/g"`).

---

### Tr


 > 
 > **<font color=red>tr '</font>a-z<font color=red>' '</font>A-Z<font color=red>'</font>**</br>
 > Replace lower case letters with upper case letters.
 > 
 > **<font color=red>tr '</font>abcd<font color=red>' '</font>jkmn<font color=red>'</font>**</br>
 > Replace `a` by `j`, `b` by `k`, `c` by `m` and `d` by `n`.

---

### Sort


 > 
 > **<font color=red>sort</font> myFile.txt**</br>
 > Sort the contents of a file.

 > 
 > **<font color=red>sort -d</font> myFile.txt**</br>
 > Sort using only blanks and alphanumeric chars (dictionary order).

 > 
 > **<font color=red>sort -k 2</font> myFile.txt**</br>
 > Sort on the second column in the file (separated by space).

# File Manipulation Utilities

---

### Uniq


 > 
 > **<font color=red>uniq</font>**</br>
 > Deletes duplicate lines in a file (the comparison is done with the previous line, so use `sort -d` before). 

 > 
 > **<font color=red>uniq -u</font>**</br>
 > Return lines that appear only once.
 > 
 > **<font color=red>uniq -d</font>**</br>
 > Return lines that appear more than once.

---

### Diff


 > 
 > **<font color=red>diff</font> myFile1 myFile2**</br>
 > Return differences between the two files.

# Json Manipulation

---

### JQ

#### Resources

* Try jq online: https://jqplay.org/#
* Interactive JSON filter : https://github.com/ynqa/jnv

#### Usage

 > 
 > **cat myFile.json <font color=red>\| jq</font>**</br>
 > 
 > **<font color=red>jq</font> myFile.json**</br>
 > 
 > **<font color=red>jq \<\<\< </font> {  "player": { "name": "apple", "color": "blue" } }**</br>

#### Flags

 > 
 > **<font color=red>-r</font>**</br>
 > Output raw strings (without the quotes).

#### Filter Json Array

````json
["myPlayer1", "myPlayer2", "myPlayer3"]
````

 > 
 > **<font color=red>jq '.\[\]'</font> myFile.json**</br>
 > Return elements line by line (without `[ ]`).
 > 
 > **<font color=red>jq '.\[2\]'</font> myFile.json**</br>
 > Return an element by its ID.
 > 
 > **<font color=red>jq '.\[2:12\]'</font> myFile.json**</br>
 > Return a subset of elements.

#### Filter Json Object

````json
{
  "player": {
    "name": "myPlayer",
    "color": "blue"
  }
}
````

 > 
 > **<font color=red>jq '.</font>player<font color=red>.</font>name<font color=red>, .</font>player<font color=red>.</font>color<font color=red>'</font> myFile.json**</br>
 > Return the `name` property.

 > 
 > **<font color=red>jq '.</font>player <font color=red>\| select(.</font>player_class <font color=red>== "</font>knight<font color=red>")'</font> myFile.json**</br>
 > Return `player` that have the property `player_class` set to `knight`.

 > 
 > **<font color=red>jq '.</font>player <font color=red>\| keys' </font>myFile.json**</br>
 > Return the keys of `player` (`name` and ` color`).
 > 
 > **<font color=red>jq '.</font>player <font color=red>\| length' </font>myFile.json**</br>
 > Return the length of `player` (here the number of properties is 2).

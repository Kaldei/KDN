---
title: JQ
summary: A lightweight and flexible JSON processor.
description: A lightweight and flexible JSON processor.
tags:
  - linux
  - json
---

# Resources

---

* Try jq online: https://jqplay.org/#
* Interactive JSON filter : https://github.com/ynqa/jnv

# Basis

---

### Usage


 > 
 > **cat myFile.json <font color=red>\| jq</font>**</br>
 > 
 > **<font color=red>jq</font> myFile.json**</br>
 > 
 > **<font color=red>jq \<\<\< </font> {  "player": { "name": "apple", "color": "blue" } }**</br>

---

### Flags


 > 
 > **<font color=red>-r</font>**</br>
 > Output raw strings (without the quotes).

# Filter

---

### Filter JSON Array


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

---

### Filter JSON Object


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

---
title: Python
summary: A note about Python.
description: A note about Python.
tags:
  - Python
---

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

# OOP

---

### Main


````py
if __name__ == '__main__':
	print("Hello")
````

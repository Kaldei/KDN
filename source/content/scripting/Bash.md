---
title: Bash
summary: A note about Bash scripting.
description: A note about Bash scripting.
tags:
  - bash
---

# Variables

---

### Basis


 > 
 > **myVar<font color=red>=</font>myValue**</br>
 > Assign a value to the variable (**warning, no space!**).
 > 
 > **myVar<font color=red>=$(</font>whoami<font color=red>)</font>**</br>
 > Assign command output to the variable.
 > 
 > **<font color=red>$</font>myVar**</br>
 > Access variable content.

---

### Array


 > 
 > **myArray<font color=red>=()</font>**</br>
 > Create an empty array.
 > 
 > **myArray<font color=red>=(</font>12 12<font color=red>)</font>**</br>
 > Create an array with values (note the space between values).

 > 
 > **myArray<font color=red>\[</font>0<font color=red>\]=</font>myValue**</br>
 > Assign a value to the first value of the array.
 > 
 > **myArray<font color=red>+=(</font>myValue<font color=red>)</font>**</br>
 > Append value at the end of the array (add a value).

 > 
 > **<font color=red>${</font>myArray<font color=red>\[</font>0<font color=red>\]}</font>**</br>
 > Return the first value of the array.
 > 
 > **<font color=red>${</font>myArray<font color=red>\[@\]}</font>**</br>
 > Return the whole array.
 > 
 > **<font color=red>${</font>myArray<font color=red>\[</font>3<font color=red>:@\]}</font>**</br>
 > Return the values form third to last.
 > 
 > **<font color=red>${#</font>myArray<font color=red>\[@\]}</font>**</br>
 > Return the array size.

---

### Special Variables


 > 
 > **<font color=red>$?</font>**</br>
 > Output code of previously executed program.

 > 
 > **<font color=red>$0</font>**</br>
 > Path of the currently called script.
 > 
 > **<font color=red>$1</font>, <font color=red>$2</font> ...**</br>
 > Arguments passed to the script.
 > 
 > **<font color=red>$#</font>**</br>
 > Arguments numbers.
 > 
 > **<font color=red>$@</font>**</br>
 > Return all the arguments.

 > 
 > **<font color=red>date</font>**</br>
 > Return date, time, and time difference.
 > 
 > **<font color=red>date "+%H"</font>**</br>	
 > Return the current hour. (`%H` = hour, `%M` = minute, `%S` = second, …).

 > 
 > **<font color=red>seq</font> 1 12**</br>
 > Return a number sequence.

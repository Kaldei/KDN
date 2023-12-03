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

# Structures

---

### Condition


````bash
if [ boolean ]
then
	...
elif
then
	...
else
	...
fi

````

![Bash-Operators.png](../../attachments/Bash-Operators.png)

---

### For Loop


````bash
for i in `seq 0 100`
do
	...
done
````

````bash
for i in {1..100}
do
	...
done
````

---

### While Loop


````bash
# Read lines for file
while read line
do
	echo $line
done < myFile
````

# Redirections

---

### Chevrons


 > 
 > **<font color=red>\></font>**</br> 
 > Redirects to a file (if it already exists, it will be overwritten).
 > 
 > **<font color=red>\>></font>**</br> 
 > Redirects to the end of a file (if it doesn't exist, it will be created).

 > 
 > **<font color=red>2></font>**</br> 
 > Redirects errors to a file (if it already exists, it will be overwritten).
 > 
 > **<font color=red>2>></font>**</br>
 > Redirects errors to the end of a file (if it doesn't exist, it will be created).
 > 
 > **<font color=red>2>&1 </font>**</br>
 > Redirects errors in the standard output.

 > 
 > **<font color=red>\<</font>**</br> 
 > Sends the contents of a file to a command.
 > 
 > **KEYWORD <font color=red>\<\<</font>**</br> 
 > Switches the console to keyboard input mode, line by line. All the lines will be sent  when the end keyword has been written.

---

### Ampersand


 > 
 > **cmd1 <font color=red>&</font> cmd2**</br>
 > First command will be executed in background. 
 > 
 > **cmd1 <font color=red>&&</font> cmd2**</br>
 > Second command is executed if the first command return code is 0 (ok).

---

### Pipe


 > 
 > **cmd1 <font color=red>\|</font> cmd2**</br>
 > Chains commands (output from command 1 is sent to command 2).
 > 
 > **cmd1 <font color=red>\||</font> cmd2**</br>
 > Second command is executed if the first command return code is not 0 (error).

# Regex

---

### Basis


 > 
 > **<font color=red>/</font>...<font color=red>/</font>**</br>
 > A regex is enclosed between two forward slashes.
 > 
 > **<font color=red>\</font>**</br>
 > Cancels the special effect of a special character.
 > 
 > **<font color=red>\|</font>**</br>
 > Alternative (or).

 > 
 > **<font color=red>^</font>**</br>
 > Start of line.
 > 
 > **<font color=red>$</font>**</br>
 > End of line.

 > 
 > **<font color=red>\[</font> ab <font color=red>\]</font>**</br>
 > Match one of the characters inside the square brackets (a or b). 
 > 
 > **<font color=red>\[</font> a<font color=red>-</font>z <font color=red>\]</font>**</br>
 > Match on a range of characters.
 > 
 > **<font color=red>
[^</font>a<font color=red>]</font>**</br>
 > Match if the character is not the one that is after the `^`.
 > 
 > **<font color=red>(</font>myWord<font color=red>)</font>**</br>
 > Match the group inside the parenthesis.
 > 
 > **<font color=red>.</font>**</br>
 > Match any character.

 > 
 > **<font color=red>?</font>**</br>
 > The preceding element is present 0 or 1 times.
 > 
 > **<font color=red>{</font> 2 <font color=red>}</font>**</br>
 > The preceding element is repeated a defined a number of times.
 > 
 > **<font color=red>{</font> 0<font color=red>,</font>3 <font color=red>}</font>**</br>
 > The preceding element is repeated between 0 and 3 times.
 > 
 > **<font color=red>\*</font>**</br>
 > The preceding element is repeated between 0 and infinite number of times.
 > 
 > **<font color=red>+</font>**</br>
 > The preceding element is repeated between 1 and infinite number of times.

---

### Useful Regexes


 > 
 > **<font color=red>ip addr show eth0 | grep -oP '(?\<=inet\s)\d+(.\d+){3}'</font>**</br>
 > Get IP Linux `eth0` interface.

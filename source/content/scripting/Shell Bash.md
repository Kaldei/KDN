---
title: Shell Bash
summary: A note about Bash.
description: A note about Bash.
tags:
  - bash
  - shell
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
 > **myArray<font color=red>=(</font> 12 12 <font color=red>)</font>**</br>
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

````bash
directories=( myDir1 myDir2 myDir3)

for directory in "${directories[@]}"; do
	mkdir -p $directory
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

 > 
 > **<font color=red>while read</font> line<font color=red>; do</font> echo $line<font color=red>; done \<</font> myFile.txt**</br>
 > One liner version of while loop to read file.

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
 > **<font color=red>\<</font> myFile**</br> 
 > Sends a file as a input command.
 > 
 > **KEYWORD <font color=red>\<\<</font>**</br> 
 > Switches the console to keyboard input mode, line by line. All the lines will be sent  when the end keyword has been written.
 > 
 > **<font color=red>\<\<\<</font> myString**</br> 
 > Sends a string as a input command.

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

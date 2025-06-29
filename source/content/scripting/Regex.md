---
title: Regex
summary: A sequence of characters to match pattern in text.
description: A sequence of characters to match pattern in text.
tags:
  - regex
---

# Basis


 > 
 > **<font color=red>/</font>...<font color=red>/</font>**</br>
 > A regex is enclosed between two forward slashes.
 > 
 > **<font color=red>\\</font>**</br>
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

# Useful Regex

---

### Extract IP from


 > 
 > **<font color=red>ip a show eth0 | grep -oP '(?\<=inet\s)\d+(.\d+){3}'</font>**</br>
 > Extract IP for`eth0` interface from `ip a` command.

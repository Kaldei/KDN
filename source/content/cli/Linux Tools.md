---
title: Linux Tools
summary: CLI tools and tricks for Linux.
description: CLI tools and tricks for Linux.
tags:
  - linux
---

# Basis

---

### Shortcuts


 > 
 > **<font color=green>Ctrl + A</font>**</br>
 > Go to the beginning of the line.
 > 
 > **<font color=green>Ctrl + E</font>**</br>
 > Go to the end of the line.

 > 
 > **<font color=green>Ctrl + Alt + F2</font>**</br>
 > Open TTY 2 (there are 6 TTYs on Linux that can be opened in parallel, from F1 to F6).

# Files

---

### Search for Files


 > 
 > **<font color=red>find</font> /search/path/ <font color=red>-name</font> myFile**</br>
 > Find a file by name.

 > 
 > **<font color=red>find</font> /search/path/ <font color=red>-type</font> f**</br>
 > Find by type (f (file), d (directory), l (symbolic link)).
 > 
 > **<font color=red>find</font> /search/path/ <font color=red>-size</font> 50M**</br>
 > Find a file by size (c (octets / bytes), k (kilo octets), M (mega octets), G (giga octets), b (blocs of 512 octets).

 > 
 > **<font color=red>find</font> /search/path/ <font color=red>-user</font> myUser**</br>
 > Find a file by user.
 > 
 > **<font color=red>find</font> /search/path/ <font color=red>-group</font> myGroup**</br>
 > Find a file by group.
 > 
 > **<font color=red>find</font> /search/path/ <font color=red>-perm</font> 000**</br>
 > Find a file by permission.

 > 
 > **<font color=red>find</font> /search/path/ <font color=red>-name</font> *.txt* <font color=red>-exec </font>rm <font color=red>{};</font>**</br>
 > Find files and execute a command for each of them (`{}` is replaced by what is found by `find`).

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

# String Manipulation

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

# Monitoring

---

### Watch


 > 
 > **<font color=red>watch</font> my-command**</br>
 > Run a command every 2 seconds (default).

 > 
 > **<font color=red>-n</font> 0.5**</br>
 > Specify the interval in seconds.
 > 
 > **<font color=red>-d</font>**</br>
 > Highlight changes.

---

### Journalctl


 > 
 > **<font color=red>journalctl -u</font> my-service.service**</br>
 > Returns logs for the specified service.
 > 
 > **<font color=red>journalctl -fu</font> my-service.service**</br>
 > Follow logs for the specified service.

 > 
 > **<font color=red>journatl --since "</font>1 hour ago<font color=red>"</font>**</br>
 > Returns logs since one hour ago.
 > 
 > **<font color=red>journalctl --since "</font>2025-01-01 12:00:00<font color=red>" --until "</font>2025-01-01 13:00:00<font color=red>"</font>**</br>
 > Returns logs between given dates.

# Networking

---

### DNS


 > 
 > **<font color=red>dig +short</font> my.domain**</br>
 > Return only IP.

 > 
 > **<font color=red>dig -x</font> 12.12.12.12**</br>
 > Reverse DNS.

 > 
 > **<font color=red>dig -t TXT</font> my.txt.record**</br>
 > Return TXT Record.
 > 
 > **<font color=red>dig -t CNAME</font> my.txt.record**</br>
 > Return CNAME Record.
 > 
 > **<font color=red>dig -t MX</font> my.txt.record**</br>
 > Return MX Record.

---

### SSL/TLS


 > 
 > **<font color=red>openssl s_client -connect</font> \[MY_HOST\]<font color=red>:</font>\[MY_PORT\]**</br>
 > Make an SSL/TLS client request.

---

### Sockets


 > 
 > **<font color=red>ss -tunp</font>**</br>
 > Returns established connections (TCP and UDP).

 > 
 > **<font color=red>ss -tulnp</font>**</br>
 > Returns listening sockets (TCP and UDP).

 > 
 > **<font color=red>ss -tuanp</font>**</br>
 > Returns established connection and listening sockets (TCP and UDP).

---

### NMCLI


 > 
 > **<font color=red>nmcli device</font>**</br>
 > List network devices (ethernet, wifi, ...)

 > 
 > **<font color=red>nmcli device wifi connect</font> MY_SSID**</br>
 > Connect to specified SSID.
 > 
 > **<font color=red>nmcli connection down</font> MY_SSID**</br>
 > Disconnect from specified SSID.

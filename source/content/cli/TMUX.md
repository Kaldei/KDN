---
title: TMUX
summary: A terminal multiplexer for Unix-like OS
description: A terminal multiplexer for Unix-like OS
tags:
  - unix
---

# Panes

---

### Split


 > 
 > **<font color=red>Ctrl + b</font> then <font color=red>%</font>**</br>
 > Split screen vertically.
 > 
 > **<font color=red>Ctrl + b</font> then <font color=red>"</font>**</br>
 > Split screen horizontally.

---

### Resize


 > 
 > **<font color=red>Ctrl + b + →</font>**</br>
 > Resize current panel.

---

### Focus


 > 
 > **<font color=red>Ctrl + b</font> then <font color=red>→</font>**</br>
 > Change focus to right panel.

---

### Navigate


 > 
 > **<font color=red>Ctrl + b </font>then <font color=red>\[</font>**</br>
 > Move your cursor up and down.

# Windows

---

### Create


 > 
 > **<font color=red>Ctrl + b</font> then <font color=red>c</font>**</br>
 > Create a new tab.

---

### Switch


 > 
 > **<font color=red>Ctrl + b</font> then <font color=red>1</font>**</br>
 > Switch to tab 1.

# Sessions

---

### List


 > 
 > **<font color=red>tmux ls</font>**</br>
 > List current existing sessions (alias for `list-sessions`).

---

### Manage


 > 
 > **<font color=red>Ctrl+b</font> then <font color=red>$</font>**</br>
 > or</br>
 > **<font color=red>tmux rename-session -t</font> mySessionId myNewName**</br>
 > Renamed a session.

---

### Attach


 > 
 > **<font color=red>Ctrl + b</font> then <font color=red>d</font>**</br>
 > or</br>
 > **<font color=red>tmux detach</font>**</br>
 > Detach form session.

 > 
 > **<font color=red>tmux attach -t</font> mySessionId**</br>
 > Attach to a session.

---

### Navigate


 > 
 > **<font color=red>Ctrl + b</font> then <font color=red>s</font>**</br>
 > Open Tmux session manager

 > 
 > **<font color=red>Ctrl + b</font> then <font color=red>)</font>**</br>
 > or </br>
 > **<font color=red>Ctrl + b</font> then <font color=red>(</font>**</br>
 > Quickly switch between sessions

# Configuration

````
# Set predix shortcut
set -g prefix ^B


# Start indexing windows at 1 instead of 0
set -g base-index 1

# Renumber windows when one is closed
set -g renumber-windows on
````

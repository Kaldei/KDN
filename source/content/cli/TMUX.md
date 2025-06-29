---
title: TMUX
summary: A terminal multiplexer for Unix-like OS
description: A terminal multiplexer for Unix-like OS
tags:
  - unix
---

# Tabs

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

# Panels

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

# Sessions

---

### List


 > 
 > **<font color=red>tmux ls</font>**</br>
 > List current existing sessions (alias for `list-sessions`).

---

### Attach


 > 
 > **<font color=red>Ctrl + b</font> then <font color=red>d</font>**</br>
 > Detach form session.

 > 
 > **<font color=red>tmux attach -t</font> 1**</br>
 > Attach to session 1.

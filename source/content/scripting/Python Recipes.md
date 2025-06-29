---
title: Python Recipes
summary: A note about Python useful bits of code.
description: A note about Python useful bits of code.
tags:
  - Python
---

# Files

---

### Copy Files

Source: [How To Copy Files - Intently](https://www.youtube.com/watch?v=vx9zFN8PxOA)

````python
from tkinter import filedialog
from pathlib import Path
import shutil

# Open a file explorer window to choose a file
src_path: str = filedialog.askopenfilename(title='Pick a file to copy')
# Open a file explorer window to choose a directory
dst_directory: str = filedialog.askopendirectory(title='Pick a destination')

# Path handle path regardless of the OS 
dst_path: Path = Path(directory) / f'copy.{src_path.split(".")[-1]}' 

# Copy a file without metadata
shutil.copyfile(src=src_path, dst=dst_path)
# Copy a file with metadata
shutil.copy2(src=src_path, dst=dst_path)

````

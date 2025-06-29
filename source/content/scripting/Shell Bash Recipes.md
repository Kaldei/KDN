---
title: Shell Bash Recipes
summary: A note about Bash useful bits of code.
description: A note about Bash useful bits of code.
tags:
  - bash
---

# Output

---

### Log Function


````bash
LOGFILE="/var/log/log_file.log"

function log {
  local level="$1"
  local message="$2"
  local timestamp=$(date +"%Y-%m-%d %H:%M:%S")
  local log_entry="$timestamp [$level] - $message"

  echo "$log_entry" | tee -a "$LOGFILE"
}
````

````bash
log "INFO" "Installing myPackage"
...

log "ERROR" "Failed Installing myPackage"
````

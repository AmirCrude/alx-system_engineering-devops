# Shell, init files, variables and expansions
## Project Overview
This project focuses on shell initialization files, variables, expansions, and aliases in Bash scripting.

### Task 0: Create an alias
#### File: 0-alias
**Objective:** Create a script that creates an alias named ls with the value rm *.

**Script Content:**

```bash
#!/bin/bash
alias ls="rm *"
```
**Description:**
This script creates an alias where typing ls will actually execute rm * (remove all files in the current directory). This is a demonstration of how aliases can override default commands.

**Usage:**

```bash
# Make the script executable
chmod +x 0-alias

# Source the script to activate the alias
source ./0-alias

# Now 'ls' command will delete all files
ls

# To use the original ls command, escape it with backslash
\ls
```
**Note:** After sourcing this script, be cautious as ls will delete files. Use \ls to access the original ls command.


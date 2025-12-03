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

### Task 1: Hello you
#### File: 1-hello_you
**Objective:** Create a script that prints hello user, where user is the current Linux user.

**Script Content:**

```bash
#!/bin/bash
echo "hello $USER"
```
**Description:**
This script uses the $USER environment variable to get the current logged-in username and prints a greeting message in the format hello username.
**Usage:**

```bash
# Make the script executable
chmod +x 1-hello_you

# Run the script
./1-hello_you

# Example output if username is 'amir':
# hello amir
```
**How it works:**

$USER is a built-in environment variable that stores the current username

The script uses double quotes to allow variable expansion

The echo command outputs the formatted string

### Task 2: The path to success is to take massive, determined action
#### File: 2-path
Objective: Add /action to the PATH environment variable, making it the last directory the shell searches for programs.

Script Content:

bash
#!/bin/bash
export PATH="$PATH:/action"
Description:
This script modifies the PATH environment variable by appending /action to its end. When the shell searches for executable programs, it will look in /action last, after checking all other directories in the PATH.

Usage:

```bash
# Make the script executable
chmod +x 2-path

# Source the script to affect current shell session
source ./2-path

# Verify /action was added to PATH
echo $PATH
```
Important Notes:

The script must be sourced (not executed) to modify the current shell's environment

Using export ensures the change is passed to child processes

The $PATH variable expansion ensures existing paths are preserved

/action is added to the end, making it the last directory searched

Example Output:

```bash
# Before sourcing:
/home/user/bin:/usr/local/bin:/usr/bin:/bin

# After sourcing:
/home/user/bin:/usr/local/bin:/usr/bin:/bin:/action
```

### Task 3: If the path be beautiful, let us not ask where it leads
#### File: 3-paths
Objective: Create a script that counts the number of directories in the PATH environment variable.

Script Content:

```bash
#!/bin/bash
echo $PATH | tr ':' '\n' | wc -l
```
Description:
This script counts how many directories are listed in the PATH variable by converting colons to newlines and counting the resulting lines. Each directory in PATH is separated by a colon (:), so this transformation allows us to count them easily.

Usage:

```bash
# Make the script executable
chmod +x 3-paths

# Run the script
./3-paths

# Or source it (both work)
. ./3-paths
```
How it works:

echo $PATH - Outputs the current PATH variable

tr ':' '\n' - Replaces all colons with newlines, putting each directory on its own line

wc -l - Counts the number of lines (each line = one directory)

Example Output:

```bash
# If PATH=/bin:/usr/bin:/usr/local/bin
./3-paths
3

# If PATH has 11 directories (as in the example)
./3-paths
11
```
Note: The script counts all directory entries in PATH, including empty ones if there are consecutive colons or trailing colons.

### Task 4: Global variables
#### File: 4-global_variables
Objective: Create a script that lists all environment variables.

Script Content:

```bash
#!/bin/bash
printenv
```
Description:
This script displays all environment variables available in the current shell session. Environment variables are global variables that are inherited by child processes and define the operating environment for programs.

Usage:

```bash
# Make the script executable
chmod +x 4-global_variables

# Run the script (can also be sourced)
./4-global_variables

# Or source it as shown in the example
source ./4-global_variables
```
How it works:

printenv is a command that prints all environment variables in the format VARIABLE=value

Environment variables include system-wide settings and user-specific configurations

Common environment variables shown: USER, HOME, PATH, SHELL, PWD, etc.

Example Output:

```text
USER=amir
HOME=/home/amir
PATH=/usr/local/bin:/usr/bin:/bin
SHELL=/bin/bash
LANG=en_US.UTF-8
PWD=/home/amir/projects
... (many more)
```
Note: The script should be sourced (source or .) to ensure it runs in the current shell context, though executing it (./4-global_variables) also works since printenv doesn't depend on shell-specific features.

### Task 5: Local variables
#### File: 5-local_variables
Objective: Create a script that lists all local variables, environment variables, and shell functions.

Script Content:

```bash
#!/bin/bash
set
```
Description:
This script uses the set command without arguments to display all shell variables (both local and environment) along with all shell function definitions. The output provides a complete view of the shell's current state.

Usage:

```bash
# Make the script executable
chmod +x 5-local_variables

# Run the script (or source it as shown in example)
./5-local_variables

# Or source it
. ./5-local_variables
```
How it works:

The set command when used without options displays:

Local variables: Variables defined in current shell session

Environment variables: Variables exported to child processes

Shell functions: All defined functions in the current shell

Output format shows variables in a way that can be reused to recreate the shell environment

Example Output (first few lines):

```text
BASH=/bin/bash
BASHOPTS=checkwinsize:cmdhist:complete_fullquote:expand_aliases:extglob:extquote:force_fignore:histappend:interactive_comments:progcomp:promptvars:sourcepath
BASH_ALIASES=()
BASH_ARGC=()
BASH_ARGV=()
BASH_CMDS=()
BASH_COMPLETION_COMPAT_DIR=/etc/bash_completion.d
BASH_LINENO=()
BASH_REMATCH=()
BASH_SOURCE=()
BASH_VERSINFO=([0]="4" [1]="3" [2]="46" [3]="1" [4]="release" [5]="x86_64-pc-linux-gnu")
BASH_VERSION='4.3.46(1)-release'
... (many more lines)
```
Note: The output will be extensive (typically 100+ lines) as it includes all shell internals. The script should be sourced (using . or source) to ensure it runs in the current shell context, though executing it also works.

### Task 6: Local variable
#### File: 6-create_local_variable
Objective: Create a new local variable named BEST with value School.

Script Content:

```bash
#!/bin/bash
BEST=School
```
Description: Creates a local shell variable BEST with value School. Local variables exist only in the current shell session.

Usage:

```bash
chmod +x 6-create_local_variable
source ./6-create_local_variable
echo $BEST  # Outputs: School
```
Note: Use source to run in current shell. The variable won't be available to child processes.

### Task 7: Global variable
#### File: 7-create_global_variable
Objective: Create a new global (environment) variable named BEST with value School.

Script Content:

```bash
#!/bin/bash
export BEST=School
```
Description: Creates and exports an environment variable BEST with value School. Environment variables are available to the current shell and all child processes.

Usage:

```bash
chmod +x 7-create_global_variable
source ./7-create_global_variable
echo $BEST           # Outputs: School
printenv | grep BEST # Shows: BEST=School
```
Note: Use export to make variables global. Unlike local variables, these are inherited by child processes.

### Task 8: Every addition to true knowledge is an addition to human power
#### File: 8-true_knowledge
Objective: Print the result of adding 128 to the value stored in environment variable TRUEKNOWLEDGE.

Script Content:

```bash
#!/bin/bash
echo $((128 + TRUEKNOWLEDGE))
```
Description: Performs arithmetic addition using bash's arithmetic expansion $(( )). Adds 128 to the value of the TRUEKNOWLEDGE environment variable.

Usage:

```bash
chmod +x 8-true_knowledge
export TRUEKNOWLEDGE=1209
./8-true_knowledge  # Outputs: 1337
```
Example:

```bash
export TRUEKNOWLEDGE=1209
./8-true_knowledge | cat -e  # Outputs: 1337$
```
Note: Uses bash arithmetic expansion $(( )) for calculation. The TRUEKNOWLEDGE variable must be set in the environment before running.

### Task 9: Divide and rule
#### File: 9-divide_and_rule
Objective: Print the result of POWER divided by DIVIDE (both environment variables).

Script Content:

```bash
#!/bin/bash
echo $((POWER / DIVIDE))
```
Description: Performs integer division using bash arithmetic expansion. Divides the value of POWER by DIVIDE.

Usage:

```bash
chmod +x 9-divide_and_rule
export POWER=42784
export DIVIDE=32
./9-divide_and_rule  # Outputs: 1337
```
Note: Uses integer division (truncates decimal). Both POWER and DIVIDE must be set as environment variables.

### Task 10: Love is anterior to life, posterior to death, initial of creation, and the exponent of breath
#### File: 10-love_exponent_breath
Objective: Display the result of BREATH to the power LOVE (both environment variables).

Script Content:

```bash
#!/bin/bash
echo $((BREATH ** LOVE))
```
Description: Performs exponentiation using bash's ** operator within arithmetic expansion.

Usage:

```bash
chmod +x 10-love_exponent_breath
export BREATH=4
export LOVE=3
./10-love_exponent_breath  # Outputs: 64
```
Note: Uses ** for exponentiation (not ^ which is XOR). Both variables must be set in the environment.

### Task 11: There are 10 types of people in the world -- Those who understand binary, and those who don't
#### File: 11-binary_to_decimal
Objective: Convert a binary number (from environment variable BINARY) to decimal.

Script Content:

```bash
#!/bin/bash
echo $((2#$BINARY))
```
Description: Uses bash arithmetic expansion with base notation 2# to interpret the binary string as a base-2 number and convert it to decimal.

Usage:

```bash
chmod +x 11-binary_to_decimal
export BINARY=10100111001
./11-binary_to_decimal  # Outputs: 1337
```
Note: 2# prefix tells bash to interpret the following digits as binary. Only contains 0s and 1s.

### Task 12: Combination
#### File: 12-combinations
Objective: Print all possible two-letter combinations (a-z) except oo, one per line, alphabetically sorted.

Script Content:

```bash
#!/bin/bash
echo {a..z}{a..z} | tr ' ' '\n' | grep -v oo
```
Description: Uses brace expansion to generate all combinations, converts to one per line, and excludes oo.

Usage:

```bash
chmod +x 12-combinations
./12-combinations
./12-combinations | wc -l  # Outputs: 675
```
Output Details:

Total combinations: 675 (26×26 - 1)
First: aa, Last: zz
Missing: oo
Alphabetical order

Note: Script must be ≤ 64 characters (this solution: 53 chars).

### Task 13: Floats
#### File: 13-print_float
Objective: Print the number from environment variable NUM with exactly two decimal places.

Script Content:

```bash
#!/bin/bash
printf "%.2f\n" $NUM
```
Description: Uses printf to format the number with two decimal places, rounding as needed.

Usage:

```bash
chmod +x 13-print_float
export NUM=3.14159265359
./13-print_float  # Outputs: 3.14
```
Note: Uses printf (allowed) not bc, sed, or awk (not allowed). Automatically rounds to two decimal places.


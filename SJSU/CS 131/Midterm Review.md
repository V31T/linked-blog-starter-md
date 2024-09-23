## Lecture 1 - Intro to Unix

- Architecture of operating system and how does shell, libraries and apps fit
	- divided into layers -> kernel, shell, libraries, applications
		- kernel: the core that interactes directly with hardware
		- shell: interface between the user and the kernel
		- libraries: collection of pre-written code that applicaitons can use to perform common tasks
		- applicaitons: software programs that users interact with, running ontop of the OS
	- together, shells help users interact with the system, libraries support code reuse and OS communication, and applications rely on both to fuinction efficiently within the OS environment
- Distinction between VPN vs IBM server
	- The VPN is used to access the private network that the IBM server is located on. 
	- The IBM server is on the network and we need to log in to the server through a SSH
- What is **ssh** used for?
	- Ans: ssh stands for Secure SHell. it allows computers to communicate securely over over an unsecured network. 
	- Notes: it is an interface for running other applications
- Why are we using **Git**? What do we mean by version control
	- we are using git because it is one of the most common version control systems
	- Version control is a system that records changes to a file or set of files over time so that you can recall specific versions later
- **What is the main function of version controls systems like GIT?**
	- To compress files for storage
	- to encrypt sensitive data
	- ==to record changes to files over time ==
	- to optimize system performance
	- none of the above
- **What is the command to change your password on the IBM server**
	- ==passwd==
	- change pwd
	- update_credentials
	- .bashrc
	- none of the above
- **explain the difference between absolute and relative pathnames in the Linux file system. provide an example of each**
	- absolute pathnames refer to file paths that start at the root directory and contain the full path to the file/directory. On the other hand, relative pathnames refer to file paths relative to the current working directory
		- absolute: /users/henrypham/thisfile
		- relative:  \*assuming\* we are in /users/henrypham already
			- -> /thisfile

## Lecture 2 - Command line basics 

- What is shell and how does it relate to the operating system kernel
	- the shell is a user interface that allows you to interact with the OS, primarily through text-based commands. It interprets commadns and communicates them to the kernel, which manages hardware and system resources. The shell acts as an intermediary between the user and the kernel
- what is a shell script
	- a shell script is a text file containing a series of commands for the shell to execute. it automates repetitive tasks by running multiple commands sequentially. shell scripts are written ins hell languages like bash or Zsh
- how do you run commands on the server
	- you can run commands on a server via SSH (secure shell) by connecting to the server using a terminal or command-line tool. once logged in, you can execute commands as if you were you using the terminal on the server itself
- what is a file in terms of UNIX?
	- in UNIX, a file is a seuqence of bytes that can represent text, programs or data. Files are used for storage, and in UNIX, everything (e.g directories, devices, etc.) is treated as a FILE
- What information can be found in inode?
	- an inode contains metadata about a file, such as: 
		- file size, Ownership (user and group), file permissions, timestamps (creation, modification), number of hard links, location of data blocks on the disk
- How do you use file descriptors?
	- file descriptors are integers that represent open files in a process.
		- 0: standard input (stdin)
		- 1: standard output (stdout)
		- 2: standard error (stderr)
	- you use them to read, write, or handle input/output for files or commands
- How can you redirect descriptors?
	- you can use redirection operators to direct input/output streams:
		- `>`: Redirects standard output to a file (`command > file.txt`)
		- `<`: Redirects standard input from a file (`command < file.txt`)
		- `2>`: Redirects standard error (`command 2> error.log`)
		- `&>`: Redirects both standard output and standard error.
- Know how you can navigate around directory structure
	- Use these basic commands to navigate:
		- `pwd`: Print current working directory
		- `cd`: Change directory (`cd /path/to/directory`)
		- `ls`: List contents of a directory (`ls -l` for details)
- What is a root directory and what does it include?
	- The **root directory** (`/`) is the topmost directory in UNIX. It contains all system directories (e.g., `/bin`, `/etc`, `/home`, `/usr`). Everything in the file system stems from root.
- Are there directories above the root?
	- No, the root directory is the highest level in the file system. there are no directories above `/`
- Distinguish between relative and absolute path
	- an absolute path starts from the root directory and gives the full location
	- relative path is relative to the current working directory
- Understand how to use options in a command
	- Many UNIX commands accept **options** or flags (e.g., `-l`, `-a`) that modify their behavior. Options are usually preceded by a `-` or `--` and can be combined (`ls -la` for a detailed list of all files).
- Understand how to read details of files on your directory
	- Use `ls -l` to see detailed file info like:
		- permissions, numbers of links, owner, file size, last modified date, file name
- Permission - how to change and interpret permission
	- file permission are shown in `rwx` format for the owner, group, and others:
		- `r`: read
		- `w`: write
		- `x`: execute
	- change permissions using `chmod`:
		- `chmod 755 file.txt` (owner can read/write/execute, others can read/execute)
- Understand how to use wildtype. Note there are many wildtypes and lecture -> just show a small subset. I may provide more wildcards on exam and you should understand how to interpret
	- Wildcards are symbols used for pattern matching in file names:
		- `*`: Matches any number of characters (`*.txt` matches all `.txt` files)
		- `?`: Matches exactly one character (`file?.txt` matches `file1.txt` but not `file12.txt`)
		- `[abc]`: Matches any one character in the brackets (`file[12].txt` matches `file1.txt` or `file2.txt`)
- Understand how to use manual to change behavior of command. That is if I gave you a command line command and the manual could you figure out what it does
	- Use the `man` command to read a manual page for a command. For example, `man ls` shows the options for `ls`. Reading the manual helps you understand how to modify a command’s behavior.
- **Which wildcard character mathces any single character in Linux?**
	- ==?==
	- *
	- \ #
	- @
- **What is the purpose of the `man` command in Linux?**
	- To manage the system processes 
	- ==To display the manual pages for commands==
	- To monitor system resources
	- To manipulate text files
- **Which of the following is a correct way to redirect both stdout and stderr to a file?**
	- command > file 2 > 1
	- command 2 > &1 > file
	- command > file & 2 > file
	- ==command &> file==
		- **Why?** `&` is a shortcut for `1 & 2`
- **Describe the correct process for exiting vi without saving changes. Why might students struggle with this and what are the protentional consequences of using the wrong command?**
	- to not save any changes the correct vi command is `:q` or `:q!` to force quit. Students may struggle with this because it is a command rather than an exit button on a GUI. a potential consequence of using the wrong command is either saving or not saving your file on accident.

## Lecture 3 - vi

- Understand the basic of using vi
	-  `vi` is a text editor available on most Unix systems. It has two primary modes:
	    1. **Command mode**: For navigation and issuing commands (this is the default mode).
	    2. **Insert mode**: For inserting text into the document (`i` to enter Insert mode, `Esc` to return to Command mode).
	- Basic commands:
	    - `i`: Insert text
	    - `Esc`: Return to command mode
	    - `:w`: Save (write)
	    - `:q`: Quit
- How do you do a quick search of your file when in vi?
	- In **Command mode**, type `/` followed by the search term, then press `Enter`. For example, `/word` will search for "word" in the document. Use `n` to go to the next occurrence and `N` for the previous one.
- Can you do a search and replace in your file quickly?
	- yes: `:%s/oldword/newword/g`
		- this replaces all occurences of `oldword` with `newword`. the `%` applies the substitution to the entire file, and the `g` ensures global replacement within each line
- how do you remove newlines when importing work docx?
	- to remove newlines you can use the following: `:%s/\n//g`
		- this removes all newlines from the document, alternatively you can use a text-processing command like `tr`:
			- `tr -d '\n\' < input.docx > output.txt` 
- How does pip `|` work?
	- the pip is used to pass the output of one command as the input to another command.
- How does echo work and why would you want to use it?
	- echo is used to display text or output values of variables in the terminal, its useful for: printing messages, displaying results of commands, debugging scritps
- How do you use grep to pull out a word in a file? Can you do this on a directory?
	- to search for a word in a file: 
		- `grep "word" filename.txt`
	- to search in all files within a directory (and subdirectories) use the `-r` (recursive) option:
		- `grep =r "word" /path/to/directory`
- How do you customize your vi editor?
	- edit `.vimrc`
- **What does the command `dd` do in vi?**
	- Duplicate the current line
	- Delete the current word
	- ==Delete the current line==
	- Move down one line
- How do you quit vi without saving in one command?
	- :wq
	- :q
	- ==:q!==
	- esc

## Lecture 4 - regex 

- we didnt go over regex. this lecture we only look at .vimrc and how to customize it
- we will revist regex in a future class

## Lecture 5 - intro to shell

- What do you need to include in your shell script to be able to run the script?
	- must include the shebang
		- `#!/bin/bash`
	- tells the system which interpreter to use
	- to make script executable run `chmod +x script.sh`
- What if you wanted to use vi to write a python program or a javascript? How would it differ from writing a shell script?
	- When using `vi` for Python or JavaScript:
		- **Shebang**: Python scripts typically include `#!/usr/bin/python3`, but it’s not required if you run them with `python3 script.py`. JavaScript doesn’t need a shebang unless you're using Node.js.
		- **Syntax**: Python and JavaScript have different syntax compared to Bash (e.g., use of indentation for Python, curly braces for JavaScript). You’ll need to follow the language's syntax rules.
		- **Execution**: For Python, you'd run `python3 script.py`. For JavaScript (with Node.js), run `node script.js`.
- How do you pass in arguments when running your scripts?
	- by listing them after the scriptname
		- `./scripts.sh arg1 arg2`
	- in the script you can access these arguments using $1 $2 $3 etx. $0 represents the script name
- Understand the different variables and where they are used
	- **Local variables**: Defined within the script or function and only available in that context.
	- **Environment variables**: Defined in the shell or globally, accessible to any child processes or scripts.
	- **Positional parameters**: Arguments passed to the script (`$1`, `$2`, etc.).
- How do you define local variables?
	- just assign the value
		- `localvar="Hello World"`
- What is a shell session?
	- a shell session is an interactive instance of a shell wher you can execute commands, run scripts, and manage processes. a new session starts each time you open a terminal window or connect via SSH
- How do you export variables so that they are included in your shell session?
	- use `export` to make variables available to other processes or child shells
		- `export MY_VAR="HELLO"`
	- once exported, the variable MY_VAR will be accessible in any child processes or scipts run during that session
- What is an exit code?
	- An **exit code** (also known as a return status) is a numerical value returned by a command or script upon completion. By convention:
		- `0`: Indicates success.
		- Non-zero values (e.g., `1`, `2`, etc.): Indicate errors or failures. You can check the exit code of the last executed command using `$?`.
- If your script fails, how can you figure out why it fails?
	- To debug a script:
		- Check the **exit code** with `$?`.
		- Use **echo** or **set -x** to print out the commands being executed and their results.
		- Use **error messages** displayed by the shell.
		- Ensure that variables and arguments are correctly passed, and permissions are properly set.
- **Which command will display the value of a specific environment variable named `MY_VAR`?**
	- print($MY_VAR)
	- echo "MY_VAR"
	- call $MY_VAR
	- ==echo $MY_VAR==

## Lecture 6 - environment variables

- What are environment files?
	- **Environment files** are configuration files that set environment variables and control the behavior of your shell session. These files are read when a shell session starts, and they define settings such as paths, user preferences, aliases, and more.
- what do these files contain?
	- **Environment files** typically contain:
		- **Environment variables** (e.g., `$PATH`, `$HOME`, `$USER`).
		- **Aliases** to simplify commands (e.g., `alias ll='ls -la'`).
		- **Shell options** and settings.
		- **Custom functions** or scripts.
		- **Startup commands** to be executed when the shell session begins.
- How does the Linux system use these files?
	-  **`~/.bashrc`**: A user-specific configuration file for interactive non-login shells.
	- **`~/.bash_profile`** or **`~/.profile`**: Configuration files for login shells (run once during login).
	- **`/etc/profile`** and **`/etc/bash.bashrc`**: System-wide environment files that apply to all users.
- How would you customize your bash session?
	- Linux uses these environment files to:
		- **Set up the shell environment** when a user logs in or starts a shell session.
		- Define **global settings** for all users (via `/etc/profile` or `/etc/environment`).
		- Configure **user-specific settings** (via `~/.bashrc` or `~/.profile`).
		- The system reads these files and applies their settings (e.g., environment variables like `$PATH` that define where to find executables).
- **How can you make changes to environment variables permanent for a specific user?**
	- Use the `permanent` flag with the export command
	- edit the /etc/environment file
	- ==Modify the .bashrc or .bash_profile in the user's home directory==
	- Changes to environment variables are always permanent
- **What does the following command do? export PATH=$PATH:/new/directory**
	- Replaces the current PATH with /new/directory
	- ==Adds /new/directory to the end of PATH==
	- Removes /new/directory from PATH
	- Delete $PATH and /new/directory from the root directory

## Lecture 7 - if-then

- if, if-then, if-then-else
	- **If**: Used to test a condition. If the condition is true, the commands within the block are executed.
	- **If-Then**: A basic conditional structure where if the condition is true, a command or set of commands is executed.
	- **If-Then-Else**: Adds an alternative (else) block, where commands will execute if the initial condition is false.
```bash
if [ condition ]; then
  # Commands if condition is true
else
  # Commands if condition is false
fi

```
- What's the differenence between using if statements to run command line versus conditions?
	- command line execution: in shell scripts, an `if` statement can check the exit status of a command
		```bash
if ls /path/to/directory; then
  echo "Directory exists."
fi
		```
		- the `ls` command runs and the `if` statement checks if it was successful (exit code 0)
	- Conditions:  The `if` statement can also test conditions like strings or numbers:
```bash
if [ "$var" -eq 10 ]; then
  echo "Var equals 10."
fi
```
- What is the script looking for when it runs a if then statement?
	- The script is evaluating the **condition** or the **exit status** of a command:
	- **Condition**: If it’s true, the commands inside the `if` block are executed.
	- **Exit status**: If the command's exit status is `0` (successful), the `then` block runs. If it’s a non-zero exit status (failure), the block is skipped.
- When using an elif statement, how are each block of command executed? Do they all get executed?
	- Only **one block** of commands is executed.
		- The script evaluates each condition in sequence. If one condition evaluates as true, the corresponding block is executed, and the rest are skipped.
		- If none of the conditions are true, the final `else` block (if present) will be executed.
	```bash
	if [ condition1 ]; then
	  # Block 1
	elif [ condition2 ]; then
	  # Block 2
	else
	  # Block 3
	fi
	```
	-  here only one of the blocks will run, depending on the first true condition
- How would you write a if statement to evaluate a condition?
	- an `if` statement evaluates a condition like this:
	```bash
	if [ "$var" -gt 5 ]; then
	  echo "Var is greater than 5."
	fi
	```
	- this checks if `var` is greater than 5 and prints a message if true.
- If given an operator for condition, predict what you think the output of the if statements would be.
	- String comparison:
		-  '=' checks if two strings are equal
		- `!=` checks if two strings are not equal.
	```bash
	if [ "$str1" = "hello" ]; then
	  echo "Strings match."
	fi
	```
	- **Numeric comparison**:
		- `-eq`: Equal to.
		- `-ne`: Not equal to.
		- `-gt`: Greater than.
		- `-lt`: Less than.
	```bash
	if [ "$num" -gt 10 ]; then
	  echo "Number is greater than 10."
	else
	  echo "Number is 10 or less."
	fi
	```
	- predicting output: if you know the value of the variable, you can predict the output;
		- if `num=12`, the output will be `"Number is greater than 10."`
		- If `num=8`, the output will be `"Number is 10 or less"`
- **What is the primary purpose of creating a shell script?**
	- To compile high-level programming languages
	- to create a graphical user interface
	- to replace the operating system's kernel
	- ==to store commands in a file for use with logic and control structures==
- **What is the correct file extension for a shell script?**
	- .exe
	- .bash
	- ==.sh==
	- .cmd
- **Write a basic shell script that accepts two command-line arguments (a first name and a last name) and prints a greeting using these arguments. Explain each line of your script, including the shebang.**
```bash
#!/bin/bash
# ^ the shebang to specify the correct shell to use for this shell script

# store 1st positional argument into variable `first`
first=$1 
# store 2nd positional argument into variable `second`
second=$2

# print to stdout using echo, uses inline variables
echo "Hello $first $second"
```







